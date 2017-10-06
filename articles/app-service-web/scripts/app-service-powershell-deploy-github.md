---
title: "PowerShell 스크립트 샘플-aaaAzure 웹 앱 만들기 및 GitHub에서 코드 배포 | Microsoft Docs"
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
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="bcfc0-103">웹앱 만들기 및 GitHub의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="bcfc0-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="bcfc0-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 연속 배포를 사용하지 않고 공용 GitHub 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="bcfc0-105">연속 배포를 사용하는 GitHub 배포는 [GitHub의 연속 배포를 사용하여 웹앱 만들기](app-service-powershell-continuous-deployment-github.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="bcfc0-106">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="bcfc0-107">또한 hello 웹 응용 프로그램 코드를 포함 하는 링크 tooGitHub 리포지토리의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="bcfc0-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="bcfc0-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bcfc0-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="bcfc0-109">Clean up deployment</span></span> 

<span data-ttu-id="bcfc0-110">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="bcfc0-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="bcfc0-111">Script explanation</span></span>

<span data-ttu-id="bcfc0-112">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-112">This script uses hello following commands.</span></span> <span data-ttu-id="bcfc0-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bcfc0-114">명령</span><span class="sxs-lookup"><span data-stu-id="bcfc0-114">Command</span></span> | <span data-ttu-id="bcfc0-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="bcfc0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bcfc0-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bcfc0-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="bcfc0-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bcfc0-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="bcfc0-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="bcfc0-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="bcfc0-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="bcfc0-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="bcfc0-121">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-121">Creates a web app.</span></span> |
| [<span data-ttu-id="bcfc0-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="bcfc0-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="bcfc0-123">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bcfc0-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bcfc0-124">Next steps</span></span>

<span data-ttu-id="bcfc0-125">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bcfc0-126">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcfc0-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
