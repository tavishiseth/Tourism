# Tourism-Management-System
Tourism Agency Management System is a solution for travel agencies to maintain the details of vehicle, employee, trip and the people booking a trip, in an easier and convenient way.  

[Tourism Management Demo Video](./Tourism%20Management.mp4)
### Necessity of the project 
Tourism Agency Management System would play a vital role in planning a perfect trip for people going on vacations.
The main purpose is to help tourism companies manage their customers and trips.  
It provides an user interface for the administrator for managing the data present in the travel agency and reduces the time of recording the data.
### Techstacks Used
1. Netbeans  
2. MySQL  
3. Java  
## ER Diagram
![image](https://user-images.githubusercontent.com/75008683/177980506-da644d8a-ada3-4ae6-a35f-ea2a340b828d.png)
## Relational Schema
![image](https://user-images.githubusercontent.com/75008683/177980603-60c6845a-802c-4f3c-b487-bc85354f6a55.png)

## CREATING TABLE QUERIES & CONSTRAINTS:
Constraints in booked_for table:  
```
CREATE TABLE `booked_for` (
  `VID` int(11) NOT NULL,
  `CID` int(11) NOT NULL,
  `TID` int(11) NOT NULL,
  `BDATE` date DEFAULT NULL,
  PRIMARY KEY (`VID`, `CID`, `TID`),
  KEY `cfk_tid1_idx` (`TID`),
  KEY `cfk_cid1_idx` (`CID`),
  CONSTRAINT `cfk_cid1` FOREIGN KEY (`CID`) REFERENCES `customer` (`cid`) ON DELETE CASCADE ON UPDATE RESTRICT,
  CONSTRAINT `cfk_tid1` FOREIGN KEY (`TID`) REFERENCES `trip` (`tid`) ON DELETE CASCADE ON UPDATE RESTRICT,
  CONSTRAINT `cfk_vid1` FOREIGN KEY (`VID`) REFERENCES `vehicle` (`vid`) ON DELETE CASCADE ON UPDATE RESTRICT
)
+-----+-----+------+------------+
| VID | CID | TID  | BDATE      |
+-----+-----+------+------------+
|   1 | 101 | 1001 | 2025-01-04 |
|   2 | 102 | 1002 | 2025-01-05 |
|   3 | 103 | 1003 | 2025-01-05 |
|   4 | 104 | 1004 | 2025-01-06 |
|   4 | 201 | 2001 | 2025-02-01 |
|   5 | 105 | 1005 | 2025-01-09 |
|   6 | 106 | 1006 | 2025-01-11 |
|   7 | 107 | 1007 | 2025-01-12 |
|   8 | 108 | 1008 | 2025-01-15 |
|  10 | 110 | 1010 | 2025-01-17 |
+-----+-----+------+------------+
```

Constraints in driven_by table:  
```
CREATE TABLE `driven_by` (
  `VID` int(11) NOT NULL,
  `EID` int(11) NOT NULL,
  `TID` int(11) NOT NULL,
  `DDATE` date DEFAULT NULL,
  PRIMARY KEY (`VID`, `EID`, `TID`),
  KEY `cfk_eid1_idx` (`EID`),
  KEY `cfk_tid2_idx` (`TID`),
  CONSTRAINT `cfk_eid1` FOREIGN KEY (`EID`) REFERENCES `employee` (`eid`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `cfk_tid2` FOREIGN KEY (`TID`) REFERENCES `trip` (`tid`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `cfk_vid2` FOREIGN KEY (`VID`) REFERENCES `vehicle` (`vid`) ON DELETE CASCADE ON UPDATE CASCADE
)
+-----+-----+------+------------+
| VID | EID | TID  | DDATE      |
+-----+-----+------+------------+
|   4 |  24 | 2001 | 2025-02-01 |
+-----+-----+------+------------+
```

No constraints in customer table:  
```
CREATE TABLE `customer` (
  `cid` int(11) NOT NULL,
  `cname` varchar(45) DEFAULT NULL,
  `caddress` varchar(45) DEFAULT NULL,
  `cphone` varchar(20) DEFAULT NULL,
  PRIMARY KEY (`cid`)
)
+-----+----------+----------+------------+
| cid | cname    | caddress | cphone     |
+-----+----------+----------+------------+
| 101 | raghav   | 123,abc  | 9908740851 |
| 102 | Joey     | 213,bcd  | 9908740311 |
| 103 | Chandler | 214,fgh  | 9928560321 |
| 104 | Ross     | 215,klm  | 9441429424 |
| 105 | Phoebe   | 314,dsa  | 9885645367 |
| 106 | Rachel   | 516,abc  | 8498469900 |
| 107 | Monica   | 517,dpk  | 1234567890 |
| 108 | Emma     | 768,fgh  | 9988776655 |
| 109 | Richard  | 897,bhv  | 6677889900 |
| 110 | Geller   | 865,vfd  | 9394061050 |
| 201 | Tavishi  | 123,Hyd  | 1234567890 |
+-----+----------+----------+------------+
```

Constraints in employee table:  
```
CREATE TABLE `employee` (
  `eid` int(11) NOT NULL AUTO_INCREMENT,
  `ename` varchar(45) NOT NULL,
  `ephone` varchar(20) NOT NULL,
  `eaddress` varchar(45) DEFAULT NULL,
  `eJdate` date NOT NULL,
  PRIMARY KEY (`eid`),
  UNIQUE KEY `eid_UNIQUE` (`eid`),
  CONSTRAINT `du_che_con` CHECK (`ejdate` >= _utf8mb4 '1990-01-01')
)
+-----+-----------+------------+-----------+------------+
| eid | ename     | ephone     | eaddress  | eJdate     |
+-----+-----------+------------+-----------+------------+
|  11 | Shannon   | 7555045129 | a234      | 2024-01-16 |
|  15 | Dawn      | 8555801440 | a254      | 2024-05-18 |
|  17 | Brittany  | 1555302988 | c254      | 2024-09-22 |
|  24 | Brandon   | 7555673090 | m261      | 2024-02-02 |
|  26 | Jack      | 9655554199 | m255      | 2024-03-04 |
|  36 | Katherine | 9455599130 | 9253      | 2024-09-28 |
|  37 | Kenneth   | 9455588277 | h567      | 2024-12-27 |
|  45 | James     | 2029182132 | s890      | 2024-01-01 |
|  82 | Mike      | 2029182136 | j123      | 2024-01-25 |
|  98 | Tavishi   | 1234567890 | Bangalore | 2025-01-06 |
+-----+-----------+------------+-----------+------------+
```

No contraints in login table:  
```
CREATE TABLE `login` (
  `username` varchar(45) NOT NULL,
  `password` varchar(45) NOT NULL,
  PRIMARY KEY (`password`, `username`)
)
+----------+----------+
| username | password |
+----------+----------+
| admin    | admin    |
+----------+----------+
```

Constraints in payment table:  
```
CREATE TABLE `payment` (
  `TID` int(11) NOT NULL,
  `CID` int(11) NOT NULL,
  `DISTANCETRAVEL` varchar(45) DEFAULT NULL,
  `AMOUNT` varchar(45) DEFAULT NULL,
  `PDATE` date DEFAULT NULL,
  PRIMARY KEY (`TID`, `CID`),
  KEY `cfk_cid_idx` (`CID`),
  CONSTRAINT `cfk_cid` FOREIGN KEY (`CID`) REFERENCES `customer` (`cid`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `cfk_tid` FOREIGN KEY (`TID`) REFERENCES `trip` (`tid`) ON DELETE CASCADE ON UPDATE CASCADE
)
+------+-----+----------------+--------+------------+
| TID  | CID | DISTANCETRAVEL | AMOUNT | PDATE      |
+------+-----+----------------+--------+------------+
| 2001 | 201 | 245            |  220.5 | 2025-02-01 |
+------+-----+----------------+--------+------------+
```

No constraints in places table:  
```
CREATE TABLE `places` (
  `idplaces` int(11) NOT NULL,
  `city` varchar(45) NOT NULL,
  `distance` varchar(45) NOT NULL
)
Empty set
```

Constraints in trip table:  
```
CREATE TABLE `trip` (
  `tid` int(11) NOT NULL,
  `source` varchar(45) DEFAULT NULL,
  `dest` varchar(45) DEFAULT NULL,
  `sdate` date DEFAULT NULL,
  `edate` date DEFAULT NULL,
  PRIMARY KEY (`tid`),
  CONSTRAINT `dateconstraint` CHECK (
    (
      (`sdate` >= sysdate())
      and (`sdate` <= _utf8mb4 '2025-12-30')
    )
  ),
  CONSTRAINT `dateconstraintsdb` CHECK (
    (
      (`edate` >= `sdate`)
      and (`edate` <= _utf8mb4 '2026-12-31')
    )
  )
+------+--------+------+------------+------------+
| tid  | source | dest | sdate      | edate      |
+------+--------+------+------------+------------+
| 1001 | Hyd    | mum  | 2025-02-04 | 2025-02-07 |
| 1002 | Blr    | koc  | 2025-02-05 | 2025-02-11 |
| 1003 | koc    | mum  | 2025-02-05 | 2025-02-08 |
| 1004 | hyd    | blr  | 2025-02-06 | 2025-02-10 |
| 1005 | chn    | blr  | 2025-02-09 | 2025-02-14 |
| 1006 | del    | chn  | 2025-02-11 | 2025-02-17 |
| 1007 | mum    | chn  | 2025-02-12 | 2025-02-19 |
| 1008 | koc    | del  | 2025-02-15 | 2025-02-19 |
| 1010 | hyd    | kol  | 2025-02-17 | 2025-02-25 |
| 2001 | Blr    | Ooty | 2025-02-01 | 2025-02-09 |
+------+--------+------+------------+------------+
```

Constraints on vehicle table:  
```
CREATE TABLE `vehicle` (
  `vid` int(11) NOT NULL AUTO_INCREMENT,
  `vname` varchar(50) DEFAULT NULL,
  `cap` varchar(11) DEFAULT NULL,
  `vtype` varchar(50) DEFAULT NULL,
  `regno` varchar(50) DEFAULT NULL,
  PRIMARY KEY (`vid`)
)
+-----+--------------+------+-------+-------+
| vid | vname        | cap  | vtype | regno |
+-----+--------------+------+-------+-------+
|   1 | mahindra-car | 4    | Car   | 211   |
|   2 | hero-bike    | 2    | Bike  | 212   |
|   3 | BMW-E-class  | 4    | Car   | 213   |
|   4 | rangerover   | 6    | SUV   | 214   |
|   5 | alto-car     | 4    | Car   | 215   |
|   6 | swift-car    | 4    | Car   | 216   |
|   7 | verna-car    | 4    | Car   | 217   |
|   8 | wolkswagen   | 4    | Car   | 218   |
|   9 | mahindra-bus | 15   | Bus   | 219   |
|  10 | BMW-SUV      | 6    | SUV   | 220   |
|  45 | Tiago        | 4    | Sedan | 789   |
|  63 | Audi         | 3    | Car   | 876   |
|  83 | Tata         | 4    | Car   | 432   |
| 131 | Jaguar       | 5    | SUV   | 453   |
| 139 | Indigo       | 3    | Car   | 123   |
+-----+--------------+------+-------+-------+
```


## FRONT-END GUI:
![image](https://github.com/user-attachments/assets/837fa2c8-ab9b-4c02-99eb-6fb7ef87d09b)
![image](https://github.com/user-attachments/assets/4c11775b-f280-4ed0-8b29-c72aac1ede96)
![image](https://github.com/user-attachments/assets/e99e8c76-df04-4cd3-abdd-c6101adad317)
![image](https://github.com/user-attachments/assets/2eae1054-43f5-457e-9cd5-3ce0f5df5cda)
![image](https://github.com/user-attachments/assets/47907c21-edd1-4b29-9daf-4db796daaadb)
![image](https://github.com/user-attachments/assets/b56aa0d3-3e1a-4c0c-98e2-44c43c01e92d)
![image](https://github.com/user-attachments/assets/75cd5287-d69a-440d-9462-70888b0321ec)
![image](https://github.com/user-attachments/assets/969874e4-bf2f-41a2-9a8f-773c78c6f054)
![image](https://github.com/user-attachments/assets/93da9e5e-d838-4cbd-a69a-674c27f1c069)










