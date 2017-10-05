---
title: "부하 분산 장치에 대한 Azure Resource Manager 지원 | Microsoft Docs"
description: "Azure Resource Manager와 함께 부하 분산 장치용 PowerShell을 사용합니다. 부하 분산 장치에 템플릿을 사용합니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="0a4b5-104">Azure Load Balancer에 대한 Azure Resource Manager 지원 사용</span><span class="sxs-lookup"><span data-stu-id="0a4b5-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="0a4b5-105">Azure의 서비스용 관리 프레임워크로는 기본적으로 Azure Resource Manager가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="0a4b5-106">이제 Azure Resource Manager 기반 API 및 도구를 사용하여 Azure Load Balancer를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="0a4b5-107">개념</span><span class="sxs-lookup"><span data-stu-id="0a4b5-107">Concepts</span></span>

<span data-ttu-id="0a4b5-108">Resource Manager를 사용하는 경우 Azure Load Balancer에 다음과 같은 자식 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="0a4b5-109">프런트 엔드 IP 구성 - 부하 분산 장치는 VIP(가상 IP)라고도 하는 프런트 엔드 IP 주소를 하나 이상 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="0a4b5-110">이러한 IP 주소는 트래픽에 대한 수신으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="0a4b5-111">백 엔드 주소 풀 - 부하가 분산될 가상 컴퓨터 NIC(네트워크 인터페이스 카드)와 연결된 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="0a4b5-112">부하 분산 규칙 - 규칙 속성은 지정된 프런트 엔드 IP와 포트 조합을 백 엔드 IP 주소와 포트 조합 집합에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="0a4b5-113">부하 분산 장치 하나에 여러 부하 분산 규칙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="0a4b5-114">각 규칙은 VM과 연결된 백 엔드 IP와 포트 및 프런트 엔드 IP와 포트의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="0a4b5-115">검색 - 검색을 사용하여 VM 인스턴스의 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="0a4b5-116">상태 검색에 실패하면 해당 VM 인스턴스는 자동으로 회전에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="0a4b5-117">인바운드 NAT 규칙 - 프런트 엔드 IP를 통해 흐르고 백 엔드 IP에 분산되는 인바운드 트래픽을 정의하는 NAT 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="0a4b5-118">빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="0a4b5-118">Quickstart templates</span></span>

<span data-ttu-id="0a4b5-119">Azure Resource Manager를 사용하면 선언적 템플릿을 통해 응용 프로그램을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="0a4b5-120">단일 템플릿에서 여러 서비스를 해당 종속성과 함께 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="0a4b5-121">동일한 템플릿을 사용하여 응용 프로그램 수명 주기의 각 단계 중에 응용 프로그램을 반복해서 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="0a4b5-122">템플릿은 가상 컴퓨터, 가상 네트워크, 가용성 집합, NIC(네트워크 인터페이스), 저장소 계정, 부하 분산 장치, 네트워크 보안 그룹 및 공용 IP에 대한 정의를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="0a4b5-123">템플릿을 사용하면 복잡한 응용 프로그램에 필요한 모든 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="0a4b5-124">버전 제어 및 공동 작업을 위해 템플릿 파일을 콘텐츠 관리 시스템에 체크 인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="0a4b5-125">템플릿에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="0a4b5-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="0a4b5-126">네트워크 리소스에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="0a4b5-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="0a4b5-127">Azure Load Balancer를 사용하는 빠른 시작 템플릿은 커뮤니티 생성 템플릿 집합을 호스트하는 [GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates) 에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="0a4b5-128">템플릿의 예:</span><span class="sxs-lookup"><span data-stu-id="0a4b5-128">Examples of templates:</span></span>

* [<span data-ttu-id="0a4b5-129">부하 분산 장치의 2개 VM 및 부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="0a4b5-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="0a4b5-130">내부 부하 분산 장치를 포함하는 VNET의 2개 VM 및 부하 분산 장치 규칙</span><span class="sxs-lookup"><span data-stu-id="0a4b5-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="0a4b5-131">부하 분산 장치의 2개 VM 및 LB에서 NAT 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="0a4b5-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="0a4b5-132">PowerShell 또는 CLI를 사용하여 Azure 부하 분산 장치 설정</span><span class="sxs-lookup"><span data-stu-id="0a4b5-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="0a4b5-133">Azure Resource Manager cmdlet, 명령줄 도구 및 REST API 시작</span><span class="sxs-lookup"><span data-stu-id="0a4b5-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="0a4b5-134">[Azure 네트워킹 Cmdlet](https://msdn.microsoft.com/library/azure/mt163510.aspx) 을 사용하여 부하 분산 장치를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="0a4b5-135">Azure Resource Manager를 사용하여 부하 분산 장치를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="0a4b5-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="0a4b5-136">Azure 리소스 관리에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="0a4b5-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="0a4b5-137">부하 분산 장치 REST API</span><span class="sxs-lookup"><span data-stu-id="0a4b5-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="0a4b5-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a4b5-138">Next steps</span></span>

<span data-ttu-id="0a4b5-139">[인터넷 연결 부하 분산 장치를 시작](load-balancer-get-started-internet-arm-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="0a4b5-140">[부하 분산 장치의 유휴 TCP 시간 제한 설정](load-balancer-tcp-idle-timeout.md)을 관리하는 방법을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="0a4b5-141">응용 프로그램이 부하 분산 장치를 통해 서버에 대한 연결 상태를 유지해야 하는 경우에는 이 내용을 숙지하고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a4b5-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>
