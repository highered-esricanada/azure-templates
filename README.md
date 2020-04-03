# ArcGIS Desktop VM templates for Azure

These [Azure Resource Manager templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/overview) are configured to launch a VM using an Esri [ArcGIS Desktop](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/esri.arcgis-desktop) image from the Azure Marketplace that is preconfigured with ArcMap 10.8 and ArcGIS Pro 2.4.3 (upgradable to 2.5).

When you open one of these templates in Azure, you must first select your subscription, and create or select a resource group in the desired region where you want to host your virtual machine.  In the remaining settings, you will be prompted for the following parameters:
* **Admin Username**: the username used to access the VM (e.g., via a remote desktop client)
* **Admin Password**: a strong password for your admin account.
* **DNS Label Prefix**: a name used to create a fully qualified domain name for the VM that looks like <my-machine-dns-name>.<region>.cloudapp.azure.com (must be a valid [hostname](https://en.wikipedia.org/wiki/Hostname#Syntax), and must be unique in the selected Azure region)
* **VM Name**: a unique name for the machine deployed in your azure account (use a simple alphanumeric name - max 15 characters)
* **VM Size**: must be a valid identifier for a machine size available in your selected region - a default value is pre-filled depending on the template you choose below.
* **Auto Shutdown Time**: the time of scheduled shutdown in HHMM format (e.g., default is 2200, to automatically shutdown the VM at 10pm)
* **Auto Shutdown Time Zone**: the time zone for the shutdown schedule time.
* **Auto Shutdown Notification Email**: the email address that will be notified prior to a VM being shut down.

## VM Sizing

You will need to choose an appropriate size of virtual machine depending on whether you will be performing analyses that involved high use of CPU/memory, or if you will be using any 3D capabilities of ArcGIS Pro.  The three templates linked below are pre-configured with three different VM sizes.  However, you can enter the identifier for any VM size that you prefer to use.

Prior to choosing the size of a VM, it is good idea to refer to the hardware system requirements for [ArcMap](https://desktop.arcgis.com/en/system-requirements/latest/arcgis-desktop-system-requirements.htm) and/or [ArcGIS Pro](https://pro.arcgis.com/en/pro-app/get-started/arcgis-pro-system-requirements.htm).

You may also review the different [sizes available for Windows VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes) in Azure.

Each VM you create will have different pay-as-you-go rates for usage depending on your chosen VM size and hosting region.  Be sure you know the budget you are working with, and understand the costs associated with the VM size you choose and the amount of time you plan to use it over a given period of time.  The Azure [pricing calculator](https://azure.microsoft.com/pricing/calculator/) is a useful tool for estimating associates costs.

Note that a VM created from the ArcGIS Desktop image will include a 128 GiB disk for the operating system that will be allocated as a Premium SSD (or as a Standard SSD if the chosen VM size does not support Premium SSD).

For each template below, shortcuts are provided to pre-configured monthly pricing estimates for each VM in Canada Central (if applicable) and US East hosting regions (you may select a different region if you prefer within the pricing calculator).  The different estimates provided are based on 50 hours (~11 hours of use per week), 100 hours (~22 hours of use per week), and 720 hours (30 days running non-stop and automatic shutdown disabled).  Note that the linked pricing estimates will default to ***US Dollars*** when opened - ensure that sure you are looking at estimated prices in ***Canadian Dollars*** (or your preferred currency) by selecting your the displayed currency at the bottom of the pricing estimate.

## Minimize costs

In addition to selecting the appropriate size for your VM, and choosing a good time for your auto shutdown schedule, you can also at any time shut down your VM to minimize usage costs.  When you do this, you must shut down the VM from the Azure portal.  It is not sufficient to shutdown the VM from within the OS (i.e., from the Windows start menu).  You must open the VM in the Azure portal, and click the **Stop** button at the top.  When you stop the VM through the Azure portal, and/or allow the auto shutdown schedule to stop your VM, then it will deallocate resources, and you will not be charged the pay-as-you-go rate for the VM until you choose to start it again.

To restart your VM to continue working with it, visit the Azure portal, open your VM, and click the 'Start' button.

## Templates

When you are ready, you can launch an image from a desried template below clicking the corresponding **Deploy to Azure** button.

### Standard performance:

This template uses a [Standard_D4_v3](https://docs.microsoft.com/en-us/azure/virtual-machines/dv3-dsv3-series?toc=/azure/virtual-machines/linux/toc.json&bc=/azure/virtual-machines/linux/breadcrumb/toc.json) VM, which offers 4 dedicated CPU cores and 16 GiB of RAM

Good for ArcMap, or ArcGIS Pro if **only** using it for 2D mapping.

#### Cost estimates:

* 50 hours / month: [Canada Central](https://azure.com/e/1b9ab303f18247dd8d54e68706d4ea66) | [East US](https://azure.com/e/9805613cc92542b28f9fb1f19971d51c)
* 100 hours / month: [Canada Central](https://azure.com/e/342551265b2e4b38bb09c78b46daa5fb) | [East US](https://azure.com/e/1652f8530baf4698ba9bfc4cdc2eb440)
* 720 hours / month: [Canada Central](https://azure.com/e/caf534c2d62f4b39b4b2c79ef43fcc80) | [East US](https://azure.com/e/927aafe566734ecbbfa567e030016222)

***\*Note:*** *prices are quoted in **US dollars** by default*

#### Launch in Azure

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_D4v3.json" target="_blank">
    <img src="https://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_D4v3.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

### Higher performance / GPU support for 3D:

This template uses a [Standard_NV6](https://docs.microsoft.com/en-us/azure/virtual-machines/nv-series?toc=/azure/virtual-machines/linux/toc.json&bc=/azure/virtual-machines/linux/breadcrumb/toc.json) VM, which offers 6 dedicated CPU cores, 56 GiB of RAM, and 1 dedicated GPU with 8 GiB of GPU memory.

Good for either ArcMap or ArcGIS Pro, including use for 3D mapping.

#### Cost estimates:

* 50 hours / month: Canada Central (not available) | [East US](https://azure.com/e/c628fec001474b1d889b474b312e39a0)
* 100 hours / month: Canada Central (not available) | [East US](https://azure.com/e/bedf8b2468b344d38377f06c1ecc7f90)
* 720 hours / month: Canada Central (not available) | [East US](https://azure.com/e/d352f352f2174a0ab9e3c49369b9b846)

***\*Note:*** *prices are quoted in **US dollars** by default*

#### Launch in Azure

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_NV6.json" target="_blank">
    <img src="https://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_NV6.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>


### Higher performance / GPU support for 3D (*promotional rate*):

This template uses a ***Standard_NV6_Promo*** VM, which has the same specifications as the [Standard_NV6](https://docs.microsoft.com/en-us/azure/virtual-machines/nv-series?toc=/azure/virtual-machines/linux/toc.json&bc=/azure/virtual-machines/linux/breadcrumb/toc.json) VM, offering 6 dedicated CPU cores, 56 GiB of RAM, and 1 dedicated GPU with 8 GiB of GPU memory.  If it is available, the only difference is that it is offered at a 40% discounted rate, though it still costs about 3x more per hour than the ***Standard_D4_v3*** image noted above.

Good for either ArcMap or ArcGIS Pro, including use for 3D mapping.

#### Cost estimates:

* 50 hours / month: Canada Central (not available) | [East US](https://azure.com/e/91ef457260354715947a9f5c5374a139)
* 100 hours / month: Canada Central (not available) | [East US](https://azure.com/e/a3fe7b6afc384145a08f34ca74b5de2c)
* 720 hours / month: Canada Central (not available) | [East US](https://azure.com/e/ddcc8ab78d6e476aafc27ce498ad5d71)

***\*Note:*** *prices are quoted in **US dollars** by default*

#### Launch in Azure

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_NV6_Promo.json" target="_blank">
    <img src="https://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_NV6_Promo.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>


### Tight budget:

This template uses a [Standard_B4ms](https://docs.microsoft.com/en-us/azure/virtual-machines/sizes-b-series-burstable?toc=/azure/virtual-machines/linux/toc.json&bc=/azure/virtual-machines/linux/breadcrumb/toc.json) VM, which offers 4 dedicated burstable CPU cores and 16 GiB of RAM.  It is designed to give you a baseline equivalent of one CPU core at 90%, but burstable up to full capcity of 4 CPUs (400%) for brief periods.  The amount of time you can use full CPU capacity is based on the amount of time that the CPU is running at below the baseline of one CPU core at 90%.

Good for with ArcMap, or ArcGIS Pro if **only** using it for 2D mapping.  Not ideal for long-running, CPU-intensive tasks.

#### Cost estimates:

* 50 hours / month: [Canada Central](https://azure.com/e/e5f0e3f09ec040ffbc07d7c810dd2405) | [East US](https://azure.com/e/744afcbcbf40419fb51630d29d2d34f6)
* 100 hours / month: [Canada Central](https://azure.com/e/1eda7d4e0a764a29820451889414952f) | [East US](https://azure.com/e/9d313bb04080428fa43cd059174f059b)
* 720 hours / month: [Canada Central](https://azure.com/e/f49f188d4a0c4863a29d8604b036e30f) | [East US](https://azure.com/e/7ab814f86d5c407892d76258af79f6cc)

***\*Note:*** *prices are quoted in **US dollars** by default*

#### Launch in Azure

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_B4ms.json" target="_blank">
    <img src="https://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fhighered-esricanada%2Fazure-templates%2Fmaster%2Farcgis_desktop_B4ms.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

