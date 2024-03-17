---

weight: 1
title: "VMware Aria Automation | How to send messages and updates"
date: 2024-03-17T00:00:00+00:00
lastmod: 2024-03-17T00:00:00+00:00
draft: false
author: "Dale Hassinger"
authorLink: "https://twitter.com/dalehassinger"
description: ""
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["VMware", "VMware Aria Automation", "Teams Messages", "Google Spaces", "Alerts", "Messages"]
categories: ["Automation"]

lightgallery: true

---

**How to send messages/updates to a Teams Channel or Google Spaces.**

<!--more-->

---

>"If everyone is moving forward together, then success takes care of itself.” — Henry Ford

---

###### VMware Aria Automation  

When new VMs are created or you run Day 2 operations from the VMware Aria Automation Catalog, I always like to send a message to a shared message system to keep the team up to date on what is being created or changed. For this Blog I am going to show example code to send messages to Microsoft Teams and Google Spaces using a Webhook. You can use this concept to send to any message system like Slack, Zoom, Discord, etc... You would just need to change the code that formats the json body that sends the message.  

I am going to show how to send messages from VMware Aria Automation using ABX Actions and Orchestrator Workflows. The process is similar but the code is slightly different on how to get Property Values. I think is will be nice to show both ways and let it up to you, the Automation Experts, to pick what works best for your processes. I always say with Automation, there is a 100 ways to do the same thing.  

---

For this Blog I am going to create a new VM. When the build process starts I will have a Extensibility Subscription setup that sends a message to Microsoft Teams and Google Spaces using a ABX Action and a Orchestrator Workflow.  

**Steps:**
01. Create a Template within the Design Section of Aria Automation. I will keep it simple for this Blog and create a single Rocky Linux VM. | See "Screen Shot 01"  
02. Make sure all the Properties that you want to display on the message is included in the Template YAML Code. Property Values will be passed to the ABX Actions and Orchestrator Workflows. | See "Screen Shot 02"  
  - You can add any Property you want to the messages. Make sure the Property is listed in the Template YAML Code.  
03. Create a Extensibility Action. | See "Screen Shot 03 and 04"  
04. Create a Extensibility Subscription to run the ABX Action or Orchestrator Workflow. | See "Screen Shot 05"  
05. Subscription definition example. | See "Screen Shot 06"  
06. Create a new VM Deployment and verify that the Subscription ran the ABX Action that you have defined.  
07. Verify that the message showed up in your message system of choice.  
08. If everything worked, time to celebrate!



---

###### Screen Shots of the Steps:

Design Template with YAML Code that has all the required Properties.

Screen Shot 01:  

{{< image src="aria-automation-messages-01.png" caption="Click to see Larger Image of Screen Shot">}}  

---

**Design Template Example YAML Code:**  

This YAML code shows all the Properties that I want to send to a ABX Action or Orchestrator Workflow.  

Click arrow to expand the code:  

{{< highlight YAML >}}  
formatVersion: 1
name: Ubuntu-20-with-minion
version: 9
inputs:
  CustomizationSpec:
    type: string
    description: Customization Specification
    default: Customization-Ubuntu-22
    title: 'Customization Spec:'
  VMName:
    type: string
    title: 'VM Name:'
    minLength: 1
    maxLength: 15
    default: LINUX-U-16
  IP:
    type: string
    default: 192.168.69.16
  BuildTime:
    type: string
    title: 'Build Time:'
    format: date-time
  vCenterFolders:
    type: string
    title: 'vCenter Folder:'
    default: Blogs
    $dynamicEnum: /data/vro-actions/TAM/DBH_vCenter_Folders
resources:
  Cloud_vSphere_Machine_1:
    type: Cloud.vSphere.Machine
    properties:
      image: vCenter-ubuntu-20
      flavor: vCenter-1CPU-2GB
      name: ${input.VMName}
      BuildTime: ${input.BuildTime}
      folderName: ${input.vCenterFolders}
      customizationSpec: ${input.CustomizationSpec}
      vmIP: ${input.IP}
      remoteAccess:
        authentication: usernamePassword
        username: administrator
        password: VMware1!
      constraints:
        - tag: Cluster:PROD
      networks:
        - network: ${resource.Cloud_vSphere_Network_1.id}
          assignment: static
          address: ${input.IP}
  Cloud_vSphere_Network_1:
    type: Cloud.vSphere.Network
    properties:
      networkType: existing
      constraints:
        - tag: Network:vCenter-VMs

