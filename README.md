# PDF Data Extraction with PyMuPDF4LLM
This repository demonstrates how to extract text, images, and structured content from PDF documents using `pymupdf4llm` in Google Colab. It also includes data preparation for `LlamaIndex` for further document analysis and information extraction.

## Overview
The project involves:

- Converting PDFs to Markdown format.
- Saving extracted content to files.
- Extracting specific pages.
- Preparing data for LlamaIndex.
- Extracting images with specified DPI.
- Chunking content for metadata-rich extraction.
- Detailed word-by-word extraction for comprehensive analysis.

## Features
1. **Markdown Conversion:** Convert PDF files to markdown format.
2. **Save Extracted Content:** Save extracted text to a file.
3. **Page-Specific Extraction:** Extract content from specific pages.
4. **LlamaIndex Compatibility:** Prepare extracted data for LlamaIndex processing.
5. **Image Extraction:** Extract images with options for resolution and format.
6. **Chunked Data Extraction:** Extract data in chunks with metadata for context.
7. **Word-by-Word Extraction:** Extract detailed word-level content from PDFs.

## Requirements
Install the required packages:

```bash
!pip install pymupdf4llm llama_index
```

## Code Examples
### 1. Extract PDF Content to Markdown
```python
import pymupdf4llm
md_text = pymupdf4llm.to_markdown("test.pdf")
print(md_text)

# Save the extracted content to a Markdown file
import pathlib
pathlib.Path("output.md").write_bytes(md_text.encode())
```

### 2. Extract Specific Pages
```python
md_text_pages = pymupdf4llm.to_markdown("test.pdf", pages=[1, 2])
print(md_text_pages)
```

### 3. Prepare Data for LlamaIndex
```python
llama_reader = pymupdf4llm.LlamaMarkdownReader()
llama_docs = llama_reader.load_data("test.pdf")
print(f"LlamaIndex Compatible Data: {len(llama_docs)}")
print(llama_docs[0].text[:500])
```

### 4. Extract Images
```python
md_text_images = pymupdf4llm.to_markdown(
    doc="test.pdf",
    pages=[0, 2],
    page_chunks=True,
    write_images=True,
    image_path="images",
    image_format="png",
    dpi=300
)
```

### 5. Chunked Data Extraction
```python
md_text_chunks = pymupdf4llm.to_markdown(
    doc="test.pdf",
    pages=[0, 1, 2],
    page_chunks=True
)
print(md_text_chunks[0])
```

### 6. Word-by-Word Extraction
```python
md_text_words = pymupdf4llm.to_markdown(
    doc="test.pdf",
    pages=[0, 1, 2],
    page_chunks=True,
    write_images=True,
    image_path="images",
    image_format="png",
    dpi=300,
    extract_words=True
)
print(md_text_words[0]['words'][:5])
```

## Output
The extracted content can be used for further data analysis, NLP applications, or preparing training data for machine learning models.

## License
This project is licensed under the [MIT License](LICENSE.txt).
