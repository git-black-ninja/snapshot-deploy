
## Deploy Snapshot from Scratch

To deploy snapshot, run this command.


```bash
  $ sh CRD-setup.sh
```

First create storageclass.

```bash
  $ kubectl create -f StorageClass.yml

```

then create PVC for deployment.

```bash
  $ kubectl create -f PersistentVolumeClaim.yml
```

Now, time to deploy deployment.

```bash
  $ kubectl create -f deployment.yml

```
### First phase complete, now add files to /var/lib/mysql in pod.
 

Create snapshot of pod's files
```bash
  $ kubectl create -f VolumeSnapshot.yml

```

finally create PVC to restore files

```bash
  $ kubectl create -f pvc-restore.yml

```
### Now, remove all the files that you created in the pod. Then, we will recover the snapshot.

Now, add the new PVC name in your deployment.

```bash
  $ kubectl edit deployments.apps test-mysql

```
## Add the name pvc-restore in the file where I show in the screenshot.
![image](https://github.com/git-black-ninja/snapshot-deploy/assets/141961610/541a3435-253f-4c80-b811-5e7e84a90f3c)
