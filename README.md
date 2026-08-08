# 🐕 Image Classification for a City Dog Show

**Udacity — AI Programming with Python**

A Python application that uses a pretrained image classifier to identify pets in images and determine whether the detected animal is a dog.

The project focuses on building the Python application around an existing image-classification model rather than training a neural network from scratch.

---

## 📋 Table of Contents

* [Project Overview](#-project-overview)
* [Project Objectives](#-project-objectives)
* [Project Architecture](#-project-architecture)
* [Repository Structure](#-repository-structure)
* [Environment Setup](#-environment-setup)
* [Running the Project](#-running-the-project)
* [Command-Line Arguments](#-command-line-arguments)
* [Implementation](#-implementation)

  * [1. Timing](#1-timing)
  * [2. Pet Image Labels](#2-pet-image-labels)
  * [3. Image Classification](#3-image-classification)
  * [4. Dog / Not-Dog Classification](#4-dog--not-dog-classification)
  * [5. Results and Model Comparison](#5-results-and-model-comparison)
* [Uploaded Image Questions](#-uploaded-image-questions)
* [Results](#-results)

---

## 🔎 Project Overview

The application processes a directory of pet images and compares the expected label from each image filename with the label returned by a pretrained image classifier.

The main workflow is:

```text
Command-Line Arguments
        │
        ▼
Read Pet Images
        │
        ▼
Extract Expected Labels
        │
        ▼
Run Pretrained Image Classifier
        │
        ▼
Normalize Prediction
        │
        ▼
Classify as Dog / Not Dog
        │
        ▼
Compare Actual vs Prediction
        │
        ▼
Calculate Statistics
        │
        ▼
Compare CNN Architectures
```

Three pretrained CNN architectures are evaluated:

* AlexNet
* VGG
* ResNet

The classifier is used as provided by the project. The main programming task is to build the surrounding Python application and correctly process and evaluate its predictions.

---

## 🎯 Project Objectives

The implementation addresses the following project requirements:

* Accept configuration through command-line arguments.
* Measure program execution time.
* Extract expected pet labels from image filenames.
* Classify images using a pretrained CNN.
* Normalize classifier output before comparison.
* Determine whether expected and predicted labels represent dogs.
* Compare actual labels against classifier predictions.
* Calculate classification statistics.
* Execute and compare multiple CNN architectures.

---

## 🎯 Project Objectives

The implementation addresses the following project requirements:

* Accept configuration through command-line arguments.
* Measure program execution time.
* Extract expected pet labels from image filenames.
* Classify images using a pretrained CNN.
* Normalize classifier output before comparison.
* Determine whether expected and predicted labels represent dogs.
* Compare actual labels against classifier predictions.
* Calculate classification statistics.
* Execute and compare multiple CNN architectures.

---

## 🏗️ Project Architecture

The application is divided into several Python modules, with each module responsible for a specific part of the workflow.

```text
                    check_images.py
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
 get_input_args.py  get_pet_labels.py  classify_images.py
          │                │                │
          ▼                ▼                ▼
   Configuration     Expected Labels    Predictions
          │                │                │
          └────────────────┼────────────────┘
                           ▼
             adjust_results4_isadog.py
                           │
                           ▼
             calculates_results_stats.py
                           │
                           ▼
                  print_results.py
                           │
                           ▼
                     Final Results
```

### Main Components

| File                                | Responsibility                                                   |
| ------------------------------------ | ------------------------------------------------------------------ |
| `check_images.py`                   | Main application and overall processing workflow                 |
| `get_input_args.py`                 | Processes command-line arguments                                 |
| `get_pet_labels.py`                 | Extracts expected labels from image filenames                    |
| `classify_images.py`                | Sends images to the pretrained classifier                        |
| `classifier.py`                     | Provides the pretrained image-classification functionality       |
| `adjust_results4_isadog.py`         | Determines dog/not-dog status and updates classification results |
| `calculates_results_stats.py`       | Calculates classification statistics                             |
| `print_results.py`                  | Displays final results                                           |
| `print_functions_for_lab_checks.py` | Provides output used for project/lab verification                |
| `dognames.txt`                      | List of recognized dog breeds                                    |
| `run_models_batch.sh`               | Runs the project using multiple model architectures              |
| `environment.yml`                   | Conda environment definition                                     |

---

## 📁 Repository Structure

```text
intropyproject-classify-pet-images/
│
├── README.md
├── environment.yml
├── .gitignore
│
├── check_images.py
├── get_input_args.py
├── get_pet_labels.py
├── classify_images.py
├── classifier.py
├── adjust_results4_isadog.py
├── calculates_results_stats.py
├── print_functions_for_lab_checks.py
├── print_results.py
├── test_classifier.py
│
├── dognames.txt
│
├── run_models_batch.sh
├── run_models_batch_uploaded.sh
│
├── pet_images/
│   └── *.jpg
│
├── uploaded_images/
│   └── *.jpg
```

---

## 🧪 Environment Setup

The project uses Python with a Conda environment.

Create the environment from the supplied environment definition:

```bash
conda env create -f environment.yml
```

Activate the environment:

```bash
conda activate <environment-name>
```

The exact environment name should match the name defined in `environment.yml`.

---

## ▶️ Running the Project

### 1. Test the `classifier` function

```bash
python test_classifier.py
```

output:

```text
Results from test_classifier.py
Image: pet_images/Collie_03797.jpg using model: vgg was classified as a: collie
```

### 2. Test the `get_input_args` function

```bash
python get_input_args.py
```

output:

```text
Dir: pet_images
Arch: vgg
Dogfile: dognames.txt
  in_arg.dir      = 'pet_images'   (expected: 'pet_images/')
  in_arg.arch     = 'vgg'   (expected: 'vgg')
  in_arg.dogfile  = 'dognames.txt'   (expected: 'dognames.txt')
Dir: uploaded_images/
Arch: resnet
Dogfile: custom_dognames.txt
  in_arg.dir      = 'uploaded_images/'
  in_arg.arch     = 'resnet'
  in_arg.dogfile  = 'custom_dognames.txt'
```

### 3. Test the `get_pet_labels` function

```bash
python get_pet_labels.py
```

output:

```python
{
        'Basenji_00963.jpg': ['basenji'],
        'Basenji_00974.jpg': ['basenji'],
        'Basset_hound_01034.jpg': ['basset hound'],
        'Beagle_01125.jpg': ['beagle'],
        'Beagle_01141.jpg': ['beagle'],
        'Beagle_01170.jpg': ['beagle'], 
        'Boston_terrier_02259.jpg': ['boston terrier'], 
        'Boston_terrier_02285.jpg': ['boston terrier'],
        ...
        'skunk_029.jpg': ['skunk']
}
```

### 4. Test the `classify_images` function

```bash
python classify_images.py
```

output:

```python
{
        'Basenji_00963.jpg': ['basenji', 'basenji', 1], 
        'Basenji_00974.jpg': ['basenji', 'basenji', 1], 
        'Basset_hound_01034.jpg': ['basset hound', 'basset, basset hound', 1], 
        'Beagle_01125.jpg': ['beagle', 'beagle', 1], 
        'Beagle_01141.jpg': ['beagle', 'beagle', 1], 
        'Beagle_01170.jpg': ['beagle', 'walker hound, walker foxhound', 0], 
        'Boston_terrier_02259.jpg': ['boston terrier', 'boston bull, boston terrier', 1], 
        'skunk_029.jpg': ['skunk', 'skunk, polecat, wood pussy', 1]
}
```

### 5. Test the `adjust_results4_isadog` function

```bash
python adjust_results4_isadog.py
```

output:

```python
{
        'Basenji_00963.jpg': ['basenji', 'basenji', 1, 1, 1], 
        'Basenji_00974.jpg': ['basenji', 'basenji', 1, 1, 1], 
        'Basset_hound_01034.jpg': ['basset hound', 'basset, basset hound', 1, 1, 1], 
        'Beagle_01125.jpg': ['beagle', 'beagle', 1, 1, 1], 
        'Beagle_01141.jpg': ['beagle', 'beagle', 1, 1, 1], 
        'Beagle_01170.jpg': ['beagle', 'walker hound, walker foxhound', 0, 1, 1], 
        'Boston_terrier_02259.jpg': ['boston terrier', 'boston bull, boston terrier', 1, 1, 1], 
        'skunk_029.jpg': ['skunk', 'skunk, polecat, wood pussy', 1, 0, 0]
}
```

### 6. Test the `calculates_results_stats` function

```bash
python calculates_results_stats.py
```

output:

```python
{
        'n_dogs_img': 7, 
        'n_match': 7, 
        'n_correct_dogs': 7, 
        'n_correct_notdogs': 1, 
        'n_correct_breed': 6, 
        'n_images': 8, 
        'n_notdogs_img': 1, 
        'pct_match': 87.5, 
        'pct_correct_dogs': 100.0, 
        'pct_correct_breed': 85.71428571428571, 
        'pct_correct_notdogs': 100.0
}
```

### Default execution

```bash
python check_images.py
```

### Specify the image directory

```bash
python check_images.py --dir pet_images/
```

### Specify the CNN architecture

```bash
python check_images.py --arch vgg
```

### Specify the dog-breed file

```bash
python check_images.py --dogfile dognames.txt
```

### Complete example

```bash
python check_images.py \
    --dir pet_images/ \
    --arch vgg \
    --dogfile dognames.txt
```

On Windows PowerShell, the same command can be written on one line:

```powershell
python check_images.py --dir pet_images/ --arch vgg --dogfile dognames.txt
```

---

## 🧾 Command-Line Arguments

The application supports three main command-line arguments.

| Argument    | Purpose                                 | Default        |
| ----------- | --------------------------------------- | -------------- |
| `--dir`     | Directory containing the images         | `pet_images/`  |
| `--arch`    | CNN architecture used by the classifier | `vgg`          |
| `--dogfile` | File containing recognized dog breeds   | `dognames.txt` |

Example:

```bash
python check_images.py --dir uploaded_images/ --arch alexnet --dogfile dognames.txt
```

---

## 🔧 Implementation

### 1. Timing

`check_images.py` records the start and end time of the full pipeline (image reading, classification, statistics) using Python's `time` module, and reports the elapsed runtime in `HH:MM:SS` format at the end of each run (see the `** Total Elapsed Runtime` line in the outputs below).

### 2. Pet Image Labels

`get_pet_labels.py` parses each filename in the image directory (e.g. `Basenji_00963.jpg`), strips the trailing digits and extension, replaces underscores with spaces, and lowercases the result to build the expected ("real") label for that image — see step 3 above.

### 3. Image Classification

`classify_images.py` calls the pretrained `classifier()` function (from `classifier.py`) on each image using the architecture chosen via `--arch`, then normalizes the returned label so it can be compared against the expected label from step 2 (case, punctuation, and whitespace differences are handled here) — see step 4 above.

### 4. Dog / Not-Dog Classification

`adjust_results4_isadog.py` checks the expected label and the classifier's label against `dognames.txt` to determine whether each represents a dog breed, appending two additional flags (`is-a-dog` for the real label, `is-a-dog` for the classifier label) to each entry's result list — see step 5 above.

### 5. Results and Model Comparison

`check_images.py` runs the full pipeline end-to-end for each of the three CNN architectures and reports summary statistics for each. The full outputs are below.

The project evaluates three pretrained CNN architectures:

```text
AlexNet
VGG
ResNet
```

Each architecture can be executed independently.

#### AlexNet

```bash
python check_images.py --arch alexnet
```

output

```text
Dir: pet_images
Arch: alexnet
Dogfile: dognames.txt
Command Line Arguments:
     dir = pet_images
    arch = alexnet
 dogfile = dognames.txt

...

# Total Images 40 # Matches: 30 # NOT Matches: 10

 ** Statistics from calculates_results_stats() function:
N Images: 40  N Dog Images: 30  N NotDog Images: 10
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed:  80.0

 ** Check Statistics - calculated from this function as a check:
N Images: 40  N Dog Images: 30  N NotDog Images: 10
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed:  80.0


*** Results Summary for CNN Model Architecture ALEXNET ***
N Images            :  40
N Dog Images        :  30
N Not-Dog Images    :  10

pct_match: 75.0
pct_correct_dogs: 100.0
pct_correct_breed: 80.0
pct_correct_notdogs: 100.0

INCORRECT Dog Breed Assignment:
Real:                     beagle   Classifier:               english foxhound
Real:                     beagle   Classifier:  walker hound, walker foxhound
Real:             boston terrier   Classifier:                        basenji
Real:           golden retriever   Classifier:                tibetan mastiff
Real:           golden retriever   Classifier:           afghan hound, afghan
Real:             great pyrenees   Classifier:                         kuvasz

** Total Elapsed Runtime: 0:0:3
```

### VGG

```bash
python check_images.py --arch vgg
```

output

```text
Dir: pet_images
Arch: vgg
Dogfile: dognames.txt
Command Line Arguments:
     dir = pet_images
    arch = vgg
 dogfile = dognames.txt

...

# Total Images 40 # Matches: 35 # NOT Matches: 5

 ** Statistics from calculates_results_stats() function:
N Images: 40  N Dog Images: 30  N NotDog Images: 10
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed:  93.3

 ** Check Statistics - calculated from this function as a check:
N Images: 40  N Dog Images: 30  N NotDog Images: 10
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed:  93.3


*** Results Summary for CNN Model Architecture VGG ***
N Images            :  40
N Dog Images        :  30
N Not-Dog Images    :  10

pct_match: 87.5
pct_correct_dogs: 100.0
pct_correct_breed: 93.33333333333333
pct_correct_notdogs: 100.0

INCORRECT Dog Breed Assignment:
Real:                     beagle   Classifier:  walker hound, walker foxhound
Real:             great pyrenees   Classifier:                         kuvasz

** Total Elapsed Runtime: 0:0:23
```

### ResNet

```bash
python check_images.py --arch resnet
```

output

```text
Dir: pet_images
Arch: resnet
Dogfile: dognames.txt
Command Line Arguments:
     dir = pet_images
    arch = resnet
 dogfile = dognames.txt

...

# Total Images 40 # Matches: 33 # NOT Matches: 7

 ** Statistics from calculates_results_stats() function:
N Images: 40  N Dog Images: 30  N NotDog Images: 10
Pct Corr dog: 100.0 Pct Corr NOTdog:  90.0  Pct Corr Breed:  90.0

 ** Check Statistics - calculated from this function as a check:
N Images: 40  N Dog Images: 30  N NotDog Images: 10
Pct Corr dog: 100.0 Pct Corr NOTdog:  90.0  Pct Corr Breed:  90.0


*** Results Summary for CNN Model Architecture RESNET ***
N Images            :  40
N Dog Images        :  30
N Not-Dog Images    :  10

pct_match: 82.5
pct_correct_dogs: 100.0
pct_correct_breed: 90.0
pct_correct_notdogs: 90.0

INCORRECT Dog/NOT Dog Assignments:
Real:                        cat   Classifier:   norwegian elkhound, elkhound

INCORRECT Dog Breed Assignment:
Real:                     beagle   Classifier:  walker hound, walker foxhound
Real:           golden retriever   Classifier:                       leonberg
Real:             great pyrenees   Classifier:                         kuvasz

** Total Elapsed Runtime: 0:0:6
```

The results can also be generated using the supplied batch script:

```bash
bash run_models_batch.sh
```

On Windows, the shell script may require Git Bash or WSL.

---

## 📊 Results

The final values in this section are taken directly from the `pet_images/` (40-image) `*** Results Summary ***` blocks shown above, under [5. Results and Model Comparison](#5-results-and-model-comparison). "Dogs Correct/Incorrect" reflects breed-level accuracy on the 30 dog images (the `pct_correct_dogs` figure was 100% for all three — every dog image was correctly identified *as a dog* — so breed match is the meaningful split here); "Not-Dogs Correct/Incorrect" reflects accuracy on the 10 non-dog images.

### Model Classification Results

| Model   | Dogs Correct (breed) | Dogs Incorrect (breed) | Not-Dogs Correct | Not-Dogs Incorrect |
| ------- | -------------------: | ---------------------: | ---------------: | -----------------: |
| AlexNet |                   24 |                      6 |               10 |                  0 |
| VGG     |                   28 |                      2 |               10 |                  0 |
| ResNet  |                   27 |                      3 |               9 |                   1 |

### Execution Time

| Model   | Execution Time |
| ------- | ---------------: |
| AlexNet |            0:0:3 |
| VGG     |           0:0:23 |
| ResNet  |            0:0:6 |

---

# 🖼️ Uploaded Image Classification

The project also evaluates a separate set of uploaded images using the three CNN architectures.

The commands are:

```bash
python check_images.py --dir uploaded_images/ --arch alexnet --dogfile dognames.txt
```

output:

```text
Dir: uploaded_images/
Arch: alexnet
Dogfile: dognames.txt
Command Line Arguments:
     dir = uploaded_images/
    arch = alexnet
 dogfile = dognames.txt

...

# Total Images 4 # Matches: 2 # NOT Matches: 2

 ** Statistics from calculates_results_stats() function:
N Images:  4  N Dog Images:  2  N NotDog Images:  2
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed:  50.0

 ** Check Statistics - calculated from this function as a check:
N Images:  4  N Dog Images:  2  N NotDog Images:  2
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed:  50.0


*** Results Summary for CNN Model Architecture ALEXNET ***
N Images            :   4
N Dog Images        :   2
N Not-Dog Images    :   2

pct_match: 50.0
pct_correct_dogs: 100.0
pct_correct_breed: 50.0
pct_correct_notdogs: 100.0

INCORRECT Dog Breed Assignment:
Real:           golden retriever   Classifier:           afghan hound, afghan

** Total Elapsed Runtime: 0:0:0
```

```bash
python check_images.py --dir uploaded_images/ --arch vgg --dogfile dognames.txt
```

```text

Dir: uploaded_images/
Arch: vgg
Dogfile: dognames.txt
Command Line Arguments:
     dir = uploaded_images/
    arch = vgg
 dogfile = dognames.txt

...

# Total Images 4 # Matches: 2 # NOT Matches: 2

 ** Statistics from calculates_results_stats() function:
N Images:  4  N Dog Images:  2  N NotDog Images:  2
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed: 100.0

 ** Check Statistics - calculated from this function as a check:
N Images:  4  N Dog Images:  2  N NotDog Images:  2
Pct Corr dog: 100.0 Pct Corr NOTdog: 100.0  Pct Corr Breed: 100.0


*** Results Summary for CNN Model Architecture VGG ***
N Images            :   4
N Dog Images        :   2
N Not-Dog Images    :   2

pct_match: 50.0
pct_correct_dogs: 100.0
pct_correct_breed: 100.0
pct_correct_notdogs: 100.0

** Total Elapsed Runtime: 0:0:2
```

```bash
python check_images.py --dir uploaded_images/ --arch resnet --dogfile dognames.txt
```

output:

```text
Dir: uploaded_images/
Arch: resnet
Dogfile: dognames.txt
Command Line Arguments:
     dir = uploaded_images/
    arch = resnet
 dogfile = dognames.txt

...

# Total Images 4 # Matches: 3 # NOT Matches: 1

 ** Statistics from calculates_results_stats() function:
N Images:  4  N Dog Images:  2  N NotDog Images:  2
Pct Corr dog: 100.0 Pct Corr NOTdog:  50.0  Pct Corr Breed: 100.0

 ** Check Statistics - calculated from this function as a check:
N Images:  4  N Dog Images:  2  N NotDog Images:  2
Pct Corr dog: 100.0 Pct Corr NOTdog:  50.0  Pct Corr Breed: 100.0


*** Results Summary for CNN Model Architecture RESNET ***
N Images            :   4
N Dog Images        :   2
N Not-Dog Images    :   2

pct_match: 75.0
pct_correct_dogs: 100.0
pct_correct_breed: 100.0
pct_correct_notdogs: 50.0

INCORRECT Dog/NOT Dog Assignments:
Real:                        cat   Classifier:   norwegian elkhound, elkhound

** Total Elapsed Runtime: 0:0:1

```

---

## ❓ Uploaded Image Questions

### 1. Did the three model architectures classify the breed of `Collie_01.jpg` as the same breed?

**Answer:**

```text
AlexNet: collie
VGG:     collie
ResNet:  collie
```

Yes — all three architectures classified `Collie_01.jpg` as **collie**. This is consistent with the uploaded-image breed-accuracy results above: VGG and ResNet each reported 100% correct breed classification, and AlexNet's only breed error (`pct_correct_breed: 50.0`) was on the golden retriever image, not the collie.

### 2. Did each model classify `Collie_01.jpg` as the same breed as `Golden_retriever_02.jpg`?

**Answer:**

Compare the two images separately for each architecture:

| Model   | Dog_01 (Collie_01.jpg) | Dog_02 (Golden_retriever_02.jpg) | Same Breed? |
| ------- | ---------------------- | -------------------------------- | ----------- |
| AlexNet | collie                 | afghan hound, afghan             | No          |
| VGG     | collie                 | golden retriever                 | No          |
| ResNet  | collie                 | golden retriever                 | No          |

No model classified the two images as the same breed. VGG and ResNet got both breeds right; AlexNet got the collie right but misclassified the golden retriever as an afghan hound — its one incorrect dog breed assignment on the uploaded set.

### 3. Did all three models correctly classify `cat_01.jpg` and `hourglass_01.jpg` as not dogs?

**Answer:**

Compare the actual expected category with the classifier result for each model.

| Image               | AlexNet   | VGG       | ResNet                                    |
| -------------------- | --------- | --------- | ------------------------------------------ |
| `cat_01.jpg`         | Correct   | Correct   | **Incorrect** — classified as a dog (norwegian elkhound, elkhound) |
| `hourglass_01.jpg`   | Correct   | Correct   | Correct                                    |

AlexNet and VGG correctly identified both non-dog images (`pct_correct_notdogs: 100.0` for each). ResNet missed one — it misclassified `cat_01.jpg` as a dog, bringing its not-dog accuracy down to 50%, while still correctly passing `hourglass_01.jpg`.

### 4. Which model architecture performed best on the four uploaded images?

**Answer:**

**VGG** performed best on the uploaded set — it was the only architecture with zero classification errors across all four images: 100% correct dog/not-dog identification and 100% correct breed identification.

* **AlexNet** — correctly identified dog vs. not-dog for all four images (100% correct dogs, 100% correct not-dogs) but got one breed wrong (golden retriever misclassified as afghan hound → 50% correct breed).
* **VGG** — no errors: both dogs correctly identified and breed-classified, both not-dogs correctly identified.
* **ResNet** — got both dog breeds right (100% correct breed) but misclassified `cat_01.jpg` as a dog, the only dog/not-dog error among the three (90% correct not-dogs on the full 40-image set, 50% on the 4-image uploaded set).

VGG's accuracy comes at a runtime cost, though: on the full `pet_images/` set above it took roughly 8x longer than AlexNet (0:0:23 vs. 0:0:3) and about 4x longer than ResNet (0:0:23 vs. 0:0:6).

---

# ✅ Project Status

**Status:** Completed

**Course:** Udacity — AI Programming with Python

**Project:** Image Classification for a City Dog Show

**Language:** Python

**Environment:** Conda

**Models:** AlexNet, VGG, ResNet

---

## 📚 Project Source & References

### Udacity Project Repository

This project is based on the Udacity **AI Programming with Python Nanodegree** revision repository:

[Udacity AIPND Revision Repository](https://github.com/udacity/AIPND-revision?utm_source=chatgpt.com)

The repository provides the original project materials and reference implementation structure for the **Image Classification for a City Dog Show** project.

### Uploaded Image Source

The `hourclass.jpg` image in the `uploaded_images/` directory was sourced from:

[Depositphotos — Vintage kerosene lamp on wooden table](https://depositphotos.com/photo/vintage-kerosene-lamp-on-wooden-table-19960419.html?utm_source=chatgpt.com)

| File                            | Source                                                  |
| ------------------------------- | ------------------------------------------------------- |
| `uploaded_images/hourclass.jpg` | Depositphotos — *Vintage kerosene lamp on wooden table* |

> **Note:** Source attribution identifies the origin of the image. Redistribution of the image in a public repository remains subject to the applicable source/license terms.
