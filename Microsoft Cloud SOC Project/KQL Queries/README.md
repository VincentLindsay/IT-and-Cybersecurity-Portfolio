# Overview
- This section features all KQL queries written in this lab.

This query views emails that were allowed to pass into a user's inbox, and contained the subject had the word "Urgent"
```KQL
MailGuard365_Threats_CL
| where Action == "Allow"
| where subject contains "Urgent"
```
This query analyzes failed login events for an administrator account.
```KQL
SecurityEvent
| where EventID == "4625"
| where AccountType == "User"
| where Account Contains "Admin"
| sort by TimeGenerated asc
```

This last query views the number of EventIDs in a Windows environment.
```KQL
SecurityEvent
| summarize EventCount = count() by EventID
| sort by EventCount desc
```

This query analyzes the top 5 accounts with failed login attempts
```KQL
SecurityEvent
| where EventID == "4625"
| summarize Count = Count() by Account
| sort by Count
| take 5
```

This query also Identifies failed logins with an hour timespan
```KQL
let LatestLogTime = toscalar(
    SecurityEvent
    | where EventID == 4625
    | summarize max(TimeGenerated)
);
SecurityEvent
| where EventID == 4625
| where TimeGenerated between (LatestLogTime - 1h .. LatestLogTime)
| where isnotempty(Account)
| summarize FailedLogins = count() by Account
| top 5 by FailedLogins desc
```

This query checks for failed login attempts - This query was used to craft the alert
```KQL
SecurityEvent 
|where EventID == "4625" 
|summarize FailedLogons = count() by Account
|where FailedLogons >= 1000
```













