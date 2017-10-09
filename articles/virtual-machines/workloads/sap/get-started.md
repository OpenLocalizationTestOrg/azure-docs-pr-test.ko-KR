---
title: "Azure Vm에서 SAP aaaGetting 시작 | Microsoft Docs"
description: "Microsoft Azure의 VM(가상 컴퓨터)에서 실행되는 SAP 솔루션에 대한 자세한 정보"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a><span data-ttu-id="54270-103">SAP 워크로드 시나리오 호스팅 및 실행에 Azure 사용</span><span class="sxs-lookup"><span data-stu-id="54270-103">Using Azure for hosting and running SAP workload scenarios</span></span>
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

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
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md 
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
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
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
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
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes]:../../linux/sizes.md
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

<span data-ttu-id="54270-104">SAP 준비 클라우드 파트너도 Microsoft Azure를 선택 하 여 확장 가능한, 규정 준수를 및 엔터프라이즈에서 입증 된 플랫폼에서 중요 한 SAP 작업 및 시나리오를 실행 하는 수 tooreliably 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-104">By choosing Microsoft Azure as your SAP ready cloud partner, you are able tooreliably run your mission critical SAP workloads and scenarios on a scalable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="54270-105">Hello 확장성, 유연성을 가져와서 Azure 절감 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-105">Get hello scalability, flexibility, and cost savings of Azure.</span></span> <span data-ttu-id="54270-106">Microsoft와 SAP 사이의 확장 hello 파트너 관계와-Azure에서 개발/테스트 및 프로덕션 시나리오에서 SAP 응용 프로그램을 실행할 수 있고 완전히 지원.</span><span class="sxs-lookup"><span data-stu-id="54270-106">With hello expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in Azure - and be fully supported.</span></span> <span data-ttu-id="54270-107">SAP NetWeaver tooSAP S4/HANA, SAP BI, Linux tooWindows, SAP HANA tooSQL에서에서 한 거둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-107">From SAP NetWeaver tooSAP S4/HANA, SAP BI, Linux tooWindows, SAP HANA tooSQL, we have you covered.</span></span> 

<span data-ttu-id="54270-108">호스팅와 SAP NetWeaver 시나리오 외에도 Azure에서 DBMS hello, 다른 호스트할 수 있습니다 Azure에서 SAP BI와 같은 다른 SAP 작업 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-108">Besides hosting SAP NetWeaver scenarios with hello different DBMS on Azure, you can host different other SAP workload scenarios, like SAP BI on Azure.</span></span> <span data-ttu-id="54270-109">"Azure 가상 컴퓨터에서의 SAP NetWeaver." hello 절의 기본 Azure 가상 컴퓨터에 SAP NetWeaver 배포에 대 한 설명서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-109">Documentation regarding SAP NetWeaver deployments on Azure native Virtual Machines can be found in hello section "SAP NetWeaver on Azure Virtual Machines."</span></span> 

<span data-ttu-id="54270-110">Azure는 CPU 및 메모리 리소스 toocover SAP 작업 부하의 SAP HANA를 활용 하 여 크기가 계속 성장 하 고 있는 네이티브 Azure 가상 컴퓨터 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-110">Azure has native Azure Virtual Machine offers that are ever growing in size of CPU and memory resources toocover SAP workload that leverages SAP HANA.</span></span> <span data-ttu-id="54270-111">이 항목에 대 한 자세한 내용은 문서를 찾는 hello hello 섹션 Azure 가상 컴퓨터에서 SAP HANA. "</span><span class="sxs-lookup"><span data-stu-id="54270-111">For more information on this topic, look up hello documents under hello section SAP HANA on Azure Virtual Machines."</span></span>

