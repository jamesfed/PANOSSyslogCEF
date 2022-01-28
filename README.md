# Introduction
Palo Alto Networks Next Generation Firewalls support sending logs (via a custom format) in the CEF (Common Event Format) syntax. PAN provide detailed configuration guides at https://docs.paloaltonetworks.com/resources/cef.html however it's a bit of a chore to extract a working configuration out of the PDFs and many of the headers included are superfluous in many environments.

This repo looks to help with this problem by providing simplified CEF templates with a subset of the fields that I've found useful in deployments in the past. Note that it's targeted at PAN-OS 10.1 and some fields may not exist in earlier releases. You should also examine the list of fields to ensure I haven't skipped over any that you would find useful in your own deployments.

# Escaping
In particular when shipping URL logs it's very likely you'll bump into issues without configuring escaping on the 'Custom Log Format' tab. Make sure you tick the 'Escaping' box and set Escaped Characters to = with the Escape Character as \.

# Notable exclusions
## Traffic
* Device Group Hierarchy
* Source/Destination VM UUID
* Tunnel ID/IMSI
* Monitor Tag/IMEI
* SCTP
* Anything SD-WAN related
* Anything Container related
* Session Owner

## Threat
* Device Group Hierarchy
* Source/Destination VM UUID
* Tunnel ID/IMSI
* Monitor Tag/IMEI
* SCTP
* Anything Container related

# Why CEF instead of plain old syslog?
CEF includes metadata to help your logging service/SIEM parse the information without using complex extractors (looking at you https://github.com/jamesfed/PANOSGraylogExtractor). 
# Contributing
If I’ve missed an important field that everyone should include in their log output please make a Pull Request with an explanation as to why you believe that field is so important and I’ll consider it for inclusion.
