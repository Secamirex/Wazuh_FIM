# SOC XDR/SIEM - File Integrity monitoring with Wazuh
File Integrity Monitoring (FIM) on Wazuh is a security process used to monitor the integrity of system and application files. FIM is an important security defence layer for any organisation monitoring sensitive assets. It provides protection for sensitive data, application, and device files by monitoring, routinely scanning, and verifying their integrity.

<h2>ENABLING MONITORING ON 'PUBLIC DIRECTORIES' of WINDOWS client</h2>

1. Download the Wazuh agent and install it on a Windows client machine. Ensure the client's PC is registered with Wazuh.
![image](https://github.com/user-attachments/assets/2c4fcd45-1fa7-4be4-b6ad-b46c63878b8d)

2. Next we need to secure  the most frequently used directory by the attackers  
	
 * 'Public directory'  under  C:\ Users

3. Next we need to include the public  directories to the FIM (File Integrity Monitoring) so that they can be monitored.  
	
The Wazuh agent config file is located under  C:\Program Files (x86)\ossec-agent\ossec.conf

4. Open up the ossec.conf file with a text editor
5. Navigate to " file integrity monitoring' section 
6. Add the following line to the config file

Note: recursion_level instructs Wazuh to inspect an monitor sub folders . By default it is set to 0  ( no sub folder monitoring) 

7. To monitor the entire directory ,  recursion_level can be removed . 
![image](https://github.com/user-attachments/assets/fdd927a6-c75c-47c1-921b-42c8afa0dd16)

8. Restart Wazuh agent from Services 

<h2>TESTING THE NEW FIM RULE</h2>

1. Create a new text file under Public > Public Documents 

![image](https://github.com/user-attachments/assets/2780063d-5cf0-4174-a664-0be569065fa8)

2. Navigate back to <strong> Wazuh FIM  > Events</strong> 
3. A new event has been lodged for  the new file creation.  Document details also shows useful info such as file hashes that can be used to further analyse the file on TI platform like VirusTotal. 
![image](https://github.com/user-attachments/assets/7ba9f5c7-f148-44a3-a3df-8aa9827b5749)

![image](https://github.com/user-attachments/assets/f2be9298-b344-425f-b2d0-a68edb533af0)

4. This rule can be used for sensitive files and for the registry  "HKEY_LOCAL_MACHINE" RUN keys listed below  as they can be hijacked by attackers  to setup persistent backdoors.

![image](https://github.com/user-attachments/assets/71e66d2d-3617-41bb-aff3-3c7b7cfaf514)



<h2>Adding WHO-DATA Monitoring Feature to OSSCEC config </h2>

This  FIM capability reports the specific changes made to the file and shows the state before and after the change

* The keyword to enable change reporting is report_changes="yes"
* Restart the Wazuh server

![image](https://github.com/user-attachments/assets/d3d317bf-ff44-4ec1-a5c4-1873cef100ca)

* Once enabled, it adds an additional " Syscheck.diff" field to the process detailed report  in which it shows the original value as well as the new modified value.
* <strong> As shown below, the " studens_grade.txt" document has been modified and the change is captured and reflected under the systemcheck.diff as expected.</strong>

![image](https://github.com/user-attachments/assets/689f292a-72be-4622-a411-0fab364d9b92)


