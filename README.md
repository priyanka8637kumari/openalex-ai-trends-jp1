# AI Research Trends Analysis

[GitHub Repository](https://github.com/priyanka8637kumari/openalex-ai-trends-jp1)

## Goal

The goal of this project is to analyze recent AI research using data from the OpenAlex API.

I wanted to explore a small sample of research publications and look at:

- number of publications per year
- average citation count
- how many publications are open access
- which publications have the highest citation counts

This is mainly a Python project where I use API requests, file handling, Pandas, OOP, data analysis, and visualization.

---

## Method

I fetch data from the OpenAlex API using the search term `artificial intelligence`.

My first API request returned some future publication years because the results were only sorted by publication date. I therefore refined the query so that it only requests publications from 2020 up to today's date.

The workflow of the project is:

**OpenAlex API → raw JSON → selected fields → Python objects → DataFrame → validation → analysis → visualization**

### 1. Fetching data from the API

I use the `requests` library to fetch data from OpenAlex.

The API request is handled inside the `fetch_works()` function. I also use `try/except` so that connection problems or API errors can be handled without stopping the whole program.

### 2. Saving the raw data

The original API response is saved as:

`data/works_data.json`

I save the raw data before changing it so that I always have the original API response available if I need to inspect it again.

### 3. Selecting relevant information

The OpenAlex response contains many nested fields, but I only need a few of them for this project.

I selected:

- `title`
- `publication_year`
- `cited_by_count`
- `is_open_access`

The `extract_relevant_fields()` function goes through the API results and creates a simpler data structure containing only the fields needed for the analysis.

### 4. Object-Oriented Programming

I use OOP to represent an individual research publication as a Python object.

`ResearchWork` is the base class and contains common information such as:

- title
- publication year
- citation count

The class also contains a `summary()` method that returns a short description of the publication.

`OpenAlexWork` inherits from `ResearchWork` and adds the open-access status.

I use `super()` to reuse the constructor from the parent class.

OOP and Pandas have different purposes in the project. OOP is used to model individual research publications, while Pandas is used to analyze the complete dataset efficiently.

### 5. Creating a DataFrame

After selecting the relevant fields, I convert the data into a Pandas DataFrame.

This makes it easier to:

- inspect data quality
- count publications
- calculate averages
- filter data
- prepare data for visualization

### 6. Validating the data

Before analyzing the dataset, I validate it using the `validate_data()` function.

I check:

- number of rows and columns
- missing values
- duplicated rows
- duplicated titles
- minimum and maximum publication year

In the dataset used for this project, no missing values or duplicated rows were found, so no additional cleaning was needed.

The validated tabular data is saved as:

`data/cleaned_works.csv`

---

## Analysis

I created separate functions for the main analysis questions:

- `get_publications_per_year()`
- `get_average_citations()`
- `get_open_access_counts()`

This keeps the analysis separated into smaller functions that are easier to understand, reuse, and test.

### Questions analyzed

1. How many publications are there per year?
2. What is the average citation count?
3. How many publications are open access compared with non-open access?
4. Which publications have the highest citation counts?

---

## Results

The dataset contains 100 research publications from OpenAlex.

The first analysis shows the distribution of publications across different years, the average citation count, and the open-access distribution.

The results are visualized with Matplotlib to make them easier to understand.

> Note: the current API request fetches 100 results. The results should therefore be understood as an analysis of the fetched sample, not as complete statistics for all AI research worldwide.

---

## Visualization

I use Matplotlib to visualize the analysis results.

The visualizations include:

- publications per year
- open access vs non-open access
- most cited publications

The goal of the visualizations is to make the results easier to understand than showing only numbers.

---

## Reflection

One important part of the project was understanding the structure of the API response before starting to process the data.

I also discovered that my first API query could return future publication dates. I therefore changed the query and used today's date as the upper limit.

I chose to save the original API response as JSON first and then create a simpler dataset for analysis. This made it easier to separate raw data from prepared data.

I used both OOP and Pandas in the project. OOP is useful for representing an individual research publication with attributes and methods, while Pandas is more suitable for analyzing many publications at the same time.

If I continued developing the project, I could add pagination to the OpenAlex API request and fetch a larger dataset. This would provide a stronger basis for analyzing research trends over time.

---

## Technologies and Libraries

This project uses:

- Python 3
- Requests
- Pandas
- Matplotlib
- JSON
- datetime
- Jupyter Notebook
- Git / GitHub

---


## Project Structure

```text
openalex-ai-trends-jp1/
│
├── data/
│   ├── works_data.json
│   └── cleaned_works.csv
│
├── project.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

   
## Installation

To set up the project locally, follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/priyanka8637kumari/openalex-ai-trends-jp1.git
   cd openalex-ai-trends-jp1
   ```
2. Create a virtual environment:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate  # On Windows use `.venv\Scripts\activate`
   ```
3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
   Then open the Jupyter Notebook and run the project.

4. Open project.ipynb in Jupyter Notebook or VS Code and run the cells from top to bottom.


