# Lab 02: Black Box Testing

## Step 1: Website Selection

Website Name: Wikipedia
Website URL: https://www.wikipedia.org

Selected Features:
1. Article Search
2. User Login

Purpose:
Design black-box tests using equivalence partitioning,
decision tables, and state transition testing.

Testing Approach:
Tests are designed from expected user-facing behavior.
No application source code is examined.

## Step 2: Equivalence Partitioning

Feature: Wikipedia Article Search

| Partition | Type | Representative Input | Expected Result |
|---|---|---|---|
| Existing article | Valid | Python (programming language) | Matching article is displayed |
| Search term with multiple matches | Valid | Apple | Search results or matching article |
| Mixed-case search | Valid | wIkIpEdIa | Search handles capitalization |
| Leading/trailing spaces | Valid | " Python " | Search handles surrounding spaces |
| Nonexistent article | Valid | xyznonexistentarticle98765 | Search results indicate no exact match |
| Empty search | Invalid | "" | Empty input is handled without an application error |
| Whitespace only | Invalid | "   " | No meaningful article query is submitted |
| Special characters only | Invalid | "@@@###" | Search handles input safely without crashing |

Note:
Invalid partitions represent inputs that are not meaningful
article searches, not necessarily inputs rejected by Wikipedia.

### Equivalence Partition Test Cases

EP01:
Input: Python (programming language)
Expected: Matching article is displayed.

EP02:
Input: Apple
Expected: Relevant article or disambiguation results.

EP03:
Input: wIkIpEdIa
Expected: Search is not blocked by capitalization.

EP04:
Input: " Python "
Expected: Surrounding whitespace is handled.

EP05:
Input: xyznonexistentarticle98765
Expected: No exact article match is reported.

EP06:
Input: Empty string
Expected: Search handles empty input gracefully.

EP07:
Input: Three spaces
Expected: Search handles whitespace-only input gracefully.

EP08:
Input: @@@###
Expected: Search handles special characters safely.

## Step 3: Decision Table Testing

Feature: Wikipedia Article Search

### Conditions

C1: Search query contains meaningful text.
C2: Exact matching article exists.
C3: Multiple possible article matches exist.

### Actions

A1: Open matching article.
A2: Display search results or disambiguation.
A3: Display no-exact-match search results.
A4: Handle empty or meaningless query.

### Decision Table

| Conditions / Actions | R1 | R2 | R3 | R4 |
|---|---|---|---|---|
| Meaningful query | T | T | T | F |
| Exact article exists | T | F | F | - |
| Multiple possible matches | F | T | F | - |
| Open matching article | X | | | |
| Display results/disambiguation | | X | | |
| Display no-exact-match results | | | X | |
| Handle empty query | | | | X |

### Decision Table Test Cases

DT01: Exact Article Match
Input: Python (programming language)
Conditions: Meaningful query, exact article exists.
Expected: Matching article opens.

DT02: Multiple Possible Matches
Input: Apple
Conditions: Meaningful query, multiple article matches.
Expected: Relevant results or disambiguation are shown.

DT03: No Exact Match
Input: xyznonexistentarticle98765
Conditions: Meaningful query, no matching article.
Expected: Search results indicate no exact match.

DT04: Empty Search
Input: ""
Conditions: Query contains no meaningful text.
Expected: Empty query is handled without crashing.

## Step 4: State Transition Testing

Feature: Wikipedia User Login

### States

S1: Logged Out
S2: Login Form Open
S3: Logged In

### Events

E1: Open login page.
E2: Submit valid credentials.
E3: Submit invalid credentials.
E4: Log out.
E5: Navigate away from login form.
E6: Attempt an authenticated action.

### State Transition Table

| Current State | Event | Expected State | Expected Result |
|---|---|---|---|
| Logged Out | Open login page | Login Form Open | Login form appears |
| Login Form Open | Submit valid credentials | Logged In | Login succeeds |
| Login Form Open | Submit invalid credentials | Login Form Open | Error shown |
| Login Form Open | Navigate away | Logged Out | Login form closes |
| Logged In | Log out | Logged Out | Session ends |
| Logged Out | Attempt authenticated action | Logged Out | Login required |
| Logged Out | Log out | Logged Out | No active session to end |
| Logged In | Submit login form again | Logged In | No second login needed |

Note:
Invalid transitions describe actions that should not create
an unauthorized or inconsistent state. They do not imply
that Wikipedia raises a programming exception.

### State Transition Test Cases

ST01: Open Login
Start: Logged Out
Event: Open login page.
Expected: Login Form Open.

ST02: Successful Login
Start: Login Form Open
Event: Submit valid credentials.
Expected: Logged In.

ST03: Failed Login
Start: Login Form Open
Event: Submit invalid credentials.
Expected: Login Form Open with error message.

ST04: Leave Login Page
Start: Login Form Open
Event: Navigate away.
Expected: Logged Out.

ST05: Logout
Start: Logged In
Event: Click logout.
Expected: Logged Out.

ST06: Unauthorized Action
Start: Logged Out
Event: Attempt an action requiring login.
Expected: User remains logged out and authentication is required.

ST07: Logout Without Session
Start: Logged Out
Event: Attempt logout.
Expected: User remains logged out.

ST08: Login While Already Authenticated
Start: Logged In
Event: Attempt to access login again.
Expected: User remains logged in.

### Complete Login Sequence

1. Start Logged Out.
2. Open login page.
3. Enter valid credentials.
4. Login succeeds.
5. User becomes Logged In.
6. User logs out.
7. User returns to Logged Out.

Expected:
The authentication lifecycle completes successfully.

### Failed Login Sequence

1. Start Logged Out.
2. Open login page.
3. Enter invalid credentials.
4. Login fails.
5. User remains on the login form.
6. User is not authenticated.

Expected:
Invalid credentials do not grant access.

## Conclusion

Equivalence partitioning helps identify representative
inputs for valid and invalid search scenarios.

Decision table testing verifies expected search behavior
under different combinations of conditions.

State transition testing verifies login, logout,
authentication failure, and invalid transitions.

These are designed black-box test cases based on
expected behavior, not executed test results.

## AI Transparency

AI assistance was used to help organize the tables
and draft test cases. The work should be reviewed
against the website's observed behavior.
