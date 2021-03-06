# Meta and Fingerprint Schema
Added fields that are derived from an event's data/fields after it is has been logged or stored and more specifically could change based on future information. In the simplest form, this would include enrichments of the data.
A good example, would be the Autonomous System Number lookup of an IP address. The reason, is because an IP address on 2018-01-01 may belong to one entity and the later in the future could be acquired by a new entity and thus the data from 2018-01-01 may be different than say 2022-01-01. Actually, a great example of this example is the IP address `1.1.1.1` that for a long time belonged to APNIC, and then was acquired by Cloudflare in 2019. The Meta schema, is a way that can help aide an analyst to know the field they are looking at may be derived from a data source or calculation that could change over time.  

The best way to use this field schema, may be to copy the fields/values that may already exist in a dataset to one of the following categories.  
For example: a url category would be set to `meta_dst_host_name_category`


## Data Fields
|Standard Name|Type|Description|Sample Value|
|---|---|---|---|
| meta_dns_response_name_count|integer|The count (number of) `dns_response_name||
| meta_dns_response_name_has_non_ascii|boolean|If there is any non ascii characters within `dns_response_name`||
| meta_dns_response_name_length|integer|Total number of response/answers in `dns_response_name`||
| meta_dst_host_name_category|string|Used for URL/domain category (ie: Adult, Abuse, Parked, RFC-1918, etc)||
| meta_http_referrer_length|integer|length of `http_referrer_original`||
| meta_log_tags|array_string|| `|
| meta_powershell_param_value_has_non_ascii|boolean|| `|
| meta_powershell_scriptblock_text_has_non_ascii|boolean|| `|
| meta_powershell_scriptblock_text_length|integer|| `|
| meta_process_command_line_has_net|boolean|if `process_command_line` contains `http:` or `ftp:\\` or `smb:\\` or `file:\\` or `://` or `localhost` or r`\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}`||
| meta_process_command_line_has_non_ascii|boolean|| `|
| meta_process_command_line_length|integer|| `|
| meta_src_ip_addr_equals_dst_ip_addr|boolean|If the `src_ip_addr` is the same value as `dst_ip_addr`||
| meta_target_user_name_is_machine|boolean|| `|
| meta_url_has_non_ascii|boolean|| `|
| meta_url_has_whitespace|boolean|| `|
| meta_url_length|integer|length of `url_original`||
| meta_url_paths_count|integer|number (count)    of paths in `url_original`. ie: `/example/url/news.php` would be `3`||
| meta_user_agent_length|integer|length of `user_agent_original`||
| meta_user_name_is_machine|boolean|| `|
| meta_user_reporter_name_is_machine|boolean|| `|
| ttp|string|Tactic, technique, and procedure||
| TBD|geo_point|Geo longitude and latitude point of a field||
| TBD|integer|Autonomous System (AS) number (BGP AS Number)||
| TBD|string|Data describing an alert||
| TBD|string|Autonomous System (AS) organization (BGP AS Name)||


# Fingerprint Schema
Enrichments that create a unique value (fingerprint)

|	        Standard Name       	|            Field Name|	    Type            	|   	    Description          	|	     Sample Value           	|
|	-------------------------------	|	-------------------------------	|	-------------------------------	|	-------------------------------	|	-------------------------------	|
| fingerprint_dns_response_name_mm3|string|MURMUR3 hash of `dns_response_name`||
| fingerprint_ip_addr_any_dst_and_src|string|Used to find any time the two IP addresses of `src_ip_addr` and `dst_ip_addr` have made a connection in any way. In order to do a true any ip pair field, sorts `fingerprint_ip_addr_pair_dst_and_src` and `fingerprint_ip_addr_pair_src_and_dst` and joins the values and then md5sum's them||
| fingerprint_ip_addr_pair_dst_and_src|string|MD5 hash of the concatenation of `dst_ip_addr` and `src_ip_addr`. Used to find any time `dst_ip_addr` makes a connection to the `src_ip_addr`||
| fingerprint_ip_addr_pair_src_and_dst|string|MD5 hash of the concatenation of `src_ip_addr` and `dst_ip_addr`. Used to find any time `src_ip_addr` makes a connection to the `dst_ip_addr`||
| fingerprint_network_4tuple|string|MD5 hash of `fingerprint_ip_addr_pair_src_and_dst` + `dst_port` + `network_protocol`||
| fingerprint_network_community_id|string|Network community ID as outlined by the standard from https://github.com/corelight/community-id-spec. Standardized hashing of network tuple. The combination, most commonly, of Source IP, Source Port, Destination IP, Destination Port, and IP Protocol allows pivoting between multiple log types|1:EeVyZ07VGj1n0rld+xCLFdM+u8M=
| fingerprint_powershell_param_value_mm3|string|MURMUR3 hash of `powershell.param.value`||
| fingerprint_powershell_scriptblock_text_sha1|string|SHA1 hash of `powershell.scriptblock.text`||
| fingerprint_process_command_line_mm3|string|MURMUR3 hash of `process_command_line`||
