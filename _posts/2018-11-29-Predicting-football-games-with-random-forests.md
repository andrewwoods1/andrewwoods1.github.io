---
layout: post
title: Predicting football matches with Random Forests and Platt scaling
---

Random forests have been shown to be an incredibly powerful means of classification. However for a problem such as football match result prediction, we're less interested in classification and moreso in the uncertainties involved. The following post gives details on the random forest model I have been working on of late, and how Platt scaling corrects the uncalibrated probabilities calculated by the classifier. 
For this model I've used fivethirtyeight's football dataset, specifically for the English premier league. I've combined this with other match data found on football-data.co.uk.

The features of the model are mostly made up from expected goals data taken from fivethirtyeight's dataset. This data gives an inidcation of a team's defensive or offensive performance in a game and has been shown to have greater predictive power than the actual goals scored in a game.
Feature engineering took the approach of trying to marry together both the short term *form* of a team and also the underlying longer term *talent* of the team. This was done by coming up with two versions of each metric used as a feature; a version calculated over the short term and the same for the longer term. 
The final list of features came to include metrics based on xG for and against, broken down by home and away, as well as xG ratio, a known good indicator of future team performance (more on xG ratio [here](http://11tegen11.net/2016/02/21/predicting-league-football-using-xg-and-more/)) 
Finally, k-means clustering was used on each distinct set of values of *xG for p.g* and *xG against p.g*. By clustering these values, we could assign them labels, and using those labels, look at how each team fared against opposition corresponding to each cluster. 
An example of such a clustering is below, for team's away performances over the previous ten game window. There are no distinct clusters here, however it is useful to stratify the teams' performances.
![Img1](/images/Rplot01.png "clustering")

The preprocessing was all done in R, simply for the use of the dplyr library. The model itself was created in python, as below
 
```python
from sklearn.ensemble import RandomForestClassifier
clf = RandomForestClassifier(n_jobs=-1,
                             random_state=123,
                             n_estimators=1000,
                             min_samples_split = 3,
                             bootstrap = True,
                             class_weight= 'balanced'
                             )

```
A common issue with posterior probabilities produced by classifiers such as a random forest is their calibration, or lack thereof. I common method of rectifying this is known as Platt scaling, which uses the sigmoid function to map the uncalibrated probabilities back to more accurate ones. See [here](https://en.wikipedia.org/wiki/Platt_scaling), [here](https://www.cs.cornell.edu/~caruana/niculescu.scldbst.crc.rev4.pdf) and [here](https://people.dsv.su.se/~henke/papers/bostrom08b.pdf) for more explanation.
Luckily, this method is built in to sci kit learn.

```python

# Fit platt's scaling on validation set
# the method argument is given 'sigmoid' to say Platt is to be used as scaling method
calib = CalibratedClassifierCV(base_estimator=clf, method = 'sigmoid', cv = 4)
calib.fit(x_train, y_train)
```
One of the drawbacks of Platt scaling is that it requires a seperate validation dataset to train the model which maps the uncalibrated probabilities to calibrated ones. Otherwise, overfitting is common. This is an issue when dealing with a relatively small amount of data as is the case here. To get around this, cross-validation can be used whereby the random forest is trained on k-1 of our k folds, with scaling being trained on the remaining fold. This is repeated k times, with a different fold being used for Platt scaling each time, thus, not losing any data from the random forest training set.

At this point, the model is complete, and hopefully with well calibrated and accurate probability estimates. A popular means of evaluating football predictions is the Ranked Probability Score, or RPS. This metric takes into account the *ranked* nature of the outcomes, i.e. Home Win >> Draw >> Away Win. A low RPS means accurate probabilities, so the lower the better.

The penal.t/y website has a [nice explainer on RPS](http://pena.lt/y/2013/03/21/how-accurate-are-the-ei-football-predictions/), and some R code which can be used to implement it is available [here](https://opisthokonta.net/?p=1333).

I've translated the code there to the python below.
```python
def RPS(pred,obs):
    ncat = pred.shape[1]
    npred = pred.shape[0]
    print 'Number of outcomes: ', ncat
    print 'Number of predictions: ', npred
    rps = np.zeros(npred)
    for i in range(npred):
        obsvec = np.zeros(ncat)
        obsvec[obs[i]] = 1
        cumulative = 0
        for j in range(ncat):
            cumulative = cumulative + (np.sum(pred[i, :j]) - np.sum(obsvec[:j]))**2
        rps[i] = cumulative
    rps = np.divide(rps,(ncat - 1))
    return rps

```

The blog [Cognitive Football](https://cognitivefootball.wordpress.com/rps-17-18/) runs a football prediction league each season, to judge the accuracy of various models. This can be used to judge the random forest model's accuracy for the last 270 games of the 17/18 Premier League season.
To do this, the RPS of my model's predictions over that period can be calculated, and this works out to be .1962, meaning my model would have came in position 18 in the league table. This RPS is compared to .1877 and .1844 for fivethirtyeight and the probabilities implied by the betting market.

As a starting point for the random forest model, the performance is relatively good and should be improved upon in the coming months.
