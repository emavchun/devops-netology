# devops-netology

There is terraform/.gitignore file. 

This file provides to ignore below files/directories from commits:
1. .terraform directories in any subdirectories within /terraform directory
2. terraform state files (all files with extension tfstate and files which contain 'tfstate' in its name)
3. crash.log file
4. all files with .tfvars extension
5. override.tf files and files ended with _override.tf
6. override.tf.json and files endedd with _override.tf.json
7. files named .terraformrc or terraform.rc

