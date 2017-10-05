---
title: "Azure의 Windows VM에서 SAP 시작 | Microsoft Docs"
description: "Microsoft Azure의 VM(가상 컴퓨터)에서 실행되는 SAP 솔루션에 대한 자세한 정보"
services: virtual-machines-windows
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e714c47-add3-44c5-a6c8-9d26472ddcc4
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ebe420ea5105fb15e42ff32ad7e8d9d8b27d8b06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-azure-windows-virtual-machines-vms"></a><span data-ttu-id="9afa5-103">Azure Windows VM(가상 컴퓨터)에서 SAP 사용</span><span class="sxs-lookup"><span data-stu-id="9afa5-103">Using SAP on Azure Windows Virtual Machines (VMs)</span></span>
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

[azure-cli]:../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../azure-subscription-service-limits.md#subscription

[dbms-guide]:../virtual-machines-windows-sap-dbms-guide.md 
[dbms-guide-2.1]:../virtual-machines-windows-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:../virtual-machines-windows-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91
[dbms-guide-2.3]:../virtual-machines-windows-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:../virtual-machines-windows-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:../virtual-machines-windows-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:../virtual-machines-windows-sap-dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:../virtual-machines-windows-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:../virtual-machines-windows-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8
[dbms-guide-5.8]:../virtual-machines-windows-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30
[dbms-guide-5]:../virtual-machines-windows-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737
[dbms-guide-8.4.1]:../virtual-machines-windows-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:../virtual-machines-windows-sap-dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d
[dbms-guide-8.4.3]:../virtual-machines-windows-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c
[dbms-guide-8.4.4]:../virtual-machines-windows-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818
[dbms-guide-900-sap-cache-server-on-premises]:../virtual-machines-windows-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:sap-deployment-guide.md  
[deployment-guide-2.2]:sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab
[deployment-guide-3.2]:sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281
[deployment-guide-3.3]:sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2
[deployment-guide-3.4]:sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e
[deployment-guide-4.1]:sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7
[deployment-guide-4.2]:sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e
[deployment-guide-4.3]:sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:sap-deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1
[deployment-guide-5.3]:sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8

[deployment-guide-configure-monitoring-scenario-1]:sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 

[deploy-template-cli]:../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:virtual-machines-windows-../linux/classic/sap-get-started.md
[getting-started-dbms]:virtual-machines-windows-../linux/classic/sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:virtual-machines-windows-../linux/classic/sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:virtual-machines-windows-../linux/classic/sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md
[getting-started-windows-classic-dbms]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:virtual-machines-windows-classic-../linux/classic/sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:sap-planning-guide.md  
[planning-guide-1.2]:sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11.4.1]:sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77
[planning-guide-11.5]:sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f
[planning-guide-2.1]:sap-planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10
[planning-guide-3.1]:sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:sap-planning-guide.md#18810088-f9be-4c97-958a-27996255c665
[planning-guide-3.2]:sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77
[planning-guide-3.3.2]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92
[planning-guide-5.1.1]:sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53
[planning-guide-5.1.2]:sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c
[planning-guide-5.2.1]:sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef
[planning-guide-5.2.2]:sap-planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3
[planning-guide-5.2]:sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7
[planning-guide-5.3.1]:sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a
[planning-guide-5.4.2]:sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:sap-planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646
[planning-guide-5.5.3]:sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30
[planning-guide-7]:sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14
[planning-guide-9.1]:sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3
[planning-guide-azure-premium-storage]:sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92

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
[planning-guide-microsoft-azure-networking]:sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd 
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[powershell-install-configure]:/powershell/azureps-cmdlets-docs
[resource-group-authoring-templates]:../../resource-group-authoring-templates.md
[resource-group-overview]:../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam 
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
[virtual-machines-linux-cli-deploy-templates]:../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../virtual-machines-windows-ps-manage.md 
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

