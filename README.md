# Web Scraping Using Python to Extract Data From Web
![WebScrapping Project cover](https://github.com/pbisht2105/Web-Scrapping-Using-Python/blob/main/Scraping%20Data%20from%20Website%20using%20Python%20cover.png)

```python
# Import necessary libraries
import os
from bs4 import BeautifulSoup
import requests 
import pandas as pd

# Print the current working directory
print(os.getcwd())

# URL of the website to scrape
url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'

# Request the page content
page = requests.get(url)

# Parse the content using BeautifulSoup
soup = BeautifulSoup(page.text, 'html.parser')

# Pretty-print the parsed HTML (optional)
print(soup.prettify())

# Find the first table in the page
table = soup.find_all('table')[0]

# Extract the titles (headers) of the table
worlds_title = table.find_all('th')
world_table_title = [title.text.strip() for title in worlds_title]
print(world_table_title)

# Initialize a DataFrame with the extracted column titles
df = pd.DataFrame(columns=world_table_title)
df

# Extract all the rows of the table (excluding the header row)
column_data = table.find_all('tr')

# Loop through all the rows (starting from the second row)
for row in column_data[1:]:
    # Extract the data cells (td elements) in each row
    row_data = row.find_all('td')
    
    # Extract and clean up the text from each cell
    ind_row_data = [data.text.strip() for data in row_data]

    # Add the row data to the DataFrame
    length = len(df)
    df.loc[length] = ind_row_data

# Save the DataFrame to a CSV file
df.to_csv(r'C:\Users\user\Downloads\My Projects\Python\Companies_Data.csv', index=False)

# Step 1: Initialize an empty list to hold all the row data
all_rows_data = []

# Step 2: Loop through all the rows starting from the second row (to skip the header)
for row in column_data[1:]:
    # Get the data cells (td elements) in the current row
    row_data = row.find_all('td')
    
    # Extract the text from each cell and strip any extra spaces
    ind_row_data = [data.text.strip() for data in row_data]
    
    # Step 3: Append the row's data to the all_rows_data list
    all_rows_data.append(ind_row_data)

# Step 4: Create a DataFrame from all the rows at once
df1 = pd.DataFrame(all_rows_data, columns=world_table_title)

# Now you can print or use the df as needed
df1
```
## Explanation of the Code

### 1. Importing Libraries:

- **os**: For checking the current working directory.
- **BeautifulSoup**: From `bs4` to parse the HTML content of the web page.
- **requests**: To fetch the webpage.
- **pandas**: To handle the tabular data and save it as a CSV file.

### 2. Requesting the Web Page:

The URL of the webpage is defined and a `GET` request is made to fetch the page content using `requests.get(url)`.

### 3. Parsing the HTML:

The HTML content of the page is parsed using `BeautifulSoup(page.text, 'html.parser')` to create a BeautifulSoup object (`soup`).

### 4. Extracting Table Headers:

The table containing the company data is located using `soup.find_all('table')[0]`, and the table headers are extracted using `find_all('th')`.  
These headers are then stripped of any extra whitespace using `.strip()` and stored in `world_table_title`.

### 5. Creating an Empty DataFrame:

A new `pandas` DataFrame `df` is created with columns named after the table headers extracted in the previous step.

### 6. Extracting Table Rows:

All table rows (`tr` elements) are extracted using `find_all('tr')`.  
A loop iterates over each row (excluding the first row, which contains the headers), extracts the data cells (`td` elements), and strips any extra whitespace from them.  
Each row's cleaned data is then added to the DataFrame.

### 7. Saving Data to CSV:

Once the DataFrame `df` is populated with all the data, it is saved as a CSV file using `df.to_csv()`. The path to the CSV file is specified in the function argument.

### 8. Alternative Data Processing:

The second block of code shows an alternative approach, where the data is accumulated in a list `all_rows_data` and then converted into a DataFrame `df1` at the end, rather than updating the DataFrame row by row in the first approach.

### 9. Output:

Finally, the resulting DataFrame `df1` is available for inspection, and all the rows are stored in the variable `all_rows_data`. The script then prints or returns the table.

---

This script will scrape data from the Wikipedia page containing the largest U.S. companies by revenue, process it into a structured format (DataFrame), and save it as a CSV file for further use.


## Author

This project was created and maintained by [Pankaj Singh Bisht](https://github.com/pbisht2105).

You can contact me at: [pbisht2105@gmail.com](mailto:pbisht2105@gmail.com).
