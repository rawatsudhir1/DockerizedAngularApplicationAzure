Deploy Dockerized Angular Application to Azure 
===============================================

Introduction
============

Your organization running angular web application to help their
customer. The entire setup is running on their premises. Company
business is growing hence facing various challenges like

-   High Availability: - To make sure service up and running all the
    time. Unavailability of service impact customer experience and
    business continuity

-   Increase in Infrastructure Cost: - There always a mismatch on
    infrastructure purchase vs. usage.

-   Fault Tolerance: - Make sure service is up and running even if some
    of the service is not functioning properly

-   Scalability: - Auto scale based on the network traffic.

-   Security: - Keep infrastructure and services secure

-   Latency: - How to reduce latency in the application

-   Quicker release cycle: -

-   Global reach: - Ability to reach global audience

> And so on...

The organization appoints you to overcome all the challenges. You
suggested to move entire application to Azure so that organization can
focus on their business. In this hands on lab we'll see how you can move
customer existing Angular based application as it is (or with minimum
changes) to Azure.

Prerequisite
============

-   VS Code 2017

-   Docker

-   Azure Subscription

Architecture
============

![](media/image1.png){width="6.5in" height="3.7881944444444446in"}

LAB
===

In step 1 we'll setup Azure virtual machine on Azure and install VS code
and Docker hub there. Step 2 involves develop, dockerized image and
deploy image to Docker Hub. Step 3 we'll setup WebApp for containers,
pull image from docker and test the sample app.

Step 1: - Setup Azure VM, Install VS Code and Docker hub
--------------------------------------------------------

-   Login to <https://ms.portal.azure.com>

-   Click **Create a resource** and search for Windows Client

> ![](media/image2.png){width="5.859418197725284in"
> height="1.4323020559930009in"}

-   Click **Windows Client**

-   Click **Create**

    ![](media/image3.png){width="6.5in" height="1.5395833333333333in"}

-   On next screen, select **Subscription** (choose the one you got it
    during the workshop)

-   Click **Create new** Resource group. Give a name and click OK

-   Provide **Virtual machine name**

-   Select **Region** which is near to your location

-   Keep default value for Availability options, Image and size

-   Provide Username, Password and Confirm Password. Keep a note of it
    as it will be used for RDP

-   Select **Allow selected ports** as **Public Inbound ports**

-   Select RDP as **Select inbound ports**

    ![](media/image4.png){width="6.5in" height="7.264583333333333in"}

-   Click **Next: Disks \>**

-   Select **Standard HDD** as **OS disk type**

    ![](media/image5.png){width="6.5in" height="3.3847222222222224in"}

-   Click **Review + Create**

-   Click **Create** once **Validation passed**

-   Once deployment is successful, click on **Go to resource**

    ![](media/image6.png){width="6.5in" height="4.377083333333333in"}

-   Click **Connect**

    ![](media/image7.png){width="4.421907261592301in"
    height="2.9948140857392826in"}

-   Click **Download RDP File**

    ![](media/image8.png){width="4.453157261592301in"
    height="3.994820647419073in"}

-   Save the RDP connection

    ![](media/image9.png){width="6.5in" height="0.44166666666666665in"}

-   Once saved, open the RDP connection file

    ![](media/image10.png){width="5.552123797025372in"
    height="2.8333541119860017in"}

-   Click **Connect** and log into the VM

-   Once logged in to the VM, open a browser and go to
    <https://code.visualstudio.com/download>

![](media/image11.png){width="5.739583333333333in"
height="2.985074365704287in"}

-   Click **User Installer** 64 bit and install VS code

-   Once VS code installation is complete, switch to browser and go to
    <https://docs.docker.com/v17.09/docker-for-windows/install/#download-docker-for-windows>
    to install docker on windows

-   Click **Get Docker for Windows (Stable)**

    ![](media/image12.png){width="4.192739501312336in"
    height="3.984403980752406in"}

-   Install docker for windows. On the last step, keep default option
    selected and click **Ok**

    ![](media/image13.png){width="6.5in" height="4.4534722222222225in"}

-   Once installation is done, click **Close and log out**

    ![](media/image14.png){width="5.760459317585302in"
    height="3.671901793525809in"}

