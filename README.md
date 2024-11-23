# SEC 10-X Filings Dataset

This dataset contains processed SEC 10-X (10-K, 10-Q) filings, focusing on Risk Factors and Management Discussion & Analysis (MD&A) sections from corporate financial reports from 1993-2023.

🔗 Original Dataset: [[SEC-EDGAR-10X]](https://sraf.nd.edu/sec-edgar-data/cleaned-10x-files/) contains stripped down versions of the original filings, details about which can be found [here](https://sraf.nd.edu/sec-edgar-data/cleaned-10x-files/10x-stage-one-parsing-documentation/). 

This dataset is a further cleaned tabulated version of the original stripped down version making it more suitable for training tasks.

Note: Documents with no match to risk factors or MD&A have been filtered out.

## Dataset Description

### Overview

This dataset is derived from SEC 10-X filings and provides structured access to two critical sections of corporate financial reports:
- Risk Factors (Item 1A)
- Management's Discussion and Analysis (Item 7)

The data has been processed to enable natural language processing and financial analysis tasks.

### Processing Methodology

The dataset was created using a parsing pipeline that addresses several key considerations:

1. **Risk Factors Extraction**
   - Multiple instances of risk factors may appear in a single filing
   - The parser identifies all instances and selects the most comprehensive section
   - When multiple valid sections are found, the longest section is retained to ensure completeness

2. **MD&A Extraction**
   - Management Discussion & Analysis sections are identified and extracted
   - Multiple MD&A sections within a filing are concatenated to preserve all relevant information

3. **Data Organization**
   - Filings are grouped by CIK (Central Index Key) and filing date
   - Multiple sections from the same filing are combined
   - Empty or invalid entries are filtered out

### Data Format

The dataset is stored in Parquet format with the following schema:
```python
{
'CSI': 'string', # Central Index Key (CIK)
'FILE_DATE': 'string', # Filing date in YYYYMMDD format
'RISK_FACTOR': 'string', # Extracted Risk Factors section
'MD&A': 'string' # Extracted Management Discussion & Analysis section
}
```
## Usage

### Loading the Dataset
```python
import datasets
dataset = datasets.load_dataset("theaayushbajaj/10-X-raw-v1", split="train")
```

### Example Applications

- Risk analysis and classification
- Temporal analysis of corporate risk factors
- Business strategy analysis through MD&A
- Corporate disclosure analysis
- Financial sentiment analysis

## Acknowledgments

- Securities and Exchange Commission (SEC) for providing access to the original filings
- [Additional acknowledgments to be added]