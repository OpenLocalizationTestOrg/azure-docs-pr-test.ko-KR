---
title: "가상 컴퓨터의 SAP NetWeaver에 대 한 고가용성 aaaAzure | Microsoft Docs"
description: "Azure Virtual Machines의 SAP NetWeaver에 대한 고가용성 가이드입니다."
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="62912-103">SAP NetWeaver에 대한 Azure Virtual Machines 고가용성</span><span class="sxs-lookup"><span data-stu-id="62912-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



<span data-ttu-id="62912-109">Azure 가상 컴퓨터에는 최소한의 시간 및 긴 조달 주기 없이 계산, 저장소 및 네트워크 리소스를 필요로 하는 조직 위한 hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-109">Azure Virtual Machines is hello solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="62912-110">Azure 가상 컴퓨터 toodeploy 클래식와 같은 응용 프로그램의 SAP NetWeaver 기반 ABAP, Java 및 ABAP + Java 스택을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-110">You can use Azure Virtual Machines toodeploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="62912-111">추가 온-프레미스 리소스 없이도 안정성과 가용성을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="62912-112">Azure Virtual Machines는 크로스-프레미스 연결을 지원하므로 Azure Virtual Machines를 조직의 온-프레미스 도메인, 사설 클라우드 및 SAP 시스템 지형에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="62912-113">이 문서에서는 수행할 수 있는 toodeploy SAP 시스템 가용성이 높은 Azure의 hello Azure 리소스 관리자 배포 모델을 사용 하 여 hello 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="62912-113">In this article, we cover hello steps that you can take toodeploy high-availability SAP systems in Azure by using hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="62912-114">다음과 같은 주요 작업을 진행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="62912-115">오른쪽 SAP Note 및 설치 가이드 hello에 나열 된 hello 찾습니다 [리소스] [ sap-ha-guide-2] 섹션.</span><span class="sxs-lookup"><span data-stu-id="62912-115">Find hello right SAP Notes and installation guides, listed in hello [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="62912-116">이 문서는 SAP 설치 설명서를 보완 하 게 하는 hello 기본 리소스는 SAP Note 설치 및 특정 플랫폼에 SAP 소프트웨어를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-116">This article complements SAP installation documentation and SAP Notes, which are hello primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="62912-117">Hello hello Azure 리소스 관리자 배포 모델 및 hello Azure 클래식 배포 모델의 차이점에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62912-117">Learn hello differences between hello Azure Resource Manager deployment model and hello Azure classic deployment model.</span></span>
* <span data-ttu-id="62912-118">Azure 배포에 적합 한 hello 모델을 선택할 수 있도록 Windows Server 장애 조치 클러스터링 쿼럼 모드에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62912-118">Learn about Windows Server Failover Clustering quorum modes, so you can select hello model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="62912-119">Azure 서비스의 Windows Server 장애 조치 클러스터링 공유 Storage에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="62912-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="62912-120">Toohelp 오류의 단일 지점 구성 요소와 같은 고급 비즈니스 응용 프로그램 프로그래밍 (ABAP) SAP 중앙 서비스 (ASCS)을 보호 하는 방법에 대해 알아봅니다 SAP 중앙 서비스 SCS () 및 데이터베이스 관리 시스템 (DBMS)와 중복 구성 요소 등의 SAP / Azure에서 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="62912-120">Learn how toohelp protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="62912-121">Azure Resource Manager를 사용하여 Azure의 Windows Server 장애 조치 클러스터링 클러스터에서 고가용성 SAP 시스템을 설치하고 구성하는 단계별 작업 예제를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="62912-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="62912-122">Windows Server 장애 조치 클러스터링 Azure에서 추가 단계가 필요한 toouse 하지만 온-프레미스 배포에 필요 하지 않은 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62912-122">Learn about additional steps required toouse Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="62912-123">사용 하 여 toosimplify 배포 하 고이 문서에서는 구성 SAP 3 계층 가용 리소스 관리자 템플릿을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-123">toosimplify deployment and configuration, in this article, we use hello SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="62912-124">hello 템플릿 고가용성 SAP 시스템에 필요한 hello 전체 인프라의 배포를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-124">hello templates automate deployment of hello entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="62912-125">hello 인프라는 SAP 시스템의 SAP 응용 프로그램 성능 표준 (SAPS) 크기 조정도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-125">hello infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="62912-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> 필수 조건</span><span class="sxs-lookup"><span data-stu-id="62912-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="62912-127">시작 하기 전에 hello 다음 섹션에서에서 설명 하는 hello 필수 구성 요소를 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-127">Before you start, make sure that you meet hello prerequisites that are described in hello following sections.</span></span> <span data-ttu-id="62912-128">또한 있는지 toocheck hello에 나열 된 모든 리소스를 될 [리소스] [ sap-ha-guide-2] 섹션.</span><span class="sxs-lookup"><span data-stu-id="62912-128">Also, be sure toocheck all resources listed in hello [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="62912-129">이 문서에서는 [관리 디스크를 사용하는 3계층 SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/)용 Azure Resource Manager 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="62912-130">유용한 템플릿 개요를 보려면 [SAP Azure Resource Manager 템플릿](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62912-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="62912-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> 리소스</span><span class="sxs-lookup"><span data-stu-id="62912-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="62912-132">이 문서에서는 Azure의 SAP 배포에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="62912-133">[SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="62912-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="62912-134">[SAP NetWeaver에 대한 Azure Virtual Machines 배포][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="62912-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="62912-135">[SAP NetWeaver에 대한 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="62912-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="62912-136">[SAP NetWeaver에 대한 Azure Virtual Machines 고가용성(이 가이드)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="62912-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="62912-137">가능 하면 항상 저희가 SAP 설치 가이드를 참조 하는 링크 toohello (hello 참조 [SAP 설치 가이드][sap-installation-guides]).</span><span class="sxs-lookup"><span data-stu-id="62912-137">Whenever possible, we give you a link toohello referring SAP installation guide (see hello [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="62912-138">필수 구성 요소와 그 좋습니다 tooread hello SAP NetWeaver 설치 안내를 신중 하 게 hello 설치 프로세스에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-138">For prerequisites and information about hello installation process, it's a good idea tooread hello SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="62912-139">이 문서에서는 Azure Virtual Machines와 함께 사용할 수 있는 SAP NetWeaver 기반 시스템에 대한 특정 작업만 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="62912-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="62912-140">이러한 SAP Note는 Azure에서 sap 관련된 toohello 항목:</span><span class="sxs-lookup"><span data-stu-id="62912-140">These SAP Notes are related toohello topic of SAP in Azure:</span></span>

| <span data-ttu-id="62912-141">Note 번호</span><span class="sxs-lookup"><span data-stu-id="62912-141">Note number</span></span> | <span data-ttu-id="62912-142">제목</span><span class="sxs-lookup"><span data-stu-id="62912-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="62912-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="62912-143">[1928533]</span></span> |<span data-ttu-id="62912-144">Azure의 SAP 응용 프로그램: 지원 제품 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="62912-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="62912-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="62912-145">[2015553]</span></span> |<span data-ttu-id="62912-146">Microsoft Azure의 SAP: 지원 필수 조건</span><span class="sxs-lookup"><span data-stu-id="62912-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="62912-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="62912-147">[1999351]</span></span> |<span data-ttu-id="62912-148">향상된 SAP용 Azure 모니터링</span><span class="sxs-lookup"><span data-stu-id="62912-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="62912-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="62912-149">[2178632]</span></span> |<span data-ttu-id="62912-150">Microsoft Azure의 SAP용 주요 모니터링 메트릭</span><span class="sxs-lookup"><span data-stu-id="62912-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="62912-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="62912-151">[1999351]</span></span> |<span data-ttu-id="62912-152">Windows에서의 가상화: 향상된 모니터링</span><span class="sxs-lookup"><span data-stu-id="62912-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="62912-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="62912-153">[2243692]</span></span> |<span data-ttu-id="62912-154">SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용</span><span class="sxs-lookup"><span data-stu-id="62912-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="62912-155">Hello에 대 한 자세한 [Azure 구독 제한인][azure-subscription-service-limits-subscription], 일반 기본 제한 및 최대 제한 사항을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-155">Learn more about hello [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="62912-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>가용성이 높은 SAP hello Azure 클래식 배포 모델 및 Azure 리소스 관리자와</span><span class="sxs-lookup"><span data-stu-id="62912-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. hello Azure classic deployment model</span></span>
<span data-ttu-id="62912-157">hello Azure 리소스 관리자 및 Azure 클래식 배포 모델 hello 다음 영역에서에서 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="62912-157">hello Azure Resource Manager and Azure classic deployment models are different in hello following areas:</span></span>

- <span data-ttu-id="62912-158">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="62912-158">Resource groups</span></span>
- <span data-ttu-id="62912-159">Azure 내부 부하 분산 장치에 hello Azure 리소스 그룹에 대 한 종속성</span><span class="sxs-lookup"><span data-stu-id="62912-159">Azure internal load balancer dependency on hello Azure resource group</span></span>
- <span data-ttu-id="62912-160">SAP 다중 SID 지원 시나리오</span><span class="sxs-lookup"><span data-stu-id="62912-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="62912-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="62912-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="62912-162">Azure 리소스 관리자를 사용할 수 있습니다 리소스 그룹 toomanage hello 응용 프로그램 리소스를 모두 Azure 구독에서.</span><span class="sxs-lookup"><span data-stu-id="62912-162">In Azure Resource Manager, you can use resource groups toomanage all hello application resources in your Azure subscription.</span></span> <span data-ttu-id="62912-163">리소스 그룹에는 통합 된 접근 방식을 모든 리소스는 hello 같은 수명 주기 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-163">An integrated approach, in a resource group, all resources have hello same life cycle.</span></span> <span data-ttu-id="62912-164">예를 들어 모든 리소스가 생성 hello에서 동일한 시간 및 이러한 hello 시에 삭제 됩니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-164">For example, all resources are created at hello same time and they are deleted at hello same time.</span></span> <span data-ttu-id="62912-165">[리소스 그룹](../../../azure-resource-manager/resource-group-overview.md#resource-groups)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62912-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="62912-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure 내부 부하 분산 장치에 hello Azure 리소스 그룹에 대 한 종속성</span><span class="sxs-lookup"><span data-stu-id="62912-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on hello Azure resource group</span></span>

<span data-ttu-id="62912-167">Hello Azure 클래식 배포 모델에서 hello Azure 내부 부하 분산 장치 (Azure 부하 분산 장치 서비스)와 hello 클라우드 서비스 간의 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-167">In hello Azure classic deployment model, there is a dependency between hello Azure internal load balancer (Azure Load Balancer service) and hello cloud service.</span></span> <span data-ttu-id="62912-168">모든 내부 부하 분산 장치에는 하나의 클라우드 서비스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="62912-169">Azure 리소스 관리자의 모든 Azure 리소스에는 Azure 리소스 그룹에 배치 toobe 필요 하며이 Azure 부하 분산 장치에 대 한 유효한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-169">In Azure Resource Manager, every Azure resource needs toobe placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="62912-170">그러나 Azure 부하 분산 장치 당 필요 toohave 하나의 Azure 리소스 그룹이 없으므로, 예를 들어 하나의 Azure 리소스 그룹 여러 Azure 부하 분산 장치를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-170">However, there is no need toohave one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="62912-171">hello 환경에 더 간단 하 고 보다 유연 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-171">hello environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="62912-172">SAP 다중 SID 지원 시나리오</span><span class="sxs-lookup"><span data-stu-id="62912-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="62912-173">Azure Resource Manager에서 하나의 클러스터에 여러 SAP SID(시스템 식별자) ASCS/SCS 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="62912-174">각 Azure 내부 부하 분산 장치의 여러 IP 주소에 대한 지원으로 인해 다중 SID 인스턴스가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="62912-175">toouse hello Azure 클래식 배포 모델에 설명 된 hello 절차를 수행 하십시오 [Azure에서 SAP NetWeaver: SIOS datakeeper를 통해 Azure에서 Windows Server 장애 조치 클러스터링을 사용 하 여 클러스터링 SAP ASCS/SCS 인스턴스에](http://go.microsoft.com/fwlink/?LinkId=613056)합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-175">toouse hello Azure classic deployment model, follow hello procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62912-176">SAP 설치에 대 한 hello Azure 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-176">We strongly recommend that you use hello Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="62912-177">Hello 클래식 배포 모델에서 사용할 수 없는 많은 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-177">It offers many benefits that are not available in hello classic deployment model.</span></span> <span data-ttu-id="62912-178">Azure [배포 모델][virtual-machines-azure-resource-manager-architecture-benefits-arm]에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="62912-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="62912-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server 장애 조치 클러스터링</span><span class="sxs-lookup"><span data-stu-id="62912-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="62912-180">Windows Server 장애 조치 클러스터링은 고가용성 SAP ASCS/SCS 설치 및 Windows의 DBMS의 hello 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-180">Windows Server Failover Clustering is hello foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="62912-181">장애 조치 클러스터는 1 + n 독립 서버 (노드) 응용 프로그램 및 서비스의 tooincrease hello 가용성 함께 작동 하는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-181">A failover cluster is a group of 1+n independent servers (nodes) that work together tooincrease hello availability of applications and services.</span></span> <span data-ttu-id="62912-182">노드 오류가 발생할 경우 hello는 정상 상태를 유지 관리 하는 동안 발생할 수 있는 오류 수를 계산 Windows Server 장애 조치 클러스터링 tooprovide 응용 프로그램 및 서비스를 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-182">If a node failure occurs, Windows Server Failover Clustering calculates hello number of failures that can occur while maintaining a healthy cluster tooprovide applications and services.</span></span> <span data-ttu-id="62912-183">다른 쿼럼 모드 tooachieve 장애 조치 클러스터링에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-183">You can choose from different quorum modes tooachieve failover clustering.</span></span>

### <span data-ttu-id="62912-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> 쿼럼 모드</span><span class="sxs-lookup"><span data-stu-id="62912-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="62912-185">Windows Server 장애 조치 클러스터링을 사용하는 경우 다음 4개의 쿼럼 모드 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="62912-186">**노드 과반수**.</span><span class="sxs-lookup"><span data-stu-id="62912-186">**Node Majority**.</span></span> <span data-ttu-id="62912-187">Hello 클러스터의 각 노드에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-187">Each node of hello cluster can vote.</span></span> <span data-ttu-id="62912-188">hello 클러스터 에서만 작동 과반수 응답이, 즉, 절반 이상이 hello로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-188">hello cluster functions only with a majority of votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="62912-189">노드 수가 균일하지 않은 클러스터에 대해 이 옵션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="62912-190">예를 들어 7 노드 클러스터에 세 개의 노드 실패 수 및 hello 클러스터 스틸 대부분을 toorun를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-190">For example, three nodes in a seven-node cluster can fail, and hello cluster stills achieves a majority and continues toorun.</span></span>  
* <span data-ttu-id="62912-191">**노드 및 디스크 과반수**.</span><span class="sxs-lookup"><span data-stu-id="62912-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="62912-192">각 노드와 hello 클러스터 저장소의 지정 된 디스크 (디스크 감시) 사용할 수 있을 때 및 통신에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-192">Each node and a designated disk (a disk witness) in hello cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="62912-193">hello 클러스터 에서만 작동 대부분 hello의 절반 이상이 hello 응답으로 즉, 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-193">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="62912-194">이 모드는 노드 수가 짝수인 클러스터 환경에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="62912-195">절반 hello 노드 및 디스크 hello 온라인 인 경우 hello 클러스터 정상 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-195">If half hello nodes and hello disk are online, hello cluster remains in a healthy state.</span></span>
* <span data-ttu-id="62912-196">**노드 및 파일 공유 과반수**.</span><span class="sxs-lookup"><span data-stu-id="62912-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="62912-197">Hello 노드 및 파일 공유를 사용할 수 있는지 여부에 관계 없이 고 통신 관리자 hello 하는 지정 된 파일 공유 (파일 공유 감시)을 만듭니다 더하기에 각 노드에서 투표 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-197">Each node plus a designated file share (a file share witness) that hello administrator creates can vote, regardless of whether hello nodes and file share are available and in communication.</span></span> <span data-ttu-id="62912-198">hello 클러스터 에서만 작동 대부분 hello의 절반 이상이 hello 응답으로 즉, 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-198">hello cluster functions only with a majority of hello votes, that is, with more than half hello votes.</span></span> <span data-ttu-id="62912-199">이 모드는 노드 수가 짝수인 클러스터 환경에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="62912-200">비슷한 toohello 노드 및 디스크 과반수 모드 있지만 미러링 모니터 파일 공유 감시 디스크 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-200">It's similar toohello Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="62912-201">이 모드는 쉽게 tooimplement 하지만 가용성이 높지 않은 자체 hello 파일 공유 하는 경우, 단일 실패 지점이 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-201">This mode is easy tooimplement, but if hello file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="62912-202">**과반수 없음: 디스크만**.</span><span class="sxs-lookup"><span data-stu-id="62912-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="62912-203">하나의 노드가 사용 가능 하 고 hello 클러스터 저장소의 특정 디스크와 통신의 경우 hello 클러스터에 쿼럼이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-203">hello cluster has a quorum if one node is available and in communication with a specific disk in hello cluster storage.</span></span> <span data-ttu-id="62912-204">해당 디스크와의 통신에도 있는 hello 노드만 hello 클러스터에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-204">Only hello nodes that also are in communication with that disk can join hello cluster.</span></span> <span data-ttu-id="62912-205">이 모드는 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="62912-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server 장애 조치 클러스터링 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="62912-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="62912-207">그림 1에서는 두 노드 클러스터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="62912-208">Hello hello 노드 사이의 네트워크 연결 실패 하 고 두 노드를 유지 하 고 실행, 쿼럼 디스크 또는 파일 공유 결정 tooprovide hello 클러스터의 응용 프로그램 및 서비스 노드에 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-208">If hello network connection between hello nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue tooprovide hello cluster's applications and services.</span></span> <span data-ttu-id="62912-209">hello 노드가 액세스 toohello 쿼럼 디스크 또는 파일 공유를 통해 서비스 계속 hello 노드가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-209">hello node that has access toohello quorum disk or file share is hello node that ensures that services continue.</span></span>

<span data-ttu-id="62912-210">이 예에서는 2 개 노드 클러스터를 사용 하므로 hello 노드 및 파일 공유 과반수 쿼럼 모드 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-210">Because this example uses a two-node cluster, we use hello Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="62912-211">hello 노드 및 디스크 과반수는 올바른 옵션이 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-211">hello Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="62912-212">프로덕션 환경에서는 쿼럼 디스크를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="62912-213">네트워크 및 저장소 시스템 기술 toomake에서는 항상 사용 가능한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-213">You can use network and storage system technology toomake it highly available.</span></span>

![그림 1: Azure에서 SAP ASCS/SCS에 대한 Windows Server 장애 조치 클러스터링 구성 예제][sap-ha-guide-figure-1000]

<span data-ttu-id="62912-215">_**그림 1:** Azure에서 SAP ASCS/SCS에 대한 Windows Server 장애 조치 클러스터링 구성 예제_</span><span class="sxs-lookup"><span data-stu-id="62912-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="62912-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> 공유 Storage</span><span class="sxs-lookup"><span data-stu-id="62912-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="62912-217">그림 1에는 2 노드 공유 Storage 클러스터도 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="62912-218">온-프레미스 공유 저장소 클러스터를 사용 하는 hello 클러스터의 모든 노드에서 공유 저장소를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-218">In an on-premises shared storage cluster, all nodes in hello cluster detect shared storage.</span></span> <span data-ttu-id="62912-219">Hello 데이터 손상 으로부터 보호 하는 잠금 메커니즘 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-219">A locking mechanism protects hello data from corruption.</span></span> <span data-ttu-id="62912-220">모든 노드는 다른 노드에 장애가 있는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="62912-221">한 노드가 실패 하면 hello 남아 있는 노드 hello 저장소 리소스의 소유권을 가져오면 및 hello 서비스의 가용성을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-221">If one node fails, hello remaining node takes ownership of hello storage resources and ensures hello availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="62912-222">SQL Server와 같은 일부 DBMS 응용 프로그램에서는 가용성을 높이기 위해 공유 디스크를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="62912-223">SQL Server Always On hello 한 개의 클러스터 노드 toohello 다른 클러스터 노드의 로컬 디스크의 로컬 디스크에서 DBMS 데이터 및 로그 파일을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-223">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="62912-224">이 경우 hello Windows 클러스터 구성에는 공유 디스크가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-224">In that case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="62912-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> 네트워킹 및 이름 확인</span><span class="sxs-lookup"><span data-stu-id="62912-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="62912-226">클라이언트 컴퓨터에 연결할 hello 클러스터 가상 IP 주소와 가상 호스트 이름을 통해 DNS 서버를 제공 하는 hello.</span><span class="sxs-lookup"><span data-stu-id="62912-226">Client computers reach hello cluster over a virtual IP address and a virtual host name that hello DNS server provides.</span></span> <span data-ttu-id="62912-227">hello 온-프레미스 노드 및 hello DNS 서버에서 여러 IP 주소를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-227">hello on-premises nodes and hello DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="62912-228">표준 설치에서는 다음 두 가지 이상의 네트워크 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="62912-229">전용된 연결이 toohello 저장소</span><span class="sxs-lookup"><span data-stu-id="62912-229">A dedicated connection toohello storage</span></span>
* <span data-ttu-id="62912-230">Hello 하트 비트에 대 한 클러스터 내부 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="62912-230">A cluster-internal network connection for hello heartbeat</span></span>
* <span data-ttu-id="62912-231">클라이언트가 tooconnect toohello 클러스터를 사용 하는 공용 네트워크</span><span class="sxs-lookup"><span data-stu-id="62912-231">A public network that clients use tooconnect toohello cluster</span></span>

## <span data-ttu-id="62912-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Azure의 Windows Server 장애 조치 클러스터링</span><span class="sxs-lookup"><span data-stu-id="62912-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="62912-233">Toobare 금속 또는 사설 클라우드 배포에 비해 Azure 가상 컴퓨터에 Windows Server 장애 조치 클러스터링 하는 추가 단계 tooconfigure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-233">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="62912-234">공유 클러스터 디스크를 빌드할 때 hello SAP ASCS/SCS 인스턴스에 tooset 여러 IP 주소와 가상 호스트 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-234">When you build a shared cluster disk, you need tooset several IP addresses and virtual host names for hello SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="62912-235">이 문서에서는 주요 개념에 설명 하 고 Azure의 SAP 고가용성 중앙 서비스 클러스터는 추가 단계가 필요한 toobuild hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-235">In this article, we discuss key concepts and hello additional steps required toobuild an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="62912-236">Hello 타사 도구 SIOS DataKeeper를 tooset 및 어떻게 tooconfigure hello Azure 내부 부하 분산 장치에 어떻게 하면 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-236">We show you how tooset up hello third-party tool SIOS DataKeeper, and how tooconfigure hello Azure internal load balancer.</span></span> <span data-ttu-id="62912-237">Azure에서 파일 공유 미러링 모니터 서버와 이러한 도구 toocreate Windows 장애 조치 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-237">You can use these tools toocreate a Windows failover cluster with a file share witness in Azure.</span></span>

![그림 2: 공유 디스크를 사용하지 않는 Azure의 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1001]

<span data-ttu-id="62912-239">_**그림 2:** 공유 디스크를 사용하지 않는 Azure의 Windows Server 장애 조치 클러스터링 구성_</span><span class="sxs-lookup"><span data-stu-id="62912-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="62912-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> SIOS DataKeeper를 사용한 Azure의 공유 디스크</span><span class="sxs-lookup"><span data-stu-id="62912-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="62912-241">고가용성 SAP ASCS/SCS 인스턴스를 위해서는 클러스터 공유 Storage가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="62912-242">2016 년 9 월의 Azure 제공 하지 않으면 공유 저장소를 공유 저장소 클러스터 toocreate를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-242">As of September 2016, Azure doesn't offer shared storage that you can use toocreate a shared storage cluster.</span></span> <span data-ttu-id="62912-243">제 3 자 소프트웨어 SIOS DataKeeper Cluster Edition toocreate 클러스터 공유 저장소를 시뮬레이션 하는 미러된 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-243">You can use third-party software SIOS DataKeeper Cluster Edition toocreate a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="62912-244">hello SIOS 솔루션 동기 실시간 데이터 복제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-244">hello SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="62912-245">다음은 클러스터에 대한 공유 디스크 리소스를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="62912-246">추가 디스크 tooeach hello 가상 컴퓨터 (Vm)의 Windows 클러스터 구성에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-246">Attach an additional disk tooeach of hello virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="62912-247">두 가상 컴퓨터 노드에서 SIOS DataKeeper Cluster Edition을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="62912-248">Hello 대상 가상 컴퓨터의 hello 원본 가상 컴퓨터 toohello 추가 디스크를 연결 된 볼륨에서 hello 추가 디스크를 연결 된 볼륨의 hello 콘텐츠를 미러링합니다 SIOS DataKeeper Cluster Edition을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors hello content of hello additional disk attached volume from hello source virtual machine toohello additional disk attached volume of hello target virtual machine.</span></span> <span data-ttu-id="62912-249">SIOS DataKeeper 소스 및 대상 로컬 볼륨 hello를 추상화 한 다음 공유 디스크로 서버 장애 조치 클러스터링 tooWindows 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-249">SIOS DataKeeper abstracts hello source and target local volumes, and then presents them tooWindows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="62912-250">[SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/)에 대한 자세한 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62912-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![그림 3: SIOS DataKeeper를 사용하는 Azure의 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1002]

<span data-ttu-id="62912-252">_**그림 3:** SIOS DataKeeper를 사용하는 Azure의 Windows Server 장애 조치 클러스터링 구성_</span><span class="sxs-lookup"><span data-stu-id="62912-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="62912-253">SQL Server와 같은 일부 DBMS 제품에서는 가용성을 높이기 위해 공유 디스크를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="62912-254">SQL Server Always On hello 한 개의 클러스터 노드 toohello 다른 클러스터 노드의 로컬 디스크의 로컬 디스크에서 DBMS 데이터 및 로그 파일을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-254">SQL Server Always On replicates DBMS data and log files from hello local disk of one cluster node toohello local disk of another cluster node.</span></span> <span data-ttu-id="62912-255">이 경우 hello Windows 클러스터 구성에는 공유 디스크가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-255">In this case, hello Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="62912-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Azure의 이름 확인</span><span class="sxs-lookup"><span data-stu-id="62912-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="62912-257">hello Azure 클라우드 플랫폼 hello 옵션 tooconfigure 가상 IP 주소, 예: 부동 IP 주소를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-257">hello Azure cloud platform doesn't offer hello option tooconfigure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="62912-258">가상 IP 주소 tooreach hello 클러스터에서에서 리소스를 hello 클라우드는 대체 솔루션 tooset이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-258">You need an alternative solution tooset up a virtual IP address tooreach hello cluster resource in hello cloud.</span></span>
<span data-ttu-id="62912-259">Azure 내부 부하 분산 장치는 hello Azure 부하 분산 서비스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-259">Azure has an internal load balancer in hello Azure Load Balancer service.</span></span> <span data-ttu-id="62912-260">Hello 내부 부하 분산 장치와 클라이언트 hello 클러스터 가상 IP 주소를 통해 hello 클러스터에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-260">With hello internal load balancer, clients reach hello cluster over hello cluster virtual IP address.</span></span>
<span data-ttu-id="62912-261">Toodeploy hello 내부 부하 분산 장치 hello 클러스터 노드를 포함 하는 hello 리소스 그룹에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-261">You need toodeploy hello internal load balancer in hello resource group that contains hello cluster nodes.</span></span> <span data-ttu-id="62912-262">그런 다음 모든 필요한 포트 전달 규칙 hello 프로브와 hello 내부 부하 분산 장치의 포트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-262">Then, configure all necessary port forwarding rules with hello probe ports of hello internal load balancer.</span></span>
<span data-ttu-id="62912-263">hello 클라이언트 hello 가상 호스트 이름을 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-263">hello clients can connect via hello virtual host name.</span></span> <span data-ttu-id="62912-264">hello DNS 서버 hello 클러스터 IP 주소와 toohello hello 클러스터의 활성 노드를 전달 하는 hello 내부 부하 분산 장치 핸들 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-264">hello DNS server resolves hello cluster IP address, and hello internal load balancer handles port forwarding toohello active node of hello cluster.</span></span>

## <span data-ttu-id="62912-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Azure IaaS(Infrastructure-as-a-Service)의 SAP NetWeaver 고가용성</span><span class="sxs-lookup"><span data-stu-id="62912-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="62912-266">tooachieve SAP 소프트웨어 구성 요소에 대해 다음과 같은 구성 요소가 tooprotect hello 해야와 같은 응용 프로그램 고가용성 SAP:</span><span class="sxs-lookup"><span data-stu-id="62912-266">tooachieve SAP application high availability, such as for SAP software components, you need tooprotect hello following components:</span></span>

* <span data-ttu-id="62912-267">SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="62912-267">SAP Application Server instance</span></span>
* <span data-ttu-id="62912-268">SAP ASCS/SCS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="62912-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="62912-269">DBMS 서버</span><span class="sxs-lookup"><span data-stu-id="62912-269">DBMS server</span></span>

<span data-ttu-id="62912-270">고가용성 시나리오에서 SAP 구성 요소 보호에 대한 자세한 내용은 [SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현][planning-guide-11]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62912-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="62912-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> 고가용성 SAP 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="62912-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="62912-272">일반적으로 hello SAP 응용 프로그램 서버 및 대화 상자 인스턴스는 특정 가용성 우선 솔루션이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-272">You usually don't need a specific high-availability solution for hello SAP Application Server and dialog instances.</span></span> <span data-ttu-id="62912-273">중복성으로 고가용성을 달성하고 다른 Azure Virtual Machines 인스턴스에서 여러 대화 상자 인스턴스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="62912-274">두 개의 Azure Virtual Machines 인스턴스에 2개 이상의 SAP 응용 프로그램 인스턴스가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![그림 4: 고가용성 SAP 응용 프로그램 서버][sap-ha-guide-figure-2000]

<span data-ttu-id="62912-276">_**그림 4:** 고가용성 SAP 응용 프로그램 서버_</span><span class="sxs-lookup"><span data-stu-id="62912-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="62912-277">호스트 SAP 응용 프로그램 서버 인스턴스가 동일한 Azure 가용성 집합 hello는 모든 가상 컴퓨터를 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-277">You must place all virtual machines that host SAP Application Server instances in hello same Azure availability set.</span></span> <span data-ttu-id="62912-278">Azure 가용성 집합은 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="62912-279">Hello의 일부인 모든 가상 컴퓨터가 동일한 도메인을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-279">All virtual machines are part of hello same upgrade domain.</span></span> <span data-ttu-id="62912-280">업그레이드 도메인에 있는 예를 들어 실행 하면 hello 가상 컴퓨터 되지 업데이트 hello에 시간 동안 가동 중지 시간이 계획 된 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-280">An upgrade domain, for example, makes sure that hello virtual machines aren't updated at hello same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="62912-281">Hello의 일부인 모든 가상 컴퓨터가 동일한 장애 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-281">All virtual machines are part of hello same fault domain.</span></span> <span data-ttu-id="62912-282">오류 도메인 예를 들어 하면 제대로 모든 가상 컴퓨터의 hello 사용할 수 없는 단일 실패 지점이 되도록 가상 컴퓨터 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects hello availability of all virtual machines.</span></span>

<span data-ttu-id="62912-283">너무 방법에 대 한 자세한[관리 가상 컴퓨터의 가용성을 hello][virtual-machines-manage-availability]합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-283">Learn more about how too[manage hello availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="62912-284">관리 되지 않는 디스크 에서만: 중요 한 toohave 변수가 hello Azure 저장소 계정에 잠재적인 단일 실패 지점이 이므로 두 개 이상의 Azure 저장소 계정, 두 개 이상의 가상 컴퓨터 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-284">Unmanaged disk only: Because hello Azure storage account is a potential single point of failure, it's important toohave at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="62912-285">이상적인 설치 프로그램에서 다른 저장소 계정에 SAP 대화 상자 인스턴스를 실행 하는 각 가상 컴퓨터의 디스크 hello이 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-285">In an ideal setup, hello disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="62912-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> 고가용성 SAP ASCS/SCS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="62912-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="62912-287">그림 5는 고가용성 SAP ASCS/SCS 인스턴스의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![그림 5: 고가용성 SAP ASCS/SCS 인스턴스][sap-ha-guide-figure-2001]

<span data-ttu-id="62912-289">_**그림 5:** 고가용성 SAP ASCS/SCS 인스턴스_</span><span class="sxs-lookup"><span data-stu-id="62912-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="62912-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Azure에서 Windows Server 장애 조치 클러스터링을 사용한 SAP ASCS/SCS 인스턴스 고가용성</span><span class="sxs-lookup"><span data-stu-id="62912-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="62912-291">Toobare 금속 또는 사설 클라우드 배포에 비해 Azure 가상 컴퓨터에 Windows Server 장애 조치 클러스터링 하는 추가 단계 tooconfigure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-291">Compared toobare metal or private cloud deployments, Azure Virtual Machines requires additional steps tooconfigure Windows Server Failover Clustering.</span></span> <span data-ttu-id="62912-292">Windows 장애 조치 클러스터 toobuild 필요 공유 클러스터 디스크, 여러 개의 IP 주소가, 여러 가상 호스트 이름 및 Azure 내부 부하 분산 장치는 SAP ASCS/SCS 인스턴스를 클러스터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-292">toobuild a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="62912-293">이 부분은 hello 문서 뒷부분에 보다 자세히 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-293">We discuss this in more detail later in hello article.</span></span>

![그림 6: SIOS DataKeeper를 사용하는 Azure의 SAP ASCS/SCS용 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1002]

<span data-ttu-id="62912-295">_**그림 6:** SIOS DataKeeper를 사용하는 Azure의 SAP ASCS/SCS용 Windows Server 장애 조치 클러스터링 구성_</span><span class="sxs-lookup"><span data-stu-id="62912-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="62912-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> 고가용성 DBMS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="62912-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="62912-297">hello DBMS은는 SAP의 단일 접촉 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-297">hello DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="62912-298">Tooprotect 필요한 고가용성 솔루션을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-298">You need tooprotect it by using a high-availability solution.</span></span> <span data-ttu-id="62912-299">Windows Server 장애 조치 클러스터링 및 hello Azure 내부 부하 분산 장치, 그림 7 Azure에서 SQL Server Always On 고가용성 솔루션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and hello Azure internal load balancer.</span></span> <span data-ttu-id="62912-300">SQL Server Always On은 자체 DBMS 복제를 사용하여 DBMS 데이터 및 로그 파일을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="62912-301">이 경우 없습니다 필요를 클러스터링 할 공유 디스크 hello 전체 설치를 단순화 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-301">In this case, you don't need cluster shared disks, which simplifies hello entire setup.</span></span>

![그림 7: SQL Server Always On을 사용하는 고가용성 SAP DBMS 예제][sap-ha-guide-figure-2003]

<span data-ttu-id="62912-303">_**그림 7:** SQL Server Always On을 사용하는 고가용성 SAP DBMS 예제_</span><span class="sxs-lookup"><span data-stu-id="62912-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="62912-304">Hello Azure 리소스 관리자 배포 모델을 사용 하 여 Azure의 SQL Server를 클러스터링 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-304">For more information about clustering SQL Server in Azure by using hello Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="62912-305">[Resource Manager를 사용하여 Azure Virtual Machines에서 수동으로 Always On 가용성 그룹 구성][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="62912-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="62912-306">[Azure에서 Always On 가용성 그룹에 대한 Azure 내부 부하 분산 장치 구성][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="62912-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="62912-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> 종단간 고가용성 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="62912-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="62912-308">아키텍처 템플릿 1을 사용하여 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="62912-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="62912-309">그림 8에서는 **단일** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="62912-310">이 시나리오는 다음과 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="62912-311">하나의 전용된 클러스터 hello SAP ASCS/SCS 인스턴스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-311">One dedicated cluster is used for hello SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="62912-312">하나의 전용된 클러스터 hello DBMS 인스턴스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-312">One dedicated cluster is used for hello DBMS instance.</span></span>
- <span data-ttu-id="62912-313">SAP 응용 프로그램 서버 인스턴스는 자체의 전용 VM에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![그림 8: ASCS/SCS 및 DBMS용 전용 클러스터를 사용하는 SAP 고가용성 아키텍처 템플릿 1][sap-ha-guide-figure-2004]

<span data-ttu-id="62912-315">_**그림 8:** SAP 고가용성 아키텍처 템플릿 1, ASCS/SCS 및 DBMS용 전용 클러스터_</span><span class="sxs-lookup"><span data-stu-id="62912-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="62912-316">아키텍처 템플릿 2를 사용하여 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="62912-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="62912-317">그림 9에서는 **단일** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="62912-318">이 시나리오는 다음과 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="62912-319">하나의 전용된 클러스터에 사용 되 **둘 다** hello SAP ASCS/SCS 인스턴스 및 DBMS hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-319">One dedicated cluster is used for **both** hello SAP ASCS/SCS instance and hello DBMS.</span></span>
- <span data-ttu-id="62912-320">SAP 응용 프로그램 서버 인스턴스는 자체의 전용 VM에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![그림 9: SAP 고가용성 아키텍처 템플릿 2 - ASCS/SCS 전용 클러스터 및 DBMS 전용 클러스터][sap-ha-guide-figure-2005]

<span data-ttu-id="62912-322">_**그림 9:** SAP 고가용성 아키텍처 템플릿 2 - ASCS/SCS 전용 클러스터 및 DBMS 전용 클러스터_</span><span class="sxs-lookup"><span data-stu-id="62912-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="62912-323">아키텍처 템플릿 3을 사용하여 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="62912-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="62912-324">그림 10에서는 &lt;SID1&gt; 및 &lt;SID2&gt;의 **두** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="62912-325">이 시나리오는 다음과 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="62912-326">하나의 전용된 클러스터에 사용 되 **둘 다** hello SAP ASCS/SCS SID1 인스턴스 *및* hello SAP ASCS/SCS SID2 인스턴스 (클러스터).</span><span class="sxs-lookup"><span data-stu-id="62912-326">One dedicated cluster is used for **both** hello SAP ASCS/SCS SID1 instance *and* hello SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="62912-327">하나의 전용 클러스터는 DBMS SID1에 사용되고 다른 전용 클러스터는 DBMS SID2에 사용됩니다(두 개의 클러스터).</span><span class="sxs-lookup"><span data-stu-id="62912-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="62912-328">SAP 시스템 SID1 hello에 대 한 SAP 응용 프로그램 서버 인스턴스는 전용된 Vm을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="62912-328">SAP Application Server instances for hello SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="62912-329">SAP 시스템 SID2 hello에 대 한 SAP 응용 프로그램 서버 인스턴스는 전용된 Vm을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="62912-329">SAP Application Server instances for hello SAP system SID2 have their own dedicated VMs.</span></span>

![그림 10: SAP 고가용성 아키텍처 템플릿 3 - 다른 ASCS/SCS 인스턴스 전용 클러스터][sap-ha-guide-figure-6003]

<span data-ttu-id="62912-331">_**그림 10:** SAP 고가용성 아키텍처 템플릿 3 - 다른 ASCS/SCS 인스턴스 전용 클러스터_</span><span class="sxs-lookup"><span data-stu-id="62912-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="62912-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Hello 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="62912-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare hello infrastructure</span></span>

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a><span data-ttu-id="62912-333">템플릿 1 아키텍처에 대 한 hello 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="62912-333">Prepare hello infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="62912-334">SAP용 Azure Resource Manager 템플릿은 필요한 리소스의 배포를 간소화하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="62912-335">hello 3 계층 템플릿은 Azure 리소스 관리자는 또한 두 클러스터에 있는 템플릿 1 아키텍처와 같은 고가용성 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-335">hello three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="62912-336">각 클러스터는 SAP ASCS/SCS 및 DBMS에 대한 SAP 단일 실패 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="62912-337">이 문서에서 설명 하는 hello 예제 시나리오에 대 한 Azure 리소스 관리자 템플릿을 읽을 수 있는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-337">Here's where you can get Azure Resource Manager templates for hello example scenario we describe in this article:</span></span>

* [<span data-ttu-id="62912-338">Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="62912-339">관리 디스크를 사용하는 Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="62912-340">사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="62912-341">관리 디스크를 사용하는 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="62912-342">템플릿 1 아키텍처에 대 한 tooprepare hello 인프라:</span><span class="sxs-lookup"><span data-stu-id="62912-342">tooprepare hello infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="62912-343">Hello hello에 Azure 포털에서에서 **매개 변수** 블레이드 hello **SYSTEMAVAILABILITY** 상자 **HA**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-343">In hello Azure portal, on hello **Parameters** blade, in hello **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![그림 11: SAP 고가용성 Azure Resource Manager 매개 변수 설정][sap-ha-guide-figure-3000]

<span data-ttu-id="62912-345">_**그림 11:** SAP 고가용성 Azure Resource Manager 매개 변수 설정_</span><span class="sxs-lookup"><span data-stu-id="62912-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="62912-346">hello 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-346">hello templates create:</span></span>

  * <span data-ttu-id="62912-347">**가상 컴퓨터**:</span><span class="sxs-lookup"><span data-stu-id="62912-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="62912-348">SAP 응용 프로그램 서버 가상 컴퓨터: <*SAPSystemSID*>-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="62912-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="62912-349">ASCS/SCS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="62912-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="62912-350">DBMS 클러스터: <*SAPSystemSID*>-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="62912-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="62912-351">**연결된 IP 주소를 갖는 모든 가상 컴퓨터에 대한 네트워크 카드**:</span><span class="sxs-lookup"><span data-stu-id="62912-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="62912-352"><*SAPSystemSID*>-nic-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="62912-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="62912-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="62912-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="62912-354"><*SAPSystemSID*>-nic-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="62912-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="62912-355">**Azure Storage 계정(비관리 디스크에만 해당)**</span><span class="sxs-lookup"><span data-stu-id="62912-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="62912-356">다음에 대한 **가용성 그룹**:</span><span class="sxs-lookup"><span data-stu-id="62912-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="62912-357">SAP 응용 프로그램 서버 가상 컴퓨터: <*SAPSystemSID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="62912-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="62912-358">SAP ASCS/SCS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="62912-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="62912-359">DBMS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="62912-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="62912-360">**Azure 내부 부하 분산 장치**:</span><span class="sxs-lookup"><span data-stu-id="62912-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="62912-361">Hello ASCS/SCS 인스턴스 및 IP 주소에 대 한 모든 포트와 <*SAPSystemSID*> 파운드-ascs</span><span class="sxs-lookup"><span data-stu-id="62912-361">With all ports for hello ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="62912-362">Hello SQL Server DBMS 및 IP 주소에 대 한 모든 포트와 <*SAPSystemSID*> 파운드-db</span><span class="sxs-lookup"><span data-stu-id="62912-362">With all ports for hello SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="62912-363">**네트워크 보안 그룹**: <*SAPSystemSID*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="62912-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="62912-364">열린 외부 프로토콜 RDP (원격 데스크톱) 포트 toohello와 <*SAPSystemSID*> 0-ascs-가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="62912-364">With an open external Remote Desktop Protocol (RDP) port toohello <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="62912-365">Azure 내부 부하 분산 장치 및 hello 네트워크 카드의 모든 IP 주소는 **동적** 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-365">All IP addresses of hello network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="62912-366">너무 변경**정적** IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-366">Change them too**static** IP addresses.</span></span> <span data-ttu-id="62912-367">설명 방법을 toodo hello 문서의 뒷부분에 나오는이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-367">We describe how toodo this later in hello article.</span></span>
>
>

### <span data-ttu-id="62912-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>프로덕션 환경에서 회사 네트워크 연결 (크로스-프레미스) toouse로 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="62912-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) toouse in production</span></span>
<span data-ttu-id="62912-369">프로덕션 SAP 시스템의 경우 Azure 사이트 간 VPN 또는 Azure ExpressRoute를 사용하여 [회사 네트워크 연결(크로스-프레미스)][planning-guide-2.2]를 통해 Azure 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="62912-370">Azure 가상 네트워크 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="62912-371">hello 가상 네트워크 및 서브넷 이미 생성 되어 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-371">hello virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="62912-372">Hello hello에 Azure 포털에서에서 **매개 변수** 블레이드 hello **NEWOREXISTINGSUBNET** 상자 **기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-372">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="62912-373">Hello에 **SUBNETID** 상자에서 준비 된 Azure 네트워크 SubnetID 설치할 toodeploy Azure 가상 컴퓨터의 전체 문자열 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-373">In hello **SUBNETID** box, add hello full string of your prepared Azure network SubnetID where you plan toodeploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="62912-374">Azure 네트워크의 모든 서브넷 목록을 tooget PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-374">tooget a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="62912-375">hello **ID** 필드 표시 hello **SUBNETID**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-375">hello **ID** field shows hello **SUBNETID**.</span></span>
4. <span data-ttu-id="62912-376">모든 목록이 tooget **SUBNETID** 이 PowerShell 명령을 실행 하는 값:</span><span class="sxs-lookup"><span data-stu-id="62912-376">tooget a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="62912-377">hello **SUBNETID** 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-377">hello **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="62912-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> 테스트 및 데모용 클라우드 전용 SAP 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="62912-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="62912-379">클라우드 전용 배포 모델에서 고가용성 SAP 시스템을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="62912-380">기본적으로 이러한 종류의 배포는 데모 및 테스트 사용 사례에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="62912-381">프로덕션 사용 사례에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="62912-382">Hello hello에 Azure 포털에서에서 **매개 변수** 블레이드 hello **NEWOREXISTINGSUBNET** 상자 **새**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-382">In hello Azure portal, on hello **Parameters** blade, in hello **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="62912-383">Hello 둡니다 **SUBNETID** 필드가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-383">Leave hello **SUBNETID** field empty.</span></span>

  <span data-ttu-id="62912-384">hello SAP Azure 리소스 관리자 템플릿을 자동으로 만듭니다. Azure 가상 네트워크 및 서브넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-384">hello SAP Azure Resource Manager template automatically creates hello Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="62912-385">또한 toodeploy 해야 DNS를 Azure 가상 네트워크의 동일한 인스턴스에 hello 및 Active Directory에 대 한 가상 컴퓨터를 전용 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-385">You also need toodeploy at least one dedicated virtual machine for Active Directory and DNS in hello same Azure Virtual Network instance.</span></span> <span data-ttu-id="62912-386">hello 템플릿 이러한 가상 컴퓨터를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-386">hello template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a><span data-ttu-id="62912-387">템플릿 2 아키텍처에 대 한 hello 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="62912-387">Prepare hello infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="62912-388">SAP toohelp 단순화 SAP 아키텍처 템플릿 2에 대 한 필요한 인프라 리소스의 배포에 대 한이 Azure 리소스 관리자 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-388">You can use this Azure Resource Manager template for SAP toohelp simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="62912-389">이 배포 시나리오를 위한 Azure Resource Manager 템플릿을 가져올 수 있는 위치는 다음과 같습니다</span><span class="sxs-lookup"><span data-stu-id="62912-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="62912-390">Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="62912-391">관리 디스크를 사용하는 Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="62912-392">사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="62912-393">관리 디스크를 사용하는 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="62912-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a><span data-ttu-id="62912-394">템플릿 3 아키텍처에 대 한 hello 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="62912-394">Prepare hello infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="62912-395">Hello 인프라를 준비 하 고 구성에 대 한 SAP 있습니다 **다중 SID**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-395">You can prepare hello infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="62912-396">예를 들어 추가 SAP ASCS/SCS 인스턴스를 *기존* 클러스터 구성에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="62912-397">자세한 내용은 참조 [Azure 리소스 관리자는 기존 클러스터 구성 toocreate SAP SID 다중 구성에 추가 SAP ASCS/SCS 인스턴스 구성][sap-ha-multi-sid-guide]합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration toocreate an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="62912-398">새 다중 SID 클러스터 toocreate 경우 hello 다중 SID를 사용할 수 있습니다 [GitHub의 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-398">If you want toocreate a new multi-SID cluster, you can use hello multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="62912-399">새 다중 SID 클러스터 toocreate toodeploy hello 다음 세 개의 템플릿이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-399">toocreate a new multi-SID cluster, you need toodeploy hello following three templates:</span></span>

* [<span data-ttu-id="62912-400">ASCS/SCS 템플릿</span><span class="sxs-lookup"><span data-stu-id="62912-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="62912-401">데이터베이스 템플릿</span><span class="sxs-lookup"><span data-stu-id="62912-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="62912-402">응용 프로그램 서버 템플릿</span><span class="sxs-lookup"><span data-stu-id="62912-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="62912-403">hello 다음 섹션에서는 있어야 hello 템플릿 및 tooprovide hello 템플릿에 필요한 hello 매개 변수에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="62912-403">hello following sections have more details about hello templates and hello parameters you need tooprovide in hello templates.</span></span>

#### <span data-ttu-id="62912-404"><a name="ASCS-SCS-template"></a> ASCS/SCS 템플릿</span><span class="sxs-lookup"><span data-stu-id="62912-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="62912-405">hello ASCS/SCS 템플릿 toocreate 여러 ASCS/SCS 인스턴스를 호스트 하는 Windows Server 장애 조치 클러스터를 사용할 수 있는 두 가상 컴퓨터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-405">hello ASCS/SCS template deploys two virtual machines that you can use toocreate a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="62912-406">hello에 hello ASCS/SCS 다중 SID 서식 파일을 tooset [ASCS/SCS 다중 SID 템플릿] [ sap-templates-3-tier-multisid-xscs-marketplace-image] 또는 [관리 하는 디스크를 사용 하 여 ASCS/SCS 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], hello 매개 변수 뒤에 대 한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-406">tooset up hello ASCS/SCS multi-SID template, in hello [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for hello following parameters:</span></span>

  - <span data-ttu-id="62912-407">**리소스 접두사**.</span><span class="sxs-lookup"><span data-stu-id="62912-407">**Resource Prefix**.</span></span>  <span data-ttu-id="62912-408">Hello 리소스 접두사를 사용 하는 tooprefix hello 배포 중에 생성 되는 모든 리소스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-408">Set hello resource prefix, which is used tooprefix all resources that are created during hello deployment.</span></span> <span data-ttu-id="62912-409">Hello 리소스 tooonly 단일 SAP 시스템에 속하지 않으면, hello 리소스의 hello 접두사 hello 단일 SAP 시스템의 SID 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-409">Because hello resources do not belong tooonly one SAP system, hello prefix of hello resource is not hello SID of one SAP system.</span></span>  <span data-ttu-id="62912-410">hello 접두사 사이 여야 합니다 **3-6 개의 문자**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-410">hello prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="62912-411">**스택 유형**.</span><span class="sxs-lookup"><span data-stu-id="62912-411">**Stack Type**.</span></span> <span data-ttu-id="62912-412">Hello SAP 시스템의 hello 스택 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-412">Select hello stack type of hello SAP system.</span></span> <span data-ttu-id="62912-413">Hello 스택 종류에 따라 Azure 부하 분산 장치 (ABAP 또는 Java만) 하나 또는 두 개 (ABAP + Java) 개인 하나의 IP 주소를 SAP 시스템에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-413">Depending on hello stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="62912-414">**OS 종류**.</span><span class="sxs-lookup"><span data-stu-id="62912-414">**OS Type**.</span></span> <span data-ttu-id="62912-415">Hello 가상 컴퓨터의 hello 운영 체제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-415">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="62912-416">**SAP 시스템 수**.</span><span class="sxs-lookup"><span data-stu-id="62912-416">**SAP System Count**.</span></span> <span data-ttu-id="62912-417">Hello 수를 선택 합니다.이 클러스터의 tooinstall SAP 시스템의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-417">Select hello number of SAP systems you want tooinstall in this cluster.</span></span>
  -  <span data-ttu-id="62912-418">**시스템 가용성**.</span><span class="sxs-lookup"><span data-stu-id="62912-418">**System Availability**.</span></span> <span data-ttu-id="62912-419">**HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-419">Select **HA**.</span></span>
  -  <span data-ttu-id="62912-420">**관리자 사용자 이름 및 관리자 암호**.</span><span class="sxs-lookup"><span data-stu-id="62912-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="62912-421">Toohello 컴퓨터에서 사용 되는 toosign 일 수 있는 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-421">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="62912-422">**새 또는 기존 서브넷**.</span><span class="sxs-lookup"><span data-stu-id="62912-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="62912-423">새 가상 네트워크와 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="62912-424">가상 네트워크는 연결 된 tooyour 온-프레미스 네트워크를 이미 있는 경우 선택 **기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-424">If you already have a virtual network that is connected tooyour on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="62912-425">**서브넷 ID**. 가상 컴퓨터를 연결 하는 hello 서브넷 toowhich hello의 hello ID를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-425">**Subnet Id**. Set hello ID of hello subnet toowhich hello virtual machines should be connected.</span></span> <span data-ttu-id="62912-426">가상 사설망 (VPN) 또는 ExpressRoute 가상 네트워크 tooconnect hello 가상 컴퓨터 tooyour 온-프레미스 네트워크의 서브넷을 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-426">Select hello subnet of your virtual private network (VPN) or ExpressRoute virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="62912-427">hello ID는 일반적으로 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-427">hello ID usually looks like this:</span></span>

   <span data-ttu-id="62912-428">/subscriptions/<*구독 ID*>/resourceGroups/<*리소스 그룹 이름*>/providers/Microsoft.Network/virtualNetworks/<*가상 네트워크 이름*>/subnets/<*서브넷 이름*></span><span class="sxs-lookup"><span data-stu-id="62912-428">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="62912-429">hello 템플릿 여러 SAP 시스템을 지 원하는 Azure 부하 분산 장치가 인스턴스 하나를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-429">hello template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="62912-430">인스턴스 번호가 00, 10, 20 hello ASCS 인스턴스 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-430">hello ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="62912-431">hello SCS 인스턴스는 인스턴스 번호 01, 11, 21에 대해 구성 됩니다...</span><span class="sxs-lookup"><span data-stu-id="62912-431">hello SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="62912-432">hello ASCS Enqueue 복제 서버 (호출자) (Linux에만 해당) 인스턴스는 인스턴스 번호 02, 12, 22에 대해 구성 됩니다...</span><span class="sxs-lookup"><span data-stu-id="62912-432">hello ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="62912-433">hello SCS 호출자 (Linux에만 해당) 인스턴스는 인스턴스 번호 03, 13, 23에 대해 구성 됩니다...</span><span class="sxs-lookup"><span data-stu-id="62912-433">hello SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="62912-434">hello 부하 분산 장치 1에 포함 되어 (Linux 용 2) VIP(s), ASCS/SCS에 대 한 1 x VIP와 호출자 (Linux에만 해당)에 대 한 1 x VIP 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-434">hello load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="62912-435">hello 다음 목록은 모든 부하 분산 규칙 (여기서 x는 hello 수가 hello SAP 시스템, 1, 2, 3... 등).</span><span class="sxs-lookup"><span data-stu-id="62912-435">hello following list contains all load balancing rules (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="62912-436">모든 SAP 시스템에 대한 Windows 특정 포트: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="62912-436">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="62912-437">ASCS 포트(x0 인스턴스 번호): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="62912-437">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="62912-438">SCS 포트(x1 인스턴스 번호): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="62912-438">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="62912-439">Linux의 ASCS ERS 포트(x2 인스턴스 번호): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="62912-439">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="62912-440">Linux의 SCS ERS 포트(x3 인스턴스 번호): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="62912-440">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="62912-441">hello 부하 분산 장치는 프로브 포트 (여기서 x는 hello 수가 hello SAP 시스템, 예를 들어 1, 2, 3 …)를 수행 하는 구성 된 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="62912-441">hello load balancer is configured toouse hello following probe ports (where x is hello number of hello SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="62912-442">ASCS/SCS 내부 부하 분산 장치 프로브 포트: 620x0</span><span class="sxs-lookup"><span data-stu-id="62912-442">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="62912-443">ERS 내부 부하 분산 장치 프로브 포트(Linux 전용): 621x2</span><span class="sxs-lookup"><span data-stu-id="62912-443">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="62912-444"><a name="database-template"></a> 데이터베이스 템플릿</span><span class="sxs-lookup"><span data-stu-id="62912-444"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="62912-445">tooinstall를 사용할 수 있는 두 개의 가상 컴퓨터가 단일 SAP 시스템에 대 한 관계형 데이터베이스 관리 시스템 (RDBMS) hello 또는 hello 데이터베이스 서식 파일 하나를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-445">hello database template deploys one or two virtual machines that you can use tooinstall hello relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="62912-446">예를 들어 5 개의 SAP 시스템에 대 한 ASCS/SCS 템플릿을 배포 하는 경우 필요한 toodeploy이 서식이 파일 5 번입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-446">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="62912-447">hello에 hello 데이터베이스 다중 SID 서식 파일을 tooset [데이터베이스 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-db-marketplace-image] 또는 [관리 하는 디스크를 사용 하 여 데이터베이스 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-db-marketplace-image-md], hello 매개 변수 뒤에 대 한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-447">tooset up hello database multi-SID template, in hello [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="62912-448">**SAP 시스템 ID**. Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-448">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="62912-449">hello ID는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-449">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="62912-450">**OS 종류**.</span><span class="sxs-lookup"><span data-stu-id="62912-450">**Os Type**.</span></span> <span data-ttu-id="62912-451">Hello 가상 컴퓨터의 hello 운영 체제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-451">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="62912-452">**데이터베이스 유형**.</span><span class="sxs-lookup"><span data-stu-id="62912-452">**Dbtype**.</span></span> <span data-ttu-id="62912-453">Hello 유형을 선택 하려는 hello 클러스터에서 tooinstall hello 데이터베이스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-453">Select hello type of hello database you want tooinstall on hello cluster.</span></span> <span data-ttu-id="62912-454">선택 **SQL** tooinstall Microsoft SQL Server를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-454">Select **SQL** if you want tooinstall Microsoft SQL Server.</span></span> <span data-ttu-id="62912-455">선택 **HANA** hello 가상 컴퓨터에서 SAP HANA tooinstall 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="62912-455">Select **HANA** if you plan tooinstall SAP HANA on hello virtual machines.</span></span> <span data-ttu-id="62912-456">Tooselect hello 올바른 운영 체제 형식이 있는지 확인: 선택 **Windows** SQL, 및 HANA에 대 한 Linux 배포를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-456">Make sure tooselect hello correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="62912-457">hello 연결된 toohello 가상 컴퓨터는 Azure 부하 분산 장치 구성 toosupport hello 선택한 데이터베이스 유형:</span><span class="sxs-lookup"><span data-stu-id="62912-457">hello Azure Load Balancer that is connected toohello virtual machines will be configured toosupport hello selected database type:</span></span>
    * <span data-ttu-id="62912-458">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="62912-458">**SQL**.</span></span> <span data-ttu-id="62912-459">hello 부하 분산 장치 부하를 분산 포트를 1433 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-459">hello load balancer will load-balance port 1433.</span></span> <span data-ttu-id="62912-460">SQL Server Always On 설치 프로그램에 대 한이 포트 toouse 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-460">Make sure toouse this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="62912-461">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="62912-461">**HANA**.</span></span> <span data-ttu-id="62912-462">hello 부하 분산 장치 부하 분산을 포트 35015 및 35017 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-462">hello load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="62912-463">인스턴스 번호와 SAP HANA tooinstall 있는지 확인 **50**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-463">Make sure tooinstall SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="62912-464">hello 부하 분산 장치 프로브 포트 62550 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-464">hello load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="62912-465">**SAP 시스템 크기**.</span><span class="sxs-lookup"><span data-stu-id="62912-465">**Sap System Size**.</span></span> <span data-ttu-id="62912-466">설정 hello 개수의 SAPS hello 새 시스템을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-466">Set hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="62912-467">SAPS hello 시스템 내용의 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-467">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="62912-468">**시스템 가용성**.</span><span class="sxs-lookup"><span data-stu-id="62912-468">**System Availability**.</span></span> <span data-ttu-id="62912-469">**HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-469">Select **HA**.</span></span>
  -  <span data-ttu-id="62912-470">**관리자 사용자 이름 및 관리자 암호**.</span><span class="sxs-lookup"><span data-stu-id="62912-470">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="62912-471">Toohello 컴퓨터에서 사용 되는 toosign 일 수 있는 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-471">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="62912-472">**서브넷 ID**. Hello ASCS/SCS 템플릿 배포의 일부로 생성 된 hello 서브넷의 hello ID 또는 hello ASCS/SCS 템플릿의 hello 배포 중에 사용 하는 hello 서브넷의 hello ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-472">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="62912-473"><a name="application-servers-template"></a> 응용 프로그램 서버 템플릿</span><span class="sxs-lookup"><span data-stu-id="62912-473"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="62912-474">hello 응용 프로그램 서버 템플릿은 단일 SAP 시스템에 대 한 SAP 응용 프로그램 서버 인스턴스로 사용할 수 있는 두 개 이상의 가상 컴퓨터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-474">hello application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="62912-475">예를 들어 5 개의 SAP 시스템에 대 한 ASCS/SCS 템플릿을 배포 하는 경우 필요한 toodeploy이 서식이 파일 5 번입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-475">For example, if you deploy an ASCS/SCS template for five SAP systems, you need toodeploy this template five times.</span></span>

<span data-ttu-id="62912-476">hello에 hello 응용 프로그램 서버 다중 SID 템플릿을를 tooset [응용 프로그램 서버 다중 SID 템플릿을] [ sap-templates-3-tier-multisid-apps-marketplace-image] 또는 [관리하는디스크를사용하여응용프로그램서버다중SID템플릿] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], hello 매개 변수 뒤에 대 한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-476">tooset up hello application servers multi-SID template, in hello [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for hello following parameters:</span></span>

  -  <span data-ttu-id="62912-477">**SAP 시스템 ID**. Hello tooinstall 원하는 SAP 시스템의 hello SAP 시스템 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-477">**Sap System Id**. Enter hello SAP system ID of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="62912-478">hello ID는 배포 된 hello 리소스에 대 한 접두사로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-478">hello ID will be used as a prefix for hello resources that are deployed.</span></span>
  -  <span data-ttu-id="62912-479">**OS 종류**.</span><span class="sxs-lookup"><span data-stu-id="62912-479">**Os Type**.</span></span> <span data-ttu-id="62912-480">Hello 가상 컴퓨터의 hello 운영 체제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-480">Select hello operating system of hello virtual machines.</span></span>
  -  <span data-ttu-id="62912-481">**SAP 시스템 크기**.</span><span class="sxs-lookup"><span data-stu-id="62912-481">**Sap System Size**.</span></span> <span data-ttu-id="62912-482">hello 수가 SAPS hello 새 시스템을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-482">hello number of SAPS hello new system will provide.</span></span> <span data-ttu-id="62912-483">SAPS hello 시스템 내용의 확실 하지 않은 경우 SAP 기술 파트너 또는 시스템 통합자에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-483">If you are not sure how many SAPS hello system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="62912-484">**시스템 가용성**.</span><span class="sxs-lookup"><span data-stu-id="62912-484">**System Availability**.</span></span> <span data-ttu-id="62912-485">**HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-485">Select **HA**.</span></span>
  -  <span data-ttu-id="62912-486">**관리자 사용자 이름 및 관리자 암호**.</span><span class="sxs-lookup"><span data-stu-id="62912-486">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="62912-487">Toohello 컴퓨터에서 사용 되는 toosign 일 수 있는 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-487">Create a new user that can be used toosign in toohello machine.</span></span>
  -  <span data-ttu-id="62912-488">**서브넷 ID**. Hello ASCS/SCS 템플릿 배포의 일부로 생성 된 hello 서브넷의 hello ID 또는 hello ASCS/SCS 템플릿의 hello 배포 중에 사용 하는 hello 서브넷의 hello ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-488">**Subnet Id**. Enter hello ID of hello subnet that you used during hello deployment of hello ASCS/SCS template, or hello ID of hello subnet that was created as part of hello ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="62912-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="62912-489"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="62912-490">예에서 hello Azure 가상 네트워크의 주소 공간 hello 10.0.0.0/16 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-490">In our example, hello address space of hello Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="62912-491">**Subnet**이라는 서브넷이 하나 있으며 주소 범위는 10.0.0.0/24입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-491">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="62912-492">모든 가상 컴퓨터와 내부 부하 분산 장치는 이 가상 네트워크에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-492">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62912-493">변경 하지 않은 hello 게스트 운영 체제 내의 toohello 네트워크 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-493">Don't make any changes toohello network settings inside hello guest operating system.</span></span> <span data-ttu-id="62912-494">여기에는 IP 주소, DNS 서버 및 서브넷이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-494">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="62912-495">Azure에서 모든 네트워크 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-495">Configure all your network settings in Azure.</span></span> <span data-ttu-id="62912-496">hello 동적 호스트 구성 프로토콜 (DHCP) 서비스 설정에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-496">hello Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="62912-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP 주소</span><span class="sxs-lookup"><span data-stu-id="62912-497"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="62912-498">tooset hello 필요한 DNS IP 주소, 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-498">tooset hello required DNS IP addresses, do hello following steps.</span></span>

1.  <span data-ttu-id="62912-499">Hello hello에 Azure 포털에서에서 **DNS 서버** 블레이드에서 있는지 확인 가상 네트워크가 **DNS 서버** 옵션이 너무 설정**사용자 지정 DNS**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-499">In hello Azure portal, on hello **DNS servers** blade, make sure that your virtual network **DNS servers** option is set too**Custom DNS**.</span></span>
2.  <span data-ttu-id="62912-500">네트워크의 hello 형식에 따라 설정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-500">Select your settings based on hello type of network you have.</span></span> <span data-ttu-id="62912-501">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="62912-501">For more information, see hello following resources:</span></span>
    * <span data-ttu-id="62912-502">[회사 네트워크 연결 (크로스-프레미스)][planning-guide-2.2]: hello hello 온-프레미스 DNS 서버의 IP 주소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-502">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add hello IP addresses of hello on-premises DNS servers.</span></span>  
    <span data-ttu-id="62912-503">온-프레미스 DNS 서버 toohello 가상 컴퓨터가 Azure에서 실행 되는 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-503">You can extend on-premises DNS servers toohello virtual machines that are running in Azure.</span></span> <span data-ttu-id="62912-504">이 시나리오에서는 hello Azure의 hello IP 주소를 추가할 수 있습니다 hello DNS 서비스를 실행 하는 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="62912-504">In that scenario, you can add hello IP addresses of hello Azure virtual machines on which you run hello DNS service.</span></span>
    * <span data-ttu-id="62912-505">[클라우드 전용 배포][planning-guide-2.1]: hello에 추가 가상 컴퓨터가 배포 DNS 서버 역할을 하는 동일한 가상 네트워크 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="62912-505">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in hello same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="62912-506">Hello Azure의 hello IP 주소 추가 toorun DNS 서비스를 설정한 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="62912-506">Add hello IP addresses of hello Azure virtual machines that you've set up toorun DNS service.</span></span>

    ![그림 12: Azure Virtual Network를 위한 DNS 서버 구성][sap-ha-guide-figure-3001]

    <span data-ttu-id="62912-508">_**그림 12:** Azure Virtual Network를 위한 DNS 서버 구성_</span><span class="sxs-lookup"><span data-stu-id="62912-508">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="62912-509">Toorestart hello Azure 가상 컴퓨터 tooapply 필요한 hello hello DNS 서버의 IP 주소를 변경 하면 변경 hello 및 hello 새 DNS 서버를 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-509">If you change hello IP addresses of hello DNS servers, you need toorestart hello Azure virtual machines tooapply hello change and propagate hello new DNS servers.</span></span>
  >
  >

<span data-ttu-id="62912-510">예에서 hello DNS 서비스가 설치 되 고 이러한 Windows 가상 컴퓨터에 구성:</span><span class="sxs-lookup"><span data-stu-id="62912-510">In our example, hello DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="62912-511">가상 컴퓨터 역할</span><span class="sxs-lookup"><span data-stu-id="62912-511">Virtual machine role</span></span> | <span data-ttu-id="62912-512">가상 컴퓨터 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="62912-512">Virtual machine host name</span></span> | <span data-ttu-id="62912-513">네트워크 카드 이름</span><span class="sxs-lookup"><span data-stu-id="62912-513">Network card name</span></span> | <span data-ttu-id="62912-514">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="62912-514">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62912-515">첫 번째 DNS 서버</span><span class="sxs-lookup"><span data-stu-id="62912-515">First DNS server</span></span> |<span data-ttu-id="62912-516">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="62912-516">domcontr-0</span></span> |<span data-ttu-id="62912-517">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="62912-517">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="62912-518">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="62912-518">10.0.0.10</span></span> |
| <span data-ttu-id="62912-519">두 번째 DNS 서버</span><span class="sxs-lookup"><span data-stu-id="62912-519">Second DNS server</span></span> |<span data-ttu-id="62912-520">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="62912-520">domcontr-1</span></span> |<span data-ttu-id="62912-521">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="62912-521">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="62912-522">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="62912-522">10.0.0.11</span></span> |

### <span data-ttu-id="62912-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>호스트 이름 및 hello SAP ASCS/SCS 클러스터 인스턴스 및 DBMS 클러스터형된 인스턴스에 대 한 고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="62912-523"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for hello SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="62912-524">온-프레미스 배포에 대해 다음의 예약된 호스트 이름 및 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-524">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="62912-525">가상 호스트 이름 역할</span><span class="sxs-lookup"><span data-stu-id="62912-525">Virtual host name role</span></span> | <span data-ttu-id="62912-526">가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="62912-526">Virtual host name</span></span> | <span data-ttu-id="62912-527">가상 고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="62912-527">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62912-528">SAP ASCS/SCS 첫 번째 클러스터 가상 호스트 이름(클러스터 관리용)</span><span class="sxs-lookup"><span data-stu-id="62912-528">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="62912-529">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="62912-529">pr1-ascs-vir</span></span> |<span data-ttu-id="62912-530">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="62912-530">10.0.0.42</span></span> |
| <span data-ttu-id="62912-531">SAP ASCS/SCS 인스턴스 가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="62912-531">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="62912-532">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="62912-532">pr1-ascs-sap</span></span> |<span data-ttu-id="62912-533">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="62912-533">10.0.0.43</span></span> |
| <span data-ttu-id="62912-534">SAP DBMS 두 번째 클러스터 가상 호스트 이름(클러스터 관리용)</span><span class="sxs-lookup"><span data-stu-id="62912-534">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="62912-535">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="62912-535">pr1-dbms-vir</span></span> |<span data-ttu-id="62912-536">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="62912-536">10.0.0.32</span></span> |

<span data-ttu-id="62912-537">Hello 클러스터를 만들 때 hello 가상 호스트 이름을 만들려면 **pr1-ascs-vir** 및 **pr1-dbms-vir** 및 hello 관련 hello 클러스터 자체를 관리 하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-537">When you create hello cluster, create hello virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and hello associated IP addresses that manage hello cluster itself.</span></span> <span data-ttu-id="62912-538">방법에 대 한 정보에 대 한 toodo이,이 참조 [클러스터 구성에서 클러스터 노드 수집][sap-ha-guide-8.12.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-538">For information about how toodo this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="62912-539">수동으로 만들 수 있습니다 hello 다른 두 개의 가상 호스트 이름, **pr1 ascs sap** 및 **pr1 dbms sap**, hello hello DNS 서버의 IP 주소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-539">You can manually create hello other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and hello associated IP addresses, on hello DNS server.</span></span> <span data-ttu-id="62912-540">hello 클러스터 SAP ASCS/SCS 인스턴스 및 클러스터형 hello DBMS 인스턴스 사용 하 여 이러한 리소스.</span><span class="sxs-lookup"><span data-stu-id="62912-540">hello clustered SAP ASCS/SCS instance and hello clustered DBMS instance use these resources.</span></span> <span data-ttu-id="62912-541">방법에 대 한 내용은 toodo이,이 참조 [클러스터 SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들][sap-ha-guide-9.1.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-541">For information about how toodo this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="62912-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Hello SAP 가상 컴퓨터에 대 한 고정 IP 주소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-542"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for hello SAP virtual machines</span></span>
<span data-ttu-id="62912-543">클러스터의 가상 컴퓨터 toouse hello를 배포한 후 모든 가상 컴퓨터 tooset 고정 IP 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-543">After you deploy hello virtual machines toouse in your cluster, you need tooset static IP addresses for all virtual machines.</span></span> <span data-ttu-id="62912-544">Hello 게스트 운영 체제 아니라 hello Azure 가상 네트워크 구성에이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-544">Do this in hello Azure Virtual Network configuration, and not in hello guest operating system.</span></span>

1.  <span data-ttu-id="62912-545">Hello Azure 포털에서에서 선택 **리소스 그룹** > **네트워크 카드** > **설정** > **IP 주소** .</span><span class="sxs-lookup"><span data-stu-id="62912-545">In hello Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="62912-546">Hello에 **IP 주소** 블레이드 아래 **할당**선택, **정적**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-546">On hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="62912-547">Hello에 **IP 주소** 상자 toouse 원하는 hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-547">In hello **IP address** box, enter hello IP address that you want toouse.</span></span>

  > [!NOTE]
  > <span data-ttu-id="62912-548">Toorestart hello Azure 가상 컴퓨터 tooapply hello 네트워크 카드의 hello IP 주소를 변경 하는 경우 해야 hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-548">If you change hello IP address of hello network card, you need toorestart hello Azure virtual machines tooapply hello change.</span></span>  
  >
  >

  ![그림 13: 각 가상 컴퓨터의 네트워크 카드 hello에 대 한 고정 IP 주소 설정][sap-ha-guide-figure-3002]

  <span data-ttu-id="62912-550">_**그림 13:** 각 가상 컴퓨터의 네트워크 카드 hello에 대 한 고정 IP 주소를 설정 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-550">_**Figure 13:** Set static IP addresses for hello network card of each virtual machine_</span></span>

  <span data-ttu-id="62912-551">즉, Active Directory/DNS 서비스에 대 한 toouse 되도록 가상 컴퓨터를 포함 하 여 모든 가상 컴퓨터에 대 한 모든 네트워크 인터페이스에 대해이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-551">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want toouse for your Active Directory/DNS service.</span></span>

<span data-ttu-id="62912-552">예제에서는 다음 가상 컴퓨터 및 고정 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-552">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="62912-553">가상 컴퓨터 역할</span><span class="sxs-lookup"><span data-stu-id="62912-553">Virtual machine role</span></span> | <span data-ttu-id="62912-554">가상 컴퓨터 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="62912-554">Virtual machine host name</span></span> | <span data-ttu-id="62912-555">네트워크 카드 이름</span><span class="sxs-lookup"><span data-stu-id="62912-555">Network card name</span></span> | <span data-ttu-id="62912-556">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="62912-556">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="62912-557">첫 번째 SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="62912-557">First SAP Application Server instance</span></span> |<span data-ttu-id="62912-558">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="62912-558">pr1-di-0</span></span> |<span data-ttu-id="62912-559">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="62912-559">pr1-nic-di-0</span></span> |<span data-ttu-id="62912-560">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="62912-560">10.0.0.50</span></span> |
| <span data-ttu-id="62912-561">두 번째 SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="62912-561">Second SAP Application Server instance</span></span> |<span data-ttu-id="62912-562">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="62912-562">pr1-di-1</span></span> |<span data-ttu-id="62912-563">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="62912-563">pr1-nic-di-1</span></span> |<span data-ttu-id="62912-564">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="62912-564">10.0.0.51</span></span> |
| <span data-ttu-id="62912-565">...</span><span class="sxs-lookup"><span data-stu-id="62912-565">...</span></span> |<span data-ttu-id="62912-566">...</span><span class="sxs-lookup"><span data-stu-id="62912-566">...</span></span> |<span data-ttu-id="62912-567">...</span><span class="sxs-lookup"><span data-stu-id="62912-567">...</span></span> |<span data-ttu-id="62912-568">...</span><span class="sxs-lookup"><span data-stu-id="62912-568">...</span></span> |
| <span data-ttu-id="62912-569">마지막 SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="62912-569">Last SAP Application Server instance</span></span> |<span data-ttu-id="62912-570">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="62912-570">pr1-di-5</span></span> |<span data-ttu-id="62912-571">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="62912-571">pr1-nic-di-5</span></span> |<span data-ttu-id="62912-572">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="62912-572">10.0.0.55</span></span> |
| <span data-ttu-id="62912-573">ASCS/SCS 인스턴스의 첫 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="62912-573">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="62912-574">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="62912-574">pr1-ascs-0</span></span> |<span data-ttu-id="62912-575">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="62912-575">pr1-nic-ascs-0</span></span> |<span data-ttu-id="62912-576">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="62912-576">10.0.0.40</span></span> |
| <span data-ttu-id="62912-577">ASCS/SCS 인스턴스의 두 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="62912-577">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="62912-578">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="62912-578">pr1-ascs-1</span></span> |<span data-ttu-id="62912-579">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="62912-579">pr1-nic-ascs-1</span></span> |<span data-ttu-id="62912-580">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="62912-580">10.0.0.41</span></span> |
| <span data-ttu-id="62912-581">DBMS 인스턴스의 첫 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="62912-581">First cluster node for DBMS instance</span></span> |<span data-ttu-id="62912-582">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="62912-582">pr1-db-0</span></span> |<span data-ttu-id="62912-583">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="62912-583">pr1-nic-db-0</span></span> |<span data-ttu-id="62912-584">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="62912-584">10.0.0.30</span></span> |
| <span data-ttu-id="62912-585">DBMS 인스턴스의 두 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="62912-585">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="62912-586">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="62912-586">pr1-db-1</span></span> |<span data-ttu-id="62912-587">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="62912-587">pr1-nic-db-1</span></span> |<span data-ttu-id="62912-588">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="62912-588">10.0.0.31</span></span> |

### <span data-ttu-id="62912-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Hello Azure 내부 부하 분산 장치에 대 한 고정 IP 주소 설정</span><span class="sxs-lookup"><span data-stu-id="62912-589"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for hello Azure internal load balancer</span></span>

<span data-ttu-id="62912-590">hello SAP Azure 리소스 관리자 템플릿 hello SAP ASCS/SCS 인스턴스 클러스터와 hello DBMS 클러스터에 사용 되는 Azure 내부 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-590">hello SAP Azure Resource Manager template creates an Azure internal load balancer that is used for hello SAP ASCS/SCS instance cluster and hello DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62912-591">hello SAP ASCS/SCS는 hello의 hello 가상 호스트 이름의 IP 주소 hello 동일 hello SAP ASCS/SCS 내부 부하 분산 장치의 hello IP 주소로: **pr1-lb-ascs**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-591">hello IP address of hello virtual host name of hello SAP ASCS/SCS is hello same as hello IP address of hello SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="62912-592">hello DBMS는 hello의 가상 이름 hello의 IP 주소 hello 동일 hello DBMS 내부 부하 분산 장치의 hello IP 주소로: **pr1 lb dbms**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-592">hello IP address of hello virtual name of hello DBMS is hello same as hello IP address of hello DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="62912-593">tooset 내부 Azure hello에 대 한 고정 IP 주소를 부하 분산 장치:</span><span class="sxs-lookup"><span data-stu-id="62912-593">tooset a static IP address for hello Azure internal load balancer:</span></span>

1.  <span data-ttu-id="62912-594">hello 초기 배포 hello 내부 부하 분산 장치 IP 주소 설정 너무**동적**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-594">hello initial deployment sets hello internal load balancer IP address too**Dynamic**.</span></span> <span data-ttu-id="62912-595">Hello hello에 Azure 포털에서에서 **IP 주소** 블레이드 아래 **할당**선택, **정적**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-595">In hello Azure portal, on hello **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="62912-596">Hello 내부 부하 분산 장치의 IP 주소 hello 설정 **pr1-lb-ascs** hello SAP ASCS/SCS 인스턴스의 hello 가상 호스트 이름의 toohello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-596">Set hello IP address of hello internal load balancer **pr1-lb-ascs** toohello IP address of hello virtual host name of hello SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="62912-597">Hello 내부 부하 분산 장치의 IP 주소 hello 설정 **pr1 lb dbms** hello DBMS 인스턴스 hello 가상 호스트 이름의 toohello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-597">Set hello IP address of hello internal load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

  ![그림 14: hello SAP ASCS/SCS 인스턴스에 대 한 hello 내부 부하 분산 장치에 대 한 고정 IP 주소 설정][sap-ha-guide-figure-3003]

  <span data-ttu-id="62912-599">_**그림 14:** hello SAP ASCS/SCS 인스턴스에 대 한 hello 내부 부하 분산 장치에 대 한 고정 IP 주소 설정_</span><span class="sxs-lookup"><span data-stu-id="62912-599">_**Figure 14:** Set static IP addresses for hello internal load balancer for hello SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="62912-600">예제에서는 다음과 같은 고정 IP 주소를 가진 두 개의 Azure 내부 부하 분산 장치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-600">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="62912-601">Azure 내부 부하 분산 장치 역할</span><span class="sxs-lookup"><span data-stu-id="62912-601">Azure internal load balancer role</span></span> | <span data-ttu-id="62912-602">Azure 내부 부하 분산 장치 이름</span><span class="sxs-lookup"><span data-stu-id="62912-602">Azure internal load balancer name</span></span> | <span data-ttu-id="62912-603">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="62912-603">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62912-604">SAP ASCS/SCS 인스턴스 내부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="62912-604">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="62912-605">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="62912-605">pr1-lb-ascs</span></span> |<span data-ttu-id="62912-606">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="62912-606">10.0.0.43</span></span> |
| <span data-ttu-id="62912-607">SAP DBMS 내부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="62912-607">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="62912-608">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="62912-608">pr1-lb-dbms</span></span> |<span data-ttu-id="62912-609">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="62912-609">10.0.0.33</span></span> |


### <span data-ttu-id="62912-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>기본 ASCS/SCS 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙</span><span class="sxs-lookup"><span data-stu-id="62912-610"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="62912-611">hello SAP Azure 리소스 관리자 템플릿은 hello 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-611">hello SAP Azure Resource Manager template creates hello ports you need:</span></span>
* <span data-ttu-id="62912-612">Hello 기본 인스턴스 수와 ABAP ASCS 인스턴스 **00**</span><span class="sxs-lookup"><span data-stu-id="62912-612">An ABAP ASCS instance, with hello default instance number **00**</span></span>
* <span data-ttu-id="62912-613">Hello 기본 인스턴스 번호를 사용 하는 Java SCS 인스턴스 **01**</span><span class="sxs-lookup"><span data-stu-id="62912-613">A Java SCS instance, with hello default instance number **01**</span></span>

<span data-ttu-id="62912-614">Hello 기본 인스턴스 수를 사용 해야 SAP ASCS/SCS 인스턴스를 설치할 때 **00** 프로그램 ABAP ASCS 인스턴스 및 hello 기본 인스턴스 수에 대 한 **01** Java SCS 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-614">When you install your SAP ASCS/SCS instance, you must use hello default instance number **00** for your ABAP ASCS instance and hello default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="62912-615">다음에 필요한 내부 부하 분산 hello SAP NetWeaver 포트에 대 한 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-615">Next, create required internal load balancing endpoints for hello SAP NetWeaver ports.</span></span>

<span data-ttu-id="62912-616">toocreate 필수 내부 부하 분산 끝점을 먼저 이러한 부하 분산 hello SAP NetWeaver ABAP ASCS 포트에 대 한 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-616">toocreate required internal load balancing endpoints, first, create these load balancing endpoints for hello SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="62912-617">서비스/부하 분산 규칙 이름</span><span class="sxs-lookup"><span data-stu-id="62912-617">Service/load balancing rule name</span></span> | <span data-ttu-id="62912-618">기본 포트 번호</span><span class="sxs-lookup"><span data-stu-id="62912-618">Default port numbers</span></span> | <span data-ttu-id="62912-619">(인스턴스 번호가 00인 ASCS 인스턴스)(ERS가 10)에 대한 구체적인 포트</span><span class="sxs-lookup"><span data-stu-id="62912-619">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62912-620">서버를 큐에 넣기/ *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="62912-620">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="62912-621">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-621">32<*InstanceNumber*></span></span> |<span data-ttu-id="62912-622">3200</span><span class="sxs-lookup"><span data-stu-id="62912-622">3200</span></span> |
| <span data-ttu-id="62912-623">ABAP 메시지 서버/ *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="62912-623">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="62912-624">36<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-624">36<*InstanceNumber*></span></span> |<span data-ttu-id="62912-625">3600</span><span class="sxs-lookup"><span data-stu-id="62912-625">3600</span></span> |
| <span data-ttu-id="62912-626">내부 ABAP 메시지/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="62912-626">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="62912-627">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-627">39<*InstanceNumber*></span></span> |<span data-ttu-id="62912-628">3900</span><span class="sxs-lookup"><span data-stu-id="62912-628">3900</span></span> |
| <span data-ttu-id="62912-629">메시지 서버 HTTP/ *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="62912-629">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="62912-630">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-630">81<*InstanceNumber*></span></span> |<span data-ttu-id="62912-631">8100</span><span class="sxs-lookup"><span data-stu-id="62912-631">8100</span></span> |
| <span data-ttu-id="62912-632">SAP 시작 서비스 ASCS HTTP/ *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="62912-632">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="62912-633">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="62912-633">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="62912-634">50013</span><span class="sxs-lookup"><span data-stu-id="62912-634">50013</span></span> |
| <span data-ttu-id="62912-635">SAP 시작 서비스 ASCS HTTP/ *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="62912-635">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="62912-636">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="62912-636">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="62912-637">50014</span><span class="sxs-lookup"><span data-stu-id="62912-637">50014</span></span> |
| <span data-ttu-id="62912-638">복제를 큐에 넣기/ *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="62912-638">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="62912-639">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="62912-639">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="62912-640">50016</span><span class="sxs-lookup"><span data-stu-id="62912-640">50016</span></span> |
| <span data-ttu-id="62912-641">SAP 시작 서비스 ERS HTTP/ *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="62912-641">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="62912-642">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="62912-642">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="62912-643">51013</span><span class="sxs-lookup"><span data-stu-id="62912-643">51013</span></span> |
| <span data-ttu-id="62912-644">SAP 시작 서비스 ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="62912-644">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="62912-645">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="62912-645">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="62912-646">51014</span><span class="sxs-lookup"><span data-stu-id="62912-646">51014</span></span> |
| <span data-ttu-id="62912-647">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="62912-647">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="62912-648">5985</span><span class="sxs-lookup"><span data-stu-id="62912-648">5985</span></span> |
| <span data-ttu-id="62912-649">파일 공유 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="62912-649">File Share *Lbrule445*</span></span> | |<span data-ttu-id="62912-650">445</span><span class="sxs-lookup"><span data-stu-id="62912-650">445</span></span> |

<span data-ttu-id="62912-651">_**표 1:** 포트 번호가 hello SAP NetWeaver ABAP ASCS 인스턴스_</span><span class="sxs-lookup"><span data-stu-id="62912-651">_**Table 1:** Port numbers of hello SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="62912-652">그런 다음 이러한 부하 분산 hello SAP NetWeaver Java SCS 포트에 대 한 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-652">Then, create these load balancing endpoints for hello SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="62912-653">서비스/부하 분산 규칙 이름</span><span class="sxs-lookup"><span data-stu-id="62912-653">Service/load balancing rule name</span></span> | <span data-ttu-id="62912-654">기본 포트 번호</span><span class="sxs-lookup"><span data-stu-id="62912-654">Default port numbers</span></span> | <span data-ttu-id="62912-655">(인스턴스 번호가 01인 SCS 인스턴스)(ERS가 11)에 대한 구체적인 포트</span><span class="sxs-lookup"><span data-stu-id="62912-655">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62912-656">서버를 큐에 넣기/ *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="62912-656">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="62912-657">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-657">32<*InstanceNumber*></span></span> |<span data-ttu-id="62912-658">3201</span><span class="sxs-lookup"><span data-stu-id="62912-658">3201</span></span> |
| <span data-ttu-id="62912-659">게이트웨이 서버/ *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="62912-659">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="62912-660">33<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-660">33<*InstanceNumber*></span></span> |<span data-ttu-id="62912-661">3301</span><span class="sxs-lookup"><span data-stu-id="62912-661">3301</span></span> |
| <span data-ttu-id="62912-662">Java 메시지 서버/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="62912-662">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="62912-663">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-663">39<*InstanceNumber*></span></span> |<span data-ttu-id="62912-664">3901</span><span class="sxs-lookup"><span data-stu-id="62912-664">3901</span></span> |
| <span data-ttu-id="62912-665">메시지 서버 HTTP/ *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="62912-665">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="62912-666">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="62912-666">81<*InstanceNumber*></span></span> |<span data-ttu-id="62912-667">8101</span><span class="sxs-lookup"><span data-stu-id="62912-667">8101</span></span> |
| <span data-ttu-id="62912-668">SAP 시작 서비스 SCS HTTP/ *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="62912-668">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="62912-669">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="62912-669">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="62912-670">50113</span><span class="sxs-lookup"><span data-stu-id="62912-670">50113</span></span> |
| <span data-ttu-id="62912-671">SAP 시작 서비스 SCS HTTP/ *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="62912-671">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="62912-672">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="62912-672">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="62912-673">50114</span><span class="sxs-lookup"><span data-stu-id="62912-673">50114</span></span> |
| <span data-ttu-id="62912-674">복제를 큐에 넣기/ *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="62912-674">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="62912-675">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="62912-675">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="62912-676">50116</span><span class="sxs-lookup"><span data-stu-id="62912-676">50116</span></span> |
| <span data-ttu-id="62912-677">SAP 시작 서비스 ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="62912-677">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="62912-678">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="62912-678">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="62912-679">51113</span><span class="sxs-lookup"><span data-stu-id="62912-679">51113</span></span> |
| <span data-ttu-id="62912-680">SAP 시작 서비스 ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="62912-680">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="62912-681">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="62912-681">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="62912-682">51114</span><span class="sxs-lookup"><span data-stu-id="62912-682">51114</span></span> |
| <span data-ttu-id="62912-683">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="62912-683">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="62912-684">5985</span><span class="sxs-lookup"><span data-stu-id="62912-684">5985</span></span> |
| <span data-ttu-id="62912-685">파일 공유 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="62912-685">File Share *Lbrule445*</span></span> | |<span data-ttu-id="62912-686">445</span><span class="sxs-lookup"><span data-stu-id="62912-686">445</span></span> |

<span data-ttu-id="62912-687">_**표 2:** 포트 번호가 hello SAP NetWeaver Java SCS 인스턴스의_</span><span class="sxs-lookup"><span data-stu-id="62912-687">_**Table 2:** Port numbers of hello SAP NetWeaver Java SCS instances_</span></span>

![그림 15: 기본 ASCS/SCS 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙][sap-ha-guide-figure-3004]

<span data-ttu-id="62912-689">_**그림 15:** 기본 ASCS/SCS 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙_</span><span class="sxs-lookup"><span data-stu-id="62912-689">_**Figure 15:** Default ASCS/SCS load balancing rules for hello Azure internal load balancer_</span></span>

<span data-ttu-id="62912-690">Hello 부하 분산 장치의 IP 주소 hello 설정 **pr1 lb dbms** hello DBMS 인스턴스 hello 가상 호스트 이름의 toohello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-690">Set hello IP address of hello load balancer **pr1-lb-dbms** toohello IP address of hello virtual host name of hello DBMS instance.</span></span>

### <span data-ttu-id="62912-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Hello ASCS/SCS 기본 부하 분산 규칙 hello Azure 내부 부하 분산 장치에 대 한 변경</span><span class="sxs-lookup"><span data-stu-id="62912-691"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer</span></span>

<span data-ttu-id="62912-692">Hello SAP ASCS 또는 SCS 인스턴스에 대 한 숫자가 다른 toouse 원하는 기본값에서 해당 포트의 hello 이름 및 값을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-692">If you want toouse different numbers for hello SAP ASCS or SCS instances, you must change hello names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="62912-693">Hello Azure 포털에서에서 선택  **<* SID*> 파운드-ascs 부하 분산 장치 * * > **부하 분산 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-693">In hello Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="62912-694">모든를 부하 분산 toohello SAP ASCS 또는 SCS 인스턴스에 속하는 규칙에 대 한 이러한 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-694">For all load balancing rules that belong toohello SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="62912-695">이름</span><span class="sxs-lookup"><span data-stu-id="62912-695">Name</span></span>
  * <span data-ttu-id="62912-696">포트</span><span class="sxs-lookup"><span data-stu-id="62912-696">Port</span></span>
  * <span data-ttu-id="62912-697">백 엔드 포트</span><span class="sxs-lookup"><span data-stu-id="62912-697">Back-end port</span></span>

  <span data-ttu-id="62912-698">예를 들어 00 too31에서 toochange hello 기본 ASCS 인스턴스 번호를 사용 하도록 하려는 경우 표 1에 나열 된 모든 포트에 대 한 toomake hello 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-698">For example, if you want toochange hello default ASCS instance number from 00 too31, you need toomake hello changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="62912-699">다음은 포트 *lbrule3200*에 대한 업데이트 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-699">Here's an example of an update for port *lbrule3200*.</span></span>

  ![그림 16: hello ASCS/SCS 기본 부하 분산 규칙 hello Azure 내부 부하 분산 장치에 대 한 변경][sap-ha-guide-figure-3005]

  <span data-ttu-id="62912-701">_**그림 16:** 변경 hello ASCS/SCS 기본 부하 분산 hello Azure 내부 부하 분산 장치에 대 한 규칙_</span><span class="sxs-lookup"><span data-stu-id="62912-701">_**Figure 16:** Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer_</span></span>

### <span data-ttu-id="62912-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Windows 가상 컴퓨터 toohello 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="62912-702"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines toohello domain</span></span>

<span data-ttu-id="62912-703">정적 IP 주소 toohello 가상 컴퓨터를 할당 하면 hello 가상 컴퓨터 toohello 도메인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-703">After you assign a static IP address toohello virtual machines, add hello virtual machines toohello domain.</span></span>

![그림 17: 가상 컴퓨터 tooa 도메인 추가][sap-ha-guide-figure-3006]

<span data-ttu-id="62912-705">_**그림 17:** 가상 컴퓨터 tooa 도메인 추가_</span><span class="sxs-lookup"><span data-stu-id="62912-705">_**Figure 17:** Add a virtual machine tooa domain_</span></span>

### <span data-ttu-id="62912-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Hello SAP ASCS/SCS 인스턴스의 클러스터 노드 모두에 레지스트리 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-706"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance</span></span>

<span data-ttu-id="62912-707">Azure 부하 분산 장치 닫히는 연결 hello 연결의 일정 시간 동안 유휴 상태인 시간 (유휴 시간 제한을) 하는 내부 부하 분산 장치를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-707">Azure Load Balancer has an internal load balancer that closes connections when hello connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="62912-708">대화 상자 인스턴스 열려 있는 연결 toohello SAP 인 큐에서 SAP 작업 프로세스 요구 toobe 전송 요청 hello 첫 큐에 넣지/큐에서 제거 되는 즉시 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-708">SAP work processes in dialog instances open connections toohello SAP enqueue process as soon as hello first enqueue/dequeue request needs toobe sent.</span></span> <span data-ttu-id="62912-709">이러한 연결은 일반적으로 시작할 때 까지는 설정 된 hello 작업 프로세스 또는 hello enqueue 프로세스가 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-709">These connections usually remain established until hello work process or hello enqueue process restarts.</span></span> <span data-ttu-id="62912-710">그러나 설정된 된 시간 동안에 대 한 hello 연결이 유휴 상태 이면 경우 hello Azure 내부 부하 분산 장치 닫히는 hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-710">However, if hello connection is idle for a set period of time, hello Azure internal load balancer closes hello connections.</span></span> <span data-ttu-id="62912-711">더 이상 없으면 hello 연결 toohello enqueue 프로세스를 다시 만들고 hello SAP 작업 프로세스 때문에 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-711">This isn't a problem because hello SAP work process reestablishes hello connection toohello enqueue process if it no longer exists.</span></span> <span data-ttu-id="62912-712">이러한 활동은 SAP 프로세스의 개발자 추적이 hello에 설명 되어 있지만 해당 추적에 많은 양의 추가 콘텐츠를 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-712">These activities are documented in hello developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="62912-713">것이 좋습니다 toochange hello TCP/IP `KeepAliveTime` 및 `KeepAliveInterval` 클러스터 노드 모두에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-713">It's a good idea toochange hello TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="62912-714">이러한 변경에 SAP 프로필 매개 변수를 hello 문서의 뒷부분에 설명 된 hello TCP/IP 매개 변수를 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-714">Combine these changes in hello TCP/IP parameters with SAP profile parameters, described later in hello article.</span></span>

<span data-ttu-id="62912-715">먼저, hello SAP ASCS/SCS 인스턴스의 클러스터 노드 모두에서 tooadd 레지스트리 항목 이러한 Windows 레지스트리 항목에 대 한 SAP ASCS/SCS Windows 클러스터 노드 모두에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-715">tooadd registry entries on both cluster nodes of hello SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="62912-716">Path</span><span class="sxs-lookup"><span data-stu-id="62912-716">Path</span></span> | <span data-ttu-id="62912-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="62912-717">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="62912-718">변수 이름</span><span class="sxs-lookup"><span data-stu-id="62912-718">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="62912-719">변수 유형</span><span class="sxs-lookup"><span data-stu-id="62912-719">Variable type</span></span> |<span data-ttu-id="62912-720">REG_DWORD(10진수)</span><span class="sxs-lookup"><span data-stu-id="62912-720">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="62912-721">값</span><span class="sxs-lookup"><span data-stu-id="62912-721">Value</span></span> |<span data-ttu-id="62912-722">120000</span><span class="sxs-lookup"><span data-stu-id="62912-722">120000</span></span> |
| <span data-ttu-id="62912-723">링크 toodocumentation</span><span class="sxs-lookup"><span data-stu-id="62912-723">Link toodocumentation</span></span> |[<span data-ttu-id="62912-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="62912-724">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="62912-725">_**표 3:** 변경 hello 첫 번째 TCP/IP 매개 변수_</span><span class="sxs-lookup"><span data-stu-id="62912-725">_**Table 3:** Change hello first TCP/IP parameter_</span></span>

<span data-ttu-id="62912-726">그런 다음 SAP ASCS/SCS에 대한 두 Windows 클러스터 노드에 대해 다음 Windows 레지스트리 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-726">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="62912-727">Path</span><span class="sxs-lookup"><span data-stu-id="62912-727">Path</span></span> | <span data-ttu-id="62912-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="62912-728">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="62912-729">변수 이름</span><span class="sxs-lookup"><span data-stu-id="62912-729">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="62912-730">변수 유형</span><span class="sxs-lookup"><span data-stu-id="62912-730">Variable type</span></span> |<span data-ttu-id="62912-731">REG_DWORD(10진수)</span><span class="sxs-lookup"><span data-stu-id="62912-731">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="62912-732">값</span><span class="sxs-lookup"><span data-stu-id="62912-732">Value</span></span> |<span data-ttu-id="62912-733">120000</span><span class="sxs-lookup"><span data-stu-id="62912-733">120000</span></span> |
| <span data-ttu-id="62912-734">링크 toodocumentation</span><span class="sxs-lookup"><span data-stu-id="62912-734">Link toodocumentation</span></span> |[<span data-ttu-id="62912-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="62912-735">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="62912-736">_**표 4:** 변경 hello 두 번째 TCP/IP 매개 변수_</span><span class="sxs-lookup"><span data-stu-id="62912-736">_**Table 4:** Change hello second TCP/IP parameter_</span></span>

<span data-ttu-id="62912-737">**클러스터 노드 모두를 다시 시작 tooapply hello 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-737">**tooapply hello changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="62912-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> SAP ASCS/SCS 인스턴스에 대한 Windows Server 장애 조치 클러스터링 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="62912-738"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="62912-739">SAP ASCS/SCS 인스턴스의 Windows Server 장애 조치(failover) 클러스터링 클러스터 설정은 다음과 같은 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-739">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="62912-740">클러스터 구성에서 클러스터 노드 hello를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-740">Collecting hello cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="62912-741">클러스터 파일 공유 감시 구성</span><span class="sxs-lookup"><span data-stu-id="62912-741">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="62912-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>클러스터 구성에서 클러스터 노드 hello를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-742"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect hello cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="62912-743">Hello 추가 역할 및 기능 마법사에서 장애 조치 클러스터링 tooboth 클러스터 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-743">In hello Add Role and Features Wizard, add failover clustering tooboth cluster nodes.</span></span>
2.  <span data-ttu-id="62912-744">장애 조치 클러스터 관리자를 사용 하 여 hello 장애 조치 클러스터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-744">Set up hello failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="62912-745">장애 조치 클러스터 관리자에서 선택 **클러스터 만들기**, 다음 hello 첫 번째 클러스터, 노드 A의 hello 이름만 추가 아직; hello 두 번째 노드 추가 하지 마십시오 이후 단계에서 hello 두 번째 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-745">In Failover Cluster Manager, select **Create Cluster**, and then add only hello name of hello first cluster, node A. Do not add hello second node yet; you'll add hello second node in a later step.</span></span>

  ![그림 18: hello 서버 또는 가상 컴퓨터 이름 hello 첫 번째 클러스터 노드 추가][sap-ha-guide-figure-3007]

  <span data-ttu-id="62912-747">_**그림 18:** hello 첫 번째 클러스터 노드 추가 hello 서버 또는 가상 컴퓨터 이름_</span><span class="sxs-lookup"><span data-stu-id="62912-747">_**Figure 18:** Add hello server or virtual machine name of hello first cluster node_</span></span>

3.  <span data-ttu-id="62912-748">Hello hello 클러스터의 네트워크 이름 (가상 호스트 이름)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-748">Enter hello network name (virtual host name) of hello cluster.</span></span>

  ![그림 19: hello 클러스터 이름을 입력 하십시오.][sap-ha-guide-figure-3008]

  <span data-ttu-id="62912-750">_**그림 19:** hello 클러스터 이름 입력_</span><span class="sxs-lookup"><span data-stu-id="62912-750">_**Figure 19:** Enter hello cluster name_</span></span>

4.  <span data-ttu-id="62912-751">Hello 클러스터를 만든 후 클러스터 유효성 검사 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-751">After you've created hello cluster, run a cluster validation test.</span></span>

  ![그림 20: hello 클러스터 유효성 검사를 실행합니다.][sap-ha-guide-figure-3009]

  <span data-ttu-id="62912-753">_**그림 20:** hello 클러스터 유효성 검사를 실행 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-753">_**Figure 20:** Run hello cluster validation check_</span></span>

  <span data-ttu-id="62912-754">Hello 프로세스의이 시점에 디스크에 대 한 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-754">You can ignore any warnings about disks at this point in hello process.</span></span> <span data-ttu-id="62912-755">파일 공유 감시 및 hello SIOS 공유 디스크 나중에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-755">You'll add a file share witness and hello SIOS shared disks later.</span></span> <span data-ttu-id="62912-756">이 단계에서는 tooworry 쿼럼에 대 한 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-756">At this stage, you don't need tooworry about having a quorum.</span></span>

  ![그림 21: 쿼럼 디스크가 없음][sap-ha-guide-figure-3010]

  <span data-ttu-id="62912-758">_**그림 21:** 쿼럼 디스크가 없음_</span><span class="sxs-lookup"><span data-stu-id="62912-758">_**Figure 21:** No quorum disk is found_</span></span>

  ![그림 22: 새 IP 주소가 필요한 코어 클러스터 리소스][sap-ha-guide-figure-3011]

  <span data-ttu-id="62912-760">_**그림 22:** 새 IP 주소가 필요한 코어 클러스터 리소스_</span><span class="sxs-lookup"><span data-stu-id="62912-760">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="62912-761">Hello 코어 클러스터 서비스의 hello IP 주소를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-761">Change hello IP address of hello core cluster service.</span></span> <span data-ttu-id="62912-762">hello 클러스터 hello 서버의 IP 주소가 hello tooone hello 가상 컴퓨터 노드를 가리키므로 hello 핵심 클러스터 서비스의 hello IP 주소를 변경할 때까지 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-762">hello cluster can't start until you change hello IP address of hello core cluster service, because hello IP address of hello server points tooone of hello virtual machine nodes.</span></span> <span data-ttu-id="62912-763">Hello에서 이렇게 **속성** hello 코어 클러스터 서비스의 IP 리소스의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-763">Do this on hello **Properties** page of hello core cluster service's IP resource.</span></span>

  <span data-ttu-id="62912-764">예를 들어 tooassign IP 주소 필요 (예에서 **10.0.0.42**) hello 클러스터 가상 호스트 이름에 대 한 **pr1-ascs-vir**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-764">For example, we need tooassign an IP address (in our example, **10.0.0.42**) for hello cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![그림 23: hello 속성 대화 상자, hello IP 주소를 변경][sap-ha-guide-figure-3012]

  <span data-ttu-id="62912-766">_**그림 23:** hello에 **속성** 대화 상자, hello IP 주소 변경_</span><span class="sxs-lookup"><span data-stu-id="62912-766">_**Figure 23:** In hello **Properties** dialog box, change hello IP address_</span></span>

  ![그림 24: hello 클러스터에 대 한 예약 된 hello IP 주소를 할당 합니다.][sap-ha-guide-figure-3013]

  <span data-ttu-id="62912-768">_**그림 24:** hello 클러스터에 대 한 예약 된 hello IP 주소 할당_</span><span class="sxs-lookup"><span data-stu-id="62912-768">_**Figure 24:** Assign hello IP address that is reserved for hello cluster_</span></span>

6.  <span data-ttu-id="62912-769">Hello 클러스터 가상 호스트 이름을 온라인 상태로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-769">Bring hello cluster virtual host name online.</span></span>

  ![그림 25: 클러스터 코어 서비스가 작동 중 이며 hello로 실행 되 고 IP 주소를 수정][sap-ha-guide-figure-3014]

  <span data-ttu-id="62912-771">_**그림 25:** 클러스터 코어 서비스가 작동 중 이며 실행 되 고 hello로 IP 주소를 수정_</span><span class="sxs-lookup"><span data-stu-id="62912-771">_**Figure 25:** Cluster core service is up and running, and with hello correct IP address_</span></span>

7.  <span data-ttu-id="62912-772">Hello 두 번째 클러스터 노드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-772">Add hello second cluster node.</span></span>

  <span data-ttu-id="62912-773">Hello 코어 클러스터 서비스가 실행 되 고, 했으므로 hello 두 번째 클러스터 노드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-773">Now that hello core cluster service is up and running, you can add hello second cluster node.</span></span>

  ![그림 26: hello 두 번째 클러스터 노드 추가][sap-ha-guide-figure-3015]

  <span data-ttu-id="62912-775">_**그림 26:** 추가 hello 두 번째 클러스터 노드_</span><span class="sxs-lookup"><span data-stu-id="62912-775">_**Figure 26:** Add hello second cluster node_</span></span>

8.  <span data-ttu-id="62912-776">두 번째 클러스터 노드 호스트 hello에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-776">Enter a name for hello second cluster node host.</span></span>

  ![그림 27: hello 두 번째 클러스터 노드 호스트 이름을 입력 하십시오.][sap-ha-guide-figure-3016]

  <span data-ttu-id="62912-778">_**그림 27:** hello 두 번째 클러스터 노드 호스트 이름 입력_</span><span class="sxs-lookup"><span data-stu-id="62912-778">_**Figure 27:** Enter hello second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="62912-779">해당 hello 해야 **모든 적합 한 저장소 toohello 클러스터 추가** 확인란은 **하지** 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-779">Be sure that hello **Add all eligible storage toohello cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![그림 28: hello 확인란을 선택 하지 마십시오][sap-ha-guide-figure-3017]

  <span data-ttu-id="62912-781">_**그림 28:** 않습니다 **하지** 선택 hello 확인란_</span><span class="sxs-lookup"><span data-stu-id="62912-781">_**Figure 28:** Do **not** select hello check box_</span></span>

  <span data-ttu-id="62912-782">쿼럼 및 디스크에 대한 경고는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-782">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="62912-783">설정 hello 쿼럼 및 공유 hello 디스크 나중에 설명 된 대로 [SAP ASCS/SCS 클러스터 공유 디스크에 대 한 SIOS DataKeeper Cluster Edition 설치][sap-ha-guide-8.12.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-783">You'll set hello quorum and share hello disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![그림 29: hello 디스크 쿼럼에 대 한 경고를 무시 합니다.][sap-ha-guide-figure-3018]

  <span data-ttu-id="62912-785">_**그림 29:** hello 디스크 쿼럼에 대 한 경고를 무시_</span><span class="sxs-lookup"><span data-stu-id="62912-785">_**Figure 29:** Ignore warnings about hello disk quorum_</span></span>


#### <span data-ttu-id="62912-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> 클러스터 파일 공유 감시 구성</span><span class="sxs-lookup"><span data-stu-id="62912-786"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="62912-787">클러스터 파일 공유 감시 구성은 다음과 같은 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-787">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="62912-788">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="62912-788">Creating a file share</span></span>
- <span data-ttu-id="62912-789">장애 조치 클러스터 관리자에서 파일 공유 감시 쿼럼 hello 설정</span><span class="sxs-lookup"><span data-stu-id="62912-789">Setting hello file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="62912-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="62912-790"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="62912-791">쿼럼 디스크 대신 파일 공유 감시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-791">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="62912-792">SIOS DataKeeper는 이 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-792">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="62912-793">이 문서의 hello 예에서 hello 파일 공유 감시는 Azure에서 실행 중인 hello Active Directory/DNS 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-793">In hello examples in this article, hello file share witness is on hello Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="62912-794">hello 파일 공유 감시 라고 **domcontr 0**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-794">hello file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="62912-795">사이트 간 VPN 이나 Azure express 경로) (통해 VPN 연결 tooAzure 구성한 것 때문에 Active Directory/DNS 서비스가 온-프레미스 이며 되지 않습니다. 적합 한 toorun 파일 공유 감시 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-795">Because you would have configured a VPN connection tooAzure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable toorun a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="62912-796">온-프레미스 Active Directory/DNS 서비스가 실행 되는 경우 온-프레미스를 실행 하는 hello Active Directory/DNS Windows 운영 체제에서 파일 공유 감시를 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="62912-796">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on hello Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="62912-797">Azure 및 Active Directory/DNS 온-프레미스로 실행되는 클러스터 노드 간 네트워크 대기 시간이 너무 커서 연결 문제를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-797">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="62912-798">닫기 toohello 클러스터 노드를 실행 하는 Azure 가상 컴퓨터에 있는지 tooconfigure hello 파일 공유 감시를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-798">Be sure tooconfigure hello file share witness on an Azure virtual machine that is running close toohello cluster node.</span></span>  
  >
  >

  <span data-ttu-id="62912-799">hello 쿼럼 드라이브에는 최소한 1, 024 MB의 여유 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-799">hello quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="62912-800">2, 048 MB의 여유 공간 hello 쿼럼 드라이브에 대 한 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-800">We recommend 2,048 MB of free space for hello quorum drive.</span></span>

2.  <span data-ttu-id="62912-801">Hello 클러스터 이름 개체를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-801">Add hello cluster name object.</span></span>

  ![그림 30: hello 클러스터 이름 개체에 대 한 hello 공유에 hello 권한 할당][sap-ha-guide-figure-3019]

  <span data-ttu-id="62912-803">_**그림 30:** hello 클러스터 이름 개체에 대 한 hello 공유에 hello 권한 할당_</span><span class="sxs-lookup"><span data-stu-id="62912-803">_**Figure 30:** Assign hello permissions on hello share for hello cluster name object_</span></span>

  <span data-ttu-id="62912-804">Hello 권한을 hello 클러스터 이름 개체에 대 한 hello 공유 hello 기관 toochange 데이터를 포함 (예에서 **pr1-ascs-vir$**).</span><span class="sxs-lookup"><span data-stu-id="62912-804">Be sure that hello permissions include hello authority toochange data in hello share for hello cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="62912-805">tooadd hello 클러스터 이름 개체 toohello 목록 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-805">tooadd hello cluster name object toohello list, select **Add**.</span></span> <span data-ttu-id="62912-806">그림 31에 표시 된 더하기 toothose에서 컴퓨터 개체에 대 한 필터 toocheck hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-806">Change hello filter toocheck for computer objects, in addition toothose shown in Figure 31.</span></span>

  ![그림 31: hello 개체 유형 tooinclude 컴퓨터 변경][sap-ha-guide-figure-3020]

  <span data-ttu-id="62912-808">_**그림 31:** hello 개체 유형 tooinclude 컴퓨터 변경_</span><span class="sxs-lookup"><span data-stu-id="62912-808">_**Figure 31:** Change hello Object Types tooinclude computers_</span></span>

  ![그림 32: hello 컴퓨터 확인란을 선택][sap-ha-guide-figure-3021]

  <span data-ttu-id="62912-810">_**그림 32:** 선택 hello **컴퓨터** 확인란_</span><span class="sxs-lookup"><span data-stu-id="62912-810">_**Figure 32:** Select hello **Computers** check box_</span></span>

4.  <span data-ttu-id="62912-811">그림 31와 같이 hello 클러스터 이름 개체를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-811">Enter hello cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="62912-812">Hello 레코드가 이미 생성 되어 때문에 그림 30에서와 같이 hello 사용 권한을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-812">Because hello record has already been created, you can change hello permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="62912-813">선택 hello **보안** hello 공유를 제거한 다음 설정의 탭에는 자세한 hello 클러스터 이름 개체에 대 한 권한.</span><span class="sxs-lookup"><span data-stu-id="62912-813">Select hello **Security** tab of hello share, and then set more detailed permissions for hello cluster name object.</span></span>

  ![그림 33: hello 파일 공유 쿼럼에 hello 클러스터 이름 개체에 대 한 보안 특성 hello 설정][sap-ha-guide-figure-3022]

  <span data-ttu-id="62912-815">_**그림 33:** hello 파일 공유 쿼럼에 hello 클러스터 이름 개체에 대 한 hello 보안 특성을 설정 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-815">_**Figure 33:** Set hello security attributes for hello cluster name object on hello file share quorum_</span></span>

##### <span data-ttu-id="62912-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>장애 조치 클러스터 관리자에서 파일 공유 감시 쿼럼 hello 설정</span><span class="sxs-lookup"><span data-stu-id="62912-816"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set hello file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="62912-817">Hello 쿼럼 설정 구성 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="62912-817">Open hello Configure Quorum Setting Wizard.</span></span>

  ![그림 34: hello 구성 클러스터 쿼럼 설정 마법사를 시작 합니다.][sap-ha-guide-figure-3023]

  <span data-ttu-id="62912-819">_**그림 34:** 시작 hello 클러스터 쿼럼 구성 설정 마법사_</span><span class="sxs-lookup"><span data-stu-id="62912-819">_**Figure 34:** Start hello Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="62912-820">Hello에 **쿼럼 구성 선택** 페이지 **hello 쿼럼 감시 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-820">On hello **Select Quorum Configuration** page, select **Select hello quorum witness**.</span></span>

  ![그림 35: 선택할 수 있는 쿼럼 구성][sap-ha-guide-figure-3024]

  <span data-ttu-id="62912-822">_**그림 35:** 선택할 수 있는 쿼럼 구성_</span><span class="sxs-lookup"><span data-stu-id="62912-822">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="62912-823">Hello에 **쿼럼 감시 선택** 페이지 **파일 공유 감시 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-823">On hello **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![그림 36: 선택 hello 파일 공유 감시][sap-ha-guide-figure-3025]

  <span data-ttu-id="62912-825">_**그림 36:** hello 파일 공유 감시를 선택 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-825">_**Figure 36:** Select hello file share witness_</span></span>

4.  <span data-ttu-id="62912-826">Hello UNC 경로 toohello 파일 공유를 입력 하십시오 (예제에서는 \\domcontr 0\FSW).</span><span class="sxs-lookup"><span data-stu-id="62912-826">Enter hello UNC path toohello file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="62912-827">toosee hello 변경할 수 있는, 선택 목록 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-827">toosee a list of hello changes you can make, select **Next**.</span></span>

  ![그림 37: hello 미러링 모니터 서버 공유에 대 한 hello 파일 공유 위치를 정의 합니다.][sap-ha-guide-figure-3026]

  <span data-ttu-id="62912-829">_**그림 37:** hello 미러링 모니터 서버 공유에 대 한 hello 파일 공유 위치를 정의 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-829">_**Figure 37:** Define hello file share location for hello witness share_</span></span>

5.  <span data-ttu-id="62912-830">한 다음 선택 hello 변경 내용을 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-830">Select hello changes you want, and then select **Next**.</span></span> <span data-ttu-id="62912-831">Toosuccessfully 필요한 38 그림에에서 표시 된 대로 hello 클러스터 구성을 다시 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-831">You need toosuccessfully reconfigure hello cluster configuration as shown in Figure 38.</span></span>  

  ![Hello 클러스터를 다시 구성 했으므로 그림 38: 확인][sap-ha-guide-figure-3027]

  <span data-ttu-id="62912-833">_**그림 38:** hello 클러스터를 다시 구성 했으면 확인_</span><span class="sxs-lookup"><span data-stu-id="62912-833">_**Figure 38:** Confirmation that you've reconfigured hello cluster_</span></span>

<span data-ttu-id="62912-834">Hello Windows 장애 조치 클러스터를 성공적으로 설치한 후 변경 내용을 toosome 임계값 tooadapt 장애 조치가 감지 tooconditions Azure에서 만든 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-834">After installing hello Windows Failover Cluster successfully, changes need toobe made toosome thresholds tooadapt failover detection tooconditions in Azure.</span></span> <span data-ttu-id="62912-835">hello 매개 변수 toobe 변경 사항은이 블로그: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-835">hello parameters toobe changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="62912-836">Hello를 작성 하는 두 개의 Vm에 있다고 가정 하면 동일한 서브넷 hello, hello 다음 매개 변수 값이 필요한 변경 toobe toothese ASCS/SCS에 대 한 Windows 클러스터 구성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-836">Assuming that your two VMs that build hello Windows Cluster Configuration for ASCS/SCS are in hello same SubNet, hello following parameters need toobe changed toothese values:</span></span>
- <span data-ttu-id="62912-837">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="62912-837">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="62912-838">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="62912-838">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="62912-839">이러한 설정 및 고객과 테스트 충분히 복원 하는 유용한 toobe hello 한쪽에 제공 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-839">These settings were tested with customers and provided a good compromise toobe resilient enough on hello one side.</span></span> <span data-ttu-id="62912-840">Hello에 다른 손 해당 설정 된 제공 빠른 SAP 소프트웨어 또는 노드/v M 실패 시 실제 오류 조건에 충분 한 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-840">On hello other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="62912-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Hello SAP ASCS/SCS 클러스터 공유 디스크에 대 한 SIOS DataKeeper 클러스터 Edition을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-841"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="62912-842">이제 Azure에서 Windows Server 장애 조치 클러스터링 구성이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-842">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="62912-843">하지만 SAP ASCS/SCS 인스턴스에 tooinstall 공유 디스크 리소스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-843">But, tooinstall an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="62912-844">Azure에서 필요한 hello 공유 디스크 리소스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-844">You cannot create hello shared disk resources you need in Azure.</span></span> <span data-ttu-id="62912-845">SIOS DataKeeper Cluster Edition은 공급 업체 솔루션 toocreate 공유 디스크 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-845">SIOS DataKeeper Cluster Edition is a third-party solution you can use toocreate shared disk resources.</span></span>

<span data-ttu-id="62912-846">SAP ASCS/SCS hello에 대 한 SIOS DataKeeper 클러스터 버전을 설치할지 클러스터 공유 디스크 이러한 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-846">Installing SIOS DataKeeper Cluster Edition for hello SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="62912-847">.NET Framework 3.5 hello를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-847">Adding hello .NET Framework 3.5</span></span>
- <span data-ttu-id="62912-848">SIOS DataKeeper 설치</span><span class="sxs-lookup"><span data-stu-id="62912-848">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="62912-849">SIOS DataKeeper 설정</span><span class="sxs-lookup"><span data-stu-id="62912-849">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="62912-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>.NET Framework 3.5 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-850"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add hello .NET Framework 3.5</span></span>
<span data-ttu-id="62912-851">자동으로 hello Microsoft.NET Framework 3.5 활성화 하거나 Windows Server 2012 r 2에 설치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-851">hello Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="62912-852">SIOS DataKeeper에 DataKeeper를 설치 하는 모든 노드에서.NET Framework toobe hello를 필요로 하므로 hello 클러스터의 모든 가상 컴퓨터의 게스트 운영 체제 hello에 hello.NET Framework 3.5를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-852">Because SIOS DataKeeper requires hello .NET Framework toobe on all nodes that you install DataKeeper on, you must install hello .NET Framework 3.5 on hello guest operating system of all virtual machines in hello cluster.</span></span>

<span data-ttu-id="62912-853">두 가지 방법으로 tooadd hello.NET Framework 3.5 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-853">There are two ways tooadd hello .NET Framework 3.5:</span></span>

- <span data-ttu-id="62912-854">39 그림에에서 나와 있는 것 처럼 windows에서 hello 추가 역할 및 기능 마법사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-854">Use hello Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![그림 39: hello 추가 역할 및 기능 마법사를 사용 하 여 hello.NET Framework 3.5 설치][sap-ha-guide-figure-3028]

  <span data-ttu-id="62912-856">_**그림 39:** hello 추가 역할 및 기능 마법사를 사용 하 여.NET Framework 3.5 설치 hello_</span><span class="sxs-lookup"><span data-stu-id="62912-856">_**Figure 39:** Install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

  ![Hello 추가 역할 및 기능 마법사를 사용 하 여 hello.NET Framework 3.5를 설치 하면 막대 그림 40: 설치 진행률][sap-ha-guide-figure-3029]

  <span data-ttu-id="62912-858">_**그림 40:** 막대 hello 추가 역할 및 기능 마법사를 사용 하 여 hello.NET Framework 3.5를 설치 하면 설치 진행률_</span><span class="sxs-lookup"><span data-stu-id="62912-858">_**Figure 40:** Installation progress bar when you install hello .NET Framework 3.5 by using hello Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="62912-859">Hello 명령줄 도구 dism.exe를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-859">Use hello command-line tool dism.exe.</span></span> <span data-ttu-id="62912-860">이 유형의 설치 tooaccess hello SxS 디렉터리 hello Windows 설치 미디어에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-860">For this type of installation, you need tooaccess hello SxS directory on hello Windows installation media.</span></span> <span data-ttu-id="62912-861">관리자 권한의 명령 프롬프트에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-861">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="62912-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> SIOS DataKeeper 설치</span><span class="sxs-lookup"><span data-stu-id="62912-862"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="62912-863">Hello 클러스터의 각 노드에서 SIOS DataKeeper Cluster Edition을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-863">Install SIOS DataKeeper Cluster Edition on each node in hello cluster.</span></span> <span data-ttu-id="62912-864">SIOS datakeeper를 통해, 가상 공유 저장소를 toocreate 동기화 된 미러를 만들고 클러스터 공유 저장소를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-864">toocreate virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="62912-865">Hello SIOS 소프트웨어를 설치 하기 전에 hello 도메인 사용자를 만들어 **DataKeeperSvc**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-865">Before you install hello SIOS software, create hello domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="62912-866">Hello 추가 **DataKeeperSvc** 사용자 toohello **로컬 관리자** 그룹 클러스터 노드 모두에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-866">Add hello **DataKeeperSvc** user toohello **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="62912-867">tooinstall SIOS DataKeeper:</span><span class="sxs-lookup"><span data-stu-id="62912-867">tooinstall SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="62912-868">클러스터 노드 모두에 hello SIOS 소프트웨어를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-868">Install hello SIOS software on both cluster nodes.</span></span>

  ![SIOS 설치 관리자][sap-ha-guide-figure-3030]

  ![그림 41: hello SIOS DataKeeper 설치의 첫 번째 페이지][sap-ha-guide-figure-3031]

  <span data-ttu-id="62912-871">_**그림 41:** hello SIOS DataKeeper 설치의 첫 번째 페이지_</span><span class="sxs-lookup"><span data-stu-id="62912-871">_**Figure 41:** First page of hello SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="62912-872">그림 42와 hello 대화 상자에서 선택 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-872">In hello dialog box shown in Figure 42, select **Yes**.</span></span>

  ![그림 42: 서비스를 사용할 수 없다고 알리는 DataKeeper][sap-ha-guide-figure-3032]

  <span data-ttu-id="62912-874">_**그림 42:** 서비스를 사용할 수 없다고 알리는 DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="62912-874">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="62912-875">그림 43에 표시 된 hello 대화 상자에서 선택 하는 권장 **도메인 또는 서버 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-875">In hello dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![그림 43: SIOS DataKeeper에 대한 사용자 선택][sap-ha-guide-figure-3033]

  <span data-ttu-id="62912-877">_**그림 43:** SIOS DataKeeper에 대한 사용자 선택_</span><span class="sxs-lookup"><span data-stu-id="62912-877">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="62912-878">Hello 도메인 계정의 사용자 이름 및 SIOS DataKeeper를 위해 만든 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-878">Enter hello domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![Hello SIOS DataKeeper 설치에 대 한 hello 도메인 사용자 이름 및 암호를 입력 하는 그림 44:][sap-ha-guide-figure-3034]

  <span data-ttu-id="62912-880">_**그림 44:** hello SIOS DataKeeper 설치에 대 한 hello 도메인 사용자 이름 및 암호를 입력 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-880">_**Figure 44:** Enter hello domain user name and password for hello SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="62912-881">그림 45 에서처럼 SIOS DataKeeper 인스턴스에 대 한 hello 라이선스 키를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-881">Install hello license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![그림 45: SIOS DataKeeper 라이선스 키 입력][sap-ha-guide-figure-3035]

  <span data-ttu-id="62912-883">_**그림 45:** SIOS DataKeeper 라이선스 키 입력_</span><span class="sxs-lookup"><span data-stu-id="62912-883">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="62912-884">메시지가 표시 되 면 hello 가상 컴퓨터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-884">When prompted, restart hello virtual machine.</span></span>

#### <span data-ttu-id="62912-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> SIOS DataKeeper 설정</span><span class="sxs-lookup"><span data-stu-id="62912-885"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="62912-886">두 노드에서 모두 SIOS DataKeeper를 설치한 후 toostart hello 구성을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-886">After you install SIOS DataKeeper on both nodes, you need toostart hello configuration.</span></span> <span data-ttu-id="62912-887">hello 구성의 hello 목표 hello 추가 디스크 간의 toohave 동기 데이터 복제 tooeach hello 가상 컴퓨터의 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-887">hello goal of hello configuration is toohave synchronous data replication between hello additional disks attached tooeach of hello virtual machines.</span></span>

1.  <span data-ttu-id="62912-888">Hello DataKeeper 관리 및 구성 도구를 시작한 다음 선택 **서버 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-888">Start hello DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="62912-889">그림 46에서 이 옵션은 빨간색 원으로 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-889">(In Figure 46, this option is circled in red.)</span></span>

  ![그림 46: SIOS DataKeeper 관리 및 구성 도구][sap-ha-guide-figure-3036]

  <span data-ttu-id="62912-891">_**그림 46:** SIOS DataKeeper 관리 및 구성 도구_</span><span class="sxs-lookup"><span data-stu-id="62912-891">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="62912-892">Hello 이름을 입력 하거나, 하 고, 두 번째 단계에서는 두 번째 노드 hello TCP/IP 주소 hello 첫 번째 노드 hello 관리 및 구성 도구를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-892">Enter hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and, in a second step, hello second node.</span></span>

  ![그림 47: 삽입 hello 이름이 나 TCP/IP 주소 hello 첫 번째 노드 hello 관리 및 구성 도구를 연결 해야 되며, 두 번째 단계에서는 hello 두 번째 노드][sap-ha-guide-figure-3037]

  <span data-ttu-id="62912-894">_**그림 47:** 되며, 두 번째 노드 hello와 두 번째 단계에서 삽입 hello 이름이 나 TCP/IP 주소 hello 첫 번째 노드 hello 관리 및 구성 도구를 연결 해야_</span><span class="sxs-lookup"><span data-stu-id="62912-894">_**Figure 47:** Insert hello name or TCP/IP address of hello first node hello Management and Configuration tool should connect to, and in a second step, hello second node_</span></span>

3.  <span data-ttu-id="62912-895">Hello 두 노드 사이의 hello 복제 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-895">Create hello replication job between hello two nodes.</span></span>

  ![그림 48: 복제 작업 만들기][sap-ha-guide-figure-3038]

  <span data-ttu-id="62912-897">_**그림 48:** 복제 작업 만들기_</span><span class="sxs-lookup"><span data-stu-id="62912-897">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="62912-898">마법사는 hello 복제 작업을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-898">A wizard guides you through hello process of creating a replication job.</span></span>
4.  <span data-ttu-id="62912-899">Hello 이름, TCP/IP 주소 및 hello 소스 노드의 디스크 볼륨을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-899">Define hello name, TCP/IP address, and disk volume of hello source node.</span></span>

  ![그림 49: hello 복제 작업의 hello 이름 정의][sap-ha-guide-figure-3039]

  <span data-ttu-id="62912-901">_**그림 49:** hello 복제 작업의 정의 hello 이름_</span><span class="sxs-lookup"><span data-stu-id="62912-901">_**Figure 49:** Define hello name of hello replication job_</span></span>

  ![그림 50: hello hello 현재 소스 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다.][sap-ha-guide-figure-3040]

  <span data-ttu-id="62912-903">_**그림 50:** hello hello 현재 소스 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-903">_**Figure 50:** Define hello base data for hello node, which should be hello current source node_</span></span>

5.  <span data-ttu-id="62912-904">Hello 이름, TCP/IP 주소 및 hello 대상 노드의 디스크 볼륨을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-904">Define hello name, TCP/IP address, and disk volume of hello target node.</span></span>

  ![그림 51: hello hello 현재 대상 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다.][sap-ha-guide-figure-3041]

  <span data-ttu-id="62912-906">_**그림 51:** hello hello 현재 대상 노드가 있어야 하 고 hello 노드에 대 한 기본 데이터를 정의 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-906">_**Figure 51:** Define hello base data for hello node, which should be hello current target node_</span></span>

6.  <span data-ttu-id="62912-907">Hello 압축 알고리즘을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-907">Define hello compression algorithms.</span></span> <span data-ttu-id="62912-908">예에서 hello 복제 스트림을 압축 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-908">In our example, we recommend that you compress hello replication stream.</span></span> <span data-ttu-id="62912-909">재 동기화의 경우에 특히 hello 복제 스트림의 hello 압축 다시 동기화 시간을 크게 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-909">Especially in resynchronization situations, hello compression of hello replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="62912-910">Note 압축 가상 컴퓨터의 CPU 및 RAM 리소스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-910">Note that compression uses hello CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="62912-911">Hello 압축 비율이 증가 하면 사용 하는 CPU 리소스 양의 hello지 않습니다 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-911">As hello compression rate increases, so does hello volume of CPU resources used.</span></span> <span data-ttu-id="62912-912">나중에 이 설정을 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-912">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="62912-913">필요한 설정 다른 toocheck이 비동기적 또는 동기적으로 hello 복제의 발생 여부.</span><span class="sxs-lookup"><span data-stu-id="62912-913">Another setting you need toocheck is whether hello replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="62912-914">*SAP ASCS/SCS 구성을 보호할 때 동기 복제를 사용해야 합니다*.</span><span class="sxs-lookup"><span data-stu-id="62912-914">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![그림 52: 복제 세부 정보 정의][sap-ha-guide-figure-3042]

  <span data-ttu-id="62912-916">_**그림 52:** 복제 세부 정보 정의_</span><span class="sxs-lookup"><span data-stu-id="62912-916">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="62912-917">Hello 복제 작업에 의해 복제 된 hello 볼륨 표현된 tooa 공유 디스크 클러스터 구성을 Windows Server 장애 조치 클러스터링 되어야 하는지 여부를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-917">Define whether hello volume that is replicated by hello replication job should be represented tooa Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="62912-918">Hello SAP ASCS/SCS 구성에 대 한 선택 **예** 클러스터에 게 표시 하는 hello Windows hello 클러스터 볼륨으로 사용할 수 있는 공유 디스크와 복제 된 볼륨 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-918">For hello SAP ASCS/SCS configuration, select **Yes** so that hello Windows cluster sees hello replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![클러스터 볼륨으로 예 tooset hello 복제 볼륨을 선택 하는 그림 53:][sap-ha-guide-figure-3043]

  <span data-ttu-id="62912-920">_**그림 53:** 선택 **예** tooset hello 복제 볼륨을 클러스터 볼륨으로_</span><span class="sxs-lookup"><span data-stu-id="62912-920">_**Figure 53:** Select **Yes** tooset hello replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="62912-921">Hello 볼륨을 만든 후 해당 hello 복제 작업은 활성 상태가 hello DataKeeper 관리 및 구성 도구 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62912-921">After hello volume is created, hello DataKeeper Management and Configuration tool shows that hello replication job is active.</span></span>

  ![그림 54: hello SAP ASCS/SCS 공유 디스크에 대 한 DataKeeper 동기 미러링이 활성화 되었습니다.][sap-ha-guide-figure-3044]

  <span data-ttu-id="62912-923">_**그림 54:** DataKeeper 동기 미러링이 hello SAP ASCS/SCS 공유 디스크에 대 한 활성화 되었습니다_</span><span class="sxs-lookup"><span data-stu-id="62912-923">_**Figure 54:** DataKeeper synchronous mirroring for hello SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="62912-924">장애 조치 클러스터 관리자 55 그림에에서 나와 있는 것 처럼 hello DataKeeper 디스크 드라이브로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-924">Failover Cluster Manager now shows hello disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![그림 55: 장애 조치 클러스터 관리자 hello 디스크를 DataKeeper 복제를 보여 줍니다.][sap-ha-guide-figure-3045]

  <span data-ttu-id="62912-926">_**그림 55:** 장애 조치 클러스터 관리자가 복제 해당 DataKeeper hello 디스크 표시_</span><span class="sxs-lookup"><span data-stu-id="62912-926">_**Figure 55:** Failover Cluster Manager shows hello disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="62912-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Hello SAP NetWeaver 시스템을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-927"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install hello SAP NetWeaver system</span></span>

<span data-ttu-id="62912-928">설정을 사용 하는 DBMS 시스템 hello에 따라 달라 지므로 hello DBMS 설치 프로그램에서 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-928">We won’t describe hello DBMS setup because setups vary depending on hello DBMS system you use.</span></span> <span data-ttu-id="62912-929">하지만 한다고 가정 가용성이 높은 DBMS hello 걱정과 hello 다양 한 DBMS 공급 업체를 Azure에 대 한 지원 hello 기능으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-929">However, we assume that high-availability concerns with hello DBMS are addressed with hello functionalities hello different DBMS vendors support for Azure.</span></span> <span data-ttu-id="62912-930">예로 SQL Server 및 Oracle 데이터베이스용 Oracle Data Guard에 대한 AlwaysOn 또는 데이터베이스 미러링을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-930">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="62912-931">이 문서에서 사용 하 여 hello 시나리오에서는 더 많은 보호 toohello DBMS 추가 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-931">In hello scenario we use in this article, we didn't add more protection toohello DBMS.</span></span>

<span data-ttu-id="62912-932">Azure에서 여러 다른 DBMS 서비스가 이러한 종류의 클러스터형 SAP ASCS/SCS 구성과 상호 작용할 경우 특별한 고려 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-932">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="62912-933">SAP NetWeaver ABAP 시스템과 Java 시스템 ABAP + Java 시스템의 설치 절차 hello 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-933">hello installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="62912-934">가장 중요 한 차이점 hello SAP ABAP 시스템 ASCS 인스턴스 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-934">hello most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="62912-935">SAP Java 시스템 hello SCS 인스턴스 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-935">hello SAP Java system has one SCS instance.</span></span> <span data-ttu-id="62912-936">SAP ABAP + Java 시스템 hello ASCS 인스턴스 하나 있으며에서 실행 되는 하나의 SCS 인스턴스에 hello 동일한 Microsoft 장애 조치 클러스터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-936">hello SAP ABAP+Java system has one ASCS instance and one SCS instance running in hello same Microsoft failover cluster group.</span></span> <span data-ttu-id="62912-937">각 SAP NetWeaver 설치 스택에 대한 설치 차이점은 명시적으로 언급됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-937">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="62912-938">다른 모든 파트 동일 hello는 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-938">You can assume that all other parts are hello same.</span></span>  
>
>

### <span data-ttu-id="62912-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> 고가용성 ASCS/SCS 인스턴스에 SAP 설치</span><span class="sxs-lookup"><span data-stu-id="62912-939"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62912-940">반드시 미러 볼륨 페이지 파일 크기가 DataKeeper tooplace 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-940">Be sure not tooplace your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="62912-941">DataKeeper는 미러된 볼륨을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-941">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="62912-942">Hello 기본값 페이지 파일 hello 임시 드라이브는 Azure 가상 컴퓨터를 D에 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-942">You can leave your page file on hello temporary drive D of an Azure virtual machine, which is hello default.</span></span> <span data-ttu-id="62912-943">아직 매크로 실행 하지 않은 경우 hello Windows 페이지 파일 toodrive Azure 가상 컴퓨터의 d:를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-943">If it's not already there, move hello Windows page file toodrive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="62912-944">고가용성 ASCS/SCS 인스턴스에 SAP 설치는 다음과 같은 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-944">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="62912-945">클러스터 된 hello SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들기</span><span class="sxs-lookup"><span data-stu-id="62912-945">Creating a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="62912-946">Hello SAP 첫 번째 클러스터 노드를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-946">Installing hello SAP first cluster node</span></span>
- <span data-ttu-id="62912-947">Hello ASCS/SCS 인스턴스의 hello SAP 프로필 수정</span><span class="sxs-lookup"><span data-stu-id="62912-947">Modifying hello SAP profile of hello ASCS/SCS instance</span></span>
- <span data-ttu-id="62912-948">프로브 포트 추가</span><span class="sxs-lookup"><span data-stu-id="62912-948">Adding a probe port</span></span>
- <span data-ttu-id="62912-949">Hello Windows 방화벽의 프로브 포트 열기</span><span class="sxs-lookup"><span data-stu-id="62912-949">Opening hello Windows firewall probe port</span></span>

#### <span data-ttu-id="62912-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>클러스터 된 hello SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들기</span><span class="sxs-lookup"><span data-stu-id="62912-950"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for hello clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="62912-951">Hello Windows DNS 관리자에서 hello ASCS/SCS 인스턴스의 hello 가상 호스트 이름에 대 한 DNS 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62912-951">In hello Windows DNS manager, create a DNS entry for hello virtual host name of hello ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="62912-952">hello ASCS/SCS 인스턴스의 수 있어야 하는 hello의 toohello 가상 호스트 이름 지정 IP 주소 hello 동일 tooAzure 부하 분산 장치를 할당 하는 hello IP 주소로 (**<*SID*> 파운드-ascs **).</span><span class="sxs-lookup"><span data-stu-id="62912-952">hello IP address that you assign toohello virtual host name of hello ASCS/SCS instance must be hello same as hello IP address that you assigned tooAzure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="62912-953">hello hello 가상 SAP ASCS/SCS 호스트 이름의 IP 주소 (**pr1 ascs sap**) Azure 부하 분산 장치의 hello IP 주소와 동일한 hello 됩니다 (**pr1-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="62912-953">hello IP address of hello virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is hello same as hello IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![Hello SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대 한 hello DNS 항목을 정의 하는 그림 56:][sap-ha-guide-figure-3046]

  <span data-ttu-id="62912-955">_**그림 56:** hello SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대 한 hello DNS 항목을 정의 합니다._</span><span class="sxs-lookup"><span data-stu-id="62912-955">_**Figure 56:** Define hello DNS entry for hello SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="62912-956">toodefine hello IP 주소가 할당 toohello 가상 호스트 이름 선택 **DNS 관리자** > **도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-956">toodefine hello IP address assigned toohello virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![그림 57: SAP ASCS/SCS 클러스터 구성을 위한 새 가상 이름 및 TCP/IP 주소][sap-ha-guide-figure-3047]

  <span data-ttu-id="62912-958">_**그림 57:** SAP ASCS/SCS 클러스터 구성을 위한 새 가상 이름 및 TCP/IP 주소_</span><span class="sxs-lookup"><span data-stu-id="62912-958">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="62912-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Hello SAP 첫 번째 클러스터 노드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-959"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install hello SAP first cluster node</span></span>

1.  <span data-ttu-id="62912-960">1. 클러스터 노드에서 hello 첫 번째 클러스터 노드 옵션을 실행 예를 들어 hello에 **pr1-ascs-0** 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-960">Execute hello first cluster node option on cluster node A. For example, on hello **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="62912-961">Azure 내부 hello에 대 한 tookeep hello 기본 포트는 부하 분산 장치, 선택:</span><span class="sxs-lookup"><span data-stu-id="62912-961">tookeep hello default ports for hello Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="62912-962">**ABAP 시스템**: **ASCS** 인스턴스 번호 **00**</span><span class="sxs-lookup"><span data-stu-id="62912-962">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="62912-963">**Java 시스템**: **SCS** 인스턴스 번호 **01**</span><span class="sxs-lookup"><span data-stu-id="62912-963">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="62912-964">**ABAP+Java 시스템**: **ASCS** 인스턴스 번호 **00** 및 **SCS** 인스턴스 번호 **01**</span><span class="sxs-lookup"><span data-stu-id="62912-964">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="62912-965">인스턴스와 hello Java SCS 인스턴스에 대 한 01 toouse 인스턴스 번호가 00 ABAP ASCS hello에 대 한 다른, toochange hello Azure 내부 부하 분산 장치 기본 부하 분산에 설명 된 규칙 먼저 [변경 hello ASCS/SCS 기본 로드 hello Azure 내부 부하 분산 장치에 대 한 규칙을 분산][sap-ha-guide-8.9]합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-965">toouse instance numbers other than 00 for hello ABAP ASCS instance and 01 for hello Java SCS instance, first you need toochange hello Azure internal load balancer default load balancing rules, described in [Change hello ASCS/SCS default load balancing rules for hello Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="62912-966">hello 다음 몇 가지 작업 아닌 문서에 설명 된 hello 표준 SAP 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-966">hello next few tasks aren't described in hello standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="62912-967">SAP 설치 설명서 hello tooinstall 첫 번째 ASCS/SCS 클러스터 노드를 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-967">hello SAP installation documentation describes how tooinstall hello first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="62912-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Hello ASCS/SCS 인스턴스의 hello SAP 프로필 수정</span><span class="sxs-lookup"><span data-stu-id="62912-968"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify hello SAP profile of hello ASCS/SCS instance</span></span>

<span data-ttu-id="62912-969">새 프로필 매개 변수 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-969">You need tooadd a new profile parameter.</span></span> <span data-ttu-id="62912-970">hello 프로필 매개 변수는 너무 오랫동안 유휴 상태일 때 닫는에서 SAP 작업 프로세스와 hello enqueue 서버 사이의 연결을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-970">hello profile parameter prevents connections between SAP work processes and hello enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="62912-971">Hello 문제 시나리오에서 설명한 대로 [hello SAP ASCS/SCS 인스턴스의 클러스터 노드 모두에 레지스트리 항목을 추가][sap-ha-guide-8.11]합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-971">We mentioned hello problem scenario in [Add registry entries on both cluster nodes of hello SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="62912-972">이 섹션에서도 도입 했습니다 두 변경 toosome 기본 TCP/IP 연결 매개 변수를입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-972">In that section, we also introduced two changes toosome basic TCP/IP connection parameters.</span></span> <span data-ttu-id="62912-973">두 번째 단계에서는 tooset hello enqueue 서버 toosend 해야는 `keep_alive` hello 연결 hello Azure 내부 부하 분산 장치의 유휴 임계값에 도달 하지 않도록 신호입니다.</span><span class="sxs-lookup"><span data-stu-id="62912-973">In a second step, you need tooset hello enqueue server toosend a `keep_alive` signal so that hello connections don't hit hello Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="62912-974">toomodify hello hello ASCS/SCS 인스턴스의 SAP 프로필:</span><span class="sxs-lookup"><span data-stu-id="62912-974">toomodify hello SAP profile of hello ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="62912-975">이 프로필 매개 변수 toohello SAP ASCS/SCS 인스턴스에 프로필을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-975">Add this profile parameter toohello SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="62912-976">예에서 hello 경로:</span><span class="sxs-lookup"><span data-stu-id="62912-976">In our example, hello path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="62912-977">예를 들어 toohello SAP SCS 인스턴스에 프로필 및 해당 경로:</span><span class="sxs-lookup"><span data-stu-id="62912-977">For example, toohello SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="62912-978">tooapply hello 변경 hello /SCS SAP ASCS 인스턴스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-978">tooapply hello changes, restart hello SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="62912-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> 프로브 포트 추가</span><span class="sxs-lookup"><span data-stu-id="62912-979"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="62912-980">Azure 부하 분산 장치와 hello 내부 부하 분산 장치의 프로브 기능 toomake hello 전체 클러스터 구성 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-980">Use hello internal load balancer's probe functionality toomake hello entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="62912-981">hello Azure 내부 부하 분산 장치는 일반적으로 hello 들어오는 작업 참여 가상 컴퓨터 사이 고르게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-981">hello Azure internal load balancer usually distributes hello incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="62912-982">그러나 하나의 인스턴스만 활성 상태가 되므로 일부 클러스터 구성에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-982">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="62912-983">hello 다른 인스턴스는 수동 이므로 hello 작업 부하를 받아들일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-983">hello other instance is passive and can’t accept any of hello workload.</span></span> <span data-ttu-id="62912-984">프로브 기능에는 hello Azure 내부 부하 분산 장치 할당 작업만 tooan 활성 인스턴스 때 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-984">A probe functionality helps when hello Azure internal load balancer assigns work only tooan active instance.</span></span> <span data-ttu-id="62912-985">Hello 프로브 기능을 통해 hello 내부 부하 분산 장치 인스턴스 활성화에 대 한 hello 작업과 hello 인스턴스만 대상을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-985">With hello probe functionality, hello internal load balancer can detect which instances are active, and then target only hello instance with hello workload.</span></span>

<span data-ttu-id="62912-986">tooadd 프로브 포트:</span><span class="sxs-lookup"><span data-stu-id="62912-986">tooadd a probe port:</span></span>

1.  <span data-ttu-id="62912-987">Hello 현재 확인 **ProbePort** hello 다음 PowerShell 명령을 실행 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-987">Check hello current **ProbePort** setting by running hello following PowerShell command.</span></span> <span data-ttu-id="62912-988">Hello 클러스터 구성에서 옵니다 hello 가상 컴퓨터 중 하나를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-988">Execute it from within one of hello virtual machines in hello cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="62912-989">프로브 포트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-989">Define a probe port.</span></span> <span data-ttu-id="62912-990">hello 기본 프로브 포트 번호는 **0**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-990">hello default probe port number is **0**.</span></span> <span data-ttu-id="62912-991">예제에서는 **62000** 프로브 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-991">In our example, we use probe port **62000**.</span></span>

  ![그림 58: hello 클러스터 구성 프로브 포트는 기본적으로 0][sap-ha-guide-figure-3048]

  <span data-ttu-id="62912-993">_**그림 58:** hello 기본 클러스터 구성 프로브 포트는 0_</span><span class="sxs-lookup"><span data-stu-id="62912-993">_**Figure 58:** hello default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="62912-994">hello 포트 번호는 SAP Azure 리소스 관리자 템플릿을에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-994">hello port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="62912-995">PowerShell에서 hello 포트 번호를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-995">You can assign hello port number in PowerShell.</span></span>

  <span data-ttu-id="62912-996">hello에 대 한 새 ProbePort 값 tooset  **SAP <*SID*> IP * * 클러스터 리소스를 hello 다음 PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-996">tooset a new ProbePort value for hello **SAP <*SID*> IP** cluster resource, run hello following PowerShell script.</span></span> <span data-ttu-id="62912-997">사용자 환경에 대 한 hello PowerShell 변수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-997">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="62912-998">Hello 스크립트를 실행 한 후 메시지 표시 toorestart hello SAP 클러스터 그룹 tooactivate hello 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-998">After hello script runs, you'll be prompted toorestart hello SAP cluster group tooactivate hello changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  <span data-ttu-id="62912-999">Hello 상태로 전환한 후  **SAP <*SID*> * * 클러스터 역할을 온라인에서 **ProbePort** toohello 새 값으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-999">After you bring hello **SAP <*SID*>** cluster role online, verify that **ProbePort** is set toohello new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![그림 59: hello 새 값을 설정한 후 hello 클러스터 포트 프로브][sap-ha-guide-figure-3049]

  <span data-ttu-id="62912-1001">_**그림 59:** hello 새 값을 설정한 후 hello 클러스터 포트 프로브_</span><span class="sxs-lookup"><span data-stu-id="62912-1001">_**Figure 59:** Probe hello cluster port after you set hello new value_</span></span>

#### <span data-ttu-id="62912-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Hello Windows 방화벽의 프로브 포트 열기</span><span class="sxs-lookup"><span data-stu-id="62912-1002"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open hello Windows firewall probe port</span></span>

<span data-ttu-id="62912-1003">클러스터 노드 모두에서 Windows 방화벽 프로브 포트 tooopen이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1003">You need tooopen a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="62912-1004">다음 스크립트는 Windows 방화벽의 프로브 포트 tooopen hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1004">Use hello following script tooopen a Windows firewall probe port.</span></span> <span data-ttu-id="62912-1005">사용자 환경에 대 한 hello PowerShell 변수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1005">Update hello PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="62912-1006">hello **ProbePort** 너무 설정**62000**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1006">hello **ProbePort** is set too**62000**.</span></span> <span data-ttu-id="62912-1007">Hello 파일 공유에 액세스할 수 이제  **\\\ascsha-clsap\sapmnt** 등에서 다른 호스트에서 **ascsha dba**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1007">Now you can access hello file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="62912-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Hello 데이터베이스 인스턴스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1008"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install hello database instance</span></span>

<span data-ttu-id="62912-1009">tooinstall hello 데이터베이스 인스턴스를 hello SAP 설치 설명서에에서 설명 된 hello 프로세스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1009">tooinstall hello database instance, follow hello process described in hello SAP installation documentation.</span></span>

### <span data-ttu-id="62912-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Hello 두 번째 클러스터 노드를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1010"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install hello second cluster node</span></span>

<span data-ttu-id="62912-1011">tooinstall hello 두 번째 클러스터 hello SAP 설치 가이드의에서 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1011">tooinstall hello second cluster, follow hello steps in hello SAP installation guide.</span></span>

### <span data-ttu-id="62912-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Hello SAP 호출자 Windows 서비스 인스턴스의 hello 시작 유형을 변경합니다</span><span class="sxs-lookup"><span data-stu-id="62912-1012"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change hello start type of hello SAP ERS Windows service instance</span></span>

<span data-ttu-id="62912-1013">Hello SAP 호출자 Windows 서비스의 시작 유형을 hello도 변경**자동 (지연 된 시작)** 클러스터 노드 모두에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1013">Change hello start type of hello SAP ERS Windows service too**Automatic (Delayed Start)** on both cluster nodes.</span></span>

![그림 60: hello SAP 호출자 인스턴스 toodelayed 자동에 대 한 hello 서비스 유형 변경][sap-ha-guide-figure-3050]

<span data-ttu-id="62912-1015">_**그림 60:** hello SAP 호출자 인스턴스 toodelayed 자동에 대 한 hello 서비스 유형 변경_</span><span class="sxs-lookup"><span data-stu-id="62912-1015">_**Figure 60:** Change hello service type for hello SAP ERS instance toodelayed automatic_</span></span>

### <span data-ttu-id="62912-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Hello SAP 기본 응용 프로그램 서버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1016"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install hello SAP Primary Application Server</span></span>

<span data-ttu-id="62912-1017">Hello 기본 응용 프로그램 서버 (PA) 인스턴스를 설치 <*SID*> 지정한 hello 가상 컴퓨터-di-0 toohost hello PAS 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1017">Install hello Primary Application Server (PAS) instance <*SID*>-di-0 on hello virtual machine that you've designated toohost hello PAS.</span></span> <span data-ttu-id="62912-1018">Azure 또는 DataKeeper 관련 설정과는 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1018">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="62912-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Hello SAP 추가 응용 프로그램 서버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1019"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install hello SAP Additional Application Server</span></span>

<span data-ttu-id="62912-1020">지정한 toohost SAP 응용 프로그램 서버 인스턴스는 모든 hello 가상 컴퓨터에는 SAP 추가 응용 프로그램 서버 (AAS)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1020">Install an SAP Additional Application Server (AAS) on all hello virtual machines that you've designated toohost an SAP Application Server instance.</span></span> <span data-ttu-id="62912-1021">예를 들어 <*SID*>-d i-1 너무 <*SID*>-d i-&lt;n&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1021">For example, on <*SID*>-di-1 too<*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="62912-1022">가용성이 높은 SAP NetWeaver 시스템의 hello 설치를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1022">This finishes hello installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="62912-1023">다음으로 장애 조치 테스트를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1023">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="62912-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Hello SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 복제를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1024"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test hello SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="62912-1025">쉽게 tootest 사용 되며 장애 조치 클러스터 관리자 및 hello SIOS DataKeeper 관리 및 구성 도구를 사용 하 여 SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 디스크 복제를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1025">It's easy tootest and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and hello SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="62912-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS 인스턴스가 클러스터 노드 A에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1026"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="62912-1027">hello **SAP PR1** 클러스터 그룹 1. 클러스터 노드에서 실행 되 고 예를 들어에 **pr1-ascs-0**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1027">hello **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="62912-1028">Hello에 참가 하는 hello 공유 디스크 드라이브를 할당 **SAP PR1** hello ASCS/SCS 인스턴스를 사용 하 여 toocluster 노드 A와 그룹을 클러스터링</span><span class="sxs-lookup"><span data-stu-id="62912-1028">Assign hello shared disk drive S, which is part of hello **SAP PR1** cluster group, and which hello ASCS/SCS instance uses, toocluster node A.</span></span>

![그림 61: 장애 조치 클러스터 관리자: hello SAP < SID > 클러스터 그룹이 클러스터 노드 A에서 실행 되 고][sap-ha-guide-figure-5000]

<span data-ttu-id="62912-1030">_**그림 61:** 장애 조치 클러스터 관리자: SAP hello <*SID*> 클러스터 그룹이 클러스터 노드 A에서 실행 되 고_</span><span class="sxs-lookup"><span data-stu-id="62912-1030">_**Figure 61:** Failover Cluster Manager: hello SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="62912-1031">Hello SIOS DataKeeper 관리 및 구성 도구에서 해당 데이터는 hello 원본 볼륨 드라이브 S toohello 대상 볼륨 드라이브 S 2. 클러스터 노드에서 클러스터 노드에서에서 동기적으로 복제 hello 공유 디스크를 볼 수 있습니다. 예를 들어에서 복제 **pr1 ascs 0 [10.0.0.40]** 너무**pr1 ascs 1 [10.0.0.41]**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1031">In hello SIOS DataKeeper Management and Configuration tool, you can see that hello shared disk data is synchronously replicated from hello source volume drive S on cluster node A toohello target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** too**pr1-ascs-1 [10.0.0.41]**.</span></span>

![그림 62:에서 SIOS DataKeeper를 복제할 수 hello 로컬 볼륨 클러스터 노드에서 toocluster 노드 B][sap-ha-guide-figure-5001]

<span data-ttu-id="62912-1033">_**그림 62:** SIOS DataKeeper를 클러스터 노드에서 toocluster 노드 B hello 로컬 볼륨 복제_</span><span class="sxs-lookup"><span data-stu-id="62912-1033">_**Figure 62:** In SIOS DataKeeper, replicate hello local volume from cluster node A toocluster node B_</span></span>

### <span data-ttu-id="62912-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>노드 A toonode B에서에서 장애 조치</span><span class="sxs-lookup"><span data-stu-id="62912-1034"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A toonode B</span></span>

1.  <span data-ttu-id="62912-1035">Hello SAP의 장애 조치 옵션 tooinitiate 다음 중 하나를 선택 <*SID*> b: 클러스터 노드 A toocluster 노드에서 클러스터 그룹</span><span class="sxs-lookup"><span data-stu-id="62912-1035">Choose one of these options tooinitiate a failover of hello SAP <*SID*> cluster group from cluster node A toocluster node B:</span></span>
  - <span data-ttu-id="62912-1036">장애 조치(failover) 클러스터 관리자 사용</span><span class="sxs-lookup"><span data-stu-id="62912-1036">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="62912-1037">장애 조치 클러스터 PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="62912-1037">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="62912-1038">Hello Windows 게스트 운영 체제 내에서 클러스터 노드 A를 다시 시작 (hello SAP의 자동 장애 조치를 시작 하는이 <*SID*> 클러스터 그룹에서 노드 A toonode B).</span><span class="sxs-lookup"><span data-stu-id="62912-1038">Restart cluster node A within hello Windows guest operating system (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
3.  <span data-ttu-id="62912-1039">Hello Azure 포털에서에서 클러스터 노드 A를 다시 시작 (hello SAP의 자동 장애 조치를 시작 하는이 <*SID*> 클러스터 그룹에서 노드 A toonode B).</span><span class="sxs-lookup"><span data-stu-id="62912-1039">Restart cluster node A from hello Azure portal (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>  
4.  <span data-ttu-id="62912-1040">Azure PowerShell을 사용 하 여 클러스터 노드 A를 다시 시작 (hello SAP의 자동 장애 조치를 시작 하는이 <*SID*> 클러스터 그룹에서 노드 A toonode B).</span><span class="sxs-lookup"><span data-stu-id="62912-1040">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of hello SAP <*SID*> cluster group from node A toonode B).</span></span>

  <span data-ttu-id="62912-1041">장애 조치 후 SAP hello <*SID*> 2. 클러스터 노드에서 실행 되 고 클러스터 그룹 실행 되는 예를 들어 **pr1-ascs-1**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1041">After failover, hello SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![그림 63: 장애 조치 클러스터 관리자에서 hello SAP < SID > 클러스터 그룹 노드에서 실행 중인 클러스터 B][sap-ha-guide-figure-5002]

  <span data-ttu-id="62912-1043">_**그림 63**: 장애 조치 클러스터 관리자에서 SAP hello <*SID*> 클러스터 그룹 B 클러스터 노드에서 실행 되 고_</span><span class="sxs-lookup"><span data-stu-id="62912-1043">_**Figure 63**: In Failover Cluster Manager, hello SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="62912-1044">hello 공유 디스크가 현재 탑재 되어 클러스터에서 노드 2. SIOS DataKeeper를 복제 하 고 데이터 원본 볼륨 드라이브 S 1. 클러스터 노드에서 클러스터 노드 B tootarget 볼륨 드라이브 S에서 복제 되는 예를 들어 **pr1 ascs 1 [10.0.0.41]** 너무**pr1 ascs 0 [10.0.0.40]**합니다.</span><span class="sxs-lookup"><span data-stu-id="62912-1044">hello shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B tootarget volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** too**pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![그림 64: SIOS DataKeeper hello 로컬 볼륨 클러스터 노드 B toocluster 노드 A에서 복제][sap-ha-guide-figure-5003]

  <span data-ttu-id="62912-1046">_**그림 64:** SIOS DataKeeper 클러스터 노드 B toocluster 노드 A에서에서 hello 로컬 볼륨 복제_</span><span class="sxs-lookup"><span data-stu-id="62912-1046">_**Figure 64:** SIOS DataKeeper replicates hello local volume from cluster node B toocluster node A_</span></span>