-   Once login back in the VM, you will notice Docker for windows is
    getting started

    ![](media/image15.png){width="3.4323162729658794in"
    height="1.7291797900262467in"}

-   Docker requires Hyper-V to be enable in VM. If you get below
    message, please click **Ok.** It will take some time

    ![](media/image16.png){width="6.5in" height="2.3895833333333334in"}

-   RDP again to Virtual machine

-   Once docker is up and running, it will prompt below message

    ![](media/image17.png){width="3.6302351268591426in"
    height="3.5989851268591426in"}

-   If you haven't have any docker account then create one at
    hub.docker.com. That account you will use to deploy your Angular
    image at docker hub (kind of repository for all your images).

-   Once you logged in, Right click on docker icon at system tray

    ![](media/image18.png){width="2.6979363517060366in"
    height="3.036480752405949in"}

-   Make sure you successfully logged in and it's running linux
    container and not windows.

-   Install Node.js runtime from <https://nodejs.org/en/download/>

-   Search for "Visual studio code", right click and run it as
    Administrator

> ![](media/image19.png){width="2.4218755468066493in"
> height="4.147774496937883in"}

-   Once Visual Studio Code opens click **Extensions** on left side
    panel

-   Click on **Extensions** and search for Docker

    ![](media/image20.png){width="3.9479451006124235in"
    height="3.95836176727909in"}

-   Click **Install**

-   Once installation is done, the screen will look like below

    ![](media/image21.png){width="6.5in" height="2.029861111111111in"}

-   Close and open Visual studio again (as run as administrator).

-   You were successfully able to setup VS code and docker

Step 2: - Develop, Dockerized image and deploy

-   On Visual Studio Code user interface, click **Terminal** and select
    **New Terminal**

    ![](media/image22.png){width="4.562533902012248in"
    height="3.7500273403324584in"}

-   If framework opens up PowerShell terminal then you can switch to
    command prompt. Click on **Customize** option for the prompt

    ![](media/image23.png){width="4.73961832895888in"
    height="1.0520909886264218in"}

-   Select **Command Prompt**

    ![](media/image24.png){width="6.5in" height="1.0555555555555556in"}

-   Once terminal opens, you can switch to c:\\ (if by default it's not
    there)

    ![](media/image25.png){width="4.390657261592301in"
    height="1.312509842519685in"}

-   Type **npm install -g \@angular/cli** and press Enter

![](media/image26.png){width="5.11982939632546in"
height="1.6927209098862641in"}

-   Type **ng new my-app** and press Enter. Select y for "**Would like
    to add Angular routing**" and press Enter for CSS (which default)
    for "**Which stylesheet format would like to use?**"

    ![](media/image27.png){width="6.5in" height="1.948611111111111in"}

-   Once process is done, it will add a new folder called **my-app** in
    the same folder. From left menu bar, click **Open Folder**

    ![](media/image28.png){width="3.708360673665792in"
    height="3.4010662729658794in"}

-   Select the **my-app** folder from the path

    ![](media/image29.png){width="6.5in" height="5.698611111111111in"}

-   Click **Select Folder**

-   Open ./src/app/app.component.ts.

-   Change the title property from \'my-app\' to \' \"Deploy Dockerized
    Angular Application to Azure\" Lab!!! \'.

    ![](media/image30.png){width="6.5in" height="2.4680555555555554in"}

-   Let's compile and run the application

-   In terminal window, type **ng serve** and press **Enter**

    ![](media/image31.png){width="6.5in" height="3.0590277777777777in"}

-   Open a browser and type http://localhost:4200

> ![](media/image32.png){width="6.5in" height="2.2527777777777778in"}

-   Switch to terminal and click CTRL+C to stop Angular runtime

-   Click **New File** icon, beside **My-App** folder

    ![](media/image33.png){width="3.22919072615923in"
    height="3.0104385389326334in"}

-   Provide file name as **Dockerfile**

    ![](media/image34.png){width="3.2864818460192478in"
    height="3.6562762467191603in"}

-   Copy and paste below code in **Dockerfile**

-   Save the file

-   Let's build the app. Type **ng build \--prod**

    ![](media/image36.png){width="6.5in" height="1.9388888888888889in"}

