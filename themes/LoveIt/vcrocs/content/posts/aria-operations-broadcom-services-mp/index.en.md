---

weight: 1
title: "VMware Aria Operations | Broadcom Services | Management Pack"
date: 2024-04-01T00:00:00+00:00
lastmod: 2024-04-01T00:00:00+00:00
draft: false
author: "Dale Hassinger"
authorLink: "https://twitter.com/dalehassinger"
description: ""
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["VMware", "VMware Aria Operations", "Management Pack", "Broadcom Services", "Management Pack Builder"]
categories: ["VMware Aria Operations"]

lightgallery: true

---

**How to use the VMware Aria Operations Management Pack Builder for Day 2 monitoring**

<!--more-->

---

###### VMware Aria Operations  

VMware Aria Operations 8.16.0 and Management Pack Builder 1.1.2 was used for this Blog Post. When new versions of VMware Aria Operations or the MP Builder are released, the code or process may need to be changed. 

---

{{< image src="mp-builder-01.png" caption="Click to see Larger Image of Screen Shot">}}  

---


I wanted to share how I created a VMware Aria Operations Management Pack to use with the Broadcom Service Status web site, [status.broadcom.com](https://status.broadcom.com). This web site shows the current status of all Broadcom Services, Broadcom Software Group or VMware Software. As a VCF Specialist, my first thought when I saw that this web site provided API access, was to create a Aria Operations Management Pack.  

When Aria Operations is pulling in the status of the Broadcom Services with a Management Pack, that will enable you to create Alerts, Dashboards, Views, Reports, etc... that are important to your environment. If you are a VMware customer, monitoring the "VMware Cloud Services" may be important to you. I am going to show how I created the Management Pack using the MP Builder and some of the custom items I created in Aria Operations. I like to use Aria Operations as the "Single Pane of Glass" for monitoring.  

Please keep this in mind after reading the details of the Blog Article. The Management Pack Builder is Designed to allow you to bring data into Aria Operations, using an API, that is important to your Environment. This is a simple example of how Powerful the MP Builder can be. Other items that could be monitored with a MP could be: Temperatures of Networking closets or Data Centers (if you have a temperature senor with API capabilities), weather conditions around your physical DC locations (There are Web Sites that allow API weather updates), Storage/Compute/Networking that doesn't have a VMware provided MP, etc... So many use cases!  

---

**See how the items show in Object Browser:**
{{< image src="mp-builder-02.png" caption="Click to see Larger Image of Screen Shot">}}  

---

**Dashboard to show the Broadcom Service Statuses:**
{{< image src="mp-builder-03.png" caption="Click to see Larger Image of Screen Shot">}}  

---

**Views created to use with the Dashboard:**
{{< image src="mp-builder-04.png" caption="Click to see Larger Image of Screen Shot">}}  

---

**YouTube Video to show how I created the Management Pack using MP Builder:**

---

{{< image src="mp-builder-05.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-06.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-07.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-08.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-09.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-10.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-11.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-12.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-13.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-14.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-15.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-16.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-17.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-18.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-19.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-20.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-21.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-22.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-23-1.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-23-2.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-23-3.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-24.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-25.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-26.png" caption="Click to see Larger Image of Screen Shot">}}  

---

{{< image src="mp-builder-27.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Objects:
{{< image src="mp-builder-28.png" caption="Click to see Larger Image of Screen Shot">}}  

---

I like to pick a icon that represents the Object.
{{< image src="mp-builder-29.png" caption="Click to see Larger Image of Screen Shot">}}  

---

Select all attributes per the screen shot.
{{< image src="mp-builder-30.png" caption="Click to see Larger Image of Screen Shot">}}  

---

Make sure all items are marked as property.
{{< image src="mp-builder-31.png" caption="Click to see Larger Image of Screen Shot">}}  

---

Make sure instance name is "Name" and Identifiers is "ID".
{{< image src="mp-builder-32.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Relationships:
{{< image src="mp-builder-33.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Events:
{{< image src="mp-builder-34.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Content:
{{< image src="mp-builder-35.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Configuration:
{{< image src="mp-builder-36.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Perform Collection:
{{< image src="mp-builder-37.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### Perform Collection Complete:
{{< image src="mp-builder-38.png" caption="Click to see Larger Image of Screen Shot">}}  

---

###### MP Build Complete:
Select Download to be able to add your your Aria Operations.
{{< image src="mp-builder-39.png" caption="Click to see Larger Image of Screen Shot">}}  

---






###### Links to resources about VMware Aria Operations Management Pack Builder:
* [Brock Peterson Blog Post | vROps Management Pack Builder](https://www.brockpeterson.com/post/vrops-management-pack-builder).  
* [YouTube | VMware Aria Management Pack Builder v1.1](https://www.youtube.com/playlist?list=PLrFo2o1FG9n4gQ60pa8CjpTDbgpUz5Hrt).  
* [GitHub Repository where you can download the Manage Pack, Dashboard and Views](https://github.com/dalehassinger/unlocking-the-potential)




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
