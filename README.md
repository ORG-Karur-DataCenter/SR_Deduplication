# 🧹 SMR Deduplication Agent

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Library-Pandas-orange)](https://pandas.pydata.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

> [!NOTE]
> A deduplication agent identifies and removes duplicate records using DOI matching, title similarity, and author/year concordance. In cases of conflict, where duplication cannot be confidently determined, both documents are retained to avoid inadvertently removing valid entries. Deduplication outputs are logged and cross-checked against independent reviewers.

This agent automates the cleanup of bibliographic records from multiple academic databases (PubMed, Embase, Cochrane, Scopus, Web of Science, etc.). It uses a hierarchical matching logic to identify and remove duplicates across different file formats.

---

## ✨ Features

- **📂 Multi-Format Support**: Automatically detects and handles:
    - **PubMed**: `.txt`, `.nbib`
    - **RIS**: `.ris` (Standard, Embase, Cochrane, Scopus, etc.)
    - **BibTeX**: `.bib` (Web of Science, Scopus)
    - **CSV/Excel**: Handles various column naming conventions.
    - **Tab-Delimited**: Web of Science `.txt` exports.
- **🔍 Automatic Discovery**: Scans the directory for all supported files—no need for specific filenames.
- **🤝 Cross-Database Deduplication**: Removes duplicates across all provided search results simultaneously.
- **🧠 Hierarchical Matching**: 
  1. **DOI Match** (Highest Priority, normalized for many variations)
  2. **PMID Match**
  3. **Exact Title Match** (Case and character normalized)
  4. **Fuzzy Title Similarity** (95% similarity or 85% with year match)

---

## 🚀 How to Use

### 1️⃣ Prepare Your Input Files
Place your exported search results in this folder. supported extensions: `.txt`, `.bib`, `.ris`, `.csv`, `.nbib`, `.ciw`, `.enw`.

### 2️⃣ Run the Program
Ensure you have Python and `pandas` installed. Run the deduplication script:
```powershell
python deduplicate_files.py
```

### 3️⃣ Get the Output
The program will generate deduplicated files for each input, appending `_deduplicated` to the filename (e.g., `scopus_export_deduplicated.bib`).

### 4️⃣ Verify Counts
You can run the counting scripts to see how many unique records were found:
```powershell
python count_records.py   # Counts records in input files
python verify_clean.py    # Counts records in output files
```

---
## 🛠️ Matching Logic Details

- **Normalization**: Titles are stripped of special characters and whitespace for exact matching.
- **DOIs**: Automatically extracts and normalizes DOIs from various prefixes and formats.
- **Stability**: Files are processed in alphabetical order to ensure consistent results across runs.
- **Efficiency**: Deduplicates within each file and then checks against all previously processed records.

---

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