<span data-ttu-id="9afa5-104">SAP 준비 클라우드 파트너로 Microsoft Azure를 선택하여 중요 업무용 SAP 워크로드를 확장 가능하고 규정을 준수하는 엔터프라이즈 입증 플랫폼에서 안정적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-104">By choosing Microsoft Azure as your SAP ready cloud partner, you will be able to reliably run your mission critical SAP workloads on a scaaleable, compliant, and enterprise-proven platform.</span></span>  <span data-ttu-id="9afa5-105">Azure의 확장성, 유연성 및 비용 절감 효과를 활용하세요.</span><span class="sxs-lookup"><span data-stu-id="9afa5-105">Get the scaleability, flexability, and cost savings of Azure.</span></span> <span data-ttu-id="9afa5-106">Microsoft와 SAP 사이의 확장된 파트너 관계 덕분에 Azure에서 개발/테스트 및 프로덕션 시나리오 전체에서 SAP 응용 프로그램을 실행할 수 있으며 완전한 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-106">With the expanded partnership between Microsoft and SAP, you can run SAP applications across dev/test and production scenarios in azure - and be fully supported.</span></span> <span data-ttu-id="9afa5-107">SAP NetWeaver에서 SAP S4/HANA로, Linux에서 Windows로, SAP HANA에서 SQL로, 모두 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-107">From SAP NetWeaver to SAP S4/HANA, Linux to Windows, SAP HANA to SQL, we have you covered.</span></span> 

<span data-ttu-id="9afa5-108">Microsoft Azure 가상 컴퓨터 서비스 및 Azure 큰 인스턴스의 SAP HANA와 함께 Microsoft는 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-108">With Microsoft Azure virtual machine services, and SAP HANA on Azure large instances, Microsoft offers a comprehensive Infrastructure As A Service (IaaS) platform.</span></span> <span data-ttu-id="9afa5-109">Azure에서는 다양한 SAP 솔루션이 지원되므로 이 "시작 문서"는 최신 SAP 문서 모음에 대한 목차 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-109">Because a wide range of SAP solutions are supported on Azure, this "getting started document will serve as a Table of Contents for our current set of SAP documents.</span></span> <span data-ttu-id="9afa5-110">더 많은 제목이 문서 라이브러리에 추가되면 여기에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-110">As more titles get added to our document library - you will see them added here.</span></span> 

