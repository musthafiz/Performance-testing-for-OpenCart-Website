# Content

- [Load testing Report](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#load-testing-report)  
- [Summary](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#summary)  
- [Introduction](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#introduction)  
- [Install](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#install)      
- [Prerequisites](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#prerequisites)   
- [Elements of a Minimal Test Plan](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#prerequisites)    
- [Test Plan](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#test-plan)    
- [Collection of API](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#collection-of-api)   
    - [List of API](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#list-of-api) 
    - [Load the JMeter Script](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#load-the-jmeter-script)  
- [Make jtl File](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#make-jtl-file)  
- [Make html File](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#make-html-file)  
- [HTML Report](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#html-report) 


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

  1) The general setting for the tests' execution, such as whether Thread Groups will run simultaneously or sequentially, is specified in the item called Test Plan.

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

    ### Make jtl file

    - **jmeter -n -t  OPENCART_T1.jmx -l report\OPENCART_T1.jtl**

    - **n**: non GUI mode

    - **t**: test plan to execute

    - **l**: output file with results

    Then continue to upgrade Threads(1 to 6) by keeping Ramp-up Same.   
    ![a](https://user-images.githubusercontent.com/92669932/189541580-9345c967-36a3-48c1-bf51-692431658b27.jpg)   
    ![d](https://user-images.githubusercontent.com/92669932/189541861-ce9b4d40-3edb-408b-affd-c3c98020fddf.jpg)

    




After completing this command  
  ### Make html file  
- **jmeter -g report\OPENCART_T1.jtl -o report\OPENCART_T1.html**  

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






















