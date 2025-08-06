# Test Plan for School Legacy COBOL Accounting System

## Overview
This test plan covers all business logic functionality in the legacy COBOL accounting system. It will be used to validate requirements with business stakeholders and later serve as the foundation for creating unit and integration tests in the Node.js modernized application.

## Test Environment
- **System Under Test**: School Legacy COBOL Accounting System
- **Initial Account Balance**: $1000.00
- **Maximum Balance Limit**: $9999.99
- **Decimal Precision**: 2 decimal places

## Test Cases

### User Interface and Navigation Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-001 | Display main menu on application start | Application is started | 1. Launch application | Menu displays with options: 1. View Balance, 2. Credit Account, 3. Debit Account, 4. Exit | | | |
| TC-002 | Valid menu option selection - View Balance | Application displays main menu | 1. Enter option "1" | System calls View Balance operation and displays current balance | | | |
| TC-003 | Valid menu option selection - Credit Account | Application displays main menu | 1. Enter option "2" | System calls Credit Account operation and prompts for amount | | | |
| TC-004 | Valid menu option selection - Debit Account | Application displays main menu | 1. Enter option "3" | System calls Debit Account operation and prompts for amount | | | |
| TC-005 | Valid menu option selection - Exit | Application displays main menu | 1. Enter option "4" | System displays "Exiting the program. Goodbye!" and terminates | | | |
| TC-006 | Invalid menu option selection | Application displays main menu | 1. Enter option "5" | System displays "Invalid choice, please select 1-4." and returns to menu | | | |
| TC-007 | Invalid menu option selection - zero | Application displays main menu | 1. Enter option "0" | System displays "Invalid choice, please select 1-4." and returns to menu | | | |
| TC-008 | Invalid menu option selection - negative | Application displays main menu | 1. Enter option "-1" | System displays "Invalid choice, please select 1-4." and returns to menu | | | |
| TC-009 | Menu loop functionality | Application displays main menu | 1. Enter valid option (1-3)<br>2. Complete operation<br>3. Verify menu redisplays | Menu redisplays after each operation until exit is selected | | | |

### View Balance Functionality Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-010 | View initial balance | System initialized with default balance | 1. Select option "1" | System displays "Current balance: 1000.00" | | | |
| TC-011 | View balance after credit transaction | Account has been credited with amount | 1. Perform credit operation<br>2. Select option "1" | System displays updated balance reflecting the credit | | | |
| TC-012 | View balance after debit transaction | Account has been debited with amount | 1. Perform debit operation<br>2. Select option "1" | System displays updated balance reflecting the debit | | | |
| TC-013 | View balance data persistence | Balance has been modified in previous session | 1. Exit application<br>2. Restart application<br>3. Select option "1" | System displays the last saved balance, not initial balance | | | |

### Credit Account Functionality Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-014 | Credit account with valid amount | Current balance is $1000.00 | 1. Select option "2"<br>2. Enter amount "100.00" | System displays "Amount credited. New balance: 1100.00" | | | |
| TC-015 | Credit account with decimal amount | Current balance is $1000.00 | 1. Select option "2"<br>2. Enter amount "25.50" | System displays "Amount credited. New balance: 1025.50" | | | |
| TC-016 | Credit account with minimum amount | Current balance is $1000.00 | 1. Select option "2"<br>2. Enter amount "0.01" | System displays "Amount credited. New balance: 1000.01" | | | |
| TC-017 | Credit account with zero amount | Current balance is $1000.00 | 1. Select option "2"<br>2. Enter amount "0.00" | System displays "Amount credited. New balance: 1000.00" | | | |
| TC-018 | Credit account with large amount | Current balance is $1000.00 | 1. Select option "2"<br>2. Enter amount "8999.99" | System displays "Amount credited. New balance: 9999.99" | | | |
| TC-019 | Credit account exceeding maximum limit | Current balance is $9000.00 | 1. Select option "2"<br>2. Enter amount "1000.00" | System behavior when exceeding $9999.99 limit needs verification | | | Boundary condition test |
| TC-020 | Credit account balance persistence | Account credited with amount | 1. Perform credit operation<br>2. Exit application<br>3. Restart and view balance | New balance is maintained after restart | | | |

### Debit Account Functionality Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-021 | Debit account with sufficient funds | Current balance is $1000.00 | 1. Select option "3"<br>2. Enter amount "100.00" | System displays "Amount debited. New balance: 900.00" | | | |
| TC-022 | Debit account with decimal amount | Current balance is $1000.00 | 1. Select option "3"<br>2. Enter amount "25.50" | System displays "Amount debited. New balance: 974.50" | | | |
| TC-023 | Debit exact balance amount | Current balance is $1000.00 | 1. Select option "3"<br>2. Enter amount "1000.00" | System displays "Amount debited. New balance: 0.00" | | | |
| TC-024 | Debit with insufficient funds | Current balance is $100.00 | 1. Select option "3"<br>2. Enter amount "150.00" | System displays "Insufficient funds for this debit." and balance remains unchanged | | | |
| TC-025 | Debit amount exceeding balance by 1 cent | Current balance is $100.00 | 1. Select option "3"<br>2. Enter amount "100.01" | System displays "Insufficient funds for this debit." and balance remains unchanged | | | |
| TC-026 | Debit minimum amount | Current balance is $1000.00 | 1. Select option "3"<br>2. Enter amount "0.01" | System displays "Amount debited. New balance: 999.99" | | | |
| TC-027 | Debit zero amount | Current balance is $1000.00 | 1. Select option "3"<br>2. Enter amount "0.00" | System displays "Amount debited. New balance: 1000.00" | | | |
| TC-028 | Debit account balance persistence | Account debited with amount | 1. Perform debit operation<br>2. Exit application<br>3. Restart and view balance | New balance is maintained after restart | | | |

