# MFA Alignment Assignment

## Objective

To perform forced alignment between speech audio and text transcripts using the Montreal Forced Aligner (MFA) and analyze the alignment before and after handling Out-of-Vocabulary (OOV) words.

---

## What is Forced Alignment

Forced alignment is the process of matching an audio file with its transcript and determining the exact start and end times of:

* Each word
* Each phoneme (sound)

The output is stored in TextGrid files, which can be viewed in Praat.

---

## Tools Used

* Montreal Forced Aligner (MFA)
* Anaconda
* Praat

---

## Dataset Structure

The dataset contains:

* `wav/` → audio files
* `transcripts/` → corresponding text files

After organizing for MFA:

alignmentdata/
└── speaker1/
    ├── audio files (.wav)
    └── transcript files (.txt)

---

## Steps Followed

### 1. Environment Setup

Created a conda environment and activated it:

```
conda create -n mfa_env python=3.10
conda activate mfa_env
```

Installed MFA:

```
pip install montreal-forced-aligner
```

---

### 2. Download Pretrained Models

```
mfa model download dictionary english_us_arpa
mfa model download acoustic english_us_arpa
```

---

### 3. Run Initial Alignment (Before OOV Handling)

```
mfa align alignmentdata english_us_arpa english_us_arpa output
```

This produced:

* TextGrid files inside `output/speaker1`
* Alignment analysis CSV

---

### 4. Validate and Check OOV Words

```
mfa validate alignmentdata english_us_arpa english_us_arpa
```

Result:

* OOV words were detected in transcripts.

---

### 5. Generate Pronunciations for OOV Words

```
mfa g2p alignmentdata english_us_arpa oov_dictionary.txt
```

---

### 6. Create Final Dictionary

Merged original dictionary with OOV dictionary:

```
type "C:\Users\Anushashankar\Documents\MFA\pretrained_models\dictionary\english_us_arpa.dict" oov_dictionary.txt > final_dictionary.txt
```

---

### 7. Run Alignment After OOV Handling

```
mfa align alignmentdata final_dictionary.txt english_us_arpa output_oov
```

This produced improved alignment results in:

```
output_oov/speaker1/
```

---

## Output Files

### Before OOV Handling

Folder:

```
output/speaker1/
```

Contains:

* TextGrid files
* alignment_analysis.csv

---

### After OOV Handling

Folder:

```
output_oov/speaker1/
```

Contains:

* Improved TextGrid files
* alignment_analysis.csv

---

## Alignment Visualization

A sample alignment was opened in Praat by loading:

* `.wav` file
* Corresponding `.TextGrid` file

The visualization shows:

* Waveform
* Word boundaries
* Phoneme boundaries

Screenshot is included as:

```
alignment_screenshot.png
```

---

## Observations

### Before OOV Handling

* Several words were not present in the dictionary.
* Alignment skipped or misaligned some words.

### After OOV Handling

* OOV words were added to the dictionary.
* Alignment improved with proper word and phoneme boundaries.

---

## Final Repository Structure

```
alignmentdata/
output/
output_oov/
final_dictionary.txt
alignment_screenshot.png
README.md
```
