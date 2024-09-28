================================================================================
Export-ADUserHashes.ps1 & Import-ADUserHashes.ps1
================================================================================

Author: bsparrow@concurrency.com
Date: 2024-08-07

--------------------------------------------------------------------------------
DESCRIPTION
--------------------------------------------------------------------------------

These PowerShell scripts are designed to export and import Active Directory 
(AD) user account password hashes between domains, specifically for users 
with a specified AD attribute set to "migrate". These scripts are designed
to be able to run on separated environments without connectivity to the other.
Files generated during the export must be manually copied to the machine where
they will be imported.

--------------------------------------------------------------------------------
PREREQUISITES
--------------------------------------------------------------------------------

- Ensure you have the necessary permissions to run these scripts in the 
  source and target domains.
- The 'DSInternals' PowerShell module must be installed and up to date.
- The AD attribute that will be used to filter users (default is 'pager') 
  should be set to "migrate" for the accounts you wish to process.

--------------------------------------------------------------------------------
EXPORT SCRIPT (Export-ADUserHashes.ps1)
--------------------------------------------------------------------------------

1. Checks if the 'DSInternals' module is installed and up to date. If not, 
   it will install or update the module.

2. Prompts you to enter the AD attribute to filter on. If no attribute is 
   provided, it defaults to 'pager'.

3. Uses cached credentials for the source domain if available. If not, it 
   prompts for credentials and caches them for future use.

4. Retrieves all user account hashes from the source domain and filters them 
   based on the specified AD attribute being set to "migrate".

5. Exports the filtered account hashes to 'C:/scripts/sourceHashes.xml'.

6. Exports necessary domain information and the attribute used to filter 
   users to 'C:/scripts/exportData.xml'.

7. Displays a success message with the count of exported accounts in green.

--------------------------------------------------------------------------------
IMPORT SCRIPT (Import-ADUserHashes.ps1)
--------------------------------------------------------------------------------

1. Checks if the `DS-Internals` module is installed and up to date. If not, 
   it will install or update the module.

2. Uses cached credentials for the target domain if available. If not, it 
   prompts for credentials and caches them for future use.

3. Imports the domain information and the attribute used to filter users from 
   'C:/scripts/exportData.xml'.

4. Imports the filtered account hashes from 'C:/scripts/sourceHashes.xml'.

5. Synchronizes the password hashes for the imported users in the target domain.

6. Displays a success message with the count of imported accounts in green.

--------------------------------------------------------------------------------
INTERACTION & REQUIREMENTS
--------------------------------------------------------------------------------

- During the execution of the export script, you will be prompted to enter the 
  AD attribute to filter on. If no attribute is provided, it defaults to 'pager'.
  
- Ensure the specified AD attribute for user accounts in the source domain is 
  set to "migrate".

- The scripts use cached credentials if available. If the credentials are not 
  available or if the operation fails, you will be prompted to provide credentials.

--------------------------------------------------------------------------------
USAGE
--------------------------------------------------------------------------------

1. Run the Export Script: Export-ADUserHashes.ps1

   Follow the prompts to enter the AD attribute and provide credentials if needed.
   The script will export the account hashes for users with the specified attribute 
   set to "migrate".

2. Copy the exported files ('sourceHashes.xml' and 'exportData.xml') to the 
   target domain environment.

3. Run the Import Script: Import-ADUserHashes.ps1

   Follow the prompts to provide credentials if needed. The script will import 
   the account hashes and synchronize passwords for users with the specified 
   attribute set to "migrate".

--------------------------------------------------------------------------------
DISCLAIMER
--------------------------------------------------------------------------------

This script was partially written, formatted, and documented by ChatGPT, an AI 
language model developed by OpenAI. While significant effort has been made to 
ensure the accuracy and reliability of the script, it is important to note the 
following:

1. Validation Required: All scripts and code provided should be thoroughly 
   validated and tested in a controlled environment before being executed in 
   a production environment. This is to ensure that they function as intended 
   and do not cause unintended consequences.

2. Potential Bugs: Despite careful review, there may still be unintended bugs 
   or issues present in the script. Users are encouraged to review the code and 
   make any necessary adjustments to suit their specific requirements and 
   environment.

3. Security Considerations: Handling credentials and sensitive data requires 
   careful attention to security best practices. Ensure that credential files 
   are stored securely and access is restricted to authorized personnel only.

4. Customization: The script may require customization to fit the unique setup 
   and requirements of your Active Directory environment. Users should have a 
   good understanding of their AD schema and configuration before making any 
   changes.

5. No Warranty: This script is provided "as-is" without any warranty of any 
   kind, either expressed or implied. The author and OpenAI disclaim all 
   warranties, including, but not limited to, the implied warranties of 
   merchantability and fitness for a particular purpose.

By using this script, you acknowledge that you understand and accept these 
conditions and take full responsibility for any outcomes resulting from its 
use.

--------------------------------------------------------------------------------
LICENSE
--------------------------------------------------------------------------------

This work is licensed under the Creative Commons Attribution 4.0 International 
License. To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/

--------------------------------------------------------------------------------
VERSION HISTORY
--------------------------------------------------------------------------------

1.0 - Initial Release
