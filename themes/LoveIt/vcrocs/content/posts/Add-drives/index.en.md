---
weight: 1
title: "Add disk to a Remote Windows Server | VMware VM"
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

tags: ["PowerShell", "PowerCLI", "Add Disk", "Windows Server"]
categories: ["VCF Automation"]

lightgallery: true

---

**Add disk to a Remote Windows Server | VMware VM**

<!--more-->

---

###### PowerShell Code

Powershell code to add disk to a Remote Windows Server | VMware VM:  

---

{{< highlight powershell >}}

#The Following code shows how to add a New Drive, bring drive online, initialize and format:

#Connect to vCenter
Connect-VIServer vCenter.vCROCS.info 

#Add new drive to VM
New-HardDisk -VM $VMNAME -CapacityGB $DISKSIZEGB -StorageFormat Thin -Controller ‘SCSI Controller 1’

#Make disk online
invoke-command -computername $VMNAME -scriptblock {Set-Disk 2 -isOffline $false}

#Initialize disk
invoke-command -computername $VMNAME -scriptblock {Initialize-Disk 2 -PartitionStyle GPT}

#Create Partition
invoke-command -computername $VMNAME -scriptblock {New-Partition -DiskNumber 2 -UseMaximumSize -DriveLetter E}

#Format drive
invoke-command -computername $VMNAME -scriptblock {Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel ‘Data’ -AllocationUnitSize 16384 -Confirm:$false}

#-------------------------------------------------------------------------

#The Following Code will show disk “Allocation Unit Size” on a remote Windows Server:

$C = Invoke-Command -ComputerName $VMname {Get-WmiObject -Class Win32_Volume -Filter “DriveLetter = ‘C:'” | Select-Object BLOCKSIZE}
$C_AllocationUnitSize = ($C.BLOCKSIZE/1024)
$C_AllocationUnitSize = ‘Disk Allocation Unit Size: ‘ + $C_AllocationUnitSize + ‘k’
$C_AllocationUnitSize

{{< /highlight >}}

---

* If you found this Blog article useful and it helped you, Buy me a coffee to start my day.  

<center>
<script type="text/javascript" src="https://cdnjs.buymeacoffee.com/1.0.0/button.prod.min.js" data-name="bmc-button" data-slug="dalehassinger" data-color="#FFDD00" data-emoji=""  data-font="Cookie" data-text="Buy me a coffee" data-outline-color="#000000" data-font-color="#000000" data-coffee-color="#ffffff" ></script>
</center>

---

{{< cusdis >}}