<span data-ttu-id="54270-112">SAP HANA에 대해 Azure의 hello 고유성에는 Azure의 경쟁을 별도로 설정 하는 한 고유 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-112">hello uniqueness of Azure for SAP HANA is a unique offer that sets Azure apart from competition.</span></span> <span data-ttu-id="54270-113">더 많은 메모리와 CPU 리소스를 호스팅 순서 tooenable에서 SAP HANA를 포함 하는 시나리오, Azure에서는 고객의 사용량 hello 까다로운 SAP 전용 too20 t B의 (60TB 확장)를 필요로 하는 SAP HANA 배포를 실행 중인의 hello 목적을 위해 완전 하드웨어 S/4HANA 또는 다른 SAP HANA 워크 로드에 대 한 메모리입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-113">In order tooenable hosting more memory and CPU resource demanding SAP scenarios involving SAP HANA, Azure offers hello usage of customer dedicated bare-metal hardware for hello purpose of running SAP HANA deployments that require up too20 TB (60 TB scale-out) of memory for S/4HANA or other SAP HANA workload.</span></span> <span data-ttu-id="54270-114">이 고유한 Azure 솔루션 (대형 인스턴스) Azure에서 SAP HANA의 hello SAP 응용 프로그램 계층 또는 기본 Azure 가상 컴퓨터에서 호스트 되는 작업 중간 웨어 계층 전용 hello 완전 하드웨어에서 SAP HANA toorun이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-114">This unique Azure solution of SAP HANA on Azure (Large Instances) allows you toorun SAP HANA on hello dedicated bare-metal hardware with hello SAP application layer or workload middle-ware layer hosted in native Azure Virtual Machines.</span></span> <span data-ttu-id="54270-115">이 솔루션은 "(대형 인스턴스) Azure에서 SAP HANA." hello 절의 여러 문서에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-115">This solution is documented in several documents in hello section "SAP HANA on Azure (Large Instances)."</span></span>   

<span data-ttu-id="54270-116">호스팅 Azure에서 SAP 작업 시나리오 또한 요구 사항 Id 통합의 및 단일 로그온 Azure Activity Directory toodifferent SAP 구성 요소 및 SAP SaaS를 사용 하 여 만들거나 PaaS 제공.</span><span class="sxs-lookup"><span data-stu-id="54270-116">Hosting SAP workload scenarios in Azure also can create requirements of Identity integration and Single-Sign-On using Azure Activity Directory toodifferent SAP components and SAP SaaS or PaaS offers.</span></span> <span data-ttu-id="54270-117">이러한 통합 및 Azure Active Directory (AAD) 및 SAP 엔터티와 단일 로그온 시나리오 목록이 설명 하 고 hello 섹션에 설명 된 "AAD SAP Id 통합 및 단일 로그온 합니다."</span><span class="sxs-lookup"><span data-stu-id="54270-117">A list of such integration and Single-Sign-On scenarios with Azure Active Directory (AAD) and SAP entities is described and documented in hello section "AAD SAP Identity Integration and Single-Sign-On."</span></span>


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a><span data-ttu-id="54270-118">Azure(큰 인스턴스)에서 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="54270-118">SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="54270-119">Azure(큰 인스턴스)에서 SAP HANA의 개요 및 아키텍처</span><span class="sxs-lookup"><span data-stu-id="54270-119">Overview and architecture of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="54270-120">제목: aaaOverview 및 Azure (대형 인스턴스)에서 아키텍처의 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="54270-120">title: aaaOverview and Architecture of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="54270-121">요약:이 아키텍처 및 기술 배포 가이드 제공 정보 toohelp에 SAP 배포 하면 Azure에서 Azure (대형 인스턴스)에서 새 SAP HANA hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-121">Summary: This Architecture and Technical Deployment Guide provides information toohelp you deploy SAP on hello new SAP HANA on Azure (Large Instances) in Azure.</span></span> <span data-ttu-id="54270-122">의도 한 toobe 포괄적인 가이드 포함 특정 설정의 SAP 솔루션 하지만 초기 배포 및 진행 중인 작업의 유용한 정보는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-122">It is not intended toobe a comprehensive guide covering specific setup of SAP solutions, but rather useful information in your initial deployment and ongoing operations.</span></span> <span data-ttu-id="54270-123">SAP 설명서를 대체 하지는 SAP HANA의 toohello 설치와 관련 된 (또는 hello hello 항목을 포함 하는 많은 SAP 지원 참고 사항).</span><span class="sxs-lookup"><span data-stu-id="54270-123">It should not replace SAP documentation related toohello installation of SAP HANA (or hello many SAP Support Notes that cover hello topic).</span></span> <span data-ttu-id="54270-124">한 개요를 제공 하 고 hello (대형 인스턴스) Azure에서 SAP HANA 설치의 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-124">It gives you an overview and provides hello additional detail of installing SAP HANA on Azure (Large Instances).</span></span>

<span data-ttu-id="54270-125">업데이트: 2017년 7월</span><span class="sxs-lookup"><span data-stu-id="54270-125">Updated: July 2017</span></span>

