# Full Stack Web Developer Nanodegree program
#Project: Logs Analysis

#Log Analysis
Project One full stack web development nanodegree program.

## Project Overview
The project requires students to create and use SQL queries that would fetch results from a large database of a news website.The objective of this project is to extend the student's SQL database skills. The code requirements suggest the use of only one single query to answer each request. The answer code presented here does not change the original database but utilizes views to answer the third query.

#Requirements
Python 3 - The code uses ver 3.6.4
Vagrant - A virtual environment builder and manager
VirtualBox - An open source virtualiztion product.
The PEP8 style guide

## How to access the project?
## Install VirtualBox

VirtualBox is the software that actually runs the virtual machine. [You can download it from virtualbox.org, here.](https://www.virtualbox.org/wiki/Download_Old_Builds_5_1) Install the _platform package_ for your operating system. You do not need the extension pack or the SDK. You do not need to launch VirtualBox after installing it; Vagrant will do that.

Currently (October 2017), the supported version of VirtualBox to install is version 5.1. Newer versions do not work with the current release of Vagrant.

**Ubuntu users:** If you are running Ubuntu 14.04, install VirtualBox using the Ubuntu Software Center instead. Due to a reported bug, installing VirtualBox from the site may uninstall other software you need.

### Install Vagrant

Vagrant is the software that configures the VM and lets you share files between your host computer and the VM's filesystem. [Download it from vagrantup.com.](https://www.vagrantup.com/downloads.html) Install the version for your operating system.

**Windows users:** The Installer may ask you to grant network permissions to Vagrant or make a firewall exception. Be sure to allow this.

![vagrant --version](https://d17h27t6h515a5.cloudfront.net/topher/2016/December/584881ee_screen-shot-2016-12-07-at-13.40.43/screen-shot-2016-12-07-at-13.40.43.png)

_If Vagrant is successfully installed, you will be able to run_ `vagrant --version`
_in your terminal to see the version number._
_The shell prompt in your terminal may differ. Here, the_ `$` _sign is the shell prompt._

### Download the VM configuration

Use Github to fork and clone, or download, the repository [https://github.com/udacity/fullstack-nanodegree-vm](https://github.com/udacity/fullstack-nanodegree-vm).

You will end up with a new directory containing the VM files. Change to this directory in your terminal with `cd`. Inside, you will find another directory called **vagrant**. Change directory to the **vagrant** directory:

![vagrant-directory](https://d17h27t6h515a5.cloudfront.net/topher/2016/December/58487f12_screen-shot-2016-12-07-at-13.28.31/screen-shot-2016-12-07-at-13.28.31.png)

_Navigating to the FSND-Virtual-Machine directory and listing the files in it._
_This picture was taken on a Mac, but the commands will look the same on Git Bash on Windows._

## Instructions

### Start the virtual machine

From your terminal, inside the **vagrant** subdirectory, run the command `vagrant up`. This will cause Vagrant to download the Linux operating system and install it. This may take quite a while (many minutes) depending on how fast your Internet connection is.

![vagrant-up-start](https://d17h27t6h515a5.cloudfront.net/topher/2016/December/58488603_screen-shot-2016-12-07-at-13.57.50/screen-shot-2016-12-07-at-13.57.50.png)

_Starting the Ubuntu Linux installation with `vagrant up`._
_This screenshot shows just the beginning of many, many pages of output in a lot of colors._

When `vagrant up` is finished running, you will get your shell prompt back. At this point, you can run `vagrant ssh` to log in to your newly installed Linux VM!

![linux-vm-login](https://d17h27t6h515a5.cloudfront.net/topher/2016/December/58488962_screen-shot-2016-12-07-at-14.12.29/screen-shot-2016-12-07-at-14.12.29.png)

_Logging into the Linux VM with `vagrant ssh`._


## cd /vagrant

Here cd into the /vagrant folder.
Unpack the database folder contents downloaded above over here. You can also copy the contents of this repository here.
To load the database type 
psql -d news -f newsdata.sql

To run the database type 
psql -d news

and explore the tables using the \dt and \d table commands and select statements.

\dt — display tables — lists the tables that are available in the database.
\d table — (replace table with the name of a table) — shows the database schema for that particular table.
Get a sense for what sort of information is in each column of these tables.

## Connecting from your code
The database that you're working with in this project is running PostgreSQL, like the forum database that you worked with in the course. So in your code, you'll want to use the psycopg2 Python module to connect to it, for instance:

db = psycopg2.connect("dbname=news")

## Create File.py
Import psycopg2
DBNAME="news"
and write the back end code.
Connect to the databse
Create a fonction
print the fonction.


#Run Python Programe To fretch QUERY Result.
You must run the commands from the Create views section here to run the python program successfully.
Use command python file.py to run the python program that fetches query results.

## Create Views
Views were created to answer the third query in the project in purpose to leave the original database unchanged. 
They break the question down into comprehensible portions.

## 1st view code:
CREATE VIEW logstar AS
SELECT count(*) as stat, 
status, cast(time as date) as day
FROM log WHERE status like '%404%'
GROUP BY status, day
ORDER BY stat desc limit 3;

## 2sd view code:
CREATE VIEW totalvisitors AS
SELECT count(*) as visitors,
cast(time as date) as errortime
FROM log
GROUP BY errortime;

## 3rd The third and last view code is as follows:
CREATE VIEW errorcount AS
SELECT * from logstar join totalvisitors
ON logstar.day = totalvisitors.errortime;

## OUTPUT RESULT
Use the code: - python file.py > output.txt
in your VM to automatically transfer the output in your output.txt file.

## Troubleshooting
If your command prompt does not start with vagrant after typing vagrant ssh then please try an older version
Udacity mentors have noticed that some newer versions of Vagrant don't work on all operating systems. Version 1.9.2 is reported to be stabler on some systems, and version 1.9.1 is the supported version on Ubuntu 17.04. You can download older versions of Vagrant from [the Vagrant releases index](https://releases.hashicorp.com/vagrant/).
