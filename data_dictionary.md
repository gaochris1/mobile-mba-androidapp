### Mobile Performance Data Dictionary

Measurement

  * **Tests**

    * JHTTPGETMT
    * JHTTPPOSTMT
    * JUDPLATENCY
    * CLOSESTTARGET

  * **Metrics**

    * phone_identity
    * network_data
    * gsm_cell_location
    * cdma_cell_location
    * cell_neighbour_tower_data
    * location

  * **Conditions**

    * PARAM_EXPIRED
    * NETACTIVITY
    * CPUACTIVITY

Jump to example result.

The FCC Measuring Broadband America (MBA) Program's Mobile Measurement Effort
developed in cooperation with SamKnows Ltd. and diverse stakeholders employs a
client-server based anonymized data collection approach to gather broadband
performance data in an open and transparent manner with the highest commitment
to protecting participants privacy. All data collected is thoroughly analyzed
and processed prior to public release to ensure that subscribers’ privacy
interests are protected.

Data related to the radio characteristics of the handset, information about
the handset type and operating system (OS) version, the GPS coordinates
available from the handset at the time each test is run, the date and time of
the observation, and the results of active test results are recorded on the
handset in JSON(JavaScript Object Notation) nested data elements within flat
files. These JSON files are then transmitted to storage servers at periodic
intervals after the completion of active test measurements. This document
describes the JSON schema nested format of the radio, handset, active test
result and other data recorded on the handset prior to transmission to the
storage infrastructure.

Jump to example result.

### Measurement Reference

|Property |Type |Description |Explanation|
|---------|-----|------------|-----------|
|_received|Integer|unix_timestamp of reception|The timestamp recoded at server side at the moment the result file is being received.|
|_sourceip|String|source ip address|The Internet Protocol (IP) address of the handset submitting the results to the collecting infrastructure as seen by the collecting infrastructure.|
|enterprise_id|String|FCC_Public|The code for different panel programs.|
|sim_operator_code|String|android.telephony.TelephonyManager  .getSimOperator()|The field holds string from the Android method that identifies the MCC+MNC(mobile country code + mobile network code) of the provider of the SIM.|
|submission_type|String|[scheduled_tests|init_tests|manual_tests]|The application logic will select one of three possible string definitions.  Data results may be recorded from handsets downloading configuration files for test schedules from SamKnows scheduling servers; performing scheduled tests parsed from configuration files residing on the handset; or from a handset user initiating a manual test. Each category of initiating test are documented in this field.|
|app_version_code|String|version code from androidmanifest.xml|The field contains the current compiled application version number parsed from the application configuration file, androidmanifest.xml. The version number confirms to a major.minor build revision practice, e.g. V 1.23 major version revision one, minor version revision 23.|
|app_version_name|String|version name from androidmanifest.xml|The field contains the current compiled application version parsed from the application configuration file, androidmanifest.xml. The name may vary depending on the target user base, e.g. wireless carrier enterprise build.|
|schedule_config_version|String|config file version|This field contains the configuration file version currently in use. The application downloads this file periodically and modifies its tests parameters accordingly.|
|timestamp|Integer|1359128122|The unix timestamp of the handset performing the measurement at the beginning of the observations.|
|datetime|String|Fri Jan 25 15:35:22 EST 2013|The unix time and date of the handset performing the measurement at the beginning of the observations.|
|timezone|Integer|-5|An integer denoting the number of hours offset from GMT time of the handset performing the measurement at the beginning of the observations.|
|tests|JSON Array|Results for JHTTPGETMT, JHTTPPOSTMT, JUDPLATENCY,CLOSESTTARGET|(See below for details of array.)  There are 3 entries in this array, one for each result type.|
|metrics|JSON Array|Results for phone_identity, network_data, [gsm_cell_location OR cdma_cell_location], cell_neighbour_tower_data, location|(See below for details of array.)  There are 6 entries in this array, one for each result type.|
|conditions|JSON Array|Results for PARAM_EXPIRED, NETACTIVITY, CPUACTIVITY|(See below for details of array.)  There are 3 entries in this array, one for each result type.|

### JHTTPGETMT Reference

