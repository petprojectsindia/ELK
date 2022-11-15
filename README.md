# ELK
This project contains information about how to set up ELK (Elastic search, Log stash and Kibana) for your project. 

# Installation Guide

- Elastic search - Download Elastic search uing the link - https://www.elastic.co/downloads/elasticsearch
  - Choose windows option to download elastic search.
  - After downloading and unziping the folder, go to config -> elasticsearch.yaml -> Add below 2 lines for disabling the security.
  
  ```
  xpack.security.enabled: false
  xpack.security.enrollment.enabled: false
  ```
 
  - Inside the bin folder execute the elasticsearch.bat file in the windows powershell.
  - Elastic search engine will start after this execution.
  
- Kibana - Download Logstash uing the link - https://www.elastic.co/downloads/kibana
  - Choose windows option to download kibana.
  - After unziping the folder execute the bin -> kibana.bat file in the powershell.
  
- Logstash - Download Logstash uing the link - https://www.elastic.co/downloads/logstash
  - Choose windows option to download logstash.
  - After unziping the folder execute the bin -> logstash.bat.
  - After the server is up and running create a new config file names logstash.conf at a particular location.
  - Please refer to the file logstash.conf.sample in this repository for reference.
  
   The structure of logstash.conf is as below - 
   
   ```
   input {
    file {
        path => "<your path here>/logs/app.log"
    }
}

output {
    elasticsearch{
        hosts => ["localhost:9200"]
        index => "<your application index here>"
    }
}
   
   ```
 - There are usually 3 sections in the logstash.conf file viz - Input, Putput and filter. ( Filter is optional
   however input and output is mandatory.
 - In the input we need to specify the log files path where our application writes the logs.
 - In the output we need to mention the elastic search server host where we want to push the logs.
 - Also, we need to create an index for every application that we want to integrate with ELK.
   Example Application A can have index - appA.
 - Once this file is ready then execute below command in the windows powershell.
 
 * Pre-requisite - Please add the ELK to the classpath ( until bin folder so that below command can be executed successfully ) 
 ```
 logstash -f logstash.conf
 ```
 
 - Once this command is executed, then opne kibana dashboard using below URL - 
 
 ```
 http://localhost:5601/
 ```
  - On the Kibana portal , search for the index which we have mentioned in our logstash.conf file.
  - USe the same index to discover the logs on the dashboard.
  
