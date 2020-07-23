---
title: SQL Style Guide
subtitle: ""
#These are "clean" theme items.
#layout: page
#callouts: home_callouts
#show_sidebar: true
layout: default
---

# SQL: Style Guide
{: .no_toc }

## Guide sections
{: .no_toc .text-delta }

- TOC
{:toc}

## Overview

These guidelines are designed to promote consistent and readable SQL code.  Clear formatting helps code to be more easily interchangeable and understandable among various colleagues.  "Legibility is one of the ultimate goals of working from a shared codebase, and... individuals who work with a team-oriented mindset produce cleaner, more readable code." [^1]

[^1]: Zenon, A.  (2020).  How to make clean code a priority.  BuiltinATX.  https://www.builtinaustin.com/2020/07/20/prioritizing-clean-code. {: .fs-2 }

## General

* Use whitespace and indentation.
* Avoid camelCase text.
* Make judicious use of white space and indentation to make code easier to read.
* Try to only use standard SQL functions instead of vendor-specific functions for
  reasons of portability.
* Keep code succinct and devoid of redundant SQL—such as unnecessary quoting or
  parentheses or `WHERE` clauses that can otherwise be derived.
* Include comments in SQL code where necessary. Use the C style opening `/*` and
  closing `*/` where possible otherwise precede comments with `--` and finish
  them with a new line.

```sql
SELECT spriden_pidm  -- student identifier
  FROM spriden
 WHERE spriden_change_ind IS NULL;
```
```sql
/* Retrieving the most current student record */
SELECT spriden_pidm
  FROM spriden
 WHERE spriden_change_ind IS NULL;
```

## Query syntax

* Always use uppercase for reserved keywords (e.g. `SELECT`, `FROM`, `WHERE`)
* Always use uppercase for built-in operators (e.g. `SUM`, `COALESCE`, `UPPER`)
* Do not use vendor-specific keywords when a standard SQL keyword exists
* Avoid using the star select (`*`) notation; specify the field names needed
* When using a `CASE` statement, place each `WHEN` and `END` on a new line
* Place aggregate functions at the end of the `SELECT` statement
* Use “river” indentation
* Align code so that keywords end on the same character boundary
* Keywords are right-aligned while other information is left-aligned
* Subqueries should be aligned on the right side of the “river” and follow the same syntactical principles as a standard query

```sql
    SELECT a.spriden_pidm,
           a.spriden_id AS university_id,
           b.sfrstcr_grde_code,
           SUM(b.sfrstcr_credit_hr) AS hours_by_grade
      FROM spriden a
 LEFT JOIN sfrstcr b
        /* Note that the ON keyword aligns to the left of the river. 
           (The DataGrip code template will not do this automatically.) */ 
        ON a.spriden_pidm = b.sfrstcr_pidm
       AND b.sfrstcr_rsts_code IN
             (SELECT b1.stvrsts_code
                FROM stvrsts b1
               WHERE b1.stvrsts_incl_sect_enrl = 'Y')
```       

## Naming conventions

* Make identifiers and names consistent and appropriately descriptive
* Names should be 30 characters or less and must start with a letter
* Names should include only lowercase letters, numbers, and underscores
* Use an underscore where you would otherwise use a space: column_name
* Avoid abbreviations when possible
* Avoid plural names and reserved keywords
* When creating an indicator or binary field, use the suffix `_ind`

## Aliasing

* Always alias tables
* Use an alias in all places that you refer to a field name
* Include the AS keyword when aliasing columns
* Use sequential alphabetical notation (`sgbstdn a LEFT JOIN stvterm b`)
* For subqueries, use the reference of the outer query but append sequential number (`a1`)

## Joining tables
* Explicitly state join type: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`
* There is no need to specify `OUTER` when indicating joins: `LEFT OUTER JOIN`
* Strive to use left joins rather than right joins

## Preferences

* Include a space before and after an equal sign
* Include a space after a comma
* Place commas immediately following the element name
* Use the `BETWEEN` keyword instead of combining multiple statements using `AND`
* Use `IN` instead of using multiple OR clauses
* Use `CASE` rather than `DECODE`
* Use `!=` rather than `<>` to test for inequality


## Attributions
{: .fs-2 }

These guidelines are based on the SQL style guide by [Simon Holywell][simon], which is licensed under a [Creative Commons Attribution - ShareAlike 4.0 International License][licence].  Based on a work at [https://www.sqlstyle.guide/][sqlstyleguide].  
{: .fs-2 }

As noted by Holywell, "These guidelines are designed to be compatible with Joe Celko's [SQL Programming Style][celko]; this guide is a little more opinionated in some areas and in others a little more relaxed. It is certainly more succinct where [Celko's book][celko] contains anecdotes and reasoning behind each rule as thoughtful prose."
{: .fs-2 }


[simon]: https://www.simonholywell.com/?utm_source=sqlstyle.guide&utm_medium=link&utm_campaign=md-document
    "SimonHolywell.com"
[celko]: https://www.amazon.com/gp/product/0120887975/ref=as_li_ss_tl?ie=UTF8&linkCode=ll1&tag=treffynnon-20&linkId=9c88eac8cd420e979675c815771313d5
    "Joe Celko's SQL Programming Style (The Morgan Kaufmann Series in Data Management Systems)"
[sqlstyleguide]: https://www.sqlstyle.guide/
    "SQL style guide by Simon Holywell"
[licence]: https://creativecommons.org/licenses/by-sa/4.0/
    "Creative Commons Attribution-ShareAlike 4.0 International License"