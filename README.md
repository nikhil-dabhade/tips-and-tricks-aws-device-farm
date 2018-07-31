# Overview
This repo contains code snippets and/or relevant material for common and advanced tips that can be used when running on AWS Device Farm.


## Read excel or properties files from your test code in AWS Device Farm
 
1. During the test packaging step, make sure the excel file is placed under src/test/resources/com/yourexcelfile.xlsx 
2. After executing the packagin command the excel/properties file will be placed in the test jar file under com folder. 
3. You can now use one of the following code snippets in your test code to read the file
 
```java 
   java.net.URL resource = ClassLoader.getSystemResource(“/com/yourexcelfile.xlsx");
   File file = new File(resource.toURI());
   FileInputStream input = new FileInputStream(file);
```

OR 

   If you are using Apache POI APIs for reading excel files: 

```java
   InputStream ins = getClass().getResourceAsStream(“/com/yourexcelfile.xlsx”);
   workbook = new XSSFWorkbook(ins);
   sheet = workbook.getSheetAt(1);
   ins.close();  
```
