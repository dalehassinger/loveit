---

weight: 1
title: "VCF Operations | Zoom MP"
date: 2025-04-20T00:00:00+00:00
lastmod: 2025-04-20T00:00:00+00:00
draft: false
author: "Dale Hassinger"
authorLink: "https://twitter.com/dalehassinger"
description: ""
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["VCF", "Operations", "Zoom", "Management Pack", "VMware Code Coach", "VMware vExpert", "MP"]
categories: ["VCF Operations"]

lightgallery: true

---

**Learn how to monitor SaaS solutions like Zoom by building a custom Management Pack.**

<!--more-->

---

>You start to see the true power of VCF Operations when you add Management Packs (MPs) tailored to the systems your organization needs to monitor.

---

###### Why create and use a Zoom MP:  

I rely on Zoom for daily conference calls. Last week, regional issues prevented users from joining scheduled meetings. This highlighted the need for alerts when SaaS tools experience problems.

While I’ve created dashboards in the past to show the status of SaaS services using the Text Display widget, I wanted to take it a step further and receive email alerts from VCF Operations—just as I do for ESXi hosts, VMs, or storage issues.

To enable this, I built a Management Pack (MP) to bring the data into VCF Operations. Once the data is available, you can create dashboards, views, alerts, and reports—just like you would for any other monitored system.

Creating Management Packs (MPs) with the MP Builder requires making API calls. I did some research and found that Zoom status information is available through a REST API.

I’ve used the MP Builder before for other use cases, so I was already familiar with the process. Building the Zoom MP took about 30 minutes.

See the screenshots and steps below—it’s a straightforward process that anyone can follow.

---

>In 2025, take some time to get hands-on with the MP Builder in VCF Operations. The platform already delivers solid monitoring out of the box, but when you start building your own Management Packs, that’s when it really starts to shine.

---

###### Dashboard Examples:  

* Colors are very poweful in VCF Operations. When you see <span style="color:green; font-weight:bold;">Green</span> it's good, while <span style="color:red; font-weight:bold;">Red</span>, <span style="color:orange; font-weight:bold;">Orange</span>, or <span style="color:yellow; font-weight:bold;">Yellow</span> suggests something may need attention.  

---

{{< image src="zoom-mp-01.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Zoom MP Alerts:  

* Screen Shots MP Alert  

---

{{< image src="zoom-mp-21.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Alert Type: "Application: Availability"  

{{< image src="zoom-mp-21-2.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Condition: If "Zoom Meetings" "Status" not equal to "operational"  

{{< image src="zoom-mp-22.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-23.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Select the Policy you want to use  

{{< image src="zoom-mp-24.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Building the MP:  

* Screen Shots creating the MP.  

---

{{< image src="zoom-mp-02.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-03.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Define the source

{{< image src="zoom-mp-04.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-05.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-06.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-07.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-08.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Define the Requests

{{< image src="zoom-mp-09.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-10.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-11.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Define the Objects

{{< image src="zoom-mp-12.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-13.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* I only pick the fields that I want to be included in VCF Operations. You do NOT have to pick all fiields.


{{< image src="zoom-mp-14.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-15.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-16.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Set default values for the MP

{{< image src="zoom-mp-17.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-18.png" caption="Click to see Larger Image of Screen Shot">}}  

---

* Perform a Collection and then Build

{{< image src="zoom-mp-19.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="zoom-mp-20.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Lessons Learned:

* Management Packs (MPs) provide a way to monitor components that aren’t included by default.  
* MPs provide a good way for you to Alert your Team when SaaS type solutions also have issues.  
* MPs are straightforward to build. Once you understand how the APIs work, you can create powerful integrations.  


---

MP Download coming soon...   

---

{{< admonition type=info title="Info" open=true >}}
In my blogs, I often emphasize that there are multiple methods to achieve the same objective. This article presents just one of the many ways you can tackle this task. I've shared what I believe to be an effective approach for this particular use case, but keep in mind that every organization and environment varies. There's no definitive right or wrong way to accomplish the tasks discussed in this article.
{{< /admonition >}}

---

{{< admonition type=warning title="Lab" open=true >}}
Always test new setups and processes, like those discussed in this blog, in a lab environment before implementing them in a production environment.
{{< /admonition >}}

---

{{< admonition type=tip title="Tips and Tricks" open=true >}}
If you found this blog helpful, consider buying me a coffee to kickstart my day.  
{{< /admonition >}}

<center>
<script type="text/javascript" src="https://cdnjs.buymeacoffee.com/1.0.0/button.prod.min.js" data-name="bmc-button" data-slug="dalehassinger" data-color="#FFDD00" data-emoji=""  data-font="Cookie" data-text="Buy me a coffee" data-outline-color="#000000" data-font-color="#000000" data-coffee-color="#ffffff" ></script>
</center>

---

{{< cusdis >}}