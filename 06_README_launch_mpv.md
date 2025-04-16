# MPV Video Player Launcher

## Overview
This bash script provides an automated way to launch the MPV video player with dynamically calculated window dimensions based on the current terminal size. The script ensures that videos are displayed in a window that fits comfortably within the terminal dimensions while maintaining proper aspect ratio.

## Requirements
- Unix-like operating system (Linux/MacOS)
- MPV media player installed
- bash shell
- tput command available (typically included in ncurses package)

## Technical Details

### Character Dimensions
The script uses fixed character dimensions for calculations:
- Character width: 19 pixels
- Character height: 32 pixels

These values are used as baseline measurements for converting terminal character spaces into pixel dimensions.

### Terminal Size Detection
The script automatically detects the current terminal dimensions using:
- tput cols: retrieves the number of columns
- tput lines: retrieves the number of lines

### Window Size Calculation
The script performs the following calculations to determine the video window size:
1. Multiplies the terminal columns by the character width (19 pixels)
2. Multiplies the terminal lines by the character height (32 pixels)
3. Subtracts 40 pixels from both width and height as padding
This ensures the video window fits within the terminal with comfortable margins.

### MPV Configuration
The script launches MPV with specific parameters:
- --no-border: Removes the window border for a cleaner appearance
- --autofit: Sets the window size based on the calculated dimensions

## Usage
The script should be:
1. Made executable (chmod +x launch_mpv.sh)
2. Called with a single argument representing the video file path
Example: ./launch_mpv.sh video_file.mp4

## File Permissions
The script must have executable permissions to function properly. Use:
chmod +x launch_mpv.sh

## Error Handling
While the script itself doesn't include explicit error handling, it relies on MPV's built-in error handling for invalid files or incorrect parameters.

## Notes
- The script assumes a standard terminal font size and spacing
- The 40-pixel reduction is applied to both dimensions to prevent the window from being too large
- The script preserves video aspect ratio through MPV's default handling
- No additional MPV parameters are set, allowing MPV to use its default configuration for other settings