## <a name="sap-hana-certifications-on-microsoft-azure"></a><span data-ttu-id="9afa5-111">Microsoft Azure의 SAP HANA 인증</span><span class="sxs-lookup"><span data-stu-id="9afa5-111">SAP HANA Certifications on Microsoft Azure</span></span>
| <span data-ttu-id="9afa5-112">SAP 제품</span><span class="sxs-lookup"><span data-stu-id="9afa5-112">SAP Product</span></span> | <span data-ttu-id="9afa5-113">지원되는 OS</span><span class="sxs-lookup"><span data-stu-id="9afa5-113">Supported OS</span></span> | <span data-ttu-id="9afa5-114">Azure 제품</span><span class="sxs-lookup"><span data-stu-id="9afa5-114">Azure Offerings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9afa5-115">SAP HANA Developer Edition(SQLODBC, ODBO(Windows 전용), ODBC, JDBC 드라이버로 구성된 HANA Client 소프트웨어, HANA Studio, HANA Database 포함)</span><span class="sxs-lookup"><span data-stu-id="9afa5-115">SAP HANA Developer Edition (including the HANA client software comprised of SQLODBC, ODBO-Windows only, ODBC, JDBC drivers, HANA studio, and HANA database)</span></span> |<span data-ttu-id="9afa5-116">Red Hat Enterprise Linux, SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="9afa5-116">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="9afa5-117">A7, A8</span><span class="sxs-lookup"><span data-stu-id="9afa5-117">A7, A8</span></span> |
| <span data-ttu-id="9afa5-118">MHANA One</span><span class="sxs-lookup"><span data-stu-id="9afa5-118">MHANA One</span></span> |<span data-ttu-id="9afa5-119">Red Hat Enterprise Linux, SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="9afa5-119">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="9afa5-120">DS14_v2(일반 공급 시)</span><span class="sxs-lookup"><span data-stu-id="9afa5-120">DS14_v2 (upon general availability)</span></span> |
| <span data-ttu-id="9afa5-121">SAP S/4HANA</span><span class="sxs-lookup"><span data-stu-id="9afa5-121">SAP S/4HANA</span></span> |<span data-ttu-id="9afa5-122">Red Hat Enterprise Linux, SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="9afa5-122">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="9afa5-123">GS5의 제어되는 가용성, Azure(큰 인스턴스)에서 SAP HANA 사용</span><span class="sxs-lookup"><span data-stu-id="9afa5-123">Controlled Availability for GS5, SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="9afa5-124">Suite on HANA, OLTP</span><span class="sxs-lookup"><span data-stu-id="9afa5-124">Suite on HANA, OLTP</span></span> |<span data-ttu-id="9afa5-125">Red Hat Enterprise Linux, SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="9afa5-125">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="9afa5-126">Azure(큰 인스턴스)에서 SAP HANA 사용</span><span class="sxs-lookup"><span data-stu-id="9afa5-126">SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="9afa5-127">HANA Enterprise for BW, OLAP</span><span class="sxs-lookup"><span data-stu-id="9afa5-127">HANA Enterprise for BW, OLAP</span></span> |<span data-ttu-id="9afa5-128">Red Hat Enterprise Linux, SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="9afa5-128">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="9afa5-129">단일 노드 배포의 GS5, Azure(큰 인스턴스)에서 SAP HANA 사용</span><span class="sxs-lookup"><span data-stu-id="9afa5-129">GS5 for single node deployments, SAP HANA on Azure (Large instances)</span></span> |
| <span data-ttu-id="9afa5-130">SAP BW/4HANA</span><span class="sxs-lookup"><span data-stu-id="9afa5-130">SAP BW/4HANA</span></span> |<span data-ttu-id="9afa5-131">Red Hat Enterprise Linux, SUSE Linux Enterprise</span><span class="sxs-lookup"><span data-stu-id="9afa5-131">Red Hat Enterprise Linux, SUSE Linux Enterprise</span></span> |<span data-ttu-id="9afa5-132">단일 노드 배포의 GS5, Azure(큰 인스턴스)에서 SAP HANA 사용</span><span class="sxs-lookup"><span data-stu-id="9afa5-132">GS5 for single node deployments, SAP HANA on Azure (Large instances)</span></span> |

## <a name="sap-netweaver-certifications"></a><span data-ttu-id="9afa5-133">SAP NetWeaver 인증</span><span class="sxs-lookup"><span data-stu-id="9afa5-133">SAP NetWeaver Certifications</span></span>
<span data-ttu-id="9afa5-134">Microsoft Azure는 다음과 같은 SAP 제품에서 인증되었고 Microsoft와 SAP의 전폭적인 지원을 받고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-134">Microsoft Azure is certified for the following SAP products, with full support from Microsoft and SAP.</span></span>