-   Once done. Let's build docker image

-   Right click on Dockerfile and click **Build Image**

    ![](media/image37.png){width="3.3096292650918637in"
    height="4.244792213473316in"}

-   Change the tag if you want and click **Enter**

    ![](media/image38.png){width="6.4062970253718285in"
    height="0.7500054680664917in"}

-   The command will start building image. Wait for sometime while it's
    building the image.

    ![](media/image39.png){width="6.5in" height="6.419444444444444in"}

-   Let's check if docker image is created or not

-   Type **docker images** and press **Enter**

    ![](media/image40.png){width="6.5in" height="1.51875in"}

-   To run docker image, type **docker run -d -p 3000:80 \--rm
    my-app:latest**

    ![](media/image41.png){width="5.807333770778652in"
    height="0.8645898950131233in"}

-   Type **docker container ls -a** and press
    **Enter**![](media/image42.png){width="6.5in"
    height="0.9659722222222222in"}

-   Open a browser, type **<http://localhost:3000/>** and press Enter

    ![](media/image43.png){width="6.5in" height="2.4763888888888888in"}

-   To stop docker container, type **docker stop \<CONTAINER ID\>**

    ![](media/image44.png){width="4.000029527559055in"
    height="0.63542104111986in"}

-   Run **docker container ls -a** to check if container is stop or
    not**.** It will show no record which means no container is running.

-   Switch to browser and refresh the page or type
    <http://localhost:3000>. Since no container is running hence you see
    **"Can't reach the page"**

    ![](media/image45.png){width="6.5in" height="2.9298611111111112in"}

-   Let's deploy docker image to docker hub

-   Let's login to docker hub. Type **docker login**

    ![](media/image46.png){width="3.83336176727909in"
    height="1.0156321084864393in"}

-   Since you are already login in docker hub, it checks against
    existing login.

-   First tag the image. Type **docker tag 'IMAGE ID'
    'DOCKER\_HUB\_NAME/IMAGE\_NAME:TAG\_NAME'**

    ![](media/image47.png){width="6.5in" height="1.80625in"}

-   Push the image, Type docker push
    **'DOCKER\_HUB\_NAME/IMAGE\_NAME:TAG\_NAME'**

> ![](media/image48.png){width="6.5in" height="1.7534722222222223in"}

-   Open a browser, type hub.docker.com. Once login, see all the
    repository

    ![](media/image49.png){width="6.5in" height="1.6576388888888889in"}

-   Great! You deployed your docker image to docker hub.

Step 3:- Setup Azure Web App for containers and Access the website

-   Open browser and type <https://portal.azure.com> . Login with the
    credential which is used to setup the subscription

-   Click **Create a resource,** type web and click **Web App for
    Containers **

    ![](media/image50.png){width="5.531290463692039in"
    height="4.1302384076990375in"}

-   Click **Create**

    ![](media/image51.png){width="6.5in" height="4.76875in"}

-   Type **App name**, select **Subscription**, create or select
    **Resource group**, select **Linux** as **OS**

    ![](media/image52.png){width="3.244815179352581in"
    height="5.598999343832021in"}

-   Click **Configure container**

-   Click **Docker Hub** as **Image source**

-   Select **Public** as **Repository Access**

-   Provide Image and tag name

    ![](media/image53.png){width="6.5in" height="3.7055555555555557in"}

-   Click **Apply**

-   Click **Create**

-   Wait while Azure makes your application deployed and configured.

-   Check notification option to check the status

    ![](media/image54.png){width="3.35419072615923in"
    height="2.7968952318460194in"}

-   **Pin to dashboard** if you like and open the tile else **go to
    resource**

    ![](media/image55.png){width="2.328141951006124in"
    height="2.1666819772528436in"}

-   On the overview page, copy **URL**

    ![](media/image56.png){width="6.916476377952756in"
    height="1.2916666666666667in"}

-   Open the browser and paste the url in address bar, press **Enter**

    ![](media/image57.png){width="6.5in" height="2.6243055555555554in"}

-   Hurray!!! You successfully able to Deploy Dockerized Angular
    Application to Azure.

Cleanup
=======

-   Please delete all the resources from the Azure portal to avoid any
    charges to your subscription
