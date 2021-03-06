## Operation Scenario

Kubernetes Events contain information about the operations of Kubernetes clusters and the scheduling of various resources, which can help OPS personnel observe daily changes in resources and locate problems. TKE supports event persistence for all your clusters. After this feature is enabled, your cluster events will be exported to the configured storage in real time. TKE also supports retrieval of event transactions using PaaS services provided by Tencent Cloud or open-source software tools. This document describes how to enable persistent storage of cluster events.

## Prerequisites

You are logged in to the [TKE console](https://console.cloud.tencent.com/tke2).

## Steps

### Enable Persistent Storage of Cluster Events

1. In the left navigation pane, click **[Event Persistence](https://console.cloud.tencent.com/tke2/persistentEvent?rid=1)** to go to the persistent cluster event storage management page. See the figure below:
![Event persistence](https://main.qcloudimg.com/raw/f5a2dbcab74a0e44b4d7a489ec8425b7.png)
2. In the row of a cluster whose "status" is "Disabled", click **Settings**.
3. On the "Set event persistence" page, set persistent event storage. See the figure below:
Main setting parameters include:
 - Persistent event storage: Enable persistent event storage.
 - Storage selection:
    - Select "Elasticsearch".
      - Elasticsearch address: Provide the address of the Elasticsearch service.
      - Index: Provide the index of Elasticsearch data.
    - Select "CLS".
    CLS instance: Provide a CLB instance in the same region as the TKE cluster.

 >! 
 > - After persistent event storage is enabled, an event collection container will be automatically deployed in your cluster, which will consume additional resources of approximately 0.2 cores of CPU and 100 MB of memory. Such resources will be released after persistent event storage is disabled.
 > - If you select the "Elasticsearch" storage, please make sure that the Elasticsearch service you provide can communicate with the current cluster network; otherwise, events cannot be stored properly. It is recommended to deploy the TKE cluster and the Elasticsearch service in the same VPC or make them have the same internet egress/ingress.

 ![Enable persistent event storage](https://main.qcloudimg.com/raw/f1e5596b7ad2516d3adb6198c2871ad6.png)
4. Click **Save** to enable persistent storage of cluster events.

### Updating or Disabling Persistent Storage of Cluster Events

1. In the left navigation pane, click **[Event Persistence](https://console.cloud.tencent.com/tke2/persistentEvent?rid=1)** to go to the persistent cluster event storage management page. See the figure below:
![Event persistence](https://main.qcloudimg.com/raw/d20bac46f4d726ec87b54fc9021fb7d6.png)
2. In the row of a cluster whose "status" is "Enabled", click **Update settings**.
3. On the "Set event persistence" page, modify based on actual needs and click **Save** to update or disable persistent storage of cluster events.

