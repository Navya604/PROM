# SOP 1 – Day NAV Python Model

# 1. Purpose

The Day NAV Python Model is an automated Python-based extraction and processing model developed to support NAV operational activities for Hedge Funds within NAHF and LATAM HF populations.

The primary objective of the model is to reduce manual extraction effort by automatically reading client files received through Outlook emails and extracting the following information:

* Fund Name
* Fund UCN
* NAV
* MTD Performance
* NAV Date
* Currency
* Additional supporting fund-level information

The model helps improve:

* Operational efficiency
* Accuracy of NAV extraction
* Standardization of output files
* Reduction of manual copy/paste work
* Faster upload readiness for RBRM and workflow processes

The model is executed daily through Dev Shell and supports multiple hedge fund families.

---

# 2. Scope

This SOP applies to:

* NAV Analysts
* Hedge Fund Operations Analysts
* NAV Reporting Team
* Analysts responsible for daily NAV extraction and validation activities

This SOP covers:

* Model setup
* Package installation
* Dev Shell execution
* Input file preparation
* Validation steps
* Debugging process
* Error handling
* Operational recovery steps
* Escalation requirements

---

# 3. IA / Fund Families Covered

The Day NAV model currently supports multiple hedge fund families.

Examples include:

* Bridgewater Associates LP
* Brigade Capital Management LP
* Arena Investors LP
* Mariner Investment Group LLC
* Orbis Investment Management Limited
* Additional supported NAHF and LATAM hedge fund families

Some fund families use:

* PDF extraction
* Excel extraction
* Outlook email extraction
* Website extraction
* Helper mapping files

Each family may have slightly different extraction logic depending on:

* File structure
* NAV layout
* MTD placement
* Naming convention
* Currency format
* File delivery method

---

# 4. Frequency

Frequency:

* Daily

Execution Timing:

* Generally executed during daily NAV gathering process
* Typically after client files are received in Outlook mailbox
* Executed before workflow validation and RBRM upload activities

---

# 5. Prerequisites

Before running the model, confirm the following:

## 5.1 System Access

The analyst must have:

* Dev Shell access
* Python installed
* Shared drive access
* Outlook access
* Folder permissions
* Read/write access to model directories

## 5.2 Required Folders

Ensure the following folders are accessible:

* Input source folder
* Helper/reference file folder
* Output folder
* Audit/archive folder

## 5.3 Required Python Packages

The required packages only need to be installed once in Dev Shell.

---

# 6. One-Time Package Installation in Dev Shell

Open Dev Shell and execute the following command:

```python
pip install pandas numpy openpyxl xlsxwriter customtkinter pywin32 pyxlsb virtualenv autopep8 pylint black tkcalendar pyinstaller python-dateutil PyMuPDF fuzzywuzzy pdfplumber msoffcrypto-tool xlrd
```

Note:

If packages are already installed previously, there is no need to reinstall them every day.

---

# 7. How to Execute the Day NAV Model in Dev Shell

## Step 1 – Open Dev Shell

Open Dev Shell from the approved corporate environment.

Wait until the terminal loads successfully.

---

## Step 2 – Navigate to the Model Directory

Use the appropriate shared drive path.

Example:

```python
G:
cd G:\2 - Transitory Records\NAV\Hedge Funds\Python Programs\Day NAV
```

Important:

The cd command is critical because the model reads helper files and output files from the current working directory.

If the wrong directory is used:

* Files may not load
* Helper mappings may fail
* Output files may not generate
* Incorrect files may be processed

---

## Step 3 – Execute the Python Script

Run the model using:

```python
python day_nav.py
```

or

```python
python "day_nav.py"
```

depending on the file naming convention.

---

## Step 4 – Monitor Dev Shell Terminal

After execution begins, monitor:

* Print statements
* Warning messages
* Missing file alerts
* Merge counts
* Fund extraction counts
* Error traceback messages

Do not close Dev Shell during execution.

---

## Step 5 – Select Files if GUI Opens

Some Day NAV models use a Tkinter GUI/file picker.

If prompted:

* Select the correct source files
* Select the correct workflow/helper file
* Confirm the selected month-end files
* Avoid selecting older files accidentally

Always verify:

* Correct reporting month
* Correct fund family
* Correct NAV date

before proceeding.

---

## Step 6 – Allow Outlook Access Prompt

If Outlook automation is used, a Microsoft Outlook warning may appear.

Example:

“A program is trying to access email information stored in Outlook.”

Action:

* Select Allow access
* Choose the required duration
* Continue execution

If access is denied:

* Email extraction will fail
* Outlook scanning logic will not run

---

# 8. Internal Processing Logic Performed by the Model

The model performs multiple automated steps internally.

