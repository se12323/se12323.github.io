b---
layout: post
title: Rsyslog
description: >
    This is how to check logs in OS.
sitemap: false
group: true
hide_last_modified: true
image: /assets/img/nsad/rsyslog/rsyslog.png
---

## System Log Checker (COMP7006_LAB 2)


## Log
A record of the operating state of a computer is called a log. In Linux, it is possible to record various events in log files or display them on the console using syslog.


## rsyslog & syslog
> ### a) syslog
> syslog is a log collection memory system that records log information of kernels and programs. It is generally recorded as 'date time, host, process: event'. syslog is a local It can record system log as well as program log information of remote host through tcp, udp protocol.
> ### b) rsyslog
> - As an upgraded version of syslog, rsyslog can simultaneously record local or remote logs in multiple lines and store log information in RDBMS such as MySQL, PGSQL, Oracle, etc. 
> - It has a powerful filter function that can filter all contents of the log.
> - rsyslog is the log system used on CentOS 6 and later systems, and has the following advantages over the older syslog log system:
>>   a) Multi-threaded support<br/>
>>   b) Protocol support such as TCP, SSL, TLS, RELP<br/>
>>   c) Powerful filter to filter any part of log information<br/>
>>   d) Support for custom output formats<br/>
>>   e) Ideal for enterprise-grade logging requirements
modularity<br/>
>>   f) Record format in log<br/>
>>   g) Date Time Host Process [pid]: Event Content<br/>
## Concepts in rsyslog
An application on the system specifies a specific channel history log. 
> p.s Channels set the logging level for logs by default. <br/>

When the program generates log information, it writes the log file to the specified local file, database, or remote rsyslog service through this channel.
Of course, the log output by the application program is also generally classified according to the stage. 
> For example, sshdconf defines a channel as log output at the authpriv, info level. # Logging - SyslogFacility AUTHPRIV - #LogLevel INFO

## Facility & Priority
