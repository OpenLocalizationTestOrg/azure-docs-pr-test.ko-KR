---
title: "Windows에서 SAP용 Azure Virtual Machines 배포 | Microsoft Docs"
description: "Azure의 Windows 가상 컴퓨터에 SAP 소프트웨어를 배포하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 22aaa98c-bb9f-472f-b546-0b294e033cda
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac7c1e3b015a21fe06f27205b27a53fc4d2f3df7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a><span data-ttu-id="59f81-103">Azure의 Windows VM에서 SAP 배포</span><span class="sxs-lookup"><span data-stu-id="59f81-103">Deploy SAP on Windows VMs in Azure</span></span>
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
<span data-ttu-id="59f81-104">[1031096]:https://launchpad.support.sap.com/#/notes/1031096</span><span class="sxs-lookup"><span data-stu-id="59f81-104">[1031096]:https://launchpad.support.sap.com/#/notes/1031096</span></span>
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
<span data-ttu-id="59f81-105">[1409604]:https://launchpad.support.sap.com/#/notes/1409604</span><span class="sxs-lookup"><span data-stu-id="59f81-105">[1409604]:https://launchpad.support.sap.com/#/notes/1409604</span></span>
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
<span data-ttu-id="59f81-106">[1619720]:https://launchpad.support.sap.com/#/notes/1619720</span><span class="sxs-lookup"><span data-stu-id="59f81-106">[1619720]:https://launchpad.support.sap.com/#/notes/1619720</span></span>
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
<span data-ttu-id="59f81-107">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="59f81-107">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
<span data-ttu-id="59f81-108">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="59f81-108">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="59f81-109">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="59f81-109">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
<span data-ttu-id="59f81-110">[2002167]:https://launchpad.support.sap.com/#/notes/2002167</span><span class="sxs-lookup"><span data-stu-id="59f81-110">[2002167]:https://launchpad.support.sap.com/#/notes/2002167</span></span>
<span data-ttu-id="59f81-111">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="59f81-111">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
<span data-ttu-id="59f81-112">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="59f81-112">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="59f81-113">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="59f81-113">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
<span data-ttu-id="59f81-114">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="59f81-114">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:sap-dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP on Windows)
[dbms-guide-2.1]:sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from the Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics to SQL Server RDBMS)
[dbms-guide-8.4.1]:sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md (Azure Virtual Machines deployment for SAP on Windows)
[deployment-guide-2.2]:#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from the Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM to an on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable the Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure the Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for the Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure the proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:sap-get-started.md
[getting-started-dbms]:sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:classic/virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:classic/virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:classic/virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:classic/virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:classic/virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:classic/virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-windows-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md (Azure Virtual Machines planning and implementation for SAP on Windows)
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on the on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with the on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises to Azure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises to Azure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises to Azure)
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../storage/storage-premium-storage.md
[storage-redundancy]:../../storage/storage-redundancy.md
[storage-scalability-targets]:../../storage/storage-scalability-targets.md
[storage-use-azcopy]:../../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../linux/attach-disk-portal.md
[virtual-machines-windows-attach-disk-portal]:../virtual-machines-windows-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-windows-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../linux/capture-image.md
[virtual-machines-linux-capture-image-capture]:../linux/capture-image.md#capture-the-vm
[virtual-machines-windows-capture-image]:../virtual-machines-windows-capture-image.md
[virtual-machines-windows-capture-image-capture]:../virtual-machines-windows-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-lvm]:../linux/configure-lvm.md
[virtual-machines-linux-configure-raid]:../linux/configure-raid.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../linux/update-agent.md
[virtual-machines-manage-availability]:../virtual-machines-windows-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:classic/ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:classic/ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:upload-image.md
[virtual-machines-windows-tutorial]:../virtual-machines-windows-hero-tutorial.md
[virtual-machines-windows-create-vm-specialized]:../virtual-machines-windows-create-vm-specialized.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md
[vpn-gateway-vpn-faq]:../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../xplat-cli-azure-resource-manager.md

<span data-ttu-id="59f81-115">Azure Virtual Machines는 긴 조달 주기 없이 최소한의 시간 안에 계산 및 저장소 리소스를 필요로 하는 조직을 위한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-115">Azure Virtual Machines is the solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="59f81-116">Azure Virtual Machines를 사용하여 Azure에서 SAP NetWeaver 기반 응용 프로그램 같은 기존 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-116">You can use Azure Virtual Machines to deploy classical applications, like SAP NetWeaver-based applications, in Azure.</span></span> <span data-ttu-id="59f81-117">추가 온-프레미스 리소스 없이도 응용 프로그램의 안정성과 가용성을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-117">Extend an application's reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="59f81-118">Azure Virtual Machines는 크로스-프레미스 연결을 지원하므로 Azure Virtual Machines를 조직의 온-프레미스 도메인, 사설 클라우드 및 SAP 시스템 지형에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-118">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="59f81-119">이 문서에서는 Azure의 Windows VM(가상 컴퓨터)에서 SAP 응용 프로그램을 배포하는 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-119">In this article, we cover the steps to deploy SAP applications on Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="59f81-120">이 문서는 [Windows에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]의 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-120">This article builds on the information in [Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide].</span></span> <span data-ttu-id="59f81-121">또한 SAP 소프트웨어를 설치 및 배포하기 위한 기본 리소스인 SAP 설치 설명서 및 SAP Note를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-121">It also complements SAP installation documentation and SAP Notes, which are the primary resources for installing and deploying SAP software.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59f81-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="59f81-122">Prerequisites</span></span>
<span data-ttu-id="59f81-123">SAP 소프트웨어 배포를 위해 Azure Virtual Machines를 설정하려면 여러 단계와 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-123">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span></span> <span data-ttu-id="59f81-124">시작하기 전에 Azure에서 Windows 가상 컴퓨터에 SAP 소프트웨어를 설치하기 위한 필수 구성 요소를 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-124">Before you start, make sure that you meet the prerequisites for installing SAP software on Windows virtual machines in Azure.</span></span>

### <a name="local-computer"></a><span data-ttu-id="59f81-125">수집</span><span class="sxs-lookup"><span data-stu-id="59f81-125">Local computer</span></span>
<span data-ttu-id="59f81-126">Windows 또는 Linux VM을 관리하려면 PowerShell 스크립트와 Azure Portal을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-126">To manage Windows or Linux VMs, you can use a PowerShell script and the Azure portal.</span></span> <span data-ttu-id="59f81-127">두 가지 도구 모두 Windows 7 또는 이후 버전의 Windows 실행하는 로컬 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-127">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span></span> <span data-ttu-id="59f81-128">Linux VM만 관리하려는 경우 이 작업에 Linux 컴퓨터를 사용하려면 Azure CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-128">If you want to manage only Linux VMs and you want to use a Linux computer for this task, you can use Azure CLI.</span></span>

### <a name="internet-connection"></a><span data-ttu-id="59f81-129">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="59f81-129">Internet connection</span></span>
<span data-ttu-id="59f81-130">SAP 소프트웨어 배포에 필요한 도구와 스크립트를 다운로드하고 실행하려면 인터넷에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-130">To download and run the tools and scripts that are required for SAP software deployment, you must be connected to the Internet.</span></span> <span data-ttu-id="59f81-131">또한 SAP용 Azure 고급 모니터링 확장을 실행하는 Azure VM에서 인터넷에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-131">The Azure VM that is running the Azure Enhanced Monitoring Extension for SAP also needs access to the Internet.</span></span> <span data-ttu-id="59f81-132">Azure VM이 Azure Virtual Network 또는 온-프레미스 도메인에 포함된 경우 관련 프록시 설정이 [프록시 구성][deployment-guide-configure-proxy]에서 설명한 대로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-132">If the Azure VM is part of an Azure virtual network or on-premises domain, make sure that the relevant proxy settings are set, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span>

### <a name="microsoft-azure-subscription"></a><span data-ttu-id="59f81-133">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="59f81-133">Microsoft Azure subscription</span></span>
<span data-ttu-id="59f81-134">활성 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-134">You need an active Azure account.</span></span>

### <a name="topology-and-networking"></a><span data-ttu-id="59f81-135">토폴로지 및 네트워킹</span><span class="sxs-lookup"><span data-stu-id="59f81-135">Topology and networking</span></span>
<span data-ttu-id="59f81-136">Azure에서 SAP 배포의 토폴로지 및 아키텍처를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-136">You need to define the topology and architecture of the SAP deployment in Azure:</span></span>

* <span data-ttu-id="59f81-137">사용할 Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="59f81-137">Azure storage accounts to be used</span></span>
* <span data-ttu-id="59f81-138">SAP 시스템을 배포할 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="59f81-138">Virtual network where you want to deploy the SAP system</span></span>
* <span data-ttu-id="59f81-139">SAP 시스템을 배포할 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="59f81-139">Resource group to which you want to deploy the SAP system</span></span>
* <span data-ttu-id="59f81-140">SAP 시스템을 배포할 Azure 영역</span><span class="sxs-lookup"><span data-stu-id="59f81-140">Azure region where you want to deploy the SAP system</span></span>
* <span data-ttu-id="59f81-141">SAP 구성(2계층 또는 3계층)</span><span class="sxs-lookup"><span data-stu-id="59f81-141">SAP configuration (two-tier or three-tier)</span></span>
* <span data-ttu-id="59f81-142">VM 크기 및 VM에 탑재할 추가 가상 하드 디스크(VHD) 수</span><span class="sxs-lookup"><span data-stu-id="59f81-142">VM sizes and the number of additional virtual hard disks (VHDs) to be mounted to the VMs</span></span>
* <span data-ttu-id="59f81-143">SAP 수정과 전송 시스템(CTS) 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-143">SAP Correction and Transport System (CTS) configuration</span></span>

<span data-ttu-id="59f81-144">SAP 소프트웨어 배포 프로세스를 시작하기 전에 Azure Storage 계정 또는 Azure Virtual Network를 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-144">Create and configure Azure storage accounts or Azure virtual networks before you begin the SAP software deployment process.</span></span> <span data-ttu-id="59f81-145">이러한 리소스를 만들고 구성하는 방법에 대한 정보는 [Windows에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-145">For information about how to create and configure these resources, see [Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide].</span></span>

### <a name="sap-sizing"></a><span data-ttu-id="59f81-146">SAP 크기 조정</span><span class="sxs-lookup"><span data-stu-id="59f81-146">SAP sizing</span></span>
<span data-ttu-id="59f81-147">SAP 크기 조정을 위해 다음 정보를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-147">Know the following information, for SAP sizing:</span></span>

* <span data-ttu-id="59f81-148">예상되는 SAP 워크로드(예: SAP Quick Sizer 도구 사용의 경우) 및 SAPS(SAP Application Performance Standard) 번호</span><span class="sxs-lookup"><span data-stu-id="59f81-148">Projected SAP workload, for example, by using the SAP Quick Sizer tool, and the SAP Application Performance Standard (SAPS) number</span></span>
* <span data-ttu-id="59f81-149">SAP 시스템의 필요한 CPU 리소스 및 메모리 소비</span><span class="sxs-lookup"><span data-stu-id="59f81-149">Required CPU resource and memory consumption of the SAP system</span></span>
* <span data-ttu-id="59f81-150">필요한 초당 입력/출력(I/O) 작업 수</span><span class="sxs-lookup"><span data-stu-id="59f81-150">Required input/output (I/O) operations per second</span></span>
* <span data-ttu-id="59f81-151">Azure에서 서로 다른 VM 간의 결과적 통신에 필요한 네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="59f81-151">Required network bandwidth of eventual communication between VMs in Azure</span></span>
* <span data-ttu-id="59f81-152">온-프레미스 자산과 Azure가 배포된 SAP 시스템 간에 필요한 네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="59f81-152">Required network bandwidth between on-premises assets and the Azure-deployed SAP system</span></span>

### <a name="resource-groups"></a><span data-ttu-id="59f81-153">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="59f81-153">Resource groups</span></span>
<span data-ttu-id="59f81-154">Azure Resource Manager에서 리소스 그룹을 사용하여 Azure 구독에서 모든 응용 프로그램 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-154">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="59f81-155">자세한 내용은 [Azure Resource Manager 개요][resource-group-overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-155">For more information, see [Azure Resource Manager overview][resource-group-overview].</span></span>

## <a name="resources"></a><span data-ttu-id="59f81-156">리소스</span><span class="sxs-lookup"><span data-stu-id="59f81-156">Resources</span></span>

### <span data-ttu-id="59f81-157"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP 리소스</span><span class="sxs-lookup"><span data-stu-id="59f81-157"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP resources</span></span>
<span data-ttu-id="59f81-158">SAP 소프트웨어 배포를 설정하는 경우 다음과 같은 SAP 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-158">When you are setting up your SAP software deployment, you need the following SAP resources:</span></span>

* <span data-ttu-id="59f81-159">SAP Note [1928533], 다음 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-159">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="59f81-160">SAP 소프트웨어 배포에 지원되는 Azure VM 크기 목록</span><span class="sxs-lookup"><span data-stu-id="59f81-160">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="59f81-161">Azure VM 크기에 대한 중요한 용량 정보</span><span class="sxs-lookup"><span data-stu-id="59f81-161">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="59f81-162">지원되는 SAP 소프트웨어 및 운영 체제(OS)와 데이터베이스 조합</span><span class="sxs-lookup"><span data-stu-id="59f81-162">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="59f81-163">Microsoft Azure에서 Windows 및 Linux에 필요한 SAP 커널 버전</span><span class="sxs-lookup"><span data-stu-id="59f81-163">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="59f81-164">SAP Note [2015553]는 Azure에서 SAP을 지원하는 SAP 소프트웨어 배포에 대한 필수 구성 요소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-164">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="59f81-165">SAP Note [2178632]는 Azure에서 SAP에 대해 보고된 모든 모니터링 메트릭에 대한 자세한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-165">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="59f81-166">SAP Note [1409604]는 Azure에서 Windows에 필요한 SAP Host Agent 버전을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-166">SAP Note [1409604] has the required SAP Host Agent version for Windows in Azure.</span></span>
* <span data-ttu-id="59f81-167">SAP Note [2191498]는 Azure에서 Linux에 필요한 SAP Host Agent 버전을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-167">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="59f81-168">SAP Note [2243692]는 Azure에서 Linux의 SAP 라이선스에 대한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-168">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="59f81-169">SAP Note [1984787]은 SUSE LINUX Enterprise Server 12에 대한 일반 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-169">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="59f81-170">SAP Note [2002167]는 Red Hat Enterprise Linux 7.x에 대한 일반 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-170">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span></span>
* <span data-ttu-id="59f81-171">SAP Note [1999351]은 SAP용 Azure 고급 모니터링 확장을 위한 추가 문제 해결 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-171">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="59f81-172">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes)는 Linux에 필요한 모든 SAP Note를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-172">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="59f81-173">[Azure PowerShell][azure-ps]에 포함된 SAP 관련 PowerShell cmdlet입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-173">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span></span>
* <span data-ttu-id="59f81-174">[Azure CLI][azure-cli]에 포함된 SAP 관련 Azure CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-174">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span></span>

