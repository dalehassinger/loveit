---
weight: 1
title: "Unlocking the Potential | VMware Aria Operations | Automation Central | VM Snaps"
date: 2023-05-13T00:00:00+00:00
lastmod: 2023-05-13T00:00:00+00:00
draft: false
author: "Dale Hassinger"
authorLink: "https://twitter.com/dalehassinger"
description: ""
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["VMware Aria Operations", "Snaps", "Automation"]
categories: ["VCF Operations"]

lightgallery: true
---

**Adding "DoNotDelete" to a VM Snap Name to control if Auto Deleted.**

<!--more-->

---

###### VMware Aria Operations 8.12 Released:

With the release of VMware Aria Operations 8.12, "Snapshot Name" was added to "Delete old snapshots".  

---

{{< image src="aria-operations-01.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Delete old snapshots:  

Adding "Snapshot Name" to "Delete old snapshots" in Automation Central may seem like a small change but it adds a lot of Power to the process. This change allows you to create a Job to run everyday that will delete all Snaps on VMs EXCEPT Snaps that have "DoNotDelete" in the name.  

---

- [x] You could also do the opposite with this process. You can have the job only delete Snapshots where the Snap Name contains the text "AutoDelete".   

---

{{< image src="aria-operations-03.png" caption="Click to see Larger Image of Screen Shot">}}  

---

I prefer using the method to auto delete all old VM snaps, unless you tell me not to. After being a VMware administrator for many years, I have seen to many VMs running with snaps older that 30 days or even with multiple snaps running and each snap 60+ days old. That is NOT best practice. VM Snaps are NOT Backups. Using Automation Central within VMware Aria Operations helps you keep your environment running better and helps you follow some best practice rules.

---

###### Schedule, Report, History amd Jobs

Here are the screens you will see in Automation Central, Schedule, Report, History amd Jobs.  
- [x] Schedule:  Nice calendar view of all scheduled jobs.
- [x] Report: Shows you how much storage you were able to re-claim by deleting old snaps.  
- [x] History: Shows you every time a Snap was deleted with details.  
- [x] Jobs: List of all Jobs you created.  

---

{{< image src="aria-operations-02.gif" caption="Click to see Larger Image of Screen Shot">}}  


---

###### Lessons Learned

{{< admonition type=info title="Lessons Learned:" open=true >}}
* Using the VMware Aria Operations Automation Central is a great way to keep snapshots cleaned up on VMs.
* Add the text "DoNotDelete" to the Snap Name, makes an easy way to save Snaps that shouldn't be auto deleted.
* Overall nice new feature added to VMware Aria Operations 8.12.

{{< /admonition >}}

---

###### Links I found to be very helpful:
* <a href="https://blogs.vmware.com/management/2023/04/whats-new-in-vmware-aria-operations-8-12.html" target="_blank">VMware Blog: What’s New in VMware Aria Operations 8.12</a>

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

{{< cusdis >}}