|Property| Type| Description| Explanation|
|--------|-----|------------|------------|
|type|String|JHTTPGETMT|The active metric type 'JHTTPGETMT' describes measurement results of the active test for download performance.|
|bytes_sec |Integer|154716|The field represents the throughput experienced during the transfer period of the test, the value is obtained dividing the total amount of bytes transferred during the “transfer_period” by the time they have been transferred. This represents hence the download speed.|
|datetime|String (Android dtime format)|Fri Jan 25 15:35:22 GMT 2013|The field represents the time the test finished in UTC represented as a Android dtime datatype.|number_of_threads|Integer|3The number of concurrent TCP connections used in the test.|
|success|Boolean|true|The field represents the success or failure of the measurement. True denotes a successful execution of the entire test.|
|target|String|n1-the1.samknows.com|The field holds a string of the measurement server target hostname or IP address. The value is pulled from the test configuration file. The test configuration file, or schedule_config file is donwloaded periodically by the application and its content specifies the parameters used for configuring the tests. An example of the file is schedule_example.xml locatetd in AndroidAppLibrary/res/raw|
|target_ipaddress|String|46.17.56.234|The field holds a four tuple colon deliminated IP address of the 'target' measurement server, as resolved by the handset's locally configured DNS for the active network used to execute the test. |
|timestamp|Integer|1359128122|The field contains the time the measurement concluded represented as a sql TIMESTAMP datatype. http://developer.android.com/reference/java/sql/Timestamp.html|
|transfer_bytes|Integer|1783936|The field contains the total bytes downloaded across all connections during the execution of the measurement.|
|transfer_time|Integer|11530334|The field contains the time the test ran for in microseconds.|
|warmup_bytes|Integer|145024|The field contains the Bytes transferred for all the TCP streams during the warm-up phase.|
|warmup_time|Integer|1309661|The field contains the time consumed for all the TCP streams to arrive at|optimal window size (Units: microseconds).|

### JHTTPPOSTMT Reference

|Property|Type|Description|Explanation|
|--------|----|-----------|-----------|
|type|String|JHTTPPOSTMT|The active metric type 'JHTTPPOSTMT' describes measurement results of the active test for upload performance. |
|bytes_sec|Integer|167995|The field represents the throughput experienced during the transfer period of|the test, the value is obtained dividing the total amount of bytes transferred during the “transfer_period” by the time they have been transferred. This represents hence the download speed.|
|datetime|String|Fri Jan 25 15:35:36 GMT 2013|The field represents the time the test finished in UTC represented as a Android dtime datatype.|
|number_of_threads|Integer|3|The number of concurrent TCP connections used in the test.|
|success|Boolean|true|The field represents the success or failure of the measurement. True denotes a successful execution of the entire test.|
|target|String|n1-the1.samknows.com|The field holds a string of the measurement server target hostname or IP address. The value is pulled from the test configuration file. The test configuration file, or schedule_config file is donwloaded periodically by the application and its content specifies the parameters used for configuring the tests. An example of the file is schedule_example.xml locatetd in AndroidAppLibrary/res/raw|
|target_ipaddress|String|46.17.56.234|The field holds a four tuple colon deliminated IP address of the 'target' measurement server, as resolved by the handset's locally configured DNS for the active network used to execute the test.|
|timestamp|Integer|1359128136|The field contains the time the measurement concluded represented as a sql TIMESTAMP datatype.|http://developer.android.com/reference/java/sql/Timestamp.html|
|transfer_bytes|Integer|1944064|The field contains the total bytes uploaded across all connections during the execution of the measurement.|
|transfer_time|Integer||11572113|The field contains the time the test ran for in microseconds.|
|warmup_bytes|Integer|114176|The field contains the Bytes transferred for all the TCP streams during the warm-up phase.|
|warmup_time|Integer|1496460|The field contains the time consumed for all the TCP streams to arrive at optimal window size (Units: microseconds).|

### JUDPLATENCY Reference

