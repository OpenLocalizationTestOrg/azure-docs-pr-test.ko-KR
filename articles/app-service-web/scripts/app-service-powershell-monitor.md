---
title: "Azure PowerShell 스크립트 샘플 - 웹 서버 로그를 사용하여 웹앱 모니터링 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 웹 서버 로그를 사용하여 웹앱 모니터링"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="d7865-103">웹 서버 로그로 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="d7865-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="d7865-104">이 시나리오에서는 리소스 그룹, App Service 계획, 웹앱을 만들고 웹 서버 로그를 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="d7865-105">그런 다음 검토하기 위해 로그 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-105">You will then download the log files for review.</span></span>

<span data-ttu-id="d7865-106">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`을 실행하여 Azure와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d7865-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d7865-107">Sample script</span></span>

<span data-ttu-id="d7865-108">[!code-powershell[기본](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "웹 서버 로그로 웹앱 모니터링")]</span><span class="sxs-lookup"><span data-stu-id="d7865-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d7865-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d7865-109">Clean up deployment</span></span> 

<span data-ttu-id="d7865-110">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, 웹앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d7865-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d7865-111">Script explanation</span></span>

<span data-ttu-id="d7865-112">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-112">This script uses the following commands.</span></span> <span data-ttu-id="d7865-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d7865-114">명령</span><span class="sxs-lookup"><span data-stu-id="d7865-114">Command</span></span> | <span data-ttu-id="d7865-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d7865-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d7865-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d7865-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d7865-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d7865-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d7865-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d7865-119">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d7865-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d7865-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d7865-121">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-121">Creates a web app.</span></span> |
| [<span data-ttu-id="d7865-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d7865-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="d7865-123">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="d7865-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="d7865-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="d7865-125">웹앱의 메트릭을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d7865-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7865-126">Next steps</span></span>

<span data-ttu-id="d7865-127">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7865-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d7865-128">Azure App Service Web Apps에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../app-service-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7865-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
