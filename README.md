import pandas as pd

# Sample data
PAD_IDs = [340, 750, 492, 650, 12493]
BN_IO_IDs = [456, 345, 234]

# Create a DataFrame to track appearance in PAD_IDs and BN_IO_IDs
result_df = pd.DataFrame(columns=['FRTID', 'ACC', 'Appeared or Not'])

# Iterate through new_dict
for frtid, pwfcnd_list in new_dict.items():
    appeared = False  # Flag to check if FRTID appeared in any list
    for pwfcnd in pwfcnd_list:
        if pwfcnd == 'P_A_D' and frtid in PAD_IDs:
            appeared = True
            result_df = result_df.append({'FRTID': frtid, 'ACC': 'P_A_D', 'Appeared or Not': 'Appeared'}, ignore_index=True)
        elif pwfcnd == 'P_A_K' and frtid in BN_IO_IDs:
            appeared = True
            result_df = result_df.append({'FRTID': frtid, 'ACC': 'P_A_K', 'Appeared or Not': 'Appeared'}, ignore_index=True)

    # If FRTID didn't appear in any list, mark it as "Not Appeared"
    if not appeared:
        result_df = result_df.append({'FRTID': frtid, 'ACC': 'Not Applicable', 'Appeared or Not': 'Not Appeared'}, ignore_index=True)

# Set FRTID column to integer type
result_df['FRTID'] = result_df['FRTID'].astype(int)

print(result_df)

