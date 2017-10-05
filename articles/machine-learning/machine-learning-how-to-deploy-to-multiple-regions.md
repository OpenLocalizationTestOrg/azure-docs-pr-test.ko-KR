---
title: "여러 지역에 Web Service를 배포하는 방법 | Microsoft Docs"
description: "새 웹 서비스를 다른 영역을 배포(복사)하는 단계입니다."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="2887e-103">여러 지역에 웹 서비스를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="2887e-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="2887e-104">새 Azure 웹 서비스를 사용하면 여러 구독 또는 작업 영역 없이 여러 지역에 웹 서비스를 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="2887e-105">가격 책정은 지역별로 이루어집니다. 따라서 웹 서비스를 배포할 각 지역에 대한 청구 계획을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="2887e-106">다른 지역에 계획을 만들려면</span><span class="sxs-lookup"><span data-stu-id="2887e-106">To create a plan in another region</span></span>
1. <span data-ttu-id="2887e-107">[Microsoft Azure 기계 학습 웹 서비스](https://services.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="2887e-108">**계획** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="2887e-109">보기 페이지의 계획에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="2887e-110">**구독** 드롭다운에서 새 계획이 상주할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="2887e-111">**지역** 드롭다운에서 새 계획에 대한 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="2887e-112">선택한 영역에 대한 계획 옵션은 페이지의 **계획 옵션** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="2887e-113">**리소스 그룹** 드롭다운에서 계획에 대한 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="2887e-114">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2887e-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="2887e-115">**계획 이름** 에 계획의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="2887e-116">**계획 옵션**에서 새 계획에 대한 청구 수준을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="2887e-117">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="2887e-118">다른 지역에 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="2887e-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="2887e-119">**웹 서비스** 메뉴 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="2887e-120">새 지역에 배포하는 웹 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="2887e-121">**복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-121">Click **Copy**.</span></span>
4. <span data-ttu-id="2887e-122">**웹 서비스 이름**에 웹 서비스의 새 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="2887e-123">**웹 서비스 설명**에 웹 서비스에 대한 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="2887e-124">**구독** 드롭다운에서 새 웹 서비스가 상주할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="2887e-125">**리소스 그룹** 드롭다운에서 웹 서비스에 대한 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="2887e-126">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2887e-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="2887e-127">**지역** 드롭다운에서 웹 서비스를 배포할 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="2887e-128">**저장소 계정** 드롭다운에서 웹 서비스에 저장할 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="2887e-129">**가격 계획** 드롭다운에서 8단계에서 선택한 영역에서 계획을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="2887e-130">**복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2887e-130">Click **Copy**.</span></span>

