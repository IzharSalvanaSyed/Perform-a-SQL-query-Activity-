# Perform-a-SQL-query-Activity-
In SQL, you use SELECT and FROM to retrieve information from a database. The ORDER BY keyword is used to sort the results based on a specific column. This is a crucial skill for security analysts to gather essential information for securing and protecting data.


## Table of contents

1. [Scenario](#scenario)
2. [Retrieve employee device data](#retrieve)
3. [Investigate login activity](#investigate)
4. [Explore the rm and rmdir commands](#evenmorecomands)
5. [Determine which command to use](#comandstouse)
6. [Conclusion](#conclusion)

## Scenario <a name="scenario">
In this scenario, you need to identify which employee devices require updates. Additionally, you should analyze user login activity to detect any unusual behavior. The necessary information can be found in the "machines" and "login_attempts" tables in the "organization" database.

Here's your task breakdown: First, gather information about the employee devices requiring updates. Next, analyze the login attempts for any unusual activity. Finally, use the "ORDER BY" keyword to organize the data obtained through your SQL queries.

Get ready to practice running your very first SQL queries!

### Note:  
This text is for taking notes. It is part of a pre-made lab, so follow along and understand the process.

## Retrieve employee device data <a name="retrieve">
you need to obtain information on employee devices because your team needs to update them. The information you need is in the machines table in the organization database.

First, you need to retrieve all the information about the employee devices.

- Run the following query to select all device information from the machines table:  
`SELECT *
FROM machines;`

### Note: Using the asterisk (*) returns all data from the specified table. Also, table names in MySQL are case-sensitive.

The output returns all the contents of the machines table:

    +--------------+------------------+----------------+---------------+-------------+
    | device_id    | operating_system | email_client   | OS_patch_date | employee_id |
    +--------------+------------------+----------------+---------------+-------------+
    | a184b775c707 | OS 1             | Email Client 1 | 2021-09-01    |        1156 |
    | a192b174c940 | OS 2             | Email Client 1 | 2021-06-01    |        1052 |
    | a305b818c708 | OS 3             | Email Client 2 | 2021-06-01    |        1182 |
    | a317b635c465 | OS 1             | Email Client 2 | 2021-03-01    |        1130 |
    | a320b137c219 | OS 2             | Email Client 2 | 2021-03-01    |        1000 |
    |...           |                  |                |               |             |
    +--------------+------------------+----------------+---------------+-------------+
    200 rows in set (0.356 sec)

Next, you want to focus on the email client running on various devices.

- Run the following query to select only the device_id and email_client columns from the machines table.  
`SELECT device_id, email_client FROM machines;`

What email client is returned in the third row?  

    +--------------+----------------+
    | device_id    | email_client   |
    +--------------+----------------+
    | a184b775c707 | Email Client 1 |
    | a192b174c940 | Email Client 1 |
    | a305b818c708 | Email Client 2 |
    | a317b635c465 | Email Client 2 |
    | a320b137c219 | Email Client 2 |
    | a398b471c573 | Email Client 2 |
    | a667b270c984 | Email Client 1 |
    | a821b452c176 | Email Client 2 |
    | a998b568c863 | Email Client 1 |
    | b157c491d493 | Email Client 1 |
    | b239c825d303 | Email Client 1 |
    | b264c773d977 | Email Client 2 |

- Email Client 2

Now, you need information on the operating systems used on various devices and their last patch date.

- Complete the query to return only the device_id, operating_system, and OS_patch_date columns from the machines table.  
`SELECT device_id, operating_system, OS_patch_date FROM machines;`

What is the patch date of the first entry?

    +--------------+------------------+---------------+
    | device_id    | operating_system | OS_patch_date |
    +--------------+------------------+---------------+
    | a184b775c707 | OS 1             | 2021-09-01    |
    | a192b174c940 | OS 2             | 2021-06-01    |
    | a305b818c708 | OS 3             | 2021-06-01    |
    | a317b635c465 | OS 1             | 2021-03-01    |
    | a320b137c219 | OS 2             | 2021-03-01    |
    | a398b471c573 | OS 3             | 2021-12-01    |
    | a667b270c984 | OS 1             | 2021-03-01    |
    | a821b452c176 | OS 2             | 2021-12-01    |
    | a998b568c863 | OS 3             | 2021-12-01    |
    | b157c491d493 | OS 2             | 2021-03-01    |
    | b239c825d303 | OS 1             | 2021-03-01    |
    | b264c773d977 | OS 2             | 2021-03-01    |
    | b265c937d713 | OS 2             | 2021-09-01    |

- 2021-09-01

## Investigate login activity <a name="investigate">
You need to analyze the information from the log_in_attempts table to determine if any unusual activity has occurred.

First, you need to investigate the locations where login attempts were made to ensure that they’re in expected areas (the United States, Canada, or Mexico).

- Write a SQL query to select the event_id and country columns from the log_in_attempts table.  
`SELECT event_id, country FROM log_in_attempts;`

Were any login attempts made from Australia?

    +----------+---------+
    | event_id | country |
    +----------+---------+
    |        1 | CAN     |
    |        2 | CAN     |
    |        3 | USA     |
    |        4 | USA     |
    |        5 | CANADA  |
    |        6 | MEXICO  |
    |        7 | CAN     |
    |        8 | US      |
    |        9 | MEX     |
    |       10 | CANADA  |
    |       11 | CANADA  |
    |       12 | USA     |
    |       13 | USA     |
    |       14 | US      |
    |       15 | USA     |
    |       16 | CAN     |
    |       17 | USA     |
    |       18 | US      |
    |       19 | US      |
    |       20 | MEXICO  |  

Next, you need to check if login attempts were made outside of the organization's working hours.

- Write a SQL query that selects the username, login_date, and login_time columns from the log_in_attempts table.
