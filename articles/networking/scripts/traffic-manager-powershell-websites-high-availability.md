---
title: "Azure PowerShell 스크립트 샘플 - 응용 프로그램 고가용성을 위한 트래픽 라우팅 | Microsoft Docs"
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
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="ada52-103">응용 프로그램 고가용성을 위한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="ada52-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="ada52-104">이 스크립트는 리소스 그룹, 2개 App Service 계획, 2개 웹앱, Traffic Manager 프로필 및 2개 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="ada52-105">Traffic Manager는 주 지역인 한 지역의 응용 프로그램 및 주 지역의 응용 프로그램을 사용할 수 없을 때 보조 지역으로 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="ada52-106">스크립트를 실행하기 전에 MyWebApp, MyWebAppL1 및 MyWebAppL2 값을 Azure에서 고유한 값으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="ada52-107">스크립트를 실행한 후에는 mywebapp.trafficmanager.net URL을 사용하여 주 지역의 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="ada52-108">필요한 경우 [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ada52-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ada52-109">Sample script</span></span>

<span data-ttu-id="ada52-110">[!code-powershell[주](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "고가용성을 위한 트래픽 라우팅")]</span><span class="sxs-lookup"><span data-stu-id="ada52-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="ada52-111">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="ada52-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ada52-112">Script explanation</span></span>

<span data-ttu-id="ada52-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 웹앱, Traffic Manager 프로필 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="ada52-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ada52-115">명령</span><span class="sxs-lookup"><span data-stu-id="ada52-115">Command</span></span> | <span data-ttu-id="ada52-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ada52-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ada52-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ada52-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="ada52-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ada52-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ada52-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="ada52-120">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-120">Creates an App Service plan.</span></span> <span data-ttu-id="ada52-121">Azure 웹앱에 대한 서버 팜과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="ada52-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="ada52-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="ada52-123">App Service 계획 내에서 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="ada52-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="ada52-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="ada52-125">App Service 계획 내에서 Azure 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="ada52-126">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="ada52-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="ada52-127">Azure Traffic Manager 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="ada52-128">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="ada52-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="ada52-129">Azure Traffic Manager 프로필에 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ada52-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ada52-130">Next steps</span></span>

<span data-ttu-id="ada52-131">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ada52-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="ada52-132">추가 네트워킹 PowerShell 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ada52-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>