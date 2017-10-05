---
title: "1단계: Machine Learning 작업 영역 만들기 | Microsoft Docs"
description: "예측 솔루션 개발 연습 1단계: 새 Azure 기계 학습 스튜디오 작업 영역을 설정하는 방법을 알아봅니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="0bd21-103">연습 1단계: 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="0bd21-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="0bd21-104">[Azure 기계 학습에서 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)연습의 첫 번째 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="0bd21-105">**기계 학습 작업 영역 만들기**</span><span class="sxs-lookup"><span data-stu-id="0bd21-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="0bd21-106">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="0bd21-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="0bd21-107">새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="0bd21-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="0bd21-108">모델 학습 및 평가</span><span class="sxs-lookup"><span data-stu-id="0bd21-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="0bd21-109">웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="0bd21-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="0bd21-110">웹 서비스 액세스</span><span class="sxs-lookup"><span data-stu-id="0bd21-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="0bd21-111">기계 학습 스튜디오를 사용하려면 Microsoft Azure 기계 학습 작업 영역이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="0bd21-112">이 작업 영역에는 실험을 만들고 관리, 게시하는 데 필요한 도구가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="0bd21-113">Azure 구독에 대한 관리자는 작업 영역을 만들고 소유자 또는 참가자로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="0bd21-114">자세한 내용은 [Azure Machine Learning 작업 영역 만들기 및 공유](machine-learning-create-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0bd21-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="0bd21-115">작업 영역을 만든 후 Machine Learning Studio([https://studio.azureml.net/Home](https://studio.azureml.net/Home))를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="0bd21-116">둘 이상의 작업 영역이 있는 경우 창의 오른쪽 위 모서리에 있는 도구 모음에서 작업 영역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Studio에서 작업 영역 선택][2]

> [!TIP]
> <span data-ttu-id="0bd21-118">작업 영역의 소유자인 경우 나중에 작업 영역에 다른 사용자를 초대하여 작업 중인 실험을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="0bd21-119">기계 학습 스튜디오의 **SETTINGS** 페이지에서 이 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="0bd21-120">각 사용자에 대한 Microsoft 계정 또는 조직 계정만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="0bd21-121">**설정** 페이지에서 **사용자**를 클릭한 다음 창의 아래쪽에 있는 **더 많은 사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0bd21-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="0bd21-122">**다음: [기존 데이터 업로드](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="0bd21-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
