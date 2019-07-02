# Emotion Recognition

This was a course assignment in which speech segments extracted from the [Emotional Prosody Speech and Transcripts](https://catalog.ldc.upenn.edu/LDC2002S28) were analyzed and used to train vaious classifiers.

## Feature Analysis
ParselMouth was used for extraction of min, max and average Pitch and intensity. These were then normalized using two techniques, Z-Score and Neutral-Normalisation. Normalization was needed since each speaker naturally has a different pitch range and other voice qualities like intensity. The mean and standard deviation of the features were then plotted and analysed.