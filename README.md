# Acoustic Side Channel Attack on Keystrokes

   This project is based off of Joshua Harrison and Partner’s Paper Acoustic Side Channel Attack on Keyboards. The attack involved in collecting a phone and zoom recording raw .wav audio of a person typing on a 2021 MacBook Pro and extracting the keysroke audio using FFT and transform to spectrograms to utilize a pre-trained CoAtNet model to predict laptop keystrokes (36 possibilities which are [a-z0-9]).

   There are 3 version of 2 models being trained and evaluated:

   1. Zoom Audio Model  (V1 and V2) for zoom recording audio
   2. Phone Audio Model (V1 and V2) for phone recording audio
   3. Zoom Audio Model (V3) for zoom recording audio
   4. Phone Audio Model (V3) for phone recodrding audio


## Repo Structure:

```
├── AudioPreprocessing          
│   ├── 0-9                                                # Contain result keystroke extractions from running the extraction program
│   ├── 0-9-clean.wav                                      # An audio of all the extracted keystroke combined
│   ├── 0-9.wav                                            # Original audio before extraction
│   ├── RecordingKeystrokeIsolator.ipynb                   # Keystroke isolator code
│   └── keystrokeExtractionLogic                           # Data flow of how the keystroke isolator works
├── CoATNet                                                # The source code of the Pre-Trained CoATNet models and the author original source code                 
├── InferencePhrase                                        # Inference Stage of the models, contains all the Pre-Trained CoATNet models and their training + eval result, all the pre-recorded audios, and the source code for running the model in 
├── Keystroke-Datasets                                     # Clean Keystoke dataset obtain from /Botacin-s-Lab/EchoCrypt/
├── Reading                                                # The original Harrison et Al paper that lay the foundation of this project 
└── README.md                                              # This file
```

## Keystroke Datasets:

Original dataset can be found through this [link](https://github.com/Botacin-s-Lab/EchoCrypt/tree/main/dataset)

## Pipeline:

   **Training and Validation of CoATNet model**
   ```
   Clean Keystroke Data -> Spectrogram Transformation -> Building CoATnet architecture -> Training and Validation -> Performance Metrics
   ```


   **Conducting Actual Attacks**
   ```
   Raw audio recording -> FFT algorithm to extract keystrokes audio -> Spectrogram Transformation -> Pre-Trained CoATnet -> Prediction
   ```


## Key Features:

   **Training and Validation Phrase**

      1. A clean keystrokes (a-z0-9) on a 2021 Macbook Pro Model obtained from https://github.com/Botacin-s-Lab/EchoCrypt/tree/main/dataset
      2. Transforming the isolated keystrokes to Mel Spectrograms and Torch Tensors
      3. Uses CoAtNet architecture which utilizes convolution and transformer layers to train on the tensors.
      4. Tracks the Performance of the model using
         Loss
         Accuracy
         Precision
         Recall
         Weighted F1 Score
         Confusion Matrix
      5. Uses early stopping to prevent overfitting and training plateau to avoid unnecessary training epochs.
      6. Automatically saves the best model for later inference stage.
      7. Generates the training, validation, Confusion matrix, Precision, Recall, and F1 score visualizations across the training and validation process.

   **Conducting Actual Attacks**

      1. Extraction of keystroke sounds from recording audio using Fast-Fourier-Transform algorithm to enhance SNR.
      2. Transforming the isolated keystrokes to Mel Spectrograms and Torch Tensors.
      3. Passing the tensors to pre-trained CoATnet models to obtain the keystroke prediction.

## Model Training and Evaluation Results:

   **Phone Model V1**\
      Training Accuracy: 1.0000\
      Validation Accuracy: 0.4500\
      Precision: 0.4965\
      Recall: 0.4500\
      F1: 0.5278\
      Model Parameters: 276,580\
      Total Epochs: 1100

   **Zoom Model V1**\
      Training Accuracy: 1.0000\
      Validation Accuracy: 0.3167\
      Precision: 0.3573\
      Recall: 0.3167\
      F1: 0.3749\
      Model Parameters: 276,580\
      Total Epochs: 1100

   **Phone Model V2**\
      Training Accuracy: 0.5486\
      Validation Accuracy: 0.5333\
      Precision: 0.5539\
      Recall: 0.5333\
      F1: 0.5360\
      Model Parameters: 276,580\
      Total Epochs: 1100
      
   **Zoom Model V2**\
      Training Accuracy: 0.6153\
      Validation Accuracy: 0.3667\
      Precision: 0.3579\
      Recall: 0.3667\
      F1: 0.3532\
      Model Parameters: 276,580\
      Total Epochs: 1100

## Requirements:
   $ Need Jupyter Notebook installed\
   $ Python version 3.11+\
   $ pip install torch torchvision torchaudio\
   $ pip install librosa numpy scikit-learn matplotlib tqdm\
   $ An Iphone 16 with a recording software (Voice Memo)\
   $ Zoom application with Zoom recording enabled with background noise suppression settings to **MEDIUM**\
   $ 2021 Macbook Pro


## Usage Instruction:
   Follow the jupyter notebook in each directory


## Known Issues:
   1. The string of all keys we would like to process isn’t complete, there is no space bar, no ., or underscores, which is why this particular code may not work successfully in a scenario where you’re on a zoom meeting trying to listen in on someone putting in login credentials (since most passwords nowadays require ,. Or underscores. Other factors may impact the results such as the speed of typing, the loudness/audio of the key stroke could impact the model Other noises (fan/Airconditioning).
   2. We didn’t use the same setup as the original Author (with a microfiber cloth under the phone)
   3. The isolator script sometimes wouldn’t actually extract all possible key strokes (for example if our sentence  has 35 valid characters, it would capture only 32).
   4. Not enough computation power to enhance the model complexity for better accuracy
   5. The Fast-Fourier Extraction script still premature and can not cleanly extracting the exact keystroke noise

## Contributors:
   1. David Nguyen - DavidNguyen1812
   2. Sarah Soliman - sarahsolimans




 
 
