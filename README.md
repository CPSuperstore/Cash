# Cash
A Customizable Terminal For Modifing Files And Things

---

To use, simply run "cashConsole.py". 

Alternatively, you can create your own script (so it can be run anywhere you need, like a web app)
Simply `import CashInterpreter`. From there, call the `interpret_command` command function.
This function takes 1 arguement, which is the command you would like to execute.

The function will return a list, which is effectively the output of the command.

---

For even more customization options, see the `config.json` file.

| Property                  | Description  |
| ------------------------ | :------------ |
| directory_root            | The Path To The Cash File Structure. _Note:_ Any file outside this directory can not be modified by Cash|
| startup_script            | A List Of Commands Which Will Be Executed On Console Startup |
| start_location            | The Path Inside The Cash Structure Where The Console Will Start  |
| default_structure         | The Default File Structure. These Files Are Only Created If The _directory_root_ directory is missing |
| text_edit_program_name    | The Name Of The Executable To Open The File In From The _tedit_ Command |
| default_history_commands  | The Number Of History Commands To Show By Default When The _history_ Command Is Executed |
| date_format               | The _datetime_ Date Format |
| dump_file_format          | The _datetime_ Format Of Dump File Names. _Note: {fname}_ Is Replaced With _error_report_filename_ |
| error_report_directory    | The Directory To Save Dump Files/Error Reports |
| error_report_filename     | The Name Of The Error File |
| capture_program_output    | If The System Should Capture External Executable Output And Return It. (This Causes Problems If The Executable Requres Command Line Input) |
| disabled_commands         | The List Of Commands Which Cannot Be Used |
| list_delimiter            | The Character To Delimit Lists |
| sql_commands              | A Dictionary Of The Custom SQL Command, And The Command It Executes (Creates Command Wrappers) |
| overrides                 | A List Of Python Files Which Contain Extra Functions. These Can Be New Commands, Or Override Current Commands. Note That They Must Accept _*args_ as their sole parameter |

---

**Other Notes**
* Any Function In Any Of The Override Files Can Be Used In The Startup Script
* The Docstring In A Function Is The Command's Help Text, And Will Automaticaly Be Displayed In The _help_ Command
* The _ping_ Command Is Not Advised On Linux Machines
* If A Script In The _overrides_ List Does Not Exist, An Error Message Will Be Printed To The Console (Not Displayed As Output), And The Console Will Continue Loading The Rest Of The Override Files

---

**Sample Config File**
```
{
    "directory_root": "root",
    "startup_script": [
        "echo Running Startup Scripts...",
        "cd ..",
        "mkdir home",
        "mkdir tmp",
        "mkdir error",
        "trunc tmp",
        "cd home",
        "clear"
    ],
    "start_location": "/home",
    "default_structure": [
        "/home/Desktop",
        "/home/Downloads",
        "/home/Music",
        "/home/Pictures",
        "/home/Videos",
        "/home/Documents",
        "/tmp"
    ],
    "text_edit_program_name": "notepad.exe",
    "default_history_commands": 10,
    "date_format": "%Y/%m/%d %I:%M:%S %p",
    "dump_file_format": "%Y-%m-%d_%H-%M-%S_{fname}",
    "error_report_directory": "/error",
    "error_report_filename": "dump.txt",
    "capture_program_output": 0,
    "disabled_commands": [
        "ping"
    ],
    "list_delimiter": "\n",
    "sql_commands": {
        "tables": "SELECT name FROM sqlite_master WHERE type='table' ORDER BY name;",
        "describe {}": "PRAGMA table_info({});"
    },
    "overrides": ["overrides.py"]
}
```
