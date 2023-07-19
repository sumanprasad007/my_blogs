---
title: "Setting Up Azure DevOps Agents on Windows ✨"
datePublished: Wed Jul 19 2023 03:41:56 GMT+0000 (Coordinated Universal Time)
cuid: clk96g3fm000k09mm3jqsapj2
slug: setting-up-azure-devops-agents-on-windows
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689737434510/8e3a783f-1cf1-415c-9aa0-02414c16f58d.png
tags: azure, developer, windows, devops, 90daysofdevops

---

## **📍**Introduction:

Azure DevOps is a powerful platform for managing and automating software development processes. To effectively utilize its features, it is essential to set up agent pools that enable the execution of pipelines and jobs. In this blog post, we will guide you through the process of setting up an agent pool on a Windows and resolving the common error message "No hosted parallelism has been purchased or granted." Let's get started! 🚀

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689737523906/3de0631c-0c2c-4751-a28b-5652221015a8.png align="center")

### **🔄** Step 1: Setting up Agent Pool on Windows 🖥️

🔹 Log in to Azure DevOps and navigate to your project.

🔹 Go to Settings, then Agent Pools.

🔹 Select the default agent pool and click on the "Get the agent" button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689737753160/892161e7-0c56-4b48-a06e-24b7e82d4418.png align="center")

### **🔄** Step 2: Downloading and Configuring the Agent 💾

🔹 Download the agent file onto your Windows machine.

🔹 Open PowerShell with administrative access.

🔹 Navigate to a suitable location where you want to set up the agent by running the following command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689737561449/cae9537b-5a6f-43dc-95c0-0277bfc656b4.png align="center")

```plaintext
cd ../..
```

🔹 Create a new directory for the agent and navigate into it:

```plaintext
mkdir agent_new ; cd agent_new
```

🔹 Extract the agent files from the downloaded ZIP archive using the following PowerShell command:

```plaintext
Add-Type -AssemblyName System.IO.Compression.FileSystem
[System.IO.Compression.ZipFile]::ExtractToDirectory("$HOME\Downloads\vsts-agent-win-x64-3.220.5.zip", "$PWD")
```

Note: Adjust the ZIP file name and version number according to the agent you downloaded

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689737614922/0d69e4f2-cd39-4f9f-b0a5-8324aae4e340.png align="center")

### **🔄** Step 3: Configuring and Running the Agent ⚙️

🔹 In the same PowerShell session, run the configuration script:

```plaintext
.\config.cmd
```

🔹 Follow the instructions provided by the configuration script to set up the agent. Enter the URL of your Azure DevOps server, select the agent pool, and provide a unique agent name when prompted.

🔹 Once the configuration is complete, run the following command to start the agent:

```plaintext
.\run.cmd
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689737661304/dd6c87c8-b13d-44c1-b15a-988ce9211d3d.png align="center")

### **🔄** Alternative Method: If you prefer a simpler approach, you can use the following steps:

🔹 Download the agent file and extract it to a suitable location on your Windows.

🔹 Open PowerShell with administrative access and navigate to the agent's directory.

🔹 Run the following commands:

```plaintext
arduinoCopy code.\config.cmd
.\run.cmd
```

### **🔄** Verification:

After the agent is successfully running, it will be listening for jobs from Azure DevOps. You can confirm its status by checking the agent pool in Azure DevOps, where the agent should appear online. ✔️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689737688884/cfe08ab9-45dd-4705-ae6e-03e362a7f038.png align="center")

## **📍** Conclusion:

By following the steps outlined in this blog post, you have learned how to set up an agent pool on a Windows in Azure DevOps. Additionally, we have resolved the common error message related to parallelism grants. Now you can confidently execute your pipelines using the default agent without encountering the mentioned errors. Thank you for reading this blog post, and we hope it has been valuable in helping you set up your Azure DevOps environment! ✅🙌

### **🔍 Thumbnail Image credits:**

[https://zoomspeaks.tech/assets/images/posts/2021/2021-05-04-configuring-azure-devops-vmss-agent-pool.png](https://zoomspeaks.tech/assets/images/posts/2021/2021-05-04-configuring-azure-devops-vmss-agent-pool.png)

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689575367342/b8274e1e-eef6-4cdb-9cf6-9a66ba1c9c15.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

%[https://youtu.be/jC0McFPuTzA] 

###