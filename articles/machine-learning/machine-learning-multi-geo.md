---
title: "다중 지역 도움말 문서 | Microsoft Docs"
description: "SCUS(미국 중남부) Azure 지역이 아닌 다른 Azure 지역에서 작업 영역을 만들고 웹 서비스를 게시하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="8ec3f-103">다중 지역 도움말 문서</span><span class="sxs-lookup"><span data-stu-id="8ec3f-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="8ec3f-104">이 문서에서는 다른 Azure 지역에서 작업 영역을 만들고 웹 서비스를 게시하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="8ec3f-105">[지역별 Azure 제품 페이지](https://azure.microsoft.com/en-us/regions/services/)는 Azure Machine Learning을 사용할 수 있는 지역을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="8ec3f-106">작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="8ec3f-106">Create a workspace</span></span>
1. <span data-ttu-id="8ec3f-107">Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="8ec3f-108">**+새로 만들기** > **Data Services** > **Machine Learning** > **빠른 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="8ec3f-109">**위치**에서 다른 지역(예: **동남 아시아**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="8ec3f-110">![다중 지역 도움말 이미지 1][1]</span><span class="sxs-lookup"><span data-stu-id="8ec3f-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="8ec3f-111">작업 영역을 선택한 다음 **기계 학습 스튜디오에 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="8ec3f-112">![다중 지역 도움말 이미지 2][2]</span><span class="sxs-lookup"><span data-stu-id="8ec3f-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="8ec3f-113">이제 다른 작업 영역처럼 사용할 수 있는 작업 영역이 다른 지역에 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="8ec3f-114">작업 영역 간에 전환하려면 화면의 오른쪽 위를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="8ec3f-115">드롭다운을 클릭하고 지역을 선택한 다음 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="8ec3f-116">모든 항목은 작업 영역 지역에 대해 로컬입니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="8ec3f-117">예를 들어 작업 영역에서 만든 모든 웹 서비스는 작업 영역이 있는 지역과 같은 지역에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="8ec3f-118">![다중 지역 도움말 이미지 3][3]</span><span class="sxs-lookup"><span data-stu-id="8ec3f-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="8ec3f-119">갤러리에서 실험 열기</span><span class="sxs-lookup"><span data-stu-id="8ec3f-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="8ec3f-120">갤러리에서 실험을 열면 실험을 복사할 지역도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![다중 지역 도움말 이미지 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="8ec3f-122">웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="8ec3f-122">Web service management</span></span>
<span data-ttu-id="8ec3f-123">프로그래밍 방식으로 웹 서비스를 관리하려면(예: 다시 학습을 위해) 지역별 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="8ec3f-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="8ec3f-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="8ec3f-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="8ec3f-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="8ec3f-126">주의할 사항</span><span class="sxs-lookup"><span data-stu-id="8ec3f-126">Things to note</span></span>
1. <span data-ttu-id="8ec3f-127">같은 지역에 속하는 작업 영역 간에만 실험을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="8ec3f-128">다른 지역의 작업 영역 간에 실험을 복사해야 하는 경우 [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment)를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="8ec3f-129">또 다른 해결 방법은 나열되지 않는 모드로 갤러리에 실험을 게시한 다음 다른 지역의 작업 영역에서 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="8ec3f-130">지역 선택기는 한 번에 한 지역의 작업 영역만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="8ec3f-131">무료 작업 영역 또는 게스트 액세스(익명) 작업 영역은 미국 중남부에서 만들어지고 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="8ec3f-132">동남 아시아의 작업 영역에서 배포된 웹 서비스는 호스팅도 동남 아시아에서 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="8ec3f-133">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="8ec3f-133">More information</span></span>
<span data-ttu-id="8ec3f-134">[Azure 기계 학습 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning)에서 질문하세요.</span><span class="sxs-lookup"><span data-stu-id="8ec3f-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
