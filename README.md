# Code Comment Classification for NLBSE'25 Tool Competition
This repository contains a multi-label classification approach to classifying code comment sentences into predefined categories for Java, Python, and Pharo codebases. Our solution builds on top of the DistilBERT model and fine-tunes it using the dataset provided by the NLBSE’25 competition organizers.

## Introduction
The NLBSE’25 tool competition challenges participants to classify code comment sentences from Java, Python, and Pharo projects into multiple categories, reflecting different types of information they convey. Our approach trains a multi-label classifier for each language using a pre-trained language model.

## Dataset
We use the dataset provided by the NLBSE’25 competition:

Source: NLBSE 2025 Tool Competition – Code Comment Classification
Languages & Categories:
Java (7 categories): summary, Ownership, Expand, usage, Pointer, deprecation, rational
Python (5 categories): Usage, Parameters, DevelopmentNotes, Expand, Summary
Pharo (7 categories): Keyimplementationpoints, Example, Responsibilities, Classreferences, Intent, Keymessages, Collaborators
The dataset includes both training and test splits for each language.

## Installation
1. Clone this repository:

`git clone https://github.com/JT-Higgins/code-comment-classification.git`

`cd code-comment-classification`


## Usage
Run the training and evaluation: Execute the script (e.g., run_classification.py) which:

* Loads the dataset for Java, Python, and Pharo.
* Applies the tokenizer and preprocesses the data.
* Fine-tunes DistilBERT for 1 epoch (by default) on each language’s training split.
* Evaluates the model on the corresponding test split.
* Prints summary results for all three languages.
`python run_classification.py`

## Methodology
* Model: DistilBERT, chosen for its efficiency and smaller size.
* Multi-Label Setup:
Each sentence can belong to multiple categories. We apply a sigmoid function on the model’s outputs and classify categories with probability > 0.5 as present.
* Training Parameters:
    * Epochs: 1 (for demonstration and efficiency)
    * Learning Rate: 5e-5
    * Batch Size: 8
    * No GPU Required: The code can run efficiently on CPU, lowering hardware barriers and making the approach more accessible.
## Results
Below is an example summary of evaluation results:

* Java: Micro-F1 ~0.84, strong performance on some categories (e.g., Ownership), weaker on Expand and rational.
* Python: Micro-F1 ~0.45, moderate on common categories like Usage and Summary, zero predictions for challenging ones like DevelopmentNotes and Expand.
* Pharo: Micro-F1 ~0.50, decent on Example and Intent, but zero predictions for multiple other categories.