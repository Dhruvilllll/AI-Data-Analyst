# Contributing to AI Data Analyst

Thank you for considering contributing to the AI Data Analyst project! 🎉

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the existing issues to avoid duplicates. When you create a bug report, include as many details as possible:

- **Use a clear and descriptive title**
- **Describe the exact steps to reproduce the problem**
- **Provide specific examples** (sample data files if applicable)
- **Describe the behavior you observed and what you expected**
- **Include screenshots** if relevant
- **Note your environment**: OS, Python version, package versions

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion:

- **Use a clear and descriptive title**
- **Provide a detailed description of the suggested enhancement**
- **Explain why this enhancement would be useful**
- **List examples of how it would be used**

### Pull Requests

1. Fork the repo and create your branch from `main`
2. If you've added code that should be tested, add tests
3. Ensure your code follows the existing style
4. Update documentation as needed
5. Write clear, descriptive commit messages
6. Submit your pull request!

## Development Setup

```bash
# Clone your fork
git clone https://github.com/your-username/ai-data-analyst.git
cd ai-data-analyst

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the app
streamlit run app.py
```

## Code Style Guidelines

- Follow PEP 8 style guide for Python code
- Use meaningful variable and function names
- Add comments for complex logic
- Keep functions focused and single-purpose
- Add docstrings to functions and classes

## Adding New Analysis Templates

To add a new deterministic analysis template:

1. Add a suggestion in `suggest_prompts()` function in `try1.py`
2. Add pattern matching logic in `prompt_to_code()` function
3. Test with sample data
4. Update README.md with the new capability

## Questions?

Feel free to open an issue with your question or reach out to the maintainers.

Thank you for contributing! 🙌