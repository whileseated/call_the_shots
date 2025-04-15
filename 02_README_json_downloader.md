# JSON Downloader Script Documentation

## Overview
This script `02_json_downloader.py` is designed to download JSON data for multiple players from a specified URL. It reads player IDs from a CSV file and systematically downloads corresponding JSON data for each player, saving the results to individual JSON files.

## Dependencies
The script requires the following Python packages:
- requests: For making HTTP requests to download JSON data
- csv: For reading player IDs from a CSV file
- time: For implementing delays between requests

## Configuration Requirements
The script expects the following configuration variables to be defined in a config.py file:
- CSV_FILE_PATH: Path to the CSV file containing player IDs
- JSON_BASE_PATH: Base directory where downloaded JSON files will be saved
- JSON_URL: URL template for downloading player data (should contain a {number} placeholder for the player ID)

## Function Descriptions

### download_json(url, filename)
This function handles the actual downloading of JSON data for a single player.

Parameters:
- url: The complete URL from which to download the JSON data
- filename: The local path where the JSON data should be saved

Functionality:
1. Makes an HTTP GET request to the specified URL with a 10-second timeout
2. Uses a custom User-Agent header to identify the request
3. Checks the response status code
4. If successful (status code 200):
   - Saves the JSON data to the specified file
   - Prints a success message
5. If unsuccessful:
   - Prints an error message with the status code
   - If available, displays the first 200 characters of the response content
6. Handles various exceptions:
   - Timeout errors
   - Connection errors
   - General request exceptions

### get_field_numbers(csv_file)
This function reads player IDs from a CSV file.

Parameters:
- csv_file: Path to the CSV file containing player IDs

Functionality:
1. Opens and reads the specified CSV file
2. Extracts the 'Player ID' column from each row
3. Returns a list of all player IDs found
4. Handles potential errors:
   - File not found errors
   - General exceptions during file reading
5. Prints status messages about the number of players found

### main()
This is the primary function that orchestrates the entire download process.

Functionality:
1. Retrieves player IDs from the CSV file using get_field_numbers()
2. If no player IDs are found, exits the program
3. For each player ID:
   - Constructs the download URL using the JSON_URL template
   - Creates a filename using the JSON_BASE_PATH and player ID
   - Calls download_json() to download and save the data
   - Implements a 1-second delay between requests to be server-friendly
4. Prints progress information including:
   - Current player being processed
   - Total number of players
   - Player ID
5. Displays a completion message when all downloads are finished

## Error Handling
The script implements comprehensive error handling for:
- Network-related issues (timeouts, connection errors)
- File operations (file not found, read errors)
- HTTP request failures
- General exceptions

## Output
The script provides detailed console output including:
- Progress indicators
- Success/failure messages
- Error details when issues occur
- Status updates for each operation

## Usage Notes
1. Ensure the config.py file exists with the required variables
2. The CSV file must contain a 'Player ID' column
3. The script creates individual JSON files for each player
4. A 1-second delay between requests helps prevent server overload
5. The script uses a custom User-Agent header to identify requests

## Best Practices
- The script implements polite downloading with delays between requests
- Comprehensive error handling ensures graceful failure
- Clear status messages help track progress
- File operations use proper context managers
- Network requests include timeouts for reliability 