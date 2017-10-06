---
title: "웹 서버 로그가 포함 된 웹 앱을 모니터링 하는 PowerShell 스크립트 샘플-aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="34201-103">웹 서버 로그로 웹앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="34201-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="34201-104">이 시나리오에서는 리소스 그룹, 앱 서비스 계획, 웹 앱 만들고 hello 웹 응용 프로그램 tooenable 웹 서버 로그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="34201-105">그런 다음 검토를 위해 hello 로그 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="34201-106">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="34201-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="34201-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="34201-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="34201-108">Clean up deployment</span></span> 

<span data-ttu-id="34201-109">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34201-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="34201-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="34201-110">Script explanation</span></span>

<span data-ttu-id="34201-111">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-111">This script uses hello following commands.</span></span> <span data-ttu-id="34201-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="34201-113">명령</span><span class="sxs-lookup"><span data-stu-id="34201-113">Command</span></span> | <span data-ttu-id="34201-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="34201-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="34201-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="34201-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="34201-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34201-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="34201-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="34201-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="34201-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34201-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="34201-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="34201-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="34201-120">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34201-120">Creates a web app.</span></span> |
| [<span data-ttu-id="34201-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="34201-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="34201-122">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="34201-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="34201-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="34201-124">웹앱의 메트릭을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="34201-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="34201-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34201-125">Next steps</span></span>

<span data-ttu-id="34201-126">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="34201-127">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34201-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