{{< /highlight >}}  


---

Highlight of YAML Code showing Properties.

Screen Shot 02:  
{{< image src="aria-automation-messages-02.png" caption="Click to see Larger Image of Screen Shot">}}  

---

Where to create Extensibility ABX Actions.

Screen Shot 03:  
{{< image src="aria-automation-messages-03-1.png" caption="Click to see Larger Image of Screen Shot">}}  

---

Example Extensibility ABX Action.

Screen Shot 04:  
{{< image src="aria-automation-messages-03-2.png" caption="Click to see Larger Image of Screen Shot">}}  

---

**Extensibility ABX Action Code:**  

Code Examples. The beginning of each ABX Action to get the Property Values is exactly the same. The difference in the code is how to send the information to each message system.  

This code is to send a message to Microsoft Teams.  

Click arrow to expand the code:  

{{< highlight PowerShell >}}  

function handler($context, $inputs) {

    # Build PowerShell variables
    if(!$inputs.resourceNames){
        $vmName = "NA"
    }else{
        $vmName = $inputs.resourceNames
    }
    if(!$inputs.customProperties.image){
        $image = "NA"
    }else{
        $image = $inputs.customProperties.image
    }
    if(!$inputs.customProperties.flavor){
        $flavor = "NA"
    }else{
        $flavor = $inputs.customProperties.flavor
    }
    if(!$inputs.customProperties.folderName){
        $folder = "NA"
    }else{
        $folder = $inputs.customProperties.folderName
    }
    if(!$inputs.customProperties.vmIP){
        $vmIP = "NA"
    }else{
        $vmIP = $inputs.customProperties.vmIP
    }
    if(!$inputs.__metadata.userName){
        $userName = "NA"
    }else{
        $userName = $inputs.__metadata.userName
    }
    
    Write-Host "--vmName:"$vmName
    Write-Host "---image:"$image
    Write-Host "--flavor:"$flavor
    Write-Host "--folder:"$folder
    Write-Host "userName:"$userName
    Write-Host "----vmIP:"$vmIP

    # --- [ Start Add Alert to Teams Channel ] ---
    
    # Define the webhook URL
    $webhookUrl = 'https://vcrocs.webhook.office.com/webhookb2/ac73a8c3-bd4572@015568c1-bbe7-hack-me-4050-add6-6f36b7b44adb/IncomingWebhook/b41cd4d2f-hack-you-12/925b-9960-4590-9251-65db25f05419'

    # --- Create the message card
$messageCard = @{
    "@type"    = "MessageCard"
    "@context" = "http://schema.org/extensions"
    "summary"  = "Issue 176715375"
    "sections" = @(
        @{
            "activityTitle"    = "vRA Automated VM Build:"
            "facts"            = @(
                @{
                    "name"  = "VM Name:"
                    "value" = "$vmName"
                },
                @{
                    "name"  = "VM IP:"
                    "value" = "$vmIP"
                },
                @{
                    "name"  = "Created By:"
                    "value" = "$userName"
                },
                @{
                    "name"  = "VM Image:"
                    "value" = "$image"
                },
                @{
                    "name"  = "vCenter Folder:"
                    "value" = "$folder"
                },
                @{
                    "name"  = "VM Flavor:"
                    "value" = "$flavor"
                }
            )
            "markdown" = $true
        }
    )
} | ConvertTo-Json -Depth 10

    # Send the message card
    Invoke-RestMethod -Uri $webhookUrl -Method Post -ContentType 'application/json' -Body $messageCard

    $outPut = "Done"
    return $outPut
}

{{< /highlight >}}  

---

This code is to send a message to Google Spaces.  

Click arrow to expand the code:  

{{< highlight PowerShell >}}  

