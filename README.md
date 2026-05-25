Outlook Cleanser Python Model
1. Purpose

The Outlook Cleanser Python Model is an automation developed to reduce manual mailbox cleanup effort for the NAV team. The model connects directly to Outlook using Python and automatically reviews emails within the mailbox to identify:

Duplicate emails
No-action emails
Emails requiring category updates
Emails that match predefined helper-file rules

The model helps improve mailbox organization and operational efficiency by reducing the amount of manual review required by analysts.

The automation uses:

Outlook COM connection
Helper Excel files
Category logic
Sender/domain matching
Subject keyword matching
Duplicate email comparison logic

This process is executed through Dev Shell.

2. Process Overview

The Outlook Cleanser Model performs the following activities internally:

Step	Process
1	Connects to Outlook mailbox
2	Reads Inbox emails
3	Extracts email properties
4	Reads helper mapping file
5	Identifies no-action emails
6	Identifies duplicate emails
7	Applies categories back to Outlook
8	Updates mailbox tagging
3. Required Inputs
Input File / Source	Purpose
Outlook Mailbox	Source of emails
Helper Excel File	Contains keyword/category rules
Python Script	Main automation script
Shared Drive Access	Required for helper/output files
4. One-Time Package Installation

Before running the model for the first time, install required packages in Dev Shell.

pip install pandas numpy openpyxl xlsxwriter customtkinter pywin32 pyxlsb virtualenv autopep8 pylint black tkcalendar pyinstaller python-dateutil PyMuPDF fuzzywuzzy pdfplumber msoffcrypto-tool xlrd

This only needs to be completed once.

5. How to Execute the Model
Step 1 – Open Outlook

Before running the model:

Open Outlook
Confirm mailbox is fully loaded
Confirm Inbox is synced
Confirm shared mailbox is accessible

Do not execute the model if Outlook is frozen or disconnected.

Step 2 – Open Dev Shell

Launch Dev Shell from the approved corporate environment.

Wait until terminal loads completely.

Step 3 – Navigate to Model Folder

Example:

R:
cd "R:\Mumbai\EMEA FUNDS\NAV GATHERING\GLOBAL NAV GATHERING\Automation\Email Tagging Modified(Internal) - JPM\New JPM code"

The path may vary depending on the environment.

Step 4 – Execute Python Script
python "TAG.py"

After execution begins, do not close Dev Shell.

6. Detailed Process Explanation
6.1 Outlook Connection

The model first creates an Outlook COM connection using pywin32.

This allows Python to:

Read Outlook folders
Read email properties
Update categories
Access shared mailboxes

The model attempts to connect to:

Main mailbox
Shared mailbox
Backup mailbox path if needed
6.2 Reading Emails

The model scans Inbox emails and extracts:

Subject
Sender email
Categories
EntryID
Attachment names
Email body

EntryID is important because it uniquely identifies the Outlook message.

6.3 Helper File Logic

The model reads a helper Excel file containing:

Approved sender emails
Domains
Subject keywords
Categories

The helper file is used to determine:

No-action emails
Auto-tagging logic
Category assignment
6.4 Duplicate Detection Logic

The model identifies duplicate emails using:

Email subject
Email body similarity
Attachment names

Image attachments such as:

.png
.jpg
.jpeg

are ignored during duplicate comparison.

6.5 Outlook Category Updates

Once matching logic is complete, the model updates Outlook categories automatically.

Examples:

No Action
Duplicate
Delaware
External Sender
7. Validation Steps

After execution:

7.1 Validate Categories

Review sample emails and confirm:

Correct category applied
No incorrect tagging
No important client emails incorrectly categorized
7.2 Validate Duplicate Logic

Confirm duplicate emails are actual duplicates.

Check:

Subject
Sender
Attachments
7.3 Validate No-Action Logic

Confirm helper-file rules worked correctly.

Ensure:

Generic keywords did not incorrectly match emails
No critical emails were tagged as no-action
8. Common Errors
Error	Possible Cause
Outlook COM error	Outlook closed/frozen
Mailbox not found	Wrong mailbox name
No emails tagged	Filter too restrictive
Wrong emails tagged	Incorrect helper rule
Duplicate logic incorrect	Comparison logic too broad
Category not updating	Outlook sync issue
9. Debugging Procedure

Debugging should always begin by identifying:

