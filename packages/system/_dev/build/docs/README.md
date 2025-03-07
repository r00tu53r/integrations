# System Integration

The System integration allows you to monitor servers, personal computers, and more.

Use the System integration to collect metrics and logs from your machines.
Then visualize that data in Kibana, create alerts to notify you if something goes wrong,
and reference data when troubleshooting an issue.

For example, if you wanted to be notified when less than 10% of the disk space is still available, you
could install the System integration to send file system metrics to Elastic.
Then, you could view real-time updates to disk space used on your system in Kibana's _[Metrics System] Overview_ dashboard.
You could also set up a new rule in the Elastic Observability Metrics app to alert you when the percent free is
less than 10% of the total disk space.

## Data streams

The System integration collects two types of data: logs and metrics.

**Logs** help you keep a record of events that happen on your machine.
Log data streams collected by the System integration include application, system, and security events on
machines running Windows and auth and syslog events on machines running macOS or Linux.
See more details in the [Logs reference](#logs-reference).

**Metrics** give you insight into the state of the machine.
Metric data streams collected by the System integration include CPU usage, load statistics, memory usage,
information on network behavior, and more.
See more details in the [Metrics reference](#metrics-reference).

You can enable and disable individual data streams. If _all_ data streams are disabled and the System integration
is still enabled, Fleet uses the default data streams.

## Requirements

You need Elasticsearch for storing and searching your data and Kibana for visualizing and managing it.
You can use our hosted Elasticsearch Service on Elastic Cloud, which is recommended, or self-manage the Elastic Stack on your own hardware.

Each data stream collects different kinds of metric data, which may require dedicated permissions
to be fetched and which may vary across operating systems.
Details on the permissions needed for each data stream are available in the [Metrics reference](#metrics-reference).

## Setup

For step-by-step instructions on how to set up an integration, see the
[Getting started](https://www.elastic.co/guide/en/welcome-to-elastic/current/getting-started-observability.html) guide.

## Troubleshooting

Note that certain data streams may access `/proc` to gather process information,
and the resulting `ptrace_may_access()` call by the kernel to check for
permissions can be blocked by
[AppArmor and other LSM software](https://gitlab.com/apparmor/apparmor/wikis/TechnicalDoc_Proc_and_ptrace), even though the System module doesn't use `ptrace` directly.

In addition, when running inside a container the proc filesystem directory of the host
should be set using `system.hostfs` setting to `/hostfs`.

## Logs reference

### Application

The Windows `application` data stream provides events from the Windows
`Application` event log.

#### Supported operating systems

- Windows

{{fields "application"}}

### System

The Windows `system` data stream provides events from the Windows `System`
event log.

#### Supported operating systems

- Windows

{{fields "system"}}


### Security

The Windows `security` data stream provides events from the Windows
`Security` event log.

#### Supported operating systems

- Windows

{{event "security"}}

{{fields "security"}}

### Auth

The `auth` data stream provides auth logs.

#### Supported operating systems

- macOS prior to 10.8
- Linux

{{fields "auth"}}

### syslog

The `syslog` data stream provides system logs.

#### Supported operating systems

- macOS
- Linux

{{fields "syslog"}}

## Metrics reference

### Core

The System `core` data stream provides usage statistics for each CPU core.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- OpenBSD
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "core"}}

### CPU

The System `cpu` data stream provides CPU statistics.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- OpenBSD
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "cpu"}}

### Disk IO

The System `diskio` data stream provides disk IO metrics collected from the
operating system. One event is created for each disk mounted on the system.

#### Supported operating systems

- Linux
- macOS (requires 10.10+)
- Windows
- FreeBSD (amd64)

#### Permissions

This data should be available without elevated permissions.

{{fields "diskio"}}

### Filesystem

The System `filesystem` data stream provides file system statistics. For each file
system, one document is provided.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- OpenBSD
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "filesystem"}}

### Fsstat

The System `fsstat` data stream provides overall file system statistics.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- OpenBSD
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "fsstat"}}

### Load

The System `load` data stream provides load statistics.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- OpenBSD

#### Permissions

This data should be available without elevated permissions.

{{fields "load"}}

### Memory

The System `memory` data stream provides memory statistics.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- OpenBSD
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "memory"}}

### Network

The System `network` data stream provides network IO metrics collected from the
operating system. One event is created for each network interface.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "network"}}

### Process

The System `process` data stream provides process statistics. One document is
provided for each process.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- Windows

#### Permissions

Process execution data should be available for an authorized user.
If running as less privileged user, it may not be able to read process data belonging to other users.

{{fields "process"}}

### Process summary

The `process_summary` data stream collects high level statistics about the running
processes.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- Windows

#### Permissions

General process summary data should be available without elevated permissions.
If the process data belongs to the other users, it will be counted as unknown value.

{{fields "process_summary"}}

### Socket summary

The System `socket_summary` data stream provides the summary of open network
sockets in the host system.

It collects a summary of metrics with the count of existing TCP and UDP
connections and the count of listening ports.

#### Supported operating systems

- FreeBSD
- Linux
- macOS
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "socket_summary"}}

### Uptime

The System `uptime` data stream provides the uptime of the host operating system.

#### Supported operating systems

- Linux
- macOS
- OpenBSD
- FreeBSD
- Windows

#### Permissions

This data should be available without elevated permissions.

{{fields "uptime"}}
