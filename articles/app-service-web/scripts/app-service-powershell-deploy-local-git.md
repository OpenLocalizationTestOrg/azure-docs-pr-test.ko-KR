---
title: "PowerShell 스크립트 샘플-aaaAzure 웹 앱 만들기 및 로컬 Git 리포지토리에서 코드 배포 | Microsoft Docs"
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
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="06f2c-103">웹앱 만들기 및 로컬 Git 리포지토리의 코드 배포</span><span class="sxs-lookup"><span data-stu-id="06f2c-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="06f2c-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 로컬 Git 리포지토리에서 웹앱 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="06f2c-105">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="06f2c-106">또한, 응용 프로그램 코드에 로컬 Git 리포지토리에서 커밋된 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="06f2c-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="06f2c-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="06f2c-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="06f2c-108">Clean up deployment</span></span> 

<span data-ttu-id="06f2c-109">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="06f2c-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="06f2c-110">Script explanation</span></span>

<span data-ttu-id="06f2c-111">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-111">This script uses hello following commands.</span></span> <span data-ttu-id="06f2c-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="06f2c-113">명령</span><span class="sxs-lookup"><span data-stu-id="06f2c-113">Command</span></span> | <span data-ttu-id="06f2c-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="06f2c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06f2c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06f2c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="06f2c-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06f2c-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="06f2c-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="06f2c-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="06f2c-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="06f2c-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="06f2c-120">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-120">Creates a web app.</span></span> |
| [<span data-ttu-id="06f2c-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="06f2c-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="06f2c-122">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="06f2c-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="06f2c-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="06f2c-124">웹앱의 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06f2c-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06f2c-125">Next steps</span></span>

<span data-ttu-id="06f2c-126">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="06f2c-127">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06f2c-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
