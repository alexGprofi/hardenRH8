# Hardening RedHat 8


## Choose the partition scheme during installation

Recommended partition scheme (can be change to fit your needs)

/			          	-  20 GB
/boot  		    	-  	1GB
/var   		     	-  20 GB
/var/log 	    	 -   5 GB
/var/tmp 	   	 -   5 GB
/var/log/audit 	-   5 GB
/home 		 		- 10 GB
/tmp 		 			- 10 GB
swap		 			 - 4 GB
/opt		  			- 10 GB  (Optional, if required)


Go to **SYSTEM** > Installation Destination

<img src="C:\Users\agomez\Pictures\Hardening\Change Partitions.png" alt="Change Partitions" style="zoom:75%;" />

Then choose **Customer** and then click on **Done**

<img src="C:\Users\agomez\Pictures\Hardening\Change Partitions_8.png" alt="Change Partitions_8" style="zoom:75%;" />

The partitions should look like these:

![Change Partitions_6](C:\Users\agomez\Pictures\Hardening\Change Partitions_6.png)

![Change Partitions_7](C:\Users\agomez\Pictures\Hardening\Change Partitions_7.png)

You can choose the size of the partitions to fit the needs of your deployment.

After choosing your partition, click on **Done**

## Choose the policy during installation

Go to **SYSTEM** > Security Policy

<img src="C:\Users\agomez\Pictures\Hardening\Sec_Options_3.png" alt="Sec_Options_3" style="zoom:75%;" />

Now choose 

1. Protection Profile for General Purpose Operatins Systems
2. Click to enable
3. Click on **Select Profile**

<img src="C:\Users\agomez\Pictures\Hardening\Sec_Options_4.png" alt="Sec_Options_4" style="zoom:75%;" />

No errors should appear in the dialog message, only info messages.

<img src="C:\Users\agomez\Pictures\Hardening\Sec_Options_5.png" alt="Sec_Options_5" style="zoom:75%;" />

If looks like the above image, then click on **Done**

Then you can continue with **Begin Installation**.

<img src="C:\Users\agomez\Pictures\Hardening\Sec_Options_7.png" alt="Sec_Options_7" style="zoom:75%;" />

## Partition information

After reboot check the partition information 

> lsblk

![lsblk](C:\Users\agomez\Pictures\Hardening\lsblk.png)



> df -Th

![df_Th](C:\Users\agomez\Pictures\Hardening\df_Th.png)




## Test the hardening


Now you can test the hardening, the following will create a `report.hmtl` file

> oscap xccdf eval  --fetch-remote-resources --profile xccdf_org.ssgproject.content_profile_ospp  --results-arf arf.xml  --report report.html  /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml

Now, check the **report.html** file

If you see any error in the report you can go and see the information related to the error or you can remediate adding the option to the command.

> oscap xccdf eval  --fetch-remote-resources --remediate --profile xccdf_org.ssgproject.content_profile_ospp  --results-arf arf.xml  --report report_fixed.html  /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml


Now, check the **report_fixed.html** file

If there is still an error after remediation, check more info of the error and review if the error, may require a reboot to be cleared.

## Steps before cloning

Despite is not required to subscribe the machine before harden. 

Unregister before cloning the machine

> subscription-manager unregister

Then run the cleanup.sh script to prepare the VM for exporting

> ./cleanup.sh


## Reference

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/security_hardening/index

https://access.redhat.com/solutions/198693
