---
title: "SAP NetWeaver 용 가상 컴퓨터 DBMS 배포 aaaAzure | Microsoft Docs"
description: "SAP NetWeaver에 대한 Azure Virtual Machines DBMS 배포"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5654dac7-4204-4387-b312-3d8b2898eb3a
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 501f6fbc2baa379b706e95d2bfba377ac129b382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-dbms-deployment-for-sap-netweaver"></a>SAP NetWeaver에 대한 Azure Virtual Machines DBMS 배포
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1114181]:https://launchpad.support.sap.com/#/notes/1114181
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
[2171857]:https://launchpad.support.sap.com/#/notes/2171857
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
[dbms-guide-managed-disks]:dbms-guide.md#f42c6cb5-d563-484d-9667-b07ae51bce29

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
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
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
[virtual-machines-azurerm-versus-azuresm]:../../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability-linux]:../../linux/manage-availability.md
[virtual-machines-manage-availability-windows]:../../windows/manage-availability.md
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
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
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

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

이 가이드는 구현 및 Microsoft Azure의 hello SAP 소프트웨어 배포에 hello 설명서의 일부입니다. 이 가이드를 읽기 전에 hello 읽을 [계획 및 구현 가이드][planning-guide]합니다. 이 문서에서는 다양 한 RDBMS 관계형 데이터베이스 관리 시스템 () 및 관련된 제품에 Microsoft Azure 가상 컴퓨터 (Vm) SAP와 함께에서 hello Azure 인프라 서비스 (IaaS) 기능으로 사용 하 여 hello 배포를 설명 합니다.

hello 용지 보완 hello SAP 설치 설명서 및 SAP Note를 설치 및 배포에 SAP 소프트웨어에 대 한 기본 리소스 hello 플랫폼을 제공 합니다.

## <a name="general-considerations"></a>일반적인 고려 사항
이 챕터에서는 Azure VM에서 SAP 관계형 DBMS 시스템을 실행할 때의 고려 사항을 소개합니다. 몇 가지 참조 toospecific DBMS 시스템에에서는이 장의입니다. 대신 특정 DBMS 시스템 hello는이 백서의 다음 장에서이 설명 처리 됩니다.

### <a name="definitions-upfront"></a>사전 정의
Hello 설명서에서는 아래 계약 내용 hello를 사용 합니다.

* IaaS: 서비스 제공 인프라
* PaaS: Platform as a Service
* SaaS: Software as a Service.
* SAP 구성 요소: ECC, BW, Solution Manager 또는 EP 등의 개별 SAP 응용 프로그램.  SAP 구성 요소는 기존의 ABAP 또는 Java 기술을 기반으로 하거나 비즈니스 개체와 같은 비NetWeaver 기반 응용 프로그램을 기반으로 사용할 수 있습니다.
* SAP 환경: 하나 이상의 SAP 구성 요소 tooperform 개발, QAS, 학습, DR 또는 프로덕션 등의 비즈니스 기능을 논리적으로 그룹화 합니다.
* SAP 지형:이 참조 toohello 전체 SAP 자산에 고객의 IT 지형 합니다. hello SAP 지형에는 모든 프로덕션 및 비프로덕션 환경이 포함 되어 있습니다.
* 예를 들어는 SAP ERP 개발 시스템, SAP BW 테스트 시스템, SAP CRM 프로덕션 시스템 등의 응용 프로그램 계층과 DBMS 계층의 SAP 시스템: hello 조합입니다. Azure 배포는 지원 되는 toodivide 온-프레미스와 Azure 간에 이러한 두 계층입니다. 즉, SAP 시스템은 온-프레미스에 배포되거나 Azure에 배포됩니다. 그러나 hello 서로 다른 시스템에서 Azure 또는 온-프레미스 SAP 지형의을 배포할 수 있습니다. 예를 들어 SAP CRM 프로덕션 시스템 온-프레미스 hello 하지만 Azure의 hello SAP CRM 개발 및 테스트 시스템을 배포할 수 있습니다.
* 클라우드 전용 배포: 여기서 hello Azure 구독이 사이트-사이트를 통해 연결 되어 있지 않거나 ExpressRoute 연결 toohello 온-프레미스 네트워크 인프라를 배포 합니다. 공통 Azure 설명서에서는 이러한 종류의 배포를 '클라우드 전용' 배포라고도 합니다. 이 방법으로 배포 된 가상 컴퓨터 이용 하 여 hello 인터넷 및 공용 인터넷 끝점 Azure의 toohello Vm을 할당 합니다. hello 온-프레미스 AD (Active Directory) 및 DNS가 이러한 유형의 배포에서 tooAzure 확장 되지 않습니다. 따라서 hello Vm hello 온-프레미스 Active Directory의 일부가 아닌 합니다. 참고: 이 문서에서 클라우드 전용 배포는 온-프레미스에서 Active Directory 또는 이름 확인을 공용 클라우드로 확장하지 않고 Azure에서 단독으로 실행 중인 전체 SAP 배경으로 정의됩니다. 클라우드 전용 구성은 프로덕션 SAP 시스템 또는 SAP STMS 또는 다른 온-프레미스 리소스 toobe 있는 온-프레미스 리소스 및 Azure에서 호스트 되는 SAP 시스템 사이 사용 해야 하는 구성에 대 한 지원 되지 않습니다.
* 크로스-프레미스: Vm 배포 tooan 사이트 간, 멀티 사이트 또는 hello 온-프레미스 센터와 Azure 간의 ExpressRoute 연결 된 Azure 구독에 있는 시나리오에 설명 합니다. 공통 Azure 설명서에서 이러한 종류의 배포를 프레미스 간 시나리오라고도 합니다. hello 연결에 대 한 hello 이유 tooextend 온-프레미스 도메인, 온-프레미스 Active Directory 및 온-프레미스 DNS를 Azure로를입니다. hello 온-프레미스 가로 확장된 toohello hello 구독의 Azure 자산 됩니다. Hello Vm이 확장명이 hello 온-프레미스 도메인의 일부를 수 있습니다. Hello 온-프레미스 도메인의 도메인 사용자 hello 서버에 액세스할 수 및 서비스를 실행할 수에 Vm (예: DBMS 서비스)입니다. 온-프레미스에 배포된 VM과 Azure에 배포된 VM 간의 통신 및 이름 확인이 가능합니다. Azure에서 SAP 자산 배포를 위한이 toobe hello 가장 일반적인 시나리오 라고 생각 됩니다. 자세한 내용은 [이 문서][vpn-gateway-cross-premises-options] 및 [이 문서][vpn-gateway-site-to-site-create]를 참조하세요.

> [!NOTE]
> 프로덕션 SAP 시스템의 경우 SAP 시스템을 실행 중인 Azure 가상 컴퓨터가 온-프레미스 도메인의 멤버인 SAP 시스템의 프레미스 간 배포가 지원됩니다. 일부 또는 전체 SAP 배경을 Azure로 배포하는 데 프레미스 간 구성이 지원됩니다. Azure의 hello 전체 SAP 지형을 실행에 온-프레미스 도메인 및 광고의 일부로 해당 Vm을 포함 해야 합니다. 이전 버전의 hello 문서, 온-프레미스와 Azure 간 크로스-프레미스 연결 된다는 hello 사실에 입각에 '혼합' hello 용어 루 팅 하는 하이브리드-IT 시나리오에 대 한 얘기 합니다. 이 경우 '혼합'도 Azure의 hello Vm은 hello의 일부 임을 의미 온-프레미스 Active Directory.
> 
> 

일부 Microsoft 문서에서는 특히 DBMS HA 구성의 경우 프레미스 간 시나리오를 약간 다르게 설명합니다. SAP 관련 문서 hello hello 경우에서 hello 크로스-프레미스 시나리오만 수행 하는 경우 toohaving 사이트 간 또는 개인 (express 경로) 연결 및 toohello 팩트 hello SAP 지형이 온-프레미스와 Azure 간에 분산 된다는 합니다.

### <a name="resources"></a>리소스
hello 다음 가이드는 hello Azure에서 SAP 배포 항목에 사용할 수 있습니다.

* [SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현][planning-guide]
* [SAP NetWeaver에 대한 Azure Virtual Machines 배포][deployment-guide]
* [SAP NetWeaver에 대한 Azure Virtual Machines DBMS 배포(이 문서)][dbms-guide]

SAP Note 다음 hello는 Azure의 SAP toohello 관련된 항목:

| Note 번호 | 제목 |
| --- | --- |
| [1928533] |Azure의 SAP 응용 프로그램: 지원 제품 및 Azure VM 유형 |
| [2015553] |Microsoft Azure의 SAP: 지원 필수 조건 |
| [1999351] |SAP용 고급 Azure 모니터링 문제 해결 |
| [2178632] |Microsoft Azure의 SAP용 주요 모니터링 메트릭 |
| [1409604] |Windows에서의 가상화: 향상된 모니터링 |
| [2191498] |Azure와 Linux의 SAP: 향상된 모니터링 |
| [2039619] |사용 하 여 Microsoft Azure의 SAP 응용 프로그램에는 Oracle 데이터베이스 hello: 제품 지원 및 버전 |
| [2233094] |DB6: Linux, UNIX 및 Windows용 IBM DB2를 사용하는 SAP 응용 프로그램 - 추가 정보 |
| [2243692] |Microsoft Azure(IaaS) VM의 Linux: SAP 라이선스 문제 |
| [1984787] |SUSE LINUX Enterprise Server 12: 설치 참고 |
| [2002167] |Red Hat Enterprise Linux 7.x: 설치 및 업그레이드 |
| [2069760] |Oracle Linux 7.x SAP 설치 및 업그레이드 |
| [1597355] |Linux에 대한 스왑 공간 권장 사항 |
| [2171857] |Oracle Database 12c - Linux에서 파일 시스템 지원 |
| [1114181] |Oracle Database 11g - Linux에서 파일 시스템 지원 |


또한 읽기 hello [SCN Wiki](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) Linux에 대 한 모든 SAP Note를 포함 하 합니다.

Microsoft Azure 아키텍처 hello 및 Microsoft Azure 가상 컴퓨터는 배포 하 고 작동 하는 방법에 대 한 작업 지식을 갖추고 있어야 합니다. 자세한 내용은 <https://azure.microsoft.com/documentation/>에서 찾을 수 있습니다.

> [!NOTE]
> 우리는 **하지** 서비스 (PaaS) 제품의 hello Microsoft Azure 플랫폼으로 Microsoft Azure 플랫폼에 논의 합니다. 이 백서는 hello DBMS를 실행 하는 온-프레미스 환경에서와 마찬가지로 데이터베이스 관리 시스템 (DBMS)에서 Microsoft Azure 가상 컴퓨터 (IaaS)를 실행 하는 방법에 대 한 합니다. 이러한 두 환경에서의 데이터베이스 기능은 매우 다르므로 서로 혼합하지 않아야 합니다. 참고 항목: <https://azure.microsoft.com/services/sql-database/>
> 
> 

IaaS를 논의 이후 일반적 hello Windows, Linux 및 DBMS 설치 및 구성은 기본적으로 hello 모든 가상 컴퓨터 또는 베어 메탈 컴퓨터 온-프레미스를 설치 하는 것과 동일 합니다. 그러나 IaaS를 사용하는 경우 일부 아키텍처 및 시스템 관리 구현이 달라집니다. hello이 문서의 목적은 tooexplain hello 특정 아키텍처 및 시스템 관리의 차이 IaaS를 사용 하는 경우에 대 한 준비 해야 합니다.

일반적으로 hello 전반적인이 문서에 설명 하는 차이의 영역은 다음과 같습니다.

* SAP 시스템 tooensure의 hello 적절 한 VM/디스크 레이아웃 계획 hello 적절 한 데이터 파일 레이아웃이 있어야 하 고 작업에 대 한 충분 한 IOPS를 얻을 수 있습니다.
* IaaS 사용 시 네트워킹 고려 사항
* 주문 toooptimize hello 데이터베이스 레이아웃에서 특정 데이터베이스 기능 toouse 합니다.
* IaaS 사용 시 백업 및 복원 고려 사항
* 배포에 다양한 이미지 형식 사용
* Azure IaaS의 고가용성

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>RDBMS 배포 구조
순서로 toofollow이이 장에서 것을 필요한 toounderstand에서 제시한 [이] [ deployment-guide-3] hello 장 [배포 가이드] [ deployment-guide]. 에 대 한 지식을 hello 다른 VM 시리즈와의 차이점 및 Azure 표준 및 프리미엄 저장소의 차이점 이해 하 고 해야이 장의 읽기 전에 알려진 합니다.

2015 년 3 월까지 운영 체제를 포함 하는 디스크의 크기 제한 too127 GB 했습니다. 이 제한은 2015년 3월에 해제되었습니다(자세한 내용은 <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/> 확인). Hello 운영 체제를 포함 하는 hello 있을 수는 디스크에는 여기에서 다른 디스크를 크기를 동일 합니다. 그럼에도 불구 하 고 여전히 좋습니다 hello 운영 체제, DBMS 및 SAP 바이너리 궁극적는 별개임 hello 데이터베이스 파일을 배포의 구조를입니다. 따라서 Azure 가상 컴퓨터에서 실행 중인 SAP 시스템에는 hello 기본 VM (또는 디스크) hello 운영 체제, 데이터베이스 관리 시스템 실행 파일 및 SAP 실행 파일과 함께 설치가 라고 생각 됩니다. hello DBMS 데이터 및 로그 파일 (표준 또는 프리미엄 저장소) Azure 저장소에 별도 디스크에 저장 하 고 논리 디스크 toohello 원래 Azure 운영 체제 이미지 VM으로 첨부 됩니다. 

활용 하 여 Azure 표준 또는 프리미엄 저장소 (예를 들어 hello DS 시리즈 또는 GS 시리즈 Vm 사용)가 있는에 의존 하는 설명 되어 있는 Azure의 기타 할당량은 [여기 (Linux)] [ virtual-machines-sizes-linux] 및 [여기 (Windows)][virtual-machines-sizes-windows]합니다. 디스크 레이아웃을 계획할 때 다음 항목 hello에 대 한 toofind hello 최상의 hello 할당량 균형이 필요 합니다.

* hello 데이터 파일 수입니다.
* hello 파일을 포함 하는 디스크의 hello 수입니다.
* hello 단일 디스크의 IOPS 할당량입니다.
* 디스크당 hello 데이터 처리량입니다.
* VM 크기당 가능한 추가 데이터 디스크 개수는 hello 합니다.
* hello 전체 저장소 처리량 VM 제공할 수 있습니다.

Azure는 데이터 디스크 IOPS 할당량을 적용합니다. 이러한 할당량은 디스크가 Azure Standard Storage에서 호스트되는지 또는 Premium Storage에서 호스트되는지에 따라 달라집니다. Hello 두 가지 유형의 저장소 간에 더 나은 I/O 대기 시간이 요소를 제공 하는 프리미엄 저장소로 매우 I/O 대기 시간이 다릅니다. Hello 여러 VM 유형의 각 제한 된 수의 데이터 디스크 수 tooattach는에 있습니다. 또한 특정 VM 유형만 Azure Premium Storage를 활용할 수 있습니다. 즉, 특정 VM 유형은 대 한 hello 결정 하지만으로 인해 발생할 수 hello CPU 및 메모리 요구 사항으로 뿐만 아니라 hello IOPS, 대기 시간 및 디스크 처리량 요구 일반적으로 hello 수의 디스크와 크기가 조정 되어 또는 프리미엄 저장소 디스크의 종류를 환영 합니다. 프리미엄 저장소로 특히 디스크의 hello 크기 또한 수 있습니다. 따라 결정 hello에 필요한 각 디스크를 낼 수 toobe 처리량 및 IOPS 수 있습니다.

hello 전체 IOPS 속도, 탑재, 디스크 hello 수 및 크기의 VM은 모두 함께 묶는 것을 hello hello hello 사실을 온-프레미스 배포와 다른 SAP 시스템 toobe의 Azure 구성이 발생할 수 있습니다. LUN 당 IOPS 제한 hello 일반적으로 온-프레미스 배포에서 구성할 수 있습니다. 반면 Azure 저장소 한도 고정 또는 hello 디스크 종류에 의존 하는 프리미엄 저장소에서와 같이 합니다. 따라서 온-프레미스 배포와 데이터베이스 서버입니다. SAP와 같은 특수 한 실행 파일에 대 한 여러 다른 볼륨을 사용 하 고 hello DBMS 또는 임시 데이터베이스 또는 테이블 공간에 대 한 특별 한 볼륨의 고객 구성 표시 됩니다. 이동된 tooAzure 온-프레미스 시스템 등을 사용 하는 경우 데이터베이스 하나 또는 하지 많은 IOPS 수행 하지 않는 파일 또는 실행에 대 한 디스크를 낭비 하 여 잠재적인 IOPS 대역폭 낭비 tooa 발생할 수 있습니다 것입니다. 따라서 Azure Vm에서 가능한 경우 hello OS 디스크에 설치 하도록 hello DBMS 및 SAP 실행 파일을 하는 것이 좋습니다.

hello hello 데이터베이스 파일 및 로그 파일을 사용 하는 Azure 저장소의 hello 유형의 배치 여 정의 해야 IOPS, 대기 시간 및 처리량 요구 사항입니다. Hello 트랜잭션 로그에 대 한 충분 한 IOPS을 순서 toohave에 hello 트랜잭션 로그에 대 한 여러 개의 디스크 파일 또는 더 큰 프리미엄 저장소 디스크를 사용 하 여 강제 tooleverage 해야 수도 있습니다. 하나를 빌드하는 것이 경우 소프트웨어는 (예: Windows 저장소 풀에 대 한 Windows 또는 MDADM 및 Linux 용 (논리 볼륨 관리자) LVM) hello 트랜잭션 로그를 포함 하는 hello 디스크를 RAID 됩니다.

- - -
> ![Windows][Logo_Windows] Windows
> 
> Azure VM의 D:\ 드라이브는 비지속형 드라이브를 hello Azure 계산 노드에서 일부 로컬 디스크에 의해 지원 됩니다. 비지속형 이기 때문에 hello VM 다시 부팅 될 때 hello D:\ 드라이브의 변경 내용을 toohello 콘텐츠가 손실 된다는 것을 의미 합니다. "변경 내용"이란 저장된 파일, 생성된 디렉터리, 설치된 응용 프로그램 등을 의미합니다.
> 
> ![Linux][Logo_Linux] Linux
> 
> Azure Linux Vm는 자동으로 드라이브 hello Azure 계산 노드에서 로컬 디스크에서 지원 되는 비지속형 드라이브 /mnt/resource에 탑재 합니다. 비지속형 이기 때문에 hello VM 다시 부팅 될 때 /mnt/resource에 모든 변경 내용을 toocontent 손실 됨을 의미 합니다. 변경 내용이란 저장된 파일, 생성된 디렉터리, 설치된 응용 프로그램 등을 의미합니다.
> 
> 

- - -
Azure VM 시리즈 hello에 종속, hello hello 로컬 디스크 노드 표시 다른 성능 같은 분류할 수 있는 계산:

* A0-A7: 매우 제한된 성능. Windows 페이지 파일 이외에 어떤 것에 대해서도 사용할 수 없음
* A8-A11: 매우 양호한 성능(수 만개의 IOPS 및 1GB/초 이상의 처리량)
* D 시리즈: 매우 양호한 성능(수 만개의 IOPS 및 1GB/초 이상의 처리량)
* DS 시리즈: 매우 양호한 성능(수 만개의 IOPS 및 1GB/초 이상의 처리량)
* G 시리즈: 매우 양호한 성능(수 만개의 IOPS 및 1GB/초 이상의 처리량)
* GS 시리즈: 매우 양호한 성능(수 만개의 IOPS 및 1GB/초 이상의 처리량)

위의 문을 sap에 인증 된 toohello VM 유형에 적용 하는 합니다. 뛰어난 IOPS 및 처리량 VM 시리즈 hello 활용 하는 방법에 대 한 tempdb 또는 임시 테이블 공간와 같은 일부 DBMS 기능을 사용 하 여 한정 합니다.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>VM 및 데이터 디스크에 대한 캐싱
데이터 디스크 hello 포털에서 또는 tooVMs 업로드 된 디스크를 탑재 하는 것을 만들면 hello VM 및 Azure 저장소에 있는 해당 디스크 간의 I/O 트래픽을 hello 캐시 되는지 여부를 선택할 수 있습니다. Azure Standard 및 Premium Storage에서는 이 유형의 캐시에 대해 두 가지 기술을 사용합니다. 두 경우 모두 hello 캐시 자체는 hello 임시 디스크 (Windows에서 D:\) 또는 Linux에서 /mnt/resource hello VM의 여 hello를 사용 하는 동일한 드라이브에서 지 원하는 디스크 것입니다.

표준 저장소 Azure hello 가능한 캐시 유형은 다음과 같습니다.

* 캐싱 없음
* 읽기 캐싱
* 읽기 및 쓰기 캐싱

Hello Azure 표준 저장소에 포함 된 모든 디스크에 대 한 캐싱을 설정 해야 순서 tooget 일관성 있고 명확한 성능을에서 **DBMS 관련 데이터 로그 파일, 파일과 테이블 공간 too'NONE'**합니다. 기본값은 hello hello hello VM의 캐싱을 남을 수 있습니다.

Azure 프리미엄 저장소에 대 한 캐싱 옵션을 다음 hello가 있습니다.

* 캐싱 없음
* 읽기 캐싱

