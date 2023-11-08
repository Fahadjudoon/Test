match = re.search(r"(\w+__PAN_DF_\d+__0x\w+)", machine_name)
    
    if match:
        key_value = match.group(1)
        key, value = key_value.split("__")[3], key_value.split("__")[1]
        format_dict[key] = value
