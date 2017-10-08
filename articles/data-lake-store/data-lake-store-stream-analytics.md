---
title: "데이터 레이크 저장소에 대 한 스트림 분석에서 aaaStream 데이터 | Microsoft Docs"
description: "Azure 스트림 분석 toostream 데이터를 사용 하 여 Azure 데이터 레이크 저장소로"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Azure 스트림 분석을 사용하여 Azure 저장소 Blob에서 Data Lake 저장소에 데이터 스트리밍
이 문서에서 toouse Azure 데이터 레이크 저장 되는 방식과 Azure 스트림 분석 작업에 대 한 출력으로 살펴봅니다. 이 문서에서는 Azure 저장소 blob (입력)에서 데이터를 읽고 하는 간단한 시나리오를 설명 하 고 쓰기 hello 데이터 tooData 레이크 저장소 (출력).

> [!NOTE]
> 이때 데이터 레이크 저장소의 생성 및 구성 출력 스트림 분석 hello 에서만 지원 됩니다 [Azure 클래식 포털](https://manage.windowsazure.com)합니다. 따라서이 자습서의 일부 hello Azure 클래식 포털을 사용 합니다.
>
>

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

* **Azure Storage 계정**. 스트림 분석 작업에 대 한이 계정 tooinput 데이터에서 blob 컨테이너를 사용 합니다. 이 자습서에서는 가정 라는 저장소 계정이 있는 **storageforasa** hello 계정 내의 컨테이너 및 **storageforasacontainer**합니다. Hello 컨테이너를 만든 후에 예제 데이터 파일 tooit을 업로드 합니다. 
  
* **Azure Data Lake Store 계정**. Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다. **asadatalakestore**라는 Data Lake Store 계정이 있다고 가정합니다. 

## <a name="create-a-stream-analytics-job"></a>스트림 분석 작업 만들기
입력 원본 및 출력 대상을 포함하는 스트림 분석 작업을 만들어 시작합니다. 이 자습서에 대 한 hello 원본이 Azure blob 컨테이너가 있으며 hello 대상이 데이터 레이크 저장소입니다.

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.

2. Hello 왼쪽된 창에서 클릭 **스트림 분석 작업이**, 클릭 하 고 **추가**합니다.

    ![Stream Analytics 작업 만들기](./media/data-lake-store-stream-analytics/create.job.png "Stream Analytics 작업 만들기")

    > [!NOTE]
    > Hello에서 작업을 만드는 확인 hello 저장소 계정 또는 사용자와 동일한 지역에 지역 간 데이터 이동의 추가 비용 발생 합니다.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Hello 작업에 대 한 Blob 입력 만들기

1. Hello 왼쪽된 창에서 hello 스트림 분석 작업에 대 한 열기 hello 페이지 클릭 hello **입력** 탭을 클릭 한 다음 **추가**합니다.

    ![입력된 tooyour 작업에 추가할](./media/data-lake-store-stream-analytics/create.input.1.png "입력된 tooyour 작업 추가")

2. Hello에 **새 입력** 블레이드에서 hello 다음 값을 제공 합니다.

    ![입력된 tooyour 작업에 추가할](./media/data-lake-store-stream-analytics/create.input.2.png "입력된 tooyour 작업 추가")

    * 에 대 한 **입력 별칭**를 작업 입력 hello에 대 한 고유한 이름을 입력 합니다.
    * **원본 형식**으로 **데이터 스트림**을 선택합니다.
    * **원본**으로 **Blob Storage**를 선택합니다.
    * **구독**에 대해 **현재 구독의 Blob Storage 사용**을 선택합니다.
    * 에 대 한 **저장소 계정**, hello 필수 소프트웨어의 일부로 만든 hello 저장소 계정을 선택 합니다. 
    * 에 대 한 **컨테이너**선택, hello 컨테이너에서 hello 만든 저장소 계정을 선택 합니다.
    * **이벤트 직렬화 형식**으로 **CSV**를 선택합니다.
    * **구분 기호**로 **탭**을 선택합니다.
    * **인코딩**으로 **UTF-8**을 선택합니다.

    **만들기**를 클릭합니다. 이제 hello 포털 hello 입력을 추가 하 고 hello 연결 tooit를 테스트 합니다.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Hello 작업에 대 한 데이터 레이크 저장소 출력 만들기

1. Hello 스트림 분석 작업에 대 한 hello 페이지, hello 클릭 **출력** 탭을 클릭 한 다음 **추가**합니다.

    ![출력 tooyour 작업을 추가](./media/data-lake-store-stream-analytics/create.output.1.png "출력 tooyour 작업 추가")

2. Hello에 **새 출력** 블레이드에서 hello 다음 값을 제공 합니다.

    ![출력 tooyour 작업을 추가](./media/data-lake-store-stream-analytics/create.output.2.png "출력 tooyour 작업 추가")

    * 에 대 한 **출력 별칭**를 입력 한 hello 작업 출력에 대 한 고유 이름입니다. 쿼리 toodirect hello 쿼리 출력 toothis Data Lake 저장소에에서 사용 되는 친숙 한 이름입니다.
    * **싱크**로 **Data Lake Store**를 선택합니다.
    * 입력 정보 요청된 tooauthorize 됩니다 tooData Lake 저장소 계정에 액세스 합니다. **권한 부여**를 클릭합니다.

3. Hello에 **새 출력** 블레이드에서 tooprovide hello 다음 값을 계속 합니다.

    ![출력 tooyour 작업을 추가](./media/data-lake-store-stream-analytics/create.output.3.png "출력 tooyour 작업 추가")

    * 에 대 한 **계정 이름**를 전송 하는 hello 작업 출력 toobe 저장할 이미 만든 hello 데이터 레이크 저장소 계정을 선택 합니다.
    * 에 대 한 **경로 접두사 패턴**, 입력 파일에 사용 된 경로 toowrite hello 내에서 파일에 데이터 레이크 저장소 계정을 지정 합니다.
    * 에 대 한 **날짜 형식**, 날짜 토큰을 사용 하는 hello 접두사 경로 있는 경우 파일 구성 됩니다 hello 날짜 형식을 선택할 수 있습니다.
    * 에 대 한 **시간 형식**시간 토큰을 사용 하는 hello 접두사 경로 있는 경우, 사용자 파일 구성할 지 hello 시간 형식을 지정 합니다.
    * **이벤트 직렬화 형식**으로 **CSV**를 선택합니다.
    * **구분 기호**로 **탭**을 선택합니다.
    * **인코딩**으로 **UTF-8**을 선택합니다.
    
    **만들기**를 클릭합니다. 이제 hello 포털 hello 출력을 추가 하 고 hello 연결 tooit를 테스트 합니다.
    
## <a name="run-hello-stream-analytics-job"></a>Hello 스트림 분석 작업을 실행 합니다.

1. 스트림 분석 작업 toorun hello에서 쿼리를 실행 해야 **쿼리** 탭 합니다. 이 자습서에서는 대체 하 여 hello 예제 쿼리를 실행할 수 있습니다 hello 화면 캡처 아래와 같이 hello로 hello 자리 표시자 작업 입력 및 출력 별칭입니다.

    ![쿼리 실행](./media/data-lake-store-stream-analytics/run.query.png "쿼리 실행")

2. 클릭 **저장** 그 다음 hello hello hello 화면 맨 위에서 **개요** 탭을 클릭 **시작**합니다. Hello 대화 상자에서 선택 **사용자 지정 시간**, hello 현재 날짜 및 시간을 설정 합니다.

    ![작업 시간 설정](./media/data-lake-store-stream-analytics/run.query.2.png "작업 시간 설정")

    클릭 **시작** toostart hello 작업 합니다. 최대 tooa 몇 분 toostart hello 작업을 걸릴 수 있습니다.

3. hello blob에서 tootrigger hello 작업 toopick hello 데이터 샘플 데이터 파일 toohello blob 컨테이너를 복사 합니다. Hello에서 예제 데이터 파일을 가져올 수 있습니다 [Azure 데이터 레이크 Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)합니다. 이 자습서에 대 한 복사 hello 파일 **vehicle1_09142014.csv**합니다. 와 같은 다양 한 클라이언트를 사용할 수 [Azure 저장소 탐색기](http://storageexplorer.com/), tooupload 데이터 tooa blob 컨테이너입니다.

4. Hello에서 **개요** 탭의 **모니터링**, hello 데이터 처리 방법을 참조 하세요.

    ![작업 모니터링](./media/data-lake-store-stream-analytics/run.query.3.png "작업 모니터링")

5. 마지막으로 hello 작업 출력 데이터를 hello Data Lake 저장소 계정에서 사용할 수 있는지 확인할 수 있습니다. 

    ![출력 확인](./media/data-lake-store-stream-analytics/run.query.4.png "출력 확인")

    Hello 데이터 탐색기 창에서 해당 hello 출력으로 작성 된 tooa 폴더 경로에 지정 된 hello 데이터 레이크 저장소 출력 설정 확인 (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>참고 항목
* [HDInsight 클러스터 toouse 데이터 레이크 저장소 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)
