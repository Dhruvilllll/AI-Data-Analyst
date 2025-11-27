# 🔧 Suggested Code Improvements

This document outlines potential enhancements to make your codebase even more professional.

## Quick Wins

### 1. Add Error Handling for File Upload Limits

**In app.py, add after line 17:**
```python
# Set maximum file size (200MB)
MAX_FILE_SIZE = 200 * 1024 * 1024  # 200MB in bytes

if uploaded and uploaded.size > MAX_FILE_SIZE:
    st.error(f"File too large! Maximum size is 200MB. Your file is {uploaded.size / (1024*1024):.1f}MB")
    st.stop()
```

### 2. Add Loading Progress Bar

**In app.py, replace line 31-34:**
```python
# Load data with progress indicator
with st.spinner("Loading file..."):
    try:
        df = load_data(uploaded)
        st.success(f"✅ File loaded successfully! {len(df):,} rows × {len(df.columns)} columns")
    except Exception as e:
        st.error(f"❌ Failed to load file: {e}")
        st.stop()
```

### 3. Add Data Validation

**In try1.py, add this function:**
```python
def validate_dataframe(df: pd.DataFrame) -> tuple[bool, str]:
    """Validate that DataFrame is suitable for analysis."""
    if df.empty:
        return False, "DataFrame is empty"
    if len(df) < 2:
        return False, "DataFrame has too few rows (minimum 2 required)"
    if len(df.columns) == 0:
        return False, "DataFrame has no columns"
    return True, "OK"
```

### 4. Improve Column Name Handling

**In try1.py, add to load_data function:**
```python
# Clean column names (remove leading/trailing spaces)
if isinstance(df, pd.DataFrame):
    df.columns = df.columns.str.strip()
```

### 5. Add Caching for Performance

**In app.py, add caching decorator:**
```python
@st.cache_data
def load_and_cache_data(file_bytes, file_name):
    """Cache loaded data to avoid reprocessing on reruns."""
    bio = io.BytesIO(file_bytes)
    bio.name = file_name
    return load_data(bio)

# Then use it:
if uploaded:
    df = load_and_cache_data(uploaded.read(), uploaded.name)
```

## Medium Priority Enhancements

### 6. Add Unit Tests

**Create tests/test_try1.py:**
```python
import pytest
import pandas as pd
from try1 import suggest_prompts, prompt_to_code

def test_suggest_prompts():
    df = pd.DataFrame({'A': [1, 2, 3], 'B': ['x', 'y', 'z']})
    suggestions = suggest_prompts(df)
    assert len(suggestions) > 0
    assert isinstance(suggestions[0], str)

def test_prompt_to_code_summary():
    df = pd.DataFrame({'A': [1, 2, 3]})
    code = prompt_to_code("Summarize the dataset", df)
    assert code is not None
    assert "info" in code.lower()
```

### 7. Add Configuration File

**Create config.py:**
```python
"""Configuration settings for AI Data Analyst."""

# Analysis settings
MAX_SUGGESTIONS = 8
MAX_FILE_SIZE_MB = 200
DEFAULT_CHART_DPI = 150

# LLM settings
DEFAULT_LLM_MODEL = "llama3.1"
LLM_TIMEOUT = 60

# Display settings
PREVIEW_ROWS = 100
MAX_DISPLAY_ROWS = 1000

# Supported file types
SUPPORTED_EXTENSIONS = {
    'csv': 'CSV Files',
    'xlsx': 'Excel Files',
    'xls': 'Excel Files (Legacy)',
    'json': 'JSON Files',
    'docx': 'Word Documents',
    'pdf': 'PDF Files'
}
```

### 8. Enhanced Logging

**Add to try1.py:**
```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
logger = logging.getLogger(__name__)

# Use throughout code:
logger.info(f"Loading file: {file_name}")
logger.warning(f"Column type detection uncertain for: {col}")
logger.error(f"Execution failed: {e}")
```

### 9. Add Type Hints Throughout

**Example for try1.py functions:**
```python
from typing import Dict, List, Optional, Union
from pathlib import Path

def load_data(file_or_path: Union[str, Path, object]) -> pd.DataFrame:
    """Load data with type hints."""
    ...

def suggest_prompts(df: pd.DataFrame, max_suggestions: int = 8) -> List[str]:
    """Generate suggestions with type hints."""
    ...

def run_code(df: pd.DataFrame, code: str) -> Dict[str, any]:
    """Execute code with type hints."""
    ...
```

### 10. Add Documentation Strings

