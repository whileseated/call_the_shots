# (C)all The Shots 

**This repository does not contain code.** 

As an experiment in llm-prompting, text-based abstraction, and unwarranted over-engineering, this repository contains detailed ReadMe files, that when fed to corresponding llms, should (but may not) produce workable code that, when combined, reveal the the CLI-based features described below.  

![Pick a Player](./images/20250415_012319.gif)  

In short, **each ReadMe file should (when uploaded to an llm) create a single file that can then be used to create a terminal-based app for locally viewing every shot videos via command-line.** Each ReadMe has been tested, and the output code has been verified as working.

Upload a ReadMe to the corresponding LLM and prompt it to accurately generate the python script while specifically adhering to every detail in the ReadMe. Be sure to include the desired output filename in your prompt, like this: `Can you please complete a python script based on data_manager.md that includes every single feature and adheres with great detail to every single item expressed in the readme? There's no need to include inline comments in the python script either, as we have the readme for explanation. In your final output, create a copyable python codeblock.`

| ReadMe File | LLM model (tested) | Output File |
|------------------------------|----------------------|---------------|
| 01_README_create_field_csv.md | o3-mini-high | 01_create_entire-field.py |  
| 02_README_json_downloader.md | claude-3.7-sonnet-max | 02_json_downloader.py |  

**Data Files**  
- [x] `01_create_entire-field.py` will create `entire-field.csv`  
- [x] `02_json_downloader.py` will create a folder of json files 

After that, you'll want to generate the five scripts that interact with the data files and glue everything together. Could it be done all-in-one? Probably!

| ReadMe File | LLM model (tested) | Output File |
|------------------------------|----------------------|---------------|
| 03_README_ui_components.md | claude-3.7-sonnet-max | ui_components.py |
| 04_README_video_manager.md | o3-mini-high | video_manager.py |  
| 05_README_data_manager.md | o3-mini-high | data_manager.py |  
| 06_README_launch_mpv.md | 03-mini-high | launch_mpv.sh |  
| 07_README_call_the_shots.md | o1 | call_the_shots.py |  


**App Files**  
- [x] `ui_components.py`   
- [x] `video_manager.py`  
- [x] `data_manager.py`  
- [x] `launch_mpv.sh`  
- [x] `call_the_shots.py`  

You will also need to create a single `config.py` file. No database is necessary.

In the end, you should have a structure of files that looks like this:

```- 01_create_entire-field.py 
- 02_json_downloader.py
- ui_components.py
- video_manager.py
- data_manager.py
- launch_mpv.sh
- call_the_shots.py```

Use `python3 call_the_shots.py` to launch the cli-app. Use letters and up-down arrows to select the player, and numbers for shot selection.