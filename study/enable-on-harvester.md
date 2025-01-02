1. Install host-path CSI
    $ deploy/kubernetes-latest/deploy.sh

2. Change the path to store data
    Edit statefulset csi-hostpathplugin spec.template.volumes[csi-data-dir] as
        - hostPath: 
            path: /var/lib/harvester/defaultdisk
            type: DirectoryOrCreate
        name: csi-data-dir

3. Create SC
    $ kubectl apply -f examples/csi-storageclass.yaml

4. Create block pvc
    $ kubectl apply -f examples/csi-pvc-block.yaml

5. Attach block pvc to pod
    $ kubectl apply -f examples/csi-pod-block.yaml

6. Create snapshot
    $ kubectl apply -f examples/csi-block-pvc-snapshot.yaml

7. Restore pvc from snapshot
    $ kubectl apply -f examples/csi-block-pvc-restore.yaml

8. Attach resotred PVC to pod
    $ kubectl apply -f examples/csi-pod-block-restore.yaml

