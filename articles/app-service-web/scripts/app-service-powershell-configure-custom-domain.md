---
title: "Azure PowerShell 스크립트 샘플 - 웹앱에 사용자 지정 도메인 할당 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 웹앱에 사용자 지정 도메인 할당"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="b97b1-103">웹앱에 사용자 지정 도메인 할당</span><span class="sxs-lookup"><span data-stu-id="b97b1-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="b97b1-104">이 샘플 스크립트는 관련된 리소스를 사용하여 App Service에서 웹앱을 만든 다음 여기에 `www.<yourdomain>`를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="b97b1-105">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="b97b1-106">또한 도메인 등록 기관의 DNS 구성 페이지에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="b97b1-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="b97b1-107">Sample script</span></span>

<span data-ttu-id="b97b1-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "웹앱에 사용자 지정 도메인 할당")]</span><span class="sxs-lookup"><span data-stu-id="b97b1-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b97b1-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="b97b1-109">Clean up deployment</span></span> 

<span data-ttu-id="b97b1-110">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="b97b1-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="b97b1-111">Script explanation</span></span>

<span data-ttu-id="b97b1-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-112">This script uses the following commands.</span></span> <span data-ttu-id="b97b1-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b97b1-114">명령</span><span class="sxs-lookup"><span data-stu-id="b97b1-114">Command</span></span> | <span data-ttu-id="b97b1-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b97b1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b97b1-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b97b1-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b97b1-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b97b1-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="b97b1-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="b97b1-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b97b1-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="b97b1-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="b97b1-121">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-121">Creates a web app.</span></span> |
| [<span data-ttu-id="b97b1-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="b97b1-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="b97b1-123">App Service 계획을 수정하여 해당 가격 책정 계층을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="b97b1-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="b97b1-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="b97b1-125">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b97b1-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b97b1-126">Next steps</span></span>

<span data-ttu-id="b97b1-127">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b97b1-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b97b1-128">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b97b1-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