Whether Outlook connected successfully
Whether emails were read successfully
Whether helper file loaded correctly
Whether category logic matched correctly
10. Print Statement Debugging Examples
10.1 Validate Outlook Connection
print(account.Name)
print(inbox.Name)
print(messages.Count)

Purpose:

Confirms Outlook connection
Confirms Inbox loaded
Confirms message count
10.2 Validate Email Reading
print(message.Subject)
print(message.SenderEmailAddress)
print(message.Categories)

Purpose:

Confirms emails are being read correctly
Confirms sender extraction
Confirms category extraction
10.3 Validate DataFrame Creation
print(df_inbox.shape)
print(df_inbox.columns)
print(df_inbox.head())

Purpose:

Confirms inbox dataset created successfully
10.4 Validate Helper File
print(df_helper.shape)
print(df_helper.columns)
print(df_helper.head())

Purpose:

Confirms helper file loaded correctly
10.5 Validate Duplicate Logic
print(df_duplicate_emails.shape)
print(df_duplicate_emails.head())

Purpose:

Confirms duplicate detection output
10.6 Validate Category Updates
print(category_dict)
print(len(category_dict))

Purpose:

Confirms categories being pushed to Outlook
11. Recovery Steps

If the model fails:

Close Outlook
Restart Outlook
Confirm mailbox sync
Reopen Dev Shell
Add print statements
Rerun model
Validate categories manually
12. Important Operational Notes
Never blindly trust automated tagging
Always review sample emails
Do not delete emails through automation
Keep helper rules controlled
Escalate major tagging issues immediately
Maintain audit copies of helper files
SOP 3 – LATAM Funds Processing Python Model
1. Purpose

The LATAM Funds Processing Python Model is used to automate processing of LATAM local fund data.

The model:

Reads LATAM source files
Maps TAX_ID to Fund UCN
Calculates NAV values
Calculates Monthly Performance
Generates standardized output files

The process reduces manual calculation and improves consistency in LATAM fund reporting.

The model is executed through Dev Shell.

2. Process Overview
Step	Process
1	Reads LATAM source file
2	Cleans source data
3	Reads TAX_ID helper file
4	Maps Fund UCN
5	Identifies latest reporting dates
6	Combines current and prior data
7	Calculates NAV and performance
8	Generates final output
3. Required Inputs
Input	Purpose
LATAM Source File	Main fund data
TAX_ID Mapping File	Fund UCN mapping
CVM Database File	Historical comparison
Python Script	Main processing logic
4. One-Time Package Installation
pip install pandas numpy openpyxl xlsxwriter customtkinter pywin32 pyxlsb virtualenv autopep8 pylint black tkcalendar pyinstaller python-dateutil PyMuPDF fuzzywuzzy pdfplumber msoffcrypto-tool xlrd
5. How to Execute the Model
Step 1 – Open Dev Shell

Launch Dev Shell.

Step 2 – Navigate to Folder
G:
cd "G:\2 - Transitory Records\NAV\Hedge Funds\Python Programs\LATAM web extraction - Local Funds"
Step 3 – Execute Python Script
python "LATAM_funds_processing_main.py"

Wait until execution completes.

6. Detailed Process Explanation
6.1 Reading Source File

The model reads the LATAM source file.

The source file may:

Use semicolon delimiters
Require manual column cleanup
Contain local formatting

The model standardizes the structure automatically.

6.2 Data Cleanup

The model:

Removes unnecessary columns
Renames columns
Converts date formats
Converts numeric formats

This ensures calculations work correctly.

6.3 TAX_ID Mapping

The model merges source data with:

TAX_ID mapping file

This adds:

Fund UCN
Fund Name

Rows without Fund UCN are removed.

6.4 Date Logic

The model identifies:

Most recent date
Prior reporting date

This is required for monthly performance calculation.

6.5 NAV and Performance Calculation

The model calculates:

NAV in thousands
Monthly Performance

The model compares:

Current values
Prior values

to calculate performance.

6.6 Output Generation

The model creates:

Final Excel output
Updated fund dataset
Calculation-ready output
7. Validation Steps

After execution:

7.1 Validate Fund UCN Mapping

Ensure:

No missing UCN
Leading zeros preserved
7.2 Validate Latest Dates

Ensure:

Correct reporting month selected
Correct prior date selected
7.3 Validate NAV Values

