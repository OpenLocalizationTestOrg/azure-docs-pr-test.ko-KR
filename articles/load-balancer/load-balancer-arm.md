---
title: "부하 분산 장치에 대 한 리소스 관리자 지원 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="ad92c-104">Azure Load Balancer에 대한 Azure Resource Manager 지원 사용</span><span class="sxs-lookup"><span data-stu-id="ad92c-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="ad92c-105">Azure 리소스 관리자는 Azure에서 서비스에 대 한 hello 기본 설정된 관리 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="ad92c-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="ad92c-106">이제 Azure Resource Manager 기반 API 및 도구를 사용하여 Azure Load Balancer를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="ad92c-107">개념</span><span class="sxs-lookup"><span data-stu-id="ad92c-107">Concepts</span></span>

<span data-ttu-id="ad92c-108">리소스 관리자와 Azure 부하 분산 장치 hello를 다음 자식 리소스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="ad92c-109">프런트 엔드 IP 구성 - 부하 분산 장치는 VIP(가상 IP)라고도 하는 프런트 엔드 IP 주소를 하나 이상 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="ad92c-110">이러한 IP 주소는 hello 트래픽에 대 한 수신으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="ad92c-111">백 엔드 주소 풀 – 이들은 hello 가상 컴퓨터 네트워크 인터페이스 카드 (NIC) toowhich 부하 배포와 연결 된 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="ad92c-112">부하 분산 규칙 – 규칙 속성에 지정 된 프런트 엔드 IP 매핑합니다 조합 포트 및 포트 조합 tooa 백 엔드 IP 주소 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="ad92c-113">부하 분산 장치 하나에 여러 부하 분산 규칙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="ad92c-114">각 규칙은 VM과 연결된 백 엔드 IP와 포트 및 프런트 엔드 IP와 포트의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="ad92c-115">프로브 – 프로브 VM 인스턴스 hello 상태 있습니다 tookeep 추적을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="ad92c-116">상태 검색이 실패 하면 hello VM 인스턴스 수행 될 순환 순서에서 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="ad92c-117">인바운드 NAT 규칙 – NAT 규칙 정의 인바운드 트래픽을 hello 프런트 엔드 IP를 통해 흐르는 hello 및 분산된 toohello 다시 IP를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="ad92c-118">빠른 시작 템플릿</span><span class="sxs-lookup"><span data-stu-id="ad92c-118">Quickstart templates</span></span>

<span data-ttu-id="ad92c-119">Azure 리소스 관리자를 사용 하면 tooprovision 선언적 템플릿을 사용 하 여 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="ad92c-120">단일 템플릿에서 여러 서비스를 해당 종속성과 함께 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="ad92c-121">Hello를 사용 하 여 동일한 템플릿 toorepeatedly hello 응용 프로그램 수명 주기의 다른 단계 동안 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="ad92c-122">템플릿은 가상 컴퓨터, 가상 네트워크, 가용성 집합, NIC(네트워크 인터페이스), 저장소 계정, 부하 분산 장치, 네트워크 보안 그룹 및 공용 IP에 대한 정의를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="ad92c-123">템플릿을 사용하면 복잡한 응용 프로그램에 필요한 모든 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="ad92c-124">버전 제어 및 공동 작업에 대 한 콘텐츠 관리 시스템에 hello 템플릿 파일을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="ad92c-125">템플릿에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ad92c-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="ad92c-126">네트워크 리소스에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ad92c-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="ad92c-127">Azure Load Balancer를 사용하는 빠른 시작 템플릿은 커뮤니티 생성 템플릿 집합을 호스트하는 [GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates) 에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="ad92c-128">템플릿의 예:</span><span class="sxs-lookup"><span data-stu-id="ad92c-128">Examples of templates:</span></span>

* [<span data-ttu-id="ad92c-129">부하 분산 장치의 2개 VM 및 부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="ad92c-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="ad92c-130">내부 부하 분산 장치를 포함하는 VNET의 2개 VM 및 부하 분산 장치 규칙</span><span class="sxs-lookup"><span data-stu-id="ad92c-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="ad92c-131">부하 분산 장치에 2 개의 Vm hello LB에서 NAT 규칙을 구성 하 고</span><span class="sxs-lookup"><span data-stu-id="ad92c-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="ad92c-132">PowerShell 또는 CLI를 사용하여 Azure 부하 분산 장치 설정</span><span class="sxs-lookup"><span data-stu-id="ad92c-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="ad92c-133">Azure Resource Manager cmdlet, 명령줄 도구 및 REST API 시작</span><span class="sxs-lookup"><span data-stu-id="ad92c-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="ad92c-134">[Azure 네트워킹 Cmdlet](https://msdn.microsoft.com/library/azure/mt163510.aspx) 사용된 toocreate 부하 분산 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="ad92c-135">어떻게 toocreate Azure 리소스 관리자를 사용 하 여 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="ad92c-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="ad92c-136">Hello Azure CLI를 사용 하 여 Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="ad92c-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="ad92c-137">부하 분산 장치 REST API</span><span class="sxs-lookup"><span data-stu-id="ad92c-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="ad92c-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad92c-138">Next steps</span></span>

<span data-ttu-id="ad92c-139">[인터넷 연결 부하 분산 장치를 시작](load-balancer-get-started-internet-arm-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="ad92c-140">자세한 내용은 방법 toomanage [부하 분산 장치에 대 한 TCP 시간 제한 설정을 유휴](load-balancer-tcp-idle-timeout.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="ad92c-141">이 응용 프로그램에 필요한 tookeep 연결 활성 서버 부하 분산 장치 뒤에 대 한 경우에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad92c-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>
