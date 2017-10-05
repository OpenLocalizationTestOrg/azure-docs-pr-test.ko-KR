---
title: "Azure PowerShell 스크립트 샘플 - 웹앱 만들기 및 Git 리포지토리의 코드 배포 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 웹앱 만들기 및 Git 리포지토리의 코드 배포"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="f5074-103">웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="f5074-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="f5074-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 로컬 Git 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="f5074-105">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`을 실행하여 Azure와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="f5074-106">또한 응용 프로그램 코드는 로컬 Git 리포지토리로 커밋될 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f5074-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="f5074-107">Sample script</span></span>

<span data-ttu-id="f5074-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포")]</span><span class="sxs-lookup"><span data-stu-id="f5074-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f5074-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="f5074-109">Clean up deployment</span></span> 

<span data-ttu-id="f5074-110">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f5074-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="f5074-111">Script explanation</span></span>

<span data-ttu-id="f5074-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-112">This script uses the following commands.</span></span> <span data-ttu-id="f5074-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f5074-114">명령</span><span class="sxs-lookup"><span data-stu-id="f5074-114">Command</span></span> | <span data-ttu-id="f5074-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f5074-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f5074-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f5074-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f5074-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f5074-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f5074-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f5074-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f5074-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f5074-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f5074-121">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-121">Creates a web app.</span></span> |
| [<span data-ttu-id="f5074-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f5074-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="f5074-123">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="f5074-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="f5074-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="f5074-125">웹앱의 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f5074-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5074-126">Next steps</span></span>

<span data-ttu-id="f5074-127">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5074-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f5074-128">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5074-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
