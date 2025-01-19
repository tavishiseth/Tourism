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

## CREATING TABLE QUERIES
1. Creating Table Booked_for:  
![image](https://user-images.githubusercontent.com/75008683/177981747-73fa34a3-9555-4886-b1c8-07a5872d44c2.png)


2. Creating Table Customer:  
![image](https://user-images.githubusercontent.com/75008683/177981775-ff64316b-a3bd-4c41-8d0a-89b67d880b8b.png)


3. Creating Table Driven_By:  
![image](https://user-images.githubusercontent.com/75008683/177981803-5bfac38f-6aae-4c52-a8be-5ef14c7a5068.png)


4. Creating Table Payment:  
![image](https://user-images.githubusercontent.com/75008683/177981840-0dd6d013-80e1-446c-9891-f5c1ad322549.png)


5. Creating Table Places:  
![image](https://user-images.githubusercontent.com/75008683/177981863-d66e8a93-d2a3-4fdf-80ea-fb8c98bf7b06.png)


6. Creating Table Employee:  
![image](https://user-images.githubusercontent.com/75008683/177981897-6334af9b-a38a-4acf-ab40-9a40e7b6687d.png)


7. Creating Table Trip:  
![image](https://user-images.githubusercontent.com/75008683/177981921-23d1fefc-b85b-4fca-a9c8-a54c64bcc17d.png)

## CREATING CONSTRAINTS:
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
```

No contraints in login table:  
```
CREATE TABLE `login` (
  `username` varchar(45) NOT NULL,
  `password` varchar(45) NOT NULL,
  PRIMARY KEY (`password`, `username`)
)
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
```

No constraints in places table:  
```
CREATE TABLE `places` (
  `idplaces` int(11) NOT NULL,
  `city` varchar(45) NOT NULL,
  `distance` varchar(45) NOT NULL
)
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