## 8.1 Outlook Email Scan

The model scans Outlook mailbox folders searching for:

* Relevant client emails
* Approved categories/tags
* In-scope hedge fund families
* Valid attachments

The model may filter based on:

* Subject line
* Sender email
* Outlook category
* Attachment name
* Date received

---

## 8.2 Attachment Extraction

The model extracts:

* PDF files
* Excel files
* CSV files
* Client return files
* NAV statements

Attachments are saved locally or processed directly.

---

## 8.3 PDF Parsing

For PDF families, the model:

* Reads PDF text
* Searches for NAV values
* Searches for MTD values
* Identifies latest month values
* Extracts fund-level information

Examples:

* Fund size extraction
* Ending Equity extraction
* Monthly Gross extraction
* Rate of Return extraction

---

## 8.4 Excel Parsing

For Excel-based families, the model:

* Reads Excel sheets
* Locates required tabs
* Extracts latest available rows
* Converts values into standardized format

---

## 8.5 Data Standardization

The model standardizes:

* Fund codes
* UCNs
* Currency values
* Percentages
* Negative values
* Date formats

Examples:

* Removes extra spaces
* Converts text to uppercase
* Preserves leading zeros in UCN
* Converts (0.45) to -0.45

---

## 8.6 Merge Logic

The model merges extracted data with:

* Workflow files
* Helper mapping files
* Fund reference files
* UCN mapping sheets

This allows:

* Fund identification
* UCN matching
* Region assignment
* Final output standardization

---

## 8.7 Output File Creation

The model generates:

* Standardized Excel output
* Validation-ready data
* NAV extraction summary
* Exception rows if applicable

Output files are generally saved in:

* Same model directory
* Output folder
* Shared drive location

---

# 9. Expected Inputs

The following files may be required depending on the family:

| Input Type            | Purpose                    |
| --------------------- | -------------------------- |
| PDF NAV files         | Source NAV extraction      |
| Excel NAV files       | Source NAV extraction      |
| Workflow file         | Fund/UCN mapping           |
| Helper reference file | Additional mapping support |
| Client return files   | MTD extraction             |
| Outlook mailbox       | Email-based extraction     |

---

# 10. Expected Outputs

| Output           | Description                   |
| ---------------- | ----------------------------- |
| NAV Output Excel | Final extracted NAV data      |
| Validation file  | Review-ready data             |
| Exception rows   | Missing or failed extractions |
| Audit output     | Archived extraction results   |

---

# 11. Validation Process

After model execution, validation must always be performed manually.

## 11.1 Validate Fund Population

Confirm:

* Expected funds are present
* No funds are missing
* No unexpected duplicate rows exist

---

## 11.2 Validate NAV Values

Cross-check:

* NAV values
* Currency values
* Date values

against original client files.

---

## 11.3 Validate MTD Values

Confirm:

* MTD percentages are accurate
* Negative values are correct
* Latest month values were extracted

---

## 11.4 Validate UCN Mapping

Ensure:

* UCN values populated correctly
* Leading zeros preserved
* No blank mappings exist

---

## 11.5 Validate Exception Rows

Review:

* Blank NAV values
* Blank MTD values
* Failed extraction rows
* Merge failures

before upload.

---

# 12. Common Operational Issues

| Issue                  | Possible Cause                         |
| ---------------------- | -------------------------------------- |
| File not found         | Wrong directory or missing source file |
| Blank NAV values       | PDF structure changed                  |
| Missing funds          | Mapping mismatch                       |
| Duplicate rows         | Duplicate merge keys                   |
| Output not created     | Permission issue                       |
| Outlook access failure | Outlook prompt denied                  |
| Merge count low        | Fund code mismatch                     |
| Wrong MTD values       | Latest row not identified correctly    |

---

# 13. Detailed Debugging Procedure

Debugging is one of the most important parts of operating Python automations.

Whenever the model fails:

* Do not immediately rerun multiple times
* Identify the exact failure point
* Use print statements strategically
* Validate intermediate outputs
* Compare with previous successful runs

---

# 14. Print Statement Debugging Examples

## 14.1 Confirm File Loaded Properly

```python
print(df.head())
print(df.shape)
print(df.columns)
```

Purpose:

* Confirms file loaded successfully
* Confirms row count
* Confirms expected columns exist

---

## 14.2 Validate Fund Mapping Keys

```python
print(df['Fund Code'].head())
print(helper['Fund Code'].head())
```

Purpose:

* Confirms formatting matches
* Identifies spacing/case issues
* Validates merge keys

---

## 14.3 Check Common Keys Before Merge

```python
common_keys = set(df['Fund Code']) & set(helper['Fund Code'])
print(len(common_keys))
print(list(common_keys)[:10])
```

