## Operation Scenario

This document guides you through the process of setting a node Label.

## Usage Restrictions

- Labels related to \*kubernetes\* and \*qcloud\* cannot be edited or deleted.
- \*kubernetes\* and \*qcloud\* labels are reserved keys and cannot be added.
- Currently, you can set Labels for one single node at a time, and batch setting is not supported.

## Steps

### Setting a Node Label in the Console

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left navigation pane, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Select the ID/name of the cluster for which to set the node Label to go to the cluster details page.
4. In the left navigation pane, select "Node Management" > "Nodes" to go to the "Node list" page.
5. Select the row of the node for which to set the Label and click **More** > **Edit a Label**.
6. In the "Edit a Label" window that pops up, edit the Label and click **Submit**. See the figure below:
![](https://main.qcloudimg.com/raw/c9565177d7b9551684624b8592bf2d4c.png)

### Using kubectl to Set a Node Label

1. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
2. Run the following command to set a node Label.
```shell
kubectl label nodes <node-name> <label-key>=<label-value>
```
3. Run the following command to view the node Label.
```shell
kubectl get nodes --show-labels
```
A message similar to the one below is returned:
```
NAME           STATUS    ROLES     AGE       VERSION         LABELS
172.17.124.5   Ready     <none>    12d       v1.10.5-tke.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/instance-type=QCLOUD,beta.kubernetes.io/os=linux,failure-domain.beta.kubernetes.io/region=sh,failure-domain.beta.kubernetes.io/zone=200001,kubernetes.io/hostname=172.17.124.5
172.17.124.8   Ready     <none>    12d       v1.10.5-tke.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/instance-type=QCLOUD,beta.kubernetes.io/os=linux,failure-domain.beta.kubernetes.io/region=sh,failure-domain.beta.kubernetes.io/zone=200001,kubernetes.io/hostname=172.17.124.8
```


