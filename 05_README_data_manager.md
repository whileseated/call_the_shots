# Data Manager

## Overview
Data Manager is a Python utility designed to handle player data in both CSV and JSON formats, specifically focused on every shot information. The module provides functions to load, parse, and extract specific shot details from data files.

## Requirements
- Python 3.x
- pandas library
- JSON_BASE_PATH configuration (must be defined in config.py)

## Core Functions

### load_player_data(csv_path)
A simple function that loads player data from a CSV file using pandas.

Parameters:
- csv_path: The file path to the CSV containing player data
Returns: A pandas DataFrame containing the player data

### get_player_json(player_id)
Retrieves and loads a player's JSON data file.

Parameters:
- player_id: The unique identifier for the player
Returns: The loaded JSON data as a Python dictionary, or None if there's an error

The function handles two potential errors:
- FileNotFoundError: When the JSON file doesn't exist
- JSONDecodeError: When the JSON file can't be properly parsed

### get_all_shots_info(player_id, round_selected, hole_selected)
Retrieves comprehensive information about all shots for a specific player, round, and hole.

Parameters:
- player_id: The unique identifier for the player
- round_selected: The round number to retrieve
- hole_selected: The hole number to retrieve
Returns: A list of dictionaries containing shot numbers and their highlight URLs

The function navigates through the JSON structure to find matching round and hole numbers, collecting shot information along the way.

### get_shots_for_hole(player_id, round_number, hole_number)
Retrieves detailed shot information for a specific hole.

Parameters:
- player_id: The unique identifier for the player
- round_number: The round number to retrieve
- hole_number: The hole number to retrieve
Returns: A list of shot data for the specified hole, or an empty list if not found

### list_available_shots(player_id, round_selected, hole_selected)
Creates a list of available shot numbers for a specific hole.

Parameters:
- player_id: The unique identifier for the player
- round_selected: The round number to check
- hole_selected: The hole number to check
Returns: A list of shot numbers (as strings) available for the specified hole

### get_highlight_url(player_id, round_selected, hole_selected, shot_number)
Retrieves the highlight video URL for a specific shot.

Parameters:
- player_id: The unique identifier for the player
- round_selected: The round number containing the shot
- hole_selected: The hole number containing the shot
- shot_number: The specific shot number to retrieve
Returns: The highlight URL as a string, or "URL not found or invalid path" if not found

## Data Structure
The module expects JSON files to follow a specific structure:
- round (array)
  - id (string): round number
  - hole (array)
    - id (string): hole number
    - shot (array)
      - num (string): shot number
      - highlightURL (string): URL to the shot video

## File Organization
- JSON files should be named as "{player_id}.json"
- JSON files should be located in the directory specified by JSON_BASE_PATH
- CSV files can be located anywhere but must be specified with full path

## Error Handling
The module includes basic error handling for:
- Missing JSON files
- Invalid JSON format
- Missing or invalid data paths within the JSON structure
- Non-existent rounds, holes, or shots

## Usage Notes
- All numeric parameters (round_selected, hole_selected, shot_number) are converted to strings when searching the JSON
- Empty lists or error messages are returned when data isn't found, preventing crashes
- The module assumes the JSON_BASE_PATH is properly configured in config.py