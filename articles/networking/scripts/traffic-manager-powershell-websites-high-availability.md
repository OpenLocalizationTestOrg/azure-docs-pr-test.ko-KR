---
title: "PowerShell 스크립트 샘플 응용 프로그램의 고가용성에 대 한 트래픽 라우팅할 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 응용 프로그램 고가용성을 위한 트래픽 라우팅"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="c8d6b-103">응용 프로그램 고가용성을 위한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="c8d6b-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="c8d6b-104">이 스크립트는 리소스 그룹, 2개 App Service 계획, 2개 웹앱, Traffic Manager 프로필 및 2개 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="c8d6b-105">트래픽 관리자는 hello 기본 지역의 hello 응용 프로그램을 사용할 수 없는 경우 hello 기본 지역으로 한 영역과 toohello 보조 지역에 트래픽을 toohello 응용 프로그램을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="c8d6b-106">Hello 스크립트를 실행 하기 전에 hello MyWebApp, MyWebAppL1 리소스 및 MyWebAppL2 Azure 간의 toounique 값 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="c8d6b-107">Hello 스크립트를 실행 한 후 hello 앱 URL mywebapp.trafficmanager.net hello 사용 하 여 hello 기본 영역에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="c8d6b-108">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c8d6b-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c8d6b-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="c8d6b-110">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="c8d6b-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c8d6b-111">Script explanation</span></span>

<span data-ttu-id="c8d6b-112">이 스크립트 명령 toocreate 리소스 그룹, 웹 응용 프로그램, 트래픽 관리자 프로필 뒤 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="c8d6b-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c8d6b-114">명령</span><span class="sxs-lookup"><span data-stu-id="c8d6b-114">Command</span></span> | <span data-ttu-id="c8d6b-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c8d6b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c8d6b-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c8d6b-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="c8d6b-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c8d6b-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c8d6b-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c8d6b-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-119">Creates an App Service plan.</span></span> <span data-ttu-id="c8d6b-120">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="c8d6b-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c8d6b-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c8d6b-122">Hello 앱 서비스 계획 내에서 Azure 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="c8d6b-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c8d6b-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="c8d6b-124">Hello 앱 서비스 계획 내에서 Azure 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="c8d6b-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="c8d6b-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="c8d6b-126">Azure Traffic Manager 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="c8d6b-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="c8d6b-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="c8d6b-128">끝점 tooan Azure 트래픽 관리자 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c8d6b-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8d6b-129">Next steps</span></span>

<span data-ttu-id="c8d6b-130">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c8d6b-131">추가 네트워킹 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d6b-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
