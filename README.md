Challenge #2
We need to write code that will query the meta data of an instance within AWS or Azure or GCP and provide a json formatted output.The choice of language and
implementation is up to you
I've created a linux virtual machine and logged into it and sent this API request :
 curl -s -H Metadata:true --noproxy "*" "http://169.254.169.254/metadata/instance?api-version=2021-02-01" | python -m json.tool
 Here IMDS is a REST API that's available at a well-known, non-routable IP address (169.254.169.254). You can only access it from within the VM. 
 The Azure Instance Metadata Service (IMDS) provides information about currently running virtual machine instances. 
 You can use it to manage and configure your virtual machines. This information includes the SKU, storage, network configurations, and upcoming maintenance events. 
 The jq utility is available in many cases, but not all. If the jq utility is missing, use | python -m json.tool instead.
 Response :
 The response is a JSON string.
 {
    "compute": {
        "azEnvironment": "AzurePublicCloud",
        "customData": "",
        "evictionPolicy": "",
        "isHostCompatibilityLayerVm": "false",
        "licenseType": "",
        "location": "eastus",
        "name": "VM2",
        "offer": "UbuntuServer",
        "osProfile": {
            "adminUsername": "adminaish",
            "computerName": "VM2",
            "disablePasswordAuthentication": "false"
        },
        "osType": "Linux",
        "placementGroupId": "",
        "plan": {
            "name": "",
            "product": "",
            "publisher": ""
        },
        "platformFaultDomain": "0",
        "platformUpdateDomain": "0",
        "priority": "",
        "provider": "Microsoft.Compute",
        "publicKeys": [],
        "publisher": "Canonical",
        "resourceGroupName": "Metadata-RG",
        "resourceId": "/subscriptions/88f9ae14-249c-43b3-91aa-b68f368830cc/resourceGroups/Metadata-RG/providers/Microsoft.Compute/virtualMachines/VM2",
        "securityProfile": {
            "secureBootEnabled": "false",
            "virtualTpmEnabled": "false"
        },
        "sku": "18_04-lts-gen2",
        "storageProfile": {
            "dataDisks": [],
            "imageReference": {
                "id": "",
                "offer": "UbuntuServer",
                "publisher": "Canonical",
                "sku": "18_04-lts-gen2",
                "version": "latest"
            },
            "osDisk": {
                "caching": "ReadWrite",
                "createOption": "FromImage",
                "diffDiskSettings": {
                    "option": ""
                },
                "diskSizeGB": "30",
                "encryptionSettings": {
                    "enabled": "false"
                },
                "image": {
                    "uri": ""
                },
                "managedDisk": {
                    "id": "/subscriptions/88f9ae14-249c-43b3-91aa-b68f368830cc/resourceGroups/Metadata-RG/providers/Microsoft.Compute/disks/VM2_OsDisk_1_c09f3af924f64c54b1230fb2fa1397ab",
                    "storageAccountType": "Premium_LRS"
                },
                "name": "VM2_OsDisk_1_c09f3af924f64c54b1230fb2fa1397ab",
                "osType": "Linux",
                "vhd": {
                    "uri": ""
                },
                "writeAcceleratorEnabled": "false"
            },
            "resourceDisk": {
                "size": "34816"
            }
        },
        "subscriptionId": "88f9ae14-249c-43b3-91aa-b68f368830cc",
        "tags": "",
        "tagsList": [],
        "userData": "",
        "version": "18.04.202210180",
        "vmId": "73924fc6-b798-4c76-af05-0ffa08bc8af4",
        "vmScaleSetName": "",
        "vmSize": "Standard_B1s",
        "zone": ""
    },
    "network": {
        "interface": [
            {
                "ipv4": {
                    "ipAddress": [
                        {
                            "privateIpAddress": "10.1.0.4",
                            "publicIpAddress": ""
                        }
                    ],
                    "subnet": [
                        {
                            "address": "10.1.0.0",
                            "prefix": "24"
                        }
                    ]
                },
                "ipv6": {
                    "ipAddress": []
                },
                "macAddress": "6045BDD7B6FE"
            }
        ]
    }
}
--------------------------
