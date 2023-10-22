# Test
import pandas as pd
import numpy as np

# 1. Read the CSV file into a pandas DataFrame
df = pd.read_csv('your_file.csv')

# 2. Extract and process the content in the 'Transition' column
def process_transition(transition):
    # Check if the transition is not empty
    if pd.notna(transition):
        # Split the transition string by space
        parts = transition.split()

        # Extract the specific parts you need
        if len(parts) >= 5:
            part_1 = parts[0]
            part_2 = parts[1]
            part_3 = parts[4]
            part_4 = parts[-1]

            # You can print or use these parts as needed
            print("Part 1 (0x1b5):", part_1)
            print("Part 2 (ST_GWS AE_CAN_FD):", part_2)
            if "Gender:" in part_3:
                part_3 = part_3.split("Gender:")[1]
            print("Part 3 (IPB_BNR):", part_3)
            print("Part 4 (trotz ak ausgeblieben):", part_4)

# Apply the process_transition function to the 'Transition' column
df['Transition'].apply(process_transition)

# Optionally, you can save the extracted data into separate columns if needed
df['Part1'] = df['Transition'].apply(lambda x: x.split()[0] if pd.notna(x) else np.nan)
df['Part2'] = df['Transition'].apply(lambda x: x.split()[1] if pd.notna(x) else np.nan)
df['Part3'] = df['Transition'].apply(lambda x: x.split()[4].split("Gender:")[1] if pd.notna(x) else np.nan)
df['Part4'] = df['Transition'].apply(lambda x: x.split()[-1] if pd.notna(x) else np.nan)

# Save the DataFrame with the extracted data to a new CSV file
df.to_csv('processed_data.csv', index=False)
