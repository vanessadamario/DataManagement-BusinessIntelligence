# Data Management and Business Intelligence

Course material for MBA students learning data management, relational databases, SQL, and business intelligence workflows.

The notebooks in this repository were originally designed for Google Colab. They now run locally with JupyterLab/Jupyter Notebook while preserving the same teaching goal: students write real SQL queries against real SQLite databases.

## Course Approach

This course is designed for master students in business administration, not for software engineers. The objective is to understand how data is organized, queried, checked, joined, summarized, and used for business analysis.

We use notebooks because they combine three things in one place:

- Explanatory text for business context and instructions.
- Executable SQL and Python cells.
- Immediate output tables, charts, and data checks.

This makes each notebook both a lecture document and a hands-on lab.

## How We Use SQLite Locally

SQLite is a lightweight relational database system. Instead of connecting to a remote database server, SQLite stores the database in a local `.db` file, such as:

- `zagimore.db`
- `HAFH.db`
- `NYPD_Material/star_schema_nypd_complaints.db`

This is useful for teaching because students can practice SQL locally without installing or managing a full database server.

In the notebooks, SQL runs through the `ipython-sql` library. A setup cell connects Jupyter to a SQLite database:

```python
%reload_ext sql
%sql sqlite:///path/to/database.db
```

After that, students can write SQL directly in notebook cells:

```sql
%%sql

SELECT name
FROM sqlite_master
WHERE type = 'table';
```

The SQL remains SQL. Python is used only to support the notebook environment, connect to local files, display results, or create charts when useful.

## Why Conda and Python Libraries Are Needed

Jupyter itself does not automatically know how to run SQL. The local Conda environment installs the libraries that make the notebooks work:

- `jupyterlab` and `notebook`: open and run notebooks locally.
- `ipykernel`: make the course environment selectable as a notebook kernel.
- `ipython-sql`: enable `%sql` and `%%sql` cells.
- `SQLAlchemy`: manage the database connection used by `ipython-sql`.
- `pandas`, `numpy`, `matplotlib`, `seaborn`: support data analysis, tables, and charts.
- `pandasql`: allow SQL-style queries over pandas DataFrames in selected examples.

The environment is defined in [requirements.txt](requirements.txt).

## Local Setup

Use Python 3.10 or 3.11. With Conda, run these commands from Terminal:

```bash
cd /Users/vanessadamario/src/DataManagement-BusinessIntelligence
conda create -n bia5476-local python=3.11
conda activate bia5476-local
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --user --name bia5476-local --display-name "Python (BIA5476 local)"
jupyter lab
```

In JupyterLab, open a notebook and select the kernel:

```text
Python (BIA5476 local)
```

More details are available in [LOCAL_SETUP.md](LOCAL_SETUP.md).

## Repository Structure

- `Week 1/`: first notebook introduction and first SQL queries.
- `Week 3/`: loading and querying the HAFH database.
- `Week 4/`: SQL querying with the ZAGIMORE database.
- `Week 5/`: database creation and additional datasets.
- `Week 6/`: Airbnb data integrity and pandas-based analysis.
- `Week 7/`: SQL over tabular data and sentiment analysis examples.
- `Week 8/`: SQL assignment using the NYPD star-schema database.
- `Final/Airbnb-Full-NYC/`: larger Airbnb CSV datasets.
- `NYPD_Material/`: NYPD database and schema material.

## Notes for Students

Start Jupyter from the project root folder. The notebooks look for files relative to this repository, so launching Jupyter elsewhere may cause file path errors.

Run notebook cells from top to bottom. The database connection cell must run before the SQL cells.

When a cell starts with `%%sql`, write SQL only in that cell. When a cell does not start with `%%sql`, it is a Python cell.
