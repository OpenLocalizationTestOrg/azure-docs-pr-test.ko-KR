---
title: "클래식 Azure PowerShell aaaCreate 인터넷 연결 부하 분산 장치-| Microsoft Docs"
description: "인터넷 연결 toocreate PowerShell을 사용 하는 클래식 모드에서 분산 장치를 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="50a7d-103">PowerShell에서 인터넷 연결 부하 분산 장치(클래식) 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="50a7d-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="50a7d-104">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="50a7d-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="50a7d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50a7d-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="50a7d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="50a7d-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="50a7d-107">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="50a7d-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="50a7d-108">Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="50a7d-109">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="50a7d-110">이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="50a7d-111">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="50a7d-112">수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="50a7d-113">PowerShell을 사용하여 부하 분산 장치 설정</span><span class="sxs-lookup"><span data-stu-id="50a7d-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="50a7d-114">아래의 hello 단계를 수행 하는 powershell을 사용 하 여 부하 분산 장치를 tooset:</span><span class="sxs-lookup"><span data-stu-id="50a7d-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="50a7d-115">Azure PowerShell을 처음 사용 하는 경우 참조 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 모든 hello 방식으로 toohello toosign를 Azure로 끝나고 구독을 선택 하는 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="50a7d-116">가상 컴퓨터를 만든 후 PowerShell cmdlet tooadd tooa 부하 분산 장치 가상 컴퓨터를 사용할 수 있습니다 hello 내에서 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="50a7d-117">Hello 부하 분산 장치 집합 이라는 toocloud "webfarm" 서비스 "mytestcloud" (또는 myctestcloud.cloudapp.net) hello에 대 한 hello 끝점 부하 분산 장치 toovirtual 추가 컴퓨터 추가한 다음 예제에서는 이름이 "w e b 1" 및 "web2"입니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="50a7d-118">hello 부하 분산 장치 포트 80에서 네트워크 트래픽을 받아 hello 로컬 끝점 (이 경우 포트 80)에 정의 된 hello 가상 컴퓨터 간에 부하를 분산 시키고 TCP를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="50a7d-119">1단계</span><span class="sxs-lookup"><span data-stu-id="50a7d-119">Step 1</span></span>

<span data-ttu-id="50a7d-120">Web1"hello 첫 번째 VM"에 대 한 부하 분산 된 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="50a7d-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="50a7d-121">2단계</span><span class="sxs-lookup"><span data-stu-id="50a7d-121">Step 2</span></span>

<span data-ttu-id="50a7d-122">Hello 두 번째 VM "web2" hello를 사용 하 여 동일한 부하 분산 집합 이름이 다른 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="50a7d-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="50a7d-123">부하 분산 장치에서 가상 컴퓨터 제거</span><span class="sxs-lookup"><span data-stu-id="50a7d-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="50a7d-124">제거 AzureEndpoint tooremove hello 부하 분산 장치에서 가상 컴퓨터 끝점을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="50a7d-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50a7d-125">Next steps</span></span>

<span data-ttu-id="50a7d-126">[내부 부하 분산 장치를 시작](load-balancer-get-started-ilb-classic-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="50a7d-127">경우 응용 프로그램 서버 부하 분산 장치 뒤에 대 한 연결 유지 tookeep 연결에 필요한를 이해할 수 있습니다 더에 대 한 [부하 분산 장치에 대 한 TCP 시간 제한 설정을 유휴](load-balancer-tcp-idle-timeout.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="50a7d-128">유휴 연결 동작에 대 한 toolearn Azure 부하 분산 장치를 사용 하는 경우 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50a7d-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
