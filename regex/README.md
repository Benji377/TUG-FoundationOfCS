# Regex (25 points)

In this assignment you will learn how to use regular expressions for a Python program.
Your regular expressions will be encoded as strings in a .json file.
A provided testsuite loads this file which tests your expressions against the basic examples for each of the five subtasks.
You only have to submit the .json file with your own regex.
## Submission Mode
* Make sure to test your regex (e.g. with our provided testsuite)
* Submit your solution as `regex.json` here in the submission space.
* Make sure your regex passes the example tests provided by the testsuite

## Assignment Description

Checking the format of a given input is one use case of regular expressions. In this assignment, you will use basic syntactic elements from regex to check if an input matches a given format. Additionally, you will save the regex encoded as a string inside of a .json file for structured use in a testsuite. (Take a look at the notes below for info about escaping backslashes) This **.json file** is also your **submission file**.

## [Task 1] Mobile phone numbers 
In this task you have to write a regex to check if the provided phone number (area code `43`) is a typical landline number from Graz (316), Vienna (1), Salzburg (662) or Innsbruck (512).
Implement the different possibilities to **begin** a number:
- `+43316`...
- `0043316`...
- `0316`...
  (... Here the area code example is Graz: 316)

The actual phone number (after the country and area code) **consists of at least one digit** and can be infinitely long.

**Possible mobile dialing codes:**
* `316`
* `1`
* `662`
* `512`


| fullmatch        | no match / not a fullmatch |
|------------------|-----------------------------|
| `+43141234`        | `+432234`                     |
| `05121519245`    | `043111213`                   |
| `00433161`         | `043316456`                   |

**Examples for phone numbers**


### [Task 2] UWU 
Create a short regular expression which only matches words that don't have the same characters following after another.
The regular expression must **NOT** contain any whitespaces! (clarification: this applies only to this subtask 3.2)
Alphabet: {U, W}, the empty string Ɛ is a match as well.

| fullmatch | no match / not a fullmatch |
|-----------|-----------------------------|
| `Ɛ`         | `UU`                      |
| `WUWU`      | `UWUU`                    |
| `UWUWU`     | `UWWWUWU`                 |
| `W`         | `WUWWUW`                  |
**Examples UWU**

### [Task 3] Email addresses 
In this exercise, you should create a regex which matches E-Mail Addresses. An Email-Address consists of a local- (before `@`) and a domain-part (after `@`).

For the local part, this rule set should apply:
- The local part must only consist of capital and lowercase letters and points.
- At the beginning and the end of the local part, a point is prohibited.
- There must not be two consecutive points.

For the domain part apply the following rules:
- The host name of the Email addresses should be "tugraz".
- The possible national codes for the Email addresses are "edu", "info" and "at".
- The hostname and the country code are separated by exactly one dot.

| fullmatch                       | no match / not a fullmatch    |
|---------------------------------|-------------------------------|
| `m.mustermann@tugraz.info`        | `dotatend.@tugraz.edu`         |
| `must.ter.frau@tugraz.edu`        | `.dotatbeginning@tugraz.at`    |
| `m@tugraz.at`                     | `two..dots@tugraz.info`       |
**Examples email addresses**

### [Task 4] Dates and time
We now want to create a regex for matching Dates and an optional time.

* The date consists of 3 decimal values separated by one period.
* Format of the date is (day.month.year). Filling leading zeros are optional here.
* Value ranges: Day [1-31], Month[1 - 12], Year [0 - 9999]

* **Optional** (!) a time can be attached to the Date.
* The separation between date and time is exactly " - " (with spaces).
* The format for time is (hour:minute). Filling leading Zeroes are mandatory here.
* Value ranges: Hour [00-23], Minute [00-59]

It is not feasible for regex to refuse formally correct but impossible dates like `31.02.2020`. You do **not** have to take those kinds of edge cases into account.

| fullmatch                | no match / not a fullmatch  |
|--------------------------|-----------------------------|
| `09.12.2010`             | `009.12.2010`               |
| `09.12.2010 - 12:30`     | `4.13.842 - 1:1`            |
| `1.1.1990 - 01:01`       | `31.02.2020 - 3:30`         |
| `1.1.0 - 00:00`          | `001.001.00000 - 000:000`   |
**Examples date and time**

**Note** Whitespaces are allowed here.

### Allowed regex syntax elements 
Below the Syntax allowed in this assignment is listed.
`.` `+` `*` `?` `|` `(` `)` `[0-9]` `[a-z]` `\` `{2}` `[A-Za-z]`

**Not allowed syntax (examples: `^`, `$`) => at least (!) -50% on your points.**
In general, everything that is not listed in the allowed elements, is not allowed.
For further notes and tips read the section "**Important Notes and Tips**" at the end of this Readme.

**FAQ:**
- "is `{3}` also allowed? " - Yes, as well as all other positive whole numbers.
- "is `[2-4]` or `[B-Fk-n]` allowed? " - Yes, as well as any other combination of digits or letters
- "is `{1,4}` allowed? " - No, it is not. Use simple quantifiers like `+`, `*` or single limits like `{4}` or `{3}`

### Important Notes and Tips
* Make yourself familiar with the concept of **escaping** in regex. Example: A colon (`.`) matches "any character" in regex. To match only the literal colon-character, you have to escape it with a backslash (`\.`)
* Encoding a regex inside of a **string** also may need **escaping**. The backslash is an escaping character for strings too. To use a regex like in the example above (`\.`) inside of a string, you have to escape the backslash from the regex again. This results in (`\\.`)
* It is recommended to use **Area-Matches** (e.g. `[0-9]`) **instead of** `0123456789` for all digits. You can combine multiple Areas (e.g. `[A-Za-z]` to match lower- and uppercase letters)
* It is not sufficient, if your regex classifies only the given examples. Your solution has to **exactly fulfill** the general assignment description
* Points can only be recieved with a serious attempt. Obviously a regex like (`.?`) would (correctly) **not** match any of the examples, that should also **not** be matched by the correct and complete regex for the according task. But with a submission like (`.?`) you will get **0 points for the according task**.
-----------------------------------------------------------------------
## Changelog
* **2023-12-13** [AR]: Fixing some mistakes, clarified allowed regex.
* **2023-12-17** [SG]: Highlight regex syntax better.
