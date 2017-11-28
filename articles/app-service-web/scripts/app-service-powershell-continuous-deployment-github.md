---
title: "PowerShell 스크립트 샘플-aaaAzure GitHub에서 연속 배포와 함께 웹 앱 만들기 | Microsoft Docs"
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
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="25b9a-103">GitHub의 연속 배포를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="25b9a-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="25b9a-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 GitHub 리포지토리의 연속 배포를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="25b9a-105">연속 배포를 사용하지 않는 GitHub 배포는 [웹앱 만들기 및 GitHub의 코드 배포](app-service-powershell-deploy-github.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25b9a-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="25b9a-106">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="25b9a-107">또한 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-107">Also, ensure that:</span></span>

- <span data-ttu-id="25b9a-108">Hello를 사용 하 여 Azure와의 연결을 만들었습니다 `az login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="25b9a-109">hello 응용 프로그램 코드는 사용자가 소유한 공용 또는 개인 GitHub 리포지토리 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="25b9a-110">[GitHub 계정에서 액세스 토큰을 만들](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)었습니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="25b9a-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="25b9a-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="25b9a-112">배포 정리</span><span class="sxs-lookup"><span data-stu-id="25b9a-112">Clean up deployment</span></span> 

<span data-ttu-id="25b9a-113">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="25b9a-114">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="25b9a-114">Script explanation</span></span>

<span data-ttu-id="25b9a-115">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-115">This script uses hello following commands.</span></span> <span data-ttu-id="25b9a-116">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="25b9a-117">명령</span><span class="sxs-lookup"><span data-stu-id="25b9a-117">Command</span></span> | <span data-ttu-id="25b9a-118">참고 사항</span><span class="sxs-lookup"><span data-stu-id="25b9a-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25b9a-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="25b9a-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="25b9a-120">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="25b9a-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="25b9a-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="25b9a-122">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="25b9a-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="25b9a-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="25b9a-124">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-124">Creates a web app.</span></span> |
| [<span data-ttu-id="25b9a-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="25b9a-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="25b9a-126">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="25b9a-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25b9a-127">Next steps</span></span>

<span data-ttu-id="25b9a-128">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="25b9a-129">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25b9a-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
