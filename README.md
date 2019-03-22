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
RIGHTS GRANTE   : INSERT, SELECT, UPDATE
TABLE(S)        : customers
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
The first role is for accessing the master and modify the customer table, to actually verify that the changes made to the master are reflected on the slave.<br>
The second role is for connecting your own slave meant to replicate changes made to the master.

*Please note:<br>Since multiple people will be granted access to modify the data contained in the customer table I can not vouch for whatever data might be inthere when you read from it*

------------------------------------------------------------------------
# Connection established / slave status
Below are screenshots to document the slave is indeed up and running - and that the master and slave are in-sync (indicated by the position number being the same on both the databases) 

------------------------------------------------------------------------
# Replication delay
Below is a screenshot to document the replication delay between the master(Singapore) and the slave(Frankfurt)
