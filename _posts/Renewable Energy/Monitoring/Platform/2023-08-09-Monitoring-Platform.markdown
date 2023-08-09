---
layout: "post"
title: "Brand Agnostic Monitoring and Control Platform for Renewable Energy Systems"
categories: "RenewableEnergy Monitoring Platform"
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
The idea of the monitoring came from the inability to monitor and control different brands of inverters, batteries, meters, and generator controllers on a single platform. This makes monitoring of these assets virtually impossible, leading to the installer and client being blind to everything happening on site.
<hr>
<p>The solution to this problem has various aspects, all of which will be discussed in extensive detail throughout this post. The aspects are as follows:</p>
<ol>
<li>Node-red</li>
<li>Linux</li>
<li>VPN</li>
<li>MySQL</li>
<li>PLC</li>
<li>Modbus</li>
<li>SCADA</li>
<li>MQTT</li>
<li>Sparkplug B Specification</li>
</ol>
<h3>Points of failure</h3>
<ol>
<li>Communications between PLC and Components</li>
<li>Communications between PLC and Raspberry PI</li>
<li>Communications between Raspberry PI and Cloud</li>
</ol>
<p>These points of failure can happen both when the system wants to read or write data from respective components. Each of these points of failure must have a robust solution to which the system will respond appropriately. More importantly, the system should respond in such a way that no data is lost, and in the case where data could not be measured, the data must be backfilled with the correct values. These factors are crucial to ensure a reliable solution to the problem in which the system responds predictably. If anything happends that was not intended it can lead to damaged equipment, or data loss. The latter will lead to a lack of understanding to what happened on site, bringing us back to the start, where we are blind to what occurs on site.</p>
<h5><i>Communication Loss Between Industrial PC and the Cloud</i></h5>
<p>We must first ask the question what happens when the industrial PC loses connection with the cloud? As the system uses MQTT to send data to the cloud, the connection between the edge device and the cloud will not be there, thus leading to the edge device not being able to push data to the cloud. The data must heap up in temporary database in order to ensure that the undelivered data has been kept track of. As soon as the connection re-establishes, the data must be sent through and deleted from the temporary database. However, this delete function must only occur when acknowledgement on receipt has been received. This can be done by setting an MQTT variable in the MQTT engine which will publish a sparkplug message from the gateway's side.</p>
<br>
<p>Another issue is the one of storing the data in the database when values are backfilled with zero's. This is easy enough to send the values and their corresponding timestamps through. However, the difficult part is to </p>


<span>$$\infty$$<span>