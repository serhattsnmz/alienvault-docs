## Microsoft Windows Event Logs through NXLog

### Integrating NXLog

Before you configure the NXLog integration, you must have the IP Address of the USM Appliance Sensor. In addition, you need to download the required files documented below. The functionality covered in this section has been tested on Windows Server 2008R2 and Windows Server 2012R2.

#### Required Files on the Windows Machine

You need to download the following files and place them in C:\Program Files (x86)\nxlog\conf on your Windows machine.

- patterndb.xml
    - The patterndb.xml file defines which events are collected and sent to USM Appliance. Any Windows Event IDs not present in this file are not forwarded, excluding events not relevant to security and improving the overall performance of the plugin.
- nxlog.conf
    - The nxlog.conf file contains general NXLog configurations as well as settings that are specific to USM Appliance:
        - `<Input in_nxlog_internal>` — specifies to send a warning message when an event storm occurs.
        - An event storm is a massive event generation in a short period of time. This might cause bandwidth issues on the network and/or performance issues on the Windows server.
        - `<Extension transform_alienvault_csv>` — specifies that the Windows events forwarded to USM Appliance appear as strings in double quotes separated by a semicolon. For example,
        - `"<event_time>";"<event_type>";"<severity>";"<channel>";"<hostname>";<event_id>;"<source_name>";"<account_name>";"<account_type>";"<domain>";"<raw_message_without_linefeeds>"`
        - `<Output out_alienvault_csv>` — specifies some unique handing of Windows events to improve the efficiency of the nxlog plugin. These include:
            - Windows Event ID not existing in the patterndb.xml file are not forwarded to USM Appliance.
            - Events are dropped when the events per second (EPS) rate reaches 200.
            > Note: See Disabling Event Storm Execution if you want to keep the events instead.
            - Any special characters such as \t, \n, and \r are replaced by a blank space.
            - If any of the <account_name>, <account_type>, or <domain> fields are empty, they will be replaced by a hyphen ("-").

#### Disabling Event Storm Execution

An event storm is a massive event generation in a short period of time. This might cause bandwidth issues on your network and/or performance issues on the Windows servers. Therefore, in the nxlog.conf file, USM Appliance configures NXLog to drop Windows events when the events per second (EPS) is 200 or higher. It will resume forwarding events as soon as the EPS returns to below 200.

If you want NXLog to forward all events, you can disable the event storm handling by editing the nxlog.conf file and commenting out the following section with #.

```
Exec    \	

    {\

	if not defined get_var('rate') { create_var('rate'); set_var('rate',1); }\
	 if not defined get_var('stormed'){ create_var('stormed',2); set_var('stormed',0); 

            set_var('rate',1); }\    

	set_var('rate',get_var('rate')+1);\
	 if not defined get_var('sec')\

	{\
	    create_var('sec',1);\

	   set_var('sec',1);\
	    if get_var('rate') >= 200 { delete_var('stormed'); create_var('stormed',2); 

               set_var('stormed',1); set_var('rate',1); drop(); } 

           else { set_var('stormed',0); set_var('rate',1); }\


	 }\
	 else if get_var('stormed') == 1\

	{\

           drop();\
	 }\
	 if get_var('rate') >= 200\
	 {\

	   if not defined get_var('warning')\
	 {\

	   log_warning("Eventstorm detected.");\
	    create_var('warning',60);\
	    set_var('warning',1);\
	 }\

	   drop();\
	 }\

    }
```

### Configure NXLog on Windows

#### To send log data through NXLog to USM Appliance

1. If not done already, download patterndb.xml and nxlog.conf, and then place in C:\Program Files (x86)\nxlog\conf on your Windows machine.

> Note: This step overwrites the default nxlog.conf file. You may want to back up the original copy before placing the one provided by AlienVault.

2. Open the nxlog.conf file in a text editor, and locate the following line:
    - `define OUTPUT_DESTINATION_ADDRESS <USM-Appliance-Sensor-IP>`
3. Replace `<USM-Appliance-Sensor-IP>` with the IP address of the USM Appliance All-in-One or USM Appliance Sensor that will receive the Windows events.
4. Uncomment the section between NXLOG and /NXLOG.

> Important: Only remove the first # symbol in each line when uncommenting the sections. The remaining # symbol indicates that the line is either a comment or optional.

5. Save the file.
6. Start or restart the NXLog service.