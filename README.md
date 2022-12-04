Challenge #2
We need to write code that will query the meta data of an instance within AWS or Azure or GCP and provide a json formatted output.



The choice of language and implementation is up to you



I've created a linux virtual machine and logged into it and sent this API request :


curl -s -H Metadata:true --noproxy "*" "http://169.254.169.254/metadata/instance?api-version=2021-02-01" | python -m json.tool


 Here IMDS is a REST API that's available at a well-known, non-routable IP address (169.254.169.254). You can only access it from within the VM. 
 
 
 The Azure Instance Metadata Service (IMDS) provides information about currently running virtual machine instances. 
 
 
 You can use it to manage and configure your virtual machines. This information includes the SKU, storage, network configurations, and upcoming maintenance events. 
 The jq utility is available in many cases, but not all. If the jq utility is missing, use | python -m json.tool instead.
 
 
 Response :
 The response is a JSON string.
 
 
 The response will be provided in response.json
