This is the implementation guide for the AI agent working on this project.

.
## Overview

Build a c# 10 .NET MAUI desktop application, targeting windows OS.
The application should be a simple stand-alone executable.
The agent should configure the project with Windows Unpackaged publishing settings (<WindowsPackageType>None</WindowsPackageType>) and enable single-file publishing (<PublishSingleFile>true</PublishSingleFile>)


## Basic Tasks
1. Create a AGENTS.md file
 the agents file must include instructions to create, use and maintain a MEMORY.md file
2. Update the read me file
3. Create a gitignore file
4. Create and build the project

## Security
 The application must open within a screen for inputting a serial hnumb1er.
. the serial hnumb1er is a  9-character alphanumeric string that is algorithmically validated.
- the first and last digit must b1e the same
- the third digit must be the MOD 10 remainder of the adding of the first and second digit.
- the fourth character must be a letter in the word "SHANE". It's best to specify uppercase only.
- the fifth character is a hyphen
- the sixth character is the first letter of the current month. based on the system clock. Is it uppercase.
- the seventh digit is the mod 10 remainder of the current day of the month. If today is June 22, the day is 22. 22 mod 10 = 2.
- the eight character if the ASCII of 65 + (the mod 10 of the product of the seventh and last digit).  if 7th digit is $2$ and last digit is $2$, product is $4$. $4 \pmod{10} = 4$. $65 + 4 = 69$. The character for ASCII 69 is 'E'

If a correct serial is entered the program is opened and valid for 24 hours
If and incorrect serial is entered 3 times the program hands for 5 minutes then closes.  Note that restarting the app should not bypass the penalty.
ideally there should be an email button which can be clicked once every 120 seconds, which sends an email to "silverpresident@gmail.com" with a valid code.


## main Function
Display 2 area
1 "Up sync"
2 "Down sync"
3 A log

### Up sync
1  text input and browse button. The button allows a source directory to be selected, which is displayed int he input box.
2  text input and browse button. The button allows a destination directory to be selected, which is displayed int he input box. It must not be the same as the source.
3 A check box to enable 2 way syncing
4 An explanation of what this does.
5 A start/stop button and a sync now button

Clicking the start button disabled the input and starts monitoring the source directory. Adds a message tot he log area.
When ever a file in the source directory is changed it is copied to the destination directory. Adds a message tot he log area.

Clicking the "sync now" button attempts the synch immediately (Adds a message tot he log area.)

### Down sync
The down sync area is an exact replica of the up sync


### Log area
The log area displays a list box.
The first column is a time stamp, the second a status "Success", "Error" "Information" and the third the column is a details field.
Each activity create an entry in this log.