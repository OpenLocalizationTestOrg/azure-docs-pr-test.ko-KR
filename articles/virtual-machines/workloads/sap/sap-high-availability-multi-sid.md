---
title: "Azure에서 SAP 다중 SID 구성 만들기 | Microsoft Docs"
description: "Windows 가상 컴퓨터의 고가용성 SAP NetWeaver 다중 SID 구성 가이드"
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
ms.openlocfilehash: b48df78df9f53ac7bf0804f55a8d36a2fe2f86b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="5fc10-103">SAP NetWeaver 다중 SID 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="5fc10-103">Create an SAP NetWeaver multi-SID configuration</span></span>

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

<span data-ttu-id="5fc10-104">2016년 9월에 Microsoft는 Azure 내부 부하 분산 장치를 사용하여 여러 가상 IP 주소를 관리할 수 있는 기능을 릴리스했습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="5fc10-105">이 기능은 Azure 외부 부하 분산 장치에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-105">This functionality already exists in the Azure external load balancer.</span></span>

<span data-ttu-id="5fc10-106">SAP 배포가 있는 경우 [Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide]에 설명된 대로 내부 부하 분산 장치를 사용하여 SAP ASCS/SCS에 대한 Windows 클러스터 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-106">If you have an SAP deployment, you can use an internal load balancer to create a Windows cluster configuration for SAP ASCS/SCS, as documented in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="5fc10-107">이 문서에서는 추가 SAP ASCS/SCS 클러스터링된 인스턴스를 기존 WSFC(Windows Server 장애 조치 클러스터링) 클러스터에 설치하여 단일 ASCS/SCS 설치에서 SAP 다중 SID 구성으로 이동하는 방법을 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-107">This article focuses on how to move from a single ASCS/SCS installation to an SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="5fc10-108">이 프로세스가 완료되면 SAP 다중 SID 클러스터가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5fc10-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5fc10-109">Prerequisites</span></span>
<span data-ttu-id="5fc10-110">[Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide]에서 설명되고 이 다이어그램에 표시된 대로 하나의 SAP ASCS/SCS 인스턴스에 사용되는 WSFC 클러스터를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![고가용성 SAP ASCS/SCS 인스턴스][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="5fc10-112">대상 아키텍처</span><span class="sxs-lookup"><span data-stu-id="5fc10-112">Target architecture</span></span>

<span data-ttu-id="5fc10-113">목적은 여기에서 설명한 것처럼 동일한 WSAFC 클러스터에서 여러 SAP ABAP ASCS 또는 SAP Java SCS 클러스터링된 인스턴스를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-113">The goal is to install multiple SAP ABAP ASCS or SAP Java SCS clustered instances in the same WSFC cluster, as illustrated here:</span></span>

![Azure에서 여러 SAP ASCS/SCS 클러스터링된 인스턴스][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="5fc10-115">각 Azure 내부 부하 분산 장치에 대한 개인 프런트 엔드 IP의 수에 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-115">There is a limit to the number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="5fc10-116">하나의 WSFC 클러스터에서 SAP ASCS/SCS 인스턴스의 최대수는 각 Azure 내부 부하 분산 장치에 대한 개인 프런트 엔드 IP의 최대수와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-116">The maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal to the maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="5fc10-117">부하 분산 장치 제한에 대한 자세한 내용은 [네트워킹 제한 - Azure Resource Manager][networking-limits-azure-resource-manager]에서 “부하 분산 장치당 개인 프런트 엔드 IP”를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fc10-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="5fc10-118">두 가지 고가용성 SAP 시스템을 포함한 전체 그림은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-118">The complete landscape with two high-availability SAP systems would look like this:</span></span>

![두 개의 SAP 시스템 SID를 포함한 SAP 고가용성 다중 SID 설치 프로그램][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="5fc10-120">설치 프로그램은 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-120">The setup must meet the following conditions:</span></span>
> - <span data-ttu-id="5fc10-121">SAP ASCS/SCS 인스턴스는 동일한 WSFC 클러스터를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-121">The SAP ASCS/SCS instances must share the same WSFC cluster.</span></span>
> - <span data-ttu-id="5fc10-122">각 DBMS SID에는 해당하는 고유한 전용 WSFC 클러스터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="5fc10-123">하나의 SAP 시스템 SID에 속하는 SAP 응용 프로그램 서버에는 고유한 전용 VM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-123">SAP application servers that belong to one SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-the-infrastructure"></a><span data-ttu-id="5fc10-124">인프라 준비</span><span class="sxs-lookup"><span data-stu-id="5fc10-124">Prepare the infrastructure</span></span>
<span data-ttu-id="5fc10-125">인프라를 준비하기 위해 다음 매개 변수를 사용하여 추가 SAP ASCS/SCS 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-125">To prepare your infrastructure, you can install an additional SAP ASCS/SCS instance with the following parameters:</span></span>

| <span data-ttu-id="5fc10-126">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="5fc10-126">Parameter name</span></span> | <span data-ttu-id="5fc10-127">값</span><span class="sxs-lookup"><span data-stu-id="5fc10-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fc10-128">SAP ASCS/SCS SID</span><span class="sxs-lookup"><span data-stu-id="5fc10-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="5fc10-129">pr1-lb-ascs</span><span class="sxs-lookup"><span data-stu-id="5fc10-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="5fc10-130">SAP DBMS 내부 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="5fc10-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="5fc10-131">PR5</span><span class="sxs-lookup"><span data-stu-id="5fc10-131">PR5</span></span> |
| <span data-ttu-id="5fc10-132">SAP 가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="5fc10-132">SAP virtual host name</span></span> | <span data-ttu-id="5fc10-133">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="5fc10-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="5fc10-134">SAP ASCS/SCS 가상 호스트 IP 주소(추가 Azure Load Balancer IP 주소)</span><span class="sxs-lookup"><span data-stu-id="5fc10-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="5fc10-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="5fc10-135">10.0.0.50</span></span> |
| <span data-ttu-id="5fc10-136">SAP ASCS/SCS 인스턴스 번호</span><span class="sxs-lookup"><span data-stu-id="5fc10-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="5fc10-137">50</span><span class="sxs-lookup"><span data-stu-id="5fc10-137">50</span></span> |
| <span data-ttu-id="5fc10-138">추가 SAP ASCS/SCS 인스턴스의 ILB 프로브 포트</span><span class="sxs-lookup"><span data-stu-id="5fc10-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="5fc10-139">62350</span><span class="sxs-lookup"><span data-stu-id="5fc10-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="5fc10-140">SAP ASCS/SCS 클러스터 인스턴스의 경우 각 IP 주소에는 고유한 프로브 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="5fc10-141">예를 들어 Azure 내부 부하 분산 장치에 있는 하나의 IP 주소가 프로브 포트 62300을 사용하는 경우 해당 부하 분산 장치의 다른 IP 주소는 프로브 포트 62300을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="5fc10-142">프로브 포트 62300이 이미 예약되어 있으므로 여기서는 프로브 포트 62350을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="5fc10-143">두 개의 노드를 포함한 기존 WSFC 클러스터에서 추가 SAP ASCS/SCS 인스턴스를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-143">You can install additional SAP ASCS/SCS instances in the existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="5fc10-144">가상 컴퓨터 역할</span><span class="sxs-lookup"><span data-stu-id="5fc10-144">Virtual machine role</span></span> | <span data-ttu-id="5fc10-145">가상 컴퓨터 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="5fc10-145">Virtual machine host name</span></span> | <span data-ttu-id="5fc10-146">고정 IP 주소</span><span class="sxs-lookup"><span data-stu-id="5fc10-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5fc10-147">ASCS/SCS 인스턴스의 첫 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="5fc10-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5fc10-148">pr1-ascs-0</span><span class="sxs-lookup"><span data-stu-id="5fc10-148">pr1-ascs-0</span></span> |<span data-ttu-id="5fc10-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="5fc10-149">10.0.0.10</span></span> |
| <span data-ttu-id="5fc10-150">ASCS/SCS 인스턴스의 두 번째 클러스터 노드</span><span class="sxs-lookup"><span data-stu-id="5fc10-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="5fc10-151">pr1-ascs-1</span><span class="sxs-lookup"><span data-stu-id="5fc10-151">pr1-ascs-1</span></span> |<span data-ttu-id="5fc10-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="5fc10-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-the-clustered-sap-ascsscs-instance-on-the-dns-server"></a><span data-ttu-id="5fc10-153">DNS 서버에서 클러스터형 SAP ASCS/SCS 인스턴스의 가상 호스트 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="5fc10-153">Create a virtual host name for the clustered SAP ASCS/SCS instance on the DNS server</span></span>

<span data-ttu-id="5fc10-154">다음 매개 변수를 사용하여 ASCS/SCS 인스턴스의 가상 호스트 이름에 대한 DNS 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-154">You can create a DNS entry for the virtual host name of the ASCS/SCS instance by using the following parameters:</span></span>

| <span data-ttu-id="5fc10-155">새 SAP ASCS/SCS 가상 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="5fc10-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="5fc10-156">연결된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="5fc10-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="5fc10-157">pr5-sap-cl</span><span class="sxs-lookup"><span data-stu-id="5fc10-157">pr5-sap-cl</span></span> |<span data-ttu-id="5fc10-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="5fc10-158">10.0.0.50</span></span> |

<span data-ttu-id="5fc10-159">새 호스트 이름 및 IP 주소는 다음 스크린샷에 표시된 것처럼 DNS 관리자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-159">The new host name and IP address are displayed in the DNS Manager, as shown in the following screenshot:</span></span>

![새로운 SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대한 정의된 DNS 항목을 강조 표시는 DNS 관리자 목록][sap-ha-guide-figure-6004]

<span data-ttu-id="5fc10-161">DNS 항목을 만드는 절차는 기본 [Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide-9.1.1]에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-161">The procedure for creating a DNS entry is also described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="5fc10-162">추가 ASCS/SCS 인스턴스의 가상 호스트 이름에 할당하는 새 IP 주소는 SAP Azure Load Balancer에 할당한 새 IP 주소와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-162">The new IP address that you assign to the virtual host name of the additional ASCS/SCS instance must be the same as the new IP address that you assigned to the SAP Azure load balancer.</span></span>
>
><span data-ttu-id="5fc10-163">이 시나리오에서 IP 주소는 10.0.0.50입니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-163">In our scenario, the IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-to-an-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="5fc10-164">PowerShell을 사용하여 기존 Azure 내부 부하 분산 장치에 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="5fc10-164">Add an IP address to an existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="5fc10-165">동일한 WSFC 클러스터에서 둘 이상의 SAP ASCS/SCS 인스턴스를 만들려면 PowerShell을 사용하여 IP 주소를 기존 Azure 내부 부하 분산 장치에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-165">To create more than one SAP ASCS/SCS instance in the same WSFC cluster, use PowerShell to add an IP address to an existing Azure internal load balancer.</span></span> <span data-ttu-id="5fc10-166">각 IP 주소에는 고유한 부하 분산 규칙, 프로브 포트, 프런트 엔드 IP 풀 및 백 엔드 풀이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="5fc10-167">다음 스크립트는 기존 부하 분산 장치에 새 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-167">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="5fc10-168">사용자 환경에 맞게 PowerShell 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-168">Update the PowerShell variables for your environment.</span></span> <span data-ttu-id="5fc10-169">스크립트는 모든 SAP ASCS /SCS 포트에 필요한 모든 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-169">The script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

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

# Get the Azure VNet and subnet
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

# Assign VM NICs to backend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of the '$VMName' VM to the backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for the ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for the port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' to the internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="5fc10-170">스크립트를 실행한 후 다음 스크린샷에 표시된 것처럼 결과가 Azure Portal에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-170">After the script has run, the results are displayed in the Azure portal, as shown in the following screenshot:</span></span>

![Azure Portal에서 새 프런트 엔드 IP 풀][sap-ha-guide-figure-6005]

### <a name="add-disks-to-cluster-machines-and-configure-the-sios-cluster-share-disk"></a><span data-ttu-id="5fc10-172">클러스터 컴퓨터에 디스크 추가 및 SIOS 클러스터 공유 디스크 구성</span><span class="sxs-lookup"><span data-stu-id="5fc10-172">Add disks to cluster machines, and configure the SIOS cluster share disk</span></span>

<span data-ttu-id="5fc10-173">각 추가 SAP ASCS/SCS 인스턴스에 새 클러스터 공유 디스크를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="5fc10-174">Windows Server 2012 R2의 경우 현재 사용 중인 WSFC 클러스터 공유 디스크는 SIOS DataKeeper 소프트웨어 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-174">For Windows Server 2012 R2, the WSFC cluster share disk currently in use is the SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="5fc10-175">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-175">Do the following:</span></span>
1. <span data-ttu-id="5fc10-176">각 클러스터 노드에 추가 디스크 또는 동일한 크기의 디스크(스트라이프해야 하는)를 추가하고 서식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-176">Add an additional disk or disks of the same size (which you need to stripe) to each of the cluster nodes, and format them.</span></span>
2. <span data-ttu-id="5fc10-177">SIOS DataKeeper를 사용하여 저장소 복제를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="5fc10-178">이 절차는 WSFC 클러스터 컴퓨터에 SIOS DataKeeper를 이미 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-178">This procedure assumes that you have already installed SIOS DataKeeper on the WSFC cluster machines.</span></span> <span data-ttu-id="5fc10-179">설치한 경우 이제 컴퓨터 간의 복제를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-179">If you have installed it, you must now configure replication between the machines.</span></span> <span data-ttu-id="5fc10-180">프로세스는 기본 [Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide-8.12.3.3]에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-180">The process is described in detail in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![새 SAP ASCS/SCS 공유 디스크에 대한 DataKeeper 동기 미러링][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="5fc10-182">SAP 응용 프로그램 서버 및 DBMS 클러스터에 대한 VM 배포</span><span class="sxs-lookup"><span data-stu-id="5fc10-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="5fc10-183">두 번째 SAP 시스템에 대한 인프라 준비를 완료하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-183">To complete the infrastructure preparation for the second SAP system, do the following:</span></span>

1. <span data-ttu-id="5fc10-184">SAP 응용 프로그램 서버에 대한 전용 VM을 배포하고 고유한 전용 가용성 그룹에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="5fc10-185">DBMS 클러스터에 대한 전용 VM을 배포하고 고유한 전용 가용성 그룹에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-the-second-sap-sid2-netweaver-system"></a><span data-ttu-id="5fc10-186">두 번째 SAP SID2 NetWeaver 시스템 설치</span><span class="sxs-lookup"><span data-stu-id="5fc10-186">Install the second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="5fc10-187">두 번째 SAP SID2 시스템을 설치하는 전체 프로세스는 기본 [Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide-9]에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-187">The complete process of installing a second SAP SID2 system is described in the main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="5fc10-188">고급 절차는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-188">The high-level procedure is as follows:</span></span>

1. <span data-ttu-id="5fc10-189">[SAP 첫 번째 클러스터 노드 설치][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="5fc10-189">[Install the SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="5fc10-190">이 단계에서는 **기존 WSFC 클러스터 노드 1**에 고가용성 ASCS/SCS 인스턴스를 포함한 SAP를 설치하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="5fc10-191">[ASCS/SCS 인스턴스의 SAP 프로필 수정][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="5fc10-191">[Modify the SAP profile of the ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="5fc10-192">[프로브 포트 구성][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="5fc10-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="5fc10-193">이 단계에서는 PowerShell을 사용하여 SAP 클러스터 리소스 SAP-SID2-IP 프로브 포트를 구성하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="5fc10-194">SAP ASCS/SCS 클러스터 노드 중 하나에서 이 구성을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-194">Execute this configuration on one of the SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="5fc10-195">[데이터베이스 인스턴스 설치][sap-ha-guide-9.2].</span><span class="sxs-lookup"><span data-stu-id="5fc10-195">[Install the database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="5fc10-196">이 단계에서는 전용 WSFC 클러스터에 DBMS를 설치하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="5fc10-197">[두 번째 클러스터 노드 설치][sap-ha-guide-9.3].</span><span class="sxs-lookup"><span data-stu-id="5fc10-197">[Install the second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="5fc10-198">이 단계에서는 기존 WSFC 클러스터 노드 2에 고가용성 ASCS/SCS 인스턴스를 포함한 SAP를 설치하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on the existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="5fc10-199">SAP ASCS /SCS 인스턴스 및 ProbePort의 Windows 방화벽 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-199">Open Windows Firewall ports for the SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="5fc10-200">SAP ASCS/SCS 인스턴스에 사용되는 두 클러스터 노드에서 SAP ASCS/SCS에서 사용하는 모든 Windows 방화벽 포트를 열고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="5fc10-201">이러한 포트는 [Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide-8.8]에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-201">These ports are listed in the [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="5fc10-202">또한 62350 시나리오에서와 같이 Azure 내부 부하 분산 장치 프로브 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5fc10-202">Also open the Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="5fc10-203">[SAP ERS Windows 서비스 인스턴스의 시작 유형 변경][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="5fc10-203">[Change the start type of the SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="5fc10-204">새 전용 VM에서 [SAP 기본 응용 프로그램 서버 설치][sap-ha-guide-9.5].</span><span class="sxs-lookup"><span data-stu-id="5fc10-204">[Install the SAP primary application server][sap-ha-guide-9.5] on the new dedicated VM.</span></span>

9. <span data-ttu-id="5fc10-205">새 전용 VM에서 [SAP 추가 응용 프로그램 서버 설치][sap-ha-guide-9.6].</span><span class="sxs-lookup"><span data-stu-id="5fc10-205">[Install the SAP additional application server][sap-ha-guide-9.6] on the new dedicated VM.</span></span>

10. <span data-ttu-id="5fc10-206">[SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 복제 테스트][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="5fc10-206">[Test the SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fc10-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fc10-207">Next steps</span></span>

- <span data-ttu-id="5fc10-208">[네트워킹 제한: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="5fc10-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="5fc10-209">[Azure Load Balancer에 대한 다중 VIP][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="5fc10-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="5fc10-210">[Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="5fc10-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
