# Introduction

The purpose of this section is to go from a blank computer with a blank hard drive to full operating camp server. The operating system we’ll be using is Ubuntu 18.04. There is a newer release 18.10 but for technical reasons, we won’t be upgrading to it. 

The computer your going to use needs to have the following specifications as a minimum:

* 2 GHz dual core processor
* 2 GiB RAM \(system memory\)
* 25 GB of hard-drive space \(or USB stick, memory card or external drive \) \(SSD is required for the production server at camp\)
* VGA capable of 1024x768 screen resolution \(Can run headless after initial setup if convenient\)
* Either a CD/DVD drive or a USB port for the installer media  .
* Internet access is required for first time setup but is not always required once on camp, as access is not always available.
* An install of PowerISO \[the evaluation version is fine\] for creating the bootable installer via USB.

{% hint style="info" %}
Download a free evaluation copy of PowerISO [here](http://www.poweriso.com/download.php).
{% endhint %}

We’ll be using **Linux Terminal Server Project \(LTSP\)** for a large part of this project. We’ll refer to LTSP a lot in the coming pages.

{% hint style="info" %}
Look more into LTSP here \[[http://www.ltsp.org/](http://www.ltsp.org/)\]
{% endhint %}

The computers we have on camp are not the best and some also don’t have hard drives. We also share the computers with GameZone, which means we can’t install Linux on the camp computers. So we turn the computers into FAT clients. 

The computer's boot using the PXE protocol and get given an image by the camp server. The image is than stored in the RAM of the computer, with all the users home directories being stored on the camp server. This way no files are actually stored on the camp computers themselves. 

FAT clients use their own RAM and CPU power to run the applications, of course this also means that their hardware requirements are the same as for running Ubuntu on normal workstations. 

We’ll list all the steps in the sidebar under the Server section, use the menu on the left to see details on all the steps.

