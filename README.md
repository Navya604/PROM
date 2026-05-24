SOP: Daily NAV Workflow Refresh – 9:00 AM Process

Process Area: NAV Workflow Refresh
Frequency: Daily
Region Coverage: NAHF and LATAM HF
Primary Tools: Shared Drive, R412 HF Metrics Report, Excel Workflow File, Alteryx Server

1. Purpose

The purpose of this SOP is to refresh the daily NAV workflow using the prior day’s workflow file and the latest R412 HF Metrics Report. The refreshed workflow is used to identify current NAV statuses, validate fund population, update regional gaps, and highlight any red items requiring immediate review or escalation.

2. Required Inputs

Before starting the process, ensure the below inputs are available:

Prior day’s NAV workflow file
Latest R412 – HF Metrics Report Master DE
Access to shared drive NAV workflow folder
Access to Alteryx server
Access to ICRD / CRD folder if regional checks are required
Excel access to update and validate workflow tabs
3. Output Files

At the end of the process, the following outputs should be available:

Refreshed workflow output from Alteryx
Refreshed website output from Alteryx
Updated daily NAV workflow file
Validated regional mapping
Red items identified and assigned for action
4. Step-by-Step Procedure
Step 1: Locate Prior Day Workflow File

Go to the shared drive location where the NAV workflow files are stored.

Identify the most recent prior day workflow file.

Make a copy of the prior day file and rename it with today’s date.

Example:

NAV Workflow_05.20.2026.xlsx

This copied file will become today’s working file.

Step 2: Prepare Today’s Workflow File

Open today’s copied workflow file.

Go to the workflow tab and website tab.

Before deleting any data, make sure all filters are removed.

Then delete the prior day’s data from both tabs, but keep the headers.

Important:

Do not delete column headers
Only delete existing data rows
Make sure the workbook structure remains unchanged
Step 3: Download / Save R412 HF Metrics Report

Go to the ICRD / CRD folder or required source location for the R412 report.

Download or save the latest R412 – HF Metrics Report Master DE.

Save the R412 file in the shared drive location with today’s date.

This file will be used as one of the required inputs in Alteryx.

Step 4: Open Alteryx Server

Open browser and go to the Alteryx production server.

Navigate to:

Collections > CRM / NAV Team Workflow Refresh

Search for:

NAHF NAV Team Work Refresh V3

Open the workflow.

Step 5: Run the Alteryx Workflow

Click Run.

If prompted, click Run again.

The workflow will ask for three input files.

Select the required files:

R412 – HF Metrics Report Master DE
Prior day workflow file – Workflow tab
Prior day workflow file – Website tab

After selecting all three files, click OK, then click Run.

Step 6: Download Alteryx Outputs

After the workflow completes successfully, download both output files.

The workflow should produce two separate outputs:

Workflow output
Website output

Save both files in the required shared drive location.

Step 7: Update Today’s Workflow File

Open today’s copied workflow file.

Unshare the workbook before pasting Alteryx output.

Go to:

Review > Share Workbook

Uncheck:

Use the old shared workbooks feature instead of the new co-authoring experience

Then click OK.

After unsharing, paste the Alteryx workflow output into the workflow tab.

Paste the Alteryx website output into the website tab.

Make sure the data is pasted under the correct headers.

Step 8: Validate Fund Count Against R412

Check the total number of funds in the refreshed workflow.

Compare the count with the R412 HF Metrics Report.

If the count does not match:

Review whether the correct R412 file was selected
Confirm the workflow and website tabs were selected correctly
Check whether any filters were left on before data deletion
Re-run Alteryx if needed
Step 9: Validate Region Column

In the workflow tab, filter the Region column.

Check for blanks.

If Region is blank:

Copy the UCN
Go to ICRD / CRD
Search the fund
Confirm the correct region
Update the Region column manually if applicable

Focus mainly on NAHF and LATAM HF populations.

Step 10: Filter Current Date Metrics

Go to the X column / Metrics column.

Filter for today’s date.

Review the current day’s items.

Identify any funds marked as Red or requiring investigation.

Step 11: Review Red Items

For any funds appearing as Red:

Review the fund name
Check how the NAV information is sourced
Determine whether data is missing or delayed
Assign the item to yourself or appropriate team member for investigation
If no data is available, reach out to Credit as needed

Add clear comments in the analysis/comment column for immediate action.

Step 12: Final Review and Share File

Before finalizing:

Confirm workflow tab is updated
Confirm website tab is updated
Confirm fund count agrees with R412
Confirm Region blanks are resolved
Confirm Red items are reviewed and assigned
Confirm comments are clear and professional

After review, share the workbook again if required.

Save the final file.

5. Validation Checks

Perform the following checks before marking the workflow as complete:

Correct date is included in file name
Prior day data was removed before new output was pasted
Correct R412 file was used
Alteryx workflow completed successfully
Both workflow and website outputs were downloaded
Workflow and website tabs were pasted correctly
Fund count agrees with R412
Region column does not have unexplained blanks
Red items are reviewed and assigned
Final workbook is saved in the correct shared drive location
6. Common Issues and Resolution
Issue 1: Alteryx output is blank

Possible cause:

Wrong input file selected
Wrong tab selected
Prior day file structure changed

Resolution:

Recheck selected files
Confirm workflow and website tabs exist
Re-run the Alteryx workflow
Issue 2: Fund count does not match R412

Possible cause:

Incorrect R412 file
Old workflow file selected
Filters were not removed before deletion

Resolution:

Confirm R412 date
Confirm prior day workflow file
Recheck deleted data
Re-run Alteryx if needed
Issue 3: Region column has blanks

Possible cause:

Newly onboarded fund
Region not mapped in source data
Missing UCN mapping

Resolution:

Search UCN in ICRD / CRD
Confirm region manually
Update Region column if applicable
Issue 4: Workbook cannot be updated

Possible cause:

Workbook is still shared
Another user has file open
Excel lock issue

Resolution:

Unshare workbook
Ask users to close the file
Save a new copy if needed
Issue 5: Red items appear in workflow

Possible cause:

Missing NAV
Data not available
Family/source issue

Resolution:

Investigate source of NAV
Check how information is received for that family
Assign to team member
Reach out to Credit if no data is available
7. Control Notes
Do not overwrite headers in workflow or website tabs.
Always validate fund count against R412 before finalizing.
Region blanks should be reviewed before publishing the file.
Red items should not be ignored; they must be assigned or investigated.
Any manual updates should be documented clearly.
If unsure, escalate to SME before finalizing.
8. LLM Prompt for Help / Troubleshooting

Use this prompt if the user needs help understanding an error or issue during the process:

I am running the daily NAV workflow refresh process.

Issue:
[paste issue here]

Files used:
- Prior day workflow:
- R412 report:
- Alteryx workflow:
- Output file:

Please help me identify:
1. Possible root cause
2. What checks I should perform
3. Step-by-step resolution
4. Whether this needs SME escalation

Do not assume missing values. If information is not available, say manual validation is required.
9. Final Completion Criteria

The process is complete only when:

Alteryx workflow has run successfully
Workflow and website outputs are pasted into today’s file
Fund count is validated against R412
Region blanks are resolved or documented
Red items are reviewed and assigned
File is saved in the shared drive with today’s date
Any exceptions are documented clearly
