# Qlik Sense QVD Builder Script

A simple script to easily build QVDs that are to be used in Qlik Sense Applications.

The script/process can be used on the Desktop/Server versions

The script is configured by an Excel file where you can add details of the QVD file that you wish to build, there is one row per QVD/QVS.

This script has been ported from Qlikview and has been modified with use of the LIB statement, so your able to use and modify for use in Qlikview.

## Folder structure

There are three main folders and the purpose of each is as follows:

#### qvds

This is the folder that the script stores all of your QVDs.

#### qvd-scripts

Contains the QVS script and the required **_loader.xlsx** file.

Place all your QVS files into this folder.

All QVS files must be saved with a QVS file extension.

#### config

Contains the config.qvs, this config file is ready for adding environment variables, not had enough time to play with for Sense, but Qlikview works well with this setup.

By having one config file for each of the following environments it makes it easy to connect t o different data sources without having the hassle of changing/switching them each time you move your apps to different servers.

+ Development
+ UAT Test
+ Production/Live

## XLS Config File (_loader.xlsx)

### Column names
+ **_scriptname:** name of the QVS file without the extension
+ **_qvdname:** the name of the QVD file that the script saves
+ **_active:** load script toggle, 0 script will skip QVS file, 1 script will process QVS file
+ **_alias:** not use at the moment, I might implement for Qualify table naming for reusing script.
+ **_incremental:** not used, intended to be used in QVS if different conditions, you can use if you want.
+ **_test:** used as a visual aid mainly, to show if script has passed, to assit other devs
+ **dependant on:** used as a visual aid to show if a script is dependant on another QVD/QVS, and to help in the ordering that the scripts get processed

## QVS Files

+ Each QVD LOAD script should be placed into it own QVS file
+ The files should be suffixed with the .qvs extension and saved into the qvd-scripts folder.
+ The LOAD table that you wish the script to store should be called **data:**, every QVS file should have a data: table to store into a QVD, as the script will not save the QVD.

## QVF Application File

You will need to create/modify the following data connections with the correct Alias names:

+ **QVDs**: Folder data connection that points to the **qvds** folder for your Sense application
+ **QVSs**: Folder data connection that points to the **qvd--scripts** folder for your Sense application
+ **YOUR_DB_NAME**: DODBC/OLE DB connection, the alias is not that important, but you will reference in your QVS file **LIB CONNECT TO 'YOUR_DB_NAME';**
+ **CONFIG**: Folder data connection that points to the **config** folder for your Sense application, not required but will be in the future