| <span data-ttu-id="9afa5-135">SAP 제품</span><span class="sxs-lookup"><span data-stu-id="9afa5-135">SAP Product</span></span> | <span data-ttu-id="9afa5-136">게스트 OS</span><span class="sxs-lookup"><span data-stu-id="9afa5-136">Guest OS</span></span> | <span data-ttu-id="9afa5-137">RDBMS</span><span class="sxs-lookup"><span data-stu-id="9afa5-137">RDBMS</span></span> | <span data-ttu-id="9afa5-138">가상 컴퓨터 유형</span><span class="sxs-lookup"><span data-stu-id="9afa5-138">Virtual Machine Types</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9afa5-139">SAP Business Suite 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="9afa5-139">SAP Business Suite Software</span></span> |<span data-ttu-id="9afa5-140">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="9afa5-140">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="9afa5-141">SQL Server, Oracle(Windows만 해당), DB2, SAP ASE</span><span class="sxs-lookup"><span data-stu-id="9afa5-141">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="9afa5-142">A5~A11, D11~D14, DS11~DS14, GS1~GS5</span><span class="sxs-lookup"><span data-stu-id="9afa5-142">A5 to A11, D11 to D14, DS11 to DS14, GS1 to GS5</span></span> |
| <span data-ttu-id="9afa5-143">SAP Business All-in-One</span><span class="sxs-lookup"><span data-stu-id="9afa5-143">SAP Business All-in-One</span></span> |<span data-ttu-id="9afa5-144">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="9afa5-144">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="9afa5-145">SQL Server, Oracle(Windows만 해당), DB2, SAP ASE</span><span class="sxs-lookup"><span data-stu-id="9afa5-145">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="9afa5-146">A5~A11, D11~D14, DS11~DS14, GS1~GS5</span><span class="sxs-lookup"><span data-stu-id="9afa5-146">A5 to A11, D11 to D14, DS11 to DS14, GS1 to GS5</span></span> |
| <span data-ttu-id="9afa5-147">SAP BusinessObjects BI</span><span class="sxs-lookup"><span data-stu-id="9afa5-147">SAP BusinessObjects BI</span></span> |<span data-ttu-id="9afa5-148">Windows</span><span class="sxs-lookup"><span data-stu-id="9afa5-148">Windows</span></span> |<span data-ttu-id="9afa5-149">해당 없음</span><span class="sxs-lookup"><span data-stu-id="9afa5-149">N/A</span></span> |<span data-ttu-id="9afa5-150">A5~A11, D11~D14, DS11~DS14, GS1~GS5</span><span class="sxs-lookup"><span data-stu-id="9afa5-150">A5 to A11, D11 to D14, DS11 to DS14, GS1 to GS5</span></span> |
| <span data-ttu-id="9afa5-151">SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="9afa5-151">SAP NetWeaver</span></span> |<span data-ttu-id="9afa5-152">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="9afa5-152">Windows, SUSE Linux Enterprise, Red Hat Enterprise Linux</span></span> |<span data-ttu-id="9afa5-153">SQL Server, Oracle(Windows만 해당), DB2, SAP ASE</span><span class="sxs-lookup"><span data-stu-id="9afa5-153">SQL Server, Oracle (Windows only), DB2, SAP ASE</span></span> |<span data-ttu-id="9afa5-154">A5~A11, D11~D14, DS11~DS14, GS1~GS5</span><span class="sxs-lookup"><span data-stu-id="9afa5-154">A5 to A11, D11 to D14, DS11 to DS14, GS1 to GS5</span></span> |

## <a name="getting-started-with-sap-hana-on-azure"></a><span data-ttu-id="9afa5-155">Azure에서 SAP HANA 시작</span><span class="sxs-lookup"><span data-stu-id="9afa5-155">Getting Started with SAP HANA on Azure</span></span>
<span data-ttu-id="9afa5-156">제목: Azure VM에서 SAP HANA 수동 설치에 대한 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-156">Title: Quickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="9afa5-157">요약: 이 빠른 시작 가이드를 사용하면 SAP NetWeaver 7.5 및 SAP HANA SP12를 수동으로 설치하여 Azure VM에서 단일 인스턴스 SAP HANA 프로토타입/데모 시스템을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-157">Summary: This quickstart guide will help to set up a single-instance SAP HANA prototype/demo system on Azure VMs by a manual installation of SAP NetWeaver 7.5 and SAP HANA SP12.</span></span> <span data-ttu-id="9afa5-158">이 가이드는 독자가 JSON 템플릿 사용 옵션을 포함하여 Azure Portal 또는 Powershell/CLI를 통한 가상 컴퓨터나 가상 네트워크 배포 방법과 같은 Azure IaaS 기본 사항에 대해 잘 알고 있다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-158">The guide presumes that the reader is familiar with Azure IaaS basics like how to deploy virtual machines or virtual networks either via the Azure portal or Powershell/CLI including the option to use json templates.</span></span> <span data-ttu-id="9afa5-159">또한 독자가 SAP HANA, SAP NetWeaver 및 온-프레미스 설치 방법에 익숙하고</span><span class="sxs-lookup"><span data-stu-id="9afa5-159">Furthermore it's expected that the reader is familiar with SAP HANA, SAP NetWeaver and how to install it on-premises.</span></span>

