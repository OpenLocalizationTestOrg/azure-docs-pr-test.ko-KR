---
title: "Azure에서 SAP SID 다중 구성은 aaaCreate | Microsoft Docs"
description: "Windows 가상 컴퓨터에 가이드 toohigh 가용성 SAP NetWeaver 다중 SID 구성"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="6d02b-103">SAP NetWeaver 다중 SID 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="6d02b-103">Create an SAP NetWeaver multi-SID configuration</span></span>

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

<span data-ttu-id="6d02b-104">2016년 9월에 Microsoft는 Azure 내부 부하 분산 장치를 사용하여 여러 가상 IP 주소를 관리할 수 있는 기능을 릴리스했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="6d02b-105">이 기능은 hello Azure 외부 부하 분산 장치에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="6d02b-106">SAP 배포를 설정한 경우 사용할 수 있습니다 Windows 클러스터 구성에는 내부 부하 분산 장치 toocreate SAP ASCS/SCS에 대 한 hello에 설명 된 대로 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="6d02b-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="6d02b-107">이 문서는 toomove 단일 ASCS/SCS 설치 tooan SAP SID 다중 구성에서 추가 SAP ASCS/SCS를 설치 하 여 기존 Windows Server 장애 조치 클러스터링 (WSFC) 클러스터에 인스턴스를 클러스터링 하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="6d02b-108">이 프로세스가 완료되면 SAP 다중 SID 클러스터가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6d02b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d02b-109">Prerequisites</span></span>
<span data-ttu-id="6d02b-110">이미 구성한 한 SAP ASCS/SCS 인스턴스에 사용 되는 WSFC 클러스터 hello에 설명 된 대로 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드] [ sap-ha-guide] 이 다이어그램에 나와 있는 것 처럼 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![고가용성 SAP ASCS/SCS 인스턴스][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="6d02b-112">대상 아키텍처</span><span class="sxs-lookup"><span data-stu-id="6d02b-112">Target architecture</span></span>

<span data-ttu-id="6d02b-113">hello ´ ֲ ° hello에 tooinstall 여러 SAP ABAP ASCS 또는 SAP Java SCS 클러스터 된 인스턴스의 동일한 WSFC 클러스터에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Azure에서 여러 SAP ASCS/SCS 클러스터링된 인스턴스][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="6d02b-115">각 Azure 내부 부하 분산 장치에 대 한 프런트 엔드 개인 ip 제한 toohello 수가입니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="6d02b-116">한 WSFC 클러스터에 있는 SAP ASCS/SCS 인스턴스의 hello 최대 수는 각 Azure 내부 부하 분산 장치에 대 한 프런트 엔드 개인 Ip의 최대 수를 같은 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="6d02b-117">부하 분산 장치 제한에 대한 자세한 내용은 [네트워킹 제한 - Azure Resource Manager][networking-limits-azure-resource-manager]에서 “부하 분산 장치당 개인 프런트 엔드 IP”를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d02b-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="6d02b-118">두 개의 고가용성 SAP 시스템과 hello 전체 가로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![두 개의 SAP 시스템 SID를 포함한 SAP 고가용성 다중 SID 설치 프로그램][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="6d02b-120">hello 설치 hello 다음 조건을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="6d02b-121">hello SAP ASCS/SCS 인스턴스를 공유 해야 hello 동일한 WSFC 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="6d02b-122">각 DBMS SID에는 해당하는 고유한 전용 WSFC 클러스터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="6d02b-123">Tooone SAP 시스템 SID 속해 있는 SAP 응용 프로그램 서버에 자체 전용된 Vm 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="6d02b-124">Hello 인프라 준비</span><span class="sxs-lookup"><span data-stu-id="6d02b-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="6d02b-125">tooprepare 인프라에 매개 변수 뒤 hello로 추가 SAP ASCS/SCS 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="6d02b-126">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="6d02b-126">Parameter name</span></span> | <span data-ttu-id="6d02b-127">값</span><span class="sxs-lookup"><span data-stu-id="6d02b-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d02b-128">SAP ASCS/SCS SID</span><span class="sxs-lookup"><span data-stu-id="6d02b-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="6d02b-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="6d02b-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="6d02b-130">SAP DBMS 내부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="6d02b-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="6d02b-131">PR5</span><span class="sxs-lookup"><span data-stu-id="6d02b-131">PR5</span></span> |
| <span data-ttu-id="6d02b-132">SAP 가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="6d02b-132">SAP virtual host name</span></span> | <span data-ttu-id="6d02b-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="6d02b-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="6d02b-134">SAP ASCS/SCS 가상 호스트 IP 주소(추가 Azure Load Balancer IP 주소)</span><span class="sxs-lookup"><span data-stu-id="6d02b-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="6d02b-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="6d02b-135">10.0.0.50</span></span> |
| <span data-ttu-id="6d02b-136">SAP ASCS/SCS 인스턴스 번호</span><span class="sxs-lookup"><span data-stu-id="6d02b-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="6d02b-137">50</span><span class="sxs-lookup"><span data-stu-id="6d02b-137">50</span></span> |
| <span data-ttu-id="6d02b-138">추가 SAP ASCS/SCS 인스턴스의 ILB 프로브 포트</span><span class="sxs-lookup"><span data-stu-id="6d02b-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="6d02b-139">62350</span><span class="sxs-lookup"><span data-stu-id="6d02b-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="6d02b-140">SAP ASCS/SCS 클러스터 인스턴스의 경우 각 IP 주소에는 고유한 프로브 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="6d02b-141">예를 들어 Azure 내부 부하 분산 장치에 있는 하나의 IP 주소가 프로브 포트 62300을 사용하는 경우 해당 부하 분산 장치의 다른 IP 주소는 프로브 포트 62300을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="6d02b-142">프로브 포트 62300이 이미 예약되어 있으므로 여기서는 프로브 포트 62350을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="6d02b-143">두 개의 노드가 있는 hello 기존 WSFC 클러스터의 추가 SAP ASCS/SCS 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="6d02b-144">가상 컴퓨터 역할</span><span class="sxs-lookup"><span data-stu-id="6d02b-144">Virtual machine role</span></span> | <span data-ttu-id="6d02b-145">가상 컴퓨터 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="6d02b-145">Virtual machine host name</span></span> | <span data-ttu-id="6d02b-146">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="6d02b-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d02b-147">ASCS/SCS 인스턴스의 첫 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="6d02b-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="6d02b-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="6d02b-148">pr1-ascs-0</span></span> |<span data-ttu-id="6d02b-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="6d02b-149">10.0.0.10</span></span> |
| <span data-ttu-id="6d02b-150">ASCS/SCS 인스턴스의 두 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="6d02b-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="6d02b-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="6d02b-151">pr1-ascs-1</span></span> |<span data-ttu-id="6d02b-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="6d02b-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="6d02b-153">Hello DNS 서버에서 클러스터 된 hello SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들기</span><span class="sxs-lookup"><span data-stu-id="6d02b-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="6d02b-154">매개 변수 뒤 hello를 사용 하 여 hello ASCS/SCS 인스턴스의 hello 가상 호스트 이름에 대 한 DNS 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="6d02b-155">새 SAP ASCS/SCS 가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="6d02b-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="6d02b-156">연결된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="6d02b-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="6d02b-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="6d02b-157">pr5-sap-cl</span></span> |<span data-ttu-id="6d02b-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="6d02b-158">10.0.0.50</span></span> |

<span data-ttu-id="6d02b-159">다음 스크린 샷에서 hello와 같이 hello 새 호스트 이름과 IP 주소가 hello DNS 관리자에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![Hello를 강조 표시 하는 DNS 관리자 목록 정의 hello 새 SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대 한 DNS 항목][sap-ha-guide-figure-6004]

<span data-ttu-id="6d02b-161">DNS 항목을 만드는 hello 절차도 주 hello에 자세히 설명 되어 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-9.1.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="6d02b-162">hello hello 추가 ASCS/SCS 인스턴스의 toohello 가상 호스트 이름이 할당 하는 새 IP 주소 해야 수 hello hello toohello SAP Azure 부하 분산 장치를 할당 하는 새 IP 주소와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="6d02b-163">이 시나리오에서 hello IP 주소가 10.0.0.50 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="6d02b-164">PowerShell을 사용 하 여에서 IP 주소 tooan 기존 Azure 내부 부하 분산 장치 추가</span><span class="sxs-lookup"><span data-stu-id="6d02b-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="6d02b-165">SAP ASCS/SCS 인스턴스가 둘 이상 toocreate hello 동일한 WSFC 클러스터의 경우 기존 Azure 내부 부하 분산 장치는 IP 주소 tooan tooadd PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="6d02b-166">각 IP 주소에는 고유한 부하 분산 규칙, 프로브 포트, 프런트 엔드 IP 풀 및 백 엔드 풀이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="6d02b-167">hello 다음 스크립트 추가 새 IP 주소 tooan 기존 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="6d02b-168">사용자 환경에 대 한 hello PowerShell 변수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="6d02b-169">hello 스크립트는 모든 SAP ASCS/SCS 포트에 대 한 모든 필요한 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="6d02b-170">Hello 스크립트를 실행 한 후 hello 스크린 샷 뒤에 표시 된 대로 Azure 포털을 hello hello에 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Hello Azure 포털에서에서 새 프런트 엔드 IP 풀][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="6d02b-172">디스크 toocluster 컴퓨터를 추가 하 고 hello SIOS 클러스터 공유 디스크를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="6d02b-173">각 추가 SAP ASCS/SCS 인스턴스에 새 클러스터 공유 디스크를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="6d02b-174">Windows Server 2012 r 2에서 현재 사용 중인 hello WSFC 클러스터 공유 디스크는 hello SIOS DataKeeper 소프트웨어 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="6d02b-175">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-175">Do hello following:</span></span>
1. <span data-ttu-id="6d02b-176">더 추가 하의 디스크 또는 디스크 hello 같은 크기 (필요한 toostripe) tooeach hello의 클러스터 노드와 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="6d02b-177">SIOS DataKeeper를 사용하여 저장소 복제를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="6d02b-178">이 절차는 WSFC 클러스터 컴퓨터 hello에 SIOS DataKeeper를 이미 설치 있음을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="6d02b-179">설치 된 경우 이제 hello 컴퓨터 간의 복제를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="6d02b-180">hello 프로세스 주 hello에 자세히 설명 되어 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-8.12.3.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![Hello 새 SAP ASCS/SCS 공유 디스크에 대 한 미러링을 동기 DataKeeper][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="6d02b-182">SAP 응용 프로그램 서버 및 DBMS 클러스터에 대한 VM 배포</span><span class="sxs-lookup"><span data-stu-id="6d02b-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="6d02b-183">두 번째 SAP 시스템 hello에 대 한 toocomplete hello 인프라 준비 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="6d02b-184">SAP 응용 프로그램 서버에 대한 전용 VM을 배포하고 고유한 전용 가용성 그룹에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="6d02b-185">DBMS 클러스터에 대한 전용 VM을 배포하고 고유한 전용 가용성 그룹에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="6d02b-186">Hello 두 번째 SID2의 SAP NetWeaver 시스템을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="6d02b-187">두 번째 SAP SID2 시스템 설치의 전체 과정 hello 주 hello에 설명 되어 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-9]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="6d02b-188">hello 고급 절차는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="6d02b-189">[Hello SAP 첫 번째 클러스터 노드 설치][sap-ha-guide-9.1.2]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="6d02b-190">이 단계에서는 설치 하는 SAP hello의 가용성이 높은 ASCS/SCS 인스턴스에서 **기존 WSFC 클러스터 노드 1**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="6d02b-191">[Hello ASCS/SCS 인스턴스의 hello SAP 프로필 수정][sap-ha-guide-9.1.3]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="6d02b-192">[프로브 포트 구성][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="6d02b-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="6d02b-193">이 단계에서는 PowerShell을 사용하여 SAP 클러스터 리소스 SAP-SID2-IP 프로브 포트를 구성하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="6d02b-194">Hello SAP ASCS/SCS 클러스터 노드 중 하나에서이 구성을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="6d02b-195">[Hello 데이터베이스 인스턴스 설치] [sap-ha-가이드-9.2].</span><span class="sxs-lookup"><span data-stu-id="6d02b-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="6d02b-196">이 단계에서는 전용 WSFC 클러스터에 DBMS를 설치하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="6d02b-197">[Hello 두 번째 클러스터 노드에 설치] [sap-ha-가이드-9.3].</span><span class="sxs-lookup"><span data-stu-id="6d02b-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="6d02b-198">이 단계에서는 hello 기존 WSFC 클러스터 노드 2의 가용성이 높은 ASCS/SCS 인스턴스에서 SAP을 설치 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="6d02b-199">SAP ASCS/SCS 인스턴스와 ProbePort hello에 대 한 Windows 방화벽 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="6d02b-200">SAP ASCS/SCS 인스턴스에 사용되는 두 클러스터 노드에서 SAP ASCS/SCS에서 사용하는 모든 Windows 방화벽 포트를 열고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="6d02b-201">이러한 포트는 hello에 나타나지 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-8.8]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="6d02b-202">Hello Azure 내부 부하 분산 장치 프로브 포트에 62350 시나리오에서 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="6d02b-203">[Hello SAP 호출자 Windows 서비스 인스턴스의 hello 시작 유형을 변경][sap-ha-guide-9.4]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="6d02b-204">[Hello SAP 기본 응용 프로그램 서버 설치] [ sap-ha-guide-9.5] 새 hello에 VM 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="6d02b-205">[Hello SAP 추가 응용 프로그램 서버 설치] [ sap-ha-guide-9.6] 새 hello에 VM 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="6d02b-206">[테스트 hello SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 복제][sap-ha-guide-10]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d02b-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d02b-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d02b-207">Next steps</span></span>

- <span data-ttu-id="6d02b-208">[네트워킹 제한: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="6d02b-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="6d02b-209">[Azure Load Balancer에 대한 다중 VIP][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="6d02b-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="6d02b-210">[Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="6d02b-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
