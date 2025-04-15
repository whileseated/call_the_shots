# Video Manager

## Overview
Video Manager is a Python utility designed to retrieve, rename, and play videos. It provides functionality to retrieve videos from online sources, rename them according to a standardized naming convention, and play them using an external media player.

## Requirements
- Python 3.x
- yt-dlp (for video downloading)
- MPV Player (for video playback)

## Functions

### download_video(url, output_filename)
This function downloads a video from a specified URL and saves it with a standardized filename.

Parameters:
- url: The URL of the video to download
- output_filename: The initial filename to save the video as (will be renamed later)

Process:
- Extracts and displays the shot number from the filename
- Downloads the video using yt-dlp with the best video and audio quality in MP4 format
- Renames the downloaded file using the generate_new_filename function
- Returns the new filename if successful, None if the download fails

The function uses yt-dlp with specific parameters to ensure high-quality MP4 output.

### generate_new_filename(old_filename)
This function transforms the original filename into a more readable format.

Parameters:
- old_filename: The original filename (format: "Firstname_Lastname_51634_3_2_4.mp4")

Process:
- Parses the old filename by splitting at underscores
- Extracts the last name, round number, hole number, and shot number
- Constructs a new filename in the format: "Lastname_round3_hole2_shot4.mp4"
- Returns the new filename if parsing is successful, otherwise returns the original filename

The function expects filenames with at least 6 parts separated by underscores.

### play_video(file_path)
This function plays a video file using an external media player.

Parameters:
- file_path: The path to the video file to be played

Process:
- Calls an external bash script (launch_mpv.sh) to play the video
- The bash script handles the configuration of the MPV player

## Usage Examples

To download a golf shot video:
```python
url = "https://example.com/video123"
filename = "John_Doe_12345_1_5_2.mp4"
new_filename = download_video(url, filename)
```

To play a downloaded video:
```python
play_video("Doe_round1_hole5_shot2.mp4")
```

## Notes
- The script is specifically designed for videos with a particular naming convention
- Videos are downloaded in the highest available quality
- Downloaded videos are renamed for easier identification and organization

