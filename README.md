# (C)all The Shots 

**This repository does not contain code.** 

As an experiment in llm-prompting, text-based abstraction, and unwarranted over-engineering, this repository contains detailed ReadMe files, that when fed to corresponding llms, should (but may not) produce workable code that, when combined, reveal the the CLI-based features in this gif.  

![Pick a Player](./images/20250415_012319.gif)  

In short, **each ReadMe file should (when uploaded to an llm) create a single file that can then be used to create a terminal-based app for locally viewing every shot videos via command-line.** 

Each ReadMe has been tested, and the output code has been verified as working.

To begin, we'll start with creating a csv that includes player names and their corresponding ID. The process for creating the csv-generating script is exactly the same for all seven scripts. 

Upload the ReadMe to the corresponding LLM and prompt it to accurately generate the python script while specifically adhering to every detail in the ReadMe, like this: `Please create a python script based on 01_README_create_field_csv.md that includes every single feature and adheres with great detail to every single item expressed in the ReadMe. In your final output, create a copyable python codeblock.`

Save those scripts according to these tables, below.

| ReadMe File | LLM model (tested) | Output File |
|------------------------------|----------------------|---------------|
| 01_README_create_field_csv.md | o3-mini-high | 01_create_entire-field.py |  
| 02_README_json_downloader.md | claude-3.7-sonnet-max | 02_json_downloader.py |  

**Data Files**  
- [x] `python3 01_create_entire-field.py` will create `entire-field.csv`  
- [x] `python3 02_json_downloader.py` will create json files for a `2025_json_data` folder

After that, you'll want to generate the five scripts that interact with the data files. Could this be done as an all-in-one script? Probably!

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
- [x] `config.py`
- [x] `call_the_shots.py`  

You will also need to smartly edit the `config.py` file to match your intended outcome. No database is necessary.

**Requirements**

Create a `requirements.txt` file with these libraries, and then run `pip install -r requirements.txt`

```
selenium==4.17.2  
webdriver-manager==4.0.1  
requests==2.31.0  
pandas==2.1.4  
prompt-toolkit==3.0.43  
yt-dlp==2023.12.30 
```  

**Finishing-Up**

In the end, you should have a structure of files that looks like this:

```
- requirements.txt
- 01_create_entire-field.py 
- 02_json_downloader.py
- ui_components.py
- video_manager.py
- data_manager.py
- launch_mpv.sh
- call_the_shots.py
```  

Use `python3 call_the_shots.py` to launch the cli-app. Use letters and up-down arrows to select the player, and numbers for shot selection, per [the gif above](images/20250415_012319.gif).

**ToDo**

- [ ] Merge all seven ReadMes into one, and test to see which llm(s) can successfully create an error-free cli-app.