# Content

- [Load testing Report](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#load-testing-report)  
- [Summary](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#summary)  
- [Introduction](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#introduction)  
- [Install](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#install)      
- [Prerequisites](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#prerequisites)   
- [Elements of a Minimal Test Plan](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#prerequisites)    
- [Test Plan](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#test-plan)    
- [Collection of API](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#collection-of-api)   
    - [List of API](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#list-of-api) 
    - [Load the JMeter Script](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#load-the-jmeter-script)     
- [Make csv File](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#make-csv-file)    
- [Make jtl File](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#make-jtl-file)  
- [Make html File](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#make-html-file)  
- [HTML Report](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#html-report) 
- [Stress Testing](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#stress-testing)    
- [Spike Testing](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#spike-testing)      
- [Endurance Testing](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#endurance-testing)
- [Read Test Data from CSV file in Jmeter](https://github.com/musthafiz/Performance-testing-for-OpenCart-Website#read-test-data-from-csv-file-in-jmeter)




# Load testing Report

| Concurrent Request  | Loop Count | Avg TPS for Total Samples  | Error Rate | Total Concurrent API request |
|               :---: |      :---: |                      :---: |                        :---: |      :---: |
| 1  | 1  | 3.350  | 0%      | 212   |
| 2  | 1  |  7     | 0%      | 424   |
| 3  | 1  |  11    | 0.47%   | 636   |
| 4  | 1  |  14.1  | 0.59%   | 848   |
| 5  | 1  |  17.6  | 0.94%   | 1060  |
| 6  | 1  |  20    | 1.18%   | 1272  |

### Summary
- While executed 3 concurrent request, found  636 request got connection timeout and error rate is 0.47%.
- Server can handle almost concurrent 424 API call with almost zero (0) error rate.



# Introduction

This document explains how to run a performance test with JMeter against an OpenCart E-commerce Site.

# Install

**Java**  
https://www.oracle.com/java/technologies/downloads/

**JMeter**  
https://jmeter.apache.org/download_jmeter.cgi  

Click =>Binaries    
=>**apache-jmeter-5.5.zip**

**We use BlazeMeter to generate JMX files**    
https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en

# Prerequisites
- As of JMeter 4.0, Java 8 and above are supported.
- we suggest  multicore cpus with 4 or more cores.
- Memory 16GB RAM is a good value.

# Elements of a minimal test plan
- Thread Group

    The root element of every test plan. Simulates the (concurrent) users and then run all requests. Each thread simulates a single user.

- HTTP Request Default (Configuration Element)

- HTTP Request (Sampler)

- Summary Report (Listener)

# Test Plan

Testplan > Add > Threads (Users) > Thread Group (this might vary dependent on the jMeter version you are using)

- Name: Users
- Number of Threads (users): 1 to 6
- Ramp-Up Period (in seconds): 10
- Loop Count: 1  

  1) The general setting for the tests execution, such as whether Thread Groups will run simultaneously or sequentially, is specified in the item called Test Plan.

  2) All HTTP Requests will use some default settings from the HTTP Request, such as the Server IP, Port Number, and Content-Encoding.

  3) Each Thread Group specifies how the HTTP Requests should be carried out. To determine how many concurrent "users" will be simulated, one must first know the number of threads. The number of actions each "user" will perform is determined by the loop count.

  4) The HTTP Header Manager, which allows you to provide the Request Headers that will be utilized by the upcoming HTTP Requests, is the first item in Thread Groups.

# Collection of API

- Run BlazeMeter  
- Collect Frequently used API  
- Save JMX file then paste => **apache-jmeter-5.5\bin**

    ### List of API 

    - [https://www.opencart.com/index.php?route=common/home](https://www.opencart.com/index.php?route=common/home)
    - [https://www.opencart.com/index.php?route=cms/feature](https://www.opencart.com/index.php?route=cms/feature)
    - [https://www.opencart.com/index.php?route=marketplace/extension](https://www.opencart.com/index.php?route=marketplace/extension)
    - [https://www.opencart.com/index.php?route=cms/company](https://www.opencart.com/index.php?route=cms/company)
    - [https://www.opencart.com/index.php?route=account/login](https://www.opencart.com/index.php?route=account/login)

   **OR**
    
  ### Load the JMeter Script 
   - File > Open (CTRL + O)
   - Locate the "OPENCART_T1.jmx" file contained on this repo
   - Continue open OPENCART_T1 to OPENCART_T6
   - Open those file
   - The Test Plan will be loaded  
   
   ![c](https://user-images.githubusercontent.com/92669932/189541560-025b250b-b00e-46a1-9b55-c4ed4f7835ec.jpg)

                                   
# Test execution (from the Terminal)
 
- JMeter should be initialized in non-GUI mode.
- Make a report folder in the **bin** folder.  
- Run Command in __jmeter\bin__ folder. 

 ### Make csv file    
 
   - **n**: non GUI mode
  - **t**: test plan to execute
  - **l**: output file with results   

```bash
  jmeter -n -t  OPENCART_T1.jmx -l OPENCART_T1.csv
```   
![csvfile](https://user-images.githubusercontent.com/92669932/197028552-faf7d3e6-d74a-46fc-b4d2-750c244f2a5e.jpg)


 ### Make jtl file

```bash
  jmeter -n -t  OPENCART_T1.jmx -l OPENCART_T1.jtl
```      
  Then continue to upgrade Threads(1 to 6) by keeping Ramp-up Same.   
  
  ![a](https://user-images.githubusercontent.com/92669932/189541580-9345c967-36a3-48c1-bf51-692431658b27.jpg)   
  
  ![d](https://user-images.githubusercontent.com/92669932/189541861-ce9b4d40-3edb-408b-affd-c3c98020fddf.jpg)

After completing this command  
   ### Make html file   
  
  ```bash
  jmeter -g report\OPENCART_T1.jtl -o OPENCART_T1.html
```
 

  - **g**: jtl results file

  - **o**: path to output folder  

  ![b](https://user-images.githubusercontent.com/92669932/189541594-c608e5c9-9679-4c80-9f90-855985cfb630.jpg)  
  ![f](https://user-images.githubusercontent.com/92669932/189541801-59a45bdd-6a12-44f3-9194-ff41b2c3d954.jpg)  
  

# HTML Report

**Number of Threads 1 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![1](https://user-images.githubusercontent.com/92669932/189543492-df0751ca-3642-4e3f-a050-0454e38117ef.jpg)  |  ![2](https://user-images.githubusercontent.com/92669932/189543499-17c168a2-5b32-4710-9bc0-df7a2b3656c7.jpg)

**Number of Threads 2 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![3](https://user-images.githubusercontent.com/92669932/189543781-8e545531-a134-4dfd-b6bc-36b6539668b5.jpg) |  ![4](https://user-images.githubusercontent.com/92669932/189543783-37624029-b0ea-4671-b5e7-e158453b6d7c.jpg)


**Number of Threads 3 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![5](https://user-images.githubusercontent.com/92669932/189543851-f5ee4f83-275f-4c9d-b716-748380ab337e.jpg)  |  ![6](https://user-images.githubusercontent.com/92669932/189543857-e2042257-9410-4a04-a301-e89631204291.jpg)


**Number of Threads 4 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![7](https://user-images.githubusercontent.com/92669932/189543865-5acac49a-e858-4ce0-95ce-92500d1a1cf0.jpg)  |  ![8](https://user-images.githubusercontent.com/92669932/189543871-749aaf77-1639-4de4-9f59-5476c63ced98.jpg)


**Number of Threads 5 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![9](https://user-images.githubusercontent.com/92669932/189543881-995a888b-c63b-4f38-8b42-d21140704dfc.jpg)  |  ![10](https://user-images.githubusercontent.com/92669932/189543883-8229a05a-6a96-41da-85c8-d8ae587ebcae.jpg)


**Number of Threads 6 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
 ![11](https://user-images.githubusercontent.com/92669932/189543896-bba2da13-370e-438c-84e9-88439c8e307e.jpg) |  ![12](https://user-images.githubusercontent.com/92669932/189543902-851bd50a-95a7-435e-8df2-a6c615786109.jpg)   


# Stress Testing

Stress Testing is a type of software testing that evaluates how the software responds under extreme conditions. It verifies how robust a system will be, and its response capabilities and error handling when it is subjected to conditions where its normal functioning can be compromised.

**Number of Threads 7 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![a](https://user-images.githubusercontent.com/92669932/189820373-01f812aa-acaa-47fc-a7f2-91e813e23a4a.jpg) |  ![b](https://user-images.githubusercontent.com/92669932/189820402-fcef18b3-cd47-4b60-8ee1-87e1a7e59a01.jpg)

  


**Number of Threads 8 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![c](https://user-images.githubusercontent.com/92669932/189820654-d0f9744c-d05e-462f-88f7-ba8f91125f29.jpg) | ![d](https://user-images.githubusercontent.com/92669932/189820670-b90a99e7-d44a-47f5-8d66-806e571c1fb4.jpg)    



**Number of Threads 9 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![e](https://user-images.githubusercontent.com/92669932/189820708-da2be22b-1718-4f9a-a89a-e5235d6d1e82.jpg)  |   ![f](https://user-images.githubusercontent.com/92669932/189820724-4217425e-491d-4177-918b-347e89281b6b.jpg)

# Spike Testing

Spike testing is a type of performance testing where the demand for an application is suddenly and drastically increased or decreased. Spike testing's objective is to ascertain how a software program will behave under highly variable traffic conditions.

**Number of Threads 15 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![s](https://user-images.githubusercontent.com/92669932/189822076-38361a8b-db25-4e43-98f4-2a582d0244fa.jpg) | ![p](https://user-images.githubusercontent.com/92669932/189822103-fdcd8c85-6d17-4135-af20-a700b5bb05d7.jpg)

# Endurance Testing
An application may be put through endurance testing to see if it can handle the processing load that will be placed on it over an extended period of time. Memory usage is tracked throughout endurance tests to identify potential issues.   

**Start Threads count 6s ; Initial Delay 0s ; Start up Time 10s ; Hold load for 600s ; Shutdown Time 0s**     

Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![e](https://user-images.githubusercontent.com/92669932/189861431-3843b069-8a12-4e38-b527-2a28700f7bf9.jpg) | ![f](https://user-images.githubusercontent.com/92669932/189861468-84b0bd3c-1531-4a30-a7b2-9d9f59964823.jpg)

![t](https://user-images.githubusercontent.com/92669932/189866938-ce1e11e2-9720-4c4f-91a6-6c79e450632b.jpg)

# Read Test Data from CSV file in Jmeter    

- Create a CSV file in the test suite folder and add test data to it.  <br/>

![csv](https://user-images.githubusercontent.com/92669932/189913089-8bab3573-ad13-4d80-b9da-ff8168b953fe.jpg)

- Add a Config Element CSV Data Set Config in Jmeter.   <br/>

![2](https://user-images.githubusercontent.com/92669932/189913286-0ef1bf60-234f-4275-8def-47d815221dab.jpg)   

- Configure ' CSV Data Set Config ' based on the need such as providing path of CSV file and variable names and other configs.   <br/>

![1](https://user-images.githubusercontent.com/92669932/189913690-80380eda-a4df-4e92-901b-5f1424dadcc2.jpg)  

- Run the test to see if data from the CSV file is read and populated in the results.  <br/>

- Run the test to see if data from CSV file is read and populated in the results.    <br/>  


**Number of Threads 13 ; Ramp-Up Period 5s**

<p float="left">
  <img src="https://user-images.githubusercontent.com/92669932/189938100-48702b1a-99a6-4de4-af25-66f069b78e1c.jpg" width="49%" />   
  <img src="https://user-images.githubusercontent.com/92669932/189938110-331e82ad-1e51-465a-a2e8-aec250760351.jpg" width="49%" />   
  <img src="https://user-images.githubusercontent.com/92669932/189938113-dee95de0-4302-41ed-9924-5ddac5836cfe.jpg" width="49%" />    
  <img src="https://user-images.githubusercontent.com/92669932/189938115-2de6ea5e-d90c-4fd1-bcc9-7e3997c52693.jpg" width="49%" />     
</p>



