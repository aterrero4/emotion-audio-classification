## Emotion-Based Audio Prediction Using Beat-Level Timbre

### Introduction

Emotion recognition in music is a critical area of interest within music information retrieval (MIR), providing insights into listener engagement, preference, and emotional response. Typically, emotional classification tasks rely on metadata or lyrical content. This project uniquely approaches emotion classification through intrinsic audio features alone, particularly leveraging detailed timbral information extracted at the beat level. Specifically, the objective is to predict emotional categories—defined by Russell's Circumplex Model (Happy, Tense, Sad, and Relaxed)—solely from beat-level audio characteristics.

### Background

In affective computing and MIR, Russell's Circumplex Model of Affect serves as a widely accepted framework, categorizing emotions into quadrants based on two dimensions: valence (positive-negative) and arousal (high-low). This project employs this model to categorize music tracks into four distinct emotional quadrants:
- **Happy**: Positive valence, high arousal
- **Tense**: Negative valence, high arousal
- **Sad**: Negative valence, low arousal
- **Relaxed**: Positive valence, low arousal

The Free Music Archive (FMA) dataset, enhanced by the EchoNest feature set, offers robust audio analysis data ideal for this exploration. EchoNest, a music intelligence company acquired by Spotify, provides detailed audio attributes such as timbre, pitch, and rhythm at high temporal resolution. Particularly relevant for this project is EchoNest’s timbre vector—a complex measure representing the tonal quality or "color" of music. Each beat-level segment includes these timbral features, captured via principal component analysis (PCA), reflecting psychoacoustic perceptions like brightness and flatness independent of pitch or loudness.

### Dataset Overview

The datasets used in this study are:

- **Free Music Archive (FMA)**:
  - Curated by researchers at EPFL for music information retrieval research.
  - Contains approximately 106,574 tracks across various genres.

- **EchoNest Audio Features**:
  - Provides detailed global and temporal audio descriptors.
  - Initially contained around 13,000 tracks with roughly 250 columns.

### Data Cleaning and Preprocessing

The preprocessing steps included:
- Flattening multi-index columns and removing sparse features (threshold: >23% missing values).
- Dropping rows with any remaining null values.
- Splitting into global audio features (valence, energy, tempo, etc.) and beat-level PCA timbre data.
- Final datasets:
  - `echonest_audio_features.csv`: Global audio descriptors.
  - `echonest_audio_temporal.csv`: Beat-level PCA timbre data (224 beats per track).

### Exploratory Data Analysis (EDA)

Key steps and findings:
- Emotional labels created based on valence and energy.
- Observed class imbalance (manageable through stratification).
- Distinct temporal patterns identified (e.g., spike at beat 120, indicative of choruses).

### Predictive Modeling & Evaluation

Modeling approach and results:
- Random Forest classifier with 5-fold cross-validation.
- Achieved a mean accuracy of approximately 71%.
- Hold-out test accuracy reached 74%.
- Confusion matrices indicated stronger predictive power for arousal compared to valence.
- Feature importance analysis revealed that the first 55 beats contained the majority of emotional cues.

### Conceptual Insights

- Beat-level PCA timbre features are strongly predictive of emotional categories.
- Early musical segments (first 55 beats) are critical for emotion recognition.

### Conclusion and Future Recommendations

This project demonstrates that intrinsic acoustic features, specifically beat-level timbral information, are sufficient for effective emotional classification in music. Future work is recommended to explore emotion-conditioned generative models (e.g., GAN-based music synthesis), utilizing the predictive insights developed here.