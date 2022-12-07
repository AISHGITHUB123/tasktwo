Challenge #2
We need to write code that will query the meta data of an instance within AWS or Azure or GCP and provide a json formatted output.



The choice of language and implementation is up to you


In orderto query the meta data of an instance within Azure and provide a json formatted output.
We use Azure Instance Metadata Service (IMDS) provides information about currently running virtual machine instances.

Let's say we have a windows VM :This VM has it's own name but it knows nothing about the azure resource manager

We use here the invoke web request to talk to 169.254.169.254 and to metadata endpoint and pass the api version latest

Lets save this output to a variable :
----------------------------------
$respraw=Invoke-WebRequest -Headers @{"Metadata"="true"} -Method GET -Proxy $Null -Uri "http://169.254.169.254/metadata/instance?api-version=2021-01-01"
we can see the response here with $respraw : It will return everything - comprises of everything compute,n/w ,license,os disk data 
userdata,tags info,
$respraw


$respraw.Content


$respraw.Content | ConvertFrom-Json | ConvertTo-Json -Depth 6

As we had kind of format so rather using invoke web request we can use invoke rest method this will prekind the format into a native powershell object

#A better way that automatically creates us a nice PowerShell object with the response
-------------------------------------------------------------------------------------
$resp=Invoke-RestMethod -Headers @{"Metadata"="true"} -Method GET -Proxy $Null -Uri "http://169.254.169.254/metadata/instance?api-version=2021-01-01"
$respJSON = $resp | ConvertTo-Json -Depth 6

Compute only, could do Network, all the main JSON headings
----------------------------------------------------------
Invoke-RestMethod -Headers @{"Metadata"="true"} -Method GET -Proxy $Null -Uri "http://169.254.169.254/metadata/instance/compute?api-version=2021-01-01"

#Just get tags
--------------
Invoke-RestMethod -Headers @{"Metadata"="true"} -Method GET -Proxy $Null -Uri "http://169.254.169.254/metadata/instance/compute/tagsList?api-version=2021-01-01"

#Linux
-------
curl -H Metadata:true --noproxy "*" "http://169.254.169.254/metadata/instance?api-version=2020-09-01" | jq
This information includes the SKU, storage, network configurations, and upcoming maintenance events.
IMDS is a REST API that's available at a well-known, non-routable IP address (169.254.169.254)

To access IMDS, create a VM from Azure Resource Manager or the Azure portal
login to the vm and pass this API request :
curl -s -H Metadata:true --noproxy "*" "http://169.254.169.254/metadata/instance?api-version=2021-02-01" | jq

This example bypasses proxies. You must bypass proxies when querying IMDS. 

The jq utility is available in many cases, but not all. If the jq utility is missing, use | python -m json.tool instead.

The response is a JSON string.
