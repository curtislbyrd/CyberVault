# Python Virtual Environment Commands

| Action                                      | Command                                      | Platform/Notes                                                                 |
|---------------------------------------------|----------------------------------------------|--------------------------------------------------------------------------------|
| Create virtual environment (standard, Python 3.3+) | `python -m venv venv`                       | Creates a virtual environment named `venv` in the current directory.           |
| Create with specific Python version         | `python3.10 -m venv venv`                   | Use the exact Python executable (e.g., `python3.10`, `python3.11`). Must be installed. |
| Create with specific Python version (using virtualenv) | `virtualenv -p /usr/local/bin/python3.10 venv` | Requires `virtualenv` package installed (`pip install virtualenv`). Path to Python may vary. |
| Activate virtual environment                | `.\venv\Scripts\activate`                   | Windows                                                                        |
| Activate virtual environment                | `source venv/bin/activate`                  | macOS / Linux                                                                  |
| Note after activation                       | —                                           | Shell prompt should show `(venv)` prefix.                                       |
| Deactivate virtual environment              | `deactivate`                                | All platforms                                                                  |
| Note after deactivation                     | —                                           | Returns to system/global Python interpreter.                                    |