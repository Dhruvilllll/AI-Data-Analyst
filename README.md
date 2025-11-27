# 🧠 Personal AI Data Analyst

> Transform your data into insights with AI-powered analysis and interactive visualizations

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28%2B-FF4B4B.svg)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

<p align="center">
  <img src="assets/demo.gif" alt="Demo" width="800">
</p>

## ✨ Features

- **📊 Multi-Format Support** - Upload CSV, Excel, JSON, DOCX, or PDF files
- **🤖 Smart Suggestions** - Automatically generates relevant analysis prompts based on your data
- **🎯 Deterministic Analysis** - Built-in templates for common data operations (no LLM required)
- **🦙 LLM Integration** - Optional local LLM support via Ollama for custom queries
- **📈 Interactive Visualizations** - Automatic chart generation with matplotlib
- **⚡ Real-Time Execution** - See results instantly with code execution sandbox
- **💾 Export Results** - Download analysis results as CSV files

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- pip package manager
- (Optional) [Ollama](https://ollama.com) for LLM-powered custom queries

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ai-data-analyst.git
   cd ai-data-analyst
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the application**
   ```bash
   streamlit run app.py
   ```

4. **Open your browser** to `http://localhost:8501`

### Optional: Set Up Local LLM

For custom prompt support, install Ollama:

```bash
# macOS/Linux
curl -fsSL https://ollama.com/install.sh | sh

# Pull a model
ollama pull llama3.1
```

## 📖 Usage

### Basic Workflow

1. **Upload Your Data** - Drag and drop or select a file (CSV, Excel, JSON, DOCX, PDF)
2. **Review Suggestions** - The app automatically suggests relevant analyses
3. **Run Analysis** - Click "Run analysis" to execute and see results
4. **Export Results** - Download tables as CSV or save visualizations

### Example Analyses

**Automatic Suggestions Include:**
- Dataset summaries with key statistics
- Top value counts for categorical columns
- Correlation heatmaps for numeric data
- Time series analysis for datetime columns
- Anomaly detection using z-scores
- Custom visualizations (histograms, scatter plots)

### Custom Queries with LLM

Enable "Use local LLM" in the sidebar to write custom analysis prompts:

```
"Show me the relationship between sales and marketing spend by region"
"Find products with declining sales over the last 6 months"
"Create a bar chart comparing revenue across all categories"
```

## 🏗️ Architecture

```
┌─────────────────┐
│   Streamlit UI  │
└────────┬────────┘
         │
    ┌────▼────────────────────────────┐
    │     Prompt Processing Layer     │
    │  ┌──────────┐    ┌───────────┐ │
    │  │Template  │    │  Ollama   │ │
    │  │ Matching │    │  LLM API  │ │
    │  └──────────┘    └───────────┘ │
    └────────┬────────────────────────┘
             │
    ┌────────▼────────────────────────┐
    │   Code Execution Engine         │
    │   (Sandboxed Python Runtime)    │
    └────────┬────────────────────────┘
             │
    ┌────────▼────────────────────────┐
    │   Result Formatting             │
    │   • Tables  • Charts  • Text    │
    └─────────────────────────────────┘
```

## 🛠️ Technology Stack

- **Frontend**: Streamlit
- **Data Processing**: Pandas, NumPy
- **Visualization**: Matplotlib
- **Document Parsing**: python-docx, pypdf
- **LLM Integration**: Ollama (optional)
- **Statistical Analysis**: SciPy

## 📂 Project Structure

```
ai-data-analyst/
├── app.py                 # Main Streamlit application
├── try1.py               # Core logic (data loading, analysis, execution)
├── requirements.txt      # Python dependencies
├── README.md            # This file
├── LICENSE              # MIT License
├── .gitignore           # Git ignore rules
├── assets/              # Screenshots and demo files
│   ├── demo.gif
│   └── screenshot.png
└── examples/            # Sample datasets
    ├── sales_data.csv
    └── customer_data.xlsx
```

## 🎯 Supported Analysis Types

| Analysis Type | Description | LLM Required |
|--------------|-------------|--------------|
| Dataset Summary | Rows, columns, types, missing values | ❌ |
| Top Counts | Most frequent values in categorical columns | ❌ |
| Statistics | Mean, median, std dev for numeric columns | ❌ |
| Histograms | Distribution visualization | ❌ |
| Scatter Plots | Relationship between two variables | ❌ |
| Time Series | Trends over time | ❌ |
| Correlation | Heatmap of numeric correlations | ❌ |
| Anomaly Detection | Z-score based outlier detection | ❌ |
| Custom Queries | Natural language to code | ✅ |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Streamlit](https://streamlit.io/)
- LLM integration powered by [Ollama](https://ollama.com)
- Inspired by the need for accessible data analysis tools

## 📧 Contact

Your Name - [@yourtwitter](https://twitter.com/yourtwitter)

Project Link: [https://github.com/yourusername/ai-data-analyst](https://github.com/yourusername/ai-data-analyst)

---

<p align="center">Made with ❤️ and Python</p>
