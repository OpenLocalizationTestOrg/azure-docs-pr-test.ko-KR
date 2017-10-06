---
title: "PowerShell 스크립트 샘플-aaaAzure 할당할 사용자 지정 도메인 tooa 웹 응용 프로그램 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-사용자 지정 도메인 tooa 웹 응용 프로그램 할당"
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
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="ff6b5-103">사용자 지정 도메인 tooa 웹 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="ff6b5-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="ff6b5-104">이 샘플 스크립트는 웹 앱 앱 서비스에서과 해당 관련된 리소스를 만들고 다음 매핑합니다 `www.<yourdomain>` tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="ff6b5-105">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="ff6b5-106">또한 toohave 액세스 tooyour 도메인 등록자의 DNS 구성 페이지가 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ff6b5-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ff6b5-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ff6b5-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ff6b5-108">Clean up deployment</span></span> 

<span data-ttu-id="ff6b5-109">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 웹 앱 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="ff6b5-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ff6b5-110">Script explanation</span></span>

<span data-ttu-id="ff6b5-111">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-111">This script uses hello following commands.</span></span> <span data-ttu-id="ff6b5-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ff6b5-113">명령</span><span class="sxs-lookup"><span data-stu-id="ff6b5-113">Command</span></span> | <span data-ttu-id="ff6b5-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ff6b5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff6b5-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ff6b5-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ff6b5-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ff6b5-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ff6b5-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="ff6b5-118">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ff6b5-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="ff6b5-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="ff6b5-120">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-120">Creates a web app.</span></span> |
| [<span data-ttu-id="ff6b5-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ff6b5-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="ff6b5-122">앱 서비스 계획 toochange 해당 가격 책정 계층을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="ff6b5-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="ff6b5-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="ff6b5-124">웹앱의 구성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff6b5-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff6b5-125">Next steps</span></span>

<span data-ttu-id="ff6b5-126">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ff6b5-127">Azure 앱 서비스 웹 앱에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../app-service-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6b5-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
