# TranslationMetric

TranslationMetric is a Python class for evaluating machine translations against reference translations using multiple metrics.

## Features

- Supports multiple evaluation metrics: characTER, chrF, and BLEU
- Handles input as lists, file paths, or multi-line strings
- Generates individual and overall scores for each metric
- Creates a JSON report with detailed evaluation results

## Installation

1. Ensure you have Python 3.6+ installed.
2. Install required packages:
```bash
pip install sacrebleu python-Levenshtein
```
3. Place `TranslationMetric.py` in your project directory.

## Usage

### Basic Usage
```python

from TranslationMetric import TranslationMetric
```
# Initialize the evaluator
```python
# parameters can be anything (will be recorded in final report)
evaluator = TranslationMetric(model_name="MyTranslationModel", version="1.0")
```
# Compare translations
```python
generated = ["This is a test.", "Another test sentence."]

reference = ["This is a reference.", "Another reference sentence."]

results = evaluator.compare_translations(generated, reference)
```
# Print overall scores
```python
for metric, score in results.items():

print(f"{metric} overall score: {score.overall}")
```
# Generate a report
```python
evaluator.generate_report("evaluation_report.json")
```
### Input Formats

The `compare_translations` method accepts various input formats:

1. Lists of strings:
```python
generated = ["Translation 1", "Translation 2"]

reference = ["Reference 1", "Reference 2"]
```
2. File paths:
```python

generated = "path/to/generated_translations.txt"

reference = "path/to/reference_translations.txt"
```
3. Multi-line strings:
```python

generated = """

Translation 1

Translation 2

"""

reference = """

Reference 1

Reference 2

"""
```
### Accessing Scores

After running `compare_translations`, you can access scores:
```python
# Overall score for a metric

chrf_overall = results['chrF'].overall

# Individual scores for a metric

bleu_scores = results['BLEU'].individual

# Specific score for a translation

characTER_score_line2 = results['characTER'].individual[1]
```
## Generating Reports

The `generate_report` method creates a JSON file with detailed evaluation information:
```python
evaluator.generate_report("evaluation_report.json")
```
This report includes:
- Datetime of evaluation
- Generated and reference translations
- Overall and individual scores for each metric
- Parameters used for evaluation

## Customization

You can add custom parameters when initializing the evaluator:
```python
evaluator = TranslationMetric(model_name="MyModel", version="2.0", custom_param="value")
```
These parameters will be included in the generated report.
