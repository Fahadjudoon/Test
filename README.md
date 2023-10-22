def process_transition(transition):
        if pd.notna(transition):
            parts = transition.split()
            part_1 = parts[0]
            part_2 = parts[1]
            part_3 = None
            part_4 = parts[-1]
            
            # Create a list to store parts after the second space
            additional_parts = []
            for part in parts[2:]:  # Start from the third part
                if "Sender:" in part:
                    break  # Stop when "Sender" is found
                additional_parts.append(part)
            
            if additional_parts:
                part_3 = " ".join(additional_parts)
            
            return part_1, part_2, part_3, part_4
        return np.nan, np.nan, np.nan, np.nan
