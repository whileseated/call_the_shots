# (C)all The Shots 

**This repository does not contain code.** 

As an experiment in llm-prompting, text-based abstraction, and unwarranted over-engineering, this repository contains detailed ReadMe files, that when fed to corresponding llms, should (but may not) produce workable code that, when combined, reveal the features described below.  

![Pick a Player](./images/20250415_012319.gif)  

In short, **each ReadMe file should (when uploaded to an llm) create a single file that can then be used to create a terminal-based app for locally viewing every shot videos via command-line.** Each ReadMe has been tested, and the output code has been verified as working.

First, you'll want to use these ReadMes to create python files. Upload the ReadMe to the LLM and tell it to accurately generate the python script while specifically adhering to every detail in the ReadMe, and be sure to include the desired output filename in your prompt.

| ReadMe File | LLM model (tested) | Output File |
|------------------------------|----------------------|---------------|
| 01_README_create_field_csv.md | o3-mini-high | 01_create_entire-field.py |  
| 02_README_json_downloader.md | claude-3.7-sonnet-max | 02_json_downloader.py |  

**Data Files**  
- [x]`01_create_entire-field.py` will create `entire-field.csv`  
- [x]`02_json_downloader.py` will create a folder of json files 

After that, you'll want to generate the five scripts that interact with the data files and glue everything together. Could it be done all-in-one? Probably!

| ReadMe File | LLM model (tested) | Output File |
|------------------------------|----------------------|---------------|
| 03_README_ui_components.md | claude-3.7-sonnet-max | ui_components.py |
| 04_README_video_manager.md | o3-mini-high | video_manager.py |

**App Files**  
- [x] `ui_components.py`   
- [x] `video_manager.py`  
- [] `data_manager.py`  
- [] `launch_mpv.sh`  
- [] `call_the_shots.py`  

You will also need to create a single `config.py` file. No database is necessary.




--

| Column 1  | Column 2  |
|-----------|-----------|
| Example 1 | Example A |
| Example 2 | Example B |
| Example 3 | Example C |
