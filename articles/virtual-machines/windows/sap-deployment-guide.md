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
# <a name="deploy-sap-on-windows-vms-in-azure"></a>Azure의 Windows VM에서 SAP 배포
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

Azure 가상 컴퓨터에는 최소한의 시간 및 긴 조달 주기 하지 않고 계산 및 저장소 리소스를 필요로 하는 조직 위한 hello 솔루션입니다. Azure에서 Azure 가상 컴퓨터 toodeploy 고전 같은 응용 프로그램, SAP NetWeaver 기반 응용 프로그램을 사용할 수 있습니다. 추가 온-프레미스 리소스 없이도 응용 프로그램의 안정성과 가용성을 확장할 수 있습니다. Azure Virtual Machines는 크로스-프레미스 연결을 지원하므로 Azure Virtual Machines를 조직의 온-프레미스 도메인, 사설 클라우드 및 SAP 시스템 지형에 통합할 수 있습니다.

이 문서에서는 hello 단계 toodeploy SAP 응용 프로그램 Windows Azure의 가상 컴퓨터 (Vm)에서 다룹니다. 이 문서에 hello 정보에 빌드 [Azure 가상 컴퓨터 계획 및 구현 Windows에서의 SAP 용][planning-guide]합니다. 또한 SAP 설치 설명서 및 설치 하 고 SAP 소프트웨어 배포에 대 한 기본 리소스 hello SAP Note를 보완 합니다.

## <a name="prerequisites"></a>필수 조건
SAP 소프트웨어 배포를 위해 Azure 가상 컴퓨터를 설정하려면 여러 단계와 리소스가 필요합니다. 시작 하기 전에 Azure에서 Windows 가상 컴퓨터에 SAP 소프트웨어를 설치 하기 위한 hello 필수 구성 요소를 충족 하는지 확인 합니다.

### <a name="local-computer"></a>수집
Windows 또는 Linux Vm toomanage, PowerShell 스크립트를 hello Azure 포털을 사용할 수 있습니다. 두 가지 도구 모두 Windows 7 또는 이후 버전의 Windows 실행하는 로컬 컴퓨터가 필요합니다. Linux Vm을 toouse Linux 컴퓨터에이 작업을 하려면만 toomanage 하려는 경우 Azure CLI를 사용할 수 있습니다.

### <a name="internet-connection"></a>인터넷 연결
여야 toodownload 및 실행된 hello 도구 및 SAP 소프트웨어 배포에 필요한 스크립트를 toohello 인터넷에 연결 합니다. hello Azure 고급 모니터링 확장의 SAP 용 hello를 실행 하는 Azure VM 인터넷 액세스 toohello를도 필요 합니다. Hello Azure VM에 Azure 가상 네트워크 또는 온-프레미스 도메인의 일부 이면 확인 hello 관련 프록시 설정을 설정 되어 있는지에 설명 된 대로 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.

### <a name="microsoft-azure-subscription"></a>Microsoft Azure 구독
활성 Azure 계정이 필요합니다.

### <a name="topology-and-networking"></a>토폴로지 및 네트워킹
Hello Azure에서 SAP 배포의 toodefine hello 토폴로지 및 아키텍처가 필요합니다.

* Azure 저장소 계정 toobe 사용
* 가상 네트워크를 toodeploy hello SAP 시스템
* 리소스 그룹 toowhich toodeploy hello SAP 시스템
* Toodeploy hello SAP 시스템을 원하는 azure 지역
* SAP 구성(2계층 또는 3계층)
* VM 크기 및 추가 가상 하드 디스크 (Vhd) toobe hello 개수의 toohello Vm 탑재
* SAP 수정과 전송 시스템(CTS) 구성

만들고 hello SAP 소프트웨어 배포 프로세스를 시작 하기 전에 Azure 저장소 계정 또는 Azure 가상 네트워크를 구성 합니다. 방법에 대 한 내용은 toocreate 이러한 리소스를 구성 하 고, 참조 [Azure 가상 컴퓨터 계획 및 구현 Windows에서의 SAP 용][planning-guide]합니다.

### <a name="sap-sizing"></a>SAP 크기 조정
Hello 다음 SAP 크기 조정에 대 한 정보를 알고:

* 예를 들어 hello SAP 빠른 조절기 도구 및 hello SAP 응용 프로그램 성능 표준 (SAPS) 번호를 사용 하 여 SAP 작업 부하를 프로젝션
* Hello SAP 시스템의 필요한 CPU 리소스 및 메모리 사용
* 필요한 초당 입력/출력(I/O) 작업 수
* Azure에서 서로 다른 VM 간의 결과적 통신에 필요한 네트워크 대역폭
* 온-프레미스 자산과 Azure 배포 SAP 시스템 hello 간에 필요한 네트워크 대역폭

### <a name="resource-groups"></a>리소스 그룹
Azure 리소스 관리자를 사용할 수 있습니다 리소스 그룹 toomanage hello 응용 프로그램 리소스를 모두 Azure 구독에서. 자세한 내용은 [Azure Resource Manager 개요][resource-group-overview]를 참조하세요.

## <a name="resources"></a>리소스

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP 리소스
SAP 소프트웨어 배포를 설정 하는 경우 다음 SAP 리소스 hello가 필요 합니다.

* SAP Note [1928533], 다음 항목을 포함합니다.
  * Hello SAP 소프트웨어 배포에 지원 되는 Azure VM 크기의 목록
  * Azure VM 크기에 대한 중요한 용량 정보
  * 지원되는 SAP 소프트웨어 및 운영 체제(OS)와 데이터베이스 조합
  * Microsoft Azure에서 Windows 및 Linux에 필요한 SAP 커널 버전

* SAP Note [2015553]는 Azure에서 SAP을 지원하는 SAP 소프트웨어 배포에 대한 필수 구성 요소를 나열합니다.
* SAP Note [2178632]는 Azure에서 SAP에 대해 보고된 모든 모니터링 메트릭에 대한 자세한 정보를 포함하고 있습니다.
* SAP Note [1409604] hello 필요한 SAP 호스트 에이전트 버전 Azure에서 Windows에 대 한 합니다.
* SAP Note [2191498] hello 필요한 SAP 호스트 에이전트 버전 Azure에서 Linux에 대 한 합니다.
* SAP Note [2243692]는 Azure에서 Linux의 SAP 라이선스에 대한 정보를 포함하고 있습니다.
* SAP Note [1984787]은 SUSE LINUX Enterprise Server 12에 대한 일반 정보를 포함하고 있습니다.
* SAP Note [2002167]는 Red Hat Enterprise Linux 7.x에 대한 일반 정보를 포함하고 있습니다.
* SAP Note [1999351] Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 추가 문제 해결 정보입니다.
* [SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes)는 Linux에 필요한 모든 SAP Note를 포함하고 있습니다.
* [Azure PowerShell][azure-ps]에 포함된 SAP 관련 PowerShell cmdlet입니다.
* [Azure CLI][azure-cli]에 포함된 SAP 관련 Azure CLI 명령입니다.

[comment]: <> (MSSedusch TODO - SAP Note 1409604에 SAP 호스트 에이전트용 ARM 패치 수준 추가)

### <a name="microsoft-resources"></a>Microsoft 리소스
다음 Microsoft 문서에서는 Azure에서 SAP 배포에 대해 설명합니다.

* [Windows에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]
* [Windows에서 SAP용 Azure Virtual Machines 배포(이 문서)][deployment-guide]
* [Windows에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]
* [Azure Portal][azure-portal]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Azure VM에서 SAP 소프트웨어에 대한 배포 시나리오
Azure에서 VM 및 연결된 디스크를 배포하기 위한 여러 옵션이 있습니다. 되므로 중요 toounderstand hello 차이점 배포 옵션 다른 단계가 tooprepare hello 배포 유형을 선택 하면에 따른 배포에 대 한 Vm을 걸릴 수 있습니다.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>시나리오 1: hello SAP 용 Azure Marketplace에서에서 VM 배포
Microsoft에서 제공 하는 이미지를 사용 하거나으로 제 3 자 hello Azure 마켓플레이스 toodeploy에서 VM 수 있습니다. hello 마켓플레이스는 Windows Server와 다른 Linux 배포판의 표준 OS 이미지 일부를 제공합니다. 또한 데이터베이스 관리 시스템(DMBS) SKU, 예를 들어 Microsoft SQL Server를 포함하고 있는 이미지를 배포할 수도 있습니다. DBMS SKU가 포함된 이미지 사용에 관한 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]를 참조하세요.

hello 다음 순서도 hello SAP 관련 Azure 마켓플레이스 hello에서 VM을 배포 하기 위한 단계를 순서 대로

