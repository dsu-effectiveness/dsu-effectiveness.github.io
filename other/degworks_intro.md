---
title: DegreeWorks Data Overview
subtitle: ""
#These are "clean" theme items.
#layout: page
#callouts: home_callouts
#show_sidebar: true
layout: default
---

# DegreeWorks Data

DegreeWorks is a degree audit tool created by Ellucian.  A degree audit verifies that a student has completed the requirements of their degree program.  An individual audit is comprised of a number of requirement blocks that are taken together and compared to the student's transcript.  DegreeWorks has four main components: (1) Scribe, where requirement blocks are created; (2) Parser Engine, which translates Scribe blocks into a format that can be used for auditing; (3) Auditor Engine, which evaluates student course data against requirement blocks; and (4) Output Engine, which reads audit results and generates an output document.

For analysis of degree requirements, we are concerned primairly with Scribe and the Parser Engine.  For analysis of individual student course-taking, we would also be concered with the Auditor Engine and/or Output Engine.

## Types of tables

There are four primary types of tables in DegreeWorks.  The majority of the necessary data related to actual degree requirements are located in the DAP tables.  The SEP tables are populated by individual students as they or their advisor complete degree plans.  DegreeWorks pulls data from Banner; the reformatted Banner data are stored in the RAD tables.

- DAP: Degree audit process
- RAD: Data repository
- SHP: Security and roles
- SEP: Student educational planner

## Degree audit process (DAP) tables

### Requirement blocks (dap_req_block)

Individual requirement blocks are stored in `dap_req_block`.  Key fields are as follows:

Field            | Data type     | Description                    
---------------- | ------------- | ------------------------------------------------------------
requirement_id   | VARCHAR2 (8)  | Requirement block ID
block_type       | VARCHAR2 (12) | Type of block (DEGREE, MAJOR, MINOR, CONC, or other)
block_value      | VARCHAR2 (12) | Key value of the block based on block type
title            | VARCHAR2 (50) | Title of the requirement block (appears on audit sheets)
period_start     | VARCHAR2 (12) | Starting catalog year
period_end       | VARCHAR2 (12) | Ending catalog year
requirement_text | CLOB          | The text of the requirement block (appears on audit sheets)
modify_date      | DATE          | The date the block was last modified

Note that the requirement text itself (in the `requirement_text` field) is stored as a character large-object (CLOB) data type.  If you copy and paste the contents of the requirement_text column into a code editor or word processor, you can view the complete text statement.

### Requirement block course details (dap_req_crs_dtl)

When a requirement block is processed, courses found in the block are stored in `dap_req_crs_dtl`.  Key fields are as follows:

Field            | Data type     | Description                    
---------------- | ------------- | ------------------------------------------------------------
dap_req_id       | VARCHAR2 (8)  | Foreign key; ties to dap_req_block.requirement_id
dap_discipline   | CHAR (12)     | Course subject
dap_number_begin | CHAR (12)     | Course number (or starting number if range of courses)
dap_number_end   | CHAR (12)     | If requirement is a range, ending course number

Note that the course subject and course number fields may also contain the wildcard character, `@`.


### dap_req_link_dtl (links one course block to another)

Relationships can be defined between different requirement blocks, either hierarchically or via an explicit linkage.  A linked block is useful when requirements need repeated in multiple blocks.  `dap_req_link_detail` stores the link from one requirement block to another.  The Auditor Engine uses this table to determine which OTHER blocks to include in a student's degree audit.

Field            | Data type     | Description                    
---------------- | ------------- | ------------------------------------------------------------
dap_req_id       | VARCHAR2 (8)  | Foreign key; ties to dap_req_block.requirement_id
dap_type_from    | CHAR (12)     | Foreign key; ties to dap_req_block.block_type
dap_value_from   | CHAR (12)     | Foreign key; ties to dap_req_block.block_value
dap_type_to      | CHAR (12)     | Block type of the referenced block (always OTHER)
dap_value_to     | CHAR (12)     | Value of referenced block (dap_req_block.block_value)
