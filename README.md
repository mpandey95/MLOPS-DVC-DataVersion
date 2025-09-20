MLOPS-DVC-DataVersion
Welcome to the MLOPS-DVC-DataVersion repository by mpandey95! This project demonstrates a simple workflow for managing data versioning using DVC (Data Version Control) integrated with Git, showcasing best practices for MLOps. Follow the steps below to set up and track data versions effectively.
Prerequisites

Git installed
Python 3.x
DVC (pip install dvc)
Access to an S3 bucket (or other DVC-supported storage)

Setup and Workflow Instructions

Clone or Fork the RepositoryClone or fork this repository to your local machine:  
git clone https://github.com/mpandey95/MLOPS-DVC-DataVersion.git
cd MLOPS-DVC-DataVersion


Create and Run dvc.pyCreate a Python script named dvc.py to generate a sample CSV file in a data folder. Use the following code:  
import pandas as pd
import os

# Create a sample DataFrame with column names
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'City': ['New York', 'Los Angeles', 'Chicago']}
df = pd.DataFrame(data)

# Ensure the "data" directory exists at the root level
data_dir = 'data'
os.makedirs(data_dir, exist_ok=True)

# Define the file path
file_path = os.path.join(data_dir, 'sample_data.csv')

# Save the DataFrame to a CSV file, including column names
df.to_csv(file_path, index=False)
print(f"CSV file saved to {file_path}")

Run the script to generate the initial data/sample_data.csv file:  
python dvc.py


Git Add-Commit-PushStage, commit, and push the initial code to your Git repository:  
git add .
git commit -m "Initial commit with dvc.py"
git push origin main


Initialize DVCInstall DVC if not already installed:  
pip install dvc

Initialize DVC in your repository:  
dvc init

This creates .dvcignore and .dvc files.

Set Up DVC Remote StorageCreate a directory named S3 for remote storage configuration:  
mkdir S3

Configure the DVC remote:  
dvc remote add -d myremote S3


Add Data to DVCTrack the data folder with DVC:  
dvc add data/

DVC will prompt you to stop tracking the data folder in Git. Follow the instructions:  
git rm -r --cached 'data'
git commit -m "Stop tracking data folder with Git"

Add the data.dvc file to Git:  
git add .gitignore data.dvc


Commit and Push Data to DVCCommit the data to DVC and push to the remote storage:  
dvc commit
dvc push


Git Add-Commit-Push for Version 1Commit the DVC metadata and push to Git:  
git add .
git commit -m "Version 1: Initial data version"
git push origin main


Update Data for Version 2Modify dvc.py to append a new row to the DataFrame. Update the script to:  
import pandas as pd
import os

# Create a sample DataFrame with column names
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'City': ['New York', 'Los Angeles', 'Chicago']}
df = pd.DataFrame(data)

# Adding new row to df for V2
new_row_loc = {'Name': 'GF1', 'Age': 20, 'City': 'City1'}
df.loc[len(df.index)] = new_row_loc

# Ensure the "data" directory exists at the root level
data_dir = 'data'
os.makedirs(data_dir, exist_ok=True)

# Define the file path
file_path = os.path.join(data_dir, 'sample_data.csv')

# Save the DataFrame to a CSV file, including column names
df.to_csv(file_path, index=False)
print(f"CSV file saved to {file_path}")

Run the script:  
python dvc.py

Check changes with:  
dvc status


Commit and Push Version 2Commit and push the updated data to DVC:  
dvc commit
dvc push

Commit and push to Git:  
git add .
git commit -m "Version 2: Added new row to data"
git push origin main


Update Data for Version 3Modify dvc.py again to append another row:  
import pandas as pd
import os

# Create a sample DataFrame with column names
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'City': ['New York', 'Los Angeles', 'Chicago']}
df = pd.DataFrame(data)

# Adding new row to df for V2
new_row_loc = {'Name': 'GF1', 'Age': 20, 'City': 'City1'}
df.loc[len(df.index)] = new_row_loc

# Adding new row to df for V3
new_row_loc2 = {'Name': 'GF2', 'Age': 30, 'City': 'City2'}
df.loc[len(df.index)] = new_row_loc2

# Ensure the "data" directory exists at the root level
data_dir = 'data'
os.makedirs(data_dir, exist_ok=True)

# Define the file path
file_path = os.path.join(data_dir, 'sample_data.csv')

# Save the DataFrame to a CSV file, including column names
df.to_csv(file_path, index=False)
print(f"CSV file saved to {file_path}")

Run the script:  
python dvc.py

Check changes:  
dvc status


Commit and Push Version 3Commit and push the updated data to DVC:  
dvc commit
dvc push

Commit and push to Git:  
git add .
git commit -m "Version 3: Added another row to data"
git push origin main


Verify StatusCheck the status of DVC and Git to ensure everything is up to date:  
dvc status
git status



Branding
This project is proudly maintained by mpandey95. It aims to simplify MLOps workflows by demonstrating data versioning with DVC and Git integration. Follow for more MLOps and data engineering projects!
License
This project is licensed under the MIT License. See the LICENSE file for details.