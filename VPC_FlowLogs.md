
## Part 1 : create a Flow Logs

- Go to Services > Under Management & Governance click "CloudWatch" > Logs > Let's get started<br>

- Create log group > Log Group name: VPC_FlowLogs<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-90.png](https://i.postimg.cc/Yqydmtd7/isaac-arnault-AWS-90.png)](https://postimg.cc/w7LXCYK4)

</p>
</details>

- Go to Services > VPC > Click on VPCs > Select our Custom VPC (myVPC) > Actions > Create flow log<br>

- Filter: select "All" > Destination log group: VPC_FlowLogs > to inform a IAM role click "Setup permissions" <br>

- Leave everything as it is by default and click "Allow"<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-91.png](https://i.postimg.cc/76f34zyT/isaac-arnault-AWS-91.png)](https://postimg.cc/cgGgMrCs)

</p>
</details>

Let's go back to our Flow Logs setup tools and select <b>flowlogsRole</b>.

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-92.png](https://i.postimg.cc/kXcBj50r/isaac-arnault-AWS-92.png)](https://postimg.cc/fJVzyMW5)

</p>
</details>

Go to Management & Governance, click on "CloudWatch" > Logs > VPC_FlowLogs

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-AWS-93.png](https://i.postimg.cc/g0G6KTcD/isaac-arnault-AWS-93.png)](https://postimg.cc/3kbR89v4)

</p>
</details>

If you have no events appearing in <b>Log Streams</b>, you should wait until they appear or you can try opening <b>WebServer-1</b> IPv4 in your browser. This will generate logs and they should appear in your console.<br>

<details>
<summary>🔵 See Log Streams</summary>
<p>

[![isaac-arnault-AWS-94.png](https://i.postimg.cc/RFktwVW3/isaac-arnault-AWS-94.png)](https://postimg.cc/2bx3DYFm)

</p>
</details>

<details>
<summary>🔵 See Logs</summary>
<p>

[![isaac-arnault-AWS-95.png](https://i.postimg.cc/tg17DGQF/isaac-arnault-AWS-95.png)](https://postimg.cc/WDv2bK44)

</p>
</details>


