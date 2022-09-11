# Menu 

- [Load testing Report](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#load-testing-report)  
- [Summary](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#summary)  
- [Introduction](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#introduction)  
- [Install](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#install)      
- [Prerequisites](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#prerequisites)   
- [Elements of a minimal test plan](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#prerequisites)    
- [Test Plan](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#test-plan)    
- [Collection of API](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#collection-of-api)   
    - [List of API](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#list-of-api) 
    - [Load the JMeter Script](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#load-the-jmeter-script)  
- [Make jtl file](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#make-jtl-file)  
- [Make html file](https://github.com/musthafiz/Load-testing-for-OpenCart-Website/edit/main/README.md#make-html-file)  


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

This document explains how to run performance test with jMeter agains a OpenCart E-commerce Site.

# Install

**Java**  
https://www.oracle.com/java/technologies/downloads/

**JMeter**  
https://jmeter.apache.org/download_jmeter.cgi  

Click =>Binaries    
=>apache-jmeter-5.5.zip

**We use BlazeMeter to generate jmx files**  
https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en

# Prerequisites
- As of JMeter 4.0, Java 8 and above are supported.
- we suggest  multicore cpus with 4 or more cores.
- Memory 16GB RAM is a good value.

# Elements of a minimal test plan
- Thread Group

    The root element of every test plan. Simulatest the (concurrent) users than run all requests. 
    Each thread simulates a single user.

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

  2) All HTTP Requests will use some default settings from the HTTP Request, such as the Server IP, Port Number, and Content Encoding.

  3) Each Thread Group specifies how the HTTP Requests should be carried out. To determine how many concurrent "users" will be simulated, one must first know the number of threads. The number of actions each "user" will perform is determined by the loop count.

  4) The HTTP Header Manager, which allows you to provide the Request Headers that will be utilized by the upcoming HTTP Requests, is the first item in Thread Groups.

# Collection of API

- Run BlazeMeter  
- Collect Frequently used API  
- Save JMX file then paste => apache-jmeter-5.5\bin

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
 
- JMeter should be initialized in non-gui mode.  
- Make a report folde in **bin** file.  
- Run Command in __jmeter\bin__ file. 

    ### Make jtl file

    - **jmeter -n -t  OPENCART_T1.jmx -l report\OPENCART_T1.jtl**

    - **n**: non GUI mode

    - **t**: test plan to execute

    - **l**: output file with results

    Then continue upgrade Threads(1 to 6) by keeping Ramp-up Same.   
    ![a](https://user-images.githubusercontent.com/92669932/189541580-9345c967-36a3-48c1-bf51-692431658b27.jpg)   
    ![d](https://user-images.githubusercontent.com/92669932/189541861-ce9b4d40-3edb-408b-affd-c3c98020fddf.jpg)

    




After completing this command  
  ### Make html file  
- **jmeter -g report\OPENCART_T1.jtl -o report\OPENCART_T1.html**  



  - **g**: jtl results file

  - **o**: path to output folder  

  ![b](https://user-images.githubusercontent.com/92669932/189541594-c608e5c9-9679-4c80-9f90-855985cfb630.jpg)  
  ![f](https://user-images.githubusercontent.com/92669932/189541801-59a45bdd-6a12-44f3-9194-ff41b2c3d954.jpg)
   






















