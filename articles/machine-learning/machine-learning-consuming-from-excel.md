---
title: "Excel에서 기계 학습 웹 서비스 aaaConsume | Microsoft Docs"
description: "Excel에서 Azure 기계 학습 웹 서비스 사용"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Excel에서 Azure 기계 학습 웹 서비스 사용
 Azure 기계 학습 스튜디오 하면 Excel에서 직접 웹 서비스를 쉽게 toocall hello toowrite 모든 코드가 필요 하지 않고 있습니다.

Excel 2013 또는 그 이상의 또는 Excel Online을 사용 하는 경우 Excel hello를 사용 하는 것이 좋습니다 [Excel 추가 기능](machine-learning-excel-add-in-for-web-services.md)합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>단계
웹 서비스를 게시합니다. [이 페이지](machine-learning-walkthrough-5-publish-web-service.md) 설명 어떻게 toodo 것입니다. 현재 hello Excel 통합 문서 기능을 단일 출력 (즉, 단일 점수 매기기 레이블) 있는 요청/응답 서비스에만 지원 됩니다. 

웹 서비스를 만든 후 클릭 hello **웹 서비스** hello studio 창의 hello 왼쪽에 섹션 및 다음 Excel에서 웹 서비스 tooconsume hello를 선택 합니다.

**기존 웹 서비스**

1. Hello에 **대시보드** hello 웹 서비스는 hello에 대 한 행에 대 한 탭 **요청/응답** 서비스입니다. 이 서비스를 단일 출력 있으면 hello 나타나야 **Excel 통합 문서 다운로드** 해당 행에 링크 합니다.
   
    ![][1]
2. **Excel 통합 문서 다운로드**를 클릭합니다.

**새 웹 서비스**

1. Hello Azure 기계 학습 웹 서비스 포털에서 선택 **사용**합니다.
2. Hello 사용 페이지 hello **웹 서비스 소비 옵션** 섹션에서 hello Excel 아이콘을 클릭 합니다.

**Hello 통합 문서를 사용 하 여**

1. 통합 문서 열기 hello입니다.
2. 보안 경고가 나타납니다. hello 클릭 **편집 사용** 단추입니다.
   
    ![][2]
3. 보안 경고가 표시됩니다. Hello 클릭 **콘텐츠 사용** 스프레드시트에 toorun 매크로 단추입니다.
   
    ![][3]
4. 매크로가 활성화되면 테이블이 생성됩니다. Hello에 대 한 입력으로 필요한 열에 파란색 RR 웹 서비스 또는 **매개 변수**합니다. Hello RR 서비스의 hello 출력 참고 **PREDICTED VALUES** 녹색으로 표시 합니다. 지정된 된 행에 대 한 모든 열 가득 차면 hello 통합 문서 자동으로 hello 점수 매기기 API를 호출 하 고 hello 채 점 된 결과 표시 합니다.
   
    ![][4]
5. tooscore에 여러 행, 데이터 및 hello 채우기 hello 두 번째 행 값이 생성 되 예측 합니다. 여러 행을 한 번에 붙여 넣을 수도 있습니다.

예측 hello로 hello Excel 기능 (그래프, 파워 맵, 조건부 서식 지정, 등) 중 하나를 사용할 수 값 toohelp hello 데이터를 시각화 합니다.    

## <a name="sharing-your-workbook"></a>통합 문서 공유
Hello 매크로 toowork API 키 hello 스프레드시트의 일부 여야 합니다. 즉, 엔터티 및 개인 신뢰 에서만 hello 통합 문서를 공유 해야 합니다.

## <a name="automatic-updates"></a>자동 업데이트
RRS 호출은 다음 두 가지 상황에서 수행됩니다.

1. 처음으로 모든 행에 내용이 hello 해당 **매개 변수**
2. Hello 때마다 **매개 변수** 모든 있던 행의 변경 내용을 해당 **매개 변수** 입력 합니다.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
