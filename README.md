# Initial-Data-Transformation-Script
import pandas as pd
import numpy as np

def transform_data(file_path, output_path):
    """
    Cleans and transforms a raw CSV file.

    Args:
        file_path (str): Path to the raw CSV file.
        output_path (str): Path to save the cleaned CSV file.
    """
    try:
        df = pd.read_csv(file_path)
    except FileNotFoundError:
        print(f"Error: The file at {file_path} was not found.")
        return
    
    # Handle missing values by filling them with a placeholder
    df.fillna('N/A', inplace=True)
    
    # Standardize date formats in a column named 'date'
    if 'date' in df.columns:
        df['date'] = pd.to_datetime(df['date'], errors='coerce')
        df.dropna(subset=['date'], inplace=True)
    
    # Save the cleaned data
    df.to_csv(output_path, index=False)
    print(f"Data successfully cleaned and saved to {output_path}")

if __name__ == "__main__":
    # Example usage
    raw_file = 'raw_data.csv'
    cleaned_file = 'cleaned_data.csv'
    transform_data(raw_file, cleaned_file)
