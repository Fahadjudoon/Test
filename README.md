import pandas as pd

# Load the CSV file into a pandas DataFrame
df = pd.read_csv("your_file.csv")

# Filter the DataFrame to select rows with "Transition" equal to "Fehler Zyklustyp 1"
filtered_df = df[df["Transition"] == "Fehler Zyklustyp 1"]

# Create a dictionary to store the desired format (0x342 as key, PAN_DF_13 as value)
format_dict = {}
for index, row in filtered_df.iterrows():
    machine_name = row["MachineName"]
    # Extract the values of interest from the "MachineName" column
    machine_name_parts = machine_name.split("__")
    if len(machine_name_parts) >= 3:
        key, value = machine_name_parts[1], machine_name_parts[2]
        format_dict[key] = value

# Now, format_dict contains the desired key-value pairs

# Print the key-value pairs (you can save them to a file if needed)
for key, value in format_dict.items():
    print(f"Key: {key}, Value: {value}")