[<span data-ttu-id="54270-126">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-126">This guide can be found here</span></span>](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a><span data-ttu-id="54270-127">인프라 및 연결 tooSAP HANA Azure (대형 인스턴스)에서</span><span class="sxs-lookup"><span data-stu-id="54270-127">Infrastructure and connectivity tooSAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="54270-128">제목: aaaInfrastructure 및 연결 tooSAP HANA Azure (대형 인스턴스)에서</span><span class="sxs-lookup"><span data-stu-id="54270-128">title: aaaInfrastructure and Connectivity tooSAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="54270-129">요약: (대형 인스턴스) Azure에서 SAP HANA의 hello 구매, 사용자와 Microsoft 엔터프라이즈 계정 팀 hello 간에 종료한 후 다양 한 네트워크 구성은 순서 tooensure 적절 한 연결에 요구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-129">Summary: After hello purchase of SAP HANA on Azure (Large Instances) is finalized between you and hello Microsoft enterprise account team, various network configurations are required in order tooensure proper connectivity.</span></span>  <span data-ttu-id="54270-130">다음 정보는 hello와 공유 toobe가이 문서 윤곽선 hello 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-130">This document outlines hello information that has toobe shared with hello following information is required.</span></span> <span data-ttu-id="54270-131">이 문서 정보에 수집 된 toobe 있고 어떤 구성 스크립트 실행 toobe 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-131">This document outlines what information has toobe collected and what configuration scripts have toobe run.</span></span> 

<span data-ttu-id="54270-132">업데이트: 2017년 7월</span><span class="sxs-lookup"><span data-stu-id="54270-132">Updated: July 2017</span></span>

[<span data-ttu-id="54270-133">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-133">This guide can be found here</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="54270-134">Azure(큰 인스턴스)에서 SAP HANA 설치</span><span class="sxs-lookup"><span data-stu-id="54270-134">Install SAP HANA in SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="54270-135">제목: aaaInstall (대형 인스턴스) Azure에서 SAP HANA에 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="54270-135">title: aaaInstall SAP HANA on SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="54270-136">요약:이 문서에서는 Azure 대형 인스턴스에서 SAP HANA를 설치 하기 위한 hello 설정 절차를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-136">Summary: This document outlines hello setup procedures for installing SAP HANA on your Azure Large Instance.</span></span> 

<span data-ttu-id="54270-137">업데이트: 2017년 7월</span><span class="sxs-lookup"><span data-stu-id="54270-137">Updated: July 2017</span></span>

[<span data-ttu-id="54270-138">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-138">This guide can be found here</span></span>](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="54270-139">Azure(큰 인스턴스)의 SAP HANA에 대한 고가용성 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="54270-139">High availability and disaster recovery of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="54270-140">제목: aaaHigh 가용성 및 재해 복구의 SAP HANA Azure (대형 인스턴스)에서</span><span class="sxs-lookup"><span data-stu-id="54270-140">title: aaaHigh Availability and Disaster Recovery of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="54270-141">요약: Azure(큰 인스턴스) 서버에서 업무상 중요한 SAP HANA를 실행할 때 HA(고가용성) 및 DR(재해 복구)은 매우 중요한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-141">Summary: High Availability (HA) and Disaster Recovery (DR) are very important aspects of running your mission-critical SAP HANA on Azure (Large Instances) server(s).</span></span> <span data-ttu-id="54270-142">sap 가져오기 toowork, 시스템 통합 업체 및/또는 Microsoft tooproperly을 설계 하 고 드립니다 hello 오른쪽 HA/DR 전략을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-142">It's import toowork with SAP, your system integrator, and/or Microsoft tooproperly architect and implement hello right HA/DR strategy for you.</span></span> <span data-ttu-id="54270-143">복구 지점 목표 (RPO) 및 특정 tooyour 환경 복구 시간 목표 (RTO)와 같은 중요 한 고려 사항으로 간주 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-143">Important considerations like Recovery Point Objective (RPO) and Recovery Time Objective (RTO), specific tooyour environment, must be considered.</span></span>  <span data-ttu-id="54270-144">이 문서에서는 기본 수준의 HA 및 DR을 사용하도록 설정하기 위한 옵션에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-144">This document explains your options for enabling your preferred level of HA and DR.</span></span>

<span data-ttu-id="54270-145">업데이트한 날짜: 2016년 12월</span><span class="sxs-lookup"><span data-stu-id="54270-145">Updated: December 2016</span></span>

[<span data-ttu-id="54270-146">이 문서는 여기에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-146">This document can be found here</span></span>](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="54270-147">Azure(큰 인스턴스)의 SAP HANA 문제 해결 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="54270-147">Troubleshooting and monitoring of SAP HANA on Azure (Large Instances)</span></span>
<span data-ttu-id="54270-148">제목: aaaTroubleshooting 및 모니터링의 SAP HANA Azure (대형 인스턴스)에서</span><span class="sxs-lookup"><span data-stu-id="54270-148">title: aaaTroubleshooting and Monitoring of SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="54270-149">요약: 이 가이드에서는 Azure 환경에서 SAP HANA의 모니터링 설정 시 유용한 정보와 추가적인 문제 해결 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-149">Summary: This guide covers information that is useful in establishing monitoring of your SAP HANA on Azure environment as well as additional troubleshooting information.</span></span> 

<span data-ttu-id="54270-150">업데이트한 날짜: 2016년 12월</span><span class="sxs-lookup"><span data-stu-id="54270-150">Updated: December 2016</span></span>

[<span data-ttu-id="54270-151">이 문서는 여기에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-151">This document can be found here</span></span>](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a><span data-ttu-id="54270-152">Azure Virtual Machines의 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="54270-152">SAP HANA on Azure Virtual Machines</span></span>

### <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="54270-153">Azure에서 SAP HANA 시작</span><span class="sxs-lookup"><span data-stu-id="54270-153">Getting started with SAP HANA on Azure</span></span>
<span data-ttu-id="54270-154">제목: Azure Vm에서 SAP HANA의 수동 설치를 위한 aaaQuickstart 가이드</span><span class="sxs-lookup"><span data-stu-id="54270-154">title: aaaQuickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="54270-155">요약:이 퀵 스타트 가이드는 단일 인스턴스 SAP HANA 시스템을 Azure Vm에서 수동 설치를 통해 SAP NetWeaver 7.5 및 SAP HANA SP12 tooset을 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="54270-155">Summary: This quickstart guide helps tooset up a single-instance SAP HANA system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="54270-156">hello 가이드 hello 판독기가 어떻게 toodeploy 가상 컴퓨터 또는 가상 네트워크 hello Azure 포털 또는 Powershell/CLI 등을 통해 옵션 toouse json 템플릿 hello와 같은 Azure IaaS 기본 사항에 잘 알고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-156">hello guide presumes that hello reader is familiar with Azure IaaS basics like how toodeploy virtual machines or virtual networks either via hello Azure portal or Powershell/CLI including hello option toouse json templates.</span></span> <span data-ttu-id="54270-157">또한 hello 판독기가 어떻게 tooinstall 것 온-프레미스 SAP HANA, SAP NetWeaver와 친숙 한 예상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-157">Furthermore it's expected that hello reader is familiar with SAP HANA, SAP NetWeaver and how tooinstall it on-premises.</span></span>

<span data-ttu-id="54270-158">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-158">Updated: June 2017</span></span>

[<span data-ttu-id="54270-159">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-159">This guide can be found here</span></span>](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a><span data-ttu-id="54270-160">Azure에서 S/4HANA SAP CAL 배포</span><span class="sxs-lookup"><span data-stu-id="54270-160">S/4HANA SAP CAL deployment on Azure</span></span>
<span data-ttu-id="54270-161">제목: Azure에서 BW/4HANA 또는 SAP S/4HANA aaaDeploy</span><span class="sxs-lookup"><span data-stu-id="54270-161">title: aaaDeploy SAP S/4HANA or BW/4HANA on Azure</span></span>

<span data-ttu-id="54270-162">요약:이 가이드에서는 S/4HANA SAP 클라우드 어플라이언스에 라이브러리를 사용 하 여 Azure에서 SAP의 toodemonstrate hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-162">Summary: This guide helps toodemonstrate hello deployment of SAP S/4HANA on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="54270-163">SAP 클라우드 어플라이언스에 라이브러리는 sap toodeploy SAP 응용 프로그램을 Azure에서 허용 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-163">SAP Cloud Appliance Library is a service by SAP that allows toodeploy SAP applications on Azure.</span></span> <span data-ttu-id="54270-164">hello 가이드에서는 단계별 hello 배포에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-164">hello guide describes step by step hello deployment.</span></span>

<span data-ttu-id="54270-165">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-165">Updated: June 2017</span></span>

[<span data-ttu-id="54270-166">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-166">This guide can be found here</span></span>](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a><span data-ttu-id="54270-167">Azure Virtual Machines의 SAP HANA 고가용성</span><span class="sxs-lookup"><span data-stu-id="54270-167">High Availability of SAP HANA in Azure Virtual Machines</span></span>
<span data-ttu-id="54270-168">제목: aaaHigh 가용성의 SAP HANA를 Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="54270-168">title: aaaHigh Availability of SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="54270-169">요약:이 설명서는 hello SUSE 12 OS의 hello 고가용성 구성을 통해 하 고 자동 장애 조치가 있는 SAP HANA tooaccommodate HANA 시스템 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-169">Summary: This guide leads you through hello high availability configuration of hello SUSE 12 OS and SAP HANA tooaccommodate HANA System replication with automatic failover.</span></span> <span data-ttu-id="54270-170">hello 가이드는 SUSE와 Azure 가상 컴퓨터에 대 한 특정 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-170">hello guide is specific for SUSE and Azure Virtual Machines.</span></span> <span data-ttu-id="54270-171">클라우드 또는 다른 비 Azure 공용 클라우드 배포 hello 가이드 Red Hat 또는 베어 메탈 또는 개인에 대 한 아직 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-171">hello guide does not apply yet for Red Hat or bare-metal or private cloud or other non-Azure public cloud deployments.</span></span>

<span data-ttu-id="54270-172">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-172">Updated: June 2017</span></span>

[<span data-ttu-id="54270-173">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-173">This guide can be found here</span></span>](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a><span data-ttu-id="54270-174">Azure VM의 SAP HANA 백업 개요</span><span class="sxs-lookup"><span data-stu-id="54270-174">SAP HANA backup overview on Azure VMs</span></span>
<span data-ttu-id="54270-175">제목: Azure 가상 컴퓨터에서 SAP HANA에 대해 aaaBackup 가이드</span><span class="sxs-lookup"><span data-stu-id="54270-175">title: aaaBackup guide for SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="54270-176">요약: 이 가이드에서는 Azure Virtual Machines에서 SAP HANA를 실행하는 백업 가능성에 대한 기본 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-176">Summary: This guide provides basic information about backup possibilities running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="54270-177">업데이트: 2017년 3월</span><span class="sxs-lookup"><span data-stu-id="54270-177">Updated: March 2017</span></span>

[<span data-ttu-id="54270-178">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-178">This guide can be found here</span></span>](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a><span data-ttu-id="54270-179">Azure VM의 SAP HANA 파일 수준 백업</span><span class="sxs-lookup"><span data-stu-id="54270-179">SAP HANA file level backup on Azure VMs</span></span>
<span data-ttu-id="54270-180">제목: aaaSAP HANA 백업 스냅숏을 기반으로 저장소</span><span class="sxs-lookup"><span data-stu-id="54270-180">title: aaaSAP HANA backup based on storage snapshots</span></span>

<span data-ttu-id="54270-181">요약: 이 가이드에서는 Azure Virtual Machines에서 SAP HANA를 실행하는 경우 Azure VM에서 스냅숏 기반 백업을 사용하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-181">Summary: This guide provides information about using snapshot-based backups on Azure VMs when running SAP HANA on Azure Virtual Machines.</span></span>

<span data-ttu-id="54270-182">업데이트: 2017년 3월</span><span class="sxs-lookup"><span data-stu-id="54270-182">Updated: March 2017</span></span>

[<span data-ttu-id="54270-183">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-183">This guide can be found here</span></span>](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a><span data-ttu-id="54270-184">Azure VM의 SAP HANA 스냅숏 기반 백업</span><span class="sxs-lookup"><span data-stu-id="54270-184">SAP HANA snapshot based backups on Azure VMs</span></span>
<span data-ttu-id="54270-185">제목: 파일 수준에서 Azure 백업의 HANA aaaSAP</span><span class="sxs-lookup"><span data-stu-id="54270-185">title: aaaSAP HANA Azure Backup on file level</span></span>

<span data-ttu-id="54270-186">요약: 이 가이드에서는 Azure Virtual Machines에서 SAP HANA를 실행하는 SAP HANA 파일 수준 백업을 사용하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-186">Summary: This guide provides information about using SAP HANA file level backup running SAP HANA on Azure Virtual Machines</span></span>

<span data-ttu-id="54270-187">업데이트: 2017년 3월</span><span class="sxs-lookup"><span data-stu-id="54270-187">Updated: March 2017</span></span>

[<span data-ttu-id="54270-188">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-188">This guide can be found here</span></span>](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a><span data-ttu-id="54270-189">Azure Virtual Machines에서 배포된 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="54270-189">SAP NetWeaver deployed on Azure Virtual Machines</span></span>

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a><span data-ttu-id="54270-190">Azure에서 SAP CAL을 통해 Windows 및 SQL Server의 SAP IDES 시스템 배포</span><span class="sxs-lookup"><span data-stu-id="54270-190">Deploy SAP IDES system on Windows and SQL Server through SAP CAL on Azure</span></span>
<span data-ttu-id="54270-191">제목: Microsoft Azure SUSE Linux Vm에서의 SAP NetWeaver aaaTesting</span><span class="sxs-lookup"><span data-stu-id="54270-191">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="54270-192">요약:이 문서에서는 Windows와 SAP 클라우드 어플라이언스에 라이브러리를 사용 하 여 Azure에서 SQL Server에 따라 프로그램 IDE SAP 시스템의 hello 배포를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-192">Summary: This document describes hello deployment of an SAP IDES system based on Windows and SQL Server on Azure using SAP Cloud Appliance Library.</span></span> <span data-ttu-id="54270-193">SAP 클라우드 어플라이언스에 라이브러리는 Azure에서 SAP 제품의 hello 배포를 허용 하는 SAP 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-193">SAP Cloud appliance Library is an SAP service that allows hello deployment of SAP products on Azure.</span></span> <span data-ttu-id="54270-194">이 문서는 SAP IDE 시스템의 hello 배포 과정을 단계별로 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-194">This document goes step by step through hello deployment of an SAP IDES system.</span></span> <span data-ttu-id="54270-195">hello IDE 시스템은 예 시일 뿐 몇 가지 다른 여러 응용 프로그램의 Microsoft Azure에서 SAP 클라우드 어플라이언스를 통해 배포할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-195">hello IDES system is just an example for several other dozen applications that can be deployed through SAP Cloud appliance on Microsoft Azure.</span></span>

<span data-ttu-id="54270-196">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-196">Updated: June 2017</span></span>

[<span data-ttu-id="54270-197">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-197">This guide can be found here</span></span>](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="54270-198">Azure의 SUSE Linux NetWeaver에 대한 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="54270-198">Quickstart guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="54270-199">제목: Microsoft Azure SUSE Linux Vm에서의 SAP NetWeaver aaaTesting</span><span class="sxs-lookup"><span data-stu-id="54270-199">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="54270-200">요약:이 문서에서는 다양 한 가지 tooconsider Microsoft Azure SUSE Linux 가상 컴퓨터 (Vm)에서 SAP NetWeaver를 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="54270-200">Summary: This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="54270-201">SAP NetWeaver는 Azure의 SUSE Linux VM에서 공식적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-201">SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="54270-202">Linux 버전, SAP 커널 버전 및 기타 세부 정보와 관련된 모든 세부 정보는 SAP 정보 1928533, "Azure의 SAP 응용 프로그램: 지원 제품 및 Azure VM 유형"에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-202">All details regarding Linux versions, SAP kernel versions, and other details can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="54270-203">업데이트 날짜: 2016년 9월</span><span class="sxs-lookup"><span data-stu-id="54270-203">Updated: September 2016</span></span>

[<span data-ttu-id="54270-204">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-204">This guide can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="54270-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>계획 및 구현</span><span class="sxs-lookup"><span data-stu-id="54270-205"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and implementation</span></span>
<span data-ttu-id="54270-206">제목: aaaAzure 가상 컴퓨터 계획 및 SAP NetWeaver 용 구현</span><span class="sxs-lookup"><span data-stu-id="54270-206">title: aaaAzure Virtual Machines planning and implementation for SAP NetWeaver</span></span>

<span data-ttu-id="54270-207">요약:이 문서를 통해 Azure 가상 컴퓨터의 SAP NetWeaver를 실행 하는 방법에 대 한 하려는 경우와 hello 가이드 toostart는입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-207">Summary: This document is hello guide toostart with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="54270-208">이 계획 및 구현 가이드를 사용 하면는 기존 또는 계획 된 SAP NetWeaver 기반 시스템 tooan 배포 된 Azure 가상 컴퓨터 환경 수 있는지 여부를 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-208">This planning and implementation guide helps you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed tooan Azure Virtual Machines environment.</span></span> <span data-ttu-id="54270-209">여러 SAP NetWeaver 배포 시나리오에 설명 하 고 특정 tooAzure는 SAP 구성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-209">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific tooAzure.</span></span> <span data-ttu-id="54270-210">hello 용지를 나열 하 고 hello 필요한 구성의 모든 정보 필요한 SAP/Azure 측면 toorun는 하이브리드 SAP 환경 hello 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-210">hello paper lists and describes all hello necessary configuration information you’ll need on hello SAP/Azure side toorun a hybrid SAP landscape.</span></span> <span data-ttu-id="54270-211">IaaS에서 SAP NetWeaver 기반 시스템의 고가용성 tooensure 취할 수 함께 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-211">Measures you can take tooensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="54270-212">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-212">Updated: June 2017</span></span>

<span data-ttu-id="54270-213">[이 가이드는 여기서 확인할 수 있습니다.][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="54270-213">[This guide can be found here][planning-guide]</span></span>

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="54270-214">Azure VM에서 SAP NetWeaver의 고가용성 구성</span><span class="sxs-lookup"><span data-stu-id="54270-214">High Availability configurations of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="54270-215">제목: aaaAzure SAP NetWeaver 용 고가용성 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="54270-215">title: aaaAzure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="54270-216">요약:이 문서에서 다룰 수행할 수 있는 toodeploy SAP 시스템 가용성이 높은 Azure의 hello Azure 리소스 관리자 배포 모델을 사용 하 여 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-216">Summary: In this document, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="54270-217">다음과 같은 주요 작업을 진행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-217">We walk you through these major tasks.</span></span> <span data-ttu-id="54270-218">어떻게 단일---오류 지점 구성 요소와 같은 고급 비즈니스 응용 프로그램 프로그래밍 (ABAP) SAP 중앙 서비스 (ASCS) hello 문서에서 설명 SAP 중앙 서비스 SCS () 및 데이터베이스 관리 시스템 (DBMS)와 중복 구성 요소 등의 SAP / 응용 프로그램 서버 toobe Azure Vm에서 실행 되 면 보호 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-218">In hello document, we describe how single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server are going toobe protected when running in Azure VMs.</span></span> <span data-ttu-id="54270-219">이 문서에서는 Azure의 Windows Server 장애 조치 클러스터링 클러스터에서 고가용성 SAP 시스템을 설치하고 구성하는 단계별 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="54270-219">A step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure is demonstrated and shown in this document.</span></span>

<span data-ttu-id="54270-220">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-220">Updated: June 2017</span></span>

[<span data-ttu-id="54270-221">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-221">This guide can be found here</span></span>](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a><span data-ttu-id="54270-222">Azure VM에서 SAP NetWeaver의 다중 SID 배포 인식</span><span class="sxs-lookup"><span data-stu-id="54270-222">Realizing Multi-SID deployments of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="54270-223">제목: aaaCreate SAP NetWeaver 다중 SID 구성</span><span class="sxs-lookup"><span data-stu-id="54270-223">title: aaaCreate an SAP NetWeaver multi-SID configuration</span></span> 

<span data-ttu-id="54270-224">요약:이 문서는 Azure Vm에서의 SAP NetWeaver의 고가용성에는 추가 toohello 문서.</span><span class="sxs-lookup"><span data-stu-id="54270-224">Summary: This document is an addition toohello document High availability for SAP NetWeaver on Azure VMs.</span></span> <span data-ttu-id="54270-225">2016 년 9 월에에서 도입 된 Azure에서 toonew 기능을 인해 것이 가능한 toodeploy 한 쌍의 Azure Vm에 여러 SAP NetWeaver ASCS/SCS 인스턴스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-225">Due toonew functionality in Azure that got introduced in September 2016, it is possible toodeploy multiple SAP NetWeaver ASCS/SCS instances in a pair of Azure VMs.</span></span> <span data-ttu-id="54270-226">이러한 구성을 사용 하 여 Vm 필요한 toodeploy toorealize 항상 사용 가능한 SAP NetWeaver 구성 hello 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-226">With such a configuration, you can reduce hello number of VMs necessary toodeploy toorealize highly available SAP NetWeaver configurations.</span></span> <span data-ttu-id="54270-227">이러한 SID 다중 구성의 hello 설정을 설명 하는 hello 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-227">hello guide describes hello setup of such multi-SID configurations.</span></span>

<span data-ttu-id="54270-228">업데이트한 날짜: 2016년 12월</span><span class="sxs-lookup"><span data-stu-id="54270-228">Updated: December 2016</span></span>

[<span data-ttu-id="54270-229">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-229">This guide can be found here</span></span>](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <span data-ttu-id="54270-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Azure VM에서 SAP NetWeaver 배포</span><span class="sxs-lookup"><span data-stu-id="54270-230"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment of SAP NetWeaver in Azure VMs</span></span>
<span data-ttu-id="54270-231">제목: aaaAzure SAP NetWeaver 용 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="54270-231">title: aaaAzure Virtual Machines deployment for SAP NetWeaver</span></span>

<span data-ttu-id="54270-232">요약:이 문서에서는 Azure의 SAP NetWeaver 소프트웨어 toovirtual 컴퓨터를 배포 하기 위한 절차 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-232">Summary: This document provides procedural guidance for deploying SAP NetWeaver software toovirtual machines in Azure.</span></span> <span data-ttu-id="54270-233">이 백서에서는 세 가지 특정 배포 시나리오 hello SAP 용 Azure 모니터링 확장에 대 한 권장 문제 해결 방법을 비롯 한 SAP 용 hello Azure 모니터링 확장 사용에 중점을 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-233">This paper focuses on three specific deployment scenarios, with an emphasis on enabling hello Azure Monitoring Extensions for SAP, including troubleshooting recommendations for hello Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="54270-234">이 문서를 읽은 hello 계획 및 구현 가이드를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-234">This paper assumes that you’ve read hello planning and implementation guide.</span></span>

<span data-ttu-id="54270-235">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-235">Updated: June 2017</span></span>

<span data-ttu-id="54270-236">[이 가이드는 여기서 확인할 수 있습니다.][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="54270-236">[This guide can be found here][deployment-guide]</span></span>

### <span data-ttu-id="54270-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="54270-237"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS deployment guide</span></span>
<span data-ttu-id="54270-238">제목: aaaAzure SAP NetWeaver 용 가상 컴퓨터 DBMS 배포</span><span class="sxs-lookup"><span data-stu-id="54270-238">title: aaaAzure Virtual Machines DBMS deployment for SAP NetWeaver</span></span>

<span data-ttu-id="54270-239">요약:이 백서에서는 SAP와 함께에서 실행 해야 하는 hello DBMS 시스템에 대 한 계획 및 구현 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-239">Summary: This paper covers planning and implementation considerations for hello DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="54270-240">일반적인 고려 사항 hello 첫 번째 부분에 나열 되어 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-240">In hello first part, general considerations are listed and presented.</span></span> <span data-ttu-id="54270-241">hello hello 문서의 다음 부분과 관련 SAP에서 지 원하는 Azure의 여러 dbms toodeployments 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-241">hello following parts of hello paper relate toodeployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="54270-242">제공되는 DBMS는 SQL Server, SAP ASE 및 Oracle입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-242">Different DBMS presented are SQL Server, SAP ASE, and Oracle.</span></span> <span data-ttu-id="54270-243">해당 특정 부품을 실행 하는 경우 SAP 시스템 Azure에서 해당 DBMS와 함께에서 대 한 tooaccount 있는 고려 사항에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-243">In those specific parts, considerations you have tooaccount for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="54270-244">주제 같은 다른 DBMS Azure에서 SAP 응용 프로그램과 함께 hello 사용에 대해 제공 됩니다 hello에서 지원 되는 백업 및 고가용성 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-244">Subjects like backup and high availability methods that are supported by hello different DBMS on Azure are presented for hello usage with SAP applications.</span></span>

<span data-ttu-id="54270-245">업데이트: 2017년 6월</span><span class="sxs-lookup"><span data-stu-id="54270-245">Updated: June 2017</span></span>

<span data-ttu-id="54270-246">[이 가이드는 여기서 확인할 수 있습니다.][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="54270-246">[This guide can be found here][dbms-guide]</span></span>

### <a name="using-azure-site-recovery-for-sap-workload"></a><span data-ttu-id="54270-247">SAP 워크로드를 위한 Azure Site Recovery 사용</span><span class="sxs-lookup"><span data-stu-id="54270-247">Using Azure Site Recovery for SAP workload</span></span>
<span data-ttu-id="54270-248">제목: aaaSAP NetWeaver: Azure Site Recovery와 재해 복구 솔루션 구축</span><span class="sxs-lookup"><span data-stu-id="54270-248">title: aaaSAP NetWeaver: Building a Disaster Recovery Solution with Azure Site Recovery</span></span> 

<span data-ttu-id="54270-249">요약:이 문서에서는 hello 방식으로 재해 복구 시나리오의 hello 목적을 위해 Azure 사이트 복구 서비스를 사용할 수 있는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="54270-249">Summary: This document describes hello way how Azure Site Recovery services can be used for hello purpose of handling disaster recovery scenarios.</span></span> <span data-ttu-id="54270-250">Azure Site Recovery Services를 사용하여 온-프레미스 SAP 지형의 재해 복구 위치로 Azure를 사용하는 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="54270-250">Cases where Azure is used as disaster recovery location for an on-premise SAP landscape using Azure Site Recovery Services.</span></span> <span data-ttu-id="54270-251">Hello 문서에서 설명 하는 또 다른 시나리오 hello Aure Azure (A2A) 재해 복구 대/소문자 및 Azure 사이트 복구와 관리 방법이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54270-251">Another scenario described in hello document is hello Aure-to-Azure (A2A) disaster recovery case and how it is managed with Azure Site Recovery.</span></span>  

<span data-ttu-id="54270-252">업데이트 날짜: 2017년 8월</span><span class="sxs-lookup"><span data-stu-id="54270-252">Updated: August 2017</span></span>

[<span data-ttu-id="54270-253">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54270-253">This guide can be found here</span></span>](http://aka.ms/asr-sap)

