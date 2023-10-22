import pandas as pd
import numpy as np

# Function to process and save the data
def process_and_save_data(input_csv, output_csv):
    # Read the CSV file into a pandas DataFrame
    df = pd.read_csv(input_csv)

    # Define a function to process the 'Transition' column
    def process_transition(transition):
        if pd.notna(transition):
            parts = transition.split()
            part_1 = parts[0]
            part_2 = parts[1]
            part_3 = parts[4].split("Gender:")[1]
            part_4 = parts[-1]
            return part_1, part_2, part_3, part_4
        return np.nan, np.nan, np.nan, np.nan

    # Apply the process_transition function to the 'Transition' column
    df[['Part1', 'Part2', 'Part3', 'Part4']] = df['Transition'].apply(process_transition).apply(pd.Series)

    # Save the DataFrame with the extracted data to a new CSV file
    df.to_csv(output_csv, index=False)

# Usage:
input_csv = 'your_file.csv'
output_csv = 'processed_data.csv'
process_and_save_data(input_csv, output_csv)

