Challenge #2
We need to write code that will query the meta data of an instance within AWS or Azure or GCP and provide a json formatted output.



The choice of language and implementation is up to you


In orderto query the meta data of an instance within Azure and provide a json formatted output.
We use Azure Instance Metadata Service (IMDS) provides information about currently running virtual machine instances.
This information includes the SKU, storage, network configurations, and upcoming maintenance events.
IMDS is a REST API that's available at a well-known, non-routable IP address (169.254.169.254)

To access IMDS, create a VM from Azure Resource Manager or the Azure portal
login to the vm and pass this API request :
curl -s -H Metadata:true --noproxy "*" "http://169.254.169.254/metadata/instance?api-version=2021-02-01" | jq

This example bypasses proxies. You must bypass proxies when querying IMDS. 

IMDS is not intended to be used behind a proxy and doing so is unsupported. Most HTTP clients provide an option for you to disable proxies on your requests, and this functionality must be utilized when communicating with IMDS.

The jq utility is available in many cases, but not all. If the jq utility is missing, use | python -m json.tool instead.

The response is a JSON string.
