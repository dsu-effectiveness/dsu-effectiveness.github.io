---
title: Banner Mnemonics
subtitle: ""
#These are "clean" theme items.
#layout: page
#callouts: home_callouts
#show_sidebar: true
layout: default
---

# Banner Mnemonics

Banner forms and tables follow a seven-character naming convention (mnemonic).  These mnemonics employ the following structure.

## Position 1
- ***Primary system*** owning the form/table.

P1 | System                    | P1 | System                    
-- | ------------------------- | -- | ------------------------- 
A  | Alumni/development        | O  | Customer contact
B  | Property tax              | P  | Payroll/personnel (HR)
C  | Courts                    | Q  | Electronic work queue
D  | Cash drawer               | R  | Financial aid
F  | Finance                   | S  | Student
G  | General                   | T  | Accounts receivable
I  | Information access        | U  | Utilities
K  | Work management           | V  | Voice response
L  | Occupational license      | X  | Records indexing
N  | Position control
  
## Position 2
- ***Module*** owning the form/table.
- This code is dependent upon the primary system code in position 1.
  
P2 | Students (S)              | P2 | Finance (F)               | P2 | General (G)               
-- | ------------------------- | -- | ------------------------- | -- | ------------------------- 
A  | Admissions                | A  | Accounts payable          | E  | Event management          
C  | Catalog                   | B  | Budget development        | J  | Job submission            
E  | Support services          | C  | Cost accounting           | L  | Letter generation   
F  | Registration/fee assess.  | E  | Electronic data interchg. | O  | Overall                   
G  | General student           | F  | Fixed assets              | P  | Purge                     
H  | Grade/academic history    | G  | General ledger            | S  | Security                  
I  | Faculty load              | I  | Investment management     | T  | Validation form/table   
L  | Location management       | O  | Operations                | U  | Utility           
O  | Overall                   | P  | Purchasing                | X  | Cross-product   
P  | Person                    | R  | Research accounting
R  | Recruiting                | S  | Stores inventory
S  | Schedule                  | T  | Validation form/table
T  | Validation form/table     | U  | Utility
U  | Utility
      

P2 | Financial aid (R)         | P2 | Human resources (P / N)   | P2 | Accounts receivable (T)               
-- | ------------------------- | -- | ------------------------- | -- | ------------------------- 
B  | Budgeting                 | A  | Application               | F  | Finance accounts rec.
C  | Record creation           | B  | Budget                    | G  | General accounts rec.
E  | Electronic data exch.     | C  | COBRA                     | O  | Overall
F  | Funds management          | D  | Benefits/deductions       | S  | Students accounts rec.
H  | History                   | E  | Employee                  | T  | Validation form/table
J  | Student employment        | H  | History                   | U  | Utility
L  | Logging                   | O  | Overall                   |    |
N  | Need analysis             | P  | General person            |    | 
O  | Common functions          | R  | Electronic approvals      |    | 
P  | Packaging/disbursement    | S  | Security                  |    | 
R  | Requirements tracking     | T  | Validation/rule table     |    | 
S  | Student sys. shared data  | U  | Utility                   |    |
T  | Validation form/table     | X  | Tax administration        |    |
U  | Utility                   |    |                           |    |
  
## Position 3
- Specifies the ***type*** of form/table.
- Generally speaking, a Banner front-end form and back-end data table are related by similar naming, with a different P3 character.
- In limited instances, the third character "V" also represents a view.

P3 | Type                      | P3 | Type
-- | ------------------------- | -- | ------------------------- 
A  | Application form          | Q  | Query form
B  | Base table/batch process  | R  | Rule or repeating table
I  | Inquiry form              | T  | General maintenance
O  | Online COBOL process      | V  | Validation form/table

## Position 4
- The remaining positions identify a unique four-character name for the form, report, process, or table.

## Example
- Table: SCBCRSE
- ***S*** [Student]
- ***C*** [Catalog]
- ***B*** [Base table]
- ***CRSE*** [Course information]
  

      