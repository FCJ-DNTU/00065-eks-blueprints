---
title : "Connect SSH from Visual Studio Code to EC2 Instance"  
date : "`r Sys.Date()`"  
weight : 2  
chapter : false  
pre : " <b> 2.2 </b> "
---

#### Connect SSH from Visual Studio Code to EC2 Instance

Connecting SSH from Visual Studio Code to an EC2 Instance is a quick alternative to using Cloud9.

1.  **Download Visual Studio Code and the Remote - SSH extension:**
    
  You can download VS Code here: [Download VSCode](https://code.visualstudio.com/download).
    
  After downloading, install the following extension:
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/001-connectec2.png?featherlight=false&width=90pc)
    
2.  **Open the SSH connection prompt:**
    
  Click on the icon in the lower-left corner of the screen, and a dialog box will appear.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/000-connectec2.png?featherlight=false&width=90pc)
    
3.  **Connect to Host:**
    
  Click on **Connect to Host**.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/002-connectec2.png?featherlight=false&width=90pc)
    
4.  **Add New SSH Host:**
    
  Click on **Add New SSH Host**.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/003-connectec2.png?featherlight=false&width=90pc)
    
5.  **Input SSH Host Name:**
    
  In the input box, enter **eks-blueprint-remote** and press Enter.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/004-connectec2.png?featherlight=false&width=90pc)
    
6.  **Configure SSH in config file:**
    
  Click on the path in **C:\\Users\\ADMIN.ssh\\config** to configure it.
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/005-connectec2.png?featherlight=false&width=90pc)
    
7.  **Update SSH configuration:**
    
  In the newly configured SSH block, update the information with the correct **IPv4 address of the EC2 Instance** and the path to the **Key Pair** on your machine.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/012-connectec2.png?featherlight=false&width=90pc)
    
8.  **Connect to EC2:**
    
  Click on the SSH icon at the bottom left corner and start the connection.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/007-connectec2.png?featherlight=false&width=90pc)
    
9.  **Select Continue:**
    
  Choose **Continue**.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/009-connectec2.png?featherlight=false&width=90pc)
    
10.  **Select Linux:**

  Click on **Linux**

  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/008-connectec2.png?featherlight=false&width=90pc)
    
11.  **Open Folder:**

  Choose **Open Folder** and click **OK**.
    
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/010-connectec2.png?featherlight=false&width=90pc)
    
12.  **Connected Interface:**

  This is what the interface looks like after connection.
  ![Create Workspace](/images/2-prerequiste/2.2-connectec2/011-connectec2.png?featherlight=false&width=90pc)