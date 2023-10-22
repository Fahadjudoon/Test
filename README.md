import pandas as pd
import re

# Function to extract and save matching content to a list
def extract_and_save_matching_content(input_csv):
    # Read the CSV file into a pandas DataFrame
    df = pd.read_csv(input_csv)

    # Define a regular expression pattern to match the "0x4c7" format
    pattern = r'(\S+) .* Sender: (\S+) trotz (.*)$'

    # Create an empty list to store the matching content
    matching_content = []

    # Loop through each row and extract matching content
    for row in df['Transition']:
        match = re.search(pattern, row)
        if match:
            matching_content.append(match.group(1))

    return matching_content

# Usage:
input_csv = 'your_new_dataset.csv'
matching_content_list = extract_and_save_matching_content(input_csv)

# Now, matching_content_list contains the matched content

