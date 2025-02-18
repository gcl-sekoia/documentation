uuid: ee54dd8e-4bd4-4fe8-9d9d-1a018cd8c4bb
name: Log Insight Windows
type: intake

## Overview
Microsoft Windows is a popular operating system developed by Microsoft since 1985.

It's available in three variants:

- Windows for desktop/laptop computers, tablets and smartphones
- Windows Server for servers
- Windows PE as a lightweight version.

{!_shared_content/operations_center/detection/generated/suggested_rules_ee54dd8e-4bd4-4fe8-9d9d-1a018cd8c4bb_do_not_edit_manually.md!}


{!_shared_content/operations_center/integrations/generated/ee54dd8e-4bd4-4fe8-9d9d-1a018cd8c4bb.md!}

## Configure

As of now, the main solution to collect Windows logs with Log Insight leverages the Rsyslog recipe. Please share your experiences with other recipes by editing this documentation.

### Rsyslog

Please refer to the documentation of Linux to forward events to your rsyslog server. The reader can consult the [Rsyslog Transport](../../../ingestion_methods/rsyslog/) documentation to forward these logs to SEKOIA.IO.
