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
# <a name="multi-geo-help-documentation"></a>다중 지역 도움말 문서
이 문서에서는 다른 Azure 지역에서 작업 영역을 만들고 웹 서비스를 게시하는 방법을 설명합니다.  hello [영역 페이지에서 Azure 제품](https://azure.microsoft.com/en-us/regions/services/) Azure 기계 학습을 사용할 수 있는 영역을 나열 합니다.

## <a name="create-a-workspace"></a>작업 영역 만들기
1. Toohello Azure 클래식 포털에에서 로그인 합니다.
2. **+새로 만들기** > **Data Services** > **Machine Learning** > **빠른 생성**을 클릭합니다.  **위치**에서 다른 지역(예: **동남 아시아**)을 선택합니다.
   ![다중 지역 도움말 이미지 1][1]
3. Hello 작업 영역을 선택한 다음 클릭 **로그인 tooML Studio**합니다.
   ![다중 지역 도움말 이미지 2][2]
4. 이제 다른 작업 영역처럼 사용할 수 있는 작업 영역이 다른 지역에 생겼습니다. tooswitch의 작업 영역 간에 모양 toohello 오른쪽 상단의 화면입니다. Hello 드롭다운, 선택 hello 지역 및 선택 hello 작업 영역을 클릭 합니다. 모든 로컬 toohello 작업 영역의 영역입니다.  예를 들어 동일한 지역에 대 한 hello 작업 영역에 있는 hello에는 모든 작업 영역에서 만든 웹 서비스에이 됩니다.
   ![다중 지역 도움말 이미지 3][3]

## <a name="open-an-experiment-from-gallery"></a>갤러리에서 실험 열기
갤러리에서 실험을 열면 toocopy hello 실험을 원하는 어떤 지역이 선택할 수 있습니다.

![다중 지역 도움말 이미지 4][4a]

## <a name="web-service-management"></a>웹 서비스 관리
tooprogrammatically 재교육 hello 지역별 주소를 사용 하는 것에 대 한와 같은 웹 서비스를 관리:

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-toonote"></a>작업 toonote
1. 실험 toohello 속해 있는 작업 영역 간에 복사할 수 있습니다 이러한 방식으로 같은 지역입니다. Toocopy 실험 해야 할 경우 다른 지역에 작업 영역에서 hello를 사용할 수 있습니다 [PowerShell](http://aka.ms/amlps) commandlet [ *복사 AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish입니다. 다른 해결 방법을 나열 되지 않은 모드에서 toopublish hello 실험 갤러리에는 다음 hello 작업 영역에서에서 열 hello 다른 지역.
2. hello 지역 선택기 한 번에 하나의 영역에 대 한 작업 영역 표시 됩니다.  
3. 무료 작업 영역 또는 게스트 액세스(익명) 작업 영역은 미국 중남부에서 만들어지고 호스트됩니다.  
4. 동남 아시아의 작업 영역에서 배포된 웹 서비스는 호스팅도 동남 아시아에서 이루어집니다.  

## <a name="more-information"></a>자세한 정보
Hello에 대해 질문 [Azure 기계 학습 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning)합니다.

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
