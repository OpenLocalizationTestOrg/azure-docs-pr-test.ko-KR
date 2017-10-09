---
title: "가상 컴퓨터 aaaAzure 계획 및 구현에 대 한 SAP NetWeaver | Microsoft Docs"
description: "SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: d7c59cc1-b2d0-4d90-9126-628f9c7a5538
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d1e9fa13d847e4d8abb3c34fd352d1f4ece3717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-planning-and-implementation-for-sap-netweaver"></a>SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현
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
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md  
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/planning-monitoring-overview-2502.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-2901]:media/virtual-machines-shared-sap-planning-guide/2901-azure-ha-sap-ha-md.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-3201]:media/virtual-machines-shared-sap-planning-guide/3201-sap-ha-with-sql-md.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-windows-capture-image-resource-manager]:../../windows/capture-image.md
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-create-upload-vhd-oracle]:../../linux/oracle-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics-windows]:../../windows/multiple-nics.md
[virtual-networks-multiple-nics-linux]:../../linux/multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md
[capture-image-linux-step-2-create-vm-image]:../../linux/capture-image.md#step-2-create-vm-image

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

긴 조달 주기를 거치지 않고도 최단 시간에 Microsoft Azure에 회사 tooacquire 계산 및 저장소 리소스가 수 있습니다. Azure 가상 컴퓨터의 SAP NetWeaver 기반 응용 프로그램을 Azure로 마찬가지로 회사 toodeploy 고전 응용 프로그램을 허용 하 고 추가로 리소스 내부에서 사용 하지 않고도 안정성과 가용성을 확장 합니다. 또한 azure 가상 컴퓨터 서비스 크로스-프레미스 연결을 사용 하면 회사 tooactively는 온-프레미스 도메인, 사설 클라우드 및 SAP 시스템 지형에 Azure 가상 컴퓨터 통합을 지원 합니다.
이 백서 hello 기초 Microsoft Azure 가상 컴퓨터에 설명 하 고 Azure에서 SAP NetWeaver 설치에 대 한 계획 및 구현 고려 사항에는 연습을 제공 및 그렇게 해야 시작 하기 전에 hello 문서 tooread 여야 Azure에서 SAP NetWeaver의 실제 배포 합니다.
hello 용지 보완 hello SAP 설치 설명서 및 SAP Note를 설치 및 배포에 SAP 소프트웨어에 대 한 기본 리소스 hello 플랫폼을 제공 합니다.

## <a name="summary"></a>요약
클라우드 컴퓨팅은 toolarge 및 다국적 회사를 중소 기업에서 점점 더 많은 중요도 hello IT 업계 내에서 취소 하는 널리 사용 되는 용어입니다.

Microsoft Azure는 hello 새로운 작업 방식을 폭넓게 제공 된 microsoft에서 클라우드 서비스 플랫폼입니다. 이제 고객은 수 toorapidly 프로 비전 및 프로 비전 해제 응용 프로그램에서 hello 클라우드 서비스로 제한 된 tootechnical 또는 예산 제한 되지 않습니다. 하드웨어 인프라에 시간과 예산을 투자를 하는 대신 고객 및 사용자에 대 한 회사는 hello 응용 프로그램, 비즈니스 프로세스 및 그 이점에 집중할 수 있습니다.

Microsoft Azure 가상 컴퓨터 서비스와 함께 Microsoft는 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다. SAP NetWeaver 기반 응용 프로그램은 Azure 가상 컴퓨터(IaaS)에서 지원됩니다. 이 백서에서는 어떻게 tooplan 및 구현 SAP NetWeaver 기반 응용 프로그램을 Microsoft Azure 내에서 선택한 hello 플랫폼으로 설명 합니다.

자체 hello 용지 두 가지 주요 측면에 중점을 둡니다.

* hello 첫 번째 부분은 Azure에서 SAP NetWeaver 기반 응용 프로그램에 대 한 두 가지 지원 되는 배포 패턴을 설명합니다. 또한 SAP 배포를 고려한 Azure의 일반적인 사용에 대해서도 설명합니다.
* hello 두 번째 파트 세부 정보 hello 첫 번째 부분에 설명 된 hello 두 가지 시나리오를 구현 합니다.

추가 리소스는 이 문서의 [리소스][planning-guide-1.2] 장을 참조하세요.

### <a name="definitions-upfront"></a>사전 정의
Hello 설명서에서는 아래 계약 내용 hello를 사용 합니다.

* IaaS: 서비스 제공 인프라
* PaaS: Platform as a Service
* SaaS: Software as a Service
* ARM: Azure Resource Manager
* SAP 구성 요소: ECC, BW, Solution Manager 또는 EP 등의 개별 SAP 응용 프로그램.  SAP 구성 요소는 기존의 ABAP 또는 Java 기술을 기반으로 하거나 비즈니스 개체와 같은 비NetWeaver 기반 응용 프로그램을 기반으로 사용할 수 있습니다.
* SAP 환경: 하나 이상의 SAP 구성 요소 tooperform 개발, QAS, 학습, DR 또는 프로덕션 등의 비즈니스 기능을 논리적으로 그룹화 합니다.
* SAP 지형:이 참조 toohello 전체 SAP 자산에 고객의 IT 지형 합니다. hello SAP 지형에는 모든 프로덕션 및 비프로덕션 환경이 포함 되어 있습니다.
* 예를 들어는 SAP ERP 개발 시스템, SAP BW 테스트 시스템, SAP CRM 프로덕션 시스템 등의 응용 프로그램 계층과 DBMS 계층의 SAP 시스템: hello 조합... Azure 배포는 지원 되는 toodivide 온-프레미스와 Azure 간에 이러한 두 계층입니다. 즉, SAP 시스템은 온-프레미스에 배포되거나 Azure에 배포됩니다. 그러나 hello 서로 다른 시스템에 Azure 또는 온-프레미스 SAP 지형의을 배포할 수 있습니다. 예를 들어 SAP CRM 프로덕션 시스템 온-프레미스 hello 하지만 Azure의 hello SAP CRM 개발 및 테스트 시스템을 배포할 수 있습니다.
* 클라우드 전용 배포: 여기서 hello Azure 구독이 사이트-사이트를 통해 연결 되어 있지 않거나 ExpressRoute 연결 toohello 온-프레미스 네트워크 인프라를 배포 합니다. 공통 Azure 설명서에서는 이러한 종류의 배포를 '클라우드 전용' 배포라고도 합니다. 이 방법으로 배포 된 가상 컴퓨터 이용 하 여 hello 인터넷 및 공용 IP 주소 및/또는 공용 DNS Azure에서 할당 된 toohello Vm 이름을 지정 합니다. Microsoft Windows에 대 한 온-프레미스 Active Directory (AD) hello 및 DNS가 이러한 유형의 배포에서 tooAzure 확장 되지 않습니다. 따라서 hello Vm hello 온-프레미스 Active Directory의 일부가 아닌 합니다. 예를 들어 OpenLDAP와 Kerberos를 함께 사용하는 Linux 구현에서도 마찬가지입니다.

> [!NOTE]
> 이 문서에서 클라우드 전용 배포는 온-프레미스에서 Active Directory/OpenLDAP 또는 이름 확인을 공용 클라우드로 확장하지 않고 Azure에서 단독으로 실행 중인 전체 SAP 지형으로 정의됩니다. 클라우드 전용 구성은 프로덕션 SAP 시스템 또는 SAP STMS 또는 다른 온-프레미스 리소스 toobe 있는 온-프레미스 리소스 및 Azure에서 호스트 되는 SAP 시스템 사이 사용 해야 하는 구성에 대 한 지원 되지 않습니다.
>
>

* 크로스-프레미스: Vm 배포 tooan 사이트 간, 멀티 사이트 또는 hello 온-프레미스 센터와 Azure 간의 ExpressRoute 연결 된 Azure 구독에 있는 시나리오에 설명 합니다. 공통 Azure 설명서에서 이러한 종류의 배포를 크로스-프레미스 시나리오라고도 합니다. hello hello 연결에 대 한 원인은 tooextend 온-프레미스 도메인, 온-프레미스 Active Directory/OpenLDAP 및 온-프레미스 DNS Azure로입니다. hello 온-프레미스 가로 확장된 toohello hello 구독의 Azure 자산 됩니다. Hello Vm이 확장명이 hello 온-프레미스 도메인의 일부를 수 있습니다. Hello 온-프레미스 도메인의 도메인 사용자 hello 서버에 액세스할 수 및 서비스를 실행할 수에 Vm (예: DBMS 서비스)입니다. 온-프레미스에 배포된 VM과 Azure에 배포된 VM 간의 통신 및 이름 확인이 가능합니다. 대부분의 SAP 자산 toobe에 배포 된 것으로 예상 하는 hello 시나리오입니다. 자세한 내용은 [이 문서][vpn-gateway-cross-premises-options] 및 [이 문서][vpn-gateway-site-to-site-create]를 참조하세요.

> [!NOTE]
> 프로덕션 SAP 시스템의 경우 SAP 시스템을 실행 중인 Azure 가상 컴퓨터가 온-프레미스 도메인의 멤버인 SAP 시스템의 크로스-프레미스 배포가 지원됩니다. 일부 또는 전체 SAP 지형을 Azure로 배포하기 위한 크로스-프레미스 구성이 지원됩니다. Azure의 hello 전체 SAP 지형을 실행에 온-프레미스 도메인 및 광고/OpenLDAP의 일부로 해당 Vm을 포함 해야 합니다. 이전 버전의 hello 문서, 온-프레미스와 Azure 간 크로스-프레미스 연결 된다는 hello 사실에 입각에 '혼합' hello 용어 루 팅 하는 하이브리드-IT 시나리오에 대 한 얘기 합니다. 또한 해당 hello Azure의 Vm hello의 일부인 hello 팩트 온-프레미스 Active Directory / OpenLDAP 합니다.
>
>

일부 Microsoft 문서에서는 특히 DBMS HA 구성의 경우 크로스-프레미스 시나리오를 약간 다르게 설명합니다. SAP 관련 문서 hello hello 경우에서 hello 크로스-프레미스 시나리오만 수행 하는 경우 toohaving 사이트 간 또는 개인 (express 경로) 연결 및 hello 팩트 hello SAP 지형이 온-프레미스와 Azure 간에 분산 된다는 합니다.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>리소스
hello 다음 추가 가이드는 hello Azure에서 SAP 배포 항목에 사용할 수 있습니다.

* [SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현(이 문서)][planning-guide]
* [SAP NetWeaver에 대한 Azure Virtual Machines 배포][deployment-guide]
* [SAP NetWeaver에 대한 Azure Virtual Machines DBMS 배포][dbms-guide]

> [!IMPORTANT]
> 가능한 SAP 설치 가이드를 참조 하는 링크 toohello 아무 곳에 나 사용 됩니다 (참조 instguide-01, 참조 <http://service.sap.com/instguides>). Toohello 필수 구성 요소 및 설치 프로세스를 hello SAP NetWeaver 설치 가이드 나올 때 항상 있어야이 문서에서는 Microsoft Azure 가상 컴퓨터에 설치 된 SAP NetWeaver 시스템에 대 한 특정 작업 방법을 배웁니다.를 자세히 확인 합니다.
>
>

SAP Note 다음 hello는 Azure의 SAP toohello 관련된 항목:

| Note 번호 | 제목 |
| --- | --- |
| [1928533] |Azure의 SAP 응용 프로그램: 지원 제품 및 크기 조정 |
| [2015553] |Microsoft Azure의 SAP: 지원 필수 조건 |
| [1999351] |SAP용 고급 Azure 모니터링 문제 해결 |
| [2178632] |Microsoft Azure의 SAP용 주요 모니터링 메트릭 |
| [1409604] |Windows에서의 가상화: 향상된 모니터링 |
| [2191498] |Azure와 Linux의 SAP: 향상된 모니터링 |
| [2243692] |Microsoft Azure(IaaS) VM의 Linux: SAP 라이선스 문제 |
| [1984787] |SUSE LINUX Enterprise Server 12: 설치 참고 |
| [2002167] |Red Hat Enterprise Linux 7.x: 설치 및 업그레이드 |
| [2069760] |Oracle Linux 7.x SAP 설치 및 업그레이드 |
| [1597355] |Linux에 대한 스왑 공간 권장 사항 |

또한 읽기 hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) Linux에 대 한 모든 SAP Note를 포함 하 합니다.

Azure 구독의 일반적인 기본 제한 및 최대 제한은 [이 문서][azure-subscription-service-limits-subscription]에 있습니다.

## <a name="possible-scenarios"></a>가능한 시나리오
SAP는 기업 내의 hello 가장 중요 한 응용 프로그램 중 하나로 보는 경우가 많습니다. 이러한 응용 프로그램의 hello 아키텍처와 작동 방식은 대부분 매우 복잡 하 고 가용성 및 성능 요구 사항을 충족 하는지 확인 하는 것이 중요 합니다.

따라서 기업은 가질 toothink 신중 하 게에 대 한 응용 프로그램에서에서 실행할 수 있습니다, 공용 클라우드 환경 hello 선택한 클라우드 공급자와 무관 합니다.

공용 클라우드 내에서 SAP NetWeaver 기반 응용 프로그램을 배포하기 위한 가능한 시스템 유형은 아래와 같습니다.

1. 중간 규모의 프로덕션 시스템
2. 개발 시스템
3. 테스트 시스템
4. 프로토타입 시스템
5. 학습/데모 시스템

순서 toosuccessfully에서 SAP 시스템에 배포할 Azure IaaS 또는 IaaS 일반적에 중요 한 toounderstand hello 중요 한 차이점이 기존 외주 업체나 호스팅 서비스 공급자의 hello 제공 및 IaaS 제공 합니다. Hello 기존 호스팅 서비스 공급자 또는 외주 업체 인프라 (네트워크, 저장소 및 서버 유형) toohello 작업 부하에 맞게 변경 하는 반면 고객이 toohost에 대신 hello 고객의 책임 toochoose hello 적절 한 작업을 IaaS 배포 합니다.

첫 번째 단계로 고객 tooverify hello 다음 항목을 필요 합니다.

* hello SAP 지원 Azure의 VM 유형
* hello SAP Azure에서 지원 되는 제품/릴리스
* hello는 Azure에서 특정 SAP 릴리스 hello에 대 한 지원 되는 OS 및 DBMS 릴리스
* 여러 다른 Azure SKU에서 제공하는 SAP 처리량

hello 답변 toothese 질문 읽을 수 SAP note에서 [1928533]합니다.

두 번째 단계로, Azure 리소스 및 대역폭 제한을 온-프레미스 시스템의 비교 toobe tooactual 리소스 소비량이 필요 합니다. 따라서 고객 필요 toobe의 hello 다양 한 기능에 잘 알고의 hello 영역에서 SAP가 지 원하는 Azure 유형을 hello:

* 여러 VM 유형의 CPU 및 메모리 리소스
* 여러 VM 유형의 IOPS 대역폭
* 여러 VM 유형의 네트워크 기능.

대부분의 데이터는 [여기(Linux)][virtual-machines-sizes-linux]와 [여기(Windows)][virtual-machines-sizes-windows]에 있습니다.

위의 hello 링크에 나열 된 제한 hello 있음을 명심 상한이 됩니다. hello 리소스에 대 한 hello 제한을, 예를 들어 IOPS 제공 될 수 있습니다 모든 상황에서이 아닙니다. hello 예외 hello 선택한 VM 유형의 CPU 및 메모리 리소스를 모두 이지만 합니다. SAP에서 지 원하는 hello VM 유형의 hello CPU 및 메모리 리소스는 예약 된 문자와 따라서 언제 든 지 사용할 수 있는 hello VM 내,

hello Microsoft Azure 플랫폼 다른 IaaS 플랫폼 처럼 다중 테 넌 트 플랫폼이입니다. 즉, 저장소, 네트워크 및 기타 리소스가 테넌트 간에 공유됩니다. 지능형 제한 및 할당량 논리가 영향 hello 다른 테 넌 트 (시끄러운 이웃) 특정에서에서 사용 되는 tooprevent 한 테 넌 트입니다. Azure의 논리 시도 대역폭에 tookeep 차이가 있지만 작은, 항상 공유 플랫폼 경향이 toointroduce 차이가 큰 편 리소스/대역폭 가용성에 사용 되는 tooin 보다 많은 고객의 온-프레미스 배포 결과적으로, 분 toominute에서 서로 다른 수준의 네트워킹 또는 저장소 I/O (hello 볼륨으로 대기 시간)에 대 한 대역폭을 발생할 수 있습니다. 온-프레미스 시스템을 Azure에서 SAP 시스템 보다 더 큰 차이 겪을 수도 있다는 hello 확률 toobe 고려를 해야 합니다.

마지막 단계는 tooevaluate 가용성 요구 사항입니다. 발생할 수 있습니다, 그리고 기본 Azure 인프라 해당 hello tooget 업데이트 되어야 하며 Vm toobe 다시 부팅을 실행 하는 hello 호스트가 필요 합니다. 이러한 경우 해당 호스트에서 실행되는 VM을 종료한 후 다시 시작할 수 있습니다. 특정 지역에 대 한 중요 하지 않은 업무 시간 동안 이와 같은 유지 관리의 hello 타이밍 이루어집니다 있지만, 비교적 긴 편 hello 잠재적인 창 컴퓨터를 다시 시작 되는 몇 시간의 발생 합니다. Hello 될 수 있는 Azure 플랫폼 내에서 다양 한 기술을 구성 toomitigate 일부 또는 모든 hello 이러한 업데이트의 영향을 하십시오. 이후 향상 기능 hello Azure 플랫폼, DBMS 및 SAP 응용 프로그램은 이러한 다시 시작의 toominimize hello 영향을 설계 합니다.

Toosuccessfully 순서로 Azure에 SAP 시스템을 배포, hello 온-프레미스 SAP 시스템 운영 체제, 데이터베이스 및 SAP 응용 프로그램 hello SAP Azure hello 리소스 hello Azure 인프라 내에 맞는 지원 매트릭스를 제공할 수 있습니다 및에 표시 되어야 합니다. 가용성 Sla Microsoft Azure에서 제공 하는 hello로 작업할 수 있습니다. 이러한 시스템을 파악 하는 대로 toodecide hello 다음 두 가지 배포 시나리오 중 하나에 필요 합니다.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>클라우드 전용-hello에 대 한 종속성 없이 Azure에 가상 컴퓨터 배포 온-프레미스 고객 네트워크
![SAP 데모 또는 학습 시나리오가 Azure에 배포된 단일 VM][planning-guide-figure-100]

이 시나리오는 단일 VM 내에서 SAP 및 기타 소프트웨어의 모든 hello 구성 요소를 설치할 학습 또는 데모 시스템에 대 한 일반입니다. 프로덕션 SAP 시스템은 이 배포 시나리오에서 지원되지 않습니다. 일반적으로이 시나리오는 hello 요구 사항을 준수를 충족 합니다.

