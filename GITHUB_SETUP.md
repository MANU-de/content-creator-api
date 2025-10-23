# GitHub Setup Guide

This guide will help you upload your Content Creator API project to GitHub while excluding sensitive files.

## What's Included in the Repository

✅ **Included Files:**
- `main.py` - FastAPI application
- `agent.py` - CrewAI agents
- `test_*.py` - Comprehensive test suite
- `conftest.py` - Test configuration
- `run_tests.py` - Test runner script
- `requirements.txt` - Production dependencies
- `requirements-test.txt` - Test dependencies
- `pytest.ini` - Pytest configuration
- `README.md` - Project documentation
- `TEST_README.md` - Testing documentation
- `.gitignore` - Git ignore rules

❌ **Excluded Files (Protected by .gitignore):**
- `venv/` - Virtual environment
- `__pycache__/` - Python cache files
- `.pytest_cache/` - Pytest cache
- `.env` - Environment variables (sensitive)
- `*.log` - Log files
- `test_report.html` - Test reports
- `htmlcov/` - Coverage reports

## Step-by-Step GitHub Upload

### Step 1: Create a GitHub Repository

1. Go to [GitHub.com](https://github.com) and sign in
2. Click the "+" icon in the top right corner
3. Select "New repository"
4. Fill in the repository details:
   - **Repository name**: `content-creator-api`
   - **Description**: `AI-powered content creation API using FastAPI and CrewAI`
   - **Visibility**: Choose Public or Private
   - **Initialize**: ❌ Do NOT check "Add a README file" (we already have one)
   - **Initialize**: ❌ Do NOT check "Add .gitignore" (we already have one)
   - **Initialize**: ❌ Do NOT check "Choose a license" (optional)
5. Click "Create repository"

### Step 2: Connect Local Repository to GitHub

Run these commands in your project directory:

```bash
# Add the GitHub repository as remote origin
git remote add origin https://github.com/YOUR_USERNAME/content-creator-api.git

# Push the main branch to GitHub
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.

### Step 3: Verify Upload

1. Go to your repository on GitHub
2. Verify that all files are present
3. Check that sensitive files are NOT visible:
   - No `venv/` folder
   - No `__pycache__/` folders
   - No `.env` file
   - No `.pytest_cache/` folder

## Alternative: Using GitHub CLI

If you have GitHub CLI installed:

```bash
# Create repository and push in one command
gh repo create content-creator-api --public --source=. --remote=origin --push
```

## Repository Structure on GitHub

Your GitHub repository will have this clean structure:

```
content-creator-api/
├── .gitignore
├── README.md
├── TEST_README.md
├── main.py
├── agent.py
├── test_main.py
├── test_agent.py
├── test_integration.py
├── conftest.py
├── run_tests.py
├── pytest.ini
├── requirements.txt
├── requirements-test.txt
└── GITHUB_SETUP.md
```

## Security Checklist

Before pushing, ensure these sensitive files are excluded:

- [ ] `.env` file (contains API keys)
- [ ] `venv/` directory (virtual environment)
- [ ] `__pycache__/` directories (Python cache)
- [ ] `.pytest_cache/` directory (test cache)
- [ ] Any log files
- [ ] Any temporary files

## Next Steps After Upload

1. **Add Environment Variables**: Set up GitHub Secrets for CI/CD
2. **Enable GitHub Actions**: For automated testing
3. **Add License**: Consider adding a LICENSE file
4. **Set up Issues**: Enable issue tracking
5. **Add Collaborators**: If working with a team

## GitHub Actions Setup (Optional)

Create `.github/workflows/test.yml` for automated testing:

```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - name: Install dependencies
        run: |
          pip install -r requirements-test.txt
      - name: Run tests
        run: |
          python -m pytest
```

## Troubleshooting

### If you get authentication errors:
```bash
# Use personal access token instead of password
git remote set-url origin https://YOUR_TOKEN@github.com/YOUR_USERNAME/content-creator-api.git
```

### If you need to update the repository:
```bash
# After making changes
git add .
git commit -m "Update: description of changes"
git push origin main
```

### If you need to remove sensitive files that were accidentally committed:
```bash
# Remove from Git but keep locally
git rm --cached .env
git rm --cached -r venv/
git rm --cached -r __pycache__/
git commit -m "Remove sensitive files"
git push origin main
```

## Repository Settings

After creating the repository, consider these settings:

1. **Branch Protection**: Protect the main branch
2. **Issues**: Enable issue tracking
3. **Wiki**: Enable if needed
4. **Discussions**: Enable for community interaction
5. **Security**: Enable security alerts

Your Content Creator API is now ready for GitHub! 🚀
