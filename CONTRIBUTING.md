# Contributing to Weather Data Analysis Project

Thank you for considering contributing to this project! Here are some guidelines to help you get started.

## How to Contribute

### Reporting Bugs

If you find a bug, please open an issue with:
- A clear, descriptive title
- Detailed steps to reproduce the bug
- Expected vs actual behavior
- Your environment (OS, Python version, etc.)
- Screenshots if applicable

### Suggesting Enhancements

Enhancement suggestions are welcome! Please open an issue with:
- A clear description of the enhancement
- Use cases and benefits
- Possible implementation approach (optional)

### Pull Requests

1. **Fork the repository** and create your branch from `main`
2. **Make your changes**:
   - Follow the existing code style
   - Add comments for complex logic
   - Update documentation if needed
3. **Test your changes**:
   - Ensure notebooks run without errors
   - Verify data processing produces expected results
4. **Commit your changes**:
   - Use clear, descriptive commit messages
   - Reference issues if applicable (e.g., "Fixes #123")
5. **Submit a pull request**:
   - Describe what changes you made and why
   - Link to related issues

## Code Style

- Follow PEP 8 guidelines for Python code
- Use meaningful variable names
- Add docstrings for functions
- Keep functions focused and modular
- Comment complex logic

## Development Setup

1. Clone your fork:
```bash
git clone https://github.com/your-username/repository-name.git
cd repository-name
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Create a new branch:
```bash
git checkout -b feature/your-feature-name
```

## Testing

- Test notebooks end-to-end before submitting
- Verify that data processing produces consistent results
- Check that visualizations render correctly

## Areas for Contribution

Some ideas for contributions:
- Additional weather metrics and indices
- Support for other Brazilian states
- Alternative ML models (ARIMA, Prophet, etc.)
- Performance optimizations
- Better error handling
- More comprehensive documentation
- Unit tests
- Data validation utilities

## Questions?

Feel free to open an issue with the "question" label if you need help or clarification.

## Code of Conduct

- Be respectful and inclusive
- Welcome newcomers and beginners
- Focus on constructive feedback
- Maintain a positive, collaborative environment

Thank you for contributing! 🎉