Azure 프리미엄 저장소에 권장 되는 tooleverage **읽기 데이터 파일에 대 한 캐싱을** hello SAP 데이터베이스와 선택한 **hello 디스크 로그 파일에 대 한 캐싱 없음**합니다.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>소프트웨어 RAID
설명한 것 처럼 위에서 필요한 hello 여러 디스크에 걸쳐 hello 데이터베이스 파일에 구성할 수 있으며 최대 IOPS 당 디스크나 프리미엄 저장소 디스크 형식을 제공 하는 Azure VM hello IOPS의 toobalance hello 번호가 필요 합니다. 디스크에 걸쳐 IOPS 부하 hello로 가장 쉬운 방법은 toodeal toobuild hello 서로 다른 디스크에 걸쳐 소프트웨어 RAID입니다. 다음 LUN hello 소프트웨어 RAID 된 hello에 다양 한 hello SAP DBMS의 데이터 파일을 배치 합니다. Tooconsider hello 뿐만 아니라 사용 프리미엄 저장소의 경우가 hello 요구 사항에 따라 달라 두 hello 이후 세 가지 다른 프리미엄 저장소 디스크 제공 표준 저장소에 따라 디스크 보다 더 높은 IOPS 할당량 합니다. Azure 프리미엄 저장소에서 I/O 대기 시간을 제공 하는 더 중요 한 hello 외에 합니다. 

Hello 다른 DBMS 시스템의 toohello 트랜잭션 로그에도 마찬가지입니다. 더 많은 Tlog 파일을 추가 하는 것 중 많은 hello DBMS 시스템 hello 파일 중 하나에 한 번에 쓰기 때문 도움이 되지 않습니다. 단일 표준 기반 저장소 보다 IOPS 속도 더 필요한 경우 디스크 제공할 수 있는 여러 표준 저장소 디스크에 걸쳐 스트라이프 할 수 있습니다. 또는 더 큰 프리미엄 저장소 디스크 형식을 전달 하는 IOPS 속도 더 이상도 요소 더 낮은 대기 시간 hello 쓰기를 위해 사용할 수 있습니다. Hello 트랜잭션 로그에 I/o를 제공 합니다.

Azure 배포에서 소프트웨어 RAID를 사용해야 하는 상황은 다음과 같습니다.

* 트랜잭션 로그/다시 실행 로그에서 Azure에서 단일 디스크에 제공하는 것보다 더 많은 IOPS를 필요로 하는 경우. 위에서 언급한 대로 소프트웨어 RAID를 사용하여 여러 디스크에 LUN을 빌드하여 이 문제를 해결할 수 있습니다.
* I/O 작업 불균일 hello 서로 다른 데이터 파일에 대해 hello SAP 데이터베이스의 합니다. 이러한 경우에 종종 대신 hello 할당량에 도달 하는 하나의 데이터 파일에서 경험할 수 있는 하나. 반면 다른 데이터 파일도 단일 디스크의 IOPS 할당량 닫기 toohello를 가져오지 않습니다. 이러한 경우 hello에 가장 쉬운 방법은 하나 toobuild 소프트웨어 RAID를 사용 하 여 여러 디스크에 걸쳐 LUN. 
* 알 수 없는 어떤 hello 정확한 I/O 작업의 데이터 파일당은 및 에서만 대략 hello 무엇을 알고 전체 DBMS hello에 대 한 IOPS 작업 됩니다. 가장 쉬운 toodo toobuild hello로 하나의 LUN 소프트웨어 RAID의 도움말입니다. 이 LUN 뒤에 있는 여러 디스크의 할당량의 hello 합 해야 IOPS 알려진 hello 충족 다음 속도입니다.

- - -
> ![Windows][Logo_Windows] Windows
> 
> Windows Server 2012 이상을 실행하는 경우 Windows 저장소 공간을 사용하는 것이 좋습니다. 이렇게 하는 것이 Windows 이전 버전의 Windows 스트라이프보다 더 효율적입니다. 운영 체제와 Windows Server 2012를 사용 하는 경우 PowerShell 명령을 사용 하 여 toocreate hello Windows 저장소 풀 및 저장소 공간을 할 수 있습니다. hello PowerShell 명령을 확인할 수 있습니다 <https://technet.microsoft.com/library/jj851254.aspx>
> 
> ![Linux][Logo_Linux] Linux
> 
> MDADM와 LVM (논리 볼륨 관리자)만 지원 되는 소프트웨어 RAID linux toobuild 됩니다. 자세한 내용은 다음 문서는 hello 읽기:
> 
> * [Linux에서 소프트웨어 RAID 구성][virtual-machines-linux-configure-raid](MDADM용)
> * [Azure에서 Linux VM에 LVM 구성][virtual-machines-linux-configure-lvm]
> 
> 

- - -
VM 시리즈 수 toowork Azure 프리미엄 저장소를 일반적으로 활용 하기 위해 고려 사항이 있습니다.

* I/O 대기 시간이 잘못에 대 한 요청이 toowhat SAN/NAS 장치 배달을 닫습니다.
* Azure 표준 저장소에서 제공할 수 있는 것보다 더 나은 I/O 대기 시간 요소에 대한 요구
* 특정 VM 유형에 대해 여러 표준 저장소 디스크를 사용하여 얻을 수 있는 것보다 더 높은 VM당 IOPS

Hello 이후 기본 Azure 저장소 복제 각 디스크 tooat 최소 3 저장소 노드에 간단한 RAID 0 스트라이프를 사용할 수 있습니다. RAID5 또는 RAID1 필요 tooimplement 하지 않습니다.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Microsoft Azure Storage
Microsoft Azure 저장소 저장소 기본 VM (OS) 및 디스크 또는 Blob tooat 최소 세 개의 별도 저장소 노드에 hello 합니다. 저장소 계정 또는 관리 디스크를 만들 때는 다음과 같은 보호를 선택할 수 있습니다.

![Azure 저장소 계정에 대해 지역에서 복제 사용][dbms-guide-figure-100]

(로컬 중복) azure 저장소 로컬 복제 적은 수의 고객이 toodeploy를 구입할 수 있었습니다 tooinfrastructure 오류로 인해 데이터 손실 로부터 보호 수준을 제공 합니다. 위와 같이 다섯 번째 되 고 hello 중 하나의 변형 처음 세 개의 서로 다른 옵션이 4 가지입니다. 자세히 살펴보면 다음과 같이 구분할 수 있습니다.

* **프리미엄 LRS(로컬 중복 저장소)**: Azure Premium Storage는 I/O 사용량이 많은 워크로드를 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다. Hello 내 hello 데이터의 복제본 세 가지 Azure 지역의 동일한 Azure 데이터 센터입니다. hello 복사본은 다른 장애 및 업그레이드 도메인 (개념 참조에 대 한 [이] [ planning-guide-3.2] hello 장 [계획 가이드][planning-guide]). Tooa 저장소 노드 오류 또는 디스크 오류로 인해 서비스에서 나가는 hello 데이터의 복제본을 발생 한 경우 새 복제본을 자동으로 생성 됩니다.
* **로컬 중복 저장소 (LRS)**:이 경우 hello 내 hello 데이터의 복제본 세 있습니다. Azure 지역의 동일한 Azure 데이터 센터입니다. hello 복사본은 다른 장애 및 업그레이드 도메인 (개념 참조에 대 한 [이] [ planning-guide-3.2] hello 장 [계획 가이드][planning-guide]). Tooa 저장소 노드 오류 또는 디스크 오류로 인해 서비스에서 나가는 hello 데이터의 복제본을 발생 한 경우 새 복제본을 자동으로 생성 됩니다. 
* **지역 중복 저장소 (GRS)**:이 경우에 세 개의 추가 피드 있는 비동기 복제 대부분의 hello 사례에 있는 다른 Azure 지역의 hello 데이터의 복제본이 hello 동일한 지리적 지역 (예: 유럽 북부 및 서 부 유럽)입니다. 따라서 3개의 추가 복제본이 생기므로 총 6개의 복제본이 있습니다. 이 변형을 추가 되는 (읽기 액세스 지리적 중복) 읽기 위해 hello 지리적 복제 된 Azure 지역에서 hello 데이터를 사용할 수 있는 위치입니다.
* **영역 중복 저장소 (ZRS)**:이 경우 3 hello 복제본의 데이터에 유지 하는 hello hello 같은 Azure 지역입니다. 에 설명 된 대로 [이] [ planning-guide-3.1] hello 장 [계획 가이드] [ planning-guide] 서로 가까이 있는 Azure 지역 데이터 센터의 수를 수 있습니다. LRS hello 경우에서 Azure 지역에 있도록 hello 서로 다른 데이터 센터에 대해 hello 복제본 배포 합니다.

자세한 내용은 [여기][storage-redundancy]에 있습니다.

> [!NOTE]
> DBMS 배포에 대 한 지리 중복 저장소의 hello 사용은 권장 되지 않습니다.
> 
> Azure 저장소 지역에서 복제는 비동기적입니다. 개별 디스크의 복제 탑재 tooa 잠금 단계에서는 단일 VM이 동기화 되지 않습니다. 따라서 서로 다른 디스크에 배포 되거나 여러 디스크에 따라 RAID는 소프트웨어에 대해 배포 된 적합 한 tooreplicate DBMS 파일 않습니다. DBMS 소프트웨어 다른 Lun 및 기본 디스크/스핀 들 간에 hello 영구 디스크 저장소가 정확 하 게 동기화 되는 필요 합니다. DBMS 소프트웨어는 다양 한 메커니즘 toosequence IO 쓰기 작업을 사용 하 고 DBMS 몇 밀리초 해도 다른 경우 hello 복제에 의해 대상으로 하는 hello 디스크 저장소가 손상 되었다고 보고 합니다. 따라서 지리적으로 복제 된 여러 디스크에 걸친 데이터베이스로 사용 하려는 데이터베이스를 구성, 이러한 복제 toobe 데이터베이스 수단 및 기능을 사용 하 여 수행 해야 합니다. 하나 안됩니다 Azure 저장소 지역 간 복제 tooperform이이 작업 합니다. 
> 
> hello 문제는 예를 통해 가장 간단한 tooexplain입니다. Azure의 hello DBMS의 데이터 파일을 포함 하는 8 개의 디스크와 하나의 hello 트랜잭션 로그 파일을 포함 하는 업로드 된 SAP 시스템이 있다고 가정해 보겠습니다. 이러한 9 개의 디스크 중 하나를 각 된 hello 데이터를 쓰고 toohello 데이터 또는 트랜잭션 로그 파일이 있는지 여부를 toothem toohello DBMS에 따라 일관 된 방법으로 작성 하는 데이터가 있습니다.
> 
> 순서 대로 tooproperly 지역 간 복제 데이터 hello 및 동일한 데이터베이스 이미지, hello 콘텐츠를 유지 관리의 모든 디스크 9 개 toobe hello 정확한 순서 hello I/O 작업에서 지리적 복제 된 실행 한 hello 9 서로 다른 디스크에 대 한 합니다. 그러나 Azure 저장소 지역 간 복제는 디스크 간에 toodeclare 종속성을 허용 하지 않습니다. 즉, Microsoft Azure 저장소 지역 간 복제 hello 팩트 다른 관련된 tooeach 있고 hello 데이터 변경 내용이 일관적 hello 순서 hello I/O 작업에서 복제 하는 경우에 이러한 9 개의 서로 다른 디스크에 hello 내용이 되었는지 알 수 없습니다. 모든 hello 9 개의 디스크 발생 했습니다.
> 
> 가능성이 높게 hello 지리적 복제 이미지 hello 시나리오에서 동일한 데이터베이스 이미지를 제공 하지 않으면, 또한 성능이 크게 저하 될 심각 하 게 수행할 수 있는 지역 중복 저장소 보여 주는 것 외에도 성능 영향을 줄 합니다. 한 마디로 말해 DBMS 형식 워크로드에 대해서는 이러한 유형의 저장소 중복을 사용하지 마세요.
> 
> 

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>VHD를 Azure 가상 컴퓨터 서비스 저장소 계정에 매핑
이 장에서 tooAzure 저장소 계정에만 적용 됩니다. Toouse 관리 하는 디스크를 사용 하도록 하려는 경우에이 장에서 설명한 hello 제한이 적용 되지 않습니다. Managed Disks에 대한 자세한 내용은 이 가이드의 [Managed Disks][dbms-guide-managed-disks] 챕터를 참조하세요.

Azure 저장소 계정은 관리 구성 요소일 뿐 아니라 제한의 대상이 됩니다. 반면 Azure 표준 저장소 계정 또는 Azure 프리미엄 저장소 계정에 대해 논의할 여부에 따라 다를 hello 제한 합니다. 나열 된 hello 정확한 기능 및 제한 사항 [여기][storage-scalability-targets]

저장소 계정당 IOPS hello에는 제한이 되므로 Azure 표준 저장소에 대 한 중요 한 toonote (의 ' 총 요청 속도입니다. ' 포함 된 행 [hello 문서][storage-scalability-targets]). 또한 2015년 7월 현재 초기 제한은 Azure 구독당 100개의 저장소 계정으로 설정되어 있습니다. 따라서 Azure 표준 저장소를 사용 하는 경우 여러 저장소 계정 간에 IOPS Vm toobalance를 좋습니다. 반면 단일 VM은 가능한 경우 하나의 저장소 계정을 사용하는 것이 이상적입니다. 따라서 Azure 표준 저장소에서 호스트되는 각 VHD가 해당 할당량 한도에 도달할 수 있는 DBMS 배포의 경우 Azure 표준 저장소를 사용하는 Azure 저장소 계정당 30-40개의 VHD만 배포해야 합니다. Hello Azure 프리미엄 저장소를 활용 하 고 toostore 큰 데이터베이스의 볼륨을 원하는 경우 수 있습니다 IOPS를 기준으로 세밀 하 게 합니다. 하지만 Azure Premium Storage 계정은 데이터 볼륨 면에서 Azure 표준 저장소 계정보다 훨씬 더 제한적입니다. 결과적으로, hello 데이터 볼륨 제한에 도달 하기 전에 Azure 프리미엄 저장소 계정 내의 Vhd 수가 제한만 배포할 수 있습니다. Hello 끝에는 Azure 저장소 계정으로 생각할 IOPS 및/또는 용량에는 기능이 제한 되어 "가상 SAN". 결과적으로, hello 작업 toodefine hello 레이아웃의 hello hello hello 다른 '가상 SAN 장치'를 통해 서로 다른 SAP 시스템의 Vhd 또는 Azure 저장소 계정, 온-프레미스 배포 에서처럼 유지 합니다.

다른 저장소 계정 tooa에서 toopresent 저장소는 좋지 않습니다 Azure 표준 저장소에 대 한 VM을 가능 하면 단일 합니다.

Hello DS 또는 GS 시리즈 Azure Vm의를 사용할 경우에 Azure 저장소 계정 표준 및 프리미엄 저장소 계정의 Vhd 가능한 toomount이 있습니다. 표준 저장소에 백업을 쓰는 백업 Vhd DBMS 데이터 및 프리미엄 저장소에 로그 파일에와 야 toomind 이러한 다른 유형의 저장소를 이용 될 수와 같은 사례를 사용 합니다. 

데이터베이스 데이터 파일과 로그 파일에 포함 된 Vhd에 허용 가능한 성능 갖춘 단일 Azure 표준 저장소 계정이 프로 비전 할 수의 고객 배포 및 테스트 약 30 too40 기반으로 합니다. 앞서 언급 했 듯이 보유할 수 있는 가능성이 toobe hello 데이터 용량 및 IOPS 하지 Azure 프리미엄 저장소 계정을의 hello 제한은입니다.

일부 모니터링 순서 tooeventually에 필요한 공유 SAN 장치 온-프레미스, Azure 저장소 계정에서 병목 상태를 검색 합니다. SAP 용 Azure 모니터링 확장 hello 및 hello Azure 포털 사용된 toodetect 일 수 있는 도구는 불충분 한 IO 성능을 제공 하 고 있는 Azure 저장소 계정 사용 중입니다.  이러한 상황이 감지 되 면 toomove 사용 중 Vm tooanother Azure 저장소 계정 좋습니다. Toohello 참조 [배포 가이드] [ deployment-guide] tooactivate hello SAP 모니터링 기능을 호스트 하는 방법에 대 한 내용은 합니다.

Azure 표준 저장소 및 Azure 표준 저장소 계정에 대한 모범 사례를 요약한 다른 문서는 여기(<https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>)를 참조하세요.

#### <a name="f42c6cb5-d563-484d-9667-b07ae51bce29"></a>Managed Disks
Managed Disks는 Azure Storage 계정에 저장된 VHD 대신 사용할 수 있는 Azure Resource Manager의 새로운 리소스 종류입니다. 관리 되는 디스크는 hello 가상 컴퓨터의 가용성 집합 연결 tooand 따라서 가상 컴퓨터와 hello 가상 컴퓨터에서 실행 되는 hello 서비스의 hello 가용성 향상 hello로 자동으로 맞춥니다. toolearn hello를 더 읽기 [개요 문서](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview)합니다.

SAP는 현재 Premium Managed Disks만 지원합니다. 자세한 내용은 SAP Note [1928533]을 읽어 보세요.’

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>Azure 표준 저장소 tooAzure 프리미엄 저장소에서에서 DBMS Vm을 배포 이동
상당한 있는 시나리오는 고객으로 서 Azure 표준 저장소에서 배포 된 VM toomove Azure 프리미엄 저장소로 발생 합니다. 디스크는 Azure 저장소 계정으로 저장 하는 경우이 불가능 hello 데이터를 실제로 이동 하지 않고 합니다. 여러 가지 방법으로 tooachieve hello 목표 가지가 있습니다.

* 모든 VHD, 기본 VHD 및 데이터 VHD를 새 Azure Premium Storage 계정으로 간단하게 복사할 수 있습니다. 종종 hello 데이터 볼륨 필요 함을 hello 사실 때문이 아니라 Azure 표준 저장소에 Vhd 수가 hello 선택한입니다. 하지만 IOPS hello 때문에 많은 Vhd 필요 합니다. TooAzure 이동 했으므로 더 적은 Vhd tooachieve 방법을 이동할 수는 프리미엄 저장소 hello IOPS 처리량을 동일 합니다. Hello에 대 한 비용을 지불 하는 표준 Azure 저장소에 사용 하는 데이터 hello 최소 디스크 크기가 아니라 hello 팩트 들어 hello Vhd 수가 않았습니다 실제로 중요 하지 비용 측면에서. 그러나 Azure 프리미엄 저장소를 지불할 hello 최소 디스크 크기에 대 한 합니다. 따라서 대부분의 고객 hello hello 숫자 필요한 tooachieve hello IOPS 처리량에서 필요한 프리미엄 저장소에 Azure Vhd의 tookeep hello 번호를 선택 하십시오. 따라서 대부분의 고객 복사본 간단한 1:1 hello 방법에 대해 결정합니다.
* 탑재되지 않은 경우 SAP 데이터베이스의 데이터베이스 백업을 포함할 수 있는 단일 VHD를 탑재합니다. Hello 백업 후 hello VHD 포함 hello 백업을 비롯 하 여 모든 Vhd를 탑재 해제 하 고 복사 hello 기본 VHD 및 Azure 프리미엄 저장소 계정에 VHD hello 백업을 사용 하 여 hello 합니다. Hello hello 기본 VHD 및 탑재 hello VHD hello 백업 사용 하 여을 기반으로 하는 VM 배포 했습니다. 추가로 만들 이제 VM hello에 대 한 프리미엄 저장소 디스크에 사용 되는 toorestore hello 데이터베이스를 비웁니다. 이 해당 hello DBMS 있습니다 toochange 경로 toohello 데이터 및 로그 파일 hello 복원 프로세스의 일환으로 가정 합니다.
* 또 다른 원인은 hello 이전 프로세스를 방금 hello 백업 VHD Azure 프리미엄 저장소로 복사한 있는 새로 배포 하 고 설치 하는 VM에 대 한 연결의 변형입니다.
* 네 번째 가능성 hello toochange hello 수 데이터베이스의 데이터 파일의가 필요할 경우 선택 합니다. 이 경우 내보내기/가져오기를 사용하여 형식이 같은 SAP 시스템 복사를 수행합니다. Azure 프리미엄 저장소 계정에 복사 된 VHD에 내보내기 파일 및 tooa toorun hello 가져오기 프로세스를 사용 하는 VM을 연결 하는 것에 넣어야 합니다. 고객은 데이터 파일의 toodecrease hello 수 하려는 경우에 주로이 가능성을 사용 합니다.

관리 되는 디스크를 사용 하면 tooPremium 저장소를 마이그레이션할 수 있습니다 하 여:

1. Hello 가상 컴퓨터 할당 취소
2. 필요한 경우 (예: DS 또는 GS) 프리미엄 저장소를 지 원하는 hello 가상 컴퓨터 tooa 크기 조정
3. Hello 디스크 관리 되는 계정 유형 tooPremium (SSD) 변경
4. 가상 컴퓨터 시작