function handler($context, $inputs) {

    # Build PowerShell variables
    if(!$inputs.resourceNames){
        $vmName = "NA"
    }else{
        $vmName = $inputs.resourceNames
    }
    if(!$inputs.customProperties.image){
        $image = "NA"
    }else{
        $image = $inputs.customProperties.image
    }
    if(!$inputs.customProperties.flavor){
        $flavor = "NA"
    }else{
        $flavor = $inputs.customProperties.flavor
    }
    if(!$inputs.customProperties.folderName){
        $folder = "NA"
    }else{
        $folder = $inputs.customProperties.folderName
    }
    if(!$inputs.customProperties.vmIP){
        $vmIP = "NA"
    }else{
        $vmIP = $inputs.customProperties.vmIP
    }
    if(!$inputs.__metadata.userName){
        $userName = "NA"
    }else{
        $userName = $inputs.__metadata.userName
    }
    
    Write-Host "--vmName:"$vmName
    Write-Host "---image:"$image
    Write-Host "--flavor:"$flavor
    Write-Host "--folder:"$folder
    Write-Host "userName:"$userName
    Write-Host "----vmIP:"$vmIP

    # --- [ Start Add Alert to Google Chat ] ---
    
    # --- Create json body for Google Alert   
$messageBody = @{
    cards = @(
        @{
            header = @{
                title    = "New VM Build"
            }
            sections = @(
                @{
                    widgets = @(
                        @{
                            keyValue = @{
                                topLabel         = "VM Name:"
                                content          = "$vmname"
                                contentMultiline = $true
                            }
                        },
                        @{
                            keyValue = @{
                                topLabel         = "VM IP:"
                                content          = "$vmIP"
                                contentMultiline = $true
                            }
                        },
                        @{
                            keyValue = @{
                                topLabel         = "Created By:"
                                content          = "$username"
                                contentMultiline = $true
                            }
                        },
                        @{
                            keyValue = @{
                                topLabel         = "VM Image:"
                                content          = "$image"
                                contentMultiline = $true
                            }
                        },
                        @{
                            keyValue = @{
                                topLabel         = "vCenter Folder:"
                                content          = "$folder"
                                contentMultiline = $true
                            }
                        },
                        @{
                            keyValue = @{
                                topLabel         = "VM Flavor:"
                                content          = "$flavor"
                                contentMultiline = $true
                            }
                        }
                    )
                }
            )
        }
    )
}
    
    $jsonMessage = $messageBody | ConvertTo-Json -Depth 10
    
    # Output the JSON to verify
    #$jsonMessage

    # Define the webhook URL (replace it with your actual webhook URL)
    $webhookUrl = 'https://chat.googleapis.com/v1/spaces/AAAAvSYSmfg/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=Vj-NoThfrmjLnkIW_iQRQw71qcE2CGxG1tkjs2ArM7o'

    # Send the message
    $results = Invoke-RestMethod -Uri $webhookUrl -Method Post -Body $jsonMessage -ContentType "application/json"

    #$outPut = "WebHook Date/Time: " + $results.createTime
    #Write-Host $outPut
    
    $outPut = "Done"

  return $outPut
}

{{< /highlight >}}  

---

Subscriptions used to start ABX Actions or Orchestrator Workflows.

Screen Shot 05:  
{{< image src="aria-automation-messages-03.png" caption="Click to see Larger Image of Screen Shot">}}  

---

Subscription definition example.

Screen Shot 06:  
{{< image src="aria-automation-messages-04.png" caption="Click to see Larger Image of Screen Shot">}}  

---

When everything is setup and working correct, this is what a Google Space Message with the New VM Build Details will look like. Very Nice!

Screen Shot ??:  
{{< image src="aria-automation-messages-google-space.png" caption="Click to see Larger Image of Screen Shot">}}  

---

Microsoft Teams Message with New VM Build Details. Very Cool!

Screen Shot ??:  
{{< image src="aria-automation-messages-teams-message.png" caption="Click to see Larger Image of Screen Shot">}}  

---




---



---

---

###### Links to resources discussed is this Blog Post:  
* [Link to my GitHub Repository for sample code like what is included in this Blog Post.](https://github.com/dalehassinger/unlocking-the-potential/)  

---

###### Versions:
VMware Aria Automation 8.16.0 was used for this Blog Post. When new versions of VMware Aria Automation are released, the code or process may need to be changed.  

---

{{< admonition type=info title="Info" open=true >}}
When I write my blogs, I always say there are many ways to accomplish the same task. This article is just one way that you could accomplish this task. I am showing what I felt was a good way to complete the use case but every organization/environment will be different. There is no right or wrong way to complete the tasks in this article.
{{< /admonition >}}

---

* If you found this Blog article useful and it helped you, Buy me a coffee to start my day.  

<center>
<script type="text/javascript" src="https://cdnjs.buymeacoffee.com/1.0.0/button.prod.min.js" data-name="bmc-button" data-slug="dalehassinger" data-color="#FFDD00" data-emoji=""  data-font="Cookie" data-text="Buy me a coffee" data-outline-color="#000000" data-font-color="#000000" data-coffee-color="#ffffff" ></script>
</center>

---
