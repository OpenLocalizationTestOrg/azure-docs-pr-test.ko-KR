---
title: "PowerShell 스크립트 샘플-aaaAzure 웹 응용 프로그램을 수동으로 확장 | Microsoft Docs"
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
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="d3813-103">수동으로 웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="d3813-103">Scale a web app manually</span></span>

<span data-ttu-id="d3813-104">이 시나리오에서는 리소스 그룹 toocreate 배웁니다 앱 서비스 계획 및 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="d3813-105">단일 인스턴스 toomultiple 인스턴스에서 hello 앱 서비스 계획을 확장 한 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="d3813-106">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d3813-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d3813-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d3813-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d3813-108">Clean up deployment</span></span> 

<span data-ttu-id="d3813-109">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d3813-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d3813-110">Script explanation</span></span>

<span data-ttu-id="d3813-111">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-111">This script uses hello following commands.</span></span> <span data-ttu-id="d3813-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d3813-113">명령</span><span class="sxs-lookup"><span data-stu-id="d3813-113">Command</span></span> | <span data-ttu-id="d3813-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d3813-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d3813-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d3813-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d3813-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d3813-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d3813-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d3813-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d3813-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d3813-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d3813-120">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-120">Creates a web app.</span></span> |
| [<span data-ttu-id="d3813-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d3813-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="d3813-122">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d3813-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3813-123">Next steps</span></span>

<span data-ttu-id="d3813-124">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d3813-125">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3813-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