### <a name="deployment-of-vms-for-sap-in-azure"></a>Azure의 SAP용 VM 배포
Microsoft Azure에서는 여러 가지 방법으로 toodeploy Vm 및 연결 된 디스크가 있습니다. 함으로써가 중요 한 toounderstand hello 차이가 있으므로 hello vm 준비 hello 방식의 배포에 종속 다를 수 있습니다. 일반적으로 다음 장 hello에 설명 된 hello 시나리오로 찾습니다.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Hello Azure Marketplace에서에서 VM 배포
Tootake Microsoft 또는 타사 VM hello Azure 마켓플레이스 toodeploy에서 이미지를 제공 합니다. Hello를 수행 하는 Azure에서 VM을 배포한 후 온-프레미스 환경에서 때와 동일한 지침 및 도구 tooinstall hello VM 내부에 SAP 소프트웨어. Hello Azure VM 내에 hello SAP 소프트웨어를 설치 하기 위한 SAP 및 Microsoft 업로드 하는 것이 좋습니다 고 hello SAP 설치 미디어에 저장할 디스크 또는 toocreate Azure VM '파일 서버' hello 필요한 SAP 설치 미디어가 모두 포함 된으로 작동 합니다.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>고객별 범용 이미지를 사용하여 VM 배포
OS 또는 DBMS 버전과 관련 된 toospecific 패치 요구 사항, 기한 hello Azure Marketplace에서에서 제공 하는 hello 이미지 요구 사항 맞지 않을 수 있습니다. 따라서 이후 여러 번 배포할 수 있는 '개인' OS/DBMS VM 이미지를 사용 하는 VM toocreate를 할 수 있습니다. 복제용 '개인' 이미지 tooprepare hello에 운영 체제를 일반화 해야 합니다는 hello 온-프레미스 VM입니다. Toohello 참조 [배포 가이드] [ deployment-guide] 방법에 대 한 자세한 내용은 toogeneralize VM입니다.

Hello 배포 hello 인스턴스를 통해 hello Azure VM의 SAP 소프트웨어 구축 hello에서 지원 되는 프로시저 이름 바꾸기 후 hello SAP 시스템 설정을 조정할 수 있는지 (특히 2 계층 시스템) 용 온-프레미스 VM에서 SAP 콘텐츠를 이미 설치한 경우 관리자 (SAP Note [1619720]). 그렇지 않으면 hello Azure VM의 hello 배포 후 나중에 hello SAP 소프트웨어를 설치할 수 있습니다.

Hello SAP 응용 프로그램에서 사용 하는 hello 데이터베이스 내용을 기준으로 SAP 설치를 통해 hello 콘텐츠를 새롭게 생성할 수도 있습니다 또는 DBMS 데이터베이스 백업이 저장 된 VHD를 사용 하 여 또는 hello DBMS toodirectly의 기능을 활용 하 여 Azure에 콘텐츠를 가져올 수 있습니다. Microsoft Azure 저장소로 백업입니다. 이 경우에 DBMS 데이터 hello로 Vhd를 준비 하 고 및 로그 파일 온-프레미스 하 고, 다음 Azure 디스크로 가져올 수 있습니다. 하지만 온-프레미스 tooAzure에서 로드 되는 DBMS 데이터의 hello 전송 toobe 온-프레미스를 준비 해야 하는 VHD 디스크를 통해 작동할 것입니다.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>일반화 되지 않은 디스크와 온-프레미스 tooAzure에서 VM 이동
확인할 toomove 온-프레미스 tooAzure (리프트 및 shift)에서 특정 SAP 시스템을 계획합니다. 이 OS hello, hello SAP 바이너리 및 결과적 DBMS 바이너리를 포함 하는 hello 디스크로 페이징하지 hello 데이터로 hello 디스크를 업로드 하 여 수행할 수 있습니다 및 로그 파일의 hello DBMS tooAzure 합니다. 반대 tooscenario 위의 2, 유지 있습니다 hello 호스트 이름, SAP SID 및 SAP 사용자 계정은 hello Azure VM에서에서 hello 온-프레미스 환경에서 구성 된 것입니다. 따라서 hello 이미지를 일반화 필요는 없습니다. 이 경우 SAP 지형 hello의 일부가 실행 되는 위치 부품 온-프레미스 및 Azure에서 크로스-프레미스 시나리오에 주로 적용 됩니다.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Azure VM을 사용한 고가용성 및 재해 복구
Azure에서는 SAP 및 DBMS 배포용 사용 하면 toodifferent 구성 요소에 적용 되는 HA (고가용성) 및 DR (재해 복구) 기능을 수행 하는 hello

### <a name="vms-deployed-on-azure-nodes"></a>Azure 노드에 배포된 VM
hello Azure 플랫폼은 배포 된 Vm에 대 한 실시간 마이그레이션과 같은 기능을 제공 하지 않습니다. 즉, 한 VM을 배포 하는 서버 클러스터에 필요한 유지 관리 없는, 경우 hello VM tooget 중지 되었다가 다시 시작 합니다. Azure에서의 유지 관리는 서버 클러스터 내의 업그레이드 도메인을 통해 수행됩니다. 한 번에 하나의 업그레이드 도메인만 유지 관리됩니다. 이러한 다시 시작 하는 동안 hello VM을 종료 하는 동안 서비스의 중단, 유지 관리를 수행 하 고 VM 다시 시작 합니다. 그러나 대부분의 DBMS 공급 업체는 hello 주 노드를 사용할 수 없는 경우 다른 노드에서 DBMS 서비스 hello를 신속 하 게 다시 시작 하는 고가용성 및 재해 복구 기능을 제공 합니다. hello Azure 플랫폼 기능 toodistribute Vm, 저장소 및 기타 Azure 서비스에서 유지 관리 또는 인프라 오류가 계획 된 업그레이드 도메인 tooensure만 영향을 미치도록 Vm 또는 서비스의 작은 하위 집합을 제공 합니다.  신중 하 게 계획 하는 사용 가능한 tooachieve 가용성 수준 비교 가능한 tooon 온-프레미스 인프라 집니다.

Microsoft Azure 가용성 집합은 Vm의 논리적 그룹 또는 Vm을 보장 하는 서비스 및 기타 서비스 되는 분산된 toodifferent 오류 도메인과 업그레이드 도메인 클러스터 내에서 됩니다 한 노드가 종료 한 시점에서 ( 읽기시간[(Linux)이] [ virtual-machines-manage-availability-linux] 또는 [(Windows)이] [ virtual-machines-manage-availability-windows] 을 참조 하십시오).

다음 그림과 같이 Vm을 롤아웃하는 경우 목적에 맞게 구성 toobe 필요:

![DBMS HA 구성에 대한 가용성 집합 정의][dbms-guide-figure-200]

Toocreate 항상 사용 가능한 독립 hello 개별 DBMS HA 기능 사용의 DBMS 배포 구성을 원하는 경우에 hello DBMS Vm에 필요 합니다.

