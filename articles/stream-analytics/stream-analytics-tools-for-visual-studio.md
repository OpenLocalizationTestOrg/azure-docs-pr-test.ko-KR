---
title: "Azure 스트림 분석 Tools for Visual Studio aaaUse | Microsoft Docs"
description: "Azure 스트림 분석 Tools for Visual Studio hello에 대 한 자습서 시작"
keywords: Visual Studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Azure Stream Analytics Tools for Visual Studio 사용
## <a name="introduction"></a>소개
이 자습서에서는 방법 Visual Studio toocreate toouse Azure 스트림 분석 도구를 작성, 로컬로 테스트, 관리 및 스트림 분석 작업을 디버그 배웁니다. 

이 자습서를 완료하고 나면 다음을 수행할 수 있습니다.
* Stream Analytics Tools for Visual Studio를 익숙하게 사용 가능
* Stream Analytics 작업 구성 및 배포
* 로컬 샘플 데이터로 로컬에서 작업 테스트
* Tootroubleshoot 문제 모니터링을 사용 합니다.
* 기존 작업 tooprojects를 내보냅니다.

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:
* Hello에 "스트림 분석 작업 만들기" 앞에 있는 hello 단계 완료 [스트림 분석 자습서를 사용 하 여 IoT 솔루션 작성](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics)합니다. 
* Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012를 사용합니다. Enterprise(Ultimate/Premium), Professional 및 Community Edition이 지원됩니다. Express Edition은 지원되지 않습니다. Visual Studio 2017은 지원되지 않습니다. 
* 사용 하 여 hello Azure SDK for.NET 버전 2.7.1 이상. Hello를 사용 하 여 설치 [웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)합니다.
* Hello 설치 [스트림 분석 Tools for Visual Studio](http://aka.ms/asatoolsvs)합니다.

## <a name="create-a-stream-analytics-project"></a>Stream Analytics 프로젝트 만들기
1. Visual Studio에서 클릭 hello **파일** 메뉴와 선택 **새 프로젝트**합니다. 

2. Hello hello 왼쪽의 템플릿 목록에서 선택 **스트림 분석** 클릭 하 고 **Azure 스트림 분석 응용 프로그램**합니다.

3. Hello 프로젝트 입력 **이름**, **위치**, 및 **솔루션 이름** 다른 프로젝트의 경우와 마찬가지로 합니다.

    ![새 프로젝트 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    **솔루션 탐색기**에 **Toll** 프로젝트가 생성됩니다.

    ![솔루션 탐색기에 생성된 Toll 프로젝트](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Hello 올바른 구독이 선택
1. Visual Studio에서 클릭 hello **보기** 메뉴를 열고 다음 **서버 탐색기**합니다.

2. Azure 계정으로 로그인합니다. 

## <a name="define-hello-input-sources"></a>Hello 입력된 소스를 정의 합니다.
1.  **솔루션 탐색기**, hello 확장 **입력** 노드 및 이름 바꾸기 **Input.json** 너무**EntryStream.json**합니다. **EntryStream.json**을 두 번 클릭합니다.
2.  hello **입력 별칭** 이제 **EntryStream**합니다. hello 입력 별칭은 hello 쿼리 스크립트에 사용 됩니다. 
3.  **원본 형식**으로 **데이터 스트림**을 선택합니다.
4.  **원본**에서 **이벤트 허브**를 선택합니다.
5.  **서비스 버스 Namespace**선택, hello **TollData** 옵션입니다.
6.  **이벤트 허브 이름**에서 **entry**를 선택합니다.
7.  **이벤트 허브 정책 이름**선택, **RootManageSharedAccessKey** (기본값 hello).
8.  **이벤트 직렬화 형식**으로 **Json**을 선택합니다. 
9.  **인코딩**으로 **UTF8**을 선택합니다. 설정에 따라 스크린 샷 hello 같이 표시 됩니다.

    ![입력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. toofinish hello 마법사 클릭 **저장**합니다. 이제 다른 toocreate hello 종료 스트림 입력된 소스를 추가할 수 있습니다. 마우스 오른쪽 단추로 클릭 hello **입력** 노드를 선택한 **새 항목**합니다.

    ![새 항목](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Hello 창에서 선택한 **Azure 스트림 분석 입력**, hello 변경 **이름** 너무**ExitStream.json**합니다. **추가**를 클릭합니다.

    ![새 항목 추가 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. 두 번 클릭 **ExitStream.json** hello 프로젝트 및 hello 입력 스트림에 대해 수행한 것 처럼 동일한 단계에 따라 hello에 있습니다. 수 있는지 tooenter **종료** hello에 대 한 **이벤트 허브 이름** hello 스크린 샷 뒤에 표시 된 대로:

    ![ExitStream 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    이제 두 입력 스트림을 정의했습니다.

    ![진입 및 종료 입력 스트림](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    다음으로, 자동차 대 한 등록 데이터를 포함 하는 hello blob 파일에 대 한 참조 데이터 입력을 추가 합니다.

13. 마우스 오른쪽 단추로 클릭 hello **입력** hello 프로젝트 및 hello 스트림 입력에 대해 수행한 것 처럼 동일한 단계에 따라 hello에서 노드. **입력 별칭**에 **Registration**을 입력하고 **원본 형식**에서 **참조 데이터**를 선택합니다.

    ![등록 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. **저장소 계정**선택, hello **tolldata** 옵션입니다. **컨테이너**에서 **tolldata**를 선택하고 **경로 패턴**에 **registration.json**을 입력합니다. 이 파일 이름은 대/소문자를 구분하므로 소문자여야 합니다.
15. toofinish hello 마법사 클릭 **저장**합니다.

이제 모든 hello 입력 정의 됩니다.

## <a name="define-hello-output"></a>Hello 출력을 정의 합니다.
1.  **솔루션 탐색기**, hello 확장 **입력** 노드와 두 번 클릭 **Output.json**합니다.

2.  **출력 별칭**에 **output**을 입력합니다. 
3.  **싱크**에서 **SQL Database**를 선택합니다.
4.  **데이터베이스**에서 **TollDataDB**를 선택합니다.
5.  **사용자 이름**에 **tolladmin**을 입력합니다. 
6.  **암호**에 **123toll!**를 입력합니다.
7.  **테이블**에 **TollDataRefJoin**을 입력합니다.
8.  **Save**를 클릭합니다.

    ![출력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Stream Analytics 쿼리 만들기
이 자습서는 여러 가지 비즈니스 질문을 관련된 tootoll 데이터 tooanswer를 시도 합니다. 또한 tooprovide 관련 응답 스트림 분석에에서 사용할 수 있는 스트림 분석 쿼리를 생성 합니다.
첫 번째 스트림 분석 작업을 시작 하기 전에 간단한 시나리오 및 hello 쿼리 구문을 살펴보겠습니다.

### <a name="introduction-toohello-stream-analytics-query-language"></a>소개 toohello 스트림 분석 쿼리 언어
Toocount hello 수가 차량이 요금 소 창구를 입력 해야 하는 경우를 가정해 봅니다. 이 예제에서는 이벤트의 연속 스트림을 이므로의 toodefine를 해야 합니다. Hello 질문 toobe "개수 차량 입력 요금 소 창구 3 분 마다?"를 수정 합니다. 데이터는 일반적으로이 방식으로 toocount tooas hello 텀블 링 개수를 참조 합니다.

이 질문에 응답 하는 hello 스트림 분석 쿼리를 확인 합니다.

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

스트림 분석 쿼리 언어는 SQL 유사 하며 추가 하는 몇 가지 확장 toospecify 시간 관련 쿼리의 항목이 hello 사용 합니다.

자세한 내용은 참조 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN에서 hello 쿼리에 사용 되는 구문입니다.

이제 첫 번째 스트림 분석 쿼리를 작성 한 인지 시간 tootest 것입니다. 경로 따라 hello에 TollApp 폴더에 있는 hello 샘플 데이터 파일을 사용 합니다.

..\TollApp\TollApp\Data

이 폴더는 hello를 다음 파일이 포함 되어 있습니다.
*   Entry.json
*   Exit.json
*   registration.json

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>개수 hello 차량이 요금 소 창구를 입력 합니다.
Hello 프로젝트에서 두 번 클릭 **Script.asaql** hello에서 tooopen hello 스크립트 **쿼리 편집기**합니다. 복사한 hello 이전 단원의 hello 스크립트 hello 편집기에 붙여 넣습니다. hello 쿼리 편집기는 IntelliSense, 구문 색 지정 및 hello 오류 표식 지원합니다.

![쿼리 편집기](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>로컬에서 Stream Analytics 쿼리 테스트

1. 구문 오류가 있을 경우 toocompile hello 쿼리 toosee hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **빌드**합니다. 

2. toovalidate이이 쿼리 샘플 데이터에 대해 로컬 샘플 데이터를 사용할 수 있습니다. Hello 입력을 마우스 오른쪽 단추로 클릭 하 고 선택 **로컬 입력 추가**합니다.

    ![로컬 입력 추가](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Hello 팝업 창에 사용자의 로컬 경로에서 hello 예제 데이터를 선택 합니다. **Save**를 클릭합니다.

    ![로컬 입력 추가 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    라는 파일 **local_EntryStream.json** tooyour 입력 폴더에 자동으로 추가 됩니다.

    ![파일 추가 tooinputs 폴더](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. Hello에 **쿼리 편집기**, 클릭 **로컬로 실행**합니다. 또는 hello F5 키를 눌러 수 있습니다.

    ![로컬로 실행](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![로컬 실행 출력](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Hello에서 모든 키 tooview hello 출력을 눌러 **ASA 로컬 실행 결과** Visual Studio의 창. 

    ![ASA 로컬 실행 결과 창](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. 클릭 **결과 폴더 열기** toocheck hello 출력 파일을 모두 CSV 및 JSON 형식입니다.

    ![결과 폴더 열기 출력](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>샘플 hello에 대 한 입력된 데이터
샘플 입력된 데이터 입력된 소스 tooa 로컬 파일에서 수도 있습니다. 
1. Hello 입력된 구성 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **예제 데이터**합니다. 

   ![샘플 데이터](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    지금은 이벤트 허브 또는 IoT Hub를 샘플링할 수 있습니다. 다른 입력 원본은 지원되지 않습니다.

2. Hello 팝업 창에 hello 사용 되는 로컬 경로 toosave hello 샘플 데이터를 입력 합니다. **샘플링**을 클릭합니다.

    ![샘플 데이터 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Hello hello 진행 상황을 볼 수 있습니다 **출력** 창. 

    ![출력 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>스트림 분석 쿼리 tooAzure 제출
1. Hello에 **쿼리 편집기**, 클릭 **tooAzure 제출** hello 스크립트 편집기에서.

    ![TooAzure 제출](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. **새 Azure Stream Analytics 작업 만들기**를 선택합니다. Hello 입력 **작업 이름**, 올바른 선택 hello 및 **구독**합니다. **제출**을 클릭합니다.

    ![작업 전송 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>작업 시작
사용자 작업을 만든 했으므로 hello 작업 보기 자동으로 열립니다. 
1. toostart hello 작업을 hello 클릭 **녹색 화살표** 단추입니다.

    ![작업 시작](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Hello 기본 설정을 선택 하 고 클릭 **시작**합니다.
 
    ![작업 시작 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    hello 작업 **상태** 쪽 변경**실행**, 및 **입력 이벤트** 및 **출력 이벤트** 나타납니다.

    ![작업 요약에서 실행 중 상태](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Visual Studio에서 hello 결과 확인
1. Visual Studio에서 열고 **서버 탐색기** hello 마우스 오른쪽 단추로 클릭 하 고 **TollDataRefJoin** 테이블입니다.
2. 선택 **테이블 데이터 표시** 작업의 toosee hello 출력 합니다.
   
    ![서버 탐색기의 테이블 데이터 표시 선택 영역](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Hello 작업 메트릭 보기
몇 가지 기본 작업 통계는 **Job Metrics(작업 메트릭)**에서 확인할 수 있습니다. 

![작업 메트릭 창](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>서버 탐색기에서 목록 hello 작업
**서버 탐색기**에서 **Stream Analytics 작업**을 클릭하고 **새로 고침**을 클릭합니다. hello 작업 아래에 나타납니다. **스트림 분석 작업이**합니다.

![서버 탐색기에 나열된 Stream Analytics 작업](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>열기 hello 작업 보기
tooopen hello 작업 보기 작업 노드를 확장 하 고 hello를 두 번 클릭 **작업 보기** 노드.

![작업 보기 노드](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>기존 작업 tooa 프로젝트 내보내기
두 가지 방법으로 기존 작업 tooa 프로젝트를 내보낼 수 있습니다.

**서버 탐색기**, hello에 hello 작업 노드를 마우스 오른쪽 단추로 클릭 **스트림 분석 작업** 노드 선택한 **tooNew 스트림 분석 프로젝트 내보내기**합니다.

![스트림 분석 프로젝트 tooNew 내보내기](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

hello 프로젝트에 생성 됩니다 **솔루션 탐색기**합니다.

![솔루션 탐색기에 생성된 프로젝트](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Hello 작업 보기를 사용 하 고 수도 있습니다 클릭 **프로젝트 생성**합니다.

![프로젝트 생성](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>알려진 문제 및 제한 사항
 
- Power BI 출력 및 Azure Date Lake Store 출력에 대한 지원은 없습니다.
- JavaScript 사용자 정의 함수를 추가 또는 변경하기 위한 편집기 지원은 없습니다.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure 스트림 분석 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
