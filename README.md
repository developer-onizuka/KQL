# KQL

> https://security.microsoft.com/

```
let LeftTable = datatable (key:int, value:string, id:int)
[
    0, "Hello", 1000,
    0, "Hola", 1001,
    1, "Salut", 1002,
    1, "Ciao", 1003,
    2, "Hallo", 1004
];
let RightTable = datatable (key:int, value:string, xid:int)
[
    0, "World", 1000,
    0, "Mundo", 1001,
    1, "Monde", 1002,
    1, "Mondo", 1003,
    2, "Welt", 1004
];
LeftTable
| project-rename xid = id
| join RightTable on xid
```

```
let LeftTable = datatable (key:int, value:string, id:int)
[
    0, "Hello", 1000,
    0, "Hola", 1001,
    1, "Salut", 1002,
    1, "Ciao", 1003,
    2, "Hallo", 1004
];
let RightTable = datatable (key:int, value:string, xid:int)
[
    0, "World", 1000,
    0, "Mundo", 1001,
    1, "Monde", 1002,
    1, "Mondo", 1003,
    2, "Welt", 1004
];
LeftTable
| project-rename xid = id
| join RightTable on xid
| summarize count() by key, key1
```

```
let EmailEvents = datatable (Timestamp:datetime, AccountName:string, Subject:string ,MalwareFilterVerdict:string)
[
    datetime(2022-12-31 22:59:59), "Nancy", "Hello", "Malware",
    datetime(2022-12-31 22:59:59), "Mike", "Hello", "Malware"
];
let IdentityLogonEvents = datatable (Timestamp:datetime, AccountName:string, DeviceName:string )
[
    datetime(2022-12-31 23:59:59), "Nancy", "Pelosi",
    datetime(2022-12-31 23:59:59), "Mike", "Pence"
];
let MaliciousEmails = EmailEvents
| where MalwareFilterVerdict == "Malware"
| project TimeEmail = Timestamp, AccountName, Subject;
MaliciousEmails
| join (IdentityLogonEvents| project LogonTime = Timestamp, AccountName, DeviceName) on AccountName
| where (LogonTime - TimeEmail) between (0min.. 60min)
| take 20
```
