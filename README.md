# demo-aks-pv-migrate
This is a migration validation repository for Kubernetes PV on AKS.

## Reference Documents
I referred to the following documents and others.
+ https://docs.microsoft.com/en-us/azure/aks/aks-migration#considerations-for-stateful-applications
+ https://docs.microsoft.com/en-us/azure/aks/azure-files-volume#mount-file-share-as-a-persistent-volume
+ https://docs.microsoft.com/en-us/azure/aks/azure-disk-volume#mount-disk-as-volume
+ https://docs.microsoft.com/en-us/azure/aks/availability-zones#azure-disk-availability-zone-support
+ https://docs.microsoft.com/en-us/azure/virtual-machines/disks-deploy-zrs?tabs=portal#limitations

# Other Notes
The following is an example of a mount error when the availability zone of Azure Managed Disks is different from the availability zone of the VM of the VMSS to be mounted.

```
  Warning  FailedAttachVolume  59s (x8 over 2m7s)  attachdetach-controller  AttachVolume.Attach failed for volume "pv-azuredisk" : rpc error: code = Unknown desc = Attach volume /subscriptions/YOUR_SUBSCRIPTIONS_ID/resourceGroups/YOUR_RESOURCE_GROUPE_NAME/providers/Microsoft.Compute/disks/pvc-mng-p-01-disk to instance aks-agentpool-xxxxxx-vmss000000 failed with Retriable: false, RetryAfter: 0s, HTTPStatusCode: 400, RawError: {
  "error": {
    "code": "BadRequest",
    "message": "Disk /subscriptions/YOUR_SUBSCRIPTIONS_ID/resourceGroups/YOUR_RESOURCE_GROUPE_NAME/providers/Microsoft.Compute/disks/pvc-mng-p-01-disk cannot be attached to the VM because it is not in zone '1'."
  }
}
  Warning  FailedMount  5s  kubelet  Unable to attach or mount volumes: unmounted volumes=[azure], unattached volumes=[azure kube-api-access-rcwhs]: timed out waiting for the condition
```