### Data Management and Persistence Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-029 | Data read operation | System initialized | 1. Perform any balance inquiry | System successfully retrieves stored balance | | | |
| TC-030 | Data write operation after credit | Account credited with amount | 1. Credit account<br>2. View balance | Updated balance is correctly stored and retrieved | | | |
| TC-031 | Data write operation after debit | Account debited with amount | 1. Debit account<br>2. View balance | Updated balance is correctly stored and retrieved | | | |
| TC-032 | Multiple transaction persistence | Multiple transactions performed | 1. Perform credit transaction<br>2. Perform debit transaction<br>3. Exit and restart<br>4. View balance | Final balance reflects all transactions | | | |

### Business Rule Validation Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-033 | Initial balance validation | Fresh system installation | 1. Start application<br>2. View balance | System displays initial balance of $1000.00 | | | |
| TC-034 | Overdraft prevention | Current balance is $50.00 | 1. Attempt to debit $100.00 | System prevents transaction and displays insufficient funds message | | | |
| TC-035 | Balance format validation | Any balance amount | 1. View balance after any transaction | Balance is displayed with exactly 2 decimal places | | | |
| TC-036 | Maximum balance boundary | Current balance is $9999.98 | 1. Credit account with $0.01 | System handles maximum balance correctly | | | Boundary condition |
| TC-037 | Negative amount handling - Credit | System prompts for credit amount | 1. Enter negative amount like "-50.00" | System behavior with negative input needs verification | | | Edge case |
| TC-038 | Negative amount handling - Debit | System prompts for debit amount | 1. Enter negative amount like "-50.00" | System behavior with negative input needs verification | | | Edge case |

### Integration Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-039 | Complete user workflow | System initialized | 1. View initial balance<br>2. Credit $200.00<br>3. Debit $50.00<br>4. View final balance<br>5. Exit | All operations complete successfully with correct balance calculations | | | |
| TC-040 | Main-Operations integration | Application started | 1. Select any menu option (1-3) | Main program successfully calls Operations program with correct parameters | | | |
| TC-041 | Operations-Data integration | Operations program called | 1. Perform any account operation | Operations program successfully calls DataProgram for read/write operations | | | |
| TC-042 | End-to-end transaction flow | System initialized | 1. Complete full transaction cycle<br>2. Verify data flow through all three programs | Data flows correctly from UI through business logic to data storage | | | |

### Error Handling and Edge Cases

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|--------|----------|
| TC-043 | Invalid amount format - letters | System prompts for amount | 1. Enter "ABC" when prompted for amount | System behavior with non-numeric input needs verification | | | |
| TC-044 | Invalid amount format - special chars | System prompts for amount | 1. Enter "!@#" when prompted for amount | System behavior with special characters needs verification | | | |
| TC-045 | Very large amount input | System prompts for amount | 1. Enter amount exceeding system limits like "999999999.99" | System handles large number input appropriately | | | |
| TC-046 | Empty input handling | System prompts for any input | 1. Press Enter without typing anything | System behavior with empty input needs verification | | | |
| TC-047 | Program termination handling | Application running | 1. Use system interrupt (Ctrl+C) or abnormal termination | System handles unexpected termination gracefully | | | |

## Test Execution Notes

### Priority Levels
- **High Priority**: TC-001 to TC-028 (Core functionality)
- **Medium Priority**: TC-029 to TC-038 (Business rules and data management)
- **Low Priority**: TC-039 to TC-047 (Integration and edge cases)

### Test Data Requirements
- Default initial balance: $1000.00
- Test amounts: $0.01, $25.50, $100.00, $999.99, $1000.00, $9999.99
- Invalid inputs: negative numbers, letters, special characters, empty strings

### Business Stakeholder Validation Points
1. Confirm initial balance amount ($1000.00)
2. Verify overdraft prevention is required business rule
3. Confirm maximum balance limit ($9999.99)
4. Validate decimal precision requirements (2 places)
5. Confirm user interface flow and menu options
6. Verify data persistence requirements between sessions

### Notes for Node.js Implementation
- These test cases will be converted to Jest unit tests
- Integration tests will use supertest for API endpoints
- Mock data layer for unit testing business logic
- Separate UI tests for frontend components
- Consider adding test cases for concurrent user scenarios in Node.js version
