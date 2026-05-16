# Local Notebook Setup

These notebooks can run locally with the same SQL teaching style used in Colab: `%sql` connects to a SQLite database, and `%%sql` cells contain the SQL queries.

## 1. Create the Python environment

Use Python 3.10 or 3.11.

Option A, standard `venv`, from the project root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --user --name bia5476-local --display-name "Python (BIA5476 local)"
```

Option B, Anaconda, useful if `python3 --version` shows an older Python:

```bash
conda create -n bia5476-local python=3.11
conda activate bia5476-local
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --user --name bia5476-local --display-name "Python (BIA5476 local)"
```

On Windows PowerShell, activate with:

```powershell
.\.venv\Scripts\Activate.ps1
```

## 2. Start Jupyter

Start Jupyter from the project root:

```bash
jupyter lab
```

Open a notebook and select the kernel named `Python (BIA5476 local)`.

## 3. How SQL runs locally

The SQL notebooks use local SQLite database files already in this project:

- `zagimore.db`
- `HAFH.db`
- `NYPD_Material/star_schema_nypd_complaints.db`
- `Week 5/star-schema-nypd-complaints-2024.db`
- `Week 5/Kaggle-AirbnbNYC-2022-2024.db`

The SQL query cells are still SQL cells. For example:

```sql
%%sql

SELECT name FROM sqlite_master WHERE type='table';
```

Only the setup/path cells were changed from Google Drive paths to local project paths.

## 4. Large local data files

The Airbnb notebooks read CSV files from:

```text
Final/Airbnb-Full-NYC/
```

The restaurant-inspection example in `Week 7/example_sql_colab.ipynb` expects this file in the project root:

```text
DOHMH_New_York_City_Restaurant_Inspection_Results_20250928.csv
```

That CSV is not currently present in the repository, so place it in the project root before running that notebook or update `csv_path` in the notebook.
