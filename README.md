# Introduction
Palo Alto Networks Next Generation Firewalls support sending logs (via a custom format) in the CEF (Common Event Format) syntax. PAN provide detailed configuration guides at https://docs.paloaltonetworks.com/resources/cef.html however it's a bit of a chore to extract a working configuration out of the PDFs and many of the headers included are superfluous in many environments.

This repo looks to help with this problem by providing simplified CEF templates with a subset of the fields that I've found useful in deployments in the past. Note that it's targeted at PAN-OS 10.1 and some fields may not exist in earlier releases. You should also examine the list of fields to ensure I haven't skipped over any that you would find useful in your own deployments.

# ⚠️ Escaping
In particular when shipping URL logs it's very likely you'll bump into issues without configuring escaping on the 'Custom Log Format' tab. Make sure you tick the 'Escaping' box and set Escaped Characters to \\\= with the Escape Character as \\.

# Notable exclusions
PAN firewalls won't allow a custom syslog profile to have more than 2048 characters per log type, to meet this requirement I have omitted the following fields.

## Traffic
* Device Group Hierarchy ($dg_hier_level_1 - $dg_hier_level_4)
* Source/Destination VM UUID ($src_uuid and $dst_uuid)
* Tunnel ID/IMSI ($tunnelid)
* Monitor Tag/IMEI ($monitortag)
* SCTP ($assoc_id)
* Anything SD-WAN related
* Anything Container related
* Session Owner

## Threat
* Device Group Hierarchy ($dg_hier_level_1 - $dg_hier_level_4)
* Source/Destination VM UUID ($src_uuid and $dst_uuid)
* Tunnel ID/IMSI ($tunnelid)
* Monitor Tag/IMEI ($monitortag)
* SCTP ($assoc_id)
* Anything Container related

## URL
* Device Group Hierarchy ($dg_hier_level_1 - $dg_hier_level_4)
* Source/Destination VM UUID ($src_uuid and $dst_uuid)
* Tunnel ID/IMSI ($tunnelid)
* Monitor Tag/IMEI ($monitortag)
* SCTP ($assoc_id)
* Anything Container related ($container_id)
* PCAP ID ($pcap_id)
* Tunnel Type ($tunnel)
* Anything POD related ($pod_namespace and $pod_name)
* Slice Service Type ($nssai_sst)
* Rule UUID ($rule_uuid)
* Sequence number ($seqno)
* Action Flags ($actionflags)

## System
* Device Group Hierarchy ($dg_hier_level_1 - $dg_hier_level_4)

## Wildfire
* Device Group Hierarchy ($dg_hier_level_1 - $dg_hier_level_4)

## Config
* Device Group Hierarchy ($dg_hier_level_1 - $dg_hier_level_4)

## GlobalProtect
Although no exclusions were made the format differs from the document provided by PAN (which doesn't seem to work out of the box). I welcome feedback on this one!

# Why CEF instead of plain old syslog?
CEF includes metadata to help your logging service/SIEM parse the information without using complex extractors (looking at you https://github.com/jamesfed/PANOSGraylogExtractor). 
# Contributing
If I’ve missed an important field that everyone should include in their log output please make a Pull Request with an explanation as to why you believe that field is so important and I’ll consider it for inclusion.