<span data-ttu-id="59f81-175">[comment]: <> (MSSedusch TODO - SAP Note 1409604에 SAP 호스트 에이전트용 ARM 패치 수준 추가)</span><span class="sxs-lookup"><span data-stu-id="59f81-175">[comment]: <> (MSSedusch TODO Add ARM patch level for SAP Host Agent in SAP Note 1409604)</span></span>

### <a name="microsoft-resources"></a><span data-ttu-id="59f81-176">Microsoft 리소스</span><span class="sxs-lookup"><span data-stu-id="59f81-176">Microsoft resources</span></span>
<span data-ttu-id="59f81-177">다음 Microsoft 문서에서는 Azure에서 SAP 배포에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-177">These Microsoft articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="59f81-178">[Windows에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="59f81-178">[Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide]</span></span>
* <span data-ttu-id="59f81-179">[Windows에서 SAP용 Azure Virtual Machines 배포(이 문서)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="59f81-179">[Azure Virtual Machines deployment for SAP on Windows (this article)][deployment-guide]</span></span>
* <span data-ttu-id="59f81-180">[Windows에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="59f81-180">[Azure Virtual Machines DBMS deployment for SAP on Windows][dbms-guide]</span></span>
* <span data-ttu-id="59f81-181">[Azure Portal][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="59f81-181">[Azure portal][azure-portal]</span></span>

## <span data-ttu-id="59f81-182"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure VM에서 SAP 소프트웨어에 대한 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="59f81-182"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Deployment scenarios for SAP software on Azure VMs</span></span>
<span data-ttu-id="59f81-183">Azure에서 VM 및 연결된 디스크를 배포하기 위한 여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-183">You have multiple options for deploying VMs and associated disks in Azure.</span></span> <span data-ttu-id="59f81-184">선택하는 배포 유형에 따라 배포를 위해 VM을 준비하는 단계가 다를 수 있으므로 배포 옵션 간의 차이점을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-184">It's important to understand the differences between deployment options, because you might take different steps to prepare your VMs for deployment based on the deployment type you choose.</span></span>

### <span data-ttu-id="59f81-185"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>시나리오 1: SAP용 Azure Marketplace에서 VM 배포</span><span class="sxs-lookup"><span data-stu-id="59f81-185"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenario 1: Deploying a VM from the Azure Marketplace for SAP</span></span>
<span data-ttu-id="59f81-186">Azure Marketplace에서 Microsoft 또는 타사에서 제공하는 이미지를 사용하여 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-186">You can use an image provided by Microsoft or by a third party in the Azure Marketplace to deploy your VM.</span></span> <span data-ttu-id="59f81-187">Marketplace는 Windows Server 및 서로 다른 Linux 배포의 일부 표준 OS 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-187">The Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span></span> <span data-ttu-id="59f81-188">또한 데이터베이스 관리 시스템(DMBS) SKU, 예를 들어 Microsoft SQL Server를 포함하고 있는 이미지를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-188">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span></span> <span data-ttu-id="59f81-189">DBMS SKU가 포함된 이미지 사용에 관한 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-189">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>

<span data-ttu-id="59f81-190">다음 순서도는 Azure Marketplace에서 VM을 배포하기 위한 SAP 관련 단계 순서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-190">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from the Azure Marketplace:</span></span>

![Azure Marketplace에서 VM 이미지를 사용하여 SAP 시스템용 VM 배포 순서도][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-the-azure-portal"></a><span data-ttu-id="59f81-192">Azure Portal을 사용하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="59f81-192">Create a virtual machine by using the Azure portal</span></span>
<span data-ttu-id="59f81-193">Azure Marketplace에서 이미지를 사용하여 새 가상 컴퓨터를 만드는 가장 쉬운 방법은 Azure Portal을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-193">The easiest way to create a new virtual machine with an image from the Azure Marketplace is by using the Azure portal.</span></span>

1.  <span data-ttu-id="59f81-194"><https://portal.azure.com/#create>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-194">Go to <https://portal.azure.com/#create>.</span></span>  <span data-ttu-id="59f81-195">또는 Azure Portal 메뉴에서 **+새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-195">Or, in the Azure portal menu, select **+ New**.</span></span>
2.  <span data-ttu-id="59f81-196">**계산**을 선택한 다음 배포할 운영 체제 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-196">Select **Compute**, and then select the type of operating system you want to deploy.</span></span> <span data-ttu-id="59f81-197">예를 들어, Windows Server 2012 R2, SUSE Linux Enterprise Server 12(SLES 12) 또는 Red Hat Enterprise Linux 7.2(RHEL 7.2)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-197">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span> <span data-ttu-id="59f81-198">기본 목록 보기에는 지원되는 일부 운영 체제가 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-198">The default list view does not show all supported operating systems.</span></span> <span data-ttu-id="59f81-199">전체 목록을 보려면 **모두 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-199">Select **see all** for a full list.</span></span> <span data-ttu-id="59f81-200">SAP 소프트웨어 배포를 위한 지원되는 운영 체제에 대한 자세한 내용은 SAP Note [1928533]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-200">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
3.  <span data-ttu-id="59f81-201">다음 페이지에서 약관을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-201">On the next page, review terms and conditions.</span></span>
4.  <span data-ttu-id="59f81-202">**배포 모델 선택** 목록에서 **Resource Manager**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-202">In the **Select a deployment model** box, select **Resource Manager**.</span></span>
5.  <span data-ttu-id="59f81-203">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-203">Select **Create**.</span></span>

<span data-ttu-id="59f81-204">마법사의 필수 매개 변수 설정을 통해 네트워크 인터페이스 및 저장소 계정과 같은 모든 필요한 리소스와 함께 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-204">The wizard guides you through setting the required parameters to create the virtual machine, in addition to all required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="59f81-205">다음은 일부 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-205">Some of these parameters are:</span></span>

1. <span data-ttu-id="59f81-206">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="59f81-206">**Basics**:</span></span>
  * <span data-ttu-id="59f81-207">**이름**: 리소스 이름(가상 컴퓨터 이름)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-207">**Name**: The name of the resource (the virtual machine name).</span></span>
 * <span data-ttu-id="59f81-208">**사용자 이름 및 암호** 또는 **SSH 공개 키**: 프로비전 중에 만든 사용자의 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-208">**Username and password** or **SSH public key**: Enter the username and password of the user that is created during the provisioning.</span></span> <span data-ttu-id="59f81-209">Linux 가상 컴퓨터의 경우 컴퓨터에 로그인하는 데 사용하는 공용 SSH(Secure Shell) 키를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-209">For a Linux virtual machine, you can enter the public Secure Shell (SSH) key that you use to sign in to the machine.</span></span>
 * <span data-ttu-id="59f81-210">**구독**: 새 가상 컴퓨터를 프로비전하는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-210">**Subscription**: Select the subscription that you want to use to provision the new virtual machine.</span></span>
 * <span data-ttu-id="59f81-211">**리소스 그룹**: VM에 대한 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-211">**Resource group**: The name of the resource group for the VM.</span></span> <span data-ttu-id="59f81-212">새 리소스 그룹의 이름 또는 기존 리소스 그룹의 이름을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-212">You can enter either the name of a new resource group or the name of a resource group that already exists.</span></span>
 * <span data-ttu-id="59f81-213">**위치**: 새 가상 컴퓨터를 배포할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-213">**Location**: Where to deploy the new virtual machine.</span></span> <span data-ttu-id="59f81-214">온-프레미스 네트워크에 가상 컴퓨터를 연결하려는 경우 온-프레미스 네트워크에 Azure를 연결하는 가상 네트워크의 위치를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-214">If you want to connect the virtual machine to your on-premises network, make sure you select the location of the virtual network that connects Azure to your on-premises network.</span></span> <span data-ttu-id="59f81-215">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]의 [Microsoft Azure 네트워킹][planning-guide-microsoft-azure-networking]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-215">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>
2. <span data-ttu-id="59f81-216">**크기**:</span><span class="sxs-lookup"><span data-stu-id="59f81-216">**Size**:</span></span>

     <span data-ttu-id="59f81-217">지원되는 VM 유형 목록은 SAP Note [1928533]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-217">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="59f81-218">Azure Premium Storage를 사용하려면 올바른 VM 유형을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-218">Be sure you select the correct VM type if you want to use Azure Premium Storage.</span></span> <span data-ttu-id="59f81-219">모든 VM 유형이 프리미엄 저장소를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-219">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="59f81-220">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]의 [Storage: Microsoft Azure Storage 및 데이터 링크][planning-guide-storage-microsoft-azure-storage-and-data-disks] 및 [Azure Premium Storage][planning-guide-azure-premium-storage]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-220">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>

3. <span data-ttu-id="59f81-221">**설정**:</span><span class="sxs-lookup"><span data-stu-id="59f81-221">**Settings**:</span></span>
   * <span data-ttu-id="59f81-222">**저장소 계정**: 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-222">**Storage account**: Select an existing storage account or create a new one.</span></span> <span data-ttu-id="59f81-223">모든 저장소 유형이 SAP 응용 프로그램 실행을 위해 작동하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-223">Not all storage types work for running SAP applications.</span></span> <span data-ttu-id="59f81-224">저장소 유형에 대한 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-224">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>
   * <span data-ttu-id="59f81-225">**가상 네트워크** 및 **서브넷**: 인트라넷에 가상 컴퓨터를 통합하려면 온-프레미스 네트워크에 연결된 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-225">**Virtual network** and **Subnet**: To integrate the virtual machine with your intranet, select the virtual network that is connected to your on-premises network.</span></span>
   * <span data-ttu-id="59f81-226">**공용 IP 주소**: 사용하려는 공용 IP 주소를 선택하거나 매개 변수를 입력하여 새 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-226">**Public IP address**: Select the public IP address that you want to use, or enter parameters to create a new public IP address.</span></span> <span data-ttu-id="59f81-227">인터넷에서 가상 컴퓨터에 액세스하는 공용 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-227">You can use a public IP address to access your virtual machine over the Internet.</span></span> <span data-ttu-id="59f81-228">또한 가상 컴퓨터에 안전하게 액세스하려면 네트워크 보안 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-228">Make sure that you also create a network security group to help secure access to your virtual machine.</span></span>
   * <span data-ttu-id="59f81-229">**네트워크 보안 그룹**: 자세한 내용은 [네트워크 보안 그룹으로 네트워크 트래픽 흐름 제어][virtual-networks-nsg]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-229">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
   * <span data-ttu-id="59f81-230">**가용성**: 가용성 집합을 선택하거나 매개 변수를 입력하여 새 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-230">**Availability**: Select an availability set, or enter the parameters to create a new availability set.</span></span> <span data-ttu-id="59f81-231">자세한 내용은 [Azure 가용성 집합][planning-guide-3.2.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-231">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
   * <span data-ttu-id="59f81-232">**모니터링**: 진단 모니터링에 대해 **사용 중지**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-232">**Monitoring**: You can select **Disable** for monitoring diagnostics.</span></span> <span data-ttu-id="59f81-233">이는 [모니터링 구성][deployment-guide-configure-monitoring-scenario-1]에서 설명한 대로 Azure 고급 모니터링을 활성화하는 명령을 실행할 때 자동으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-233">It is enabled automatically when you run the commands to enable the Azure Enhanced Monitoring Extension, as described in [Configure monitoring][deployment-guide-configure-monitoring-scenario-1].</span></span>

4. <span data-ttu-id="59f81-234">**요약**:</span><span class="sxs-lookup"><span data-stu-id="59f81-234">**Summary**:</span></span>

  <span data-ttu-id="59f81-235">선택 내용을 검토한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-235">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="59f81-236">선택한 리소스 그룹에서 가상 컴퓨터가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-236">Your virtual machine is deployed in the resource group you selected.</span></span>

#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="59f81-237">템플릿을 사용하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="59f81-237">Create a virtual machine by using a template</span></span>
<span data-ttu-id="59f81-238">[azure-quickstart-templates GitHub 리포지토리][azure-quickstart-templates-github]에 게시된 SAP 템플릿 중 하나를 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-238">You can create a virtual machine by using one of the SAP templates published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="59f81-239">또한 [Azure Portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms] 또는 [Azure CLI][virtual-machines-linux-tutorial]를 사용하여 가상 컴퓨터를 수동으로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-239">You also can manually create a virtual machine by using the [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span></span>

* <span data-ttu-id="59f81-240">[**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="59f81-240">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span></span>

  <span data-ttu-id="59f81-241">한 대의 가상 컴퓨터를 사용하여 2계층 시스템을 만들려면 이 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-241">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="59f81-242">[**3계층 구성(여러 가상 컴퓨터) 템플릿**(sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="59f81-242">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span></span>

  <span data-ttu-id="59f81-243">여러 대의 가상 컴퓨터를 사용하여 3계층 시스템을 만들려면 이 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-243">To create a three-tier system by using multiple virtual machines, use this template.</span></span>

<span data-ttu-id="59f81-244">Azure Portal에서 템플릿에 대한 다음 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-244">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="59f81-245">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="59f81-245">**Basics**:</span></span>
  * <span data-ttu-id="59f81-246">**구독**: 템플릿을 배포하는 데 사용하는 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-246">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="59f81-247">**리소스 그룹**: 템플릿을 배포하는 데 사용하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-247">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="59f81-248">새 리소스 그룹을 만들거나 구독에서 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-248">You can create a new resource group, or you can select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="59f81-249">**위치**: 템플릿을 배포할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-249">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="59f81-250">기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 위치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-250">If you selected an existing resource group, the location of that resource group is used.</span></span>

2. <span data-ttu-id="59f81-251">**설정**:</span><span class="sxs-lookup"><span data-stu-id="59f81-251">**Settings**:</span></span>
  * <span data-ttu-id="59f81-252">**SAP 시스템 ID**: SAP 시스템 ID(SID)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-252">**SAP System ID**: The SAP System ID (SID).</span></span>
  * <span data-ttu-id="59f81-253">**OS 형식**: 배포할 운영 체제, 예를 들어 Windows Server 2012 R2, SUSE Linux Enterprise Server 12(SLES 12) 또는 Red Hat Enterprise Linux 7.2(RHEL 7.2)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-253">**OS type**: The operating system you want to deploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span>

    <span data-ttu-id="59f81-254">기본 목록 보기에는 지원되는 일부 운영 체제가 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-254">The default list view does not show all supported operating systems.</span></span> <span data-ttu-id="59f81-255">전체 목록을 보려면 **모두 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-255">Select **see all** for a full list.</span></span> <span data-ttu-id="59f81-256">SAP 소프트웨어 배포를 위한 지원되는 운영 체제에 대한 자세한 내용은 SAP Note [1928533]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-256">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
  * <span data-ttu-id="59f81-257">**SAP 시스템 크기**: SAP 시스템의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-257">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="59f81-258">새 시스템에서 제공하는 SAP의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-258">The number of SAPS the new system provides.</span></span> <span data-ttu-id="59f81-259">시스템에 필요한 SAP의 수를 모를 경우 SAP 기술 파트너 또는 시스템 통합자에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-259">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="59f81-260">**시스템 가용성**(3계층 템플릿만 해당): 시스템 가용성입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-260">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="59f81-261">고가용성 설치에 적합한 구성의 경우 **HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-261">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="59f81-262">두 데이터베이스 서버와 ABAP SAP 중앙 서비스(ASCS)에 대한 두 서버가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-262">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span></span>
  * <span data-ttu-id="59f81-263">**저장소 유형**(2계층 템플릿에만 해당): 사용하는 저장소 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-263">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="59f81-264">더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-264">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="59f81-265">저장소 유형에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-265">For more information about storage types, see these resources:</span></span>
      * <span data-ttu-id="59f81-266">[SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]</span><span class="sxs-lookup"><span data-stu-id="59f81-266">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="59f81-267">[Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="59f81-267">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="59f81-268">[Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="59f81-268">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="59f81-269">[Microsoft Azure Storage 소개][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="59f81-269">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="59f81-270">**관리 사용자 이름** 및 **관리 암호**: 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-270">**Admin username** and **Admin password**: A username and password.</span></span>
    <span data-ttu-id="59f81-271">가상 컴퓨터에 로그인하기 위한 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-271">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="59f81-272">**새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-272">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span></span> <span data-ttu-id="59f81-273">온-프레미스 네트워크에 연결되어 있는 가상 네트워크가 이미 있는 경우 **기존**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-273">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="59f81-274">**서브넷 ID**: 가상 컴퓨터를 연결할 서브넷의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-274">**Subnet ID**: The ID of the subnet the virtual machines will connect to.</span></span> <span data-ttu-id="59f81-275">온-프레미스 네트워크에 가상 컴퓨터를 연결하는 데 사용할 VPN(가상 사설망) 또는 Azure ExpressRoute 가상 네트워크의 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-275">Select the subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="59f81-276">ID는 일반적으로 다음과 같이 표시합니다. /subscriptions/&lt;구독 id>/resourceGroups/&lt;리소스 그룹 이름>/providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름>/subnets/&lt;서브넷 이름></span><span class="sxs-lookup"><span data-stu-id="59f81-276">The ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="59f81-277">**사용 약관**:</span><span class="sxs-lookup"><span data-stu-id="59f81-277">**Terms and conditions**:</span></span>  
    <span data-ttu-id="59f81-278">약관을 검토하고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-278">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="59f81-279">**구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-279">Select **Purchase**.</span></span>

<span data-ttu-id="59f81-280">Azure Marketplace에서 이미지를 사용하는 경우 Azure VM 에이전트가 기본적으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-280">The Azure VM Agent is deployed by default when you use an image from the Azure Marketplace.</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="59f81-281">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-281">Configure proxy settings</span></span>
<span data-ttu-id="59f81-282">온-프레미스 네트워크가 구성된 방법에 따라 VM에 프록시를 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-282">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="59f81-283">VM이 VPN 또는 ExpressRoute를 통해 온-프레미스 네트워크에 연결된 경우 인터넷에 액세스하지 못할 수도 있으며 필수 확장을 다운로드하거나 모니터링 데이터를 수집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-283">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="59f81-284">자세한 내용은 [프록시 구성][deployment-guide-configure-proxy]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-284">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="59f81-285">도메인 가입(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="59f81-285">Join a domain (Windows only)</span></span>
<span data-ttu-id="59f81-286">Azure 배포가 Azure 사이트 간 VPN 연결 또는 ExpressRoute를 통해 온-프레미스 Active Directory 또는 DNS 인스턴스에 연결된 경우(이 상태를 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]에서는 *cross-premises*라 함) VM이 온-프레미스 도메인에 가입할 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-286">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="59f81-287">이 작업에 대한 고려사항에 대한 자세한 내용은 [온-프레미스 도메인에 VM 가입(Windows에만 해당)][deployment-guide-4.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-287">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <span data-ttu-id="59f81-288"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-288"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configure monitoring</span></span>
<span data-ttu-id="59f81-289">사용자의 환경에서 SAP을 지원하도록 하려면 [SAP용 Azure 고급 모니터링 확장 구성][deployment-guide-4.5]에서 설명한 대로 SAP용 Azure 모니터링 확장을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-289">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="59f81-290">[SAP 리소스][deployment-guide-2.2]에 나열된 리소스에서 SAP 모니터링 필수 조건 및 SAP 커널과 SAP 호스트 에이전트의 필수 최소 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-290">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="59f81-291">모니터링 확인</span><span class="sxs-lookup"><span data-stu-id="59f81-291">Monitoring check</span></span>
<span data-ttu-id="59f81-292">[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-292">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

#### <a name="post-deployment-steps"></a><span data-ttu-id="59f81-293">배포 후 단계</span><span class="sxs-lookup"><span data-stu-id="59f81-293">Post-deployment steps</span></span>
<span data-ttu-id="59f81-294">VM을 만들고 VM이 배포된 후 VM에 필수 소프트웨어 구성 요소를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-294">After you create the VM and the VM is deployed, you need to install the required software components in the VM.</span></span> <span data-ttu-id="59f81-295">이 유형의 VM 배포에서 배포/소프트웨어 설치 순서 때문에 설치할 소프트웨어가 Azure 내에, 다른 VM 상에 또는 연결할 수 있는 디스크로 이미 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-295">Because of the deployment/software installation sequence in this type of VM deployment, the software to be installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span></span> <span data-ttu-id="59f81-296">또는 온-프레미스 자산에 연결되는(설치 공유) 프레미스 간 시나리오 사용을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-296">Or, consider using a cross-premises scenario, in which connectivity to the on-premises assets (installation shares) is given.</span></span>

<span data-ttu-id="59f81-297">Azure에서 VM을 배포한 후 온-프레미스 환경에서와 동일한 지침 및 도구를 사용하여 VM에 SAP 소프트웨어를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-297">After you deploy your VM in Azure, follow the same guidelines and tools to install the SAP software on your VM as you would in an on-premises environment.</span></span> <span data-ttu-id="59f81-298">Azure VM에 SAP 소프트웨어를 설치할 때는 SAP 설치 미디어를 Azure VHD에 업로드 및 저장하거나 필요한 SAP 설치 미디어를 모두 포함하고 있는 파일 서버로 사용할 Azure VM을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-298">To install SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store the SAP installation media on Azure VHDs, or that you create an Azure VM that works as a file server that has all the required SAP installation media.</span></span>

<span data-ttu-id="59f81-299">[comment]: <> (MSSedusch TODO - 파일 관리(예: 파일 서버 또는 VHD)를 권장해야 하는 이유가 무엇인가요? 온-프레미스에서와 차이가 있나요?)</span><span class="sxs-lookup"><span data-stu-id="59f81-299">[comment]: <> (MSSedusch TODO why do we need to recommend a file management, for example, File Server or VHD? Is that so different from on-premises?)</span></span>

### <span data-ttu-id="59f81-300"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>시나리오 2: SAP용 사용자 지정 이미지를 사용하여 VM 배포</span><span class="sxs-lookup"><span data-stu-id="59f81-300"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenario 2: Deploying a VM with a custom image for SAP</span></span>
<span data-ttu-id="59f81-301">다른 버전의 운영 체제 또는 DBMS는 패치 요구 사항이 다르므로 Azure Marketplace에서 찾을 수 있는 이미지가 요구에 맞지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-301">Because different versions of an operating system or DBMS have different patch requirements, the images you find in the Azure Marketplace might not meet your needs.</span></span> <span data-ttu-id="59f81-302">그 대신에 나중에 다시 배포할 수 있는 고유한 OS/DBMS VM 이미지를 사용하여 VM을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-302">You might instead want to create a VM by using your own OS/DBMS VM image, which you can deploy again later.</span></span>
<span data-ttu-id="59f81-303">Linux에 대한 개인 이미지를 만들려면 Windows에 대해 개인 이미지를 만드는 방법과 다른 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-303">You use different steps to create a private image for Linux than to create one for Windows.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="59f81-305">Windows</span><span class="sxs-lookup"><span data-stu-id="59f81-305">Windows</span></span>
>
> <span data-ttu-id="59f81-306">여러 가상 컴퓨터를 배포하는 데 사용할 수 있는 Windows 이미지를 준비하려면 Windows 설정(예: Windows SID 및 호스트 이름)을 온-프레미스 VM에서 추상화 또는 일반화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-306">To prepare a Windows image that you can use to deploy multiple virtual machines, the Windows settings (like Windows SID and hostname) must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="59f81-307">[sysprep](https://msdn.microsoft.com/library/hh825084.aspx)을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-307">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) to do this.</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="59f81-309">Linux</span><span class="sxs-lookup"><span data-stu-id="59f81-309">Linux</span></span>
>
> <span data-ttu-id="59f81-310">여러 가상 컴퓨터를 배포하는 데 사용할 수 있는 Linux 이미지를 준비하려면 일부 Linux 설정을 온-프레미스 VM에서 추상화 또는 일반화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-310">To prepare a Linux image that you can use to deploy multiple virtual machines, some Linux settings must be abstracted or generalized on the on-premises VM.</span></span> <span data-ttu-id="59f81-311">`waagent -deprovision`을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-311">You can use `waagent -deprovision`  to do this.</span></span> <span data-ttu-id="59f81-312">자세한 내용은 [Azure에서 실행 중인 Linux 가상 컴퓨터 캡처][virtual-machines-linux-capture-image] 및 [Azure Linux 에이전트 사용자 가이드][virtual-machines-linux-agent-user-guide-command-line-options]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-312">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and the [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span></span>
>
>

- - -
<span data-ttu-id="59f81-313">사용자 지정 이미지를 준비하고 만든 다음 해당 이미지를 사용하여 여러 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-313">You can prepare and create a custom image, and then use it to create multiple new VMs.</span></span> <span data-ttu-id="59f81-314">이 방법을 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-314">This is described in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span> <span data-ttu-id="59f81-315">SAP Software Provision Manager를 사용하여 새 SAP 시스템을 설치하거나(가상 컴퓨터에 연결된 VHD에서 데이터베이스 백업을 복원) DBMS에서 지원하는 경우 Azure Storage에서 데이터베이스 백업을 직접 복원하여 데이터베이스 콘텐츠를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-315">Set up your database content either by using SAP Software Provisioning Manager to install a new SAP system (restores a database backup from a VHD that's attached to the virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span></span> <span data-ttu-id="59f81-316">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-316">For more information, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span> <span data-ttu-id="59f81-317">온-프레미스 VM(특히 2계층 시스템)에 SAP 시스템을 이미 설치한 경우 Azure VM을 배포한 후에 SAP Software Provisioning Manager에서 지원하는 시스템 이름 변경 절차를 사용하여 SAP 시스템 설정을 조정할 수 있습니다(SAP Note [1619720]).</span><span class="sxs-lookup"><span data-stu-id="59f81-317">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt the SAP system settings after the deployment of the Azure VM by using the System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span></span> <span data-ttu-id="59f81-318">그렇지 않은 경우 Azure VM 배포 후 SAP 소프트웨어를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-318">Otherwise, you can install the SAP software after you deploy the Azure VM.</span></span>

<span data-ttu-id="59f81-319">다음 순서도는 사용자 지정 이미지에서 VM을 배포하기 위한 SAP 관련 단계 순서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-319">The following flowchart shows the SAP-specific sequence of steps for deploying a VM from a custom image:</span></span>

![개인 Marketplace에서 VM 이미지를 사용하여 SAP 시스템용 VM 배포 순서도][deployment-guide-figure-300]

#### <a name="create-the-virtual-machine"></a><span data-ttu-id="59f81-321">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="59f81-321">Create the virtual machine</span></span>
<span data-ttu-id="59f81-322">Azure Portal에서 개인 OS 이미지를 사용하여 배포를 만들려면 다음 SAP 템플릿 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-322">To create a deployment by using a private OS image from the Azure portal, use one of the following SAP templates.</span></span> <span data-ttu-id="59f81-323">이러한 템플릿은 [azure-quickstart-templates GitHub 리포지토리][azure-quickstart-templates-github]에 게시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-323">These templates are published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="59f81-324">또한 [PowerShell][virtual-machines-upload-image-windows-resource-manager]을 사용하여 가상 컴퓨터를 수동으로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-324">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span></span>

* <span data-ttu-id="59f81-325">[**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="59f81-325">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span></span>

  <span data-ttu-id="59f81-326">한 대의 가상 컴퓨터를 사용하여 2계층 시스템을 만들려면 이 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-326">To create a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="59f81-327">[**3계층 구성(여러 가상 컴퓨터) 템플릿**(sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="59f81-327">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span></span>

  <span data-ttu-id="59f81-328">여러 대의 가상 컴퓨터 또는 고유한 OS 이미지를 사용하여 3계층 시스템을 만들려면 이 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-328">To create a three-tier system by using multiple virtual machines or your own OS image, use this template.</span></span>

<span data-ttu-id="59f81-329">Azure Portal에서 템플릿에 대한 다음 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-329">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="59f81-330">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="59f81-330">**Basics**:</span></span>
  * <span data-ttu-id="59f81-331">**구독**: 템플릿을 배포하는 데 사용하는 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-331">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="59f81-332">**리소스 그룹**: 템플릿을 배포하는 데 사용하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-332">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="59f81-333">새 리소스 그룹을 만들거나 구독에서 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-333">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="59f81-334">**위치**: 템플릿을 배포할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-334">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="59f81-335">기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 위치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-335">If you selected an existing resource group, the location of that resource group is used.</span></span>
2. <span data-ttu-id="59f81-336">**설정**:</span><span class="sxs-lookup"><span data-stu-id="59f81-336">**Settings**:</span></span>
  * <span data-ttu-id="59f81-337">**SAP 시스템 ID**: SAP 시스템 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-337">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="59f81-338">**OS 형식**: 배포하려는 운영 체제 형식(예: Windows 또는 Linux)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-338">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="59f81-339">**SAP 시스템 크기**: SAP 시스템의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-339">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="59f81-340">새 시스템에서 제공하는 SAP의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-340">The number of SAPS the new system provides.</span></span> <span data-ttu-id="59f81-341">시스템에 필요한 SAP의 수를 모를 경우 SAP 기술 파트너 또는 시스템 통합자에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-341">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="59f81-342">**시스템 가용성**(3계층 템플릿만 해당): 시스템 가용성입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-342">**System availability** (three-tier template only): The system availability.</span></span>

    <span data-ttu-id="59f81-343">고가용성 설치에 적합한 구성의 경우 **HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-343">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="59f81-344">ASCS용 2개의 데이터베이스 서버 및 2개의 서버가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-344">Two database servers and two servers for ASCS are created.</span></span>
  * <span data-ttu-id="59f81-345">**저장소 유형**(2계층 템플릿에만 해당): 사용하는 저장소 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-345">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="59f81-346">더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-346">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="59f81-347">저장소 유형에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-347">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="59f81-348">[SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]</span><span class="sxs-lookup"><span data-stu-id="59f81-348">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="59f81-349">[Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="59f81-349">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="59f81-350">[Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="59f81-350">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="59f81-351">[Microsoft Azure Storage 소개][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="59f81-351">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="59f81-352">**사용자 이미지 VHD URI**: 개인 OS 이미지 VHD의 URI(예: https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-352">**User image VHD URI**: The URI of the private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="59f81-353">**사용자 이미지 저장소 계정**: 개인 OS 이미지가 저장된 저장소 계정의 이름(예: https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd)의 &lt;accountname>)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-353">**User image storage account**: The name of the storage account where the private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="59f81-354">**관리 사용자 이름** 및 **관리 암호**: 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-354">**Admin username** and **Admin password**: The username and password.</span></span>

    <span data-ttu-id="59f81-355">가상 컴퓨터에 로그인하기 위한 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-355">A new user is created, for signing in to the virtual machine.</span></span>
  * <span data-ttu-id="59f81-356">**새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-356">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span></span> <span data-ttu-id="59f81-357">온-프레미스 네트워크에 연결되어 있는 가상 네트워크가 이미 있는 경우 **기존**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-357">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="59f81-358">**서브넷 ID**: 가상 컴퓨터를 연결할 서브넷의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-358">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="59f81-359">온-프레미스 네트워크에 가상 컴퓨터를 연결하는 데 사용할 ExpressRoute 가상 네트워크의 서브넷 또는 VPN을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-359">Select the subnet of your VPN or ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="59f81-360">ID는 일반적으로 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-360">The ID usually looks like this:</span></span>

    <span data-ttu-id="59f81-361">/subscriptions/&lt;구독 id>/resourceGroups/&lt;리소스 그룹 이름>/providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름>/subnets/&lt;서브넷 이름></span><span class="sxs-lookup"><span data-stu-id="59f81-361">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="59f81-362">**사용 약관**:</span><span class="sxs-lookup"><span data-stu-id="59f81-362">**Terms and conditions**:</span></span>  
    <span data-ttu-id="59f81-363">약관을 검토하고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-363">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="59f81-364">**구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-364">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent-linux-only"></a><span data-ttu-id="59f81-365">VM 에이전트 설치(Linux에만 해당)</span><span class="sxs-lookup"><span data-stu-id="59f81-365">Install the VM Agent (Linux only)</span></span>
<span data-ttu-id="59f81-366">이전 섹션에서 설명한 템플릿을 사용하려면 Linux 에이전트가 사용자 이미지에 이미 설치되어 있어야 하며, 그렇지 않으면 배포에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-366">To use the templates described in the preceding section, the Linux Agent must already be installed in the user image, or the deployment will fail.</span></span> <span data-ttu-id="59f81-367">[Azure VM 에이전트 다운로드, 설치 및 사용][deployment-guide-4.4]에 설명된 대로 VM 에이전트를 다운로드하고 사용자 이미지에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-367">Download and install the VM Agent in the user image as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span> <span data-ttu-id="59f81-368">템플릿을 사용하지 않는 경우 나중에 VM 에이전트를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-368">If you don’t use the templates, you also can install the VM Agent later.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="59f81-369">도메인 가입(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="59f81-369">Join a domain (Windows only)</span></span>
<span data-ttu-id="59f81-370">Azure 배포가 Azure 사이트 간 VPN 연결 또는 Azure ExpressRoute를 통해 온-프레미스 Active Directory 또는 DNS 인스턴스에 연결된 경우(이 상태를 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]에서는 *cross-premises*라 함) VM이 온-프레미스 도메인에 가입할 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-370">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="59f81-371">이 단계에 대한 고려사항에 대한 자세한 내용은 [온-프레미스 도메인에 VM 가입(Windows에만 해당)][deployment-guide-4.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-371">For more information about considerations for this step, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="59f81-372">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-372">Configure proxy settings</span></span>
<span data-ttu-id="59f81-373">온-프레미스 네트워크가 구성된 방법에 따라 VM에 프록시를 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-373">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="59f81-374">VM이 VPN 또는 ExpressRoute를 통해 온-프레미스 네트워크에 연결된 경우 인터넷에 액세스하지 못할 수도 있으며 필수 확장을 다운로드하거나 모니터링 데이터를 수집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-374">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="59f81-375">자세한 내용은 [프록시 구성][deployment-guide-configure-proxy]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-375">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="59f81-376">모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-376">Configure monitoring</span></span>
<span data-ttu-id="59f81-377">사용자의 환경에서 SAP을 지원하도록 하려면 [SAP용 Azure 고급 모니터링 확장 구성][deployment-guide-4.5]에서 설명한 대로 SAP용 Azure 모니터링 확장을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-377">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="59f81-378">[SAP 리소스][deployment-guide-2.2]에 나열된 리소스에서 SAP 모니터링 필수 조건 및 SAP 커널과 SAP 호스트 에이전트의 필수 최소 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-378">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="59f81-379">모니터링 확인</span><span class="sxs-lookup"><span data-stu-id="59f81-379">Monitoring check</span></span>
<span data-ttu-id="59f81-380">[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-380">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>




### <span data-ttu-id="59f81-381"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>시나리오 3: SAP에서 일반화되지 않은 Azure VHD를 사용하여 온-프레미스 VM 이동</span><span class="sxs-lookup"><span data-stu-id="59f81-381"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span></span>
<span data-ttu-id="59f81-382">이 시나리오에서는 온-프레미스 환경에서 특정 SAP 시스템을 Azure로 이동하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-382">In this scenario, you plan to move a specific SAP system from an on-premises environment to Azure.</span></span> <span data-ttu-id="59f81-383">OS, SAP 이진 파일 및 결과적 DBMS 이진 파일을 포함하고 있는 VHD와 함께 DBMS 데이터와 로그 파일이 있는 VHD를 Azure에 업로드하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-383">You can do this by uploading the VHD that has the OS, the SAP binaries, and eventually the DBMS binaries, plus the VHDs with the data and log files of the DBMS, to Azure.</span></span> <span data-ttu-id="59f81-384">[시나리오 2: SAP용 사용자 지정 이미지로 VM 배포][deployment-guide-3.3]에서 설명한 시나리오와는 달리 이 경우 Azure VM의 호스트 이름, SAP SID 및 SAP 사용자 계정을 온-프레미스 환경에서 구성했으므로 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-384">Unlike the scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep the hostname, SAP SID, and SAP user accounts in the Azure VM, because they were configured in the on-premises environment.</span></span> <span data-ttu-id="59f81-385">OS를 일반화할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-385">You do not need to generalize the OS.</span></span> <span data-ttu-id="59f81-386">이 시나리오는 SAP 지형의 일부는 온-프레미스를 실행하고 일부는 Azure에서 실행하는 프레미스 간 시나리오에 가장 자주 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-386">This scenario applies most often to cross-premises scenarios where part of the SAP landscape runs on-premises and part of it runs on Azure.</span></span>

<span data-ttu-id="59f81-387">이 시나리오에서 VM 에이전트는 배포하는 동안 자동으로 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-387">In this scenario, the VM Agent is not automatically installed during deployment.</span></span> <span data-ttu-id="59f81-388">SAP을 실행하려면 VM 에이전트 및 SAP용 Azure 고급 모니터링 확장이 필요하므로 가상 컴퓨터를 만든 후에 두 구성 요소를 모두 수동으로 다운로드하여 설치하고 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-388">Because the VM Agent and the Azure Enhanced Monitoring Extension for SAP required for to run SAP, you need to download, install, and enable both components manually after you create the virtual machine.</span></span>

<span data-ttu-id="59f81-389">Azure VM 에이전트에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-389">For more information about the Azure VM Agent, see the following resources.</span></span>

<span data-ttu-id="59f81-390">[comment]: <> (MSSedusch TODO - 아래 Windows 링크 업데이트)</span><span class="sxs-lookup"><span data-stu-id="59f81-390">[comment]: <> (MSSedusch TODO Update Windows Link below)</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="59f81-392">Windows</span><span class="sxs-lookup"><span data-stu-id="59f81-392">Windows</span></span>
>
> <span data-ttu-id="59f81-393"><http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx></span><span class="sxs-lookup"><span data-stu-id="59f81-393"><http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx></span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="59f81-395">Linux</span><span class="sxs-lookup"><span data-stu-id="59f81-395">Linux</span></span>
>
> <span data-ttu-id="59f81-396">[Azure Linux 에이전트 사용자 가이드][virtual-machines-linux-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="59f81-396">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span></span>
>
>

- - -

<span data-ttu-id="59f81-397">다음 순서도는 일반화되지 않은 Azure VHD를 사용하여 온-프레미스 VM을 이동하기 위한 단계의 순서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-397">The following flowchart shows the sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span></span>

![VM 디스크를 사용하여 SAP 시스템용 VM 배포 순서도][deployment-guide-figure-400]

<span data-ttu-id="59f81-399">디스크가 Azure에 이미 업로드되고 정의되어 있다고 가정하고([Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide] 참조) 다음 몇 섹션에서 설명하는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-399">Assuming that the disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), do the tasks described in the next few sections.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="59f81-400">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-400">Create a virtual machine</span></span>
<span data-ttu-id="59f81-401">Azure Portal을 통해 개인 OS 디스크를 사용하여 배포를 만들려면 [azure-quickstart-templates GitHub 리포지토리][azure-quickstart-templates-github]에 게시된 SAP 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-401">To create a deployment by using a private OS disk through the Azure portal, use the SAP template published in the [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="59f81-402">또한 PowerShell을 사용하여 가상 컴퓨터를 직접 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-402">You also can manually create a virtual machine, by using PowerShell.</span></span>

* <span data-ttu-id="59f81-403">[**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span><span class="sxs-lookup"><span data-stu-id="59f81-403">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span></span>

  <span data-ttu-id="59f81-404">한 대의 가상 컴퓨터를 사용하여 2계층 시스템을 만들려면 이 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-404">To create a two-tier system by using only one virtual machine, use this template.</span></span>

<span data-ttu-id="59f81-405">Azure Portal에서 템플릿에 대한 다음 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-405">In the Azure portal, enter the following parameters for the template:</span></span>

1. <span data-ttu-id="59f81-406">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="59f81-406">**Basics**:</span></span>
  * <span data-ttu-id="59f81-407">**구독**: 템플릿을 배포하는 데 사용하는 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-407">**Subscription**: The subscription to use to deploy the template.</span></span>
  * <span data-ttu-id="59f81-408">**리소스 그룹**: 템플릿을 배포하는 데 사용하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-408">**Resource group**: The resource group to use to deploy the template.</span></span> <span data-ttu-id="59f81-409">새 리소스 그룹을 만들거나 구독에서 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-409">You can create a new resource group or select an existing resource group in the subscription.</span></span>
  * <span data-ttu-id="59f81-410">**위치**: 템플릿을 배포할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-410">**Location**: Where to deploy the template.</span></span> <span data-ttu-id="59f81-411">기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 위치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-411">If you selected an existing resource group, the location of that resource group is used.</span></span>
2. <span data-ttu-id="59f81-412">**설정**:</span><span class="sxs-lookup"><span data-stu-id="59f81-412">**Settings**:</span></span>
  * <span data-ttu-id="59f81-413">**SAP 시스템 ID**: SAP 시스템 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-413">**SAP System ID**: The SAP System ID.</span></span>
  * <span data-ttu-id="59f81-414">**OS 형식**: 배포하려는 운영 체제 형식(예: Windows 또는 Linux)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-414">**OS type**: The operating system type you want to deploy (Windows or Linux).</span></span>
  * <span data-ttu-id="59f81-415">**SAP 시스템 크기**: SAP 시스템의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-415">**SAP system size**: The size of the SAP system.</span></span>

    <span data-ttu-id="59f81-416">새 시스템에서 제공하는 SAP의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-416">The number of SAPS the new system provides.</span></span> <span data-ttu-id="59f81-417">시스템에 필요한 SAP의 수를 모를 경우 SAP 기술 파트너 또는 시스템 통합자에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-417">If you are not sure how many SAPS the system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="59f81-418">**저장소 유형**(2계층 템플릿에만 해당): 사용하는 저장소 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-418">**Storage type** (two-tier template only): The type of storage to use.</span></span>

    <span data-ttu-id="59f81-419">더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-419">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="59f81-420">저장소 유형에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-420">For more information about storage types, see the following resources:</span></span>
      * <span data-ttu-id="59f81-421">[SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]</span><span class="sxs-lookup"><span data-stu-id="59f81-421">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="59f81-422">[Linux에서 SAP용 Azure Virtual Machine DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="59f81-422">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="59f81-423">[Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="59f81-423">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="59f81-424">[Microsoft Azure Storage 소개][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="59f81-424">[Introduction to Microsoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="59f81-425">**OS 디스크 VHD URI**: 개인 OS 디스크의 URI(예: https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd)입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-425">**OS disk VHD URI**: The URI of the private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span></span>
  * <span data-ttu-id="59f81-426">**새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-426">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span></span> <span data-ttu-id="59f81-427">온-프레미스 네트워크에 연결되어 있는 가상 네트워크가 이미 있는 경우 **기존**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-427">If you already have a virtual network that is connected to your on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="59f81-428">**서브넷 ID**: 가상 컴퓨터를 연결할 서브넷의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-428">**Subnet ID**: The ID of the subnet to which the virtual machines will connect to.</span></span> <span data-ttu-id="59f81-429">온-프레미스 네트워크에 가상 컴퓨터를 연결하는 데 사용할 Azure ExpressRoute 가상 네트워크의 서브넷 또는 VPN을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-429">Select the subnet of your VPN or Azure ExpressRoute virtual network to use to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="59f81-430">ID는 일반적으로 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-430">The ID usually looks like this:</span></span>

    <span data-ttu-id="59f81-431">/subscriptions/&lt;구독 id>/resourceGroups/&lt;리소스 그룹 이름>/providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름>/subnets/&lt;서브넷 이름></span><span class="sxs-lookup"><span data-stu-id="59f81-431">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="59f81-432">**사용 약관**:</span><span class="sxs-lookup"><span data-stu-id="59f81-432">**Terms and conditions**:</span></span>  
    <span data-ttu-id="59f81-433">약관을 검토하고 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-433">Review and accept the legal terms.</span></span>

4.  <span data-ttu-id="59f81-434">**구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-434">Select **Purchase**.</span></span>

#### <a name="install-the-vm-agent"></a><span data-ttu-id="59f81-435">VM 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="59f81-435">Install the VM Agent</span></span>
<span data-ttu-id="59f81-436">이전 섹션에서 설명한 템플릿을 사용하려면 VM 에이전트가 OS 디스크에 설치되어 있어야 하며, 그렇지 않으면 배포에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-436">To use the templates described in the preceding section, the VM Agent must be installed on the OS disk, or the deployment will fail.</span></span> <span data-ttu-id="59f81-437">[Azure VM 에이전트 다운로드, 설치 및 사용][deployment-guide-4.4]에 설명된 대로 VM 에이전트를 다운로드하고 VM에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-437">Download and install the VM Agent in the VM, as described in [Download, install, and enable the Azure VM Agent][deployment-guide-4.4].</span></span>

<span data-ttu-id="59f81-438">이전 섹션에서 설명한 템플릿을 사용하지 않는 경우 나중에 VM 에이전트를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-438">If you don’t use the templates described in the preceding section, you can also install the VM Agent afterwards.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="59f81-439">도메인 가입(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="59f81-439">Join a domain (Windows only)</span></span>
<span data-ttu-id="59f81-440">Azure 배포가 Azure 사이트 간 VPN 연결 또는 ExpressRoute를 통해 온-프레미스 Active Directory 또는 DNS 인스턴스에 연결된 경우(이 상태를 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]에서는 *cross-premises*라 함) VM이 온-프레미스 도메인에 가입할 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-440">If your Azure deployment is connected to an on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that the VM is joining an on-premises domain.</span></span> <span data-ttu-id="59f81-441">이 작업에 대한 고려사항에 대한 자세한 내용은 [온-프레미스 도메인에 VM 가입(Windows에만 해당)][deployment-guide-4.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-441">For more information about considerations for this task, see [Join a VM to an on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="59f81-442">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-442">Configure proxy settings</span></span>
<span data-ttu-id="59f81-443">온-프레미스 네트워크가 구성된 방법에 따라 VM에 프록시를 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-443">Depending on how your on-premises network is configured, you might need to set up the proxy on your VM.</span></span> <span data-ttu-id="59f81-444">VM이 VPN 또는 ExpressRoute를 통해 온-프레미스 네트워크에 연결된 경우 인터넷에 액세스하지 못할 수도 있으며 필수 확장을 다운로드하거나 모니터링 데이터를 수집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-444">If your VM is connected to your on-premises network via VPN or ExpressRoute, the VM might not be able to access the Internet, and won't be able to download the required extensions or collect monitoring data.</span></span> <span data-ttu-id="59f81-445">자세한 내용은 [프록시 구성][deployment-guide-configure-proxy]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-445">For more information, see [Configure the proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="59f81-446">모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-446">Configure monitoring</span></span>
<span data-ttu-id="59f81-447">사용자의 환경에서 SAP을 지원하도록 하려면 [SAP용 Azure 고급 모니터링 확장 구성][deployment-guide-4.5]에서 설명한 대로 SAP용 Azure 모니터링 확장을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-447">To be sure your environment supports SAP, set up the Azure Monitoring Extension for SAP as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="59f81-448">[SAP 리소스][deployment-guide-2.2]에 나열된 리소스에서 SAP 모니터링 필수 조건 및 SAP 커널과 SAP 호스트 에이전트의 필수 최소 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-448">Check the prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in the resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="59f81-449">모니터링 확인</span><span class="sxs-lookup"><span data-stu-id="59f81-449">Monitoring check</span></span>
<span data-ttu-id="59f81-450">[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-450">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

## <a name="update-the-monitoring-configuration-for-sap"></a><span data-ttu-id="59f81-451">SAP용 모니터링 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="59f81-451">Update the monitoring configuration for SAP</span></span>
<span data-ttu-id="59f81-452">다음과 시나리오에서 SAP 모니터링 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-452">Update the SAP monitoring configuration in any of the following scenarios:</span></span>
* <span data-ttu-id="59f81-453">Microsoft/SAP 공동 팀은 모니터링 기능을 확장했으며 더 많거나 적은 카운터를 요청하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-453">The joint Microsoft/SAP team extends the monitoring capabilities and requests more or fewer counters.</span></span>
* <span data-ttu-id="59f81-454">Microsoft는 모니터링 데이터를 제공하는 새 버전의 기본 Azure 인프라를 도입했으며, SAP용 Azure 고급 모니터링 확장은 이러한 변화에 적응해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-454">Microsoft introduces a new version of the underlying Azure infrastructure that delivers the monitoring data, and the Azure Enhanced Monitoring Extension for SAP needs to be adapted to those changes.</span></span>
* <span data-ttu-id="59f81-455">Azure VM에서 VHD를 추가로 탑재하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-455">You mount additional VHDs to your Azure VM or you remove a VHD.</span></span> <span data-ttu-id="59f81-456">이 시나리오에서 저장소 관련 데이터의 컬렉션을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-456">In this scenario, update the collection of storage-related data.</span></span> <span data-ttu-id="59f81-457">끝점을 추가 또는 삭제하거나 VM에 IP 주소를 할당하여 구성을 변경해도 모니터링 구성에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-457">Changing your configuration by adding or deleting endpoints or by assigning IP addresses to a VM does not affect the monitoring configuration.</span></span>
* <span data-ttu-id="59f81-458">Azure VM의 크기를 변경합니다(예: 크기 A5에서 다른 VM 크기로).</span><span class="sxs-lookup"><span data-stu-id="59f81-458">You change the size of your Azure VM, for example, from size A5 to any other VM size.</span></span>
* <span data-ttu-id="59f81-459">Azure VM에 새 네트워크 인터페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-459">You add new network interfaces to your Azure VM.</span></span>

<span data-ttu-id="59f81-460">모니터링 설정을 업데이트하려면 [SAP 용 Azure 고급 모니터링 확장][deployment-guide-4.5]의 절차에 따라 모니터링 인프라를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-460">To update monitoring settings, update the monitoring infrastructure by following the steps in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a><span data-ttu-id="59f81-461">Linux VM에서 SAP 소프트웨어 배포에 대한 세부 작업</span><span class="sxs-lookup"><span data-stu-id="59f81-461">Detailed tasks for SAP software deployment on a Windows VM</span></span>
<span data-ttu-id="59f81-462">이 섹션에서는 구성 및 배포 프로세스에서 특정 작업을 수행하기 위한 세부 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-462">This section has detailed steps for doing specific tasks in the configuration and deployment process.</span></span>

### <span data-ttu-id="59f81-463"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Azure PowerShell cmdlet 배포</span><span class="sxs-lookup"><span data-stu-id="59f81-463"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Deploy Azure PowerShell cmdlets</span></span>
1.  <span data-ttu-id="59f81-464">[Microsoft Azure 다운로드](https://azure.microsoft.com/downloads/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-464">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="59f81-465">**명령줄 도구** 아래의 **PowerShell** 아래에서 **Windows 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-465">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span></span>
3.  <span data-ttu-id="59f81-466">Microsoft Download Manager 대화 상자에서 다운로드한 파일(예: WindowsAzurePowershellGet.3f.3f.3fnew.exe)에 대해 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-466">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="59f81-467">Microsoft 웹 플랫폼 설치 관리자(Microsoft Web PI)를 실행하려면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-467">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="59f81-468">다음과 같은 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-468">A page that looks like this appears:</span></span>

  <span data-ttu-id="59f81-469">![Azure PowerShell cmdlet 설치 페이지][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="59f81-469">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="59f81-470">**설치**를 선택한 다음 Microsoft 소프트웨어 사용 조건에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-470">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="59f81-471">PowerShell이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-471">PowerShell is installed.</span></span> <span data-ttu-id="59f81-472">**마침**을 선택하여 설치 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-472">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="59f81-473">일반적으로 매월 업데이트되는 PowerShell cmdlet에 대한 업데이트를 자주 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="59f81-473">Check frequently for updates to the PowerShell cmdlets, which usually are updated monthly.</span></span> <span data-ttu-id="59f81-474">업데이트를 확인하는 가장 쉬운 방법은 앞의 설치 단계를 5단계에 표시되는 설치 페이지까지 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-474">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span> <span data-ttu-id="59f81-475">cmdlet의 릴리스 날짜 및 릴리스 번호는 5단계에 표시되는 페이지에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-475">The release date and release number of the cmdlets are included on the page shown in step 5.</span></span> <span data-ttu-id="59f81-476">SAP Note [1928533] 또는 SAP Note [2015553]에 달리 명시되지 않은 한 Azure PowerShell cmdlet의 최신 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-476">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with the latest version of Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="59f81-477">컴퓨터에 설치된 Azure PowerShell cmdlet의 버전을 확인하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-477">To check the version of the Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span></span>
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
<span data-ttu-id="59f81-478">결과는 다음과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-478">The result looks like this:</span></span>

<span data-ttu-id="59f81-479">![Azure PowerShell cmdlet 버전 검사의 결과][deployment-guide-figure-600]
<a name="figure-6"></a></span><span class="sxs-lookup"><span data-stu-id="59f81-479">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span></span>

<span data-ttu-id="59f81-480">컴퓨터에 설치된 Azure cmdlet 버전이 현재 버전인 경우 설치 마법사의 첫 페이지의 제품 제목에 **(설치됨)**을 추가하여 이 사실을 표시합니다(다음 스크린샷 참조).</span><span class="sxs-lookup"><span data-stu-id="59f81-480">If the Azure cmdlet version installed on your computer is the current version, the first page of the installation wizard indicates it by adding **(Installed)** to the product title (see the following screenshot).</span></span> <span data-ttu-id="59f81-481">사용자의 PowerShell Azure cmdlet은 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-481">Your PowerShell Azure cmdlets are up-to-date.</span></span> <span data-ttu-id="59f81-482">설치 마법사를 닫으려면 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-482">To close the installation wizard, select **Exit**.</span></span>

<span data-ttu-id="59f81-483">![Azure PowerShell cmdlet의 최신 버전이 설치되었음을 나타내는 Azure PowerShell cmdlet 설치 페이지][deployment-guide-figure-700]
<a name="figure-7"></a></span><span class="sxs-lookup"><span data-stu-id="59f81-483">![Installation page for Azure PowerShell cmdlets indicating that the most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span></span>

### <span data-ttu-id="59f81-484"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Azure CLI 배포</span><span class="sxs-lookup"><span data-stu-id="59f81-484"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Deploy Azure CLI</span></span>
1.  <span data-ttu-id="59f81-485">[Microsoft Azure 다운로드](https://azure.microsoft.com/downloads/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-485">Go to [Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="59f81-486">**명령줄 도구** 아래의 **Azure 명령줄 인터페이스** 아래에서 운영 체제에 대한 **설치** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-486">Under **Command-line tools**, under **Azure command-line interface**, select the **Install** link for your operating system.</span></span>
3.  <span data-ttu-id="59f81-487">Microsoft Download Manager 대화 상자에서 다운로드한 파일(예: WindowsAzureXPlatCLI.3f.3f.3fnew.exe)에 대해 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-487">In the Microsoft Download Manager dialog box, for the downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="59f81-488">Microsoft 웹 플랫폼 설치 관리자(Microsoft Web PI)를 실행하려면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-488">To run Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="59f81-489">다음과 같은 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-489">A page that looks like this appears:</span></span>

  <span data-ttu-id="59f81-490">![Azure PowerShell cmdlet 설치 페이지][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="59f81-490">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="59f81-491">**설치**를 선택한 다음 Microsoft 소프트웨어 사용 조건에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-491">Select **Install**, and then accept the Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="59f81-492">Azure CLI가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-492">Azure CLI is installed.</span></span> <span data-ttu-id="59f81-493">**마침**을 선택하여 설치 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-493">Select **Finish** to close the installation wizard.</span></span>

<span data-ttu-id="59f81-494">일반적으로 매월 업데이트 되는 Azure CLI에 대한 업데이트를 자주 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="59f81-494">Check frequently for updates to Azure CLI, which usually is updated monthly.</span></span> <span data-ttu-id="59f81-495">업데이트를 확인하는 가장 쉬운 방법은 앞의 설치 단계를 5단계에 표시되는 설치 페이지까지 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-495">The easiest way to check for updates is to do the preceding installation steps, up to the installation page shown in step 5.</span></span>


<span data-ttu-id="59f81-496">컴퓨터에 설치된 Azure CLI의 버전을 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-496">To check the version of Azure CLI that is installed on your computer, run this command:</span></span>
```
azure --version
```

<span data-ttu-id="59f81-497">결과는 다음과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-497">The result looks like this:</span></span>

<span data-ttu-id="59f81-498">![Azure CLI 버전 검사의 결과][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span><span class="sxs-lookup"><span data-stu-id="59f81-498">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span></span>

### <span data-ttu-id="59f81-499"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>온-프레미스 도메인에 VM 가입(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="59f81-499"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Join a VM to an on-premises domain (Windows only)</span></span>
<span data-ttu-id="59f81-500">온-프레미스 Active Directory 및 DNS가 Azure로 확장되는 프레미스 간 시나리오에서 SAP VM을 배포하는 경우 VM은 온-프레미스 도메인에 가입될 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-500">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that the VMs are joining an on-premises domain.</span></span> <span data-ttu-id="59f81-501">온-프레미스 도메인에 VM을 가입하는 세부 단계 및 온-프레미스 도메인의 멤버가 되기 위해 필요한 추가 소프트웨어는 고객마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-501">The detailed steps you take to join a VM to an on-premises domain, and the additional software required to be a member of an on-premises domain, varies by customer.</span></span> <span data-ttu-id="59f81-502">일반적으로 VM을 온-프레미스 도메인에 가입하려면 맬웨어 방지 소프트웨어와 같은 추가 소프트웨어 및 백업 또는 모니터링 소프트웨어를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-502">Usually, to join a VM to an on-premises domain, you need to install additional software, like antimalware software, and backup or monitoring software.</span></span>

<span data-ttu-id="59f81-503">이 시나리오에서 VM이 환경의 도메인에 가입할 때 인터넷 프록시 설정이 강제로 적용된 경우 게스트 VM의 Windows 로컬 시스템 계정(S-1-5-18)이 동일한 프록시 설정을 포함하고 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-503">In this scenario, you also need to make sure that if Internet proxy settings are forced when a VM joins a domain in your environment, the Windows Local System Account (S-1-5-18) in the Guest VM has the same proxy settings.</span></span> <span data-ttu-id="59f81-504">가장 쉬운 방법은 도메인 내 시스템에 적용하는 도메인 그룹 정책을 사용하여 프록시를 강제 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-504">The easiest option is to force the proxy by using a domain Group Policy, which applies to systems in the domain.</span></span>

### <span data-ttu-id="59f81-505"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Azure VM 에이전트 다운로드, 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="59f81-505"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Download, install, and enable the Azure VM Agent</span></span>
<span data-ttu-id="59f81-506">일반화되지 않은 OS 이미지(예: Windows 시스템 준비 도구 또는 sysprep)에서 배포된 가상 컴퓨터의 경우 Azure VM 에이전트를 수동으로 다운로드, 설치 및 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-506">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in the Windows System Preparation, or sysprep, tool), you need to manually download, install, and enable the Azure VM Agent.</span></span>

<span data-ttu-id="59f81-507">Azure Marketplace에서 VM을 배포하는 경우 이 단계가 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-507">If you deploy a VM from the Azure Marketplace, this step is not required.</span></span> <span data-ttu-id="59f81-508">Azure Marketplace의 이미지는 Azure VM 에이전트를 이미 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-508">Images from the Azure Marketplace already have the Azure VM Agent.</span></span>

#### <span data-ttu-id="59f81-509"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span><span class="sxs-lookup"><span data-stu-id="59f81-509"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span></span>
1.  <span data-ttu-id="59f81-510">Azure VM 에이전트 다운로드:</span><span class="sxs-lookup"><span data-stu-id="59f81-510">Download the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="59f81-511">[Azure VM 에이전트 설치 관리자 패키지](https://go.microsoft.com/fwlink/?LinkId=394789)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-511">Download the [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span></span>
  2.  <span data-ttu-id="59f81-512">VM 에이전트 MSI 패키지를 PC 또는 서버에 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-512">Store the VM Agent MSI package locally on a personal computer or server.</span></span>
2.  <span data-ttu-id="59f81-513">Azure VM 에이전트 설치:</span><span class="sxs-lookup"><span data-stu-id="59f81-513">Install the Azure VM Agent:</span></span>
  1.  <span data-ttu-id="59f81-514">RDP(원격 데스크톱 프로토콜)를 사용하여 배포된 Azure VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-514">Connect to the deployed Azure VM by using Remote Desktop Protocol (RDP).</span></span>
  2.  <span data-ttu-id="59f81-515">VM에서 [Windows 탐색기] 창을 열고 VM 에이전트의 MSI 파일에 대한 대상 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-515">Open a Windows Explorer window on the VM and select the target directory for the MSI file of the VM Agent.</span></span>
  3.  <span data-ttu-id="59f81-516">로컬 컴퓨터/서버에서 VM의 VM 에이전트 대상 디렉터리로 Azure VM 에이전트 설치 관리자 MSI 파일을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-516">Drag the Azure VM Agent Installer MSI file from your local computer/server to the target directory of the VM Agent on the VM.</span></span>
  4.  <span data-ttu-id="59f81-517">VM에서 MSI 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-517">Double-click the MSI file on the VM.</span></span>
3.  <span data-ttu-id="59f81-518">온-프레미스 도메인에 가입된 VM의 경우 [프록시 구성][deployment-guide-configure-proxy]에서 설명한 대로 최종 인터넷 프록시 설정이 VM의 Windows 로컬 시스템 계정(S-1-5-18)에도 적용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-518">For VMs that are joined to on-premises domains, make sure that eventual Internet proxy settings also apply to the Windows Local System account (S-1-5-18) in the VM, as described in [Configure the proxy][deployment-guide-configure-proxy].</span></span> <span data-ttu-id="59f81-519">VM 에이전트를 이 컨텍스트에서 실행하고 Azure에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-519">The VM Agent runs in this context and needs to be able to connect to Azure.</span></span>

<span data-ttu-id="59f81-520">사용자 개입 없이 Azure VM 에이전트를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-520">No user interaction is required to update the Azure VM Agent.</span></span> <span data-ttu-id="59f81-521">VM 에이전트가 자동으로 업데이트되며 VM을 다시 시작할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-521">The VM Agent is automatically updated, and does not require a VM restart.</span></span>

#### <span data-ttu-id="59f81-522"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span><span class="sxs-lookup"><span data-stu-id="59f81-522"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span></span>
<span data-ttu-id="59f81-523">다음 명령을 사용하여 Linux용 VM 에이전트를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-523">Use the following commands to install the VM Agent for Linux:</span></span>

* <span data-ttu-id="59f81-524">**SELS(SUSE Linux Enterprise Server)**</span><span class="sxs-lookup"><span data-stu-id="59f81-524">**SUSE Linux Enterprise Server (SLES)**</span></span>

  ```
  sudo zypper install WALinuxAgent
  ```

* <span data-ttu-id="59f81-525">**RHEL(Red Hat Enterprise Linux)**</span><span class="sxs-lookup"><span data-stu-id="59f81-525">**Red Hat Enterprise Linux (RHEL)**</span></span>

  ```
  sudo yum install WALinuxAgent
  ```

<span data-ttu-id="59f81-526">에이전트가 이미 설치된 경우 Azure Linux 에이전트를 업데이트하려면 [GitHub에서 VM의 Azure Linux 에이전트를 최신 버전으로 업데이트][virtual-machines-linux-update-agent]에서 설명한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-526">If the agent is already installed, to update the Azure Linux Agent, do the steps described in [Update the Azure Linux Agent on a VM to the latest version from GitHub][virtual-machines-linux-update-agent].</span></span>

### <span data-ttu-id="59f81-527"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>프록시 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-527"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configure the proxy</span></span>
<span data-ttu-id="59f81-528">Windows에서 프록시를 구성하기 위해 거치는 단계는 Linux에서 프록시를 구성하는 방법과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-528">The steps you take to configure the proxy in Windows are different from the way you configure the proxy in Linux.</span></span>

#### <a name="windows"></a><span data-ttu-id="59f81-529">Windows</span><span class="sxs-lookup"><span data-stu-id="59f81-529">Windows</span></span>
<span data-ttu-id="59f81-530">로컬 시스템 계정이 인터넷에 액세스하려면 프록시 설정을 올바르게 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-530">Proxy settings must be set up correctly for the Local System account to access the Internet.</span></span> <span data-ttu-id="59f81-531">그룹 정책으로 프록시 설정을 지정하지 않은 경우 로컬 시스템 계정에 대해 프록시 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-531">If your proxy settings are not set by Group Policy, you can configure the settings for the Local System account.</span></span>

1. <span data-ttu-id="59f81-532">**시작**으로 이동하고 **gpedit.msc**를 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-532">Go to **Start**, enter **gpedit.msc**, and then select **Enter**.</span></span>
2. <span data-ttu-id="59f81-533">**컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소** > **Internet Explorer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-533">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span></span> <span data-ttu-id="59f81-534">**사용자 단위보다는 컴퓨터 단위로 프록시 설정 만들기**가 사용하지 않도록 설정되거나 구성되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-534">Make sure that the setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span></span>
3. <span data-ttu-id="59f81-535">**제어판**에서 **네트워크 및 공유 센터** > **인터넷 옵션**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-535">In **Control Panel**, go to **Network and Sharing Center** > **Internet Options**.</span></span>
4. <span data-ttu-id="59f81-536">**연결** 탭에서 **LAN 설정** 버튼을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-536">On the **Connections** tab, select the **LAN settings** button.</span></span>
5. <span data-ttu-id="59f81-537">**자동으로 설정 검색**을 확인란을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-537">Clear the **Automatically detect settings** check box.</span></span>
6. <span data-ttu-id="59f81-538">**LAN에 프록시 서버 사용**을 선택한 다음 프록시 주소 및 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-538">Select the **Use a proxy server for your LAN** check box, and then enter the proxy address and port.</span></span>
7. <span data-ttu-id="59f81-539">**고급** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-539">Select the **Advanced** button.</span></span>
8. <span data-ttu-id="59f81-540">**예외** 상자에 IP 주소 **168.63.129.16**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-540">In the **Exceptions** box, enter the IP address **168.63.129.16**.</span></span> <span data-ttu-id="59f81-541">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-541">Select **OK**.</span></span>


#### <a name="linux"></a><span data-ttu-id="59f81-542">Linux</span><span class="sxs-lookup"><span data-stu-id="59f81-542">Linux</span></span>
<span data-ttu-id="59f81-543">\\etc\\waagent.conf에 있는 Microsoft Azure 게스트 에이전트의 구성 파일에서 올바른 프록시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-543">Configure the correct proxy in the configuration file of the Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span></span>

<span data-ttu-id="59f81-544">다음 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-544">Set the following parameters:</span></span>

1.  <span data-ttu-id="59f81-545">**HTTP 프록시 호스트**</span><span class="sxs-lookup"><span data-stu-id="59f81-545">**HTTP proxy host**.</span></span> <span data-ttu-id="59f81-546">예를 들어 **proxy.corp.local**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-546">For example, set it to **proxy.corp.local**.</span></span>
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  <span data-ttu-id="59f81-547">**HTTP 프록시 포트**</span><span class="sxs-lookup"><span data-stu-id="59f81-547">**HTTP proxy port**.</span></span> <span data-ttu-id="59f81-548">예를 들어 **80**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-548">For example, set it to **80**.</span></span>
  ```
  HttpProxy.Port=<port of the proxy host>

  ```
3.  <span data-ttu-id="59f81-549">에이전트를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-549">Restart the agent.</span></span>

  ```
  sudo service waagent restart
  ```

<span data-ttu-id="59f81-550">\\etc\\waagent.conf의 프록시 설정은 필요한 VM 확장에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-550">The proxy settings in \\etc\\waagent.conf also apply to the required VM extensions.</span></span> <span data-ttu-id="59f81-551">Azure 리포지토리를 사용하려는 경우 이러한 리포지토리에 대한 트래픽이 온-프레미스 인트라넷을 통해 전달되지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-551">If you want to use the Azure repositories, make sure that the traffic to these repositories is not going through your on-premises intranet.</span></span> <span data-ttu-id="59f81-552">강제 터널링을 사용하도록 사용자 정의 경로를 만든 경우 사이트 간 VPN 연결을 통해서가 아니라 인터넷에 직접 리포지토리로 트래픽을 라우트하는 경로를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-552">If you created user-defined routes to enable forced tunneling, make sure that you add a route that routes traffic to the repositories directly to the Internet, and not through your site-to-site VPN connection.</span></span>

* <span data-ttu-id="59f81-553">**SLES**</span><span class="sxs-lookup"><span data-stu-id="59f81-553">**SLES**</span></span>

  <span data-ttu-id="59f81-554">\\etc\\regionserverclnt.cfg에 나열된 IP 주소에 대한 경로도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-554">You also need to add routes for the IP addresses listed in \\etc\\regionserverclnt.cfg.</span></span> <span data-ttu-id="59f81-555">다음 그림은 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-555">The following figure shows an example:</span></span>

  ![강제 터널링][deployment-guide-figure-50]


* <span data-ttu-id="59f81-557">**RHEL**</span><span class="sxs-lookup"><span data-stu-id="59f81-557">**RHEL**</span></span>

  <span data-ttu-id="59f81-558">\\etc\\yum.repos.d\\rhui-load-balancers에 나열된 호스트의 IP 주소에 대한 경로도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-558">You also need to add routes for the IP addresses of the hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span></span> <span data-ttu-id="59f81-559">예는 앞의 그림을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-559">For an example, see the preceding figure.</span></span>

<span data-ttu-id="59f81-560">사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달][virtual-networks-udr-overview]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-560">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span></span>

### <span data-ttu-id="59f81-561"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>SAP용 Azure 고급 모니터링 확장 구성</span><span class="sxs-lookup"><span data-stu-id="59f81-561"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configure the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="59f81-562">[Azure에서 SAP용 VM 배포 시나리오][deployment-guide-3]에서 설명한 대로 VM을 준비한 경우 Azure VM 에이전트가 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-562">When you've prepared the VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], the Azure VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="59f81-563">다음 단계는 글로벌 Azure 데이터 센터에 있는 Azure 확장 리포지토리에서 사용할 수 있는 SAP용 Azure 고급 모니터링 확장을 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-563">The next step is to deploy the Azure Enhanced Monitoring Extension for SAP, which is available in the Azure Extension Repository in the global Azure datacenters.</span></span> <span data-ttu-id="59f81-564">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide-9.1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-564">For more information, see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide-9.1].</span></span>

<span data-ttu-id="59f81-565">PowerShell 또는 Azure CLI를 사용하여 SAP용 Azure 고급 모니터링 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-565">You can use PowerShell or Azure CLI to install and configure the Azure Enhanced Monitoring Extension for SAP.</span></span> <span data-ttu-id="59f81-566">Windows 컴퓨터를 사용하여 Windows 또는 Linux VM에 확장을 설치하려는 경우 [Azure PowerShell][deployment-guide-4.5.1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-566">To install the extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span></span> <span data-ttu-id="59f81-567">Linux 데스크톱을 사용하여 Linux VM에 확장을 설치하려면 [Azure CLI][deployment-guide-4.5.2]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-567">To install the extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span></span>

#### <span data-ttu-id="59f81-568"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Linux 및 Windows VM용 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="59f81-568"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell for Linux and Windows VMs</span></span>
<span data-ttu-id="59f81-569">PowerShell을 사용하여 SAP용 Azure 고급 모니터링 확장을 설치하려면:</span><span class="sxs-lookup"><span data-stu-id="59f81-569">To install the Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span></span>

1. <span data-ttu-id="59f81-570">최신 버전의 Azure PowerShell cmdlet을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-570">Make sure that you have installed the latest version of the Azure PowerShell cmdlet.</span></span> <span data-ttu-id="59f81-571">자세한 내용은 [Azure PowerShell cmdlet 배포][deployment-guide-4.1]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-571">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>  
2. <span data-ttu-id="59f81-572">다음 PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-572">Run the following PowerShell cmdlet.</span></span>
  <span data-ttu-id="59f81-573">사용 가능한 환경 목록을 보려면 `commandlet Get-AzureRmEnvironment`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-573">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="59f81-574">공용 Azure를 사용하려는 경우 환경은 **AzureCloud**입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-574">If you want to use public Azure, your environment is **AzureCloud**.</span></span> <span data-ttu-id="59f81-575">중국의 Azure인 경우 **AzureChinaCloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-575">For Azure in China, select **AzureChinaCloud**.</span></span>


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of the environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

<span data-ttu-id="59f81-576">계정 데이터 및 Azure Virtual Machine을 입력한 후 스크립트가 필수 확장을 배포하고 필요한 기능을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-576">After you enter your account data and identify the Azure virtual machine, the script deploys the required extensions and enables the required features.</span></span> <span data-ttu-id="59f81-577">이 작업은 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-577">This can take several minutes.</span></span>
<span data-ttu-id="59f81-578">`Set-AzureRmVMAEMExtension`에 대한 자세한 내용은[Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-578">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span></span>

![SAP 관련 Azure cmdlet Set-AzureRmVMAEMExtension의 성공적인 실행][deployment-guide-figure-900]

<span data-ttu-id="59f81-580">`Set-AzureRmVMAEMExtension` 구성은 SAP을 위해 호스트 모니터링을 구성하는 모든 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-580">The `Set-AzureRmVMAEMExtension` configuration does all the steps to configure host monitoring for SAP.</span></span>

<span data-ttu-id="59f81-581">스크립트 출력에는 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-581">The script output includes the following information:</span></span>

* <span data-ttu-id="59f81-582">기본 VHD(OS 포함)와 VM에 탑재된 모든 추가 VHD에 대한 모니터링이 구성되었다는 확인이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-582">Confirmation that monitoring for the base VHD (with the OS) and all additional VHDs mounted to the VM has been configured.</span></span>
* <span data-ttu-id="59f81-583">다음 두 개의 메시지는 특정 저장소 계정에 대한 저장소 메트릭의 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-583">The next two messages confirm the configuration of Storage Metrics for a specific storage account.</span></span>
* <span data-ttu-id="59f81-584">출력 한 줄에는 모니터링 구성의 실제 업데이트 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-584">One line of output gives the status of the actual update of the monitoring configuration.</span></span>
* <span data-ttu-id="59f81-585">출력의 또 다른 줄은 구성이 배포되거나 업데이트되었음을 확인해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-585">Another line of output confirms that the configuration has been deployed or updated.</span></span>
* <span data-ttu-id="59f81-586">출력의 마지막 줄은 정보 제공용이며,</span><span class="sxs-lookup"><span data-stu-id="59f81-586">The last line of output is informational.</span></span> <span data-ttu-id="59f81-587">모니터링 구성을 테스트 하는 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-587">It shows your options for testing the monitoring configuration.</span></span>

<span data-ttu-id="59f81-588">Azure 고급 모니터링의 모든 단계가 성공적으로 실행되고 Azure 인프라가 필요한 데이터를 제공하는지 확인하려면 [SAP용 Azure 고급 모니터링에 대한 준비 검사][deployment-guide-5.1]에 설명된 대로 SAP용 Azure 고급 모니터링 확장에 대한 준비 검사를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-588">To check that all steps of Azure Enhanced Monitoring have been executed successfully, and that the Azure Infrastructure provides the necessary data, proceed with the readiness check for the Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="59f81-589">Azure 진단이 관련 데이터를 수집하도록 15-30 분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-589">Wait 15-30 minutes for Azure Diagnostics to collect the relevant data.</span></span>

#### <span data-ttu-id="59f81-590"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Linux VM용 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="59f81-590"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI for Linux VMs</span></span>
<span data-ttu-id="59f81-591">Azure CLI를 사용하여 SAP용 Azure 고급 모니터링 확장을 설치하려면:</span><span class="sxs-lookup"><span data-stu-id="59f81-591">To install the Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span></span>

1. <span data-ttu-id="59f81-592">[Azure CLI 설치][azure-cli]에 설명한 대로 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-592">Install Azure CLI, as described in [Install the Azure CLI][azure-cli].</span></span>
2. <span data-ttu-id="59f81-593">Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-593">Sign in with your Azure account:</span></span>

  ```
  azure login
  ```

3. <span data-ttu-id="59f81-594">Azure Resource Manager 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-594">Switch to Azure Resource Manager mode:</span></span>

  ```
  azure config mode arm
  ```

4. <span data-ttu-id="59f81-595">Azure 고급 모니터링을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-595">Enable Azure Enhanced Monitoring:</span></span>

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. <span data-ttu-id="59f81-596">Azure 고급 모니터링 확장이 Azure Linux VM에서 활성 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-596">Verify that the Azure Enhanced Monitoring Extension is active on the Azure Linux VM.</span></span> <span data-ttu-id="59f81-597">\\var\\lib\\AzureEnhancedMonitor\\PerfCounters 파일이 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-597">Check whether the file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span></span> <span data-ttu-id="59f81-598">존재하면 명령 프롬프트에서 이 명령을 실행하여 Azure 고급 모니터가 수집한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-598">If it exists, at a command prompt, run this command to display information collected by the Azure Enhanced Monitor:</span></span>
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

<span data-ttu-id="59f81-599">출력은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-599">The output looks like this:</span></span>
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <span data-ttu-id="59f81-600"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>종단 간 모니터링 확인 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="59f81-600"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Checks and troubleshooting for end-to-end monitoring</span></span>
<span data-ttu-id="59f81-601">Azure VM을 배포하고 관련 Azure 모니터링 인프라를 설정한 후 Azure 고급 모니터링 확장의 모든 구성 요소가 예상한 대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-601">After you have deployed your Azure VM and set up the relevant Azure monitoring infrastructure, check whether all the components of the Azure Enhanced Monitoring Extension are working as expected.</span></span>

<span data-ttu-id="59f81-602">[SAP용 Azure 고급 모니터링 확장에 대한 준비 검사][deployment-guide-5.1]에 설명된 대로 SAP용 Azure 고급 모니터링 확장에 대한 준비 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-602">Run the readiness check for the Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for the Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="59f81-603">모든 준비 검사 결과가 긍정적이고 모든 관련 성능 카운터가 정상으로 나타나면 Azure 모니터링이 성공적으로 설정된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-603">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring successfully set up.</span></span> <span data-ttu-id="59f81-604">SAP Note [SAP 리소스][deployment-guide-2.2]에 설명된 SAP 호스트 에이전트 설치를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-604">You can proceed with the installation of SAP Host Agent described in the SAP Notes in [SAP resources][deployment-guide-2.2].</span></span> <span data-ttu-id="59f81-605">준비 검사에서 카운터가 누락된 것으로 나타나는 경우 [Azure 모니터링 인프라 구성에 대한 상태 검사][deployment-guide-5.2]에 설명된 대로 Azure 모니터링 인프라에 대한 상태 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-605">If the readiness check indicates that counters are missing, run the health check for the Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="59f81-606">자세한 문제 해결 옵션은 [SAP용 Azure 모니터링 문제 해결][deployment-guide-5.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-606">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="59f81-607"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>SAP용 Azure 고급 모니터링 확장에 대한 준비 검사</span><span class="sxs-lookup"><span data-stu-id="59f81-607"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Readiness check for the Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="59f81-608">이 검사에서는 SAP 응용 프로그램 내부에 나타나는 모든 성능 메트릭이 기반 Azure 모니터링 인프라에서 제공되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-608">This check makes sure that all performance metrics that appear inside your SAP application are provided by the underlying Azure monitoring infrastructure.</span></span>

#### <a name="run-the-readiness-check-on-a-windows-vm"></a><span data-ttu-id="59f81-609">Windows VM에서 준비 검사 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-609">Run the readiness check on a Windows VM</span></span>

1.  <span data-ttu-id="59f81-610">Azure Virtual Machine에 로그인합니다(관리자 계정 사용은 필요하지 않음).</span><span class="sxs-lookup"><span data-stu-id="59f81-610">Sign in to the Azure virtual machine (using an admin account is not necessary).</span></span>
2.  <span data-ttu-id="59f81-611">명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-611">Open a Command Prompt window.</span></span>
3.  <span data-ttu-id="59f81-612">명령 프롬프트에서 디렉터리를 SAP용 Azure 모니터링 확장의 설치 폴더: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-612">At the command prompt, change the directory to the installation folder of the Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span></span>

  <span data-ttu-id="59f81-613">모니터링 확장에 대한 경로의 *버전*이 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-613">The *version* in the path to the monitoring extension might vary.</span></span> <span data-ttu-id="59f81-614">설치 폴더에 여러 모니터링 확장 버전의 폴더가 표시되는 경우 AzureEnhancedMonitoring Windows 서비스의 구성을 확인한 다음 *실행 파일 경로*로 나타난 폴더로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-614">If you see folders for multiple versions of the monitoring extension in the installation folder, check the configuration of the AzureEnhancedMonitoring Windows service, and then switch to the folder indicated as *Path to executable*.</span></span>

  ![SAP용 Azure 고급 모니터링 확장을 실행하는 서비스 속성][deployment-guide-figure-1000]

4.  <span data-ttu-id="59f81-616">명령 프롬프트에서 매개 변수 없이 **azperflib.exe**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-616">At the command prompt, run **azperflib.exe** without any parameters.</span></span>

  > [!NOTE]
  > <span data-ttu-id="59f81-617">Azperflib.exe는 루프에서 실행되고 60초마다 수집한 카운터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-617">Azperflib.exe runs in a loop and updates the collected counters every 60 seconds.</span></span> <span data-ttu-id="59f81-618">루프를 종료하려면 명령 프롬프트 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-618">To end the loop, close the Command Prompt window.</span></span>
  >
  >

<span data-ttu-id="59f81-619">Azure 고급 모니터링 확장이 설치되어 있지 않거나 AzureEnhancedMonitoring 서비스가 실행되고 있지 않으면 확장이 올바르게 구성되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-619">If the Azure Enhanced Monitoring Extension is not installed, or the AzureEnhancedMonitoring service is not running, the extension has not been configured correctly.</span></span> <span data-ttu-id="59f81-620">확장을 배포하는 방법에 대한 자세한 내용은 [SAP용 Azure 모니터링 인프라 문제 해결][deployment-guide-5.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-620">For detailed information about how to deploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

##### <a name="check-the-output-of-azperflibexe"></a><span data-ttu-id="59f81-621">azperflib.exe의 출력 확인</span><span class="sxs-lookup"><span data-stu-id="59f81-621">Check the output of azperflib.exe</span></span>
<span data-ttu-id="59f81-622">Azperflib.exe 출력은 SAP용 Azure 성능 카운터가 모두 채워진 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-622">Azperflib.exe output shows all populated Azure performance counters for SAP.</span></span> <span data-ttu-id="59f81-623">수집된 카운터 목록의 맨 아래에 있는 요약 및 상태 표시기가 Azure 모니터링의 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-623">At the bottom of the list of collected counters, a summary and health indicator show the status of Azure monitoring.</span></span>

<span data-ttu-id="59f81-624">![문제가 없음을 나타내는 azperflib.exe를 실행하여 표시된 상태 검사 출력][deployment-guide-figure-1100]
<a name="figure-11"></a></span><span class="sxs-lookup"><span data-stu-id="59f81-624">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span></span>

<span data-ttu-id="59f81-625">빈 상태로 보고되는 **카운터 합계** 출력 및 이전 그림에 표시된 **상태 정보**에 대해 반환되는 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-625">Check the result returned for the **Counters total** output, which is reported as empty, and for **Health status**, shown in the preceding figure.</span></span>

<span data-ttu-id="59f81-626">결과 값을 다음과 같이 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-626">Interpret the resulting values as follows:</span></span>

| <span data-ttu-id="59f81-627">Azperflib.exe 결과 값</span><span class="sxs-lookup"><span data-stu-id="59f81-627">Azperflib.exe result values</span></span> | <span data-ttu-id="59f81-628">Azure 모니터링 상태 정보</span><span class="sxs-lookup"><span data-stu-id="59f81-628">Azure monitoring health status</span></span> |
| --- | --- |
| <span data-ttu-id="59f81-629">**API 호출 - 사용할 수 없음**</span><span class="sxs-lookup"><span data-stu-id="59f81-629">**API Calls - not available**</span></span> | <span data-ttu-id="59f81-630">사용할 수 없는 카운터는 가상 컴퓨터 구성에 적용할 수 없거나 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-630">Counters that are not available might be either not applicable to the virtual machine configuration, or are errors.</span></span> <span data-ttu-id="59f81-631">**상태 정보**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-631">See **Health status**.</span></span> |
| <span data-ttu-id="59f81-632">**카운터 합계 - 비어 있음**</span><span class="sxs-lookup"><span data-stu-id="59f81-632">**Counters total - empty**</span></span> |<span data-ttu-id="59f81-633">다음 두 Azure 저장소 카운터는 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-633">The following two Azure storage counters can be empty:</span></span> <ul><li><span data-ttu-id="59f81-634">저장소 읽기 작업 대기 시간 서버 밀리초</span><span class="sxs-lookup"><span data-stu-id="59f81-634">Storage Read Op Latency Server msec</span></span></li><li><span data-ttu-id="59f81-635">저장소 읽기 작업 대기 시간 E2E 밀리초</span><span class="sxs-lookup"><span data-stu-id="59f81-635">Storage Read Op Latency E2E msec</span></span></li></ul><span data-ttu-id="59f81-636">그 외의 카운터는 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-636">All other counters must have values.</span></span> |
| <span data-ttu-id="59f81-637">**상태 정보**</span><span class="sxs-lookup"><span data-stu-id="59f81-637">**Health status**</span></span> |<span data-ttu-id="59f81-638">반환 상태가 **OK**를 표시하는 경우에만 OK입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-638">Only OK if return status shows **OK**.</span></span> |
| <span data-ttu-id="59f81-639">**진단**</span><span class="sxs-lookup"><span data-stu-id="59f81-639">**Diagnostics**</span></span> |<span data-ttu-id="59f81-640">상태 정보에 대한 자세한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-640">Detailed information about health status.</span></span> |

<span data-ttu-id="59f81-641">**상태 정보** 값이 **OK**가 아닌 경우 [Azure 모니터링 인프라 상태 검사][deployment-guide-5.2]의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-641">If the **Health status** value is not **OK**, follow the instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span>

#### <a name="run-the-readiness-check-on-a-linux-vm"></a><span data-ttu-id="59f81-642">Linux VM에서 준비 검사 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-642">Run the readiness check on a Linux VM</span></span>

1.  <span data-ttu-id="59f81-643">SSH를 사용하여 Azure Virtual Machine에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-643">Connect to the Azure Virtual Machine by using SSH.</span></span>

2.  <span data-ttu-id="59f81-644">Azure 고급 모니터링 확장의 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-644">Check the output of the Azure Enhanced Monitoring Extension.</span></span>

  <span data-ttu-id="59f81-645">a.</span><span class="sxs-lookup"><span data-stu-id="59f81-645">a.</span></span>  <span data-ttu-id="59f81-646">`more /var/lib/AzureEnhancedMonitor/PerfCounters` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-646">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span></span>

   <span data-ttu-id="59f81-647">**예상 결과**: 성능 카운터 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-647">**Expected result**: Returns list of performance counters.</span></span> <span data-ttu-id="59f81-648">파일은 비어 있으면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-648">The file should not be empty.</span></span>

 <span data-ttu-id="59f81-649">b.</span><span class="sxs-lookup"><span data-stu-id="59f81-649">b.</span></span> <span data-ttu-id="59f81-650">`cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-650">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span></span>

   <span data-ttu-id="59f81-651">**예상 결과**: 오류가 **없는** 한 줄을 반환합니다. 예: **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span><span class="sxs-lookup"><span data-stu-id="59f81-651">**Expected result**: Returns one line where the error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span></span>

  <span data-ttu-id="59f81-652">c.</span><span class="sxs-lookup"><span data-stu-id="59f81-652">c.</span></span> <span data-ttu-id="59f81-653">`more /var/lib/AzureEnhancedMonitor/LatestErrorRecord` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-653">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span></span>

    <span data-ttu-id="59f81-654">**예상 결과**: 빈 상태로 반환하거나 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-654">**Expected result**: Returns as empty or does not exist.</span></span>

<span data-ttu-id="59f81-655">이전 검사가 성공하지 못한 경우 다음 추가 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-655">If the preceding check was not successful, run these additional checks:</span></span>

1.  <span data-ttu-id="59f81-656">waagent가 설치되고 사용하도록 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-656">Make sure that the waagent is installed and enabled.</span></span>

  <span data-ttu-id="59f81-657">a.</span><span class="sxs-lookup"><span data-stu-id="59f81-657">a.</span></span>  <span data-ttu-id="59f81-658">`sudo ls -al /var/lib/waagent/` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-658">Run `sudo ls -al /var/lib/waagent/`</span></span>

      <span data-ttu-id="59f81-659">**예상 결과**: waagent 디렉터리의 내용을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-659">**Expected result**: Lists the content of the waagent directory.</span></span>

  <span data-ttu-id="59f81-660">b.</span><span class="sxs-lookup"><span data-stu-id="59f81-660">b.</span></span>  <span data-ttu-id="59f81-661">`ps -ax | grep waagent` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-661">Run `ps -ax | grep waagent`</span></span>

   <span data-ttu-id="59f81-662">**예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /usr/sbin/waagent -daemon`</span><span class="sxs-lookup"><span data-stu-id="59f81-662">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span></span>

2. <span data-ttu-id="59f81-663">Linux 진단 확장이 설치되고 사용하도록 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-663">Make sure that the Linux Diagnostic Extension is installed and enabled.</span></span>

  <span data-ttu-id="59f81-664">a.</span><span class="sxs-lookup"><span data-stu-id="59f81-664">a.</span></span>  <span data-ttu-id="59f81-665">`sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-665">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`</span></span>

   <span data-ttu-id="59f81-666">**예상 결과**: Linux 진단 확장 디렉터리의 내용을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-666">**Expected result**: Lists the content of the Linux Diagnostic Extension directory.</span></span>

 <span data-ttu-id="59f81-667">b.</span><span class="sxs-lookup"><span data-stu-id="59f81-667">b.</span></span> <span data-ttu-id="59f81-668">`ps -ax | grep diagnostic` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-668">Run `ps -ax | grep diagnostic`</span></span>

   <span data-ttu-id="59f81-669">**예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span><span class="sxs-lookup"><span data-stu-id="59f81-669">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span></span>

3.   <span data-ttu-id="59f81-670">Azure 고급 모니터링 확장이 설치되고 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-670">Make sure that the Azure Enhanced Monitoring Extension is installed and running.</span></span>

  <span data-ttu-id="59f81-671">a.</span><span class="sxs-lookup"><span data-stu-id="59f81-671">a.</span></span>  <span data-ttu-id="59f81-672">`sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-672">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`</span></span>

    <span data-ttu-id="59f81-673">**예상 결과**: Azure 고급 모니터링 확장 디렉터리의 내용을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-673">**Expected result**: Lists the content of the Azure Enhanced Monitoring Extension directory.</span></span>

  <span data-ttu-id="59f81-674">b.</span><span class="sxs-lookup"><span data-stu-id="59f81-674">b.</span></span> <span data-ttu-id="59f81-675">`ps -ax | grep AzureEnhanced` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-675">Run `ps -ax | grep AzureEnhanced`</span></span>

     <span data-ttu-id="59f81-676">**예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span><span class="sxs-lookup"><span data-stu-id="59f81-676">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span></span>

3. <span data-ttu-id="59f81-677">SAP Note [1031096] 에 설명된 대로 SAP 호스트 에이전트를 설치하고 `saposcol`의 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-677">Install SAP Host Agent as described in SAP Note [1031096], and check the output of `saposcol`.</span></span>

  <span data-ttu-id="59f81-678">a.</span><span class="sxs-lookup"><span data-stu-id="59f81-678">a.</span></span>  <span data-ttu-id="59f81-679">`/usr/sap/hostctrl/exe/saposcol -d` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-679">Run `/usr/sap/hostctrl/exe/saposcol -d`</span></span>

  <span data-ttu-id="59f81-680">b.</span><span class="sxs-lookup"><span data-stu-id="59f81-680">b.</span></span>  <span data-ttu-id="59f81-681">`dump ccm` 실행</span><span class="sxs-lookup"><span data-stu-id="59f81-681">Run `dump ccm`</span></span>

  <span data-ttu-id="59f81-682">c.</span><span class="sxs-lookup"><span data-stu-id="59f81-682">c.</span></span>  <span data-ttu-id="59f81-683">**Virtualization_Configuration\Enhanced Monitoring Access** 메트릭이 **true**인지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-683">Check whether the **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span></span>

<span data-ttu-id="59f81-684">SAP NetWeaver ABAP 응용 프로그램 서버가 이미 설치된 경우 트랜잭션 ST06을 열고 고급 모니터링이 사용하도록 설정되어 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-684">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span></span>

<span data-ttu-id="59f81-685">이 검사 중 하나 이상에 실패한 경우 확장을 배포하는 방법에 대한 자세한 내용은 [SAP용 Azure 모니터링 인프라 문제 해결][deployment-guide-5.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-685">If any of these checks fail, and for detailed information about how to redeploy the extension, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="59f81-686"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Azure 모니터링 인프라 구성에 대한 상태 검사</span><span class="sxs-lookup"><span data-stu-id="59f81-686"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Health check for the Azure monitoring infrastructure configuration</span></span>
<span data-ttu-id="59f81-687">모니터링 데이터의 일부가 [SAP용 Azure 고급 모니터링에 대한 준비 검사][deployment-guide-5.1]에서 설명한 테스트에 표시된 대로 올바르게 전달되지 않는 경우 `Test-AzureRmVMAEMExtension` cmdlet을 실행하여 Azure 모니터링 인프라 및 SAP용 모니터링 확장이 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-687">If some of the monitoring data is not delivered correctly as indicated by the test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run the `Test-AzureRmVMAEMExtension` cmdlet to check whether the Azure monitoring infrastructure and the monitoring extension for SAP are configured correctly.</span></span>

1.  <span data-ttu-id="59f81-688">[Azure PowerShell cmdlet 배포][deployment-guide-4.1]에 설명된 대로 최신 버전의 Azure PowerShell cmdlet을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-688">Make sure that you have installed the latest version of the Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>
2.  <span data-ttu-id="59f81-689">다음 PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-689">Run the following PowerShell cmdlet.</span></span> <span data-ttu-id="59f81-690">사용 가능한 환경 목록을 보려면 `Get-AzureRmEnvironment` cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-690">For a list of available environments, run the cmdlet `Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="59f81-691">공용 Azure를 사용하려면**AzureCloud** 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-691">To use public Azure, select the **AzureCloud** environment.</span></span> <span data-ttu-id="59f81-692">중국의 Azure인 경우 **AzureChinaCloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-692">For Azure in China, select **AzureChinaCloud**.</span></span>
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of the environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  <span data-ttu-id="59f81-693">계정 데이터를 입력하고 Azure Virtual Machine을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-693">Enter your account data and identify the Azure virtual machine.</span></span>

  ![SAP 관련 Azure cmdlet Test-VMConfigForSAP_GUI의 입력 페이지][deployment-guide-figure-1200]

4. <span data-ttu-id="59f81-695">선택한 가상 컴퓨터의 구성을 테스트하는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-695">The script tests the configuration of the virtual machine you select.</span></span>

  ![SAP용 Azure 모니터링 인프라의 성공적인 테스트 출력][deployment-guide-figure-1300]

<span data-ttu-id="59f81-697">모든 상태 검사 결과가 **OK**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-697">Make sure that every health check result is **OK**.</span></span> <span data-ttu-id="59f81-698">일부 검사가 **OK**를 표시하지 않는 경우 [SAP용 Azure 고급 모니터링 확장 구성][deployment-guide-4.5]에서 설명한 대로 업데이트 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-698">If some checks do not display **OK**, run the update cmdlet as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="59f81-699">15분 기다린 다음 [SAP용 Azure 고급 모니터링에 대한 준비 검사][deployment-guide-5.1] 및 [Azure 모니터링 인프라 구성에 대한 상태 검사][deployment-guide-5.2]에 설명된 검사를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-699">Wait 15 minutes, and repeat the checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="59f81-700">검사에서 여전히 일부 또는 모든 카운터에 문제가 있다고 표시하는 경우 [SAP용 Azure 모니터링 인프라 문제 해결][deployment-guide-5.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-700">If the checks still indicate a problem with some or all counters, see [Troubleshooting the Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="59f81-701"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>SAP용 Azure 모니터링 인프라 문제 해결</span><span class="sxs-lookup"><span data-stu-id="59f81-701"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Troubleshooting the Azure monitoring infrastructure for SAP</span></span>

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] <span data-ttu-id="59f81-703">Azure 성능 카운터가 전혀 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-703">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="59f81-704">AzureEnhancedMonitoring Windows 서비스에서 Azure의 성능 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-704">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="59f81-705">서비스가 올바르게 설치되지 않은 경우 또는 VM에서 실행되지 않는 경우 성능 메트릭을 수집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-705">If the service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="59f81-706">Azure 고급 모니터링 확장의 설치 디렉터리가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-706">The installation directory of the Azure Enhanced Monitoring Extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="59f81-707">문제</span><span class="sxs-lookup"><span data-stu-id="59f81-707">Issue</span></span>
<span data-ttu-id="59f81-708">설치 디렉터리 C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-708">The installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span></span>

###### <a name="solution"></a><span data-ttu-id="59f81-709">해결 방법</span><span class="sxs-lookup"><span data-stu-id="59f81-709">Solution</span></span>
<span data-ttu-id="59f81-710">확장이 설치되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-710">The extension is not installed.</span></span> <span data-ttu-id="59f81-711">(앞에서 설명한) 프록시 문제인지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-711">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="59f81-712">컴퓨터를 다시 시작하거나 `Set-AzureRmVMAEMExtension` 구성 스크립트를 다시 실행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-712">You might need to restart the machine or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a><span data-ttu-id="59f81-713">Azure 고급 모니터링 서비스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-713">Service for Azure Enhanced Monitoring does not exist</span></span>

###### <a name="issue"></a><span data-ttu-id="59f81-714">문제</span><span class="sxs-lookup"><span data-stu-id="59f81-714">Issue</span></span>
<span data-ttu-id="59f81-715">AzureEnhancedMonitoring Windows 서비스가 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-715">The AzureEnhancedMonitoring Windows service does not exist.</span></span>

<span data-ttu-id="59f81-716">Azperflib.exe 출력에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-716">Azperflib.exe output throws an error:</span></span>

<span data-ttu-id="59f81-717">![SAP용 Azure 고급 모니터링 확장의 서비스가 실행되고 있지 않음을 나타내는 Azperflib.exe의 실행][deployment-guide-figure-1400]
<a name="figure-14"></a></span><span class="sxs-lookup"><span data-stu-id="59f81-717">![Execution of azperflib.exe indicates that the service of the Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span></span>

###### <a name="solution"></a><span data-ttu-id="59f81-718">해결 방법</span><span class="sxs-lookup"><span data-stu-id="59f81-718">Solution</span></span>
<span data-ttu-id="59f81-719">서비스가 없으면 SAP용 Azure 고급 모니터링 확장이 제대로 설치되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-719">If the service does not exist, the Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span></span> <span data-ttu-id="59f81-720">[Azure에서 SAP용 VM 배포 시나리오][deployment-guide-3]에서 배포 시나리오에 대해 설명된 단계에 따라 확장을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-720">Redeploy the extension by using the steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span></span>

<span data-ttu-id="59f81-721">확장을 배포하고 1시간 후 Azure VM 내에서 Azure 성능 카운터가 제공되는지 여부를 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-721">After you deploy the extension, after one hour, check again whether the Azure performance counters are provided in the Azure VM.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-to-start"></a><span data-ttu-id="59f81-722">Azure 고급 모니터링에 대한 서비스가 있지만 시작하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-722">Service for Azure Enhanced Monitoring exists, but fails to start</span></span>

###### <a name="issue"></a><span data-ttu-id="59f81-723">문제</span><span class="sxs-lookup"><span data-stu-id="59f81-723">Issue</span></span>
<span data-ttu-id="59f81-724">AzureEnhancedMonitoring Windows 서비스가 존재하고 사용하도록 설정되었지만 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-724">The AzureEnhancedMonitoring Windows service exists and is enabled, but fails to start.</span></span> <span data-ttu-id="59f81-725">자세한 내용은 응용 프로그램 이벤트 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-725">For more information, check the application event log.</span></span>

###### <a name="solution"></a><span data-ttu-id="59f81-726">해결 방법</span><span class="sxs-lookup"><span data-stu-id="59f81-726">Solution</span></span>
<span data-ttu-id="59f81-727">구성이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-727">The configuration is incorrect.</span></span> <span data-ttu-id="59f81-728">[SAP용 Azure 고급 모니터링 확장 구성][deployment-guide-4.5]에 설명된 대로 VM에 대한 모니터링 확장을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-728">Restart the monitoring extension for the VM, as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] <span data-ttu-id="59f81-730">일부 Azure 성능 카운터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-730">Some Azure performance counters are missing</span></span>
<span data-ttu-id="59f81-731">AzureEnhancedMonitoring Windows 서비스에서 Azure의 성능 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-731">The AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="59f81-732">이 서비스는 여러 원본에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-732">The service gets data from several sources.</span></span> <span data-ttu-id="59f81-733">일부 구성 데이터는 로컬로 수집되고 일부 성능 메트릭은 Azure 진단에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-733">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="59f81-734">저장소 카운터는 저장소 구독 수준에 대한 로깅에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-734">Storage counters are used from your logging on the storage subscription level.</span></span>

<span data-ttu-id="59f81-735">SAP Note [1999351]을 사용한 문제 해결로 문제가 해결되지 않으면 `Set-AzureRmVMAEMExtension` 구성 스크립트를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-735">If troubleshooting by using SAP Note [1999351] doesn't resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span> <span data-ttu-id="59f81-736">사용하도록 설정한 후 바로 저장소 분석 또는 진단 카운터가 생성되지 않을 수 있으므로 1시간 동안 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-736">You might have to wait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="59f81-737">문제가 지속되면 Windows용 BC-OP-NT-AZR 또는 Linux 가상 컴퓨터용 BC-OP-LNX-AZR 구성 요소에 대한 SAP 고객 지원 메시지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-737">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] <span data-ttu-id="59f81-739">Azure 성능 카운터가 전혀 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-739">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="59f81-740">Azure의 성능 메트릭은 데몬에 의해 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-740">Performance metrics in Azure are collected by a daemon.</span></span> <span data-ttu-id="59f81-741">데몬이 실행되지 않는 경우 성능 메트릭은 전혀 수집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-741">If the daemon is not running, no performance metrics can be collected.</span></span>

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="59f81-742">Azure 고급 모니터링 확장의 설치 디렉터리가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-742">The installation directory of the Azure Enhanced Monitoring extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="59f81-743">문제</span><span class="sxs-lookup"><span data-stu-id="59f81-743">Issue</span></span>
<span data-ttu-id="59f81-744">디렉터리 \\var\\lib\\waagent\\에 Azure 고급 모니터링 확장에 대한 하위 디렉터리가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-744">The directory \\var\\lib\\waagent\\ does not have a subdirectory for the Azure Enhanced Monitoring extension.</span></span>

###### <a name="solution"></a><span data-ttu-id="59f81-745">해결 방법</span><span class="sxs-lookup"><span data-stu-id="59f81-745">Solution</span></span>
<span data-ttu-id="59f81-746">확장이 설치되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-746">The extension is not installed.</span></span> <span data-ttu-id="59f81-747">(앞에서 설명한) 프록시 문제인지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-747">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="59f81-748">컴퓨터를 다시 시작하거나 `Set-AzureRmVMAEMExtension` 구성 스크립트를 다시 실행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-748">You might need to restart the machine and/or rerun the `Set-AzureRmVMAEMExtension` configuration script.</span></span>

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] <span data-ttu-id="59f81-750">일부 Azure 성능 카운터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-750">Some Azure performance counters are missing</span></span>
<span data-ttu-id="59f81-751">Azure에서 성능 메트릭은 여러 원본에서 데이터를 가져오는 데몬에 의해 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-751">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span></span> <span data-ttu-id="59f81-752">일부 구성 데이터는 로컬로 수집되고 일부 성능 메트릭은 Azure 진단에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-752">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="59f81-753">저장소 카운터는 저장소 구독의 로그에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-753">Storage counters come from the logs in your storage subscription.</span></span>

<span data-ttu-id="59f81-754">알려진 문제의 전체 최신 목록은 SAP용 고급 Azure 모니터링에 대한 추가 문제 해결 정보를 포함하고 있는 SAP Note [1999351]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59f81-754">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span></span>

<span data-ttu-id="59f81-755">SAP Note [1999351]을 사용한 문제 해결로 문제가 해결되지 않는 경우 [SAP용 Azure 고급 모니터링 확장 구성][deployment-guide-4.5]에 설명된 대로 `Set-AzureRmVMAEMExtension` 구성 스크립트를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-755">If troubleshooting by using SAP Note [1999351] does not resolve the issue, rerun the `Set-AzureRmVMAEMExtension` configuration script as described in [Configure the Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="59f81-756">사용하도록 설정한 후 바로 저장소 분석 또는 진단 카운터가 생성되지 않을 수 있으므로 1시간 동안 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-756">You might have to wait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="59f81-757">문제가 지속되면 Windows용 BC-OP-NT-AZR 또는 Linux 가상 컴퓨터용 BC-OP-LNX-AZR 구성 요소에 대한 SAP 고객 지원 메시지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59f81-757">If the problem persists, open an SAP customer support message on the component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>
