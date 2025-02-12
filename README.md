# livecsv

**livecsv** is a custom SQLAlchemy dialect that loads CSV data from a remote source into an in‑memory DuckDB instance with caching support. It is designed for read‑only use and allows you to query CSV data as if it were a relational table.

## Installation

Install livecsv using pip:

```bash
pip install livecsv

Dependencies

livecsv depends on the following packages:
	•	SQLAlchemy (>=2.0.0)
	•	duckdb
	•	duckdb_engine

These dependencies will be automatically installed when you install livecsv.

Usage

The livecsv dialect lets you create a SQLAlchemy engine with a custom connection string that loads CSV data from a remote URL. The CSV is loaded into an in‑memory DuckDB instance, and the data is cached for a configurable number of minutes.

Connection String Format

The connection string format for livecsv is:

livecsv://<ssl_mode>/<cache_minutes>/<tablename>/<csv_url>

	•	ssl_mode: Either secure (for HTTPS) or insecure (for HTTP).
	•	cache_minutes: The number of minutes to cache the CSV data before refreshing. If 0, it is unlimited (not refreshed).
	•	tablename: The name of the table that will be created in the in‑memory database.
	•	csv_url: The URL to the CSV file (if the URL does not start with http, a scheme will be automatically prepended based on the ssl_mode).

Example

Below is a sample code snippet that demonstrates how to use livecsv:

from sqlalchemy import create_engine, text

# Create an engine using the livecsv dialect.
engine = create_engine(
    "livecsv://secure/10/usernames/support.staffbase.com/hc/en-us/article_attachments/360009197031/username.csv"
)

# Query the table created from the CSV.
with engine.connect() as conn:
    result = conn.execute(text("SELECT * FROM usernames LIMIT 1")).fetchall()
    for row in result:
        print(row)

In this example, livecsv:
	•	Loads the CSV from the specified URL.
	•	Creates a table named usernames.
	•	Caches the data for 10 minutes.
	•	Allows you to query the data using SQLAlchemy.

Testing with pytest

livecsv includes tests that can be run using pytest.

Steps to Run Tests
	1.	Install pytest (if you haven’t already):

pip install pytest


	2.	Set the Test Environment Variable
To run tests with known data (instead of fetching a remote CSV), set the environment variable LIVECSV_TEST to "1". For example, on Linux/macOS:

export LIVECSV_TEST=1

On Windows (cmd):

set LIVECSV_TEST=1


	3.	Run pytest
From the root of your project, run:

pytest

The tests will create a table with known test data (for example, a table with a row like ('booker12', 9012, 'Rachel', 'Booker')) and assert that the queries return the expected results.

License

This project is licensed under the MIT License. See the LICENSE file for details.

Author

Your Name – your.email@example.com

### 2. Create an HTML File With a Download Link

Create an HTML file (for example, `download_readme.html`) with the following content. When this file is opened in a browser, the user can click the download link to receive the `README.md` file:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Download README.md</title>
</head>
<body>
  <h1>Download README.md</h1>
  <p>Click the link below to download the README.md file:</p>
  <a id="download-link" href="#" download="README.md">Download README.md</a>

  <script>
    // The text content of the README.md file.
    var readmeContent = `# livecsv

**livecsv** is a custom SQLAlchemy dialect that loads CSV data from a remote source into an in‑memory DuckDB instance with caching support. It is designed for read‑only use and allows you to query CSV data as if it were a relational table.

## Installation

Install livecsv using pip:

\`\`\`bash
pip install livecsv
\`\`\`

## Dependencies

livecsv depends on the following packages:

- [SQLAlchemy](https://www.sqlalchemy.org/) (>=2.0.0)
- [duckdb](https://github.com/duckdb/duckdb)
- [duckdb_engine](https://pypi.org/project/duckdb-engine/)

These dependencies will be automatically installed when you install livecsv.

## Usage

The livecsv dialect lets you create a SQLAlchemy engine with a custom connection string that loads CSV data from a remote URL. The CSV is loaded into an in‑memory DuckDB instance, and the data is cached for a configurable number of minutes.

### Connection String Format

The connection string format for livecsv is:

\`\`\`
livecsv://<ssl_mode>/<cache_minutes>/<tablename>/<csv_url>
\`\`\`

- **ssl_mode**: Either \`secure\` (for HTTPS) or \`insecure\` (for HTTP).
- **cache_minutes**: The number of minutes to cache the CSV data before refreshing.
- **tablename**: The name of the table that will be created in the in‑memory database.
- **csv_url**: The URL to the CSV file (if the URL does not start with \`http\`, a scheme will be automatically prepended based on the ssl_mode).

### Example

Below is a sample code snippet that demonstrates how to use livecsv:

\`\`\`python
from sqlalchemy import create_engine, text

# Create an engine using the livecsv dialect.
engine = create_engine(
    "livecsv://secure/10/usernames/support.staffbase.com/hc/en-us/article_attachments/360009197031/username.csv"
)

# Query the table created from the CSV.
with engine.connect() as conn:
    result = conn.execute(text("SELECT * FROM usernames LIMIT 1")).fetchall()
    for row in result:
        print(row)
\`\`\`

In this example, livecsv:
- Loads the CSV from the specified URL.
- Creates a table named \`usernames\`.
- Caches the data for 10 minutes.
- Allows you to query the data using SQLAlchemy.

## Testing with pytest

livecsv includes tests that can be run using [pytest](https://docs.pytest.org/).

### Steps to Run Tests

1. **Install pytest** (if you haven't already):

   \`\`\`bash
   pip install pytest
   \`\`\`

2. **Set the Test Environment Variable**

   To run tests with known data (instead of fetching a remote CSV), set the environment variable \`LIVECSV_TEST\` to \`"1"\`. For example, on Linux/macOS:

   \`\`\`bash
   export LIVECSV_TEST=1
   \`\`\`

   On Windows (cmd):

   \`\`\`bash
   set LIVECSV_TEST=1
   \`\`\`

3. **Run pytest**

   From the root of your project, run:

   \`\`\`bash
   pytest
   \`\`\`

   The tests will create a table with known test data (for example, a table with a row like \`('booker12', 9012, 'Rachel', 'Booker')\`) and assert that the queries return the expected results.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Author
Eyal Rahmani
