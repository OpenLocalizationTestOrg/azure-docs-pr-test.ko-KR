---
title: "PowerShell 스크립트 샘플-aaaAzure 웹 앱 만들기 및 코드 tooa 스테이징 환경 배포 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-웹 앱 만들기 및 코드 tooa 스테이징 환경 배포"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="c8f63-103">웹 앱을 만들고 코드 tooa 스테이징 환경 배포</span><span class="sxs-lookup"><span data-stu-id="c8f63-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="c8f63-104">이 샘플 스크립트 웹 응용 프로그램 앱 서비스의 "준비"를 호출 하는 추가 배포 슬롯으로 만들고 "스테이징" 슬롯 샘플 앱 toohello 다음 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="c8f63-105">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c8f63-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c8f63-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c8f63-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="c8f63-107">Clean up deployment</span></span> 

<span data-ttu-id="c8f63-108">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c8f63-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c8f63-109">Script explanation</span></span>

<span data-ttu-id="c8f63-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-110">This script uses hello following commands.</span></span> <span data-ttu-id="c8f63-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c8f63-112">명령</span><span class="sxs-lookup"><span data-stu-id="c8f63-112">Command</span></span> | <span data-ttu-id="c8f63-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c8f63-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c8f63-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c8f63-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c8f63-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c8f63-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c8f63-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c8f63-117">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c8f63-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c8f63-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c8f63-119">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-119">Creates a web app.</span></span> |
| [<span data-ttu-id="c8f63-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c8f63-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="c8f63-121">앱 서비스 계획 toochange 해당 가격 책정 계층을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="c8f63-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="c8f63-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="c8f63-123">웹앱에 대한 배포 슬롯을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="c8f63-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c8f63-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="c8f63-125">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="c8f63-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="c8f63-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="c8f63-127">웹앱의 배포 슬롯을 프로덕션으로 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c8f63-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8f63-128">Next steps</span></span>

<span data-ttu-id="c8f63-129">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c8f63-130">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8f63-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