<span data-ttu-id="9afa5-160">업데이트 날짜: 2016년 9월</span><span class="sxs-lookup"><span data-stu-id="9afa5-160">Updated: September 2016</span></span>

[<span data-ttu-id="9afa5-161">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-161">This guide can be found here</span></span>](../virtual-machines-linux-sap-hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a><span data-ttu-id="9afa5-162">Azure의 SUSE Linux NetWeaver에 대한 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-162">Quickstart Guide for NetWeaver on SUSE Linux on Azure</span></span>
<span data-ttu-id="9afa5-163">제목: Microsoft Azure SUSE Linux VM에서 SAP NetWeaver 테스트</span><span class="sxs-lookup"><span data-stu-id="9afa5-163">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span> 

<span data-ttu-id="9afa5-164">요약: 이 문서에서는 Microsoft Azure SUSE Linux VM(가상 컴퓨터)에서 SAP NetWeaver를 실행할 때 고려해야 할 다양한 항목을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-164">Summary: This article describes various things to consider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="9afa5-165">2016년 5월 19일을 기준으로 SAP NetWeaver는 Azure의 SUSE Linux VM에서 공식적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-165">As of May 19 2016 SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="9afa5-166">Linux 버전, SAP 커널 버전 등과 관련된 모든 세부 정보는 SAP 정보 1928533, "Azure의 SAP 응용 프로그램: 지원 제품 및 Azure VM 유형"에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-166">All details regarding Linux versions, SAP kernel versions and so on can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>

<span data-ttu-id="9afa5-167">업데이트 날짜: 2016년 9월</span><span class="sxs-lookup"><span data-stu-id="9afa5-167">Updated: September 2016</span></span>

[<span data-ttu-id="9afa5-168">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-168">This guide can be found here</span></span>](../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deploying-sap-ides-ehp7-sp3-for-sap-erp-60-on-microsoft-azure"></a><span data-ttu-id="9afa5-169">Microsoft Azure에서 SAP IDES EHP7 SP3 for SAP ERP 6.0 배포</span><span class="sxs-lookup"><span data-stu-id="9afa5-169">Deploying SAP IDES EHP7 SP3 for SAP ERP 6.0 on Microsoft Azure</span></span>
<span data-ttu-id="9afa5-170">제목: Azure VM에서 SAP HANA 수동 설치에 대한 빠른 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-170">Title: Quickstart guide for manual installation of SAP HANA on Azure VMs</span></span>

<span data-ttu-id="9afa5-171">요약: 이 문서에서는 SAP 클라우드 어플라이언스 라이브러리 3.0을 통해 Microsoft Azure에서 SQL Server 및 Windows OS와 함께 실행되는 SAP IDES를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-171">Summary: This article describes how to deploy SAP IDES running with SQL Server and Windows OS on Microsoft Azure via SAP Cloud Appliance Library 3.0.</span></span> 

<span data-ttu-id="9afa5-172">업데이트 날짜: 2016년 9월</span><span class="sxs-lookup"><span data-stu-id="9afa5-172">Updated: September 2016</span></span>

[<span data-ttu-id="9afa5-173">이 가이드는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-173">This guide can be found here</span></span>](sap-cal-ides-erp6-ehp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <span data-ttu-id="9afa5-174"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>계획 및 구현</span><span class="sxs-lookup"><span data-stu-id="9afa5-174"><a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Planning and Implementation</span></span>
<span data-ttu-id="9afa5-175">제목: Azure VM(Virtual Machines)에서 SAP NetWeaver - 계획 및 구현 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-175">Title: SAP NetWeaver on Azure Virtual Machines (VMs) – Planning and Implementation Guide</span></span>

<span data-ttu-id="9afa5-176">요약: Azure 가상 컴퓨터에서 SAP NetWeaver를 실행하는 것을 고려하는 경우 시작하기 위한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-176">Summary: This is the paper to start with if you are thinking about running SAP NetWeaver in Azure Virtual Machines.</span></span> <span data-ttu-id="9afa5-177">이 계획 및 구현 가이드를 사용하면 기존 또는 계획된 SAP NetWeaver 기반 시스템을 Azure 가상 컴퓨터 환경에 배포할 수 있는지 여부를 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-177">This planning and implementation guide will help you evaluate whether an existing or planned SAP NetWeaver-based system can be deployed to an Azure Virtual Machines environment.</span></span> <span data-ttu-id="9afa5-178">여러 SAP NetWeaver 배포 시나리오를 다루며 Azure에 고유한 SAP 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-178">It covers multiple SAP NetWeaver deployment scenarios, and includes SAP configurations that are specific to Azure.</span></span> <span data-ttu-id="9afa5-179">문서는 SAP/Azure 측면에서 하이브리드 SAP 환경을 실행하는 데 필요한 모든 구성 정보를 나열하고 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-179">The paper lists and describes all the necessary configuration information you’ll need on the SAP/Azure side to run a hybrid SAP landscape.</span></span> <span data-ttu-id="9afa5-180">IaaS에서 SAP NetWeaver 기반 시스템의 고가용성을 보장하기 위해 수행할 수 있는 측정값에 대해서도 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-180">Measures you can take to ensure high availability of SAP NetWeaver-based systems on IaaS are also covered.</span></span>

<span data-ttu-id="9afa5-181">업데이트 날짜: 2016년 8월</span><span class="sxs-lookup"><span data-stu-id="9afa5-181">Updated: August 2016</span></span>

<span data-ttu-id="9afa5-182">[이 가이드는 여기서 확인할 수 있습니다.][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="9afa5-182">[This guide can be found here][planning-guide]</span></span>

## <span data-ttu-id="9afa5-183"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>배포</span><span class="sxs-lookup"><span data-stu-id="9afa5-183"><a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Deployment</span></span>
<span data-ttu-id="9afa5-184">제목: Azure VM(Virtual Machines)에서 SAP NetWeaver - 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-184">Title: SAP NetWeaver on Azure Virtual Machines (VMs) – Deployment Guide</span></span>

<span data-ttu-id="9afa5-185">요약: 이 문서에서는 Azure의 가상 컴퓨터에 SAP NetWeaver 소프트웨어를 배포하기 위한 절차 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-185">Summary: This document provides procedural guidance for deploying SAP NetWeaver software to virtual machines in Azure.</span></span> <span data-ttu-id="9afa5-186">이 문서에서는 SAP용 Azure 모니터링 확장에 대한 권장 문제 해결 방법을 비롯한 SAP용 Azure 모니터링 확장 사용을 중점적으로 세 가지 특정 배포 시나리오에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-186">This paper focuses on three specific deployment scenarios, with an emphasis on enabling the Azure Monitoring Extensions for SAP, including troubleshooting recommendations for the Azure Monitoring Extensions for SAP.</span></span> <span data-ttu-id="9afa5-187">이 문서에서는 계획 및 구현 가이드를 읽은 것을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-187">This paper assumes that you’ve read the planning and implementation guide.</span></span>

<span data-ttu-id="9afa5-188">업데이트한 날짜: 2016년 12월</span><span class="sxs-lookup"><span data-stu-id="9afa5-188">Updated: December 2016</span></span>

<span data-ttu-id="9afa5-189">[이 가이드는 여기서 확인할 수 있습니다.][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="9afa5-189">[This guide can be found here][deployment-guide]</span></span>

## <span data-ttu-id="9afa5-190"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-190"><a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>DBMS Deployment Guide</span></span>
<span data-ttu-id="9afa5-191">제목: Azure VM(Virtual Machines)에서 SAP NetWeaver - DBMS 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-191">Title: SAP NetWeaver on Azure Virtual Machines (VMs) – DBMS Deployment Guide</span></span>

<span data-ttu-id="9afa5-192">요약: 이 문서에서는 SAP와 함께 실행해야 하는 DBMS 시스템에 대한 계획 및 구현 고려 사항을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-192">Summary: This paper covers planning and implementation considerations for the DBMS systems that should run in conjunction with SAP.</span></span> <span data-ttu-id="9afa5-193">첫 번째 부분에서는 일반적인 고려 사항이 나열되고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-193">In the first part, general considerations are listed and presented.</span></span> <span data-ttu-id="9afa5-194">문서의 다음 부분은 SAP에서 지원되는 Azure의 여러 DBMS 배포와 관련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-194">The following parts of the paper relate to deployments of different DBMS in Azure that are supported by SAP.</span></span> <span data-ttu-id="9afa5-195">제공되는 DBMS은 SQL Server, SAP ASE 및 Oracle입니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-195">Different DBMS presented are SQL Server, SAP ASE and Oracle.</span></span> <span data-ttu-id="9afa5-196">해당 특정 부분 고려 사항에서 설명된 DBMS와 함께 Azure에서 SAP를 실행 중인 경우에 대해 설명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-196">In those specific parts considerations you have to account for when you are running SAP systems on Azure in conjunction with those DBMS are discussed.</span></span> <span data-ttu-id="9afa5-197">Azure의 각 DMS에서 지원되는 백업 및 고가용성 방법과 같은 주제가 SAP 응용 프로그램과 함께 사용하기 위해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-197">Subjects like backup and high availability methods that are supported by the different DBMS on Azure are presented for the usage with SAP applications.</span></span>

<span data-ttu-id="9afa5-198">업데이트 날짜: 2016년 8월</span><span class="sxs-lookup"><span data-stu-id="9afa5-198">Updated: August 2016</span></span>

<span data-ttu-id="9afa5-199">[이 가이드는 여기서 확인할 수 있습니다.][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="9afa5-199">[This guide can be found here][dbms-guide]</span></span>

## <span data-ttu-id="9afa5-200"><a name="63dab028-2c4f-4636-8f99-90bbb264eaba"></a>고가용성 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-200"><a name="63dab028-2c4f-4636-8f99-90bbb264eaba"></a>High Availability Deployment Guide</span></span>
<span data-ttu-id="9afa5-201">제목: Azure VM(Virtual Machines)에서 SAP NetWeaver - 고가용성 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="9afa5-201">Title: SAP NetWeaver on Azure Virtual Machines (VMs) – High Availability Deployment Guide</span></span>

<span data-ttu-id="9afa5-202">요약: 이 문서에서는 Azure에서 SAP ASCS/SCS 및 DBMS와 같은 SAP 단일 실패 지점 구성 요소를 보호하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-202">Summary: This document describes how SAP single point of failure components like the SAP ASCS/SCS and DBMS can be protected in Azure.</span></span> <span data-ttu-id="9afa5-203">SAP ASCS/SCS, DBMS 및 응용 프로그램 서버의 구성 요소는 SAP NetWeaver 시스템(예: SAP NetWeaver ABAP, SAP NetWeaver Java, SAP NetWeaver ABAP+Java 시스템)의 기능에 필수적입니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-203">Components of the SAP ASCS/SCS, DBMS and application servers are essential for the functionality of SAP NetWeaver systems, e.g. SAP NetWeaver ABAP, SAP NetWeaver Java, SAP NetWeaver ABAP+Java systems.</span></span> <span data-ttu-id="9afa5-204">따라서 고가용성 기능은 해당 구성 요소가 운영 체제 미설치 및 Hyper-V 환경에 대한 Windows 클러스터 구성으로 실행된 것처럼 서버 또는 VM에 오류가 발생해도 지탱할 수 있도록 하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9afa5-204">Therefore, high-availability functionality needs to be put in place to make sure that those components can sustain a failure of a server or a VM as done with Windows Cluster configurations for bare-metal and Hyper-V environments.</span></span>

<span data-ttu-id="9afa5-205">업데이트한 날짜: 2016년 12월</span><span class="sxs-lookup"><span data-stu-id="9afa5-205">Updated: December 2016</span></span>

<span data-ttu-id="9afa5-206">[이 가이드는 여기서 확인할 수 있습니다.][ha-guide]</span><span class="sxs-lookup"><span data-stu-id="9afa5-206">[This guide can be found here][ha-guide]</span></span>

