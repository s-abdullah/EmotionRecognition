# Emotion Recognition

This was a course assignment in which speech segments extracted from the [Emotional Prosody Speech and Transcripts](https://catalog.ldc.upenn.edu/LDC2002S28) were analyzed and used to train various classifiers. These classifiers were then analyzed in terms on performance.

## Feature Analysis
ParselMouth was used for extraction of min, max and average Pitch and intensity. These were then normalized using two techniques, Z-Score and Neutral-Normalisation. Normalization was needed since each speaker naturally has a different pitch range and other voice qualities like intensity. The mean and standard deviation of the features were then plotted and analysed.

### Plots of the Features

#### Intensity Features
The Normal Intensities that were extracted gave these plots:

![alt text][notI]

The Z-Score Normalised Intensities that were extracted gave these plots:

![alt text][zI]


The Neutral Normalised Intensities that were extracted gave these plots:

![alt text][neuI]

#### Pitch Features
The Normal Pitch's that were extracted gave these plots:

![alt text][notP]


The Z-Score Normalised Pitch's that were extracted gave these plots:

![alt text][zP]


The Neutral Normalised Pitch's that were extracted gave these plots:

![alt text][neuP]

### Discussion
* The most apparent thing that can be noticed by looked at the Intensity based features is the
importance of normalization. At a cursory glance, all of them seem to have pretty much the
similar. but after normalization we can see how much they vary. If we look more closely, then
the Z-Score normalizations give a wider more apparent variation than the Neutral utterance-
based normalizations. Another advantage of the Z-score is that, unlike the neutral utterance-
based normalizations, it will not give the zero to the average features for the neutral utterances.
The Z-score normalizations give more variation hence that is what I looked at more and it was
also the normalization that I used for the classification task.

* One interesting thing to note is that, only the average Z-Score normalized pitch has a noticeably
low standard deviation. Otherwise, all the emotions for all the features have a fair it of standard
deviation. This leads me to believe that the definition of Neutral Emotion is more universal as 7
different actors over a bunch of utterances had similar average pitch.

* One of the most interesting aspects of the data is how Panic, Elation and Hot-Anger have the
highest average pitch and intensity values for both unnormalized and normalized, even though
are very different emotions with different position in the arousal-valence graph. But if we look
deeper into the feature of these three emotions, they become even more interesting. One may
expect Hot-Anger to have the highest Intensity in all three Intensity based features but it
doesn’t. Elation has the highest average intensity and also a higher minimum intensity, both
normalized and unnormalized. But if we look at the z-score normalized minimum intensity; Hot-
anger stands out with the lowest score by far. This shows that Hot-Anger had the highest
variation between its Intensity values while Elation with a higher minimum Intensity did not.
This resulted in a higher average Intensity for Elation over Hot-Anger, which was very surprising.
Though it makes intuitive sense for panic to have the highest average pitch, which shows in the
data.

* It is also very interesting to note that Boredom and Neutral both have very similar pitch and
intensity feature, both unnormalized and normalized. They both have relatively low standard
deviation for average pitch.

* The average intensity of sadness, anxiety and neutral were the lowest, both unnormalized and
normalized. This makes sense because when you’re anxious or sad, you may have less intensity
in your voice and for neutral since you’re not "emotionally" invested in what you are talking
about therefore it might not have the same intensity. Along with anxiety, sadness and neutral,
shame also has the lowest normalized pitch. So, it is really interesting to see that shame has a
lower pitch but not a low intensity.

* It was also observed very different emotions such as Happy and Despair had similar Z-score
normalized average values particularly for average intensity.

## Classification
A set of acoustic-prosodic features were extracted using the openSMILE toolkit. They were normalized using the same techinques as stated above. These were then used in a one-speaker-out cross validation to predict the emotion categories. For the openSMILE the "The INTERSPEECH 2009 Emotion Challenge feature set" was extracted.

Classifier was trained using 4 Hidden layer Perceptron for 500 iterations and stochastic gradient descent
with hyperbolic tangent as activation and adaptive learning rate.

The overall result of the Perceptron was:

![alt text][overall]

The average over all the speaker was:

![alt text][all7]

And then the one-speaker-out cross validation result was:

![alt text][ind]

### Additional Experiments
Additionally, different Machine Learning algorithms were also tried to see their performance:

* Naive Bayes Gaussian 

![alt text][nb]

* Centroid

![alt text][cen]

* Ridge Regression

![alt text][ridge]

#### Notes
Even though, the overall precision for Mean Centroid and Naïve Bayes is the same as that if my final perceptron classifier, it is important to keep it mind that the individual emotion recognition was done better by the perceptron, for example of you look at “Sadness”. That is why it was chosen over the rest. Individual results for all classifiers are saved in the notebook.

### Analysis
#### Classes that were easiest to Pick

* *Hot-Anger*: As discussed in the earlier section, this had the highest average intensity and pitch along with Panic and Elation but it differentiated itself from these two by having the highest variation between the minimum and maximum as well. So, if it was apparent in 6 features, then it will be apparent in 384 features as well. Also, Hot-Anger is a really specific emotion and hence it would be easier to act out and due to its specificity, have less variation in the utterances. This would lead to easy classification.

* *Elation*: With its high average intensity and pitch that set it apart from most emotions in the feature analysis. It was different from Hot-Anger due its less variation, and it can be set apart from panic because its average feature values were higher. This was just the 6 features in the previous section, an additional 384 would help it differentiate even more.

* *Boredom*: This also had a high F1 score. I believe since everyone knows boredom and had experienced it, therefore there is a well-accepted definition of boredom. This leads me to believe there was less variation in the utterance for this emotion by the actors and hence it would be easily classified.

Boredom along with Hot-Anger and Elation are very apparent emotions that are easy to sense and see and act. That is why I believe they were easier to pick

#### Classes that were most difficult to Pick

* *Anxiety*: I believe this is a hard emotion to classify as person as well. Anxiety manifests in different ways with different people and hence everyone would have their own definition. It also a very subtle emotion that can be missed if a person doesn’t pay much attention. I believe that is why the classifier was not able to pick is effectively, because different actors would have acted it out differently, further more anxiety has many physical traits such as pacing, deep breathing that might not be captured by the data.

* *Pride*: Again, pride can manifest in different ways across different people and I believe it is different across genders as well. Also, there is no set definition on how to act with pride so every actor would have been doing his/her own version which would have led to large variation hence the classifier performed badly.

#### Further Improvements

I tried 5 different classifiers, three of which are stated in the previous section under additional experiments. I noticed that the average scores can be misleading because in many of the experiments some emotions such as “Sadness” weren’t being classified at all. SVM was the worst performing and wasn’t included in the report.

Firstly, I would like to experiment with different feature sets. Secondly it would be helpful to perform unsupervised learning and see which classes are the most closest to each other so that specific features to differentiate between them could be extracted. I believe experimenting with deep learning techniques (CNN, LSTM) would be the best way forward since the Perceptron gave the best and most evenly distributed results. I would also have liked to made a custom Perceptron with different activation functions across the layers and the inclusion of dropout to deal with overfitting (sklearn does not have these options). There also a big variation between speaker results, with 27% F1 being the highest for cl_001 and 15% F1 being the lowest for cc_001. Gathering more data and training on larger dataset would also be quite helpful.
 
Lastly, I would like to different preprocessing techniques, like sieving out outliers and trying different normalization techniques.

[notI]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/intensity.gif 
[neuI]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/zintensity.gif 
[zI]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/NeutralNormalisedintensity.gif 

[notP]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/pitch.gif 
[neuP]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/zpitch.gif 
[zP]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/NeutralNormalisedpitch.gif 

[ind]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/individual.gif 

[cen]: https://github.com/s-abdullah/EmotionRecognition/blob/master/Images/centroid.png 
[nb]: https://github.com/s-abdullah/EmotionRecognition/blob/master/Images/nb.png 
[ridge]: https://github.com/s-abdullah/EmotionRecognition/blob/master/Images/ridge.png 
[all7]: https://github.com/s-abdullah/EmotionRecognition/blob/master/Images/all7.png 
[overall]: https://github.com/s-abdullah/EmotionRecognition/blob/master/Images/overall.png 