|Property| Type| Description| Explanation|
|type|String|JUDPLATENCY|The active metric type 'JUDPLATENCY' describes measurement results of the|active test for latency performance.|
|datetime|String|Fri Jan 25 15:36:07 GMT 2013|The field contains the time test finished in UTC.|
|lost_packets|Integer|1|The field contains the number of lost packets during the test|
|rtt_avg|Integer|255144|The field contains the average RTT in microseconds|
|rtt_max|Integer|1488525|The field contains the maximum RTT in microseconds|
|rtt_min|Integer|68023|The field contains the minimum RTT in microseconds|
|rtt_stddev|Integer|243171|The field contains the standard deviation RTT measured in microseconds|
|success|Boolean|true|The field contains the number of successes (note: use|failures/(successes+failures)) for packet loss)|
|target|String|n1-the1.samknows.com|The field holds a string of the measurement server target hostname or IP address. The value is pulled from the test configuration file.|
|target_ipaddress|String|46.17.56.234|The field holds a four tuple colon deliminated IP address of the 'target' measurement server, as resolved by the handset's locally configured DNS for the active network used to execute the test.|
|timestamp|Integer|1359128167|The field contains the time the measurement concluded represented as a sql TIMESTAMP datatype. http://developer.android.com/reference/java/sql/Timestamp.html|

### CLOSESTTARGET Reference

|Property| Type |Description |Explanation|
|--------|------|------------|-----------|
|type|String|CLOSESTTARGET|The active metric type 'CLOSESTTARGET' contains the nearest (in latency) measurement server that the client assess as it activates for testing|
|timestamp|Integer|1384442005|The field contains the time the measurement concluded represented as a sql TIMESTAMP datatype.|http://developer.android.com/reference/java/sql/Timestamp.html|
|datetime|String|Thu Nov 14 09:13:25 CST 2013|The field contains the time test finished in UTC.|
|success|Boolean|true|The field represents the success or failure of the measurement. True denotes a successful execution of the entire test.|
|ip_closest_target|String|4.30.14.254|The field contains the IP address of the nearest measurement server|

### phone_identity Reference

|Property| Type |Description |Explanation|
|--------|----|-----------|-----------|
|type|String|phone_identity|The passive metric type 'phone_identity' describes features of the handset and|installed operating system.|
|datetime|String|Fri Jan 25 15:35:07 GMT 2013|The unix time and date of the handset performing the measurement at the|beginning of the observations.|
|manufacturer|String|api android.os.Build.MANUFACTURER|The field holds a string from the Android method that identifies the handset manufacturer.| 
|model|String|api android.os.Build.MODEL|The field holds a string from the Android method that identifies the handset model.|
|os_type|String|android|The field holds a string for the Operating System of the handset. This value is set by the application logic.|
|os_version|Integer|api android.os.Build.VERSION.SDK_INT|
|timestamp|Integer|1359128107|The field contains the unix timestamp of the handset performing the measurement at the beginning of the observations as a sql TIMESTAMP datatype. http://developer.android.com/reference/java/sql/Timestamp.html|

### network_data Reference

|Property|Type|Description|Explanation|
|--------|----|-----------|-----------|
|type|String|network_data|The passive metric type 'network_data' describes features of the wireless|connectivity of the active network connection.|
|active_network_type|String|android.net.ConnectivityManager  .getActiveNetworkInfo()  .getTypeName() |The field holds an integer from the Android method that identifies the type of wireless network that provides Internet connectivity at the time of the observation.|
|active_network_type_code|String|android.net.ConnectivityManager  .getActiveNetworkInfo()  .getType()| The field holds string from the Android method that identifies the type of wireless network that provides Internet connectivity at the time of the observation.|
|connected|Boolean|android.net.ConnectivityManager  .getActiveNetworkInfo()  .isConnected() |The field holds boolean true or false value from the Android method that identifies whether network connectivity exists and it is possible to establish connections and pass data.|
|datetime|String|Fri Jan 25 15:35:07 GMT 2013|The unix time and date of the handset performing the measurement at the|beginning of the observations.|
|network_operator_code|String|android.telephony.TelephonyManager  .getNetworkOperator() |The field holds string from the Android method that identifies the numeric name (MCC+MNC) of the current registered operator of the Internet connectivity|at the time of the observation.|
|network_operator_name|String|android.telephony.TelephonyManager  .getNetworkOperatorName()|The field holds string from the Android method that identifies the text readable name of the current registered operator of the Internet connectivity at the time of the observation.|
|network_type_code|Integer|android.telephony.TelephonyManager  .getNetworkType()|The field holds an integer from the Android method that identifies a constant indicating the radio technology (network type) currently in use on the handset for data transmission.|
|phone_type_code|Integer|api android.telephony.TelephonyManager  .getPhoneType()|The field holds an integer from the Android method that identifies a constant indicating the device phone type.|
|network_type|String|HSDPA|The field holds a string converted from the Android method that identifies a|constant indicating the radio technology (network type) currently in use on|the handset for data transmission.|
|phone_type_code|Integer|api android.telephony.TelephonyManager  .getPhoneType()|The field holds an integer from the Android method that identifies a constant indicating the device phone type.|
|phone_type|String|GSM|The field holds a string converted from the Android method that identifies a|constant indicating the device phone type.|
|roaming|Boolean|android.telephony.TelephonyManager  .isNetworkRoaming()|The field holds a boolean true false value from the Android method that identifies whether the active connection is considered roaming on the current|network, for GSM purposes.|
|sim_operator_name|String|android.telephony.TelephonyManager  .getSimOperatorName()|The field holds string from the Android method that identifies the Service Provider Name (SPN)|
|timestamp|Integer|1359128107|The unix timestamp of the handset performing the measurement at the beginning|of the observations.|

