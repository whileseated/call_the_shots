# UI Components Documentation

This document provides a detailed explanation of the user interface components used in the application. The UI components facilitate user interaction through command-line prompts with auto-completion capabilities for selecting players, rounds, holes, and shots.

## Overview

The UI components module provides several interactive prompt functions that guide users through selecting different elements of data. These components use the prompt-toolkit library to provide autocompletion features and user-friendly input methods.

## Dependencies

The module requires:
- prompt_toolkit library for interactive command-line interfaces
- pandas for data manipulation
- A CSV file containing player data with columns for Player ID and Full Name
- A config file with CSV_FILE_PATH defined

## Component Descriptions

### Display Choices

The display_choices function presents numbered options to users and returns their selection. It accepts a list of choices, displays them with numbers, and prompts the user to select one by entering the corresponding number. The function then returns the selected choice.

This component doesn't use autocompletion but provides a simple way to display and select from a limited set of options. It's valuable when the selection set is small and displaying all options simultaneously makes sense.

### Autocomplete Player Selection

The autocomplete_player function provides a player selection interface with autocompletion. It reads player data from the configured CSV file, creates an autocomplete prompt with all player names, and returns both the selected player's name and their Player ID.

As the user types, the function suggests matching player names, making it easier to find and select a specific player from a large roster. The function accesses the Player ID from the data file to return along with the name, which is useful for subsequent data processing.

### Round Selection

The select_round function creates a prompt for selecting a tournament round (1-4) with autocompletion support. It provides a simple interface for users to choose which round of a tournament they want to view data for.

The function offers autocompletion for the four possible rounds in a typical tournament, making selection fast and error-resistant. 

### Hole Selection

The select_hole function creates a prompt for selecting a hole (1-18) with autocompletion. It generates a list of holes from 1 to 18 and allows users to select one with the help of autocompletion.

This makes it easy for users to specify which hole they're interested in, with autocompletion reducing typing and potential errors.

### Shot Selection

The select_shot function presents available shots for a specific hole and allows the user to select one. It displays numbered shots and returns the user's selection based on their numeric input.

The function includes both a numeric selection interface where shots are displayed with corresponding numbers, and an autocompletion-based approach for shot selection. The implementation appears to have both approaches, with the numeric selection being the active one.

## Usage Flow

A typical user interaction flow would proceed as follows:
1. Select a player using autocomplete_player
2. Select a tournament round using select_round
3. Select a specific hole using select_hole
4. View and select from available shots for that hole/player using select_shot

Each step uses autocompletion where appropriate to simplify user input and reduce errors.

## Implementation Notes

The module integrates with a data manager component that loads player data, and it requires a properly formatted CSV file with player information. The WordCompleter class from prompt_toolkit is used extensively to provide the autocompletion functionality.

The last function (select_shot) appears to have two implementations - one using numbered choices and another using autocompletion. In the current version, the numbered selection is active while the autocompletion code appears to be inactive (not reached in normal execution). 