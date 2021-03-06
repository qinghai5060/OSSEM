# Event Schema
Event fields used to define specific metadata of the event itself. For example event_uid or event_creation_timestamp

## Data Fields
|Standard Name|Type|Description|Sample Value|
|---|---|---|---|
| @timestamp|date|The most accurate timestamp of the log. Commonly this will be the original reporting timestamp from the log. However, if you believe the log timestamp has been altered or skewed (ie: either due to timezone issues or NTP skew)then replace this field with the most likely timestamp. Always keep the original log timestamp in the field `event_creation_time`|43201.2404861111|
|event_duration|float|The length/duration of the event in seconds  (e.g., 1 min is 60.0)|60|
| event_error|string|Information about an error||
| event_error_code|integer|Integer that defines a particular `event_error`||
| event_id|integer|event identifier for specific event logs. Event ids might repeat across different data sources. This is most common in Windows using EventID|1|
| event_category_type|string|A description of the event, which can help with categorization. If the vendor defines a category/grouping for its log. ie: Zeek has a few category types for its many logs (`network-protocols`, `network-observations`, etc...). Example. sysmon event id 12 is `EventType` field is this.|network-protocols|
| event_ip_addr|string|The IP address from which the event/log came from. There may be multiple IP addresses in an event (ie: syslog could have forwarder IP), this field is to be the most true log IP (ie: NOT the forwarders IP)|10.10.10.10|
| event_host_name|string|The host name from which the event/log came from. There may be multiple host names in an event (ie: syslog could have forwarder host name), this field is to be the most true log host name (ie: NOT the forwarders name)|bobs.uncle-pc|
| event_original_message|string|The (original) log message from the source before any ETL manipulations/modifications||
| event_original_time|date|original time when event/log was created as reported from the log source itself|43201.2404861111|
| event_recorded_time|date|The time the log was recorded on disk or data plane or if there is another timestamp with the log (common scenario if there is a a manager of many devices or the log itself tracks log time and log written/recorded time)  (e.g., 1 min is 60.0)|4/11/2018 5:46:18|
| event_severity|string|Event level/severity. The severity of the event as defined manually or usually via the original log, commonly this would be syslog severity. The number codes should be converted to their corresponding string value|alert|
|event_status|string|Defines the status of a particular event|User logon with expired account|
| event_status_code|integer|Integer that defines a particular `event_status`|3221225875|
|event_sub_status|string|Additional status information|Account expired 300 days ago|
| event_sub_status_code|integer|Integer that defines a particular `event_sub_status`|0|
| event_sub_category_type|string|What sub type is for the given `event_category_type`, #TODO: this need fleshed out more...|Microsoft-Windows-Sysmon/Operational|
| event_sub_type|string|What sub type is for the given `event_type`, this should be closest to what the vendor calls it. ie: Zeek Conn log would be `conn`. PaloAlto traffic log would be `traffic`. Additonal example, for `wef` the channel `Sysmon` would be `Microsoft-Windows-Sysmon/Operational`|Microsoft-Windows-Sysmon/Operational|
| event_timezone|string|Timezone of the event if it can be determined. Format such as: UTC, UTC+1, UTC-5, etc..|UTC|
| event_type|string|What the event/log is (ie: zeek, wef/windows, paloalto, cisco, etc). The general type of device of the log|winevent|
| event_type_detailed|string|Additional description of `event_type` if applicable #TODO: this need fleshed out more...||
|event_uid|string|Unique ID specific to the log/event as recorded from the source. For example in Windows event logs, use RecordNumber|CMzY3i4YoNZ3mT5yu5|
| event_vendor|string|Name of the vendor for the log (examples: `PaloAlto`, `Corelight`, `Cisco`, `Juniper`, `VMWare`, etc...)|Microsoft|


### TODO:
figure out something like windows - application channel that has a souce within..  so `event_type:wef` `event_sub_type:Application` then what is (for example) `Application Error` (should probably be called `event_category_type`) and then `Application Crashing Events` would be `event_sub_category_type` 