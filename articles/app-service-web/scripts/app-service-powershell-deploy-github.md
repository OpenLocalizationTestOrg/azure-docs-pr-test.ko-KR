---
title: "Azure PowerShell 스크립트 샘플 - 웹앱 만들기 및 GitHub의 코드 배포 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 웹앱 만들기 및 GitHub의 코드 배포"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1f7fc21dc12c334f5d347ae9918bd62945bede64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="107a8-103">웹앱 만들기 및 GitHub의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="107a8-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="107a8-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 연속 배포를 사용하지 않고 공용 GitHub 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="107a8-105">연속 배포를 사용하는 GitHub 배포는 [GitHub의 연속 배포를 사용하여 웹앱 만들기](app-service-powershell-continuous-deployment-github.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="107a8-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="107a8-106">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="107a8-107">또한 웹앱 코드를 포함하는 GitHub 리포지토리에 대한 링크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="107a8-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="107a8-108">Sample script</span></span>

<span data-ttu-id="107a8-109">[!code-powershell[기본](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "웹앱 만들기 및 GitHub의 코드 배포")]</span><span class="sxs-lookup"><span data-stu-id="107a8-109">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="107a8-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="107a8-110">Clean up deployment</span></span> 

<span data-ttu-id="107a8-111">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-111">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="107a8-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="107a8-112">Script explanation</span></span>

<span data-ttu-id="107a8-113">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-113">This script uses the following commands.</span></span> <span data-ttu-id="107a8-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="107a8-115">명령</span><span class="sxs-lookup"><span data-stu-id="107a8-115">Command</span></span> | <span data-ttu-id="107a8-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="107a8-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="107a8-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="107a8-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="107a8-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="107a8-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="107a8-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="107a8-120">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="107a8-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="107a8-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="107a8-122">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-122">Creates a web app.</span></span> |
| [<span data-ttu-id="107a8-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="107a8-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="107a8-124">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-124">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="107a8-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="107a8-125">Next steps</span></span>

<span data-ttu-id="107a8-126">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="107a8-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="107a8-127">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="107a8-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
