# Little Data Scientist
The idea began when a parent of a 9th grader asked me to create a real Python project for her son. I suggested adapting a small tool I use in my daily data analysis process. This repository isn’t meant to provide complete code examples, but rather to share project ideas that students can explore and learn from all by themselves. Happy coding!


## ✨ Learning Goals
- **Programming Concepts**: Functions, data structures, file I/O, command-line arguments
- **Data Analysis**: Working with structured data, row filtering, column selection
- **Software Development**: Version control with Git and GitHub, virtual environments, testing
- **Modern Tools**: AI/LLM integration, database operations, professional development workflow


## Project overview
This project aims to create a single-script Python app `pick` to select columns and rows from a delimited text file (such as CSV and TSV) for comprehensive data analysis. This tool helps users work with CSV/TSV data files using both command-line operations and Python programming concepts.


## Development Environments and Tools
✨ Students will set up their development environments and use the tools for coding. They should follow the provided links and install everything as instructed.


### Windows Subsystem for Linux (WSL)
For students using Windows, it is recommended to install the[ WSL](https://learn.microsoft.com/en-us/windows/wsl/about), which lets you run Linux distributions and command-line tools natively for development.

✨ Students will install WSL and the Ubuntu distro. If you're under parent control, ask your parent to install.

For Ubuntu, it can be installed via the following command in a Command Prompt (requires administrator privilege)
```
wsl --install
```


### Visual Studio Code (VSCode)
[VSCode](https://code.visualstudio.com/) is a free, open-source code editor with built-in support for debugging, Git integration, syntax highlighting, intelligent code completion, and extensions for virtually any programming language or workflow. It runs on Windows, macOS, and Linux, and is widely used for both quick scripting and full-scale software development. VSCode has AI builtin.

✨ Students will use VSCode as the editor for coding, versioning, and interacting with their GitHub repositories.

Extensions to install:
- Python
- Remote Development
- Any theme you like (optional)

After students installed the Remote Development extension, they should be able to connect to the WSL and start coding.


### GitHub
GitHub is a cloud-based platform for hosting Git repositories, enabling version control, collaboration, and code sharing among developers.

✨ Students will need a GitHub account (free) and then create an empty repository named `pick`. You're going to have a repo like:
```
https://github.com/your-account/pick
```
✨ Students will connect to their GitHub account within VSCode so they will be able to synchronize changes between local repo and remote repo.


### Git
Git is a distributed version control system that tracks changes in code, enabling collaboration, branching, and history management for software projects. With Git, students will be able to revert their code once at any time for example after making a mistake.

✨ Students: clone your GitHub repo locally.

In WSL or a VSCode shell, run:
```
$ git clone https://github.com/your-account/pick
```

Students should have a local foler named `pick` in WSL.

### uv
[uv](https://docs.astral.sh/uv/) is an extremely fast Python package and project manager.

✨ Students: use `uv` to create the Python virtual environment (venv), activate it, and install packages.

Go to the `pick` folder in WSL, run the command below to initialize the project:
```
uv init . --name pick
```

You should see something like `Hello from pick!` by running the following command:
```
uv run main.py
```
The command also create a Python virutual environment in a hidden folder `.venv`.

### Polars
[Polars](https://pola.rs/) is an open-source library for data manipulation, known for being one of the fastest data processing solutions on a single machine.

✨ Students: run the following command to install polars
```
uv add polars
```

### DuckDB
[DuckDB](https://duckdb.org/) is an open-source, in-process analytical database optimized for fast SQL queries on large datasets, often used for data science and analytics.

✨ Students: run the following command to install polars
```
uv add duckdb
```

You can use the following command to test if it's installed correctly:
```
uv run duckdb
```

With DuckDB, students can practice common database CRUD operations, which stand for:
- Create → add new records (e.g., INSERT in SQL)
- Read → retrieve data (e.g., SELECT)
- Update → modify existing records (e.g., UPDATE)
- Delete → remove records (e.g., DELETE)


## The `pick` tool
pick is a command-line (CLI) tool that works with delimited text files such as a CSV or TSV. It has the following syntax:
```
usage: pk [options] [--] [selections_file]

Pick from a file based on a SQL query or columns (names or indices) with/without a row filter.

positional arguments:
  selections_file       Selections (a SQL query or columns with/without a row filter)

options:
  -h, --help            show this help message and exit
  -d, --delimiter d     Single-character delimiter used in the input file (default: None)
  -t, --tab             Use tab as the delimiter (overrides --delimiter)
  -H, --headers [list]  Indicates whether the input file has headers, if a comma-separated list provided, use it as the headers
  -o, --output <file>   Output to file
  -n, --output-headers  Include headers from the output file
  -s, --separator s     Separator used in the output file
  -i, --interactive     Run in interactive mode
```

Examples of usage:
```
  # Select columns by name or index (mix freely, repeat as needed).`
  # - Regex patterns are supported for column names.
  # - Indices are 1-based (negative allowed, slices too).
  # - Use '!' to deselect a column.
  # - If no columns are given, all are selected.
  $ pk Name,HP '^Type.*$' Total,-3,-1 7:10 '!6' Name pokemon.csv

  # Save to output file:
  $ pk Name HP pokemon.csv -s '\t' -o pokemon_lite.tsv

  # Assign custom headers to a file that has no header row:
  $ pk HP Name pokemon_lite.tsv -H Name,HP

  # Filter rows while selecting columns ($ refers to column in the filter):
  $ pk Name,Speed '$Legendary == true & $Speed >= 100' pokemon.csv

  # Query with SQL syntax:
  $ pk "SELECT Name, Speed FROM self WHERE Legendary == true AND Speed >= 100" pokemon.csv

  # Read from standard input and write to standard output as TSV with headers:
  $ cat pokemon.csv | pk Name HP Speed -d ',' -s '      ' -n

  # Open file interactively (pl, lf, and df objects available):
  $ pk pokemon.csv -H -i
```

Notes:
- 

Explanations of arguments

✨ Students: 

- Reads CSV/TSV from files or standard input
- Allows column selection by name or index
- Filters data using simple expressions or SQL queries
- Supports interactive data exploration
- Outputs processed data in various formats to file or standard output

## Project Requirements

Core Features (Required)
Basic CSV Reader: Load and display CSV files
Column Selection: Select specific columns by name or number
Simple Filtering: Filter rows based on basic conditions
Data Export: Save results to new CSV files
Interactive Mode: Explore data in a Python shell
Help System: Built-in help and examples

Advanced Features (Optional/Stretch Goals)
SQL Queries: Use SQL syntax for complex data operations
AI Integration: Natural language queries using LangChain
Data Visualization: Basic charts and graphs
Database Storage: Save/load data using DuckDB
Web Interface: Simple web UI for the tool

Development Environment Setup (for Windows user)

Visual Studio Code + WSL Extension
1. Windows Subsystem for Linux (WSL)

 Install WSL2 with Ubuntuwsl --install -d Ubuntu# Update systemsudo apt update && sudo apt upgrade -y# Install essential toolssudo apt install git curl build-essential

2. Visual Studio Code + WSL Extension
Install VS Code on Windows
Install "WSL" extension in VS Code
Connect to WSL: Ctrl+Shift+P → "WSL: Connect to WSL"
3. Python Environment with UV

 Install UV (modern Python package manager)curl -LsSf https://astral.sh/uv/install.sh | sh# Create project directorymkdir data-analysis-toolcd data-analysis-tool# Initialize Python projectuv inituv add polars pandas  # Core data libraries
4. Git Repository Setup

 Initialize Gitgit initgit remote add origin https://github.com/your-username/data-analysis-tool.git# Create .gitignoreecho "*.pyc__pycache__/.venv/*.csv*.db" > .gitignore
5. Additional Tools

 DuckDB for data analysis
uv add duckdb

 LangChain for AI integration  uv add langchain langchain-openai

 Development toolsuv add pytest black ruff

Project Structure

Development Phases
Phase 1: Foundation (Weeks 1-2)

Set up development environment
Create basic CSV reader
Implement column selection
Write first tests
GitHub repository setup

Phase 2: Core Features (Weeks 3-4)
Add data filtering capabilities
Implement export functionality
Create interactive mode
Add command-line interface
Documentation and examples

Phase 3: Advanced Features (Weeks 5-6)
SQL query support with DuckDB
Basic AI integration with LangChain
Simple data visualization
Web interface (optional)

Phase 4: Polish & Present (Week 7)
Code review and refactoring
Comprehensive testing
User documentation
Project presentation
Key Programming Concepts Covered
Data Structures: Lists, dictionaries, sets
File Operations: Reading/writing CSV files
Error Handling: Try/except blocks
Command Line: Argument parsing with argparse
Object-Oriented Programming: Classes and methods
Testing: Unit tests with pytest
Version Control: Git workflow
Virtual Environments: Dependency management

Sample Learning Activities
Week 1: Getting Started

# Simple CSV reader exerciseimport csvdef read_csv_file(filename):    """Read a CSV file and return the data"""    with open(filename, 'r') as file:        reader = csv.reader(file)        headers = next(reader)        data = list(reader)    return headers, data# Test with sample student dataheaders, data = read_csv_file('students.csv')print(f"Columns: {headers}")print(f"Number of rows: {len(data)}")
Week 3: Data Filtering

def filter_by_grade(data, min_grade):    """Filter students by minimum grade"""    return [row for row in data if float(row[2]) >= min_grade]def filter_by_subject(data, subject):    """Filter by subject name"""    return [row for row in data if subject.lower() in row[1].lower()]
Week 5: AI Integration

from langchain.llms import OpenAIfrom langchain.chains import ConversationChaindef natural_language_query(data, question):    """Use AI to interpret natural language queries about data"""    llm = OpenAI(temperature=0)    # Convert question to data operation    # Implementation details...
Assessment Rubric
Technical Skills (40%)
Code quality and organization
Proper use of functions and classes
Error handling
Testing coverage
Data Analysis (30%)
Correct implementation of filtering
SQL query functionality
Data export capabilities
Understanding of data structures
Project Management (20%)
Git usage and commit history
Documentation quality
Code comments and docstrings
Project organization
Innovation (10%)
Creative features
AI integration
User experience improvements
Problem-solving approach
Sample Data Sets
Student Grades: Name, Subject, Grade, Date
Sales Data: Product, Price, Date, Salesperson
Weather Data: Date, Temperature, Humidity, Precipitation
Sports Statistics: Player, Team, Points, Games
Movie Ratings: Title, Genre, Rating, Year
Extensions and Next Steps
Data Visualization: Add matplotlib/plotly charts
Web Dashboard: Flask/FastAPI web interface
Machine Learning: Simple predictions with scikit-learn
Real-time Data: Stream processing capabilities
API Integration: Fetch data from web APIs
Mobile App: Create a companion mobile app
This project provides a perfect balance of practical programming skills, data analysis concepts, and modern development practices that will prepare students for advanced computer science courses and real-world development work.