Cross-check sample funds against source file.

7.4 Validate Monthly Performance

Review:

Extreme values
Blank performance rows
Negative performance values
8. Common Errors
Error	Possible Cause
File not found	Wrong folder
Column error	Source format changed
Missing Fund UCN	TAX_ID mapping missing
Date conversion error	Invalid date format
Blank performance	Prior date missing
Output not generated	Output file open
9. Debugging Procedure

Always debug step by step.

Confirm:

Source file loaded
Mapping file loaded
Merge completed correctly
Dates identified correctly
Calculations completed correctly
10. Print Statement Debugging Examples
10.1 Validate Source File
print(df.shape)
print(df.head())
print(df.columns)

Purpose:

Confirms source file loaded correctly
10.2 Validate Mapping File
print(df_ids.shape)
print(df_ids.columns)
print(df_ids.head())

Purpose:

Confirms mapping file loaded successfully
10.3 Validate Merge
print(data.shape)
print(data[['TAX_ID','Fund UCN','Fund Name']].head())

Purpose:

Confirms Fund UCN mapping
10.4 Validate Missing UCN
print(data['Fund UCN'].isna().sum())

Purpose:

Shows rows that will be dropped
10.5 Validate Date Logic
print(unique_dates)
print(most_recent_date)
print(prior_date)

Purpose:

Confirms reporting dates selected correctly
10.6 Validate Final Output
print(data_combined.shape)
print(data_combined.tail())

Purpose:

Confirms final dataset structure
10.7 Validate Calculations
print(data_combined[['Fund Name','NAV (Thous)','Monthly_Performance']].tail())

Purpose:

Confirms NAV and performance calculations
11. Recovery Steps

If the model fails:

Close all Excel files
Validate source files
Validate mapping files
Restart Dev Shell
Add print statements
Rerun model
Validate output
12. Important Operational Notes
Always validate Fund UCN mapping
Never ignore dropped rows
Validate performance calculations manually
Retain source/output files for audit
Escalate source structure changes immediately





Prompt Name: Outlook Cleanser Python Debugging Support

I am debugging the Outlook Cleanser Python model used for mailbox tagging, no-action email identification, and duplicate email detection.

Issue:
[paste issue here]

Error message from Dev Shell:
[paste full error here]

Code section:
[paste relevant code here]

Files / mailbox used:
- Outlook mailbox:
- Helper file:
- Python file:
- Output/action expected:

Please help me debug this step by step.

Provide:
1. What the error means in simple terms
2. Likely root cause
3. Whether the issue is Outlook-related, mailbox permission-related, category-related, helper file-related, duplicate logic-related, or code-related
4. Exact line or section likely causing the issue
5. What print statements I should add
6. Where I should add those print statements
7. What output I should expect from each print statement
8. How to interpret the print results
9. Step-by-step fix
10. Validation checks after fixing

Important:
- Do not assume mailbox access is correct
- If categories are not updating, suggest Outlook COM checks
- If no-action emails are incorrect, suggest helper file and keyword checks
- If duplicates are wrong, suggest subject/body/attachment comparison checks
- Keep explanation simple enough for an analyst to follow



Prompt Name: LATAM Funds Processing Python Debugging Support

I am debugging the LATAM Funds Processing Python model used for LATAM local fund NAV and monthly performance processing.

Issue:
[paste issue here]

Error message from Dev Shell:
[paste full error here]

Code section:
[paste relevant code here]

Files used:
- LATAM source file:
- TAX_ID mapping file:
- CVM database file:
- Output file:

Please help me debug this step by step.

Provide:
1. What the error means in simple terms
2. Likely root cause
3. Whether the issue is source file-related, delimiter-related, TAX_ID mapping-related, Fund UCN-related, date conversion-related, NAV calculation-related, performance calculation-related, or code-related
4. Exact line or section likely causing the issue
5. What print statements I should add
6. Where I should add those print statements
7. What output I should expect from each print statement
8. How to interpret the print results
9. Step-by-step fix
10. Validation checks after fixing

Important:
- Do not assume TAX_ID mapping is complete
- If output is blank, check rows dropped after Fund UCN mapping
- If performance is wrong, check current and prior date logic
- If CSV is not reading correctly, check delimiter and column split logic
- Keep explanation simple enough for an analyst to follow
