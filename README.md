# Assignment8Database
This is the 8th assignment for PBA Database soft2019spring

-------------------------------------------------------------------------------------------------

# What it is
This is a how-to guide that let's you setup your own MySql-slave and connect it to a MySql-master. I wasn't really sure how to go about documenting the replication and the update time, so I decided using screenshots.

---------------------------------------------------------------------------------------------------
# What you need
All the information you need to create your slave can be found in the *setup_info.txt* file.
The file conntains information reguarding 2 user roles:<br>
````
------------------------------------------------------------------
This account is used for logging into the MySql-master
------------------------------------------------------------------
MASTER-IPADR    : *****
USER-LOGIN      : *****
USER-PASSWORD   : *****
RIGHTS GRANTED  : SUPER, RELOAD, LOCK, INSERT, SELECT, UPDATE
TABLE(S)        : all tables (customers, employees - for modification and reads)
------------------------------------------------------------------

This account is used for creating your own slave
------------------------------------------------------------------
MASTER-IPADR    : *****
USER-LOGIN      : *****
USER-PASSWORD   : *****
RIGHTS GRANTED  : REPLICATION SLAVE
TABLE(S)        : all tables
------------------------------------------------------------------
````
The first role is for accessing the master and modify the *customer* and/or *employees* table, to actually verify that the changes made to the master are reflected on the slave.<br>
The second role is for connecting your own slave meant to replicate changes made to the master.
<br>
<br>
<b>Privileges:</b><br>
SUPER : to show the master status to make a note of the position, this is needed when creating the slave<br>
RELOAD : to flush and lock the tables before dumping data<br>
LOCK : needed to execute the mysqldump command<br>
INSERT, UPDATE, SELECT : to modify data as needed.<br>
REPLICATION SLAVE : needed to connect a slave to the master for replication<br>
<br>

*Please note:<br>Since multiple people will be granted access to modify the data contained in the customer table I can not vouch for whatever data might be inthere when you read from it*

<b>Important - when setting up your own slave, please be aware that I have already used *SERVER-ID : 1* and *SERVER-ID : 2* for the master and my own slave - so you have to assign a different id to your slave, also - the reviewer before you might have used ID : 3 </b>

# step-by-step
For at step-by-step guide on how to master-slave replication please follow the guide from the assignment text.

------------------------------------------------------------------------
# Connection established / slave status
Below are screenshots to document the slave is indeed up and running - and that the master and slave are in-sync (indicated by the position number being the same on both the databases) 

![connection](https://github.com/cph-js284/Assignment8Database/blob/master/images/slave_status.png)
<br>
*The green arrows in the top of the image indicates the slave is up and running and waiting to receive event from the master - The green arrow in the bottom of the image indicates no I/O-errors*<br>
*The blue arrows are pointing to the position the slave is reading from the log both of these positions are identical with the position of the master (screenshot below) meaning they are in-sync*<br>
<br>
![masterstatus](https://github.com/cph-js284/Assignment8Database/blob/master/images/master_status.png)

------------------------------------------------------------------------
# Replication delay
Below is a screenshot to document the replication delay between the master(Singapore) and the slave(Frankfurt)
![replication_delay](https://github.com/cph-js284/Assignment8Database/blob/master/images/replicationdelay.png)
<br>
*The arrow point to the number of seconds delay between the master and slave. A ping test between between the master and Copenhagen results in roughly 400ms delay, which would indeed be rounded down to 0 secs.*
