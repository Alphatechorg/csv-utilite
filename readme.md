# CSV-UTILITE DOCUMENTATION

csv-utilite is a Python package designed to facilitate working with CSV files in a more convenient and Pythonic manner compared to the built-in csv module. It provides a set of modules with classes and functions to perform various tasks related to CSV file handling.

## Installation

You can install csv-utilite via pip:

```pip install csv_utilite ```

## CORE MODULES

### Reader

This module contains the Reader class, which extends the functionality of csv.reader. It offers additional features such as automatic type casting, handling missing values, and support for different dialects.

``` from csv_utilite import Reader ```

### Example usage
```python
from csv_utilite import Reader 

with open('myfile.csv', 'r') as file:
  reader = Reader(file, dialect='excel', type_cast=True, na_values=['', 'NULL'])
  for row in reader:
    print(row)  

```
   

### Writer

The writer.py module includes the Writer class, a subclass of csv.writer, enhanced with features like automatic type casting and support for different dialects.

``` from csv_utilite import Writer ```
 
### Example usage
```python
from csv_utilite import Writer
with open('output.csv', 'w', newline='') as file:
    writer = Writer(file, dialect='excel', na_rep='NA')
    writer.writerow([1, 2.5, True, None, 'abc'])
    writer.writerows([[3, 4.7, False, 'NA', ''], [None, None, True, 'NA', 'xyz']])

```
## UTILITY MODULES

### Manipulation

This module provides functions for common operations on CSV data, such as filtering rows, sorting, merging multiple files, and handling headers.


``` from csv_utilite import filter_rows, sort_rows ```

### Example usage
```python
from csv_utilite import filter_rows, sort_rows, merge_files  
# Filter rows
data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
filtered_data = filter_rows(data, lambda row: sum(row) > 10)
print(filtered_data)  

# Sort rows
sorted_data = sort_rows(data, key=lambda row: row[1], reverse=True)
print(sorted_data)  

# Merge files
file_paths = ['file1.csv', 'file2.csv', 'file3.csv']
output_path = 'merged.csv'
merge_files(file_paths, output_path, dialect='excel', has_header=True)

```

### Formatting

formatting.py includes functions for formatting CSV data, such as adding or removing quotes, handling newlines within fields, and customizing delimiters.


``` from csv_utilite import add_quotes, remove_quotes ```

### Example usage

```python
import csv
from csv_utilite import quote_fields, remove_quotes, handle_newlines

# Quote fields
data = [['Name', 'Age', 'City'], ['John', 25, 'New York'], ['Jane', 30, 'London, UK']]
quoted_data = quote_fields(data, quoting=csv.QUOTE_NONNUMERIC)
print(quoted_data)  

# Remove quotes
quoted_data = [['"Name"', '"Age"', '"City"'], ['"John"', '"25"', '"New York"'], ['"Jane"', '"30"', '"London, UK"']]
unquoted_data = remove_quotes(quoted_data)
print(unquoted_data)  

# Handle newlines
data = [['Name', 'Address'], ['John', '123 Main St.\nNew York, NY'], ['Jane', 'Flat 5\nLondon, UK']]
formatted_data = handle_newlines(data, replacement=' ')
print(formatted_data) 

```


### Validation

The validation.py module provides functions to validate CSV data against predefined rules or schemas, ensuring data integrity and consistency.

``` from csv_utilite import validate_schema ```

### Example usage

```python
from csv_utilite import validate_rows, validate_headers
# Validate rows
data = [[1, 2, 3], [4, 'five', 6], [7, 8, 'nine']]
validators = {
    0: lambda x: isinstance(x, int) and x > 0,
    1: lambda x: isinstance(x, int) or isinstance(x, str),
    2: lambda x: isinstance(x, int) and x < 10
}
valid_data = validate_rows(data, validators)
print(valid_data) 

# Validate headers
headers = ['Name', 'Age', 'City', 'Country']
required_headers = ['Name', 'Age', 'City']
is_valid = validate_headers(headers, required_headers)
print(is_valid) 

```


### conversion

This module contains functions to convert CSV data to and from other formats like JSON, Excel, SQL tables, etc.


``` from csv_utilite import csv_to_json, json_to_csv ```

### Example usage

```python

from csv_utilite import csv_to_json, json_to_csv
# CSV to JSON
data = [['Name', 'Age', 'City'], ['John', 25, 'New York'], ['Jane', 30, 'London']]
json_data = csv_to_json(data[1:], headers=data[0], orient='records')
print(json_data)  

# JSON to CSV
json_data = [{'Name': 'John', 'Age': 25, 'City': 'New York'}, {'Name': 'Jane', 'Age': 30, 'City': 'London'}]
csv_data = json_to_csv(json_data, headers=['Name', 'Age', 'City'])
print(csv_data)  

```

### Generation

The generation.py module includes functions to generate CSV files from various data sources, such as dictionaries, databases, or APIs.


``` from csv_utilite import generate_from_dict ```

# Example usage

``` from csv_utilite import generate_from_db, generate_from_dict ```

```python

from csv_utilite import generate_from_db, generate_from_dict

# Generate CSV from a dictionary
data = {'Name': 'John', 'Age': 25, 'City': 'New York'}
output_path = 'output.csv'
generate_from_dict(data, output_path, headers=['Name', 'Age', 'City'])

# Generate CSV from a list of dictionaries
data = [{'Name': 'John', 'Age': 25, 'City': 'New York'},
        {'Name': 'Jane', 'Age': 30, 'City': 'London'}]
output_path = 'output.csv'
generate_from_dict(data, output_path)

# Generate CSV from a database query (assuming a valid database connection)
query = "SELECT name, age, city FROM users"
db_connection =  ...# ... (initialize database connection)
output_path = 'output.csv'
generate_from_db(query, db_connection, output_path)

```
## Contributions

All meaningful contributions are welcome.

We appreciate any improvements, bug fixes, or new features you can contribute to this project. Feel free to fork this repository, make your changes, and submit a pull request.

# Conclusion
csv-utilite simplifies CSV file handling in Python by providing a comprehensive set of classes and functions for reading, writing, manipulating, formatting, validating, converting, and generating CSV data. With its intuitive API and enhanced features, csv-utilite is a valuable tool for data processing tasks involving CSV files.