![hello Azure Marketplace에서에서 VM 이미지를 사용 하 여 SAP 시스템에 대 한 VM 배포 순서도][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 가상 컴퓨터 만들기
hello 가장 쉬운 방법은 toocreate hello Azure Marketplace에서에서 이미지가 있는 새 가상 컴퓨터를 hello Azure 포털을 사용 하는 것입니다.

1.  너무 이동<https://portal.azure.com/#create>합니다.  Hello Azure 포털 메뉴에서에서 선택 하거나 **+ 새로 만들기**합니다.
2.  선택 **계산**, 한 다음 운영 체제 toodeploy 원하는의 hello 유형을 선택 합니다. 예를 들어, Windows Server 2012 R2, SUSE Linux Enterprise Server 12(SLES 12) 또는 Red Hat Enterprise Linux 7.2(RHEL 7.2)입니다. hello 기본 목록 보기는 지원 되는 모든 운영 체제를 표시 하지 않습니다. 전체 목록을 보려면 **모두 보기**를 선택합니다. SAP 소프트웨어 배포를 위한 지원되는 운영 체제에 대한 자세한 내용은 SAP Note [1928533]을 참조하세요.
3.  Hello 다음 페이지에서 약관을 검토 합니다.
4.  Hello에 **배포 모델 선택** 상자 **리소스 관리자**합니다.
5.  **만들기**를 선택합니다.

tooall에서 네트워크 인터페이스 및 저장소 계정과 같은 리소스를 필요로 하는 또한을 hello 마법사를 통해 필요한 hello 매개 변수 toocreate hello 가상 컴퓨터를 설정 합니다. 다음은 일부 매개 변수입니다.

1. **기본 사항**:
  * **이름**: hello 리소스 (hello 가상 컴퓨터 이름)의 hello 이름입니다.
 * **사용자 이름 및 암호** 또는 **SSH 공개 키**: hello 이름과 hello를 프로 비전 하는 동안 만들어진 hello 사용자의 암호를 입력 합니다. Linux 가상 컴퓨터에 대 한 toosign toohello 컴퓨터에서 사용 하는 hello 공용 SSH (보안 셸) 키를 입력할 수 있습니다.
 * **구독**: toouse tooprovision hello 새 가상 컴퓨터를 원하는 hello 구독을 선택 합니다.
 * **리소스 그룹**: hello VM에 대 한 hello 리소스 그룹의 hello 이름입니다. 새 리소스 그룹 또는 hello 이름 이미 있는 리소스 그룹의의 hello 이름 중 하나를 입력할 수 있습니다.
 * **위치**: 여기서 toodeploy hello 새 가상 컴퓨터. Tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크를 사용 하도록 하려는 경우 Azure tooyour 온-프레미스 네트워크를 연결 하는 hello 가상 네트워크의 hello 위치를 선택 했는지 확인 합니다. 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]의 [Microsoft Azure 네트워킹][planning-guide-microsoft-azure-networking]을 참조하세요.
2. **크기**:

     지원되는 VM 유형 목록은 SAP Note [1928533]을 참조하세요. Azure 프리미엄 저장소 toouse를 하려는 경우 hello 올바른 VM 유형을 선택 해야 합니다. 모든 VM 유형이 Premium Storage를 지원하지는 않습니다. 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]의 [Storage: Microsoft Azure Storage 및 데이터 링크][planning-guide-storage-microsoft-azure-storage-and-data-disks] 및 [Azure Premium Storage][planning-guide-azure-premium-storage]를 참조하세요.

3. **설정**:
   * **저장소 계정**: 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다. 모든 저장소 유형이 SAP 응용 프로그램 실행을 위해 작동하지는 않습니다. 저장소 유형에 대한 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]를 참조하세요.
   * **가상 네트워크** 및 **서브넷**: 인트라넷에 연결 된 tooyour 온-프레미스 네트워크를 가상 네트워크를 선택 hello와 toointegrate hello 가상 컴퓨터.
   * **공용 IP 주소**: hello 공용 IP 주소 매개 변수 toocreate 새 공용 IP 주소를 입력 하거나 toouse, 원하는 선택 합니다. Hello 인터넷을 통해 공용 IP 주소 tooaccess 가상 컴퓨터를 사용할 수 있습니다. 네트워크 보안 그룹 toohelp 보안 액세스 tooyour 가상 컴퓨터를 만들 수도 있는지 확인 합니다.
   * **네트워크 보안 그룹**: 자세한 내용은 [네트워크 보안 그룹으로 네트워크 트래픽 흐름 제어][virtual-networks-nsg]를 참조하세요.
   * **가용성**: 가용성 집합을 선택 하거나 입력 hello 매개 변수 toocreate 새 가용성 집합입니다. 자세한 내용은 [Azure 가용성 집합][planning-guide-3.2.3]을 참조하세요.
   * **모니터링**: 진단 모니터링에 대해 **사용 중지**를 선택할 수 있습니다. 그가 자동으로 설정 hello 명령을 tooenable hello Azure 고급 모니터링 확장을 실행 하는 경우에 설명 된 대로 [구성 모니터링][deployment-guide-configure-monitoring-scenario-1]합니다.

4. **요약**:

  선택 내용을 검토한 다음 **확인**을 선택합니다.

가상 컴퓨터가 선택한 hello 리소스 그룹에 배포 됩니다.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>템플릿을 사용하여 가상 컴퓨터 만들기
Hello에 게시 하는 hello SAP 템플릿 중 하나를 사용 하 여 가상 컴퓨터를 만들 수 [azure-빠른 시작-템플릿 GitHub 리포지토리][azure-quickstart-templates-github]합니다. 또한 수동으로 만들려면 가상 컴퓨터 hello를 사용 하 여 [Azure 포털][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], 또는 [Azure CLI ][virtual-machines-linux-tutorial].

* [**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image]

  하나의 가상 컴퓨터를 사용 하 여 2 계층 시스템 toocreate이이 템플릿을 사용 합니다.
* [**3계층 구성(여러 가상 컴퓨터) 템플릿**(sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image]

  여러 가상 컴퓨터를 사용 하 여 3 계층 시스템 toocreate이이 템플릿을 사용 합니다.

Azure 포털 hello hello 서식 파일에 대 한 매개 변수 뒤 hello를 입력 합니다.

1. **기본 사항**:
  * **구독**: hello 구독 toouse toodeploy hello 템플릿.
  * **리소스 그룹**: hello 리소스 그룹 toouse toodeploy hello 템플릿. 새 리소스 그룹을 만들거나 hello 구독에 기존 리소스 그룹을 선택할 수 있습니다.
  * **위치**: 여기서 toodeploy hello 서식 파일입니다. 기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 hello 위치가 사용 됩니다.

2. **설정**:
  * **SAP 시스템 ID**: hello SAP 시스템 ID (SID)입니다.
  * **OS 유형**: 운영 체제 toodeploy, 예를 들어, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), 또는 Red Hat Enterprise Linux (RHEL 7.2) 7.2 hello 합니다.

    hello 기본 목록 보기는 지원 되는 모든 운영 체제를 표시 하지 않습니다. 전체 목록을 보려면 **모두 보기**를 선택합니다. SAP 소프트웨어 배포를 위한 지원되는 운영 체제에 대한 자세한 내용은 SAP Note [1928533]을 참조하세요.
  * **SAP 시스템 크기**: hello hello SAP 시스템의 크기입니다.

    hello 수 SAPS hello 새로운 시스템 제공합니다. 개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.
  * **시스템 가용성** (3 계층 템플릿에만 해당): 시스템 가용성 hello 합니다.

    고가용성 설치에 적합한 구성의 경우 **HA**를 선택합니다. 두 데이터베이스 서버와 ABAP SAP 중앙 서비스(ASCS)에 대한 두 서버가 만들어집니다.
  * **저장소 유형** (2 계층 템플릿에만 해당): 저장소 toouse 유형의 hello 합니다.

    더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다. 저장소 유형에 대한 자세한 내용은 다음 리소스를 참조하세요.
      * [SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]
      * [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]
      * [Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]
      * [Azure 저장소 소개 tooMicrosoft][storage-introduction]
  * **관리 사용자 이름** 및 **관리 암호**: 사용자 이름 및 암호입니다.
    로그인 toohello 가상 컴퓨터에 사용할 새 사용자가 만들어집니다.
  * **새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다. 가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.
  * **서브넷 ID**: hello 서브넷 hello 가상 컴퓨터의 hello ID에 연결 됩니다. 가상 사설망 (VPN) 또는 Azure ExpressRoute 가상 네트워크 toouse tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다. hello ID 일반적으로 다음과 같은: /subscriptions/&lt;구독 id > /resourceGroups/&lt;리소스 그룹 이름 > /providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름 > /subnets/&lt;서브넷 이름 >

3. **사용 약관**:  
    검토 하 고 hello 약관에 동의 합니다.

4.  **구매**를 선택합니다.

hello Azure VM 에이전트는 hello Azure Marketplace에서에서 이미지를 사용 하는 경우 기본적으로 배포 됩니다.

#### <a name="configure-proxy-settings"></a>프록시 설정 구성
온-프레미스 네트워크 구성 방법에 따라 VM에 tooset hello 프록시를 할 수 있습니다. 연결 된 tooyour 온-프레미스 네트워크 VPN 또는 express 경로 통해 VM을 사용 하는 경우 hello VM 수 있습니다 수 tooaccess hello 인터넷 및 않습니다 수 toodownload hello 필요한 확장 수 또는 수 모니터링 데이터를 수집. 자세한 내용은 참조 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.

