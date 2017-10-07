---
title: "aaaMulti 지역 도움말 설명서 | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate 작업 영역 hello 남 중앙 미국 (SCUS)와에서 다른 Azure 지역에서 웹 서비스를 게시 하 고 Azure 지역입니다."
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="e4031-103">다중 지역 도움말 문서</span><span class="sxs-lookup"><span data-stu-id="e4031-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="e4031-104">이 문서에서는 다른 Azure 지역에서 작업 영역을 만들고 웹 서비스를 게시하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="e4031-105">hello [영역 페이지에서 Azure 제품](https://azure.microsoft.com/en-us/regions/services/) Azure 기계 학습을 사용할 수 있는 영역을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="e4031-106">작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="e4031-106">Create a workspace</span></span>
1. <span data-ttu-id="e4031-107">Toohello Azure 클래식 포털에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="e4031-108">**+새로 만들기** > **Data Services** > **Machine Learning** > **빠른 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="e4031-109">**위치**에서 다른 지역(예: **동남 아시아**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="e4031-110">![다중 지역 도움말 이미지 1][1]</span><span class="sxs-lookup"><span data-stu-id="e4031-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="e4031-111">Hello 작업 영역을 선택한 다음 클릭 **로그인 tooML Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="e4031-112">![다중 지역 도움말 이미지 2][2]</span><span class="sxs-lookup"><span data-stu-id="e4031-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="e4031-113">이제 다른 작업 영역처럼 사용할 수 있는 작업 영역이 다른 지역에 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="e4031-114">tooswitch의 작업 영역 간에 모양 toohello 오른쪽 상단의 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="e4031-115">Hello 드롭다운, 선택 hello 지역 및 선택 hello 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="e4031-116">모든 로컬 toohello 작업 영역의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="e4031-117">예를 들어 동일한 지역에 대 한 hello 작업 영역에 있는 hello에는 모든 작업 영역에서 만든 웹 서비스에이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="e4031-118">![다중 지역 도움말 이미지 3][3]</span><span class="sxs-lookup"><span data-stu-id="e4031-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="e4031-119">갤러리에서 실험 열기</span><span class="sxs-lookup"><span data-stu-id="e4031-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="e4031-120">갤러리에서 실험을 열면 toocopy hello 실험을 원하는 어떤 지역이 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![다중 지역 도움말 이미지 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="e4031-122">웹 서비스 관리</span><span class="sxs-lookup"><span data-stu-id="e4031-122">Web service management</span></span>
<span data-ttu-id="e4031-123">tooprogrammatically 재교육 hello 지역별 주소를 사용 하는 것에 대 한와 같은 웹 서비스를 관리:</span><span class="sxs-lookup"><span data-stu-id="e4031-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="e4031-124">https://asiasoutheast.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="e4031-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="e4031-125">https://europewest.management.azureml.net</span><span class="sxs-lookup"><span data-stu-id="e4031-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="e4031-126">작업 toonote</span><span class="sxs-lookup"><span data-stu-id="e4031-126">Things toonote</span></span>
1. <span data-ttu-id="e4031-127">실험 toohello 속해 있는 작업 영역 간에 복사할 수 있습니다 이러한 방식으로 같은 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="e4031-128">Toocopy 실험 해야 할 경우 다른 지역에 작업 영역에서 hello를 사용할 수 있습니다 [PowerShell](http://aka.ms/amlps) commandlet [ *복사 AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish입니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="e4031-129">다른 해결 방법을 나열 되지 않은 모드에서 toopublish hello 실험 갤러리에는 다음 hello 작업 영역에서에서 열 hello 다른 지역.</span><span class="sxs-lookup"><span data-stu-id="e4031-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="e4031-130">hello 지역 선택기 한 번에 하나의 영역에 대 한 작업 영역 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="e4031-131">무료 작업 영역 또는 게스트 액세스(익명) 작업 영역은 미국 중남부에서 만들어지고 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="e4031-132">동남 아시아의 작업 영역에서 배포된 웹 서비스는 호스팅도 동남 아시아에서 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="e4031-133">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e4031-133">More information</span></span>
<span data-ttu-id="e4031-134">Hello에 대해 질문 [Azure 기계 학습 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4031-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
