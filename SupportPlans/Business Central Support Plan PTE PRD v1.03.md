November 2, 2025

# AGENT PROMPT

You are an expert Dynamics 365 Business Central AL developer.  You have extensive experience in the design, architecture, coding, testing, and debugging Business Central projects written in the AL language.

You will help develop a Business Central Per Tenant Extension (PTE).  The "docs" folder of this project contains a Markdown file, which is the PRD for the PTE.  The docs folder also contains associated image files that are wireframe diagrams for the PTE pages.

Please help develop the PTE.

Please use the latest development standards for the Business Central AL programming language.  Make sure not to use old, deprecated, or obsolete keywords, properties, procedures, or codeunits.

After generating the application code, please review all of the code for any syntax errors or compiler errors, and correct the errors.


# Overview

Our organization, ERP Support Team, offers annual support plans to Dynamics 365 Business Central partners and customers.

We would like a Per Tenant Extension (PTE) in Dynamics 365 Business Central that allows us to record, track, and manage these support plans.

The PTE will be developed in the native Business Central AL programming language.

Before starting any work, output the current Date and Time as the "Start Time".  When your work is complete, output the current Date and Time as the "End Time".


# Project Name

Support Plans

## Version

Support Plans Version 1.0.3.0

## Business Value

- Record and track customer support contracts in Business Central 
- Store customer support contacts to facilitate support requests and service approvals
- Quickly and easily verify contract status and view expiration date
- Quickly identify contracts that are ending soon or have expired
- Record support related information, such as Business Central Tenant ID


# AL Project Configuration

## app.json Values

The application will have the following values in the app.json file:

- Name: Support Plans
- Publisher: ERP Support Team
- Version: <same value as application version number listed above>
- Brief: Support Plans Management
- Description: Manage and track customer support plans in Business Central
- Platform: 26.0.0.0
- Application: 26.0.0.0
- Runtime: 15.0
- Object Range: 60100 to 60199
- Privacy Statement: <https://bluedragonflyllc.com/privacy-policy>
- EULA: <https://bluedragonflyllc.com/terms-and-conditions>
- Help: <https://bluedragonflyllc.com/support>
- URL: <https://bluedragonflyllc.com>
- Context Sensitive Help: <https://bluedragonflyllc.com/support>
- Resource Exposure Policy: Allow Debugging = True, Allow Downloading Source = True, Include Source in Symbol File = True
- Features: NoImplicitWith
- Do not include the deprecated “showMyCode” property in the app.json file

## launch.json Values

Modify this value in the launch.json file:

Startup Object ID: (object ID for the Support Plan List Page)

Verify that the following values are configured in the launch.json file:

- Configuration Name:  Microsoft cloud sandbox
- Environment Type: Sandbox
- Environment Name: Sandbox

Do not modify any other values in the launch.json file


## AL Object Naming Convention

The following components will be assembled to form the AL object name.

If the AL object name exceeds 20 characters for a Permission Set, or exceeds 30 characters for all other object types, please display the proposed object name and ask for feedback on a shorter name that will meet the max AL object name length requirement.

1. Prefix: SP - All objects will start with "SP", which stands for Support Plan

2. Name: Name the object based on it's purpose or function, with no spaces and initial capitals for each word. 

For example:

- Plans Setup
- Plans List
- Plan Card
- Plan Notes
- Plan Level
- Plan Status

3. Object Abbreviation:  A single letter to represent the AL object type

Values:

- C = Codeunit
- P = Page
- Q = Query
- R = Report
- T = Table
- PE = Page Extension
- TE = Table Extension
- RE = Report Extension
- PS = Permission Set

4. Object Suffix:  A constant three letter suffix that represents the application publisher to ensure unique object names in BC.

- Suffix value:  EST

EST is an abbreviation for "ERP Support Team"

### Object Name Examples

- Support Plans List Page:  Object Name: "SP Support Plans P EST", Caption: "Support Plans"
- Support Plan Card Page:  Object Name: "SP Support Plan P EST", Caption: "Support Plan"
- Support Plans Table:  Object Name: "SP Support Plans T EST", Caption: "Support Plans"
- Support Plan Level Enum:  Object Name: "SP Support Plan Level E EST", Caption: "Support Plan Level"


## File Naming Convention

File names will be based on the AL object name with spaces removed.  A suffix will then be added to the end of the file name.

