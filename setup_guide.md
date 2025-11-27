# 📚 Detailed Setup Guide

This guide will walk you through setting up the AI Data Analyst on your local machine.

## Table of Contents
- [System Requirements](#system-requirements)
- [Installation Methods](#installation-methods)
- [Troubleshooting](#troubleshooting)
- [Advanced Configuration](#advanced-configuration)

## System Requirements

### Minimum Requirements
- **OS**: Windows 10/11, macOS 10.15+, or Linux
- **Python**: 3.8 or higher
- **RAM**: 4GB minimum (8GB recommended)
- **Disk Space**: 500MB for dependencies

### Recommended Requirements
- **Python**: 3.10 or higher
- **RAM**: 8GB or more
- **Disk Space**: 2GB (includes space for Ollama models if using LLM features)

## Installation Methods

### Method 1: Standard Installation (Recommended)

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/ai-data-analyst.git
cd ai-data-analyst

# 2. Create a virtual environment
python -m venv venv

# 3. Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# 4. Install dependencies
pip install -r requirements.txt

# 5. Run the application
streamlit run app.py
```

### Method 2: Using Conda

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/ai-data-analyst.git
cd ai-data-analyst

# 2. Create conda environment
conda create -n data-analyst python=3.10
conda activate data-analyst

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the application
streamlit run app.py
```

### Method 3: Docker (Coming Soon)

Docker support is planned for future releases.

## Setting Up LLM Features (Optional)

### Installing Ollama

**macOS:**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Linux:**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Windows:**
Download and install from [ollama.com](https://ollama.com)

### Pulling Models

```bash
# Recommended model (balanced performance)
ollama pull llama3.1

# Other options
ollama pull mistral
ollama pull codellama
ollama pull phi
```

### Verifying Ollama Installation

```bash
# Check if ollama is running
ollama list

# Test a model
ollama run llama3.1 "Hello, world!"
```

## First Run

1. **Start the application:**
   ```bash
   streamlit run app.py
   ```

2. **Access the web interface:**
   - Your browser should open automatically
   - If not, navigate to `http://localhost:8501`

3. **Upload test data:**
   - Try the sample CSV in `examples/` folder
   - Or upload your own data file

4. **Run an analysis:**
   - Select a suggested prompt
   - Click "Run analysis"
   - View your results!

## Troubleshooting

### Common Issues

**Issue: `ModuleNotFoundError`**
```bash
# Solution: Ensure all dependencies are installed
pip install -r requirements.txt
```

**Issue: Streamlit won't start**
```bash
# Solution: Check if port 8501 is available
# Try running on a different port
streamlit run app.py --server.port 8502
```

**Issue: Ollama not found**
```bash
# Solution: Add Ollama to PATH
# macOS/Linux: Add to ~/.bashrc or ~/.zshrc
export PATH=$PATH:/usr/local/bin

# Windows: Add Ollama installation directory to System PATH
```

**Issue: Memory errors with large files**
- Solution: Use a system with more RAM or process smaller data chunks
- Consider sampling your dataset before analysis

**Issue: Charts not displaying**
```bash
# Solution: Reinstall matplotlib
pip uninstall matplotlib
pip install matplotlib
```

### Getting Help

If you encounter issues not listed here:

1. Check [existing GitHub issues](https://github.com/yourusername/ai-data-analyst/issues)
2. Create a new issue with:
   - Detailed error messages
   - Steps to reproduce
   - Your environment details (OS, Python version)
3. Join discussions in the repository

## Advanced Configuration

### Customizing Streamlit Settings

Create `.streamlit/config.toml`:

```toml
[theme]
primaryColor = "#FF4B4B"
backgroundColor = "#FFFFFF"
secondaryBackgroundColor = "#F0F2F6"
textColor = "#262730"
font = "sans serif"

[server]
port = 8501
enableCORS = false
enableXsrfProtection = true

[browser]
gatherUsageStats = false
```

### Environment Variables

Create a `.env` file for custom settings:

```bash
OLLAMA_HOST=http://localhost:11434
DEFAULT_MODEL=llama3.1
MAX_FILE_SIZE_MB=200
```

### Performance Tuning

For large datasets:

1. Increase memory limits in Streamlit config
2. Use data sampling for preview
3. Enable caching for repeated operations

## Next Steps

- Read the [Usage Guide](README.md#usage)
- Explore [Contributing Guidelines](CONTRIBUTING.md)
- Check out [Example Notebooks](examples/)

---

Need more help? Open an issue on GitHub!