Purpose:

* Confirms merge logic working
* Identifies mapping failures
* Validates helper file consistency

---

## 14.4 Validate NAV Extraction

```python
print(nav_value)
print(mtd_value)
```

Purpose:

* Confirms extracted values
* Identifies parsing issues
* Confirms correct section of PDF read

---

## 14.5 Validate Merge Results

```python
print(df_merge.shape)
print(df_merge.head())
```

Purpose:

* Confirms merge completed
* Identifies dropped rows
* Validates final dataset

---

## 14.6 Identify Missing Funds

```python
missing = set(expected_funds) - set(output['Fund Name'])
print(missing)
```

Purpose:

* Identifies funds not extracted
* Helps isolate failed family

---

## 14.7 Debug Specific Fund Family

```python
print(file_name)
print(text[:500])
```

Purpose:

* Confirms correct file being read
* Helps identify PDF structure changes

---

# 15. Step-by-Step Recovery Procedure

## Step 1

Close all Excel files.

---

## Step 2

Restart Dev Shell.

---

## Step 3

Confirm source files are correct.

---

## Step 4

Validate helper/workflow file.

---

## Step 5

Add print statements.

---

## Step 6

Run the model again.

---

## Step 7

Review traceback carefully.

---

## Step 8

Compare with prior successful output.

---

# 16. Example Error Interpretation

## Example 1 – File Not Found

```python
FileNotFoundError
```

Meaning:

* Wrong directory
* Missing file
* Incorrect file name

Resolution:

* Validate cd path
* Confirm source file exists
* Confirm extension matches

---

## Example 2 – KeyError

```python
KeyError: 'Fund Code'
```

Meaning:

* Column missing
* Column renamed
* Extra spaces in column name

Resolution:

```python
print(df.columns)
```

Compare against expected column structure.

---

## Example 3 – Merge Returns 0 Rows

Meaning:

* Mapping mismatch
* Spacing issue
* Upper/lowercase issue

Resolution:

```python
df['Fund Code'] = df['Fund Code'].str.strip().str.upper()
```

Apply same formatting to helper file.

---

## Example 4 – Wrong NAV Extracted

Meaning:

* PDF structure changed
* Wrong section parsed
* Multiple NAV values found

Resolution:

* Print extracted text
* Compare with prior month file
* Update parsing logic

---

# 17. Important Operational Notes

* Always validate output manually before upload.
* Never trust automation output without spot checks.
* Preserve audit copies of source files.
* Avoid editing output manually unless approved.
* Always compare unusual NAV changes.
* Validate large variances carefully.
* Remove duplicate source files from folders.
* Ensure Outlook prompts are approved during execution.

---

# 18. Escalation Requirements

Escalate when:

* Entire family extraction fails
* PDF structure changes significantly
* Merge counts drop materially
* Output file not generated
* Outlook automation stops working
* UCN mapping fails repeatedly
* Large population differences identified

Provide the following during escalation:

* Screenshot of error
* Source file used
* Output file
* Dev Shell logs
* Exact traceback
* Steps already attempted
* Sample failed fund

---

# 19. Final Analyst Checklist Before Completion

Before completing the process, confirm:

* Model executed successfully
* Output file generated
* NAV values validated
* MTD values validated
* UCN mappings validated
* Missing funds reviewed
* Exception rows reviewed
* Audit copy saved
* Final output ready for downstream usage

---

# 20. Conclusion

The Day NAV Python Model is a critical operational automation used to support NAV gathering and reporting activities.

Proper execution, validation, and debugging are essential to ensure:

* Data accuracy
* Operational stability
* Audit readiness
* Timely reporting
* Reduction of operational risk

Analysts must always combine automation output with operational review and validation before final submission or upload activities.







Prompt Name: Day NAV Python Debugging Support

I am debugging the Day NAV Python model used for NAV/MTD extraction.

Issue:
[paste issue here]

Error message from Dev Shell:
[paste full error here]

Code section:
[paste relevant code here]

Files used:
- Source file:
- Helper/workflow file:
- Output file:

Please help me debug this step by step.

Provide:
1. What the error means in simple terms
2. Likely root cause
3. Whether the issue is file-related, mapping-related, Outlook-related, PDF/Excel extraction-related, or code-related
4. Exact line or section likely causing the issue
5. What print statements I should add
6. Where I should add those print statements
7. What output I should expect from each print statement
8. How to interpret the print results
9. Step-by-step fix
10. Validation checks after fixing

Important:
- Do not assume missing values
- If merge keys may be mismatched, suggest key normalization checks
- If PDF extraction may have failed, suggest text preview checks
- If Outlook extraction may have failed, suggest mailbox/category checks
- Keep the explanation simple enough for an analyst to follow
