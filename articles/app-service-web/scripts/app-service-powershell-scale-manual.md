---
title: "Azure PowerShell 스크립트 샘플 - 수동으로 웹앱 크기 조정 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 수동으로 웹앱 크기 조정"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="00e17-103">수동으로 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="00e17-103">Scale a web app manually</span></span>

<span data-ttu-id="00e17-104">이 시나리오에서는 리소스 그룹, App Service 계획 및 웹앱을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="00e17-105">그런 다음 단일 인스턴스에서 여러 인스턴스로 App Service 계획의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="00e17-106">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`을 실행하여 Azure와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="00e17-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="00e17-107">Sample script</span></span>

<span data-ttu-id="00e17-108">[!code-powershell[기본](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "수동으로 웹앱 크기 조정")]</span><span class="sxs-lookup"><span data-stu-id="00e17-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="00e17-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="00e17-109">Clean up deployment</span></span> 

<span data-ttu-id="00e17-110">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="00e17-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="00e17-111">Script explanation</span></span>

<span data-ttu-id="00e17-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-112">This script uses the following commands.</span></span> <span data-ttu-id="00e17-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="00e17-114">명령</span><span class="sxs-lookup"><span data-stu-id="00e17-114">Command</span></span> | <span data-ttu-id="00e17-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="00e17-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="00e17-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="00e17-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="00e17-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="00e17-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="00e17-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="00e17-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="00e17-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="00e17-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="00e17-121">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-121">Creates a web app.</span></span> |
| [<span data-ttu-id="00e17-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="00e17-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="00e17-123">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="00e17-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00e17-124">Next steps</span></span>

<span data-ttu-id="00e17-125">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00e17-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="00e17-126">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e17-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
