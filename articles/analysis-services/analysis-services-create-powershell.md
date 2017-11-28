---
title: "PowerShell을 사용 하 여 Azure Analysis Services 서버 aaaCreate | Microsoft Docs"
description: "자세한 방법을 toocreate Azure Analysis Services PowerShell을 사용 하 여 서버"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="b46f7-103">PowerShell을 사용하여 Azure Analysis Services 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="b46f7-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="b46f7-104">이 퀵 스타트의 설명에서 사용 하 여 PowerShell hello 명령줄 toocreate Azure Analysis Services 서버에는 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md) Azure 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="b46f7-105">이 작업을 수행하려면 Azure PowerShell 모듈 버전 4.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="b46f7-106">toofind hello 버전을 실행 ` Get-Module -ListAvailable AzureRM`합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="b46f7-107">tooinstall 또는 업그레이드를 참조 하세요. [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="b46f7-108">서버를 만들면 새로운 유료 서비스가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="b46f7-109">toolearn 더 참조 [Analysis Services 가격](https://azure.microsoft.com/pricing/details/analysis-services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b46f7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b46f7-110">Prerequisites</span></span>
<span data-ttu-id="b46f7-111">toocomplete 해야이 빠른 시작:</span><span class="sxs-lookup"><span data-stu-id="b46f7-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="b46f7-112">**Azure 구독**: 방문 [Azure 무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate 계정.</span><span class="sxs-lookup"><span data-stu-id="b46f7-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="b46f7-113">**Azure Active Directory**: 구독이 Azure Active Directory 테넌트와 연결되어 있고 해당 디렉터리에 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="b46f7-114">toolearn 더 참조 [인증 및 사용자 권한을](analysis-services-manage-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="b46f7-115">AzureRm.AnalysisServices 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="b46f7-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="b46f7-116">hello를 사용 하면 구독에 서버 toocreate [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) 모듈 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="b46f7-117">PowerShell 세션에 hello AzureRm.AnalysisServices 모듈을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="b46f7-118">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="b46f7-118">Sign in tooAzure</span></span>

<span data-ttu-id="b46f7-119">Hello를 사용 하 여 Azure 구독 tooyour 로그인 [추가 AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="b46f7-120">지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="b46f7-121">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b46f7-121">Create a resource group</span></span>
 
<span data-ttu-id="b46f7-122">[Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="b46f7-123">서버를 만들 때 구독에서 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="b46f7-124">리소스 그룹이 아직 없는 경우 hello를 사용 하 여 한 새를 만들 수 있습니다 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="b46f7-125">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello 미국 서 부 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="b46f7-126">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="b46f7-126">Create a server</span></span>

<span data-ttu-id="b46f7-127">Hello를 사용 하 여 새 서버 만들기 [새로 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="b46f7-128">hello 다음 예제에서는 hello D1 계층에서는 hello 미국 서 부 지역에서 myResourceGroup myServer 라는 서버를 만들고 지정 philipc@adventureworks.com 서버 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="b46f7-129">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="b46f7-129">Clean up resources</span></span>

<span data-ttu-id="b46f7-130">Hello를 사용 하 여 hello 서버 구독에서 제거할 수 있습니다 [제거 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="b46f7-131">이 컬렉션의 다른 빠른 시작 및 자습서로 계속하는 경우에는 서버를 제거하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b46f7-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="b46f7-132">hello 다음 예제에서는 hello 서버를 제거 hello 이전 단계에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="b46f7-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="b46f7-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b46f7-133">Next steps</span></span>
<span data-ttu-id="b46f7-134">[PowerShell을 사용하여 Azure Analysis Services 관리](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="b46f7-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="b46f7-135">[SSDT에서 모델 배포](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="b46f7-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="b46f7-136">Azure Portal에서 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="b46f7-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)