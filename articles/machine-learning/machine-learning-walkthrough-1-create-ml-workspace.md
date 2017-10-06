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
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a>연습 1단계: 기계 학습 작업 영역 만들기
이 hello 연습의 첫 번째 단계 hello [Azure 기계 학습에서 예측 분석 솔루션을 개발](machine-learning-walkthrough-develop-predictive-solution.md)합니다.

1. **기계 학습 작업 영역 만들기**
2. [기존 데이터 업로드](machine-learning-walkthrough-2-upload-data.md)
3. [새 실험 만들기](machine-learning-walkthrough-3-create-new-experiment.md)
4. [학습 하 고 hello 모델 평가](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Hello 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)
6. [Hello 웹 서비스에 액세스](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

기계 학습 스튜디오 toouse toohave Microsoft Azure 기계 학습 작업 영역 필요합니다. 이 작업 영역에 toocreate 필요한 hello 도구, 관리 하 고 실험을 게시 합니다.  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

Azure 구독에 대 한 관리자에 게 필요한 toocreate hello 작업 영역을 소유자 또는 참가자 수를 추가 합니다. 자세한 내용은 [Azure Machine Learning 작업 영역 만들기 및 공유](machine-learning-create-workspace.md)를 참조하세요.

작업 영역을 만든 후 Machine Learning Studio([https://studio.azureml.net/Home](https://studio.azureml.net/Home))를 엽니다. 둘 이상의 작업 영역을 사용 하는 경우에 hello 창의 hello 오른쪽 위 모서리에 hello 도구 모음에서 hello 작업 영역을 선택할 수 있습니다.

![Studio에서 작업 영역 선택][2]

> [!TIP]
> Hello 작업 영역의 소유자 사항이 경우 다른 사용자를 초대 하 여 작업 중인 hello 실험을 공유할 수 있습니다 toohello 작업 영역입니다. Hello에 기계 학습 스튜디오에서 이렇게 하려면 **설정을** 페이지. 하기만 하면 hello Microsoft 계정 또는 조직 계정을 각 사용자에 대 한 합니다.
> 
> Hello에 **설정** 페이지에서 **사용자**, 클릭 **더 사용자 초대** hello hello 창 맨 아래에 있습니다.
> 
> 

- - -
**다음: [기존 데이터 업로드](machine-learning-walkthrough-2-upload-data.md)**

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
