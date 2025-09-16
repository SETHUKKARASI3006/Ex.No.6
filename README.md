# Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

## Date: 16-09-2025
## Register no. : 212223230201
## Aim:
Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools

## AI Tools Required:
- Microsoft Copilot
- Google Gemini
- OpenAI ChatGPT
  
## Prompt:

```
How can you write a single function that automatically reads both .csv and .json files into a list of dictionaries?
```

## Code Implementation:

Microsoft Copilot:

```
import csv
import json
import os

def read_file_to_dicts(file_path):
    _, ext = os.path.splitext(file_path)
    ext = ext.lower()

    if ext == '.csv':
        with open(file_path, mode='r', encoding='utf-8') as f:
            reader = csv.DictReader(f)
            return [row for row in reader]

    elif ext == '.json':
        with open(file_path, mode='r', encoding='utf-8') as f:
            data = json.load(f)
            if isinstance(data, list):
                return data
            elif isinstance(data, dict):
                return [data]
            else:
                raise ValueError("Unsupported JSON structure")

    else:
        raise ValueError("Unsupported file format. Only .csv and .json are supported.")
```

Google Gemini:

```
import csv
import json
import os

def read_data_to_list_of_dicts(file_path):
    """
    Reads data from a .csv or .json file into a list of dictionaries.

    Args:
        file_path (str): The path to the file.

    Returns:
        list: A list of dictionaries containing the file data.
              Returns an empty list if the file format is not supported.
    """
    _, file_extension = os.path.splitext(file_path)
    data = []

    if file_extension.lower() == '.csv':
        try:
            with open(file_path, mode='r', newline='', encoding='utf-8') as f:
                reader = csv.DictReader(f)
                data = list(reader)
        except FileNotFoundError:
            print(f"Error: The file {file_path} was not found.")
        except Exception as e:
            print(f"An error occurred while reading the CSV file: {e}")

    elif file_extension.lower() == '.json':
        try:
            with open(file_path, mode='r', encoding='utf-8') as f:
                data = json.load(f)
                # Ensure the loaded data is a list of dictionaries
                if not isinstance(data, list) or not all(isinstance(item, dict) for item in data):
                    print("Warning: JSON file does not contain a list of dictionaries. Returning as-is.")
        except FileNotFoundError:
            print(f"Error: The file {file_path} was not found.")
        except json.JSONDecodeError:
            print(f"Error: Could not decode JSON from the file {file_path}.")
        except Exception as e:
            print(f"An error occurred while reading the JSON file: {e}")

    else:
        print(f"Unsupported file format: {file_extension}. Please use .csv or .json.")

    return data

# --- Example Usage ---

# Create dummy .csv and .json files for demonstration
sample_csv_data = [
    {'name': 'Alice', 'age': '30', 'city': 'New York'},
    {'name': 'Bob', 'age': '25', 'city': 'Los Angeles'}
]
with open('sample.csv', 'w', newline='', encoding='utf-8') as csvfile:
    fieldnames = ['name', 'age', 'city']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(sample_csv_data)

sample_json_data = [
    {'name': 'Charlie', 'age': 35, 'city': 'Chicago'},
    {'name': 'Diana', 'age': 28, 'city': 'Houston'}
]
with open('sample.json', 'w', encoding='utf-8') as jsonfile:
    json.dump(sample_json_data, jsonfile, indent=4)

# Test the function with both file types
csv_data = read_data_to_list_of_dicts('sample.csv')
print("Data from CSV file:")
print(csv_data)

json_data = read_data_to_list_of_dicts('sample.json')
print("\nData from JSON file:")
print(json_data)
```

OpenAI ChatGPT:

```
import csv
import json
import os

def read_file_as_dicts(file_path):
    """
    Reads both CSV and JSON files and converts them into a list of dictionaries.
    :param file_path: Path to the .csv or .json file
    :return: list of dictionaries
    """
    if not os.path.exists(file_path):
        raise FileNotFoundError(f"File {file_path} does not exist")

    file_extension = os.path.splitext(file_path)[1].lower()

    if file_extension == ".csv":
        with open(file_path, mode="r", encoding="utf-8") as f:
            reader = csv.DictReader(f)
            return [row for row in reader]

    elif file_extension == ".json":
        with open(file_path, mode="r", encoding="utf-8") as f:
            data = json.load(f)
            # Ensure JSON is always returned as list of dicts
            if isinstance(data, dict):
                return [data]
            elif isinstance(data, list):
                return data
            else:
                raise ValueError("Unsupported JSON format")

    else:
        raise ValueError("Unsupported file format. Use .csv or .json")


# Example Usage
if __name__ == "__main__":
    # Test with CSV
    csv_data = read_file_as_dicts("sample.csv")
    print("CSV Data:", csv_data)

    # Test with JSON
    json_data = read_file_as_dicts("sample.json")
    print("JSON Data:", json_data)
```

## Explanation:
Experiment the persona pattern as a programmer for any specific applications related with your interesting area. 
Generate the output using more than one AI tool and based on the code generation analyse and discussing that. 

### Persona Pattern:
As a data engineer working in the domain of automated data ingestion for analytics, this function is designed to streamline the process of reading structured data from common formats. It abstracts file handling logic and ensures compatibility across different data pipelines.

### AI Tool Comparison:


<img width="2376" height="1440" alt="_- visual selection" src="https://github.com/user-attachments/assets/510c78e6-e4e7-4d09-853c-a69960a805de" />

## Insights:
- All tools generated similar logic using csv.DictReader and json.load.
- Copilot provided the most comprehensive structure with proper error handling and support for both list and dict JSON formats.
- ChatGPT suggested modularizing the code for scalability.
- Gemini/Bard required manual prompting for edge case handling.

## Conclusion:
The experiment successfully demonstrated how a single Python function can be designed to handle multiple data formats. By leveraging multiple AI tools, we were able to compare code quality, robustness, and clarity. This approach enhances productivity and helps in selecting the best implementation strategy for real-world applications.

## Result: 
The corresponding Prompt is executed successfully.
