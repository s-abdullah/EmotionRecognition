# Emotion Recognition

This was a course assignment in which speech segments extracted from the [Emotional Prosody Speech and Transcripts](https://catalog.ldc.upenn.edu/LDC2002S28) were analyzed and used to train various classifiers. These classifiers were then analyzed in terms on performance.

## Feature Analysis
ParselMouth was used for extraction of min, max and average Pitch and intensity. These were then normalized using two techniques, Z-Score and Neutral-Normalisation. Normalization was needed since each speaker naturally has a different pitch range and other voice qualities like intensity. The mean and standard deviation of the features were then plotted and analysed.

### Plots of the Features
The Normal Intensities that were extracted gave these plots:

![alt text][notI]

The Z-Score Normalised Intensities that were extracted gave these plots:

![alt text][zI]


The Neutral Normalised Intensities that were extracted gave these plots:

![alt text][neuI]


The Normal Pitch's that were extracted gave these plots:

![alt text][notP]


The Z-Score Normalised Pitch's that were extracted gave these plots:

![alt text][zP]


The Neutral Normalised Pitch's that were extracted gave these plots:

![alt text][neuP]






[notI]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/intensity.gif 
[neuI]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/zintensity.gif 
[zI]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/NeutralNormalisedintensity.gif 

[notP]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/pitch.gif 
[neuP]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/zpitch.gif 
[zP]: https://github.com/s-abdullah/EmotionRecognition/blob/master/gifs/NeutralNormalisedpitch.gif 