* hello Vm 자체는 hello 공용 네트워크를 통해 액세스할 수 있습니다. Hello Vm toohello 내에서 실행 되는 hello 응용 프로그램에 대 한 네트워크에 직접 연결 온-프레미스 hello 데모 또는 학습 콘텐츠를 소유 하거나 hello 회사의 네트워크 또는 hello 고객 필요 하지 않습니다.
* Hello 교육 또는 데모 시나리오를 나타내는 여러 Vm을 발생 한 경우 네트워크 통신 및 이름 확인 hello Vm 간의 toowork가 필요 합니다. 그러나 Vm hello 집합 간의 통신 Vm의 여러 집합 간섭 없이 나란히 배포 수 있도록 격리 toobe 필요 합니다.  
* 인터넷 연결이 hello 최종 사용자 tooremote 로그인에 대 한 Azure에서 Vm 호스트 toohello에 필요 합니다. Hello 게스트 OS에 따라 RDS/터미널 서비스 또는 VNC/ssh를 사용 tooaccess hello VM tooeither hello 학습 작업을 수행 하거나 hello 데모를 수행 합니다. SAP 포트 3200, 3300 & 3600 사용할 수 있습니다 하는 경우 노출할 hello SAP 응용 프로그램 인스턴스는 모든 인터넷 연결 된 데스크톱에서 액세스할 수 있습니다.
* hello SAP 시스템 (및만 최종 사용자 액세스 하기 위해 공용 인터넷 연결 필요 하 고 연결 tooother Azure의 Vm이 필요 하지 않습니다는 Azure의 독립 실행형 시나리오 여기서 나타냅니다.
* Sap GUI 및 브라우저는 설치 되 고 hello VM에서 직접 실행 합니다.
* VM toohello 원래 상태로 빠르게 다시 새 배포 및 해당 원래 상태로 다시가 필요 합니다.
* 여러 Vm을 Active Directory에서 구현 되는 데모 및 학습 시나리오의 경우 hello / OpenLDAP 및/또는 DNS 서비스는 Vm의 각 집합에 필요 합니다.

![Azure 클라우드 서비스의 단일 데모 또는 학습 시나리오를 나타내는 VM 그룹][planning-guide-figure-200]

각각 hello VM(s) hello 염두에서 tookeep 여기서 각각의 hello 집합 hello VM 이름은 동일 hello는 필요 toobe 병렬로 배포 설정 합니다.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>크로스-프레미스-단일의 배포 또는를 Azure의 hello 온-프레미스 네트워크에 완전히 통합 되 고 hello 요구 사항에 여러 SAP Vm
![사이트 간 연결이 있는 VPN(크로스 프레미스)][planning-guide-figure-300]

이 시나리오는 가능한 여러 배포 패턴을 포함하는 크로스-프레미스 시나리오입니다. Azure에서 hello SAP 지형 온-프레미스의 일부 및 SAP 지형 hello의 다른 부분을 실행할 처럼 간단 하 게 설명할 수 있습니다. Hello SAP 구성 요소 부분은 Azure에서 실행 되는 hello 팩트의 모든 측면은 최종 사용자에 게 투명 해야 합니다. 따라서 SAP 전송 Correction System (STMS), RFC 통신, 인쇄 hello, 보안 (예: SSO) 등 Azure에서 실행 하는 hello SAP 시스템에 대 한 원활 하 게 작동 합니다. 하지만 hello 크로스-프레미스 시나리오도 여기서 hello 전체 SAP 지형 hello 고객의 도메인과 Azure에서 실행 하 고 DNS를 Azure로 확장 하는 시나리오를 설명 합니다.

> [!NOTE]
> 운영 중인 SAP 시스템을 실행 하는 데 사용할 수 있는 hello 배포 시나리오입니다.
>
>

읽기 [이 여기서] [ vpn-gateway-create-site-to-site-rm-powershell] 방법에 대 한 자세한 내용은 tooconnect 온-프레미스 tooMicrosoft Azure 네트워크

> [!IMPORTANT]
> Azure와 온-프레미스 고객 배포 간의 크로스-프레미스 시나리오에 대 한 논의 하 고 때 전체 SAP 시스템의 hello 세분성에서 찾고 있습니다. 크로스-프레미스 시나리오에서 *지원되지 않는* 시나리오는 다음과 같습니다.
>
> * 배포 방법마다 SAP 응용 프로그램의 다른 계층을 실행합니다. 예를 들어 hello DBMS 계층 온-프레미스에 있지만 hello SAP 응용 프로그램 계층 또는 그 반대로 Azure Vm으로 배포 된 Vm에서 실행 합니다.
> * SAP 계층 구성 요소 일부는 Azure에 있고, 일부는 온-프레미스에 있습니다. 예를 들어 온-프레미스와 Azure Vm 간의 hello SAP 응용 프로그램 계층의 인스턴스를 분할합니다.
> * 단일 시스템의 SAP 인스턴스를 실행하는 VM을 여러 Azure 영역에 배포하는 것은 지원되지 않습니다.
>
> 이러한 제한에 대 한 hello 설명에는 특히 hello 응용 프로그램 인스턴스 및 SAP 시스템의 hello DBMS 계층 간의 단일 SAP 시스템 내에서 대기 시간이 매우 짧아야 고성능 네트워크에 대 한 hello 요구 사항입니다.
>
>

### <a name="supported-os-and-database-releases"></a>지원되는 OS 및 데이터베이스 릴리스
* Azure Virtual Machines 서비스에 대해 지원되는 Microsoft 서버 소프트웨어는 이 문서에 나열되어 있습니다. <http://support.microsoft.com/kb/2721672>
* 지원되는 운영 체제 릴리스, SAP 소프트웨어와 연계해서 Azure 가상 컴퓨터 서비스에서 지원되는 데이터베이스 시스템 릴리스는 SAP 정보 [1928533]에 설명되어 있습니다.
* Azure 가상 컴퓨터 서비스에서 지원되는 SAP 응용 프로그램 및 릴리스는 SAP 정보 [1928533]에 설명되어 있습니다.
* 64 비트 이미지만 게스트 Vm에 Azure로 SAP 시나리오 지원된 toorun 적용 됩니다. 즉, 64비트 SAP 응용 프로그램 및 데이터베이스만 지원됩니다.

## <a name="microsoft-azure-virtual-machine-services"></a>Microsoft Azure 가상 컴퓨터 서비스
hello Microsoft Azure 플랫폼은 프로그램 인터넷 규모 클라우드 서비스 플랫폼 호스팅되며 Microsoft 데이터 센터 작동 합니다. hello 플랫폼 hello Microsoft Azure 가상 컴퓨터 서비스 (서비스 또는 IaaS 인프라)와 서비스 (PaaS) 기능으로 우수한 플랫폼 집합이 포함 되어 있습니다.

hello Azure 플랫폼 선불 기술에 대 한 hello 필요성을 줄이고 및 인프라를 구입 합니다. 유지 관리를 단순화 및 응용 프로그램을 작동 주문형 계산 및 저장소 toohost 제공 하 여 확장 및 웹 응용 프로그램 및 연결 된 응용 프로그램을 관리 합니다. 인프라 관리에는 고가용성을 위해 설계 된 플랫폼으로 자동화 된 및 동적으로 늘리는 toomatch 사용 해야 하는 hello 옵션 종 량 제 가격 모델을 사용 합니다.

![Microsoft Azure 가상 컴퓨터 서비스 위치 지정][planning-guide-figure-400]

Azure 가상 컴퓨터 서비스를 Microsoft가 있도록 toodeploy 사용자 지정 서버 이미지 tooAzure IaaS 인스턴스로 (그림 4 참조). hello Azure의 가상 컴퓨터 기반 Hyper-v 가상 하드 드라이브 (VHD)으로 되며 수 toorun 게스트 OS로 서로 다른 운영 체제.

운영 측면에서 볼 때 온-프레미스에 배포 된 가상 컴퓨터와 유사한 Azure 가상 컴퓨터 서비스에서 제공 하는 hello가 적습니다. 그러나이 필요 하지 않은 중요 한 장점 hello tooprocure, 관리 및 hello 인프라를 관리 합니다. 개발자와 관리자에는 이러한 가상 컴퓨터 내에서 hello 운영 체제 이미지의 모든 권한을 가집니다. 관리자는 toothose 가상 컴퓨터 tooperform 유지 관리 및 소프트웨어 배포 작업 뿐만 아니라 작업 문제 해결에 원격으로에 로그온 수 있습니다. 관계 toodeployment hello만 제한이 적용 되지만 Azure Vm의 hello 크기와 기능 배포는 온-프레미스에서 수행될 수 있으므로 이러한 제한이 구성에서 그리 세밀한 부분이 아닐 수 있습니다. 다음을 조합한 다양한 VM 유형을 선택할 수 있습니다.

* vCPU 수
* 메모리
* 연결할 수 있는 VHD 수
* 네트워크 및 저장소 대역폭

hello 크기와 다양 한 서로 다른 가상 컴퓨터 크기 제한인 제공 되는 테이블에 [(Linux)이이 문서] [ virtual-machines-sizes-linux] 및 [(Windows)이이 문서] [ virtual-machines-sizes-windows].

아시다시피 가상 컴퓨터에는 다양한 제품군 또는 시리즈가 있습니다. Hello 제품군 Vm에 따라 구분할 수 있습니다.

* A0-A7 VM 유형: 모든 VM이 SAP용으로 인증된 것은 아닙니다. Azure IaaS가 도입된 첫 번째 VM 시리즈입니다.
* A8-A11 VM 유형: 고성능 컴퓨팅 인스턴스. 기타 A 시리즈 VM보다 더 나은 성능의 다른 컴퓨팅 호스트에서 실행됩니다.
* D/Dv2 시리즈 VM 유형: A0-A7보다 더 나은 성능을 제공합니다. Hello VM 유형의 일부 sap에 인증 됩니다.
* DS/DSv2 시리즈 VM 유형: 유사한 tooD/Dv2 시리즈, 하지만 이며이 프리미엄 저장소 수 tooconnect tooAzure (장을 참조 [Azure 프리미엄 저장소] [ planning-guide-3.3.2] 이 문서의). 마찬가지로 모든 VM 유형이 SAP용으로 인증된 것은 아닙니다.
* G 시리즈 VM 유형: 높은 메모리 VM 유형입니다.
* GS 시리즈 VM 유형: G 시리즈과 하지만 hello 옵션 toouse Azure 프리미엄 저장소를 포함 하 여 (장을 참조 [Azure 프리미엄 저장소] [ planning-guide-3.3.2] 이 문서의). GS 시리즈 Vm을 사용 하 여 데이터베이스 서버, 경우에 DB 데이터 및 트랜잭션 로그 파일에 대 한 필수 toouse 프리미엄 저장소

다른 VM 시리즈에 hello를 동일한 CPU 및 메모리 구성을 찾을 수 있습니다. 그럼에도 불구 하 고 hello 다른 계열에서 이러한 Vm의 hello 처리량 성능을를 조회 하는 경우 이러한 상당히 다를 수 있습니다. Hello 동일 하더라도 CPU 및 메모리 구성 합니다. 이유는 hello 여러 VM 유형의 hello 도입 hello 기본 호스트 서버 하드웨어에 다른 처리량 특징을입니다.  일반적으로 처리량 성능을에 표시 된 hello 차이점은에 반영 hello의 hello 가격 다른 Vm입니다.

일부 다른 VM 시리즈 (Azure 지역 다음 장 참조)에 대 한 hello Azure 지역 중 하나를 각에 제공 될 수 있습니다. 또한 일부 VM 또는 VM 시리즈만 SAP용으로 인증되어 있습니다.

> [!IMPORTANT]
> SAP note에서 나열 된 유일한 hello 하위 집합 VM 유형 및 구성의 SAP NetWeaver 기반 응용 프로그램의 hello 용도로 [1928533] 지원 됩니다.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Azure 지역
Microsoft 이라는 ' Azure 지역 '으로 toodeploy를 가상 컴퓨터를 수 있습니다. Azure 지역은 지리적으로 근접한 하나 또는 여러 개의 데이터 센터일 수 있습니다. 대부분의 hello에 대 한 지리적 영역 hello world Microsoft에에서 두 개 이상의 Azure 지역에 있습니다. 유럽의 경우 '북유럽' 및 '유럽 서부'라는 Azure 지역이 있습니다. 특성이 나 기술적 재해 두 Azure 지역 hello에 영향을 주지 않으므로 있도록 지리적 지역 내에서 이러한 두 Azure 지역 만큼 중요 한 거리로 분리 되어 동일한 지리적 지역입니다. Microsoft에서는 서로 다른 지리적 지역에 새 Azure 영역 전체적으로 구축 꾸준히, 이후 이러한 지역 hello 수 꾸준히 성장 하 고 2015 년 12 월을 기준으로 발표 이미 추가 영역 20 Azure 영역 hello 수에 도달 합니다. 중국에서 두 hello Azure 영역을 포함 하 여 이러한 모든 지역에 SAP 시스템을 배포할 수는 고객으로 서 있습니다. Azure 지역에 대한 최신 정보를 보려면 <https://azure.microsoft.com/regions/> 웹 사이트를 참조하세요.

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>hello Microsoft Azure 가상 컴퓨터 개념
Microsoft Azure를 제공 하며 제공 된 인프라 서비스 (IaaS) 솔루션 toohost으로 가상 컴퓨터 기능이 비슷한 온-프레미스 가상화 솔루션으로 합니다. Hello Azure 포털, PowerShell 또는 CLI를 내 toocreate에서 가상 컴퓨터 수 또한 배포 및 관리 기능을 제공 하는 됩니다입니다.

Azure 리소스 관리자를 사용 하면 tooprovision 선언적 템플릿을 사용 하 여 응용 프로그램입니다. 단일 템플릿에서 여러 서비스를 해당 종속성과 함께 배포할 수 있습니다. Hello를 사용 하 여 동일한 템플릿 toorepeatedly hello 응용 프로그램 수명 주기의 다른 단계 동안 응용 프로그램을 배포 합니다.

Resource Manager 템플릿 사용에 대한 자세한 내용은 다음 항목에서 찾을 수 있습니다.

* [배포 및 Azure 리소스 관리자 템플릿 및 hello Azure CLI를 사용 하 여 가상 컴퓨터 관리] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Azure Resource Manager 및 PowerShell을 사용하여 가상 컴퓨터 관리][virtual-machines-deploy-rmtemplates-powershell]
* <https://azure.microsoft.com/documentation/templates/>

다른 흥미로운 기능은 tooprepare 특정 수 tooquickly 중인 저장소 요구 사항을 충족 하는 가상 컴퓨터 인스턴스를 배포할 수 있는 가상 컴퓨터에서 hello 기능 toocreate 이미지를입니다.

Virtual Machines에서 이미지를 만드는 방법에 대한 자세한 내용은 [이 문서(Linux)][virtual-machines-linux-capture-image-resource-manager] 및 [이 문서(Windows)][virtual-machines-windows-capture-image-resource-manager]에 있습니다.

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>장애 도메인
오류 도메인 실패 동안 실제 블레이드 나 랙을 장애 도메인 고려할 수 및 데이터 센터에 포함 된 매우 밀접 한 관련이 toohello 실제 인프라의 물리적 단위를 나타낼를 hello 두 간에 직접적인 일대일 매핑이 없습니다.

Microsoft Azure 가상 컴퓨터 서비스에서 단일 SAP 시스템의 일부분으로 여러 가상 컴퓨터를 배포할 때에 적용할 수 있습니다 hello Azure 패브릭 컨트롤러 toodeploy 함으로써 hello의 hello 요구 사항을 충족 하는 여러 장애 도메인으로 응용 프로그램 Microsoft Azure SLA 합니다. 그러나 Azure 배율 단위 (수백 대의 컴퓨터 노드 또는 저장소 노드 및 네트워킹의 컬렉션)를 통해 오류 도메인의 분포를 hello 또는 Vm tooa의 hello 할당 특정 장애 도메인은 매길 없는 직접 제어 합니다. 순서 toodirect hello Azure 패브릭 컨트롤러 toodeploy 여러 장애 도메인을 통해 Vm 집합이, tooassign Azure 가용성 집합 toohello Vm 배포 시에 필요합니다. Azure 가용성 집합에 대한 자세한 내용은 이 문서의 [Azure 가용성 집합][planning-guide-3.2.3] 장을 참조하세요.

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>업그레이드 도메인
업그레이드 도메인은 여러 Vm에서 실행 되는 SAP 인스턴스, 구성 된 SAP 시스템 내에서 VM을 업데이트 하는 방법은 toodetermine 데 도움이 되는 논리 단위를 나타냅니다. 업그레이드를 수행할 때 Microsoft Azure 이러한 업그레이드 도메인을 개별적으로 업데이트 하는 hello 과정을 진행 합니다. 배포 시에 여러 업그레이드 도메인에 VM을 분산하여 잠재적인 가동 중지 시간으로부터 SAP 시스템을 일부 보호할 수 있습니다. 서로 다른 업그레이드 도메인에 분산 하는 SAP 시스템의 hello Vm tooforce Azure toodeploy 주문에서 각 VM의 배포 시 tooset 특정 특성을 해야 합니다. 유사한 tooFault 도메인, Azure 배율 단위는 여러 업그레이드 도메인으로 구분 됩니다. 순서 toodirect hello Azure 패브릭 컨트롤러 toodeploy 서로 다른 업그레이드 도메인을 통해 Vm 집합이, tooassign Azure 가용성 집합 toohello Vm 배포 시에 필요합니다. Azure 가용성 집합에 대한 자세한 내용은 아래의 [Azure 가용성 집합][planning-guide-3.2.3] 장을 참조하세요.

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Azure 가용성 집합
단일 Azure 가용성 집합 내에서 azure 가상 컴퓨터는 Azure 패브릭 컨트롤러 hello에 의해 여러 장애 도메인과 업그레이드 도메인을 통해 배포 됩니다. hello hello 분포 통해 여러 장애 도메인과 업그레이드 도메인의 목적은 tooprevent hello 사례 인프라 유지 관리 또는 단일 장애 도메인 내에서 오류에 종료 되는 SAP 시스템의 모든 Vm입니다. 기본적으로 VM은 가용성 집합에 속하지 않습니다. 가용성 집합에 VM의 hello 참여 배포 시 또는 나중에 다시 구성 및 VM의 다시 배포 하 여 정의 됩니다.

가용성 집합 관련 tooFault 및 업그레이드 도메인에 Azure 가용성 집합 및 hello 방법을 toounderstand hello 개념 읽을 [이 문서][virtual-machines-manage-availability]

json 템플릿을 통해 ARM에 대 한 가용성 집합 toodefine 참조 [rest api 사양 hello](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) "availability"으로 검색 합니다.

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>저장소: Microsoft Azure Storage 및 데이터 디스크
Microsoft Azure 가상 컴퓨터는 다양한 저장소 유형을 활용합니다. Azure 가상 컴퓨터 서비스에서 SAP를 구현할 때는 이러한 두 가지 주요 저장소 유형 간의 중요 한 toounderstand hello 차이점은:

* 비영구 휘발성 저장소
* 영구 저장소

hello 비영구 저장소 실행 중인 가상 컴퓨터 직접 연결 된 toohello 하며 hello 계산 노드 자체 hello 로컬 인스턴스 저장소 (임시 저장소)에 있습니다. hello 크기 hello hello 배포 시작 시 선택한 가상 컴퓨터의 hello 크기에 따라 달라 집니다. 이 저장소 유형은 휘발성 이며 가상 컴퓨터 인스턴스를 다시 시작할 때 hello 디스크를 초기화 하는 따라서 합니다. 일반적으로 hello 운영 체제에 대 한 hello 페이지는이 임시 디스크에 배치 됩니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> Windows Vm에서 hello 임시 드라이브는 배포 된 VM의 D:\ 드라이브로 탑재 됩니다.
>
> ![Linux][Logo_Linux] Linux
>
> Linux VM에서는 /mnt/resource 또는 /mnt로 탑재됩니다. 자세한 내용은 다음 항목을 참조하세요.
>
> * [어떻게 tooAttach 데이터 디스크 tooa Linux 가상 컴퓨터][virtual-machines-linux-how-to-attach-disk]
> * <https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux#temporary-disk>
>
>

- - -
hello 실제 드라이브는 hello 호스트 서버 자체에 저장 되므로 휘발성입니다. 배포 시에서 hello VM 이동 하는 경우 (예: hello 호스트 또는 종료 및 다시 시작에 due toomaintenance) hello 드라이브 hello 내용이 손실 됩니다. 따라서 아니므로 옵션 toostore이이 드라이브에 중요 한 데이터입니다. 2015 년 6 월을 기준으로 같이 표시 하는 매우 다양 한 성능 특징을 가진 다른 VM 시리즈 간의 hello이이 유형의 저장소에 사용 되는 미디어 유형의 마다 다릅니다.

* A5-A7: 매우 제한된 성능. 페이지 파일 이외의 다른 항목에는 권장되지 않습니다.
* A8-A11: 매우 양호한 성능(수 만 IOPS 및 1GB/초 이상의 처리량)
* D 시리즈: 매우 양호한 성능(수 만 IOPS 및 1GB/초 이상의 처리량)
* DS 시리즈: 매우 양호한 성능(수 만 IOPS 및 1GB/초 이상의 처리량)
* G 시리즈: 매우 양호한 성능(수 만 IOPS 및 1GB/초 이상의 처리량)
* GS 시리즈: 매우 양호한 성능(수 만 IOPS 및 1GB/초 이상의 처리량)

위의 문을 sap에 인증 된 toohello VM 유형에 적용 하는 합니다. 일부 DBMS 기능 사용 하 여 뛰어난 IOPS 및 처리량 VM 시리즈 hello 활용 하는 방법에 대 한 한정 합니다. 자세한 내용은 참조 hello [DBMS 배포 가이드][dbms-guide]합니다.

Microsoft Azure 저장소 지속형 저장소 및 hello 일반적인 수준 보호 및 SAN 저장소에 중복성을 제공 합니다. Azure 저장소에 따라 디스크는 hello Azure 저장소 서비스에 있는 가상 하드 디스크 (Vhd). hello 로컬 OS 디스크 (Windows c:\, Linux/개발/sda1) hello Azure 저장소에 저장 된 추가 볼륨/디스크 탑재 된 toohello VM 가져오기 너무 저장 하는, 및입니다.

가능한 tooupload 기존 VHD를 온-프레미스 또는 Azure 내에서 빈 컨테이너를 만들 사용 되며 해당 toodeployed Vm을 연결 합니다.

를 작성 하거나 Azure 저장소로 VHD 업로드 후 가능한 toomount 되며 기존 가상 컴퓨터 및 VHD 되지 않은 기존 toocopy 해당 tooan 연결 합니다.

해당 VHD는 지속되므로 해당 VHD 내의 데이터 및 변경 내용은 재부팅한 후 가상 컴퓨터 인스턴스를 다시 만들어도 안전하게 유지됩니다. 인스턴스를 삭제 하는 경우에 이러한 Vhd 안전 하 게 유지 하 고 다시 배포할 수 있으며 또는 비-OS 디스크의 경우 탑재 된 tooother Vm 수 있습니다.

Hello 내에서 Azure 저장소 중복 서로 다른 수준의 네트워크를 구성할 수 있습니다.

* 선택할 수 있는 최소 수준 '로컬 '는 놀랄 hello 내 hello 데이터의 해당 toothree 복제본은 동일한 데이터 센터의 Azure 지역 (장을 참조 [Azure 지역][planning-guide-3.1]).
* 영역 중복 저장소를 내에서 여러 데이터 센터를 통해 확산 hello 3 이미지 hello 같은 Azure 지역입니다.
* 기본 중복성 수준은 hello에서 호스팅되는 다른 Azure 지역에 hello 데이터의 세 가지 다른 이미지로 hello 콘텐츠를 비동기적으로 복제 지리적 중복성을 동일한 지리적 지역입니다.

또한 hello 다른 중복 옵션에 대 한이 문서의 맨 위에 hello 표를 참조: <https://azure.microsoft.com/pricing/details/storage/>

Azure Storage에 관한 자세한 내용은 다음 항목에서 찾을 수 있습니다.

* <https://azure.microsoft.com/documentation/services/storage/>
* <https://azure.microsoft.com/services/site-recovery>
* <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview.aspx>

#### <a name="azure-standard-storage"></a>Azure 표준 저장소
Azure 표준 저장소 Azure IaaS 릴리스 되었을 때 사용할 수 있는 저장소의 hello 유형의 했습니다. 이 저장소에서는 IOPS 할당량이 단일 디스크 단위로 적용되었습니다. 대기 시간 hello 일반적으로 배포 된 SAN/NAS 장치를 고성능 SAP 시스템에 대 한 온-프레미스 호스트 동일한 클래스에 없습니다. Azure 표준 저장소를 수백 대 한 충분 한 입증 하는 hello 그럼에도 불구 하 고 그 동안 Azure에 배포 된 SAP 시스템입니다.

표준 저장소 계정은 Azure에 저장 되어 있는 디스크 hello 실제 데이터는 저장 된 hello 볼륨의 저장소 트랜잭션, 아웃 바운드 데이터 전송 및 중복성 옵션 선택에 따라 요금이 청구 됩니다. Hello 최대 1 t B의 크기에 많은 디스크를 만들 수 있지만 빈 상태로 유지 하는 것으로 비용이 부과 되지 않습니다. 그런 다음 각 100gb VHD를 채우지 hello 표준 크기 hello와 VHD를 만든 아닌와 100GB 저장 하기 위한 요금이 청구 됩니다.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Azure 프리미엄 저장소
2015년 4월 Microsoft는 Azure Premium Storage를 도입했습니다. 프리미엄 저장소 hello 목표 tooprovide로 도입 된:

* 더 나은 I/O 대기 시간
* 향상된 처리량
* 변동이 작은 I/O 대기 시간

이 위해 대부분의 변경 내용은 어떤 hello의 가장 중요 한 두 가지는:

* Azure 저장소 노드 hello에에서 SSD 디스크 사용
* 지 원하는 새 읽기 캐시 hello Azure 계산 노드의 로컬 SSD

기능 변경 되지 않은 반대 tooStandard 저장소 hello 디스크 (또는 VHD) hello 크기에 따라 달라 프리미엄 저장소 현재에이 문서에 표시 된 대로 세 개의 서로 다른 디스크 범주: <https://azure.microsoft.com/ 가격 책정/세부 정보/저장/관리 되지 않는-디스크 />

IOPS/디스크 및 디스크 처리량/디스크 hello 디스크의 hello 크기 범주에 종속 되어 있는지 표시

Hello 경우 프리미엄 저장소의 비용된으로 이러한 disks 이지만 이러한 디스크의 hello 양이 hello 디스크 내에 저장 된 hello 데이터의 독립적인 hello 크기 범주에 저장 된 hello 실제 데이터 볼륨 않습니다.

표시 된 hello 크기 범주에 직접 매핑하는 프리미엄 저장소에 디스크를 만들 수도 있습니다. 프리미엄 저장소에 표준 저장소에서 디스크를 복사 하는 경우에 특히 hello 사례 수 있습니다. 이러한 경우에는 매핑 toohello 다음 가장 큰 프리미엄 저장소 디스크 옵션 수행 됩니다.

특정 VM 시리즈 hello Azure 프리미엄 저장소에서에서 이용할 수 있도록 알아야 합니다. 2015 년 12 월을 기준으로 hello DS-및 GS 시리즈 이들은입니다. DS 시리즈 hello는 기본적으로 hello 동일 DS 시리즈 hello 기능 toomount 프리미엄 저장소에 있는지 hello 예외로 D 시리즈 Vm 기반 또한 toodisks 표준 저장소를 Azure에 호스트 되는 합니다. 동일한 작업 G 시리즈 비교 tooGS 계열에 대해 유효합니다.

경우 체크 아웃 하는 hello 부분에 있는 hello DS 시리즈 Vm의 [(Linux)이이 문서] [ virtual-machines-sizes-linux] 및 [(Windows)이이 문서][virtual-machines-sizes-windows]를 보면 VM 수준 hello hello 단위로 데이터 볼륨 제한 사항 tooPremium 저장소 디스크가 있는지입니다. 다른 DS 시리즈 또는 GS 시리즈 Vm에 탑재할 수 있는 데이터 디스크에 대 한 예정 toohello 수 다양 한 제한 사항가지고 있습니다. 이러한 제한도 위에서 언급 한 hello 문서에 설명 되어 있습니다. 하지만, 예를 들어 32 x P30 디스크 tooa를 탑재 하는 경우 단일 DS14 VM 얻을 수 있다는 없습니다 32 배 P30 디스크의 최대 처리량 hello 의미 본질적으로 합니다. Hello 문서 제한 데이터 처리량에 설명 된 대로 VM 수준에서 최대 처리량을 hello 대신 합니다.

프리미엄 Storage에 대한 자세한 내용은 <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>에서 찾을 수 있습니다.

#### <a name="c55b2c6e-3ca1-4476-be16-16c81927550f"></a>관리 디스크
Managed Disks는 Azure Storage 계정에 저장된 VHD 대신 사용할 수 있는 Azure Resource Manager의 새로운 리소스 종류입니다. 관리 되는 디스크는 hello 가상 컴퓨터의 가용성 집합 연결 tooand 따라서 가상 컴퓨터와 hello 가상 컴퓨터에서 실행 되는 hello 서비스의 hello 가용성 향상 hello로 자동으로 맞춥니다. 자세한 내용은 hello 읽을 [개요 문서](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview)합니다.

가상 컴퓨터의 hello 배포 및 관리를 단순화 하기 위해 때문에 tooyou 사용 하 여 관리 되는 디스크를 권장 합니다.
SAP는 현재 Premium Managed Disks만 지원합니다. 자세한 내용은 SAP Note [1928533]을 참조하세요.

#### <a name="azure-storage-accounts"></a>Azure 저장소 계정
Azure에서 서비스 또는 VM을 배포할 때 VHD 및 VM 이미지의 배포는 Azure Storage 계정이라는 단위로 구성할 수 있습니다. Toocarefully 해야 Azure 배포를 계획할 때는 Azure의 hello 제한을 고려 합니다. Hello 한쪽에 Azure 구독 당 저장소 계정 제한 수가입니다. Hello에 제한이 고정된 되어 있지만 각 Azure 저장소 계정은 많은 수의 VHD 파일을 저장할 수, 총 저장소 계정당 IOPS입니다. 많은 I/O 호출을 만드는 DBMS 시스템과 수백 개의 SAP Vm을 배포할 때는 여러 Azure 저장소 계정 간에 높은 IOPS DBMS Vm toodistribute 것이 좋습니다. 주의 해야 tooexceed hello 현재 제한 안 Azure 저장소 계정 구독 당 합니다. 이 개념은 이미 참조 하는 hello에서 더 자세하게 설명 저장소 SAP 시스템에 대 한 hello 데이터베이스 배포의 필수 요소 이므로 [DBMS 배포 가이드][dbms-guide]합니다.

Azure Storage 계정에 대한 자세한 내용은 [이 문서][storage-scalability-targets]에 있습니다. 이 문서의 내용을 보면는 Azure 저장소 계정 표준 및 프리미엄 저장소 계정 간에 hello 제한 사항에 차이가 있습니다. 주요 차이점은 저장소 계정 내에 저장할 수 있는 데이터의 hello 볼륨입니다. 표준 저장소 hello 볼륨이 프리미엄 저장소 보다 큰 크기를입니다. 다른 쪽에서는 표준 저장소 계정을 hello hello에서 심각 하 게 hello Azure 프리미엄 저장소 계정에는 이러한 제한이 있지만 iop (열 ' 총 요청 속도입니다. ' 참조), 제한 됩니다. SAP 시스템, 특히 DBMS 서버 hello hello 배포를 설명할 때 세부 정보 및 결과 이러한 차이를 설명 합니다.

저장소 계정 내에서 구성 하 고 다른 Vhd 분류 hello 목적을 위해 hello 가능성 toocreate 다른 컨테이너가 있을 수 있습니다. 이러한 컨테이너는 일반적으로 다른 VM의 VHD를 분리하는 등의 용도로 사용됩니다. 단일 Azure 저장소 계정 아래에서 컨테이너를 하나만 사용하거나 여러 개를 사용할 경우 성능상의 문제는 없습니다.

Azure 내에서 VHD 이름 hello tooprovide hello Azure 내에서 VHD에 대 한 고유한 이름을 필요한 명명 연결 뒤를 따릅니다.

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

위에 언급 한 hello 문자열로 toouniquely hello Azure 저장소에 저장 된 VHD를 식별 해야 합니다.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Microsoft Azure 네트워킹
Microsoft Azure hello 매핑 원하는 모든 시나리오를 허용 하는 네트워크 인프라를 제공 toorealize SAP 소프트웨어와 함께 합니다. hello 기능이 됩니다.