* Hello Vm toohello 추가 동일한 Azure 가상 네트워크 (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* hello hello HA 구성의 Vm hello에 속해 있어야 동일한 서브넷입니다. Hello 서로 다른 서브넷 간의 이름 확인 클라우드 전용 배포에서는 IP 확인 works만 수는 없습니다. 프레미스 간 배포에 대한 ExpressRoute 또는 사이트 간 연결을 사용하여 하나 이상의 서브넷이 있는 네트워크가 이미 구성되어 있습니다. 이름 확인을 수행 toohello에 따라 온-프레미스 AD 정책 및 네트워크 인프라입니다. 

[comment]: <> (ARM에서 여전히 true인 경우 MSSedusch TODO 테스트)

#### <a name="ip-addresses"></a>IP 주소
HA 구성 위한 toosetup hello Vm 복원이 쉬운 방식으로 매우 권장 됩니다. Hello HA 구성 내에서 IP 주소 tooaddress hello HA 파트너에 의존 하지 않는 Azure에서 신뢰할 수 있는 고정 IP 주소 사용 됩니다. Azure에는 두 가지 “종료” 개념이 있습니다.

* Azure 포털에서 또는 Azure PowerShell cmdlet 중지 AzureRmVM 종료:이 경우 hello 가상 컴퓨터 종료 되 고 할당을 취소 합니다. Azure 계정은 사용 하는 hello 저장소 유발 hello만 금액이 청구 되므로 더 이상이 VM에 대 한 청구 됩니다. 그러나 hello hello 네트워크 인터페이스의 개인 IP 주소를 고정 한 경우 hello IP 주소가 해제 되 고 해당 hello 네트워크 인터페이스 hello VM의 다시 시작 후에 다시 할당 된 hello 이전 IP 주소를 가져옵니다는 보장 되지 않습니다. Hello 수행 hello를 통해 Azure 포털 종료 되었거나 중지 AzureRmVM를 자동으로 호출 하 여 할당 취소로 인해 수도 있습니다. Toodeallocate hello 컴퓨터 사용 중지 AzureRmVM StayProvisioned 원하지 않는 경우 
* Hello OS 수준에서 VM 종료 하면 VM hello 가져옵니다 종료 하 고 할당이 취소 되지는 않습니다. 그러나이 경우 Azure 계정 청구 되며 VM 종료 된다는 hello 사실에 입각 불구 하 고 hello에 대 한 합니다. 이러한 경우 hello IP 주소 tooa의 hello 할당 중지 VM은으로 그대로 유지가 되었습니다. Hello 종료 vm 내에서 VM 강제로 하지 않음을 자동으로 할당 취소 합니다.

크로스-프레미스 시나리오에 대해서도 기본적으로 종료 및 할당 취소에서 VM hello hello IP 주소의 할당 취소 경우에 의미 DHCP 설정의 온-프레미스 정책이 서로 다릅니다. 

* hello 예외는 고정 IP 주소 tooa 네트워크 인터페이스를 할당 한 경우 설명 [여기][virtual-networks-reserved-private-ip]합니다.
* 이러한 경우 hello IP 주소는 유지 됩니다 고정 hello 네트워크 인터페이스는 삭제 되지 않습니다.

> [!IMPORTANT]
> 순서 tookeep hello 전체 배포에서 간단 하 고 관리할 수 있는 권장 toosetup 명확한 hello Vm hello 관련 된 여러 Vm 간에 이름 확인이 방식으로 Azure 내에서 DBMS HA 또는 DR 구성의 파트너 hello 합니다.
> 
> 

## <a name="deployment-of-host-monitoring"></a>호스트 모니터링 배포
Azure 가상 컴퓨터의 SAP 응용 프로그램의 생산적인 사용에 대 한 SAP hello 기능 tooget 호스트 hello Azure 가상 컴퓨터를 실행 하는 hello 물리적 호스트에서 데이터를 모니터링 해야 합니다. SAPOSCOL 및 SAP HostAgent에서 이 기능을 사용하려면 특정 SAP HostAgent 패치 수준이 필요합니다. hello 정확한 패치 수준은 SAP Note에서 설명 [1409604]합니다.

호스트 데이터 tooSAPOSCOL 및 SAP 호스트 에이전트를 제공 하는 구성의 배포 및 해당 구성 요소의 hello 수명 주기 관리에 대 한 hello 내용은 toohello 참조 [배포 가이드][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>구체적인 tooMicrosoft SQL Server
### <a name="sql-server-iaas"></a>SQL Server IaaS
Microsoft Azure부터 Windows Server 플랫폼 tooAzure 가상 컴퓨터에서 빌드된 기존 SQL Server 응용 프로그램 쉽게 마이그레이션할 수 있습니다. 가상 컴퓨터에서 SQL Server에는 이러한 응용 프로그램 tooMicrosoft Azure로 쉽게 마이그레이션하여 여 있습니다 tooreduce hello 총 소유 비용을의 배포, 관리 및 유지 관리의 엔터프라이즈 범위의 응용 수 있습니다. SQL Server는 Azure 가상 컴퓨터에서 사용 관리자와 개발자가 hello 동일한 개발 및 관리 도구를 사용할 수 있는 온-프레미스를 계속 사용할 수 있습니다. 

> [!IMPORTANT]
> 하지 논의 Microsoft Azure SQL 데이터베이스의 hello Microsoft Azure 플랫폼 서비스 제품으로 하는 플랫폼입니다. 이 문서에 대 한 hello 설명은 온-프레미스 배포에서 Azure 가상 컴퓨터를 활용 hello Azure의 서비스 기능으로는 인프라에 대 한 알려진 hello SQL Server 제품을 실행 하는 방법에 대 한 않습니다. 이러한 두 환경에서의 데이터베이스 기능은 다르므로 서로 혼합하지 않아야 합니다. 참고 항목: <https://azure.microsoft.com/services/sql-database/>
> 
> 

Tooreview이 가장 좋습니다 [이] [ virtual-machines-sql-server-infrastructure-services] 계속 하기 전에 문서입니다.

Hello에 부분에서 위의 hello 링크 hello 설명서의 다음 섹션에서는 데이터가 집계 되어 언급 합니다. SAP에 대한 정보도 언급되며 몇 가지 개념도 보다 자세히 설명합니다. 그러나 hello SQL Server 관련 문서를 읽기 전에 먼저 위에 hello 설명서를 통해 toowork를 좋습니다 됩니다.

계속하기 전에 다음과 같은 IaaS의 SQL Server 관련 정보를 참조하세요.

* **Virtual Machine SLA**: Azure에서 실행 중인 Virtual Machines용 SLA는 <https://azure.microsoft.com/support/legal/sla/>에 있습니다.  
* **SQL 버전 지원**: SAP 고객의 경우 Microsoft Azure Virtual Machines에서 SQL Server 2008 R2 이상 버전을 지원합니다. 이전 버전은 지원되지 않습니다. 자세한 내용은 이 일반 [지원 설명](https://support.microsoft.com/kb/956893) 을 참조하세요. 일반적으로 SQL Server 2008은 Microsoft에서도 지원됩니다. 그러나 SQL Server 2008 r 2와 함께 도입 된 SAP 용 toosignificant 기능 인해 SQL Server 2008 r 2는 hello SAP 용 최소 릴리스입니다. SQL Server 2012 및 2014 hello IaaS 시나리오 (예: Azure 저장소로 직접 백업)를 밀접 하 게 통합 된 확장 염두에서에 둬야 합니다. 따라서 제한할이 용지 tooSQL Server 2012 및 2014의 최신 패치 수준으로 Azure에 대 한 합니다.
* **SQL 기능 지원**: 대부분의 SQL Server 기능이 Microsoft Azure Virtual Machines에서 지원되지만 몇 가지 예외가 있습니다. **공유 디스크를 사용하는 SQL Server 장애 조치(failover) 클러스터링은 지원되지 않습니다**.  데이터베이스 미러링, AlwaysOn 가용성 그룹, 복제, 로그 전달 및 Service Broker와 같은 분산 기술은 단일 Azure 지역 내에서 지원됩니다. SQL Server AlwaysOn은 여기(<https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>)에 설명된 대로 다른 Azure 지역 간 지원됩니다.  검토 hello [지원 정책](https://support.microsoft.com/kb/956893) 내용을 확인 합니다. Toodeploy AlwaysOn 구성에 표시 방법의 예로 [이] [ virtual-machines-workload-template-sql-alwayson] 문서. 또한 hello 문서화 하는 모범 사례를 확인해 [여기][virtual-machines-sql-server-infrastructure-services] 
* **SQL 성능**: 확신 Microsoft Azure 호스트 된 가상 컴퓨터 비교 tooother 공용 클라우드 가상화 서비스 하지만 개별 결과에 매우 잘 수행 다를 수 있습니다. [이 문서][virtual-machines-sql-server-performance-best-practices]를 참조하세요.
* **이미지를 사용 하 여 Azure 마켓플레이스의**: hello 가장 빠른 방법은 toodeploy 새 Microsoft Azure VM은 toouse hello Azure Marketplace에서에서 이미지입니다. SQL Server를 포함 하는 hello Azure Marketplace에서에서 이미지 있습니다. SQL Server 이미 설치 되어 있는 hello 이미지는 SAP NetWeaver 응용 프로그램에 대 한 즉시 사용할 수 없습니다. hello 이유는 이러한 이미지 및 SAP NetWeaver 시스템에 필요한 hello 데이터 정렬 하지 내 hello 기본 SQL Server 데이터 정렬에 설치 되며입니다. toouse 이러한 이미지를 주문 하 장에서 설명 하는 hello 단계 확인 [hello Microsoft Azure Marketplace에서 SQL Server 이미지를 사용 하 여][dbms-guide-5.6]합니다. 
* 자세한 내용은 [가격 책정 정보](https://azure.microsoft.com/pricing/) 를 확인하세요. hello [SQL Server 2012 라이선스 가이드](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) 및 [SQL Server 2014 라이선스 가이드](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) 중요 한 리소스 수도 있습니다.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Azure VM의 SAP 관련 SQL Server 설치에 대한 SQL Server 구성 지침
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>SAP 관련 SQL Server 배포용 VM/VHD 구조에 대한 권장 사항
Hello 일반적인 설명에 따라 SQL Server 실행 파일을 찾을, hello VM의 OS 디스크의 hello 시스템 드라이브에 설치 (c: 드라이브\)합니다.  일반적으로 대부분의 hello SQL Server 시스템 데이터베이스는 SAP NetWeaver 작업에 의해 높은 수준에서 사용 되지 않습니다. 따라서 hello 시스템 데이터베이스 (master, msdb 및 model) SQL Server의 hello C:\ 드라이브에 남아 있을 수 있습니다. 예외일 수 tempdb hello 경우 일부 SAP ERP 및 모든 BW 작업의 더 큰 데이터 볼륨 또는 hello에 맞출 수 없는 I/O 작업 볼륨이 필요할 수 있는 원본 VM입니다. 이러한 시스템에 대 한 단계를 수행 하는 hello는 수행 해야 합니다.

* Hello 주 tempdb 데이터 파일 toohello 이동 hello SAP 데이터베이스의 hello 주 데이터 파일과 같은 논리 드라이브입니다.
* Hello SAP 사용자 데이터베이스의 데이터 파일을 포함 하는 다른 논리 드라이브의 hello tooeach 하는 추가 tempdb 데이터 파일을 추가 합니다.
* Hello tempdb 로그 파일 toohello, 포함 된 논리 드라이브 hello 사용자 데이터베이스 로그 파일을 추가 합니다.
* **로컬 Ssd를 사용 하 여 사용 하는 VM 유형에** hello 계산 노드 tempdb 데이터 및 로그 파일 hello D:\ 드라이브에 저장할 수 있습니다. 그럼에도 불구 하 고는 것이 권장 toouse tempdb 데이터 파일이 여러 개 있습니다. D:\ 드라이브 볼륨을 다른 주의 기반 hello VM 유형으로 해야 합니다.

이러한 구성은 tempdb tooconsume hello 시스템 드라이브는 수 tooprovide 보다 더 많은 공간을 사용 합니다. 순서 toodetermine hello 적절 한 tempdb 크기에서 온-프레미스를 실행 중인 기존 시스템에서 hello tempdb 크기를 확인할 수 하나. 또한 이러한 구성을 hello 시스템 드라이브로 제공할 수 없는 tempdb에 대 한 IOPS 값을 사용 합니다. 다시 온-프레미스를 실행 중인 시스템 toosee tempdb에서 예상한 하는 hello IOPS 값을 파생 시킬 수 있습니다를 tempdb에 대 한 사용된 toomonitor I/O 작업 수 있습니다.

VM 구성, SAP 데이터베이스와 SQL Server를 실행 하 고 hello D:\ 드라이브에 tempdb 데이터 및 tempdb 로그 파일 위치 같습니다.

![SAP용 Azure IaaS VM의 참조 구성][dbms-guide-figure-300]

해당 hello D:\ 드라이브에 hello VM 유형에 종속 다양 한 크기에 주의 합니다. Tempdb의 hello 크기 요구 사항을에 종속 될 수도 있습니다 강제 toopair tempdb 데이터 및 hello로 로그 파일 SAP 데이터베이스 데이터 및 로그 파일 D:\ 드라이브를 너무 작은 경우에 합니다.

#### <a name="formatting-hello-disks"></a>Hello 디스크 서식 지정
SQL Server hello SQL Server 데이터 및 로그를 포함 하는 디스크에 대 한 NTFS 블록 크기에 대 한 파일 64k 있어야 합니다. 필요 tooformat hello D:\ 드라이브 있습니다. 이 드라이브는 미리 포맷되어 있습니다.

Hello 복원 작업이 나 데이터베이스 생성 초기화 하지 hello 데이터 파일의 hello 파일 hello 콘텐츠 비우기를 통해, 있어야 하는지 순서 toomake hello 사용자 컨텍스트 hello SQL Server 서비스 실행 되 고 있는지에 특정 권한을 있습니다. 일반적으로 hello Windows 관리자 그룹의 사용자가 이러한 권한이 있습니다. Windows 관리자가 아닌 사용자의 hello 사용자 컨텍스트에서 hello SQL Server 서비스를 실행 하면 해당 사용자 hello '볼륨 유지 관리 작업을 수행' 사용자 권한을 tooassign 할 수 있습니다.  이 Microsoft 기술 자료 문서 hello 세부 사항을 볼: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>데이터베이스 압축의 영향
I/O 대역폭이 제한 요인으로 작용할 수 있는 구성에서를 IOPS를 줄이는 모든 수단이 Azure와 같은 IaaS 시나리오에서 실행할 수 있는 toostretch hello 작업 부하를 이해할 수 있습니다. 따라서 수행 하지 않은 경우 SQL Server PAGE 압축을 적용 좋습니다 SAP와 Microsoft 모두 기존 SAP 데이터베이스 tooAzure 업로드 하기 전에.

tooAzure 업로드 하기 전에 hello 권장 tooperform 데이터베이스 압축은 두 가지 이유에서 제공 됩니다.

* 업로드 된 데이터 toobe hello 양을 낮습니다.
* hello hello 압축 실행 기간 동안 더 많은 Cpu 또는 I/O 대역폭이 더 높거나 이하의 I/O 대기 시간 온-프레미스 보다 강력한 하드웨어 사용할 수 있다고 가정 하면 짧습니다.
* 데이터베이스 크기가 작은 디스크 할당에 대 한 tooless 비용이 발생할 수 있습니다.

데이터베이스 압축은 Azure 가상 컴퓨터에서도 온-프레미스에서와 마찬가지로 잘 작동합니다. 방법에 대 한 자세한 내용은 여기 toocompress 기존 SAP SQL Server 데이터베이스를 선택: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blob-storage"></a>SQL Server 2014 - Azure Blob Storage에 데이터베이스 파일 직접 저장
SQL Server 2014 vhd 주위에 ' 래퍼' hello 없이 Azure Blob 저장소에서 직접 hello 가능성 toostore 데이터베이스 파일을 엽니다. 특히 표준 Azure 저장소 서비스 또는 더 작은 VM 형식을 사용 하는이 통해 시나리오 탑재 된 toosome 더 작은 VM 유형이 될 수 있는 디스크 수가 제한에 의해 적용는 IOPS의 hello 제한을 해결할 수 있습니다. 이 방법은 사용자 데이터베이스에는 적용되지만 SQL Server의 시스템 데이터베이스에는 사용할 수 없습니다. SQL Server의 데이터 및 로그 파일에도 사용할 수 있습니다. SAP SQL Server 데이터베이스 대신 이러한 방식으로 toodeploy 원하는 경우 hello 다음 염두에서에 둬야 '묶어서' Vhd에:

* 사용 된 저장소 계정 요구 toobe hello hello 사용 되는 toodeploy hello SQL Server VM에서 실행 되는 것 처럼 동일한 Azure 지역 hello 합니다.
* 배포에도이 방법에 대 한 고려 사항 앞에 나열 된 Vhd의 hello 분포에 대 한 다른 Azure 저장소 계정을 통해 적용 됩니다. 의미 hello hello 제한의 hello Azure 저장소 계정에 대해 I/O 작업 수입니다.

[comment]: <> (MSSedusch TODO 하지만 저장소 대역폭이 아닌 네트워크 대역폭을 사용하지 않나요?)

이 유형의 배포에 대한 세부 정보는 다음에 나열되어 있습니다. <https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure>

여기에 설명 되어 있는 최소 SQL Server 2014 toohave 패치 릴리스 순서 toostore SQL Server 데이터 파일에 Azure 프리미엄 저장소에서 직접 필요한: <https://support.microsoft.com/kb/3063054>합니다. 표준 저장소를 Azure에 SQL Server 데이터 파일을 저장할 hello 릴리스 버전의 SQL Server 2014와 작동 합니다. 그러나 hello 매우 동일한 패치 포함 다른 일련의 수정 하는 SQL Server 데이터 파일 및 백업에 대 한 Azure Blob 저장소의 hello 직접 사용 안정적 수 있습니다. 따라서 일반적으로 이러한 패치를 사용하는 것이 좋습니다.

### <a name="sql-server-2014-buffer-pool-extension"></a>SQL Server 2014 버퍼 풀 확장
SQL Server 2014에는 버퍼 풀 확장이라는 새로운 기능이 도입되었습니다. 이 기능은 로컬 Ssd 서버 또는 VM에서 지 원하는 두 번째 수준 캐시를 사용 하 여 메모리에 유지 되는 SQL Server의 hello 버퍼 풀을 확장 합니다. 그러면 tookeep '메모리'에서 데이터의 작업 집합이 있습니다. 비교 tooaccessing Azure 표준 저장소 hello 액세스의 Azure VM의 로컬 Ssd에 저장 되어 있는 hello 버퍼 풀 확장 hello로 여러 가지 요소 들이 더 빠릅니다.  따라서 뛰어난 IOPS 및 처리량이 있는 hello VM 유형의 hello 로컬 D:\ 드라이브를 활용 하는 매우 합리적인 방법이 tooreduce hello IOPS는 Azure 저장소에 대해 로드 및 쿼리 응답 시간을 크게 향상 될 수 있습니다. 이 이점은 Premium Storage를 사용하지 않는 경우에 특히 적용됩니다. 프리미엄 저장소 및 hello 계산 노드에 대해 프리미엄 Azure 읽기 캐시 hello hello 사용의 경우 데이터 파일에 대 한 권장 사항에 따라 큰 차이가 없는 예상 됩니다. (SQL Server 버퍼 풀 확장 및 프리미엄 저장소 읽기 캐시) 모두 캐시 hello hello 계산 노드의 로컬 디스크에 사용 하는 것이 위해서입니다.
이 기능에 대한 자세한 내용은 다음 설명서를 확인하세요. <https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension> 

### <a name="backuprecovery-considerations-for-sql-server"></a>SQL Server에 대한 백업/복구 고려 사항
Azure에 SQL Server를 배포하는 경우 백업 방법을 검토해야 합니다. Hello 시스템이 생산적인 시스템이 아닌 경우에 SQL Server에서 호스트 되는 hello SAP 데이터베이스를 백업 해야 주기적으로 합니다. Azure 저장소에 백업을 중요성이 존중 toocompensating 저장소 충돌에에서 세 개의 이미지를 유지 되므로 합니다. hello 우선 순위 적절 한 백업 및 복구 계획을 유지 관리 하는 지점 시간 복구 기능에서을 제공 하 여 논리적/수동 오류 보완할 수 있습니다 더 합니다. Hello 목표 tooeither 백업을 toorestore hello 데이터베이스 사용 다시 이므로 tooa 특정 지점에서 Azure tooseed 시간 또는 toouse hello 백업에 다른 시스템 hello 기존 데이터베이스를 복사 하 여 합니다. 예를 들어으로 전환할 수 있습니다의 hello는 2 계층 SAP 구성 tooa 3 계층 시스템 설정에서 동일한 시스템 백업을 복원 하 여 합니다.

세 가지 방법으로 toobackup SQL Server tooAzure 저장소 가지가 있습니다.

1. SQL Server 2012 CU4 및 더 높은 수 기본적으로 백업 데이터베이스 tooa URL입니다. Hello 블로그가 내용은 [백업/복원 향상-5 부-SQL Server 2014의에서 새로운 기능](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx)합니다. [SQL Server 2012 SP1 CU4 이상][dbms-guide-5.5.1] 챕터를 참조하세요.
2. SQL Server 릴리스 이전 tooSQL 2012 CU4 리디렉션 기능 toobackup tooa VHD를 사용 하 고 기본적으로 hello 쓰기 스트림을 구성 된 Azure 저장소 위치 추구할 수 있습니다. [SQL Server 2012 SP1 CU3 및 이전 버전][dbms-guide-5.5.2] 챕터를 참조하세요.
3. hello 마지막 방법은 tooperform 디스크 장치에 기존 SQL Server 백업 toodisk 명령입니다. 온-프레미스 배포 패턴과 동일 toohello 이므로이 문서에 자세히 설명 하지 않습니다.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 SP1 CU4 이상
이 기능은 toodirectly 백업 tooAzure BLOB 저장소가 있습니다. 이 방법에서는 없이 tooother 디스크, 디스크 및 IOPS 용량을 사용 하는 백업 해야 합니다. hello 아이디어는 기본적으로이:

 ![SQL Server 2012 백업 tooMicrosoft Azure 저장소 BLOB을 사용 하 여][dbms-guide-figure-400]

이 경우이 hello 장점은 toospend 디스크 toostore SQL Server 백업의에 필요 하지 않습니다 하나입니다. 따라서 더 적은 디스크 할당 및 디스크 IOPS를 사용 하 여 데이터 및 로그 파일에 대 한 수의 전체 대역폭 hello 합니다. Hello 백업의 최대 크기는 1TB 제한 tooa 최대가 문서의 '제한' hello 섹션에 설명 된 대로: <https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url#limitations>합니다. SQL Server 백업 압축을 사용 했는데도 hello 백업 크기의 크기가 1TB를 초과 하면, hello 장에서 설명 하는 기능 [SQL Server 2012 SP1 CU3 및 이전 릴리스에] [ dbms-guide-5.5.2] 이 문서에 필요 toobe 사용 합니다.

[관련 설명서](https://docs.microsoft.com/sql/relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure) hello 백업이 Azure BLOB 저장소에서 직접 toorestore 하지 권장 hello 복원의 Azure Blob 저장소에 대 한 백업에서 데이터베이스를 설명 하는 > 25GB입니다. 이 문서의 hello 권장은 단순히에 따라 성능 고려 사항 toofunctional 제한 하지 인해 합니다. 따라서 상황별로 서로 다른 조건이 적용될 수 있습니다.

이러한 형식의 백업 설정 및 활용 방법에 대한 설명서는 [이](https://docs.microsoft.com/sql/relational-databases/tutorial-use-azure-blob-storage-service-with-sql-server-2016) 자습서에서 확인할 수 있습니다.

Hello 일련의 단계의 예를 읽을 수 [여기](https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url)합니다.

백업을 자동화은 가장 높은 중요도 toomake 각 백업에 대 한 hello Blob 다르게 명명 된 있는지 합니다. 덮어씁니다 그렇지 않은 경우 및 hello 복원 체인이 손상 되었습니다.

Hello 세 가지 유형의 백업 간에 가지 toomix 하지 순서에서 권장 toocreate 백업에 사용 된 hello 저장소 계정 아래로 다른 컨테이너입니다. hello 컨테이너 수 vm만 또는 VM 및 백업 유형입니다. hello 스키마 같을 수 있습니다.

 ![별도 저장소 계정에서 컨테이너를 다른 SQL Server 2012 백업 tooMicrosoft – Azure 저장소 BLOB을 사용 하 여][dbms-guide-figure-500]

동일한 저장소 계정 위치 hello hello에 백업이 수행 되지 않습니다 hello 위의 hello 예제 Vm 배포 됩니다. 새 저장소 계정을 특히 hello 백업에 대 한 것입니다. Hello 저장소 계정 내에서 백업 및 hello VM 이름 hello 형식의 매트릭스를 사용 하 여 만든 다른 컨테이너 있을 것입니다. 이러한 구분 쉽게 tooadministrate hello 백업 hello 사용 하면 여러 Vm입니다.

hello 백업을 직접 쓰면 hello Blob toohello hello 데이터 디스크는 VM의 수를 추가 됩니다. 따라서 hello 최대 데이터 디스크 hello 데이터에 대 한 hello 특정 VM SKU에 탑재을 최대화 하 하나 및 트랜잭션 로그 파일 및 저장소 컨테이너에 대해 백업 실행 합니다. 

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 SP1 CU3 및 이전 버전
hello Azure 저장소에 직접 백업 tooachieve 순서에서에서 수행 해야 하는 첫 번째 단계 것 너무 연결 되어 있는 toodownload hello msi[이](https://www.microsoft.com/download/details.aspx?id=40740) KBA 문서.

Hello x64 설치 파일 및 hello 설명서를 다운로드 합니다. 호출 프로그램을 설치 하는 hello 파일: 'Microsoft SQL Server Backup tooMicrosoft Azure 도구'. 철저 하 게 hello 제품의 hello 설명서를 확인 합니다.  hello 도구는 기본적으로 hello 방식으로 다음에서 작동 합니다.

* SQL Server 쪽 hello에서 hello SQL Server 백업에 대 한 디스크 위치가 정의 됩니다 (이에 hello D:\ 드라이브를 사용 하지 않습니다).
* hello 도구 다른 유형의 백업 toodifferent Azure 저장소 컨테이너를 사용 하는 toodirect 될 수 있는 toodefine 규칙이 있습니다.
* Hello 규칙을 저장 되 면 hello 도구 hello Vhd/디스크 toohello 이전에 정의 된 Azure 저장소 위치의의 hello 백업 tooone의 hello 쓰기 스트림을 리디렉션합니다.
* hello 도구 몇 KB 크기의 작은 스텁 파일에서 전송 hello hello SQL Server에 대해 정의 된 VHD/디스크에 백업 됩니다. **Azure 저장소에서 다시 필요한 toorestore 이므로이 파일 hello 저장소 위치에 두어야 합니다.**
  * Microsoft Azure 저장소를 통해 hello 스텁 파일을 복구할 수 있습니다 (예: hello 스텁 파일을 포함 하는 hello 저장소 미디어의 손실) 통해 hello 스텁 파일을 잃어버린 hello tooa Microsoft Azure 저장소 계정의 백업 옵션을 선택한 경우 배치 된 hello 저장소 컨테이너에서 다운로드 합니다. 그런 다음 hello 스텁 파일 hello 도구는 구성 된 toodetect 및 업로드 toohello hello 로컬 컴퓨터에서 폴더에 두어야 hello 사용 하 여 동일한 컨테이너 hello 원래 규칙 암호화가 사용 된 경우 동일한 암호화 암호가 합니다. 

이 hello 스키마 보다 최신 버전의 SQL Server에 대해 위에서 설명한 대로에 배치할 수 직접 주소는 Azure 저장소 위치를 허용 하지 않는 SQL Server 릴리스에 대해서도 의미 합니다.

이 방법은 Azure Storage에 대해 기본적으로 백업을 지원하는 최신 SQL Server 버전에서는 사용하지 않아야 합니다. Azure에 hello 네이티브 백업 제한인 Azure에 기본 백업 실행을 차단 하는 예외입니다.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>다른 가능성 toobackup SQL Server 데이터베이스
다른 가능성 toobackup 데이터베이스 tooattach 추가 데이터 디스크 tooa에서 toostore 백업을 사용 하는 VM입니다. 이 경우 toomake hello 디스크 전체 실행 하지 않는 있는지 해야 합니다. 해당 되는 hello 경우 toounmount hello 디스크 해야 파일과 하므로 toospeak '보관' 새 빈 디스크를 바꿉니다. 해당 경로의 아래로 이동 하려는 경우 tookeep hello hello 데이터베이스 파일과 함께 Vhd hello 하에서에서 별도 Azure 저장소 계정에 이러한 Vhd입니다.

두 번째 가능성 toouse 연결 하면 여러 디스크를 가질 수 있는 대규모 VM 32VHDs와 D14 예입니다. 저장소 공간 toobuild 하는 공유를 작성할 수 있는 유연한 환경을 적합 한 다음 백업 대상으로 다른 DBMS 서버 hello 사용 합니다.

몇 가지 모범 사례가 [여기](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) 에 설명되어 있습니다. 

#### <a name="performance-considerations-for-backupsrestores"></a>백업/복원에 대한 성능 고려 사항
완전 배포 에서처럼 백업/복원 성능은 동시에 읽을 수 있는 볼륨 수 및 이러한 볼륨의 어떤 hello 출력 수에 따라 달라 집니다. 또한 hello 백업 압축을 통해 CPU 사용률 tooeight CPU 스레드를 방금 된 Vm에서 중요 한 역할을 재생 수 있습니다. 따라서 다음을 가정할 수 있습니다.

* hello 디스크 hello 수를 적게 사용 되지 않는 toostore hello 데이터 파일, hello 읽기에서 전반적인 처리량을 더 작은 hello 합니다.
* 더 작은 hello hello VM의에서 CPU 스레드 수가 hello, 백업 압축의 심각한 hello 영향 hello 합니다.
* 대상 (Blob, Vhd 또는 디스크) hello toowrite hello를 백업, 더 적은 hello 처리량 hello 합니다.
* hello 작은 hello VM 크기, hello 작은 hello 저장소 처리량 할당량 쓰기 및 Azure 저장소에서 읽기 Hello 백업이 Azure Blob에 직접 저장 되는 여부 또는 Azure Blob에 다시 저장 된 Vhd에 저장 여부는 독립적입니다.

Microsoft Azure 저장소 BLOB을 사용 하 여 최신 릴리스에서 hello 백업 대상으로, 각각의 특정 백업에 대 한 제한 된 toodesignating 하나만 URL 대상이 됩니다.

하지만 이전 릴리스에서 hello 'Microsoft SQL Server Backup tooMicrosoft Azure 도구'를 사용할 경우 파일 대상을 두 개 이상 정의할 수 있습니다. 둘 이상의 대상을 사용 하 여 hello 백업을 확장할 수 있고 hello hello 백업 처리량이 더 높습니다. 따라서 특성도 hello Azure 저장소 계정에서 여러 파일에 있습니다. 이 테스트에서는 어떤 hello 백업 확장으로 얻을 수 hello 처리량을 분명히 얻을 수는 여러 파일 대상을 사용 하 여 이상에서 구현 된 SQL Server 2012 SP1 CU4에 있습니다. 하면 수도 의해 차단 되지 않는지 hello 기본 백업 에서처럼 1TB 제한 hello Azure에 있습니다.

그러나 염두에서에 둬야, hello 처리량도 hello hello hello 백업에 사용할 Azure 저장소 계정 위치에 따라 달라 집니다. 관념은 toolocate hello 저장소 계정에서 실행 중인 Vm hello와 다른 지역에 수도 있습니다. 예를 들어 hello VM 구성은 서 부 유럽에서 실행 하는 hello 북부 유럽의 마련할 tooback를 사용 하는 저장소 계정을 저장 합니다. 확실히 hello 백업 처리량에 영향을 주 이며 희박 toogenerate 150 m B/초의 처리량 toobe hello 대상 저장소와 hello Vm hello에서 실행 중인 경우에 가능 하지만 보이기 어려워 동일한 지역의 데이터 센터입니다.

#### <a name="managing-backup-blobs"></a>백업 BLOB 관리
요구 사항 toomanage hello 백업을 직접 있습니다. 많은 blob 자주 트랜잭션 로그 백업을 실행 하 여 만들어졌는지 hello expectation 이므로 이러한 blob 관리 쉽게 수 과부하를 일으킬 hello Azure 포털입니다. Azure 저장소 탐색기는 것이 좋습니다 tooleverage 쉽습니다. 몇 가지 유용한 탐색기, toomanage Azure 저장소 계정 수 있는

* Azure SDK가 설치되어 있는 Microsoft Visual Studio(<https://azure.microsoft.com/downloads/>)
* Microsoft Azure Storage 탐색기(<https://azure.microsoft.com/downloads/>)
* 타사 도구

에 대 한 백업 및 Azure에서 SAP 자세한 내용은 참조 너무[SAP 백업 가이드 hello](sap-hana-backup-guide.md) 자세한 정보에 대 한 합니다.

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>Microsoft Azure Marketplace hello에서 SQL Server 이미지를 사용 하 여
Microsoft은 Azure 마켓플레이스 이미 버전의 SQL Server를 포함 하는 hello에 Vm을 제공 합니다. SQL Server 및 Windows 용 라이선스가 필요한 SAP 고객,이 이미 설치 된 SQL Server Vm 구성 함으로써 라이선스에 대 한는 영업 기회 toobasically 커버 hello 요구 될 수 있습니다. SAP에 대 한 이러한 이미지 순서 toouse에 hello 고려 사항에 따라 필요 toobe 수행 합니다.

* hello SQL Server 정품 버전에만 ' Windows 전용 ' VM Azure 마켓플레이스의 배포 보다 비용이 더 많이 획득 합니다. 이러한 문서 toocompare 가격 참조: <https://azure.microsoft.com/pricing/details/virtual-machines/windows/> 및 <https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-enterprise/>합니다. 
* SQL Server 2012처럼 SAP에서 지원하는 SQL Server 릴리스만 사용할 수 있습니다.
* hello Azure Marketplace에서에서 제공 하는 hello Vm에 설치 된 hello SQL Server 인스턴스의 데이터 정렬이 hello hello 데이터 정렬의 SAP NetWeaver 필요 hello SQL Server 인스턴스 toorun 않습니다. Hello 지시 hello 섹션 다음에 사항이 있는 hello 데이터 정렬을 변경할 수 있습니다.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Hello는 Microsoft Windows/SQL Server VM의 SQL Server 데이터 정렬 변경
Hello SQL Server 이미지 hello Azure Marketplace에서에서 SAP NetWeaver 응용 프로그램에서 필요한 toouse hello 데이터 정렬 설정 되지 않는 이후 toobe hello 배포 후 즉시 변경 해야 합니다. SQL Server 2012에 대 한 hello로 수행할 수 있습니다 다음 단계는 즉시 hello VM가 배포 되 고 관리자가 수 toolog hello에 배포 된 VM:

* '관리자'로 Windows 명령 창을 엽니다.
* Hello 디렉터리 tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012를 변경 합니다.
* Hello 명령을 실행: /QUIET Setup.exe /ACTION = REBUILDDATABASE /INSTANCENAME = MSSQLSERVER /SQLSYSADMINACCOUNTS =`<local_admin_account_name`> /SQLCOLLATION SQL_Latin1_General_Cp850_BIN2 =   
  * `<local_admin_account_name`> hello 갤러리를 통해 처음으로 hello에 대 한 hello VM을 배포할 때 hello 관리자 계정으로 정의 된 hello 계정입니다.

hello 프로세스 몇 분만 사용 해야 합니다. 순서 toomake 있는지에서 hello 단계 hello 올바른 결과 함께 결국 여부 hello 다음 단계를 수행 합니다.

* SQL Server Management Studio를 엽니다.
* 쿼리 창을 엽니다.
* Hello SQL Server 마스터 데이터베이스에서 sp_helpsort 명령을 hello를 실행 합니다.

hello 원하는 결과 같습니다.

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

이것이 hello 결과 SAP 배포를 중지 하 고 hello setup 명령은 작동 하지 않는 이유 예상 대로 조사 합니다. 다른 SQL Server 코드 페이지를 사용 하 여 SQL Server 인스턴스에 SAP NetWeaver 응용 프로그램 배포 hello 위에 언급 된 것 보다는 **하지** 지원 합니다.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>Azure의 SAP용 SQL Server 고가용성
이 백서의 앞에서 설명 했 듯이 hello 가장 오래 된 SQL Server 고가용성 기능의 hello 사용 하는데 필요한 가능성 toocreate 공유 저장소 없이 있습니다. 이 기능에는 장애 조치 클러스터 WSFC (Windows Server) hello 사용자 데이터베이스 (및 결국 tempdb)에 대 한 공유 디스크를 사용 하 여 두 개 이상의 SQL Server 인스턴스를 설치 합니다. 또한 SAP에서 지원 되는 hello 오랜 시간이 표준 고가용성 방법입니다. Azure에서는 공유 저장소를 지원하지 않으므로 공유 디스크 클러스터 구성의 SQL Server 고가용성 구성을 인식할 수 없습니다. 그러나 여러 가지 고가용성 방법은 될 수도 및 hello 다음 섹션에서에서 설명 합니다.

#### <a name="sql-server-log-shipping"></a>SQL Server 로그 전달
고가용성 (HA)의 hello 메서드 중 하나는 SQL Server 로그 전달 합니다. Hello HA 구성에 참여 하는 hello Vm가 이름 확인에 관한 작업, 아무런 문제가 및 Azure의 hello 설정은 온-프레미스를 수행 하는 모든 설치에서와 동일 합니다. IP 확인만 toorely는 권장 되지 않습니다. 로그 전달 및 로그 전달 관련 원칙 hello에 대 한 예정 toosetting, 사용이 설명서를 확인 합니다.

<https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server>

순서 tooreally에서 모든 가용성을 높이기 위해, 한 toodeploy hello Vm은 내에서 이러한는 로그 전달 구성 toobe 내 hello 동일한 Azure 가용성 집합에 있어야 합니다.

#### <a name="database-mirroring"></a>데이터베이스 미러링
SAP에서 지 원하는 데이터베이스 미러링 (SAP Note 참조 [965908]) hello SAP 연결 문자열에에서 장애 조치 파트너 정의에 의존 합니다. Hello 크로스-프레미스의 경우에 대 한 가정 해당 hello 두 대의 Vm은 hello에 동일한 도메인 및 해당 hello 사용자 컨텍스트 hello 두 SQL Server 인스턴스가 실행 되 고, 도메인 사용자와 관련 된 hello 두 SQL Server 인스턴스에서에 충분 한 권한이 있어야 합니다. 따라서 Azure에서 데이터베이스 미러링의 hello 설치 일반적인 온-프레미스 설치/구성 간에 다르지 않습니다.

클라우드 전용 배포의 hello 가장 쉬운 방법은 toohave 대로 다른 도메인 설정 Azure toohave에서 해당 DBMS Vm (및 이상적인 전용된 SAP Vm) 한 도메인 내 합니다.

인증서 hello 데이터베이스 미러링 끝점을 여기에 설명 된 대로에 사용할 수 도메인 수 없는 경우: <https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql>

Azure에서 데이터베이스 미러링을 자습서 tooset 여기에서 찾을 수 있습니다: <https://docs.microsoft.com/sql/database-engine/database-mirroring/database-mirroring-sql-server> 

#### <a name="sql-server-always-on"></a>SQL Server Always On
Always On SAP 온-프레미스에 대 한 지원 됩니다 (SAP Note 참조 [1772688]), 지원된 toobe Azure에서 SAP와 함께에서 사용 되는 것이 합니다. 하나는 항상에서 Windows Server 장애 조치 클러스터 (WSFC) 구성을 다른 Vm 간에 만들 수 없음을 hello 팩트 Azure의 디스크 수 toocreate 공유 되지 않는다는 것은 아닙니다. 하지 않았는지 hello 가능성 toouse 공유 디스크를 쿼럼으로 hello 클러스터 구성에만 의미 합니다. 따라서 Azure에서는 항상 WSFC 구성을 빌드할 수 있으며 단순히 공유 디스크를 활용 하는 hello 쿼럼 유형을 선택 하지 수도 있습니다. hello Azure 환경 해당 Vm에 배포 된 Vm 이름으로 hello 및 hello Vm hello에 있어야 합니다. 해결 해야 동일한 도메인입니다. 이는 Azure 전용 및 프레미스 간 배포에만 적용됩니다. SQL Server 가용성 그룹 수신기 (하지 Azure 가용성 집합 hello와 혼동된 toobe) hello 배포 특별 한 고려 사항이 가능한 그대로 toosimply AD/DNS 개체를 만들 Azure가이 시점에서 허용 하지 않는 이후 온-프레미스입니다. 따라서 일부 다른 설치 단계는 필요한 tooovercome hello Azure의 특정 동작입니다.

가용성 그룹 수신기를 사용하는 경우 몇 가지 고려 사항이 있습니다.

* 가용성 그룹 수신기를 사용 하는 것은 Windows Server 2012 이상 hello VM의 게스트 OS만 가능 합니다. Toomake이이 패치 적용 하는 Windows Server 2012에 대 한 필요한: <https://support.microsoft.com/kb/2854082> 
* Windows Server 2008 R2이이 패치 존재 하지 않는 필요 Always On에 대 한 toobe 레지스트리에 hello 동일 방식 hello 연결 문자열에 장애 조치 파트너 지정 하 여 데이터베이스 미러링 (수행 통해 SAP default.pfl 매개 변수 dbs/mss/서버 hello – SAP 메모를 참조 하십시오. [965908]).
* 가용성 그룹 수신기, hello 데이터베이스 Vm을 사용 하 여 연결 toobe 경우 tooa 부하 분산 장치는 전용입니다. 이름 확인 클라우드 전용 배포에는 SAP의 모든 Vm 필요 하거나 동일한 가상 네트워크를 hello 또는 hello etc\host 파일에는 SAP 응용 프로그램 계층 hello 유지 관리에서 필요한 시스템 (응용 프로그램 서버, DBMS 서버 및 (A) SCS 서버)에 주문 tooget hello의 VM 이름을 hello SQL Server Vm을 확인 합니다. Azure가 인 경우 두 Vm 부수적 종료에서에서 새 IP 주소를 할당 하는 순서 tooavoid에서 하나 해야 고정 IP 주소 할당 hello Always On 구성 (고정 IP 주소에서 설명 하는 정의에서 해당 Vm의 toohello 네트워크 인터페이스 [이] [ virtual-networks-reserved-private-ip] 문서)

[comment]: <> (이전 블로그)
[comment]: <> (<https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, <https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx>) 
* 최신 기능을 갖춘 Azure hello 클러스터 이름을 할당 하기 때문에 할당 된 hello 클러스터에 특별 IP 주소를 해야 하는 hello WSFC 클러스터 구성을 빌드할 때 필요한 특별 한 단계는 hello hello 노드 hello 클러스터와 동일한 IP 주소 에 생성 됩니다. 즉, 수동 단계를 수행된 하는 다른 IP 주소 toohello 클러스터 tooassign 이어야 합니다.
* hello 가용성 그룹 수신기는 toobe hello hello 가용성 그룹의 주 및 보조 복제본을 실행 하는 toohello Vm 할당 된 TCP/IP 끝점과 함께 Azure에서 만든 것입니다.
* 이러한 끝점은 Acl로 필요 toosecure 수 있습니다.

[comment]: <> (TODO 이전 블로그)
[comment]: <> (자세한 단계 hello 및 Azure에서 AlwaysOn 구성 설치의 필요성은 hello 자습서 사용할 수 있는 [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups] 해 보면 보는 가장)
[comment]: <> (AlwaysOn 설정 hello Azure 갤러리를 통해 미리 구성 된 < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (가용성 그룹 수신기 생성은 [이][virtual-machines-windows-classic-ps-sql-int-listener] 자습서에 잘 설명되어 있습니다.)
[comment]: <> (ACL을 사용한 네트워크 끝점 보호는 여기를 참조하세요.)
[comment]: <> (*    <https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx> )
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>) 

SQL Server Always On 가용성 그룹의 가능한 toodeploy이 서로 다른 Azure 지역 통해 합니다. 이 기능은 hello Azure VNet 대 Vnet 연결을 활용 하 여 ([자세히][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (TODO 이전 블로그)
[comment]: <> (이러한 시나리오에서는 SQL Server AlwaysOn 가용성 그룹의 hello 설치 여기에 설명 된: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx> 합니다.) 

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Azure의 SQL Server 고가용성 요약
상시 대기 이미지만 적은 이유 tooinsist 하나는 Azure 저장소의 hello 콘텐츠 보호 하는 hello 팩트를 제공입니다. 즉, 고가용성 시나리오 tooonly 비활성화 hello 으로부터 보호 합니다.

* Azure의 hello 서버 클러스터에 toomaintenance 또는 기타 이유로 인해 전체적으로 hello VM 사용 불가능
* Hello SQL Server 인스턴스의 소프트웨어 문제
* 데이터가 삭제되고 지정 시간 복구가 필요하여 수동 오류로부터 보호해야 하는 경우

일치 하는 기술 hello 세 번째 경우 수 작성 된 로그 전달 하는 반면 데이터베이스 미러링 또는 Always On hello 처음 두 가지 경우를 다룰 수 있습니다 주장할 수 있을 하나 찾습니다.

Toobalance 해야 Always On, 비교 tooDatabase의 더 복잡 한 설정을 hello 미러링와 Always On hello 이점이 있습니다. 이러한 이점은 다음과 같습니다.

* 읽기 가능한 보조 복제본
* 보조 복제본에서 백업
* 향상된 확장성
* 둘 이상의 보조 복제본

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Azure의 SAP용 SQL Server에 대한 일반적 요약
이 가이드에는 많은 권장 사항이 있으며 Azure 배포를 계획하기 전에 두 번 이상 읽는 것이 좋습니다. 일반적으로 하지만 될 있는지 toofollow hello Azure의 특정 지점에서 상위 10 개의 일반 DBMS:

[comment]: <> (2.3 더 높은 처리량이 필요한 경우 수행할 작업 하나 이상의 VHD는?)
1. Hello 최신 DBMS 릴리스, Azure의 hello를 가장 많은 이점을 있는 SQL Server 2014와 같은 사용 합니다. SQL Server를 포함 한 백업 릴리스는 Azure 저장소 hello 기능이 SQL Server 2012 SP1 CU4,입니다. 그러나 SAP와 함께에서 것이 좋습니다 이상 SQL Server 2014 SP1 c u 1 또는 SQL Server 2012 SP2 및 hello 최신 CU입니다.
2. Azure toobalance hello 데이터 파일 레이아웃과 Azure 제한 사항에서 SAP 시스템 지형을 프로그램을 신중 하 게 계획 합니다.
   * 너무 많은 디스크 필요는 없지만 충분 한 tooensure 필요한 IOPS에 도달할 수 있어야 합니다.
   * Managed Disks를 사용하지 않는 경우 IOPS는 Azure Storage 계정별로 제한되며, 해당 저장소 계정도 각 Azure 구독 내에서 제한됩니다([자세한 내용][azure-subscription-service-limits]). 
   * 처리량이 늘어나며 tooachieve 필요한 경우 디스크에 걸쳐만 스트라이프 합니다.
3. 소프트웨어를 설치 하지 않거나 또는 영구적이 고이 드라이브에는 Windows 컴퓨터를 다시 부팅 시 대로 hello D:\ 드라이브에 지 속성을 필요로 하는 파일을 배치 합니다.
4. Azure Standard Storage에 대해 디스크 캐싱을 사용하지 마세요.
5. Azure 지역에서 복제된 저장소 계정을 사용하지 마세요.  DBMS 워크로드에 대한 로컬 중복을 사용합니다.
6. DBMS 공급 업체의 HA/DR 솔루션 tooreplicate 데이터베이스 데이터를 사용 합니다.
7. 항상 이름 확인을 사용하고 IP 주소를 사용하지 마세요.
8. Hello 가장 높은 데이터베이스 압축을 사용 가능 합니다. SQL Server의 경우 페이지 압축입니다.
9. Hello Azure Marketplace에서에서 SQL Server 이미지를 사용 하 여 주의 해야 합니다. Hello 하나는 SQL Server를 사용 하면 SAP NetWeaver 시스템에 설치 하기 전에 hello 인스턴스 데이터 정렬을 변경 해야 합니다.
10. 설치 하 고에 설명 된 대로 Azure 용 SAP Host Monitoring hello 구성 [배포 가이드][deployment-guide]합니다.

## <a name="specifics-toosap-ase-on-windows"></a>Windows에서 ASE 비슷하므로 tooSAP
Microsoft Azure를 시작 하면 기존 SAP ASE 응용 프로그램 tooAzure 가상 컴퓨터를 쉽게 마이그레이션할 수 있습니다. 가상 컴퓨터에서 SAP ASE 이러한 응용 프로그램 tooMicrosoft Azure로 쉽게 마이그레이션하여 여 있습니다 tooreduce hello 총 소유 비용을의 배포, 관리 및 엔터프라이즈 너비 응용 프로그램의 유지 관리를 수 있습니다. SAP ASE Azure 가상 컴퓨터에서 사용 관리자와 개발자가 동일한 개발 및 관리 도구를 사용할 수 있는 온-프레미스 hello를 계속 사용할 수 있습니다.

Hello 여기에서 찾을 수 있는 Azure 가상 컴퓨터에 대 한 SLA는: <https://azure.microsoft.com/support/legal/sla/virtual-machines>

우리는 확신 Microsoft Azure 호스트 된 가상 컴퓨터 비교 tooother 공용 클라우드 가상화 서비스 하지만 개별 결과에 매우 잘 수행 다를 수 있습니다. SAP VM Sku 별도 SAP Note에서 제공 되는 서로 다른 SAP 인증 hello의 SAPS 숫자 크기 조정 [1928533]합니다.

문 및 Azure 저장소, SAP Vm 배포 또는 SAP 모니터링의 큰지에 toohello 사용의 권장 사항을 toodeployments SAP ASE의 SAP 응용 프로그램이 문서의 처음 네 개의 장 hello 전체에서 명시 된 대로 함께 적용 됩니다.

### <a name="sap-ase-version-support"></a>SAP ASE 버전 지원
SAP는 현재 SAP ASE 버전 16.0을 SAP Business Suite 제품과 함께 사용하도록 지원합니다. SAP Business Suite 제품은 통해서만 제공 함께 사용 하는 JDBC 및 ODBC 드라이버 toobe 또는 SAP ASE 서버에 대 한 모든 업데이트에서 SAP Service Marketplace hello: <https://support.sap.com/swdc>합니다.

설치 온-프레미스의 경우와 Sybase 웹 사이트에서 직접 hello SAP ASE 서버 또는 hello JDBC 및 ODBC 드라이버에 대 한 업데이트를 다운로드 하지 않습니다. 에 대 한 자세한 내용은 패치, SAP Business Suite 제품 온-프레미스로 사용 하기 위해 사용할 수 있는 및 Azure 가상 컴퓨터에서 SAP Note 다음 hello 참조:

* [1590719]
* [1973241]

Hello에서 SAP ASE에서 SAP Business Suite 실행에 대 한 일반 정보를 찾을 수 있습니다 [SCN](https://www.sap.com/community/topic/ase.html)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Azure VM의 SAP 관련 SAP ASE 설치에 대한 SAP ASE 구성 지침
#### <a name="structure-of-hello-sap-ase-deployment"></a>Hello SAP ASE 배포의 구조
Hello 일반적인 설명에 따라 SAP ASE 실행 파일을 찾을, hello VM의 OS 디스크의 hello 시스템 드라이브에 설치 (c: 드라이브\)합니다. 일반적으로 대부분의 hello SAP ASE 시스템과 도구 데이터베이스 하지 실제로에서 활용 됩니다 하드 SAP NetWeaver 작업 합니다. 따라서 시스템을 hello 및 도구 데이터베이스 (master, model, saptools sybmgmtdb, sybsystemdb)도 hello C:\ 드라이브에 남아 있을 수 있습니다. 

예외에는 모든 작업 테이블 및 일부 SAP ERP 및 모든 BW 작업의 경우 더 큰 데이터 볼륨 또는 원래 hello에 맞출 수 없는 I/O 작업 볼륨이 필요할 수 있습니다. 있는 SAP ASE에 의해 생성 된 임시 테이블을 포함 하는 hello 임시 데이터베이스 수 있습니다. VM의 OS 디스크 (c: 드라이브\)합니다.

SAPInst/SWPM의 버전 사용 tooinstall hello 시스템 hello에 따라, hello 데이터베이스 포함 될 수 있습니다.

* SAP ASE를 설치할 때 만들어지는 단일 SAP ASE tempdb
* SAP ASE 및 hello SAP 설치 루틴에서 만든 추가 saptempdb는 설치 하 여 생성 하는 SAP ASE tempdb
* SAP ASE 및 수동으로 만든 추가 tempdb는 설치 하 여 생성 하는 SAP ASE tempdb (SAP Note 예를 들어 다음 [1752266]) toomeet ERP/BW 특정 tempdb 요구 사항

특정 ERP 또는 모든 BW 작업의 경우 이렇게 하면, 큰지에 tooperformance에서 또한 이외의 C:\ 드라이브에 tempdb (SWPM 또는 수동으로)을 생성 하는 hello의 tookeep hello tempdb 장치 있습니다. 하나 toocreate 없는 추가 tempdb 있으면 좋습니다 (SAP Note [1752266]).

이러한 시스템 hello에 대 한 또한 tempdb를 생성 하는 hello에 대 한 다음 단계를 수행 해야 합니다.

* Hello 첫 번째 tempdb 장치 toohello 첫 번째 장치 hello SAP 데이터베이스의 이동
* Hello hello SAP 데이터베이스의 장치를 포함 된 Vhd의 tempdb 장치 tooeach 추가

이 구성을 사용 하면 tempdb tooeither hello 시스템 드라이브는 수 tooprovide 보다 더 많은 공간을 사용 합니다. 참조로 하나 온-프레미스를 실행 중인 기존 시스템에서 hello tempdb 장치 크기를 확인할 수 있습니다. 또는 이러한 구성 hello 시스템 드라이브로 제공할 수 없는 tempdb에 대 한 IOPS 값을 사용 합니다. 다시 온-프레미스를 실행 중인 시스템에는 tempdb에 대 한 사용된 toomonitor I/O 작업 수 있습니다.

Hello hello VM의 D:\ 드라이브에 저장 하는 모든 SAP ASE 장치 하면 안 됩니다. 또한 toohello tempdb hello tempdb에 보관 하는 hello 개체는 임시만 하는 경우에 마찬가지입니다.

#### <a name="impact-of-database-compression"></a>데이터베이스 압축의 영향
I/O 대역폭이 제한 요인으로 작용할 수 있는 구성에서를 IOPS를 줄이는 모든 수단이 Azure와 같은 IaaS 시나리오에서 실행할 수 있는 toostretch hello 작업 부하를 이해할 수 있습니다. 따라서 하는 것이 좋습니다 toomake SAP ASE 압축 기존 SAP 데이터베이스 tooAzure 업로드 하기 전에 사용 되도록 합니다.

구현 되지 않은 경우 tooAzure를 업로드 하기 전에 hello 권장 tooperform 압축 몇 가지 이유로에서 제공 됩니다.

* 데이터 업로드 toobe tooAzure hello 양을 낮습니다.
* hello hello 압축 실행 기간은 짧은 더 많은 Cpu 또는 I/O 대역폭이 더 높거나 이하의 I/O 대기 시간 온-프레미스 보다 강력한 하드웨어 사용할 수 있다고 가정 하면
* 데이터베이스 크기가 작은 디스크 할당에 대 한 tooless 비용이 발생할 수 있습니다.

데이터 및 LOB 압축은 Azure 가상 컴퓨터에서 호스트되는 VM에서도 온-프레미스에서와 마찬가지로 작동합니다. 에 대 한 자세한 내용은 toocheck 압축 이미 사용 중이면 기존 SAP ASE 데이터베이스에서 확인 하는 방법은 SAP Note [1750510]합니다.

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>DBACockpit toomonitor 데이터베이스 인스턴스를 사용 하 여
데이터베이스 플랫폼으로 SAP ASE를 사용 하는, SAP 시스템에 대 한 hello DBACockpit는 DBACockpit 트랜잭션에 포함 된 브라우저 창을 또는 Webdynpro로 액세스할 수 있습니다. 그러나 모니터링 하기 위한 모든 기능을 hello 되며 관리 hello 데이터베이스 hello DBACockpit의 hello Webdynpro 구현에서 사용할 수 있습니다.

으로 온-프레미스 시스템 몇 가지 단계가 필요 tooenable hello DBACockpit hello Webdynpro 구현에 의해 사용 되는 모든 SAP NetWeaver 기능 합니다. SAP Note를 따라 [1245200] tooenable hello webdynpros의 사용 및 생성 hello 필요한 것입니다. 지침 hello에 메모 위에 hello, http 및 https 연결에 사용 되는 hello 포트 toobe 함께 hello 인터넷 통신 관리자 (icm) 구성 합니다. http에 대 한 hello 기본 설정은 다음과 같습니다.

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
> 
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
> 
> 

및 DBACockpit 트랜잭션에서 생성 된 hello 링크 유사한 toothis 표시 됩니다.

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

에 따라와 hello Azure 가상 컴퓨터 호스팅 hello SAP 시스템 사이트를 통해 연결 하는 방법을 멀티 사이트 또는 express 경로 (크로스-프레미스 배포의 경우) 해야 toomake 있는지 해당 ICM 사용 확인 될 수 있는 정규화 된 호스트 이름 hello에 tooopen 시도 하 고 있는 컴퓨터에서 DBACockpit hello 합니다. SAP Note 참조 [773830] ICM 결정 하는 방법 toounderstand hello 프로필 매개 변수 및 매개 변수 icm/host_name_full 집합에 따라 정규화 된 호스트 이름을 명시적으로 필요한 경우.

온-프레미스와 Azure 간 크로스-프레미스 연결 없이 클라우드 전용 시나리오에서 hello VM을 배포한 경우 공용 IP 주소와는 domainlabel toodefine 필요 합니다. hello hello VM 아래의 hello 공용 DNS 이름 형식:

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
> 
> 

자세한 내용은 관련 toohello DNS 이름을 찾을 수 [여기][virtual-machines-azurerm-versus-azuresm]합니다.

설정을 hello SAP 프로필 매개 변수 icm/host_name_full toohello hello Azure VM hello 링크의 DNS 이름을 유사 하 게 나타날 수 있습니다.

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

이 경우에 필요 toomake 해야 합니다.

* Hello ICM으로 사용 되는 포트 toocommunicate hello TCP/IP에 대 한 Azure 포털에서에서 인바운드 규칙 toohello 네트워크 보안 그룹 추가
* ICM hello로 TCP/IP 사용 포트 toocommunicate hello에 대 한 인바운드 규칙 toohello Windows 방화벽 구성 추가

자동화 된 가져온 사용 가능한 모든 수정에 대 한 권장 tooperiodically hello 수정 컬렉션 SAP Note 적용 가능한 tooyour SAP 버전을 적용 합니다.

* [1558958]
* [1619967]
* [1882376]

SAP ASE에 대 한 DBA Cockpit에 대 한 자세한 내용은 SAP Note 다음 hello에 있습니다.

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>SAP ASE에 대한 백업/복구 고려 사항
Azure에 SAP ASE를 배포하는 경우 백업 방법을 검토해야 합니다. 경우에 hello 시스템 운영 중인 시스템이, SAP ASE에서 호스트 되는 hello SAP 데이터베이스를 백업 해야 주기적으로 합니다. Azure 저장소에 백업을 중요성이 존중 toocompensating 저장소 충돌에에서 세 개의 이미지를 유지 되므로 합니다. hello 적절 한 백업 및 복원 계획을 유지 관리에 대 한 주된 이유 때문입니다 지점 시간 복구 기능에서을 제공 하 여 논리적/수동 오류 보완할 수 있습니다. Hello 목표 tooeither 백업을 toorestore hello 데이터베이스 사용 다시 이므로 tooa 특정 지점에서 Azure tooseed 시간 또는 toouse hello 백업에 다른 시스템 hello 기존 데이터베이스를 복사 하 여 합니다. 예를 들어으로 전환할 수 있습니다의 hello는 2 계층 SAP 구성 tooa 3 계층 시스템 설정에서 동일한 시스템 백업을 복원 하 여 합니다.

Azure works에서 데이터베이스 백업 및 복원 hello 동일한 방식으로 온-프레미스를 수행 합니다. 다음 SAP Note를 참조하세요.

* [1588316]
* [1585981]

여기에는 덤프 구성 생성 및 백업 예약에 대한 자세한 내용이 나와 있습니다. 전략 및 구성할 수 요구 사항에 따라 데이터베이스 및 로그 toodisk hello 기존 디스크 중 하나에 덤프 하거나 hello 백업에 대 한 추가 디스크를 추가 합니다. 오류 발생 시 데이터 손실의 tooreduce hello 위험 toouse 데이터베이스 장치가 있는 디스크를 권장 합니다.

데이터 및 LOB 압축 SAP ASE 외에도 백업 압축을 제공합니다. 복사 하는 hello 데이터베이스 및 로그를 사용 하 여 공간을 덜 toooccupy toouse 백업 압축 것이 좋습니다. 자세한 내용은 SAP Note [1588316]을 참조하세요. 압축 hello 백업이 중요 tooreduce hello 양의 toodownload 백업 또는 hello tooon-프레미스 Azure 가상 컴퓨터에서에서 백업 덤프에 포함 된 Vhd를 계획 하는 경우에 전송할 데이터 toobe 이기도 합니다.

데이터베이스 또는 로그 덤프 대상으로 D:\ 드라이브를 사용하지 마세요.

#### <a name="performance-considerations-for-backupsrestores"></a>백업/복원에 대한 성능 고려 사항
완전 배포 에서처럼 백업/복원 성능은 동시에 읽을 수 있는 볼륨 수 및 이러한 볼륨의 어떤 hello 출력 수에 따라 달라 집니다. 또한 hello 백업 압축을 통해 CPU 사용률 tooeight CPU 스레드를 방금 된 Vm에서 중요 한 역할을 재생 수 있습니다. 따라서 다음을 가정할 수 있습니다.

* hello 사용 되는 디스크 toostore hello 수를 적게 데이터베이스 장치 hello, 더 작은 hello 전반적인 hello 읽기 처리량
* 더 작은 hello hello VM의에서 CPU 스레드 수가 hello, 백업 압축의 심각한 hello 영향 hello
* hello에 더 적은 toowrite hello 백업 대상 (디스크, Stripe 디렉터리), 더 적은 hello 처리량 hello

tooincrease hello 수가 대상 toowrite toothere 두 가지 옵션, 필요에 따라 사용 되 는/결합 될 수 있습니다.

* Hello 백업 대상 볼륨을 해당 스트라이프 볼륨에서 순서 tooimprove hello IOPS 처리량에 여러 탑재 된 디스크 스트라이프
* SAP ASE 수준에서 덤프 구성 만들기를 사용 하는 둘 이상의 대상 디렉터리 toowrite hello 덤프를

탑재된 여러 디스크에 볼륨을 스트라이프하는 방법은 이 가이드의 앞부분에서 설명했습니다. 여러 디렉터리를 사용 하 여 hello SAP ASE 덤프 구성에 대 한 자세한 내용은 hello에 사용 되는 toocreate hello 덤프 구성 인 저장 프로시저 sp_config_dump에 toohello 문서를 참조 하십시오. [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Azure VM을 사용한 재해 복구
#### <a name="data-replication-with-sap-sybase-replication-server"></a>SA Sybase Replication Server를 사용한 데이터 복제
Hello로 SAP Sybase 복제 서버 (SRS) SAP ASE 비동기적으로 웜 대기 솔루션 tootransfer 데이터베이스 트랜잭션 tooa 멀리 떨어진 위치를 제공합니다. 

hello 설치 되 고 SRS의 작동에도 온-프레미스와 마찬가지로 Azure 가상 컴퓨터 서비스에서 호스팅되는 VM에서 기능적으로 작동 합니다.

SAP Replication Server를 통한 ASE HADR은 향후 릴리스에 도입될 예정입니다. 이 기능은 곧 Microsoft Azure Platform에 대해 테스트되고 릴리스될 예정입니다.

## <a name="specifics-toosap-ase-on-linux"></a>Linux에서 비슷하므로 tooSAP ASE
Microsoft Azure를 시작 하면 기존 SAP ASE 응용 프로그램 tooAzure 가상 컴퓨터를 쉽게 마이그레이션할 수 있습니다. 가상 컴퓨터에서 SAP ASE 이러한 응용 프로그램 tooMicrosoft Azure로 쉽게 마이그레이션하여 여 있습니다 tooreduce hello 총 소유 비용을의 배포, 관리 및 엔터프라이즈 너비 응용 프로그램의 유지 관리를 수 있습니다. SAP ASE Azure 가상 컴퓨터에서 사용 관리자와 개발자가 동일한 개발 및 관리 도구를 사용할 수 있는 온-프레미스 hello를 계속 사용할 수 있습니다.

중요 한 tooknow hello 여기에서 찾을 수 있는 공식 Sla는 Azure Vm을 배포 하기 위한: <https://azure.microsoft.com/support/legal/sla>

SAP 크기 조정 정보 및 SAP 인증 VM SKU 목록은 SAP Note [1928533]을 참조하세요. Azure Virtual Machines에 대한 추가 SAP 크기 조정 문서는 <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> 및 <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>에서 찾을 수 있습니다.

문 및 Azure 저장소, SAP Vm 배포 또는 SAP 모니터링의 큰지에 toohello 사용의 권장 사항을 toodeployments SAP ASE의 SAP 응용 프로그램이 문서의 처음 네 개의 장 hello 전체에서 명시 된 대로 함께 적용 됩니다.

hello 다음 두 SAP Note에서 Linux 및 ASE ASE에 대 한 일반 정보에에서 포함 클라우드 hello:

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>SAP ASE 버전 지원
SAP는 현재 SAP ASE 버전 16.0을 SAP Business Suite 제품과 함께 사용하도록 지원합니다. SAP Business Suite 제품은 통해서만 제공 함께 사용 하는 JDBC 및 ODBC 드라이버 toobe 또는 SAP ASE 서버에 대 한 모든 업데이트에서 SAP Service Marketplace hello: <https://support.sap.com/swdc>합니다.

설치 온-프레미스의 경우와 Sybase 웹 사이트에서 직접 hello SAP ASE 서버 또는 hello JDBC 및 ODBC 드라이버에 대 한 업데이트를 다운로드 하지 않습니다. 에 대 한 자세한 내용은 패치, SAP Business Suite 제품 온-프레미스로 사용 하기 위해 사용할 수 있는 및 Azure 가상 컴퓨터에서 SAP Note 다음 hello 참조:

* [1590719]
* [1973241]

Hello에서 SAP ASE에서 SAP Business Suite 실행에 대 한 일반 정보를 찾을 수 있습니다 [SCN](https://www.sap.com/community/topic/ase.html)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Azure VM의 SAP 관련 SAP ASE 설치에 대한 SAP ASE 구성 지침
#### <a name="structure-of-hello-sap-ase-deployment"></a>Hello SAP ASE 배포의 구조
Hello 일반적인 설명에 따라 SAP ASE 해야 수 있는 파일 또는 실행 hello (/sybase) VM의 hello 루트 파일 시스템에 설치 됩니다. 일반적으로 대부분의 hello SAP ASE 시스템과 도구 데이터베이스 하지 실제로에서 활용 됩니다 하드 SAP NetWeaver 작업 합니다. 따라서 시스템을 hello 및 도구 데이터베이스 (master, model, saptools sybmgmtdb, sybsystemdb) hello 루트 파일 시스템에 남아 있을 수 있습니다. 

예외에는 모든 작업 테이블 및 일부 SAP ERP 및 모든 BW 작업의 경우 필요할 수 있습니다. 있습니다 더 큰 데이터 볼륨 또는 I/O 작업에서 원래 hello에 맞지 않는 볼륨 SAP ASE에 의해 생성 된 임시 테이블을 포함 하는 hello 임시 데이터베이스 수 있습니다. VM의 OS 디스크입니다.

SAPInst/SWPM의 버전 사용 tooinstall hello 시스템 hello에 따라, hello 데이터베이스 포함 될 수 있습니다.

* SAP ASE를 설치할 때 만들어지는 단일 SAP ASE tempdb
* SAP ASE 및 hello SAP 설치 루틴에서 만든 추가 saptempdb는 설치 하 여 생성 하는 SAP ASE tempdb
* SAP ASE 및 수동으로 만든 추가 tempdb는 설치 하 여 생성 하는 SAP ASE tempdb (SAP Note 예를 들어 다음 [1752266]) toomeet ERP/BW 특정 tempdb 요구 사항

특정 ERP 또는 모든 BW 작업의 경우 적합, 큰지에 tooperformance tookeep hello tempdb 장치는 단일 Azure 데이터 디스크 또는 Linux RAID로 나타낼 수 있는 별도 파일 시스템에서 만든 또한 hello tempdb (SWPM 또는 수동으로) 여러 Azure 데이터 디스크를 확장 합니다. 하나 toocreate 없는 추가 tempdb 있으면 좋습니다 (SAP Note [1752266]).

이러한 시스템 hello에 대 한 또한 tempdb를 생성 하는 hello에 대 한 다음 단계를 수행 해야 합니다.

* Hello 첫 번째 tempdb 디렉터리 toohello 첫 번째 파일 시스템의 hello SAP 데이터베이스를 이동 합니다.
* Tempdb 디렉터리 tooeach hello SAP 데이터베이스의 파일 시스템을 포함 하는 hello 디스크 추가

이 구성을 사용 하면 tempdb tooeither hello 시스템 드라이브는 수 tooprovide 보다 더 많은 공간을 사용 합니다. 참조로 하나 온-프레미스를 실행 중인 기존 시스템에서 hello tempdb 디렉터리 크기를 확인할 수 있습니다. 또는 이러한 구성 hello 시스템 드라이브로 제공할 수 없는 tempdb에 대 한 IOPS 값을 사용 합니다. 다시 온-프레미스를 실행 중인 시스템에는 tempdb에 대 한 사용된 toomonitor I/O 작업 수 있습니다.

/Mnt 또는 /mnt/resource hello VM의 SAP ASE 디렉터리가 저장 하면 안 됩니다. 또한 toohello tempdb /mnt 또는 /mnt/resource에는 기본 Azure VM 임시 인 공간 지속 되지 않으며 이므로 hello 개체 hello tempdb에 보관 하며 임시만 하는 경우에 마찬가지입니다. Azure VM 임시 공간 hello에 대 한 자세한 내용은에서 확인할 수 있습니다 [이 문서][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>데이터베이스 압축의 영향
I/O 대역폭이 제한 요인으로 작용할 수 있는 구성에서를 IOPS를 줄이는 모든 수단이 Azure와 같은 IaaS 시나리오에서 실행할 수 있는 toostretch hello 작업 부하를 이해할 수 있습니다. 따라서 하는 것이 좋습니다 toomake SAP ASE 압축 기존 SAP 데이터베이스 tooAzure 업로드 하기 전에 사용 되도록 합니다.

구현 되지 않은 경우 tooAzure를 업로드 하기 전에 hello 권장 tooperform 압축 몇 가지 이유로에서 제공 됩니다.

* 데이터 업로드 toobe tooAzure hello 양을 낮습니다.
* hello hello 압축 실행 기간은 짧은 더 많은 Cpu 또는 I/O 대역폭이 더 높거나 이하의 I/O 대기 시간 온-프레미스 보다 강력한 하드웨어 사용할 수 있다고 가정 하면
* 데이터베이스 크기가 작은 디스크 할당에 대 한 tooless 비용이 발생할 수 있습니다.

데이터 및 LOB 압축은 Azure 가상 컴퓨터에서 호스트되는 VM에서도 온-프레미스에서와 마찬가지로 작동합니다. 에 대 한 자세한 내용은 toocheck 압축 이미 사용 중이면 기존 SAP ASE 데이터베이스에서 확인 하는 방법은 SAP Note [1750510]합니다. 데이터베이스 압축에 대한 자세한 내용은 SAP Note [2121797]을 참조하세요.

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>DBACockpit toomonitor 데이터베이스 인스턴스를 사용 하 여
데이터베이스 플랫폼으로 SAP ASE를 사용 하는, SAP 시스템에 대 한 hello DBACockpit는 DBACockpit 트랜잭션에 포함 된 브라우저 창을 또는 Webdynpro로 액세스할 수 있습니다. 그러나 모니터링 하기 위한 모든 기능을 hello 되며 관리 hello 데이터베이스 hello DBACockpit의 hello Webdynpro 구현에서 사용할 수 있습니다.

으로 온-프레미스 시스템 몇 가지 단계가 필요 tooenable hello DBACockpit hello Webdynpro 구현에 의해 사용 되는 모든 SAP NetWeaver 기능 합니다. SAP Note를 따라 [1245200] tooenable hello webdynpros의 사용 및 생성 hello 필요한 것입니다. 지침 hello에 메모 위에 hello, http 및 https 연결에 사용 되는 hello 포트 toobe 함께 hello 인터넷 통신 관리자 (icm) 구성 합니다. http에 대 한 hello 기본 설정은 다음과 같습니다.

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
> 
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
> 
> 

및 DBACockpit 트랜잭션에서 생성 된 hello 링크 유사한 toothis 표시 됩니다.

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

에 따라와 hello Azure 가상 컴퓨터 호스팅 hello SAP 시스템 사이트를 통해 연결 하는 방법을 멀티 사이트 또는 express 경로 (크로스-프레미스 배포의 경우) 해야 toomake 있는지 해당 ICM 사용 확인 될 수 있는 정규화 된 호스트 이름 hello에 tooopen 시도 하 고 있는 컴퓨터에서 DBACockpit hello 합니다. SAP Note 참조 [773830] ICM 결정 하는 방법 toounderstand hello 프로필 매개 변수 및 매개 변수 icm/host_name_full 집합에 따라 정규화 된 호스트 이름을 명시적으로 필요한 경우.

온-프레미스와 Azure 간 크로스-프레미스 연결 없이 클라우드 전용 시나리오에서 hello VM을 배포한 경우 공용 IP 주소와는 domainlabel toodefine 필요 합니다. hello hello VM 아래의 hello 공용 DNS 이름 형식:

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
> 
> 

자세한 내용은 관련 toohello DNS 이름을 찾을 수 [여기][virtual-machines-azurerm-versus-azuresm]합니다.

설정을 hello SAP 프로필 매개 변수 icm/host_name_full toohello hello Azure VM hello 링크의 DNS 이름을 유사 하 게 나타날 수 있습니다.

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

이 경우에 필요 toomake 해야 합니다.

* Hello ICM으로 사용 되는 포트 toocommunicate hello TCP/IP에 대 한 Azure 포털에서에서 인바운드 규칙 toohello 네트워크 보안 그룹 추가
* ICM hello로 TCP/IP 사용 포트 toocommunicate hello에 대 한 인바운드 규칙 toohello Windows 방화벽 구성 추가

자동화 된 가져온 사용 가능한 모든 수정에 대 한 권장 tooperiodically hello 수정 컬렉션 SAP Note 적용 가능한 tooyour SAP 버전을 적용 합니다.

* [1558958]
* [1619967]
* [1882376]

SAP ASE에 대 한 DBA Cockpit에 대 한 자세한 내용은 SAP Note 다음 hello에 있습니다.

* [1605680]
* [1757924]
* [1757928]
* [1758182]
* [1758496]    
* [1814258]
* [1922555]
* [1956005]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>SAP ASE에 대한 백업/복구 고려 사항
Azure에 SAP ASE를 배포하는 경우 백업 방법을 검토해야 합니다. 경우에 hello 시스템 운영 중인 시스템이, SAP ASE에서 호스트 되는 hello SAP 데이터베이스를 백업 해야 주기적으로 합니다. Azure 저장소에 백업을 중요성이 존중 toocompensating 저장소 충돌에에서 세 개의 이미지를 유지 되므로 합니다. hello 적절 한 백업 및 복원 계획을 유지 관리에 대 한 주된 이유 때문입니다 지점 시간 복구 기능에서을 제공 하 여 논리적/수동 오류 보완할 수 있습니다. Hello 목표 tooeither 백업을 toorestore hello 데이터베이스 사용 다시 이므로 tooa 특정 지점에서 Azure tooseed 시간 또는 toouse hello 백업에 다른 시스템 hello 기존 데이터베이스를 복사 하 여 합니다. 예를 들어으로 전환할 수 있습니다의 hello는 2 계층 SAP 구성 tooa 3 계층 시스템 설정에서 동일한 시스템 백업을 복원 하 여 합니다.

Azure works에서 데이터베이스 백업 및 복원 hello 동일한 방식으로 온-프레미스를 수행 합니다. 다음 SAP Note를 참조하세요.

* [1588316]
* [1585981]

여기에는 덤프 구성 생성 및 백업 예약에 대한 자세한 내용이 나와 있습니다. 전략 및 구성할 수 요구 사항에 따라 데이터베이스 및 로그 toodisk hello 기존 디스크 중 하나에 덤프 하거나 hello 백업에 대 한 추가 디스크를 추가 합니다. 오류 발생 시 데이터 손실의 tooreduce hello 위험 권장 toouse 데이터베이스 디렉터리/파일이 있는 디스크입니다.

데이터 및 LOB 압축 SAP ASE 외에도 백업 압축을 제공합니다. 복사 하는 hello 데이터베이스 및 로그를 사용 하 여 공간을 덜 toooccupy toouse 백업 압축 것이 좋습니다. 자세한 내용은 SAP Note [1588316]을 참조하세요. 압축 hello 백업이 중요 tooreduce hello 양의 toodownload 백업 또는 hello tooon-프레미스 Azure 가상 컴퓨터에서에서 백업 덤프에 포함 된 Vhd를 계획 하는 경우에 전송할 데이터 toobe 이기도 합니다.

Hello Azure VM 임시 공간 /mnt 또는 /mnt/resource 데이터베이스 또는 로그 덤프 대상으로 사용 하지 마십시오.

#### <a name="performance-considerations-for-backupsrestores"></a>백업/복원에 대한 성능 고려 사항
완전 배포 에서처럼 백업/복원 성능은 동시에 읽을 수 있는 볼륨 수 및 이러한 볼륨의 어떤 hello 출력 수에 따라 달라 집니다. 또한 hello 백업 압축을 통해 CPU 사용률 tooeight CPU 스레드를 방금 된 Vm에서 중요 한 역할을 재생 수 있습니다. 따라서 다음을 가정할 수 있습니다.

* hello 사용 되는 디스크 toostore hello 수를 적게 데이터베이스 장치 hello, 더 작은 hello 전반적인 hello 읽기 처리량
* 더 작은 hello hello VM의에서 CPU 스레드 수가 hello, 백업 압축의 심각한 hello 영향 hello
* hello 적은 대상 (Linux 소프트웨어 raid를 장점 디스크) toowrite hello를 백업, 더 적은 hello 처리량 hello

tooincrease hello 수가 대상 toowrite toothere 두 가지 옵션, 필요에 따라 사용 되 는/결합 될 수 있습니다.

* Hello 백업 대상 볼륨을 해당 스트라이프 볼륨에서 순서 tooimprove hello IOPS 처리량에 여러 탑재 된 디스크 스트라이프
* SAP ASE 수준에서 덤프 구성 만들기를 사용 하는 둘 이상의 대상 디렉터리 toowrite hello 덤프를

탑재된 여러 디스크에 볼륨을 스트라이프하는 방법은 이 가이드의 앞부분에서 설명했습니다. 여러 디렉터리를 사용 하 여 hello SAP ASE 덤프 구성에 대 한 자세한 내용은 hello에 사용 되는 toocreate hello 덤프 구성 인 저장 프로시저 sp_config_dump에 toohello 문서를 참조 하십시오. [Sybase Infocenter](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Azure VM을 사용한 재해 복구
#### <a name="data-replication-with-sap-sybase-replication-server"></a>SA Sybase Replication Server를 사용한 데이터 복제
Hello로 SAP Sybase 복제 서버 (SRS) SAP ASE 비동기적으로 웜 대기 솔루션 tootransfer 데이터베이스 트랜잭션 tooa 멀리 떨어진 위치를 제공합니다. 

hello 설치 되 고 SRS의 작동에도 온-프레미스와 마찬가지로 Azure 가상 컴퓨터 서비스에서 호스팅되는 VM에서 기능적으로 작동 합니다.

SAP Replication Server를 통한 ASE HADR은 현재 지원되지 않습니다. 테스트를 받는 이며 hello 나중에 Microsoft Azure 플랫폼에 대 한 출시 수 수 있습니다.

## <a name="specifics-toooracle-database-on-windows"></a>구체적인 tooOracle Windows에서 데이터베이스
Oracle 소프트웨어는 Microsoft Windows Hyper-v와 Azure에서 Oracle toorun에서 지원 됩니다. 자세한 내용은 Windows Hyper-v와 Azure의 hello 일반 지원에 확인 하십시오: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces> 

Hello 일반 지원에 다음 Oracle 데이터베이스를 활용 하는 SAP 응용 프로그램의 hello 특정 시나리오 에서도 지원 됩니다. 세부 정보는 hello 문서의이 부분 이름은 지정 됩니다.

### <a name="oracle-version-support"></a>Oracle 지원 버전
Azure Virtual Machines에서 Oracle의 SAP 실행을 위해 지원되는 Oracle 버전 및 해당 OS 버전에 대한 자세한 내용은 SAP Note [2039619]에서 찾을 수 있습니다.

Oracle에서의 SAP Business Suite 실행에 대한 일반 정보는 1DX: <https://www.sap.com/community/topic/oracle.html>에서 찾을 수 있습니다.

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Azure VM의 SAP 설치에 대한 Oracle 구성 지침
#### <a name="storage-configuration"></a>저장소 구성
NTFS로 포맷된 디스크를 사용하는 하나의 Oracle 인스턴스만 지원됩니다. 모든 데이터베이스 파일 hello Vhd 또는 관리 하는 디스크에 따라 NTFS 파일 시스템에 저장 되어야 합니다. 이러한 디스크는 탑재 된 toohello Azure VM 및 Azure 페이지 BLOB 저장소를 기반으로 (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) 또는 관리 하는 디스크 (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). 모든 종류의 네트워크 드라이브 또는 Azure 파일 서비스와 같은 원격 공유:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx> 
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Oracle 데이터베이스 파일에 대해 지원되지 **않습니다** .

이 문서의 장에서에 작성 된 문이 hello Azure 페이지 BLOB 저장소 서비스 또는 관리 하는 디스크에 따라 디스크를 사용 하 여 [Vm 및 데이터 디스크에 대 한 캐싱을] [ dbms-guide-2.1] 및 [Microsoft Azure 저장소] [ dbms-guide-2.3] toodeployments hello Oracle 데이터베이스도로 적용 합니다.

Hello 문서의 hello 일반 부분의 앞부분에 나오는 설명 했 듯이 할당량 Azure 디스크에 대 한 IOPS 처리량에 존재 합니다. hello 정확한 할당량 hello VM 유형에 따라 사용 됩니다. VM 유형과 해당 할당량의 목록은 [여기(Linux)][virtual-machines-sizes-linux] 및 [여기(Windows)][virtual-machines-sizes-windows]에 있습니다.

지원 되는 Azure VM 유형 tooidentify hello, tooSAP 참고 참조 [1928533]합니다.

가능한 toostore로 디스크당 hello 현재 IOPS 할당량이 hello 요구를 충족 하는 모든 hello 하나의 단일 탑재 된 디스크에 대 한 DB 파일입니다. 

더 많은 IOPS 필요한 경우이 가장 좋습니다 (Windows Server 2012에서 사용할 수 및 더 높은) toouse 창 저장소 풀 또는 여러 탑재 된 디스크를 통해 하나의 큰 논리적 장치를 toocreate Windows 2008 r 2에 대 한 스트라이프 Windows ( 장참조[소프트웨어 RAID] [ dbms-guide-2.2] 이 문서의). 이 방법은 hello 관리 오버 헤드 toomanage hello 디스크 공간을 단순화 하 고 hello 노력을 피할 수 toomanually 여러 탑재 된 디스크 파일을 배포 합니다.

#### <a name="backup--restore"></a>백업/복원
백업 / 복원 기능, SAP BR hello * 도구 Oracle에서 지원 되는 hello 같은 방식에서 같이 표준 Windows Server 운영 체제 및 Hyper-v입니다. Oracle 복구 관리자 (RMAN) 백업 toodisk 및 디스크에서 복원도 지원 됩니다.

#### <a name="high-availability"></a>고가용성
높은 가용성 및 재해 복구를 위해 Oracle Data Guard가 지원됩니다. 자세한 내용은 [이 설명서][virtual-machines-windows-classic-configure-oracle-data-guard]에 있습니다.

#### <a name="other"></a>기타
Azure 가용성 집합 또는 SAP 모니터링와 같은 기타 모든 일반 항목에도 Oracle 데이터베이스 hello로 Vm의 배포를 위해이 문서의 처음 세 개의 장 hello에 설명 된 대로 적용 됩니다.

## <a name="specifics-toooracle-database-on-oracle-linux"></a>구체적인 tooOracle 데이터베이스 Oracle linux
Oracle 소프트웨어는 Microsoft Windows Hyper-v와 Azure에서 Oracle toorun에서 지원 됩니다. 자세한 내용은 Windows Hyper-v와 Azure의 hello 일반 지원에 확인 하십시오: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces> 

Hello 일반 지원에 다음 Oracle 데이터베이스를 활용 하는 SAP 응용 프로그램의 hello 특정 시나리오 에서도 지원 됩니다. 세부 정보는 hello 문서의이 부분 이름은 지정 됩니다.

### <a name="oracle-version-support"></a>Oracle 지원 버전
Azure Virtual Machines에서 Oracle의 SAP 실행을 위해 지원되는 Oracle 버전 및 해당 OS 버전에 대한 자세한 내용은 SAP Note [2039619]에서 찾을 수 있습니다.

Oracle에서의 SAP Business Suite 실행에 대한 일반 정보는 1DX: <https://www.sap.com/community/topic/oracle.html>에서 찾을 수 있습니다.

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Azure VM의 SAP 설치에 대한 Oracle 구성 지침
#### <a name="storage-configuration"></a>저장소 구성
ext3, ext4 및 xfs로 포맷된 디스크를 사용하는 하나의 Oracle 인스턴스만 지원됩니다. 모든 데이터베이스 파일은 VHD 또는 Managed Disks 기반의 파일 시스템에 저장되어야 합니다. 이러한 디스크는 탑재 된 toohello Azure VM 및 Azure 페이지 BLOB 저장소를 기반으로 (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) 또는 관리 하는 디스크 (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). 모든 종류의 네트워크 드라이브 또는 Azure 파일 서비스와 같은 원격 공유:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx> 
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Oracle 데이터베이스 파일에 대해 지원되지 **않습니다** .

이 문서의 장에서에 작성 된 문이 hello Azure 페이지 BLOB 저장소 서비스 또는 관리 하는 디스크에 따라 디스크를 사용 하 여 [Vm 및 데이터 디스크에 대 한 캐싱을] [ dbms-guide-2.1] 및 [Microsoft Azure 저장소] [ dbms-guide-2.3] toodeployments hello Oracle 데이터베이스도로 적용 합니다.

Hello 문서의 hello 일반 부분의 앞부분에 나오는 설명 했 듯이 할당량 Azure 디스크에 대 한 IOPS 처리량에 존재 합니다. hello 정확한 할당량 hello VM 유형에 따라 사용 됩니다. VM 유형과 해당 할당량의 목록은 [여기(Linux)][virtual-machines-sizes-linux] 및 [여기(Windows)][virtual-machines-sizes-windows]에 있습니다.

지원 되는 Azure VM 유형 tooidentify hello, tooSAP 참고 참조 [1928533]

가능한 toostore로 디스크당 hello 현재 IOPS 할당량이 hello 요구를 충족 하는 모든 hello 하나의 단일 탑재 된 디스크에 대 한 DB 파일입니다. 

더 많은 IOPS 필요한 경우이 가장 좋습니다 toouse LVM (논리 볼륨 관리자) 또는 MDADM toocreate 하나의 큰 논리 볼륨을 여러 탑재 된 디스크. 또한 이 문서의 [소프트웨어 RAID][dbms-guide-2.2] 챕터를 참조하세요. 이 방법은 hello 관리 오버 헤드 toomanage hello 디스크 공간을 단순화 하 고 hello 노력을 피할 수 toomanually 여러 탑재 된 디스크 파일을 배포 합니다.

#### <a name="backup--restore"></a>백업/복원
백업 / 복원 기능, SAP BR hello * 도구 Oracle에서 지원 되는 hello 같은 방식에서 같이 베어 메탈 및 Hyper-v입니다. Oracle 복구 관리자 (RMAN) 백업 toodisk 및 디스크에서 복원도 지원 됩니다.

#### <a name="high-availability"></a>고가용성
높은 가용성 및 재해 복구를 위해 Oracle Data Guard가 지원됩니다. 자세한 내용은 [이 설명서][virtual-machines-windows-classic-configure-oracle-data-guard]에 있습니다.

#### <a name="other"></a>기타
Azure 가용성 집합 또는 SAP 모니터링와 같은 기타 모든 일반 항목에도 Oracle 데이터베이스 hello로 Vm의 배포를 위해이 문서의 처음 세 개의 장 hello에 설명 된 대로 적용 됩니다.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Windows에서 SAP MaxDB 데이터베이스 hello에 대 한 구체적인 정보
### <a name="sap-maxdb-version-support"></a>SAP MaxDB 버전 지원
SAP는 현재 SAP MaxDB 버전 7.9를 Azure의 SAP NetWeaver 기반 제품에 사용하도록 지원합니다. SAP Service Marketplace에서 SAP NetWeaver 기반 제품을 함께 사용 하는 JDBC 및 ODBC 드라이버 toobe 또는 SAP MaxDB 서버에 대 한 모든 업데이트 hello을 통해서만 제공 됩니다 <https://support.sap.com/swdc>합니다.
SAP MaxDB에서의 SAP NetWeaver 실행에 대한 일반 정보는 <https://www.sap.com/community/topic/maxdb.html>에서 찾을 수 있습니다.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>SAP MaxDB DBMS에 대해 지원되는 Microsoft Windows 버전 및 Azure VM 유형
Azure에서 SAP MaxDB dbms toofind 지원 hello Microsoft Windows 버전을 참조 하세요.

* [SAP PAM(제품 가용성 매트릭스)][sap-pam]
* SAP Note [1928533]

Toouse hello 최신 버전의 Microsoft Windows 2012 r 2는 Microsoft Windows hello 운영 체제 가장 좋습니다.

### <a name="available-sap-maxdb-documentation"></a>사용 가능한 SAP MaxDB 설명서
SAP Note 다음 hello에서 SAP MaxDB 문서 목록이 업데이트 hello를 찾을 수 있습니다 [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Azure VM의 SAP 설치에 대한 SAP MaxDB 구성 지침
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>저장소 구성
SAP MaxDB에 대 한 azure 저장소의 유용한 장에서 설명한 hello 일반 권장 사항에 따라 [RDBMS 배포의 구조][dbms-guide-2]합니다.

> [!IMPORTANT]
> 다른 데이터베이스처럼 SAP MaxDB에도 데이터 및 로그 파일이 있습니다. 그러나 SAP MaxDB 용어에서 hello 올바른 용어는 "볼륨" (아닙니다: "file"). 예를 들어 SAP MaxDB 데이터 볼륨 및 로그 볼륨이 있습니다. 운영 체제 디스크 볼륨과 혼동하지 마세요. 
> 
> 

한마디로 다음을 수행해야 합니다.

* Azure 저장소 계정을 사용 하는 경우 너무 hello SAP MaxDB 데이터 및 로그 볼륨 (예: 파일)를 보유 하는 hello Azure 저장소 계정을 설정**로컬 중복 저장소 (LRS)** 장에 지정 된 대로 [MicrosoftAzure저장소] [dbms-guide-2.3].
* 로그 볼륨 (예: 파일)에 대 한 hello IO 경로에서 SAP MaxDB 데이터 볼륨 (예: 파일)에 대 한 별도 hello IO 경로입니다. 즉, SAP MaxDB 데이터 볼륨 (예: 파일)가 하나의 논리 드라이브에 설치 된 toobe SAP MaxDB 로그 볼륨 (예: 파일) toobe 다른 논리 드라이브에 설치 했습니다.
* Hello 적절 한 캐싱 종류 설정 사용할지 표준 Azure 또는 Azure 프리미엄 저장소 장에 설명 된 대로 및 SAP MaxDB 데이터 또는 로그 볼륨 (예: 파일)에 대 한 수행할 여부에 따라 각 디스크에 대 한 [Vm및데이터디스크에대한캐싱을][dbms-guide-2.1].
* 디스크당 hello 현재 IOPS 할당량이 hello 요구를 충족 하는 경우으로 가능한 toostore 모든 hello 데이터 볼륨은 단일 탑재 된 디스크에 사용 되며 다른 단일 탑재 된 디스크에 모든 데이터베이스 로그 볼륨을 저장할 수도 합니다.
* IOPS 및/또는 공간이 더 필요한 경우이 가장 좋습니다 (Microsoft Windows Server 2012에서 사용할 수 및 더 높은) toouse Microsoft 창 저장소 풀 또는 Microsoft Windows 하나의 큰 논리적 장치에 대 한 Microsoft Windows 2008 R2 toocreate 스트라이프 여러 탑재 된 디스크. 또한 이 문서의 [소프트웨어 RAID][dbms-guide-2.2] 챕터를 참조하세요. 이 방법은 hello 관리 오버 헤드 toomanage hello 디스크 공간 단순 해지고 여러 탑재 된 디스크 파일을 수동으로 배포 하는 hello 노력을 피할 수 있습니다.
* 가장 높은 IOPS 요구 hello에 대 한 DS 시리즈 및 GS 시리즈 Vm에서 사용 가능한 Azure 프리미엄 저장소를 사용할 수 있습니다.

![SAP MaxDB DBMS에 대한 Azure IaaS VM의 참조 구성][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>백업 및 복원
Azure에 SAP MaxDB를 배포하는 경우 백업 방법을 검토해야 합니다. Hello 시스템이 생산적인 시스템이 아닌 경우에 SAP MaxDB에서 호스트 되는 hello SAP 데이터베이스를 백업 해야 주기적으로 합니다. Azure 저장소에는 세 개의 이미지가 유지되므로 저장소 오류 및 더 중요한 작동 또는 관리 오류에 대한 시스템 보호 면에서 백업의 중요성이 줄어들었습니다. hello 적절 한 백업 및 복원 계획을 유지 관리에 대 한 주된 이유는 되므로 지정 시간 복구 기능을 제공 하 여 논리적 또는 수동 오류 조정할 수 있습니다. Hello 목표 이므로 tooeither 사용 하 여 백업을 toorestore hello 데이터베이스 tooa 특정 지점에서 Azure tooseed 시간 또는 toouse hello 백업에 다른 시스템 hello 기존 데이터베이스를 복사 하 여 합니다. 예를 들어으로 전환할 수 있습니다의 hello는 2 계층 SAP 구성 tooa 3 계층 시스템 설정에서 동일한 시스템 백업을 복원 하 여 합니다.

SAP Note에 나열 된 Azure 작동 hello 같은 방식으로 표준 SAP MaxDB를 사용할 수 있도록 온-프레미스 시스템에 적용 되는 백업/복원 hello SAP MaxDB 설명서 문서 중 하나에서 설명 하는 도구에서에서 데이터베이스 백업 및 복원 [767598 ]. 

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>백업 및 복원에 대한 성능 고려 사항
완전 배포 에서처럼 백업 및 복원 성능은 이러한 볼륨의 병렬 및 hello 처리량에 읽을 수 있는 볼륨 수에 따라 달라 집니다. 또한 hello 백업 압축을 통해 CPU 사용률 tooeight CPU 스레드를 된 Vm에서 중요 한 역할을 수행할 수 있습니다. 따라서 다음을 가정할 수 있습니다.

* 사용 되는 디스크 toostore hello 데이터베이스 장치 hello 수를 적게 hello, hello 낮은 hello 전체 읽기 처리량
* 더 작은 hello hello VM의에서 CPU 스레드 수가 hello, 백업 압축의 심각한 hello 영향 hello
* hello hello 낮은 hello 처리량을 더 적은 toowrite hello 백업 대상 (디스크, Stripe 디렉터리)

tooincrease hello 수가 대상에 toowrite, 사용할 수 있는, 조합에 있을 수 있음 필요에 따라 두 가지가 있습니다.

* 백업에 대해 별도의 볼륨을 지정합니다.
* Hello 백업 대상 볼륨을 해당 스트라이프 디스크 볼륨의 순서 tooimprove hello IOPS 처리량에 여러 탑재 된 디스크 스트라이프
* 다음을 위한 별도의 전용 논리적 디스크 장치가 필요합니다.
  * SAP MaxDB 백업 볼륨(즉, 파일)
  * SAP MaxDB 데이터 볼륨(즉, 파일)
  * SAP MaxDB 로그 볼륨(즉, 파일)

탑재된 여러 디스크에 대한 볼륨 스트라이프는 이 문서 앞부분의 [소프트웨어 RAID][dbms-guide-2.2] 챕터에서 설명했습니다. 

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>기타
일반 다른 모든 설명서에는 Azure 가용성 집합 또는 SAP 모니터링 hello SAP MaxDB 데이터베이스와 Vm의 배포를 위해이 문서의 처음 세 개의 장 hello에 설명 된 대로도 적용 됩니다.
다른 SAP MaxDB 관련 설정은 투명 tooAzure Vm 고 SAP Note에 나열 된 다른 문서에 설명 된 [767598 ] 및 이러한 SAP note에서:

* [826037] 
* [1139904]
* [1173395]

## <a name="specifics-for-sap-livecache-on-windows"></a>Windows의 SAP liveCache에 대한 고유 정보
### <a name="sap-livecache-version-support"></a>SAP liveCache 버전 지원
Azure Virtual Machines에서 지원되는 SAP liveCache의 최소 버전은 **EhP 2 for SAP SCM 7.0** 이상에 대해 릴리스된 **liveCache 7.9.08.31** 및 **LCA-Build 25**를 포함하는 **SAP LC/LCAPPS 10.0 SP 25**입니다.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>SAP liveCache DBMS에 대해 지원되는 Microsoft Windows 버전 및 Azure VM 유형
Azure에서 SAP liveCache에 대 한 toofind 지원 hello Microsoft Windows 버전 참조:

* [SAP PAM(제품 가용성 매트릭스)][sap-pam]
* SAP Note [1928533]

Toouse hello 최신 버전의 hello 운영 체제가 Microsoft Windows Server 가장 좋습니다. 

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Azure VM의 SAP 설치에 대한 SAP liveCache 구성 지침
#### <a name="recommended-azure-vm-types"></a>권장되는 Azure VM 유형
SAP liveCache 거 대 한 계산을 수행 하는 응용 프로그램 그대로 hello 양과 RAM과 CPU의 속도 SAP liveCache 성능에 큰 영향을 있습니다. 

SAP에서 지 원하는 hello Azure VM 유형에 (SAP Note [1928533]), 모든 가상 CPU 리소스 할당 toohello VM 전용된 물리적 CPU 리소스가 hello 하이퍼바이저에 의해 지원 됩니다. 오버프로비저닝이 발생되지 않습니다(따라서 CPU 리소스에 대한 경쟁 없음).

마찬가지로, SAP에서 지 원하는 모든 Azure VM 인스턴스 형식에 대해 hello VM 메모리는 100% 매핑된 toohello 물리적 메모리-과도 프로 비전 (오버 커밋), 예를 들어, 사용 되지 않습니다.

이러한 관점에서 것은 좋습니다 toouse hello 새 D 시리즈 또는 DS 시리즈 (Azure 프리미엄 저장소와 함께)에서 Azure VM 유형은 60 %A 시리즈 hello 보다 빠른 프로세서가 있는입니다. Hello 가장 높은 RAM과 CPU 부하를 사용할 수 있습니다 G 시리즈 및 GS 시리즈 (Azure 프리미엄 저장소와 함께)에서 Vm hello 최신 Intel® Xeon® 프로세서 hello 메모리 및 hello D의 4 번 hello 솔리드 스테이트 드라이브 저장소 (Ssd) 두 번 포함 하는 E5 v3 제품군 / DS 시리즈 합니다.

#### <a name="storage-configuration"></a>저장소 구성
Azure 저장소 최선의 방법 권장 사항에 대 한 SAP MaxDB 장에서 설명한 hello 모든 SAP liveCache은 SAP MaxDB 기술을 기반으로, [저장소 구성] [ dbms-guide-8.4.1] SAP liveCache에 대 한 유효 합니다. 

#### <a name="dedicated-azure-vm-for-livecache"></a>liveCache용 전용 Azure VM
SAP liveCache 컴퓨팅 기능을 집중적으로 사용 하는 대로 생산적인 사용에 대 한 것이 좋습니다 toodeploy 전용된 Azure 가상 컴퓨터에서. 

![생산적인 사용 사례를 위한 liveCache용 전용 Azure VM][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>백업 및 복원
백업 및 복원, 성능 고려 사항 포함 하 여 hello 관련 SAP MaxDB 장에서 이미 설명 [백업 및 복원] [ dbms-guide-8.4.2] 및 [백업에 대 한 성능 고려 사항 복원 및][dbms-guide-8.4.3]합니다. 

#### <a name="other"></a>기타
기타 모든 일반 항목 hello에서 이미 설명 된 관련 SAP MaxDB [이] [ dbms-guide-8.4.4] 장 합니다. 

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Windows에서 SAP 콘텐츠 서버 hello에 대 한 구체적인 정보
hello SAP 콘텐츠 서버는 서로 다른 형식에서 전자 문서와 같은 별도 서버 기반 구성 요소로, toostore 콘텐츠입니다. SAP 콘텐츠 서버 hello 기술을 개발 하 여 제공 하며 toobe 사용 되는 응용 프로그램 간 모든 SAP 응용 프로그램에 대 한 있습니다. 별도의 시스템에 설치됩니다. 일반적인 콘텐츠는 자료 및 기술 웨어하우스나 hello mySAP PLM 문서 관리 시스템에서에서 발생 하는 기술 드로잉의 설명서 교육을 진행 합니다. 

### <a name="sap-content-server-version-support"></a>SAP Content Server 버전 지원
SAP에서 현재 다음을 지원합니다.

* **SAP Content Server** 버전 **6.50 이상**
* **SAP MaxDB 버전 7.9**
* **Microsoft IIS(인터넷 정보 서비스) 버전 8.0 이상**

Hello toouse hello이이 문서 작성 당시에는 SAP 콘텐츠 서버에서의 최신 버전을 적극 권장 **6.50 SP4**, 및 최신 버전의 hello **Microsoft IIS 8.5**합니다. 

Hello에 SAP 콘텐츠 서버 및 Microsoft IIS의 최신 지원 hello 버전 확인 [SAP 제품 사용 가능성 행렬 (PAM)][sap-pam]합니다.

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>SAP Content Server에 대해 지원되는 Microsoft Windows 버전 및 Azure VM 유형
Azure에서 SAP 콘텐츠 서버에 대 한 지원 되는 Windows 버전 아웃 toofind 참조:

* [SAP PAM(제품 가용성 매트릭스)][sap-pam]
* SAP Note [1928533]

Toouse hello 최신 버전의 Microsoft Windows Server 가장 좋습니다.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Azure VM의 SAP 설치에 대한 SAP Content Server 구성 지침
#### <a name="storage-configuration"></a>저장소 구성
모든 Azure 저장소 모범 사례 장에서 설명한 SAP MaxDB에 대 한 권장 사항 hello MaxDB SAP 데이터베이스의 toostore 파일 SAP 콘텐츠 서버를 구성 하는 경우 [저장소 구성] [ dbms-guide-8.4.1] 도 hello SAP 콘텐츠 서버 시나리오에 대해 유효 합니다. 

Hello 파일 시스템의 SAP 콘텐츠 서버 toostore 파일을 구성 하는 경우 전용된 논리 드라이브 toouse 것이 좋습니다. Windows 저장소 공간을 사용 하 여 사용 하면 tooalso 증가 논리 디스크 크기 및 IOPS 처리량 장에 설명 된 대로 [소프트웨어 RAID][dbms-guide-2.2]합니다. 

#### <a name="sap-content-server-location"></a>SAP Content Server 위치
SAP 콘텐츠 서버에 toobe hello에 배포 된 동일한 Azure 지역 및 SAP 시스템 hello를 배포 하는 Azure VNET 합니다. Toodeploy SAP 콘텐츠 서버 구성 요소는 전용된 Azure VM 또는 hello hello SAP 시스템에서 실행 하는 동일한 VM 것인지 무료 toodecide 됩니다. 

![SAP Content Server용 전용 Azure VM][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>SAP Cache Server 위치
hello SAP 캐시 서버는 추가 서버 기반 구성 요소 tooprovide 액세스 too(cached) 문서 로컬로입니다. SAP 캐시 서버 hello hello 문서 SAP 콘텐츠 서버에 캐시합니다. 문서가 여러 위치에서 두 번 이상 검색 toobe 가질 경우 toooptimize 네트워크 트래픽입니다. hello 일반적은 해당 hello SAP 캐시 서버 hello SAP 캐시 서버에 액세스 하는 toobe 실제로 닫기 toohello 클라이언트가지고 있다고 가정 합니다. 

다음 두 가지 옵션이 있습니다.

1. **클라이언트는 백 엔드 SAP 시스템** 해당 SAP 시스템은 클라이언트 구성된 tooaccess SAP 콘텐츠 서버는 백 엔드 SAP 시스템을 사용 하는 경우. SAP 시스템과 SAP 콘텐츠 서버 hello에 배포 되 hello에 같은 Azure 지역 – 닫기 실제로 동일한 Azure 데이터 센터-다른 tooeach 합니다. 따라서 없습니다 필요 toohave 전용된 SAP 캐시 서버입니다. SAP UI (SAP GUI 나 웹 브라우저) 클라이언트 액세스 hello SAP 시스템을 직접 및 hello SAP hello SAP 콘텐츠 서버에서에서 시스템 검색 문서.
2. **클라이언트는 온-프레미스 웹 브라우저** hello SAP 콘텐츠 서버에 구성 된 toobe hello 웹 브라우저에서 직접 액세스할 수 있습니다. 이 경우 온-프레미스를 실행 하는 웹 브라우저는 클라이언트의 hello SAP 콘텐츠 서버. 온-프레미스 데이터 센터 및 Azure 데이터 센터 (이상적으로 닫기 tooeach 다른) 서로 다른 물리적 위치에 배치 됩니다. 온-프레미스 데이터 센터는 Azure 사이트 간 VPN 또는 express 경로 통해 연결 된 tooAzure입니다. 두 옵션 모두 보안 VPN 네트워크 연결 tooAzure를 제공 하지만 사이트 간 네트워크 연결에는 hello 온-프레미스 데이터 센터 및 hello Azure 데이터 센터 간 네트워크 대역폭 및 대기 시간 SLA를 제공 하지 않습니다. 액세스 toodocuments toospeed, hello 다음 중 하나를 수행할 수 있습니다.
   1. 온-프레미스 SAP 캐시 서버를 설치, toohello 온-프레미스 웹 브라우저를 닫습니다 (옵션을 [이] [ dbms-guide-900-sap-cache-server-on-premises] 그림)
   2. 빠른 속도와 짧은 대기 시간의 온-프레미스 데이터 센터와 Azure 데이터 센터 간 전용 네트워크 연결을 제공하는 Azure ExpressRoute를 구성합니다.

![옵션 tooinstall SAP 캐시 서버 온-프레미스][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>백업/복원
Hello 백업/복원 절차 및 성능 고려 사항은 SAP MaxDB 장에서 이미 설명 된 hello MaxDB SAP 데이터베이스의 hello SAP 콘텐츠 서버 toostore 파일을 구성 하는 경우 [백업 및 복원] [ dbms-guide-8.4.2] 및 장 [백업 및 복원에 대 한 성능 고려 사항][dbms-guide-8.4.3]합니다. 

Hello 파일 시스템의 hello SAP 콘텐츠 서버 toostore 파일을 구성 하는 경우 한 가지 방법은 tooexecute 수동 백업/복원 hello 전체 파일 구조는 hello 문서의 위치입니다. 비슷한 tooSAP MaxDB 백업/복원, 백업 목적을 위해 toohave 전용된 디스크 볼륨을 권장 합니다. 

#### <a name="other"></a>기타
다른 SAP 콘텐츠 서버 특정 설정은 투명 tooAzure Vm 고 다양 한 문서 및 SAP Note에서 설명 합니다.

* <https://service.sap.com/contentserver> 
* SAP Note [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Windows에서 LUW 용 DB2 비슷하므로 tooIBM
Microsoft azure Linux, UNIX 및 Windows (LUW) tooAzure 가상 컴퓨터에 대해 IBM d b 2에서 실행 중인 기존 SAP 응용 프로그램을 쉽게 마이그레이션할 수 있습니다. LUW 용 IBM d b 2에서의 SAP, 사용 관리자와 개발자가 동일한 개발 및 관리 도구를 사용할 수 있는 온-프레미스 hello를 계속 사용할 수 있습니다.
LUW에서 찾을 수 있습니다에 대 한 SAP Business Suite IBM d b 2에서 실행 하는 방법에 대 한 일반 정보에 SAP 커뮤니티 네트워크 (SCN) hello <https://www.sap.com/community/topic/db2-for-linux-unix-and-windows.html>합니다.

Azure에서 LUW용 DB2의 SAP에 대한 추가 정보 및 업데이트는 SAP Note [2233094]를 참조하세요. 

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Linux, UNIX 및 Windows용 IBM DB2 버전 지원
Microsoft Azure Virtual Machines 서비스에서 LUW용 IBM DB2의 SAP는 DB2 버전 10.5부터 지원됩니다.

지원 되는 SAP 제품 및 Azure VM 유형에 대 한 정보를 참고 tooSAP 참조 [1928533]합니다.

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Azure VM의 SAP 설치에 대한 Linux, UNIX 및 Windows용 IBM DB2 구성 지침
#### <a name="storage-configuration"></a>저장소 구성
모든 데이터베이스 파일을 직접 연결 된 디스크에 따라 hello NTFS 파일 시스템에 저장 되어야 합니다. 이러한 디스크는 탑재 된 toohello Azure VM 및 Azure 페이지 BLOB 저장소에 따라 (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) 또는 관리 하는 디스크 (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). 모든 종류의 네트워크 드라이브 또는 원격 공유 hello 다음 Azure 파일 서비스는 같은 **하지** 데이터베이스 파일에 대 한 지원: 

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Azure 페이지 BLOB 저장소 서비스 또는 관리 하는 디스크에 따라 디스크를 사용 하는 경우이 문서의 장에서에 작성 된 문이 hello [RDBMS 배포의 구조] [ dbms-guide-2] IBM DB2 hello로 toodeployments에도 적용 LUW 데이터베이스입니다. 

Hello 문서의 hello 일반 부분의 앞부분에 나오는 설명 했 듯이 할당량 디스크에 대 한 IOPS 처리량에 존재 합니다. hello 정확한 할당량 사용 hello VM 형식에 따라 달라 집니다. VM 유형과 해당 할당량의 목록은 [여기(Linux)][virtual-machines-sizes-linux] 및 [여기(Windows)][virtual-machines-sizes-windows]에 있습니다.

디스크당 hello 현재 IOPS 할당량은 충분 한 것이 가능한 toostore로 모든 hello 하나의 단일 탑재 된 디스크에 데이터베이스 파일입니다. 

성능 고려 사항 toochapter "데이터 보안 및 성능 고려 사항에 대 한 데이터베이스 디렉터리" SAP 설치 가이드에서 참조 합니다.

(Windows Server 2012에서 사용할 수 및 더 높은) Windows 저장소 풀을 사용할 수 있습니다 또는 Windows 2008 r 2와 Windows 스트라이프 장에서 설명 또는 [소프트웨어 RAID] [ dbms-guide-2.2] 이 문서의 toocreate 하나의 큰 논리적 장치 여러 디스크에 걸쳐 있습니다.
Sapdata 및 saptmp 디렉터리에 대 한 hello DB2 저장소 경로 포함 하는 hello 디스크, 실제 디스크 섹터 크기는 512KB를 지정 해야 합니다. Windows 저장소 풀을 사용할 경우 만들어야 hello hello 매개 변수를 사용 하 여 명령줄 인터페이스를 통해 수동으로 저장소 풀이 "-LogicalSectorSizeDefault"입니다. 자세한 내용은 <https://technet.microsoft.com/itpro/powershell/windows/storage/new-storagepool>을 참조하세요.

#### <a name="backuprestore"></a>백업/복원
IBM d b 2에 대 한 백업/복원 기능 hello LUW에서 지원 되는 hello 동일 방식에서 같이 표준 Windows Server 운영 체제 및 Hyper-v입니다.

유효한 데이터베이스 백업 전략이 있는지 확인해야 합니다. 

완전 배포 에서처럼 백업/복원 성능은 동시에 읽을 수 있는 볼륨 수 및 이러한 볼륨의 어떤 hello 출력 수에 따라 다릅니다. 또한 hello 백업 압축을 통해 CPU 사용률 tooeight CPU 스레드를 방금 된 Vm에서 중요 한 역할을 재생 수 있습니다. 따라서 다음을 가정할 수 있습니다.

* hello 사용 되는 디스크 toostore hello 수를 적게 데이터베이스 장치 hello, 더 작은 hello 전반적인 hello 읽기 처리량
* 더 작은 hello hello VM의에서 CPU 스레드 수가 hello, 백업 압축의 심각한 hello 영향 hello
* hello hello 낮은 hello 처리량을 더 적은 toowrite hello 백업 대상 (디스크, Stripe 디렉터리)

대상으로 toowrite tooincrease hello 수, 두 가지 옵션이 필요에 따라 사용 되 는/결합 될 수 있습니다.

* Hello 백업 대상 볼륨을 해당 스트라이프 볼륨에서 순서 tooimprove hello IOPS 처리량에 여러 디스크 스트라이프
* 에 둘 이상의 대상 디렉터리 toowrite hello 백업을 사용 하 여

#### <a name="high-availability-and-disaster-recovery"></a>고가용성 및 재해 복구
MSCS(Microsoft Cluster Server)는 지원되지 않습니다.

DB2 HADR(고가용성 재해 복구)은 지원됩니다. Hello HA 구성의 가상 컴퓨터를 hello가 이름 확인에 관한 작업을 Azure의 hello 설치 프로그램에서 온-프레미스 수행 된 모든 설정과 다르지 않습니다. IP 확인만 toorely는 권장 되지 않습니다.

Hello 데이터베이스 디스크를 저장 하는 hello 저장소 계정에 대 한 지리적 복제를 사용 하지 마십시오. 자세한 내용은 참조 toochapter [Microsoft Azure 저장소] [ dbms-guide-2.3] 및 장 [고가용성 및 재해 복구 Azure Vm과] [ dbms-guide-3].

#### <a name="other"></a>기타
Azure 가용성 집합 또는 SAP 모니터링와 같은 일반 다른 모든 항목 에서도 LUW 용 IBM d b 2와 Vm의 배포를 위해이 문서의 처음 세 개의 장 hello에 설명 된 대로 적용 됩니다. 

또한 toochapter 참조할 [Azure 요약에서의 SAP 용 일반 SQL Server][dbms-guide-5.8]합니다.

## <a name="specifics-tooibm-db2-for-luw-on-linux"></a>Linux에서 LUW 용 DB2 비슷하므로 tooIBM
Microsoft azure Linux, UNIX 및 Windows (LUW) tooAzure 가상 컴퓨터에 대해 IBM d b 2에서 실행 중인 기존 SAP 응용 프로그램을 쉽게 마이그레이션할 수 있습니다. LUW 용 IBM d b 2에서의 SAP, 사용 관리자와 개발자가 동일한 개발 및 관리 도구를 사용할 수 있는 온-프레미스 hello를 계속 사용할 수 있습니다. LUW에서 찾을 수 있습니다에 대 한 SAP Business Suite IBM d b 2에서 실행 하는 방법에 대 한 일반 정보에 SAP 커뮤니티 네트워크 (SCN) hello <https://www.sap.com/community/topic/db2-for-linux-unix-and-windows.html>합니다.

Azure에서 LUW용 DB2의 SAP에 대한 추가 정보 및 업데이트는 SAP Note [2233094]를 참조하세요.

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Linux, UNIX 및 Windows용 IBM DB2 버전 지원
Microsoft Azure Virtual Machines 서비스에서 LUW용 IBM DB2의 SAP는 DB2 버전 10.5부터 지원됩니다.

지원 되는 SAP 제품 및 Azure VM 유형에 대 한 정보를 참고 tooSAP 참조 [1928533]합니다.

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Azure VM의 SAP 설치에 대한 Linux, UNIX 및 Windows용 IBM DB2 구성 지침
#### <a name="storage-configuration"></a>저장소 구성
모든 데이터베이스 파일은 직접 연결된 디스크 기반의 파일 시스템에 저장되어야 합니다. 이러한 디스크는 탑재 된 toohello Azure VM 및 Azure 페이지 BLOB 저장소에 따라 (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) 또는 관리 하는 디스크 (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). 모든 종류의 네트워크 드라이브 또는 원격 공유 hello 다음 Azure 파일 서비스는 같은 **하지** 데이터베이스 파일에 대 한 지원:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

Azure 페이지 BLOB 저장소에 따라 디스크를 사용 하는 경우이 문서의 장에서에 작성 된 문이 hello [RDBMS 배포의 구조] [ dbms-guide-2] LUW 데이터베이스 용 IBM DB2 hello로 toodeployments에도 적용 합니다.

Hello 문서의 hello 일반 부분의 앞부분에 나오는 설명 했 듯이 할당량 디스크에 대 한 IOPS 처리량에 존재 합니다. hello 정확한 할당량 사용 hello VM 형식에 따라 달라 집니다. VM 유형과 해당 할당량의 목록은 [여기(Linux)][virtual-machines-sizes-linux] 및 [여기(Windows)][virtual-machines-sizes-windows]에 있습니다.

디스크당 hello 현재 IOPS 할당량은 충분 한 것이 가능한 toostore로 모든 hello 하나의 단일 디스크에 데이터베이스 파일입니다.

성능 고려 사항 toochapter "데이터 보안 및 성능 고려 사항에 대 한 데이터베이스 디렉터리" SAP 설치 가이드에서 참조 합니다.

또는 또는 사용할 수 있습니다 (논리 볼륨 관리자) LVM MDADM 장에 설명 된 대로 [소프트웨어 RAID] [ dbms-guide-2.2] 이 문서 toocreate 하나의 큰 논리적 장치의 여러 디스크에 걸쳐 있습니다.
Sapdata 및 saptmp 디렉터리에 대 한 hello DB2 저장소 경로 포함 하는 hello 디스크, 실제 디스크 섹터 크기는 512KB를 지정 해야 합니다.

#### <a name="backuprestore"></a>백업/복원
IBM d b 2에 대 한 백업/복원 기능 hello LUW에서 지원 되는 hello 표준 Linux 설치 온-프레미스에서 방식으로 동일 합니다.

유효한 데이터베이스 백업 전략이 있는지 확인해야 합니다.

완전 배포 에서처럼 백업/복원 성능은 동시에 읽을 수 있는 볼륨 수 및 이러한 볼륨의 어떤 hello 출력 수에 따라 다릅니다. 또한 hello 백업 압축을 통해 CPU 사용률 tooeight CPU 스레드를 방금 된 Vm에서 중요 한 역할을 재생 수 있습니다. 따라서 다음을 가정할 수 있습니다.

* hello 사용 되는 디스크 toostore hello 수를 적게 데이터베이스 장치 hello, 더 작은 hello 전반적인 hello 읽기 처리량
* 더 작은 hello hello VM의에서 CPU 스레드 수가 hello, 백업 압축의 심각한 hello 영향 hello
* hello hello 낮은 hello 처리량을 더 적은 toowrite hello 백업 대상 (디스크, Stripe 디렉터리)

대상으로 toowrite tooincrease hello 수, 두 가지 옵션이 필요에 따라 사용 되 는/결합 될 수 있습니다.

* Hello 백업 대상 볼륨을 해당 스트라이프 볼륨에서 순서 tooimprove hello IOPS 처리량에 여러 디스크 스트라이프
* 에 둘 이상의 대상 디렉터리 toowrite hello 백업을 사용 하 여

#### <a name="high-availability-and-disaster-recovery"></a>고가용성 및 재해 복구
DB2 HADR(고가용성 재해 복구)은 지원됩니다. Hello HA 구성의 가상 컴퓨터를 hello가 이름 확인에 관한 작업을 Azure의 hello 설치 프로그램에서 온-프레미스 수행 된 모든 설정과 다르지 않습니다. IP 확인만 toorely는 권장 되지 않습니다.

Hello 데이터베이스 디스크를 저장 하는 hello 저장소 계정에 대 한 지리적 복제를 사용 하지 마십시오. 자세한 내용은 참조 toochapter [Microsoft Azure 저장소] [ dbms-guide-2.3] 및 장 [고가용성 및 재해 복구 Azure Vm과] [ dbms-guide-3].

#### <a name="other"></a>기타
Azure 가용성 집합 또는 SAP 모니터링와 같은 일반 다른 모든 항목 에서도 LUW 용 IBM d b 2와 Vm의 배포를 위해이 문서의 처음 세 개의 장 hello에 설명 된 대로 적용 됩니다.

또한 toochapter 참조할 [Azure 요약에서의 SAP 용 일반 SQL Server][dbms-guide-5.8]합니다.

