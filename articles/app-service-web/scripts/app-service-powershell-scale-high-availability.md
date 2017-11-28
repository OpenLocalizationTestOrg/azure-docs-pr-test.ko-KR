---
title: "PowerShell 스크립트 샘플-aaaAzure 고가용성 아키텍처를 통해 전 세계 웹 앱 확장 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 전세계에 고가용성 아키텍처를 가진 웹앱 확장"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="280dd-103">전세계에 고가용성 아키텍처를 가진 웹앱 확장</span><span class="sxs-lookup"><span data-stu-id="280dd-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="280dd-104">이 시나리오에서는 리소스 그룹, 두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="280dd-105">우선을 사용할 수 있는 나면 hello 실습 완료 되 면 수 있는 아키텍처는 hello 가장 낮은 네트워크 대기 시간에 따라 웹 응용 프로그램의 글로벌 가용성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="280dd-106">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="280dd-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="280dd-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="280dd-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="280dd-108">Clean up deployment</span></span> 

<span data-ttu-id="280dd-109">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="280dd-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="280dd-110">Script explanation</span></span>

<span data-ttu-id="280dd-111">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-111">This script uses hello following commands.</span></span> <span data-ttu-id="280dd-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="280dd-113">명령</span><span class="sxs-lookup"><span data-stu-id="280dd-113">Command</span></span> | <span data-ttu-id="280dd-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="280dd-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="280dd-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="280dd-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="280dd-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="280dd-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="280dd-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="280dd-118">Traffic Manager 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="280dd-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="280dd-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="280dd-120">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="280dd-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="280dd-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="280dd-122">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-122">Creates a web app.</span></span> |
| [<span data-ttu-id="280dd-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="280dd-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="280dd-124">Traffic Manager 프로필에서 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="280dd-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="280dd-125">Next steps</span></span>

<span data-ttu-id="280dd-126">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="280dd-127">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="280dd-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
