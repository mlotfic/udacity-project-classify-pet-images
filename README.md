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
* [Rubric Evidence](#-rubric-evidence)
* [Uploaded Image Questions](#-uploaded-image-questions)
* [Results](#-results)
* [Key Python Concepts](#-key-python-concepts)
* [Lessons Learned](#-lessons-learned)
* [Reproducibility](#-reproducibility)
* [Conclusion](#-conclusion)

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
| ----------------------------------- | ---------------------------------------------------------------- |
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
│
└── screenshots/
    ├── 01_command_arguments.png
    ├── 02_pet_labels.png
    ├── 03_classification.png
    ├── 04_dog_not_dog.png
    ├── 05_timing.png
    └── 06_model_comparison.png
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

The application measures the execution time of the main processing workflow.

The timer starts before image processing and stops after processing is complete.

Conceptually:

```python
start_time = time()

# Main processing
...

end_time = time()

total_time = end_time - start_time
```

The elapsed time is then displayed as part of the final program output.

#### Implementation checks

* Timer starts before the main processing.
* Timer stops after processing.
* Total execution time is calculated.
* Execution time is displayed.

### 2. Pet Image Labels

The `get_pet_labels()` function extracts the expected pet label from each image filename.

For example:

```text
Poodle_07956.jpg
```

is converted to:

```text
poodle
```

A filename containing multiple words can also be converted into a normalized label.

For example:

```text
fox_squirrel_01.jpg
```

becomes:

```text
fox squirrel
```

The resulting dictionary follows the required project structure:

```python
{
    "Poodle_07956.jpg": ["poodle"],
    "fox_squirrel_01.jpg": ["fox squirrel"]
}
```

The filename is used as the dictionary key, while the extracted label is stored in the value.

---

### 3. Image Classification

Each image is passed to the pretrained classifier using its complete path.

The selected model architecture is also passed to the classifier.

The implementation follows the required pattern:

```python
classifier(images_dir + users_key, model)
```

The classifier returns a predicted label.

Before comparing the prediction with the expected label, the result is normalized:

```python
classifier_label = classifier_label.lower().strip()
```

This prevents capitalization and leading/trailing whitespace from affecting the comparison.

The application then records whether the prediction matches the expected label.

---

## 4. Dog / Not-Dog Classification

The project evaluates two independent labels:

### Actual label

The expected label is obtained from the image filename.

### Classifier label

The predicted label is returned by the pretrained image classifier.

Each label is classified as either:

```text
Dog
```

or:

```text
Not Dog
```

This produces four possible outcomes:

| Actual  | Classifier | Result    |
| ------- | ---------- | --------- |
| Dog     | Dog        | Correct   |
| Not Dog | Not Dog    | Correct   |
| Dog     | Not Dog    | Incorrect |
| Not Dog | Dog        | Incorrect |

This distinction is important because the project evaluates more than whether the classifier recognizes an animal.

The application specifically determines whether the classifier correctly identifies the image as a **dog or not a dog**.

---

## 5. Results and Model Comparison

The project evaluates three pretrained CNN architectures:

```text
AlexNet
VGG
ResNet
```

Each architecture can be executed independently.

### AlexNet

```bash
python check_images.py --arch alexnet
```

### VGG

```bash
python check_images.py --arch vgg
```

### ResNet

```bash
python check_images.py --arch resnet
```

The results can also be generated using the supplied batch script:

```bash
bash run_models_batch.sh
```

On Windows, the shell script may require Git Bash or WSL.

---

# 📸 Rubric Evidence

Screenshots are provided to document the major implementation requirements.

### Command-Line Arguments

![Command Line Arguments](screenshots/01_command_arguments.png)

Evidence includes:

* `--dir` implemented.
* Default image directory configured.
* `--arch` implemented.
* Default architecture configured.
* `--dogfile` implemented.
* Default dog-name file configured.

---

### Pet Image Labels

![Pet Image Labels](screenshots/02_pet_labels.png)

Evidence demonstrates that:

* Image filenames are processed.
* Expected pet labels are extracted.
* Image entries are stored in the required structure.

---

### Image Classification

![Image Classification](screenshots/03_classification.png)

Evidence demonstrates:

* Complete image paths are passed to the classifier.
* The selected architecture is used.
* Classifier output is normalized.
* Classification results are stored.
* Correct and incorrect classifications are counted.

---

### Dog / Not-Dog Classification

![Dog Not Dog Classification](screenshots/04_dog_not_dog.png)

Evidence demonstrates:

* Actual labels are classified as dog/not-dog.
* Classifier labels are classified as dog/not-dog.
* Dog/dog matches are identified.
* Not-dog/not-dog matches are identified.
* Dog/not-dog mismatches are identified.
* Not-dog/dog mismatches are identified.

---

### Timing

![Timing Results](screenshots/05_timing.png)

Evidence demonstrates:

* Timing starts before processing.
* Timing stops after processing.
* Total execution time is calculated.
* Execution time is displayed.

---

### Model Comparison

![Model Comparison](screenshots/06_model_comparison.png)

Evidence demonstrates:

* AlexNet was executed.
* VGG was executed.
* ResNet was executed.
* Classification statistics were generated.
* Model results were compared.

---

# 📊 Results

The final values in this section should be taken directly from the actual project execution.

Do not manually estimate or invent these values.

## Model Classification Results

| Model   | Dogs Correct | Dogs Incorrect | Not-Dogs Correct | Not-Dogs Incorrect |
| ------- | -----------: | -------------: | ---------------: | -----------------: |
| AlexNet |            — |              — |                — |                  — |
| VGG     |            — |              — |                — |                  — |
| ResNet  |            — |              — |                — |                  — |

## Execution Time

| Model   | Execution Time |
| ------- | -------------: |
| AlexNet |              — |
| VGG     |              — |
| ResNet  |              — |

> Replace the placeholders with the values produced by the completed project execution.

---

# 🖼️ Uploaded Image Classification

The project also evaluates a separate set of uploaded images using the three CNN architectures.

The commands are:

```bash
python check_images.py --dir uploaded_images/ --arch alexnet --dogfile dognames.txt
```

```bash
python check_images.py --dir uploaded_images/ --arch vgg --dogfile dognames.txt
```

```bash
python check_images.py --dir uploaded_images/ --arch resnet --dogfile dognames.txt
```

Record the actual classifier output below.

## AlexNet

```text
Dog_01.jpg: ...
Dog_02.jpg: ...
Animal_Name_01.jpg: ...
Object_Name_01.jpg: ...
```

## VGG

```text
Dog_01.jpg: ...
Dog_02.jpg: ...
Animal_Name_01.jpg: ...
Object_Name_01.jpg: ...
```

## ResNet

```text
Dog_01.jpg: ...
Dog_02.jpg: ...
Animal_Name_01.jpg: ...
Object_Name_01.jpg: ...
```

---

# ❓ Questions Regarding Uploaded Image Classification

## 1. Did the three model architectures classify the breed of `Dog_01.jpg` as the same breed?

**Answer:**

Replace this section with the actual classifications produced by AlexNet, VGG, and ResNet.

For example:

```text
AlexNet: [breed]
VGG:     [breed]
ResNet:  [breed]
```

Then state whether all three predictions were identical.

---

## 2. Did each model classify `Dog_01.jpg` as the same breed as `Dog_02.jpg`?

**Answer:**

Compare the two images separately for each architecture:

| Model   | Dog_01 | Dog_02 | Same Breed? |
| ------- | ------ | ------ | ----------- |
| AlexNet | —      | —      | —           |
| VGG     | —      | —      | —           |
| ResNet  | —      | —      | —           |

Use the actual classifier results to complete the table.

---

## 3. Did all three models correctly classify `Animal_Name_01.jpg` and `Object_Name_01.jpg` as not dogs?

**Answer:**

Compare the actual expected category with the classifier result for each model.

| Image                | AlexNet | VGG | ResNet |
| -------------------- | ------- | --- | ------ |
| `Animal_Name_01.jpg` | —       | —   | —      |
| `Object_Name_01.jpg` | —       | —   | —      |

State which predictions were correct and identify any misclassification.

---

## 4. Which model architecture performed best on the four uploaded images?

**Answer:**

The best-performing architecture should be selected using the actual results from the four uploaded images.

Consider:

* Correct dog classifications.
* Correct non-dog classifications.
* Incorrect dog classifications.
* Incorrect non-dog classifications.

Do not select a model based only on general knowledge about AlexNet, VGG, or ResNet. Use the results produced by this project.

---

# 🧠 Key Python Concepts

This project provides practical experience with several Python concepts:

### Command-line arguments

Using `argparse` to allow users to configure:

* Image directory.
* CNN architecture.
* Dog-breed file.

### Dictionaries

Used to associate image filenames with extracted labels and classification information.

### Functions

The application is divided into functions and modules with separate responsibilities.

### String processing

Used for:

* Extracting labels from filenames.
* Converting labels to lowercase.
* Removing unnecessary whitespace.
* Comparing normalized labels.

### File and directory processing

Used to locate and process images from the selected directory.

### Timing

Python's timing functionality is used to measure program execution time.

### Conditional logic

Used to determine:

* Dog vs. not-dog.
* Correct vs. incorrect classification.
* Model-specific results.

---

# ✅ Project Status

**Status:** Completed

**Course:** Udacity — AI Programming with Python

**Project:** Image Classification for a City Dog Show

**Language:** Python

**Environment:** Conda

**Models:** AlexNet, VGG, ResNet
#   u d a c i t y - p r o j e c t - c l a s s i f y - p e t - i m a g e s  
 