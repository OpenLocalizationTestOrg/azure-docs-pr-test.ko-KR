---
title: "aaaCopy 기계 학습 예제에서는 실험-Azure | Microsoft Docs"
description: "Toouse 예제 기계 학습 toocreate 새 실험 Cortana 인텔리전스 갤러리 및 Microsoft Azure 기계 학습 실험 하는 방법에 대해 알아봅니다."
keywords: "기계 학습 예제, 샘플 실험, 기계 학습 샘플"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 555f05cf9af2040d1703707f7583396d5da9f156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-example-experiments-toocreate-new-machine-learning-experiments"></a>예제에서는 실험 toocreate 새 기계 학습 실험 복사
toostart 예제로 실험 하는 방법에 대해 알아봅니다 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/) 기계 학습 실험 처음부터 새로 만드는 대신 합니다. 사용자 고유의 기계 학습 솔루션 hello 예제 toobuild를 사용할 수 있습니다.

hello 갤러리 hello Microsoft Azure 기계 학습 팀과 hello 기계 학습 커뮤니티에서 공유 하 여 예제에서는 실험에 있습니다. 실험에 대한 질문을 하거나 의견을 게시할 수도 있습니다.

hello 3 분 비디오를 시청 하세요 toouse hello 갤러리, 방법 toosee [타인의 작업 toodo 데이터 과학 복사](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) hello 계열에서 [초보자를 위한 데이터 과학](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-toocopy-in-cortana-intelligence-gallery"></a>실험 toocopy Cortana 인텔리전스 갤러리에서 찾기
toosee 어떤 실험은 사용할 수 있는, 이동 toohello [갤러리](https://gallery.cortanaintelligence.com/) 클릭 **실험** hello hello 페이지 위쪽에 있습니다.

### <a name="find-hello-newest-or-most-popular-experiments"></a>최신 또는 가장 인기 있는 실험 hello 찾기
이 페이지에서 확인할 수 있습니다 **최근에 추가 된** 실험, 또는 toolook에서 아래로 스크롤하여 **인기 있는 이란** 또는 hello 최신 **인기 있는 Microsoft 실험**합니다.

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a>특정 요구 사항을 충족하는 실험 찾기
모든 toobrowse 실험:

1. 클릭 **모두 찾아보기** hello hello 페이지 위쪽에 있습니다.
2. Hello 왼쪽에 아래 **지정 하 여 구체화** hello에 **범주** 섹션에서 **실험** 의 실험 hello 모든 toosee hello 갤러리입니다.
3. 두 가지 방법으로 요구 사항을 충족하는 실험을 찾을 수 있습니다.
   * **Hello 왼쪽에 필터를 선택 합니다.** PCA 기반 비정상 검색 알고리즘을 사용 하는 toobrowse 실험 예를 들어:와 **실험** 아래에서 선택한 **범주**, 클릭 **모두 표시**합니다. 그런 다음 **사용된 알고리즘**에서 **PCA 기반 변칙 검색**을 선택합니다. <br></br>
     ![필터 선택](./media/machine-learning-sample-experiments/refine-the-view.png)
   * **Hello 검색 상자를 사용 합니다.** Toofind 실험 관련 Microsoft가 제공 하는 예를 들어 2 클래스 지원 벡터 컴퓨터 알고리즘을 사용 하는 toodigit 인식 hello 검색 상자에 "자리 인식"를 입력 합니다. 그런 다음 선택 hello 필터 **실험**, **Microsoft 콘텐츠만**, 및 **2 클래스 지원 벡터 컴퓨터**:<br></br>
     ![Hello 검색 상자를 사용 하 여](./media/machine-learning-sample-experiments/search-for-experiments.png)
4. 항목에 대 한 자세한는 실험 toolearn를 클릭 합니다.
5. toorun hello 실험을 수정, 클릭 하 여 및/또는 **Studio에서 열기** hello 실험 페이지에 있습니다. <br></br>

    ![예제 실험](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > 을 열 때 실험 기계 학습 스튜디오에서 hello에 대 한 처음으로 무료로 시도 또는 Azure 구독을 구입할 수 있습니다. [Hello 기계 학습 스튜디오 무료 평가판 및 유료 서비스에 알아보기](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a>예제를 템플릿으로 사용하여 새 실험 만들기
갤러리 예제를 템플릿으로 사용하여 Machine Learning Studio에서 새 실험을 만들 수도 있습니다.

1. Microsoft 계정 자격 증명 toohello 프로그램 इ न क [Studio](https://studio.azureml.net), 클릭 하 고 **새로** toocreate 실험 합니다.
2. Hello 예제 콘텐츠 하나를 클릭 합니다.

새 실험 hello 예제에서는 실험을 템플릿으로 사용 하 여 기계 학습 스튜디오 작업 영역에서 만들어집니다.

## <a name="next-steps"></a>다음 단계
* [다양한 소스에서 데이터 가져오기](machine-learning-data-science-import-data.md)
* [기계 학습에서 hello R 언어에 대 한 빠른 시작 자습서](machine-learning-r-quickstart.md)
* [Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)
