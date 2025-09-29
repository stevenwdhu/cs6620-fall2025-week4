# CI/CD with GitHub Actions

This repository contains a simple Python calculator application with **intentional linting errors**. Your task is to fix these errors and make the CI pipeline pass successfully.

## Step 1: Fork and Clone the Repository

1. Fork this repository to your GitHub account by clicking the "Fork" button
2. Clone your forked repository to your local machine

## Step 2: Add YAML File

1. Go to your forked repository on GitHub
2. Click on the "Actions" tab
3. Click on "Simple workflow"
4. Replace the default content with the following YAML configuration:
   ```yaml
   name: Python CI with Linting

   on:
     push:
       branches: [ main, develop ]
     pull_request:
       branches: [ main, develop ]

   jobs:
     lint:
       runs-on: ubuntu-latest
       
       steps:
       - name: Checkout code
         uses: actions/checkout@v4
       
       - name: Set up Python
         uses: actions/setup-python@v4
         with:
           python-version: '3.11'
       
       - name: Install dependencies
         run: |
           python -m pip install --upgrade pip
           pip install flake8 pylint
       
       - name: Lint with flake8
         run: |
           # Stop the build if there are Python syntax errors or undefined names
           flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
           # Exit with error on any linting issues
           flake8 . --count --max-line-length=127 --statistics
       
       - name: Lint with pylint
         run: |
           pylint app.py --fail-under=8.0
   ```

5. Name the file `ci.yml` 
6. Click "Commit changes" to commit directly to the main branch
7. Watch the CI pipeline run and **fail**

## Step 3: Identify Linting Errors

1. Click on the failed workflow in the "Actions" tab
2. Review the CI logs to identify what linting errors exist in `app.py`
3. Take note of all the errors reported by flake8 and pylint

## Step 4: Create a New Branch

1. Pull the latest changes from your repository:
2. Create and switch to a new branch called `fix-lint-errors`:


## Step 5: Fix the Linting Errors

1. Open `app.py` in your editor
2. Fix all the linting errors identified by flake8 and pylint
3. Save your changes

## Step 6: Commit and Push Your Fixes

1. Add and commit your changes
2. Push the branch to your GitHub repository


## Step 7: Create a Pull Request

1. Go to your repository on GitHub
2. You should see a notification to create a Pull Request for your `fix-lint-errors` branch
3. Click "Compare & pull request"
4. Add a description of what you fixed
5. Click "Create pull request"

## Step 8: Observe the CI Pipeline

1. On the Pull Request page, watch the CI pipeline run
2. Verify the pipeline passes successfully with a green checkmark ✅
3. Once the checks pass, click "Merge pull request"
4. Click "Confirm merge" to merge your changes into the main branch

## 📝 Submission Requirements

Submit the following:

1. **GitHub Repository URL**: Link to your forked repository
2. **Screenshot**: Capture of the successful CI pipeline run (green checkmark on PR page)
