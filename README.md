# Automated Data Scraping Tool

This tool automatically scrapes pricing data from websites and runs on GitHub Actions for cloud execution.

## Setup Instructions

### 1. Repository Setup
1. Create a new GitHub repository
2. Upload all files from this directory to the repository
3. Ensure you have the following files:
   - `main.py` (your scraping script)
   - `urls with titles.csv` (input data)
   - `.github/workflows/scraper.yml` (GitHub Actions workflow)
   - `requirements.txt` (Python dependencies)

### 2. Configure Secrets

#### For Local Development:
1. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```
2. Edit `.env` with your actual values:
   ```bash
   # Get your API key from: https://openrouter.ai/keys
   OPENROUTER_API_KEY="sk-or-v1-your-actual-api-key-here"
   YOUR_SITE_URL="https://your-website.com"
   YOUR_SITE_NAME="Your Site Name"
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Run locally:
   ```bash
   python main.py
   ```

The script will automatically detect and load the `.env` file for local development.

#### For GitHub Actions:
Go to your GitHub repository → Settings → Secrets and variables → Actions

Add the following repository secrets:
- `OPENROUTER_API_KEY`: Your OpenRouter API key
- `YOUR_SITE_URL`: Your website URL (e.g., https://appsisi.com)
- `YOUR_SITE_NAME`: Your site name (e.g., appsi)

### 3. Running the Scraper

#### Manual Trigger:
1. Go to your repository
2. Click on "Actions" tab
3. Select "Data Scraping Automation" workflow
4. Click "Run workflow" button

#### Automatic Schedule (Optional):
Uncomment the schedule section in `.github/workflows/scraper.yml` to run automatically:
```yaml
schedule:
  - cron: '0 9 * * 1'  # Every Monday at 9 AM UTC
```

### 4. Accessing Results

After the workflow completes:
1. Go to the "Actions" tab
2. Click on the completed workflow run
3. Download the "scraping-results" artifact
4. The results will also be automatically committed to your repository

## Files

- `main.py`: Main scraping script
- `urls with titles.csv`: Input CSV with URLs to scrape
- `pricing_results_with_resume.json`: Output JSON with scraped data
- `requirements.txt`: Python dependencies
- `.github/workflows/scraper.yml`: GitHub Actions workflow configuration

## Features

- **Smart Environment Handling**: Automatically detects local `.env` file or GitHub Actions secrets
- **Environment Validation**: Validates all required environment variables before starting
- **Cloud Execution**: Runs on GitHub's servers, no need to keep your laptop running
- **Resume Capability**: Can resume from where it left off if interrupted
- **Automatic Results**: Results are saved as artifacts and committed to repository
- **Secure**: API keys stored as encrypted GitHub secrets or local `.env` file (never committed)
- **Manual/Scheduled**: Can run on-demand or on a schedule
- **Intelligent AI Processing**: Uses AI to find and extract pricing information from websites

## Notes

- The workflow has a timeout to prevent infinite running
- Results are kept for 30 days as artifacts
- The script includes rate limiting to be respectful to target websites
- All output is logged in the GitHub Actions console