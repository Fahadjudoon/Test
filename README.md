import pandas as pd

# Assuming you have your DataFrame already loaded as NK_df

# Step 1: Filter the DataFrame
filtered_df = NK_df[(NK_df['LSTTYP'] == '1_COM') & (NK_df['DIR'] == 'OUTPUT') & (NK_df['BUSSNM'] == 'CAN_1')]

# Step 2: Create a dictionary to store unique 'FRTID' and their corresponding 'PWFCND'
frtid_pwfcnd_dict = {}

for index, row in filtered_df.iterrows():
    frtid = row['FRTID']
    pwfcnd = row['PWFCND']
    if frtid not in frtid_pwfcnd_dict:
        frtid_pwfcnd_dict[frtid] = pwfcnd

# Step 3: Convert the dictionary to a DataFrame
result_df = pd.DataFrame(list(frtid_pwfcnd_dict.items()), columns=['FRTID', 'PWFCND'])

# Step 4: Save the result DataFrame to a CSV file
result_df.to_csv('result.csv', index=False)
