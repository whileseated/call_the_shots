# Call The Shots

## Overview
Call The Shots is a Python application designed to allow users to select and view every shot videos. The application provides an interactive console interface for users to select a player, round, hole, and specific shot, then downloads and plays the corresponding video.

## Key Dependencies
The script relies on several custom modules:

```python
from ui_components import autocomplete_player, select_round, select_hole, select_shot  
from data_manager import get_shots_for_hole  
from video_manager import download_video, play_video  
from config import JSON_BASE_PATH
```

## Main Functionality
The application is built around a single `main()` function that orchestrates the entire workflow, from player selection to video playback.

### Player Selection System
The application begins by calling `autocomplete_player()` from the ui_components module. This function:
1. Presents the user with an autocomplete interface for selecting a player
2. Returns two values: the player's full name (as a string) and the player's unique ID (as a string or integer)
3. The returned player name is then formatted by replacing spaces with underscores using the `.replace(' ', '_')` method
4. The player ID is stored for later use in retrieving the player's shot data

### Round Selection System
After player selection, the application calls `select_round()` from the ui_components module. This function:
1. Presents the user with a menu of available rounds
2. Returns a single value representing the selected round number
3. The round number is stored as the variable `round_selected` for subsequent operations

### Hole Selection System
Following round selection, the application calls `select_hole()` from the ui_components module. This function:
1. Presents the user with a menu of holes available for the previously selected round
2. Returns a single value representing the selected hole number
3. The hole number is stored as the variable `hole_selected` for subsequent operations

### Shot Data Retrieval
The application then retrieves shot data by calling `get_shots_for_hole(player_id, round_selected, hole_selected)` from the data_manager module. This function:
1. Uses the previously collected player_id, round_selected, and hole_selected values to locate the relevant shot data
2. Returns a list of dictionaries, where each dictionary contains information about a specific shot
3. Each shot dictionary must include at least:
   - A 'num' key containing the shot number as a string
   - A 'highlightURL' key containing the URL to the video of that shot

### Shot Selection System
If shot data is successfully retrieved, the application then:
1. Creates a list of descriptive strings for each shot (format: "Shot {shot_number}")
2. Only includes shots that have a non-empty 'highlightURL' value
3. Calls `select_shot(shot_descriptions)` from the ui_components module, passing the list of shot descriptions
4. This function presents the user with a menu of available shots and returns the selected shot description
5. The application then extracts the shot number from the returned description by splitting the string and taking the second element

### Video Retrieval and Playback
After a shot is selected, the application:
1. Finds the complete shot information by searching through the previously retrieved shots data
2. Constructs an INITIAL filename in the format: "{formatted_player_name}_{player_id}_{round_selected}_{hole_selected}_{shot_number}.mp4"
3. Calls `download_video(url, filename)` from the video_manager module to download the video

   **EXTREMELY IMPORTANT - FILENAME TRANSFORMATION:**
   - The `download_video` function internally transforms the filename completely:
     - It downloads using the original filename passed as an argument
     - Then it RENAMES the file to a DIFFERENT format: "{lastname}_round{round}_hole{hole}_shot{shot}.mp4"
     - For example, an input filename of "Francis_Ouimet_28237_3_3_3.mp4" becomes "McIlroy_round3_hole3_shot3.mp4"
     - The function RETURNS this NEW filename as its return value
   
4. The return value from `download_video` MUST be captured in a variable:
   ```
   downloaded_file = download_video(shot_data['highlightURL'], filename)
   ```

5. If download is successful (downloaded_file is not None):
   - Prompt the user with "Play file? (Y/N): "
   - If the user enters 'Y' (case-insensitive), call `play_video` USING THE NEW FILENAME:
   ```
   play_video(downloaded_file)  # Use the returned filename, NOT the original!
   ```
   
   **CRITICAL ERROR PREVENTION:**
   - NEVER pass the original filename to `play_video`
   - ALWAYS use the filename returned by `download_video`
   - Example of CORRECT usage:
     ```
     filename = "Francis_Ouimet_28237_3_3_3.mp4"  # Original filename
     downloaded_file = download_video(url, filename)  # Returns "McIlroy_round3_hole3_shot3.mp4"
     play_video(downloaded_file)  # CORRECT: Uses "McIlroy_round3_hole3_shot3.mp4"
     ```
   - Example of INCORRECT usage:
     ```
     filename = "Francis_Ouimet_28237_3_3_3.mp4"  # Original filename
     download_video(url, filename)  # Return value ignored!
     play_video(filename)  # WRONG: Uses original "Francis_Ouimet_28237_3_3_3.mp4"
     ```

### Error Handling
The application includes error handling for several scenarios:
1. If no shots are available for the selected hole, displays "No shots available for this hole."
2. If the selected shot doesn't have a valid URL, displays "No valid URL available for the selected shot."
3. If the video download fails (download_video returns None), displays "Failed to download the video."
4. If the video file cannot be found for playback with the error "No such file or directory", this is almost certainly because you're using the wrong filename - verify that you're using the filename returned by download_video, not the original filename.

## Program Flow
The complete flow of the application is as follows:
1. Select player (with autocomplete functionality)
2. Select round from available options
3. Select hole from available options
4. Retrieve shot information for the selected hole
5. Display available shots to the user
6. Select a specific shot to view
7. Download the video for the selected shot: 
   - Create an initial filename with player details and IDs
   - Pass this to download_video
   - STORE THE RETURNED NEW FILENAME in a variable (this is a completely different filename!)
8. Optionally play the downloaded video using the NEW filename returned by download_video, never the original filename

## Configuration
The application uses a JSON_BASE_PATH constant imported from a config module, which should specify the location of player data JSON files.

## Execution
The script is designed to be run directly as a Python module. When executed, it immediately calls the main() function.