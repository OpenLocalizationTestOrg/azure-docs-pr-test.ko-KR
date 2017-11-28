---
title: "Windows에서의 SAP 용 가상 컴퓨터 배포 aaaAzure | Microsoft Docs"
description: "Toodeploy SAP 하는 방법을 알아보려면 Azure에서 Windows 가상 컴퓨터에는 소프트웨어입니다."
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
ms.openlocfilehash: 121e317afc6498a896959e58ebfbdcbef9432ef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-on-windows-vms-in-azure"></a><span data-ttu-id="68a34-103">Azure의 Windows VM에서 SAP 배포</span><span class="sxs-lookup"><span data-stu-id="68a34-103">Deploy SAP on Windows VMs in Azure</span></span>
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
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
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
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
[dbms-guide-5.6]:sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
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
[deployment-guide-3.2]:#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
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
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
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
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
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

<span data-ttu-id="68a34-115">Azure 가상 컴퓨터에는 최소한의 시간 및 긴 조달 주기 하지 않고 계산 및 저장소 리소스를 필요로 하는 조직 위한 hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-115">Azure Virtual Machines is hello solution for organizations that need compute and storage resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="68a34-116">Azure에서 Azure 가상 컴퓨터 toodeploy 고전 같은 응용 프로그램, SAP NetWeaver 기반 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-116">You can use Azure Virtual Machines toodeploy classical applications, like SAP NetWeaver-based applications, in Azure.</span></span> <span data-ttu-id="68a34-117">추가 온-프레미스 리소스 없이도 응용 프로그램의 안정성과 가용성을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-117">Extend an application's reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="68a34-118">Azure Virtual Machines는 크로스-프레미스 연결을 지원하므로 Azure Virtual Machines를 조직의 온-프레미스 도메인, 사설 클라우드 및 SAP 시스템 지형에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-118">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="68a34-119">이 문서에서는 hello 단계 toodeploy SAP 응용 프로그램 Windows Azure의 가상 컴퓨터 (Vm)에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-119">In this article, we cover hello steps toodeploy SAP applications on Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="68a34-120">이 문서에 hello 정보에 빌드 [Azure 가상 컴퓨터 계획 및 구현 Windows에서의 SAP 용][planning-guide]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-120">This article builds on hello information in [Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide].</span></span> <span data-ttu-id="68a34-121">또한 SAP 설치 설명서 및 설치 하 고 SAP 소프트웨어 배포에 대 한 기본 리소스 hello SAP Note를 보완 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-121">It also complements SAP installation documentation and SAP Notes, which are hello primary resources for installing and deploying SAP software.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68a34-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="68a34-122">Prerequisites</span></span>
<span data-ttu-id="68a34-123">SAP 소프트웨어 배포를 위해 Azure 가상 컴퓨터를 설정하려면 여러 단계와 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-123">Setting up an Azure virtual machine for SAP software deployment involves multiple steps and resources.</span></span> <span data-ttu-id="68a34-124">시작 하기 전에 Azure에서 Windows 가상 컴퓨터에 SAP 소프트웨어를 설치 하기 위한 hello 필수 구성 요소를 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-124">Before you start, make sure that you meet hello prerequisites for installing SAP software on Windows virtual machines in Azure.</span></span>

### <a name="local-computer"></a><span data-ttu-id="68a34-125">수집</span><span class="sxs-lookup"><span data-stu-id="68a34-125">Local computer</span></span>
<span data-ttu-id="68a34-126">Windows 또는 Linux Vm toomanage, PowerShell 스크립트를 hello Azure 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-126">toomanage Windows or Linux VMs, you can use a PowerShell script and hello Azure portal.</span></span> <span data-ttu-id="68a34-127">두 가지 도구 모두 Windows 7 또는 이후 버전의 Windows 실행하는 로컬 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-127">For both tools, you need a local computer running Windows 7 or a later version of Windows.</span></span> <span data-ttu-id="68a34-128">Linux Vm을 toouse Linux 컴퓨터에이 작업을 하려면만 toomanage 하려는 경우 Azure CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-128">If you want toomanage only Linux VMs and you want toouse a Linux computer for this task, you can use Azure CLI.</span></span>

### <a name="internet-connection"></a><span data-ttu-id="68a34-129">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="68a34-129">Internet connection</span></span>
<span data-ttu-id="68a34-130">여야 toodownload 및 실행된 hello 도구 및 SAP 소프트웨어 배포에 필요한 스크립트를 toohello 인터넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-130">toodownload and run hello tools and scripts that are required for SAP software deployment, you must be connected toohello Internet.</span></span> <span data-ttu-id="68a34-131">hello Azure 고급 모니터링 확장의 SAP 용 hello를 실행 하는 Azure VM 인터넷 액세스 toohello를도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-131">hello Azure VM that is running hello Azure Enhanced Monitoring Extension for SAP also needs access toohello Internet.</span></span> <span data-ttu-id="68a34-132">Hello Azure VM에 Azure 가상 네트워크 또는 온-프레미스 도메인의 일부 이면 확인 hello 관련 프록시 설정을 설정 되어 있는지에 설명 된 대로 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-132">If hello Azure VM is part of an Azure virtual network or on-premises domain, make sure that hello relevant proxy settings are set, as described in [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

### <a name="microsoft-azure-subscription"></a><span data-ttu-id="68a34-133">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="68a34-133">Microsoft Azure subscription</span></span>
<span data-ttu-id="68a34-134">활성 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-134">You need an active Azure account.</span></span>

### <a name="topology-and-networking"></a><span data-ttu-id="68a34-135">토폴로지 및 네트워킹</span><span class="sxs-lookup"><span data-stu-id="68a34-135">Topology and networking</span></span>
<span data-ttu-id="68a34-136">Hello Azure에서 SAP 배포의 toodefine hello 토폴로지 및 아키텍처가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-136">You need toodefine hello topology and architecture of hello SAP deployment in Azure:</span></span>

* <span data-ttu-id="68a34-137">Azure 저장소 계정 toobe 사용</span><span class="sxs-lookup"><span data-stu-id="68a34-137">Azure storage accounts toobe used</span></span>
* <span data-ttu-id="68a34-138">가상 네트워크를 toodeploy hello SAP 시스템</span><span class="sxs-lookup"><span data-stu-id="68a34-138">Virtual network where you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="68a34-139">리소스 그룹 toowhich toodeploy hello SAP 시스템</span><span class="sxs-lookup"><span data-stu-id="68a34-139">Resource group toowhich you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="68a34-140">Toodeploy hello SAP 시스템을 원하는 azure 지역</span><span class="sxs-lookup"><span data-stu-id="68a34-140">Azure region where you want toodeploy hello SAP system</span></span>
* <span data-ttu-id="68a34-141">SAP 구성(2계층 또는 3계층)</span><span class="sxs-lookup"><span data-stu-id="68a34-141">SAP configuration (two-tier or three-tier)</span></span>
* <span data-ttu-id="68a34-142">VM 크기 및 추가 가상 하드 디스크 (Vhd) toobe hello 개수의 toohello Vm 탑재</span><span class="sxs-lookup"><span data-stu-id="68a34-142">VM sizes and hello number of additional virtual hard disks (VHDs) toobe mounted toohello VMs</span></span>
* <span data-ttu-id="68a34-143">SAP 수정과 전송 시스템(CTS) 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-143">SAP Correction and Transport System (CTS) configuration</span></span>

<span data-ttu-id="68a34-144">만들고 hello SAP 소프트웨어 배포 프로세스를 시작 하기 전에 Azure 저장소 계정 또는 Azure 가상 네트워크를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-144">Create and configure Azure storage accounts or Azure virtual networks before you begin hello SAP software deployment process.</span></span> <span data-ttu-id="68a34-145">방법에 대 한 내용은 toocreate 이러한 리소스를 구성 하 고, 참조 [Azure 가상 컴퓨터 계획 및 구현 Windows에서의 SAP 용][planning-guide]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-145">For information about how toocreate and configure these resources, see [Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide].</span></span>

### <a name="sap-sizing"></a><span data-ttu-id="68a34-146">SAP 크기 조정</span><span class="sxs-lookup"><span data-stu-id="68a34-146">SAP sizing</span></span>
<span data-ttu-id="68a34-147">Hello 다음 SAP 크기 조정에 대 한 정보를 알고:</span><span class="sxs-lookup"><span data-stu-id="68a34-147">Know hello following information, for SAP sizing:</span></span>

* <span data-ttu-id="68a34-148">예를 들어 hello SAP 빠른 조절기 도구 및 hello SAP 응용 프로그램 성능 표준 (SAPS) 번호를 사용 하 여 SAP 작업 부하를 프로젝션</span><span class="sxs-lookup"><span data-stu-id="68a34-148">Projected SAP workload, for example, by using hello SAP Quick Sizer tool, and hello SAP Application Performance Standard (SAPS) number</span></span>
* <span data-ttu-id="68a34-149">Hello SAP 시스템의 필요한 CPU 리소스 및 메모리 사용</span><span class="sxs-lookup"><span data-stu-id="68a34-149">Required CPU resource and memory consumption of hello SAP system</span></span>
* <span data-ttu-id="68a34-150">필요한 초당 입력/출력(I/O) 작업 수</span><span class="sxs-lookup"><span data-stu-id="68a34-150">Required input/output (I/O) operations per second</span></span>
* <span data-ttu-id="68a34-151">Azure에서 서로 다른 VM 간의 결과적 통신에 필요한 네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="68a34-151">Required network bandwidth of eventual communication between VMs in Azure</span></span>
* <span data-ttu-id="68a34-152">온-프레미스 자산과 Azure 배포 SAP 시스템 hello 간에 필요한 네트워크 대역폭</span><span class="sxs-lookup"><span data-stu-id="68a34-152">Required network bandwidth between on-premises assets and hello Azure-deployed SAP system</span></span>

