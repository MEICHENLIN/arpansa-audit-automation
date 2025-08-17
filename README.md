# ARPANSA Audit Data Automation
As the volume and complexity of audit data at ARPANSA increased, traditional Excel-based workflows became inefficient and unsustainable. The audit files were often unstructured, with inconsistent formats, complicated columns, and data that was difficult to interpret or analyse effectively. These issues resulted in manual, error-prone processes and slow turnaround times for key tasks.

This system addresses those challenges by transforming the legacy Excel data into a normalised MySQL database schema and generating “IMRT” and “3DRT” audit graphs for further analysis.

By streamlining data ingestion, structuring complex datasets, and automating repetitive tasks, this solution improves readability, enhances maintainability, and enables faster, more reliable auditing — laying the groundwork for scalable, data-driven operations at ARPANSA.

A local program is developed as a substitution of front-end to allow user to run the automated process with various options.

## Recommended System Requirement

* **CPU**: 3.2GHz x 2 cores
* **RAM**: 16GB
* **Hard drive**: 40GB
* **Operating** **system**: Linux(centOS)

## Technology
* Database: Mysql 8.0
* Backend: Django Rest Framework 3.11.1
* Deployment: Docker 19.03.13
* Python dependencies:
  * Django 3.1.1
  * mysqlclient 1.4.0
  * matplotlib 3.3.1
  * pandas 1.1.1
  * drf-yasg 1.17.1

## Getting Started
### Deploy our service
Before you start, make sure `git`, `docker` and `docker-compose` are installed on the server.(If you need help with this, instructions can be found in our [deployment guide](https://github.com/MEICHENLIN/Automated-Audit-Benchmarking/blob/main/Doc/AA-Koala%20Deployment%20Guide.pdf).

**1. Pull code from our github repo**

   ```shell 
   git clone https://github.com/MEICHENLIN/arpansa-audit-automation.git
   ```

(Alternatively, you can upload the code in server directory onto the server)

**2. Deploy**

   ```shell
   cd Server
   sudo docker-compose up -d
   ```
### Use local program
Once deployment completes, you can use local program to run our predefined audit process.
Here takes inserting result as an example.
1. Open `uploadData.xlsx` and fill in the data you want to insert into database

2. Open the `Demo.py` and call `insertResult()`
```python
from LocalProgram.resultRequest import *
resultRequest.insertNewResult()
```
3. If it returns a json in the console, meaning it has succesfully inserted the result

4. You can check the inserted result by calling `listResults()`
```python
from LocalProgram.resultRequest import *
resultRequest.listResults()
```
5. Go to download folder, open the downloaded Excel, all the data in database are now downloaded in this file.

## List of files
```
├── Doc
├── LocalProgram
│   ├── Demo.py
│   ├── config.py
│   ├── graphRequest.py
│   ├── resultRequest.py
│   ├── tests
│   └── upload
└── Server
    ├── AAB
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── apps
    │   └── graphs
    │       ├── Services
    │       │   └── graphService.py
    │       ├── admin.py
    │       ├── apps.py
    │       ├── migrations
    │       ├── models.py
    │       ├── serializers.py
    │       ├── tests
    │       │   ├── test_urls.py
    │       │   └── test_views.py
    │       ├── urls.py
    │       └── views.py
    ├── utils
        ├── images
        ├── plGraphs  
        ├── plot.py
        └── sample.py
```