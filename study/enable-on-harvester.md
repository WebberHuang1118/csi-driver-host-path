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

9. Use for VM Snapshot
    9.1 Edit setting csi-driver-config as "value: '{"hostpath.csi.k8s.io":{"volumeSnapshotClassName":"csi-hostpath-snapclass"}}'"
    9.2 Create a PVC with host-path CSI
    9.3 Take VM snapshot
    9.4 Restore VM snapshot to a new/existing VM

