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
Notes:
Even though, the overall precision for Mean Centroid and Naïve Bayes is the same as that if my final perceptron classifier, it is important to keep it mind that the individual emotion recognition was done better by the perceptron, for example of you look at “Sadness”. That is why it was chosen over the rest. Individual results for all classifiers are saved in the notebook.

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

