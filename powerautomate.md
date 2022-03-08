1. When a new email arrives (V3)  
2. Html to text > Body  
3. Html to text 2 > Subject  
4. Initialize variable > Name:DateFormat, Type: String, Value: Received Time  
5. Compose(ConvertDate) > Input:formatDateTime(variables('DateFormat'),'MM/dd/yyyy')   
6. Initialize variable2 > Name:TitleTrim, Type:String, Value: None  
7. Initialize variable 3 > Name:TrimSubject, Type: String, Value: None  
8. Set variable > Name:TrimTitle, Value: first(skip(split(replace(triggerBody()?['Subject'],' ','/'),'/'),2))  
9. Set variable2 > Name:TrimSubject, Value: last(split(triggerBody()?['subject'],'Change Request '))   
10. Compose > trim(substring(variables('TrimSubject'),5,sub(length(variables('TrimSubject')),5)))   
11. Add a row into a table:  
```
Location: OneDrive  
Document Library: OneDrive  
File: FileName  
Table: Table1  
Received Date: Outputs of ConvertDate  
Ticket No: TrimTitle  
Subject: Outputs of Compose  
Requested By: trim(first(split(last(split(body('Html_to_text'),'Requested By:')),'Following Text')))    
```

