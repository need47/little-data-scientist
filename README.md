# Little Data Scientist
This project started when a parent of a 9th grader asked me to create a real Python project for her son. I suggested adapting a small tool I use in my daily data analysis work.

This repository doesn’t provide finished solutions — instead, it shares a project idea that students can explore, build, and learn from on their own.

Happy coding! 🚀


## ✨ Learning Goals
- **Programming Concepts**: Functions, data structures, file input/output, command-line arguments
- **Data Analysis**: Handling structured data, filtering rows, selecting columns
- **Software Development**: Using Git and GitHub, working with virtual environments, writing tests
- **Modern Tools**: Exploring AI/LLM integration, practicing database operations, following professional workflows

This project balances practical programming, data analysis, and modern development skills. It will help prepare students for advanced computer science courses and real-world software projects.


## 📖 Project overview
The project is to build a Python command-line app called `pick`.

`pick` lets you select columns and rows from text files (CSV/TSV). It’s a lightweight tool that demonstrates how data analysts work with structured data, while also teaching key programming concepts.


## 🛠 Development Environments and Tools
Students will set up their coding environment and practice using professional tools. Follow the links and instructions carefully.


### Windows Subsystem for Linux (WSL)
If you’re on Windows, install [WSL](https://learn.microsoft.com/en-us/windows/wsl/about), WSL lets you run Linux distributions and use Linux command-line tools for development.

✨ Steps:
- Ask a parent for help if admin privileges are required.
- Open `Command Prompt` as administrator and run:
```
wsl --install
```
- Choose `Ubuntu` as your Linux distribution (default)
  

### Visual Studio Code (VSCode)
[VSCode](https://code.visualstudio.com/) s a free, open-source code editor with support for debugging, Git, intelligent completion, and tons of extensions. It’s widely used by professionals. VSCode also has AI built in.

✨ Use VSCode for:
- Writing and editing code
- Managing GitHub repositories
- Running your app inside WSL

Recommended extensions:
- **Python**
- **Remote Development**
- Any theme you like (optional)

Once installed, connect VSCode to WSL and start coding directly in Ubuntu.


### GitHub
[GitHub](https://github.com/) is where developers store and share code.

✨ Steps:
1. Create a free GitHub account.
2. Create a new, empty repository named pick. It will look like:
```
https://github.com/your-account/pick
```
3. Connect VSCode to GitHub so you can sync your local and remote repos.


### Git
[Git](https://git-scm.com/) is a version control system to track changes in code. It helps you undo mistakes, experiment safely, and collaborate.

✨ Clone your GitHub repo locally:

In WSL or a VSCode shell, run:
```
$ git clone https://github.com/your-account/pick
```

This creates a local folder named `pick` in WSL.


### uv
[uv](https://docs.astral.sh/uv/) is a super-fast Python package and project manager.

✨ Go to your `pick` folder in WSL and initialize your project with:
```
uv init . --name pick
```

Test it with:
```
uv run main.py
```

You should see `Hello from pick!`

This also creates a hidden `.venv` folder with your Python virtual environment.

### Polars
[Polars](https://pola.rs/) is a high-performance library for data manipulation.

✨ Install with
```
uv add polars
```

### DuckDB
[DuckDB](https://duckdb.org/) s an in-process analytical database — great for practicing SQL with real datasets.

✨ Install with:
```
uv add duckdb
```

Test the installation:
```
uv run duckdb
```

You’ll then be ready to practice the four database operations:
- **Create** → add new records (e.g., INSERT)
- **Read** → retrieve data (e.g., SELECT)
- **Update** → modify existing records (e.g., UPDATE)
- **Delete** → remove records (e.g., DELETE)


## The `pick` tool
Students will develop the `pick`, which is a command-line (CLI) tool or working with CSV/TSV files. It has the following syntax:
```
pick [options] [--] [selections_file]
```

Examples of usage:
```
  # Select columns by name or index (mix freely, repeat as needed).`
  # - Regex patterns are supported for column names.
  # - Indices are 1-based (negative allowed, slices too).
  # - Use '!' to deselect a column.
  # - If no columns are given, all are selected.
  $ pk Name,HP '^Type.*$' Total,-3,-1 7:10 '!6' Name pokemon.csv

  # Save results to a file:
  $ pk Name HP pokemon.csv -s '\t' -o pokemon_lite.tsv

  # Add headers to a file that has none:
  $ pk HP Name pokemon_lite.tsv -H Name,HP

  # Filter rows with conditions:
  $ pk Name,Speed '$Legendary == true & $Speed >= 100' pokemon.csv

  # Query with SQL:
  $ pk "SELECT Name, Speed FROM self WHERE Legendary == true AND Speed >= 100" pokemon.csv

  # Pipe data through:
  $ cat pokemon.csv | pk Name HP Speed -d ',' -s '      ' -n

  # Explore interactively:
  $ pk pokemon.csv -H -i
```

Basic requirements:
- Allow a file or standard input (`-` means stdin) as an input.
- Guess delimiter (e.g., `,` for .csv and `\t` for .tsv) from file extension unless overridden by `-d`.
- Use `-H` to specify whether the file has headers (or provide custom headers).
- Select columns by name or index (mix freely, repeat as needed). Use '!' to deselect a column.
- Use one-based indexing for column selection. Negative indices count from the end.
- Filter rows by conditions. Use `$col` or `$1` syntax for column in the filter expression.

Optional requirements:
- Allow to use a SQL query to select columns and/or filter rows.
- Allow interactive data exploration via `-i`

🪄 Hints: Leverage Polars to handle the input and output.


# Advanced Goal
🤖 Artificial Intelligence (AI) is everywhere. Keep up with it. Leverage a Large Language Model (LLM) or even [Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro) to let users query and explore CSV/TSV files in plain English. For example, instead of writing SQL or filters, a student could type: `Show me all Pokémon with speed over 100 that are legendary`.

👉 Try things out, make mistakes, and discover along the way — that’s how real learning happens. Enjoy the journey!
