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

## Using testng.xml file in AWS Device Farm

1. The xml file should be named testng.xml (case-sensitive).

2. When you are packaging your tests using the steps mentioned in [Device Farm documentation](https://docs.aws.amazon.com/devicefarm/latest/developerguide/test-types-android-appium-java-testng.html) the testng.xml should be placed under **src/test/resources** in your source code folder structure. 

      The packaging step will put the xml file on the root level of *-tests.jar file which is one of the two .jar file that are   generated as output from the packaging process. They can also be found inside the zip-with-dependencies.zip file.

3. Currently, Device Farm supports basic filtering using testng.xml in the standard mode of execution. This means you can mention the suite and the test cases under it that you want to run. Work is been done to expand the supported feature set of testng.xml with time. 
 
For e.g. Our [Github Appium sample tests](https://github.com/aws-samples/aws-device-farm-appium-tests-for-sample-app) has several test classes and if you want to execute only 2 test classes named AlertTest and CameraTest the testing.xml for it would look like: 
 
 <?xml version="1.0" encoding="UTF-8"?>
 <!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
 <suite name="Default Suite">
     <test name="aws-device-farm-appium-testng-tests-for-ios-sample-app">
         <classes>
             <class name="Tests.AlertTest"/>
             <class name="Tests.Native.CameraTest"/>
         </classes>
     </test>
 </suite>
