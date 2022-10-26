### Delete Files older Than 30 Days
Using the find command, you can search for and delete all files that have been modified more than X days. Also, if required you can delete them with a single command.

First of all, list all files older than 30 days under /opt/backup directory.
```
find /opt/backup -type f -mtime +30 
```
Verify the file list and make sure no useful file is listed in the above command. Once confirmed, you are good to go to delete those files with the following command.
```
find /opt/backup -type f -mtime +30 -delete 
```
### Delete Files with Specific Extension
You can also specify more filters to locate commands rather than deleting all files. For example, you can only delete files with the “.log” extension and modified before 30 days.

For the safe side, first, do a dry run and list files matching the criteria.
```
find /var/log -name "*.log" -type f -mtime +30 
```
Once the list is verified, delete those files by running the following command:
```
find /var/log -name "*.log" -type f -mtime +30 -delete 
```
The above command will delete only files with a .log extension and with the last modification date older than 30 days.

### Delete Old Directory Recursively
The `-delete` option may fail if the directory is not empty. In that case, we will use the Linux rm command with find to accomplish the deletion.

Searching all the directories under /var/log modified before 90 days using the command below.
```
find /var/log -type d -mtime +90 
```
Here we can execute the rm command using -exec command line option. Find command output will be sent to rm command as input.
```
find /var/log -type d -mtime +30 -exec rm -rf {} \; 
```
