This is the implementation guide for the AI agent working on this project.

## Overview

Build a C# 10 .NET MAUI desktop application targeting Windows OS.
The application should be a simple stand-alone executable.
The agent should configure the project with Windows Unpackaged publishing settings (<WindowsPackageType>None</WindowsPackageType>) and enable single-file publishing (<PublishSingleFile>true</PublishSingleFile>).

## Basic Tasks
1. Create an AGENTS.md file.
   The agents file must include instructions to create, use, and maintain a MEMORY.md file.
2. Update the readme file.
3. Create a .gitignore file.
4. Create and build the project.


## Security & Validation
The application must initially present a lock screen requiring a 9-character alphanumeric serial number. 
Validation rules (evaluated against the system clock's current UTC/local time):
1. Char 1: Digit (0-9)
2. Char 2: Digit (0-9)
3. Char 3: Digit = (Char 1 + Char 2) % 10
4. Char 4: Uppercase character from the set ['S','H','A','N','E']
5. Char 5: Literal hyphen '-'
6. Char 6: Uppercase first letter of the current month name (e.g., 'J' for June)
7. Char 7: Digit = (Current Day of Month) % 10
8. Char 8: Character derived from ASCII code: 65 + ((Char 7 * Char 9) % 10)
9. Char 9: Digit (Must exactly match Char 1)

i.e
- The first and last digit must be the same.
- The third digit must be the MOD 10 remainder of the sum of the first and second digit.
- The fourth character must be a letter in the word "SHANE." It's best to specify uppercase only.
- The fifth character is a hyphen.
- The sixth character is the first letter of the current month based on the system clock. It is uppercase.
- The seventh digit is the mod 10 remainder of the current day of the month. If today is June 22, the day is 22. 22 mod 10 = 2.
- The eighth character is the ASCII character for 65 + (the mod 10 of the product of the seventh and last digit). If the seventh digit is 2 and the last digit is 2, the product is 4. 4 mod 10 = 4. 65 + 4 = 69. The character for ASCII 69 is 'E'.


- Activation Period: A valid entry grants application access for exactly 24 hours.
- Lockout Penalty: 3 consecutive failed entries disables the input, forces an asynchronous 5-minute UI delay (hang), and then terminates the application process.  Note that restarting the app should not bypass the penalty.

## Valid Keys
- Request Code Button: Rate-limited to once per 120 seconds. Clicking it opens a window with a textbox containing 7 codes valid for the next 7 days (today included) date displayed next to it. The text should be easily copyable.


## Main Function
Display 3 areas:
1. "Up sync"
2. "Down sync"
3. A log

### Up sync
1. Text input and browse button. The button allows a source directory to be selected, which is displayed in the input box.
2. Text input and browse button. The button allows a destination directory to be selected, which is displayed in the input box. It must not be the same as the source.
3. A checkbox to enable 2-way syncing.
4. An explanation of what this does.
5. A start/stop button and a sync now button.

Clicking the start button disables the input and starts monitoring the source directory. Adds a message to the log area.
Whenever a file in the source directory is changed, it is copied to the destination directory. Adds a message to the log area.

Clicking the "sync now" button attempts the sync immediately. (Adds a message to the log area.)

### Down sync
The down sync area is an exact replica of the up sync.

### Two Way sync and Up vs Down Sync

- Two way sync allows syncing to happen in both directions.
- In "Up Sync" the systems prioritizes copying the local file to the remote location and treats the local file as the authoritative copy.
- In "Down Sync" the systems prioritizes copying the remote file to the local location and treats the remote file as the authoritative copy.
- having Up and Down Sync allows us to sync 2 pair of directories simultaneously.

### Log area
- The log area displays a list box.
- The first column is a time stamp, the second a status "Success", "Error", or "Information," and the third column is a details field.
- Each activity creates an entry in this log.
- Color code log area according to status

## File Collisions & Subdirectories:
- When a file changes and copies over, what happens if the file already exists preserve the authoratiatve copy and add a note tot he log.
- it monitor subfolders recursively

## The "Stop" Button
- When clicked to stop
  - Inputs are re-enabled, 
  - monitoring ceases, 
  - log entry is added

## Techincial
- Queue each file sync as a cancellable  async task.
- The folders may be network locations or mapped drives.