### gsm_cell_location Reference

|Property| Type |Description |Explanation|
|--------|----|-----------|-----------|
type|String|gsm_cell_location|The passive metric type 'gsm_cell_location' describes the location of handsetdetermined by the GSM provider technology.|
|bit_error_rate|Integer|android.telephony.SignalStrength.getGsmBitErrorRate()|The field holds an integer from the Android method that identifies the GSM bit error rate (0-7, 99) as defined in TS 27.007 8.5.|
|cell_tower_id|Integer|api android.telephony.gsm.GsmCellLocation.getCid()|The field holds an integer from the Android method that identifies the GSM tower location id, noting -1 if unknown, and 0xffff as the max allowable value.|
|datetime|String|Fri Jan 25 15:35:07 GMT 2013|The unix time and date of the handset performing the measurement at the beginning of the observations.|
|location_area_code|Integer|android.telephony.gsm.GsmCellLocation.getLac()|The field holds an integer from the Android method that identifies the GSM location area code, noting -1 if unknown, and 0xffff as the max allowable value.|
|signal_strength|Integer|android.telephony.SignalStrength .getGsmSignalStrength()|The field holds an integer from the Android method that identifies the GSM Signal Strength, with valid values are (0-31, 99) as defined in TS 27.007 8.|
|timestamp|Integer|1359128107|The unix timestamp of the handset performing the measurement at the beginning of the observations.|
|umts_psc|Integer|android.telephony.gsm.GsmCellLocation.getPsc()|The field holds an integer from the Android method that identifies the primary scrambling code of the serving cell on a UMTS network.|



