---
weight: 1
title: "NSX-T security Tags and PowerShell"
date: 2021-12-31T00:00:00+00:00
lastmod: 2021-12-31T00:00:00+00:00
draft: false
author: "Dale Hassinger"
authorLink: "https://twitter.com/dalehassinger"
description: ""
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["PowerShell", "PowerCLI", "NSX-T", "VMware", "vRealize", "Automation"]
categories: ["VCF Automation"]

lightgallery: true

---

**How to work with NSX-T security Tags using PowerShell**

<!--more-->

---

###### PowerShell Code to work with NSX-T APIs

Included some examples of code to Automate adding/removing NSX-T Security Tags from VMs. Also some code to show which VMs are assigned to a Security TAG or which TAGs are assigned to a VM.  
  
Code Samples:
* Add NSX-T Security TAG to a VM.
* Remove NSX-T Security TAG from a VM.
* Show All VMs assigned to a NSX-T Security TAG
* Show All Security TAGs assigned to a VM 

 
Hope you find these snippets of code useful.

---

Click to expand code:
{{< highlight powershell >}}

# Connect to vCenter
$vCenterName = 'vCenter.vCrocs.info'
Connect-VIServer $vCenterName -Credential $cred

Disconnect-VIServer * -Force -Confirm:$false

Start NSX-T

# ----- [ Start Add a Single NSX-T TAG to VM ] --------------------------------------------------

# Add code to allow untrusted SSL certs
# Use when connecting to NSX-T Server and running from a Windows Computer
Add-Type @" 
    using System; 
    using System.Net; 
    using System.Net.Security; 
    using System.Security.Cryptography.X509Certificates; 
    public class ServerCertificateValidationCallback 
    { 
        public static void Ignore() 
        { 
            ServicePointManager.ServerCertificateValidationCallback +=  
                delegate 
                ( 
                    Object obj,  
                    X509Certificate certificate,  
                    X509Chain chain,  
                    SslPolicyErrors errors 
                ) 
                { 
                    return true; 
                }; 
        } 
    } 
"@  
[ServerCertificateValidationCallback]::Ignore(); 


# ----- [ This section connects you to vCenter ] ------------------------------------------------------------------
$vCenterName = 'vCenter.vCROCS.info'
Connect-VIServer $vCenterName -Credential $cred

# Connect to vCenter and fetch virtual machine info.
$vmInfo = Get-VM -Name DBH-213 | Get-View


# ----- [ This section defines the API header ] ------------------------------------------------------------------
# Set Username/Password info for API
$user = 'srv_vRA_NSXT@vCROCS.info'
$nsxpassword = 'VMware!1'
$pair = "$($user):$($nsxpassword)"
$encodedCredentials = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Pair))
$headers = @{ Authorization = "Basic $encodedCredentials" }

$vmid = $vm.Config.InstanceUuid
$newtag = 'UST.SM.UBUNTU_SERVER'
$JSON = @"
{
    "external_id": "$vmid",
    "tags": [
        {"scope": "", "tag": "$newtag"}
    ]
}
"@

$posturl = "https://$nsxmanager/api/v1/fabric/virtual-machines?action=add_tags"
Invoke-RestMethod -Uri $posturl -Headers $headers -Method Post -Body $JSON -ContentType "application/json"

# ----- [ End Add a Single TAG ] --------------------------------------------------


# ----- [ Start Get NSX-T TAGs assigned to VM ] --------------------------------------------------

$vmid = $vm.Config.InstanceUuid
$geturl = "https://$nsxmanager/api/v1/fabric/virtual-machines?external_id=$vmid&included_fields=tags"
$getrequest = Invoke-RestMethod -Uri $geturl -Headers $headers -Method Get -ContentType "application/json"
$currenttags = $getrequest.results.tags.Tag
$currenttags

# ----- [ End Get NSX-T TAGs assigned to VM ] --------------------------------------------------


# ----- [ Start remove NSX-T TAG from VM ] --------------------------------------------------

$vmid = $vm.Config.InstanceUuid
$newtag = 'UST.SM.UBUNTU_SERVER'
$JSON = @"
{
    "external_id": "$vmid",
    "tags": [
        {"scope": "", "tag": "$newtag"}
    ]
}
"@

$posturl = "https://$nsxmanager/api/v1/fabric/virtual-machines?action=remove_tags"
Invoke-RestMethod -Uri $posturl -Headers $headers -Method Post -Body $JSON -ContentType "application/json"

# ----- [ End remove NSX-T TAG from VM ] --------------------------------------------------


# ----- [ Start Get VMs assigned to a TAG NSX-T ] --------------------------------------------------

$geturl = "https://$nsxmanager/policy/api/v1/infra/tags/effective-resources?scope=&tag=UST.SM.UBUNTU_SERVER"
$result = Invoke-RestMethod -Uri $geturl -Headers $headers -Method Get -Body $JSON -ContentType "application/json"

Write-Host $result.results.target_display_name

# ----- [ End Get VMs assigned to a TAG NSX-T ] --------------------------------------------------


{{< /highlight >}}

---

###### Lessons Learned:
* Very easy to automate NSX-T Security TAG processes after you learn the urls.
* NSX-T API documentation is easily accessed and well documented.

---

###### Salt Links I found to be very helpful:
* [SaltStack Cheat Sheet](https://sites.google.com/site/mrxpalmeiras/saltstack/salt-cheat-sheet)
* [SaltStack Tutorials](https://docs.saltproject.io/en/getstarted/)
* [SaltStack Documentation](https://docs.saltproject.io/en/latest/contents.html)
* [SaltStack Community Slack Channel](https://saltstackcommunity.slack.com)

---  

* If you found this Blog article useful and it helped you, Buy me a coffee to start my day.  

<center>
<script type="text/javascript" src="https://cdnjs.buymeacoffee.com/1.0.0/button.prod.min.js" data-name="bmc-button" data-slug="dalehassinger" data-color="#FFDD00" data-emoji=""  data-font="Cookie" data-text="Buy me a coffee" data-outline-color="#000000" data-font-color="#000000" data-coffee-color="#ffffff" ></script>
</center>

---

{{< cusdis >}}