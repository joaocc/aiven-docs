---
title: Storing data in custom clouds
sidebar_label: Data storage
keywords: [bring your own cloud, byoc, custom cloud, BYOC cloud, object storage, tiered storage, S3 bucket, S3]
---

import ConsoleLabel from "@site/src/components/ConsoleIcons";

Bring your own cloud (BYOC) allows you to use object storage in your own remote cloud account to store [cold data](/docs/platform/howto/byoc/store-data#tiered-storage) and [backups](/docs/platform/howto/byoc/store-data#user-owned-backups).

## Tiered storage

You can store data hosted in your custom cloud using tiered storage, a data allocation
mechanism for improved efficiency and cost optimization. When enabled, tiered storage
allows moving data automatically between hot storage (for frequently accessed, critical,
and often updated data) and cold storage (for rarely accessed, static, or archived data).

Cold storage for BYOC-hosted services uses object storage in your own remote cloud account.
For purposes of the cold storage:

- In AWS BYOC, one S3 bucket is created per custom cloud.
- In Google Cloud BYOC, one S3 bucket is created per BYOC-hosted service.

To use tiered storage in a BYOC-hosted service, tiered storage needs to be enabled both
[in your custom cloud](/docs/platform/howto/byoc/store-data#enable-in-a-custom-cloud) and
[in the BYOC-hosted service](/docs/platform/howto/byoc/store-data#enable-on-a-service).

### Enable in a custom cloud

- Each custom cloud you create has tiered storage enabled by default.
- For existing custom clouds created in the past with no tiered storage support,
  [contact the Aiven support team](mailto:support@aiven.io) to request enabling tiered
  storage.

:::note
You cannot deactivate tiered storage on your custom cloud once it's activated.
:::

### Enable on a service

#### Prerequisites

- At least one [custom cloud](/docs/platform/howto/byoc/create-custom-cloud)
- At least one [Aiven-manged service](/docs/platform/howto/create_new_service), either
  Aiven for Apache Kafka® or Aiven for ClickHouse®, hosted in a custom cloud

  :::note
  If your service is not hosted in a custom cloud, find out whether you can
  [migrate to a custom cloud](/docs/platform/howto/byoc/manage-byoc-service#migrate-an-existing-service-to-a-custom-cloud).
  :::

#### Limitations

- BYOC supports tiered storage for the following service types:
  - [Aiven for Apache Kafka](/docs/products/kafka/howto/kafka-tiered-storage-get-started)
  - [Aiven for ClickHouse](/docs/products/clickhouse/concepts/clickhouse-tiered-storage)
- Non-BYOC services with Aiven-owned tiered storage enabled cannot be migrated to BYOC,
  and the tiered storage mechanism they use cannot be changed to use object storage in
  your own remote cloud account as cold storage.

#### Activate tiered storage

You can activate tiered storage for A BYOC service either during service creation or on
an existing service.

##### Activate on a new service

1. Log in to the [Aiven Console](https://console.aiven.io/), and go to your organization.
1. Click **Admin** in the top navigation, and click <ConsoleLabel name="bringyourowncloud"/>
   in the sidebar.
1. Select a custom cloud where to activate tiered storage, and go to the **Tiered storage**
   tab.
1. Click **Activate tiered storage**, use the toggle for enabling tiered storage, and click
   **Next**.

   Now, the updated infrastructure Terraform template and variables file are generated with
   the new tiered storage configuration.

1. Copy or download the template and re-deploy it in your remote cloud account using the
   variables provided in the variables file.

##### Activate on an existing service

1. Log in to the [Aiven Console](https://console.aiven.io/), and go to your organization.
1. Click **Admin** in the top navigation, and click <ConsoleLabel name="bringyourowncloud"/>
   in the sidebar.
1. Select a custom cloud where to activate tiered storage, and go to the **Tiered storage**
   tab.
1. Click **Activate tiered storage**, use the toggle for enabling tiered storage, and click
   **Next**.

   Now, the updated infrastructure Terraform template and variables file are generated with
   the new tiered storage configuration.

1. Copy or download the template and re-deploy it in your remote cloud account using the
   variables provided in the variables file.

## User-owned backups

By default, data backups of BYOC-hosted services are stored in object storage in your own
remote cloud account. For purposes of data backups:

- In AWS BYOC, one S3 bucket is created per custom cloud.
- In Google Cloud BYOC, one S3 bucket is created per BYOC-hosted service.

## Related pages

-   [Enable tiered storage for Aiven for Apache Kafka](/docs/products/kafka/howto/enable-kafka-tiered-storage).
-   [Enable tiered storage for Aiven for ClickHouse](/docs/products/kafka/howto/enable-kafka-tiered-storage).
-   [About bring your own cloud](/docs/platform/concepts/byoc)
-   [Bring your own cloud networking and security](/docs/platform/howto/byoc/networking-security)
-   [Enable bring your own cloud (BYOC)](/docs/platform/howto/byoc/enable-byoc)
-   [Create a custom cloud in Aiven](/docs/platform/howto/byoc/create-custom-cloud)
-   [Download an infrastructure template and a variables file](/docs/platform/howto/byoc/download-infrastructure-template)
