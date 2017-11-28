---
title: "SAP NetWeaver에 대한 Azure Virtual Machines 고가용성 | Microsoft Docs"
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
ms.openlocfilehash: d00db895ffcf9ba9a51e3df2dae5d33c0277dd6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a><span data-ttu-id="7f5e0-103">SAP NetWeaver에 대한 Azure Virtual Machines 고가용성</span><span class="sxs-lookup"><span data-stu-id="7f5e0-103">Azure Virtual Machines high availability for SAP NetWeaver</span></span>

<span data-ttu-id="7f5e0-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="7f5e0-104">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="7f5e0-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="7f5e0-105">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
<span data-ttu-id="7f5e0-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="7f5e0-106">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="7f5e0-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="7f5e0-107">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="7f5e0-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="7f5e0-108">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>

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



<span data-ttu-id="7f5e0-109">Azure Virtual Machines는 긴 조달 주기 없이 최소한의 시간 안에 계산, Storage 및 네트워크 리소스를 필요로 하는 조직을 위한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-109">Azure Virtual Machines is the solution for organizations that need compute, storage, and network resources, in minimal time, and without lengthy procurement cycles.</span></span> <span data-ttu-id="7f5e0-110">Azure Virtual Machines를 사용하여 SAP NetWeaver 기반 ABAP, Java 및 ABAP+Java 스택과 같은 기존 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-110">You can use Azure Virtual Machines to deploy classic applications like SAP NetWeaver-based ABAP, Java, and an ABAP+Java stack.</span></span> <span data-ttu-id="7f5e0-111">추가 온-프레미스 리소스 없이도 안정성과 가용성을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-111">Extend reliability and availability without additional on-premises resources.</span></span> <span data-ttu-id="7f5e0-112">Azure Virtual Machines는 크로스-프레미스 연결을 지원하므로 Azure Virtual Machines를 조직의 온-프레미스 도메인, 사설 클라우드 및 SAP 시스템 지형에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-112">Azure Virtual Machines supports cross-premises connectivity, so you can integrate Azure Virtual Machines into your organization's on-premises domains, private clouds, and SAP system landscape.</span></span>

<span data-ttu-id="7f5e0-113">이 문서에서는 Azure Resource Manager 배포 모델을 사용하여 Azure에서 고가용성 SAP 시스템을 배포하기 위한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-113">In this article, we cover the steps that you can take to deploy high-availability SAP systems in Azure by using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7f5e0-114">다음과 같은 주요 작업을 진행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-114">We walk you through these major tasks:</span></span>

* <span data-ttu-id="7f5e0-115">적절한 SAP Note 및 설치 가이드를 찾습니다([리소스][sap-ha-guide-2] 섹션에 나열).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-115">Find the right SAP Notes and installation guides, listed in the [Resources][sap-ha-guide-2] section.</span></span> <span data-ttu-id="7f5e0-116">이 문서는 특정 플랫폼에 SAP 소프트웨어를 설치 및 배포하는 데 도움이 되는 기본 리소스인 SAP 설치 설명서 및 SAP Note를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-116">This article complements SAP installation documentation and SAP Notes, which are the primary resources that can help you install and deploy SAP software on specific platforms.</span></span>
* <span data-ttu-id="7f5e0-117">Azure Resource Manager 배포 모델 및 Azure 클래식 배포 모델 간 차이를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-117">Learn the differences between the Azure Resource Manager deployment model and the Azure classic deployment model.</span></span>
* <span data-ttu-id="7f5e0-118">Windows Server 장애 조치 클러스터링 쿼럼 모드에 대해 자세히 알아보고 사용 중인 Azure 배포에 적합한 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-118">Learn about Windows Server Failover Clustering quorum modes, so you can select the model that is right for your Azure deployment.</span></span>
* <span data-ttu-id="7f5e0-119">Azure 서비스의 Windows Server 장애 조치 클러스터링 공유 Storage에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-119">Learn about Windows Server Failover Clustering shared storage in Azure services.</span></span>
* <span data-ttu-id="7f5e0-120">Azure의 단일 실패 지점 구성 요소(예: ASCS(ABAP(고급 비즈니스 응용 프로그램 프로그래밍) SAP 중앙 서비스)/SCS(SAP 중앙 서비스) 및 DBMS(데이터베이스 관리 시스템)) 및 중복 구성 요소(예: SAP 응용 프로그램 서버)를 보호하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-120">Learn how to help protect single-point-of-failure components like Advanced Business Application Programming (ABAP) SAP Central Services (ASCS)/SAP Central Services (SCS) and database management systems (DBMS), and redundant components like SAP Application Server, in Azure.</span></span>
* <span data-ttu-id="7f5e0-121">Azure Resource Manager를 사용하여 Azure의 Windows Server 장애 조치 클러스터링 클러스터에서 고가용성 SAP 시스템을 설치하고 구성하는 단계별 작업 예제를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-121">Follow a step-by-step example of an installation and configuration of a high-availability SAP system in a Windows Server Failover Clustering cluster in Azure by using Azure Resource Manager.</span></span>
* <span data-ttu-id="7f5e0-122">Azure에서 Windows Server 장애 조치 클러스터링을 사용하는 데 필요한 추가 단계도 알아봅니다. 이러한 단계는 온-프레미스 배포에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-122">Learn about additional steps required to use Windows Server Failover Clustering in Azure, but which are not needed in an on-premises deployment.</span></span>

<span data-ttu-id="7f5e0-123">이 문서에서는 배포 및 구성을 단순화하기 위해 SAP 3계층 고가용성 Resource Manager 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-123">To simplify deployment and configuration, in this article, we use the SAP three-tier high-availability Resource Manager templates.</span></span> <span data-ttu-id="7f5e0-124">이 템플릿은 고가용성 SAP 시스템에 필요한 전체 인프라의 배포를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-124">The templates automate deployment of the entire infrastructure that you need for a high-availability SAP system.</span></span> <span data-ttu-id="7f5e0-125">또한 이러한 인프라는 SAP 시스템의 SAPS(SAP 응용 프로그램 성능 표준) 크기 조정도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-125">The infrastructure also supports SAP Application Performance Standard (SAPS) sizing of your SAP system.</span></span>

## <span data-ttu-id="7f5e0-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> 필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f5e0-126"><a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Prerequisites</span></span>
<span data-ttu-id="7f5e0-127">시작하기 전에 다음 섹션에 설명된 필수 조건을 충족하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-127">Before you start, make sure that you meet the prerequisites that are described in the following sections.</span></span> <span data-ttu-id="7f5e0-128">또한 [리소스][sap-ha-guide-2] 섹션에서 나열하는 리소스도 모두 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-128">Also, be sure to check all resources listed in the [Resources][sap-ha-guide-2] section.</span></span>

<span data-ttu-id="7f5e0-129">이 문서에서는 [관리 디스크를 사용하는 3계층 SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/)용 Azure Resource Manager 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-129">In this article, we use Azure Resource Manager templates for [three-tier SAP NetWeaver using Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/).</span></span> <span data-ttu-id="7f5e0-130">유용한 템플릿 개요를 보려면 [SAP Azure Resource Manager 템플릿](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-130">For a helpful overview of templates, see [SAP Azure Resource Manager templates](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).</span></span>

## <span data-ttu-id="7f5e0-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> 리소스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-131"><a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Resources</span></span>
<span data-ttu-id="7f5e0-132">이 문서에서는 Azure의 SAP 배포에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-132">These articles cover SAP deployments in Azure:</span></span>