### <a name="resource-groups"></a><span data-ttu-id="68a34-153">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="68a34-153">Resource groups</span></span>
<span data-ttu-id="68a34-154">Azure 리소스 관리자를 사용할 수 있습니다 리소스 그룹 toomanage hello 응용 프로그램 리소스를 모두 Azure 구독에서.</span><span class="sxs-lookup"><span data-stu-id="68a34-154">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="68a34-155">자세한 내용은 [Azure Resource Manager 개요][resource-group-overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-155">For more information, see [Azure Resource Manager overview][resource-group-overview].</span></span>

## <a name="resources"></a><span data-ttu-id="68a34-156">리소스</span><span class="sxs-lookup"><span data-stu-id="68a34-156">Resources</span></span>

### <span data-ttu-id="68a34-157"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP 리소스</span><span class="sxs-lookup"><span data-stu-id="68a34-157"><a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP resources</span></span>
<span data-ttu-id="68a34-158">SAP 소프트웨어 배포를 설정 하는 경우 다음 SAP 리소스 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-158">When you are setting up your SAP software deployment, you need hello following SAP resources:</span></span>

* <span data-ttu-id="68a34-159">SAP Note [1928533], 다음 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-159">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="68a34-160">Hello SAP 소프트웨어 배포에 지원 되는 Azure VM 크기의 목록</span><span class="sxs-lookup"><span data-stu-id="68a34-160">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="68a34-161">Azure VM 크기에 대한 중요한 용량 정보</span><span class="sxs-lookup"><span data-stu-id="68a34-161">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="68a34-162">지원되는 SAP 소프트웨어 및 운영 체제(OS)와 데이터베이스 조합</span><span class="sxs-lookup"><span data-stu-id="68a34-162">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="68a34-163">Microsoft Azure에서 Windows 및 Linux에 필요한 SAP 커널 버전</span><span class="sxs-lookup"><span data-stu-id="68a34-163">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="68a34-164">SAP Note [2015553]는 Azure에서 SAP을 지원하는 SAP 소프트웨어 배포에 대한 필수 구성 요소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-164">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="68a34-165">SAP Note [2178632]는 Azure에서 SAP에 대해 보고된 모든 모니터링 메트릭에 대한 자세한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-165">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="68a34-166">SAP Note [1409604] hello 필요한 SAP 호스트 에이전트 버전 Azure에서 Windows에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-166">SAP Note [1409604] has hello required SAP Host Agent version for Windows in Azure.</span></span>
* <span data-ttu-id="68a34-167">SAP Note [2191498] hello 필요한 SAP 호스트 에이전트 버전 Azure에서 Linux에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-167">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="68a34-168">SAP Note [2243692]는 Azure에서 Linux의 SAP 라이선스에 대한 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-168">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="68a34-169">SAP Note [1984787]은 SUSE LINUX Enterprise Server 12에 대한 일반 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-169">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="68a34-170">SAP Note [2002167]는 Red Hat Enterprise Linux 7.x에 대한 일반 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-170">SAP Note [2002167] has general information about Red Hat Enterprise Linux 7.x.</span></span>
* <span data-ttu-id="68a34-171">SAP Note [1999351] Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 추가 문제 해결 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-171">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="68a34-172">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes)는 Linux에 필요한 모든 SAP Note를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-172">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="68a34-173">[Azure PowerShell][azure-ps]에 포함된 SAP 관련 PowerShell cmdlet입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-173">SAP-specific PowerShell cmdlets that are part of [Azure PowerShell][azure-ps].</span></span>
* <span data-ttu-id="68a34-174">[Azure CLI][azure-cli]에 포함된 SAP 관련 Azure CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-174">SAP-specific Azure CLI commands that are part of [Azure CLI][azure-cli].</span></span>

[comment]: <> (MSSedusch TODO - SAP Note 1409604에 SAP 호스트 에이전트용 ARM 패치 수준 추가)

### <a name="microsoft-resources"></a><span data-ttu-id="68a34-176">Microsoft 리소스</span><span class="sxs-lookup"><span data-stu-id="68a34-176">Microsoft resources</span></span>
<span data-ttu-id="68a34-177">다음 Microsoft 문서에서는 Azure에서 SAP 배포에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-177">These Microsoft articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="68a34-178">[Windows에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="68a34-178">[Azure Virtual Machines planning and implementation for SAP on Windows][planning-guide]</span></span>
* <span data-ttu-id="68a34-179">[Windows에서 SAP용 Azure Virtual Machines 배포(이 문서)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="68a34-179">[Azure Virtual Machines deployment for SAP on Windows (this article)][deployment-guide]</span></span>
* <span data-ttu-id="68a34-180">[Windows에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="68a34-180">[Azure Virtual Machines DBMS deployment for SAP on Windows][dbms-guide]</span></span>
* <span data-ttu-id="68a34-181">[Azure Portal][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="68a34-181">[Azure portal][azure-portal]</span></span>

## <span data-ttu-id="68a34-182"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure VM에서 SAP 소프트웨어에 대한 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="68a34-182"><a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Deployment scenarios for SAP software on Azure VMs</span></span>
<span data-ttu-id="68a34-183">Azure에서 VM 및 연결된 디스크를 배포하기 위한 여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-183">You have multiple options for deploying VMs and associated disks in Azure.</span></span> <span data-ttu-id="68a34-184">되므로 중요 toounderstand hello 차이점 배포 옵션 다른 단계가 tooprepare hello 배포 유형을 선택 하면에 따른 배포에 대 한 Vm을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-184">It's important toounderstand hello differences between deployment options, because you might take different steps tooprepare your VMs for deployment based on hello deployment type you choose.</span></span>

### <span data-ttu-id="68a34-185"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>시나리오 1: hello SAP 용 Azure Marketplace에서에서 VM 배포</span><span class="sxs-lookup"><span data-stu-id="68a34-185"><a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Scenario 1: Deploying a VM from hello Azure Marketplace for SAP</span></span>
<span data-ttu-id="68a34-186">Microsoft에서 제공 하는 이미지를 사용 하거나으로 제 3 자 hello Azure 마켓플레이스 toodeploy에서 VM 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-186">You can use an image provided by Microsoft or by a third party in hello Azure Marketplace toodeploy your VM.</span></span> <span data-ttu-id="68a34-187">hello 마켓플레이스는 Windows Server와 다른 Linux 배포판의 표준 OS 이미지 일부를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-187">hello Marketplace offers some standard OS images of Windows Server and different Linux distributions.</span></span> <span data-ttu-id="68a34-188">또한 데이터베이스 관리 시스템(DMBS) SKU, 예를 들어 Microsoft SQL Server를 포함하고 있는 이미지를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-188">You also can deploy an image that includes database management system (DBMS) SKUs, for example, Microsoft SQL Server.</span></span> <span data-ttu-id="68a34-189">DBMS SKU가 포함된 이미지 사용에 관한 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-189">For more information about using images with DBMS SKUs, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>

<span data-ttu-id="68a34-190">hello 다음 순서도 hello SAP 관련 Azure 마켓플레이스 hello에서 VM을 배포 하기 위한 단계를 순서 대로</span><span class="sxs-lookup"><span data-stu-id="68a34-190">hello following flowchart shows hello SAP-specific sequence of steps for deploying a VM from hello Azure Marketplace:</span></span>

![hello Azure Marketplace에서에서 VM 이미지를 사용 하 여 SAP 시스템에 대 한 VM 배포 순서도][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a><span data-ttu-id="68a34-192">Hello Azure 포털을 사용 하 여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="68a34-192">Create a virtual machine by using hello Azure portal</span></span>
<span data-ttu-id="68a34-193">hello 가장 쉬운 방법은 toocreate hello Azure Marketplace에서에서 이미지가 있는 새 가상 컴퓨터를 hello Azure 포털을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-193">hello easiest way toocreate a new virtual machine with an image from hello Azure Marketplace is by using hello Azure portal.</span></span>

1.  <span data-ttu-id="68a34-194">너무 이동<https://portal.azure.com/#create>합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-194">Go too<https://portal.azure.com/#create>.</span></span>  <span data-ttu-id="68a34-195">Hello Azure 포털 메뉴에서에서 선택 하거나 **+ 새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-195">Or, in hello Azure portal menu, select **+ New**.</span></span>
2.  <span data-ttu-id="68a34-196">선택 **계산**, 한 다음 운영 체제 toodeploy 원하는의 hello 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-196">Select **Compute**, and then select hello type of operating system you want toodeploy.</span></span> <span data-ttu-id="68a34-197">예를 들어, Windows Server 2012 R2, SUSE Linux Enterprise Server 12(SLES 12) 또는 Red Hat Enterprise Linux 7.2(RHEL 7.2)입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-197">For example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span> <span data-ttu-id="68a34-198">hello 기본 목록 보기는 지원 되는 모든 운영 체제를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-198">hello default list view does not show all supported operating systems.</span></span> <span data-ttu-id="68a34-199">전체 목록을 보려면 **모두 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-199">Select **see all** for a full list.</span></span> <span data-ttu-id="68a34-200">SAP 소프트웨어 배포를 위한 지원되는 운영 체제에 대한 자세한 내용은 SAP Note [1928533]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-200">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
3.  <span data-ttu-id="68a34-201">Hello 다음 페이지에서 약관을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-201">On hello next page, review terms and conditions.</span></span>
4.  <span data-ttu-id="68a34-202">Hello에 **배포 모델 선택** 상자 **리소스 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-202">In hello **Select a deployment model** box, select **Resource Manager**.</span></span>
5.  <span data-ttu-id="68a34-203">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-203">Select **Create**.</span></span>

<span data-ttu-id="68a34-204">tooall에서 네트워크 인터페이스 및 저장소 계정과 같은 리소스를 필요로 하는 또한을 hello 마법사를 통해 필요한 hello 매개 변수 toocreate hello 가상 컴퓨터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-204">hello wizard guides you through setting hello required parameters toocreate hello virtual machine, in addition tooall required resources, like network interfaces and storage accounts.</span></span> <span data-ttu-id="68a34-205">다음은 일부 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-205">Some of these parameters are:</span></span>

1. <span data-ttu-id="68a34-206">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="68a34-206">**Basics**:</span></span>
  * <span data-ttu-id="68a34-207">**이름**: hello 리소스 (hello 가상 컴퓨터 이름)의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-207">**Name**: hello name of hello resource (hello virtual machine name).</span></span>
 * <span data-ttu-id="68a34-208">**사용자 이름 및 암호** 또는 **SSH 공개 키**: hello 이름과 hello를 프로 비전 하는 동안 만들어진 hello 사용자의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-208">**Username and password** or **SSH public key**: Enter hello username and password of hello user that is created during hello provisioning.</span></span> <span data-ttu-id="68a34-209">Linux 가상 컴퓨터에 대 한 toosign toohello 컴퓨터에서 사용 하는 hello 공용 SSH (보안 셸) 키를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-209">For a Linux virtual machine, you can enter hello public Secure Shell (SSH) key that you use toosign in toohello machine.</span></span>
 * <span data-ttu-id="68a34-210">**구독**: toouse tooprovision hello 새 가상 컴퓨터를 원하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-210">**Subscription**: Select hello subscription that you want toouse tooprovision hello new virtual machine.</span></span>
 * <span data-ttu-id="68a34-211">**리소스 그룹**: hello VM에 대 한 hello 리소스 그룹의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-211">**Resource group**: hello name of hello resource group for hello VM.</span></span> <span data-ttu-id="68a34-212">새 리소스 그룹 또는 hello 이름 이미 있는 리소스 그룹의의 hello 이름 중 하나를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-212">You can enter either hello name of a new resource group or hello name of a resource group that already exists.</span></span>
 * <span data-ttu-id="68a34-213">**위치**: 여기서 toodeploy hello 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="68a34-213">**Location**: Where toodeploy hello new virtual machine.</span></span> <span data-ttu-id="68a34-214">Tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크를 사용 하도록 하려는 경우 Azure tooyour 온-프레미스 네트워크를 연결 하는 hello 가상 네트워크의 hello 위치를 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-214">If you want tooconnect hello virtual machine tooyour on-premises network, make sure you select hello location of hello virtual network that connects Azure tooyour on-premises network.</span></span> <span data-ttu-id="68a34-215">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]의 [Microsoft Azure 네트워킹][planning-guide-microsoft-azure-networking]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-215">For more information, see [Microsoft Azure networking][planning-guide-microsoft-azure-networking] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>
2. <span data-ttu-id="68a34-216">**크기**:</span><span class="sxs-lookup"><span data-stu-id="68a34-216">**Size**:</span></span>

     <span data-ttu-id="68a34-217">지원되는 VM 유형 목록은 SAP Note [1928533]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-217">For a list of supported VM types, see SAP Note [1928533].</span></span> <span data-ttu-id="68a34-218">Azure 프리미엄 저장소 toouse를 하려는 경우 hello 올바른 VM 유형을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-218">Be sure you select hello correct VM type if you want toouse Azure Premium Storage.</span></span> <span data-ttu-id="68a34-219">모든 VM 유형이 Premium Storage를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-219">Not all VM types support Premium Storage.</span></span> <span data-ttu-id="68a34-220">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]의 [Storage: Microsoft Azure Storage 및 데이터 링크][planning-guide-storage-microsoft-azure-storage-and-data-disks] 및 [Azure Premium Storage][planning-guide-azure-premium-storage]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-220">For more information, see [Storage: Microsoft Azure Storage and data disks][planning-guide-storage-microsoft-azure-storage-and-data-disks] and [Azure Premium Storage][planning-guide-azure-premium-storage] in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span>

3. <span data-ttu-id="68a34-221">**설정**:</span><span class="sxs-lookup"><span data-stu-id="68a34-221">**Settings**:</span></span>
   * <span data-ttu-id="68a34-222">**저장소 계정**: 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-222">**Storage account**: Select an existing storage account or create a new one.</span></span> <span data-ttu-id="68a34-223">모든 저장소 유형이 SAP 응용 프로그램 실행을 위해 작동하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-223">Not all storage types work for running SAP applications.</span></span> <span data-ttu-id="68a34-224">저장소 유형에 대한 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-224">For more information about storage types, see [Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span>
   * <span data-ttu-id="68a34-225">**가상 네트워크** 및 **서브넷**: 인트라넷에 연결 된 tooyour 온-프레미스 네트워크를 가상 네트워크를 선택 hello와 toointegrate hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="68a34-225">**Virtual network** and **Subnet**: toointegrate hello virtual machine with your intranet, select hello virtual network that is connected tooyour on-premises network.</span></span>
   * <span data-ttu-id="68a34-226">**공용 IP 주소**: hello 공용 IP 주소 매개 변수 toocreate 새 공용 IP 주소를 입력 하거나 toouse, 원하는 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-226">**Public IP address**: Select hello public IP address that you want toouse, or enter parameters toocreate a new public IP address.</span></span> <span data-ttu-id="68a34-227">Hello 인터넷을 통해 공용 IP 주소 tooaccess 가상 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-227">You can use a public IP address tooaccess your virtual machine over hello Internet.</span></span> <span data-ttu-id="68a34-228">네트워크 보안 그룹 toohelp 보안 액세스 tooyour 가상 컴퓨터를 만들 수도 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-228">Make sure that you also create a network security group toohelp secure access tooyour virtual machine.</span></span>
   * <span data-ttu-id="68a34-229">**네트워크 보안 그룹**: 자세한 내용은 [네트워크 보안 그룹으로 네트워크 트래픽 흐름 제어][virtual-networks-nsg]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-229">**Network security group**: For more information, see [Control network traffic flow with network security groups][virtual-networks-nsg].</span></span>
   * <span data-ttu-id="68a34-230">**가용성**: 가용성 집합을 선택 하거나 입력 hello 매개 변수 toocreate 새 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-230">**Availability**: Select an availability set, or enter hello parameters toocreate a new availability set.</span></span> <span data-ttu-id="68a34-231">자세한 내용은 [Azure 가용성 집합][planning-guide-3.2.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-231">For more information, see [Azure availability sets][planning-guide-3.2.3].</span></span>
   * <span data-ttu-id="68a34-232">**모니터링**: 진단 모니터링에 대해 **사용 중지**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-232">**Monitoring**: You can select **Disable** for monitoring diagnostics.</span></span> <span data-ttu-id="68a34-233">그가 자동으로 설정 hello 명령을 tooenable hello Azure 고급 모니터링 확장을 실행 하는 경우에 설명 된 대로 [구성 모니터링][deployment-guide-configure-monitoring-scenario-1]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-233">It is enabled automatically when you run hello commands tooenable hello Azure Enhanced Monitoring Extension, as described in [Configure monitoring][deployment-guide-configure-monitoring-scenario-1].</span></span>

4. <span data-ttu-id="68a34-234">**요약**:</span><span class="sxs-lookup"><span data-stu-id="68a34-234">**Summary**:</span></span>

  <span data-ttu-id="68a34-235">선택 내용을 검토한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-235">Review your selections, and then select **OK**.</span></span>

<span data-ttu-id="68a34-236">가상 컴퓨터가 선택한 hello 리소스 그룹에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-236">Your virtual machine is deployed in hello resource group you selected.</span></span>

#### <a name="create-a-virtual-machine-by-using-a-template"></a><span data-ttu-id="68a34-237">템플릿을 사용하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="68a34-237">Create a virtual machine by using a template</span></span>
<span data-ttu-id="68a34-238">Hello에 게시 하는 hello SAP 템플릿 중 하나를 사용 하 여 가상 컴퓨터를 만들 수 [azure-빠른 시작-템플릿 GitHub 리포지토리][azure-quickstart-templates-github]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-238">You can create a virtual machine by using one of hello SAP templates published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="68a34-239">또한 수동으로 만들려면 가상 컴퓨터 hello를 사용 하 여 [Azure 포털][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], 또는 [Azure CLI ][virtual-machines-linux-tutorial].</span><span class="sxs-lookup"><span data-stu-id="68a34-239">You also can manually create a virtual machine by using hello [Azure portal][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], or [Azure CLI][virtual-machines-linux-tutorial].</span></span>

* <span data-ttu-id="68a34-240">[**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="68a34-240">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]</span></span>

  <span data-ttu-id="68a34-241">하나의 가상 컴퓨터를 사용 하 여 2 계층 시스템 toocreate이이 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-241">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="68a34-242">[**3계층 구성(여러 가상 컴퓨터) 템플릿**(sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span><span class="sxs-lookup"><span data-stu-id="68a34-242">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]</span></span>

  <span data-ttu-id="68a34-243">여러 가상 컴퓨터를 사용 하 여 3 계층 시스템 toocreate이이 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-243">toocreate a three-tier system by using multiple virtual machines, use this template.</span></span>

<span data-ttu-id="68a34-244">Azure 포털 hello hello 서식 파일에 대 한 매개 변수 뒤 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-244">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="68a34-245">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="68a34-245">**Basics**:</span></span>
  * <span data-ttu-id="68a34-246">**구독**: hello 구독 toouse toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68a34-246">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="68a34-247">**리소스 그룹**: hello 리소스 그룹 toouse toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68a34-247">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="68a34-248">새 리소스 그룹을 만들거나 hello 구독에 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-248">You can create a new resource group, or you can select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="68a34-249">**위치**: 여기서 toodeploy hello 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-249">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="68a34-250">기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 hello 위치가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-250">If you selected an existing resource group, hello location of that resource group is used.</span></span>

2. <span data-ttu-id="68a34-251">**설정**:</span><span class="sxs-lookup"><span data-stu-id="68a34-251">**Settings**:</span></span>
  * <span data-ttu-id="68a34-252">**SAP 시스템 ID**: hello SAP 시스템 ID (SID)입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-252">**SAP System ID**: hello SAP System ID (SID).</span></span>
  * <span data-ttu-id="68a34-253">**OS 유형**: 운영 체제 toodeploy, 예를 들어, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), 또는 Red Hat Enterprise Linux (RHEL 7.2) 7.2 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-253">**OS type**: hello operating system you want toodeploy, for example, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), or Red Hat Enterprise Linux 7.2 (RHEL 7.2).</span></span>

    <span data-ttu-id="68a34-254">hello 기본 목록 보기는 지원 되는 모든 운영 체제를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-254">hello default list view does not show all supported operating systems.</span></span> <span data-ttu-id="68a34-255">전체 목록을 보려면 **모두 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-255">Select **see all** for a full list.</span></span> <span data-ttu-id="68a34-256">SAP 소프트웨어 배포를 위한 지원되는 운영 체제에 대한 자세한 내용은 SAP Note [1928533]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-256">For more information about supported operating systems for SAP software deployment, see SAP Note [1928533].</span></span>
  * <span data-ttu-id="68a34-257">**SAP 시스템 크기**: hello hello SAP 시스템의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-257">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="68a34-258">hello 수 SAPS hello 새로운 시스템 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-258">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="68a34-259">개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-259">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="68a34-260">**시스템 가용성** (3 계층 템플릿에만 해당): 시스템 가용성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-260">**System availability** (three-tier template only): hello system availability.</span></span>

    <span data-ttu-id="68a34-261">고가용성 설치에 적합한 구성의 경우 **HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-261">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="68a34-262">두 데이터베이스 서버와 ABAP SAP 중앙 서비스(ASCS)에 대한 두 서버가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-262">Two database servers and two servers for ABAP SAP Central Services (ASCS) are created.</span></span>
  * <span data-ttu-id="68a34-263">**저장소 유형** (2 계층 템플릿에만 해당): 저장소 toouse 유형의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-263">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="68a34-264">더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-264">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="68a34-265">저장소 유형에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-265">For more information about storage types, see these resources:</span></span>
      * <span data-ttu-id="68a34-266">[SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]</span><span class="sxs-lookup"><span data-stu-id="68a34-266">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="68a34-267">[Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="68a34-267">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="68a34-268">[Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="68a34-268">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="68a34-269">[Azure 저장소 소개 tooMicrosoft][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="68a34-269">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="68a34-270">**관리 사용자 이름** 및 **관리 암호**: 사용자 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-270">**Admin username** and **Admin password**: A username and password.</span></span>
    <span data-ttu-id="68a34-271">로그인 toohello 가상 컴퓨터에 사용할 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-271">A new user is created, for signing in toohello virtual machine.</span></span>
  * <span data-ttu-id="68a34-272">**새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-272">**New or existing subnet**: Determines whether a new virtual network and subnet are  created or an existing subnet is used.</span></span> <span data-ttu-id="68a34-273">가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-273">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="68a34-274">**서브넷 ID**: hello 서브넷 hello 가상 컴퓨터의 hello ID에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-274">**Subnet ID**: hello ID of hello subnet hello virtual machines will connect to.</span></span> <span data-ttu-id="68a34-275">가상 사설망 (VPN) 또는 Azure ExpressRoute 가상 네트워크 toouse tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-275">Select hello subnet of your virtual private network (VPN) or Azure ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="68a34-276">hello ID 일반적으로 다음과 같은: /subscriptions/&lt;구독 id > /resourceGroups/&lt;리소스 그룹 이름 > /providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름 > /subnets/&lt;서브넷 이름 ></span><span class="sxs-lookup"><span data-stu-id="68a34-276">hello ID usually looks like this: /subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="68a34-277">**사용 약관**:</span><span class="sxs-lookup"><span data-stu-id="68a34-277">**Terms and conditions**:</span></span>  
    <span data-ttu-id="68a34-278">검토 하 고 hello 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-278">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="68a34-279">**구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-279">Select **Purchase**.</span></span>

<span data-ttu-id="68a34-280">hello Azure VM 에이전트는 hello Azure Marketplace에서에서 이미지를 사용 하는 경우 기본적으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-280">hello Azure VM Agent is deployed by default when you use an image from hello Azure Marketplace.</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="68a34-281">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-281">Configure proxy settings</span></span>
<span data-ttu-id="68a34-282">온-프레미스 네트워크 구성 방법에 따라 VM에 tooset hello 프록시를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-282">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="68a34-283">연결 된 tooyour 온-프레미스 네트워크 VPN 또는 express 경로 통해 VM을 사용 하는 경우 hello VM 수 있습니다 수 tooaccess hello 인터넷 및 않습니다 수 toodownload hello 필요한 확장 수 또는 수 모니터링 데이터를 수집.</span><span class="sxs-lookup"><span data-stu-id="68a34-283">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="68a34-284">자세한 내용은 참조 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-284">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="68a34-285">도메인 가입(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="68a34-285">Join a domain (Windows only)</span></span>
<span data-ttu-id="68a34-286">Azure 배포는 Azure 사이트 간 VPN 연결 또는 express 경로 통해 연결 된 tooan 온-프레미스 Active Directory 또는 DNS 인스턴스인 경우 (이 라고 *크로스-프레미스* 에 [Azure 가상 컴퓨터 계획 및 Linux에서의 SAP 용 구현][planning-guide]), 해당 hello VM는 온-프레미스 도메인에 가입 하는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-286">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="68a34-287">이 작업에 대 한 고려 사항에 대 한 자세한 내용은 참조 [(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입][deployment-guide-4.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-287">For more information about considerations for this task, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <span data-ttu-id="68a34-288"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-288"><a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Configure monitoring</span></span>
<span data-ttu-id="68a34-289">사용자 환경에 설명 된 대로 SAP 용 Azure 모니터링 확장 hello 설정 SAP를 지원 하는지 toobe [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-289">toobe sure your environment supports SAP, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="68a34-290">SAP 모니터링 및에 나열 된 hello 리소스에서 SAP 커널 및 SAP 호스트 에이전트의 최소 필수 버전에 대 한 hello 필수 구성 요소 확인 [SAP 리소스][deployment-guide-2.2]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-290">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="68a34-291">모니터링 확인</span><span class="sxs-lookup"><span data-stu-id="68a34-291">Monitoring check</span></span>
<span data-ttu-id="68a34-292">[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-292">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

#### <a name="post-deployment-steps"></a><span data-ttu-id="68a34-293">배포 후 단계</span><span class="sxs-lookup"><span data-stu-id="68a34-293">Post-deployment steps</span></span>
<span data-ttu-id="68a34-294">만든 후 배포 하는 hello VM 및 VM hello, hello VM에서에서 tooinstall hello 필요한 소프트웨어 구성 요소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-294">After you create hello VM and hello VM is deployed, you need tooinstall hello required software components in hello VM.</span></span> <span data-ttu-id="68a34-295">이 유형의 VM 배포에 배포/소프트웨어 설치 시퀀스 hello 때문에 hello 소프트웨어 toobe 설치 하거나 Azure에 연결할 수 있는 디스크 또는 다른 VM에서 사용할 수 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-295">Because of hello deployment/software installation sequence in this type of VM deployment, hello software toobe installed must already be available, either in Azure, on another VM, or as a disk that can be attached.</span></span> <span data-ttu-id="68a34-296">또는 제공할지 크로스-프레미스 시나리오는 연결의 toohello 온-프레미스 자산 (공유 설치)를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-296">Or, consider using a cross-premises scenario, in which connectivity toohello on-premises assets (installation shares) is given.</span></span>

<span data-ttu-id="68a34-297">다음과 같은 hello Azure에서 VM을 배포한 후 온-프레미스 환경에서 사용 하는 때 VM에서 지침 및 도구 tooinstall hello SAP 소프트웨어.</span><span class="sxs-lookup"><span data-stu-id="68a34-297">After you deploy your VM in Azure, follow hello same guidelines and tools tooinstall hello SAP software on your VM as you would in an on-premises environment.</span></span> <span data-ttu-id="68a34-298">또는 모든 hello 파일 서버로 작동 하는 Azure VM을 만드는 tooinstall Azure VM에서 SAP 소프트웨어를 모두 SAP 및 Microsoft 업로드 Azure Vhd에 hello SAP 설치 미디어를 저장 하는 것이 좋습니다 SAP 설치 미디어가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-298">tooinstall SAP software on an Azure VM, both SAP and Microsoft recommend that you upload and store hello SAP installation media on Azure VHDs, or that you create an Azure VM that works as a file server that has all hello required SAP installation media.</span></span>

[comment]: <> (필요한 이유가 무엇입니까 toorecommend 파일 관리, 예를 들어 MSSedusch TODO, 파일 서버 또는 VHD? 온-프레미스에서와 차이가 있나요?)

### <span data-ttu-id="68a34-300"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>시나리오 2: SAP용 사용자 지정 이미지를 사용하여 VM 배포</span><span class="sxs-lookup"><span data-stu-id="68a34-300"><a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Scenario 2: Deploying a VM with a custom image for SAP</span></span>
<span data-ttu-id="68a34-301">서로 다른 버전의 운영 체제 또는 DBMS의 서로 다른 패치 요구 사항 때문에 hello Azure Marketplace에서에서 찾을 hello 이미지 요구를 충족 하지 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-301">Because different versions of an operating system or DBMS have different patch requirements, hello images you find in hello Azure Marketplace might not meet your needs.</span></span> <span data-ttu-id="68a34-302">대신 나중에 다시 배포할 수 있는 사용자 고유의 OS/DBMS VM 이미지를 사용 하 여 toocreate VM을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-302">You might instead want toocreate a VM by using your own OS/DBMS VM image, which you can deploy again later.</span></span>
<span data-ttu-id="68a34-303">Linux 용 다른 단계가 toocreate 개인 이미지를 사용 하 여 Windows 용 toocreate 하나 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-303">You use different steps toocreate a private image for Linux than toocreate one for Windows.</span></span>

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="68a34-305">Windows</span><span class="sxs-lookup"><span data-stu-id="68a34-305">Windows</span></span>
>
> <span data-ttu-id="68a34-306">여러 가상 컴퓨터, Windows 설정 (예: Windows SID 및 호스트 이름) hello 추상화 이거나 일반화 toodeploy hello에 사용할 수 있는 Windows 이미지 tooprepare 온-프레미스 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-306">tooprepare a Windows image that you can use toodeploy multiple virtual machines, hello Windows settings (like Windows SID and hostname) must be abstracted or generalized on hello on-premises VM.</span></span> <span data-ttu-id="68a34-307">사용할 수 있습니다 [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-307">You can use [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo this.</span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="68a34-309">Linux</span><span class="sxs-lookup"><span data-stu-id="68a34-309">Linux</span></span>
>
> <span data-ttu-id="68a34-310">Linux 이미지를 사용할 수 있는 toodeploy 여러 가상 컴퓨터를 tooprepare 일부 Linux 설정이 해야 추상화 된 또는에 일반화 된 hello 온-프레미스 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-310">tooprepare a Linux image that you can use toodeploy multiple virtual machines, some Linux settings must be abstracted or generalized on hello on-premises VM.</span></span> <span data-ttu-id="68a34-311">사용할 수 있습니다 `waagent -deprovision` toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-311">You can use `waagent -deprovision`  toodo this.</span></span> <span data-ttu-id="68a34-312">자세한 내용은 참조 [Azure에서 실행 중인 Linux 가상 컴퓨터를 캡처] [ virtual-machines-linux-capture-image] 및 hello [Azure Linux 에이전트 사용자 가이드][virtual-machines-linux-agent-user-guide-command-line-options]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-312">For more information, see [Capture a Linux virtual machine running on Azure][virtual-machines-linux-capture-image] and hello [Azure Linux agent user guide][virtual-machines-linux-agent-user-guide-command-line-options].</span></span>
>
>

- - -
<span data-ttu-id="68a34-313">준비 및 사용자 지정 이미지 만들기 및 toocreate 사용 여러 새 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-313">You can prepare and create a custom image, and then use it toocreate multiple new VMs.</span></span> <span data-ttu-id="68a34-314">이 방법을 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-314">This is described in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide].</span></span> <span data-ttu-id="68a34-315">SAP Software Provisioning Manager tooinstall 새 SAP 시스템을 사용 하 여 데이터베이스의 설정 내용 (연결 된 toohello 가상 컴퓨터가 VHD에서 데이터베이스 백업을 복원) 또는 직접 하는 경우 Azure 저장소에서 데이터베이스 백업을 복원 하 여 DBMS 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-315">Set up your database content either by using SAP Software Provisioning Manager tooinstall a new SAP system (restores a database backup from a VHD that's attached toohello virtual machine) or by directly restoring a database backup from Azure storage, if your DBMS supports it.</span></span> <span data-ttu-id="68a34-316">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-316">For more information, see [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide].</span></span> <span data-ttu-id="68a34-317">이미 온-프레미스 VM (특히 2 계층 시스템) 용에 SAP 시스템을 설치한 경우 조정할 수 있습니다 hello SAP 시스템 설정을 hello Azure VM의 hello 배포 후 SAP 소프트웨어 구축에서 지 원하는 hello 이름 바꾸기 절차를 사용 하 여 관리자 (SAP Note [1619720]).</span><span class="sxs-lookup"><span data-stu-id="68a34-317">If you have already installed an SAP system on your on-premises VM (especially for two-tier systems), you can adapt hello SAP system settings after hello deployment of hello Azure VM by using hello System Rename procedure supported by SAP Software Provisioning Manager (SAP Note [1619720]).</span></span> <span data-ttu-id="68a34-318">그렇지 않으면 hello Azure VM을 배포한 후 hello SAP 소프트웨어를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-318">Otherwise, you can install hello SAP software after you deploy hello Azure VM.</span></span>

<span data-ttu-id="68a34-319">hello 다음 순서도 hello SAP 관련 사용자 지정 이미지에서 VM을 배포 하기 위한 단계를 순서 대로</span><span class="sxs-lookup"><span data-stu-id="68a34-319">hello following flowchart shows hello SAP-specific sequence of steps for deploying a VM from a custom image:</span></span>

![개인 Marketplace에서 VM 이미지를 사용하여 SAP 시스템용 VM 배포 순서도][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a><span data-ttu-id="68a34-321">Hello 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="68a34-321">Create hello virtual machine</span></span>
<span data-ttu-id="68a34-322">hello Azure 포털에서에서 개인 OS 이미지를 사용 하 여 배포 toocreate hello SAP 서식 파일을 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-322">toocreate a deployment by using a private OS image from hello Azure portal, use one of hello following SAP templates.</span></span> <span data-ttu-id="68a34-323">이러한 템플릿은 hello에 게시 된 [azure-빠른 시작-템플릿 GitHub 리포지토리][azure-quickstart-templates-github]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-323">These templates are published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="68a34-324">또한 [PowerShell][virtual-machines-upload-image-windows-resource-manager]을 사용하여 가상 컴퓨터를 수동으로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-324">You also can manually create a virtual machine, by using [PowerShell][virtual-machines-upload-image-windows-resource-manager].</span></span>

* <span data-ttu-id="68a34-325">[**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="68a34-325">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-image)][sap-templates-2-tier-user-image]</span></span>

  <span data-ttu-id="68a34-326">하나의 가상 컴퓨터를 사용 하 여 2 계층 시스템 toocreate이이 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-326">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>
* <span data-ttu-id="68a34-327">[**3계층 구성(여러 가상 컴퓨터) 템플릿**(sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span><span class="sxs-lookup"><span data-stu-id="68a34-327">[**Three-tier configuration (multiple virtual machines) template** (sap-3-tier-user-image)][sap-templates-3-tier-user-image]</span></span>

  <span data-ttu-id="68a34-328">여러 가상 컴퓨터 또는 운영 체제 이미지를 직접 사용 하 여 3 계층 시스템 toocreate이이 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-328">toocreate a three-tier system by using multiple virtual machines or your own OS image, use this template.</span></span>

<span data-ttu-id="68a34-329">Azure 포털 hello hello 서식 파일에 대 한 매개 변수 뒤 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-329">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="68a34-330">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="68a34-330">**Basics**:</span></span>
  * <span data-ttu-id="68a34-331">**구독**: hello 구독 toouse toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68a34-331">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="68a34-332">**리소스 그룹**: hello 리소스 그룹 toouse toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68a34-332">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="68a34-333">Hello 구독에 기존 리소스 그룹을 선택 하거나 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-333">You can create a new resource group or select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="68a34-334">**위치**: 여기서 toodeploy hello 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-334">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="68a34-335">기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 hello 위치가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-335">If you selected an existing resource group, hello location of that resource group is used.</span></span>
2. <span data-ttu-id="68a34-336">**설정**:</span><span class="sxs-lookup"><span data-stu-id="68a34-336">**Settings**:</span></span>
  * <span data-ttu-id="68a34-337">**SAP 시스템 ID**: hello SAP 시스템 id입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-337">**SAP System ID**: hello SAP System ID.</span></span>
  * <span data-ttu-id="68a34-338">**OS 유형**: hello 운영 체제 유형을 toodeploy (Windows 또는 Linux)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-338">**OS type**: hello operating system type you want toodeploy (Windows or Linux).</span></span>
  * <span data-ttu-id="68a34-339">**SAP 시스템 크기**: hello hello SAP 시스템의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-339">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="68a34-340">hello 수 SAPS hello 새로운 시스템 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-340">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="68a34-341">개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-341">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="68a34-342">**시스템 가용성** (3 계층 템플릿에만 해당): 시스템 가용성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-342">**System availability** (three-tier template only): hello system availability.</span></span>

    <span data-ttu-id="68a34-343">고가용성 설치에 적합한 구성의 경우 **HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-343">Select **HA** for a configuration that is suitable for a high-availability installation.</span></span> <span data-ttu-id="68a34-344">ASCS용 2개의 데이터베이스 서버 및 2개의 서버가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-344">Two database servers and two servers for ASCS are created.</span></span>
  * <span data-ttu-id="68a34-345">**저장소 유형** (2 계층 템플릿에만 해당): 저장소 toouse 유형의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-345">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="68a34-346">더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-346">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="68a34-347">저장소 형식에 대 한 자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="68a34-347">For more information about storage types, see hello following resources:</span></span>
      * <span data-ttu-id="68a34-348">[SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]</span><span class="sxs-lookup"><span data-stu-id="68a34-348">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="68a34-349">[Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="68a34-349">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="68a34-350">[Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="68a34-350">[Premium Storage: High-performance storage for Azure virtual machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="68a34-351">[Azure 저장소 소개 tooMicrosoft][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="68a34-351">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="68a34-352">**사용자 이미지 VHD URI**: hello 개인 OS 이미지, 예를 들어 https:// VHD URI hello&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-352">**User image VHD URI**: hello URI of hello private OS image VHD, for example, https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="68a34-353">**사용자 이미지 저장소 계정이**: hello 개인 OS 이미지가 저장 된 예를 들어 hello 저장소 계정의 hello 이름을 &lt;accountname > https://에서&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-353">**User image storage account**: hello name of hello storage account where hello private OS image is stored, for example, &lt;accountname> in https://&lt;accountname>.blob.core.windows.net/vhds/userimage.vhd.</span></span>
  * <span data-ttu-id="68a34-354">**관리자 사용자 이름** 및 **관리자 암호**: hello 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="68a34-354">**Admin username** and **Admin password**: hello username and password.</span></span>

    <span data-ttu-id="68a34-355">로그인 toohello 가상 컴퓨터에 사용할 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-355">A new user is created, for signing in toohello virtual machine.</span></span>
  * <span data-ttu-id="68a34-356">**새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-356">**New or existing subnet**: Determines whether a new virtual network and subnet is created or an existing subnet is used.</span></span> <span data-ttu-id="68a34-357">가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-357">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="68a34-358">**서브넷 ID**: hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-358">**Subnet ID**: hello ID of hello subnet toowhich hello virtual machines will connect to.</span></span> <span data-ttu-id="68a34-359">VPN 또는 express 경로 가상 네트워크 toouse tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-359">Select hello subnet of your VPN or ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="68a34-360">hello ID는 일반적으로 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-360">hello ID usually looks like this:</span></span>

    <span data-ttu-id="68a34-361">/subscriptions/&lt;구독 id>/resourceGroups/&lt;리소스 그룹 이름>/providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름>/subnets/&lt;서브넷 이름></span><span class="sxs-lookup"><span data-stu-id="68a34-361">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="68a34-362">**사용 약관**:</span><span class="sxs-lookup"><span data-stu-id="68a34-362">**Terms and conditions**:</span></span>  
    <span data-ttu-id="68a34-363">검토 하 고 hello 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-363">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="68a34-364">**구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-364">Select **Purchase**.</span></span>

#### <a name="install-hello-vm-agent-linux-only"></a><span data-ttu-id="68a34-365">Hello VM 에이전트 (Linux에만 해당) 설치</span><span class="sxs-lookup"><span data-stu-id="68a34-365">Install hello VM Agent (Linux only)</span></span>
<span data-ttu-id="68a34-366">toouse hello 템플릿 hello 이전 섹션에에서 설명 된 Linux 에이전트는 hello 사용자 이미지 또는 hello 배포에 이미 설치 되어 있어야 하는 hello 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-366">toouse hello templates described in hello preceding section, hello Linux Agent must already be installed in hello user image, or hello deployment will fail.</span></span> <span data-ttu-id="68a34-367">다운로드 하 여에 설명 된 대로 hello 사용자 이미지의 hello VM 에이전트 설치 [다운로드, 설치 및 hello Azure VM 에이전트를 사용 하도록 설정][deployment-guide-4.4]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-367">Download and install hello VM Agent in hello user image as described in [Download, install, and enable hello Azure VM Agent][deployment-guide-4.4].</span></span> <span data-ttu-id="68a34-368">템플릿 hello를 사용 하지 않는 경우 나중에 VM 에이전트 hello도 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-368">If you don’t use hello templates, you also can install hello VM Agent later.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="68a34-369">도메인 가입(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="68a34-369">Join a domain (Windows only)</span></span>
<span data-ttu-id="68a34-370">Azure 배포는 Azure 사이트 간 VPN 연결 또는 Azure ExpressRoute를 통해 연결 된 tooan 온-프레미스 Active Directory 또는 DNS 인스턴스인 경우 (이 라고 *크로스-프레미스* 에 [Azure 가상 컴퓨터 계획 및 구현 Linux에서의 SAP 용][planning-guide]), 해당 hello VM는 온-프레미스 도메인에 가입 하는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-370">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or Azure ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="68a34-371">이 단계에 대 한 고려 사항에 대 한 자세한 내용은 참조 [(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입][deployment-guide-4.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-371">For more information about considerations for this step, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="68a34-372">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-372">Configure proxy settings</span></span>
<span data-ttu-id="68a34-373">온-프레미스 네트워크 구성 방법에 따라 VM에 tooset hello 프록시를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-373">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="68a34-374">연결 된 tooyour 온-프레미스 네트워크 VPN 또는 express 경로 통해 VM을 사용 하는 경우 hello VM 수 있습니다 수 tooaccess hello 인터넷 및 않습니다 수 toodownload hello 필요한 확장 수 또는 수 모니터링 데이터를 수집.</span><span class="sxs-lookup"><span data-stu-id="68a34-374">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="68a34-375">자세한 내용은 참조 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-375">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="68a34-376">모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-376">Configure monitoring</span></span>
<span data-ttu-id="68a34-377">사용자 환경에 설명 된 대로 SAP 용 Azure 모니터링 확장 hello 설정 SAP를 지원 하는지 toobe [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-377">toobe sure your environment supports SAP, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="68a34-378">SAP 모니터링 및에 나열 된 hello 리소스에서 SAP 커널 및 SAP 호스트 에이전트의 최소 필수 버전에 대 한 hello 필수 구성 요소 확인 [SAP 리소스][deployment-guide-2.2]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-378">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="68a34-379">모니터링 확인</span><span class="sxs-lookup"><span data-stu-id="68a34-379">Monitoring check</span></span>
<span data-ttu-id="68a34-380">[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-380">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>




### <span data-ttu-id="68a34-381"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>시나리오 3: SAP에서 일반화되지 않은 Azure VHD를 사용하여 온-프레미스 VM 이동</span><span class="sxs-lookup"><span data-stu-id="68a34-381"><a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Scenario 3: Moving an on-premises VM by using a non-generalized Azure VHD with SAP</span></span>
<span data-ttu-id="68a34-382">이 시나리오에서는 온-프레미스 환경 tooAzure에서 특정 SAP 시스템 toomove를 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-382">In this scenario, you plan toomove a specific SAP system from an on-premises environment tooAzure.</span></span> <span data-ttu-id="68a34-383">있습니다 수 hello hello OS, SAP 바이너리 hello, VHD를 업로드 하 여이 작업을 수행할 결국 DBMS 바이너리 및 hello 데이터로 hello Vhd hello 및 로그 파일의 DBMS tooAzure hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-383">You can do this by uploading hello VHD that has hello OS, hello SAP binaries, and eventually hello DBMS binaries, plus hello VHDs with hello data and log files of hello DBMS, tooAzure.</span></span> <span data-ttu-id="68a34-384">에 설명 된 hello 시나리오와 달리 [시나리오 2: SAP 용 사용자 지정 이미지를 사용 하 여 VM 배포][deployment-guide-3.3],이 경우 hello 호스트 이름, SAP SID 유지 및 없기 때문에 hello Azure VM에서에서 SAP 사용자 계정 hello 온-프레미스 환경에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-384">Unlike hello scenario described in [Scenario 2: Deploying a VM with a custom image for SAP][deployment-guide-3.3], in this case, you keep hello hostname, SAP SID, and SAP user accounts in hello Azure VM, because they were configured in hello on-premises environment.</span></span> <span data-ttu-id="68a34-385">Toogeneralize hello OS 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-385">You do not need toogeneralize hello OS.</span></span> <span data-ttu-id="68a34-386">이 시나리오는 가장 자주 toocross 온-프레미스 SAP 지형 hello의 일부는 온-프레미스를 실행 하 고 시나리오의 일부는 Azure에서 실행을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-386">This scenario applies most often toocross-premises scenarios where part of hello SAP landscape runs on-premises and part of it runs on Azure.</span></span>

<span data-ttu-id="68a34-387">이 시나리오에서는 hello VM 에이전트가 설치 되지 않았습니다 자동으로 배포 중.</span><span class="sxs-lookup"><span data-stu-id="68a34-387">In this scenario, hello VM Agent is not automatically installed during deployment.</span></span> <span data-ttu-id="68a34-388">때문에 VM 에이전트 hello 및 hello Azure 고급 모니터링 확장의 SAP 용 toorun SAP에 필요한, 해야 toodownload, 설치 및 활성화는 모두 hello 가상 컴퓨터를 만든 후에 수동으로 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-388">Because hello VM Agent and hello Azure Enhanced Monitoring Extension for SAP required for toorun SAP, you need toodownload, install, and enable both components manually after you create hello virtual machine.</span></span>

<span data-ttu-id="68a34-389">Hello Azure VM 에이전트에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-389">For more information about hello Azure VM Agent, see hello following resources.</span></span>

[comment]: <> (MSSedusch TODO - 아래 Windows 링크 업데이트)

- - -
> ![Windows][Logo_Windows] <span data-ttu-id="68a34-392">Windows</span><span class="sxs-lookup"><span data-stu-id="68a34-392">Windows</span></span>
>
> <span data-ttu-id="68a34-393"><http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx></span><span class="sxs-lookup"><span data-stu-id="68a34-393"><http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx></span></span>
>
> ![Linux][Logo_Linux] <span data-ttu-id="68a34-395">Linux</span><span class="sxs-lookup"><span data-stu-id="68a34-395">Linux</span></span>
>
> <span data-ttu-id="68a34-396">[Azure Linux 에이전트 사용자 가이드][virtual-machines-linux-agent-user-guide]</span><span class="sxs-lookup"><span data-stu-id="68a34-396">[Azure Linux Agent User Guide][virtual-machines-linux-agent-user-guide]</span></span>
>
>

- - -

<span data-ttu-id="68a34-397">다음 순서도 hello 단계는 온-프레미스 VM 일반화 되지 않은 Azure VHD를 사용 하 여 이동에 대 한 hello 시퀀스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-397">hello following flowchart shows hello sequence of steps for moving an on-premises VM by using a non-generalized Azure VHD:</span></span>

![VM 디스크를 사용하여 SAP 시스템용 VM 배포 순서도][deployment-guide-figure-400]

<span data-ttu-id="68a34-399">Hello 디스크 이미 업로드 및 Azure에 정의 된 이라고 가정할 (참조 [Azure 가상 컴퓨터 계획 및 구현 Linux에서의 SAP 용][planning-guide]), hello 작업에에서 설명 된 수행 hello 다음 몇 개 섹션.</span><span class="sxs-lookup"><span data-stu-id="68a34-399">Assuming that hello disk is already uploaded and defined in Azure (see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), do hello tasks described in hello next few sections.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="68a34-400">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="68a34-400">Create a virtual machine</span></span>
<span data-ttu-id="68a34-401">hello에 게시 된 hello SAP 서식 파일을 사용 하는 hello Azure 포털을 통해 개인 OS 디스크를 사용 하 여 배포 toocreate [azure-빠른 시작-템플릿 GitHub 리포지토리][azure-quickstart-templates-github]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-401">toocreate a deployment by using a private OS disk through hello Azure portal, use hello SAP template published in hello [azure-quickstart-templates GitHub repository][azure-quickstart-templates-github].</span></span> <span data-ttu-id="68a34-402">또한 PowerShell을 사용하여 가상 컴퓨터를 직접 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-402">You also can manually create a virtual machine, by using PowerShell.</span></span>

* <span data-ttu-id="68a34-403">[**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span><span class="sxs-lookup"><span data-stu-id="68a34-403">[**Two-tier configuration (only one virtual machine) template** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]</span></span>

  <span data-ttu-id="68a34-404">하나의 가상 컴퓨터를 사용 하 여 2 계층 시스템 toocreate이이 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-404">toocreate a two-tier system by using only one virtual machine, use this template.</span></span>

<span data-ttu-id="68a34-405">Azure 포털 hello hello 서식 파일에 대 한 매개 변수 뒤 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-405">In hello Azure portal, enter hello following parameters for hello template:</span></span>

1. <span data-ttu-id="68a34-406">**기본 사항**:</span><span class="sxs-lookup"><span data-stu-id="68a34-406">**Basics**:</span></span>
  * <span data-ttu-id="68a34-407">**구독**: hello 구독 toouse toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68a34-407">**Subscription**: hello subscription toouse toodeploy hello template.</span></span>
  * <span data-ttu-id="68a34-408">**리소스 그룹**: hello 리소스 그룹 toouse toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="68a34-408">**Resource group**: hello resource group toouse toodeploy hello template.</span></span> <span data-ttu-id="68a34-409">Hello 구독에 기존 리소스 그룹을 선택 하거나 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-409">You can create a new resource group or select an existing resource group in hello subscription.</span></span>
  * <span data-ttu-id="68a34-410">**위치**: 여기서 toodeploy hello 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-410">**Location**: Where toodeploy hello template.</span></span> <span data-ttu-id="68a34-411">기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 hello 위치가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-411">If you selected an existing resource group, hello location of that resource group is used.</span></span>
2. <span data-ttu-id="68a34-412">**설정**:</span><span class="sxs-lookup"><span data-stu-id="68a34-412">**Settings**:</span></span>
  * <span data-ttu-id="68a34-413">**SAP 시스템 ID**: hello SAP 시스템 id입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-413">**SAP System ID**: hello SAP System ID.</span></span>
  * <span data-ttu-id="68a34-414">**OS 유형**: hello 운영 체제 유형을 toodeploy (Windows 또는 Linux)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-414">**OS type**: hello operating system type you want toodeploy (Windows or Linux).</span></span>
  * <span data-ttu-id="68a34-415">**SAP 시스템 크기**: hello hello SAP 시스템의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-415">**SAP system size**: hello size of hello SAP system.</span></span>

    <span data-ttu-id="68a34-416">hello 수 SAPS hello 새로운 시스템 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-416">hello number of SAPS hello new system provides.</span></span> <span data-ttu-id="68a34-417">개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-417">If you are not sure how many SAPS hello system requires, ask your SAP Technology Partner or System Integrator.</span></span>
  * <span data-ttu-id="68a34-418">**저장소 유형** (2 계층 템플릿에만 해당): 저장소 toouse 유형의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-418">**Storage type** (two-tier template only): hello type of storage toouse.</span></span>

    <span data-ttu-id="68a34-419">더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-419">For larger systems, we highly recommend using Azure Premium Storage.</span></span> <span data-ttu-id="68a34-420">저장소 형식에 대 한 자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="68a34-420">For more information about storage types, see hello following resources:</span></span>
      * <span data-ttu-id="68a34-421">[SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]</span><span class="sxs-lookup"><span data-stu-id="68a34-421">[Use of Azure Premium SSD Storage for SAP DBMS Instance][2367194]</span></span>
      * <span data-ttu-id="68a34-422">[Linux에서 SAP용 Azure Virtual Machine DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]</span><span class="sxs-lookup"><span data-stu-id="68a34-422">[Microsoft Azure Storage][dbms-guide-2.3] in [Azure Virtual Machine DBMS deployment for SAP on Linux][dbms-guide]</span></span>
      * <span data-ttu-id="68a34-423">[Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]</span><span class="sxs-lookup"><span data-stu-id="68a34-423">[Premium Storage: High-performance storage for Azure Virtual Machine workloads][storage-premium-storage-preview-portal]</span></span>
      * <span data-ttu-id="68a34-424">[Azure 저장소 소개 tooMicrosoft][storage-introduction]</span><span class="sxs-lookup"><span data-stu-id="68a34-424">[Introduction tooMicrosoft Azure Storage][storage-introduction]</span></span>
  * <span data-ttu-id="68a34-425">**OS 디스크 VHD URI**: hello 개인 OS 디스크의 예를 들어 https:// URI hello&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-425">**OS disk VHD URI**: hello URI of hello private OS disk, for example, https://&lt;accountname>.blob.core.windows.net/vhds/osdisk.vhd.</span></span>
  * <span data-ttu-id="68a34-426">**새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-426">**New or existing subnet**: Determines whether a new virtual network and subnet are created, or an existing subnet is used.</span></span> <span data-ttu-id="68a34-427">가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-427">If you already have a virtual network that is connected tooyour on-premises network, select **Existing**.</span></span>
  * <span data-ttu-id="68a34-428">**서브넷 ID**: hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-428">**Subnet ID**: hello ID of hello subnet toowhich hello virtual machines will connect to.</span></span> <span data-ttu-id="68a34-429">VPN 이나 Azure express 경로 가상 네트워크 toouse tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-429">Select hello subnet of your VPN or Azure ExpressRoute virtual network toouse tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="68a34-430">hello ID는 일반적으로 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-430">hello ID usually looks like this:</span></span>

    <span data-ttu-id="68a34-431">/subscriptions/&lt;구독 id>/resourceGroups/&lt;리소스 그룹 이름>/providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름>/subnets/&lt;서브넷 이름></span><span class="sxs-lookup"><span data-stu-id="68a34-431">/subscriptions/&lt;subscription id>/resourceGroups/&lt;resource group name>/providers/Microsoft.Network/virtualNetworks/&lt;virtual network name>/subnets/&lt;subnet name></span></span>

3. <span data-ttu-id="68a34-432">**사용 약관**:</span><span class="sxs-lookup"><span data-stu-id="68a34-432">**Terms and conditions**:</span></span>  
    <span data-ttu-id="68a34-433">검토 하 고 hello 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-433">Review and accept hello legal terms.</span></span>

4.  <span data-ttu-id="68a34-434">**구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-434">Select **Purchase**.</span></span>

#### <a name="install-hello-vm-agent"></a><span data-ttu-id="68a34-435">Hello VM 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-435">Install hello VM Agent</span></span>
<span data-ttu-id="68a34-436">서식 파일에 설명 된 toouse hello hello 이전 섹션, hello VM 에이전트를 설치 해야 hello 운영 체제 디스크 또는 hello 배포가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-436">toouse hello templates described in hello preceding section, hello VM Agent must be installed on hello OS disk, or hello deployment will fail.</span></span> <span data-ttu-id="68a34-437">다운로드 하 여에 설명 된 대로 VM hello에 hello VM 에이전트 설치 [다운로드, 설치 및 hello Azure VM 에이전트를 사용 하도록 설정][deployment-guide-4.4]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-437">Download and install hello VM Agent in hello VM, as described in [Download, install, and enable hello Azure VM Agent][deployment-guide-4.4].</span></span>

<span data-ttu-id="68a34-438">Hello 이전 섹션에에서 설명 된 대로 hello 템플릿을 사용 하지 않는 경우 나중에 hello VM 에이전트를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-438">If you don’t use hello templates described in hello preceding section, you can also install hello VM Agent afterwards.</span></span>

#### <a name="join-a-domain-windows-only"></a><span data-ttu-id="68a34-439">도메인 가입(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="68a34-439">Join a domain (Windows only)</span></span>
<span data-ttu-id="68a34-440">Azure 배포는 Azure 사이트 간 VPN 연결 또는 express 경로 통해 연결 된 tooan 온-프레미스 Active Directory 또는 DNS 인스턴스인 경우 (이 라고 *크로스-프레미스* 에 [Azure 가상 컴퓨터 계획 및 Linux에서의 SAP 용 구현][planning-guide]), 해당 hello VM는 온-프레미스 도메인에 가입 하는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-440">If your Azure deployment is connected tooan on-premises Active Directory or DNS instance via an Azure site-to-site VPN connection or ExpressRoute (this is called *cross-premises* in [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]), it is expected that hello VM is joining an on-premises domain.</span></span> <span data-ttu-id="68a34-441">이 작업에 대 한 고려 사항에 대 한 자세한 내용은 참조 [(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입][deployment-guide-4.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-441">For more information about considerations for this task, see [Join a VM tooan on-premises domain (Windows only)][deployment-guide-4.3].</span></span>

#### <a name="configure-proxy-settings"></a><span data-ttu-id="68a34-442">프록시 설정 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-442">Configure proxy settings</span></span>
<span data-ttu-id="68a34-443">온-프레미스 네트워크 구성 방법에 따라 VM에 tooset hello 프록시를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-443">Depending on how your on-premises network is configured, you might need tooset up hello proxy on your VM.</span></span> <span data-ttu-id="68a34-444">연결 된 tooyour 온-프레미스 네트워크 VPN 또는 express 경로 통해 VM을 사용 하는 경우 hello VM 수 있습니다 수 tooaccess hello 인터넷 및 않습니다 수 toodownload hello 필요한 확장 수 또는 수 모니터링 데이터를 수집.</span><span class="sxs-lookup"><span data-stu-id="68a34-444">If your VM is connected tooyour on-premises network via VPN or ExpressRoute, hello VM might not be able tooaccess hello Internet, and won't be able toodownload hello required extensions or collect monitoring data.</span></span> <span data-ttu-id="68a34-445">자세한 내용은 참조 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-445">For more information, see [Configure hello proxy][deployment-guide-configure-proxy].</span></span>

#### <a name="configure-monitoring"></a><span data-ttu-id="68a34-446">모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-446">Configure monitoring</span></span>
<span data-ttu-id="68a34-447">사용자 환경에 설명 된 대로 SAP 용 Azure 모니터링 확장 hello 설정 SAP를 지원 하는지 toobe [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-447">toobe sure your environment supports SAP, set up hello Azure Monitoring Extension for SAP as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="68a34-448">SAP 모니터링 및에 나열 된 hello 리소스에서 SAP 커널 및 SAP 호스트 에이전트의 최소 필수 버전에 대 한 hello 필수 구성 요소 확인 [SAP 리소스][deployment-guide-2.2]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-448">Check hello prerequisites for SAP monitoring, and required minimum versions of SAP Kernel and SAP Host Agent, in hello resources listed in [SAP resources][deployment-guide-2.2].</span></span>

#### <a name="monitoring-check"></a><span data-ttu-id="68a34-449">모니터링 확인</span><span class="sxs-lookup"><span data-stu-id="68a34-449">Monitoring check</span></span>
<span data-ttu-id="68a34-450">[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-450">Check whether monitoring is working, as described in [Checks and troubleshooting for setting up end-to-end monitoring][deployment-guide-troubleshooting-chapter].</span></span>

## <a name="update-hello-monitoring-configuration-for-sap"></a><span data-ttu-id="68a34-451">SAP 용 hello 모니터링 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="68a34-451">Update hello monitoring configuration for SAP</span></span>
<span data-ttu-id="68a34-452">Hello hello 다음 시나리오 중 하나에서 SAP 모니터링 구성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-452">Update hello SAP monitoring configuration in any of hello following scenarios:</span></span>
* <span data-ttu-id="68a34-453">hello 공동 Microsoft/SAP 팀 hello 모니터링 기능을 확장 하 고 더 많거나 적은 카운터를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-453">hello joint Microsoft/SAP team extends hello monitoring capabilities and requests more or fewer counters.</span></span>
* <span data-ttu-id="68a34-454">Microsoft hello 기본 Azure 인프라의 hello 모니터링 데이터를 제공 하는 새 버전을 도입 하 고 SAP 요구 toobe에 대 한 Azure 고급 모니터링 확장 hello toothose 변경을 채택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-454">Microsoft introduces a new version of hello underlying Azure infrastructure that delivers hello monitoring data, and hello Azure Enhanced Monitoring Extension for SAP needs toobe adapted toothose changes.</span></span>
* <span data-ttu-id="68a34-455">추가 Vhd tooyour Azure VM을 탑재 하거나 VHD를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-455">You mount additional VHDs tooyour Azure VM or you remove a VHD.</span></span> <span data-ttu-id="68a34-456">이 시나리오에서는 저장소 관련 데이터의 hello 컬렉션을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-456">In this scenario, update hello collection of storage-related data.</span></span> <span data-ttu-id="68a34-457">끝점을 삭제 하거나, IP를 할당 하 여 구성 변경 주소 tooa VM hello 모니터링 구성을 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-457">Changing your configuration by adding or deleting endpoints or by assigning IP addresses tooa VM does not affect hello monitoring configuration.</span></span>
* <span data-ttu-id="68a34-458">Azure VM의 hello 크기 예를 들어에서 변경한 크기 A5 tooany 다른 VM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-458">You change hello size of your Azure VM, for example, from size A5 tooany other VM size.</span></span>
* <span data-ttu-id="68a34-459">새 네트워크 인터페이스 tooyour Azure VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-459">You add new network interfaces tooyour Azure VM.</span></span>

<span data-ttu-id="68a34-460">단계를 모니터링 설정을 업데이트 hello hello를 수행 하 여 모니터링 인프라 tooupdate [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-460">tooupdate monitoring settings, update hello monitoring infrastructure by following hello steps in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a><span data-ttu-id="68a34-461">Linux VM에서 SAP 소프트웨어 배포에 대한 세부 작업</span><span class="sxs-lookup"><span data-stu-id="68a34-461">Detailed tasks for SAP software deployment on a Windows VM</span></span>
<span data-ttu-id="68a34-462">이 섹션에 hello 구성 및 배포 프로세스에서 특정 작업을 수행 하는 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-462">This section has detailed steps for doing specific tasks in hello configuration and deployment process.</span></span>

### <span data-ttu-id="68a34-463"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Azure PowerShell cmdlet 배포</span><span class="sxs-lookup"><span data-stu-id="68a34-463"><a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Deploy Azure PowerShell cmdlets</span></span>
1.  <span data-ttu-id="68a34-464">너무 이동[Microsoft Azure 다운로드](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-464">Go too[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="68a34-465">**명령줄 도구** 아래의 **PowerShell** 아래에서 **Windows 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-465">Under **Command-line tools**, under **PowerShell**, select **Windows install**.</span></span>
3.  <span data-ttu-id="68a34-466">다운로드 한 hello 파일 (예를 들어 WindowsAzurePowershellGet.3f.3f.3fnew.exe)에 대 한 hello Microsoft 다운로드 관리자 대화 상자에서 선택 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-466">In hello Microsoft Download Manager dialog box, for hello downloaded file (for example, WindowsAzurePowershellGet.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="68a34-467">Microsoft 웹 플랫폼 설치 관리자 (Microsoft 웹 PI) toorun 선택 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-467">toorun Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="68a34-468">다음과 같은 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-468">A page that looks like this appears:</span></span>

  <span data-ttu-id="68a34-469">![Azure PowerShell cmdlet 설치 페이지][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="68a34-469">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="68a34-470">선택 **설치**, 다음 hello Microsoft 소프트웨어 사용 조건에 동의 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-470">Select **Install**, and then accept hello Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="68a34-471">PowerShell이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-471">PowerShell is installed.</span></span> <span data-ttu-id="68a34-472">선택 **마침** tooclose hello 설치 마법사.</span><span class="sxs-lookup"><span data-stu-id="68a34-472">Select **Finish** tooclose hello installation wizard.</span></span>

<span data-ttu-id="68a34-473">일반적으로 매월 업데이트 되며 업데이트 toohello PowerShell cmdlet에 대 한 자주 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-473">Check frequently for updates toohello PowerShell cmdlets, which usually are updated monthly.</span></span> <span data-ttu-id="68a34-474">업데이트에 대 한 가장 쉬운 방법은 toocheck hello는 toodo hello 이전 toohello 설치 페이지 5 단계에 표시 된 설치 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-474">hello easiest way toocheck for updates is toodo hello preceding installation steps, up toohello installation page shown in step 5.</span></span> <span data-ttu-id="68a34-475">hello 릴리스 날짜 및 릴리스 번호 hello cmdlet의 5 단계에 표시 된 hello 페이지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-475">hello release date and release number of hello cmdlets are included on hello page shown in step 5.</span></span> <span data-ttu-id="68a34-476">SAP Note에서 달리 명시 하지 않는 한 [1928533] 또는 SAP Note [2015553], hello 최신 버전의 Azure PowerShell cmdlet 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-476">Unless stated otherwise in SAP Note [1928533] or SAP Note [2015553], we recommend that you work with hello latest version of Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="68a34-477">toocheck hello 버전의 hello 사용자 컴퓨터에 설치 된 Azure PowerShell cmdlet이 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-477">toocheck hello version of hello Azure PowerShell cmdlets that are installed on your computer, run this PowerShell command:</span></span>
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
<span data-ttu-id="68a34-478">hello 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-478">hello result looks like this:</span></span>

<span data-ttu-id="68a34-479">![Azure PowerShell cmdlet 버전 검사의 결과][deployment-guide-figure-600]
<a name="figure-6"></a></span><span class="sxs-lookup"><span data-stu-id="68a34-479">![Result of Azure PowerShell cmdlet version check][deployment-guide-figure-600]
<a name="figure-6"></a></span></span>

<span data-ttu-id="68a34-480">Hello Azure cmdlet 버전이 컴퓨터에 설치 되어 현재 버전 hello 이면 hello 설치 마법사의 첫 번째 페이지 hello 나타냅니다 추가 하 여 **(설치)** toohello 제품명 (hello 다음 스크린샷 참조).</span><span class="sxs-lookup"><span data-stu-id="68a34-480">If hello Azure cmdlet version installed on your computer is hello current version, hello first page of hello installation wizard indicates it by adding **(Installed)** toohello product title (see hello following screenshot).</span></span> <span data-ttu-id="68a34-481">사용자의 PowerShell Azure cmdlet은 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-481">Your PowerShell Azure cmdlets are up-to-date.</span></span> <span data-ttu-id="68a34-482">tooclose hello 설치 마법사, 선택 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-482">tooclose hello installation wizard, select **Exit**.</span></span>

<span data-ttu-id="68a34-483">![설치 된 Azure PowerShell cmdlet의 해당 hello 가장 최신 버전을 나타내는 Azure PowerShell cmdlet에 대 한 설치 페이지][deployment-guide-figure-700]
<a name="figure-7"></a></span><span class="sxs-lookup"><span data-stu-id="68a34-483">![Installation page for Azure PowerShell cmdlets indicating that hello most recent version of Azure PowerShell cmdlets are installed][deployment-guide-figure-700]
<a name="figure-7"></a></span></span>

### <span data-ttu-id="68a34-484"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Azure CLI 배포</span><span class="sxs-lookup"><span data-stu-id="68a34-484"><a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Deploy Azure CLI</span></span>
1.  <span data-ttu-id="68a34-485">너무 이동[Microsoft Azure 다운로드](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-485">Go too[Microsoft Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>
2.  <span data-ttu-id="68a34-486">아래 **명령줄 도구**아래 **Azure 명령줄 인터페이스**선택, hello **설치** 운영 체제에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-486">Under **Command-line tools**, under **Azure command-line interface**, select hello **Install** link for your operating system.</span></span>
3.  <span data-ttu-id="68a34-487">다운로드 한 hello 파일 (예를 들어 WindowsAzureXPlatCLI.3f.3f.3fnew.exe)에 대 한 hello Microsoft 다운로드 관리자 대화 상자에서 선택 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-487">In hello Microsoft Download Manager dialog box, for hello downloaded file (for example, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), select **Run**.</span></span>
4.  <span data-ttu-id="68a34-488">Microsoft 웹 플랫폼 설치 관리자 (Microsoft 웹 PI) toorun 선택 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-488">toorun Microsoft Web Platform Installer (Microsoft Web PI), select **Yes**.</span></span>
5.  <span data-ttu-id="68a34-489">다음과 같은 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-489">A page that looks like this appears:</span></span>

  <span data-ttu-id="68a34-490">![Azure PowerShell cmdlet 설치 페이지][deployment-guide-figure-500]<a name="figure-5"></a></span><span class="sxs-lookup"><span data-stu-id="68a34-490">![Installation page for Azure PowerShell cmdlets][deployment-guide-figure-500]<a name="figure-5"></a></span></span>

6.  <span data-ttu-id="68a34-491">선택 **설치**, 다음 hello Microsoft 소프트웨어 사용 조건에 동의 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-491">Select **Install**, and then accept hello Microsoft Software License Terms.</span></span>
7.  <span data-ttu-id="68a34-492">Azure CLI가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-492">Azure CLI is installed.</span></span> <span data-ttu-id="68a34-493">선택 **마침** tooclose hello 설치 마법사.</span><span class="sxs-lookup"><span data-stu-id="68a34-493">Select **Finish** tooclose hello installation wizard.</span></span>

<span data-ttu-id="68a34-494">업데이트 tooAzure CLI 일반적으로 매월 업데이트 됩니다에 대 한 자주 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-494">Check frequently for updates tooAzure CLI, which usually is updated monthly.</span></span> <span data-ttu-id="68a34-495">업데이트에 대 한 가장 쉬운 방법은 toocheck hello는 toodo hello 이전 toohello 설치 페이지 5 단계에 표시 된 설치 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-495">hello easiest way toocheck for updates is toodo hello preceding installation steps, up toohello installation page shown in step 5.</span></span>


<span data-ttu-id="68a34-496">toocheck hello 버전의 컴퓨터에 설치 된 Azure CLI이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-496">toocheck hello version of Azure CLI that is installed on your computer, run this command:</span></span>
```
azure --version
```

<span data-ttu-id="68a34-497">hello 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-497">hello result looks like this:</span></span>

<span data-ttu-id="68a34-498">![Azure CLI 버전 검사의 결과][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span><span class="sxs-lookup"><span data-stu-id="68a34-498">![Result of Azure CLI version check][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a></span></span>

### <span data-ttu-id="68a34-499"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="68a34-499"><a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Join a VM tooan on-premises domain (Windows only)</span></span>
<span data-ttu-id="68a34-500">크로스-프레미스 시나리오에서 SAP Vm을 배포 하는 경우 온-프레미스 Active Directory 및 DNS를 Azure에서 확장 된 것 hello Vm 온-프레미스 도메인에 가입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-500">If you deploy SAP VMs in a cross-premises scenario, where on-premises Active Directory and DNS are extended in Azure, it is expected that hello VMs are joining an on-premises domain.</span></span> <span data-ttu-id="68a34-501">hello toojoin VM tooan 온-프레미스 도메인을 사용 하는 자세한 단계 및 hello 필요한 추가 소프트웨어 toobe는 온-프레미스 도메인의 구성원에 따라 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-501">hello detailed steps you take toojoin a VM tooan on-premises domain, and hello additional software required toobe a member of an on-premises domain, varies by customer.</span></span> <span data-ttu-id="68a34-502">일반적으로, VM tooan toojoin 온-프레미스 도메인, 맬웨어 방지 프로그램 소프트웨어 및 백업 또는 모니터링 소프트웨어와 같은 tooinstall 추가 소프트웨어가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-502">Usually, toojoin a VM tooan on-premises domain, you need tooinstall additional software, like antimalware software, and backup or monitoring software.</span></span>

<span data-ttu-id="68a34-503">이 시나리오에서 VM 환경에서 도메인에 연결할 때 인터넷 프록시 설정을 강제 hello Windows hello 게스트 VM에서에서 로컬 시스템 계정 (S-1-5-18)에 같은 프록시 설정을 hello 있는지 toomake가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-503">In this scenario, you also need toomake sure that if Internet proxy settings are forced when a VM joins a domain in your environment, hello Windows Local System Account (S-1-5-18) in hello Guest VM has hello same proxy settings.</span></span> <span data-ttu-id="68a34-504">hello 가장 쉬운 방법은 tooforce hello 프록시 도메인 toosystems hello 도메인에 적용 되는 그룹 정책을 사용 하 여입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-504">hello easiest option is tooforce hello proxy by using a domain Group Policy, which applies toosystems in hello domain.</span></span>

### <span data-ttu-id="68a34-505"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>다운로드, 설치 및 hello Azure VM 에이전트를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68a34-505"><a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Download, install, and enable hello Azure VM Agent</span></span>
<span data-ttu-id="68a34-506">(예: 하지 않는 hello sysprep 나 Windows 시스템 준비 도구에서 생성 되는 이미지)이 생성 되어 있지는 OS 이미지에서 배포 되는 가상 컴퓨터를 toomanually 다운로드, 설치 및 사용 hello Azure VM 에이전트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-506">For virtual machines that are deployed from an OS image that is not generalized (for example, an image that doesn't originate in hello Windows System Preparation, or sysprep, tool), you need toomanually download, install, and enable hello Azure VM Agent.</span></span>

<span data-ttu-id="68a34-507">Hello Azure Marketplace에서에서 VM을 배포 하는 경우에이 단계가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-507">If you deploy a VM from hello Azure Marketplace, this step is not required.</span></span> <span data-ttu-id="68a34-508">Hello Azure Marketplace에서에서 이미지 hello Azure VM 에이전트는 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-508">Images from hello Azure Marketplace already have hello Azure VM Agent.</span></span>

#### <span data-ttu-id="68a34-509"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span><span class="sxs-lookup"><span data-stu-id="68a34-509"><a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows</span></span>
1.  <span data-ttu-id="68a34-510">Hello Azure VM 에이전트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-510">Download hello Azure VM Agent:</span></span>
  1.  <span data-ttu-id="68a34-511">Hello 다운로드 [Azure VM 에이전트 설치 관리자 패키지](https://go.microsoft.com/fwlink/?LinkId=394789)합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-511">Download hello [Azure VM Agent installer package](https://go.microsoft.com/fwlink/?LinkId=394789).</span></span>
  2.  <span data-ttu-id="68a34-512">개인용 컴퓨터 또는 서버 hello VM 에이전트 MSI 패키지를 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-512">Store hello VM Agent MSI package locally on a personal computer or server.</span></span>
2.  <span data-ttu-id="68a34-513">Hello Azure VM 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-513">Install hello Azure VM Agent:</span></span>
  1.  <span data-ttu-id="68a34-514">연결 toohello 프로토콜 RDP (원격 데스크톱)를 사용 하 여 Azure VM을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-514">Connect toohello deployed Azure VM by using Remote Desktop Protocol (RDP).</span></span>
  2.  <span data-ttu-id="68a34-515">Hello VM 에이전트의 MSI 파일 hello에 대 한 대상 디렉터리 선택 hello 및 hello VM에서 Windows 탐색기 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-515">Open a Windows Explorer window on hello VM and select hello target directory for hello MSI file of hello VM Agent.</span></span>
  3.  <span data-ttu-id="68a34-516">Hello VM에서 VM 에이전트 hello의 로컬 컴퓨터/서버 toohello 대상 디렉터리에서 hello Azure VM 에이전트 설치 프로그램 MSI 파일을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-516">Drag hello Azure VM Agent Installer MSI file from your local computer/server toohello target directory of hello VM Agent on hello VM.</span></span>
  4.  <span data-ttu-id="68a34-517">Hello VM에 hello MSI 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-517">Double-click hello MSI file on hello VM.</span></span>
3.  <span data-ttu-id="68a34-518">Vm는 조인 된 tooon 온-프레미스 도메인에 대해 확인 결과적 인터넷 프록시 설정이 적용 toohello Windows 로컬 시스템 계정 (S-1-5-18)에서 VM hello에 설명 된 대로 [hello 프록시 구성] [ deployment-guide-configure-proxy].</span><span class="sxs-lookup"><span data-stu-id="68a34-518">For VMs that are joined tooon-premises domains, make sure that eventual Internet proxy settings also apply toohello Windows Local System account (S-1-5-18) in hello VM, as described in [Configure hello proxy][deployment-guide-configure-proxy].</span></span> <span data-ttu-id="68a34-519">hello VM 에이전트는이 컨텍스트에서 실행 되며 toobe 수 tooconnect tooAzure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-519">hello VM Agent runs in this context and needs toobe able tooconnect tooAzure.</span></span>

<span data-ttu-id="68a34-520">사용자 개입 없이 필요한 tooupdate hello Azure VM 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-520">No user interaction is required tooupdate hello Azure VM Agent.</span></span> <span data-ttu-id="68a34-521">hello VM 에이전트가 자동으로 업데이트 및 VM 다시 시작할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-521">hello VM Agent is automatically updated, and does not require a VM restart.</span></span>

#### <span data-ttu-id="68a34-522"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span><span class="sxs-lookup"><span data-stu-id="68a34-522"><a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux</span></span>
<span data-ttu-id="68a34-523">사용 하 여 hello 다음 Linux 용 tooinstall hello VM 에이전트를 명령:</span><span class="sxs-lookup"><span data-stu-id="68a34-523">Use hello following commands tooinstall hello VM Agent for Linux:</span></span>

* <span data-ttu-id="68a34-524">**SELS(SUSE Linux Enterprise Server)**</span><span class="sxs-lookup"><span data-stu-id="68a34-524">**SUSE Linux Enterprise Server (SLES)**</span></span>

  ```
  sudo zypper install WALinuxAgent
  ```

* <span data-ttu-id="68a34-525">**RHEL(Red Hat Enterprise Linux)**</span><span class="sxs-lookup"><span data-stu-id="68a34-525">**Red Hat Enterprise Linux (RHEL)**</span></span>

  ```
  sudo yum install WALinuxAgent
  ```

<span data-ttu-id="68a34-526">Tooupdate hello Azure Linux 에이전트에 설명 된 단계를 hello 수행 hello 에이전트가 이미 설치 되어 있으면 [GitHub에서 VM toohello 최신 버전에서 업데이트 hello Azure Linux 에이전트][virtual-machines-linux-update-agent]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-526">If hello agent is already installed, tooupdate hello Azure Linux Agent, do hello steps described in [Update hello Azure Linux Agent on a VM toohello latest version from GitHub][virtual-machines-linux-update-agent].</span></span>

### <span data-ttu-id="68a34-527"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Hello 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-527"><a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Configure hello proxy</span></span>
<span data-ttu-id="68a34-528">Windows에서 tooconfigure hello 프록시를 수행 하는 hello 단계는 Linux에서 hello 프록시를 구성 하는 hello 방법은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-528">hello steps you take tooconfigure hello proxy in Windows are different from hello way you configure hello proxy in Linux.</span></span>

#### <a name="windows"></a><span data-ttu-id="68a34-529">Windows</span><span class="sxs-lookup"><span data-stu-id="68a34-529">Windows</span></span>
<span data-ttu-id="68a34-530">프록시 설정이 올바르게 설정 해야 hello tooaccess hello 인터넷 로컬 시스템 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-530">Proxy settings must be set up correctly for hello Local System account tooaccess hello Internet.</span></span> <span data-ttu-id="68a34-531">프록시 설정이 그룹 정책에 의해을 설정 하지는 hello 로컬 시스템 계정에 대 한 hello 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-531">If your proxy settings are not set by Group Policy, you can configure hello settings for hello Local System account.</span></span>

1. <span data-ttu-id="68a34-532">너무 이동**시작**, 입력 **gpedit.msc**를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-532">Go too**Start**, enter **gpedit.msc**, and then select **Enter**.</span></span>
2. <span data-ttu-id="68a34-533">**컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소** > **Internet Explorer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-533">Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Internet Explorer**.</span></span> <span data-ttu-id="68a34-534">해당 hello 설정 되었는지 확인 **프록시 설정을 컴퓨터별 (보다는 만들기 사용자 단위)** 비활성화 되었거나 구성 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-534">Make sure that hello setting **Make proxy settings per-machine (rather than per-user)** is disabled or not configured.</span></span>
3. <span data-ttu-id="68a34-535">**제어판**, 너무 이동**네트워크 및 공유 센터** > **인터넷 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-535">In **Control Panel**, go too**Network and Sharing Center** > **Internet Options**.</span></span>
4. <span data-ttu-id="68a34-536">Hello에 **연결** 탭, 선택 hello **LAN 설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-536">On hello **Connections** tab, select hello **LAN settings** button.</span></span>
5. <span data-ttu-id="68a34-537">지우기 hello **자동으로 설정 검색** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-537">Clear hello **Automatically detect settings** check box.</span></span>
6. <span data-ttu-id="68a34-538">선택 hello **사용자 LAN에 프록시 서버를 사용 하 여** 확인란을 선택한 다음 hello 프록시 주소와 포트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-538">Select hello **Use a proxy server for your LAN** check box, and then enter hello proxy address and port.</span></span>
7. <span data-ttu-id="68a34-539">선택 hello **고급** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-539">Select hello **Advanced** button.</span></span>
8. <span data-ttu-id="68a34-540">Hello에 **예외** 상자 hello IP 주소를 입력 **168.63.129.16**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-540">In hello **Exceptions** box, enter hello IP address **168.63.129.16**.</span></span> <span data-ttu-id="68a34-541">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-541">Select **OK**.</span></span>


#### <a name="linux"></a><span data-ttu-id="68a34-542">Linux</span><span class="sxs-lookup"><span data-stu-id="68a34-542">Linux</span></span>
<span data-ttu-id="68a34-543">Hello에 있는 Microsoft Azure 게스트 에이전트의 hello 구성 파일에서 올바른 프록시 hello 구성 \\등\\waagent.conf 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-543">Configure hello correct proxy in hello configuration file of hello Microsoft Azure Guest Agent, which is located at \\etc\\waagent.conf.</span></span>

<span data-ttu-id="68a34-544">Hello 매개 변수 뒤를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-544">Set hello following parameters:</span></span>

1.  <span data-ttu-id="68a34-545">**HTTP 프록시 호스트**</span><span class="sxs-lookup"><span data-stu-id="68a34-545">**HTTP proxy host**.</span></span> <span data-ttu-id="68a34-546">예를 들어 너무 설정**proxy.corp.local**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-546">For example, set it too**proxy.corp.local**.</span></span>
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  <span data-ttu-id="68a34-547">**HTTP 프록시 포트**</span><span class="sxs-lookup"><span data-stu-id="68a34-547">**HTTP proxy port**.</span></span> <span data-ttu-id="68a34-548">예를 들어 너무 설정**80**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-548">For example, set it too**80**.</span></span>
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  <span data-ttu-id="68a34-549">Hello 에이전트를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-549">Restart hello agent.</span></span>

  ```
  sudo service waagent restart
  ```

<span data-ttu-id="68a34-550">프록시 설정이 hello \\등\\waagent.conf도 필요한 toohello VM 확장을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-550">hello proxy settings in \\etc\\waagent.conf also apply toohello required VM extensions.</span></span> <span data-ttu-id="68a34-551">Toouse 하려는 경우 Azure 저장소 hello hello 트래픽 toothese 저장소는 온-프레미스 인트라넷을 통해 잘못 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-551">If you want toouse hello Azure repositories, make sure that hello traffic toothese repositories is not going through your on-premises intranet.</span></span> <span data-ttu-id="68a34-552">사용자 정의 만든 경우 경로 tooenable 강제 터널링, toohello 저장소 트래픽을 라우팅하는 경로 추가 해야 toohello 인터넷에 직접를 사용 하 여 사이트 간 VPN 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-552">If you created user-defined routes tooenable forced tunneling, make sure that you add a route that routes traffic toohello repositories directly toohello Internet, and not through your site-to-site VPN connection.</span></span>

* <span data-ttu-id="68a34-553">**SLES**</span><span class="sxs-lookup"><span data-stu-id="68a34-553">**SLES**</span></span>

  <span data-ttu-id="68a34-554">에 나열 된 hello IP 주소에도 tooadd 경로 필요 \\등\\regionserverclnt.cfg 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-554">You also need tooadd routes for hello IP addresses listed in \\etc\\regionserverclnt.cfg.</span></span> <span data-ttu-id="68a34-555">hello 다음 그림은 예:</span><span class="sxs-lookup"><span data-stu-id="68a34-555">hello following figure shows an example:</span></span>

  ![강제 터널링][deployment-guide-figure-50]


* <span data-ttu-id="68a34-557">**RHEL**</span><span class="sxs-lookup"><span data-stu-id="68a34-557">**RHEL**</span></span>

  <span data-ttu-id="68a34-558">에 나열 된 hello 호스트의 IP 주소 hello에도 tooadd 경로 필요 \\등\\yum.repos.d\\rhui-부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-558">You also need tooadd routes for hello IP addresses of hello hosts listed in \\etc\\yum.repos.d\\rhui-load-balancers.</span></span> <span data-ttu-id="68a34-559">예를 들어 hello 앞에 그림을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-559">For an example, see hello preceding figure.</span></span>

<span data-ttu-id="68a34-560">사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달][virtual-networks-udr-overview]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-560">For more information about user-defined routes, see [User-defined routes and IP forwarding][virtual-networks-udr-overview].</span></span>

### <span data-ttu-id="68a34-561"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Azure 고급 모니터링 확장의 SAP 용 hello 구성</span><span class="sxs-lookup"><span data-stu-id="68a34-561"><a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Configure hello Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="68a34-562">에 설명 된 대로 hello VM 준비 했으므로 때 [Azure에서의 SAP 용 Vm 배포 시나리오][deployment-guide-3], hello hello 가상 컴퓨터에 Azure VM 에이전트가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-562">When you've prepared hello VM as described in [Deployment scenarios of VMs for SAP on Azure][deployment-guide-3], hello Azure VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="68a34-563">hello 다음 단계는 toodeploy hello Azure 고급 모니터링 확장 hello 글로벌 Azure 데이터 센터에서 Azure 확장 리포지토리에서 hello에서 사용할 수 있는 SAP 용입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-563">hello next step is toodeploy hello Azure Enhanced Monitoring Extension for SAP, which is available in hello Azure Extension Repository in hello global Azure datacenters.</span></span> <span data-ttu-id="68a34-564">자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide-9.1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-564">For more information, see [Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide-9.1].</span></span>

<span data-ttu-id="68a34-565">PowerShell 또는 Azure CLI tooinstall를 사용할 수 있으며 Azure 고급 모니터링 확장의 SAP 용 hello 구성.</span><span class="sxs-lookup"><span data-stu-id="68a34-565">You can use PowerShell or Azure CLI tooinstall and configure hello Azure Enhanced Monitoring Extension for SAP.</span></span> <span data-ttu-id="68a34-566">Windows 컴퓨터를 사용 하 여 Windows 또는 Linux VM에서 tooinstall hello 확장 참조 [Azure PowerShell][deployment-guide-4.5.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-566">tooinstall hello extension on a Windows or Linux VM by using a Windows machine, see [Azure PowerShell][deployment-guide-4.5.1].</span></span> <span data-ttu-id="68a34-567">Linux 데스크톱을 사용 하 여 Linux VM의 tooinstall hello 확장 참조 [Azure CLI][deployment-guide-4.5.2]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-567">tooinstall hello extension on a Linux VM by using a Linux desktop, see [Azure CLI][deployment-guide-4.5.2].</span></span>

#### <span data-ttu-id="68a34-568"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Linux 및 Windows VM용 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="68a34-568"><a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell for Linux and Windows VMs</span></span>
<span data-ttu-id="68a34-569">PowerShell을 사용 하 여 tooinstall hello Azure 고급 모니터링 확장의 SAP 용:</span><span class="sxs-lookup"><span data-stu-id="68a34-569">tooinstall hello Azure Enhanced Monitoring Extension for SAP by using PowerShell:</span></span>

1. <span data-ttu-id="68a34-570">Hello hello Azure PowerShell cmdlet의 최신 버전을 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-570">Make sure that you have installed hello latest version of hello Azure PowerShell cmdlet.</span></span> <span data-ttu-id="68a34-571">자세한 내용은 [Azure PowerShell cmdlet 배포][deployment-guide-4.1]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-571">For more information, see [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>  
2. <span data-ttu-id="68a34-572">Hello 다음 PowerShell cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-572">Run hello following PowerShell cmdlet.</span></span>
  <span data-ttu-id="68a34-573">사용 가능한 환경 목록을 보려면 `commandlet Get-AzureRmEnvironment`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-573">For a list of available environments, run `commandlet Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="68a34-574">Toouse 공용 Azure에서 사용자 환경에는 원하는 경우 **azure 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-574">If you want toouse public Azure, your environment is **AzureCloud**.</span></span> <span data-ttu-id="68a34-575">중국의 Azure인 경우 **AzureChinaCloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-575">For Azure in China, select **AzureChinaCloud**.</span></span>


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

<span data-ttu-id="68a34-576">계정 데이터를 입력 하 고 hello Azure 가상 컴퓨터를 식별 한 후 hello 스크립트 hello 필수 확장명을 배포 하 고 hello 필요한 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-576">After you enter your account data and identify hello Azure virtual machine, hello script deploys hello required extensions and enables hello required features.</span></span> <span data-ttu-id="68a34-577">이 작업은 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-577">This can take several minutes.</span></span>
<span data-ttu-id="68a34-578">`Set-AzureRmVMAEMExtension`에 대한 자세한 내용은[Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-578">For more information about `Set-AzureRmVMAEMExtension`, see [Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension].</span></span>

![SAP 관련 Azure cmdlet Set-AzureRmVMAEMExtension의 성공적인 실행][deployment-guide-figure-900]

<span data-ttu-id="68a34-580">hello `Set-AzureRmVMAEMExtension` 구성과 모든 hello 단계 tooconfigure 호스트 SAP 용 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-580">hello `Set-AzureRmVMAEMExtension` configuration does all hello steps tooconfigure host monitoring for SAP.</span></span>

<span data-ttu-id="68a34-581">hello 다음 정보를 포함 하는 hello 스크립트 출력:</span><span class="sxs-lookup"><span data-stu-id="68a34-581">hello script output includes hello following information:</span></span>

* <span data-ttu-id="68a34-582">확인 구성 된 VM toohello 탑재 그에 대 한 모니터링 기본 hello (hello OS)가 있는 VHD 및 모든 추가 Vhd.</span><span class="sxs-lookup"><span data-stu-id="68a34-582">Confirmation that monitoring for hello base VHD (with hello OS) and all additional VHDs mounted toohello VM has been configured.</span></span>
* <span data-ttu-id="68a34-583">hello 다음 두 메시지는 특정 저장소 계정에 대 한 저장소 메트릭의 hello 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-583">hello next two messages confirm hello configuration of Storage Metrics for a specific storage account.</span></span>
* <span data-ttu-id="68a34-584">출력 한 줄에 hello hello 모니터링 구성의 실제 업데이트의 hello 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-584">One line of output gives hello status of hello actual update of hello monitoring configuration.</span></span>
* <span data-ttu-id="68a34-585">다른 출력 줄이 해당 hello 구성이 배포 또는 업데이트 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-585">Another line of output confirms that hello configuration has been deployed or updated.</span></span>
* <span data-ttu-id="68a34-586">출력의 마지막 줄 hello는 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-586">hello last line of output is informational.</span></span> <span data-ttu-id="68a34-587">테스트 hello 모니터링 구성에 대 한 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-587">It shows your options for testing hello monitoring configuration.</span></span>

<span data-ttu-id="68a34-588">에 설명 된 대로 Azure 고급 모니터링의 모든 단계가 성공적으로 실행 하 고 hello 필요한 데이터를 제공 하는 Azure 인프라 해당 hello toocheck 계속 hello Azure 고급 모니터링 확장 SAP 용 hello 준비 확인 [SAP 용 Azure 고급 모니터링에 대 한 준비 상태 검사가][deployment-guide-5.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-588">toocheck that all steps of Azure Enhanced Monitoring have been executed successfully, and that hello Azure Infrastructure provides hello necessary data, proceed with hello readiness check for hello Azure Enhanced Monitoring Extension for SAP, as described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="68a34-589">Azure 진단 toocollect hello 관련 데이터 15-30 분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-589">Wait 15-30 minutes for Azure Diagnostics toocollect hello relevant data.</span></span>

#### <span data-ttu-id="68a34-590"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Linux VM용 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="68a34-590"><a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI for Linux VMs</span></span>
<span data-ttu-id="68a34-591">tooinstall hello Azure 고급 모니터링 확장의 SAP 용 Azure CLI를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="68a34-591">tooinstall hello Azure Enhanced Monitoring Extension for SAP by using Azure CLI:</span></span>

1. <span data-ttu-id="68a34-592">에 설명 된 대로 Azure CLI를 설치 [설치 hello Azure CLI][azure-cli]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-592">Install Azure CLI, as described in [Install hello Azure CLI][azure-cli].</span></span>
2. <span data-ttu-id="68a34-593">Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-593">Sign in with your Azure account:</span></span>

  ```
  azure login
  ```

3. <span data-ttu-id="68a34-594">TooAzure Resource Manager 모드로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-594">Switch tooAzure Resource Manager mode:</span></span>

  ```
  azure config mode arm
  ```

4. <span data-ttu-id="68a34-595">Azure 고급 모니터링을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-595">Enable Azure Enhanced Monitoring:</span></span>

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. <span data-ttu-id="68a34-596">Hello Azure Linux VM에 활성화 되어 해당 hello Azure 고급 모니터링 확장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-596">Verify that hello Azure Enhanced Monitoring Extension is active on hello Azure Linux VM.</span></span> <span data-ttu-id="68a34-597">검사 파일을 여부 hello \\var\\lib\\AzureEnhancedMonitor\\PerfCounters 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-597">Check whether hello file \\var\\lib\\AzureEnhancedMonitor\\PerfCounters exists.</span></span> <span data-ttu-id="68a34-598">이 특성이 있으면 명령 프롬프트에서이 명령을 toodisplay 정보 hello Azure 향상 된 모니터에 의해 수집 된를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-598">If it exists, at a command prompt, run this command toodisplay information collected by hello Azure Enhanced Monitor:</span></span>
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

<span data-ttu-id="68a34-599">hello 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-599">hello output looks like this:</span></span>
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <span data-ttu-id="68a34-600"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>종단 간 모니터링 확인 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="68a34-600"><a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Checks and troubleshooting for end-to-end monitoring</span></span>
<span data-ttu-id="68a34-601">Azure VM을 배포 하면 관련 Azure 모니터링 인프라 hello 설정한 후 hello Azure 고급 모니터링 확장의 모든 hello 구성 요소가 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-601">After you have deployed your Azure VM and set up hello relevant Azure monitoring infrastructure, check whether all hello components of hello Azure Enhanced Monitoring Extension are working as expected.</span></span>

<span data-ttu-id="68a34-602">에 설명 된 대로 Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 hello 준비 검사를 실행 [Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 준비 상태 검사가][deployment-guide-5.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-602">Run hello readiness check for hello Azure Enhanced Monitoring Extension for SAP as described in [Readiness check for hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-5.1].</span></span> <span data-ttu-id="68a34-603">모든 준비 검사 결과가 긍정적이고 모든 관련 성능 카운터가 정상으로 나타나면 Azure 모니터링이 성공적으로 설정된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-603">If all readiness check results are positive and all relevant performance counters appear OK, Azure monitoring successfully set up.</span></span> <span data-ttu-id="68a34-604">Hello에 hello SAP Note에서 설명 하는 SAP 호스트 에이전트 설치를 진행할 수 [SAP 리소스][deployment-guide-2.2]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-604">You can proceed with hello installation of SAP Host Agent described in hello SAP Notes in [SAP resources][deployment-guide-2.2].</span></span> <span data-ttu-id="68a34-605">Hello 준비 확인 되는 것 카운터가 누락 되었거나에 설명 된 대로 Azure 모니터링 인프라 hello에 대 한 hello 상태 검사를 실행 하는 경우 [Azure 모니터링 인프라 구성에 대 한 상태 검사] [ deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="68a34-605">If hello readiness check indicates that counters are missing, run hello health check for hello Azure monitoring infrastructure, as described in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="68a34-606">자세한 문제 해결 옵션은 [SAP용 Azure 모니터링 문제 해결][deployment-guide-5.3]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-606">For more troubleshooting options, see [Troubleshooting Azure monitoring for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="68a34-607"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 준비 확인</span><span class="sxs-lookup"><span data-stu-id="68a34-607"><a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Readiness check for hello Azure Enhanced Monitoring Extension for SAP</span></span>
<span data-ttu-id="68a34-608">이 검사 하면 SAP 응용 프로그램 내에 표시 되는 모든 성능 메트릭을 hello 기본 Azure 모니터링 인프라에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-608">This check makes sure that all performance metrics that appear inside your SAP application are provided by hello underlying Azure monitoring infrastructure.</span></span>

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a><span data-ttu-id="68a34-609">Windows VM에서 hello 준비 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-609">Run hello readiness check on a Windows VM</span></span>

1.  <span data-ttu-id="68a34-610">Toohello Azure 가상 컴퓨터에에서 로그인 (관리자 계정을 사용 하 여 필요 하지 않음).</span><span class="sxs-lookup"><span data-stu-id="68a34-610">Sign in toohello Azure virtual machine (using an admin account is not necessary).</span></span>
2.  <span data-ttu-id="68a34-611">명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-611">Open a Command Prompt window.</span></span>
3.  <span data-ttu-id="68a34-612">Hello 명령 프롬프트에서 hello 디렉터리 toohello 설치 폴더의 hello Azure 고급 모니터링 확장 SAP에 대 한 변경: c:\\패키지\\플러그 인\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;버전 >\\삭제</span><span class="sxs-lookup"><span data-stu-id="68a34-612">At hello command prompt, change hello directory toohello installation folder of hello Azure Enhanced Monitoring Extension for SAP: C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop</span></span>

  <span data-ttu-id="68a34-613">hello *버전* hello 경로 toohello에 모니터링 확장 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-613">hello *version* in hello path toohello monitoring extension might vary.</span></span> <span data-ttu-id="68a34-614">여러 버전의 hello 설치 폴더, hello AzureEnhancedMonitoring Windows 서비스의 hello 구성 확인 화면에 확장을 모니터링 하는 hello에 대 한 폴더를 표시 하 고 스위치 toohello 폴더도 표시 되는 다음 경우 *경로 tooexecutable* .</span><span class="sxs-lookup"><span data-stu-id="68a34-614">If you see folders for multiple versions of hello monitoring extension in hello installation folder, check hello configuration of hello AzureEnhancedMonitoring Windows service, and then switch toohello folder indicated as *Path tooexecutable*.</span></span>

  ![서비스 실행 중의 속성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-figure-1000]

4.  <span data-ttu-id="68a34-616">Hello 명령 프롬프트에서 실행 **azperflib.exe** 매개 변수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-616">At hello command prompt, run **azperflib.exe** without any parameters.</span></span>

  > [!NOTE]
  > <span data-ttu-id="68a34-617">Azperflib.exe는 루프에서 실행 되며 60 초 마다 hello 수집 된 카운터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-617">Azperflib.exe runs in a loop and updates hello collected counters every 60 seconds.</span></span> <span data-ttu-id="68a34-618">명령 프롬프트 창 닫기 hello tooend hello 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-618">tooend hello loop, close hello Command Prompt window.</span></span>
  >
  >

<span data-ttu-id="68a34-619">Azure 고급 모니터링 확장 설치 되지 않은 hello 또는 hello AzureEnhancedMonitoring 서비스를 실행 하지 않는 경우 hello 확장이 올바르게 구성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-619">If hello Azure Enhanced Monitoring Extension is not installed, or hello AzureEnhancedMonitoring service is not running, hello extension has not been configured correctly.</span></span> <span data-ttu-id="68a34-620">Toodeploy 확장 hello 하는 방법에 대 한 자세한 내용은 참조 [문제 해결 SAP 용 Azure 모니터링 인프라 hello][deployment-guide-5.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-620">For detailed information about how toodeploy hello extension, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

##### <a name="check-hello-output-of-azperflibexe"></a><span data-ttu-id="68a34-621">Azperflib.exe의 hello 출력 확인</span><span class="sxs-lookup"><span data-stu-id="68a34-621">Check hello output of azperflib.exe</span></span>
<span data-ttu-id="68a34-622">Azperflib.exe 출력은 SAP용 Azure 성능 카운터가 모두 채워진 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-622">Azperflib.exe output shows all populated Azure performance counters for SAP.</span></span> <span data-ttu-id="68a34-623">수집 된 카운터 목록의 hello의 hello 맨 아래에 요약 및 상태 표시기 Azure 모니터링의 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-623">At hello bottom of hello list of collected counters, a summary and health indicator show hello status of Azure monitoring.</span></span>

<span data-ttu-id="68a34-624">![문제가 없음을 나타내는 azperflib.exe를 실행하여 표시된 상태 검사 출력][deployment-guide-figure-1100]
<a name="figure-11"></a></span><span class="sxs-lookup"><span data-stu-id="68a34-624">![Output of health check by executing azperflib.exe, which indicates that no problems exist][deployment-guide-figure-1100]
<a name="figure-11"></a></span></span>

<span data-ttu-id="68a34-625">Hello에 대 한 반환 하는 hello 결과 확인 **카운터 합계** 및 비어 있는 것으로 보고 되는 출력 **상태**hello 앞 그림에에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-625">Check hello result returned for hello **Counters total** output, which is reported as empty, and for **Health status**, shown in hello preceding figure.</span></span>

<span data-ttu-id="68a34-626">Hello 결과 값을 다음과 같이 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-626">Interpret hello resulting values as follows:</span></span>

| <span data-ttu-id="68a34-627">Azperflib.exe 결과 값</span><span class="sxs-lookup"><span data-stu-id="68a34-627">Azperflib.exe result values</span></span> | <span data-ttu-id="68a34-628">Azure 모니터링 상태 정보</span><span class="sxs-lookup"><span data-stu-id="68a34-628">Azure monitoring health status</span></span> |
| --- | --- |
| <span data-ttu-id="68a34-629">**API 호출 - 사용할 수 없음**</span><span class="sxs-lookup"><span data-stu-id="68a34-629">**API Calls - not available**</span></span> | <span data-ttu-id="68a34-630">사용할 수 없는 카운터 중 하나는 적용 되지 않음 toohello 가상 컴퓨터 구성 될 수 있습니다 또는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-630">Counters that are not available might be either not applicable toohello virtual machine configuration, or are errors.</span></span> <span data-ttu-id="68a34-631">**상태 정보**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-631">See **Health status**.</span></span> |
| <span data-ttu-id="68a34-632">**카운터 합계 - 비어 있음**</span><span class="sxs-lookup"><span data-stu-id="68a34-632">**Counters total - empty**</span></span> |<span data-ttu-id="68a34-633">다음 두 개의 Azure 저장소 카운터 hello 비어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-633">hello following two Azure storage counters can be empty:</span></span> <ul><li><span data-ttu-id="68a34-634">저장소 읽기 작업 대기 시간 서버 밀리초</span><span class="sxs-lookup"><span data-stu-id="68a34-634">Storage Read Op Latency Server msec</span></span></li><li><span data-ttu-id="68a34-635">저장소 읽기 작업 대기 시간 E2E 밀리초</span><span class="sxs-lookup"><span data-stu-id="68a34-635">Storage Read Op Latency E2E msec</span></span></li></ul><span data-ttu-id="68a34-636">그 외의 카운터는 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-636">All other counters must have values.</span></span> |
| <span data-ttu-id="68a34-637">**상태 정보**</span><span class="sxs-lookup"><span data-stu-id="68a34-637">**Health status**</span></span> |<span data-ttu-id="68a34-638">반환 상태가 **OK**를 표시하는 경우에만 OK입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-638">Only OK if return status shows **OK**.</span></span> |
| <span data-ttu-id="68a34-639">**진단**</span><span class="sxs-lookup"><span data-stu-id="68a34-639">**Diagnostics**</span></span> |<span data-ttu-id="68a34-640">상태 정보에 대한 자세한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-640">Detailed information about health status.</span></span> |

<span data-ttu-id="68a34-641">경우 hello **상태** 값이 **확인**, hello 지침에 따라 [Azure 모니터링 인프라 구성에 대 한 상태 검사] [ deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="68a34-641">If hello **Health status** value is not **OK**, follow hello instructions in [Health check for Azure monitoring infrastructure configuration][deployment-guide-5.2].</span></span>

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a><span data-ttu-id="68a34-642">Linux VM의 hello 준비 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-642">Run hello readiness check on a Linux VM</span></span>

1.  <span data-ttu-id="68a34-643">SSH를 사용 하 여 toohello Azure 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-643">Connect toohello Azure Virtual Machine by using SSH.</span></span>

2.  <span data-ttu-id="68a34-644">Hello Azure 고급 모니터링 확장의 hello 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-644">Check hello output of hello Azure Enhanced Monitoring Extension.</span></span>

  <span data-ttu-id="68a34-645">a.</span><span class="sxs-lookup"><span data-stu-id="68a34-645">a.</span></span>  <span data-ttu-id="68a34-646">`more /var/lib/AzureEnhancedMonitor/PerfCounters` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-646">Run `more /var/lib/AzureEnhancedMonitor/PerfCounters`</span></span>

   <span data-ttu-id="68a34-647">**예상 결과**: 성능 카운터 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-647">**Expected result**: Returns list of performance counters.</span></span> <span data-ttu-id="68a34-648">hello 파일은 비워둘 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-648">hello file should not be empty.</span></span>

 <span data-ttu-id="68a34-649">b.</span><span class="sxs-lookup"><span data-stu-id="68a34-649">b.</span></span> <span data-ttu-id="68a34-650">`cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-650">Run `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`</span></span>

   <span data-ttu-id="68a34-651">**예상 결과**: 여기서는 hello 오류 반환 한 줄 **none**, 예를 들어 **3; 구성 합니다. 오류 발생; 0, 0; none, 0, 1456416792, tst servercs;**</span><span class="sxs-lookup"><span data-stu-id="68a34-651">**Expected result**: Returns one line where hello error is **none**, for example, **3;config;Error;;0;0;none;0;1456416792;tst-servercs;**</span></span>

  <span data-ttu-id="68a34-652">c.</span><span class="sxs-lookup"><span data-stu-id="68a34-652">c.</span></span> <span data-ttu-id="68a34-653">`more /var/lib/AzureEnhancedMonitor/LatestErrorRecord` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-653">Run `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`</span></span>

    <span data-ttu-id="68a34-654">**예상 결과**: 빈 상태로 반환하거나 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-654">**Expected result**: Returns as empty or does not exist.</span></span>

<span data-ttu-id="68a34-655">Hello 위의 확인 하지 못한 경우, 이러한 추가 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-655">If hello preceding check was not successful, run these additional checks:</span></span>

1.  <span data-ttu-id="68a34-656">해당 hello waagent 설치 및 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-656">Make sure that hello waagent is installed and enabled.</span></span>

  <span data-ttu-id="68a34-657">a.</span><span class="sxs-lookup"><span data-stu-id="68a34-657">a.</span></span>  <span data-ttu-id="68a34-658">`sudo ls -al /var/lib/waagent/` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-658">Run `sudo ls -al /var/lib/waagent/`</span></span>

      <span data-ttu-id="68a34-659">**예상 결과**: hello waagent 디렉터리의 hello 콘텐츠를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-659">**Expected result**: Lists hello content of hello waagent directory.</span></span>

  <span data-ttu-id="68a34-660">b.</span><span class="sxs-lookup"><span data-stu-id="68a34-660">b.</span></span>  <span data-ttu-id="68a34-661">`ps -ax | grep waagent` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-661">Run `ps -ax | grep waagent`</span></span>

   <span data-ttu-id="68a34-662">**예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /usr/sbin/waagent -daemon`</span><span class="sxs-lookup"><span data-stu-id="68a34-662">**Expected result**: Displays one entry similar to: `python /usr/sbin/waagent -daemon`</span></span>

2. <span data-ttu-id="68a34-663">해당 hello Linux 진단 확장 설치 및 활성화 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="68a34-663">Make sure that hello Linux Diagnostic Extension is installed and enabled.</span></span>

  <span data-ttu-id="68a34-664">a.</span><span class="sxs-lookup"><span data-stu-id="68a34-664">a.</span></span>  <span data-ttu-id="68a34-665">`sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-665">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'`</span></span>

   <span data-ttu-id="68a34-666">**예상 결과**: hello Linux 진단 확장 디렉터리의 hello 콘텐츠를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-666">**Expected result**: Lists hello content of hello Linux Diagnostic Extension directory.</span></span>

 <span data-ttu-id="68a34-667">b.</span><span class="sxs-lookup"><span data-stu-id="68a34-667">b.</span></span> <span data-ttu-id="68a34-668">`ps -ax | grep diagnostic` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-668">Run `ps -ax | grep diagnostic`</span></span>

   <span data-ttu-id="68a34-669">**예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span><span class="sxs-lookup"><span data-stu-id="68a34-669">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`</span></span>

3.   <span data-ttu-id="68a34-670">해당 hello Azure 고급 모니터링 확장 설치 되어 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-670">Make sure that hello Azure Enhanced Monitoring Extension is installed and running.</span></span>

  <span data-ttu-id="68a34-671">a.</span><span class="sxs-lookup"><span data-stu-id="68a34-671">a.</span></span>  <span data-ttu-id="68a34-672">`sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-672">Run `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'`</span></span>

    <span data-ttu-id="68a34-673">**예상 결과**: hello Azure 고급 모니터링 확장 디렉터리의 hello 콘텐츠를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-673">**Expected result**: Lists hello content of hello Azure Enhanced Monitoring Extension directory.</span></span>

  <span data-ttu-id="68a34-674">b.</span><span class="sxs-lookup"><span data-stu-id="68a34-674">b.</span></span> <span data-ttu-id="68a34-675">`ps -ax | grep AzureEnhanced` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-675">Run `ps -ax | grep AzureEnhanced`</span></span>

     <span data-ttu-id="68a34-676">**예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span><span class="sxs-lookup"><span data-stu-id="68a34-676">**Expected result**: Displays one entry similar to: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`</span></span>

3. <span data-ttu-id="68a34-677">SAP Note에서 설명 된 대로 SAP 호스트 에이전트를 설치 [1031096]의 hello 출력을 확인 하 고 `saposcol`합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-677">Install SAP Host Agent as described in SAP Note [1031096], and check hello output of `saposcol`.</span></span>

  <span data-ttu-id="68a34-678">a.</span><span class="sxs-lookup"><span data-stu-id="68a34-678">a.</span></span>  <span data-ttu-id="68a34-679">`/usr/sap/hostctrl/exe/saposcol -d` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-679">Run `/usr/sap/hostctrl/exe/saposcol -d`</span></span>

  <span data-ttu-id="68a34-680">b.</span><span class="sxs-lookup"><span data-stu-id="68a34-680">b.</span></span>  <span data-ttu-id="68a34-681">`dump ccm` 실행</span><span class="sxs-lookup"><span data-stu-id="68a34-681">Run `dump ccm`</span></span>

  <span data-ttu-id="68a34-682">c.</span><span class="sxs-lookup"><span data-stu-id="68a34-682">c.</span></span>  <span data-ttu-id="68a34-683">확인 여부 hello **Virtualization_Configuration\Enhanced 모니터링 액세스** 메트릭은 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-683">Check whether hello **Virtualization_Configuration\Enhanced Monitoring Access** metric is **true**.</span></span>

<span data-ttu-id="68a34-684">SAP NetWeaver ABAP 응용 프로그램 서버가 이미 설치된 경우 트랜잭션 ST06을 열고 고급 모니터링이 사용하도록 설정되어 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-684">If you already have an SAP NetWeaver ABAP application server installed, open transaction ST06 and check whether enhanced monitoring is enabled.</span></span>

<span data-ttu-id="68a34-685">하나라도 이러한 검사 중 실패 하 고 tooredeploy 확장 hello 하는 방법에 대 한 자세한 내용은 참조 하는 경우 [문제 해결 SAP 용 Azure 모니터링 인프라 hello][deployment-guide-5.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-685">If any of these checks fail, and for detailed information about how tooredeploy hello extension, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="68a34-686"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Azure 모니터링 인프라 구성 hello에 대 한 상태 확인</span><span class="sxs-lookup"><span data-stu-id="68a34-686"><a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Health check for hello Azure monitoring infrastructure configuration</span></span>
<span data-ttu-id="68a34-687">Hello 테스트에 설명 된 일부 데이터를 모니터링 하는 hello 제대로 전달 되지 않으면 [SAP 용 Azure 고급 모니터링에 대 한 준비 상태 검사가][deployment-guide-5.1]실행 hello `Test-AzureRmVMAEMExtension` cmdlet toocheck 여부 hello Azure 모니터링 인프라 및 SAP에 대 한 확장을 모니터링 하는 hello 올바르게 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-687">If some of hello monitoring data is not delivered correctly as indicated by hello test described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1], run hello `Test-AzureRmVMAEMExtension` cmdlet toocheck whether hello Azure monitoring infrastructure and hello monitoring extension for SAP are configured correctly.</span></span>

1.  <span data-ttu-id="68a34-688">에 설명 된 대로 hello hello Azure PowerShell cmdlet의 최신 버전을 설치 했는지 확인 [배포 Azure PowerShell cmdlet][deployment-guide-4.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-688">Make sure that you have installed hello latest version of hello Azure PowerShell cmdlet, as described in [Deploying Azure PowerShell cmdlets][deployment-guide-4.1].</span></span>
2.  <span data-ttu-id="68a34-689">Hello 다음 PowerShell cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-689">Run hello following PowerShell cmdlet.</span></span> <span data-ttu-id="68a34-690">사용 가능한 환경 목록이 hello cmdlet를 실행 합니다. `Get-AzureRmEnvironment`합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-690">For a list of available environments, run hello cmdlet `Get-AzureRmEnvironment`.</span></span> <span data-ttu-id="68a34-691">공용, 선택 toouse hello **azure 클라우드** 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-691">toouse public Azure, select hello **AzureCloud** environment.</span></span> <span data-ttu-id="68a34-692">중국의 Azure인 경우 **AzureChinaCloud**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-692">For Azure in China, select **AzureChinaCloud**.</span></span>
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  <span data-ttu-id="68a34-693">계정 데이터를 입력 하 고 hello Azure 가상 컴퓨터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-693">Enter your account data and identify hello Azure virtual machine.</span></span>

  ![SAP 관련 Azure cmdlet Test-VMConfigForSAP_GUI의 입력 페이지][deployment-guide-figure-1200]

4. <span data-ttu-id="68a34-695">선택 hello hello 가상 컴퓨터의 테스트 hello 구성을 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-695">hello script tests hello configuration of hello virtual machine you select.</span></span>

  ![SAP 용 Azure 모니터링 인프라 hello의 성공적인 테스트 출력][deployment-guide-figure-1300]

<span data-ttu-id="68a34-697">모든 상태 검사 결과가 **OK**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-697">Make sure that every health check result is **OK**.</span></span> <span data-ttu-id="68a34-698">일부 검사 표시 되지 않는 경우 **확인**, hello 업데이트 cmdlet을 실행 하에 설명 된 대로 [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-698">If some checks do not display **OK**, run hello update cmdlet as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="68a34-699">15 분 정도 기다린 후에 설명 된 반복 hello 검사 [SAP 용 Azure 고급 모니터링에 대 한 준비 상태 검사가] [ deployment-guide-5.1] 및 [Azure 모니터링 인프라 구성상태확인] [deployment-guide-5.2].</span><span class="sxs-lookup"><span data-stu-id="68a34-699">Wait 15 minutes, and repeat hello checks described in [Readiness check for Azure Enhanced Monitoring for SAP][deployment-guide-5.1] and [Health check for Azure Monitoring Infrastructure Configuration][deployment-guide-5.2].</span></span> <span data-ttu-id="68a34-700">Hello 검사에는 여전히 일부 또는 전체 카운터에 문제가 있음을 나타낼, 참조 [문제 해결 SAP 용 Azure 모니터링 인프라 hello][deployment-guide-5.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-700">If hello checks still indicate a problem with some or all counters, see [Troubleshooting hello Azure monitoring infrastructure for SAP][deployment-guide-5.3].</span></span>

### <span data-ttu-id="68a34-701"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>SAP 용 Azure 모니터링 인프라 hello 문제 해결</span><span class="sxs-lookup"><span data-stu-id="68a34-701"><a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Troubleshooting hello Azure monitoring infrastructure for SAP</span></span>

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] <span data-ttu-id="68a34-703">Azure 성능 카운터가 전혀 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-703">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="68a34-704">hello AzureEnhancedMonitoring Windows 서비스를 Azure의 성능 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-704">hello AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="68a34-705">Hello 서비스를 올바르게 설치 되지 않은 경우 또는 VM에서 실행 되지 않는 경우 없음 성능 메트릭을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-705">If hello service has not been installed correctly or if it is not running in your VM, no performance metrics can be collected.</span></span>

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="68a34-706">hello Azure 고급 모니터링 확장의 설치 디렉터리 hello 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-706">hello installation directory of hello Azure Enhanced Monitoring Extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="68a34-707">문제</span><span class="sxs-lookup"><span data-stu-id="68a34-707">Issue</span></span>
<span data-ttu-id="68a34-708">hello 설치 디렉터리: c:\\패키지\\플러그 인\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;버전 >\\놓기 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-708">hello installation directory C:\\Packages\\Plugins\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;version>\\drop is empty.</span></span>

###### <a name="solution"></a><span data-ttu-id="68a34-709">해결 방법</span><span class="sxs-lookup"><span data-stu-id="68a34-709">Solution</span></span>
<span data-ttu-id="68a34-710">hello 확장이 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-710">hello extension is not installed.</span></span> <span data-ttu-id="68a34-711">(앞에서 설명한) 프록시 문제인지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-711">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="68a34-712">Toorestart hello 컴퓨터나 hello를 다시 실행된 해야 `Set-AzureRmVMAEMExtension` 구성 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-712">You might need toorestart hello machine or rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a><span data-ttu-id="68a34-713">Azure 고급 모니터링 서비스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-713">Service for Azure Enhanced Monitoring does not exist</span></span>

###### <a name="issue"></a><span data-ttu-id="68a34-714">문제</span><span class="sxs-lookup"><span data-stu-id="68a34-714">Issue</span></span>
<span data-ttu-id="68a34-715">hello AzureEnhancedMonitoring Windows 서비스가 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-715">hello AzureEnhancedMonitoring Windows service does not exist.</span></span>

<span data-ttu-id="68a34-716">Azperflib.exe 출력에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-716">Azperflib.exe output throws an error:</span></span>

<span data-ttu-id="68a34-717">![Azperflib.exe의 실행 SAP 용 Azure 고급 모니터링 확장 hello의 hello 서비스가 실행 되지 않습니다 나타냅니다.][deployment-guide-figure-1400]
<a name="figure-14"></a></span><span class="sxs-lookup"><span data-stu-id="68a34-717">![Execution of azperflib.exe indicates that hello service of hello Azure Enhanced Monitoring Extension for SAP is not running][deployment-guide-figure-1400]
<a name="figure-14"></a></span></span>

###### <a name="solution"></a><span data-ttu-id="68a34-718">해결 방법</span><span class="sxs-lookup"><span data-stu-id="68a34-718">Solution</span></span>
<span data-ttu-id="68a34-719">Hello 서비스가 없는 경우 Azure 고급 모니터링 확장의 SAP 용 hello 올바르게 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-719">If hello service does not exist, hello Azure Enhanced Monitoring Extension for SAP has not been installed correctly.</span></span> <span data-ttu-id="68a34-720">배포 시나리오에 대 한 설명 하는 hello 단계를 사용 하 여 hello 확장을 다시 배포 [Azure의 SAP 용 Vm 배포 시나리오][deployment-guide-3]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-720">Redeploy hello extension by using hello steps described for your deployment scenario in [Deployment scenarios of VMs for SAP in Azure][deployment-guide-3].</span></span>

<span data-ttu-id="68a34-721">Hello Azure 성능 카운터가 hello Azure VM에서에서 제공 되는지 여부를 1 시간 후 hello 확장 프로그램을 배포한 후 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-721">After you deploy hello extension, after one hour, check again whether hello Azure performance counters are provided in hello Azure VM.</span></span>

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a><span data-ttu-id="68a34-722">Azure 고급 모니터링 서비스가 존재 하지만 toostart 실패</span><span class="sxs-lookup"><span data-stu-id="68a34-722">Service for Azure Enhanced Monitoring exists, but fails toostart</span></span>

###### <a name="issue"></a><span data-ttu-id="68a34-723">문제</span><span class="sxs-lookup"><span data-stu-id="68a34-723">Issue</span></span>
<span data-ttu-id="68a34-724">hello AzureEnhancedMonitoring Windows 서비스 및를 사용 하는 있지만 toostart 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-724">hello AzureEnhancedMonitoring Windows service exists and is enabled, but fails toostart.</span></span> <span data-ttu-id="68a34-725">자세한 내용은 hello 응용 프로그램 이벤트 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-725">For more information, check hello application event log.</span></span>

###### <a name="solution"></a><span data-ttu-id="68a34-726">해결 방법</span><span class="sxs-lookup"><span data-stu-id="68a34-726">Solution</span></span>
<span data-ttu-id="68a34-727">hello 구성이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-727">hello configuration is incorrect.</span></span> <span data-ttu-id="68a34-728">에 설명 된 대로 VM hello에 대 한 확장을 모니터링 하는 hello를 다시 시작 [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-728">Restart hello monitoring extension for hello VM, as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span>

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] <span data-ttu-id="68a34-730">일부 Azure 성능 카운터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-730">Some Azure performance counters are missing</span></span>
<span data-ttu-id="68a34-731">hello AzureEnhancedMonitoring Windows 서비스를 Azure의 성능 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-731">hello AzureEnhancedMonitoring Windows service collects performance metrics in Azure.</span></span> <span data-ttu-id="68a34-732">hello 서비스는 여러 원본에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-732">hello service gets data from several sources.</span></span> <span data-ttu-id="68a34-733">일부 구성 데이터는 로컬로 수집되고 일부 성능 메트릭은 Azure 진단에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-733">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="68a34-734">저장소 카운터는 사용자가 로그온 hello 저장소 구독 수준에서에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-734">Storage counters are used from your logging on hello storage subscription level.</span></span>

<span data-ttu-id="68a34-735">SAP Note를 사용 하 여 문제를 해결 하는 경우 [1999351] hello 문제 해결, hello를 다시 실행 하지 않는 `Set-AzureRmVMAEMExtension` 구성 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-735">If troubleshooting by using SAP Note [1999351] doesn't resolve hello issue, rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span> <span data-ttu-id="68a34-736">설정 된 후에 즉시 저장소 분석 또는 진단 카운터를 만들 수 수 없으므로 toowait 한 시간을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-736">You might have toowait an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="68a34-737">Hello 문제가 계속 되 면 hello Windows에 대 한 구성 요소 OP NT AZR BC 또는 BC-OP-LNX-AZR Linux 가상 컴퓨터에 SAP 고객 지원 메시지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-737">If hello problem persists, open an SAP customer support message on hello component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] <span data-ttu-id="68a34-739">Azure 성능 카운터가 전혀 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-739">Azure performance counters do not show up at all</span></span>
<span data-ttu-id="68a34-740">Azure의 성능 메트릭은 데몬에 의해 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-740">Performance metrics in Azure are collected by a daemon.</span></span> <span data-ttu-id="68a34-741">Hello 디먼이 실행 되지 않는 경우 없음 성능 메트릭을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-741">If hello daemon is not running, no performance metrics can be collected.</span></span>

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a><span data-ttu-id="68a34-742">hello Azure 고급 모니터링 확장의 설치 디렉터리 hello 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-742">hello installation directory of hello Azure Enhanced Monitoring extension is empty</span></span>

###### <a name="issue"></a><span data-ttu-id="68a34-743">문제</span><span class="sxs-lookup"><span data-stu-id="68a34-743">Issue</span></span>
<span data-ttu-id="68a34-744">hello 디렉터리 \\var\\lib\\waagent\\ hello Azure 고급 모니터링 확장에 대 한 하위 디렉터리는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-744">hello directory \\var\\lib\\waagent\\ does not have a subdirectory for hello Azure Enhanced Monitoring extension.</span></span>

###### <a name="solution"></a><span data-ttu-id="68a34-745">해결 방법</span><span class="sxs-lookup"><span data-stu-id="68a34-745">Solution</span></span>
<span data-ttu-id="68a34-746">hello 확장이 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-746">hello extension is not installed.</span></span> <span data-ttu-id="68a34-747">(앞에서 설명한) 프록시 문제인지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-747">Determine whether this is a proxy issue (as described earlier).</span></span> <span data-ttu-id="68a34-748">Toorestart hello 컴퓨터 및/또는 다시 실행된 hello 해야 `Set-AzureRmVMAEMExtension` 구성 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-748">You might need toorestart hello machine and/or rerun hello `Set-AzureRmVMAEMExtension` configuration script.</span></span>

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] <span data-ttu-id="68a34-750">일부 Azure 성능 카운터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-750">Some Azure performance counters are missing</span></span>
<span data-ttu-id="68a34-751">Azure에서 성능 메트릭은 여러 원본에서 데이터를 가져오는 데몬에 의해 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-751">Performance metrics in Azure are collected by a daemon, which gets data from several sources.</span></span> <span data-ttu-id="68a34-752">일부 구성 데이터는 로컬로 수집되고 일부 성능 메트릭은 Azure 진단에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-752">Some configuration data is collected locally, and some performance metrics are read from Azure Diagnostics.</span></span> <span data-ttu-id="68a34-753">저장소 카운터 저장소 구독에서 hello 로그에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-753">Storage counters come from hello logs in your storage subscription.</span></span>

<span data-ttu-id="68a34-754">알려진 문제의 전체 최신 목록은 SAP용 고급 Azure 모니터링에 대한 추가 문제 해결 정보를 포함하고 있는 SAP Note [1999351]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68a34-754">For a complete and up-to-date list of known issues, see SAP Note [1999351], which has additional troubleshooting information for Enhanced Azure Monitoring for SAP.</span></span>

<span data-ttu-id="68a34-755">SAP Note를 사용 하 여 문제를 해결 하는 경우 [1999351] hello 문제를 해결, hello를 다시 실행 하지 않는 `Set-AzureRmVMAEMExtension` 구성 스크립트에 설명 된 대로 [구성 hello Azure 고급 모니터링 확장SAP용][deployment-guide-4.5].</span><span class="sxs-lookup"><span data-stu-id="68a34-755">If troubleshooting by using SAP Note [1999351] does not resolve hello issue, rerun hello `Set-AzureRmVMAEMExtension` configuration script as described in [Configure hello Azure Enhanced Monitoring Extension for SAP][deployment-guide-4.5].</span></span> <span data-ttu-id="68a34-756">설정 된 후에 즉시 저장소 분석 또는 진단 카운터를 만들 수 수 없으므로 한 시간에 대 한 toowait를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-756">You might have toowait for an hour because storage analytics or diagnostics counters might not be created immediately after they are enabled.</span></span> <span data-ttu-id="68a34-757">Hello 문제가 계속 되 면 hello Windows에 대 한 구성 요소 OP NT AZR BC 또는 BC-OP-LNX-AZR Linux 가상 컴퓨터에 SAP 고객 지원 메시지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68a34-757">If hello problem persists, open an SAP customer support message on hello component BC-OP-NT-AZR for Windows or BC-OP-LNX-AZR for a Linux virtual machine.</span></span>