* Windows 터미널 서비스 또는 ssh/VNC Vm toohello 직접 외부 hello에 대 한 액세스
* 액세스 tooservices 및 hello Vm 내에서 응용 프로그램에서 사용 하는 특정 포트
* Azure VM으로 배포된 VM 그룹 간의 내부 통신 및 이름 확인
* 고객의 온-프레미스 네트워크와 hello Azure 네트워크 간에 크로스-프레미스 연결
* Azure 지역 간 연결 또는 Azure 사이트 간 데이터 센터 연결

자세한 내용은 <https://azure.microsoft.com/documentation/services/virtual-network/>에서 찾을 수 있습니다.

많은 다양 한 작업이 tooconfigure 이름 및 Azure의 IP 확인 됩니다. 이 문서에서 클라우드 전용 시나리오 hello 기본 Azure DNS를 사용 하 여 (대비 toodefining에서는 자체 DNS 서비스)에 의존 합니다. 사용자 고유의 DNS 서버를 설정하는 대신 사용할 수 있는 새 Azure DNS 서비스도 있습니다. 자세한 내용은 [이 문서][virtual-networks-manage-dns-in-vnet] 및 [이 페이지](https://azure.microsoft.com/services/dns/)에 있습니다.

크로스-프레미스 시나리오에 대 한 hello 팩트에 의존 하는 hello 온-프레미스 AD/OpenLDAP/DNS가 VPN 또는 개인 연결 tooAzure를 통해 확장 합니다. 특정 시나리오 여기에 설명 된 대로 것 필요한 toohave Azure에 설치 되는 AD/OpenLDAP 복제본.

네트워킹 및 이름 확인은 SAP 시스템에 대 한 hello 데이터베이스 배포의 필수 요소,이 개념 hello에 보다 자세히 설명 되어 [DBMS 배포 가이드][dbms-guide]합니다.

##### <a name="azure-virtual-networks"></a>Azure 가상 네트워크
Azure 가상 네트워크를 만들어서 Azure DHCP 기능에 의해 할당 hello 개인 IP 주소 hello 주소 범위를 정의할 수 있습니다. 크로스-프레미스 시나리오에서 정의 된 hello IP 주소 범위 계속 할당 되는 DHCP를 사용 하 여 Azure에서. 그러나 도메인 이름 확인 온-프레미스 (hello Vm은 온-프레미스 도메인의 일부는 가정)를 수행 하 고 따라서 서로 다른 Azure 클라우드 서비스 이외의 주소를 확인할 수 있습니다.

Azure 요구 toobe 모든 가상 컴퓨터가 tooa 가상 네트워크를 연결 합니다.

자세한 내용은 [이 문서][resource-groups-networking] 및 [이 페이지](https://azure.microsoft.com/documentation/services/virtual-network/)에 있습니다.

[comment]: <> (Hello OpenLDAP 항목 + ARM; 포함 하는 아티클을 찾을 MShermannd 할 일 수 없습니다.)
[comment]: <> (MSSedusch - <https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> VM을 배포한 후 기본적으로 가상 네트워크 구성을 hello를 변경할 수 없습니다. hello TCP/IP 설정은 toohello Azure DHCP 서버를 유지 해야 합니다. 기본 동작은 동적 IP 할당입니다.
>
>

hello hello 가상 네트워크 카드의 MAC 주소가 변경 될 수 있습니다, 예를 들어 다음 크기 조정 및 hello Windows 또는 Linux 게스트 OS hello 새 네트워크 카드를 선택 하 고이 경우 DHCP tooassign hello IP 및 DNS 주소를 자동으로 사용 합니다.

##### <a name="static-ip-assignment"></a>고정 IP 할당
가능한 tooassign 고정 또는 예약 된 IP 주소는 Azure 가상 네트워크 내에서 tooVMs 합니다. Azure 가상 네트워크에서 실행 중인 hello Vm이이 기능에서 필요한 경우 일부 시나리오에 필요한 훌륭한 가능성 tooleverage 열립니다. hello IP 할당 hello hello VM의 실행 여부 및 종료에 관계 없이 VM의 hello 존재 전체에서 유효 합니다. 결과적으로, tootake 필요한 hello 가상 네트워크에 대 한 hello 범위의 IP 주소를 정의할 때 계정에 Vm (실행 중 / 중지 된 VM)의 전체 수 hello 합니다. hello VM 및 네트워크 인터페이스 삭제 될 때까지 또는 hello IP 주소를 다시 할당 취소 될 때까지 hello IP 주소 할당 된 상태로 유지 됩니다. 자세한 내용은 [이 문서][virtual-networks-static-private-ip-arm-pportal]를 참조하세요.

##### <a name="multiple-nics-per-vm"></a>VM당 여러 NIC
Azure 가상 컴퓨터에 대해 여러 개의 vNIC(가상 네트워크 인터페이스 카드)를 정의할 수 있습니다. 여러 vNICs을 hello 기능 toohave와 tooset where, 예를 들어 하나의 vNIC를 통해 클라이언트 트래픽이 라우팅됩니다 및 백 엔드 트래픽은 두 번째 vNIC 통해 라우팅됩니다 네트워크 트래픽 구분을 시작할 수 있습니다. VM에서 서로 다른 제한 사항이 유형의 hello에 의존 하는 toohello 수가 vNICs 인식 합니다. 정확한 세부 정보, 기능 및 제한 사항은 다음 문서에서 찾을 수 있습니다.

* [여러 NIC가 있는 Windows VM 만들기][virtual-networks-multiple-nics-windows]
* [여러 NIC가 있는 Linux VM 만들기][virtual-networks-multiple-nics-linux]
* [템플릿을 사용하여 다중 NIC VM 배포][virtual-network-deploy-multinic-arm-template]
* [PowerShell을 사용하여 다중 NIC VM 배포][virtual-network-deploy-multinic-arm-ps]
* [Hello Azure CLI를 사용 하 여 다중 NIC Vm 배포][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>사이트 간 연결
크로스-프레미스에서는 투명한 영구 VPN 연결을 사용하여 Azure VM과 온-프레미스가 연결되어 있습니다. 것은 예상된 toobecome hello 가장 일반적인 SAP 배포 패턴 Azure 에서입니다. hello 가정 운영 절차와 Azure의 SAP 인스턴스를 사용 하 여 프로세스 투명 하 게 작동 하는입니다. 즉, 있습니다 해야 이러한 시스템에서 수 tooprint 수 뿐만 아니라 SAP Transport Management System (TMS) tootransport 개발 시스템에서 온-프레미스 배포 Azure tooa 테스트 시스템에 변경 하는 hello를 사용 합니다. 사이트 간 연결에 대한 추가 설명서는 [이 문서][vpn-gateway-create-site-to-site-rm-powershell]에 있습니다.

##### <a name="vpn-tunnel-device"></a>VPN 터널 장치
사이트 간 연결 (온-프레미스 데이터 센터 tooAzure 데이터 센터) toocreate 순서, tooeither 필요를 얻고 VPN 장치를 구성 하거나 라우팅 및 원격 액세스 서비스 (RRAS) 도입 된 Windows server 소프트웨어 구성 요소 사용 2012입니다.

* [PowerShell을 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기][vpn-gateway-create-site-to-site-rm-powershell]
* [사이트 간 VPN Gateway 연결을 위한 VPN 장치 정보][vpn-gateway-about-vpn-devices]
* [VPN Gateway FAQ][vpn-gateway-vpn-faq]

![온-프레미스와 Azure 간의 사이트 간 연결][planning-guide-figure-600]

hello 위의 그림에서는 두 개의 Azure 구독이 있는 Azure의 가상 네트워크 사용에 대 한 예약 된 IP 주소 하위 범위를 보여 줍니다. hello에서 hello 연결 온-프레미스 네트워크 tooAzure VPN을 통해 설정 됩니다.

#### <a name="point-to-site-vpn"></a>지점 및 사이트 간 VPN
지점-사이트 VPN Azure에 모든 클라이언트 컴퓨터 tooconnect 자체 VPN으로 필요합니다. Hello SAP 시나리오를 살펴보고, 지점 및 사이트 연결은 바람직하지 않습니다. 따라서 추가 참조가 없는 toopoint-사이트 VPN 연결을 제공 됩니다.

자세한 내용은 다음 항목에 있습니다.
* [지점 및 사이트 연결 tooa VNet을 구성 합니다. Azure 포털 hello를 사용 하 여](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
* [지점 및 사이트 연결 tooa VNet 구성 PowerShell을 사용 하 여](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

#### <a name="multi-site-vpn"></a>다중 사이트 VPN
또한 이제 azure 단일 Azure 구독에 대 한 hello 가능성 toocreate 다중 사이트 VPN 연결을 제공합니다. 이전에 단일 구독 제한 tooone 사이트 간 VPN 연결 했습니다. 이 제한은 단일 구독에 대한 다중 사이트 VPN 연결을 통해 해결되었습니다. 따라서 크로스-프레미스 구성을 통해 특정 구독에 대 한 Azure 지역 둘 이상의 가능한 tooleverage 있습니다.

추가 설명서는 [이 문서][vpn-gateway-create-site-to-site-rm-powershell]를 참조하세요.

[comment]: <> (MShermannd TODO - ARM 문서 링크가 없습니다.)

#### <a name="vnet-toovnet-connection"></a>VNet tooVNet 연결
다중 사이트 VPN을 사용 하 여 각 hello 지역에 별도 Azure 가상 네트워크 tooconfigure를 해야 합니다. 그러나 경우가 매우 자주 hello 다른 지역에 hello 소프트웨어 구성 요소를 서로 통신 해야 하는 hello 요구를 해야 합니다. 이상적으로 이러한 통신 해야 라우팅되지 없어 toohello와 하나의 Azure 지역 tooon 온-프레미스에서 다른 Azure 지역입니다. tooshortcut, Azure 제공 hello 가능성 tooconfigure에서 하나의 Azure 가상 네트워크 하나 지역 tooanother 다른 영역에서 호스트 되는 Azure 가상 네트워크에에서 연결 합니다. 이 기능을 VNet 간 연결이라고 합니다. 이 기능에 대한 자세한 내용은 <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>에서 찾을 수 있습니다.

#### <a name="private-connection-tooazure--expressroute"></a>개인 연결 tooAzure-express 경로
Microsoft Azure express 경로 또는 공동 배치 환경 어느 hello 고객의 온-프레미스 인프라와 Azure 데이터 센터 간에 개인 연결 hello 만들기를 허용 합니다. 다양한 MPLS(패킷 전환) VPN 공급자 또는 기타 네트워크 서비스 공급자에서 Express 경로를 제공합니다. ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. ExpressRoute 연결은 hello 인터넷 보다 보안성이 높으며, 더 안정적이 여러 병렬 회로, 빨라진 속도 및 일반 연결 보다 더 낮은 대기 시간을 제공합니다.

Azure Express 경로 및 제공 서비스에 대한 자세한 내용은 여기에서 찾을 수 있습니다.

* <https://azure.microsoft.com/documentation/services/expressroute/>
* <https://azure.microsoft.com/pricing/details/expressroute/>
* <https://azure.microsoft.com/documentation/articles/expressroute-faqs/>

Express 경로는 여기에 설명된 것처럼 단일 Express 경로 회로를 통해 여러 Azure 구독을 가능하게 합니다.

* <https://azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://azure.microsoft.com/documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>크로스 프레미스 강제 터널링
사이트 간, 지점 및 사이트 간 또는 express 경로 통해 온-프레미스 도메인에 가입 된 Vm을 위한 모든 hello 사용자도 해당 Vm에 대 한 hello 인터넷 프록시 설정이 배포 되는지를 있는지 있는지 toomake를 해야 합니다. 기본적으로 해당 Vm 또는 브라우저 tooaccess hello 인터넷 hello 회사 프록시를 통과 하지는 않지만 Azure toohello 통해 직접 연결 하는 것을 사용 하 여 사용자에서 실행 되는 소프트웨어 인터넷 합니다. 짝수 hello 프록시 설정 되지 않은 hello 회사 프록시를 통해 100% 솔루션 toodirect hello 트래픽 hello 프록시에 대 한 소프트웨어 및 서비스 toocheck의 책임에 있기 때문입니다. 인터넷 트래픽이 toohello 다시 우회 수 hello VM에서에서 실행 되는 소프트웨어는 수행 되지 않습니다. 관리자가 hello 설정을 조작, Azure toohello 인터넷을 통해 직접 합니다.

이 tooavoid 순서, 온-프레미스와 Azure 간의 사이트 간 연결으로 강제 터널링를 구성할 수 있습니다. hello hello 강제 터널링 기능에 대 한 자세한 설명을 게시 여기 <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

ExpressRoute에서 강제 터널링 hello ExpressRoute BGP를 통해 기본 경로 보급 하는 고객으로 활성화 되어 피어 링 세션입니다.

#### <a name="summary-of-azure-networking"></a>Azure 네트워킹 요약
이 장에서는 Azure 네트워킹에 대한 여러 가지 중요 사항이 포함되어 있습니다. 다음은 hello 주 항목에 대 한 요약이입니다.

* Azure 가상 네트워크 tooset tooyour 고유의 요구에 따라 hello 네트워크를 통해
* Azure 가상 네트워크 IP 주소 범위 tooVMs tooassign 사용된 하거나 고정된 IP 주소 tooVMs 할당 수 있습니다.
* 사이트 간 또는 지점 및 사이트 연결 toocreate Azure 가상 네트워크를 먼저 필요한을 tooset
* 가상 컴퓨터가 배포 된 것이 더 이상 가상 네트워크에 할당할 toohello VM 가능한 toochange hello

### <a name="quotas-in-azure-virtual-machine-services"></a>Azure 가상 컴퓨터 서비스의 할당량
에서는 필요한 toobe hello 팩트에 대 한 hello 저장소 지우고 네트워크 인프라 hello Azure 인프라의에서 다양 한 서비스를 실행 하는 Vm 간에 공유 됩니다. 알아본 hello 고객의 데이터 센터에서와 마찬가지로 과다 hello 인프라 리소스 중 일부는 내부 tooa 정도 하십시오. Microsoft Azure 플랫폼 hello 디스크, CPU, 네트워크 및 기타 할당량 toolimit hello 리소스 소비 및 toopreserve 일관성 있고 명확한 성능을 사용합니다.  hello 다른 VM 유형 (예: A5, A6, 등) hello 디스크 수, CPU, RAM에 대 한 할당량이 각기 다릅니다 및 네트워크 합니다.

> [!NOTE]
> SAP에서 지 원하는 hello VM 유형의 CPU 및 메모리 리소스 hello 호스트 노드에서 미리 할당 됩니다. 이 hello VM을 배포한 후 hello 리소스 hello 호스트에는 VM 유형 hello에 정의 된 대로 사용할 수 있는 것을 의미 합니다.
>
>

계획 및 Azure 솔루션에 SAP 크기 조정 각 가상 컴퓨터 크기에 대 한 할당량을 hello 때 고려해 야 합니다. hello VM 할당량 설명 [여기 (Linux)] [ virtual-machines-sizes-linux] 및 [여기 (Windows)][virtual-machines-sizes-windows]합니다.

설명 하는 hello 할당량 hello 이론적인 최대값을 나타냅니다.  디스크당 hello 제한인 IOPS 작은 io (8kb) 수행할 수 있습니다 하지만 되었을 수 있습니다 크지 큰 Io (1mb)으로.  hello IOPS 제한은 단일 디스크의 hello 세분성에 적용 됩니다.

대략적인 의사 결정 트리 toodecide 여부나 기존 시스템을 Azure에 주문 toodeploy hello 시스템에서 다르게 구성할 toobe 필요 여부는 SAP 시스템이 Azure 가상 컴퓨터 서비스와 기능에 채택 된 아래의 hello 의사 결정 트리 사용 설정할 수 있습니다.

![의사 결정 트리 toodecide 기능 toodeploy Azure의 SAP][planning-guide-figure-700]

**1 단계**: hello와 가장 중요 한 정보 toostart은 지정된 된 SAP 시스템에 대 한 hello SAPS 요구 사항입니다. 경우에 SAP 시스템 hello 이미 hello DBMS 부분과 hello SAP 응용 프로그램 부분으로 구분 하는 hello SAPS 요구 사항을 필요 toobe 2 계층 구성에서 온-프레미스를 배포 합니다. 기존 시스템의 경우 사용 중인 하드웨어 toohello 종종 결정 하거나 수 예상 SAPS와 관련 된 hello 기존 SAP 벤치 마크에 기초 합니다. hello 결과 볼 수 있습니다: <http://global.sap.com/campaigns/benchmark/index.epx>합니다.
새로 배포 된 SAP 시스템에 대 한 hello 시스템의 hello SAPS 요구 사항을 결정 해야 하는 크기 조정 연습 벗어났는지 해야 합니다.
Azure의 SAP 크기 조정에 대해서는 블로그 <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx> 및 첨부된 문서를 참조하세요.

**2 단계**: 기존 시스템에 대 한 I/O 볼륨 hello 및 hello DBMS 서버의 초당 I/O 작업을 측정 해야 합니다. 새로 계획된 하는 시스템에 대 한도 실습 hello 새 시스템에 대 한 크기 조정 하는 hello hello DBMS 측면 대략적 hello I/O 요구를 제공 해야 합니다. 를 알 수 없는 경우 결국 tooconduct 개념 증명 해야 합니다.

**3 단계**: 비교 hello SAPS 요구 사항을 hello DBMS 서버와 Azure의 hello SAPS hello 각 VM 유형이 제공할 수 있습니다. hello 여러 Azure VM 유형의 SAPS에 hello 내용은 SAP Note에서 설명 [1928533]합니다. hello 포커스 hello DBMS VM에 먼저 되므로 되어야 hello 데이터베이스 계층은 규모가 확장 되지 않는 hello 대부분의 배포에서의 SAP NetWeaver 시스템을 hello 계층입니다. 반면 SAP 응용 프로그램 계층 hello 확장할 수 있습니다. Hello SAP 지원 Azure VM 유형에 필요한 hello SAPS를 제공할 수 있는, Azure에서 계획 된 hello SAP 시스템의 hello 작업을 실행할 수 없습니다. 내보내도록 toodeploy hello 시스템 온-프레미스 또는 hello 시스템 toochange hello 작업 볼륨 사용 해야 합니다.

**4단계**: [여기(Linux)][virtual-machines-sizes-linux]와 [여기(Windows)][virtual-machines-sizes-windows]서 설명하는 대로 Azure에서는 사용자가 Standard Storage 또는 Premium Storage 중 어느 것을 사용하든지 간에 디스크당 IOPS 할당량을 적용합니다. VM 유형 hello에 종속, 탑재할 수 있는 데이터 디스크의 hello 수가 달라 집니다. 결과적으로, 각각 hello 여러 VM 유형의 얻을 수 있는 최대 IOPS 값을 계산할 수 있습니다. Hello 데이터베이스 파일 레이아웃에 종속, hello 게스트 운영 체제에서에서 toobecome 하나의 볼륨 디스크를 스트라이프 할 수 있습니다. 그러나 배포 된 SAP 시스템의 hello 현재 IOPS 볼륨이 Azure와 메모리가 더 많은 기회가 toocompensate 없는 경우 hello 가장 큰 VM 유형의 계산 hello 제한을 초과 하는 경우 hello 작업이 hello SAP 시스템의 있습니다 수 영향을 받지 심각 하 게 합니다. 이러한 경우에는 지점 hello Azure 시스템에서 배포 하면 안 되는 위치를 누르면 수 있습니다.

**5 단계**: SAP 시스템에서 특히 2 계층 구성에서 온-프레미스를 배포 하는, hello 확률이 hello 시스템 toobe 3 계층 구성에서 Azure에 구성 된 할 수 있습니다. 이 단계에에서 있는지 여부는 구성 요소를 확장할 수 없습니다 및 hello CPU 및 메모리 리소스에는 다른 Azure VM 유형 혜택 hello에 적합 하지 않은 hello SAP 응용 프로그램 계층 toocheck이 필요 합니다. 실제로 이러한 구성 요소에 있으면 hello SAP 시스템과 해당 작업을 Azure에 배포할 수 없습니다. 하지만 여러 Azure Vm에 hello SAP 응용 프로그램 구성 요소를 확장할 수 있습니다, hello 시스템을 Azure에 배포 될 수 있습니다.

**6 단계**: hello DBMS 및 SAP 응용 프로그램 계층 구성 요소를 Azure Vm에서 실행할 수 있습니다, hello 구성 toobe와와 관련 하 여 정의 해야 합니다.

* Azure VM의 수
* Hello 개별 구성 요소에 대 한 VM 유형
* DBMS VM tooprovide Vhd 수가 충분 한 IOPS

## <a name="managing-azure-assets"></a>Azure 자산 관리
### <a name="azure-portal"></a>Azure 포털
hello Azure 포털에는 세 가지 인터페이스 toomanage Azure VM 배포 중 하나입니다. hello Azure 포털을 통해 이미지에서 Vm을 배포 하는 등의 hello 기본 관리 작업을 수행할 수 있습니다. 또한 저장소 계정, 가상 네트워크 만들기를 hello 및 기타 Azure 구성 요소는 또한 작업 hello Azure 포털 효율적으로 처리할 수 있습니다. 그러나 온-프레미스 tooAzure에서 Vhd를 업로드 하거나 Azure 내에서 VHD를 복사할 등과 같은 기능을 가지 타사 도구 또는 PowerShell 또는 CLI를 통해 관리 해야 하는 작업입니다.

![Microsoft Azure Portal - 가상 컴퓨터 개요][planning-guide-figure-800]

[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Hello 가상 컴퓨터 인스턴스에 대 한 관리 및 구성 작업 hello Azure 포털 내에서 수행할 수 있습니다.

외에도 다시 시작 하 고 가상 컴퓨터 종료 수 연결, 분리 및 toocapture hello 인스턴스의 이미지 준비에 대 한 hello 가상 컴퓨터 인스턴스용 데이터 디스크를 만들 있고 hello 크기 hello 가상 컴퓨터 인스턴스를 구성 합니다.

Azure 포털 hello toodeploy 기본 기능을 제공 하 고 Vm 및 기타 여러 Azure 서비스를 구성 합니다. 그러나 모두 사용할 수 없음 기능 hello Azure 포털 적용 됩니다. 에서는 Azure 포털 hello 되는 등의 가능한 tooperform 작업:

* TooAzure Vhd를 업로드 하는 중
* VM 복사

[comment]: <> (MShermannd TODO - SAP VM에 대한 자동화 서비스는 어떻습니까?)
[comment]: <> (MSSedusch - 가능한 한 여러 VM 배포)
[comment]: <> (MSSedusch도 모든 종류의 배포에 대 한 자동화 hello Azure 포털으로 수는 없습니다. 여러 Vm의 스크립트 배포 등의 작업 hello Azure 포털을 통해 수는 없습니다.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Microsoft Azure PowerShell cmdlet을 통한 관리
Windows PowerShell은 Azure에서 많은 수의 시스템을 배포하는 고객에 의해 널리 채택되어온 강력하고 확장 가능한 프레임워크입니다. 데스크톱, 랩톱 또는 전용된 관리 스테이션에 PowerShell cmdlet의 hello 설치 후 hello PowerShell cmdlet을 원격으로 실행할 수 있습니다.

프로세스 tooenable hello Azure PowerShell cmdlet 사용에 대 한 로컬 데스크톱/랩톱 hello 및 구독에서 설명 하는 방법을 사용 하 여 사용에 대 한 hello tooconfigure hello Azure [이 여기서][powershell-install-configure]합니다.

Tooinstall, 업데이트 하 고 hello Azure PowerShell cmdlet을 구성 하는 방법에 대 한 자세한 단계에서 찾을 수 또한 [hello 배포 가이드의이 장의][deployment-guide-4.1]합니다.

사용자 환경 개선 지금까지 되었습니다 PS (PowerShell)는 보다 강력한 도구 toodeploy Vm hello 및 사용자 지정 toocreate hello 배포 된 Vm의 단계를 확실히 합니다. Hello Azure 포털에서에서 작업을 수행할 수 있거나 PS cmdlet을 사용 해도 PS cmdlet toosupplement 관리 작업을 사용 하는 Azure에서 SAP 인스턴스를 실행 하는 hello 고객의 모든 toomanage 독점적으로 Azure에서 배포 합니다. Hello Azure 관련 cmdlet 공유 hello 명명 규칙으로 hello 2000 개가 넘는 Windows 관련 cmdlet 동일, 이므로 쉬운 작업이 Windows 관리자 tooleverage 이러한 cmdlet.

<http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>에서 예제를 참조하세요.

[comment]: <> (MShermannd TODO - 테스트할 때 새 CLI 명령을 설명합니다.)
Hello SAP 용 Azure 모니터링 확장의 배포 (장을 참조 [SAP 용 Azure 모니터링 솔루션] [ planning-guide-9.1] 이 문서의)은 PowerShell 또는 CLI를 통해만 가능 합니다. 따라서 필수 tooset 중일 하 고 PowerShell 또는 CLI를 배포 하거나 Azure의 SAP NetWeaver 시스템을 관리할 때는 구성 합니다.  

Azure에서 제공 하는 더 많은 기능이 새 PS cmdlet toobe 추가 hello cmdlet 업데이트 해야 하는 것입니다. 따라서는 의미 toocheck hello Azure 다운로드 사이트 이상 hello 달에 한 번 <https://azure.microsoft.com/downloads/> hello cmdlet의 새 버전에 대 한 합니다. hello 이전 버전 위에 hello 새 버전을 설치 합니다.

Azure 관련 PowerShell 명령의 일반 목록은 <https://docs.microsoft.com/powershell/azure/overview>를 확인하세요.

### <a name="management-via-microsoft-azure-cli-commands"></a>Microsoft Azure CLI 명령을 통한 관리
Linux를 사용 하 고 원하는 toomanage Azure 고객에 게 리소스 Powershell 옵션 아닐 수 있습니다. Microsoft는 대안으로 Azure CLI를 제공합니다.
hello Azure CLI hello Azure 플랫폼을 다루기 위한 크로스 플랫폼 명령 집합이 한 오픈 소스를 제공 합니다. hello Azure CLI의 hello hello Azure 포털에에서 있는 동일한 기능을 제공 합니다.

설치, 구성 및 CLI toouse tooaccomplish 명령이 하는 방식에 대 한 정보에 대 한 Azure 작업 참조

* [Hello Azure CLI를 설치 합니다.][xplat-cli]
* [배포 및 Azure 리소스 관리자 템플릿 및 hello Azure CLI를 사용 하 여 가상 컴퓨터 관리] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 hello Azure CLI를 사용 하 여][xplat-cli-azure-resource-manager]

또한 자세한 [Linux Vm에 대 한 Azure CLI] [ deployment-guide-4.5.2] hello에 [배포 가이드] [ planning-guide] toouse Azure CLI toodeploy hello Azure 모니터링 하는 방법에 SAP에 대 한 확장입니다.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>다양 한 방법 toodeploy Azure의 SAP 용 Vm
이 장에서 hello 다양 한 방법 toodeploy Azure에서 VM에 설명 합니다. 이 장에서는 Azure의 VM 및 VHD의 처리뿐만 아니라 추가 준비 절차도 설명합니다.

### <a name="deployment-of-vms-for-sap"></a>SAP용 VM 배포
Microsoft Azure에서는 여러 가지 방법으로 toodeploy Vm 및 연결 된 디스크가 있습니다. 따라서가 매우 중요 한 toounderstand hello 차이가 있으므로 hello vm 준비 hello 배포 방법에 따라 다를 수 있습니다. 일반적으로 살펴보면는 다음 시나리오는 hello:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>일반화 되지 않은 디스크와 온-프레미스 tooAzure에서 VM 이동
확인할 toomove 온-프레미스 tooAzure에서 특정 SAP 시스템을 계획합니다. 이 hello hello 운영 체제를 포함 하는 VHD를 업로드 하 여 수행할 수 있습니다, SAP 바이너리 및 DBMS 바이너리 hello와 Vhd의 hello DBMS tooAzure hello 데이터 및 로그 파일과 함께 hello 합니다. 반대로 너무[시나리오 2 아래][planning-guide-5.1.2], hello 호스트 이름, SAP SID를 유지 하 고 hello 온-프레미스 환경에서 구성 된 대로 hello Azure VM에서에서 SAP 사용자 계정입니다. 따라서 hello 이미지를 일반화 필요는 없습니다. 장 참조 [일반화 되지 않은 디스크와 온-프레미스 tooAzure에서 VM 이동 준비] [ planning-guide-5.2.1] 온-프레미스 준비 단계와 일반화 되지 않은 Vm 또는 Vhd tooAzure 업로드에 대 한이 문서의. 읽기 장 [시나리오 3: 온-프레미스에서 일반화 되지 않은 Azure VHD를 사용 하 여 sap VM 이동] [ deployment-guide-3.4] hello에 [배포 가이드] [ deployment-guide] Azure에서 이미지 배포의 자세한 단계입니다.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>고객별 이미지를 사용하여 VM 배포
OS 또는 DBMS 버전의 toospecific 패치 요구 사항, 기한 hello Azure Marketplace에서에서 제공 하는 hello 이미지 요구 사항 맞지 않을 수 있습니다. 따라서 이후 여러 번 배포할 수 있는 '개인' OS/DBMS VM 이미지를 사용 하는 VM toocreate를 할 수 있습니다. tooprepare 복제용 '개인' 이미지 hello 다음 항목이 toobe 것으로 간주 합니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> 여기서 자세한 내용을 보려면: <https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed> hello 온-프레미스에서 추상화/일반화 hello Windows 설정 (예: Windows SID 및 호스트 이름) 이어야 합니다 Hello sysprep 명령을 통해 VM입니다.
>
>
> ![Linux][Logo_Linux] Linux
>
> 에 대 한 이러한 문서에 설명 된 hello 단계에 따라 [SUSE][virtual-machines-linux-create-upload-vhd-suse], [Red Hat][virtual-machines-linux-redhat-create-upload-vhd], 또는 [Oracle Linux] [ virtual-machines-linux-create-upload-vhd-oracle], tooprepare VHD toobe tooAzure 업로드 합니다.
>
>

- - -
Hello 배포 hello 인스턴스를 통해 hello Azure VM의 SAP 소프트웨어 구축 hello에서 지원 되는 프로시저 이름 바꾸기 후 hello SAP 시스템 설정을 조정할 수 있는지 (특히 2 계층 시스템) 용 온-프레미스 VM에서 SAP 콘텐츠를 이미 설치한 경우 관리자 (SAP Note [1619720]). 장 참조 [SAP 용 고객별 이미지를 사용 하 여 VM을 배포 하기 위한 준비] [ planning-guide-5.2.2] 및 [온-프레미스 tooAzure에서 VHD를 업로드 하는 중] [ planning-guide-5.3.2]온-프레미스 준비 단계와 일반화 된 VM tooAzure 업로드에 대 한이 문서의. 읽기 장 [시나리오 2: SAP 용 사용자 지정 이미지를 사용 하 여 VM 배포] [ deployment-guide-3.3] hello에 [배포 가이드] [ deployment-guide] 배포의 자세한 단계 이러한 Azure의 이미지에에서 있습니다.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Hello Azure Marketplace에서 VM 배포
Toouse Microsoft 또는 타사 제공 VM 이미지 hello Azure 마켓플레이스 toodeploy에서 VM을 합니다. Hello를 수행 하는 Azure에서 VM을 배포한 후 동일한 지침 및 도구 tooinstall hello SAP 소프트웨어 및/또는 DBMS VM 내 온-프레미스 환경에서 같은 합니다. 장을 참조 하십시오 배포 설명 보다 자세한 [시나리오 1: hello SAP 용 Azure Marketplace에서 VM 배포] [ deployment-guide-3.2] hello에 [배포 가이드] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Azure용 SAP로 VM 준비
Azure에 Vm을 업로드 하기 전에 toomake 있는지 hello Vm 및 Vhd에는 특정 요구 사항을 충족 해야 합니다. 사용 되는 hello 배포 방법에 따라 약간씩 차이가 있습니다.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>일반화 되지 않은 디스크와 온-프레미스 tooAzure에서 VM 이동 준비
일반적인 배포 방법은 SAP 시스템 tooAzure 온-프레미스에서에서 실행 되는 기존 VM toomove는 합니다. VM 및 hello hello VM에서 실행 될 사용 하 여 Azure에서 SAP 시스템 동일한 호스트 이름 hello와 대부분 동일 hello SAP SID입니다. 이 경우 여러 배포 하지 hello 게스트 VM의 OS를 일반화 해야 합니다. 온-프레미스 네트워크 hello Azure로 확장 하는 경우 (장을 참조 [크로스-프레미스-단일의 배포 또는를 Azure의 hello 온-프레미스 네트워크에 완전히 통합 되 고 hello 요구 사항에 여러 SAP Vm] [ planning-guide-2.2] 이 문서에), 다음에 hello 동일한 도메인 계정을 온-프레미스 하기 전에 사용 했던 것과 hello VM 내에서 사용할 수 있습니다.

고유한 Azure VM 디스크를 준비할 때의 요구 사항은 다음과 같습니다.

* 원래 hello VHD 포함 hello 운영 체제에는 최대 크기는 127GB만 있을 수 있습니다. 2015 년 3 월의 hello 끝에이 제한을 제거 (를) 가져왔습니다. 이제 hello hello 운영 체제가 포함 된 VHD 수 too1TB의 크기를 다른 Azure 저장소도 VHD를 호스트 합니다.
* Toobe hello 고정 VHD 형식에에서 필요 합니다. 동적 VHD 또는 VHDx 형식의 VHD는 Azure에서 아직 지원되지 않습니다. 동적 Vhd CLI 또는 PowerShell commandlet hello VHD를 업로드 하는 경우 변환 된 toostatic Vhd 됩니다.
* Vhd 탑재 된 toohello VM 및 Azure toohello VM 필요 toobe도 고정된 VHD 형식으로 다시 탑재 되어야 합니다. 데이터 디스크의 크기 제한에 대해 알아보려면 [이 문서(Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux)와 [이 문서(Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows)를 확인하세요. 동적 Vhd CLI 또는 PowerShell commandlet hello VHD를 업로드 하는 경우 변환 된 toostatic Vhd 됩니다.
* 추가 Microsoft 기술 지원 서비스 또는 VM을 배포 하는 hello 될 때까지 서비스 및 응용 프로그램 toorun 위한 컨텍스트로 할당할 수도 및 더 적절 한 사용자가 사용할 수 있는 관리자 권한이 있는 다른 로컬 계정을 사용할 수 있습니다.
* 클라우드 전용 배포 시나리오를 사용 하 여 hello 사례에 대 한 (장을 참조 [클라우드 전용-hello에 대 한 종속성 없이 Azure에 가상 컴퓨터 배포 온-프레미스 고객 네트워크] [ planning-guide-2.1] 이 문서) 조합 하 여이 배포 방법을 도메인 계정에는 Azure의 hello Azure 디스크를 배포 하는 작동 하지 않을 수 있습니다. 인 hello DBMS 또는 SAP 응용 프로그램 같은 toorun 사용 되는 서비스 계정에 대 한 경우 특히 유용 합니다. 따라서 이러한 도메인 계정은 VM 로컬 계정으로 tooreplace 필요 하 고 hello VM에서에서 hello 온-프레미스 도메인 계정을 삭제 합니다. Hello VM 이미지에 온-프레미스 도메인 사용자가 유지 합니다. 중요 하지 않은 경우 hello에서 VM을 배포 하는 hello 크로스-프레미스 시나리오 장에 설명 된 대로 [크로스-프레미스-단일의 배포 또는를 Azure의 hello 요구 사항에 여러 SAP Vm hello 온-프레미스 네트워크에 완전히 통합 되어] [ planning-guide-2.2] 이 문서에 있습니다.
* 도메인 계정을 DBMS 로그인으로 사용 되었습니다. hello 시스템 온-프레미스 및 해당 Vm을 실행 하는 경우 사용자가 toobe 클라우드 전용 시나리오에서 배포 된 것으로 간주 되, hello 도메인 사용자 toobe 삭제 해야 합니다. 다른 VM 로컬 사용자 및 로컬 관리자에 게 추가 되는지 로그인/사용자로 hello dbms에 관리자 자격으로 toomake가 필요 합니다.
* Hello 특정 배포 시나리오에 필요할 수 있습니다 하는 것 처럼 다른 로컬 계정을 추가 합니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> 이 시나리오에서는 hello VM 없는 일반화 (sysprep) 필요한 tooupload 이며 hello Azure에서 VM을 배포 합니다.
> D:\ 드라이브가 사용되지 않음을 확인합니다.
> 그리고 이 문서의 [연결된 디스크에 대한 자동 탑재 설정][planning-guide-5.5.3] 장에서 설명한 대로 연결된 디스크에 대해 디스크 자동 탑재를 설정합니다.
>
> ![Linux][Logo_Linux] Linux
>
> 이 시나리오에서는 없는 일반화 (waagent-deprovision) hello의 VM은 필요한 tooupload 및 hello Azure에서 VM을 배포 합니다.
> /mnt/resource가 사용되지 않는지와 모든 디스크가 uuid를 통해 탑재되는지 확인합니다. Hello OS 디스크에 대 한 hello 부팅 로더 항목 hello uuid 기반 탑재에도 적용 되었는지 확인 합니다.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>SAP용 고객별 이미지를 사용하여 VM 배포 준비
일반화된 OS를 포함하는 VHD 파일은 Azure Storage 계정의 컨테이너에 저장되거나 관리 디스크 이미지로 저장됩니다. 장에 설명 된 대로 배포 템플릿 파일의 원본으로 hello VHD 또는 관리 되는 디스크 이미지를 참조 하 여 이러한 이미지에서 새 VM을 배포할 수 [시나리오 2: SAP 용 사용자 지정 이미지를 사용 하 여 VM 배포] [ deployment-guide-3.3]의 hello [배포 가이드][deployment-guide]합니다.

고유한 Azure VM 이미지를 준비할 때의 요구 사항은 다음과 같습니다.

* 원래 hello VHD 포함 hello 운영 체제에는 최대 크기는 127GB만 있을 수 있습니다. 2015 년 3 월의 hello 끝에이 제한을 제거 (를) 가져왔습니다. 이제 hello hello 운영 체제가 포함 된 VHD 수 too1TB의 크기를 다른 Azure 저장소도 VHD를 호스트 합니다.
* Toobe hello 고정 VHD 형식에에서 필요 합니다. 동적 VHD 또는 VHDx 형식의 VHD는 Azure에서 아직 지원되지 않습니다. 동적 Vhd CLI 또는 PowerShell commandlet hello VHD를 업로드 하는 경우 변환 된 toostatic Vhd 됩니다.
* Vhd 탑재 된 toohello VM 및 Azure toohello VM 필요 toobe도 고정된 VHD 형식으로 다시 탑재 되어야 합니다. 데이터 디스크의 크기 제한에 대해 알아보려면 [이 문서(Linux)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux)와 [이 문서(Windows)](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows)를 확인하세요. 동적 Vhd CLI 또는 PowerShell commandlet hello VHD를 업로드 하는 경우 변환 된 toostatic Vhd 됩니다.
* 클라우드 전용 시나리오에서 hello VM의에서 사용자가 존재 하지 것입니다로 등록 된 도메인 사용자가 hello 모든 이후 (장을 참조 [클라우드 전용-hello에 대 한 종속성 없이 Azure에 가상 컴퓨터 배포 온-프레미스 고객 네트워크] [ planning-guide-2.1] 이 문서의), 서비스 계정에는 Azure의 hello 이미지를 배포 하는 작동 하지 않을 수 이러한 도메인을 사용 합니다. 인 DBMS 또는 SAP 응용 프로그램 같은 toorun 사용 되는 서비스 계정에 대 한 경우 특히 유용 합니다. 따라서 이러한 도메인 계정은 VM 로컬 계정으로 tooreplace 필요 하 고 hello VM에서에서 hello 온-프레미스 도메인 계정을 삭제 합니다. Hello VM 이미지에 온-프레미스 도메인 사용자가 유지 하지 못할 문제가 때 hello에서 VM을 배포 하는 hello 크로스-프레미스 시나리오 장에 설명 된 대로 [크로스-프레미스-단일의 배포 또는를 Azure의 hello 요구 사항에 여러 SAP Vm hello 온-프레미스 네트워크에 완전히 통합 되 고] [ planning-guide-2.2] 이 문서에 있습니다.
* 추가 Microsoft 지원부에서 문제를 조사 하거나 VM을 배포 하는 hello 될 때까지 서비스 및 응용 프로그램 toorun 위한 컨텍스트로 할당할 수도 및 더 적절 한 사용자가 사용할 수 있는 관리자 권한이 있는 다른 로컬 계정을 사용할 수 있습니다.
* 클라우드 전용 배포 및 실행 하는 경우 사용자가 시스템 온-프레미스 hello 또는 도메인 계정을 DBMS 로그인으로 사용 된 위치에서 hello 도메인 사용자를 삭제 해야 합니다. Toomake hello 로컬 관리자와 다른 VM 로컬 사용자 hello dbms에 관리자 자격의 로그인/사용자로 추가 되어 있는지 필요 합니다.
* Hello 특정 배포 시나리오에 필요할 수 있습니다 하는 것 처럼 다른 로컬 계정을 추가 합니다.
* 권장된 toocopy hello 최신 버전의 hello SAP 소프트웨어 Provisioning Manager DVD이 hello 이미지에 설치 된 SAP NetWeaver hello hello Azure 배포의 hello 지점에서 원래 이름에서 hello 호스트 이름의 이름 변경 될 경우 hello 템플릿입니다. 이렇게 하면 tooeasily 사용 하 여 hello SAP 제공 이름 바꾸기 기능 tooadapt hello 변경 된 호스트 이름 및/또는 변경 hello SID hello hello 내에서 SAP 시스템의 새 복사본을 시작 하는 즉시 VM 이미지를 배포 합니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> D:\ 드라이브가 사용되지 않는지 확인하고 이 문서의 [연결된 디스크에 대한 자동 탑재 설정][planning-guide-5.5.3] 장에서 설명한 대로 연결된 디스크에 대해 디스크 자동 탑재를 설정하세요.
>
> ![Linux][Logo_Linux] Linux
>
> /mnt/resource가 사용되지 않는지와 모든 디스크가 uuid를 통해 탑재되는지 확인합니다. Hello OS 디스크에 대 한 hello 부팅 로더 항목 hello uuid 기반 탑재에도 적용 되었는지 확인 합니다.
>
>

- - -
* SAP GUI(관리 및 설치용)를 이러한 템플릿에 미리 설치할 수 있습니다.
* 기타 소프트웨어 hello VM의 이름 바꾸기 필요한 toorun hello 크로스-프레미스 시나리오에서 성공적으로 Vm이이 소프트웨어는 hello 작업할 수으로 설치할 수 있습니다.

Hello VM 충분히 준비 toobe 일반적이 고 영향을 받지 않게 계정/사용자 hello에서 사용할 수 없는 대상 Azure 배포 시나리오, 이러한 이미지를 일반화 hello 마지막 준비 단계를 수행 합니다.

##### <a name="generalizing-a-vm"></a>VM 일반화
- - -
> ![Windows][Logo_Windows] Windows
>
> hello 마지막 단계에서 관리자 계정으로 VM tooa toolog입니다. '관리자 권한'으로 Windows 명령 창을 엽니다. Too%windir%\windows\system32\sysprep 이동한 다음 sysprep.exe를 실행 합니다.
> 작은 창이 나타납니다. 이 옵션은 중요 한 toocheck hello '일반화' 옵션 (hello 기본 있지 않음)을 기본값인 '다시 부팅' too'Shutdown hello 종료 옵션을 변경 하 고 '. 이 절차 hello sysprep 프로세스 실행 된 온-프레미스 VM의 게스트 OS hello에 있다고 가정 합니다.
> Azure에서 이미 실행 중인 VM과 tooperform hello 프로시저를 원하는 경우에 설명 된 hello 단계에 따라 [이 여기서](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/capture-image-resource)합니다.
>
> ![Linux][Logo_Linux] Linux
>
> [어떻게 toocapture 리소스 관리자 템플릿으로 Linux 가상 컴퓨터 toouse][capture-image-linux-step-2-create-vm-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>온-프레미스 tooAzure 간에 Vm 및 Vhd 전송
VM 이미지와 디스크 tooAzure 업로드 hello Azure 포털을 통해 수 없으면 있으므로 toouse Azure PowerShell cmdlet 또는 CLI 필요. 또 다른 원인은 'AzCopy' hello 도구의 hello 사용 합니다. hello 도구 (양방향)으로 온-프레미스와 Azure 간에 Vhd를 복사할 수 있습니다. 또한 Azure 지역 간에 VHD를 복사할 수도 있습니다. AzCopy의 다운로드 및 사용에 대해서는 [이 설명서][storage-use-azcopy]를 참조하세요.

세 번째 대체 것 toouse 다양 한 제 3 자 GUI 기반 도구입니다. 그러나 이러한 도구가 Azure 페이지 Blob을 지원하는지 확인하세요. Azure 페이지 Blob toouse 필요 목적에 맞는 저장 (hello 차이 다음과 같습니다: <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>). 또한 Azure에서 제공 하는 hello 도구는 hello Vm 및 Vhd 업로드 toobe 필요한 압축에 매우 효율적입니다. 이 처럼 효율적인 압축 hello 업로드 시간 (대상에서 hello 온-프레미스 시설과 hello Azure 배포 지역의 인터넷 업로드 링크 toohello를 hello에 따라 그래도 다름) 줄어들기 때문에 유용 합니다. 이기는 같은 Vm/Vhd toohello 유럽 Azure 데이터 센터 hello 유럽 위치 toohello 미국 기반 Azure 데이터 센터 업로드 보다 시간이 오래 걸립니다.에서 VM 또는 VHD를 업로드 걸린다고 생각 합니다.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>온-프레미스 tooAzure에서 VHD를 업로드 하는 중
기존 VM 또는 VHD hello에서 온-프레미스 이러한 VM 네트워크 또는 장의에 나열 된 VHD 필요한 toomeet hello 요구 사항 tooupload [일반화 되지 않은 디스크와 온-프레미스 tooAzure에서 VM 이동 준비] [ planning-guide-5.2.1] 이 문서의.

이러한 VM 일반화 toobe 필요는 없습니다 및 hello 상태 및 모양에 후 종료 hello 온-프레미스 측 업로드할 수 있습니다. hello에 마찬가지입니다 모든 운영 체제에 포함 되지 않은 추가 Vhd입니다.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>VHD를 업로드한 후 Azure 디스크로 만들기
이 경우 म tooupload VHD 또는 비,에 OS 및 tooa VM에 데이터 디스크로 탑재 하거나 운영 체제 디스크로 사용. 이 작업은 다중 단계로 진행됩니다.

**PowerShell**

* Tooyour 구독과 로그인 *AzureRmAccount 로그인*
* 설정 된 컨텍스트의 hello 구독 *집합 AzureRmContext* SubscriptionId 매개 변수 또는-s u b 참조 및 <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* 업로드 된 VHD hello *추가 AzureRmVhd* tooan Azure 저장소 계정-참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (선택 사항) Hello VHD에서에서 관리 되는 디스크를 만들와 *새로 AzureRmDisk* -참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermdisk>
* 새 VM config toohello VHD의 hello 운영 체제 디스크 또는 디스크를 관리 하는 설정 *집합 AzureRmVMOSDisk* -참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
* 와 hello VM 구성에서 새 VM 만들기 *새로 AzureRmVM* -참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>
* 데이터 디스크 tooa 추가 된 새 VM *추가 AzureRmVMDataDisk* -참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk>

**Azure CLI 2.0**

* Tooyour 구독과 로그인 *az 로그인*
* *az account set --subscription `<subscription name or id`>*를 사용하여 구독 선택
* 업로드 된 VHD hello *az 저장소 blob 업로드* -참조 [hello를 사용 하 여 Azure 저장소와 Azure CLI][storage-azure-cli]
* (선택 사항) Hello VHD에서에서 관리 되는 디스크를 만들와 *az 디스크 만들기* -https://docs.microsoft.com/cli/azure/disk#create 참조
* 와 운영 체제 디스크로 VHD 또는 관리 되는 디스크를 업로드 하는 hello를 지정 하는 새 VM 만들기 *az vm 만들기* 및 매개 변수 *--os-디스크 연결*
* 데이터 디스크 tooa 추가 된 새 VM *az vm 디스크를 연결* 및 매개 변수 *-새로 만들기*

**템플릿**

* Hello Azure CLI 또는 Powershell로 VHD 업로드
* (선택 사항) Hello VHD Powershell, Azure CLI 또는 hello Azure 포털에서에서 관리 되는 디스크를 만들려면
* 에 표시 된 대로 hello VHD를 참조 하는 JSON 템플릿을 사용 하 여 hello VM 배포 [이 예제 JSON 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json) 에서처럼 관리 하는 디스크를 사용 하 여 또는 [이 예제 JSON 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-disk-md/azuredeploy.json)합니다.

#### <a name="deployment-of-a-vm-image"></a>VM 이미지 배포
기존 VM 또는 VHD hello에서 온-프레미스 네트워크에 순서 toouse 것을 Azure VM 이미지로 이러한 VM 또는 VHD 장에 나열 된 toomeet hello 요구를 갖 tooupload [SAP용고객별이미지를사용하여VM을배포하기위한준비] [ planning-guide-5.2.2] 이 문서의.

* 사용 하 여 *sysprep* windows 또는 *waagent-deprovision* Linux toogeneralize에 VM-참조 [Sysprep 기술 참조](https://technet.microsoft.com/library/cc766049.aspx) Windows 용 또는 [어떻게 toocapture는 리소스 관리자 템플릿으로 Linux 가상 컴퓨터 toouse] [ capture-image-linux-step-2-create-vm-image] Linux 용
* Tooyour 구독과 로그인 *AzureRmAccount 로그인*
* 설정 된 컨텍스트의 hello 구독 *집합 AzureRmContext* SubscriptionId 매개 변수 또는-s u b 참조 및 <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* 업로드 된 VHD hello *추가 AzureRmVhd* tooan Azure 저장소 계정-참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (선택 사항) Hello VHD에서에서 관리 되는 디스크 이미지 만들기와 *새로 AzureRmImage* -참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermimage>
* 새 VM config toothe의 OS 디스크 hello 설정
  * VHD로 설정(*Set-AzureRmVMOSDisk -SourceImageUri -CreateOption fromImage* 사용) - <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk> 참조
  * 관리 디스크 이미지 *Set-AzureRmVMSourceImage* - <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage> 참조
* 와 hello VM 구성에서 새 VM 만들기 *새로 AzureRmVM* -참조 <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>

**Azure CLI 2.0**

* 사용 하 여 *sysprep* windows 또는 *waagent-deprovision* Linux toogeneralize에 VM-참조 [Sysprep 기술 참조](https://technet.microsoft.com/library/cc766049.aspx) Windows 용 또는 [어떻게 toocapture는 리소스 관리자 템플릿으로 Linux 가상 컴퓨터 toouse] [ capture-image-linux-step-2-create-vm-image] Linux 용
* Tooyour 구독과 로그인 *az 로그인*
* *az account set --subscription `<subscription name or id`>*를 사용하여 구독 선택
* 업로드 된 VHD hello *az 저장소 blob 업로드* -참조 [hello를 사용 하 여 Azure 저장소와 Azure CLI][storage-azure-cli]
* (선택 사항) Hello VHD에서에서 관리 되는 디스크 이미지 만들기와 *az 이미지 만들기* -https://docs.microsoft.com/cli/azure/image#create 참조
* Hello는 VHD 또는 관리 되는 디스크 이미지와 운영 체제 디스크로 업로드를 지정 하는 새 VM 만들기 *az vm 만들기* 및 매개 변수 *-이미지*

**템플릿**

* 사용 하 여 *sysprep* windows 또는 *waagent-deprovision* Linux toogeneralize에 VM-참조 [Sysprep 기술 참조](https://technet.microsoft.com/library/cc766049.aspx) Windows 용 또는 [어떻게 toocapture는 리소스 관리자 템플릿으로 Linux 가상 컴퓨터 toouse] [ capture-image-linux-step-2-create-vm-image] Linux 용
* Hello Azure CLI 또는 Powershell로 VHD 업로드
* (선택 사항) Hello VHD Powershell, Azure CLI 또는 hello Azure 포털에서에서 관리 되는 디스크 이미지 만들기
* 에 표시 된 대로 hello VHD 이미지를 참조 하는 JSON 템플릿을 사용 하 여 hello VM 배포 [이 예제 JSON 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-image/azuredeploy.json) 에 나와 있는 것 처럼 관리 되는 디스크 이미지를 hello를 사용 하 여 또는 [이 예제 JSON 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json)합니다.

#### <a name="downloading-vhds-or-managed-disks-tooon-premises"></a>Vhd 또는 관리 하는 디스크 tooon 온-프레미스를 다운로드합니다.
Azure 인프라 서비스 뿐만 수 tooupload Vhd 및 SAP 시스템의 단방향 street 아닙니다. SAP를 이동할 수 시스템을 Azure hello 온-프레미스 환경으로 스풀링됩니다.

Hello의 hello 시간 동안 다운로드 hello Vhd 또는 디스크 관리를 활성화할 수 없습니다. 탑재 된 tooVMs 인 디스크를 다운로드 하는 경우에 hello VM 요구 toobe를 종료 하 고 할당 취소 합니다. 그런 다음 새 시스템을 사용 하는 tooset 해야 온-프레미스와 Azure에서 시스템 hello 시스템 계속 작동할 수 수 있으면 hello 시간 hello에 다운로드 하 고 설치 프로그램의 새 hello hello 있는 콘텐츠 toodownload hello 데이터베이스 검색. 를 디스크에 압축된 된 데이터베이스 백업을 수행 하 여 긴 가동 중지 시간을 하지 않도록 하 고만 hello OS 기본 VM 다운로드 하는 대신 해당 디스크를 다운로드할 수 있습니다.

#### <a name="powershell"></a>PowerShell

  * 관리 디스크 다운로드  
  먼저 tooget 액세스 toohello blob hello 관리 되는 디스크의 원본으로 사용 해야 합니다. 다음 기본 blob tooa hello 새 저장소 계정을 복사한 hello blob이 저장소 계정에서 다운로드할 수 있습니다.

  ```powershell
  $access = Grant-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name> -Access Read -DurationInSecond 3600
  $key = (Get-AzureRmStorageAccountKey -ResourceGroupName <resource group> -Name <storage account name>)[0].Value
  $destContext = (New-AzureStorageContext -StorageAccountName <storage account name -StorageAccountKey $key)
  Start-AzureStorageBlobCopy -AbsoluteUri $access.AccessSAS -DestContainer <container name> -DestBlob <blob name> -DestContext $destContext
  # Wait for blob copy toofinish
  Get-AzureStorageBlobCopyState -Container <container name> -Blob <blob name> -Context $destContext
  Save-AzureRmVhd -SourceUri <blob in new storage account> -LocalFilePath <local file path> -StorageKey $key
  # Wait for download toofinish
  Revoke-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name>
  ```

  * VHD 다운로드  
  Hello VM을 종료를 사용할 수 있습니다 및 SAP 시스템 hello 중지 되 면 hello PowerShell cmdlet 저장 AzureRmVhd hello에 온-프레미스 대상 toodownload hello VHD 디스크 toohello 온-프레미스 세계를 백업 합니다. Azure 포털 (필요 toonavigate toohello 저장소 계정 및 hello 저장소 컨테이너 hello VHD 생성 된 위치)을 필요한 tooknow hello VHD 있어야 할 위치 해야 하는, hello hello ' 저장소 ' 섹션에서에서 찾을 수 있는 VHD의 hello URL의 hello 순서 toodo에서 에 복사 합니다.

  그런 다음 단순히 hello VHD (해당 이름 포함)의 실제 위치 hello로 hello VHD toodownload 및 hello LocalFilePath hello URL로 SourceUri hello 매개 변수를 정의 하 여 hello 명령을 활용할 수 있습니다. hello 명령 같을 수 있습니다.

  ```powerhell
  Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
  ```

  Hello 저장 AzureRmVhd cmdlet의 자세한 정보를 확인 하십시오 여기 <https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvhd>합니다.

#### <a name="cli-20"></a>CLI 2.0
  * 관리 디스크 다운로드  
  먼저 tooget 액세스 toohello blob hello 관리 되는 디스크의 원본으로 사용 해야 합니다. 다음 기본 blob tooa hello 새 저장소 계정을 복사한 hello blob이 저장소 계정에서 다운로드할 수 있습니다.
  ```
  az disk grant-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --duration-in-seconds 3600
  az storage blob download --sas-token "<sas token>" --account-name <account name> --container-name <container name> --name <blob name> --file <local file>
  az disk revoke-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>"
  ```

  * VHD 다운로드   
  SAP 시스템 hello를 중지 하 고 hello VM을 종료를 hello Azure CLI 명령을 사용할 수 있습니다 _azure 저장소 blob 다운로드_ hello 온-프레미스 대상에서 toodownload hello VHD 디스크 백 toohello 온-프레미스 세계 합니다. Azure 포털 (필요 toonavigate toohello 저장소 계정 및 hello 저장소 컨테이너 hello VHD 생성 된 위치)을 필요한 tooknow 순서 toodo hello 이름 및 hello hello ' 저장소 ' 섹션에서에서 찾을 수 있는 VHD의 hello 컨테이너의 hello 필요,에 있는 hello VHD에 복사 되어야 합니다.

  그런 다음 단순히 hello (해당 이름 포함) VHD의 hello 물리적 대상 위치로 hello 매개 변수 blob 및 hello VHD toodownload와 hello 대상의 컨테이너를 정의 하 여 hello 명령을 활용할 수 있습니다. hello 명령 같을 수 있습니다.

  ```
  az storage blob download --name <name of hello VHD toodownload> --container-name <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --file <destination of hello VHD toodownload>
  ```

### <a name="transferring-vms-and-disks-within-azure"></a>Azure 내에서 VM 및 디스크 전송
#### <a name="copying-sap-systems-within-azure"></a>Azure 내에서 SAP 시스템 복사
SAP 시스템 또는 심지어는 전용된 DBMS 서버는 SAP 응용 프로그램 계층을 지 원하는 데이터 hello 또는 hello 이진 파일과 함께 hello 운영 체제 중 하나를 포함 하는 여러 개의 디스크 구성 가능성이 되며 로그 hello SAP 데이터베이스의 파일입니다. 디스크 복사의 Azure 기능 hello 지도 hello 저장 디스크 tooa 로컬 디스크의 Azure 기능에는 동기화 메커니즘이, 여러 디스크를 동기적으로 스냅숏 것입니다. 따라서 hello 상태의 hello 복사 하거나 디스크를 탑재 되어 있는 경우에 저장 hello에 대 한 동일한 VM은 달라질 수 있습니다. 즉,는 서로 다른 데이터와 명확 하 게 hello 서로 다른 디스크에 포함 된의 구체적인 경우 hello hello 데이터베이스 hello 끝에 일치 하지 않게 됩니다.

**결론: 순서 toocopy 또는 toostop hello SAP 시스템이 필요 하 고 필요에 SAP 시스템 구성의 일부 디스크 저장 hello 아래로 tooshut VM 배포. 복사 하거나 디스크 tooeither hello 집합을 다운로드할 수 있습니다 다음 Azure 또는 온-프레미스에서 hello SAP 시스템의 복사본을 만듭니다.**

데이터 디스크는 Azure 저장소 계정에 VHD 파일로 저장할 수 있습니다 및 tooa 직접 연결 된 가상 컴퓨터 수 있습니다. 또는 이미지 형식으로 사용할 수 있습니다. 이 경우 hello VHD는 가상 컴퓨터에 연결 된 toohello 있을 때까지 복사한 tooanother 위치입니다. Azure의 hello VHD 파일의 전체 이름을 hello Azure 내에서 고유 해야 합니다. 이미 앞에서 설명 했 듯이 hello 이름이 세 부분으로 이루어진 이름을 다음과 같은 종류의:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

데이터 디스크를 관리 디스크로 사용할 수도 있습니다. 이 경우 hello 관리 되는 디스크에는 연결 된 toohello 가상 컴퓨터에 있을 때까지 새 관리 되는 디스크 사용된 toocreate입니다. hello 이름 hello 관리 되는 디스크의 리소스 그룹 내에서 고유 해야 합니다.

##### <a name="powershell"></a>PowerShell
에 표시 된 대로 Azure PowerShell cmdlet toocopy VHD를 사용할 수 있습니다 [이 여기서][storage-powershell-guide-full-copy-vhd]합니다. toocreate 새 관리 되는 디스크 hello 다음 예제와 같이 새로 AzureRmDiskConfig 및 새로운 AzureRmDisk를 사용 합니다.

```powershell
$config = New-AzureRmDiskConfig -CreateOption Copy -SourceUri "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" -Location <location>
New-AzureRmDisk -ResourceGroupName <resource group name> -DiskName <disk name> -Disk $config
```

##### <a name="cli-20"></a>CLI 2.0
에 표시 된 대로 Azure CLI toocopy VHD를 사용할 수 있습니다 [이 여기서][storage-azure-cli-copy-blobs]합니다. toocreate 새 관리 되는 디스크를 사용 하 여 *az 디스크 만들기* hello 다음 예제와 같이 합니다.

```
az disk create --source "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --name <disk name> --resource-group <resource group name> --location <location>
```

##### <a name="azure-storage-tools"></a>Azure 저장소 도구
* <http://storageexplorer.com/>

Azure Storage 탐색기의 전문가 버전은 아래 페이지에서 확인할 수 있습니다.

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

hello 저장소 계정 내의 VHD 자체는 프로세스는 몇 초 밖에 (유사한 tooSAN 하드웨어 쓰기 유휴 복사본 및 복사를 사용 하 여 스냅숏 만들기)를 사용 하십시오. Hello VHD 파일의 복사본을 만들었으면 tooa 가상 컴퓨터 또는 이미지 tooattach로 hello VHD toovirtual 컴퓨터의 복사본을 사용 하 여 연결할 수 있습니다.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -ManagedDiskId <managed disk id> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name <disk name> -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption fromImage
$vm | Update-AzureRmVM

# attach a copy of hello managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$diskConfig = New-AzureRmDiskConfig -Location $vm.Location -CreateOption Copy -SourceUri <source managed disk id>
$disk = New-AzureRmDisk -DiskName <disk name> -Disk $diskConfig -ResourceGroupName <resource group name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Caching <caching option> -Lun <lun, for example 0> -CreateOption attach -ManagedDiskId $disk.Id
$vm | Update-AzureRmVM
```
##### <a name="cli-20"></a>CLI 2.0
```

# attach a vhd tooa vm
az vm unmanaged-disk attach --resource-group <resource group name> --vm-name <vm name> --vhd-uri <path toovhd>

# attach a managed disk tooa vm
az vm disk attach --resource-group <resource group name> --vm-name <vm name> --disk <managed disk id>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.

# attach a copy of a managed disk tooa vm
az disk create --name <new disk name> --resource-group <resource group name> --location <location of target virtual machine> --source <source managed disk id>
az vm disk attach --disk <new disk name or managed disk id> --resource-group <resource group name> --vm-name <vm name> --caching <caching option> --lun <lun, for example 0>
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Azure 저장소 계정 간 디스크 복사
Hello Azure 포털에서이 작업을 수행할 수 없습니다. Azure PowerShell cmdlet, Azure CLI 또는 타사 저장소 브라우저를 사용할 수 있습니다. PowerShell cmdlet을 hello 또는 CLI 명령을 만들고 여러 저장소 계정 및 hello Azure 구독 내의 여러 지역과 hello 기능 tooasynchronously 복사 blob을 포함 하는 blob를 관리할 수 있습니다.

##### <a name="powershell"></a>PowerShell
구독 간에 VHD를 복사할 수도 있습니다. 자세한 내용은 [이 문서][storage-powershell-guide-full-copy-vhd]를 참조하세요.

hello hello PS cmdlet 논리의 기본 흐름은 다음과 같습니다.

* Hello에 대 한 저장소 계정 컨텍스트 만들기 **소스** 저장소 계정과 *새로 AzureStorageContext* -참조 <https://msdn.microsoft.com/library/dn806380.aspx>
* Hello에 대 한 저장소 계정 컨텍스트 만들기 **대상** 저장소 계정과 *새로 AzureStorageContext* -참조 <https://msdn.microsoft.com/library/dn806380.aspx>
* 사용 하 여 hello 복사를 시작 합니다.

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* 포함 하는 루프에 hello 복사본의 hello 상태 확인

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* 위에서 설명한 것 처럼 hello 새 VHD tooa 가상 컴퓨터를 연결 합니다.

예제는 [이 문서][storage-powershell-guide-full-copy-vhd]를 참조하세요.

##### <a name="cli-20"></a>CLI 2.0
* 사용 하 여 hello 복사를 시작 합니다.

```
az storage blob copy start --source-blob <source blob name> --source-container <source container name> --source-account-name <source storage account name> --source-account-key <source storage account key> --destination-container <target container name> --destination-blob <target blob name> --account-name <target storage account name> --account-key <target storage account name>
```

* 경우 hello hello 상태 확인 된 루프의 복사본

```
az storage blob show --name <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* 위에서 설명한 것 처럼 hello 새 VHD tooa 가상 컴퓨터를 연결 합니다.

예제는 [이 문서][storage-azure-cli-copy-blobs]를 참조하세요.

### <a name="disk-handling"></a>디스크 처리
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>SAP 배포를 위한 VM/디스크 구조
이상적으로 VM의 hello 구조는 처리를 hello 및 hello 연결 된 디스크는 매우 간단한 수 있어야 합니다. 온-프레미스 설치에서 고객은 서버 설치를 구성하는 여러 가지 방법을 개발했습니다.

* Hello 운영 체제를 포함 하는 하나의 기본 디스크 및 모든 hello 이진 파일의 DBMS 및/또는 SAP hello 합니다. 2015 년 3 월 이후이 디스크는 too127GB 크기 제한도 많아집니다 이전 제한 하는 대신 too1TB를 수 있습니다.
* Hello DBMS를 포함 하는 하나 또는 여러 개의 디스크 로그 hello SAP 데이터베이스의 파일 및 DBMS 임시 저장소 영역의 hello의 hello 로그 파일 (DBMS hello 지 원하는 경우이). Hello 데이터베이스 로그 IOPS 요구 사항이 높은 경우 toostripe 필요한 순서 tooreach hello IOPS 볼륨에 여러 디스크가 필요 합니다.
* (Hello DBMS 지 원하는 경우이) hello SAP 데이터베이스의 데이터베이스 파일 하나 또는 두 개의 및 hello DBMS 임시 데이터 파일에도 포함 하는 디스크의 수입니다.

![SAP용 Azure IaaS VM의 참조 구성][planning-guide-figure-1300]

[comment]: <> (MShermannd TODO - Linux 구조를 설명합니다.)

- - -
> ![Windows][Logo_Windows] Windows
>
> 많은 고객에 대해 살펴보았습니다 구성 위치, 예를 들어 SAP 및 DBMS 바이너리가 설치 되지 않은 위치 hello OS가 설치 된 hello c:\ 드라이브에 있습니다. 이 경우 여러 가지 이유로 했습니다 하지만 toohello 루트 근본적, 일반적으로 hello 드라이브가 작고 OS 업그레이드 10 ~ 15 년 전에 추가 공간이 필요 합니다. 두 조건이 오늘날에는 그렇게 많지 않은 편입니다. 오늘 hello c:\ 드라이브를 큰 볼륨 디스크나 Vm에 매핑할 수 있습니다. 해당 구조에서 간단한 순서 tookeep 배포에서는 권장 toofollow Azure의 SAP NetWeaver 시스템에 대 한 다음 배포 패턴
>
> hello Windows 운영 체제 페이지 파일 d: 드라이브 (비영구 디스크) hello에 있어야 합니다.
>
> ![Linux][Logo_Linux] Linux
>
> 에 설명 된 대로 linux /mnt/mnt/리소스에서 hello Linux 스왑 파일을 배치 [이 여기서][virtual-machines-linux-agent-user-guide]합니다. hello 스왑 파일 hello Linux 에이전트 /etc/waagent.conf hello 구성 파일에서 구성할 수 있습니다. 추가 하거나 hello 다음 설정을 변경 합니다.
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

tooactivate hello 변경 해야 toorestart hello와 Linux 에이전트

```
sudo service waagent restart
```

SAP Note를 읽어 보십시오 [1597355] hello에 대 한 자세한 내용은 스왑 파일 크기를 권장 합니다.

- - -
hello IOPS 요구 사항 및 필요한 hello 대기 시간이가 hello DBMS 데이터 파일 및 이러한 디스크에서 호스팅되는 Azure 저장소의 hello 유형에 대해 사용 되는 디스크의 hello 수를 확인 해야 합니다. 정확한 할당량에 대한 설명은 [이 문서(Linux)][virtual-machines-sizes-linux]와 [이 문서(Windows)][virtual-machines-sizes-windows]에 있습니다.

자신의 경험 지난 2 년 hello 통해 SAP 배포을 근거로 우리으로 요약할 수 있는 몇 가지 단원:

* 항상 IOPS 트래픽 toodifferent 데이터 파일은 해당 SAP 데이터베이스를 나타내는 파일을 기존 고객 시스템 수 있는 다르게 크기의 데이터를 이후 동일 hello 아닙니다. 따라서 더 잘 RAID 구성을 사용 하 여 해당 Lun 된 여러 디스크 tooplace hello 데이터 파일에 대해 toobe 아웃 되어 있습니다. 여기서 IOPS 속도 hello DBMS 트랜잭션 로그에 대 한 단일 디스크의 hello 할당량에 도달 하는 표준 Azure 저장소와 특히 상황 있었습니다. 이러한 시나리오에서는 프리미엄 저장소의 hello 사용을 권장 또는 소프트웨어와 함께 디스크 RAID 또는 여러 표준 저장소를 집계 합니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Linux에서 소프트웨어 RAID 구성][virtual-machines-linux-configure-raid]
> * [Azure에서 Linux VM에 LVM 구성][virtual-machines-linux-configure-lvm]
> * [Azure 저장소 비밀 및 Linux I/O 최적화](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* 프리미엄 저장소는 중요한 트랜잭션 로그 쓰기에서 특히 더 나은 성능을 나타냅니다. SAP 시나리오를 예상된 toodeliver 프로덕션 성능와 같은 것이 좋습니다 toouse Azure 프리미엄 저장소를 활용할 수 있는 VM 시리즈 합니다.

Hello, 운영 체제를 포함 하는 hello 디스크와을 권장 하는 대로 sap 바이너리 hello 이며 hello 데이터베이스 (기본 VM)도 더 이상 too127GB 제한 합니다. 이제 가질 수 있습니다 too1TB의 크기를 구성 합니다. 예를 들어 필요한 파일 등 hello 모두 만큼 충분 한 공간 tookeep 수, 일괄 처리 작업 로그가 SAP 해야이 됩니다.

더 많은 제안 및 특히 DBMS Vm에 대 한 자세한 내용은 참조 하십시오 hello에 대 한 [DBMS 배포 가이드][dbms-guide]

#### <a name="disk-handling"></a>디스크 처리
대부분의 시나리오에서 VM hello에 순서 toodeploy hello SAP 데이터베이스의 toocreate 추가 디스크가 필요 합니다. Hello 고려 사항에 대 한 다양 한 장의 디스크에 얘기 [SAP 배포를 위한 VM/디스크 구조] [ planning-guide-5.5.1] 이 문서의. Azure 포털 hello tooattach 있으며이 기본 VM을 배포한 후 디스크를 분리 합니다. hello 디스크 연결/분리 hello VM이 위쪽 인 경우 및 중지 될 때 뿐만 아니라 실행 될 수 있습니다. 디스크를 연결할 때 hello Azure 포털 제공 tooattach 빈 디스크를 제공 받거나이 시점에서 않은 기존 디스크 tooanother VM을 연결 합니다.

**참고**: 디스크 언제 든 지 연결된 tooone VM 수만 있습니다.

![Azure 표준 저장소에서 디스크 연결/분리][planning-guide-figure-1400]

새 가상 컴퓨터의 hello 배포 하는 동안를 toouse 관리 하는 디스크를 지정 하거나 Azure 저장소 계정에 디스크를 저장 하는지 여부를 결정할 수 있습니다. Toouse 프리미엄 저장소를 사용 하도록 하려는 경우 관리 되는 디스크를 사용 하는 것이 좋습니다.

다음으로 toocreate 새롭고 빈 디스크를 원하는 또는 toohello VM을 이제 연결 tooselect가 이전에 업로드 하 고 있어야 하는 기존 디스크를 변경할지 여부를 toodecide가 필요 합니다.

**중요 한**: 있습니다 **하지 않으면** Azure 표준 저장소와 호스트 캐싱 toouse 원하는 합니다. 기본값은 NONE hello hello 호스트 캐시 기본 설정을 유지 해야 합니다. Azure 프리미엄 저장소를 활성화 해야 읽기 캐싱을 hello I/O 특징이 데이터베이스 데이터 파일에 대 한 일반적인 I/O 트래픽을 같은 주로 읽기 이면. 데이터베이스 트랜잭션 로그 파일의 경우 캐싱 없음이 권장됩니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Hello Azure 포털에서에서 tooattach 데이터 디스크 하는 방법][virtual-machines-linux-attach-disk-portal]
>
> 디스크가 연결 되어 있으면 toolog toohello VM tooopen hello Windows 디스크 관리자에에서 필요 합니다. 장에 권장 된 대로 자동 탑재를 사용 하지 않는 경우 [연결 된 디스크에 대 한 자동 탑재 설정][planning-guide-5.5.3], hello 새로 연결 된 볼륨 필요한 toobe 온라인 되 고 초기화 합니다.
>
> ![Linux][Logo_Linux] Linux
>
> 디스크가 연결 되어 toohello VM에서에서 toolog를 해야에 설명 된 대로 hello 디스크 초기화 [이 문서][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Hello 새 디스크가 비어 있는 디스크 이면 tooformat hello 디스크도 필요 합니다. 서식 지정을 위해의 데이터 및 로그 파일 hello DBMS를 위해 특별히 DBMS 적용 hello의 완전 배포의 경우와 동일한 권장 사항이 있습니다.

이미 설명한 것 처럼 장에서 [Microsoft Azure 가상 컴퓨터 개념 hello][planning-guide-3.2], Azure 저장소 계정은 I/O 볼륨 측면에서 리소스를 무한히 제공 하지 않습니다 IOPS, 데이터 볼륨입니다. 일반적으로 DBMS VM이 그 영향을 가장 많이 받게 됩니다. 몇 가지 높은 I/O 볼륨 Vm toodeploy 순서 toostay hello Azure 저장소 계정 볼륨의 hello 제한 내에 있는 경우 최상의 toouse 각 VM에 대 한 별도 저장소 계정 수 있습니다. 그렇지 않으면, toosee 필요 각 단일 저장소 계정의 hello 한계에 도달 하지 않고 개별 저장소 계정 간에 이러한 Vm 균형을 맞출 수는 방법입니다. 자세한 내용은 hello에 대해서는 설명 [DBMS 배포 가이드][dbms-guide]합니다. 또한 순수한 SAP 응용 프로그램 서버 VM 또는 결과적으로는 추가 VHD를 요구할 수 있는 기타 VHD의 경우에도 이러한 제한에 유의해야 합니다. 관리 디스크를 사용하는 경우에는 이러한 제한이 적용되지 않습니다. Toouse 프리미엄 저장소를 계획 하는 경우에 관리 되는 디스크를 사용 하는 것이 좋습니다.

저장소 계정에 대해 관련이 다른 항목은 저장소 계정에 Vhd hello 지리적 복제 가져오는지 여부입니다. 지리적 복제를 사용 하도록 설정 하거나 hello VM 수준이 아닌 저장소 계정 수준 hello에를 사용할 수 있습니다. 지리적 복제를 사용 하는 경우 저장소 계정 내에서 다른 Azure 데이터 센터에 복제 됩니다 hello 내의 hello Vhd hello 동일한 지역입니다. 이 결정 하기 전에 hello 다음 제한 사항을 고려해 야:

Azure 지역에서 복제는 VM의 각 VHD에서 로컬로 작동 하 고 hello IOs 시간 순서에 따라 VM의 여러 Vhd에 걸쳐 복제 하지 않습니다. 따라서 hello 나타내는 모든 추가 연결 된 Vhd toohello VM 뿐만 아니라 기본 VM hello는 VHD는 서로 독립적으로 복제 됩니다. 이 없는 hello에서 hello 변경 간 여러 Vhd를 의미 합니다. hello IOs hello 있다는 사실을 복제 hello 순서에 관계 없이 기록 되는 지역에서 복제 없다는 의미입니다 데이터베이스가 여러 Vhd로 분산 된 데이터베이스 서버에 대 한 값입니다. 또한 toohello DBMS에에서도 있을 수 있습니다 다른 응용 프로그램 프로세스를 작성 하거나 여러 Vhd에 및 중요 한 tookeep hello 순서 변경의 경우 데이터를 조작 위치. 이러한 경우가 요구되면 Azure의 지역에서 복제 기능을 사용하지 않도록 설정해야 합니다. 다른 VM 집합이 아닌 특정 VM 집합에 대해 지역에서 복제 기능이 필요한지 또는 이 기능을 원하는지에 따라, 이미 VM 및 관련된 VHD를 지역에서 복제 기능이 사용되거나 사용되지 않도록 설정된 다른 저장소 계정으로 분류할 수 있습니다.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>연결된 디스크에 대한 자동 탑재 설정
- - -
> ![Windows][Logo_Windows] Windows
>
> 자체 이미지나 디스크에서 생성 되는 Vm이 필요한 toocheck 가능 hello 자동 탑재 매개 변수를 설정 합니다. 이 매개 변수를 설정 하면 hello VM을 다시 시작 하거나 Azure toomount hello에 재배포 연결/탑재 된 드라이브 자동으로 다시 후 있습니다.
> hello 매개 변수는 hello Azure Marketplace에에서 Microsoft에서 제공 하는 hello 이미지에 대해 설정 됩니다.
>
> 순서 tooset hello 자동 탑재에 hello 명령줄 실행 diskpart.exe 여기의 hello 설명서를 참조 하세요.
>
> * [DiskPart 명령줄 옵션](https://technet.microsoft.com/library/bb490893.aspx)
> * [Automount](http://technet.microsoft.com/library/cc753703.aspx)
>
> hello Windows 명령줄 창은 관리자 권한으로 열어야 합니다.
>
> 디스크가 연결 되어 있으면 toolog toohello VM tooopen hello Windows 디스크 관리자에에서 필요 합니다. 장에 권장 된 대로 자동 탑재를 사용 하지 않는 경우 [연결 된 디스크에 대 한 자동 탑재 설정][planning-guide-5.5.3], hello을 새로 연결 된 볼륨 > toobe 온라인 되 고 초기화 해야 합니다.
>
> ![Linux][Logo_Linux] Linux
>
> 에 설명 된 대로 tooinitialize 새로 연결 된 빈 디스크를 필요한 [이 여기서][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]합니다.
> 새 디스크 toohello /etc/fstab tooadd 해야합니다.
>
>

- - -
### <a name="final-deployment"></a>최종 배포
Hello에 대 한 최종 배포 및 특히 SAP Extended monitoring toohello 배포 시는 정확한 단계를 참조 하십시오 toohello [배포 가이드][deployment-guide]합니다.

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Azure VM 내에서 실행되는 SAP 시스템에 액세스
클라우드 전용 시나리오에 대 한 hello 간에 tooconnect toothose SAP 시스템을 할 수 있습니다 SAP GUI를 사용 하 여 공용 인터넷 합니다. 이러한 경우 hello 다음 절차 필요 toobe 적용 합니다.

다음과 같은 작용이 hello 문서의 뒷부분에 나오는 다른 주요 시나리오에 hello 온-프레미스 시스템과 Azure 시스템 간의 Azure express 경로 연결 또는 사이트 간 연결 (VPN 터널)를 포함 하는 크로스-프레미스 배포에 연결 tooSAP 시스템 hello 합니다.

### <a name="remote-access-toosap-systems"></a>원격 액세스 tooSAP 시스템
Azure 리소스 관리자는 hello 이전 클래식 모델에서와 같은 더 이상 기본 끝점이 없습니다. 다음과 같은 조건이 충족되면 ARM Azure VM의 모든 포트는 열려 있습니다.

1. 네트워크 보안 그룹 없음 hello 서브넷 또는 hello 네트워크 인터페이스에 대해 정의 됩니다. Vm 네트워크 트래픽 tooAzure 이른바 "네트워크 보안 그룹"을 통해 보호할 수 있습니다. 자세한 내용은 [NSG(네트워크 보안 그룹)란?][virtual-networks-nsg]을 참조하세요.
2. Azure 부하 분산 장치는 hello 네트워크 인터페이스에 대해 정의 된   

차이가 hello 아키텍처 기존 모델 및 ARM에 설명 된 대로 [이 여기서][virtual-machines-azure-resource-manager-architecture]합니다.

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Hello 클라우드 전용 시나리오에 대 한 SAP 시스템, SAP GUI 연결 구성
세부 정보 toothis 항목을 설명 하는이 문서를 참조 하십시오: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>VM 내의 방화벽 설정 변경
가상 컴퓨터 tooallow에서 필요한 tooconfigure hello 방화벽 수도 인바운드 트래픽을 tooyour SAP 시스템입니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> 기본적으로 hello Azure 배포 VM 내에서 Windows 방화벽이 켜져 있습니다. 열린 tooallow hello SAP 포트 toobe 필요 하면, 그렇지 않으면 hello SAP GUI 됩니다 하지 수 tooconnect.
> toodo이:
>
> * 제어판 \ 시스템 및 Security\Windows 방화벽 too'Advanced 설정를 엽니다.
> * 인바운드 규칙을 마우스 오른쪽 단추로 클릭하고 ‘새 규칙’을 선택합니다.
> * Hello에 다음과 같은 마법사는 새 '포트' 규칙을 toocreate 선택 했습니다.
> * Hello 마법사의 다음 단계를 hello 설정을 그대로 두고 hello TCP 및 형식에 원하는 hello 포트 번호에서 tooopen 합니다. 여기서 SAP 인스턴스 ID는 00이므로 3200을 사용했습니다. 인스턴스가 다른 인스턴스 번호가 hello 인스턴스 번호를 기준으로 앞서 정의한 hello 포트 열어야 합니다.
> * Hello hello 마법사의 다음 부분에서는 tooleave hello 연결 허용 ' 항목 ' 확인 해야 합니다.
> * Hello hello 마법사의 다음 단계에서 도메인, 개인 및 공용 네트워크에 대 한 hello 규칙 적용 되는지 여부를 toodefine가 필요 합니다. 조정 하십시오 것 필요한 tooyour 있어야 하는 경우. 그러나 toohave hello 규칙이 적용 toohello 공용 네트워크를 할 hello 공용 네트워크를 통해 외부 hello에서 SAP GUI에 연결 합니다.
> * Hello 마법사의 마지막 단계를 hello hello 규칙의 이름을 고 '마침' 키를 눌러 저장 합니다.
>
> hello 규칙은 즉시 적용 됩니다.
>
> ![포트 규칙 정의][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> hello Linux 이미지 hello Azure Marketplace에서에서 기본적으로 hello iptables 방화벽을 사용 하지 않는 및 hello 연결 tooyour SAP 시스템 작동 해야 합니다. Iptables toohello 설명서를 참조 하십시오 또는 방화벽 tooallow hello 사용 되는 인바운드 tcp 트래픽의 너무 iptables 또는 다른 방화벽을 설정한 경우 포트 32xx (여기서 xx는 SAP 시스템의 hello 시스템 번호)입니다.
>
>

- - -
#### <a name="security-recommendations"></a>보안 권장 사항
hello SAP GUI 연결 하지 즉시 tooany hello SAP 인스턴스 (포트 32xx) 실행 하 고 있지만 hello 포트를 열어야 toohello SAP message server 프로세스 (포트 36xx)를 통해 먼저 연결 합니다. Hello 지난 hello 동일한 포트에서에서 사용 된 hello 메시지 서버 hello 내부 통신 toohello 응용 프로그램 인스턴스에 대해. tooprevent 온-프레미스 응용 프로그램 서버에서 내부 Azure hello 메시지 서버와 통신할 실수로 통신 포트를 변경할 수 있습니다. Hello toochange hello SAP 메시지 서버와 프로젝트 테스트용 개발의 복제본 등의 온-프레미스 시스템에서 복제 된 시스템에서 해당 응용 프로그램 인스턴스 tooa 다른 포트 번호 간의 내부 통신을 적극 권장 등입니다. 이 hello 기본 프로필 매개 변수와 함께 수행할 수 있습니다.

> rdisp/msserv_internal
>
>

에 설명 된 대로 [hello SAP Message Server에 대 한 보안 설정](https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm)

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>SAP 인스턴스의 클라우드 전용 배포 개념
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>SAP NetWeaver 데모/학습 시나리오가 있는 단일 VM
![Azure 클라우드 서비스에서 격리 실행 단일 VM SAP 데모 시스템 hello로 같은 VM 이름][planning-guide-figure-1700]

이 시나리오에서는 (장을 참조 [클라우드 전용] [ planning-guide-2.1] 이 문서의)는 단일 VM에 hello 전체 학습/데모 시나리오가 포함 된 일반적인 학습/데모 시스템 시나리오를 구현 합니다. VM 이미지 템플릿을 통해 hello 배포를 수행할 가정 합니다. 또한 가정 hello hello 있는 Vm 사용 하 여 배포 되는 이러한 데모/학습 Vm 필요 toobe의 여러 같은 이름입니다.

hello 가정은 장의 일부 섹션에 설명 된 대로 VM 이미지를 만든 [Azure 용 SAP와 함께 준비 Vm] [ planning-guide-5.2] 이 문서에 있습니다.

이벤트 tooimplement hello 시나리오의 hello 시퀀스는 다음과 같습니다.

##### <a name="powershell"></a>PowerShell
* 모든 학습/데모 환경에 대한 새 리소스 그룹 만들기

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```
* Toouse 관리 하는 디스크를 표시 하지 않으려는 경우 새 저장소 계정 만들기

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* 새 가상 네트워크 만들기 hello 모든 학습/데모 지형 tooenable hello 사용에 대 한 동일한 호스트 이름 및 IP 주소입니다. hello 가상 네트워크만 SSH에 대 한 트래픽 tooport 3389 tooenable 원격 데스크톱 액세스 및 포트 22 허용 하는 네트워크 보안 그룹에 의해 보호 됩니다.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Hello에서 사용 되는 tooaccess hello 가상 컴퓨터 일 수 있는 새 공용 IP 주소 만들기 인터넷

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Hello 가상 컴퓨터용 새 네트워크 인터페이스 만들기

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* 가상 컴퓨터를 만듭니다. Hello 클라우드 전용 시나리오에 대 한 모든 VM은 hello 동일한 이름입니다. hello hello SAP NetWeaver 인스턴스의 해당 Vm에서의 SAP SID 동일도 hello 합니다. Hello Azure 리소스 그룹 내에서 hello VM의 hello 이름을 toobe 고유 하지만 서로 다른 Azure 리소스 그룹에 hello로 Vm을 실행할 수 같은 이름입니다. 기본 '관리자' 계정은 Windows hello 또는 Linux에 대 한 ' 루트' 유효 하지 않습니다. 따라서 새 관리자 사용자 이름 암호와 함께 정의 toobe가 필요 합니다. hello VM의 hello 크기는 toobe 정의 필요 합니다.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES-SAP" -Skus "12-SP1" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "Oracle" -Offer "Oracle-Linux" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a Managed Disk Image
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -Id <Id of Managed Disk Image>
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* 필요에 따라 디스크를 더 추가하고 필요한 콘텐츠를 복원합니다. 모든 blob (Url toohello blob) 이름은 Azure 내에서 고유 해야 한다는 점에 유의.

```powershell
# Optional: Attach additional VHD data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM

# Optional: Attach additional Managed Disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -DiskSizeInGB 1023 -CreateOption empty -Lun 0 | Update-AzureRmVM
```

##### <a name="cli"></a>CLI
linux 코드 예제에서는 다음 hello는 사용할 수 있습니다. Windows, 하십시오 하나 위에서 설명한 것 처럼 PowerShell을 사용 하 여 또는 적용 $rgName 대신 hello 예제 toouse %rgName% 하 고 hello Windows 명령을 사용 하 여 hello 환경 변수 설정 *설정*합니다.

* 모든 학습/데모 환경에 대한 새 리소스 그룹 만들기

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
az group create --name $rgName --location "North Europe"
```

* 새 저장소 계정 만들기

```
az storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku Standard_LRS --name $rgNameLower
```

* 새 가상 네트워크 만들기 hello 모든 학습/데모 지형 tooenable hello 사용에 대 한 동일한 호스트 이름 및 IP 주소입니다. hello 가상 네트워크만 SSH에 대 한 트래픽 tooport 3389 tooenable 원격 데스크톱 액세스 및 포트 22 허용 하는 네트워크 보안 그룹에 의해 보호 됩니다.

```
az network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

az network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
az network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group SAPERPDemoNSG
```

* Hello에서 사용 되는 tooaccess hello 가상 컴퓨터 일 수 있는 새 공용 IP 주소 만들기 인터넷

```
az network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --dns-name $rgNameLower --allocation-method Dynamic
```

* Hello 가상 컴퓨터용 새 네트워크 인터페이스 만들기

```
az network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-address SAPERPDemoPIP --subnet Subnet1 --vnet-name SAPERPDemoVNet
```

* 가상 컴퓨터를 만듭니다. Hello 클라우드 전용 시나리오에 대 한 모든 VM은 hello 동일한 이름입니다. hello hello SAP NetWeaver 인스턴스의 해당 Vm에서의 SAP SID 동일도 hello 합니다. Hello Azure 리소스 그룹 내에서 hello VM의 hello 이름을 toobe 고유 하지만 서로 다른 Azure 리소스 그룹에 hello로 Vm을 실행할 수 같은 이름입니다. 기본 '관리자' 계정은 Windows hello 또는 Linux에 대 한 ' 루트' 유효 하지 않습니다. 따라서 새 관리자 사용자 이름 암호와 함께 정의 toobe가 필요 합니다. hello VM의 hello 크기는 toobe 정의 필요 합니다.

```
#####
# Create virtual machines using storage accounts
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password

#####
# Create virtual machines using Managed Disks
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd> --authentication-type password

#####
# Create a new virtual machine with a Managed Disk Image
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id> --authentication-type password
```

* 필요에 따라 디스크를 더 추가하고 필요한 콘텐츠를 복원합니다. 모든 blob (Url toohello blob) 이름은 Azure 내에서 고유 해야 한다는 점에 유의.

```
# Optional: Attach additional VHD data disks
az vm unmanaged-disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --vhd-uri https://$rgNameLower.blob.core.windows.net/vhds/data.vhd  --new

# Optional: Attach additional Managed Disks
az vm disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --disk datadisk --new
```

##### <a name="template"></a>템플릿
Github의 azure-빠른 시작-템플릿 리포지토리 hello에 hello 예제 서식 파일을 사용할 수 있습니다.

* [간단한 Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [간단한 Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [이미지의 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Azure 내에서 toocommunicate 해야 하는 Vm 집합 구현
이 클라우드 전용 시나리오는 여기서 hello hello 데모/학습 시나리오를 나타내는 소프트웨어가 걸쳐 여러 Vm 데모 및 학습 목적에 대 한 일반적인 시나리오입니다. hello 다른 구성 요소 hello 다른 Vm 필요 toocommunicate 서로에서 설치 됩니다. 또한 이 시나리오에서는 온-프레미스 네트워크 통신이나 크로스-프레미스 시나리오가 필요하지 않습니다.

이 시나리오는 장에서 설명 하는 hello 설치의 확장 [단일 VM SAP NetWeaver 데모/학습 시나리오와] [ planning-guide-7.1] 이 문서의. 이 경우 기존 리소스 그룹 tooan 가상 컴퓨터를 더 추가 됩니다. 다음 예제에서는 hello 교육 가로 hello에는 SAP ASCS/SCS VM DBMS 및 SAP 응용 프로그램 서버 인스턴스 VM 실행 하는 VM 구성 됩니다.

이 시나리오를 작성 하기 전에 하기 전에 hello 시나리오에서 이미 살펴보았던 기본 설정에 대 한 toothink을 해야 합니다.

#### <a name="resource-group-and-virtual-machine-naming"></a>리소스 그룹 및 가상 컴퓨터 이름 지정
모든 리소스 그룹 이름은 고유해야 합니다. `<rg-name`>-접미사와 같은 리소스의 고유한 이름 지정 체계를 개발합니다.

hello 가상 컴퓨터 이름에 toobe hello 리소스 그룹 내에서 고유 합니다.

#### <a name="set-up-network-for-communication-between-hello-different-vms"></a>간의 통신을 위한 네트워크 설정 hello 여러 Vm
![Azure 가상 네트워크 내의 VM 집합][planning-guide-figure-1900]

이름 hello의 복제본으로 충돌 같은 학습/데모 지형 tooprevent 모든 가로 toocreate Azure 가상 네트워크 사용 해야 합니다. Azure가 DNS 이름 확인을 제공 하거나 Azure (하지 toobe 여기에 설명 추가) 외부 자체 DNS 서버를 구성할 수 있습니다. 이 시나리오에서는 자체 DNS를 구성하지 않습니다. 단일 Azure Virtual Network 내의 모든 가상 컴퓨터의 경우 호스트 이름을 통한 통신이 사용되도록 설정됩니다.

hello 이유 tooseparate 학습 또는 데모 지형을 가상 네트워크 및 뿐만 아니라 리소스 그룹 수 있습니다:

* SAP hello 자체 AD/OpenLDAP와 각 hello 지형 도메인 서버 요구 toobe 파트가 요구 설정한 대로 가로입니다.  
* 설정에 구성 요소 고정된 IP 주소와 해당 필요 toowork SAP 지형을 hello 합니다.

Azure 가상 네트워크와 어떻게 toodefine 하에서 확인할 수 있습니다 하는 방법에 대 한 자세한 내용은 [이 여기서][virtual-networks-create-vnet-arm-pportal]합니다.

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>회사 네트워크 연결을 사용하여 SAP VM 배포(프레미스 간)
SAP 지형을 실행 하 고 고급 DBMS 서버용 베어 메탈 간에 toodivide hello 배포, SAP 시스템과 Azure IaaS 응용 프로그램 계층 및 보다 작은 2 계층에 대 한 온-프레미스 가상화 된 환경을 구성 합니다. 하나의 SAP 지형 내의 SAP 시스템에 필요 하며 서로 및 많은 기타 소프트웨어 구성 요소 배포 형식에 관계 없이 hello 회사에 배포 된 toocommunicate 이라고 하는 hello 기본 가정 합니다. 또한 있어야 hello 배포에 따른 차이가 hello 최종 사용자가 SAP GUI 나 기타 인터페이스를 사용 하 여 연결 합니다. 이러한 조건이 발생 한 경우에 충족 수 hello 온-프레미스 Active Directory/OpenLDAP 및 DNS 서비스 toohello 사이트-에-사이트/다중 사이트 연결 또는 Azure express 경로 같은 개인 연결을 통해 Azure 시스템을 확장 합니다.

Azure의 SAP 구현 세부 사항을 hello에 백그라운드 더 순서 tooget에서 좋습니다 tooread 장 [SAP 인스턴스의 개념의 클라우드 전용 배포] [ planning-guide-7] 설명 하는이 문서의 hello 기본 사항 중 일부는 Azure와 이러한 사용 방법을 Azure에서 SAP 응용 프로그램과 함께 생성 합니다.

### <a name="scenario-of-an-sap-landscape"></a>SAP 지형 시나리오
hello 크로스-프레미스 시나리오 설명할 수 있습니다 대략 같은 아래 hello 그래픽:

![온-프레미스와 Azure 자산 간의 사이트 간 연결][planning-guide-figure-2100]

위에 표시 된 hello 시나리오 hello 온-프레미스 AD/OpenLDAP 있고 DNS tooAzure 확장 있는 시나리오를 설명 합니다. Hello 온-프레미스 측에서는 특정 IP 주소 범위가 Azure 구독 당으로 예약 됩니다. hello IP 주소 범위는 Azure 가상 네트워크 tooan hello Azure 측에 할당 됩니다.

#### <a name="security-considerations"></a>보안 고려 사항
hello 최소 요구 사항을 보안 통신 프로토콜의 hello 사용 같은 수준이 브라우저 액세스에 대 한 SSL/TLS 또는 시스템에 대 한 VPN 기반 연결에 대 한 액세스 toohello Azure 서비스입니다. hello 간주 회사 회사별로 회사 네트워크와 Azure 간에 VPN 연결 hello 매우 다르게 처리 됩니다. 일부 회사에서는 모든 hello 포트를 대충 열어 수 있습니다. 일부 회사에서는 경우가 toobe 매우 정확한 tooopen 등 필요한 포트에.

일반적인 SAP 아래 hello 표에 통신 포트가 나와 있습니다. 기본적으로 충분 한 tooopen hello SAP 게이트웨이 포트만 것입니다.

| 부여 | 포트 이름 | 예: `<nn`> = 01 | 기본 범위(최소-최대) | 주석 |
| --- | --- | --- | --- | --- |
| 디스패처 |sapdp`<nn>` 참조: * |3201 |3200 – 3299 |SAP 디스패처, Windows 및 Java용 SAP GUI에서 사용 |
| 메시지 서버 |sapms`<sid`> 참조: ** |3600 |제한 없는 sapms`<anySID`> |sid = SAP-System-ID |
| 게이트웨이 |sapgw`<nn`> 참조: * |3301 |제한 없음 |SAP 게이트웨이, CPIC 및 RFC 통신에 사용 |
| SAP 라우터 |sapdp99 |3299 |제한 없음 |유일한 CI (중앙 인스턴스) 서비스 이름은 설치 후 /etc/services tooan 임의의 값에 할당 될 수 있습니다. |

*) nn = SAP 인스턴스 번호

**) sid = SAP-System-ID

여러 SAP 제품에 필요한 포트 또는 SAP 제품 서비스에 대한 자세한 내용은 여기 <http://scn.sap.com/docs/DOC-17124>에서 확인할 수 있습니다.
이 문서와 전용 수 tooopen 포트 특정 SAP 제품 및 시나리오에 필요한 hello VPN 장치에 있어야 합니다.

다른 보안 조치 toocreate 수 이러한 시나리오에서 Vm을 배포 하는 경우는 [네트워크 보안 그룹] [ virtual-networks-nsg] toodefine 액세스 규칙입니다.

### <a name="dealing-with-different-virtual-machine-series"></a>다른 가상 컴퓨터 시리즈 처리
Microsoft에서는 지난 12 개월 동안 hello 과정에서 많은 더 많은 VM 메모리 Vcpu 수에서 다른 형식을 추가 하거나 더 중요 한 하드웨어에서 실행 되 고 합니다. 이러한 모든 VM이 SAP에서 지원되는 것은 아닙니다(SAP 정보 [1928533]에서 지원되는 VM 형식 참조). 해당 VM 중 일부는 다른 호스트 하드웨어 세대에서 실행됩니다. 이러한 호스트 하드웨어 세대 hello 세분성에는 Azure 확장 단위에 배포 시작 됩니다. 여기서 선택한에서 실행할 수 없습니다. hello 다른 VM 크기 hello 동일한 확장 단위 의미의 경우 발생할 수 있습니다. 가용성 집합에 다른 하드웨어를 기반으로 확장 단위 hello 기능 toospan 제한 됩니다.  예를 들어 toorun hello A5-A11 Vm에서 DBMS 및 hello G 시리즈 Vm에서 SAP 응용 프로그램 계층을 할 수 하는 경우 단일 SAP 시스템 또는 다른 가용성 집합 내에서 서로 다른 SAP 시스템 toodeploy 강제에 합니다.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Azure의 SAP 인스턴스에서 로컬 네트워크 프린터로 인쇄
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>프레미스 간 시나리오에서 TCP/IP를 통해 인쇄
Azure VM에서 온-프레미스 TCP/IP 기반 네트워크 프린터 설정은 전체 hello VPN 사이트 간 터널 또는 express 경로 연결을 설정할 필요가 가정 하 고 회사 네트워크와 동일 합니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo이:
>
> * 네트워크 프린터 중 일부는 구성 마법사는 Azure VM에서 프린터를 쉽게 tooset 있도록가 함께 제공 됩니다. 마법사 소프트웨어가 되지 않은 경우 프린터 hello "수동"으로 hello 프린터를 tooset toocreate 새 TCP/IP 프린터 포트는와 함께 배포 합니다.
> * 열기 제어판 -> 장치 및 프린터 -> 프린터 추가 열기
> * TCP/IP 주소 또는 호스트 이름을 사용하여 프린터 추가 선택
> * Hello hello 프린터의 IP 주소 입력
> * 프린터 포트 표준 9100
> * 필요한 경우 hello 적절 한 프린터 드라이버를 수동으로 설치 합니다.
>
> ![Linux][Logo_Linux] Linux
>
> * Windows 적시에 따라 hello 표준 절차 tooinstall 네트워크 프린터와 같은
> * hello에 대 한 공용 Linux 가이드를 따르십시오 [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) 또는 [Red Hat 및 Oracle Linux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) 방법에는 프린터 tooadd 합니다.
>
>

- - -
![네트워크 인쇄][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>프레미스 간 시나리오에서 SMB를 통한 호스트 기반 프린터(공유 프린터)
호스트 기반 프린터는 기본적으로 네트워크와 호환되지 않습니다. 하지만 hello 프린터에 연결 된 tooa 전원이 켜진 컴퓨터는 네트워크 상의 컴퓨터 간에 호스트 기반 프린터를 공유할 수 있습니다. 회사 네트워크를 사이트 간 또는 Express 경로에 연결하고 로컬 프린터를 공유합니다. hello SMB 프로토콜 이름 서비스로 DNS가 아닌 NetBIOS를 사용합니다. hello NetBIOS 호스트 이름은 hello DNS 호스트 이름과 다를 수 있습니다. hello 표준 대/소문자는 hello NetBIOS 호스트 이름과 hello DNS 호스트 이름을 동일 합니다. hello DNS 도메인 않습니다 hello NetBIOS 이름 공간에 의미가 없습니다. Hello DNS 호스트 이름으로 이루어진 정규화 된 DNS 호스트 이름을 적절 하 게 hello 및 DNS 도메인 hello NetBIOS 이름 공간에서 사용 하면 안 됩니다.

hello 프린터 공유 hello 네트워크에서 고유한 이름으로 식별 됩니다.

* (항상 필요) hello SMB 호스트의 호스트 이름입니다.
* Hello 공유 (항상 필요)의 이름입니다.
* 프린터 공유 hello에 없는 경우 hello 도메인의 이름을 SAP 시스템과 같은 도메인입니다.
* 또한 사용자 이름 및 암호 필요 tooaccess hello 프린터 공유를 수 있습니다.

방법:

- - -
> ![Windows][Logo_Windows] Windows
>
> 로컬 프린터를 공유합니다.
> Hello Azure VM에서에서 Windows 탐색기 hello 및 hello 프린터의 hello 공유 이름 입력을 엽니다.
> 프린터 설치 마법사는 hello 설치 과정을 안내 합니다.
>
> ![Linux][Logo_Linux] Linux
>
> 다음은 Linux의 네트워크 프린터 구성에 대한 설명서의 몇 가지 예입니다. 여기에는 Linux의 인쇄에 대한 장도 포함되어 있습니다. Hello 작동할지 hello VM으로 Azure Linux VM에서 같은 방식으로 VPN의 일부입니다.
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_(Samba)_Share_or_Windows_Share>
> * RHEL 또는 Oracle Linux <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Printer_Configuration.html#s1-printing-smb-printer>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>USB 프린터(프린터 전달)
Hello 원격 데스크톱 서비스 tooprovide 사용자 hello 액세스의 Azure hello 능력 원격 세션에서 tootheir 로컬 프린터 장치를 사용할 수 없습니다.

- - -
> ![Windows][Logo_Windows] Windows
>
> Windows 인쇄에 대한 자세한 내용은 여기 <http://technet.microsoft.com/library/jj590748.aspx>에서 찾을 수 있습니다.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>프레미스 간에 SAP Azure 시스템을 Correction and Transport System(TMS)에 통합
SAP Change and Transport System (TMS) 요구 구성 toobe tooexport hello 하 고 hello 지형 내의 시스템 간에 전송 요청을 가져옵니다. 반면 hello QA (품질 보증) 및 생산 시스템 (PRD)는 온-프레미스 SAP 시스템 (DEV)의 개발 인스턴스 hello Azure에 살고 있는 가정 합니다. 또한 중앙 전송 디렉터리가 있다고 가정합니다.

##### <a name="configuring-hello-transport-domain"></a>Hello 전송 도메인 구성
에 설명 된 대로 전송 도메인 컨트롤러를 hello으로 지정 하는 hello 시스템에서 전송 도메인 구성 [전송 도메인 컨트롤러 구성 hello](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm)합니다. 시스템 사용자 tmsadm에 게 만들어집니다 및 hello RFC 대상을 생성 됩니다 필요 합니다. Hello 트랜잭션 s m 59를 사용 하 여 이러한 RFC 연결을 확인할 수 있습니다. 전송 도메인 전체에서 호스트 이름 확인을 사용할 수 있어야 합니다.

방법:

* 이 시나리오에서 hello 온-프레미스 QAS 시스템을 CTS 도메인 컨트롤러로 hello 수를 결정 했습니다. 트랜잭션 STMS를 호출합니다. hello TMS 대화 상자가 나타납니다. 전송 도메인 구성 대화 상자가 표시됩니다. 이 대화 상자는 전송 도메인을 아직 구성하지 않은 경우에만 나타납니다.
* 해당 자동으로 생성 하는 hello 사용자 tmsadm에 게 권한이 있는지 확인 (s m 59-> ABAP 연결-> TMSADM@E61.DOMAIN_E61 -> 세부 정보-유틸리티 > 권한 부여 테스트->). 트랜잭션의 hello 초기 화면 STMS이 SAP 시스템 이제 다음 그림과 같이 hello 전송 도메인의 hello 컨트롤러로 작동 하는지 표시 됩니다.

![Hello 도메인 컨트롤러에서 트랜잭션 STMS의 초기 화면][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Hello 전송 도메인에에서 SAP 시스템 포함
전송 도메인에 SAP 시스템을 포함 하 여 hello 시퀀스 모양은 다음과 같습니다.

* Azure의 DEV 시스템 hello toohello 전송 시스템 (클라이언트 000) 이동 하 고 트랜잭션 STMS를 호출 합니다. 기타 구성 hello 대화 상자에서 선택한 도메인에 시스템 포함을 계속 합니다. 도메인 컨트롤러 hello 대상 호스트로 지정 ([hello 전송 도메인에에서 SAP 시스템 포함](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). hello 시스템 대기 toobe hello 전송 도메인에 포함 되었습니다.
* 보안상의 이유로 다음 해야 toogo 백 toohello 도메인 컨트롤러 tooconfirm 요청 합니다. 시스템 개요와 승인을 선택 hello 대기 중인 시스템의 합니다. 다음 hello 프롬프트 및 hello 구성 배포 되는 것으로 확인 합니다.

이 SAP 시스템은 이제 모든 hello에 대 한 필요한 정보를 hello hello 전송 도메인의 다른 SAP 시스템 포함 됩니다. Hello에 이와 hello 주소 tooall hello 다른 SAP 시스템 및 SAP 시스템 hello hello 전송 제어 프로그램의 hello 전송 프로필에 입력 된 hello 새 SAP 시스템의 데이터 전송 됩니다. Hello 도메인의 toohello 전송 디렉터리에 액세스와 Rfc가 작동 하는지 여부를 확인 합니다.

전송 시스템 hello 구성을 hello 설명서에 설명 된 대로 평소 대로 계속 [Change and Transport System](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)합니다.

방법:

* 온-프레미스의 STMS가 올바르게 구성되어 있는지 확인합니다.
* Visa, 그 Azure에서 가상 컴퓨터에서 hello 전송 도메인 컨트롤러의 hello 호스트 이름을 확인할 수 있는지 확인 합니다.
* 트랜잭션 STMS 호출 -> 기타 구성 -> 도메인에 시스템 포함
* Hello hello 프레미스 TMS 시스템에서 연결을 확인 합니다.
* 전송 경로, 그룹 및 계층을 일반적인 방식으로 구성합니다.

사이트 간 연결 된 크로스-프레미스 시나리오, 온-프레미스와 Azure 간의 hello 대기 시간이 길 수 있습니다. 개발 및 테스트 시스템 tooproduction 통해 개체에 전송 hello 시퀀스를 따르거나 전송 적용 म 또는 지원 패키지 toohello 서로 다른 시스템을 있습니다 한다는 것을 알아야 hello 중앙 전송의 hello 위치에 종속 디렉터리, 일부 hello 시스템 hello 중앙 전송 디렉터리에 데이터를 쓰거나 읽는 높은 대기 시간이 발생 합니다. hello 상황은 데이터 센터 hello 멀리 떨어져 있는 다른 데이터 센터를 통해 hello 다른 시스템을 분산 하는 위치와 유사한 tooSAP 가로 구성입니다.

이러한 대기 시간과 관련 toowork 정렬 하며 hello 시스템 작업을 빠르게에서 읽기 또는 쓰기 tooor hello 전송 디렉터리 Azure 및 링크 hello 전송 도메인에 두 개의 STMS 전송 도메인 (온-프레미스에 대 한. 및 hello 시스템과 하나를 설정할 수 Hello 원리 hello SAP TMS에서에서이 개념을 설명 하는이 설명서를 확인 하십시오: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/frameset.htm>합니다.

방법:

* 트랜잭션 STMS를 사용하여 각 위치(온-프레미스 및 Azure)에서 전송 도메인 설정 <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* 도메인 링크를 사용 하 여 hello 도메인을 링크 하 고 hello 두 도메인 간에 hello 링크를 확인 합니다.
  <http://help.sap.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/content.htm>
* Hello 구성 toohello 연결 된 시스템을 배포 합니다.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Azure 및 온-프레미스에 있는 SAP 인스턴스 간의 RFC 트래픽(프레미스 간)
Azure 및 온-프레미스에 있는 시스템 간의 RFC 트래픽 toowork가 필요 합니다. tooset 연결을 호출 트랜잭션 s m 59를 소스 시스템 toodefine 해야 하는 hello 대상 시스템에 대 한 RFC 연결 합니다. hello 구성은 RFC 연결의 유사한 toohello 표준 설치 합니다.

Hello 크로스-프레미스 시나리오에서 서로 toocommunicate 해야 하는 SAP 시스템을 실행된 중인 hello Vm hello 같은 도메인을 가정 합니다. 따라서 hello SAP 시스템 간의 RFC 연결의 설치와 동일 hello 설정 단계 및 온-프레미스 시나리오에서 입력 합니다.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Azure에 있는 SAP 인스턴스의 '로컬' 파일 공유에 액세스하기 또는 그 반대로 액세스하기
Azure에 있는 SAP 인스턴스 tooaccess 파일 공유 hello 회사 프레미스 내의 필요 합니다. 또한 온-프레미스 SAP 인스턴스가 Azure에 있는 파일 공유를 tooaccess 필요 합니다. tooenable hello 파일 공유 hello 권한과 hello 로컬 시스템의 공유 옵션을 구성 해야 합니다. Hello VPN 또는 express 경로 연결 데이터 센터와 Azure 사이 있는지 tooopen hello 포트를 확인 합니다.

## <a name="supportability"></a>지원 가능성
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>SAP용 Azure 모니터링 솔루션
중요 업무용 SAP 시스템에 Azure hello SAP의 tooenable hello 모니터링 순서 모니터링 도구인 SAPOSCOL 또는 SAP 호스트 에이전트 SAP 용 Azure 모니터링 확장을 통해 hello Azure 가상 컴퓨터 서비스 호스트에서 데이터를 가져옵니다. Microsoft 결정 하지 toogenerically 구현 hello 필요한 기능을 Azure로 SAP에서 hello 요구 된 매우 구체적인 tooSAP 응용 프로그램을 이후 했지만 고객 toodeploy hello 필요한 모니터링 구성 요소와 구성을 tootheir 위해 남겨 둘 Azure에서 실행 중인 가상 컴퓨터입니다. 그러나 배포 및 수명 주기 관리의 구성 요소를 모니터링 하는 hello는 대부분을 자동으로 Azure.

#### <a name="solution-design"></a>솔루션 디자인
Azure VM 에이전트 및 확장 프레임 워크의 hello 아키텍처에 따라은 SAP Monitoring tooenable 개발 하는 hello 솔루션. hello Azure VM 에이전트 및 확장 프레임 워크의 hello 아이디어는 소프트웨어 응용 프로그램 사용 가능한 VM 내에서 hello Azure VM 확장 갤러리에서 tooallow 설치입니다. 이 개념의 기본 개념은의 경우 같은 SAP 용 Azure 모니터링 확장 hello tooallow 원칙 hello, hello 한 특수 기능 배포 시 해당 소프트웨어의 VM 및 hello 구성으로 배포 합니다.

' Azure VM 에이전트 ' hello Azure 포털에서에서 VM 생성 시 기본적으로 VM은 Windows Vm에 주입 된 hello 내에서 특정 Azure VM 확장의 처리를 사용 하는 번호입니다. SUSE, Red Hat 또는 Oracle Linux, 발생 한 경우 hello VM 에이전트가 이미 Azure 마켓플레이스 이미지의 일부입니다. Linux VM을 업로드 합니다 하나 경우 온-프레미스 tooAzure hello VM 에이전트에 toobe 수동으로 설치 합니다.

Azure의 hello 모니터링 솔루션의 기본 구성 요소를 다음과 같이 표시 된 SAP에 대 한 hello:

![Microsoft Azure 확장 구성 요소][planning-guide-figure-2400]

Hello 위의 블록 다이어그램에 나와 있는 것 처럼 hello SAP 용 모니터링 솔루션의 한 부분 hello Azure VM 이미지와 Azure Operations에서 관리 되는 전역 복제 리포지토리인 Azure 확장 갤러리에서 호스트 됩니다. hello hello hello Azure Operations toopublish hello SAP 용 Azure 모니터링 확장의 새로운 버전으로 SAP toowork의 Azure 구현에서 작업 하는 공동 SAP/MS 팀의 합니다.

새 Windows VM을 배포 하면 ' Azure VM 에이전트 ' hello hello VM에 자동으로 추가 됩니다. hello이이 에이전트의 기능은 로드 toocoordinate hello 및 hello Azure 확장의 구성에 대 한 SAP NetWeaver 시스템 모니터링 합니다. Linux Vm에 대 한 hello Azure VM 에이전트가 이미 hello Azure 마켓플레이스 OS 이미지의 일부입니다.

그러나 여전히 toobe hello 고객에 의해 실행 해야 하는 단계는. 이것이 hello 사용 및 성능 수집-hello의 구성입니다. hello 프로세스 관련 toohello '구성' PowerShell 스크립트 또는 CLI 명령에 의해 자동으로 수행 합니다. PowerShell 스크립트 hello hello에 설명 된 대로 hello Microsoft Azure 스크립트 센터에서에서 다운로드할 수 있습니다 [배포 가이드][deployment-guide]합니다.

hello hello의 전체 아키텍처 SAP 용 Azure 모니터링 솔루션은 다음과 같습니다.

![SAP NetWeaver용 Azure 모니터링 솔루션][planning-guide-figure-2500]

**Hello 정확한 방법-tooand 이러한 PowerShell cmdlet 또는 명령 CLI 사용 하 여 배포 시의 자세한 단계를 따라 hello에 제공 된 hello 지침 [배포 가이드][deployment-guide]합니다.**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Azure 배치 SAP 인스턴스를 SAProuter에 통합
Azure에서 실행 되는 SAP 인스턴스 필요 toobe SAProuter에서 액세스할 수 있는 합니다.

![SAP-라우터 네트워크 연결][planning-guide-figure-2600]

SAProuter 직접 IP 연결 하는 경우 참여 시스템 간에 TCP/IP 통신을 hello 수 있습니다. 네트워크 수준에서 hello 통신 파트너 간의 종단 간 연결 없음 필요 하다는 hello 이점이 제공 합니다. SAProuter hello 3299 기본적으로 포트에서 수신 대기 합니다.
SAProuter를 통해 tooconnect SAP 인스턴스 toogive hello SAProuter 문자열 및 모든 시도가 tooconnect 호스트 이름이 필요 합니다.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
지금까지 hello 문서의 hello 초점은 SAP NetWeaver 일반적 했거나 hello SAP NetWeaver ABAP 스택에 있습니다. 이번 소 단원에서는 hello SAP Java 스택에 대 한 특정 고려 사항도 나열 됩니다. Hello 가장 중요 한 SAP NetWeaver Java만 기반 응용 프로그램 중 하나는 hello SAP Enterprise Portal입니다. SAP PI, SAP Solution Manager 사용할 SAP NetWeaver ABAP hello 및 Java 스택을 모두와 다른 SAP NetWeaver 기반 응용 프로그램입니다. 따라서 확실히 스택이 필요 tooconsider 특정 측면 관련된 toohello SAP NetWeaver Java도 합니다.

### <a name="sap-enterprise-portal"></a>SAP Enterprise Portal
크로스-프레미스 시나리오에서 배포 하는 경우 온-프레미스 설치에서 SAP Portal Azure 가상 컴퓨터에 설치 하는 hello 다르지 않습니다. Hello DNS는 온-프레미스에서 수행 됩니다, 이후 hello 개별 인스턴스의 포트 설정 hello 구성 된 온-프레미스로 수행할 수 있습니다. hello 권장 사항 및 지금까지이 문서에 설명 된 제한 사항을 일반적 SAP Enterprise Portal 또는 SAP NetWeaver Java 스택에도 hello와 같은 응용 프로그램에 적용 됩니다.

![공개된 SAP 포털][planning-guide-figure-2700]

일부 고객이 특수 배포 시나리오로 hello hello SAP Enterprise Portal toohello 인터넷에 직접 표시 상태인 hello 가상 컴퓨터 호스트는 사이트 간 VPN 터널 또는 express 경로 통해 연결 된 toohello 회사 네트워크입니다. 이 시나리오에서는 특정 포트를 열고 방화벽 또는 네트워크 보안 그룹에 의해 차단 되지 않음 되었는지 toomake를 구조가 있습니다. hello 동일한 방법을 해야 toobe 온-프레미스에서 클라우드 전용 시나리오에서 tooconnect tooan SAP Java 인스턴스를 사용할 때 적용 합니다.

hello 초기 포털 URI는 http (s):`<Portalserver`>: 5XX00/irj hello 포트 50000 + (시스템 번호 × 100) 하 여 형성 되는 위치입니다. hello 기본 포털 URI의 SAP 시스템 00은 `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj 합니다. 자세한 내용은 <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>을 참조하세요.

![끝점 구성][planning-guide-figure-2800]

Toocustomize hello URL 및/또는 SAP Enterprise Portal의 포트를 원하는 경우에이 설명서를 참조 하세요.

* [포털 URL 변경](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [기본 포트 번호, 포털 포트 번호 변경](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Azure Virtual Machines에서 실행되는 SAP NetWeaver의 HA(고가용성) 및 DR(재해 복구)
### <a name="definition-of-terminologies"></a>용어 정의
hello 용어 **고가용성 (HA)** 은 일반적으로 관련된 tooa 설정 기술을 통해 IT 서비스의 비즈니스 연속성을 제공 하 여 IT 작업 중단을 최소화 하는 중복 되는, 내결함성 장애 조치 보호 되는 구성 요소 hello 내부 **동일한** 데이터 센터입니다. 우리의 경우에는 단일 Azure 지역 내부에서의 고가용성이 고려됩니다.

**DR(재해 복구)** 또한 IT 서비스 중단을 최소화하고 복구를 수행하는 것을 목표로 하지만 일반적으로 수백 킬로미터 거리에 있는 **여러 다른** 데이터 센터 간에 발생하게 됩니다. 경우에 hello 내에서 서로 다른 Azure 지역 간의 일반적으로 동일한 지리적 지역 고객으로 서 사용자가 설정한 값에 따라 또는 합니다.

### <a name="overview-of-high-availability"></a>고가용성 개요
고가용성에 대 한 SAP Azure에서 두 부분으로 hello 토론 분리 수 있습니다.:

* **Azure 인프라 고가용성** - 계산(VM), 네트워크, 저장소 등의 HA와 이러한 HA가 SAP 응용 프로그램 가용성 향상에 주는 이점
* **SAP 응용 프로그램 고가용성** - 다음과 같은 SAP 소프트웨어 구성 요소의 HA
  * SAP 응용 프로그램 서버
  * SAP ASCS/SCS 인스턴스
  * DB 서버

및 Azure 인프라 HA와 결합되는 방식

Azure에서 고가용성 SAP 온-프레미스 물리적 또는 가상 환경에서 일부 차이점 비교 tooSAP 고가용성에 있습니다. hello 다음 SAP에서 백서는 Windows에서 가상화 된 환경에서 표준 SAP 고가용성 구성을: <http://scn.sap.com/docs/DOC-44415>합니다. Windows의 경우와 마찬가지로 Linux용 sapinst 통합 SAP-HA 구성은 없습니다. Linux용 온-프레미스 SAP HA에 대한 자세한 내용은 <http://scn.sap.com/docs/DOC-8541>에서 확인할 수 있습니다.

### <a name="azure-infrastructure-high-availability"></a>Azure 인프라 고가용성
현재 단일 VM SLA는 99.9%입니다. tooget 관념 hello 제품의 빌드 단순히 수 같은 단일 VM의 가용성을 hello 같습니다 방법 hello 사용할 수 있는 다양 한 Azure Sla: <https://azure.microsoft.com/support/legal/sla/>합니다.

hello 계산에 대 한 hello 단위로 매월 또는 43200 분 30 일입니다. 따라서 가동 중지 시간 0.05% 해당 too21.6 분입니다. 일반적으로 hello 서로 다른 서비스의 가용성을 hello hello 방식으로 다음에서 곱하기 됩니다.

(가용성 서비스 #1/100) * (가용성 서비스 #2/100) * (가용성 서비스 #3/100) *…

결과는 다음과 같습니다.

(99.95/100) * (99.9/100) * (99.9/100) = 0.9975 또는 전체 가용성 99.75%

#### <a name="virtual-machine-vm-high-availability"></a>VM(가상 컴퓨터) 고가용성
가상 컴퓨터의 hello 가용성에 영향을 줄 수 있는 Azure 플랫폼 이벤트에 두 가지: 계획 된 유지 관리 계획 되지 않은 유지 관리 합니다.

* 계획 된 유지 관리 이벤트 Azure 플랫폼 tooimprove 기본 Microsoft toohello를 통한 정기적인 업데이트는 전체 안정성, 성능 및 가상 컴퓨터에서 실행 되는 hello 플랫폼 인프라의 보안을 합니다.
* 계획 되지 않은 유지 관리 이벤트에는 어떤 방식으로든에서 hello 하드웨어 또는 기본 가상 컴퓨터가 실제 인프라에 오류가 발생 하는 경우 발생 합니다. 여기에는 로컬 네트워크 오류, 로컬 디스크 오류 또는 기타 랙 수준의 오류가 포함될 수도 있습니다. 이러한 오류가 감지 되 면 hello Azure 플랫폼 hello 비정상 물리적 서버에 가상 컴퓨터 tooa 정상 물리적 서버를 호스트에서 가상 컴퓨터를 자동으로 마이그레이션합니다. 이러한 이벤트는 경우는 드물기 하지만 가상 컴퓨터 tooreboot 발생할 수 있습니다.

이 설명서에서 자세한 내용을 찾을 수 있습니다. <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Azure 저장소 중복성
Microsoft Azure 저장소 계정에 hello 데이터는 항상 복제 tooensure 내 구성과 고가용성을 일시적인 하드웨어 오류의 hello 면 에서도 hello Azure 저장소 SLA를 충족 합니다.

Azure 저장소는 기본적으로 세 개의 이미지 hello 데이터의 동기화가, 이후 RAID5 또는 여러 Azure 디스크에 걸쳐 RAID1 필요 하지 않습니다.

이 문서에서 자세한 내용을 찾을 수 있습니다. <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Azure 인프라 VM이 다시 시작 tooAchieve SAP 응용 프로그램의 "고가용성 정보"를 사용 하 여
Windows Server 장애 조치 클러스터링 (WSFC) 또는 Pacemaker linux와 같은 toouse 기능 하지 않으려면 (현재만 이상 SLES 12에 지원 됨), 과소 tooprotect hello의 계획 되거나 계획 되지 않은 가동 중지 시간 으로부터 SAP 시스템은 Azure VM이 다시 시작 물리적 서버를 azure 인프라 및 전반적인 기본 Azure 플랫폼입니다.

> [!NOTE]
> 것이 중요 한 toomention Vm 및 응용 프로그램이 아닌는 주로 보호 Azure VM이 다시 시작 합니다. VM 다시 시작 기능은 SAP 응용 프로그램의 고가용성을 제공하지 않지만 특정 수준의 인프라 가용성을 제공하므로 간접적으로 SAP 시스템의 "고가용성"을 제공합니다. 걸립니다 toorestart VM 호스트 계획적 이거나 비계획적인 정전 후 hello 시간에 대 한 SLA를 제공 하지도 됩니다. 따라서 이러한 방식의 '고가용성'은 (A)SCS 또는 DBMS와 같은 SAP 시스템의 중요한 구성 요소에 적합하지 않습니다.
>
>

고가용성을 위한 또 다른 중요한 인프라 요소는 저장소입니다. 예를 들어 Azure Storage SLA에 따른 가용성은 99.9%입니다. 디스크가 있는 모든 VM을 단일 Azure 저장소 계정에 배포하는 경우 Azure 저장소를 사용할 수 없게 되어 해당 Azure 저장소 계정에 배치된 모든 VM을 사용할 수 없게 되고 해당 VM 내에서 실행되는 모든 SAP 구성 요소로 사용할 수 없게 될 수 있습니다.  

모든 VM을 단일 Azure 저장소 계정에 두는 대신, 각 VM에 대해 전용 저장소 계정을 사용할 수 있습니다. 이러한 방식에서는 여러 독립적인 Azure 저장소 계정을 사용하여 전반적인 VM 및 SAP 응용 프로그램 가용성이 증가하게 됩니다.

Azure 관리 되는 디스크에 연결 된 hello 가상 컴퓨터의 장애 도메인 hello에 자동으로 배치 됩니다. 배치 하는 경우 설정 하 고 관리 하는 디스크를 사용 하는 두 개의 가상 컴퓨터가 가용성, hello 플랫폼 하므로 여러 장애 도메인으로 hello 관리 하는 디스크를 배포 합니다. 프리미엄 저장소 toouse 하려는 경우 뿐만 디스크 관리를 사용 하는 것이 좋습니다.

Azure 인프라 HA 및 Storage 계정을 사용하는 SAP NetWeaver 시스템의 샘플 아키텍처는 다음과 같습니다.

![HA tooachieve SAP 응용 프로그램 "higher" 가용성 Azure 인프라를 활용합니다.][planning-guide-figure-2900]

Azure 인프라 HA 및 관리 디스크를 사용하는 SAP NetWeaver 시스템의 샘플 아키텍처는 다음과 같습니다.

![HA tooachieve SAP 응용 프로그램 "higher" 가용성 Azure 인프라를 활용합니다.][planning-guide-figure-2901]

중요 한 SAP 구성 요소에 대 한 hello 지금까지 다음을 수행:

* SAP AS(응용 프로그램 서버)의 고가용성

  SAP 응용 프로그램 서버 인스턴스는 중복 구성 요소입니다. 각 SAP AS 인스턴스는 다른 Azure 장애 도메인 및 업그레이드 도메인([장애 도메인][planning-guide-3.2.1] 및 [업그레이드 도메인][planning-guide-3.2.2] 장 참조)에서 실행되는 자체 VM에 배포됩니다. 이는 Azure 가용성 집합을 사용하여 보장됩니다([Azure 가용성 집합][planning-guide-3.2.3] 장 참조). 각 SAP AS 인스턴스는 자체 Azure 저장소 계정에 배치됩니다.

  Azure 저장소 계정 하나를 사용할 수 없게 되면 해당 SAP AS가 있는 단일 VM을 사용할 수 없게 됩니다. 그러나 단일 Azure 구독 내에서는 Azure 저장소 계정 수가 제한됩니다. hello VM 다시 부팅 한 후에 (A) SCS 인스턴스의 자동 시작 tooensure tooset hello Autostart 매개 변수 (A) SCS 인스턴스에 장에서 설명 하는 프로필을 시작 하 고 있는지 확인 [SAP 인스턴스에 대 한 자동 시작 사용 하 여] [ planning-guide-11.5].
  자세한 내용은 [SAP 응용 프로그램 서버의 고가용성][planning-guide-11.4.1] 장을 참조하세요.

  관리 디스크를 사용하더라도 해당 디스크는 Azure Storage 계정에도 저장되므로 Storage가 중단되면 사용이 불가능해질 수 있습니다.

* *더 높은* 가용성

  여기 SAP (A) SCS 인스턴스에 설치 된 Azure VM이 다시 시작 tooprotect hello VM 활용합니다. Hello Azure의 계획 되거나 계획 되지 않은 가동 중지의 경우 서버에서 사용 가능한 다른 서버에 Vm을 다시 시작 합니다. 이 경우 (A) SCS 인스턴스에 hello을 앞서 언급 했 듯이 Vm 및 응용 프로그램이 아닌 보호할 주로 Azure VM이 다시 시작 합니다. VM이 다시 시작 하는 hello를 통해 연락할 주소 하지 직접 SAP (A) SCS 인스턴스의 "높은 가용성"입니다. hello VM 다시 부팅 한 후에 (A) SCS 인스턴스의 자동 시작 tooinsure tooset Autostart 매개 변수 (A) SCS 인스턴스에 장에서 설명 하는 프로필을 시작 하 고 있는지 확인 [SAP 인스턴스에 대 한 자동 시작 사용 하 여][planning-guide-11.5]합니다. 즉, 단일 VM에서 실행 되는 단일 실패 지점 (SPOF)와 hello (A) SCS 인스턴스에 hello 결정 하는 요소의 hello hello 전체 SAP 지형의 가용성 됩니다.

* *더 높은* 가용성

  여기에서 비슷한 toohello SAP (A) SCS 인스턴스에 대/소문자를 사용 하 고 Azure VM이 다시 시작 tooprotect hello VM 설치 된 DBMS 소프트웨어와 함께 사용 했습니다 "높은 가용성"의 DBMS 소프트웨어 VM이 다시 시작을 통해 달성 합니다.
  DBMS는 단일 VM에서 실행 되는 SPOF 이기도 아니며 hello 결정 하는 요소 hello 전체 SAP 지형의의 가용성을 hello에 대 한 합니다.

### <a name="sap-application-high-availability-on-azure-iaas"></a>Azure IaaS의 SAP 응용 프로그램 고가용성
tooprotect 필요 tooachieve 전체 SAP 시스템 고가용성을 예제 중복 SAP 응용 프로그램 서버에 대 한 모든 중요 SAP 시스템 구성 요소와 DBMS 및 SAP (A) SCS 인스턴스에 같은 고유한 구성 (예를 들어 단일 실패 지점)입니다.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>SAP 응용 프로그램 서버의 고가용성
Hello SAP 응용 프로그램 서버/대화 상자 인스턴스는 하지 특정 고가용성 솔루션에 대 한 필요한 toothink. 고가용성은 단순히 중복성에 의해 획득되므로 다른 가상 컴퓨터에서 충분히 확보될 수 있습니다. 모든 위치 hello Vm hello 동일한 Azure 가용성 집합 tooavoid hello에서 업데이트 될 수 있습니다에 시간 동안 가동 중지 시간이 계획 된 유지 관리 합니다. 다른 업그레이드 및 Azure 배율 단위 내에서 오류 도메인 기반으로 구축 된 hello 기본 기능이 장에 이미 도입 된 [업그레이드 도메인][planning-guide-3.2.2]합니다. Azure 가용성 집합은 이 문서의 [Azure 가용성 집합][planning-guide-3.2.3] 장에서 설명했습니다.

Azure 배율 단위 내에서 Azure 가용성 집합이 사용할 수 있는 장애 도메인 및 업그레이드 도메인 수는 제한되어 있습니다. 이 하나의 가용성 집합에 Vm의 수를 넣기, 조만간 둘 이상의 VM에서에서 끝난 hello 동일한 오류 또는 업그레이드 도메인을 의미 합니다.

전용된의 Vm에 있는 인스턴스의 몇 가지 SAP 응용 프로그램 서버를 배포 및 그림 다음 hello hello 끝에 시나리오 5 개의 업그레이드 도메인이, 가져온 있다고 가정 합니다. 향후 hello hello 실제 최대 장애 도메인과 업데이트 도메인 수는 가용성 집합 내에서 변경 될 수 있습니다.

![Azure에 있는 SAP 응용 프로그램 서버의 HA][planning-guide-figure-3000]

이 설명서에서 자세한 내용을 찾을 수 있습니다. <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Windows hello SAP (A) SCS 인스턴스의 고가용성
Windows Server 장애 조치 클러스터 (WSFC)는 자주 사용 되는 솔루션 tooprotect hello SAP (A) SCS 인스턴스입니다. 이 솔루션은 "HA 설치"의 형태로 sapinst에도 통합되어 있습니다. 이 시점에서 Azure 인프라 hello 수 tooprovide hello 기능 tooset hello 필요한 Windows Server 장애 조치 클러스터 hello 같은 방식으로 작업이 수행 되는 온-프레미스를 아닙니다.

2016 년 1 월을 기준으로 hello Windows 운영 체제를 실행 하는 hello Azure 클라우드 플랫폼의 클러스터 공유 볼륨을 사용 하 여 두 개의 Azure Vm 간에 공유 디스크에 hello 가능성을 제공 하지 않습니다.

올바른 솔루션에는 있지만 WSFC에 통합 될 수 있는 동기 및 투명 한 디스크 복제에 의해 공유 볼륨을 제공 하는 타사 소프트웨어의 hello 사용법입니다. 이 방법은 해당만 hello 활성 클러스터 노드 수 tooaccess 시간으로 된 지점에 복사 hello 디스크 중 하나가 의미 합니다. 2016 년 1 월이이 HA 기준으로 Windows 게스트 OS는 Azure Vm에서 SIOS DataKeeper 타사 소프트웨어와 함께에서 지원 되는 tooprotect hello SAP (A) SCS 인스턴스에 구성은합니다.

배치 하 여 공유 디스크 클러스터 리소스 tooWindows 장애 조치 클러스터를 제공 하는 hello SIOS DataKeeper 솔루션:

* 연결 된 Windows 클러스터 구성에 있는 hello 가상 컴퓨터 (Vm)의 tooeach는 추가 Azure VHD
* 두 VM 노드에서 실행되는 SIOS DataKeeper Cluster Edition
* SIOS DataKeeper Cluster Edition hello 내용의 hello 추가 동기적으로 반영 하는 방식에서으로 구성 된 것 VHD 대상 VM의 원본 Vm tooadditional VHD 연결 된 볼륨에서 볼륨을 연결 합니다.
* SIOS DataKeeper hello 소스 및 대상 로컬 볼륨 추상화 이며 tooWindows 단일 공유 디스크 장애 조치 클러스터를 제공 합니다.

방법은 모든 세부 정보를 찾을 수 있습니다 hello에서 SIOS DataKeeper 및 SAP와 Windows 장애 조치 클러스터 tooinstall [SAP ASCS 인스턴스 클러스터링 SIOS datakeeper를 통해 Azure에서 Windows Server 장애 조치 클러스터를 사용 하 여] [ ha-guide-classic]백서에 나와 있습니다.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Linux에서 hello SAP (A) SCS 인스턴스의 고가용성
2015 년 12 월을 기준으로 해당 tooshared 디스크가 Azure에서 Linux Vm에 대 한 WSFC도 됩니다. Azure의 Linux에서 SAP를 실행하는 경우에 SIOS for Windows와 같은 타사 소프트웨어를 실행해도 괜찮은지는 아직 검증되지 않았습니다.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Hello SAP 데이터베이스 인스턴스의 고가용성
hello 표준 SAP DBMS HA 설치에 따라 두 DBMS Vm이 사용 된 DBMS 고가용성 기능에서 활성 DBMS 인스턴스 toohello hello tooreplicate 데이터의 수동 DBMS 인스턴스로 VM 두 번째입니다.

고가용성 및 재해 복구 기능 일반 뿐만 아니라 특정 DBMS의 DBMS에 대 한 hello에 설명 된 [DBMS 배포 가이드][dbms-guide]합니다.

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>에 대 한 종단 간 고가용성 hello 전체 SAP 시스템
Azure의 전체 SAP NetWeaver HA 아키텍처의 두 가지 예는 Windows용과 Linux용입니다.

오류가 발생 하면 관리 되지 않는: hello 개념 아래에 설명 된 대로 toobe 많은 SAP 시스템을 배포 하 고 Vm 배포 수 hello 구독 당 저장소 계정 hello 최대 제한을 초과 하는 경우 약간 손상 할 수 있습니다. 이러한 경우에 Vm의 Vhd toobe 한 저장소 계정 내에서 결합 해야 합니다. 일반적으로는 이를 위해 여러 다른 SAP 시스템에 있는 SAP 응용 프로그램 계층 VM의 VHD를 결합할 수 있습니다.  여기서는 서로 다른 SAP 시스템에 있는 여러 DBMS VM의 다른 VHD를 단일 Azure 저장소 계정에 결합했습니다. 함으로써 Azure 저장소 계정의 hello IOPS 제한 염두에서에 두고 (<https://azure.microsoft.com/documentation/articles/storage-scalability-targets>)


##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] Windows의 HA
![Azure IaaS의 SQL Server를 사용한 SAP NetWeaver 응용 프로그램 HA 아키텍처][planning-guide-figure-3200]

hello Azure 구성은 다음 인프라 문제 및 패치를 적용 하는 호스트에서 toominimize 영향 hello SAP NetWeaver 시스템에 사용 됩니다.

* hello 완벽 한 시스템 (필수-DBMS 계층, (A) SCS 인스턴스 및에서 완전 한 응용 프로그램 계층 필요 toorun hello 동일한 위치) Azure에 배포 됩니다.
* hello 전체 시스템이 (필수)는 단일 Azure 구독 내에서 실행 됩니다.
* hello 전체 시스템이 (필수)는 하나의 Azure 가상 네트워크 내에서 실행 됩니다.
* 모든 hello Vm이 toohello 된 경우에 세 개의 가용성 집합으로 hello 단일 SAP 시스템의 Vm의 hello 분리 가능한가 동일한 가상 네트워크입니다.
* 단일 SAP 시스템의 DBMS 인스턴스를 실행하는 모든 VM이 하나의 가용성 집합에 있습니다. SQL Server AlwaysOn 또는 Oracle Data Guard와 같은 네이티브 DBMS 고가용성 기능이 사용되므로 시스템당 둘 이상의 VM에서 DBMS 인스턴스가 실행된다고 가정할 수 있습니다.
* DBMS 인스턴스를 실행하는 모든 VM은 자체 저장소 계정을 사용합니다. DBMS 데이터 및 로그 파일이 hello 데이터를 동기화 하는 DBMS 고가용성 기능을 사용 하 여 하나의 저장소 계정 tooanother 저장소 계정에서 복제 됩니다. 저장소 계정 하나를 사용할 수 없게 하나의 SQL Windows 클러스터 노드가 아니라 하지 hello 전체 SQL Server 서비스를 사용할 수 없게를 하면 됩니다.
* 단일 SAP 시스템의 (A)SCS 인스턴스를 실행하는 모든 VM이 하나의 가용성 집합에 있습니다. Windows Server 장애 조치 클러스터 (WSFC)는 해당 Vm tooprotect hello (A) SCS 인스턴스에 내의 구성 되어 있습니다.
* (A)SCS 인스턴스를 실행하는 모든 VM은 자체 저장소 계정을 사용합니다. (A) SCS 인스턴스 파일 및 SAP 전역 폴더 SIOS DataKeeper 복제를 사용 하 여 하나의 저장소 계정 tooanother 저장소 계정에서 복제 됩니다. 저장소 계정 하나를 사용할 수 없게 하나 (A)를 사용할 수 없게 하면 SCS Windows 클러스터 노드에 않고 전체 hello 없습니다 (A) SCS 서비스입니다.
* 모든 hello Vm hello SAP 응용 프로그램 서버 계층을 나타내는 세 번째 가용성 집합에 있습니다.
* SAP 응용 프로그램 서버를 실행 하는 모든 hello Vm 자체 저장소 계정을 사용 합니다. 저장소 계정 하나를 사용할 수 없게가 다른 SAP AS 계속 toorun 한 SAP 응용 프로그램 서버를 사용할 수 없게를 하면 됩니다.

hello 다음 그림에 표시 된 hello를 관리 하는 디스크를 사용 하 여 동일한 가로 그림입니다.

![Azure IaaS의 SQL Server를 사용한 SAP NetWeaver 응용 프로그램 HA 아키텍처][planning-guide-figure-3201]

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] Linux의 HA
SAP ha Azure에서 linux hello 아키텍처는 기본적으로 hello 위에서 설명한 Windows as 구문과 동일 합니다. 2016년 1월 현재 SAP (A)SCS HA 솔루션은 아직Azure의 Linux에서 지원되지 않습니다.

이 인해 2016 년 1 월의 SAP Linux Azure 시스템으로 구현할 수 없는 HA hello (A) SCS 인스턴스에 대 한 없으므로 수집기와 같은 가용성 SAP Azure 시스템으로 hello 되며 단일 인스턴스 SAP ASE 데이터베이스 hello 됩니다.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>SAP 인스턴스에 대해 자동 시작 사용
SAP은 hello 기능 toostart SAP 인스턴스 hello VM 내에서 운영 체제 hello hello 시작 후 즉시 제공 합니다. 정확한 단계는 hello SAP 기술 자료 문서에 설명 된 [1909114]합니다. 그러나 SAP은 하지 권장 toouse hello 설정을 더 이상 인스턴스 다시 시작의 hello 순서로 컨트롤이 있기 때문에 둘 이상의 VM에 영향을 받은 또는 다중 인스턴스 VM 당 실행 한 것으로 가정 합니다. 결국 가져오는 다시 시작 하는 단일 VM의 VM 및 hello 경우에서 단일 SAP 응용 프로그램 서버 인스턴스의 일반적인 Azure 시나리오를 가정할 때 hello 자동 시작 실제로 중요 하지 않은 및이 매개 변수를 추가 하 여 사용 하도록 설정할 수 있습니다.

    Autostart = 1

Hello에 프로필 hello SAP ABAP 또는 Java 인스턴스를 시작합니다.

> [!NOTE]
> hello Autostart 매개 변수는 일부 결점도 있을 수 있습니다. 좀 더 자세하게 hello 매개 변수 트리거 hello 관련 hello 인스턴스의 Windows/Linux 서비스를 시작 하는 경우 SAP ABAP 또는 Java 인스턴스의 시작 부분을 hello 합니다. 기능이 기는 hello 대/소문자 hello 운영 체제를 부팅 합니다. 그러나 SAP 서비스를 다시 시작하는 것도 SUM이나 기타 업데이트 또는 업그레이드와 같은 SAP 소프트웨어 수명 주기 관리 기능의 일반적인 측면에 해당합니다. 이러한 기능은 모두 자동으로 다시 시작 하는 인스턴스 toobe를 예상할 수 없습니다. 따라서 hello Autostart 매개 변수 등의 작업을 실행 하기 전에 해제 되어야 합니다. hello Autostart 매개 변수는도 ASCS/SCS/CI 같은 클러스터 되는 SAP 인스턴스에 대 한 사용 해야 합니다.
>
>

SAP 인스턴스의 자동 시작과 관련된 자세한 내용은 다음 항목을 참조하세요.

* [Unix 서버 시작/중지에 따른 SAP 시작/중지](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [SAP NetWeaver 관리 에이전트 시작 및 중지](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [어떻게 tooenable 자동 HANA 데이터베이스 시작](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>대형 3계층 SAP 시스템
3계층 SAP 구성의 고가용성 측면은 이전 섹션에서 이미 설명되었습니다. 하지만 시스템 hello DBMS 서버 요구 사항은 너무 큰 Azure에 있는 toohave 있지만 hello SAP 응용 프로그램 계층을 Azure에 배포 될 수 없습니다.

#### <a name="location-of-3-tier-sap-configurations"></a>3계층 SAP 구성의 위치
지원 되는 toosplit hello 응용 프로그램 자체 또는 hello 응용 프로그램 계층과 DBMS 계층 온-프레미스와 Azure 간에 없습니다. SAP 시스템은 온-프레미스 또는 Azure에 완전히 배포됩니다. 경우도 많습니다 지원된 toohave hello 응용 프로그램 서버 중 일부 온-프레미스 및 일부 다른 Azure에서 실행 합니다. Hello hello 토론의 시작점입니다. 또한 SAP 시스템의 toohave hello DBMS 구성 요소에서 지원 되지 않는 하 고 다른 두 Azure 지역에 배포 된 SAP 응용 프로그램 서버 계층 hello 합니다. 미국 서부에 DBMS를 배포하고 미국 중부에 SAP 응용 프로그램 계층을 배포하는 경우를 예로 들 수 있습니다. 이러한 구성을 지원 하지 않는 이유는 hello SAP NetWeaver 아키텍처의 hello 대기 시간 민감도입니다.

그러나 지난 해 데이터의 hello 과정 센터 파트너 공동 위치 tooAzure 영역을 개발합니다. 이러한 공동 위치 종종는 매우 근접 toohello 실제 Azure 데이터 센터 내의 Azure 지역입니다. 대기 시간이 2ms 보다 작은 hello 짧은 거리 및 자산을 Azure ExpressRoute 통해 hello 공동 위치에 연결 될 수 있습니다. 이러한 경우 toolocate hello DBMS 계층 (SAN/NAS 저장소 포함) 이러한 공동 배치 및 Azure의 hello SAP 응용 프로그램 계층에서이 가능 합니다. 2015년 12월을 기준으로 이와 같은 배포는 더 이상 진행되지 않고 있습니다. 하지만 SAP 이외의 응용 프로그램 배포를 사용하는 다른 고객들은 이러한 접근 방식을 이미 사용하고 있습니다.

### <a name="offline-backup-of-sap-systems"></a>SAP 시스템의 오프라인 백업
Hello에 종속 없습니다 (2 계층 또는 3 계층) 선택한 SAP 구성 될 수 필요 tooback를 있습니다. hello VM 자체와 toohave hello 데이터베이스의 백업 hello 콘텐츠입니다. hello DBMS 관련 백업 예상된 toobe 데이터베이스 메서드를 사용 하 여 수행 됩니다. Hello 서로 다른 데이터베이스에 대 한 자세한 내용은에서 확인할 수 있습니다 [DBMS 가이드][dbms-guide]합니다. 다른 손 hello, hello SAP 데이터를 백업할 수 있습니다 (도 hello 데이터베이스 콘텐츠 포함) 오프 라인으로이 섹션에 설명 된 대로 또는 온라인 hello 다음 섹션에 설명 된 대로 합니다.

기본적으로 hello 오프 라인 백업 hello hello Azure 포털을 통해 VM 종료와 hello 기본 VM 디스크 및 모든 연결 된 디스크 toohello VM의 복사본이 필요 합니다. 이 지정 시간 이미지가의 hello VM 및 연결 된 디스크 유지 합니다. 다른 Azure 저장소 계정에 백업' toocopy hello' 좋습니다. 장에 설명 된 절차를 따라서 hello [Azure 저장소 계정 간에 디스크 복사] [ planning-guide-5.4.2] 이 문서의 적용 됩니다.
Azure hello를 사용 하 여 hello 종료 외에도 하나 포털도 작업을 수행할 수 Powershell 또는 CLI를 통해 여기에 설명 된 대로: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

해당 상태로의 복원을 구성 될 hello를 삭제할 경우의 기본 VM도 hello의 원래 디스크 hello 대로 기반 VM 및 탑재 된 디스크를 다시 복사 hello 저장 된 디스크 toohello 원래 저장소 계정 또는 리소스 그룹을 관리 하는 디스크와 다음 hello 시스템을 다시 배포 합니다.
이 문서는 어떻게 tooscript이 프로세스는에 예가 나와 Powershell: <http://www.westerndevs.com/azure-snapshots/>

확인 하십시오 있는지 tooinstall 새 SAP 라이선스 만들어지므로 위에서 설명한 것 처럼 VM 백업을 복원 하 여 새 하드웨어 키입니다.

### <a name="online-backup-of-an-sap-system"></a>SAP 시스템의 온라인 백업
Hello에 설명 된 대로 DBMS DBMS 관련 메서드를 수행 하는 hello의 백업 [DBMS 가이드][dbms-guide]합니다.

Hello SAP 시스템 내에서 다른 Vm은 Azure 가상 컴퓨터 백업 기능을 사용 하 여 백업할 수 있습니다. Azure 가상 컴퓨터 백업 2015 초기에 도입 된 이며 한편 전체 Azure에서 VM 표준 방법을 tooback 합니다. Azure 백업에서는 Azure의 hello 백업을 저장 하는 VM의 복원을 다시 하며

> [!NOTE]
> 2015 년 12 월을 기준으로 VM 백업을 사용 하 여 유지 하지 않습니다 SAP에 사용 되는 hello 고유 VM ID 라이선스입니다. 즉, VM 백업 복원 하 여 새 SAP 라이센스 키의 설치 hello VM 복원 된 것으로 간주 됩니다 toobe 새 VM이 필요 함 및 중 저장 된 대체 되지 않습니다.
>
> ![Windows][Logo_Windows] Windows
>
> 이론적으로, Vm 실행된 데이터베이스를 백업할 수 있습니다를 일관성 있게 hello DBMS 시스템 hello Windows VSS를 지 원하는 경우 (볼륨 섀도 복사본 서비스 <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx >) SQL Server는 예를 들어, 다른 이름으로 합니다.
> 그러나 데이터베이스의 Azure VM 백업 기반의 특정 시간 복원은 가능하지 않습니다. 따라서 Azure VM 백업에 의존 하지 않고 DBMS 기능 있는 데이터베이스의 tooperform 백업 않는 것이 좋습니다.
>
> Azure 가상 컴퓨터 백업에 잘 알고 tooget 여기서 시작 하십시오: <https://docs.microsoft.com/azure/backup/backup-azure-vms>합니다.
>
> 다른 가능성 toouse 조합 Microsoft Data Protection Manager의 데이터베이스 백업/복원에 Azure VM 및 Azure 백업에 설치 됩니다. 자세한 내용은 <https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction>에서 찾을 수 있습니다.  
>
> ![Linux][Logo_Linux] Linux
>
> Linux에서 VSS 없는 해당 tooWindows 있습니다. 따라서 파일 일치 백업만 가능하고 응용 프로그램 일치 백업은 가능하지 않습니다. hello SAP DBMS 백업을 수행 해야 DBMS 기능을 사용 하 여 합니다. hello hello SAP 관련 데이터를 포함 하는 파일 시스템 저장할 수 있습니다, 예를 들어 여기 사용 하 여 tar 설명 된 대로: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>프로덕션 SAP 지형에 대한 DR 사이트로 사용되는 Azure
Mid 2014부터 Hyper-v, 시스템 센터 및 Azure 확장 toovarious 구성 온-프레미스 기반으로 Hyper-v를 실행 하는 Vm에 대 한 DR 사이트와 Azure의 hello 사용을 사용 하도록 설정 합니다.

이 솔루션은 하는 toodeploy 방법을 자세히 보여 주는 블로그 여기에 설명 되어: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>합니다.

## <a name="summary"></a>요약
Azure에서 SAP 시스템에 대 한 고가용성의 hello 주요 점은 다음과 같습니다.

* SAP 단일 실패 지점이 hello를 정확 하 게 보호할 수 없는 시점에서, 온-프레미스 배포에서 수행할 수 있습니다 하는 방식으로 hello 동일 합니다. hello 이유는 타사 소프트웨어의 hello 사용 하지 않고 Azure에서 공유 디스크 클러스터는 아직 빌드할 수 없습니다.
* Hello DBMS 계층에 대 한 공유 디스크 클러스터 기술에 의존 하지 않는 toouse DBMS 기능을 해야 합니다. Hello 내용은 [DBMS 가이드][dbms-guide]합니다.
* hello Azure 인프라 또는 호스트 유지 관리 작업의에서 오류 도메인 내의 문제 toominimize hello 영향, Azure 가용성 집합을 사용 해야 합니다.
  * 하나는 toohave 좋습니다 hello SAP 응용 프로그램 계층에 대 한 가용성 집합입니다.
  * Hello SAP DBMS 계층에 별도 가용성 집합 toohave 것이 좋습니다.
  * 서로 다른 SAP 시스템의 Vm에 대 한 동일한 가용성 집합 tooapply hello는 권장 되지 않습니다.
  * Toouse 프리미엄 디스크 관리 되는 것이 좋습니다.
* Hello SAP DBMS 계층을 백업 하려는 hello를 확인 하십시오 [DBMS 가이드][dbms-guide]합니다.
* SAP 대화 상자 인스턴스를 백업 거의 의미가 일반적으로 더 빠른 tooredeploy 단순한 대화 상자 인스턴스 이기 때문입니다.
* 백업 hello VM의 SAP 시스템 hello와 함께 hello 글로벌 디렉터리를 포함 하는 hello 여러 인스턴스의 모든 hello 프로필 의미가 및 Windows 백업을 사용 하 여 수행 해야 하거나, linux tar 예를 들어 있습니다. Hello를 사용 하 여를 보다 쉽게 tooback 하도록 하는 Windows Server 2008 (R2) 및 Windows Server 2012 (R2) 간의 차이가 있으므로 최신 Windows Server를 해제, toorun Windows 게스트 운영 체제로 Windows Server 2012 (R2) 것이 좋습니다.