**Example for major functions:**
```python
def prompt_to_code(prompt: str, df: pd.DataFrame) -> Optional[str]:
    """
    Convert natural language prompts to executable Python code.
    
    This function uses pattern matching to identify common analysis
    requests and generates corresponding pandas/matplotlib code.
    
    Args:
        prompt: Natural language description of desired analysis
        df: Input DataFrame to analyze
        
    Returns:
        Python code as string if pattern matched, None otherwise
        
    Examples:
        >>> code = prompt_to_code("Show summary statistics", df)
        >>> code = prompt_to_code("Create histogram of 'price'", df)
        
    Notes:
        - Returns None for unrecognized patterns
        - Code assumes 'df' variable exists in execution context
        - Generated code should not call plt.show()
    """
    ...
```

## Advanced Enhancements

### 11. Add Data Export Options

**Add to app.py after results display:**
```python
if res["type"] == "dataframe":
    col1, col2, col3 = st.columns(3)
    with col1:
        csv = res["df"].to_csv(index=False)
        st.download_button("📥 CSV", csv, "result.csv", "text/csv")
    with col2:
        buffer = io.BytesIO()
        res["df"].to_excel(buffer, index=False)
        st.download_button("📥 Excel", buffer.getvalue(), "result.xlsx")
    with col3:
        json = res["df"].to_json(orient="records", indent=2)
        st.download_button("📥 JSON", json, "result.json")
```

### 12. Add Session State for History

**In app.py:**
```python
# Initialize session state
if 'analysis_history' not in st.session_state:
    st.session_state.analysis_history = []

# After successful analysis:
st.session_state.analysis_history.append({
    'prompt': final_prompt,
    'timestamp': datetime.now(),
    'result_type': res['type']
})

# Add sidebar history viewer:
with st.sidebar:
    if st.session_state.analysis_history:
        st.markdown("### Recent Analyses")
        for i, item in enumerate(reversed(st.session_state.analysis_history[-5:])):
            st.text(f"{i+1}. {item['prompt'][:50]}...")
```

### 13. Add Data Profiling Report

**Create new function in try1.py:**
```python
def generate_profile_report(df: pd.DataFrame) -> Dict[str, any]:
    """Generate comprehensive data profile."""
    return {
        'shape': df.shape,
        'memory_usage': df.memory_usage(deep=True).sum() / 1024**2,
        'duplicates': df.duplicated().sum(),
        'dtypes': df.dtypes.value_counts().to_dict(),
        'missing': df.isnull().sum().to_dict(),
        'numeric_summary': df.describe().to_dict() if len(df.select_dtypes(include=['number']).columns) > 0 else {}
    }
```

### 14. Add Better Error Messages

**Create error_messages.py:**
```python
ERROR_MESSAGES = {
    'file_too_large': '📊 File too large! Try:\n• Filtering data in Excel\n• Splitting into smaller files\n• Using CSV instead of Excel',
    'invalid_format': '❌ Invalid file format. Supported: CSV, Excel, JSON, DOCX, PDF',
    'parse_error': '⚠️ Could not parse file. Check:\n• File not corrupted\n• Correct encoding\n• Valid format',
    'llm_not_found': '🤖 Ollama not found. Install from https://ollama.com',
    'execution_error': '💥 Code execution failed. This might be due to:\n• Missing values\n• Incorrect column names\n• Data type issues'
}
```

### 15. Add Keyboard Shortcuts

**In app.py:**
```python
# Add keyboard shortcuts hint
st.sidebar.markdown("""
### ⌨️ Keyboard Shortcuts
- `Ctrl + Enter` - Run analysis
- `Ctrl + R` - Reload data
- `Ctrl + /` - Toggle sidebar
""")
```

## Code Quality Checklist

- [ ] Add type hints to all functions
- [ ] Write docstrings for all public functions
- [ ] Add unit tests (aim for 80% coverage)
- [ ] Set up pre-commit hooks (black, flake8, isort)
- [ ] Add input validation for all user inputs
- [ ] Implement proper logging
- [ ] Create configuration management
- [ ] Add performance monitoring
- [ ] Document all magic numbers
- [ ] Refactor long functions (keep under 50 lines)

## Pre-commit Hook Setup

**Create .pre-commit-config.yaml:**
```yaml
repos:
  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        language_version: python3.10
  
  - repo: https://github.com/pycqa/flake8
    rev: 6.0.0
    hooks:
      - id: flake8
        args: ['--max-line-length=120']
  
  - repo: https://github.com/pycqa/isort
    rev: 5.12.0
    hooks:
      - id: isort
```

Then run:
```bash
pip install pre-commit
pre-commit install
```

---

These improvements will make your code more maintainable, testable, and professional!