* <span data-ttu-id="7f5e0-133">[SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-133">[Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide]</span></span>
* <span data-ttu-id="7f5e0-134">[SAP NetWeaver에 대한 Azure Virtual Machines 배포][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-134">[Azure Virtual Machines deployment for SAP NetWeaver][deployment-guide]</span></span>
* <span data-ttu-id="7f5e0-135">[SAP NetWeaver에 대한 Azure Virtual Machines DBMS 배포][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-135">[Azure Virtual Machines DBMS deployment for SAP NetWeaver][dbms-guide]</span></span>
* <span data-ttu-id="7f5e0-136">[SAP NetWeaver에 대한 Azure Virtual Machines 고가용성(이 가이드)][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-136">[Azure Virtual Machines high availability for SAP NetWeaver (this guide)][sap-ha-guide]</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-137">가능한 경우 참조용 SAP 설치 가이드에 대한 링크를 제공합니다([SAP 설치 가이드][sap-installation-guides] 참조).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-137">Whenever possible, we give you a link to the referring SAP installation guide (see the [SAP installation guides][sap-installation-guides]).</span></span> <span data-ttu-id="7f5e0-138">설치 프로세스의 필수 조건 및 자세한 내용을 보려면 SAP NetWeaver 설치 가이드를 자세히 읽어 보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-138">For prerequisites and information about the installation process, it's a good idea to read the SAP NetWeaver installation guides carefully.</span></span> <span data-ttu-id="7f5e0-139">이 문서에서는 Azure Virtual Machines와 함께 사용할 수 있는 SAP NetWeaver 기반 시스템에 대한 특정 작업만 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-139">This article covers only specific tasks for SAP NetWeaver-based systems that you can use with Azure Virtual Machines.</span></span>
>
>

<span data-ttu-id="7f5e0-140">이러한 SAP Note는 Azure의 SAP 항목과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-140">These SAP Notes are related to the topic of SAP in Azure:</span></span>

| <span data-ttu-id="7f5e0-141">Note 번호</span><span class="sxs-lookup"><span data-stu-id="7f5e0-141">Note number</span></span> | <span data-ttu-id="7f5e0-142">제목</span><span class="sxs-lookup"><span data-stu-id="7f5e0-142">Title</span></span> |
| --- | --- |
| <span data-ttu-id="7f5e0-143">[1928533]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-143">[1928533]</span></span> |<span data-ttu-id="7f5e0-144">Azure의 SAP 응용 프로그램: 지원 제품 및 크기 조정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-144">SAP Applications on Azure: Supported Products and Sizing</span></span> |
| <span data-ttu-id="7f5e0-145">[2015553]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-145">[2015553]</span></span> |<span data-ttu-id="7f5e0-146">Microsoft Azure의 SAP: 지원 필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f5e0-146">SAP on Microsoft Azure: Support Prerequisites</span></span> |
| <span data-ttu-id="7f5e0-147">[1999351]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-147">[1999351]</span></span> |<span data-ttu-id="7f5e0-148">향상된 SAP용 Azure 모니터링</span><span class="sxs-lookup"><span data-stu-id="7f5e0-148">Enhanced Azure Monitoring for SAP</span></span> |
| <span data-ttu-id="7f5e0-149">[2178632]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-149">[2178632]</span></span> |<span data-ttu-id="7f5e0-150">Microsoft Azure의 SAP용 주요 모니터링 메트릭</span><span class="sxs-lookup"><span data-stu-id="7f5e0-150">Key Monitoring Metrics for SAP on Microsoft Azure</span></span> |
| <span data-ttu-id="7f5e0-151">[1999351]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-151">[1999351]</span></span> |<span data-ttu-id="7f5e0-152">Windows에서의 가상화: 향상된 모니터링</span><span class="sxs-lookup"><span data-stu-id="7f5e0-152">Virtualization on Windows: Enhanced Monitoring</span></span> |
| <span data-ttu-id="7f5e0-153">[2243692]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-153">[2243692]</span></span> |<span data-ttu-id="7f5e0-154">SAP DBMS 인스턴스에 Azure Premium SSD Storage 사용</span><span class="sxs-lookup"><span data-stu-id="7f5e0-154">Use of Azure Premium SSD Storage for SAP DBMS Instance</span></span> |

<span data-ttu-id="7f5e0-155">일반적인 기본 및 최대 제한 사항을 포함하여 [Azure 구독 제한][azure-subscription-service-limits-subscription]에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-155">Learn more about the [limitations of Azure subscriptions][azure-subscription-service-limits-subscription], including general default limitations and maximum limitations.</span></span>

## <span data-ttu-id="7f5e0-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Azure Resource Manager 및 Azure 클래식 배포 모델의 고가용성 SAP</span><span class="sxs-lookup"><span data-stu-id="7f5e0-156"><a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>High-availability SAP with Azure Resource Manager vs. the Azure classic deployment model</span></span>
<span data-ttu-id="7f5e0-157">Azure Resource Manager와 Azure 클래식 배포 모델은 다음과 같은 영역에서 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-157">The Azure Resource Manager and Azure classic deployment models are different in the following areas:</span></span>

- <span data-ttu-id="7f5e0-158">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="7f5e0-158">Resource groups</span></span>
- <span data-ttu-id="7f5e0-159">Azure 리소스 그룹에 대한 Azure 내부 부하 분산 장치 종속성</span><span class="sxs-lookup"><span data-stu-id="7f5e0-159">Azure internal load balancer dependency on the Azure resource group</span></span>
- <span data-ttu-id="7f5e0-160">SAP 다중 SID 지원 시나리오</span><span class="sxs-lookup"><span data-stu-id="7f5e0-160">Support for SAP multi-SID scenarios</span></span>

### <span data-ttu-id="7f5e0-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="7f5e0-161"><a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Resource groups</span></span>
<span data-ttu-id="7f5e0-162">Azure Resource Manager에서 리소스 그룹을 사용하여 Azure 구독에서 모든 응용 프로그램 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-162">In Azure Resource Manager, you can use resource groups to manage all the application resources in your Azure subscription.</span></span> <span data-ttu-id="7f5e0-163">통합 접근 방식의 리소스 그룹에서는 모든 리소스가 동일한 수명 주기를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-163">An integrated approach, in a resource group, all resources have the same life cycle.</span></span> <span data-ttu-id="7f5e0-164">예를 들어 모든 리소스가 동시에 생성되고 동시에 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-164">For example, all resources are created at the same time and they are deleted at the same time.</span></span> <span data-ttu-id="7f5e0-165">[리소스 그룹](../../../azure-resource-manager/resource-group-overview.md#resource-groups)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-165">Learn more about [resource groups](../../../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

### <span data-ttu-id="7f5e0-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure 리소스 그룹에 대한 Azure 내부 부하 분산 장치 종속성</span><span class="sxs-lookup"><span data-stu-id="7f5e0-166"><a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a> Azure internal load balancer dependency on the Azure resource group</span></span>

<span data-ttu-id="7f5e0-167">Azure 클래식 배포 모델에는 Azure 내부 부하 분산 장치(Azure Load Balancer 서비스)와 클라우드 서비스 간의 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-167">In the Azure classic deployment model, there is a dependency between the Azure internal load balancer (Azure Load Balancer service) and the cloud service.</span></span> <span data-ttu-id="7f5e0-168">모든 내부 부하 분산 장치에는 하나의 클라우드 서비스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-168">Every internal load balancer needs one cloud service.</span></span>

<span data-ttu-id="7f5e0-169">Azure Resource Manager에서는 모든 Azure 리소스를 Azure 리소스 그룹에 배치해야 합니다. Azure Load Balancer의 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-169">In Azure Resource Manager, every Azure resource needs to be placed into an Azure resource group, and this is valid for Azure Load Balancer as well.</span></span> <span data-ttu-id="7f5e0-170">그러나 Azure 리소스 그룹이 Azure Load Balancer당 하나씩 있어야 하는 것은 아닙니다. 즉, Azure 리소스 그룹 하나에 여러 Azure Load Balancer가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-170">However, there is no need to have one Azure resource group per Azure load balancer, e.g. one Azure resource group can contain multiple Azure Load Balancers.</span></span> <span data-ttu-id="7f5e0-171">환경은 더 간단하고 보다 유연합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-171">The environment is simpler and more flexible.</span></span> 

### <a name="support-for-sap-multi-sid-scenarios"></a><span data-ttu-id="7f5e0-172">SAP 다중 SID 지원 시나리오</span><span class="sxs-lookup"><span data-stu-id="7f5e0-172">Support for SAP multi-SID scenarios</span></span>

<span data-ttu-id="7f5e0-173">Azure Resource Manager에서 하나의 클러스터에 여러 SAP SID(시스템 식별자) ASCS/SCS 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-173">In Azure Resource Manager, you can install multiple SAP system identifier (SID) ASCS/SCS instances in one cluster.</span></span> <span data-ttu-id="7f5e0-174">각 Azure 내부 부하 분산 장치의 여러 IP 주소에 대한 지원으로 인해 다중 SID 인스턴스가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-174">Multi-SID instances are possible because of support for multiple IP addresses for each Azure internal load balancer.</span></span>

<span data-ttu-id="7f5e0-175">Azure 클래식 배포 모델을 사용하려면 [Azure의 SAP NetWeaver: SIOS Datakeeper를 통해 Azure에서 Windows Server 장애 조치 클러스터를 사용하여 SAP ASCS/SCS 인스턴스 클러스터링](http://go.microsoft.com/fwlink/?LinkId=613056)에 설명된 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-175">To use the Azure classic deployment model, follow the procedures described in [SAP NetWeaver in Azure: Clustering SAP ASCS/SCS instances by using Windows Server Failover Clustering in Azure with SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f5e0-176">SAP 설치를 위해서는 Azure Resource Manager 배포 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-176">We strongly recommend that you use the Azure Resource Manager deployment model for your SAP installations.</span></span> <span data-ttu-id="7f5e0-177">이 모델은 클래식 배포 모델에서 사용할 수 없는 다양한 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-177">It offers many benefits that are not available in the classic deployment model.</span></span> <span data-ttu-id="7f5e0-178">Azure [배포 모델][virtual-machines-azure-resource-manager-architecture-benefits-arm]에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-178">Learn more about Azure [deployment models][virtual-machines-azure-resource-manager-architecture-benefits-arm].</span></span>   
>
>

## <span data-ttu-id="7f5e0-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server 장애 조치 클러스터링</span><span class="sxs-lookup"><span data-stu-id="7f5e0-179"><a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering</span></span>
<span data-ttu-id="7f5e0-180">Windows Server 장애 조치 클러스터링은 Windows에서 고가용성 SAP ASCS/SCS를 설치하고 DBMS를 사용하기 위한 기반이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-180">Windows Server Failover Clustering is the foundation of a high-availability SAP ASCS/SCS installation and DBMS in Windows.</span></span>

<span data-ttu-id="7f5e0-181">장애 조치 클러스터는 함께 작동하여 응용 프로그램 및 서비스의 가용성을 높이는 1+n개 독립 서버(노드) 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-181">A failover cluster is a group of 1+n independent servers (nodes) that work together to increase the availability of applications and services.</span></span> <span data-ttu-id="7f5e0-182">노드에 장애가 발생하는 경우 Windows Server 장애 조치 클러스터링은 응용 프로그램 및 서비스를 제공하기 위해 정상 클러스터를 유지 관리하는 동안 발생할 수 있는 장애 횟수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-182">If a node failure occurs, Windows Server Failover Clustering calculates the number of failures that can occur while maintaining a healthy cluster to provide applications and services.</span></span> <span data-ttu-id="7f5e0-183">장애 조치 클러스터링을 달성하기 위해 여러 다른 쿼럼 모드 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-183">You can choose from different quorum modes to achieve failover clustering.</span></span>

### <span data-ttu-id="7f5e0-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> 쿼럼 모드</span><span class="sxs-lookup"><span data-stu-id="7f5e0-184"><a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Quorum modes</span></span>
<span data-ttu-id="7f5e0-185">Windows Server 장애 조치 클러스터링을 사용하는 경우 다음 4개의 쿼럼 모드 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-185">You can choose from four quorum modes when you use Windows Server Failover Clustering:</span></span>

* <span data-ttu-id="7f5e0-186">**노드 과반수**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-186">**Node Majority**.</span></span> <span data-ttu-id="7f5e0-187">각 클러스터 노드에서 투표할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-187">Each node of the cluster can vote.</span></span> <span data-ttu-id="7f5e0-188">클러스터는 투표 수의 과반수, 즉 절반 이상일 때만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-188">The cluster functions only with a majority of votes, that is, with more than half the votes.</span></span> <span data-ttu-id="7f5e0-189">노드 수가 균일하지 않은 클러스터에 대해 이 옵션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-189">We recommend this option for clusters that have an uneven number of nodes.</span></span> <span data-ttu-id="7f5e0-190">예를 들어 7 노드 클러스터 중에서 3개의 노드에서 장애가 발생해도 클러스터는 과반수 조건이 충족되므로 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-190">For example, three nodes in a seven-node cluster can fail, and the cluster stills achieves a majority and continues to run.</span></span>  
* <span data-ttu-id="7f5e0-191">**노드 및 디스크 과반수**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-191">**Node and Disk Majority**.</span></span> <span data-ttu-id="7f5e0-192">사용 가능하고 통신이 설정되어 있을 때마다 각 노드와 클러스터 Storage의 지정된 디스크(디스크 감시)가 투표할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-192">Each node and a designated disk (a disk witness) in the cluster storage can vote when they are available and in communication.</span></span> <span data-ttu-id="7f5e0-193">클러스터는 투표 수의 과반수, 즉 절반 이상일 때만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-193">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="7f5e0-194">이 모드는 노드 수가 짝수인 클러스터 환경에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-194">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="7f5e0-195">노드 및 디스크 절반이 온라인 상태이면 클러스터는 정상 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-195">If half the nodes and the disk are online, the cluster remains in a healthy state.</span></span>
* <span data-ttu-id="7f5e0-196">**노드 및 파일 공유 과반수**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-196">**Node and File Share Majority**.</span></span> <span data-ttu-id="7f5e0-197">노드 및 파일 공유가 사용 가능하고 통신이 설정되어 있는지에 관계 없이 각 노드와 관리자가 만든 지정된 파일 공유를 더한 크기(파일 공유 감시)가 투표할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-197">Each node plus a designated file share (a file share witness) that the administrator creates can vote, regardless of whether the nodes and file share are available and in communication.</span></span> <span data-ttu-id="7f5e0-198">클러스터는 투표 수의 과반수, 즉 절반 이상일 때만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-198">The cluster functions only with a majority of the votes, that is, with more than half the votes.</span></span> <span data-ttu-id="7f5e0-199">이 모드는 노드 수가 짝수인 클러스터 환경에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-199">This mode makes sense in a cluster environment with an even number of nodes.</span></span> <span data-ttu-id="7f5e0-200">이 모드는 노드 및 디스크 과반수 모드와 유사하지만 감시 디스크 대신 감시 파일 공유를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-200">It's similar to the Node and Disk Majority mode, but it uses a witness file share instead of a witness disk.</span></span> <span data-ttu-id="7f5e0-201">이 모드는 구현하기는 쉽지만 파일 공유 자체의 가용성이 낮을 경우 단일 실패 지점이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-201">This mode is easy to implement, but if the file share itself is not highly available, it might become a single point of failure.</span></span>
* <span data-ttu-id="7f5e0-202">**과반수 없음: 디스크만**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-202">**No Majority: Disk Only**.</span></span> <span data-ttu-id="7f5e0-203">하나의 노드를 사용할 수 있고 클러스터 Storage의 특정 디스크와 통신이 설정된 경우 클러스터에는 쿼럼이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-203">The cluster has a quorum if one node is available and in communication with a specific disk in the cluster storage.</span></span> <span data-ttu-id="7f5e0-204">해당 디스크와도 통신하는 노드만 클러스터에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-204">Only the nodes that also are in communication with that disk can join the cluster.</span></span> <span data-ttu-id="7f5e0-205">이 모드는 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-205">We recommend that you do not use this mode.</span></span>
 

## <span data-ttu-id="7f5e0-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server 장애 조치 클러스터링 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-206"><a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering on-premises</span></span>
<span data-ttu-id="7f5e0-207">그림 1에서는 두 노드 클러스터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-207">Figure 1 shows a cluster of two nodes.</span></span> <span data-ttu-id="7f5e0-208">노드 간 네트워크 연결이 끊어지고 두 노드는 계속 작동될 경우 쿼럼 디스크 또는 파일 공유는 클러스터의 응용 프로그램 및 서비스를 계속 제공할 노드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-208">If the network connection between the nodes fails and both nodes stay up and running, a quorum disk or file share determines which node will continue to provide the cluster's applications and services.</span></span> <span data-ttu-id="7f5e0-209">쿼럼 디스크 또는 파일 공유에 액세스할 수 있는 노드는 서비스가 계속되도록 하는 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-209">The node that has access to the quorum disk or file share is the node that ensures that services continue.</span></span>

<span data-ttu-id="7f5e0-210">이 예제에서는 두 노드 클러스터를 사용하므로 노드 및 파일 공유 과반수 쿼럼 모드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-210">Because this example uses a two-node cluster, we use the Node and File Share Majority quorum mode.</span></span> <span data-ttu-id="7f5e0-211">노드 및 디스크 과반수도 사용 가능한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-211">The Node and Disk Majority also is a valid option.</span></span> <span data-ttu-id="7f5e0-212">프로덕션 환경에서는 쿼럼 디스크를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-212">In a production environment, we recommend that you use a quorum disk.</span></span> <span data-ttu-id="7f5e0-213">네트워크 및 Storage 시스템 기술을 사용하여 항상 고가용성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-213">You can use network and storage system technology to make it highly available.</span></span>

![그림 1: Azure에서 SAP ASCS/SCS에 대한 Windows Server 장애 조치 클러스터링 구성 예제][sap-ha-guide-figure-1000]

<span data-ttu-id="7f5e0-215">_**그림 1:** Azure에서 SAP ASCS/SCS에 대한 Windows Server 장애 조치 클러스터링 구성 예제_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-215">_**Figure 1:** Example of a Windows Server Failover Clustering configuration for SAP ASCS/SCS in Azure_</span></span>

### <span data-ttu-id="7f5e0-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> 공유 Storage</span><span class="sxs-lookup"><span data-stu-id="7f5e0-216"><a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Shared storage</span></span>
<span data-ttu-id="7f5e0-217">그림 1에는 2 노드 공유 Storage 클러스터도 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-217">Figure 1 also shows a two-node shared storage cluster.</span></span> <span data-ttu-id="7f5e0-218">온-프레미스 공유 Storage 클러스터에서 클러스터의 모든 노드는 공유 Storage를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-218">In an on-premises shared storage cluster, all nodes in the cluster detect shared storage.</span></span> <span data-ttu-id="7f5e0-219">잠금 메커니즘을 통해 데이터가 손상으로부터 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-219">A locking mechanism protects the data from corruption.</span></span> <span data-ttu-id="7f5e0-220">모든 노드는 다른 노드에 장애가 있는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-220">All nodes can detect if another node fails.</span></span> <span data-ttu-id="7f5e0-221">한 노드가 실패하면 나머지 하나가 Storage 리소스의 소유권을 가지며, 서비스의 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-221">If one node fails, the remaining node takes ownership of the storage resources and ensures the availability of services.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-222">SQL Server와 같은 일부 DBMS 응용 프로그램에서는 가용성을 높이기 위해 공유 디스크를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-222">You don't need shared disks for high availability with some DBMS applications, like with SQL Server.</span></span> <span data-ttu-id="7f5e0-223">SQL Server AlwaysOn은 한 클러스터 노드의 로컬 디스크에서 다른 클러스터 노드의 로컬 디스크로 DBMS 데이터 및 로그 파일을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-223">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="7f5e0-224">이 경우 Windows 클러스터 구성에는 공유 디스크가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-224">In that case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="7f5e0-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> 네트워킹 및 이름 확인</span><span class="sxs-lookup"><span data-stu-id="7f5e0-225"><a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Networking and name resolution</span></span>
<span data-ttu-id="7f5e0-226">클라이언트 컴퓨터는 DNS 서버에서 제공하는 가상 IP 주소 및 가상 호스트 이름을 통해 클러스터에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-226">Client computers reach the cluster over a virtual IP address and a virtual host name that the DNS server provides.</span></span> <span data-ttu-id="7f5e0-227">온-프레미스 노드와 DNS 서버는 여러 개의 IP 주소를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-227">The on-premises nodes and the DNS server can handle multiple IP addresses.</span></span>

<span data-ttu-id="7f5e0-228">표준 설치에서는 다음 두 가지 이상의 네트워크 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-228">In a typical setup, you use two or more network connections:</span></span>

* <span data-ttu-id="7f5e0-229">Storage에 대한 전용 연결</span><span class="sxs-lookup"><span data-stu-id="7f5e0-229">A dedicated connection to the storage</span></span>
* <span data-ttu-id="7f5e0-230">하트비트에 대한 클러스터 내부 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="7f5e0-230">A cluster-internal network connection for the heartbeat</span></span>
* <span data-ttu-id="7f5e0-231">클라이언트에서 클러스터에 연결하는 데 사용하는 공용 네트워크</span><span class="sxs-lookup"><span data-stu-id="7f5e0-231">A public network that clients use to connect to the cluster</span></span>

## <span data-ttu-id="7f5e0-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Azure의 Windows Server 장애 조치 클러스터링</span><span class="sxs-lookup"><span data-stu-id="7f5e0-232"><a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="7f5e0-233">운영 체제 미설치 또는 사설 클라우드 배포에 비해, Azure Virtual Machines는 Windows Server 장애 조치 클러스터링을 구성하기 위한 추가 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-233">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="7f5e0-234">공유 클러스터 디스크를 만들려면 SAP ASCS/SCS 인스턴스에 대해 여러 개의 IP 주소 및 가상 호스트 이름을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-234">When you build a shared cluster disk, you need to set several IP addresses and virtual host names for the SAP ASCS/SCS instance.</span></span>

<span data-ttu-id="7f5e0-235">이 문서에서는 Azure에서 SAP 고가용성 중앙 서비스 클러스터를 구축하는 데 필요한 핵심 개념 및 추가 단계에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-235">In this article, we discuss key concepts and the additional steps required to build an SAP high-availability central services cluster in Azure.</span></span> <span data-ttu-id="7f5e0-236">타사 도구 SIOS DataKeeper를 설정하고 Azure 내부 부하 분산 장치를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-236">We show you how to set up the third-party tool SIOS DataKeeper, and how to configure the Azure internal load balancer.</span></span> <span data-ttu-id="7f5e0-237">이러한 도구와 Azure에서 파일 공유 감시를 사용하여 Windows 장애 조치 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-237">You can use these tools to create a Windows failover cluster with a file share witness in Azure.</span></span>

![그림 2: 공유 디스크를 사용하지 않는 Azure의 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1001]

<span data-ttu-id="7f5e0-239">_**그림 2:** 공유 디스크를 사용하지 않는 Azure의 Windows Server 장애 조치 클러스터링 구성_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-239">_**Figure 2:** Windows Server Failover Clustering configuration in Azure without a shared disk_</span></span>

### <span data-ttu-id="7f5e0-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> SIOS DataKeeper를 사용한 Azure의 공유 디스크</span><span class="sxs-lookup"><span data-stu-id="7f5e0-240"><a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Shared disk in Azure with SIOS DataKeeper</span></span>
<span data-ttu-id="7f5e0-241">고가용성 SAP ASCS/SCS 인스턴스를 위해서는 클러스터 공유 Storage가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-241">You need cluster shared storage for a high-availability SAP ASCS/SCS instance.</span></span> <span data-ttu-id="7f5e0-242">2016년 9월을 기준으로 Azure는 공유 Storage 클러스터를 만드는 데 사용할 수 있는 공유 Storage를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-242">As of September 2016, Azure doesn't offer shared storage that you can use to create a shared storage cluster.</span></span> <span data-ttu-id="7f5e0-243">타사 소프트웨어 SIOS DataKeeper Cluster Edition을 사용하여 클러스터 공유 Storage를 시뮬레이션하는 미러링된 Storage를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-243">You can use third-party software SIOS DataKeeper Cluster Edition to create a mirrored storage that simulates cluster shared storage.</span></span> <span data-ttu-id="7f5e0-244">SIOS 솔루션은 실시간 동기 데이터 복제 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-244">The SIOS solution provides real-time synchronous data replication.</span></span> <span data-ttu-id="7f5e0-245">다음은 클러스터에 대한 공유 디스크 리소스를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-245">This is how you can create a shared disk resource for a cluster:</span></span>

1. <span data-ttu-id="7f5e0-246">Windows 클러스터 구성에 있는 각 VM(가상 컴퓨터)에 추가 디스크 하나를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-246">Attach an additional disk to each of the virtual machines (VMs) in a Windows cluster configuration.</span></span>
2. <span data-ttu-id="7f5e0-247">두 가상 컴퓨터 노드에서 SIOS DataKeeper Cluster Edition을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-247">Run SIOS DataKeeper Cluster Edition on both virtual machine nodes.</span></span>
3. <span data-ttu-id="7f5e0-248">원본 가상 컴퓨터의 추가 디스크 연결 볼륨의 콘텐츠를 대상 가상 컴퓨터의 추가 디스크 연결 볼륨에 미러링하는 방식으로 SIOS DataKeeper Cluster Edition을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-248">Configure SIOS DataKeeper Cluster Edition so that it mirrors the content of the additional disk attached volume from the source virtual machine to the additional disk attached volume of the target virtual machine.</span></span> <span data-ttu-id="7f5e0-249">SIOS DataKeeper는 원본 및 대상 로컬 볼륨을 추상화한 다음 Windows Server 장애 조치 클러스터링에 단일 공유 디스크로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-249">SIOS DataKeeper abstracts the source and target local volumes, and then presents them to Windows Server Failover Clustering as one shared disk.</span></span>

<span data-ttu-id="7f5e0-250">[SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/)에 대한 자세한 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-250">Get more information about [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).</span></span>

![그림 3: SIOS DataKeeper를 사용하는 Azure의 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1002]

<span data-ttu-id="7f5e0-252">_**그림 3:** SIOS DataKeeper를 사용하는 Azure의 Windows Server 장애 조치 클러스터링 구성_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-252">_**Figure 3:** Windows Server Failover Clustering configuration in Azure with SIOS DataKeeper_</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-253">SQL Server와 같은 일부 DBMS 제품에서는 가용성을 높이기 위해 공유 디스크를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-253">You don't need shared disks for high availability with some DBMS products, like SQL Server.</span></span> <span data-ttu-id="7f5e0-254">SQL Server AlwaysOn은 한 클러스터 노드의 로컬 디스크에서 다른 클러스터 노드의 로컬 디스크로 DBMS 데이터 및 로그 파일을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-254">SQL Server Always On replicates DBMS data and log files from the local disk of one cluster node to the local disk of another cluster node.</span></span> <span data-ttu-id="7f5e0-255">이 경우 Windows 클러스터 구성에는 공유 디스크가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-255">In this case, the Windows cluster configuration doesn't need a shared disk.</span></span>
>
>

### <span data-ttu-id="7f5e0-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Azure의 이름 확인</span><span class="sxs-lookup"><span data-stu-id="7f5e0-256"><a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Name resolution in Azure</span></span>
<span data-ttu-id="7f5e0-257">Azure 클라우드 플랫폼은 부동 IP 주소와 같은 가상 IP 주소를 구성하는 옵션을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-257">The Azure cloud platform doesn't offer the option to configure virtual IP addresses, such as floating IP addresses.</span></span> <span data-ttu-id="7f5e0-258">클라우드의 클러스터 리소스에 연결하도록 가상 IP 주소를 설정하기 위한 대체 솔루션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-258">You need an alternative solution to set up a virtual IP address to reach the cluster resource in the cloud.</span></span>
<span data-ttu-id="7f5e0-259">Azure의 Azure Load Balancer 서비스에는 내부 부하 분산 장치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-259">Azure has an internal load balancer in the Azure Load Balancer service.</span></span> <span data-ttu-id="7f5e0-260">내부 부하 분산 장치를 사용하면 클라이언트는 클러스터 가상 IP 주소를 통해 클러스터에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-260">With the internal load balancer, clients reach the cluster over the cluster virtual IP address.</span></span>
<span data-ttu-id="7f5e0-261">클러스터 노드를 포함하는 리소스 그룹에 부하 분산 장치를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-261">You need to deploy the internal load balancer in the resource group that contains the cluster nodes.</span></span> <span data-ttu-id="7f5e0-262">그런 후 내부 부하 분산 장치의 프로브 포트를 사용하여 필요한 모든 포트 전달 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-262">Then, configure all necessary port forwarding rules with the probe ports of the internal load balancer.</span></span>
<span data-ttu-id="7f5e0-263">클라이언트는 가상 호스트 이름을 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-263">The clients can connect via the virtual host name.</span></span> <span data-ttu-id="7f5e0-264">DNS 서버는 클러스터 IP 주소를 확인하고 내부 부하 분산 장치는 클러스터의 활성 노드에 대한 포트 전달을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-264">The DNS server resolves the cluster IP address, and the internal load balancer handles port forwarding to the active node of the cluster.</span></span>

## <span data-ttu-id="7f5e0-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Azure IaaS(Infrastructure-as-a-Service)의 SAP NetWeaver 고가용성</span><span class="sxs-lookup"><span data-stu-id="7f5e0-265"><a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver high availability in Azure Infrastructure-as-a-Service (IaaS)</span></span>
<span data-ttu-id="7f5e0-266">SAP 응용 프로그램 고가용성(예: SAP 소프트웨어 구성 요소)을 달성하려면 다음 구성 요소를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-266">To achieve SAP application high availability, such as for SAP software components, you need to protect the following components:</span></span>

* <span data-ttu-id="7f5e0-267">SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-267">SAP Application Server instance</span></span>
* <span data-ttu-id="7f5e0-268">SAP ASCS/SCS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-268">SAP ASCS/SCS instance</span></span>
* <span data-ttu-id="7f5e0-269">DBMS 서버</span><span class="sxs-lookup"><span data-stu-id="7f5e0-269">DBMS server</span></span>

<span data-ttu-id="7f5e0-270">고가용성 시나리오에서 SAP 구성 요소 보호에 대한 자세한 내용은 [SAP NetWeaver에 대한 Azure Virtual Machines 계획 및 구현][planning-guide-11]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-270">For more information about protecting SAP components in high-availability scenarios, see [Azure Virtual Machines planning and implementation for SAP NetWeaver][planning-guide-11].</span></span>

### <span data-ttu-id="7f5e0-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> 고가용성 SAP 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="7f5e0-271"><a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> High-availability SAP Application Server</span></span>
<span data-ttu-id="7f5e0-272">일반적으로 SAP 응용 프로그램 서버 및 대화 상자 인스턴스의 경우 특정 고가용성 솔루션이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-272">You usually don't need a specific high-availability solution for the SAP Application Server and dialog instances.</span></span> <span data-ttu-id="7f5e0-273">중복성으로 고가용성을 달성하고 다른 Azure Virtual Machines 인스턴스에서 여러 대화 상자 인스턴스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-273">You achieve high availability by redundancy, and you'll configure multiple dialog instances in different instances of Azure Virtual Machines.</span></span> <span data-ttu-id="7f5e0-274">두 개의 Azure Virtual Machines 인스턴스에 2개 이상의 SAP 응용 프로그램 인스턴스가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-274">You should have at least two SAP application instances installed in two instances of Azure Virtual Machines.</span></span>

![그림 4: 고가용성 SAP 응용 프로그램 서버][sap-ha-guide-figure-2000]

<span data-ttu-id="7f5e0-276">_**그림 4:** 고가용성 SAP 응용 프로그램 서버_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-276">_**Figure 4:** High-availability SAP Application Server_</span></span>

<span data-ttu-id="7f5e0-277">SAP 응용 프로그램 서버 인스턴스를 호스트하는 모든 가상 컴퓨터를 동일한 Azure 가용성 집합에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-277">You must place all virtual machines that host SAP Application Server instances in the same Azure availability set.</span></span> <span data-ttu-id="7f5e0-278">Azure 가용성 집합은 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-278">An Azure availability set ensures that:</span></span>

* <span data-ttu-id="7f5e0-279">모든 가상 컴퓨터가 동일한 업그레이드 도메인에 속하는지 여부.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-279">All virtual machines are part of the same upgrade domain.</span></span> <span data-ttu-id="7f5e0-280">예를 들어 업그레이드 도메인은 가상 컴퓨터가 계획된 유지 관리 가동 중지 시간 동안 동시에 업데이트되지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-280">An upgrade domain, for example, makes sure that the virtual machines aren't updated at the same time during planned maintenance downtime.</span></span>
* <span data-ttu-id="7f5e0-281">모든 가상 컴퓨터가 동일한 장애 도메인에 속하는지 여부.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-281">All virtual machines are part of the same fault domain.</span></span> <span data-ttu-id="7f5e0-282">예를 들어 장애 도메인은 어떤 단일 장애 지점도 모든 가상 컴퓨터의 가용성에 영향을 주지 않도록 가상 컴퓨터가 배포되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-282">A fault domain, for example, makes sure that virtual machines are deployed so that no single point of failure affects the availability of all virtual machines.</span></span>

<span data-ttu-id="7f5e0-283">[가상 컴퓨터의 가용성 관리][virtual-machines-manage-availability] 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-283">Learn more about how to [manage the availability of virtual machines][virtual-machines-manage-availability].</span></span>

<span data-ttu-id="7f5e0-284">비관리 디스크에만 해당하는 설명: Azure Storage 계정은 잠재적인 단일 실패 지점일 수 있으므로 둘 이상의 가상 컴퓨터가 배포될 둘 이상의 Azure Storage 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-284">Unmanaged disk only: Because the Azure storage account is a potential single point of failure, it's important to have at least two Azure storage accounts, in which at least two virtual machines are distributed.</span></span> <span data-ttu-id="7f5e0-285">이상적인 설치에서는 SAP 대화 상자 인스턴스를 실행하는 각 가상 컴퓨터의 디스크를 다른 저장소 계정에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-285">In an ideal setup, the disks of each virtual machine that is running an SAP dialog instance would be deployed in a different storage account.</span></span>

### <span data-ttu-id="7f5e0-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> 고가용성 SAP ASCS/SCS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-286"><a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> High-availability SAP ASCS/SCS instance</span></span>
<span data-ttu-id="7f5e0-287">그림 5는 고가용성 SAP ASCS/SCS 인스턴스의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-287">Figure 5 is an example of a high-availability SAP ASCS/SCS instance.</span></span>

![그림 5: 고가용성 SAP ASCS/SCS 인스턴스][sap-ha-guide-figure-2001]

<span data-ttu-id="7f5e0-289">_**그림 5:** 고가용성 SAP ASCS/SCS 인스턴스_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-289">_**Figure 5:** High-availability SAP ASCS/SCS instance_</span></span>

#### <span data-ttu-id="7f5e0-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Azure에서 Windows Server 장애 조치 클러스터링을 사용한 SAP ASCS/SCS 인스턴스 고가용성</span><span class="sxs-lookup"><span data-stu-id="7f5e0-290"><a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> SAP ASCS/SCS instance high availability with Windows Server Failover Clustering in Azure</span></span>
<span data-ttu-id="7f5e0-291">운영 체제 미설치 또는 사설 클라우드 배포에 비해, Azure Virtual Machines는 Windows Server 장애 조치 클러스터링을 구성하기 위한 추가 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-291">Compared to bare metal or private cloud deployments, Azure Virtual Machines requires additional steps to configure Windows Server Failover Clustering.</span></span> <span data-ttu-id="7f5e0-292">Windows 장애 조치 클러스터를 구축하려면 SAP ASCS/SCS 인스턴스를 클러스터링하기 위한 공유 클러스터 디스크, 일부 IP 주소, 가상 호스트 이름 및 Azure 내부 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-292">To build a Windows failover cluster, you need a shared cluster disk, several IP addresses, several virtual host names, and an Azure internal load balancer for clustering an SAP ASCS/SCS instance.</span></span> <span data-ttu-id="7f5e0-293">이 내용은 문서 뒷부분에서 좀 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-293">We discuss this in more detail later in the article.</span></span>

![그림 6: SIOS DataKeeper를 사용하는 Azure의 SAP ASCS/SCS용 Windows Server 장애 조치 클러스터링 구성][sap-ha-guide-figure-1002]

<span data-ttu-id="7f5e0-295">_**그림 6:** SIOS DataKeeper를 사용하는 Azure의 SAP ASCS/SCS용 Windows Server 장애 조치 클러스터링 구성_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-295">_**Figure 6:** Windows Server Failover Clustering for an SAP ASCS/SCS configuration in Azure with SIOS DataKeeper_</span></span>

### <span data-ttu-id="7f5e0-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> 고가용성 DBMS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-296"><a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>High-availability DBMS instance</span></span>
<span data-ttu-id="7f5e0-297">DBMS는 SAP 시스템의 단일 연락 지점이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-297">The DBMS also is a single point of contact in an SAP system.</span></span> <span data-ttu-id="7f5e0-298">따라서 고가용성 솔루션을 사용하여 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-298">You need to protect it by using a high-availability solution.</span></span> <span data-ttu-id="7f5e0-299">그림 7에서는 Windows Server 장애 조치 클러스터링 및 Azure 내부 부하 분산 장치를 사용하여 Azure의 SQL Server Always On 고가용성 솔루션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-299">Figure 7 shows a SQL Server Always On high-availability solution in Azure, with Windows Server Failover Clustering and the Azure internal load balancer.</span></span> <span data-ttu-id="7f5e0-300">SQL Server Always On은 자체 DBMS 복제를 사용하여 DBMS 데이터 및 로그 파일을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-300">SQL Server Always On replicates DBMS data and log files by using its own DBMS replication.</span></span> <span data-ttu-id="7f5e0-301">이 경우 전체 설정을 간소화하는 클러스터 공유 디스크가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-301">In this case, you don't need cluster shared disks, which simplifies the entire setup.</span></span>

![그림 7: SQL Server Always On을 사용하는 고가용성 SAP DBMS 예제][sap-ha-guide-figure-2003]

<span data-ttu-id="7f5e0-303">_**그림 7:** SQL Server Always On을 사용하는 고가용성 SAP DBMS 예제_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-303">_**Figure 7:** Example of a high-availability SAP DBMS, with SQL Server Always On_</span></span>

<span data-ttu-id="7f5e0-304">Azure Resource Manager 배포 모델을 사용하는 Azure의 SQL Server 클러스터링에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-304">For more information about clustering SQL Server in Azure by using the Azure Resource Manager deployment model, see these articles:</span></span>

* <span data-ttu-id="7f5e0-305">[Resource Manager를 사용하여 Azure Virtual Machines에서 수동으로 Always On 가용성 그룹 구성][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-305">[Configure Always On availability group in Azure Virtual Machines manually by using Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]</span></span>
* <span data-ttu-id="7f5e0-306">[Azure에서 Always On 가용성 그룹에 대한 Azure 내부 부하 분산 장치 구성][virtual-machines-windows-portal-sql-alwayson-int-listener]</span><span class="sxs-lookup"><span data-stu-id="7f5e0-306">[Configure an Azure internal load balancer for an Always On availability group in Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]</span></span>

## <span data-ttu-id="7f5e0-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> 종단간 고가용성 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="7f5e0-307"><a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> End-to-end high-availability deployment scenarios</span></span>

### <a name="deployment-scenario-using-architectural-template-1"></a><span data-ttu-id="7f5e0-308">아키텍처 템플릿 1을 사용하여 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="7f5e0-308">Deployment scenario using Architectural Template 1</span></span>

<span data-ttu-id="7f5e0-309">그림 8에서는 **단일** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-309">Figure 8 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="7f5e0-310">이 시나리오는 다음과 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-310">This scenario is set up as follows:</span></span>

- <span data-ttu-id="7f5e0-311">하나의 전용 클러스터는 SAP ASCS/SCS 인스턴스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-311">One dedicated cluster is used for the SAP ASCS/SCS instance.</span></span>
- <span data-ttu-id="7f5e0-312">하나의 전용 클러스터는 DBMS 인스턴스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-312">One dedicated cluster is used for the DBMS instance.</span></span>
- <span data-ttu-id="7f5e0-313">SAP 응용 프로그램 서버 인스턴스는 자체의 전용 VM에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-313">SAP Application Server instances are deployed in their own dedicated VMs.</span></span>

![그림 8: ASCS/SCS 및 DBMS용 전용 클러스터를 사용하는 SAP 고가용성 아키텍처 템플릿 1][sap-ha-guide-figure-2004]

<span data-ttu-id="7f5e0-315">_**그림 8:** SAP 고가용성 아키텍처 템플릿 1, ASCS/SCS 및 DBMS용 전용 클러스터_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-315">_**Figure 8:** SAP high-availability Architectural Template 1, dedicated clusters for ASCS/SCS and DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-2"></a><span data-ttu-id="7f5e0-316">아키텍처 템플릿 2를 사용하여 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="7f5e0-316">Deployment scenario using Architectural Template 2</span></span>

<span data-ttu-id="7f5e0-317">그림 9에서는 **단일** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-317">Figure 9 shows an example of an SAP NetWeaver high-availability architecture in Azure for **one** SAP system.</span></span> <span data-ttu-id="7f5e0-318">이 시나리오는 다음과 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-318">This scenario is set up as follows:</span></span>

- <span data-ttu-id="7f5e0-319">하나의 전용 클러스터는 SAP ASCS/SCS 인스턴스 및 DBMS **모두**에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-319">One dedicated cluster is used for **both** the SAP ASCS/SCS instance and the DBMS.</span></span>
- <span data-ttu-id="7f5e0-320">SAP 응용 프로그램 서버 인스턴스는 자체의 전용 VM에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-320">SAP Application Server instances are deployed in own dedicated VMs.</span></span>

![그림 9: SAP 고가용성 아키텍처 템플릿 2 - ASCS/SCS 전용 클러스터 및 DBMS 전용 클러스터][sap-ha-guide-figure-2005]

<span data-ttu-id="7f5e0-322">_**그림 9:** SAP 고가용성 아키텍처 템플릿 2 - ASCS/SCS 전용 클러스터 및 DBMS 전용 클러스터_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-322">_**Figure 9:** SAP high-availability Architectural Template 2, with a dedicated cluster for ASCS/SCS and a dedicated cluster for DBMS_</span></span>

### <a name="deployment-scenario-using-architectural-template-3"></a><span data-ttu-id="7f5e0-323">아키텍처 템플릿 3을 사용하여 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="7f5e0-323">Deployment scenario using Architectural Template 3</span></span>

<span data-ttu-id="7f5e0-324">그림 10에서는 &lt;SID1&gt; 및 &lt;SID2&gt;의 **두** SAP 시스템을 위한 Azure의 SAP NetWeaver 고가용성 아키텍처의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-324">Figure 10 shows an example of an SAP NetWeaver high-availability architecture in Azure for **two** SAP systems, with &lt;SID1&gt; and &lt;SID2&gt;.</span></span> <span data-ttu-id="7f5e0-325">이 시나리오는 다음과 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-325">This scenario is set up as follows:</span></span>

- <span data-ttu-id="7f5e0-326">하나의 전용 클러스터는 SAP ASCS/SCS SID1 인스턴스 *및* SAP ASCS/SCS SID2 인스턴스 **모두**에 사용됩니다(하나의 클러스터).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-326">One dedicated cluster is used for **both** the SAP ASCS/SCS SID1 instance *and* the SAP ASCS/SCS SID2 instance (one cluster).</span></span>
- <span data-ttu-id="7f5e0-327">하나의 전용 클러스터는 DBMS SID1에 사용되고 다른 전용 클러스터는 DBMS SID2에 사용됩니다(두 개의 클러스터).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-327">One dedicated cluster is used for DBMS SID1, and another dedicated cluster is used for DBMS SID2 (two clusters).</span></span>
- <span data-ttu-id="7f5e0-328">SAP 시스템 SID1에 대한 SAP 응용 프로그램 서버 인스턴스에는 자체의 전용 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-328">SAP Application Server instances for the SAP system SID1 have their own dedicated VMs.</span></span>
- <span data-ttu-id="7f5e0-329">SAP 시스템 SID2에 대한 SAP 응용 프로그램 서버 인스턴스에는 자체의 전용 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-329">SAP Application Server instances for the SAP system SID2 have their own dedicated VMs.</span></span>

![그림 10: SAP 고가용성 아키텍처 템플릿 3 - 다른 ASCS/SCS 인스턴스 전용 클러스터][sap-ha-guide-figure-6003]

<span data-ttu-id="7f5e0-331">_**그림 10:** SAP 고가용성 아키텍처 템플릿 3 - 다른 ASCS/SCS 인스턴스 전용 클러스터_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-331">_**Figure 10:** SAP high-availability Architectural Template 3, with a dedicated cluster for different ASCS/SCS instances_</span></span>

## <span data-ttu-id="7f5e0-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="7f5e0-332"><a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a> Prepare the infrastructure</span></span>

### <a name="prepare-the-infrastructure-for-architectural-template-1"></a><span data-ttu-id="7f5e0-333">아키텍처 템플릿 1에 대한 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="7f5e0-333">Prepare the infrastructure for Architectural Template 1</span></span>
<span data-ttu-id="7f5e0-334">SAP용 Azure Resource Manager 템플릿은 필요한 리소스의 배포를 간소화하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-334">Azure Resource Manager templates for SAP help simplify deployment of required resources.</span></span>

<span data-ttu-id="7f5e0-335">또한 Azure Resource Manager의 3계층 템플릿은 2개의 클러스터가 있는 아키텍처 템플릿 1과 같은 고가용성 시나리오도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-335">The three-tier templates in Azure Resource Manager also support high-availability scenarios, such as in Architectural Template 1, which has two clusters.</span></span> <span data-ttu-id="7f5e0-336">각 클러스터는 SAP ASCS/SCS 및 DBMS에 대한 SAP 단일 실패 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-336">Each cluster is an SAP single point of failure for SAP ASCS/SCS and DBMS.</span></span>

<span data-ttu-id="7f5e0-337">이 문서에서 설명하는 예제 시나리오를 위한 Azure Resource Manager 템플릿을 가져올 수 있는 위치는 다음과 같습니다</span><span class="sxs-lookup"><span data-stu-id="7f5e0-337">Here's where you can get Azure Resource Manager templates for the example scenario we describe in this article:</span></span>

* [<span data-ttu-id="7f5e0-338">Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-338">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [<span data-ttu-id="7f5e0-339">관리 디스크를 사용하는 Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-339">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [<span data-ttu-id="7f5e0-340">사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-340">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [<span data-ttu-id="7f5e0-341">관리 디스크를 사용하는 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-341">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

<span data-ttu-id="7f5e0-342">아키텍처 템플릿 1에 대한 인프라를 준비하려면:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-342">To prepare the infrastructure for Architectural Template 1:</span></span>

- <span data-ttu-id="7f5e0-343">Azure Portal에서 **매개 변수** 블레이드의 **SYSTEMAVAILABILITY** 상자에서 **HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-343">In the Azure portal, on the **Parameters** blade, in the **SYSTEMAVAILABILITY** box, select **HA**.</span></span>

  ![그림 11: SAP 고가용성 Azure Resource Manager 매개 변수 설정][sap-ha-guide-figure-3000]

<span data-ttu-id="7f5e0-345">_**그림 11:** SAP 고가용성 Azure Resource Manager 매개 변수 설정_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-345">_**Figure 11:** Set SAP high-availability Azure Resource Manager parameters_</span></span>


  <span data-ttu-id="7f5e0-346">템플릿은 다음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-346">The templates create:</span></span>

  * <span data-ttu-id="7f5e0-347">**가상 컴퓨터**:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-347">**Virtual machines**:</span></span>
    * <span data-ttu-id="7f5e0-348">SAP 응용 프로그램 서버 가상 컴퓨터: <*SAPSystemSID*>-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-348">SAP Application Server virtual machines: <*SAPSystemSID*>-di-<*Number*></span></span>
    * <span data-ttu-id="7f5e0-349">ASCS/SCS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-349">ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-ascs-<*Number*></span></span>
    * <span data-ttu-id="7f5e0-350">DBMS 클러스터: <*SAPSystemSID*>-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-350">DBMS cluster: <*SAPSystemSID*>-db-<*Number*></span></span>

  * <span data-ttu-id="7f5e0-351">**연결된 IP 주소를 갖는 모든 가상 컴퓨터에 대한 네트워크 카드**:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-351">**Network cards for all virtual machines, with associated IP addresses**:</span></span>
    * <span data-ttu-id="7f5e0-352"><*SAPSystemSID*>-nic-di-<*Number*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-352"><*SAPSystemSID*>-nic-di-<*Number*></span></span>
    * <span data-ttu-id="7f5e0-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-353"><*SAPSystemSID*>-nic-ascs-<*Number*></span></span>
    * <span data-ttu-id="7f5e0-354"><*SAPSystemSID*>-nic-db-<*Number*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-354"><*SAPSystemSID*>-nic-db-<*Number*></span></span>

  * <span data-ttu-id="7f5e0-355">**Azure Storage 계정(비관리 디스크에만 해당)**</span><span class="sxs-lookup"><span data-stu-id="7f5e0-355">**Azure storage accounts (unmanaged disks only)**</span></span>

  * <span data-ttu-id="7f5e0-356">다음에 대한 **가용성 그룹**:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-356">**Availability groups** for:</span></span>
    * <span data-ttu-id="7f5e0-357">SAP 응용 프로그램 서버 가상 컴퓨터: <*SAPSystemSID*>-avset-di</span><span class="sxs-lookup"><span data-stu-id="7f5e0-357">SAP Application Server virtual machines: <*SAPSystemSID*>-avset-di</span></span>
    * <span data-ttu-id="7f5e0-358">SAP ASCS/SCS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-avset-ascs</span><span class="sxs-lookup"><span data-stu-id="7f5e0-358">SAP ASCS/SCS cluster virtual machines: <*SAPSystemSID*>-avset-ascs</span></span>
    * <span data-ttu-id="7f5e0-359">DBMS 클러스터 가상 컴퓨터: <*SAPSystemSID*>-avset-db</span><span class="sxs-lookup"><span data-stu-id="7f5e0-359">DBMS cluster virtual machines: <*SAPSystemSID*>-avset-db</span></span>

  * <span data-ttu-id="7f5e0-360">**Azure 내부 부하 분산 장치**:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-360">**Azure internal load balancer**:</span></span>
    * <span data-ttu-id="7f5e0-361">ASCS/SCS 인스턴스 및 IP 주소 <*SAPSystemSID*>-lb-ascs에 대한 모든 포트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-361">With all ports for the ASCS/SCS instance and IP address <*SAPSystemSID*>-lb-ascs</span></span>
    * <span data-ttu-id="7f5e0-362">SQL Server DBMS 및 IP 주소 <*SAPSystemSID*>-lb-db에 대한 모든 포트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-362">With all ports for the SQL Server DBMS and IP address <*SAPSystemSID*>-lb-db</span></span>

  * <span data-ttu-id="7f5e0-363">**네트워크 보안 그룹**: <*SAPSystemSID*>-nsg-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-363">**Network security group**: <*SAPSystemSID*>-nsg-ascs-0</span></span>  
    * <span data-ttu-id="7f5e0-364"><*SAPSystemSID*>-ascs-0 가상 컴퓨터에 대해 열려 있는 외부 RDP(원격 데스크톱 프로토콜) 포트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-364">With an open external Remote Desktop Protocol (RDP) port to the <*SAPSystemSID*>-ascs-0 virtual machine</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-365">네트워크 카드 및 Azure 내부 부하 분산 장치의 모든 IP 주소는 기본적으로 **동적**입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-365">All IP addresses of the network cards and Azure internal load balancers are **dynamic** by default.</span></span> <span data-ttu-id="7f5e0-366">이 주소를 **고정** IP 주소와 비교해보세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-366">Change them to **static** IP addresses.</span></span> <span data-ttu-id="7f5e0-367">이를 수행하는 방법은 문서 뒷부분에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-367">We describe how to do this later in the article.</span></span>
>
>

### <span data-ttu-id="7f5e0-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> 프로덕션 환경에서 사용하기 위해 회사 네트워크 연결(크로스-프레미스)을 사용하여 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="7f5e0-368"><a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a> Deploy virtual machines with corporate network connectivity (cross-premises) to use in production</span></span>
<span data-ttu-id="7f5e0-369">프로덕션 SAP 시스템의 경우 Azure 사이트 간 VPN 또는 Azure ExpressRoute를 사용하여 [회사 네트워크 연결(크로스-프레미스)][planning-guide-2.2]를 통해 Azure 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-369">For production SAP systems, deploy Azure virtual machines with [corporate network connectivity (cross-premises)][planning-guide-2.2] by using Azure Site-to-Site VPN or Azure ExpressRoute.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-370">Azure 가상 네트워크 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-370">You can use your Azure Virtual Network instance.</span></span> <span data-ttu-id="7f5e0-371">가상 네트워크 및 서브넷은 이미 생성되고 준비되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-371">The virtual network and subnet have already been created and prepared.</span></span>
>
>

1.  <span data-ttu-id="7f5e0-372">Azure Portal에서 **매개 변수** 블레이드의 **NEWOREXISTINGSUBNET** 상자에서 **기존**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-372">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **existing**.</span></span>
2.  <span data-ttu-id="7f5e0-373">Azure Virtual Machines를 배포하려는 경우 **SUBNETID** 상자에서 준비된 Azure 네트워크 서브넷 ID의 전체 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-373">In the **SUBNETID** box, add the full string of your prepared Azure network SubnetID where you plan to deploy your Azure virtual machines.</span></span>
3.  <span data-ttu-id="7f5e0-374">모든 Azure 네트워크 서브넷 목록을 가져오려면 이 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-374">To get a list of all Azure network subnets, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  <span data-ttu-id="7f5e0-375">**ID** 필드에 **SUBNETID**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-375">The **ID** field shows the **SUBNETID**.</span></span>
4. <span data-ttu-id="7f5e0-376">모든 **SUBNETID** 값 목록을 가져오려면 이 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-376">To get a list of all **SUBNETID** values, run this PowerShell command:</span></span>

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  <span data-ttu-id="7f5e0-377">**SUBNETID**는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-377">The **SUBNETID** looks like this:</span></span>

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <span data-ttu-id="7f5e0-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> 테스트 및 데모용 클라우드 전용 SAP 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="7f5e0-378"><a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Deploy cloud-only SAP instances for test and demo</span></span>
<span data-ttu-id="7f5e0-379">클라우드 전용 배포 모델에서 고가용성 SAP 시스템을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-379">You can deploy your high-availability SAP system in a cloud-only deployment model.</span></span> <span data-ttu-id="7f5e0-380">기본적으로 이러한 종류의 배포는 데모 및 테스트 사용 사례에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-380">This kind of deployment primarily is useful for demo and test use cases.</span></span> <span data-ttu-id="7f5e0-381">프로덕션 사용 사례에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-381">It's not suited for production use cases.</span></span>

- <span data-ttu-id="7f5e0-382">Azure Portal에서 **매개 변수** 블레이드의 **NEWOREXISTINGSUBNET** 상자에서 **신규**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-382">In the Azure portal, on the **Parameters** blade, in the **NEWOREXISTINGSUBNET** box, select **new**.</span></span> <span data-ttu-id="7f5e0-383">**SUBNETID** 필드는 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-383">Leave the **SUBNETID** field empty.</span></span>

  <span data-ttu-id="7f5e0-384">SAP Azure Resource Manager 템플릿은 Azure 가상 네트워크 및 서브넷을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-384">The SAP Azure Resource Manager template automatically creates the Azure virtual network and subnet.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-385">또한 동일한 Azure 가상 네트워크 인스턴스에 Active Directory 및 DNS에 대한 하나 이상의 전용 가상 컴퓨터를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-385">You also need to deploy at least one dedicated virtual machine for Active Directory and DNS in the same Azure Virtual Network instance.</span></span> <span data-ttu-id="7f5e0-386">이 템플릿이 이러한 가상 컴퓨터를 만들지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-386">The template doesn't create these virtual machines.</span></span>
>
>


### <a name="prepare-the-infrastructure-for-architectural-template-2"></a><span data-ttu-id="7f5e0-387">아키텍처 템플릿 2에 대한 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="7f5e0-387">Prepare the infrastructure for Architectural Template 2</span></span>

<span data-ttu-id="7f5e0-388">이 Azure Resource Manager 템플릿을 사용하면 SAP에서 SAP 아키텍처 템플릿 2에 필요한 인프라 리소스를 간단히 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-388">You can use this Azure Resource Manager template for SAP to help simplify deployment of required infrastructure resources for SAP Architectural Template 2.</span></span>

<span data-ttu-id="7f5e0-389">이 배포 시나리오를 위한 Azure Resource Manager 템플릿을 가져올 수 있는 위치는 다음과 같습니다</span><span class="sxs-lookup"><span data-stu-id="7f5e0-389">Here's where you can get Azure Resource Manager templates for this deployment scenario:</span></span>

* [<span data-ttu-id="7f5e0-390">Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-390">Azure Marketplace image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [<span data-ttu-id="7f5e0-391">관리 디스크를 사용하는 Azure Marketplace 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-391">Azure Marketplace image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [<span data-ttu-id="7f5e0-392">사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-392">Custom image</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [<span data-ttu-id="7f5e0-393">관리 디스크를 사용하는 사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="7f5e0-393">Custom image using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-the-infrastructure-for-architectural-template-3"></a><span data-ttu-id="7f5e0-394">아키텍처 템플릿 3에 대한 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="7f5e0-394">Prepare the infrastructure for Architectural Template 3</span></span>

<span data-ttu-id="7f5e0-395">인프라를 준비하고 **다중 SID**용 SAP를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-395">You can prepare the infrastructure and configure SAP for **multi-SID**.</span></span> <span data-ttu-id="7f5e0-396">예를 들어 추가 SAP ASCS/SCS 인스턴스를 *기존* 클러스터 구성에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-396">For example, you can add an additional SAP ASCS/SCS instance into an *existing* cluster configuration.</span></span> <span data-ttu-id="7f5e0-397">자세한 내용은 [추가 SAP ASCS/SCS 인스턴스를 기존 클러스터 구성에 구성하여 Azure Resource Manager에서 SAP 다중 SID 구성 만들기][sap-ha-multi-sid-guide]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-397">For more information, see [Configure an additional SAP ASCS/SCS instance into an existing cluster configuration to create an SAP multi-SID configuration in Azure Resource Manager][sap-ha-multi-sid-guide].</span></span>

<span data-ttu-id="7f5e0-398">새 다중 SID 클러스터를 만들려면 [GitHub에 있는 다중 SID 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-398">If you want to create a new multi-SID cluster, you can use the multi-SID [quickstart templates on GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="7f5e0-399">새 다중 SID 클러스터를 만들려면 다음 세 가지 템플릿을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-399">To create a new multi-SID cluster, you need to deploy the following three templates:</span></span>

* [<span data-ttu-id="7f5e0-400">ASCS/SCS 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f5e0-400">ASCS/SCS template</span></span>](#ASCS-SCS-template)
* [<span data-ttu-id="7f5e0-401">데이터베이스 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f5e0-401">Database template</span></span>](#database-template)
* [<span data-ttu-id="7f5e0-402">응용 프로그램 서버 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f5e0-402">Application servers template</span></span>](#application-servers-template)

<span data-ttu-id="7f5e0-403">다음 섹션에는 템플릿에서 제공해야 하는 템플릿과 매개 변수에 대한 자세한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-403">The following sections have more details about the templates and the parameters you need to provide in the templates.</span></span>

#### <span data-ttu-id="7f5e0-404"><a name="ASCS-SCS-template"></a> ASCS/SCS 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f5e0-404"><a name="ASCS-SCS-template"></a> ASCS/SCS template</span></span>

<span data-ttu-id="7f5e0-405">ASCS/SCS 템플릿은 여러 ASCS/SCS 인스턴스를 호스팅하는 Windows 서버 장애 조치(failover) 클러스터를 만드는 데 사용할 수 있는 두 개의 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-405">The ASCS/SCS template deploys two virtual machines that you can use to create a Windows Server failover cluster that hosts multiple ASCS/SCS instances.</span></span>

<span data-ttu-id="7f5e0-406">ASCS/SCS 다중 SID 템플릿을 설정하려면 [ASCS/SCS 다중 SID 템플릿][sap-templates-3-tier-multisid-xscs-marketplace-image] 또는 [관리 디스크를 사용하는 ASCS/SCS 다중 SID 템플릿][sap-templates-3-tier-multisid-xscs-marketplace-image-md]에서 다음 매개 변수 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-406">To set up the ASCS/SCS multi-SID template, in the [ASCS/SCS multi-SID template][sap-templates-3-tier-multisid-xscs-marketplace-image] or [ASCS/SCS multi-SID template using Managed Disks][sap-templates-3-tier-multisid-xscs-marketplace-image-md], enter values for the following parameters:</span></span>

  - <span data-ttu-id="7f5e0-407">**리소스 접두사**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-407">**Resource Prefix**.</span></span>  <span data-ttu-id="7f5e0-408">배포 중에 만들어진 모든 리소스 앞에 붙는 접두사로 사용되는 리소스 접두사를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-408">Set the resource prefix, which is used to prefix all resources that are created during the deployment.</span></span> <span data-ttu-id="7f5e0-409">리소스는 하나의 SAP 시스템에만 속하지 않으므로 리소스의 접두사는 SAP 시스템 하나의 SID가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-409">Because the resources do not belong to only one SAP system, the prefix of the resource is not the SID of one SAP system.</span></span>  <span data-ttu-id="7f5e0-410">접두사는 **3-6자** 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-410">The prefix must be between **three and six characters**.</span></span>
  - <span data-ttu-id="7f5e0-411">**스택 유형**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-411">**Stack Type**.</span></span> <span data-ttu-id="7f5e0-412">SAP 시스템의 스택 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-412">Select the stack type of the SAP system.</span></span> <span data-ttu-id="7f5e0-413">스택 유형에 따라 Azure Load Balancer에는 SAP 시스템당 하나(ABAP 또는 Java 중 하나만) 또는 둘(ABAP 및 Java 각각 하나씩)의 개인 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-413">Depending on the stack type, Azure Load Balancer has one (ABAP or Java only) or two (ABAP+Java) private IP addresses per SAP system.</span></span>
  -  <span data-ttu-id="7f5e0-414">**OS 종류**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-414">**OS Type**.</span></span> <span data-ttu-id="7f5e0-415">가상 컴퓨터의 운영 체제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-415">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="7f5e0-416">**SAP 시스템 수**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-416">**SAP System Count**.</span></span> <span data-ttu-id="7f5e0-417">이 클러스터에 설치하려는 SAP 시스템의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-417">Select the number of SAP systems you want to install in this cluster.</span></span>
  -  <span data-ttu-id="7f5e0-418">**시스템 가용성**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-418">**System Availability**.</span></span> <span data-ttu-id="7f5e0-419">**HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-419">Select **HA**.</span></span>
  -  <span data-ttu-id="7f5e0-420">**관리자 사용자 이름 및 관리자 암호**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-420">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="7f5e0-421">컴퓨터에 로그인하는 데 사용할 수 있는 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-421">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="7f5e0-422">**새 또는 기존 서브넷**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-422">**New Or Existing Subnet**.</span></span> <span data-ttu-id="7f5e0-423">새 가상 네트워크와 서브넷을 만들어야 하는지 또는 기존 서브넷을 사용해야 하는지 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-423">Set whether a new virtual network and subnet should be created, or an existing subnet should be used.</span></span> <span data-ttu-id="7f5e0-424">온-프레미스 네트워크에 연결되어 있는 가상 네트워크가 이미 있는 경우 **기존** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-424">If you already have a virtual network that is connected to your on-premises network, select **existing**.</span></span>
  -  <span data-ttu-id="7f5e0-425">**서브넷 ID**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-425">**Subnet Id**.</span></span> <span data-ttu-id="7f5e0-426">가상 컴퓨터를 연결해야 하는 서브넷의 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-426">Set the ID of the subnet to which the virtual machines should be connected.</span></span> <span data-ttu-id="7f5e0-427">온-프레미스 네트워크에 가상 컴퓨터를 연결할 VPN(가상 사설망) 또는 ExpressRoute 가상 네트워크의 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-427">Select the subnet of your virtual private network (VPN) or ExpressRoute virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="7f5e0-428">ID는 일반적으로 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-428">The ID usually looks like this:</span></span>

   <span data-ttu-id="7f5e0-429">/subscriptions/<*구독 ID*>/resourceGroups/<*리소스 그룹 이름*>/providers/Microsoft.Network/virtualNetworks/<*가상 네트워크 이름*>/subnets/<*서브넷 이름*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-429">/subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*></span></span>

<span data-ttu-id="7f5e0-430">템플릿은 여러 SAP 시스템을 지원하는 하나의 Azure Load Balancer 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-430">The template deploys one Azure Load Balancer instance, which supports multiple SAP systems.</span></span>

- <span data-ttu-id="7f5e0-431">ASCS 인스턴스의 인스턴스 번호는 00, 10, 20...으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-431">The ASCS instances are configured for instance number 00, 10, 20...</span></span>
- <span data-ttu-id="7f5e0-432">SCS 인스턴스의 인스턴스 번호는 01, 11, 21...로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-432">The SCS instances are configured for instance number 01, 11, 21...</span></span>
- <span data-ttu-id="7f5e0-433">ASCS ERS(Enqueue Replication Server)(Linux 전용) 인스턴스의 인스턴스 번호는 02, 12, 22...로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-433">The ASCS Enqueue Replication Server (ERS) (Linux only) instances are configured for instance number 02, 12, 22...</span></span>
- <span data-ttu-id="7f5e0-434">SCS ERS(Linux 전용) 인스턴스의 인스턴스 번호는 03, 13, 23...으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-434">The SCS ERS (Linux only) instances are configured for instance number 03, 13, 23...</span></span>

<span data-ttu-id="7f5e0-435">부하 분산 장치는 하나의(Linux용 2개) VIP, ASCS/SCS용 1x VIP 및 ERS용 1x VIP(Linux 전용)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-435">The load balancer contains 1 (2 for Linux) VIP(s), 1x VIP for ASCS/SCS and 1x VIP for ERS (Linux only).</span></span>

<span data-ttu-id="7f5e0-436">다음 목록은 모든 부하 분산 규칙을 포함하며 여기서 x는 SAP 시스템의 번호입니다(예: 1, 2, 3...).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-436">The following list contains all load balancing rules (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="7f5e0-437">모든 SAP 시스템에 대한 Windows 특정 포트: 445, 5985</span><span class="sxs-lookup"><span data-stu-id="7f5e0-437">Windows-specific ports for every SAP system: 445, 5985</span></span>
- <span data-ttu-id="7f5e0-438">ASCS 포트(x0 인스턴스 번호): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span><span class="sxs-lookup"><span data-stu-id="7f5e0-438">ASCS ports (instance number x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016</span></span>
- <span data-ttu-id="7f5e0-439">SCS 포트(x1 인스턴스 번호): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span><span class="sxs-lookup"><span data-stu-id="7f5e0-439">SCS ports (instance number x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116</span></span>
- <span data-ttu-id="7f5e0-440">Linux의 ASCS ERS 포트(x2 인스턴스 번호): 33x2, 5x213, 5x214, 5x216</span><span class="sxs-lookup"><span data-stu-id="7f5e0-440">ASCS ERS ports on Linux (instance number x2): 33x2, 5x213, 5x214, 5x216</span></span>
- <span data-ttu-id="7f5e0-441">Linux의 SCS ERS 포트(x3 인스턴스 번호): 33x3, 5x313, 5x314, 5x316</span><span class="sxs-lookup"><span data-stu-id="7f5e0-441">SCS ERS ports on Linux (instance number x3): 33x3, 5x313, 5x314, 5x316</span></span>

<span data-ttu-id="7f5e0-442">부하 분산 장치는 다음 프로브 포트를 사용하도록 구성되며 여기서 x는 SAP 시스템의 번호입니다(예: 1, 2, 3...).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-442">The load balancer is configured to use the following probe ports (where x is the number of the SAP system, for example, 1, 2, 3...):</span></span>
- <span data-ttu-id="7f5e0-443">ASCS/SCS 내부 부하 분산 장치 프로브 포트: 620x0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-443">ASCS/SCS internal load balancer probe port: 620x0</span></span>
- <span data-ttu-id="7f5e0-444">ERS 내부 부하 분산 장치 프로브 포트(Linux 전용): 621x2</span><span class="sxs-lookup"><span data-stu-id="7f5e0-444">ERS internal load balancer probe port (Linux only): 621x2</span></span>

#### <span data-ttu-id="7f5e0-445"><a name="database-template"></a> 데이터베이스 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f5e0-445"><a name="database-template"></a> Database template</span></span>

<span data-ttu-id="7f5e0-446">데이터베이스 템플릿은 단일 SAP 시스템에 대한 관계형 데이터베이스 관리 시스템(RDBMS)을 설치하는 데 사용할 수 있는 하나 또는 두 개의 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-446">The database template deploys one or two virtual machines that you can use to install the relational database management system (RDBMS) for one SAP system.</span></span> <span data-ttu-id="7f5e0-447">예를 들어 5개 SAP 시스템에 대해 ASCS/SCS 템플릿을 배포하는 경우 이 템플릿을 5번 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-447">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="7f5e0-448">데이터베이스 다중 SID 템플릿을 설정하려면 [데이터베이스 다중 SID 템플릿][sap-templates-3-tier-multisid-db-marketplace-image] 또는 [관리 디스크를 사용하는 데이터베이스 다중 SID 템플릿][sap-templates-3-tier-multisid-db-marketplace-image-md]에서 다음 매개 변수 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-448">To set up the database multi-SID template, in the [database multi-SID template][sap-templates-3-tier-multisid-db-marketplace-image] or [database multi-SID template using Managed Disks][sap-templates-3-tier-multisid-db-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="7f5e0-449">**SAP 시스템 ID**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-449">**Sap System Id**.</span></span> <span data-ttu-id="7f5e0-450">설치하려는 SAP 시스템의 SAP 시스템 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-450">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="7f5e0-451">이 ID는 배포되는 리소스의 접두사로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-451">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="7f5e0-452">**OS 종류**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-452">**Os Type**.</span></span> <span data-ttu-id="7f5e0-453">가상 컴퓨터의 운영 체제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-453">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="7f5e0-454">**데이터베이스 유형**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-454">**Dbtype**.</span></span> <span data-ttu-id="7f5e0-455">클러스터에 설치하려는 데이터베이스의 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-455">Select the type of the database you want to install on the cluster.</span></span> <span data-ttu-id="7f5e0-456">Microsoft SQL Server를 설치하려는 경우 **SQL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-456">Select **SQL** if you want to install Microsoft SQL Server.</span></span> <span data-ttu-id="7f5e0-457">가상 컴퓨터에 SAP HANA를 설치하려는 경우 **HANA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-457">Select **HANA** if you plan to install SAP HANA on the virtual machines.</span></span> <span data-ttu-id="7f5e0-458">올바른 운영 체제 종류, 즉, SQL에는 **Windows**를 선택하고 HANA에는 Linux 배포를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-458">Make sure to select the correct operating system type: select **Windows** for SQL, and select a Linux distribution for HANA.</span></span> <span data-ttu-id="7f5e0-459">가상 컴퓨터에 연결되는 Azure Load Balancer는 선택한 다음 데이터베이스 유형을 지원하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-459">The Azure Load Balancer that is connected to the virtual machines will be configured to support the selected database type:</span></span>
    * <span data-ttu-id="7f5e0-460">**SQL**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-460">**SQL**.</span></span> <span data-ttu-id="7f5e0-461">부하 분산 장치에서 1433 포트의 부하를 균형 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-461">The load balancer will load-balance port 1433.</span></span> <span data-ttu-id="7f5e0-462">SQL Server Always On 설정에 이 포트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-462">Make sure to use this port for your SQL Server Always On setup.</span></span>
    * <span data-ttu-id="7f5e0-463">**HANA**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-463">**HANA**.</span></span> <span data-ttu-id="7f5e0-464">부하 분산 장치에서 35015 및 35017 포트의 부하를 균형 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-464">The load balancer will load-balance ports 35015 and 35017.</span></span> <span data-ttu-id="7f5e0-465">**50** 인스턴스 번호의 SAP HANA를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-465">Make sure to install SAP HANA with instance number **50**.</span></span>
    <span data-ttu-id="7f5e0-466">부하 분산 장치에서 62550 프로브 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-466">The load balancer will use probe port 62550.</span></span>
  -  <span data-ttu-id="7f5e0-467">**SAP 시스템 크기**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-467">**Sap System Size**.</span></span> <span data-ttu-id="7f5e0-468">새 시스템에서 제공하는 SAP의 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-468">Set the number of SAPS the new system will provide.</span></span> <span data-ttu-id="7f5e0-469">시스템에 필요한 SAP의 양을 모를 경우 SAP 기술 파트너 또는 시스템 통합자에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-469">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="7f5e0-470">**시스템 가용성**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-470">**System Availability**.</span></span> <span data-ttu-id="7f5e0-471">**HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-471">Select **HA**.</span></span>
  -  <span data-ttu-id="7f5e0-472">**관리자 사용자 이름 및 관리자 암호**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-472">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="7f5e0-473">컴퓨터에 로그인하는 데 사용할 수 있는 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-473">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="7f5e0-474">**서브넷 ID**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-474">**Subnet Id**.</span></span> <span data-ttu-id="7f5e0-475">ASCS/SCS 템플릿 배포 중에 사용된 서브넷의 ID 또는 ASCS/SCS 템플릿 배포의 일부로 만든 서브넷의 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-475">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>

#### <span data-ttu-id="7f5e0-476"><a name="application-servers-template"></a> 응용 프로그램 서버 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f5e0-476"><a name="application-servers-template"></a> Application servers template</span></span>

<span data-ttu-id="7f5e0-477">응용 프로그램 서버 템플릿은 하나의 SAP 시스템을 위한 SAP 응용 프로그램 서버 인스턴스로 사용할 수 있는 둘 이상의 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-477">The application servers template deploys two or more virtual machines that can be used as SAP Application Server instances for one SAP system.</span></span> <span data-ttu-id="7f5e0-478">예를 들어 5개 SAP 시스템에 대해 ASCS/SCS 템플릿을 배포하는 경우 이 템플릿을 5번 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-478">For example, if you deploy an ASCS/SCS template for five SAP systems, you need to deploy this template five times.</span></span>

<span data-ttu-id="7f5e0-479">응용 프로그램 서버 다중 SID 템플릿을 설정하려면 [응용 프로그램 서버 다중 SID 템플릿][sap-templates-3-tier-multisid-apps-marketplace-image] 또는 [관리 디스크를 사용하는 응용 프로그램 서버 다중 SID 템플릿][sap-templates-3-tier-multisid-apps-marketplace-image-md]에서 다음 매개 변수 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-479">To set up the application servers multi-SID template, in the [application servers multi-SID template][sap-templates-3-tier-multisid-apps-marketplace-image] or [application servers multi-SID template using Managed Disks][sap-templates-3-tier-multisid-apps-marketplace-image-md], enter values for the following parameters:</span></span>

  -  <span data-ttu-id="7f5e0-480">**SAP 시스템 ID**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-480">**Sap System Id**.</span></span> <span data-ttu-id="7f5e0-481">설치하려는 SAP 시스템의 SAP 시스템 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-481">Enter the SAP system ID of the SAP system you want to install.</span></span> <span data-ttu-id="7f5e0-482">이 ID는 배포되는 리소스의 접두사로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-482">The ID will be used as a prefix for the resources that are deployed.</span></span>
  -  <span data-ttu-id="7f5e0-483">**OS 종류**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-483">**Os Type**.</span></span> <span data-ttu-id="7f5e0-484">가상 컴퓨터의 운영 체제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-484">Select the operating system of the virtual machines.</span></span>
  -  <span data-ttu-id="7f5e0-485">**SAP 시스템 크기**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-485">**Sap System Size**.</span></span> <span data-ttu-id="7f5e0-486">새 시스템에서 제공하는 SAP의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-486">The number of SAPS the new system will provide.</span></span> <span data-ttu-id="7f5e0-487">시스템에 필요한 SAP의 양을 모를 경우 SAP 기술 파트너 또는 시스템 통합자에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-487">If you are not sure how many SAPS the system will require, ask your SAP Technology Partner or System Integrator.</span></span>
  -  <span data-ttu-id="7f5e0-488">**시스템 가용성**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-488">**System Availability**.</span></span> <span data-ttu-id="7f5e0-489">**HA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-489">Select **HA**.</span></span>
  -  <span data-ttu-id="7f5e0-490">**관리자 사용자 이름 및 관리자 암호**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-490">**Admin Username and Admin Password**.</span></span> <span data-ttu-id="7f5e0-491">컴퓨터에 로그인하는 데 사용할 수 있는 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-491">Create a new user that can be used to sign in to the machine.</span></span>
  -  <span data-ttu-id="7f5e0-492">**서브넷 ID**.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-492">**Subnet Id**.</span></span> <span data-ttu-id="7f5e0-493">ASCS/SCS 템플릿 배포 중에 사용된 서브넷의 ID 또는 ASCS/SCS 템플릿 배포의 일부로 만든 서브넷의 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-493">Enter the ID of the subnet that you used during the deployment of the ASCS/SCS template, or the ID of the subnet that was created as part of the ASCS/SCS template deployment.</span></span>


### <span data-ttu-id="7f5e0-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="7f5e0-494"><a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure virtual network</span></span>
<span data-ttu-id="7f5e0-495">이 예제에서 Azure 가상 네트워크의 주소 공간은 10.0.0.0/16입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-495">In our example, the address space of the Azure virtual network is 10.0.0.0/16.</span></span> <span data-ttu-id="7f5e0-496">**Subnet**이라는 서브넷이 하나 있으며 주소 범위는 10.0.0.0/24입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-496">There is one subnet called **Subnet**, with an address range of 10.0.0.0/24.</span></span> <span data-ttu-id="7f5e0-497">모든 가상 컴퓨터와 내부 부하 분산 장치는 이 가상 네트워크에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-497">All virtual machines and internal load balancers are deployed in this virtual network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f5e0-498">게스트 운영 체제 내의 네트워크 설정은 변경하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-498">Don't make any changes to the network settings inside the guest operating system.</span></span> <span data-ttu-id="7f5e0-499">여기에는 IP 주소, DNS 서버 및 서브넷이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-499">This includes IP addresses, DNS servers, and subnet.</span></span> <span data-ttu-id="7f5e0-500">Azure에서 모든 네트워크 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-500">Configure all your network settings in Azure.</span></span> <span data-ttu-id="7f5e0-501">DHCP(동적 호스트 구성 프로토콜) 서비스가 사용자 설정을 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-501">The Dynamic Host Configuration Protocol (DHCP) service propagates your settings.</span></span>
>
>

### <span data-ttu-id="7f5e0-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP 주소</span><span class="sxs-lookup"><span data-stu-id="7f5e0-502"><a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP addresses</span></span>

<span data-ttu-id="7f5e0-503">필요한 DNS IP 주소를 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-503">To set the required DNS IP addresses, do the following steps.</span></span>

1.  <span data-ttu-id="7f5e0-504">Azure Portal의 **DNS 서버** 블레이드에서 가상 네트워크 **DNS 서버** 옵션이 **사용자 지정 DNS**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-504">In the Azure portal, on the **DNS servers** blade, make sure that your virtual network **DNS servers** option is set to **Custom DNS**.</span></span>
2.  <span data-ttu-id="7f5e0-505">사용 중인 네트워크의 종류에 따라 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-505">Select your settings based on the type of network you have.</span></span> <span data-ttu-id="7f5e0-506">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-506">For more information, see the following resources:</span></span>
    * <span data-ttu-id="7f5e0-507">[회사 네트워크 연결(크로스-프레미스)][planning-guide-2.2]: 온-프레미스 DNS 서버의 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-507">[Corporate network connectivity (cross-premises)][planning-guide-2.2]: Add the IP addresses of the on-premises DNS servers.</span></span>  
    <span data-ttu-id="7f5e0-508">Azure에서 실행되는 가상 컴퓨터로 온-프레미스 DNS 서버를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-508">You can extend on-premises DNS servers to the virtual machines that are running in Azure.</span></span> <span data-ttu-id="7f5e0-509">이 시나리오에서는 DNS 서비스를 실행하는 Azure Virtual Machines의 IP 주소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-509">In that scenario, you can add the IP addresses of the Azure virtual machines on which you run the DNS service.</span></span>
    * <span data-ttu-id="7f5e0-510">[클라우드 전용 배포][planning-guide-2.1]: DNS 서버 역할을 하는 동일한 Virtual Network 인스턴스에 추가 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-510">[Cloud-only deployment][planning-guide-2.1]: Deploy an additional virtual machine in the same Virtual Network instance that serves as a DNS server.</span></span> <span data-ttu-id="7f5e0-511">DNS 서비스를 실행하도록 설정한 Azure Virtual Machines의 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-511">Add the IP addresses of the Azure virtual machines that you've set up to run DNS service.</span></span>

    ![그림 12: Azure Virtual Network를 위한 DNS 서버 구성][sap-ha-guide-figure-3001]

    <span data-ttu-id="7f5e0-513">_**그림 12:** Azure Virtual Network를 위한 DNS 서버 구성_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-513">_**Figure 12:** Configure DNS servers for Azure Virtual Network_</span></span>

  > [!NOTE]
  > <span data-ttu-id="7f5e0-514">DNS 서버의 IP 주소를 변경하는 경우 변경 내용을 적용하고 새 DNS 서버를 전파하기 위해 Azure Virtual Machines를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-514">If you change the IP addresses of the DNS servers, you need to restart the Azure virtual machines to apply the change and propagate the new DNS servers.</span></span>
  >
  >

<span data-ttu-id="7f5e0-515">이 예제에서는 다음 Windows 가상 컴퓨터에서 DNS 서비스가 설치되고 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-515">In our example, the DNS service is installed and configured on these Windows virtual machines:</span></span>

| <span data-ttu-id="7f5e0-516">가상 컴퓨터 역할</span><span class="sxs-lookup"><span data-stu-id="7f5e0-516">Virtual machine role</span></span> | <span data-ttu-id="7f5e0-517">가상 컴퓨터 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-517">Virtual machine host name</span></span> | <span data-ttu-id="7f5e0-518">네트워크 카드 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-518">Network card name</span></span> | <span data-ttu-id="7f5e0-519">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7f5e0-519">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7f5e0-520">첫 번째 DNS 서버</span><span class="sxs-lookup"><span data-stu-id="7f5e0-520">First DNS server</span></span> |<span data-ttu-id="7f5e0-521">domcontr-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-521">domcontr-0</span></span> |<span data-ttu-id="7f5e0-522">pr1-nic-domcontr-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-522">pr1-nic-domcontr-0</span></span> |<span data-ttu-id="7f5e0-523">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="7f5e0-523">10.0.0.10</span></span> |
| <span data-ttu-id="7f5e0-524">두 번째 DNS 서버</span><span class="sxs-lookup"><span data-stu-id="7f5e0-524">Second DNS server</span></span> |<span data-ttu-id="7f5e0-525">domcontr-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-525">domcontr-1</span></span> |<span data-ttu-id="7f5e0-526">pr1-nic-domcontr-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-526">pr1-nic-domcontr-1</span></span> |<span data-ttu-id="7f5e0-527">10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="7f5e0-527">10.0.0.11</span></span> |

### <span data-ttu-id="7f5e0-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> SAP ASCS/SCS 클러스터형 인스턴스 및 DBMS 클러스터형 인스턴스의 호스트 이름 및 고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7f5e0-528"><a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a> Host names and static IP addresses for the SAP ASCS/SCS clustered instance and DBMS clustered instance</span></span>

<span data-ttu-id="7f5e0-529">온-프레미스 배포에 대해 다음의 예약된 호스트 이름 및 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-529">For on-premises deployment, you need these reserved host names and IP addresses:</span></span>

| <span data-ttu-id="7f5e0-530">가상 호스트 이름 역할</span><span class="sxs-lookup"><span data-stu-id="7f5e0-530">Virtual host name role</span></span> | <span data-ttu-id="7f5e0-531">가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-531">Virtual host name</span></span> | <span data-ttu-id="7f5e0-532">가상 고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7f5e0-532">Virtual static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f5e0-533">SAP ASCS/SCS 첫 번째 클러스터 가상 호스트 이름(클러스터 관리용)</span><span class="sxs-lookup"><span data-stu-id="7f5e0-533">SAP ASCS/SCS first cluster virtual host name (for cluster management)</span></span> |<span data-ttu-id="7f5e0-534">pr1-ascs-vir</span><span class="sxs-lookup"><span data-stu-id="7f5e0-534">pr1-ascs-vir</span></span> |<span data-ttu-id="7f5e0-535">10.0.0.42</span><span class="sxs-lookup"><span data-stu-id="7f5e0-535">10.0.0.42</span></span> |
| <span data-ttu-id="7f5e0-536">SAP ASCS/SCS 인스턴스 가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-536">SAP ASCS/SCS instance virtual host name</span></span> |<span data-ttu-id="7f5e0-537">pr1-ascs-sap</span><span class="sxs-lookup"><span data-stu-id="7f5e0-537">pr1-ascs-sap</span></span> |<span data-ttu-id="7f5e0-538">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="7f5e0-538">10.0.0.43</span></span> |
| <span data-ttu-id="7f5e0-539">SAP DBMS 두 번째 클러스터 가상 호스트 이름(클러스터 관리용)</span><span class="sxs-lookup"><span data-stu-id="7f5e0-539">SAP DBMS second cluster virtual host name (cluster management)</span></span> |<span data-ttu-id="7f5e0-540">pr1-dbms-vir</span><span class="sxs-lookup"><span data-stu-id="7f5e0-540">pr1-dbms-vir</span></span> |<span data-ttu-id="7f5e0-541">10.0.0.32</span><span class="sxs-lookup"><span data-stu-id="7f5e0-541">10.0.0.32</span></span> |

<span data-ttu-id="7f5e0-542">클러스터를 만들 때 만들 가상 호스트 이름 **pr1-ascs-vir** 및 **pr1-dbms-vir**클러스터 자체를 관리하는 연결된 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-542">When you create the cluster, create the virtual host names **pr1-ascs-vir** and **pr1-dbms-vir** and the associated IP addresses that manage the cluster itself.</span></span> <span data-ttu-id="7f5e0-543">이 작업을 수행하는 방법에 대한 정보는 [클러스터 구성에서 클러스터 노드 수집][sap-ha-guide-8.12.1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-543">For information about how to do this, see [Collect cluster nodes in a cluster configuration][sap-ha-guide-8.12.1].</span></span>

<span data-ttu-id="7f5e0-544">DNS 서버에서 다른 두 가상 호스트 이름 **pr1 ascs sap** 및 **pr1 dbms sap**와 연결된 IP 주소는 수동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-544">You can manually create the other two virtual host names, **pr1-ascs-sap** and **pr1-dbms-sap**, and the associated IP addresses, on the DNS server.</span></span> <span data-ttu-id="7f5e0-545">클러스터형 SAP ASCS/SCS 인스턴스 및 클러스터형 DBMS 인스턴스는 이러한 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-545">The clustered SAP ASCS/SCS instance and the clustered DBMS instance use these resources.</span></span> <span data-ttu-id="7f5e0-546">이 작업을 수행하는 방법에 대한 정보는 [클러스터형 SAP ASCS/SCS 인스턴스의 가상 호스트 이름 만들기][sap-ha-guide-9.1.1]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-546">For information about how to do this, see [Create a virtual host name for a clustered SAP ASCS/SCS instance][sap-ha-guide-9.1.1].</span></span>

### <span data-ttu-id="7f5e0-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> SAP 가상 컴퓨터에 대한 고정 IP 주소 설정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-547"><a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a> Set static IP addresses for the SAP virtual machines</span></span>
<span data-ttu-id="7f5e0-548">클러스터에서 사용할 가상 컴퓨터를 배포한 후 모든 가상 컴퓨터에 대해 고정 IP 주소를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-548">After you deploy the virtual machines to use in your cluster, you need to set static IP addresses for all virtual machines.</span></span> <span data-ttu-id="7f5e0-549">이 작업은 게스트 운영 체제가 아니라 Azure Virtual Network 구성에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-549">Do this in the Azure Virtual Network configuration, and not in the guest operating system.</span></span>

1.  <span data-ttu-id="7f5e0-550">Azure Portal에서 **리소스 그룹** > **네트워크 카드** > **설정** > **IP 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-550">In the Azure portal, select **Resource Group** > **Network Card** > **Settings** > **IP Address**.</span></span>
2.  <span data-ttu-id="7f5e0-551">**IP 주소** 블레이드의 **할당** 아래에서 **고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-551">On the **IP addresses** blade, under **Assignment**, select **Static**.</span></span> <span data-ttu-id="7f5e0-552">**IP 주소** 상자에 사용할 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-552">In the **IP address** box, enter the IP address that you want to use.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7f5e0-553">네트워크 카드의 IP 주소를 변경하는 경우 Azure Virtual Machines를 다시 시작하여 변경 내용을 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-553">If you change the IP address of the network card, you need to restart the Azure virtual machines to apply the change.</span></span>  
  >
  >

  ![그림 13: 각 가상 컴퓨터의 네트워크 카드에 대한 고정 IP 주소 설정][sap-ha-guide-figure-3002]

  <span data-ttu-id="7f5e0-555">_**그림 13:** 각 가상 컴퓨터의 네트워크 카드에 대한 고정 IP 주소 설정_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-555">_**Figure 13:** Set static IP addresses for the network card of each virtual machine_</span></span>

  <span data-ttu-id="7f5e0-556">모든 네트워크 인터페이스, 즉 Active Directory/DNS 서비스에 사용하려는 가상 컴퓨터를 비롯한 모든 가상 컴퓨터에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-556">Repeat this step for all network interfaces, that is, for all virtual machines, including virtual machines that you want to use for your Active Directory/DNS service.</span></span>

<span data-ttu-id="7f5e0-557">예제에서는 다음 가상 컴퓨터 및 고정 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-557">In our example, we have these virtual machines and static IP addresses:</span></span>

| <span data-ttu-id="7f5e0-558">가상 컴퓨터 역할</span><span class="sxs-lookup"><span data-stu-id="7f5e0-558">Virtual machine role</span></span> | <span data-ttu-id="7f5e0-559">가상 컴퓨터 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-559">Virtual machine host name</span></span> | <span data-ttu-id="7f5e0-560">네트워크 카드 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-560">Network card name</span></span> | <span data-ttu-id="7f5e0-561">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7f5e0-561">Static IP address</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7f5e0-562">첫 번째 SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-562">First SAP Application Server instance</span></span> |<span data-ttu-id="7f5e0-563">pr1-di-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-563">pr1-di-0</span></span> |<span data-ttu-id="7f5e0-564">pr1-nic-di-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-564">pr1-nic-di-0</span></span> |<span data-ttu-id="7f5e0-565">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="7f5e0-565">10.0.0.50</span></span> |
| <span data-ttu-id="7f5e0-566">두 번째 SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-566">Second SAP Application Server instance</span></span> |<span data-ttu-id="7f5e0-567">pr1-di-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-567">pr1-di-1</span></span> |<span data-ttu-id="7f5e0-568">pr1-nic-di-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-568">pr1-nic-di-1</span></span> |<span data-ttu-id="7f5e0-569">10.0.0.51</span><span class="sxs-lookup"><span data-stu-id="7f5e0-569">10.0.0.51</span></span> |
| <span data-ttu-id="7f5e0-570">...</span><span class="sxs-lookup"><span data-stu-id="7f5e0-570">...</span></span> |<span data-ttu-id="7f5e0-571">...</span><span class="sxs-lookup"><span data-stu-id="7f5e0-571">...</span></span> |<span data-ttu-id="7f5e0-572">...</span><span class="sxs-lookup"><span data-stu-id="7f5e0-572">...</span></span> |<span data-ttu-id="7f5e0-573">...</span><span class="sxs-lookup"><span data-stu-id="7f5e0-573">...</span></span> |
| <span data-ttu-id="7f5e0-574">마지막 SAP 응용 프로그램 서버 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-574">Last SAP Application Server instance</span></span> |<span data-ttu-id="7f5e0-575">pr1-di-5</span><span class="sxs-lookup"><span data-stu-id="7f5e0-575">pr1-di-5</span></span> |<span data-ttu-id="7f5e0-576">pr1-nic-di-5</span><span class="sxs-lookup"><span data-stu-id="7f5e0-576">pr1-nic-di-5</span></span> |<span data-ttu-id="7f5e0-577">10.0.0.55</span><span class="sxs-lookup"><span data-stu-id="7f5e0-577">10.0.0.55</span></span> |
| <span data-ttu-id="7f5e0-578">ASCS/SCS 인스턴스의 첫 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="7f5e0-578">First cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="7f5e0-579">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-579">pr1-ascs-0</span></span> |<span data-ttu-id="7f5e0-580">pr1-nic-ascs-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-580">pr1-nic-ascs-0</span></span> |<span data-ttu-id="7f5e0-581">10.0.0.40</span><span class="sxs-lookup"><span data-stu-id="7f5e0-581">10.0.0.40</span></span> |
| <span data-ttu-id="7f5e0-582">ASCS/SCS 인스턴스의 두 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="7f5e0-582">Second cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="7f5e0-583">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-583">pr1-ascs-1</span></span> |<span data-ttu-id="7f5e0-584">pr1-nic-ascs-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-584">pr1-nic-ascs-1</span></span> |<span data-ttu-id="7f5e0-585">10.0.0.41</span><span class="sxs-lookup"><span data-stu-id="7f5e0-585">10.0.0.41</span></span> |
| <span data-ttu-id="7f5e0-586">DBMS 인스턴스의 첫 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="7f5e0-586">First cluster node for DBMS instance</span></span> |<span data-ttu-id="7f5e0-587">pr1-db-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-587">pr1-db-0</span></span> |<span data-ttu-id="7f5e0-588">pr1-nic-db-0</span><span class="sxs-lookup"><span data-stu-id="7f5e0-588">pr1-nic-db-0</span></span> |<span data-ttu-id="7f5e0-589">10.0.0.30</span><span class="sxs-lookup"><span data-stu-id="7f5e0-589">10.0.0.30</span></span> |
| <span data-ttu-id="7f5e0-590">DBMS 인스턴스의 두 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="7f5e0-590">Second cluster node for DBMS instance</span></span> |<span data-ttu-id="7f5e0-591">pr1-db-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-591">pr1-db-1</span></span> |<span data-ttu-id="7f5e0-592">pr1-nic-db-1</span><span class="sxs-lookup"><span data-stu-id="7f5e0-592">pr1-nic-db-1</span></span> |<span data-ttu-id="7f5e0-593">10.0.0.31</span><span class="sxs-lookup"><span data-stu-id="7f5e0-593">10.0.0.31</span></span> |

### <span data-ttu-id="7f5e0-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Azure 내부 부하 분산 장치의 고정 IP 주소 설정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-594"><a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a> Set a static IP address for the Azure internal load balancer</span></span>

<span data-ttu-id="7f5e0-595">SAP Azure Resource Manager 템플릿은 SAP ASCS/SCS 인스턴스 클러스터 및 DBMS 클러스터에 사용되는 Azure 내부 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-595">The SAP Azure Resource Manager template creates an Azure internal load balancer that is used for the SAP ASCS/SCS instance cluster and the DBMS cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f5e0-596">SAP ASCS/SCS의 가상 호스트 이름 IP 주소는 SAP ASCS/SCS 내부 부하 분산 장치 **pr1-lb-ascs**의 IP 주소와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-596">The IP address of the virtual host name of the SAP ASCS/SCS is the same as the IP address of the SAP ASCS/SCS internal load balancer: **pr1-lb-ascs**.</span></span>
> <span data-ttu-id="7f5e0-597">DBMS의 가상 호스트 이름 IP 주소는 DBMS 내부 부하 분산 장치 **pr1-lb-dbms**의 IP 주소와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-597">The IP address of the virtual name of the DBMS is the same as the IP address of the DBMS internal load balancer: **pr1-lb-dbms**.</span></span>
>
>

<span data-ttu-id="7f5e0-598">Azure 내부 부하 분산 장치의 고정 IP 주소를 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-598">To set a static IP address for the Azure internal load balancer:</span></span>

1.  <span data-ttu-id="7f5e0-599">초기 배포는 내부 부하 분산 장치 IP 주소를 **동적**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-599">The initial deployment sets the internal load balancer IP address to **Dynamic**.</span></span> <span data-ttu-id="7f5e0-600">Azure Portal에서 **IP 주소** 블레이드의 **할당** 아래에서 **고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-600">In the Azure portal, on the **IP addresses** blade, under **Assignment**, select **Static**.</span></span>
2.  <span data-ttu-id="7f5e0-601">내부 부하 분산 장치 **pr1-lb-ascs**의 IP 주소를 SAP ASCS/SCS 인스턴스의 가상 호스트 이름 IP 주소로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-601">Set the IP address of the internal load balancer **pr1-lb-ascs** to the IP address of the virtual host name of the SAP ASCS/SCS instance.</span></span>
3.  <span data-ttu-id="7f5e0-602">내부 부하 분산 장치 **pr1-lb-dbms**의 IP 주소를 DBMS 인스턴스의 가상 호스트 이름 IP 주소로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-602">Set the IP address of the internal load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

  ![그림 14: SAP ASCS/SCS 인스턴스의 내부 부하 분산 장치에 대한 고정 IP 주소 설정][sap-ha-guide-figure-3003]

  <span data-ttu-id="7f5e0-604">_**그림 14:** SAP ASCS/SCS 인스턴스의 내부 부하 분산 장치에 대한 고정 IP 주소 설정_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-604">_**Figure 14:** Set static IP addresses for the internal load balancer for the SAP ASCS/SCS instance_</span></span>

<span data-ttu-id="7f5e0-605">예제에서는 다음과 같은 고정 IP 주소를 가진 두 개의 Azure 내부 부하 분산 장치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-605">In our example, we have two Azure internal load balancers that have these static IP addresses:</span></span>

| <span data-ttu-id="7f5e0-606">Azure 내부 부하 분산 장치 역할</span><span class="sxs-lookup"><span data-stu-id="7f5e0-606">Azure internal load balancer role</span></span> | <span data-ttu-id="7f5e0-607">Azure 내부 부하 분산 장치 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-607">Azure internal load balancer name</span></span> | <span data-ttu-id="7f5e0-608">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="7f5e0-608">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f5e0-609">SAP ASCS/SCS 인스턴스 내부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-609">SAP ASCS/SCS instance internal load balancer</span></span> |<span data-ttu-id="7f5e0-610">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="7f5e0-610">pr1-lb-ascs</span></span> |<span data-ttu-id="7f5e0-611">10.0.0.43</span><span class="sxs-lookup"><span data-stu-id="7f5e0-611">10.0.0.43</span></span> |
| <span data-ttu-id="7f5e0-612">SAP DBMS 내부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-612">SAP DBMS internal load balancer</span></span> |<span data-ttu-id="7f5e0-613">pr1-lb-dbms</span><span class="sxs-lookup"><span data-stu-id="7f5e0-613">pr1-lb-dbms</span></span> |<span data-ttu-id="7f5e0-614">10.0.0.33</span><span class="sxs-lookup"><span data-stu-id="7f5e0-614">10.0.0.33</span></span> |


### <span data-ttu-id="7f5e0-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Azure 내부 부하 분산 장치에 대한 기본 ASCS/SCS 부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="7f5e0-615"><a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a> Default ASCS/SCS load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="7f5e0-616">SAP Azure Resource Manager 템플릿은 다음에 대해 필요한 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-616">The SAP Azure Resource Manager template creates the ports you need:</span></span>
* <span data-ttu-id="7f5e0-617">기본 인스턴스 번호가 **00**인 ABAP ASCS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-617">An ABAP ASCS instance, with the default instance number **00**</span></span>
* <span data-ttu-id="7f5e0-618">기본 인스턴스 번호가 **01**인 Java SCS 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7f5e0-618">A Java SCS instance, with the default instance number **01**</span></span>

<span data-ttu-id="7f5e0-619">SAP ASCS/SCS 인스턴스를 설치하면 ABAP ASCS 인스턴스에 대해 기본 인스턴스 번호 **00**을, Java SCS 인스턴스에 대해 기본 인스턴스 번호 **01**을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-619">When you install your SAP ASCS/SCS instance, you must use the default instance number **00** for your ABAP ASCS instance and the default instance number **01** for your Java SCS instance.</span></span>

<span data-ttu-id="7f5e0-620">다음으로 SAP NetWeaver 포트에 대한 필수 내부 부하 분산 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-620">Next, create required internal load balancing endpoints for the SAP NetWeaver ports.</span></span>

<span data-ttu-id="7f5e0-621">필수 내부 부하 분산 끝점을 만들려면 먼저 SAP NetWeaver ABAP ASCS 포트에 대한 다음과 같은 부하 분산 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-621">To create required internal load balancing endpoints, first, create these load balancing endpoints for the SAP NetWeaver ABAP ASCS ports:</span></span>

| <span data-ttu-id="7f5e0-622">서비스/부하 분산 규칙 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-622">Service/load balancing rule name</span></span> | <span data-ttu-id="7f5e0-623">기본 포트 번호</span><span class="sxs-lookup"><span data-stu-id="7f5e0-623">Default port numbers</span></span> | <span data-ttu-id="7f5e0-624">(인스턴스 번호가 00인 ASCS 인스턴스)(ERS가 10)에 대한 구체적인 포트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-624">Concrete ports for (ASCS instance with instance number 00) (ERS with 10)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f5e0-625">서버를 큐에 넣기/ *lbrule3200*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-625">Enqueue Server / *lbrule3200*</span></span> |<span data-ttu-id="7f5e0-626">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-626">32<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-627">3200</span><span class="sxs-lookup"><span data-stu-id="7f5e0-627">3200</span></span> |
| <span data-ttu-id="7f5e0-628">ABAP 메시지 서버/ *lbrule3600*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-628">ABAP Message Server / *lbrule3600*</span></span> |<span data-ttu-id="7f5e0-629">36<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-629">36<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-630">3600</span><span class="sxs-lookup"><span data-stu-id="7f5e0-630">3600</span></span> |
| <span data-ttu-id="7f5e0-631">내부 ABAP 메시지/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-631">Internal ABAP Message / *lbrule3900*</span></span> |<span data-ttu-id="7f5e0-632">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-632">39<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-633">3900</span><span class="sxs-lookup"><span data-stu-id="7f5e0-633">3900</span></span> |
| <span data-ttu-id="7f5e0-634">메시지 서버 HTTP/ *Lbrule8100*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-634">Message Server HTTP / *Lbrule8100*</span></span> |<span data-ttu-id="7f5e0-635">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-635">81<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-636">8100</span><span class="sxs-lookup"><span data-stu-id="7f5e0-636">8100</span></span> |
| <span data-ttu-id="7f5e0-637">SAP 시작 서비스 ASCS HTTP/ *Lbrule50013*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-637">SAP Start Service ASCS HTTP / *Lbrule50013*</span></span> |<span data-ttu-id="7f5e0-638">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="7f5e0-638">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7f5e0-639">50013</span><span class="sxs-lookup"><span data-stu-id="7f5e0-639">50013</span></span> |
| <span data-ttu-id="7f5e0-640">SAP 시작 서비스 ASCS HTTP/ *Lbrule50014*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-640">SAP Start Service ASCS HTTPS / *Lbrule50014*</span></span> |<span data-ttu-id="7f5e0-641">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="7f5e0-641">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7f5e0-642">50014</span><span class="sxs-lookup"><span data-stu-id="7f5e0-642">50014</span></span> |
| <span data-ttu-id="7f5e0-643">복제를 큐에 넣기/ *Lbrule50016*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-643">Enqueue Replication / *Lbrule50016*</span></span> |<span data-ttu-id="7f5e0-644">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="7f5e0-644">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="7f5e0-645">50016</span><span class="sxs-lookup"><span data-stu-id="7f5e0-645">50016</span></span> |
| <span data-ttu-id="7f5e0-646">SAP 시작 서비스 ERS HTTP/ *Lbrule51013*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-646">SAP Start Service ERS HTTP *Lbrule51013*</span></span> |<span data-ttu-id="7f5e0-647">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="7f5e0-647">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7f5e0-648">51013</span><span class="sxs-lookup"><span data-stu-id="7f5e0-648">51013</span></span> |
| <span data-ttu-id="7f5e0-649">SAP 시작 서비스 ERS HTTP *Lbrule51014*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-649">SAP Start Service ERS HTTP *Lbrule51014*</span></span> |<span data-ttu-id="7f5e0-650">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="7f5e0-650">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7f5e0-651">51014</span><span class="sxs-lookup"><span data-stu-id="7f5e0-651">51014</span></span> |
| <span data-ttu-id="7f5e0-652">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-652">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="7f5e0-653">5985</span><span class="sxs-lookup"><span data-stu-id="7f5e0-653">5985</span></span> |
| <span data-ttu-id="7f5e0-654">파일 공유 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-654">File Share *Lbrule445*</span></span> | |<span data-ttu-id="7f5e0-655">445</span><span class="sxs-lookup"><span data-stu-id="7f5e0-655">445</span></span> |

<span data-ttu-id="7f5e0-656">_**표 1:** SAP NetWeaver ABAP ASCS 인스턴스의 포트 번호_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-656">_**Table 1:** Port numbers of the SAP NetWeaver ABAP ASCS instances_</span></span>

<span data-ttu-id="7f5e0-657">그런 후 SAP NetWeaver Java SCS 포트에 대한 다음과 같은 부하 분산 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-657">Then, create these load balancing endpoints for the SAP NetWeaver Java SCS ports:</span></span>

| <span data-ttu-id="7f5e0-658">서비스/부하 분산 규칙 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-658">Service/load balancing rule name</span></span> | <span data-ttu-id="7f5e0-659">기본 포트 번호</span><span class="sxs-lookup"><span data-stu-id="7f5e0-659">Default port numbers</span></span> | <span data-ttu-id="7f5e0-660">(인스턴스 번호가 01인 SCS 인스턴스)(ERS가 11)에 대한 구체적인 포트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-660">Concrete ports for (SCS instance with instance number 01) (ERS with 11)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f5e0-661">서버를 큐에 넣기/ *lbrule3201*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-661">Enqueue Server / *lbrule3201*</span></span> |<span data-ttu-id="7f5e0-662">32<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-662">32<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-663">3201</span><span class="sxs-lookup"><span data-stu-id="7f5e0-663">3201</span></span> |
| <span data-ttu-id="7f5e0-664">게이트웨이 서버/ *lbrule3301*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-664">Gateway Server / *lbrule3301*</span></span> |<span data-ttu-id="7f5e0-665">33<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-665">33<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-666">3301</span><span class="sxs-lookup"><span data-stu-id="7f5e0-666">3301</span></span> |
| <span data-ttu-id="7f5e0-667">Java 메시지 서버/ *lbrule3900*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-667">Java Message Server / *lbrule3900*</span></span> |<span data-ttu-id="7f5e0-668">39<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-668">39<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-669">3901</span><span class="sxs-lookup"><span data-stu-id="7f5e0-669">3901</span></span> |
| <span data-ttu-id="7f5e0-670">메시지 서버 HTTP/ *Lbrule8101*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-670">Message Server HTTP / *Lbrule8101*</span></span> |<span data-ttu-id="7f5e0-671">81<*InstanceNumber*></span><span class="sxs-lookup"><span data-stu-id="7f5e0-671">81<*InstanceNumber*></span></span> |<span data-ttu-id="7f5e0-672">8101</span><span class="sxs-lookup"><span data-stu-id="7f5e0-672">8101</span></span> |
| <span data-ttu-id="7f5e0-673">SAP 시작 서비스 SCS HTTP/ *Lbrule50113*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-673">SAP Start Service SCS HTTP / *Lbrule50113*</span></span> |<span data-ttu-id="7f5e0-674">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="7f5e0-674">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7f5e0-675">50113</span><span class="sxs-lookup"><span data-stu-id="7f5e0-675">50113</span></span> |
| <span data-ttu-id="7f5e0-676">SAP 시작 서비스 SCS HTTP/ *Lbrule50114*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-676">SAP Start Service SCS HTTPS / *Lbrule50114*</span></span> |<span data-ttu-id="7f5e0-677">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="7f5e0-677">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7f5e0-678">50114</span><span class="sxs-lookup"><span data-stu-id="7f5e0-678">50114</span></span> |
| <span data-ttu-id="7f5e0-679">복제를 큐에 넣기/ *Lbrule50116*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-679">Enqueue Replication / *Lbrule50116*</span></span> |<span data-ttu-id="7f5e0-680">5<*InstanceNumber*>16</span><span class="sxs-lookup"><span data-stu-id="7f5e0-680">5<*InstanceNumber*>16</span></span> |<span data-ttu-id="7f5e0-681">50116</span><span class="sxs-lookup"><span data-stu-id="7f5e0-681">50116</span></span> |
| <span data-ttu-id="7f5e0-682">SAP 시작 서비스 ERS HTTP *Lbrule51113*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-682">SAP Start Service ERS HTTP *Lbrule51113*</span></span> |<span data-ttu-id="7f5e0-683">5<*InstanceNumber*>13</span><span class="sxs-lookup"><span data-stu-id="7f5e0-683">5<*InstanceNumber*>13</span></span> |<span data-ttu-id="7f5e0-684">51113</span><span class="sxs-lookup"><span data-stu-id="7f5e0-684">51113</span></span> |
| <span data-ttu-id="7f5e0-685">SAP 시작 서비스 ERS HTTP *Lbrule51114*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-685">SAP Start Service ERS HTTP *Lbrule51114*</span></span> |<span data-ttu-id="7f5e0-686">5<*InstanceNumber*>14</span><span class="sxs-lookup"><span data-stu-id="7f5e0-686">5<*InstanceNumber*>14</span></span> |<span data-ttu-id="7f5e0-687">51114</span><span class="sxs-lookup"><span data-stu-id="7f5e0-687">51114</span></span> |
| <span data-ttu-id="7f5e0-688">Win RM *Lbrule5985*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-688">Win RM *Lbrule5985*</span></span> | |<span data-ttu-id="7f5e0-689">5985</span><span class="sxs-lookup"><span data-stu-id="7f5e0-689">5985</span></span> |
| <span data-ttu-id="7f5e0-690">파일 공유 *Lbrule445*</span><span class="sxs-lookup"><span data-stu-id="7f5e0-690">File Share *Lbrule445*</span></span> | |<span data-ttu-id="7f5e0-691">445</span><span class="sxs-lookup"><span data-stu-id="7f5e0-691">445</span></span> |

<span data-ttu-id="7f5e0-692">_**표 2:** SAP NetWeaver Java SCS 인스턴스의 포트 번호_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-692">_**Table 2:** Port numbers of the SAP NetWeaver Java SCS instances_</span></span>

![그림 15: Azure 내부 부하 분산 장치의 기본 ASCS/SCS 부하 분산 규칙][sap-ha-guide-figure-3004]

<span data-ttu-id="7f5e0-694">_**그림 15:** Azure 내부 부하 분산 장치의 기본 ASCS/SCS 부하 분산 규칙_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-694">_**Figure 15:** Default ASCS/SCS load balancing rules for the Azure internal load balancer_</span></span>

<span data-ttu-id="7f5e0-695">부하 분산 장치 **pr1-lb-dbms**의 IP 주소를 DBMS 인스턴스의 가상 호스트 이름 IP 주소로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-695">Set the IP address of the load balancer **pr1-lb-dbms** to the IP address of the virtual host name of the DBMS instance.</span></span>

### <span data-ttu-id="7f5e0-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Azure 내부 부하 분산 장치에 대한 ASCS/SCS 기본 부하 분산 규칙 변경</span><span class="sxs-lookup"><span data-stu-id="7f5e0-696"><a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a> Change the ASCS/SCS default load balancing rules for the Azure internal load balancer</span></span>

<span data-ttu-id="7f5e0-697">SAP ASCS 또는 SCS 인스턴스에 대해 다른 번호를 사용하려는 경우 해당 포트의 이름과 값을 기본 값에서 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-697">If you want to use different numbers for the SAP ASCS or SCS instances, you must change the names and values of their ports from default values.</span></span>

1.  <span data-ttu-id="7f5e0-698">Azure Portal에서 **<*SID*>-lb-ascs 부하 분산 장치** > **부하 부산 규칙**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-698">In the Azure portal, select **<*SID*>-lb-ascs load balancer** > **Load Balancing Rules**.</span></span>
2.  <span data-ttu-id="7f5e0-699">SAP ASCS 또는 SCS 인스턴스에 속하는 모든 부하 분산 규칙에 대해 다음 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-699">For all load balancing rules that belong to the SAP ASCS or SCS instance, change these values:</span></span>

  * <span data-ttu-id="7f5e0-700">이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-700">Name</span></span>
  * <span data-ttu-id="7f5e0-701">포트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-701">Port</span></span>
  * <span data-ttu-id="7f5e0-702">백 엔드 포트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-702">Back-end port</span></span>

  <span data-ttu-id="7f5e0-703">예를 들어 기본 ASCS 인스턴스 번호를 00에서 31로 변경하려는 경우 표 1에 나열된 모든 포트에 대해 이러한 변경을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-703">For example, if you want to change the default ASCS instance number from 00 to 31, you need to make the changes for all ports listed in Table 1.</span></span>

  <span data-ttu-id="7f5e0-704">다음은 포트 *lbrule3200*에 대한 업데이트 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-704">Here's an example of an update for port *lbrule3200*.</span></span>

  ![그림 16: Azure 내부 부하 분산 장치의 기본 ASCS/SCS 부하 분산 규칙 변경][sap-ha-guide-figure-3005]

  <span data-ttu-id="7f5e0-706">_**그림 16:** Azure 내부 부하 분산 장치의 기본 ASCS/SCS 부하 분산 규칙 변경_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-706">_**Figure 16:** Change the ASCS/SCS default load balancing rules for the Azure internal load balancer_</span></span>

### <span data-ttu-id="7f5e0-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> 도메인에 Windows 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="7f5e0-707"><a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a> Add Windows virtual machines to the domain</span></span>

<span data-ttu-id="7f5e0-708">가상 컴퓨터에 고정 IP 주소를 할당한 후 가상 컴퓨터를 도메인에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-708">After you assign a static IP address to the virtual machines, add the virtual machines to the domain.</span></span>

![그림 17: 도메인에 가상 컴퓨터 추가][sap-ha-guide-figure-3006]

<span data-ttu-id="7f5e0-710">_**그림 17:** 도메인에 가상 컴퓨터 추가_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-710">_**Figure 17:** Add a virtual machine to a domain_</span></span>

### <span data-ttu-id="7f5e0-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> SAP ASCS/SCS 인스턴스의 클러스터 노드 둘 다에 대한 레지스트리 항목 추가</span><span class="sxs-lookup"><span data-stu-id="7f5e0-711"><a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a> Add registry entries on both cluster nodes of the SAP ASCS/SCS instance</span></span>

<span data-ttu-id="7f5e0-712">Azure Load Balancer에는 설정된 시간(유휴 제한 시간) 동안 연결이 유휴 상태일 때 연결을 닫는 내부 부하 분산 장치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-712">Azure Load Balancer has an internal load balancer that closes connections when the connections are idle for a set period of time (an idle timeout).</span></span> <span data-ttu-id="7f5e0-713">대화 상자 인스턴스의 SAP 작업 프로세스는 첫 번째 큐에 넣지/큐에서 제거 요청이 전송되는 즉시 SAP 큐에 넣기 프로세스에 대한 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-713">SAP work processes in dialog instances open connections to the SAP enqueue process as soon as the first enqueue/dequeue request needs to be sent.</span></span> <span data-ttu-id="7f5e0-714">이러한 연결은 일반적으로 작업 프로세스 또는 큐에 넣기 프로세스가 다시 시작될 때까지 설정 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-714">These connections usually remain established until the work process or the enqueue process restarts.</span></span> <span data-ttu-id="7f5e0-715">그러나 연결이 설정 기간 동안 유휴 상태이면 Azure 내부 부하 분산 장치는 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-715">However, if the connection is idle for a set period of time, the Azure internal load balancer closes the connections.</span></span> <span data-ttu-id="7f5e0-716">그렇지만 연결이 더 이상 없는 경우 SAP 작업 프로세스는 큐에 넣기 프로세스에 대한 연결을 다시 설정하기 때문에 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-716">This isn't a problem because the SAP work process reestablishes the connection to the enqueue process if it no longer exists.</span></span> <span data-ttu-id="7f5e0-717">이러한 활동은 SAP 프로세스의 개발자 추적에 설명되어 있지만 해당 추적에 많은 양의 추가 콘텐츠가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-717">These activities are documented in the developer traces of SAP processes, but they create a large amount of extra content in those traces.</span></span> <span data-ttu-id="7f5e0-718">따라서 두 클러스터 노드에서 TCP/IP `KeepAliveTime` 및 `KeepAliveInterval`을 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-718">It's a good idea to change the TCP/IP `KeepAliveTime` and `KeepAliveInterval` on both cluster nodes.</span></span> <span data-ttu-id="7f5e0-719">이 문서 뒷부분에 설명된 것처럼 TCP/IP 매개 변수의 이러한 변경 내용을 SAP 프로필 매개 변수와 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-719">Combine these changes in the TCP/IP parameters with SAP profile parameters, described later in the article.</span></span>

<span data-ttu-id="7f5e0-720">SAP ASCS/SCS 인스턴스의 두 클러스터 노드에 대해 레지스트리 항목을 추가하려면 먼저 SAP ASCS/SCS에 대한 두 Windows 클러스터 노드에 대해 다음 Windows 레지스트리 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-720">To add registry entries on both cluster nodes of the SAP ASCS/SCS instance, first, add these Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="7f5e0-721">Path</span><span class="sxs-lookup"><span data-stu-id="7f5e0-721">Path</span></span> | <span data-ttu-id="7f5e0-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="7f5e0-722">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="7f5e0-723">변수 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-723">Variable name</span></span> |`KeepAliveTime` |
| <span data-ttu-id="7f5e0-724">변수 유형</span><span class="sxs-lookup"><span data-stu-id="7f5e0-724">Variable type</span></span> |<span data-ttu-id="7f5e0-725">REG_DWORD(10진수)</span><span class="sxs-lookup"><span data-stu-id="7f5e0-725">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="7f5e0-726">값</span><span class="sxs-lookup"><span data-stu-id="7f5e0-726">Value</span></span> |<span data-ttu-id="7f5e0-727">120000</span><span class="sxs-lookup"><span data-stu-id="7f5e0-727">120000</span></span> |
| <span data-ttu-id="7f5e0-728">설명서 링크</span><span class="sxs-lookup"><span data-stu-id="7f5e0-728">Link to documentation</span></span> |[<span data-ttu-id="7f5e0-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span><span class="sxs-lookup"><span data-stu-id="7f5e0-729">https://technet.microsoft.com/en-us/library/cc957549.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

<span data-ttu-id="7f5e0-730">_**표 3:** 첫 번째 TCP/IP 매개 변수 변경_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-730">_**Table 3:** Change the first TCP/IP parameter_</span></span>

<span data-ttu-id="7f5e0-731">그런 다음 SAP ASCS/SCS에 대한 두 Windows 클러스터 노드에 대해 다음 Windows 레지스트리 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-731">Then, add this Windows registry entries on both Windows cluster nodes for SAP ASCS/SCS:</span></span>

| <span data-ttu-id="7f5e0-732">Path</span><span class="sxs-lookup"><span data-stu-id="7f5e0-732">Path</span></span> | <span data-ttu-id="7f5e0-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span><span class="sxs-lookup"><span data-stu-id="7f5e0-733">HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</span></span> |
| --- | --- |
| <span data-ttu-id="7f5e0-734">변수 이름</span><span class="sxs-lookup"><span data-stu-id="7f5e0-734">Variable name</span></span> |`KeepAliveInterval` |
| <span data-ttu-id="7f5e0-735">변수 유형</span><span class="sxs-lookup"><span data-stu-id="7f5e0-735">Variable type</span></span> |<span data-ttu-id="7f5e0-736">REG_DWORD(10진수)</span><span class="sxs-lookup"><span data-stu-id="7f5e0-736">REG_DWORD (Decimal)</span></span> |
| <span data-ttu-id="7f5e0-737">값</span><span class="sxs-lookup"><span data-stu-id="7f5e0-737">Value</span></span> |<span data-ttu-id="7f5e0-738">120000</span><span class="sxs-lookup"><span data-stu-id="7f5e0-738">120000</span></span> |
| <span data-ttu-id="7f5e0-739">설명서 링크</span><span class="sxs-lookup"><span data-stu-id="7f5e0-739">Link to documentation</span></span> |[<span data-ttu-id="7f5e0-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span><span class="sxs-lookup"><span data-stu-id="7f5e0-740">https://technet.microsoft.com/en-us/library/cc957548.aspx</span></span>](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

<span data-ttu-id="7f5e0-741">_**표 4:** 두 번째 TCP/IP 매개 변수 변경_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-741">_**Table 4:** Change the second TCP/IP parameter_</span></span>

<span data-ttu-id="7f5e0-742">**변경 내용을 적용하려면 두 클러스터 노드를 모두 다시 시작합니다.**</span><span class="sxs-lookup"><span data-stu-id="7f5e0-742">**To apply the changes, restart both cluster nodes**.</span></span>

### <span data-ttu-id="7f5e0-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> SAP ASCS/SCS 인스턴스에 대한 Windows Server 장애 조치 클러스터링 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-743"><a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Set up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance</span></span>

<span data-ttu-id="7f5e0-744">SAP ASCS/SCS 인스턴스의 Windows Server 장애 조치(failover) 클러스터링 클러스터 설정은 다음과 같은 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-744">Setting up a Windows Server Failover Clustering cluster for an SAP ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="7f5e0-745">클러스터 구성에서 클러스터 노드 수집</span><span class="sxs-lookup"><span data-stu-id="7f5e0-745">Collecting the cluster nodes in a cluster configuration</span></span>
- <span data-ttu-id="7f5e0-746">클러스터 파일 공유 감시 구성</span><span class="sxs-lookup"><span data-stu-id="7f5e0-746">Configuring a cluster file share witness</span></span>

#### <span data-ttu-id="7f5e0-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> 클러스터 구성에서 클러스터 노드 수집</span><span class="sxs-lookup"><span data-stu-id="7f5e0-747"><a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a> Collect the cluster nodes in a cluster configuration</span></span>

1.  <span data-ttu-id="7f5e0-748">역할 및 기능 추가 마법사에서 장애 조치 클러스터링을 두 클러스터 노드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-748">In the Add Role and Features Wizard, add failover clustering to both cluster nodes.</span></span>
2.  <span data-ttu-id="7f5e0-749">장애 조치 클러스터 관리자를 사용하여 장애 조치 클러스터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-749">Set up the failover cluster by using Failover Cluster Manager.</span></span> <span data-ttu-id="7f5e0-750">장애 조치 클러스터 관리자에서 **클러스터 만들기**를 선택한 다음 첫 번째 클러스터 노드, 노드 A의 이름만 추가합니다. 두 번째 노드를 아직 추가하지 마십시오. 이후 단계에서 두 번째 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-750">In Failover Cluster Manager, select **Create Cluster**, and then add only the name of the first cluster, node A. Do not add the second node yet; you'll add the second node in a later step.</span></span>

  ![그림 18: 첫 번째 클러스터 노드의 서버 또는 가상 컴퓨터 이름 추가][sap-ha-guide-figure-3007]

  <span data-ttu-id="7f5e0-752">_**그림 18:** 첫 번째 클러스터 노드의 서버 또는 가상 컴퓨터 이름 추가_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-752">_**Figure 18:** Add the server or virtual machine name of the first cluster node_</span></span>

3.  <span data-ttu-id="7f5e0-753">클러스터의 네트워크 이름(가상 호스트 이름)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-753">Enter the network name (virtual host name) of the cluster.</span></span>

  ![그림 19: 클러스터 이름 입력][sap-ha-guide-figure-3008]

  <span data-ttu-id="7f5e0-755">_**그림 19:** 클러스터 이름 입력_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-755">_**Figure 19:** Enter the cluster name_</span></span>

4.  <span data-ttu-id="7f5e0-756">클러스터를 만든 후에 클러스터 유효성 검사 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-756">After you've created the cluster, run a cluster validation test.</span></span>

  ![그림 20: 클러스터 유효성 검사 실행][sap-ha-guide-figure-3009]

  <span data-ttu-id="7f5e0-758">_**그림 20:** 클러스터 유효성 검사 실행_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-758">_**Figure 20:** Run the cluster validation check_</span></span>

  <span data-ttu-id="7f5e0-759">프로세스의 이 시점에 표시되는 디스크에 대한 경고는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-759">You can ignore any warnings about disks at this point in the process.</span></span> <span data-ttu-id="7f5e0-760">파일 공유 감시 및 SIOS 공유 디스크는 나중에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-760">You'll add a file share witness and the SIOS shared disks later.</span></span> <span data-ttu-id="7f5e0-761">이 단계에서는 쿼럼이 없어도 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-761">At this stage, you don't need to worry about having a quorum.</span></span>

  ![그림 21: 쿼럼 디스크가 없음][sap-ha-guide-figure-3010]

  <span data-ttu-id="7f5e0-763">_**그림 21:** 쿼럼 디스크가 없음_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-763">_**Figure 21:** No quorum disk is found_</span></span>

  ![그림 22: 새 IP 주소가 필요한 코어 클러스터 리소스][sap-ha-guide-figure-3011]

  <span data-ttu-id="7f5e0-765">_**그림 22:** 새 IP 주소가 필요한 코어 클러스터 리소스_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-765">_**Figure 22:** Core cluster resource needs a new IP address_</span></span>

5.  <span data-ttu-id="7f5e0-766">핵심 클러스터 서비스의 IP 주소를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-766">Change the IP address of the core cluster service.</span></span> <span data-ttu-id="7f5e0-767">서버의 IP 주소가 가상 컴퓨터 노드 중 하나를 가리키므로 핵심 클러스터 서비스의 IP 주소를 변경할 때까지 클러스터를 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-767">The cluster can't start until you change the IP address of the core cluster service, because the IP address of the server points to one of the virtual machine nodes.</span></span> <span data-ttu-id="7f5e0-768">핵심 클러스터 서비스의 IP 리소스에 대한 **속성** 페이지에서 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-768">Do this on the **Properties** page of the core cluster service's IP resource.</span></span>

  <span data-ttu-id="7f5e0-769">예를 들어 클러스터 가상 호스트 이름 **pr1-ascs-vir**에 대한 IP 주소(이 예제에서 **10.0.0.42**)를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-769">For example, we need to assign an IP address (in our example, **10.0.0.42**) for the cluster virtual host name **pr1-ascs-vir**.</span></span>

  ![그림 23: 속성 대화 상자에서 IP 주소 변경][sap-ha-guide-figure-3012]

  <span data-ttu-id="7f5e0-771">_**그림 23:** **속성** 대화 상자에서 IP 주소 변경_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-771">_**Figure 23:** In the **Properties** dialog box, change the IP address_</span></span>

  ![그림 24: 클러스터에 예약된 IP 주소 할당][sap-ha-guide-figure-3013]

  <span data-ttu-id="7f5e0-773">_**그림 24:** 클러스터에 예약된 IP 주소 할당_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-773">_**Figure 24:** Assign the IP address that is reserved for the cluster_</span></span>

6.  <span data-ttu-id="7f5e0-774">클러스터 가상 호스트 이름을 온라인으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-774">Bring the cluster virtual host name online.</span></span>

  ![그림 25: 올바른 IP 주소를 사용하여 작동 및 실행하는 클러스터 코어 서비스][sap-ha-guide-figure-3014]

  <span data-ttu-id="7f5e0-776">_**그림 25:** 올바른 IP 주소를 사용하여 작동 및 실행하는 클러스터 코어 서비스_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-776">_**Figure 25:** Cluster core service is up and running, and with the correct IP address_</span></span>

7.  <span data-ttu-id="7f5e0-777">두 번째 클러스터 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-777">Add the second cluster node.</span></span>

  <span data-ttu-id="7f5e0-778">핵심 클러스터 서비스가 작동 및 실행되고 있으므로 두 번째 클러스터 노드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-778">Now that the core cluster service is up and running, you can add the second cluster node.</span></span>

  ![그림 26: 두 번째 클러스터 노드 추가][sap-ha-guide-figure-3015]

  <span data-ttu-id="7f5e0-780">_**그림 26:** 두 번째 클러스터 노드 추가_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-780">_**Figure 26:** Add the second cluster node_</span></span>

8.  <span data-ttu-id="7f5e0-781">두 번째 클러스터 노드 호스트의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-781">Enter a name for the second cluster node host.</span></span>

  ![그림 27: 두 번째 클러스터 노드 호스트 이름 입력][sap-ha-guide-figure-3016]

  <span data-ttu-id="7f5e0-783">_**그림 27:** 두 번째 클러스터 노드 호스트 이름 입력_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-783">_**Figure 27:** Enter the second cluster node host name_</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7f5e0-784">**클러스터에 사용할 수 있는 모든 저장소를 추가하세요.** 확인란을 선택하지 **않았는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-784">Be sure that the **Add all eligible storage to the cluster** check box is **NOT** selected.</span></span>  
  >
  >

  ![그림 28: 확인란 선택 안 함][sap-ha-guide-figure-3017]

  <span data-ttu-id="7f5e0-786">_**그림 28:** 확인란 **선택 안 함**_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-786">_**Figure 28:** Do **not** select the check box_</span></span>

  <span data-ttu-id="7f5e0-787">쿼럼 및 디스크에 대한 경고는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-787">You can ignore warnings about quorum and disks.</span></span> <span data-ttu-id="7f5e0-788">[SAP ASCS/SCS 클러스터 공유 디스크용 SIOS DataKeeper Cluster Edition 설치][sap-ha-guide-8.12.3]에서 설명한 대로 쿼럼을 설정하고 나중에 디스크를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-788">You'll set the quorum and share the disk later, as described in [Installing SIOS DataKeeper Cluster Edition for SAP ASCS/SCS cluster share disk][sap-ha-guide-8.12.3].</span></span>

  ![그림 29: 디스크 쿼럼에 대한 경고 무시][sap-ha-guide-figure-3018]

  <span data-ttu-id="7f5e0-790">_**그림 29:** 디스크 쿼럼에 대한 경고 무시_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-790">_**Figure 29:** Ignore warnings about the disk quorum_</span></span>


#### <span data-ttu-id="7f5e0-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> 클러스터 파일 공유 감시 구성</span><span class="sxs-lookup"><span data-stu-id="7f5e0-791"><a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configure a cluster file share witness</span></span>

<span data-ttu-id="7f5e0-792">클러스터 파일 공유 감시 구성은 다음과 같은 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-792">Configuring a cluster file share witness involves these tasks:</span></span>

- <span data-ttu-id="7f5e0-793">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="7f5e0-793">Creating a file share</span></span>
- <span data-ttu-id="7f5e0-794">장애 조치 클러스터 관리자에서 파일 공유 감시 쿼럼 설정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-794">Setting the file share witness quorum in Failover Cluster Manager</span></span>

##### <span data-ttu-id="7f5e0-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="7f5e0-795"><a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Create a file share</span></span>

1.  <span data-ttu-id="7f5e0-796">쿼럼 디스크 대신 파일 공유 감시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-796">Select a file share witness instead of a quorum disk.</span></span> <span data-ttu-id="7f5e0-797">SIOS DataKeeper는 이 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-797">SIOS DataKeeper supports this option.</span></span>

  <span data-ttu-id="7f5e0-798">이 문서의 예제에서 파일 공유 감시는 Azure에서 실행되는 Active Directory/DNS 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-798">In the examples in this article, the file share witness is on the Active Directory/DNS server that is running in Azure.</span></span> <span data-ttu-id="7f5e0-799">파일 공유 감시를 **domcontr-0**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-799">The file share witness is called **domcontr-0**.</span></span> <span data-ttu-id="7f5e0-800">Azure에 대해 VPN 연결을 구성했으므로(사이트 간 VPN 또는 Azure ExpressRoute를 통해) Active Directory/DNS 서비스는 온-프레미스이며 파일 공유 감시를 실행하는 데 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-800">Because you would have configured a VPN connection to Azure (via Site-to-Site VPN or Azure ExpressRoute), your Active Directory/DNS service is on-premises and isn't suitable to run a file share witness.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7f5e0-801">Active Directory/DNS 서비스는 온-프레미스로만 실행되므로 온-프레미스로 실행되는 Active Directory/DNS Windows 운영 체제에서 파일 공유 감시를 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-801">If your Active Directory/DNS service runs only on-premises, don't configure your file share witness on the Active Directory/DNS Windows operating system that is running on-premises.</span></span> <span data-ttu-id="7f5e0-802">Azure 및 Active Directory/DNS 온-프레미스로 실행되는 클러스터 노드 간 네트워크 대기 시간이 너무 커서 연결 문제를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-802">Network latency between cluster nodes running in Azure and Active Directory/DNS on-premises might be too large and cause connectivity issues.</span></span> <span data-ttu-id="7f5e0-803">클러스터 노드와 가깝게 실행되는 Azure Virtual Machines에서 파일 공유 감시를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-803">Be sure to configure the file share witness on an Azure virtual machine that is running close to the cluster node.</span></span>  
  >
  >

  <span data-ttu-id="7f5e0-804">쿼럼 드라이브에는 1,024MB 이상의 여유 공간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-804">The quorum drive needs at least 1,024 MB of free space.</span></span> <span data-ttu-id="7f5e0-805">쿼럼 드라이브에 2,048MB의 여유 공간을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-805">We recommend 2,048 MB of free space for the quorum drive.</span></span>

2.  <span data-ttu-id="7f5e0-806">클러스터 이름 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-806">Add the cluster name object.</span></span>

  ![그림 30: 클러스터 이름 개체의 공유를 위한 권한 할당][sap-ha-guide-figure-3019]

  <span data-ttu-id="7f5e0-808">_**그림 30:** 클러스터 이름 개체의 공유를 위한 권한 할당_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-808">_**Figure 30:** Assign the permissions on the share for the cluster name object_</span></span>

  <span data-ttu-id="7f5e0-809">클러스터 이름 개체(예제의 **pr1-ascs-vir$**)에 대한 공유에서 데이터를 변경할 수 있는 권한이 포함되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-809">Be sure that the permissions include the authority to change data in the share for the cluster name object (in our example, **pr1-ascs-vir$**).</span></span>

3.  <span data-ttu-id="7f5e0-810">목록에 클러스터 이름 개체를 추가하려면 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-810">To add the cluster name object to the list, select **Add**.</span></span> <span data-ttu-id="7f5e0-811">그림 31에서 보여 주는 방법 외에도 필터를 변경하여 컴퓨터 개체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-811">Change the filter to check for computer objects, in addition to those shown in Figure 31.</span></span>

  ![그림 31: 개체 유형을 변경하여 컴퓨터 포함][sap-ha-guide-figure-3020]

  <span data-ttu-id="7f5e0-813">_**그림 31:** 개체 유형을 변경하여 컴퓨터 포함_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-813">_**Figure 31:** Change the Object Types to include computers_</span></span>

  ![그림 32: 컴퓨터 확인란 선택][sap-ha-guide-figure-3021]

  <span data-ttu-id="7f5e0-815">_**그림 32:** **컴퓨터** 확인란 선택_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-815">_**Figure 32:** Select the **Computers** check box_</span></span>

4.  <span data-ttu-id="7f5e0-816">그림 31과 같이 클러스터 이름 개체를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-816">Enter the cluster name object as shown in Figure 31.</span></span> <span data-ttu-id="7f5e0-817">레코드가 이미 만들어졌으므로 그림 30과 같이 권한을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-817">Because the record has already been created, you can change the permissions, as shown in Figure 30.</span></span>

5.  <span data-ttu-id="7f5e0-818">공유의 **보안** 탭을 선택한 후 클러스터 이름 개체에 대한 좀 더 자세한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-818">Select the **Security** tab of the share, and then set more detailed permissions for the cluster name object.</span></span>

  ![그림 33: 파일 공유 쿼럼의 클러스터 이름 개체에 대한 보안 특성 설정][sap-ha-guide-figure-3022]

  <span data-ttu-id="7f5e0-820">_**그림 33:** 파일 공유 쿼럼의 클러스터 이름 개체에 대한 보안 특성 설정_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-820">_**Figure 33:** Set the security attributes for the cluster name object on the file share quorum_</span></span>

##### <span data-ttu-id="7f5e0-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> 장애 조치 클러스터 관리자에서 파일 공유 감시 쿼럼 설정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-821"><a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a> Set the file share witness quorum in Failover Cluster Manager</span></span>

1.  <span data-ttu-id="7f5e0-822">쿼럼 설정 구성 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-822">Open the Configure Quorum Setting Wizard.</span></span>

  ![그림 34: 클러스터 쿼럼 설정 구성 마법사 시작][sap-ha-guide-figure-3023]

  <span data-ttu-id="7f5e0-824">_**그림 34:** 클러스터 쿼럼 설정 구성 마법사 시작_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-824">_**Figure 34:** Start the Configure Cluster Quorum Setting Wizard_</span></span>

2.  <span data-ttu-id="7f5e0-825">**쿼럼 구성 선택** 페이지에서 **쿼럼 감시 선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-825">On the **Select Quorum Configuration** page, select **Select the quorum witness**.</span></span>

  ![그림 35: 선택할 수 있는 쿼럼 구성][sap-ha-guide-figure-3024]

  <span data-ttu-id="7f5e0-827">_**그림 35:** 선택할 수 있는 쿼럼 구성_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-827">_**Figure 35:** Quorum configurations you can choose from_</span></span>

3.  <span data-ttu-id="7f5e0-828">**쿼럼 감시 선택** 페이지에서 **파일 공유 감시 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-828">On the **Select Quorum Witness** page, select **Configure a file share witness**.</span></span>

  ![그림 36: 파일 공유 감시 선택][sap-ha-guide-figure-3025]

  <span data-ttu-id="7f5e0-830">_**그림 36:** 파일 공유 감시 선택_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-830">_**Figure 36:** Select the file share witness_</span></span>

4.  <span data-ttu-id="7f5e0-831">파일 공유에 대한 UNC 경로를 입력합니다(예제의 \\domcontr-0\FSW).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-831">Enter the UNC path to the file share (in our example, \\domcontr-0\FSW).</span></span> <span data-ttu-id="7f5e0-832">변경할 수 있는 목록을 표시하려면 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-832">To see a list of the changes you can make, select **Next**.</span></span>

  ![그림 37: 공유 감시를 위한 파일 공유 위치 정의][sap-ha-guide-figure-3026]

  <span data-ttu-id="7f5e0-834">_**그림 37:** 공유 감시를 위한 파일 공유 위치 정의_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-834">_**Figure 37:** Define the file share location for the witness share_</span></span>

5.  <span data-ttu-id="7f5e0-835">원하는 변경 내용을 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-835">Select the changes you want, and then select **Next**.</span></span> <span data-ttu-id="7f5e0-836">그림 38과 같이 클러스터 구성을 성공적으로 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-836">You need to successfully reconfigure the cluster configuration as shown in Figure 38.</span></span>  

  ![그림 38: 클러스터를 다시 구성했는지 확인][sap-ha-guide-figure-3027]

  <span data-ttu-id="7f5e0-838">_**그림 38:** 클러스터를 다시 구성했는지 확인_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-838">_**Figure 38:** Confirmation that you've reconfigured the cluster_</span></span>

<span data-ttu-id="7f5e0-839">Windows 장애 조치(failover) 클러스터를 성공적으로 설치한 후 장애 조치(failover) 검색이 Azure의 상태에 맞게 조정되도록 일부 임계값을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-839">After installing the Windows Failover Cluster successfully, changes need to be made to some thresholds to adapt failover detection to conditions in Azure.</span></span> <span data-ttu-id="7f5e0-840">변경할 매개 변수는 https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ 블로그에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-840">The parameters to be changed are documented in this blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/ .</span></span> <span data-ttu-id="7f5e0-841">ASCS/SCS에 대한 Windows 클러스터 구성을 빌드하는 2개의 VM이 동일한 서브넷에 있다고 가정할 경우 다음 매개 변수를 다음과 같은 값으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-841">Assuming that your two VMs that build the Windows Cluster Configuration for ASCS/SCS are in the same SubNet, the following parameters need to be changed to these values:</span></span>
- <span data-ttu-id="7f5e0-842">SameSubNetDelay = 2</span><span class="sxs-lookup"><span data-stu-id="7f5e0-842">SameSubNetDelay = 2</span></span>
- <span data-ttu-id="7f5e0-843">SameSubNetThreshold = 15</span><span class="sxs-lookup"><span data-stu-id="7f5e0-843">SameSubNetThreshold = 15</span></span>

<span data-ttu-id="7f5e0-844">이러한 설정은 고객과 함께 테스트되었으며 어떤 면에서는 충분히 복원력이 있는 좋은 타협안을 제공했으나</span><span class="sxs-lookup"><span data-stu-id="7f5e0-844">These settings were tested with customers and provided a good compromise to be resilient enough on the one side.</span></span> <span data-ttu-id="7f5e0-845">다른 측면에서는 SAP 소프트웨어 또는 노드/VM 장애의 실제 오류 상태에서 충분히 빠른 장애 조치(failover)를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-845">On the other hand those settings were providing fast enough failover in real error conditions on SAP software or node/VM failure.</span></span> 

### <span data-ttu-id="7f5e0-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> SAP ASCS/SCS 클러스터 공유 디스크에 대한 SIOS DataKeeper Cluster Edition 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-846"><a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a> Install SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk</span></span>

<span data-ttu-id="7f5e0-847">이제 Azure에서 Windows Server 장애 조치 클러스터링 구성이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-847">You now have a working Windows Server Failover Clustering configuration in Azure.</span></span> <span data-ttu-id="7f5e0-848">그렇지만 SAP ASCS/SCS 인스턴스를 설치하려면 공유 디스크 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-848">But, to install an SAP ASCS/SCS instance, you need a shared disk resource.</span></span> <span data-ttu-id="7f5e0-849">Azure에서는 필요한 공유 디스크 리소스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-849">You cannot create the shared disk resources you need in Azure.</span></span> <span data-ttu-id="7f5e0-850">SIOS DataKeeper Cluster Edition은 공유 디스크 리소스를 만드는 데 사용할 수 있는 타사 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-850">SIOS DataKeeper Cluster Edition is a third-party solution you can use to create shared disk resources.</span></span>

<span data-ttu-id="7f5e0-851">SAP ASCS/SCS 클러스터 공유 디스크에 대한 SIOS DataKeeper Cluster Edition 설치는 다음과 같은 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-851">Installing SIOS DataKeeper Cluster Edition for the SAP ASCS/SCS cluster share disk involves these tasks:</span></span>

- <span data-ttu-id="7f5e0-852">.NET Framework 3.5 추가</span><span class="sxs-lookup"><span data-stu-id="7f5e0-852">Adding the .NET Framework 3.5</span></span>
- <span data-ttu-id="7f5e0-853">SIOS DataKeeper 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-853">Installing SIOS DataKeeper</span></span>
- <span data-ttu-id="7f5e0-854">SIOS DataKeeper 설정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-854">Setting up SIOS DataKeeper</span></span>

#### <span data-ttu-id="7f5e0-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> .NET Framework 3.5 추가</span><span class="sxs-lookup"><span data-stu-id="7f5e0-855"><a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a> Add the .NET Framework 3.5</span></span>
<span data-ttu-id="7f5e0-856">Microsoft.NET Framework 3.5는 Windows Server 2012 R2에서 자동으로 활성화되거나 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-856">The Microsoft .NET Framework 3.5 isn't automatically activated or installed on Windows Server 2012 R2.</span></span> <span data-ttu-id="7f5e0-857">SIOS DataKeeper는 DataKeeper를 설치하는 모든 노드에 .NET Framework를 필요로 하므로 클러스터의 모든 가상 컴퓨터의 게스트 운영 체제에 .NET Framework 3.5를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-857">Because SIOS DataKeeper requires the .NET Framework to be on all nodes that you install DataKeeper on, you must install the .NET Framework 3.5 on the guest operating system of all virtual machines in the cluster.</span></span>

<span data-ttu-id="7f5e0-858">.NET Framework 3.5는 두 가지 방법으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-858">There are two ways to add the .NET Framework 3.5:</span></span>

- <span data-ttu-id="7f5e0-859">그림 39와 같이 Windows에서 역할 및 기능 추가 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-859">Use the Add Roles and Features Wizard in Windows as shown in Figure 39.</span></span>

  ![그림 39: 역할 및 기능 추가 마법사를 사용하여 .NET Framework 3.5 설치][sap-ha-guide-figure-3028]

  <span data-ttu-id="7f5e0-861">_**그림 39:** 역할 및 기능 추가 마법사를 사용하여 .NET Framework 3.5 설치_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-861">_**Figure 39:** Install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

  ![그림 40: 역할 및 기능 추가 마법사를 사용하여 .NET Framework 3.5를 설치할 때의 설치 진행률 표시줄][sap-ha-guide-figure-3029]

  <span data-ttu-id="7f5e0-863">_**그림 40:** 역할 및 기능 추가 마법사를 사용하여 .NET Framework 3.5를 설치할 때의 설치 진행률 표시줄_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-863">_**Figure 40:** Installation progress bar when you install the .NET Framework 3.5 by using the Add Roles and Features Wizard_</span></span>

- <span data-ttu-id="7f5e0-864">명령줄 도구 dism.exe를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-864">Use the command-line tool dism.exe.</span></span> <span data-ttu-id="7f5e0-865">이 유형의 설치에서는 Windows 설치 미디어의 SxS 디렉터리에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-865">For this type of installation, you need to access the SxS directory on the Windows installation media.</span></span> <span data-ttu-id="7f5e0-866">관리자 권한의 명령 프롬프트에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-866">At an elevated command prompt, type:</span></span>

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <span data-ttu-id="7f5e0-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> SIOS DataKeeper 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-867"><a name="dd41d5a2-8083-415b-9878-839652812102"></a> Install SIOS DataKeeper</span></span>

<span data-ttu-id="7f5e0-868">클러스터의 각 노드에 SIOS DataKeeper Cluster Edition을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-868">Install SIOS DataKeeper Cluster Edition on each node in the cluster.</span></span> <span data-ttu-id="7f5e0-869">SIOS DataKeeper를 사용하여 가상 공유 저장소를 만들려면 동기화된 미러를 만든 후 클러스터 공유 저장소를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-869">To create virtual shared storage with SIOS DataKeeper, create a synced mirror and then simulate cluster shared storage.</span></span>

<span data-ttu-id="7f5e0-870">SIOS 소프트웨어를 설치하기 전에 도메인 사용자 **DataKeeperSvc**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-870">Before you install the SIOS software, create the domain user **DataKeeperSvc**.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-871">**DataKeeperSvc** 사용자를 두 클러스터 노드의 **로컬 관리자** 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-871">Add the **DataKeeperSvc** user to the **Local Administrator** group on both cluster nodes.</span></span>
>
>

<span data-ttu-id="7f5e0-872">SIOS DataKeeper를 설치하려면:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-872">To install SIOS DataKeeper:</span></span>

1.  <span data-ttu-id="7f5e0-873">두 클러스터 노드에서 SIOS 소프트웨어를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-873">Install the SIOS software on both cluster nodes.</span></span>

  ![SIOS 설치 관리자][sap-ha-guide-figure-3030]

  ![그림 41: SIOS DataKeeper 설치의 첫 번째 페이지][sap-ha-guide-figure-3031]

  <span data-ttu-id="7f5e0-876">_**그림 41:** SIOS DataKeeper 설치의 첫 번째 페이지_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-876">_**Figure 41:** First page of the SIOS DataKeeper installation_</span></span>

2.  <span data-ttu-id="7f5e0-877">그림 42에서 보여 주는 대화 상자에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-877">In the dialog box shown in Figure 42, select **Yes**.</span></span>

  ![그림 42: 서비스를 사용할 수 없다고 알리는 DataKeeper][sap-ha-guide-figure-3032]

  <span data-ttu-id="7f5e0-879">_**그림 42:** 서비스를 사용할 수 없다고 알리는 DataKeeper_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-879">_**Figure 42:** DataKeeper informs you that a service will be disabled_</span></span>

3.  <span data-ttu-id="7f5e0-880">그림 43에서 보여 주는 대화 상자에서 **도메인 또는 서버 계정**을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-880">In the dialog box shown in Figure 43, we recommend that you select **Domain or Server account**.</span></span>

  ![그림 43: SIOS DataKeeper에 대한 사용자 선택][sap-ha-guide-figure-3033]

  <span data-ttu-id="7f5e0-882">_**그림 43:** SIOS DataKeeper에 대한 사용자 선택_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-882">_**Figure 43:** User selection for SIOS DataKeeper_</span></span>

4.  <span data-ttu-id="7f5e0-883">SIOS DataKeeper에 대해 만든 도메인 계정 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-883">Enter the domain account user name and passwords that you created for SIOS DataKeeper.</span></span>

  ![그림 44: SIOS DataKeeper 설치를 위한 도메인 사용자 이름 및 암호 입력][sap-ha-guide-figure-3034]

  <span data-ttu-id="7f5e0-885">_**그림 44:** SIOS DataKeeper 설치를 위한 도메인 사용자 이름 및 암호 입력_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-885">_**Figure 44:** Enter the domain user name and password for the SIOS DataKeeper installation_</span></span>

5.  <span data-ttu-id="7f5e0-886">그림 45와 같이 SIOS DataKeeper 인스턴스를 위한 라이선스 키를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-886">Install the license key for your SIOS DataKeeper instance as shown in Figure 45.</span></span>

  ![그림 45: SIOS DataKeeper 라이선스 키 입력][sap-ha-guide-figure-3035]

  <span data-ttu-id="7f5e0-888">_**그림 45:** SIOS DataKeeper 라이선스 키 입력_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-888">_**Figure 45:** Enter your SIOS DataKeeper license key_</span></span>

6.  <span data-ttu-id="7f5e0-889">메시지가 표시되면 가상 컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-889">When prompted, restart the virtual machine.</span></span>

#### <span data-ttu-id="7f5e0-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> SIOS DataKeeper 설정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-890"><a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Set up SIOS DataKeeper</span></span>

<span data-ttu-id="7f5e0-891">두 노드에 SIOS DataKeeper를 설치한 후 구성을 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-891">After you install SIOS DataKeeper on both nodes, you need to start the configuration.</span></span> <span data-ttu-id="7f5e0-892">이러한 구성의 목표는 각 가상 컴퓨터에 연결된 추가 디스크 간에 동기식으로 데이터를 복제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-892">The goal of the configuration is to have synchronous data replication between the additional disks attached to each of the virtual machines.</span></span>

1.  <span data-ttu-id="7f5e0-893">DataKeeper 관리 및 구성 도구를 시작한 다음 **서버 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-893">Start the DataKeeper Management and Configuration tool, and then select **Connect Server**.</span></span> <span data-ttu-id="7f5e0-894">그림 46에서 이 옵션은 빨간색 원으로 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-894">(In Figure 46, this option is circled in red.)</span></span>

  ![그림 46: SIOS DataKeeper 관리 및 구성 도구][sap-ha-guide-figure-3036]

  <span data-ttu-id="7f5e0-896">_**그림 46:** SIOS DataKeeper 관리 및 구성 도구_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-896">_**Figure 46:** SIOS DataKeeper Management and Configuration tool_</span></span>

2.  <span data-ttu-id="7f5e0-897">관리 및 구성 도구에서 연결해야 하는 첫 번째 노드의 이름 또는 TCP/IP 주소를 삽입한 후 다음 단계에서 두 번째 노드에 대해 동일한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-897">Enter the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and, in a second step, the second node.</span></span>

  ![그림 47: 관리 및 구성 도구에서 연결해야 하는 첫 번째 노드의 이름 또는 TCP/IP 주소를 삽입한 후 다음 단계에서 두 번째 노드에 대해 동일한 작업 수행][sap-ha-guide-figure-3037]

  <span data-ttu-id="7f5e0-899">_**그림 47:** 관리 및 구성 도구에서 연결해야 하는 첫 번째 노드의 이름 또는 TCP/IP 주소를 삽입한 후 다음 단계에서 두 번째 노드에 대해 동일한 작업 수행_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-899">_**Figure 47:** Insert the name or TCP/IP address of the first node the Management and Configuration tool should connect to, and in a second step, the second node_</span></span>

3.  <span data-ttu-id="7f5e0-900">두 노드 간에 복제 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-900">Create the replication job between the two nodes.</span></span>

  ![그림 48: 복제 작업 만들기][sap-ha-guide-figure-3038]

  <span data-ttu-id="7f5e0-902">_**그림 48:** 복제 작업 만들기_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-902">_**Figure 48:** Create a replication job_</span></span>

  <span data-ttu-id="7f5e0-903">마법사에서 복제 작업을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-903">A wizard guides you through the process of creating a replication job.</span></span>
4.  <span data-ttu-id="7f5e0-904">소스 노드의 이름, TCP/IP 주소 및 디스크 볼륨을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-904">Define the name, TCP/IP address, and disk volume of the source node.</span></span>

  ![그림 49: 복제 작업 이름 정의][sap-ha-guide-figure-3039]

  <span data-ttu-id="7f5e0-906">_**그림 49:** 복제 작업 이름 정의_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-906">_**Figure 49:** Define the name of the replication job_</span></span>

  ![그림 50: 현재 원본 노드에 해당하는 노드의 기본 데이터 정의][sap-ha-guide-figure-3040]

  <span data-ttu-id="7f5e0-908">_**그림 50:** 현재 원본 노드에 해당하는 노드의 기본 데이터 정의_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-908">_**Figure 50:** Define the base data for the node, which should be the current source node_</span></span>

5.  <span data-ttu-id="7f5e0-909">대상 노드의 이름, TCP/IP 주소 및 디스크 볼륨을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-909">Define the name, TCP/IP address, and disk volume of the target node.</span></span>

  ![그림 51: 현재 대상 노드에 해당하는 노드의 기본 데이터 정의][sap-ha-guide-figure-3041]

  <span data-ttu-id="7f5e0-911">_**그림 51:** 현재 대상 노드에 해당하는 노드의 기본 데이터 정의_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-911">_**Figure 51:** Define the base data for the node, which should be the current target node_</span></span>

6.  <span data-ttu-id="7f5e0-912">압축 알고리즘을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-912">Define the compression algorithms.</span></span> <span data-ttu-id="7f5e0-913">예제에서는 복제 스트림을 압축하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-913">In our example, we recommend that you compress the replication stream.</span></span> <span data-ttu-id="7f5e0-914">특히 재동기화 상황에서는 복제 스트림을 압축하면 재동기화 시간을 크게 단축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-914">Especially in resynchronization situations, the compression of the replication stream dramatically reduces resynchronization time.</span></span> <span data-ttu-id="7f5e0-915">압축에는 가상 컴퓨터의 CPU 및 RAM 리소스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-915">Note that compression uses the CPU and RAM resources of a virtual machine.</span></span> <span data-ttu-id="7f5e0-916">압축 속도가 증가하면 사용되는 CPU 리소스 양도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-916">As the compression rate increases, so does the volume of CPU resources used.</span></span> <span data-ttu-id="7f5e0-917">나중에 이 설정을 조정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-917">You also can adjust this setting later.</span></span>

7.  <span data-ttu-id="7f5e0-918">확인해야 하는 또 다른 설정은 복제가 비동기식 또는 동기식 중에서 어떤 방식으로 발생하는가 입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-918">Another setting you need to check is whether the replication occurs asynchronously or synchronously.</span></span> <span data-ttu-id="7f5e0-919">*SAP ASCS/SCS 구성을 보호할 때 동기 복제를 사용해야 합니다*.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-919">*When you protect SAP ASCS/SCS configurations, you must use synchronous replication*.</span></span>  

  ![그림 52: 복제 세부 정보 정의][sap-ha-guide-figure-3042]

  <span data-ttu-id="7f5e0-921">_**그림 52:** 복제 세부 정보 정의_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-921">_**Figure 52:** Define replication details_</span></span>

8.  <span data-ttu-id="7f5e0-922">복제 작업에 의해 복제되는 볼륨을 Windows Server 장애 조치 클러스터링 클러스터 구성에 공유 디스크로 나타낼지 여부를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-922">Define whether the volume that is replicated by the replication job should be represented to a Windows Server Failover Clustering cluster configuration as a shared disk.</span></span> <span data-ttu-id="7f5e0-923">SAP ASCS/SCS 구성의 경우 Windows 클러스터가 복제된 볼륨을 클러스터 볼륨으로 사용할 수 있는 공유 디스크로 인식하도록 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-923">For the SAP ASCS/SCS configuration, select **Yes** so that the Windows cluster sees the replicated volume as a shared disk that it can use as a cluster volume.</span></span>

  ![그림 53: 예를 선택하여 복제된 볼륨을 클러스터 볼륨으로 설정][sap-ha-guide-figure-3043]

  <span data-ttu-id="7f5e0-925">_**그림 53:** **예**를 선택하여 복제된 볼륨을 클러스터 볼륨으로 설정_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-925">_**Figure 53:** Select **Yes** to set the replicated volume as a cluster volume_</span></span>

  <span data-ttu-id="7f5e0-926">볼륨을 만든 후 DataKeeper 관리 및 구성 도구에서 복제 작업 활성화되어 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-926">After the volume is created, the DataKeeper Management and Configuration tool shows that the replication job is active.</span></span>

  ![그림 54: SAP ASCS/SCS 공유 디스크에 대해 활성화된 DataKeeper 동기식 미러링][sap-ha-guide-figure-3044]

  <span data-ttu-id="7f5e0-928">_**그림 54:** SAP ASCS/SCS 공유 디스크에 대해 활성화된 DataKeeper 동기식 미러링_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-928">_**Figure 54:** DataKeeper synchronous mirroring for the SAP ASCS/SCS share disk is active_</span></span>

  <span data-ttu-id="7f5e0-929">이제 그림 55와 같이 장애 조치 클러스터 관리자에서 디스크를 DataKeeper 디스크로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-929">Failover Cluster Manager now shows the disk as a DataKeeper disk, as shown in Figure 55.</span></span>

  ![그림 55: 장애 조치 클러스터 관리자에서 표시하는 DataKeeper에서 복제한 디스크][sap-ha-guide-figure-3045]

  <span data-ttu-id="7f5e0-931">_**그림 55:** 장애 조치 클러스터 관리자에서 표시하는 DataKeeper에서 복제한 디스크_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-931">_**Figure 55:** Failover Cluster Manager shows the disk that DataKeeper replicated_</span></span>

## <span data-ttu-id="7f5e0-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> SAP NetWeaver 시스템 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-932"><a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a> Install the SAP NetWeaver system</span></span>

<span data-ttu-id="7f5e0-933">설정은 사용하는 DBMS 시스템에 따라 다르므로 DBMS 설정에 대해서는 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-933">We won’t describe the DBMS setup because setups vary depending on the DBMS system you use.</span></span> <span data-ttu-id="7f5e0-934">그러나 다른 DBMS 공급업체가 Azure에 대해 지원하는 기능으로 DBMS의 고가용성 문제가 해결된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-934">However, we assume that high-availability concerns with the DBMS are addressed with the functionalities the different DBMS vendors support for Azure.</span></span> <span data-ttu-id="7f5e0-935">예로 SQL Server 및 Oracle 데이터베이스용 Oracle Data Guard에 대한 AlwaysOn 또는 데이터베이스 미러링을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-935">For example, Always On or database mirroring for SQL Server, and Oracle Data Guard for Oracle databases.</span></span> <span data-ttu-id="7f5e0-936">이 문서에서 사용하는 시나리오에서는 DBMS에 대해 추가 보호를 적용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-936">In the scenario we use in this article, we didn't add more protection to the DBMS.</span></span>

<span data-ttu-id="7f5e0-937">Azure에서 여러 다른 DBMS 서비스가 이러한 종류의 클러스터형 SAP ASCS/SCS 구성과 상호 작용할 경우 특별한 고려 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-937">There are no special considerations when different DBMS services interact with this kind of clustered SAP ASCS/SCS configuration in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-938">SAP NetWeaver ABAP 시스템, Java 시스템 및 ABAP+Java 시스템의 설치 절차는 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-938">The installation procedures of SAP NetWeaver ABAP systems, Java systems, and ABAP+Java systems are almost identical.</span></span> <span data-ttu-id="7f5e0-939">가장 중요한 차이점은 SAP ABAP 시스템에 ASCS 인스턴스가 하나 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-939">The most significant difference is that an SAP ABAP system has one ASCS instance.</span></span> <span data-ttu-id="7f5e0-940">SAP Java 시스템에는 하나의 SCS 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-940">The SAP Java system has one SCS instance.</span></span> <span data-ttu-id="7f5e0-941">SAP ABAP+Java 시스템에서는 동일한 Microsoft 장애 조치 클러스터 그룹에 하나의 ASCS 인스턴스와 하나의 SCS 인스턴스가 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-941">The SAP ABAP+Java system has one ASCS instance and one SCS instance running in the same Microsoft failover cluster group.</span></span> <span data-ttu-id="7f5e0-942">각 SAP NetWeaver 설치 스택에 대한 설치 차이점은 명시적으로 언급됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-942">Any installation differences for each SAP NetWeaver installation stack are explicitly mentioned.</span></span> <span data-ttu-id="7f5e0-943">다른 모든 부분은 동일하다고 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-943">You can assume that all other parts are the same.</span></span>  
>
>

### <span data-ttu-id="7f5e0-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> 고가용성 ASCS/SCS 인스턴스에 SAP 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-944"><a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Install SAP with a high-availability ASCS/SCS instance</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f5e0-945">DataKeeper 미러된 볼륨에 페이지 파일을 배치하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-945">Be sure not to place your page file on DataKeeper mirrored volumes.</span></span> <span data-ttu-id="7f5e0-946">DataKeeper는 미러된 볼륨을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-946">DataKeeper does not support mirrored volumes.</span></span> <span data-ttu-id="7f5e0-947">Azure Virtual Machines의 임시 드라이브 D에 페이지 파일을 둘 수 있습니다. 이것이 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-947">You can leave your page file on the temporary drive D of an Azure virtual machine, which is the default.</span></span> <span data-ttu-id="7f5e0-948">Windows 페이지 파일을 Azure 가상 컴퓨터의 D 드라이브로 이동하지 않은 경우 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-948">If it's not already there, move the Windows page file to drive D: of your Azure virtual machine.</span></span>
>
>

<span data-ttu-id="7f5e0-949">고가용성 ASCS/SCS 인스턴스에 SAP 설치는 다음과 같은 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-949">Installing SAP with a high-availability ASCS/SCS instance involves these tasks:</span></span>

- <span data-ttu-id="7f5e0-950">클러스터형 SAP ASCS/SCS 인스턴스의 가상 호스트 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="7f5e0-950">Creating a virtual host name for the clustered SAP ASCS/SCS instance</span></span>
- <span data-ttu-id="7f5e0-951">SAP 첫 번째 클러스터 노드 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-951">Installing the SAP first cluster node</span></span>
- <span data-ttu-id="7f5e0-952">ASCS/SCS 인스턴스의 SAP 프로필 수정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-952">Modifying the SAP profile of the ASCS/SCS instance</span></span>
- <span data-ttu-id="7f5e0-953">프로브 포트 추가</span><span class="sxs-lookup"><span data-stu-id="7f5e0-953">Adding a probe port</span></span>
- <span data-ttu-id="7f5e0-954">Windows 방화벽 프로브 포트 열기</span><span class="sxs-lookup"><span data-stu-id="7f5e0-954">Opening the Windows firewall probe port</span></span>

#### <span data-ttu-id="7f5e0-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> 클러스터형 SAP ASCS/SCS 인스턴스의 가상 호스트 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="7f5e0-955"><a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a> Create a virtual host name for the clustered SAP ASCS/SCS instance</span></span>

1.  <span data-ttu-id="7f5e0-956">Windows DNS 관리자에서 ASCS/SCS 인스턴스의 가상 호스트 이름에 대한 DNS 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-956">In the Windows DNS manager, create a DNS entry for the virtual host name of the ASCS/SCS instance.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7f5e0-957">ASCS/SCS 인스턴스의 가상 호스트 이름에 할당하는 IP 주소는 Azure Load Balancer에 할당한 IP 주소와 동일해야 합니다(**<*SID*>-lb-ascs**).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-957">The IP address that you assign to the virtual host name of the ASCS/SCS instance must be the same as the IP address that you assigned to Azure Load Balancer (**<*SID*>-lb-ascs**).</span></span>  
  >
  >

  <span data-ttu-id="7f5e0-958">가상 SAP ASCS/SCS 호스트 이름의 IP 주소(**pr1-ascs-sap**)는 Azure Load Balancer의 IP 주소(**pr1-lb-ascs**)와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-958">The IP address of the virtual SAP ASCS/SCS host name (**pr1-ascs-sap**) is the same as the IP address of Azure Load Balancer (**pr1-lb-ascs**).</span></span>

  ![그림 56: SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대한 DNS 항목 정의][sap-ha-guide-figure-3046]

  <span data-ttu-id="7f5e0-960">_**그림 56:** SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대한 DNS 항목 정의_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-960">_**Figure 56:** Define the DNS entry for the SAP ASCS/SCS cluster virtual name and TCP/IP address_</span></span>

2.  <span data-ttu-id="7f5e0-961">가상 호스트 이름에 할당된 IP 주소를 정의하려면 **DNS 관리자** > **도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-961">To define the IP address assigned to the virtual host name, select **DNS Manager** > **Domain**.</span></span>

  ![그림 57: SAP ASCS/SCS 클러스터 구성을 위한 새 가상 이름 및 TCP/IP 주소][sap-ha-guide-figure-3047]

  <span data-ttu-id="7f5e0-963">_**그림 57:** SAP ASCS/SCS 클러스터 구성을 위한 새 가상 이름 및 TCP/IP 주소_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-963">_**Figure 57:** New virtual name and TCP/IP address for SAP ASCS/SCS cluster configuration_</span></span>

#### <span data-ttu-id="7f5e0-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> SAP 첫 번째 클러스터 노드 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-964"><a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a> Install the SAP first cluster node</span></span>

1.  <span data-ttu-id="7f5e0-965">클러스터 노드 A에서 첫 번째 클러스터 노드 옵션을 실행합니다(예: **pr1-ascs-0** 호스트).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-965">Execute the first cluster node option on cluster node A. For example, on the **pr1-ascs-0** host.</span></span>
2.  <span data-ttu-id="7f5e0-966">Azure 내부 부하 분산 장치에 대한 기본 포트를 유지하려면 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-966">To keep the default ports for the Azure internal load balancer, select:</span></span>

  * <span data-ttu-id="7f5e0-967">**ABAP 시스템**: **ASCS** 인스턴스 번호 **00**</span><span class="sxs-lookup"><span data-stu-id="7f5e0-967">**ABAP system**: **ASCS** instance number **00**</span></span>
  * <span data-ttu-id="7f5e0-968">**Java 시스템**: **SCS** 인스턴스 번호 **01**</span><span class="sxs-lookup"><span data-stu-id="7f5e0-968">**Java system**: **SCS** instance number **01**</span></span>
  * <span data-ttu-id="7f5e0-969">**ABAP+Java 시스템**: **ASCS** 인스턴스 번호 **00** 및 **SCS** 인스턴스 번호 **01**</span><span class="sxs-lookup"><span data-stu-id="7f5e0-969">**ABAP+Java system**: **ASCS** instance number **00** and **SCS** instance number **01**</span></span>

  <span data-ttu-id="7f5e0-970">ABAP ASCS 인스턴스에는 00이 아닌 다른 인스턴스 번호, Java SCS 인스턴스에는 01을 사용하려면 먼저 [Azure 내부 부하 분산 장치의 기본 ASCS/SCS 부하 분산 규칙 변경][sap-ha-guide-8.9]에서 설명한 대로 Azure 내부 부하 분산 장치의 기본 부하 분산 규칙을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-970">To use instance numbers other than 00 for the ABAP ASCS instance and 01 for the Java SCS instance, first you need to change the Azure internal load balancer default load balancing rules, described in [Change the ASCS/SCS default load balancing rules for the Azure internal load balancer][sap-ha-guide-8.9].</span></span>

<span data-ttu-id="7f5e0-971">다음 몇 가지 작업은 표준 SAP 설치 설명서에서 설명되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-971">The next few tasks aren't described in the standard SAP installation documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-972">SAP 설치 설명서에는 첫 번째 ASCS/SCS 클러스터 노드를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-972">The SAP installation documentation describes how to install the first ASCS/SCS cluster node.</span></span>
>
>

#### <span data-ttu-id="7f5e0-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> ASCS/SCS 인스턴스의 SAP 프로필 수정</span><span class="sxs-lookup"><span data-stu-id="7f5e0-973"><a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a> Modify the SAP profile of the ASCS/SCS instance</span></span>

<span data-ttu-id="7f5e0-974">새 프로필 매개 변수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-974">You need to add a new profile parameter.</span></span> <span data-ttu-id="7f5e0-975">이 프로필 매개 변수는 연결이 너무 오랫동안 유휴 상태일 때 SAP 작업 프로세스와 큐에 넣기 서버 사이의 연결이 닫히지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-975">The profile parameter prevents connections between SAP work processes and the enqueue server from closing when they are idle for too long.</span></span> <span data-ttu-id="7f5e0-976">[SAP ASCS/SCS 인스턴스의 두 클러스터 노드에 대한 레지스트리 항목 추가][sap-ha-guide-8.11]에서 문제 시나리오를 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-976">We mentioned the problem scenario in [Add registry entries on both cluster nodes of the SAP ASCS/SCS instance][sap-ha-guide-8.11].</span></span> <span data-ttu-id="7f5e0-977">이 섹션에서는 몇 가지 기본 TCP/IP 연결 매개 변수에 대한 두 가지 변경 내용도 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-977">In that section, we also introduced two changes to some basic TCP/IP connection parameters.</span></span> <span data-ttu-id="7f5e0-978">두 번째 단계에서는 연결이 Azure 부하 부산 장치의 유휴 임계값에 도달하지 않게 `keep_alive` 신호를 보내도록 큐에 추가 서버를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-978">In a second step, you need to set the enqueue server to send a `keep_alive` signal so that the connections don't hit the Azure internal load balancer's idle threshold.</span></span>

<span data-ttu-id="7f5e0-979">ASCS/SCS 인스턴스의 SAP 프로필을 수정하려면:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-979">To modify the SAP profile of the ASCS/SCS instance:</span></span>

1.  <span data-ttu-id="7f5e0-980">SAP ASCS/SCS 인스턴스에 프로필에 이 프로필 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-980">Add this profile parameter to the SAP ASCS/SCS instance profile:</span></span>

  ```
  enque/encni/set_so_keepalive = true
  ```
  <span data-ttu-id="7f5e0-981">이 예제에서 경로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-981">In our example, the path is:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  <span data-ttu-id="7f5e0-982">예: SAP SCS 인스턴스 프로필 및 해당 경로</span><span class="sxs-lookup"><span data-stu-id="7f5e0-982">For example, to the SAP SCS instance profile and corresponding path:</span></span>

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  <span data-ttu-id="7f5e0-983">변경 내용을 적용하려면 SAP ASCS/SCS 인스턴스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-983">To apply the changes, restart the SAP ASCS /SCS instance.</span></span>

#### <span data-ttu-id="7f5e0-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> 프로브 포트 추가</span><span class="sxs-lookup"><span data-stu-id="7f5e0-984"><a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Add a probe port</span></span>

<span data-ttu-id="7f5e0-985">내부 부하 분산 장치의 프로브 기능을 사용하여 전체 클러스터 구성이 Azure Load Balancer에서 작동하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-985">Use the internal load balancer's probe functionality to make the entire cluster configuration work with Azure Load Balancer.</span></span> <span data-ttu-id="7f5e0-986">일반적으로 Azure 내부 부하 분산 장치는 참여하는 가상 컴퓨터 간에 동일하게 들어오는 작업 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-986">The Azure internal load balancer usually distributes the incoming workload equally between participating virtual machines.</span></span> <span data-ttu-id="7f5e0-987">그러나 하나의 인스턴스만 활성 상태가 되므로 일부 클러스터 구성에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-987">However, this won't work in some cluster configurations because only one instance is active.</span></span> <span data-ttu-id="7f5e0-988">다른 인스턴스는 수동 상태이므로 워크로드를 받아들일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-988">The other instance is passive and can’t accept any of the workload.</span></span> <span data-ttu-id="7f5e0-989">검색 기능은 Azure 내부 부하 분산 장치가 활성 인스턴스에만 작업을 할당할 때 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-989">A probe functionality helps when the Azure internal load balancer assigns work only to an active instance.</span></span> <span data-ttu-id="7f5e0-990">검색 기능을 사용하면 내부 부하 분산 장치는 활성 상태인 인스턴스를 감지한 후 해당 인스턴스만 워크로드 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-990">With the probe functionality, the internal load balancer can detect which instances are active, and then target only the instance with the workload.</span></span>

<span data-ttu-id="7f5e0-991">프로브 포트를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="7f5e0-991">To add a probe port:</span></span>

1.  <span data-ttu-id="7f5e0-992">다음 PowerShell 명령을 실행하여 현재 **ProbePort** 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-992">Check the current **ProbePort** setting by running the following PowerShell command.</span></span> <span data-ttu-id="7f5e0-993">이 명령은 클러스터 구성의 가상 컴퓨터 중 하나에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-993">Execute it from within one of the virtual machines in the cluster configuration.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  <span data-ttu-id="7f5e0-994">프로브 포트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-994">Define a probe port.</span></span> <span data-ttu-id="7f5e0-995">프로브 포트 기본값은 **0**입니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-995">The default probe port number is **0**.</span></span> <span data-ttu-id="7f5e0-996">예제에서는 **62000** 프로브 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-996">In our example, we use probe port **62000**.</span></span>

  ![그림 58: 기본적으로 0인 클러스터 구성 프로브 포트][sap-ha-guide-figure-3048]

  <span data-ttu-id="7f5e0-998">_**그림 58:** 기본 클러스터 구성 프로브 포트는 0_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-998">_**Figure 58:** The default cluster configuration probe port is 0_</span></span>

  <span data-ttu-id="7f5e0-999">포트 번호는 SAP Azure Resource Manager 템플릿에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-999">The port number is defined in SAP Azure Resource Manager templates.</span></span> <span data-ttu-id="7f5e0-1000">PowerShell에서 포트 번호를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1000">You can assign the port number in PowerShell.</span></span>

  <span data-ttu-id="7f5e0-1001">**SAP <*SID*> IP** 클러스터 리소스에 대한 새 ProbePort 값을 설정하려면 다음 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1001">To set a new ProbePort value for the **SAP <*SID*> IP** cluster resource, run the following PowerShell script.</span></span> <span data-ttu-id="7f5e0-1002">사용자 환경에 맞게 PowerShell 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1002">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="7f5e0-1003">스크립트가 실행된 후 변경 내용을 활성화하도록 SAP 클러스터 그룹을 다시 시작할 것인지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1003">After the script runs, you'll be prompted to restart the SAP cluster group to activate the changes.</span></span>

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

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
  Write-Host "Current probe port property of the SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting the new probe port property of the SAP cluster resource '$SAPIPresourceName' to '$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want to take restart SAP cluster role '$SAPClusterRoleName', to activate the changes (yes/no)?"

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

  <span data-ttu-id="7f5e0-1004">**SAP <*SID*>** 클러스터 역할을 온라인으로 전환한 후에 **ProbePort**가 새 값으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1004">After you bring the **SAP <*SID*>** cluster role online, verify that **ProbePort** is set to the new value.</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![그림 59: 새 값을 설정한 후 클러스터 포트 검색][sap-ha-guide-figure-3049]

  <span data-ttu-id="7f5e0-1006">_**그림 59:** 새 값을 설정한 후 클러스터 포트 검색_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1006">_**Figure 59:** Probe the cluster port after you set the new value_</span></span>

#### <span data-ttu-id="7f5e0-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Windows 방화벽 프로브 포트 열기</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1007"><a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a> Open the Windows firewall probe port</span></span>

<span data-ttu-id="7f5e0-1008">두 클러스터 노드에서 Windows 방화벽 프로브 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1008">You need to open a Windows firewall probe port on both cluster nodes.</span></span> <span data-ttu-id="7f5e0-1009">다음 스크립트를 사용하여 Windows 방화벽 프로브 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1009">Use the following script to open a Windows firewall probe port.</span></span> <span data-ttu-id="7f5e0-1010">사용자 환경에 맞게 PowerShell 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1010">Update the PowerShell variables for your environment.</span></span>

  ```PowerShell
  $ProbePort = 62000   # ProbePort of the Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

<span data-ttu-id="7f5e0-1011">**ProbePort**가 **62000**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1011">The **ProbePort** is set to **62000**.</span></span> <span data-ttu-id="7f5e0-1012">이제 **ascsha-dbas** 등의 다른 호스트에서 **\\\ascsha-clsap\sapmnt** 파일 공유에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1012">Now you can access the file share **\\\ascsha-clsap\sapmnt** from other hosts, such as from **ascsha-dbas**.</span></span>

### <span data-ttu-id="7f5e0-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> 데이터베이스 인스턴스 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1013"><a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a> Install the database instance</span></span>

<span data-ttu-id="7f5e0-1014">데이터베이스 인스턴스를 설치하려면 SAP 설치 설명서에 설명된 프로세스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1014">To install the database instance, follow the process described in the SAP installation documentation.</span></span>

### <span data-ttu-id="7f5e0-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> 두 번째 클러스터 노드 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1015"><a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a> Install the second cluster node</span></span>

<span data-ttu-id="7f5e0-1016">두 번째 클러스터 노드를 설치하려면 SAP 설치 가이드의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1016">To install the second cluster, follow the steps in the SAP installation guide.</span></span>

### <span data-ttu-id="7f5e0-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> SAP ERS Windows 서비스 인스턴스의 시작 유형 변경</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1017"><a name="094bc895-31d4-4471-91cc-1513b64e406a"></a> Change the start type of the SAP ERS Windows service instance</span></span>

<span data-ttu-id="7f5e0-1018">두 클러스터 노드에서 SAP ERS Windows 서비스의 시작 유형을 **자동(지연된 시작)**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1018">Change the start type of the SAP ERS Windows service to **Automatic (Delayed Start)** on both cluster nodes.</span></span>

![그림 60: SAP ERS 인스턴스의 서비스 유형을 지연된 자동으로 변경][sap-ha-guide-figure-3050]

<span data-ttu-id="7f5e0-1020">_**그림 60:** SAP ERS 인스턴스의 서비스 유형을 지연된 자동으로 변경_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1020">_**Figure 60:** Change the service type for the SAP ERS instance to delayed automatic_</span></span>

### <span data-ttu-id="7f5e0-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> SAP 기본 응용 프로그램 서버 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1021"><a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a> Install the SAP Primary Application Server</span></span>

<span data-ttu-id="7f5e0-1022">PAS(기본 응용 프로그램 서버)를 호스트하도록 지정한 가상 컴퓨터에 PAS 인스턴스 <*SID*>-di-0를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1022">Install the Primary Application Server (PAS) instance <*SID*>-di-0 on the virtual machine that you've designated to host the PAS.</span></span> <span data-ttu-id="7f5e0-1023">Azure 또는 DataKeeper 관련 설정과는 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1023">There are no dependencies on Azure or DataKeeper-specific settings.</span></span>

### <span data-ttu-id="7f5e0-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> SAP 추가 응용 프로그램 서버 설치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1024"><a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a> Install the SAP Additional Application Server</span></span>

<span data-ttu-id="7f5e0-1025">SAP 응용 프로그램 서버 인스턴스를 호스트하도록 지정한 모든 가상 컴퓨터에 SAP AAS(추가 응용 프로그램 서버)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1025">Install an SAP Additional Application Server (AAS) on all the virtual machines that you've designated to host an SAP Application Server instance.</span></span> <span data-ttu-id="7f5e0-1026"><*SID*>-di-1 ~ <*SID*>-di-&lt;n&gt;을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1026">For example, on <*SID*>-di-1 to <*SID*>-di-&lt;n&gt;.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5e0-1027">이는 고가용성 SAP NetWeaver 시스템의 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1027">This finishes the installation of a high-availability SAP NetWeaver system.</span></span> <span data-ttu-id="7f5e0-1028">다음으로 장애 조치 테스트를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1028">Next, proceed with failover testing.</span></span>
>


## <span data-ttu-id="7f5e0-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 복제 테스트</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1029"><a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a> Test the SAP ASCS/SCS instance failover and SIOS replication</span></span>
<span data-ttu-id="7f5e0-1030">장애 조치 클러스터 관리자 및 SIOS DataKeeper 관리 및 구성 도구를 사용하여 SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 디스크 복제를 쉽게 테스트하고 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1030">It's easy to test and monitor an SAP ASCS/SCS instance failover and SIOS disk replication by using Failover Cluster Manager and the SIOS DataKeeper Management and Configuration tool.</span></span>

### <span data-ttu-id="7f5e0-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS 인스턴스가 클러스터 노드 A에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1031"><a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS instance is running on cluster node A</span></span>

<span data-ttu-id="7f5e0-1032">**SAP PR1** 클러스터 그룹이 클러스터 노드 A(예: **pr1-ascs-0**)에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1032">The **SAP PR1** cluster group is running on cluster node A. For example, on **pr1-ascs-0**.</span></span> <span data-ttu-id="7f5e0-1033">**SAP PR1** 클러스터 그룹에 속하고 ASCS/SCS 인스턴스에서 사용하는 S 공유 디스크 드라이브를 클러스터 노드 A에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1033">Assign the shared disk drive S, which is part of the **SAP PR1** cluster group, and which the ASCS/SCS instance uses, to cluster node A.</span></span>

![그림 61: 장애 조치 클러스터 관리자 - 클러스터 노드 A에서 실행 중인 SAP <SID> 클러스터 그룹][sap-ha-guide-figure-5000]

<span data-ttu-id="7f5e0-1035">_**그림 61:** 장애 조치 클러스터 관리자 - 클러스터 노드 A에서 실행 중인 SAP <*SID*> 클러스터 그룹_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1035">_**Figure 61:** Failover Cluster Manager: The SAP <*SID*> cluster group is running on cluster node A_</span></span>

<span data-ttu-id="7f5e0-1036">SIOS DataKeeper 관리 및 구성 도구에서 공유 디스크 데이터가 클러스터 노드 A의 S 원본 볼륨 드라이브에서 클러스터 노드 B의 S 대상 볼륨 드라이브로 동기식으로 복제되는 것을 확인할 수 있습니다(예: **pr1-ascs-0 [10.0.0.40]**에서 **pr1-ascs-1 [10.0.0.41]**로 복제됨).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1036">In the SIOS DataKeeper Management and Configuration tool, you can see that the shared disk data is synchronously replicated from the source volume drive S on cluster node A to the target volume drive S on cluster node B. For example, it's replicated from **pr1-ascs-0 [10.0.0.40]** to **pr1-ascs-1 [10.0.0.41]**.</span></span>

![그림 62: SIOS DataKeeper에서 클러스터 노드 A로부터 클러스터 노드 B에 로컬 볼륨 복제][sap-ha-guide-figure-5001]

<span data-ttu-id="7f5e0-1038">_**그림 62:** SIOS DataKeeper에서 클러스터 노드 A로부터 클러스터 노드 B에 로컬 볼륨 복제_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1038">_**Figure 62:** In SIOS DataKeeper, replicate the local volume from cluster node A to cluster node B_</span></span>

### <span data-ttu-id="7f5e0-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> 노드 A에서 노드 B로 장애 조치</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1039"><a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a> Failover from node A to node B</span></span>

1.  <span data-ttu-id="7f5e0-1040">이러한 옵션 중 하나를 선택하여 클러스터 노드 A에서 클러스터 노드 B로 SAP <*SID*> 클러스터 그룹의 장애 조치를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1040">Choose one of these options to initiate a failover of the SAP <*SID*> cluster group from cluster node A to cluster node B:</span></span>
  - <span data-ttu-id="7f5e0-1041">장애 조치(failover) 클러스터 관리자 사용</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1041">Use Failover Cluster Manager</span></span>  
  - <span data-ttu-id="7f5e0-1042">장애 조치 클러스터 PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1042">Use Failover Cluster PowerShell</span></span>

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  <span data-ttu-id="7f5e0-1043">Windows 게스트 운영 체제 내에서 클러스터 노드 A를 다시 시작합니다(노드 A에서 노드 B로의 SAP <*SID*> 클러스터 그룹의 자동 장애 조치 시작).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1043">Restart cluster node A within the Windows guest operating system (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
3.  <span data-ttu-id="7f5e0-1044">Azure Portal에서 클러스터 노드 A를 다시 시작합니다(노드 A에서 노드 B로의 SAP <*SID*> 클러스터 그룹의 자동 장애 조치 시작).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1044">Restart cluster node A from the Azure portal (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>  
4.  <span data-ttu-id="7f5e0-1045">Azure PowerShell을 사용하여 클러스터 노드 A를 다시 시작합니다(노드 A에서 노드 B로의 SAP <*SID*> 클러스터 그룹의 자동 장애 조치 시작).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1045">Restart cluster node A by using Azure PowerShell (this initiates an automatic failover of the SAP <*SID*> cluster group from node A to node B).</span></span>

  <span data-ttu-id="7f5e0-1046">장애 조치 후 SAP <*SID*> 클러스터 그룹이 클러스터 노드 B(예: **pr1-ascs-1**에서 실행 중)에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1046">After failover, the SAP <*SID*> cluster group is running on cluster node B. For example, it's running on **pr1-ascs-1**.</span></span>

  ![그림 63: 장애 조치 클러스터 관리자: 클러스터 노드 B에서 실행 중인 SAP <SID> 클러스터 그룹][sap-ha-guide-figure-5002]

  <span data-ttu-id="7f5e0-1048">_**그림 63**: 장애 조치 클러스터 관리자: 클러스터 노드 B에서 실행 중인 SAP <*SID*> 클러스터 그룹_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1048">_**Figure 63**: In Failover Cluster Manager, the SAP <*SID*> cluster group is running on cluster node B_</span></span>

  <span data-ttu-id="7f5e0-1049">이제 공유 디스크가 클러스터 노드 B에 탑재됩니다. SIOS DataKeeper에서 데이터를 클러스터 노드 B의 S 소스 볼륨 드라이브에서 클러스터 노드 A의 S 대상 볼륨 드라이브로 복제합니다(예: **pr1-ascs-1 [10.0.0.41]**에서 **pr1-ascs-0 [10.0.0.40]**으로 복제).</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1049">The shared disk is now mounted on cluster node B. SIOS DataKeeper is replicating data from source volume drive S on cluster node B to target volume drive S on cluster node A. For example, it's replicating from **pr1-ascs-1 [10.0.0.41]** to **pr1-ascs-0 [10.0.0.40]**.</span></span>

  ![그림 64: SIOS DataKeeper에서 클러스터 노드 B로부터 클러스터 노드 A에 로컬 볼륨 복제][sap-ha-guide-figure-5003]

  <span data-ttu-id="7f5e0-1051">_**그림 64:** SIOS DataKeeper에서 클러스터 노드 B로부터 클러스터 노드 A에 로컬 볼륨 복제_</span><span class="sxs-lookup"><span data-stu-id="7f5e0-1051">_**Figure 64:** SIOS DataKeeper replicates the local volume from cluster node B to cluster node A_</span></span>