### cdma_cell_location Reference
|Property|Type|Description|Explanation|
|--------|----|-----------|-----------|
|type|String|cdma_cell_location|The passive metric type 'cdma_cell_location' describes the location of handset determined by the CDMA provider technology. |
|datetime|String|Fri Jan 25 15:35:07 GMT 2013|The unix time and date of the handset performing the measurement at the beginning of the observations.|
|timestamp|Integer|1359128107|The unix timestamp of the handset performing the measurement at the beginning of the observations. |
|base_station_id|Integer|android.telephony.cdma.CdmaCellLocation   .getBaseStationId()|The field holds an integer from the Android method that identifies the cdma base station identification number, and -1 if unknown. |base_station_latitude|Integer|android.telephony.cdma.CdmaCellLocation   .getBaseStationLatitude()|The field holds an integer from the Android method that identifies the cdma latitude as a decimal number as specified in 3GPP2 C.S0005-A v6.0. (http://www.3gpp2.org/public_html/specs/C.S0005-A_v6.0.pdf) It is represented in units of 0.25 seconds and ranges from -1296000 to 1296000, both values inclusive (corresponding to a range of -90 to +90 degrees). Integer.MAX_VALUE is considered invalid value.|
|base_station_longitude|Integer|android.telephony.cdma.CdmaCellLocation   .getBaseStationLongitude()|The field holds an integer from the Android method that identifies the cdma longitude is a decimal number as specified in 3GPP2 C.S0005-A v6.0. (http://www.3gpp2.org/public_html/specs/C.S0005-A_v6.0.pdf) It is represented in units of 0.25 seconds and ranges from -2592000 to 2592000, both values inclusive (corresponding to a range of -180 to +180 degrees). Integer.MAX_VALUE is considered invalid value.|
|system_id|Integer|android.telephony.cdma.CdmaCellLocation   .getSystemId()|The field holds an integer from the Android method that identifies the cdma system identification number, and -1 if unknown.|
|network_id|Integer|android.telephony.cdma.CdmaCellLocation   .getNetworkId()|The field holds an integer from the Android method that identifies the cdma network identification number, and -1 if unknown.|
|dbm|Integer|android.telephony.SignalStrength   .getCdmaDbm()|The field holds an integer from the Android method that identifies the CDMA RSSI value in dBm.|
|ecio|Integer|api android.telephony.SignalStrength   .getCdmaEcio()|The field holds an integer from the Android method that identifies the CDMA Ec/Io value in dB*10|

### cell_neighbour_tower_data Reference

|Property| Type |Description |Explanation|
|--------|----|-----------|-----------|
|type|String|cell_neighbour_tower_data|The passive metric type 'cell_neighbour_tower_data' describes the location of handset determined by the GSM provider technology. Calls to this constructor require a radio network type to specified, and responses to the respective Android API calls return the values from the appropriate access network methods.|
|cell_tower_id|Integer|api android.telephony.NeighboringCellInfo   .getCid()|The field holds an integer from the Android method that identifies the neighboring cell tower location id, noting -1 if unknown, and 0xffff as the max allowable value.|
|datetime|String|Thu Jan 24 22:38:33 EST 2013|The unix time and date of the handset performing the measurement at the beginning of the observations.|
|location_area_code|Integer|android.telephony.NeighboringCellInfo   .getLac()|The field holds an integer from the Android method that identifies the neighboring cell tower location area code.|
|network_type_code|Integer|android.telephony.NeighboringCellInfo   .getNetworkType()|The field holds an integer from the Android method that identifies the neighboring cell tower network type while neighboring cell location is stored. Return TelephonyManager.NETWORK_TYPE_UNKNOWN means that the location information is unavailable. Return TelephonyManager.NETWORK_TYPE_GPRS or TelephonyManager.NETWORK_TYPE_EDGE means that Neighboring Cell information is stored for GSM network, in which NeighboringCellInfo   .getLac and NeighboringCellInfo   .getCid should be called to access location. Return TelephonyManager.NETWORK_TYPE_UMTS, TelephonyManager.NETWORK_TYPE_HSDPA, TelephonyManager.NETWORK_TYPE_HSUPA, or TelephonyManager.NETWORK_TYPE_HSPA means that Neighboring Cell information is stored for UMTS network, in which NeighboringCellInfo   .getPsc should be called to access location.|
|network_type|String|UMTS|The field holds a string converted from the Android method that identifies the neighboring cell tower network type while neighboring cell location is stored.|
|rssi|Integer|android.telephony.NeighboringCellInfo   .getRssi()|Received signal strength or UNKNOWN_RSSI if unknown For GSM, it is in "asu" ranging from 0 to 31 (dBm = -113 + 2*asu) 0 means "-113 dBm or less" and 31 means "-51 dBm or greater" For UMTS, it is the Level index of CPICH RSCP defined in TS 25.125|
|timestamp|Integer|1359085113|The unix timestamp of the handset performing the measurement at the beginning of the observations.|
|umts_psc|Integer|android.telephony.NeighboringCellInfo   .getPsc()|The field holds an integer from the Android method that identifies the neighboring cell tower Primary Scrambling Code in 9 bits format in UMTS, 0x1ff max value UNKNOWN_CID if in GSM or CMDA or unknown. |
### location Reference

|Property |Type |Description |Explanation|
|--------|----|-----------|-----------|
|type|String|location|The passive metric type 'location' describes the location of the handset determined by network provider technology or GPS at the time of the observation|
|accuracy|Float|android.location.Location   .getAccuracy()|The field holds a float from the Android method that identifies the accuracy of this location, in meters.|
|datetime|String|Thu Jan 24 22:40:05 EST 2013|The unix time and date of the handset performing the measurement at the beginning of the observations.|
|latitude|Double|android.location.Location   .getLatitude()|The field holds a double from the Android method that identifies the latitude, in degrees.|
|location_type|String|[network|gps]|The field holds a string that identifies whether location was derived from the cellular network technology or the handset's GPS.|
|longitude|Double|android.location.Location   .getLongitude()|The field holds a double from the Android method that identifies the longitude, in degrees.|
|timestamp|String|android.location.Location   .getTime()|The unix timestamp of the handset performing the measurement at the beginning of the observations.||

### PARAM_EXPIRED Reference

|Property |Type |Description| Explanation|
|--------|----|-----------|-----------|
|type|String|PARAM_EXPIRED|The passive metric type 'PARAM_EXPIRED' is a metric which tells that value of a parameter has been expired. At the time being it is used to get control the value of the closest target.|
|datetime|String|Fri Jan 25 10:22:13 EST 2013|The unix time and date of the handset performing the measurement at the beginning of the observations.|
|success|Boolean|false|The field holds boolean true or false value that identifies whether the test execution expired.|
|timestamp|Integer|1359127333|The unix timestamp of the handset performing the measurement at the beginning of the observations.|


### NETACTIVITY Reference
|Property |Type |Description |Explanation|
|--------|----|-----------|-----------|
|type|String|NETACTIVITY|The passive metric type 'NETACTIVITY' describes the traffic sent and received by the handset during a test condition period.|
|bytesin|Integer|0|The field holds an integer value that identifies the number of bytes received by the handset during the test condition period.|bytesout|Integer|0|The field holds an integer value that identifies the number of bytes sent by the handset during the test condition period.|
|datetime|String|Fri Jan 25 10:23:21 EST 2013|The unix time and date of the handset performing the measurement at the beginning of the observations.|
|maxbytesin|Integer|10000|The field holds an integer value that identifies the maximum limit of bytes to be received by the handset during the test condition period.|
|maxbytesout|Integer|5000|The field holds an integer value that identifies the maximum limit of bytes to be sent by the handset during the test condition period.|
|success|Boolean|true|The field holds a boolean value that identifies whether the condition is met. Meaning that bytes received during the test condition period are less than maxbytesin and the bytes sent during the test condition period are less than maxbytesout.|
|timestamp|Integer|1359127401|The unix timestamp of the handset performing the measurement at the beginning of the observations.|


### CPUACTIVITY Reference

|Property |Type| Description |Explanation|
|--------|----|-----------|-----------|
type|String|CPUACTIVITY|The passive metric type 'CPUACTIVITY' describes the cpu activity of the handset during a test condition period. |
|datetime|String|Fri Jan 25 10:23:16 EST 2013|The unix time and date of the handset performing the measurement at the beginning of the observations. |
|max_average|Integer|25|The field holds an integer value that identifies the maximum limit of cpu activity on the handset during the test condition period. |
|read_average|Integer|5|The field holds an integer value that identifies the read average of the handset's cpu activity handset during the measurement observation calculated from /proc/stat in CpuUsageReader.java. |
|success|Boolean|true|The field holds a boolean value that identifies whether the cpu activity has been lower of max_average during the test condition period. |
|timestamp|Integer|1359127396|The unix timestamp of the handset performing the measurement at the beginning of the observations.|

### Example

    
    
    

    {

        "conditions": [

            {

                "datetime": "Fri Jan 25 04:22:13 EST 2013",

                "timestamp": "1359105733",

                "type": "PARAM_EXPIRED",

                "success": "false"

            },

            {

                "timestamp": "1359105782",

                "maxbytesout": "5000",

                "bytesin": "0",

                "maxbytesin": "10000",

                "datetime": "Fri Jan 25 04:23:02 EST 2013",

                "type": "NETACTIVITY",

                "success": "true",

                "bytesout": "0"

            },

            {

                "timestamp": "1359105777",

                "max_average": "25",

                "datetime": "Fri Jan 25 04:22:57 EST 2013",

                "type": "CPUACTIVITY",

                "success": "true",

                "read_average": "2"

            },

            {

                "timestamp": "1359105820",

                "maxbytesout": "5000",

                "bytesin": "0",

                "maxbytesin": "10000",

                "datetime": "Fri Jan 25 04:23:40 EST 2013",

                "type": "NETACTIVITY",

                "success": "true",

                "bytesout": "0"

            },

            {

                "timestamp": "1359105815",

                "max_average": "25",

                "datetime": "Fri Jan 25 04:23:35 EST 2013",

                "type": "CPUACTIVITY",

                "success": "true",

                "read_average": "2"

            },

            {

                "timestamp": "1359105860",

                "maxbytesout": "5000",

                "bytesin": "0",

                "maxbytesin": "10000",

                "datetime": "Fri Jan 25 04:24:20 EST 2013",

                "type": "NETACTIVITY",

                "success": "true",

                "bytesout": "0"

            },

            {

                "timestamp": "1359105855",

                "max_average": "25",

                "datetime": "Fri Jan 25 04:24:15 EST 2013",

                "type": "CPUACTIVITY",

                "success": "true",

                "read_average": "3"

            }

        ],

        "tests": [

            {

                "timestamp": "1359105757",

                "type": "CLOSESTTARGET",

                "datetime": "Fri Jan 25 04:22:37 EST 2013",

                "success": "true",

                "closest_target": "ispmon.samknows.mlab3.lga01.measurement-lab.org",

                "ip_closest_target": "74.63.50.46"

            },

            {

                "timestamp": "1359105795",

                "number_of_threads": "3",

                "target": "ispmon.samknows.mlab3.lga01.measurement-lab.org",

                "warmup_bytes": "300520",

                "type": "JHTTPGETMT",

                "datetime": "Fri Jan 25 04:23:15 EST 2013",

                "bytes_sec": "293758",

                "success": "true",

                "transfer_time": "10229828",

                "transfer_bytes": "3005100",

                "target_ipaddress": "74.63.50.46",

                "warmup_time": "1030365"

            },

            {

                "timestamp": "1359105835",

                "number_of_threads": "3",

                "target": "ispmon.samknows.mlab3.lga01.measurement-lab.org",

                "warmup_bytes": "303104",

                "type": "JHTTPPOSTMT",

                "datetime": "Fri Jan 25 04:23:55 EST 2013",

                "bytes_sec": "151220",

                "success": "true",

                "transfer_time": "11118897",

                "transfer_bytes": "1681408",

                "target_ipaddress": "74.63.50.46",

                "warmup_time": "1351745"

            },

            {

                "timestamp": "1359105890",

                "rtt_avg": "99221",

                "rtt_min": "56030",

                "rtt_max": "1754730",

                "target": "ispmon.samknows.mlab3.lga01.measurement-lab.org",

                "rtt_stddev": "221421",

                "lost_packets": "0",

                "type": "JUDPLATENCY",

                "datetime": "Fri Jan 25 04:24:50 EST 2013",

                "success": "true",

                "target_ipaddress": "74.63.50.46",

                "received_packets": "58"

            }

        ],

        "metrics": [

            {

                "timestamp": 1359105723,

                "model": "HTC Vision",

                "datetime": "Fri Jan 25 04:22:03 EST 2013",

                "type": "phone_identity",

                "manufactor": "HTC",

                "os_version": "10",

                "os_type": "android"

            },

            {

                "network_operator_name": "T-Mobile",

                "active_network_type": "mobile",

                "timestamp": "1359105723",

                "network_operator_code": "310260",

                "network_type": "HSDPA",

                "sim_operator_name": "",

                "phone_type": "GSM",

                "sim_operator_code": "310260",

                "connected": "true",

                "roaming": "false",

                "datetime": "Fri Jan 25 04:22:03 EST 2013",

                "type": "network_data"

            },

            {

                "timestamp": "1359105723",

                "umts_psc": "136",

                "signal_strength": "7",

                "location_area_code": -1,

                "bit_error_rate": "-1",

                "datetime": "Fri Jan 25 04:22:03 EST 2013",

                "type": "gsm_cell_location",

                "cell_tower_id": "-1"

            },

            {

                "timestamp": "1359085205",

                "longitude": "-77.19999999",

                "latitude": "38.79999999",

                "location_type": "network",

                "datetime": "Thu Jan 24 22:40:05 EST 2013",

                "type": "location",

                "accuracy": "867.0"

            }

        ],

        "submission_type": "scheduled_tests",

        "_sourceip": "208.54.90.144",

        "_received": 1359105891

    }

    

