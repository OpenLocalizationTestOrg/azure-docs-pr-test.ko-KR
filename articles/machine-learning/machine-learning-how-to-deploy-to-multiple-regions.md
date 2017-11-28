---
title: "웹 서비스 aaaHow toodeploy toomultiple 영역 | Microsoft Docs"
description: "단계 toodeploy (복사) 새 웹 서비스 tooother 영역입니다."
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
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="c13ff-103">어떻게 toodeploy 웹 서비스 toomultiple 영역</span><span class="sxs-lookup"><span data-stu-id="c13ff-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="c13ff-104">hello 새 Azure 웹 서비스를 사용 하면 tooeasily 여러 구독 또는 작업 영역 필요 없이 웹 서비스 toomultiple 영역을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="c13ff-105">가격 책정은 지역별로 고유 하므로는 hello 웹 서비스를 배포할 각 지역에 대 한 청구 계획을 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="c13ff-106">toocreate 다른 지역에 계획</span><span class="sxs-lookup"><span data-stu-id="c13ff-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="c13ff-107">[Microsoft Azure 기계 학습 웹 서비스](https://services.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="c13ff-108">Hello 클릭 **계획** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="c13ff-109">보기 페이지를 덮어쓰며 hello 계획, 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="c13ff-110">Hello에서 **구독** 드롭다운에서 hello 새 계획 상주할 선택 hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="c13ff-111">Hello에서 **지역** 드롭다운에서 hello 새 계획에 대 한 지역 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="c13ff-112">hello 선택한 영역에 대 한 계획 옵션 hello hello에 표시 됩니다 **계획 옵션** hello 페이지의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="c13ff-113">Hello에서 **리소스 그룹** 드롭다운을 선택 hello 계획에 대 한 리소스를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="c13ff-114">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c13ff-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="c13ff-115">**계획 이름** hello 계획의 hello 이름 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="c13ff-116">아래 **계획 옵션**, hello 새 계획에 대 한 hello 청구 수준을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="c13ff-117">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="c13ff-118">Hello 웹 서비스 tooanother 영역 배포</span><span class="sxs-lookup"><span data-stu-id="c13ff-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="c13ff-119">Hello 클릭 **웹 서비스** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="c13ff-120">Hello tooa 새 영역을 배포 하는 웹 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="c13ff-121">**복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-121">Click **Copy**.</span></span>
4. <span data-ttu-id="c13ff-122">**웹 서비스 이름이**를 hello 웹 서비스에 대 한 새 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="c13ff-123">**웹 서비스 기술**를 hello 웹 서비스에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="c13ff-124">Hello에서 **구독** 드롭다운을 새 웹 서비스는 hello에 상주할 선택 hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="c13ff-125">Hello에서 **리소스 그룹** 드롭다운을 선택 hello 웹 서비스에 대 한 리소스를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="c13ff-126">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c13ff-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="c13ff-127">Hello에서 **지역** 드롭다운에서 toodeploy hello 웹 서비스에서 선택 hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="c13ff-128">Hello에서 **저장소 계정** 드롭다운을 선택는 toostore hello에서 저장소 계정을 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="c13ff-129">Hello에서 **가격 계획** 드롭다운에서 8 단계에서 선택한 hello 지역에 대 한 계획을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="c13ff-130">**복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c13ff-130">Click **Copy**.</span></span>

