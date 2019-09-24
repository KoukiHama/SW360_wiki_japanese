The following scenario:

There is an existing machine with sw360 installed. However, the machine requires a new installation from scratch. The contents of the server A should be moved to a new server B. This article will explain what to do.

### Getting Data from Server A

There are several section to preserve as **special** data and configuration.

#### User Setup

The users can be exported from the current instance using the CSV download from the users pages in the sw360 admin menue. The reason why an export of the users is required is the password: If a user has changed the password, the changed password is unknown and cannot be set to a default value again (would be confusing to the user). 

With the CSV export the password that users have set for themselves is exported as hash value. Thus the passwords of the users are preserved for the import to a new server.

#### Configuration files

The main services that require special configuration file handling are:

* **sw360-portlets**: There is the sw360properties and some configuration files. usually, ```sw360.properties``` is the most likely changed file (for setting the clearing organizations for example), but it depends what you have set in the files. You will find the configuration files here:
```
/opt/apache-tomcat-.../webapp/sw360-portlet/WEB-INF/classes
```
* **fossology service**: there is the configuration where the fossology server is in the file ```fossology.properties``` and the keys for logging in (public / private key). Location is:
```
/opt/apache-tomcat-.../webapp/fossology/WEB-INF/classes
```
* **moderation service**: There is configuration for the e-mail sending for example, most likely in sw360.properties. Check for yourself if you have changed the other files.

There are configuration files in all services, please check if you have more files to preserve for migration. Usually these are set at deployment of the vagrant in an uniform manner, so no special handling would be required in normally.

As a step you could copy these to some preserving location.

#### Database: The real data: components, projects, etc.

Th real data should be migrated too. Originally, this part should ave been covered by the CSV Import / Export in the Admin menu of the sw360 (not the liferay admin menue). However, in version 1.2 and 1.3 of sw360, the changes to the data model were considerable intensive that adjustments of the CSV import export have been suspended. In other words, not everything in your database gets exported properly and therefore the subsequent import would be incomplete.

Luckily, the coucdbdb files can be copied, so far without hazzle. In order to copy the couchdb files, consider the following steps:

1. Stop the sw360 application (shutdown tomcat).
2. Shutdown couchdb
3. Change to root.
4. Copy the following couchdb files out of the machine from ```/var/lib/couchdb```:
```
sw360attachments.couch
sw360db.couch
sw360fossologykeys.couch
```
The file ```sw360users``` is already by the CSV export (see above).
5. Restart the machine if you prefer.

### Setting data on Server B

For the new server, the service should be shut down for moving the files in: the tomcat and the couchdb in this order actually.

Then, copy the files to the same location where they were copied from.

#### Copying the couchdb files back

The couchdb files should be copied back to the machine. Since the couchdb user is not (should not) be enabled for login, you will likely need to copy this first to your user location, then log in and move the files to the actualy target location of the couchdb server using root.

* make sure couchdb is not running.
* Copy the database files into the ```/var/lib/couchdb```. If you prefer you could have the original (empty database files preserved). Most likely you will use:
```
$ mv /home/siemagrant/sw360attachemnts.couch /var/lib/couchdb
...
```
* Adjust the rights and the ownership and the group on the couchdb files (the same as the other *.couch files). Most likely you will need:
```
$ chown couchdb:couchdb sw360attachemnts.couch
...
```
* bascically it is about to have this like the other files that are there (for example ```sw360users.couch```)
* start couch db again

#### Copying the config files back

As mentioned about the referring files need to be copied into the service locations at deployment (note: fully aware of that this configuration handling is odd or classic to be euphemistic. Maybe we will make a config service at some time).

1. **sw360-portlet**: the file location on the server is here:
```
/opt/apache-tomcat-.../webapp/sw360-portlet/WEB-INF/classes
```
2. **fossology service**: also the location is likely here:
```
/opt/apache-tomcat-.../webapp/fossology/WEB-INF/classes
```

#### Reimport the Users CSV

Using the setup-admin login you can import the users.csv export from server A. It should contain also all rights settings as well as the password hashes of the individual user passwords