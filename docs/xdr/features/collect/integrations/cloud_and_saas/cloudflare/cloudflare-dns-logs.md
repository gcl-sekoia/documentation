uuid: bd9d0f51-114e-499a-bb7a-4f2d0a518b04
name: Cloudflare DNS logs
type: intake

## Overview

Cloudflare is a global network designed to make everything you connect to the Internet secure, private, fast, and reliable.

In this documentation, you will learn how to collect and send Cloudflare DNS logs to SEKOIA.IO.

{!_shared_content/operations_center/detection/generated/suggested_rules_bd9d0f51-114e-499a-bb7a-4f2d0a518b04_do_not_edit_manually.md!}

{!_shared_content/operations_center/integrations/generated/bd9d0f51-114e-499a-bb7a-4f2d0a518b04.md!}

## Configuration

### Create the intake on SEKOIA.IO

Go to the [intake page](https://app.sekoia.io/operations/intakes) and create a new intake from the format Cloudflare.

### Configure events forwarding on Cloudflare

{!_shared_content/operations_center/integrations/cloudflare_necessary_info.md!}

#### Create a Logpush job

Configure a [Logpush job](https://developers.cloudflare.com/logs/reference/logpush-api-configuration/){:target="_blank"} with the following destination:

`https://intake.sekoia.io/plain/batch?header_X-SEKOIAIO-INTAKE-KEY=<YOUR_INTAKE_KEY>`


To do so, you can manage Logpush with cURL:

```bash
$ curl -X POST https://api.cloudflare.com/client/v4/zones/<CLOUDFLARE_ZONE_ID>/logpush/jobs \
-H "Authorization: Bearer <CLOUDFLARE_API_TOKEN>" \
-H "Content-Type: application/json" \
--data '{
    "dataset": "dns_logs",
    "enabled": true,
    "max_upload_bytes": 5000000,
    "max_upload_records": 1000,
    "logpull_options":"fields=ColoCode,EDNSSubnet,EDNSSubnetLength,QueryName,QueryType,ResponseCached,ResponseCode,SourceIP,Timestamp&timestamps=unix",
    "destination_conf": "https://intake.sekoia.io/plain/batch?header_X-SEKOIAIO-INTAKE-KEY=<YOUR_INTAKE_KEY>"
}' # (1)
```

1. will return
```json
{
  "errors": [],
  "messages": [],
  "result": {
    "id": 148,
    "dataset": "dns_log",
    "enabled": false,
    "name": "<DOMAIN_NAME>",
    "logpull_options": "fields=<LIST_OF_FIELDS>=rfc3339",
    "destination_conf": "https://intake.sekoia.io/plain/batch?header_X-SEKOIAIO-INTAKE-KEY=<YOUR_INTAKE_KEY>",
    "last_complete": null,
    "last_error": null,
    "error_message": null
  },
  "success": true
}
```

!!! Important
    Replace :

    - `<YOUR_INTAKE_KEY>` with the Intake key you generated in the [Create the intake on SEKOIA.IO](#create-the-intake-on-sekoiaio) step.
    - `<CLOUDFLARE_API_TOKEN>` with the API Token you generated
    - `<CLOUDFLARE_ZONE_ID>` with the Zone ID you grabbed

{!_shared_content/operations_center/integrations/cloudflare_useful_zones_scoped_api_endpoints.md!}
