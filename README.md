# Readme for Abstracting Every Shot

**This project does not contain code.** 

As an experiment, this repository contains detailed ReadMe files, that when fed to corresponding llms, should (but may not) produce workable code that, when combined, reveal the features described below.

In short, *each ReadMe file should (when uploaded to an llm) create a single file that can then be used to create a terminal-based app for locally viewing every shot videos via command-line.* Each ReadMe here has been tested, and the output code has been verified as working.

First, you'll want to use the ReadMe files to create the python files, according to this table, or any way you'd like.

| ReadMe File | LLM model (tested) | Output File |
|------------------------------|----------------------|---------------|
| 01_README_create_field_csv.md | o3-mini-high | 01_create_entire-field.py
| 02_README_json_downloader.md | claude-3.7-sonnet-max | 02_json_downloader.py

*Data Files*  
`01_create_entire-field.py` will create `entire-field.csv`  
`02_json_downloader.py` will create a folder of json files 

*App Files*  
`video_manager_04.py`  
`ui_components.py`   
`data_manager_05.py`  
`main_06.py`  

You will also need to create a single `config.py` file. No database is necessary.




--

| Column 1  | Column 2  |
|-----------|-----------|
| Example 1 | Example A |
| Example 2 | Example B |
| Example 3 | Example C |
