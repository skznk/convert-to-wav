Audio Folder Conversion & Dataset Splitter

This project provides utilities to:

Convert audio files in a folder (including subdirectories) to WAV format

Preserve the original directory structure in the output folder

Split WAV files into train / validation / test datasets based on directory labels

Folder-to-WAV Conversion

The conToWav function converts all audio files in a directory tree to WAV format while preserving the original folder structure.

Usage

Call the function from main:

conToWav(path_to_folder, path_to_outputfolder)

Parameters

path_to_folder
Path to the input folder containing audio files and subdirectories.

path_to_outputfolder
Path to the output folder where converted WAV files will be written.
The original directory structure is preserved.

Behavior

Non-WAV audio files are converted to WAV.

Existing WAV files are copied as-is.

Files that already exist in the output folder are skipped (safe to rerun).

Train / Validation / Test Split

The splitInto function splits WAV files into training, validation, and test sets based on probability.

Each subdirectory name is treated as a label (e.g., spoken digits, classes).

Usage
splitInto(
    path_to_folder,
    train_prob,
    val_prob,
    test_prob,
    path_to_train,
    path_to_val,
    path_to_test,
    names_of_subdirectories
)

Parameters

path_to_folder
Path to the folder containing WAV files organized by label subdirectories.

train_prob, val_prob, test_prob
Probabilities for splitting the data (e.g. 0.7, 0.15, 0.15).

path_to_train, path_to_val, path_to_test
Output directories for the train, validation, and test datasets.

names_of_subdirectories
A list of subdirectory names representing class labels.

Example:

['zero', 'one', 'two', 'three', 'four',
 'five', 'six', 'seven', 'eight', 'nine']

Notes

The directory names are used as labels for training a neural network.

This design ensures label consistency between the dataset structure and the model.

The script is safe to rerun without duplicating work.

Example Workflow
conToWav("raw_audio", "wav_audio")

splitInto(
    "wav_audio",
    0.7, 0.15, 0.15,
    "dataset/train",
    "dataset/val",
    "dataset/test",
    ['zero','one','two','three','four','five','six','seven','eight','nine']
)

