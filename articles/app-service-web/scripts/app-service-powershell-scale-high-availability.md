---
title: "Azure PowerShell 스크립트 샘플 - 전세계에 고가용성 아키텍처를 가진 웹앱 확장 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 전세계에 고가용성 아키텍처를 가진 웹앱 확장"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 9acd1cf4d1a5705811c4dedc545505ec0ac55fc7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="f0eec-103">전세계에 고가용성 아키텍처를 가진 웹앱 확장</span><span class="sxs-lookup"><span data-stu-id="f0eec-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="f0eec-104">이 시나리오에서는 리소스 그룹, 두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="f0eec-105">실행이 완료되면 가장 낮은 네트워크 대기 시간에 따라 웹앱의 전역적 가용성을 제공하는 가용성이 좋은 아키텍처를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="f0eec-106">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`을 실행하여 Azure와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f0eec-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f0eec-107">Sample script</span></span>

<span data-ttu-id="f0eec-108">[!code-powershell[기본](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "전세계에 고가용성 아키텍처를 가진 웹앱 확장")]</span><span class="sxs-lookup"><span data-stu-id="f0eec-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f0eec-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="f0eec-109">Clean up deployment</span></span> 

<span data-ttu-id="f0eec-110">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f0eec-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="f0eec-111">Script explanation</span></span>

<span data-ttu-id="f0eec-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-112">This script uses the following commands.</span></span> <span data-ttu-id="f0eec-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f0eec-114">명령</span><span class="sxs-lookup"><span data-stu-id="f0eec-114">Command</span></span> | <span data-ttu-id="f0eec-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f0eec-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0eec-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f0eec-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f0eec-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f0eec-118">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="f0eec-118">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="f0eec-119">Traffic Manager 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-119">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="f0eec-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f0eec-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f0eec-121">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f0eec-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f0eec-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f0eec-123">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-123">Creates a web app.</span></span> |
| [<span data-ttu-id="f0eec-124">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="f0eec-124">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="f0eec-125">Traffic Manager 프로필에서 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-125">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0eec-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0eec-126">Next steps</span></span>

<span data-ttu-id="f0eec-127">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0eec-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f0eec-128">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0eec-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
