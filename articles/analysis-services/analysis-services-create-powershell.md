---
title: "PowerShell을 사용하여 Azure Analysis Services 서버 만들기 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure Analysis Services 서버를 만드는 방법 알아보기"
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
ms.openlocfilehash: cb42fd3ed51364cf478848cc51ebbb2f175e96d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="8eca8-103">PowerShell을 사용하여 Azure Analysis Services 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="8eca8-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="8eca8-104">이 빠른 시작은 Azure 구독의 [Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)에서 Azure Analysis Services 서버를 만들기 위해 명령줄에서 PowerShell 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="8eca8-105">이 작업을 수행하려면 Azure PowerShell 모듈 버전 4.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="8eca8-106">버전을 찾으려면 ` Get-Module -ListAvailable AzureRM`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-106">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="8eca8-107">설치 또는 업그레이드하려면 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eca8-107">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="8eca8-108">서버를 만들면 새로운 유료 서비스가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="8eca8-109">자세한 내용은 [Analysis Services 가격 책정](https://azure.microsoft.com/pricing/details/analysis-services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eca8-109">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8eca8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8eca8-110">Prerequisites</span></span>
<span data-ttu-id="8eca8-111">이 빠른 시작을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-111">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="8eca8-112">**Azure 구독**: [Azure 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/)으로 이동하여 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="8eca8-113">**Azure Active Directory**: 구독이 Azure Active Directory 테넌트와 연결되어 있고 해당 디렉터리에 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="8eca8-114">자세한 내용은 [인증 및 사용자 권한](analysis-services-manage-users.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eca8-114">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="8eca8-115">AzureRm.AnalysisServices 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="8eca8-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="8eca8-116">구독에서 서버를 만들려면 [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) 구성 요소 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-116">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="8eca8-117">PowerShell 세션으로 AzureRm.AnalysisServices 모듈을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-117">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a><span data-ttu-id="8eca8-118">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="8eca8-118">Sign in to Azure</span></span>

<span data-ttu-id="8eca8-119">[Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) 명령을 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-119">Sign in to your Azure subscription by using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="8eca8-120">화면에 나타나는 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-120">Follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="8eca8-121">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8eca8-121">Create a resource group</span></span>
 
<span data-ttu-id="8eca8-122">[Azure 리소스 그룹](../azure-resource-manager/resource-group-overview.md)은 Azure 리소스가 그룹으로 배포되고 관리되는 논리 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="8eca8-123">서버를 만들 때 구독에서 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="8eca8-124">아직 리소스 그룹이 없는 경우 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 명령을 사용하여 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-124">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="8eca8-125">다음 예제에서는 미국 서부 지역의 `myResourceGroup`라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-125">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="8eca8-126">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="8eca8-126">Create a server</span></span>

<span data-ttu-id="8eca8-127">[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) 명령을 사용하여 새 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-127">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="8eca8-128">다음 예제에서는 D1 계층, 미국 서부 지역, myResourceGroup에서 myServer라는 서버를 만들고 서버 관리자로 philipc@adventureworks.com을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-128">The following example creates a server named myServer in myResourceGroup, in the West US region, at the D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="8eca8-129">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="8eca8-129">Clean up resources</span></span>

<span data-ttu-id="8eca8-130">[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) 명령을 사용하여 구독에서 서버를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-130">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="8eca8-131">이 컬렉션의 다른 빠른 시작 및 자습서로 계속하는 경우에는 서버를 제거하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8eca8-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="8eca8-132">다음 예제에서는 이전 단계에서 만든 서버를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8eca8-132">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="8eca8-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8eca8-133">Next steps</span></span>
<span data-ttu-id="8eca8-134">[PowerShell을 사용하여 Azure Analysis Services 관리](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="8eca8-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="8eca8-135">[SSDT에서 모델 배포](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="8eca8-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="8eca8-136">Azure Portal에서 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="8eca8-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)