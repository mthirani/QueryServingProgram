# QueryServingProgram

### To start executing the QueryServing module, you need to follow the below pre-requisite:

1. Install Docker from the below link if you don't have (needed to run elastic search engine on it). https://docs.docker.com/v17.12/install/#supported-platforms
2. Obtain the elastic search for docker: 
```
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.2.0
```
3. Start the elastic search without ever stopping it to have all the input records to be retained once inputted.
```
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.2.0
```
For more information on above Steps 2 and 3, refer to https://www.elastic.co/guide/en/elasticsearch/reference/7.2/docker.html#docker-prod-cluster-composefile

4. To test whether the elasticsearch engine has been started successfully on your local, you can issue a curl command which will return the cluster status as green or red which is followed by curl command:
```
curl http://127.0.0.1:9200/_cat/health
1472225929 15:38:49 docker-cluster green 2 2 4 2 0 0 0 0 - 100.0%
```

4. Note your port number, cluster name, hostname

### If you followed the above steps, then your cluster name is *docker-cluster*, port number is *9300* and hostname is *localhost* which will be needed as an input to start the below JAR package.

JAR to download: https://drive.google.com/drive/folders/12jZZGBMIvcMXj2mrQC0xWXFoUMqPg20I?usp=sharing

Once you have the JAR, run the below command:

```
java -jar queryserving.jar localhost 9300 docker-cluster
```

#### It will prompt you for your inputs one by one and follow them to run the program. Below is the sample program execution:
```
ERROR StatusLogger Log4j2 could not find a logging implementation. Please add log4j-core to the classpath. Using SimpleLogger to log to the console...
Do you have any file to load? Press Y for Yes or any other character for No
Y
Press enter after you input the path for the file to load :: 
/Users/mayankthirani/Desktop/document.json
Press enter after you input the string to query for :: 
MON
Found 10 below suggestions for the query string
testing_monthylrevenueinlower
Sixth_Monthly_Revenue
Nineth_Monthly_Revenue
Fifth_Monthly_Revenue
Twice_Monthly_Revenue
Half_Monthly_Revenue
Quarterly_Monthly_Revenue
Eight_Monthly_Revenue
Sub_Monthly_Revenue
Forth_Monthly_Revenue
Do you have more string to query for? Press Y for Yes or any other character for No
Y
Press enter after you input the string to query for :: 
rev
Found 10 below suggestions for the query string
test test_revenueinlower
Revenue
RevenueSomething
revenueinlowercase
Sixth_Monthly_Revenue
Nineth_Monthly_Revenue
Fifth_Monthly_Revenue
Twice_Monthly_Revenue
SeventhMonthly_Revenue
Half_Monthly_Revenue
Do you have more string to query for? Press Y for Yes or any other character for No
N
```

#### The input file to load in elastic search is being taken as JSON file with a list of name, score pairs. Sample file which is being loaded:
```
[
   {
      "name":"Revenue",
      "score":100
   },
   {
      "name":"Yearly_Revenue",
      "score":20
   },
   {
      "name":"Monthly_Revenue",
      "score":30
   },
   {
      "name":"Sub_Monthly_Revenue",
      "score":40
   },
   {
      "name":"Quarterly_Monthly_Revenue",
      "score":50
   },
   {
      "name":"Half_Monthly_Revenue",
      "score":60
   },
   {
      "name":"Twice_Monthly_Revenue",
      "score":70
   },
   {
      "name":"Thrice_Monthly_Revenue",
      "score":35
   },
   {
      "name":"Forth_Monthly_Revenue",
      "score":38
   },
   {
      "name":"Fifth_Monthly_Revenue",
      "score":80
   },
   {
      "name":"Sixth_Monthly_Revenue",
      "score":90
   },
   {
      "name":"SeventhMonthly_Revenue",
      "score":66
   },
   {
      "name":"Eight_Monthly_Revenue",
      "score":45
   },
   {
      "name":"Nineth_Monthly_Revenue",
      "score":88
   },
   {
      "name":"TenthRevenue",
      "score":89
   },
   {
      "name":"EleventhRevenue",
      "score":89
   },
   {
      "name":"EleventhRevenueSomething",
      "score":99
   },
   {
      "name":"RevenueSomething",
      "score":97
   },
   {
      "name":"revenueinlowercase",
      "score":95
   },
   {
      "name":"_revenueinlower",
      "score":101
   },
   {
      "name":"test test_revenueinlower",
      "score":105
   },
   {
      "name":"testing_monthylrevenueinlower",
      "score":110
   }
]
```