Suffix values:

- Codeunit
- Enum
- Page
- PageExt
- PermissionSet
- Table
- TableExt

All AL code files will have a ".al" file extension.

### File Name Examples

Here are example file names based on the rules listed above.

- Support Plans List Page:  File Name: SPSupportPlansPEST.Page.al
- Support Plan Card Page:  File Name: SPSupportPlanPEST.Page.al
- Support Plans Table:  File Name: SPSupportPlansTEST.Table.al
- Support Plan Level Enum:  File Name: SPSupportPlanLevelEEST.Enum.al


**Application Requirements**

The PTE must meet the following requirements and specifications, and allow a user to perform the following processes in Dynamics 365 Business Central.

# Support Plan Number Series

A new number series called “SP” should be created automatically by the Support Plan Setup page in the standard Business Central No. Series page.

The Number Series will start with SP10001. There will be no end number and no dates associated with the new No. Series.


# Support Plans Setup Page

A Setup page will be used to specify configuration options for the Support Plan application.

The setup page will have the following field:

1. Support Plans No. Series

The SP number series will be created by the setup page, and this field will be populated with the SP number series.

The Support Plans No. Series will provide the default record number when a new Support Plan is created.

## Support Plans Setup Table

The field values on the Support Plans Setup Page will be stored in the Support Plans Setup Table.

This should be a standard Business Central AL "Setup Table" with a single record, using the standard BC Setup Table design pattern.


# Support Plan List Page

This is a Business Central "List Page" that displays all Support Plans records.

1. Plan No. (the next number from the SP No. Series will be automatically assigned)
2. Customer No. (a lookup field allowing the selection of an existing BC Customer No. value)
3. Customer Name (automatically populated with the Name value of the selected Customer)
4. Start Date (a Date picker field)
5. End Date (a Date picker field)
6. Level (a drop down / combo box field allowing the user to select a support plan Level)
7. Status (a calculated field displaying contract status, such as Active, Ending in \< 30 days, Expired)

The Plan No. field will be a link to open the Support Plan card page and display the selected Support Plan record.


# Support Plan Card Page

This is a Business Central "card page" that allows a user to enter a new support plan for an existing Business Central customer.

When a user clicks on a Support Plan No. value on a row on the Support Plan List Page, the Support Plan card page will open and display the existing support plan record.

When a new Support Plan is created, automatically populate the Contract No. field with the next number from the SP No. Series (e.g. SP10001), and save the new Support Plan record.

Support Plan records will be stored in a custom table.

## Support Plans Table

The Support Plan card page will display the following "header record" fields from the Support Plans table.  These fields will be read-only and will not be editable.

1.  Support Plan No.
2.  Customer No.
3.  Customer Name
4.  Created By (user name)
5.  Created Date

## Plan Details Fast Tab

The Plan Details fast tab will display user editable fields from the support plan record in the Support Plans table.

The user will be able to enter or edit the following field values:

- Start Date: Default to current calendar date
- End Date: Default to current calendar date, plus one year, minus one day (e.g. if start date is 4/1/2025, end date would be 3/31/2026)
- Level (Drop down with Enum values of Basic or Premium)

The following field will be a calculated by comparing the End Date to the current date.  The field will be read only and will not be editable.

- Status: Values of Active, Ending, or Expired

**Status Field Value and Calculation**

The Status field will display a calculated value based on the plan End Date.

- Display “Active” in Green text if End Date is more than 30 days from the current date
- Display “Ending” in Yellow text if End Date is 1 to 30 days from the current date
- Display “Expired” in Red text if End Date is the current date or prior to the current date

## Notes List Part

- The "Notes" list part allows a user to view multiple notes tied to the support plan (shown as a List Part on the Support Plan Card Page)
- The user can add a new Note in this section
- Support Plan Notes are saved in a separate custom table
- Support Plan Note records will be associated with the Support Plan No. value in the 
- Notes will be sorted by date descending, with the newest note on top 

The Note List Part will display the following fields:

1. Date:  Read only datetime when the note record was created / inserted
2. User:  Read only text field with the BC username who created the note
3. Note:  500 character text field to store note text

### Note Table

1. Support Plan No: Link to the support plan record
2. Date:  datetime when the note record was created / inserted
3. User:  text field with the BC username who created the note
4. Note:  500 character text field to store note text



