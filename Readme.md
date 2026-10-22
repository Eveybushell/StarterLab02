# Step 1 Website/Feature Selection

- Website: Autostraddle
- URL: https://www.autostraddle.com/
- Features: Sign In, View AF+ Article

# Step 2 Equivalence Partitioning with Email in Sign in Form

| Classification   | Partition             | Range or Condition  | Expected Result                     |
| ---------------- | --------------------- | ------------------- | ----------------------------------- |
| Email address | Invalid pattern | Invalid email pattern  | Display `Please enter a valid email address` |
| Email address | Invalid email  | Unrecognized email | Display `Unrecognized email` |
| Email address | Valid email | Recognized email | Check password |

# Step 3 Decision tables with Viewing AF+ Article

### Conditions:
- is Logged In
- is AF+ Subscriber

### Actions:
- Displays premium article
- Displays invitation to subscribe

### Table:

| Conditions and Actions         | Rule 1 | Rule 2 | Rule 3 | Rule 4 | Rule 5 | Rule 6 |
| ------------------------------ | :----: | :----: | :----: | :----: | :----: | :----: |
| Is logged in                   |    T    |   F     |    T    |   F     |
| Has an AF+ Subscription        |    T    |   T     |    F    |   F     |
| **Displays premium article**   |    X    |        |        |        |
| **Displays invitation to subscribe**   |        |    X    |   X     |    X    |

### Test Cases:

### TC01: Logged In and Subscriber

- **isSignedIn:** True
- **IsSubscriber:** True
- **Expected Result:** Display full article

### TC02: Logged Out and Subscriber

- **isSignedIn:** False
- **IsSubscriber:** True
- **Expected Result:** Display invitation to subscribe

### TC03: Logged In and Not Subscriber

- **isSignedIn:** True
- **IsSubscriber:** False
- **Expected Result:** Display invitation to subscribe

### TC04: Logged Out and Not Subscriber

- **isSignedIn:** False
- **IsSubscriber:** False
- **Expected Result:** Display invitation to subscribe

# Step 4 State Transition Testing on Sign In

### States:
- Signed Out
- Signed In
- Warning
- Temporarily Locked

### Events
- Signing in Correctly
- Signing in Incorrectly
- Invalid password 4 times
- Invalid password 5 times

### Valid transitions:
- Signed Out -> Signed In (Signing in Correctly)
- Signed Out -> Warning (Invalid password 4 times)
- Warning -> Temporarily Locked (Invalid password 5 times)

### Invalid transition:
- Signed Out -> Signed Out (Signing in Incorrectly)

### Table

| Current State | Event            | Expected State | Expected Result          |
| ------------- | ---------------- | -------------- | ------------------------ |
| Signed Out    | Correct Sign In  | Signed In      | Go to main page          |
| Signed Out    | Incorrect Sign In | Signed Out    | Display correct error message |
| Signed Out    | 4th Invalid Password | Warning    | Display Warning message  |
| Signed Out    | 5th Invalid Password | Temporarily locked | Display Account Lock message |

### Test Cases

| Test ID | Step | Current State | Event            | Expected State | Expected Result    | Transition Type |
| ---- | - | ------------- | ---------------- | -------------- | ------------------------ | --------------- |
| ST01 | - | Signed Out    | Correct Sign In  | Signed In      | Go to main page          | Valid |
| ST02 | - | Signed Out    | Incorrect Sign In | Signed Out    | Display correct error message | Invalid |
| ST03 | 1 | Signed Out    | 1st Incorrect Password | Signed Out    | Display Incorrect Password message | Invalid |
|  -   | 2 | Signed Out    | 2nd Incorrect Password | Signed Out | Display Incorrect Password message | Invalid |
|  -   | 3 | Signed Out    | 3rd Incorrect Password | Signed Out | Display Incorrect Password message | Invalid |  
|  -   | 4 | Signed Out    | 4th Incorrect Password | Warning | Display Warning message | Valid |    
| ST04 | 1 | Signed Out    | 1st Invalid Password | Signed Out | Display Incorrect Password message | Invalid |
|  -   | 2 | Signed Out    | 2nd Incorrect Password | Signed Out | Display Incorrect Password message | Invalid |  
|  -   | 3 | Signed Out    | 3rd Incorrect Password | Signed Out | Display Incorrect Password message | Invalid |  
|  -   | 4 | Signed Out    | 4th Incorrect Password | Warning | Display Warning message | Valid |  
|  -   | 5 | Warning    | 5th Incorrect Password | Temporarily Locked | Display Account Locked message | Valid |  


