# Entire Field Player Scraper

This script scrapes player names and IDs from a specified URL and saves it to a CSV file. It uses Selenium with Chrome WebDriver to interact with a web page and extract information.

## Dependencies

- Python 3.x
- Selenium
- Chrome WebDriver
- webdriver_manager
- logging (built-in)
- csv (built-in)
- re (built-in)
- time (built-in)
- traceback (built-in)

## Configuration

1. Setting the URL:
You need a separate configuration file (typically named config.py) that contains a variable called CREATE_FIELD_URL. This variable should store the URL of the webpage from which the player data will be scraped.

2. Initializing Chrome WebDriver with Selenium 4:

   - Chrome Options Setup:
First, create and configure your Chrome options object. This involves setting any command-line flags or parameters you normally require (for example, disabling automation detection, starting the browser in maximized mode, disabling extensions, and specifying a user agent).

   - Using the Service Class:
Instead of your previous method, you should use the Service class from Selenium’s selenium.webdriver.chrome.service. Here’s how it works conceptually:

      - Use a ChromeDriver manager (like the one provided by webdriver_manager) to automatically install and return the correct path to the ChromeDriver executable.

      - Create a Service object using this path. This encapsulates the executable’s location and the necessary options to initialize it.

   - Instantiating the WebDriver:
Finally, create the Chrome WebDriver by passing in the Service object along with your previously configured Chrome options. This method ensures that you’re following the Selenium 4 API guidelines and avoids the error that comes from passing multiple values for the options argument.

## Script Overview

The script performs the following operations:

1. Sets up logging with the following configuration:
   - Log level: INFO
   - Format: Timestamp - Level - Message

2. Configures Chrome WebDriver with specific options:
   - Disables automation detection
   - Starts in maximized window
   - Disables infobars and extensions
   - Sets a specific user agent
   - Disables sandbox and dev-shm-usage

3. Main scraping process:
   - Initializes Chrome WebDriver
   - Navigates to the specified URL
   - Waits 5 seconds for initial page load
   - Locates player rows using CSS selector "tr[class^='player-']"
   - Processes each player row to extract:
     - Player ID (removes leading zeros)
     - Player name
   - Saves data to 'entire-field.csv'

## Error Handling

The script includes comprehensive error handling:
- Logs all errors with full traceback
- Captures and logs page source in case of errors
- Ensures proper cleanup of WebDriver resources

## Output

The script generates a CSV file named 'entire-field.csv' with the following columns:
- Player ID
- Full Name

## Detailed Process Flow

1. Script initialization:
   - Sets up logging
   - Configures Chrome options
   - Initializes WebDriver

2. Page interaction:
   - Navigates to target URL
   - Implements explicit wait (20 seconds) for player rows
   - Uses WebDriverWait for element presence

3. Data extraction:
   - Iterates through player rows
   - Extracts player ID using regex pattern 'player-(\d+)'
   - Removes leading zeros from player IDs
   - Extracts player names using CSS selector "span.chakra-text.css-hmig5c"

4. Data storage:
   - Creates CSV file with headers
   - Writes player data row by row
   - Uses UTF-8 encoding

5. Cleanup:
   - Properly closes WebDriver
   - Handles any remaining resources

## Logging Details

The script logs the following information:
- Chrome options setup
- WebDriver initialization
- URL navigation attempts
- Number of player rows found
- Individual row processing status
- Player ID and name extraction
- File writing operations
- Error details and stack traces
- Page source in case of errors

## CSS Selectors Used

- Player rows: "tr[class^='player-']"
- Player names: "span.chakra-text.css-hmig5c"

## Important Notes

1. The script requires Chrome browser to be installed
2. Internet connection is required for WebDriver initialization
3. The target website must be accessible
4. The script handles dynamic content loading with explicit waits
5. All errors are logged for debugging purposes

## Usage

In a python virtual environment, ensure all dependencies are installed, including:
`pip install selenium webdriver_manager`

1. Create config.py with CREATE_FIELD_URL
2. Run the script: `python 01_create_entire-field.py`
3. Check the generated entire-field.csv file
4. Monitor the console for logging output 