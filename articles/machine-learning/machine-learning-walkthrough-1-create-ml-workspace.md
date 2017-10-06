---
title: "1단계: Machine Learning 작업 영역 만들기 | Microsoft Docs"
description: "예측 솔루션 연습을 개발 하는 hello의 1 단계: 자세한 방법을 tooset 새 Azure 기계 학습 스튜디오 작업 영역을 합니다."
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
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="61121-103">연습 1단계: 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="61121-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="61121-104">이 hello 연습의 첫 번째 단계 hello [Azure 기계 학습에서 예측 분석 솔루션을 개발](machine-learning-walkthrough-develop-predictive-solution.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="61121-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="61121-105">**기계 학습 작업 영역 만들기**</span><span class="sxs-lookup"><span data-stu-id="61121-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="61121-106">기존 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="61121-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="61121-107">새 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="61121-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="61121-108">학습 하 고 hello 모델 평가</span><span class="sxs-lookup"><span data-stu-id="61121-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="61121-109">Hello 웹 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="61121-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="61121-110">Hello 웹 서비스에 액세스</span><span class="sxs-lookup"><span data-stu-id="61121-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="61121-111">기계 학습 스튜디오 toouse toohave Microsoft Azure 기계 학습 작업 영역 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="61121-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="61121-112">이 작업 영역에 toocreate 필요한 hello 도구, 관리 하 고 실험을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61121-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="61121-113">Azure 구독에 대 한 관리자에 게 필요한 toocreate hello 작업 영역을 소유자 또는 참가자 수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="61121-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="61121-114">자세한 내용은 [Azure Machine Learning 작업 영역 만들기 및 공유](machine-learning-create-workspace.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61121-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="61121-115">작업 영역을 만든 후 Machine Learning Studio([https://studio.azureml.net/Home](https://studio.azureml.net/Home))를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="61121-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="61121-116">둘 이상의 작업 영역을 사용 하는 경우에 hello 창의 hello 오른쪽 위 모서리에 hello 도구 모음에서 hello 작업 영역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61121-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Studio에서 작업 영역 선택][2]

> [!TIP]
> <span data-ttu-id="61121-118">Hello 작업 영역의 소유자 사항이 경우 다른 사용자를 초대 하 여 작업 중인 hello 실험을 공유할 수 있습니다 toohello 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="61121-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="61121-119">Hello에 기계 학습 스튜디오에서 이렇게 하려면 **설정을** 페이지.</span><span class="sxs-lookup"><span data-stu-id="61121-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="61121-120">하기만 하면 hello Microsoft 계정 또는 조직 계정을 각 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="61121-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="61121-121">Hello에 **설정** 페이지에서 **사용자**, 클릭 **더 사용자 초대** hello hello 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61121-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="61121-122">**다음: [기존 데이터 업로드](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="61121-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