#### <a name="join-a-domain-windows-only"></a>도메인 가입(Windows에만 해당)
Azure 배포는 Azure 사이트 간 VPN 연결 또는 express 경로 통해 연결 된 tooan 온-프레미스 Active Directory 또는 DNS 인스턴스인 경우 (이 라고 *크로스-프레미스* 에 [Azure 가상 컴퓨터 계획 및 Linux에서의 SAP 용 구현][planning-guide]), 해당 hello VM는 온-프레미스 도메인에 가입 하는 것으로 예상 합니다. 이 작업에 대 한 고려 사항에 대 한 자세한 내용은 참조 [(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입][deployment-guide-4.3]합니다.

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>모니터링 구성
사용자 환경에 설명 된 대로 SAP 용 Azure 모니터링 확장 hello 설정 SAP를 지원 하는지 toobe [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다. SAP 모니터링 및에 나열 된 hello 리소스에서 SAP 커널 및 SAP 호스트 에이전트의 최소 필수 버전에 대 한 hello 필수 구성 요소 확인 [SAP 리소스][deployment-guide-2.2]합니다.

#### <a name="monitoring-check"></a>모니터링 확인
[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.

#### <a name="post-deployment-steps"></a>배포 후 단계
만든 후 배포 하는 hello VM 및 VM hello, hello VM에서에서 tooinstall hello 필요한 소프트웨어 구성 요소가 필요 합니다. 이 유형의 VM 배포에 배포/소프트웨어 설치 시퀀스 hello 때문에 hello 소프트웨어 toobe 설치 하거나 Azure에 연결할 수 있는 디스크 또는 다른 VM에서 사용할 수 이미 있어야 합니다. 또는 제공할지 크로스-프레미스 시나리오는 연결의 toohello 온-프레미스 자산 (공유 설치)를 사용 하는 것이 좋습니다.

다음과 같은 hello Azure에서 VM을 배포한 후 온-프레미스 환경에서 사용 하는 때 VM에서 지침 및 도구 tooinstall hello SAP 소프트웨어. 또는 모든 hello 파일 서버로 작동 하는 Azure VM을 만드는 tooinstall Azure VM에서 SAP 소프트웨어를 모두 SAP 및 Microsoft 업로드 Azure Vhd에 hello SAP 설치 미디어를 저장 하는 것이 좋습니다 SAP 설치 미디어가 필요 합니다.

[comment]: <> (필요한 이유가 무엇입니까 toorecommend 파일 관리, 예를 들어 MSSedusch TODO, 파일 서버 또는 VHD? 온-프레미스에서와 차이가 있나요?)

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>시나리오 2: SAP용 사용자 지정 이미지를 사용하여 VM 배포
서로 다른 버전의 운영 체제 또는 DBMS의 서로 다른 패치 요구 사항 때문에 hello Azure Marketplace에서에서 찾을 hello 이미지 요구를 충족 하지 수도 있습니다. 대신 나중에 다시 배포할 수 있는 사용자 고유의 OS/DBMS VM 이미지를 사용 하 여 toocreate VM을 할 수 있습니다.
Linux 용 다른 단계가 toocreate 개인 이미지를 사용 하 여 Windows 용 toocreate 하나 보다 합니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> 여러 가상 컴퓨터, Windows 설정 (예: Windows SID 및 호스트 이름) hello 추상화 이거나 일반화 toodeploy hello에 사용할 수 있는 Windows 이미지 tooprepare 온-프레미스 VM입니다. 사용할 수 있습니다 [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo이 있습니다.
>
> ![Linux][Logo_Linux] Linux
>
> Linux 이미지를 사용할 수 있는 toodeploy 여러 가상 컴퓨터를 tooprepare 일부 Linux 설정이 해야 추상화 된 또는에 일반화 된 hello 온-프레미스 VM입니다. 사용할 수 있습니다 `waagent -deprovision` toodo이 있습니다. 자세한 내용은 참조 [Azure에서 실행 중인 Linux 가상 컴퓨터를 캡처] [ virtual-machines-linux-capture-image] 및 hello [Azure Linux 에이전트 사용자 가이드][virtual-machines-linux-agent-user-guide-command-line-options]합니다.
>
>

- - -
준비 및 사용자 지정 이미지 만들기 및 toocreate 사용 여러 새 Vm입니다. 이 방법을 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide]에서 설명합니다. SAP Software Provisioning Manager tooinstall 새 SAP 시스템을 사용 하 여 데이터베이스의 설정 내용 (연결 된 toohello 가상 컴퓨터가 VHD에서 데이터베이스 백업을 복원) 또는 직접 하는 경우 Azure 저장소에서 데이터베이스 백업을 복원 하 여 DBMS 지원합니다. 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]를 참조하세요. 이미 온-프레미스 VM (특히 2 계층 시스템) 용에 SAP 시스템을 설치한 경우 조정할 수 있습니다 hello SAP 시스템 설정을 hello Azure VM의 hello 배포 후 SAP 소프트웨어 구축에서 지 원하는 hello 이름 바꾸기 절차를 사용 하 여 관리자 (SAP Note [1619720]). 그렇지 않으면 hello Azure VM을 배포한 후 hello SAP 소프트웨어를 설치할 수 있습니다.

hello 다음 순서도 hello SAP 관련 사용자 지정 이미지에서 VM을 배포 하기 위한 단계를 순서 대로

![개인 Marketplace에서 VM 이미지를 사용하여 SAP 시스템용 VM 배포 순서도][deployment-guide-figure-300]

#### <a name="create-hello-virtual-machine"></a>Hello 가상 컴퓨터 만들기
hello Azure 포털에서에서 개인 OS 이미지를 사용 하 여 배포 toocreate hello SAP 서식 파일을 다음 중 하나를 사용 합니다. 이러한 템플릿은 hello에 게시 된 [azure-빠른 시작-템플릿 GitHub 리포지토리][azure-quickstart-templates-github]합니다. 또한 [PowerShell][virtual-machines-upload-image-windows-resource-manager]을 사용하여 가상 컴퓨터를 수동으로 만들 수도 있습니다.

* [**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-user-image)][sap-templates-2-tier-user-image]

  하나의 가상 컴퓨터를 사용 하 여 2 계층 시스템 toocreate이이 템플릿을 사용 합니다.
* [**3계층 구성(여러 가상 컴퓨터) 템플릿**(sap-3-tier-user-image)][sap-templates-3-tier-user-image]

  여러 가상 컴퓨터 또는 운영 체제 이미지를 직접 사용 하 여 3 계층 시스템 toocreate이이 템플릿을 사용 합니다.

Azure 포털 hello hello 서식 파일에 대 한 매개 변수 뒤 hello를 입력 합니다.

1. **기본 사항**:
  * **구독**: hello 구독 toouse toodeploy hello 템플릿.
  * **리소스 그룹**: hello 리소스 그룹 toouse toodeploy hello 템플릿. Hello 구독에 기존 리소스 그룹을 선택 하거나 새 리소스 그룹을 만들 수 있습니다.
  * **위치**: 여기서 toodeploy hello 서식 파일입니다. 기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 hello 위치가 사용 됩니다.
2. **설정**:
  * **SAP 시스템 ID**: hello SAP 시스템 id입니다.
  * **OS 유형**: hello 운영 체제 유형을 toodeploy (Windows 또는 Linux)를 클릭 합니다.
  * **SAP 시스템 크기**: hello hello SAP 시스템의 크기입니다.

    hello 수 SAPS hello 새로운 시스템 제공합니다. 개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.
  * **시스템 가용성** (3 계층 템플릿에만 해당): 시스템 가용성 hello 합니다.

    고가용성 설치에 적합한 구성의 경우 **HA**를 선택합니다. ASCS용 2개의 데이터베이스 서버 및 2개의 서버가 생성됩니다.
  * **저장소 유형** (2 계층 템플릿에만 해당): 저장소 toouse 유형의 hello 합니다.

    더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다. 저장소 형식에 대 한 자세한 내용은 다음 리소스는 hello 참조:
      * [SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]
      * [Linux에서 SAP용 Azure Virtual Machines DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]
      * [Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]
      * [Azure 저장소 소개 tooMicrosoft][storage-introduction]
  * **사용자 이미지 VHD URI**: hello 개인 OS 이미지, 예를 들어 https:// VHD URI hello&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd 합니다.
  * **사용자 이미지 저장소 계정이**: hello 개인 OS 이미지가 저장 된 예를 들어 hello 저장소 계정의 hello 이름을 &lt;accountname > https://에서&lt;accountname >.blob.core.windows.net/vhds/userimage.vhd 합니다.
  * **관리자 사용자 이름** 및 **관리자 암호**: hello 사용자 이름 및 암호.

    로그인 toohello 가상 컴퓨터에 사용할 새 사용자가 만들어집니다.
  * **새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다. 가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.
  * **서브넷 ID**: hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 됩니다. VPN 또는 express 경로 가상 네트워크 toouse tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다. hello ID는 일반적으로 다음과 같이 보입니다.

    /subscriptions/&lt;구독 id>/resourceGroups/&lt;리소스 그룹 이름>/providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름>/subnets/&lt;서브넷 이름>

3. **사용 약관**:  
    검토 하 고 hello 약관에 동의 합니다.

4.  **구매**를 선택합니다.

#### <a name="install-hello-vm-agent-linux-only"></a>Hello VM 에이전트 (Linux에만 해당) 설치
toouse hello 템플릿 hello 이전 섹션에에서 설명 된 Linux 에이전트는 hello 사용자 이미지 또는 hello 배포에 이미 설치 되어 있어야 하는 hello 실패 합니다. 다운로드 하 여에 설명 된 대로 hello 사용자 이미지의 hello VM 에이전트 설치 [다운로드, 설치 및 hello Azure VM 에이전트를 사용 하도록 설정][deployment-guide-4.4]합니다. 템플릿 hello를 사용 하지 않는 경우 나중에 VM 에이전트 hello도 설치할 수 있습니다.

#### <a name="join-a-domain-windows-only"></a>도메인 가입(Windows에만 해당)
Azure 배포는 Azure 사이트 간 VPN 연결 또는 Azure ExpressRoute를 통해 연결 된 tooan 온-프레미스 Active Directory 또는 DNS 인스턴스인 경우 (이 라고 *크로스-프레미스* 에 [Azure 가상 컴퓨터 계획 및 구현 Linux에서의 SAP 용][planning-guide]), 해당 hello VM는 온-프레미스 도메인에 가입 하는 것으로 예상 합니다. 이 단계에 대 한 고려 사항에 대 한 자세한 내용은 참조 [(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입][deployment-guide-4.3]합니다.

#### <a name="configure-proxy-settings"></a>프록시 설정 구성
온-프레미스 네트워크 구성 방법에 따라 VM에 tooset hello 프록시를 할 수 있습니다. 연결 된 tooyour 온-프레미스 네트워크 VPN 또는 express 경로 통해 VM을 사용 하는 경우 hello VM 수 있습니다 수 tooaccess hello 인터넷 및 않습니다 수 toodownload hello 필요한 확장 수 또는 수 모니터링 데이터를 수집. 자세한 내용은 참조 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.

#### <a name="configure-monitoring"></a>모니터링 구성
사용자 환경에 설명 된 대로 SAP 용 Azure 모니터링 확장 hello 설정 SAP를 지원 하는지 toobe [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다. SAP 모니터링 및에 나열 된 hello 리소스에서 SAP 커널 및 SAP 호스트 에이전트의 최소 필수 버전에 대 한 hello 필수 구성 요소 확인 [SAP 리소스][deployment-guide-2.2]합니다.

#### <a name="monitoring-check"></a>모니터링 확인
[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.




### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>시나리오 3: SAP에서 일반화되지 않은 Azure VHD를 사용하여 온-프레미스 VM 이동
이 시나리오에서는 온-프레미스 환경 tooAzure에서 특정 SAP 시스템 toomove를 계획합니다. 있습니다 수 hello hello OS, SAP 바이너리 hello, VHD를 업로드 하 여이 작업을 수행할 결국 DBMS 바이너리 및 hello 데이터로 hello Vhd hello 및 로그 파일의 DBMS tooAzure hello 합니다. 에 설명 된 hello 시나리오와 달리 [시나리오 2: SAP 용 사용자 지정 이미지를 사용 하 여 VM 배포][deployment-guide-3.3],이 경우 hello 호스트 이름, SAP SID 유지 및 없기 때문에 hello Azure VM에서에서 SAP 사용자 계정 hello 온-프레미스 환경에서 구성합니다. Toogeneralize hello OS 필요가 없습니다. 이 시나리오는 가장 자주 toocross 온-프레미스 SAP 지형 hello의 일부는 온-프레미스를 실행 하 고 시나리오의 일부는 Azure에서 실행을 적용 합니다.

이 시나리오에서는 hello VM 에이전트가 설치 되지 않았습니다 자동으로 배포 중. 때문에 VM 에이전트 hello 및 hello Azure 고급 모니터링 확장의 SAP 용 toorun SAP에 필요한, 해야 toodownload, 설치 및 활성화는 모두 hello 가상 컴퓨터를 만든 후에 수동으로 구성 요소입니다.

Hello Azure VM 에이전트에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하세요.

[comment]: <> (MSSedusch TODO - 아래 Windows 링크 업데이트)

- - -
> ![Windows][Logo_Windows] Windows
>
> <http://blogs.msdn.com/b/wats/archive/2014/02/17/bginfo-guest-agent-extension-for-azure-vms.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Azure Linux 에이전트 사용자 가이드][virtual-machines-linux-agent-user-guide]
>
>

- - -

다음 순서도 hello 단계는 온-프레미스 VM 일반화 되지 않은 Azure VHD를 사용 하 여 이동에 대 한 hello 시퀀스를 나타냅니다.

![VM 디스크를 사용하여 SAP 시스템용 VM 배포 순서도][deployment-guide-figure-400]

Hello 디스크 이미 업로드 및 Azure에 정의 된 이라고 가정할 (참조 [Azure 가상 컴퓨터 계획 및 구현 Linux에서의 SAP 용][planning-guide]), hello 작업에에서 설명 된 수행 hello 다음 몇 개 섹션.

#### <a name="create-a-virtual-machine"></a>가상 컴퓨터 만들기
hello에 게시 된 hello SAP 서식 파일을 사용 하는 hello Azure 포털을 통해 개인 OS 디스크를 사용 하 여 배포 toocreate [azure-빠른 시작-템플릿 GitHub 리포지토리][azure-quickstart-templates-github]합니다. 또한 PowerShell을 사용하여 가상 컴퓨터를 직접 만들 수도 있습니다.

* [**2계층 구성(단일 가상 컴퓨터) 템플릿**(sap-2-tier-user-disk)][sap-templates-2-tier-os-disk]

  하나의 가상 컴퓨터를 사용 하 여 2 계층 시스템 toocreate이이 템플릿을 사용 합니다.

Azure 포털 hello hello 서식 파일에 대 한 매개 변수 뒤 hello를 입력 합니다.

1. **기본 사항**:
  * **구독**: hello 구독 toouse toodeploy hello 템플릿.
  * **리소스 그룹**: hello 리소스 그룹 toouse toodeploy hello 템플릿. Hello 구독에 기존 리소스 그룹을 선택 하거나 새 리소스 그룹을 만들 수 있습니다.
  * **위치**: 여기서 toodeploy hello 서식 파일입니다. 기존 리소스 그룹을 선택한 경우 해당 리소스 그룹의 hello 위치가 사용 됩니다.
2. **설정**:
  * **SAP 시스템 ID**: hello SAP 시스템 id입니다.
  * **OS 유형**: hello 운영 체제 유형을 toodeploy (Windows 또는 Linux)를 클릭 합니다.
  * **SAP 시스템 크기**: hello hello SAP 시스템의 크기입니다.

    hello 수 SAPS hello 새로운 시스템 제공합니다. 개수 SAPS hello 시스템을 사용 하려면 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.
  * **저장소 유형** (2 계층 템플릿에만 해당): 저장소 toouse 유형의 hello 합니다.

    더 큰 시스템의 경우 Azure Premium Storage를 사용하는 것이 좋습니다. 저장소 형식에 대 한 자세한 내용은 다음 리소스는 hello 참조:
      * [SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용][2367194]
      * [Linux에서 SAP용 Azure Virtual Machine DBMS 배포][dbms-guide]의 [Microsoft Azure Storage][dbms-guide-2.3]
      * [Premium Storage: Azure Virtual Machine 워크로드를 위한 고성능 저장소][storage-premium-storage-preview-portal]
      * [Azure 저장소 소개 tooMicrosoft][storage-introduction]
  * **OS 디스크 VHD URI**: hello 개인 OS 디스크의 예를 들어 https:// URI hello&lt;accountname >.blob.core.windows.net/vhds/osdisk.vhd 합니다.
  * **새로운 또는 기존 서브넷**: 새 가상 네트워크 및 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 결정합니다. 가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.
  * **서브넷 ID**: hello 서브넷 toowhich hello 가상 컴퓨터의 hello ID에 연결 됩니다. VPN 이나 Azure express 경로 가상 네트워크 toouse tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다. hello ID는 일반적으로 다음과 같이 보입니다.

    /subscriptions/&lt;구독 id>/resourceGroups/&lt;리소스 그룹 이름>/providers/Microsoft.Network/virtualNetworks/&lt;가상 네트워크 이름>/subnets/&lt;서브넷 이름>

3. **사용 약관**:  
    검토 하 고 hello 약관에 동의 합니다.

4.  **구매**를 선택합니다.

#### <a name="install-hello-vm-agent"></a>Hello VM 에이전트를 설치 합니다.
서식 파일에 설명 된 toouse hello hello 이전 섹션, hello VM 에이전트를 설치 해야 hello 운영 체제 디스크 또는 hello 배포가 실패 합니다. 다운로드 하 여에 설명 된 대로 VM hello에 hello VM 에이전트 설치 [다운로드, 설치 및 hello Azure VM 에이전트를 사용 하도록 설정][deployment-guide-4.4]합니다.

Hello 이전 섹션에에서 설명 된 대로 hello 템플릿을 사용 하지 않는 경우 나중에 hello VM 에이전트를 설치할 수도 있습니다.

#### <a name="join-a-domain-windows-only"></a>도메인 가입(Windows에만 해당)
Azure 배포는 Azure 사이트 간 VPN 연결 또는 express 경로 통해 연결 된 tooan 온-프레미스 Active Directory 또는 DNS 인스턴스인 경우 (이 라고 *크로스-프레미스* 에 [Azure 가상 컴퓨터 계획 및 Linux에서의 SAP 용 구현][planning-guide]), 해당 hello VM는 온-프레미스 도메인에 가입 하는 것으로 예상 합니다. 이 작업에 대 한 고려 사항에 대 한 자세한 내용은 참조 [(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입][deployment-guide-4.3]합니다.

#### <a name="configure-proxy-settings"></a>프록시 설정 구성
온-프레미스 네트워크 구성 방법에 따라 VM에 tooset hello 프록시를 할 수 있습니다. 연결 된 tooyour 온-프레미스 네트워크 VPN 또는 express 경로 통해 VM을 사용 하는 경우 hello VM 수 있습니다 수 tooaccess hello 인터넷 및 않습니다 수 toodownload hello 필요한 확장 수 또는 수 모니터링 데이터를 수집. 자세한 내용은 참조 [hello 프록시 구성][deployment-guide-configure-proxy]합니다.

#### <a name="configure-monitoring"></a>모니터링 구성
사용자 환경에 설명 된 대로 SAP 용 Azure 모니터링 확장 hello 설정 SAP를 지원 하는지 toobe [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다. SAP 모니터링 및에 나열 된 hello 리소스에서 SAP 커널 및 SAP 호스트 에이전트의 최소 필수 버전에 대 한 hello 필수 구성 요소 확인 [SAP 리소스][deployment-guide-2.2]합니다.

#### <a name="monitoring-check"></a>모니터링 확인
[종단 간 모니터링 설정 확인 및 문제 해결][deployment-guide-troubleshooting-chapter]에서 설명한 대로 모니터링이 작동하는지 여부를 확인합니다.

## <a name="update-hello-monitoring-configuration-for-sap"></a>SAP 용 hello 모니터링 구성 업데이트
Hello hello 다음 시나리오 중 하나에서 SAP 모니터링 구성을 업데이트 합니다.
* hello 공동 Microsoft/SAP 팀 hello 모니터링 기능을 확장 하 고 더 많거나 적은 카운터를 요청 합니다.
* Microsoft hello 기본 Azure 인프라의 hello 모니터링 데이터를 제공 하는 새 버전을 도입 하 고 SAP 요구 toobe에 대 한 Azure 고급 모니터링 확장 hello toothose 변경을 채택 합니다.
* 추가 Vhd tooyour Azure VM을 탑재 하거나 VHD를 제거 합니다. 이 시나리오에서는 저장소 관련 데이터의 hello 컬렉션을 업데이트 합니다. 끝점을 삭제 하거나, IP를 할당 하 여 구성 변경 주소 tooa VM hello 모니터링 구성을 적용 되지 않습니다.
* Azure VM의 hello 크기 예를 들어에서 변경한 크기 A5 tooany 다른 VM 크기입니다.
* 새 네트워크 인터페이스 tooyour Azure VM을 추가 합니다.

단계를 모니터링 설정을 업데이트 hello hello를 수행 하 여 모니터링 인프라 tooupdate [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.

## <a name="detailed-tasks-for-sap-software-deployment-on-a-windows-vm"></a>Linux VM에서 SAP 소프트웨어 배포에 대한 세부 작업
이 섹션에 hello 구성 및 배포 프로세스에서 특정 작업을 수행 하는 단계를 설명 합니다.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Azure PowerShell cmdlet 배포
1.  너무 이동[Microsoft Azure 다운로드](https://azure.microsoft.com/downloads/)합니다.
2.  **명령줄 도구** 아래의 **PowerShell** 아래에서 **Windows 설치**를 선택합니다.
3.  다운로드 한 hello 파일 (예를 들어 WindowsAzurePowershellGet.3f.3f.3fnew.exe)에 대 한 hello Microsoft 다운로드 관리자 대화 상자에서 선택 **실행**합니다.
4.  Microsoft 웹 플랫폼 설치 관리자 (Microsoft 웹 PI) toorun 선택 **예**합니다.
5.  다음과 같은 페이지가 나타납니다.

  ![Azure PowerShell cmdlet 설치 페이지][deployment-guide-figure-500]<a name="figure-5"></a>

6.  선택 **설치**, 다음 hello Microsoft 소프트웨어 사용 조건에 동의 하 고 있습니다.
7.  PowerShell이 설치됩니다. 선택 **마침** tooclose hello 설치 마법사.

일반적으로 매월 업데이트 되며 업데이트 toohello PowerShell cmdlet에 대 한 자주 확인 합니다. 업데이트에 대 한 가장 쉬운 방법은 toocheck hello는 toodo hello 이전 toohello 설치 페이지 5 단계에 표시 된 설치 단계입니다. hello 릴리스 날짜 및 릴리스 번호 hello cmdlet의 5 단계에 표시 된 hello 페이지에 포함 됩니다. SAP Note에서 달리 명시 하지 않는 한 [1928533] 또는 SAP Note [2015553], hello 최신 버전의 Azure PowerShell cmdlet 사용 하는 것이 좋습니다.

toocheck hello 버전의 hello 사용자 컴퓨터에 설치 된 Azure PowerShell cmdlet이 PowerShell 명령을 실행 합니다.
```powershell
Import-Module Azure
(Get-Module Azure).Version
```
hello 결과 다음과 같습니다.

![Azure PowerShell cmdlet 버전 검사의 결과][deployment-guide-figure-600]
<a name="figure-6"></a>

Hello Azure cmdlet 버전이 컴퓨터에 설치 되어 현재 버전 hello 이면 hello 설치 마법사의 첫 번째 페이지 hello 나타냅니다 추가 하 여 **(설치)** toohello 제품명 (hello 다음 스크린샷 참조). 사용자의 PowerShell Azure cmdlet은 최신 상태입니다. tooclose hello 설치 마법사, 선택 **종료**합니다.

![설치 된 Azure PowerShell cmdlet의 해당 hello 가장 최신 버전을 나타내는 Azure PowerShell cmdlet에 대 한 설치 페이지][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Azure CLI 배포
1.  너무 이동[Microsoft Azure 다운로드](https://azure.microsoft.com/downloads/)합니다.
2.  아래 **명령줄 도구**아래 **Azure 명령줄 인터페이스**선택, hello **설치** 운영 체제에 대 한 링크입니다.
3.  다운로드 한 hello 파일 (예를 들어 WindowsAzureXPlatCLI.3f.3f.3fnew.exe)에 대 한 hello Microsoft 다운로드 관리자 대화 상자에서 선택 **실행**합니다.
4.  Microsoft 웹 플랫폼 설치 관리자 (Microsoft 웹 PI) toorun 선택 **예**합니다.
5.  다음과 같은 페이지가 나타납니다.

  ![Azure PowerShell cmdlet 설치 페이지][deployment-guide-figure-500]<a name="figure-5"></a>

6.  선택 **설치**, 다음 hello Microsoft 소프트웨어 사용 조건에 동의 하 고 있습니다.
7.  Azure CLI가 설치되어 있습니다. 선택 **마침** tooclose hello 설치 마법사.

업데이트 tooAzure CLI 일반적으로 매월 업데이트 됩니다에 대 한 자주 확인 합니다. 업데이트에 대 한 가장 쉬운 방법은 toocheck hello는 toodo hello 이전 toohello 설치 페이지 5 단계에 표시 된 설치 단계입니다.


toocheck hello 버전의 컴퓨터에 설치 된 Azure CLI이 명령을 실행 합니다.
```
azure --version
```

hello 결과 다음과 같습니다.

![Azure CLI 버전 검사의 결과][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>(Windows에만 해당) VM tooan 온-프레미스 도메인에 가입
크로스-프레미스 시나리오에서 SAP Vm을 배포 하는 경우 온-프레미스 Active Directory 및 DNS를 Azure에서 확장 된 것 hello Vm 온-프레미스 도메인에 가입 됩니다. hello toojoin VM tooan 온-프레미스 도메인을 사용 하는 자세한 단계 및 hello 필요한 추가 소프트웨어 toobe는 온-프레미스 도메인의 구성원에 따라 고객 합니다. 일반적으로, VM tooan toojoin 온-프레미스 도메인, 맬웨어 방지 프로그램 소프트웨어 및 백업 또는 모니터링 소프트웨어와 같은 tooinstall 추가 소프트웨어가 필요 합니다.

이 시나리오에서 VM 환경에서 도메인에 연결할 때 인터넷 프록시 설정을 강제 hello Windows hello 게스트 VM에서에서 로컬 시스템 계정 (S-1-5-18)에 같은 프록시 설정을 hello 있는지 toomake가 필요 합니다. hello 가장 쉬운 방법은 tooforce hello 프록시 도메인 toosystems hello 도메인에 적용 되는 그룹 정책을 사용 하 여입니다.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>다운로드, 설치 및 hello Azure VM 에이전트를 사용 하도록 설정
(예: 하지 않는 hello sysprep 나 Windows 시스템 준비 도구에서 생성 되는 이미지)이 생성 되어 있지는 OS 이미지에서 배포 되는 가상 컴퓨터를 toomanually 다운로드, 설치 및 사용 hello Azure VM 에이전트가 필요 합니다.

Hello Azure Marketplace에서에서 VM을 배포 하는 경우에이 단계가 필요 하지 않습니다. Hello Azure Marketplace에서에서 이미지 hello Azure VM 에이전트는 이미 있습니다.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Hello Azure VM 에이전트를 다운로드 합니다.
  1.  Hello 다운로드 [Azure VM 에이전트 설치 관리자 패키지](https://go.microsoft.com/fwlink/?LinkId=394789)합니다.
  2.  개인용 컴퓨터 또는 서버 hello VM 에이전트 MSI 패키지를 로컬로 저장 합니다.
2.  Hello Azure VM 에이전트를 설치 합니다.
  1.  연결 toohello 프로토콜 RDP (원격 데스크톱)를 사용 하 여 Azure VM을 배포 합니다.
  2.  Hello VM 에이전트의 MSI 파일 hello에 대 한 대상 디렉터리 선택 hello 및 hello VM에서 Windows 탐색기 창을 엽니다.
  3.  Hello VM에서 VM 에이전트 hello의 로컬 컴퓨터/서버 toohello 대상 디렉터리에서 hello Azure VM 에이전트 설치 프로그램 MSI 파일을 끕니다.
  4.  Hello VM에 hello MSI 파일을 두 번 클릭 합니다.
3.  Vm는 조인 된 tooon 온-프레미스 도메인에 대해 확인 결과적 인터넷 프록시 설정이 적용 toohello Windows 로컬 시스템 계정 (S-1-5-18)에서 VM hello에 설명 된 대로 [hello 프록시 구성] [ deployment-guide-configure-proxy]. hello VM 에이전트는이 컨텍스트에서 실행 되며 toobe 수 tooconnect tooAzure 필요 합니다.

사용자 개입 없이 필요한 tooupdate hello Azure VM 에이전트입니다. hello VM 에이전트가 자동으로 업데이트 및 VM 다시 시작할 필요가 없습니다.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
사용 하 여 hello 다음 Linux 용 tooinstall hello VM 에이전트를 명령:

* **SELS(SUSE Linux Enterprise Server)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **RHEL(Red Hat Enterprise Linux)**

  ```
  sudo yum install WALinuxAgent
  ```

Tooupdate hello Azure Linux 에이전트에 설명 된 단계를 hello 수행 hello 에이전트가 이미 설치 되어 있으면 [GitHub에서 VM toohello 최신 버전에서 업데이트 hello Azure Linux 에이전트][virtual-machines-linux-update-agent]합니다.

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Hello 프록시 구성
Windows에서 tooconfigure hello 프록시를 수행 하는 hello 단계는 Linux에서 hello 프록시를 구성 하는 hello 방법은 다릅니다.

#### <a name="windows"></a>Windows
프록시 설정이 올바르게 설정 해야 hello tooaccess hello 인터넷 로컬 시스템 계정에 대 한 합니다. 프록시 설정이 그룹 정책에 의해을 설정 하지는 hello 로컬 시스템 계정에 대 한 hello 설정을 구성할 수 있습니다.

1. 너무 이동**시작**, 입력 **gpedit.msc**를 선택한 후 **Enter**합니다.
2. **컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소** > **Internet Explorer**를 선택합니다. 해당 hello 설정 되었는지 확인 **프록시 설정을 컴퓨터별 (보다는 만들기 사용자 단위)** 비활성화 되었거나 구성 되어 있지 않습니다.
3. **제어판**, 너무 이동**네트워크 및 공유 센터** > **인터넷 옵션**합니다.
4. Hello에 **연결** 탭, 선택 hello **LAN 설정** 단추입니다.
5. 지우기 hello **자동으로 설정 검색** 확인란 합니다.
6. 선택 hello **사용자 LAN에 프록시 서버를 사용 하 여** 확인란을 선택한 다음 hello 프록시 주소와 포트를 입력 합니다.
7. 선택 hello **고급** 단추입니다.
8. Hello에 **예외** 상자 hello IP 주소를 입력 **168.63.129.16**합니다. **확인**을 선택합니다.


#### <a name="linux"></a>Linux
Hello에 있는 Microsoft Azure 게스트 에이전트의 hello 구성 파일에서 올바른 프록시 hello 구성 \\등\\waagent.conf 합니다.

Hello 매개 변수 뒤를 설정 합니다.

1.  **HTTP 프록시 호스트** 예를 들어 너무 설정**proxy.corp.local**합니다.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **HTTP 프록시 포트** 예를 들어 너무 설정**80**합니다.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Hello 에이전트를 다시 시작 합니다.

  ```
  sudo service waagent restart
  ```

프록시 설정이 hello \\등\\waagent.conf도 필요한 toohello VM 확장을 적용 합니다. Toouse 하려는 경우 Azure 저장소 hello hello 트래픽 toothese 저장소는 온-프레미스 인트라넷을 통해 잘못 되어 있는지 확인 합니다. 사용자 정의 만든 경우 경로 tooenable 강제 터널링, toohello 저장소 트래픽을 라우팅하는 경로 추가 해야 toohello 인터넷에 직접를 사용 하 여 사이트 간 VPN 연결 합니다.

* **SLES**

  에 나열 된 hello IP 주소에도 tooadd 경로 필요 \\등\\regionserverclnt.cfg 합니다. hello 다음 그림은 예:

  ![강제 터널링][deployment-guide-figure-50]


* **RHEL**

  에 나열 된 hello 호스트의 IP 주소 hello에도 tooadd 경로 필요 \\등\\yum.repos.d\\rhui-부하 분산 장치입니다. 예를 들어 hello 앞에 그림을 참조 하세요.

사용자 정의 경로에 대한 자세한 내용은 [사용자 정의 경로 및 IP 전달][virtual-networks-udr-overview]을 참조하세요.

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Azure 고급 모니터링 확장의 SAP 용 hello 구성
에 설명 된 대로 hello VM 준비 했으므로 때 [Azure에서의 SAP 용 Vm 배포 시나리오][deployment-guide-3], hello hello 가상 컴퓨터에 Azure VM 에이전트가 설치 되어 있습니다. hello 다음 단계는 toodeploy hello Azure 고급 모니터링 확장 hello 글로벌 Azure 데이터 센터에서 Azure 확장 리포지토리에서 hello에서 사용할 수 있는 SAP 용입니다. 자세한 내용은 [Linux에서 SAP용 Azure Virtual Machines 계획 및 구현][planning-guide-9.1]을 참조하세요.

PowerShell 또는 Azure CLI tooinstall를 사용할 수 있으며 Azure 고급 모니터링 확장의 SAP 용 hello 구성. Windows 컴퓨터를 사용 하 여 Windows 또는 Linux VM에서 tooinstall hello 확장 참조 [Azure PowerShell][deployment-guide-4.5.1]합니다. Linux 데스크톱을 사용 하 여 Linux VM의 tooinstall hello 확장 참조 [Azure CLI][deployment-guide-4.5.2]합니다.

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Linux 및 Windows VM용 Azure PowerShell
PowerShell을 사용 하 여 tooinstall hello Azure 고급 모니터링 확장의 SAP 용:

1. Hello hello Azure PowerShell cmdlet의 최신 버전을 설치 했는지 확인 합니다. 자세한 내용은 [Azure PowerShell cmdlet 배포][deployment-guide-4.1]를 참조하세요.  
2. Hello 다음 PowerShell cmdlet을 실행 합니다.
  사용 가능한 환경 목록을 보려면 `commandlet Get-AzureRmEnvironment`을 실행합니다. Toouse 공용 Azure에서 사용자 환경에는 원하는 경우 **azure 클라우드**합니다. 중국의 Azure인 경우 **AzureChinaCloud**를 선택합니다.


      ```powershell
      $env = Get-AzureRmEnvironment -Name <name of hello environment>
      Login-AzureRmAccount -Environment $env
      Set-AzureRmContext -SubscriptionName <subscription name>

      Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
      ```

계정 데이터를 입력 하 고 hello Azure 가상 컴퓨터를 식별 한 후 hello 스크립트 hello 필수 확장명을 배포 하 고 hello 필요한 기능을 사용할 수 있습니다. 이 작업은 몇 분 정도 걸릴 수 있습니다.
`Set-AzureRmVMAEMExtension`에 대한 자세한 내용은[Set-AzureRmVMAEMExtension][msdn-set-azurermvmaemextension]을 참조하세요.

![SAP 관련 Azure cmdlet Set-AzureRmVMAEMExtension의 성공적인 실행][deployment-guide-figure-900]

hello `Set-AzureRmVMAEMExtension` 구성과 모든 hello 단계 tooconfigure 호스트 SAP 용 모니터링 합니다.

hello 다음 정보를 포함 하는 hello 스크립트 출력:

* 확인 구성 된 VM toohello 탑재 그에 대 한 모니터링 기본 hello (hello OS)가 있는 VHD 및 모든 추가 Vhd.
* hello 다음 두 메시지는 특정 저장소 계정에 대 한 저장소 메트릭의 hello 구성을 확인합니다.
* 출력 한 줄에 hello hello 모니터링 구성의 실제 업데이트의 hello 상태를 제공합니다.
* 다른 출력 줄이 해당 hello 구성이 배포 또는 업데이트 되었는지 확인 합니다.
* 출력의 마지막 줄 hello는 알림입니다. 테스트 hello 모니터링 구성에 대 한 옵션을 보여 줍니다.

에 설명 된 대로 Azure 고급 모니터링의 모든 단계가 성공적으로 실행 하 고 hello 필요한 데이터를 제공 하는 Azure 인프라 해당 hello toocheck 계속 hello Azure 고급 모니터링 확장 SAP 용 hello 준비 확인 [SAP 용 Azure 고급 모니터링에 대 한 준비 상태 검사가][deployment-guide-5.1]합니다. Azure 진단 toocollect hello 관련 데이터 15-30 분 동안 기다립니다.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Linux VM용 Azure CLI
tooinstall hello Azure 고급 모니터링 확장의 SAP 용 Azure CLI를 사용 하 여:

1. 에 설명 된 대로 Azure CLI를 설치 [설치 hello Azure CLI][azure-cli]합니다.
2. Azure 계정으로 로그인합니다.

  ```
  azure login
  ```

3. TooAzure Resource Manager 모드로 전환 합니다.

  ```
  azure config mode arm
  ```

4. Azure 고급 모니터링을 사용하도록 설정합니다.

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Hello Azure Linux VM에 활성화 되어 해당 hello Azure 고급 모니터링 확장을 확인 합니다. 검사 파일을 여부 hello \\var\\lib\\AzureEnhancedMonitor\\PerfCounters 존재 합니다. 이 특성이 있으면 명령 프롬프트에서이 명령을 toodisplay 정보 hello Azure 향상 된 모니터에 의해 수집 된를 실행 합니다.
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

hello 출력은 다음과 같습니다.
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>종단 간 모니터링 확인 및 문제 해결
Azure VM을 배포 하면 관련 Azure 모니터링 인프라 hello 설정한 후 hello Azure 고급 모니터링 확장의 모든 hello 구성 요소가 예상 대로 작동 하는지 확인 합니다.

에 설명 된 대로 Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 hello 준비 검사를 실행 [Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 준비 상태 검사가][deployment-guide-5.1]합니다. 모든 준비 검사 결과가 긍정적이고 모든 관련 성능 카운터가 정상으로 나타나면 Azure 모니터링이 성공적으로 설정된 것입니다. Hello에 hello SAP Note에서 설명 하는 SAP 호스트 에이전트 설치를 진행할 수 [SAP 리소스][deployment-guide-2.2]합니다. Hello 준비 확인 되는 것 카운터가 누락 되었거나에 설명 된 대로 Azure 모니터링 인프라 hello에 대 한 hello 상태 검사를 실행 하는 경우 [Azure 모니터링 인프라 구성에 대 한 상태 검사] [ deployment-guide-5.2]. 자세한 문제 해결 옵션은 [SAP용 Azure 모니터링 문제 해결][deployment-guide-5.3]을 참조하세요.

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Azure 고급 모니터링 확장의 SAP 용 hello에 대 한 준비 확인
이 검사 하면 SAP 응용 프로그램 내에 표시 되는 모든 성능 메트릭을 hello 기본 Azure 모니터링 인프라에서 제공 됩니다.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Windows VM에서 hello 준비 검사를 실행 합니다.

1.  Toohello Azure 가상 컴퓨터에에서 로그인 (관리자 계정을 사용 하 여 필요 하지 않음).
2.  명령 프롬프트 창을 엽니다.
3.  Hello 명령 프롬프트에서 hello 디렉터리 toohello 설치 폴더의 hello Azure 고급 모니터링 확장 SAP에 대 한 변경: c:\\패키지\\플러그 인\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;버전 >\\삭제

  hello *버전* hello 경로 toohello에 모니터링 확장 다를 수 있습니다. 여러 버전의 hello 설치 폴더, hello AzureEnhancedMonitoring Windows 서비스의 hello 구성 확인 화면에 확장을 모니터링 하는 hello에 대 한 폴더를 표시 하 고 스위치 toohello 폴더도 표시 되는 다음 경우 *경로 tooexecutable* .

  ![서비스 실행 중의 속성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-figure-1000]

4.  Hello 명령 프롬프트에서 실행 **azperflib.exe** 매개 변수 없이 합니다.

  > [!NOTE]
  > Azperflib.exe는 루프에서 실행 되며 60 초 마다 hello 수집 된 카운터를 업데이트 합니다. 명령 프롬프트 창 닫기 hello tooend hello 루프입니다.
  >
  >

Azure 고급 모니터링 확장 설치 되지 않은 hello 또는 hello AzureEnhancedMonitoring 서비스를 실행 하지 않는 경우 hello 확장이 올바르게 구성 되지 않았습니다. Toodeploy 확장 hello 하는 방법에 대 한 자세한 내용은 참조 [문제 해결 SAP 용 Azure 모니터링 인프라 hello][deployment-guide-5.3]합니다.

##### <a name="check-hello-output-of-azperflibexe"></a>Azperflib.exe의 hello 출력 확인
Azperflib.exe 출력은 SAP용 Azure 성능 카운터가 모두 채워진 상태로 표시됩니다. 수집 된 카운터 목록의 hello의 hello 맨 아래에 요약 및 상태 표시기 Azure 모니터링의 hello 상태를 표시 합니다.

![문제가 없음을 나타내는 azperflib.exe를 실행하여 표시된 상태 검사 출력][deployment-guide-figure-1100]
<a name="figure-11"></a>

Hello에 대 한 반환 하는 hello 결과 확인 **카운터 합계** 및 비어 있는 것으로 보고 되는 출력 **상태**hello 앞 그림에에서 표시 합니다.

Hello 결과 값을 다음과 같이 해석 합니다.

| Azperflib.exe 결과 값 | Azure 모니터링 상태 정보 |
| --- | --- |
| **API 호출 - 사용할 수 없음** | 사용할 수 없는 카운터 중 하나는 적용 되지 않음 toohello 가상 컴퓨터 구성 될 수 있습니다 또는 오류가 발생 합니다. **상태 정보**를 참조하세요. |
| **카운터 합계 - 비어 있음** |다음 두 개의 Azure 저장소 카운터 hello 비어 있을 수 있습니다. <ul><li>저장소 읽기 작업 대기 시간 서버 밀리초</li><li>저장소 읽기 작업 대기 시간 E2E 밀리초</li></ul>그 외의 카운터는 값이 있어야 합니다. |
| **상태 정보** |반환 상태가 **OK**를 표시하는 경우에만 OK입니다. |
| **진단** |상태 정보에 대한 자세한 정보입니다. |

경우 hello **상태** 값이 **확인**, hello 지침에 따라 [Azure 모니터링 인프라 구성에 대 한 상태 검사] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Linux VM의 hello 준비 검사를 실행 합니다.

1.  SSH를 사용 하 여 toohello Azure 가상 컴퓨터를 연결 합니다.

2.  Hello Azure 고급 모니터링 확장의 hello 출력을 확인 합니다.

  a.  `more /var/lib/AzureEnhancedMonitor/PerfCounters` 실행

   **예상 결과**: 성능 카운터 목록을 반환합니다. hello 파일은 비워둘 수 없습니다.

 b. `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error` 실행

   **예상 결과**: 여기서는 hello 오류 반환 한 줄 **none**, 예를 들어 **3; 구성 합니다. 오류 발생; 0, 0; none, 0, 1456416792, tst servercs;**

  c. `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord` 실행

    **예상 결과**: 빈 상태로 반환하거나 존재하지 않습니다.

Hello 위의 확인 하지 못한 경우, 이러한 추가 검사를 실행 합니다.

1.  해당 hello waagent 설치 및 활성화 되어 있는지 확인 합니다.

  a.  `sudo ls -al /var/lib/waagent/` 실행

      **예상 결과**: hello waagent 디렉터리의 hello 콘텐츠를 나열 합니다.

  b.  `ps -ax | grep waagent` 실행

   **예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /usr/sbin/waagent -daemon`

2. 해당 hello Linux 진단 확장 설치 및 활성화 되어 있는지 확인 하십시오.

  a.  `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-'` 실행

   **예상 결과**: hello Linux 진단 확장 디렉터리의 hello 콘텐츠를 나열 합니다.

 b. `ps -ax | grep diagnostic` 실행

   **예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py -daemon`

3.   해당 hello Azure 고급 모니터링 확장 설치 되어 실행 중인지 확인 합니다.

  a.  `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-/'` 실행

    **예상 결과**: hello Azure 고급 모니터링 확장 디렉터리의 hello 콘텐츠를 나열 합니다.

  b. `ps -ax | grep AzureEnhanced` 실행

     **예상 결과**: 다음과 유사한 한 항목을 표시합니다. `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`

3. SAP Note에서 설명 된 대로 SAP 호스트 에이전트를 설치 [1031096]의 hello 출력을 확인 하 고 `saposcol`합니다.

  a.  `/usr/sap/hostctrl/exe/saposcol -d` 실행

  b.  `dump ccm` 실행

  c.  확인 여부 hello **Virtualization_Configuration\Enhanced 모니터링 액세스** 메트릭은 **true**합니다.

SAP NetWeaver ABAP 응용 프로그램 서버가 이미 설치된 경우 트랜잭션 ST06을 열고 고급 모니터링이 사용하도록 설정되어 있는지 여부를 확인합니다.

하나라도 이러한 검사 중 실패 하 고 tooredeploy 확장 hello 하는 방법에 대 한 자세한 내용은 참조 하는 경우 [문제 해결 SAP 용 Azure 모니터링 인프라 hello][deployment-guide-5.3]합니다.

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Azure 모니터링 인프라 구성 hello에 대 한 상태 확인
Hello 테스트에 설명 된 일부 데이터를 모니터링 하는 hello 제대로 전달 되지 않으면 [SAP 용 Azure 고급 모니터링에 대 한 준비 상태 검사가][deployment-guide-5.1]실행 hello `Test-AzureRmVMAEMExtension` cmdlet toocheck 여부 hello Azure 모니터링 인프라 및 SAP에 대 한 확장을 모니터링 하는 hello 올바르게 구성 되어 있습니다.

1.  에 설명 된 대로 hello hello Azure PowerShell cmdlet의 최신 버전을 설치 했는지 확인 [배포 Azure PowerShell cmdlet][deployment-guide-4.1]합니다.
2.  Hello 다음 PowerShell cmdlet을 실행 합니다. 사용 가능한 환경 목록이 hello cmdlet를 실행 합니다. `Get-AzureRmEnvironment`합니다. 공용, 선택 toouse hello **azure 클라우드** 환경입니다. 중국의 Azure인 경우 **AzureChinaCloud**를 선택합니다.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  계정 데이터를 입력 하 고 hello Azure 가상 컴퓨터를 식별 합니다.

  ![SAP 관련 Azure cmdlet Test-VMConfigForSAP_GUI의 입력 페이지][deployment-guide-figure-1200]

4. 선택 hello hello 가상 컴퓨터의 테스트 hello 구성을 스크립팅 합니다.

  ![SAP 용 Azure 모니터링 인프라 hello의 성공적인 테스트 출력][deployment-guide-figure-1300]

모든 상태 검사 결과가 **OK**인지 확인합니다. 일부 검사 표시 되지 않는 경우 **확인**, hello 업데이트 cmdlet을 실행 하에 설명 된 대로 [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다. 15 분 정도 기다린 후에 설명 된 반복 hello 검사 [SAP 용 Azure 고급 모니터링에 대 한 준비 상태 검사가] [ deployment-guide-5.1] 및 [Azure 모니터링 인프라 구성상태확인] [deployment-guide-5.2]. Hello 검사에는 여전히 일부 또는 전체 카운터에 문제가 있음을 나타낼, 참조 [문제 해결 SAP 용 Azure 모니터링 인프라 hello][deployment-guide-5.3]합니다.

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>SAP 용 Azure 모니터링 인프라 hello 문제 해결

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Azure 성능 카운터가 전혀 표시되지 않습니다.
hello AzureEnhancedMonitoring Windows 서비스를 Azure의 성능 메트릭을 수집합니다. Hello 서비스를 올바르게 설치 되지 않은 경우 또는 VM에서 실행 되지 않는 경우 없음 성능 메트릭을 수집할 수 있습니다.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>hello Azure 고급 모니터링 확장의 설치 디렉터리 hello 비어 있습니다.

###### <a name="issue"></a>문제
hello 설치 디렉터리: c:\\패키지\\플러그 인\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;버전 >\\놓기 비어 있습니다.

###### <a name="solution"></a>해결 방법
hello 확장이 설치 되지 않았습니다. (앞에서 설명한) 프록시 문제인지 여부를 결정합니다. Toorestart hello 컴퓨터나 hello를 다시 실행된 해야 `Set-AzureRmVMAEMExtension` 구성 스크립트입니다.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Azure 고급 모니터링 서비스가 없습니다.

###### <a name="issue"></a>문제
hello AzureEnhancedMonitoring Windows 서비스가 존재 하지 않습니다.

Azperflib.exe 출력에 오류가 발생합니다.

![Azperflib.exe의 실행 SAP 용 Azure 고급 모니터링 확장 hello의 hello 서비스가 실행 되지 않습니다 나타냅니다.][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>해결 방법
Hello 서비스가 없는 경우 Azure 고급 모니터링 확장의 SAP 용 hello 올바르게 설치 되지 않았습니다. 배포 시나리오에 대 한 설명 하는 hello 단계를 사용 하 여 hello 확장을 다시 배포 [Azure의 SAP 용 Vm 배포 시나리오][deployment-guide-3]합니다.

Hello Azure 성능 카운터가 hello Azure VM에서에서 제공 되는지 여부를 1 시간 후 hello 확장 프로그램을 배포한 후 다시 확인 합니다.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Azure 고급 모니터링 서비스가 존재 하지만 toostart 실패

###### <a name="issue"></a>문제
hello AzureEnhancedMonitoring Windows 서비스 및를 사용 하는 있지만 toostart 실패 합니다. 자세한 내용은 hello 응용 프로그램 이벤트 로그를 확인 합니다.

###### <a name="solution"></a>해결 방법
hello 구성이 올바르지 않습니다. 에 설명 된 대로 VM hello에 대 한 확장을 모니터링 하는 hello를 다시 시작 [구성 hello Azure 고급 모니터링 확장의 SAP 용][deployment-guide-4.5]합니다.

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] 일부 Azure 성능 카운터가 없습니다.
hello AzureEnhancedMonitoring Windows 서비스를 Azure의 성능 메트릭을 수집합니다. hello 서비스는 여러 원본에서 데이터를 가져옵니다. 일부 구성 데이터는 로컬로 수집되고 일부 성능 메트릭은 Azure 진단에서 읽습니다. 저장소 카운터는 사용자가 로그온 hello 저장소 구독 수준에서에서 사용 됩니다.

SAP Note를 사용 하 여 문제를 해결 하는 경우 [1999351] hello 문제 해결, hello를 다시 실행 하지 않는 `Set-AzureRmVMAEMExtension` 구성 스크립트입니다. 설정 된 후에 즉시 저장소 분석 또는 진단 카운터를 만들 수 수 없으므로 toowait 한 시간을 할 수 있습니다. Hello 문제가 계속 되 면 hello Windows에 대 한 구성 요소 OP NT AZR BC 또는 BC-OP-LNX-AZR Linux 가상 컴퓨터에 SAP 고객 지원 메시지를 엽니다.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Azure 성능 카운터가 전혀 표시되지 않습니다.
Azure의 성능 메트릭은 데몬에 의해 수집됩니다. Hello 디먼이 실행 되지 않는 경우 없음 성능 메트릭을 수집할 수 있습니다.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>hello Azure 고급 모니터링 확장의 설치 디렉터리 hello 비어 있습니다.

###### <a name="issue"></a>문제
hello 디렉터리 \\var\\lib\\waagent\\ hello Azure 고급 모니터링 확장에 대 한 하위 디렉터리는 없습니다.

###### <a name="solution"></a>해결 방법
hello 확장이 설치 되지 않았습니다. (앞에서 설명한) 프록시 문제인지 여부를 결정합니다. Toorestart hello 컴퓨터 및/또는 다시 실행된 hello 해야 `Set-AzureRmVMAEMExtension` 구성 스크립트입니다.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] 일부 Azure 성능 카운터가 없습니다.
Azure에서 성능 메트릭은 여러 원본에서 데이터를 가져오는 데몬에 의해 수집됩니다. 일부 구성 데이터는 로컬로 수집되고 일부 성능 메트릭은 Azure 진단에서 읽습니다. 저장소 카운터 저장소 구독에서 hello 로그에서 제공 됩니다.

알려진 문제의 전체 최신 목록은 SAP용 고급 Azure 모니터링에 대한 추가 문제 해결 정보를 포함하고 있는 SAP Note [1999351]을 참조하세요.

SAP Note를 사용 하 여 문제를 해결 하는 경우 [1999351] hello 문제를 해결, hello를 다시 실행 하지 않는 `Set-AzureRmVMAEMExtension` 구성 스크립트에 설명 된 대로 [구성 hello Azure 고급 모니터링 확장SAP용][deployment-guide-4.5]. 설정 된 후에 즉시 저장소 분석 또는 진단 카운터를 만들 수 수 없으므로 한 시간에 대 한 toowait를 할 수 있습니다. Hello 문제가 계속 되 면 hello Windows에 대 한 구성 요소 OP NT AZR BC 또는 BC-OP-LNX-AZR Linux 가상 컴퓨터에 SAP 고객 지원 메시지를 엽니다.
