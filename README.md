# KQL


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
let IdentityLogonEvents = datatable (Timestamp:datetime , AccountName:string, DaviceName:string )
[
    datetime(2022-12-31), "Nancy", "Pelosi",
];
IdentityLogonEvents

```
