# Contributing Guidelines

Thank you for your interest in contributing to the SIR Epidemic Model project! This is an academic project for the DSTT G5 course (AM609L).

## How to Contribute

### Reporting Issues
- Use the GitHub Issues tab to report bugs or suggest enhancements
- Provide clear steps to reproduce any issues
- Include relevant environment information (Python version, OS, etc.)

### Code Contributions
1. Fork the repository
2. Create a new branch for your feature/fix: `git checkout -b feature/your-feature-name`
3. Make your changes with clear, descriptive commit messages
4. Ensure all tests pass and the notebook runs without errors
5. Submit a Pull Request with a clear description of changes

### Notebook Standards
- Keep notebook cells organized with clear markdown headers
- Use relative paths for data files (e.g., `Data/india_covid_cleaned.csv`)
- Include comments explaining complex calculations
- Ensure outputs are saved in the notebook for reproducibility

### Data Files
- Do not commit large raw data files (>50MB) directly
- Use Git LFS for large files if necessary
- Document data sources and preprocessing steps

## Development Setup

```bash
# Clone your fork
git clone https://github.com/yourusername/SIR-Epidemic-Model.git
cd SIR-Epidemic-Model

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start Jupyter
jupyter notebook
```

## Code Style

- Follow PEP 8 for Python code
- Use descriptive variable names
- Add type hints where appropriate
- Document functions with docstrings

## Questions?

Feel free to open an issue for any questions about contributing!