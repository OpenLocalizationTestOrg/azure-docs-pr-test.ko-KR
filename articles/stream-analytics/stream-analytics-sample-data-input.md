---
title: "Azure 스트림 분석을 위한 aaa 샘플링 입력 | Microsoft Docs"
description: "Stream Analytics 작업의 문제를 해결할 때 문제를 정확히 찾아냅니다."
keywords: "입력, 입력 샘플링 문제 해결"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Azure Stream Analytics 입력 스트림 샘플링

Azure Stream Analytics를 사용 하 여 toostart 필요 없이 hello 포털에서 쿼리를 테스트 또는 작업을 중지 하 고 파일에서 제공 하는 입력된 이벤트를 샘플링할 수 있습니다.

## <a name="testing-your-query"></a>쿼리 테스트

Hello 스트림 분석 작업 세부 정보 창에서 엽니다 hello **쿼리 편집기** 아래 hello 쿼리 이름을 클릭 하 여 블레이드 **쿼리**합니다. (예제 시나리오에서는 쿼리가 아직 생성 되었으므로 클릭 하 여 hello **< >** 자리 표시자입니다.)

![hello 스트림 분석 쿼리 편집기](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

쿼리를 만들기 위한 풍부한 편집기 블레이드 hello hello 이전 버전에 포함 되어 표시 됩니다. 해당 표시 hello 입 / 출력 하는 hello 쿼리에서 사용 하는이 작업에 대해 정의 된 hello 블레이드 새으로 업데이트 되었지만 이제 왼쪽 창입니다.

![hello 스트림 분석 쿼리 편집기는 입력 값과 출력 목록](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

또한 정의되지 않은 추가 입력 및 출력이 표시됩니다. 로 시작 하는 hello 새 쿼리 템플릿을에서 온 합니다. 이러한 변경 또는 심지어 hello 쿼리를 편집할 때 완전히 사라집니다. 지금은 무시해도 무방합니다.

샘플 입력 데이터로 tootest 입력을 중 하나를 마우스 오른쪽 단추로 클릭 한 다음 선택 **파일에서 샘플 데이터 업로드**합니다.

![hello 스트림 분석 쿼리 편집기 샘플 데이터를에서 업로드 파일 명령](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Hello 업로드가 완료 되 면 클릭 **테스트** tootest hello에 대해이 쿼리 예제 데이터를 제공 합니다.

![hello 스트림 분석 쿼리 편집기 테스트 단추](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

나중에 사용할 toosave hello 테스트 출력을 원하는 경우 쿼리의 hello 출력 링크 toohello 다운로드 결과 사용 하 여 hello 브라우저에 표시 됩니다. 이제 쉽고 반복적으로 쿼리를 수정 하 고 테스트할 수 것 반복 해 서 toosee 어떻게 변경 되는지 hello 출력 합니다.

![Stream Analytics 쿼리 편집기 샘플 출력](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

Hello 이미지 앞에, 두 번째 출력 추가 되어, 호출 **HighAvgTempOutput**합니다.

쿼리에서 여러 출력을 사용 하는 경우 각 출력에 대 한 hello 결과 개별적으로 볼 수 있으며 서로 쉽게 설정/해제할 수 있습니다.

Hello 결과 만족 하는 후 쿼리 저장, 작업, 지켜봅니다을 시작한 스트림 분석의 hello 매직을 감시 합니다.

## <a name="get-help"></a>도움말 보기

추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
