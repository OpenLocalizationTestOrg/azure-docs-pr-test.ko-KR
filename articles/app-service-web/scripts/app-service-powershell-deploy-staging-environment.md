---
title: "Azure PowerShell 스크립트 샘플 - 웹앱 만들기 및 스테이징 환경에 코드 배포 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 웹앱 만들기 및 스테이징 환경에 코드 배포"
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
ms.openlocfilehash: 55adc13350eb0f4711efa3c901f6e4e7755dfb27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="13d25-103">웹앱 만들기 및 스테이징 환경에 코드 배포</span><span class="sxs-lookup"><span data-stu-id="13d25-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="13d25-104">이 샘플 스크립트는 "스테이징"이라는 추가 배포 슬롯을 사용하여 App Service에서 웹앱을 만든 다음 "스테이징" 슬롯에 샘플 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="13d25-105">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`을 실행하여 Azure와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="13d25-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="13d25-106">Sample script</span></span>

<span data-ttu-id="13d25-107">[!code-powershell[기본](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "웹앱 만들기 및 스테이징 환경에 코드 배포")]</span><span class="sxs-lookup"><span data-stu-id="13d25-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="13d25-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="13d25-108">Clean up deployment</span></span> 

<span data-ttu-id="13d25-109">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="13d25-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="13d25-110">Script explanation</span></span>

<span data-ttu-id="13d25-111">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-111">This script uses the following commands.</span></span> <span data-ttu-id="13d25-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="13d25-113">명령</span><span class="sxs-lookup"><span data-stu-id="13d25-113">Command</span></span> | <span data-ttu-id="13d25-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="13d25-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="13d25-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="13d25-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="13d25-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="13d25-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="13d25-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="13d25-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="13d25-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="13d25-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="13d25-120">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-120">Creates a web app.</span></span> |
| [<span data-ttu-id="13d25-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="13d25-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="13d25-122">App Service 계획을 수정하여 해당 가격 책정 계층을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="13d25-123">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="13d25-123">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="13d25-124">웹앱에 대한 배포 슬롯을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-124">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="13d25-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="13d25-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="13d25-126">리소스 그룹에서 리소스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-126">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="13d25-127">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="13d25-127">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="13d25-128">웹앱의 배포 슬롯을 프로덕션으로 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-128">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="13d25-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13d25-129">Next steps</span></span>

<span data-ttu-id="13d25-130">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13d25-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="13d25-131">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13d25-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
