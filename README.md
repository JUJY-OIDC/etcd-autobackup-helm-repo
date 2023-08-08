# ETCD-AutoBackup-Helm-Repo

![image-20230806054900608](https://raw.githubusercontent.com/na3150/typora-img/main/uPic/image-20230806054900608.png)

<h3 align="center">ETCD-AutoBackup</h3>
<p align="center">Auto-Backup Service of ETCD snapshot data according to Kubernetes cluster update<br>
  <br>
 <a href="https://github.com/JUJY-OIDC/etcd-autobackup-helm-repo">Helm Chart</a>
    ·
    <a href="https://github.com/JUJY-OIDC/etcd-autobackup">Code Repo</a>
</p>


<br>

## 👀 Features

**☁️ Save snapshot data at Cloud**

- Save the snapshot data in a cloud provider of your choice.
- Provided vendor : AWS, OCI, NCP

**🧸 User-friendly**

- Provides ease of use through Helm packaging.
- Just fill in the `values.yaml` according to the user.

**🕹️ Versioning**

- Seperation of hot data(7 days, archiving) and cold data(15 days, deletion) using lifecycle policy. 
- Currently only available in AWS.

**🎈 Singleton Pattern**
- One application must be running at a time so that jobs are not duplicated (snapshots are not duplicated).
- Adopt Singleton Pattern to activate only one application instance at the same time

<br>

## 🫧 Configuration

The following table lists the configurable parameters for `vaules.yaml` of the etcd-autobackup chart and their default values.

| Parameter                            | Description                                                  | Default                      |
| ------------------------------------ | ------------------------------------------------------------ | ---------------------------- |
| `etcd.cert_path` (required)          | Value of the directory path containing `ca.crt`, `server.crt`, `server.key`. | `/etc/kubernetes/pki/etcd/ ` |
| `etcd.endpoint` (required)           | Value of endpoint of etcd. This must contain port number and must be a private IP. | none                         |
| `cloudProvider` (required)           | The cloud provider where you want to save the snapshot. You can choose from `aws`, `oci` or `ncp`. | `oci`                        |
| `oci.user_ocid`                      | If you choose oci, value of user ocid. <br> `ocid1.user.oci1..xxxxxxx` | none                         |
| `oci.tenancy_ocid`                   | If you choose oci, value of tenancy ocid. `ocid1.tenancy.oc1..xxxxxxx` | none                         |
| `oci.api_key_path`                   | If you choose oci, value of the path of oci api key. This must exist on the master node. Write the path from the master node. | none                         |
| `oci.bucket_region`                  | If you choose oci, value of bucket region.                   | none                         |
| `oci.namespace`                      | If you choose oci, value of namsapce.                        | none                         |
| `aws.access_key_id`                  | If you choose aws, value of access key id                    | none                         |
| `aws.secret_access_key`              | If you choose aws, value of secret access key                | none                         |
| `aws.region`                         | If you choose aws, value of default region for aws cli       | none                         |
| `ncp.access_key_id`                  | If you choose ncp, value of access key id                    | none                         |
| `ncp.secret_access_key`              | If you choose ncp, value secret access key                   | none                         |
| `ncp.region`                         | If you choose ncp, value of default region                   | none                         |

<br>

## 🤖 Usage 
[Helm](https://helm.sh/) must be installed to use the charts. Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.
### Add helm chart repository to your environment

Once Helm is set up properly, add the repo as follows:

```
$ helm repo add etcd-autobackup https://jujy-oidc.github.io/etcd-autobackup-helm-repo/stable
$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "etcd-autobackup" chart repository
Update Complete. ⎈Happy Helming!⎈
```

### Confirm the repository
```
$ helm repo list
NAME           	URL
...
etcd-autobackup	https://jujy-oidc.github.io/etcd-autobackup-helm-repo/stable
```

### Search charts in the repository
You can then run `helm search repo etcd-autobackup` to see the charts.
```
$ helm search repo etcd-autobackup
NAME                           	CHART VERSION	APP VERSION	DESCRIPTION         
etcd-autobackup/etcd-autobackup	1.0.0        	           	A Helm chart for etcd-autobackup service
```

### Custom values
Download `values.yaml` and write it according to your convenience. Check the [configuration](#-configuration).

```
wget https://github.com/JUJY-OIDC/etcd-autobackup-helm-repo/blob/main/etcd-autobackup/values.yaml
```

### Using the chart
Specify `values.yaml` using `--values` option and install helm chart.
Make sure the `values.yaml` path is clear.

```
helm install etcd-autobackup etcd-autobackup/etcd-autobackup --values=values.yaml
```

All objects created by helm are managed in the `etcd-autobackup` namespace.

When the installation is complete, you can see that the Deployment and ConfigMap are created.

<br>

## ✍️ License

(목표) apache or MIT

<br>

## 👩🏻‍💻 Contributors
<table>
  <tr>
    <td align="center"><a href="https://github.com/juyoung810"><img src="https://avatars.githubusercontent.com/u/57140735?v=4" width="100px;" alt=""/><br /><sub><b>김주영</b></sub></a></td>
    <td align="center"><a href="https://github.com/na3150"><img src="https://avatars.githubusercontent.com/u/64996121?v=4" width="100px;" alt=""/><br /><sub><b>성나영</b></sub></a></td>
    <td align="center"><a href="https://github.com/ziwooda"><img src="https://avatars.githubusercontent.com/u/70079416?v=4" width="100px;" alt=""/><br /><sub><b>정지우</b></sub></a></td>
    <td align="center"><a href="https://github.com/yugyeongh"><img src="https://avatars.githubusercontent.com/u/72396865?v=4" width="100px;" alt=""/><br /><sub><b>현유경</b></sub></a></td>
   
  </tr>
  </table>









