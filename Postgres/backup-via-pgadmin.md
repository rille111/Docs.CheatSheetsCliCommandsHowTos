# Making Backups of PostgreSQL

## PreReqs

* Download pgAdmin
* Get Kubectl (through gcloud cli?) and connect to our projects


### Connect & Add our database to pgAdmin

* Go to folder `kubernetes-postgres`
* Run `.\open-tunnel-to-sql.ps1` and wait
* Open pgAdmin (use your master password (your own)
* Rightclick Servers and Create, name it whatever and use host: localhost or 127.0.0.1 
	* The password is in the readme of `kubernetes-postgres` folder


## Take backup

* Right click the database `cmsdata` and click Backup (you can also backup nested stuff but that wont cover the entire db)
	* Filename format: cmsdata-backup-2019-08-29.tar
	* Format: TAR
	* Encoding: UTF8
	* Role name: postgres  (or whatever is admin/root)
* Dump Options:
	* Click Data, Pre-data, Post-data = Yes
* Click Backup!
* Ensure size is reasonable (5+mb)

## Make a restore (test)

* Create a new database
* Rightclick that database and hit Restore
* Browse to the file and choose `postgres` as Role name
* Restore options:
	* Pre, Post and Data = Yes
* Hit restore and make sure data is there
* Profit!

## Put backup to Google Storage

* Login in to https://console.cloud.google.com/
* Switch user to your Kumobits account
* Change project to `Customers-Aften`
* Click menu and click Storage
* Click `aftenbil-files-and-backups`
* Click folder `sql-backups`
* Drag & drop the backup file, observe the file size

