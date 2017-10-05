---
title: "Azure PowerShell 스크립트 샘플 - GitHub의 연속 배포를 사용하여 웹앱 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - GitHub의 연속 배포를 사용하여 웹앱 만들기"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="d4f05-103">GitHub의 연속 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d4f05-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="d4f05-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 GitHub 리포지토리의 연속 배포를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="d4f05-105">연속 배포를 사용하지 않는 GitHub 배포는 [웹앱 만들기 및 GitHub의 코드 배포](app-service-powershell-deploy-github.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4f05-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="d4f05-106">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="d4f05-107">또한 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-107">Also, ensure that:</span></span>

- <span data-ttu-id="d4f05-108">`az login` 명령을 사용하여 Azure와 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="d4f05-109">응용 프로그램 코드는 사용자가 소유한 공용 또는 개인 GitHub 리포지토리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="d4f05-110">[GitHub 계정에서 액세스 토큰을 만들](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="d4f05-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d4f05-111">Sample script</span></span>

<span data-ttu-id="d4f05-112">[!code-powershell[기본](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "GitHub의 연속 배포를 사용하여 웹앱 만들기")]</span><span class="sxs-lookup"><span data-stu-id="d4f05-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d4f05-113">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d4f05-113">Clean up deployment</span></span> 

<span data-ttu-id="d4f05-114">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d4f05-115">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d4f05-115">Script explanation</span></span>

<span data-ttu-id="d4f05-116">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-116">This script uses the following commands.</span></span> <span data-ttu-id="d4f05-117">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d4f05-118">명령</span><span class="sxs-lookup"><span data-stu-id="d4f05-118">Command</span></span> | <span data-ttu-id="d4f05-119">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d4f05-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4f05-120">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d4f05-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d4f05-121">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d4f05-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d4f05-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d4f05-123">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d4f05-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d4f05-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d4f05-125">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-125">Creates a web app.</span></span> |
| [<span data-ttu-id="d4f05-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d4f05-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="d4f05-127">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4f05-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4f05-128">Next steps</span></span>

<span data-ttu-id="d4f05-129">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4f05-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d4f05-130">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4f05-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
