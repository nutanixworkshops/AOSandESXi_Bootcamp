.. title:: Nutanix Orientation for vSphere Administrators

.. toctree::
   :maxdepth: 2
   :caption: Nutanix Configuration
   :name: _configuration_labs
   :hidden:

   nutanixTechOverviewLab/nutanixTechOverviewLab
   storageConfiguration/storageConfiguration

.. toctree::
   :maxdepth: 2
   :caption: Workloads
   :name: _workload_labs
   :hidden:

   deployingWorkloads/deployingWorkloads
   managingWorkloads/managingWorkloads

.. toctree::
   :maxdepth: 2
   :caption: Nutanix Operations
   :name: _operations_labs
   :hidden:

   cvm/cvm
   healthNccLogs/healthNccLogs
   ipmi/ipmi

.. toctree::
   :maxdepth: 2
   :caption: Data Protection 
   :name: _dp_labs
   :hidden:
 
   ssr/ssr
   dataProtection/dataProtection

.. toctree::  
   :maxdepth: 2
   :caption: Optional Reading
   :name: _optional_labs
   :hidden:   
    
   readingLab1/readingLab1

.. toctree::
   :maxdepth: 2
   :caption: Appendix
   :name: _appendix
   :hidden:
        
   appendix/glossary
   frame/frame

.. _getting_started:

---------------
Getting Started
---------------

Welcome to the Nutanix Orientation for vSphere Administrators Bootcamp! This workbook accompanies an instructor-led session that introduces Nutanix technologies and common management tasks. Each section has a lesson and one or more lab exercises to give you hands-on practice. The instructor explains the exercises and answers any additional questions that you may have.

At the end of the bootcamp, attendees should understand the basic concepts and technologies that make up the Nutanix system and how it operates with vCenter and ESXi as the hypervisor.

A working knowledge of vSphere operations is assumed, such as how to deploy a VM from a template and work with datastores.

What's New 
++++++++++

- This workshop, we often call then "bootcamps" is new and focusses on how vSphere integrates with Nutanix.
    - AOS 5.19.x, vCenter/vSphere 6.5u1


Agenda
++++++

- Introductions
- Nutanix Presentation
- Nutanix Configuration Labs
- Deploying and Managing Workloads Labs
- (Optional) Reading - vCenter/vSphere Setup for Nutanix

Introductions
+++++++++++++

- Name
- Familiarity with Nutanix 

Initial Setup
+++++++++++++

- Take note of the *Passwords* being used.
- Log into your virtual desktops (connection info below)

Environment Details
+++++++++++++++++++

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images, networks, and VMs required to complete the exercises.

Networking
..........

Hosted POC clusters follow a standard naming convention:

- **Cluster Name** - POC\ *XYZ*
- **Subnet** - 10.**21**.\ *XYZ*\ .0
- **Cluster IP** - 10.**21**.\ *XYZ*\ .37
- **vCenter IP** - 10.**21**.\ *XYZ*\ .40

If provisioned from the marketing pool:

- **Cluster Name** - MKT\ *XYZ*
- **Subnet** - 10.**20**.\ *XYZ*\ .0
- **Cluster IP** - 10.**20**.\ *XYZ*\ .37
- **vCenter IP** - 10.**20**.\ *XYZ*\ .40

For example:

- **Cluster Name** - POC055
- **Subnet** - 10.21.55.0
- **Cluster IP** - 10.21.55.37
- **vCenter IP** - 10.21.55.40

Throughout the Workshop there are multiple instances where you will need to substitute *XYZ* with the correct octet for your subnet, for example:

.. list-table::
   :widths: 25 75
   :header-rows: 1

   * - IP Address
     - Description
   * - 10.21.\ *XYZ*\ .37
     - Prism ELement, aka PE, aka Nutanix Cluster Virtual IP, aka VIP
   * - 10.21.\ *XYZ*\ .40
     - **vCenter** VM IP

Each cluster is configured with 2 VLANs which can be used for VMs:

.. list-table::
  :widths: 25 25 10 40
  :header-rows: 1

  * - Network Name
    - Address
    - VLAN
    - DHCP Scope
  * - Primary
    - 10.21.\ *XYZ*\ .1/25
    - 0
    - 10.21.\ *XYZ*\ .50-10.21.\ *XYZ*\ .124
  * - Secondary
    - 10.21.\ *XYZ*\ .129/25
    - *XYZ1*
    - 10.21.\ *XYZ*\ .132-10.21.\ *XYZ*\ .253

Credentials
...........

.. note::

  The *<Cluster Password>* is unique to each cluster and will be provided by the leader of the Workshop.

.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - Credential
     - Username
     - Password
   * - Prism Element
     - admin
     - *<Cluster Password>*
   * - vCenter
     - administrator@vsphere.local
     - *<Cluster Password>*
   * - Controller VM
     - nutanix
     - *<Cluster Password>*

Access Instructions
+++++++++++++++++++

The Nutanix Hosted POC environment can be accessed a number of different ways:

Lab Access User Credentials
...........................

PHX Based Clusters:
**Username:** PHX-POCxxx-User01 (up to PHX-POCxxx-User20), **Password:** *<Provided by Instructor>*

RTP Based Clusters:
**Username:** RTP-POCxxx-User01 (up to RTP-POCxxx-User20), **Password:** *<Provided by Instructor>*

Frame VDI
.........

Login to: https://frame.nutanix.com/x/labs

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Parallels VDI
.................

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Employee Pulse Secure VPN
..........................

Download the client:

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** Credentials

Install the client.

In Pulse Secure Client, **Add** a connection:

For PHX:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - PHX
- **Server URL** - xlv-uswest1.nutanix.com

For RTP:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - RTP
- **Server URL** - xlv-useast1.nutanix.com


Nutanix Version Info
++++++++++++++++++++

- **AOS Version** - 5.18.x
- **vCenter/vSphere Version** - 6.5u1 
