---
weight: 1
title: "PowerCLI Getting Started"
date: 2020-04-19T00:00:00+00:00
lastmod: 2020-04-19T00:00:00+00:00
draft: false
author: "Dale Hassinger"
authorLink: "https://twitter.com/dalehassinger"
description: ""
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["PowerShell", "PowerCLI"]
categories: ["VCF Automation"]

lightgallery: true

---

**PowerCLI Basics**

<!--more-->

---

###### PowerCLI Code

Some basic PowerCLI commands to get started. I have some simple scripts in production that are 10 lines of code and I have some scripts that do a lot that are 2500 lines of code. Take the time to learn all the commands that are available and you will be amazed at what you can automate.

---

{{< highlight powershell >}}

#Here are some basic commands that you can keep adding additional code
#and get more precise on what you want to see.

#Connect to a vCenter

Connect-VIServer vcsa.domain.org

#Disconnect from vCenter and not be prompted

Disconnect-VIServer vcsa.domain.org -confirm:$false

#Get VM Listing

#Shows all VMs
Get-VM

#Shows all VMs sorted by Name
Get-VM | Sort-Object Name

#Shows all VMs sorted by Name that are Powered On
Get-VM | Where-Object {$_.Powerstate -eq 'PoweredOn'} | Sort-Object Name

#Shows all VMs sorted by Name, that are Powered On and only shows
#Name,MemoryGB,NumCpu
Get-VM | Where-Object {$_.Powerstate -eq 'PoweredOn'} | Sort-Object Name | Select-Object Name,MemoryGB,NumCpu

{{< /highlight >}}

---

###### Why use PowerCLI  

Picking a scripting language for automation can be a hard decision. My #1 reason to use PowerShell was because of the PowerCLI PowerShell module that VMware maintains. You can use the PowerCLI module to automate almost all of the VMware Products.  

There hasn't been any automation process that I have not been able to use PowerShell to automate. PowerShell has a great collection of modules available to use with different products. PowerShell is also easy to use with Products that make APIs available.

---

**Happy Scripting!**

---

* If you found this Blog article useful and it helped you, Buy me a coffee to start my day.  

<center>
<script type="text/javascript" src="https://cdnjs.buymeacoffee.com/1.0.0/button.prod.min.js" data-name="bmc-button" data-slug="dalehassinger" data-color="#FFDD00" data-emoji=""  data-font="Cookie" data-text="Buy me a coffee" data-outline-color="#000000" data-font-color="#000000" data-coffee-color="#ffffff" ></script>
</center>

---

{{< cusdis >}}