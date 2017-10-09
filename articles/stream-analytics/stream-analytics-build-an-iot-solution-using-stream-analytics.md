---
title: "스트림 분석을 사용 하 여는 IoT 솔루션 aaaBuild | Microsoft Docs"
description: "Hello 톨게이트 시나리오의 스트림 분석 IoT 솔루션에 대 한 자습서 시작"
keywords: "iot 솔루션, 창 함수"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Stream Analytics를 사용하여 IoT 솔루션 빌드
## <a name="introduction"></a>소개
이 자습서에서는 살펴보겠습니다 어떻게 toouse Azure 스트림 분석 tooget 데이터에서 실시간 정보입니다. 개발자가 기록 레코드 또는 참조 데이터 tooderive 비즈니스 통찰력 스트림을 클릭 스트림, 로그 및 장치에서 생성 된 이벤트와 같은 데이터를 쉽게 결합할 수 있습니다. Microsoft Azure에서 호스팅되는 완전히 관리 되는 실시간 스트림 계산 서비스, Azure 스트림 분석 준비 하 고 분 후에 실행할 기본 제공 복원 력, 낮은 대기 시간 및 확장성 tooget 제공 합니다.

이 자습서를 완료하고 나면 다음을 수행할 수 있습니다.

* Hello Azure 스트림 분석 포털 숙지 합니다.
* 스트리밍 작업 구성 및 배포
* 실제 문제를 명확히 하 고 hello 스트림 분석 쿼리 언어를 사용 하 여이 해결 합니다.
* 안심하고 Stream Analytics를 사용하여 고객에 대한 스트리밍 솔루션 개발
* 모니터링 및 로깅 경험 tootroubleshoot 문제 hello를 사용 합니다.

## <a name="prerequisites"></a>필수 조건
사용자는 필요 hello 필수 구성 요소 toocomplete 다음이 자습서:

* 최신 버전의 hello [Azure PowerShell](/powershell/azure/overview)
* 2015, visual Studio 2017 또는 무료 hello [Visual Studio 커뮤니티](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* [Azure 구독](https://azure.microsoft.com/pricing/free-trial/)
* Hello 컴퓨터에서 관리자 권한
* 다운로드 [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) hello Microsoft 다운로드 센터에서
* 선택 사항: 소스 코드에서 hello TollApp 이벤트 생성기에 대 한 [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>시나리오 소개: “Hello, Toll!”
톨게이트 요금소는 일반적인 현상입니다. 볼 수 있는 이러한 여러 고속도로, 브리지 및 터널 hello 전 세계 합니다. 각 요금소에는 여러 개의 요금 창구가 있습니다. 수동 부스에서 toopay hello 유료 tooan 수행자를 중지합니다. 자동화 된 부스에서 각 창구 위쪽 센서를 차량을 부착 toohello 차량의 바람막이 hello 요금 소 창구를 전달 하면 RFID 카드를 스캔 합니다. 이 프로토콜은 차량을 이러한 요금 소를 통해 쉽게 toovisualize hello 통로으로 흥미로운 작업도 수행할 수 있는 이벤트 스트림을 합니다.

![요금 창구에 서 있는 자동차 사진](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>들어오는 데이터
이 자습서에서는 두 가지 데이터 스트림을 사용합니다. 센서 hello 나타내기에 설치 하 고 hello 요금 소 종료 hello 첫 번째 스트림에 생성 합니다. hello 두 번째 스트림이 차량 등록 데이터를 가진 정적 조회 데이터 집합입니다.

### <a name="entry-data-stream"></a>진입 데이터 스트림
hello 입력 데이터 스트림을 요금 소에 들어갈 때 자동차에 대 한 정보를 포함 합니다.

| TollId | EntryTime | LicensePlate | 시스템 상태 | 계정을 | 모델 | VehicleType | VehicleWeight | Toll | 태그 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |JNB 7001 |NY |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |XYZ 1003 |CT |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |1007 BNJ |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CDE 1007 |NJ |Toyota |4x4 |1 |0 |6 |321987654 |

Hello 열에 대 한 간단한 설명은 다음과 같습니다.

| 열 | 설명 |
| --- | --- |
| TollId |요금 소 창구를 고유 하 게 식별 하는 hello 요금 소 창구 ID |
| EntryTime |hello 차량 toohello 요금 소 창구 UTC에서의 항목의 hello 날짜 및 시간 |
| LicensePlate |hello 번호판 hello 차량 |
| 시스템 상태 |미국의 주 이름 |
| 계정을 |hello 자동차의 hello 제조업체 |
| 모델 |hello 자동차의 hello 모델 번호 |
| VehicleType |여객 차량의 경우 1, 화물 차량의 경우 2 |
| WeightType |차량 무게(톤), 승용차는 0 |
| Toll |usd로 hello 유료 값 |
| 태그 |E-tag 지불; 자동화 하는 hello 자동차에 hello hello 지불 수동으로 수행 된 빈 값 |

### <a name="exit-data-stream"></a>진출 데이터 스트림
hello 종료 데이터 스트림을 hello 유료 스테이션을 그대로 두고 자동차에 대 한 정보를 포함 합니다.

| **TollId** | **ExitTime** | **LicensePlate** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |JNB 7001 |
| 1 |2014-09-10T12:03:00.0000000Z |YXZ 1001 |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |XYZ 1003 |
| 1 |2014-09-10T12:08:00.0000000Z |1007 BNJ |
| 2 |2014-09-10T12:07:00.0000000Z |CDE 1007 |

Hello 열에 대 한 간단한 설명은 다음과 같습니다.

| 열 | 설명 |
| --- | --- |
| TollId |요금 소 창구를 고유 하 게 식별 하는 hello 요금 소 창구 ID |
| ExitTime |hello 날짜와 시간을 utc로 요금 소 창구 hello 차량 종료 |
| LicensePlate |hello 번호판 hello 차량 |

### <a name="commercial-vehicle-registration-data"></a>화물 차량 등록 데이터
hello 자습서에서는 정적 상용차 등록 데이터베이스 스냅숏을 사용 합니다.

| LicensePlate | RegistrationId | 만료됨 |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| BAC 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Hello 열에 대 한 간단한 설명은 다음과 같습니다.

| 열 | 설명 |
| --- | --- |
| LicensePlate |hello 번호판 hello 차량 |
| RegistrationId |hello 차량 등록 ID |
| 만료됨 |hello hello 차량 등록 상태: 0 차량 등록 중인 경우 등록이 만료 되 면 1 |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Azure 스트림 분석에 대 한 hello 환경 설정
toocomplete이이 자습서에서는 Microsoft Azure 구독이 필요 합니다. Microsoft는 Microsoft Azure 서비스에 대한 평가판을 제공합니다.

Azure 계정이 없는 경우 [평가판 버전을 요청](http://azure.microsoft.com/pricing/free-trial/)할 수 있습니다.

> [!NOTE]
> 무료 평가판에 대해 toosign, 문자 메시지 및 유효한 신용 카드를 받을 수 있는 모바일 장치가 필요 합니다.
> 
> 

Toofollow hello Azure 크레딧 사용에 가장 적합 hello 내릴 수 있도록이 문서의 끝 hello에 hello ""정리 하 여 Azure 계정"섹션에서 단계 확인 해야 합니다.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Hello 자습서에 필요한 Azure 리소스를 프로 비전
이 자습서에서는 두 개의 이벤트 허브 tooreceive *항목* 및 *종료* 데이터 스트림을 합니다. Azure SQL 데이터베이스의 hello 스트림 분석 작업 hello 결과 출력합니다. Azure 저장소는 차량 등록에 대한 참조 데이터를 저장합니다.

사용할 수 있습니다 hello Setup.ps1 스크립트 hello TollApp 폴더에 GitHub toocreate에 필요한 모든 리소스. Hello 관심 있는 시간을 실행 하는 것이 좋습니다. 어떻게 tooconfigure hello Azure 포털에서에서 이러한 리소스를 참조 하는 방법에 대 한 자세한 toolearn 원하는 경우 toohello "Azure 포털에서 자습서 리소스 구성" 부록 합니다.

다운로드 하 고 hello 지원 저장 [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) 폴더 및 파일입니다.

**Microsoft Azure PowerShell** 창을 *관리자 권한으로*엽니다. Azure PowerShell 아직 없는 경우 hello 지침에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview) tooinstall 것입니다.

Windows.ps1,.dll 및.exe 파일에 자동으로 차단, 하기 때문에 hello 스크립트를 실행 하기 전에 tooset hello 실행 정책이 필요 합니다. Hello Azure PowerShell 창에서 실행 되 고 있는지 확인 *관리자로 서*합니다. **Set-ExecutionPolicy unrestricted**를 실행합니다. 메시지가 표시되면 **Y**를 입력합니다.

![Azure PowerShell 창에서 실행 중인 "Set-executionpolicy unrestricted"의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

실행 **Get-executionpolicy** toomake hello 명령 작동 하는지 확인 합니다.

![Azure PowerShell 창에서 실행 중인 "Get-ExecutionPolicy"의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Hello 스크립트 및 응용 프로그램 생성기 있는 toohello 디렉터리를 이동 합니다.

!["Cd.\TollApp\TollApp" hello Azure PowerShell 창에서 실행의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

형식 **.\\ Setup.ps1** tooset Azure 계정 만들기 및 필요한 모든 리소스를 구성 및 toogenerate 이벤트를 시작 합니다. hello 스크립트 임의로 선택 영역 toocreate 리소스 합니다. hello를 전달할 수 있습니다, tooexplicitly 지역을 지정 **-위치** hello 다음 예제 에서처럼 매개 변수:

**.\\Setup.ps1 -location “Central US”**

![Hello Azure 로그인 페이지의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

hello 스크립트 열립니다 hello **로그인** Microsoft Azure에 대 한 페이지입니다. 계정 자격 증명을 입력합니다.

> [!NOTE]
> 계정에 대 한 액세스 toomultiple 구독이 묻는 tooenter hello 구독 이름을 hello 자습서 toouse 되도록 됩니다.
> 
> 

hello 스크립트에는 몇 분 toorun을 걸릴 수 있습니다. 완료 되 면 hello 출력 스크린 샷 다음 hello와 같아야 합니다.

![Hello Azure PowerShell 창에서 hello 스크립트의 출력의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

다음 스크린 샷 유사한 toohello 있는 다른 창도 나타납니다. 이 응용 프로그램 이벤트를 보내는 tooAzure 이벤트 허브 필요한 toorun hello 자습서 인 합니다. 따라서 hello 응용 프로그램을 중지 하거나 마십시오 hello 자습서를 완료 될 때까지이 창을 닫습니다.

!["이벤트 허브 데이터 전송 중" 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

있습니다 수 toosee 리소스에에서 있어야 Azure 포털 이제 합니다. 너무 이동<https://portal.azure.com>, 및 계정 자격 증명을 사용 하 여 로그인 합니다. 일부 기능은 hello 클래식 포털 활용 현재 참고 합니다. 다음 단계가 명확하게 표시됩니다.

### <a name="azure-event-hubs"></a>Azure Event Hubs
Hello Azure 포털에서에서 클릭 **더 많은 서비스** hello hello 관리 왼쪽된 창 아래쪽에 있습니다. 형식 **이벤트 허브** hello 제공 된 필드와 클릭 **이벤트 허브**합니다. 그러면 새 브라우저 창 toodisplay hello **서비스 버스** hello에 대 한 영역 **클래식 포털**합니다. 여기서 hello hello Setup.ps1 스크립트에서 만든 이벤트 허브를 확인할 수 있습니다.

![서비스 버스](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Hello로 시작 하는 하나 클릭 *tolldata*합니다. Hello 클릭 **이벤트 허브** 탭 합니다. 이 네임스페이스에서 만든 *진입*과 *진출*이라는 두 개의 이벤트 허브가 표시됩니다.

![Hello 클래식 포털의 이벤트 허브 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Azure 저장소 컨테이너
1. 브라우저 열려 tooAzure 포털에서 toohello 탭을 돌아갑니다. 클릭 **저장소** hello hello 자습서에 사용 되는 hello Azure 포털 toosee hello Azure 저장소 컨테이너의 왼쪽에 있습니다.
   
    ![저장소 메뉴 항목](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Hello로 시작 하는 하나 클릭 *tolldata*합니다. Hello 클릭 **컨테이너** 탭 toosee hello 만들 컨테이너입니다.
   
    ![Hello Azure 포털에서에서 컨테이너 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Hello 클릭 **tolldata** 컨테이너 toosee hello 차량 등록 데이터를 사용 하는 JSON 파일을 업로드 합니다.
   
    ![Hello 컨테이너에서 hello registration.json 파일의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Azure SQL Database
1. Azure 포털 toohello hello 브라우저에서 열렸으면 hello 첫 번째 탭에서 다시 이동 합니다. 클릭 **SQL 데이터베이스** hello hello 자습서에 사용 되 고 클릭 하는 hello Azure 포털 toosee hello SQL 데이터베이스의 왼쪽에 **tolldatadb**합니다.
   
    ![만든 hello SQL 데이터베이스의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Hello 포트 번호 없이 복사 hello 서버 이름 (*servername*. 예를 들어 database.windows.net).
    ![만든 hello SQL 데이터베이스 db의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Visual Studio에서 toohello 데이터베이스 연결
Visual Studio tooaccess 쿼리 결과 사용 하 여 hello 출력 데이터베이스에 있습니다.

Visual Studio에서 toohello SQL 데이터베이스 (hello 대상)을 연결 합니다.

1. Visual Studio를 열고 클릭 **도구** > **tooDatabase 연결**합니다.
2. 표시되는 메시지에 따라 **Microsoft SQL Server**를 데이터 원본으로 클릭합니다.
   
    ![데이터 원본 변경 대화 상자](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. Hello에 **서버 이름** 필드, hello Azure 포털에서에서 hello 이전 섹션에서 복사한 hello 이름을 붙여 넣습니다 (즉, *servername*. database.windows.net).
4. **SQL Server 인증 사용**을 클릭합니다.
5. 입력 **tolladmin** hello에 **사용자 이름** 필드 및 **123toll!** hello에 **암호** 필드입니다.
6. 클릭 **데이터베이스 이름 선택 또는 입력**를 선택 하 고 **TollDataDB** hello 데이터베이스로 합니다.
   
    ![연결 추가 대화 상자](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. **확인**을 클릭합니다.
8. 서버 탐색기를 엽니다.
   
    ![서버 탐색기](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Hello TollDataDB 데이터베이스에 4 개의 테이블을 참조 하십시오.
   
    ![Hello TollDataDB 데이터베이스의 테이블](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>이벤트 생성기: TollApp 샘플 프로젝트
PowerShell 스크립트 hello hello TollApp 샘플 응용 프로그램을 사용 하 여 toosend 이벤트를 자동으로 시작 합니다. Tooperform 추가 단계가 필요 없습니다.

그러나 경우에 관심이 있는 구현 정보를 찾을 수 있습니다 hello TollApp 응용 프로그램의 소스 코드 hello GitHub에서 [샘플/TollApp](https://aka.ms/azure-stream-analytics-toll-source)합니다.

![Visual Studio에 표시된 샘플 코드의 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Stream Analytics 작업 만들기
1. Azure 포털 hello 새 스트림 분석 작업 클릭 hello 페이지 toocreate의 hello 왼쪽 위 모서리에 있는 녹색 더하기 기호를 hello 합니다. **인텔리전스+분석**을 선택한 다음 **Stream Analytics 작업**을 클릭합니다.
   
    ![새 단추](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. 작업 이름을 지정 hello 구독 유효성 검사, 해결 한 다음 hello에서 새 리소스 그룹을 만듭니다는 hello 이벤트 허브 저장소와 동일한 지역 (기본값 hello 스크립트에 대 한 미국 중남부은).
3. 클릭 **Pin toodashboard** 차례로 **만들기** hello hello 페이지 맨 아래에 있습니다.
   
    ![Stream Analytics 작업 만들기 옵션](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>입력 원본 정의
1. hello 작업 만들고 hello 작업 페이지를 엽니다. 또는 hello 포털 대시보드에서 분석 작업을 생성 하는 hello를 클릭할 수 있습니다.

2. Hello 클릭 **입력** toodefine hello 원본 데이터를 탭 합니다.
   
    ![hello 입력 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. **입력 추가**를 클릭합니다.
   
    ![hello 추가 입력 옵션](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. **입력 별칭**으로 **EntryStream**을 입력합니다.
5. 원본 형식은 **데이터 스트림**입니다.
6. 원본은 **Event hub**입니다.
7. **서비스 버스 네임 스페이스** hello에 TollData 하나 드롭 다운 hello 이어야 합니다.
8. **이벤트 허브 이름** 설정할지 너무**항목**합니다.
9. **이벤트 허브 정책 이름*은 **RootManageSharedAccessKey** (기본값 hello).
10. **이벤트 직렬화 형식**에 대해 **JSON**을, **인코딩**에 대해 **UTF8**을 선택합니다.
   
    설정이 다음과 같이 표시됩니다.
   
    ![이벤트 허브 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. 클릭 **만들기** hello hello 페이지 toofinish hello 마법사 맨 아래에 있습니다.
    
    Hello 수행한는 hello 항목 스트림을 만들었으므로 이제 같은 단계 toocreate hello 종료 스트림에 합니다. Hello 스크린 샷 뒤에서 같이 있는지 tooenter 값 수입니다.
    
    ![Hello 종료 스트림에 대 한 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    다음 두 진입 스트림을 정의했을 것입니다.
    
    ![Hello Azure 포털에에서 입력된 스트림을 정의](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    다음으로, 자동차 대 한 등록 데이터를 포함 하는 hello blob 파일에 대 한 참조 데이터 입력을 추가 합니다.
11. 클릭 **추가**, 한 다음 hello 동일 hello 스트림 입력에 대 한 처리에 선택에 따라 **참조 데이터** 대신 **데이터 스트림을** 및 hello **입력 별칭**  은 **등록**합니다.

12. **tolldata**로 시작하는 저장소 계정입니다. hello 컨테이너 이름은 여야 합니다 **tolldata**, 및 hello **경로 패턴** 해야 **registration.json**합니다. 이 파일 이름은 대/소문자를 구분하므로 **소문자**여야 합니다.
    
    ![블로그 저장소 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. 클릭 **만들기** toofinish hello 마법사.

이제 모든 입력이 정의되었습니다.

## <a name="define-output"></a>출력 정의
1. Hello 스트림 분석 작업 개요 창에서 선택 **출력**합니다.
   
    ![hello 출력 탭 및 옵션 "출력을 추가 합니다."](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. **추가**를 클릭합니다.
3. 집합 hello **출력 별칭** too'output' 차례로 **싱크** 너무**SQL 데이터베이스**합니다.
3. Hello hello 문서의 "Visual Studio에서 연결 tooDatabase" 섹션에에서 사용 된 hello 서버 이름을 선택 합니다. 데이터베이스 이름은 hello **TollDataDB**합니다.
4. 입력 **tolladmin** hello에 **USERNAME** 필드 **123toll!** hello에 **암호** 필드 및 **TollDataRefJoin** hello에 **테이블** 필드입니다.
   
    ![SQL Database 설정](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. **만들기**를 클릭합니다.

## <a name="azure-stream-analytics-query"></a>Azure Stream Analytics 쿼리
hello **쿼리** 탭 hello 들어오는 데이터를 변환 하는 SQL 쿼리를 포함 합니다.

![쿼리 추가 toohello 쿼리 탭](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

이 자습서는 tooanswer tooprovide Azure 스트림 분석에에서 사용할 수 있는 tootoll 데이터와 구문 스트림 분석 쿼리 관련 된 여러 가지 비즈니스 질문 관련 응답을 시도 합니다.

첫 번째 스트림 분석 작업을 시작 하기 전에 몇 가지 시나리오와 hello 쿼리 구문을 살펴보겠습니다.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>소개 tooAzure 스트림 분석 쿼리 언어
- - -
Toocount hello 수가 차량이 요금 소 창구를 입력 해야 하는 경우를 가정해 봅니다. 이벤트의 연속 스트림을 이기 때문에 있는 toodefine는 "기간 시간입니다." Hello 질문 toobe "개수 차량 입력 요금 소 창구 3 분 마다?"를 수정 해 보겠습니다. 이 일반적으로 참조 된 tooas hello count 텀블 링입니다.

이 질문에 응답 하는 hello Azure 스트림 분석 쿼리를 살펴보겠습니다.

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

볼 수 있듯이 Azure 스트림 분석 쿼리 언어는 SQL 유사 하며 추가 하는 몇 가지 확장 toospecify 시간 관련 쿼리의 항목이 hello 사용 합니다.

자세한 내용은 참고 [시간 관리](https://msdn.microsoft.com/library/azure/mt582045.aspx) 및 [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN에서 hello 쿼리에 사용 되는 구문입니다.

## <a name="testing-azure-stream-analytics-queries"></a>Azure Stream Analytics 쿼리 테스트
이제 첫 번째 Azure 스트림 분석 쿼리를 작성 한 경로 따라 hello에 TollApp 폴더에 있는 예제 데이터 파일을 사용 하 여 시간 tootest입니다.

**..\\TollApp\\TollApp\\Data**

이 폴더는 hello를 다음 파일이 포함 되어 있습니다.

* Entry.json
* Exit.json
* registration.json

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>질문 1: 요금 창구에 들어가는 차량 수
1. Azure 포털 hello 및 이동 tooyour 만든 Azure 스트림 분석 작업을 엽니다. Hello 클릭 **쿼리** 탭 하 고 hello 이전 섹션에서 쿼리를 붙여 넣습니다.

2. toovalidate 기호 및 선택 샘플 데이터를 클릭 하 여 EntryStream 입력 hello에 hello 데이터 업로드에 대해이 쿼리... hello **파일에서 샘플 데이터 업로드**합니다.

    ![Hello Entry.json 파일의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. 로컬 컴퓨터와 클릭 선택 hello 파일 (Entry.json) 나타나는 hello 창에서 **확인**합니다. hello **테스트** 아이콘 이제 켜려면 되며 클릭할 수 있습니다.
   
    ![Hello Entry.json 파일의 스크린 샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Hello 쿼리의 hello 출력 예상 대로 인지 확인 합니다.
   
    ![Hello 테스트의 결과](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>보고서 2 질문: hello 요금 소 창구를 통해 각 자동차 toopass에 대 한 총 시간
hello 요금 소를 통해 자동차 toopass 하는 데 필요한 평균 시간 hello hello 프로세스 및 hello 고객 경험 tooassess hello 효율성을 수 있습니다.

toofind hello 총 시간 hello ExitTime 스트림 사용 하 여 toojoin hello EntryTime 스트림이 필요 합니다. Hello 스트림을 TollId 및 LicencePlate 열에 연결 됩니다. hello **조인** 연산자는 hello 허용 가능한 시간 차이 hello 가입 이벤트를 설명 하는 임시 여유 toospecify 필요 합니다. 사용 하 여 **DATEDIFF** 이벤트를 서로 15 분 이내 해야 함을 toospecify 작동 합니다. Hello도 적용 **DATEDIFF** 함수 tooexit 및 항목 toocompute hello 실제 시간을 자동차 hello에서 소비한 시간 스테이션에 전화 합니다. Hello 사용의 hello 차이가 **DATEDIFF** 에서 사용 하는 경우는 **선택** 문을 아닌 **조인** 조건.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest 업데이트 hello 쿼리 hello에이 쿼리 **쿼리** hello 작업에 대 한 합니다. Hello 테스트 파일에 대 한 추가 **ExitStream** 마찬가지로 **EntryStream** 위에 입력 했습니다.
   
2. **테스트**를 클릭합니다.

3. Hello 확인란 tootest hello 쿼리 및 뷰 hello 출력을 선택 합니다.
   
    ![Hello 테스트의 출력](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>질문 3: 등록 기간이 만료된 모든 화물 차량 보고
Azure 스트림 분석 데이터 toojoin의 정적 스냅숏 임시 데이터 스트림에 사용 수 있습니다. toodemonstrate이이 기능을 사용 하 여 hello 샘플 질문을 수행 합니다.

Hello 소 업체에 상용차 등록 될 검사를 위해 정차할 수 없이 hello 요금 소 창구를 통해 전달할 수 있습니다. 상용차 등록 조회 테이블 tooidentify 등록 만료 된 모든 상용차를 사용 합니다.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest 참조 데이터를 사용 하 여 쿼리를 이미 수행한 hello 참조 데이터에 대 한 입력된 소스 toodefine를 할 수 있습니다.

tootest 붙여넣기 hello 쿼리 hello로이 쿼리에서 **쿼리** 탭을 클릭 **테스트**, 샘플 데이터 및 클릭 hello 두 입력된 소스 및 hello 등록 지정 **테스트**합니다.  
   
![Hello 테스트의 출력](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Hello 스트림 분석 작업 시작
이제 시간 toofinish hello 구성 및 시작 hello 작업입니다. 일치 하는 항목 hello hello의 스키마는 출력을 생성 하는 질문 3 자에서 hello 쿼리 저장 **TollDataRefJoin** 출력 테이블입니다.

이동 toohello 작업 **대시보드**를 클릭 하 고 **시작**합니다.

![Hello 작업 대시보드에 hello 시작 단추 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

Hello 대화 상자가 열리면 변경 hello **시작 출력** 너무 시간**사용자 지정 시간**합니다. 현재 시간 hello 하기 전에 hello 시간 tooone 시간을 변경 합니다. 이러한 변경 하면 hello 이벤트 허브의 모든 이벤트 hello 자습서의 hello 시작 부분에서 toogenerate hello 이벤트를 시작한 이후에 처리 됩니다. 이제 hello 클릭 **시작** 단추 toostart hello 작업 합니다.

![사용자 지정 시간 선택 항목](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Hello 작업을 시작 몇 분 정도 걸릴 수 있습니다. 스트림 분석에 대 한 최상위 페이지 hello hello 상태를 볼 수 있습니다.

![Hello 작업의 hello 상태 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Visual Studio에서 결과 확인
1. Visual Studio 서버 탐색기를 열고 hello를 마우스 오른쪽 단추로 클릭 **TollDataRefJoin** 테이블입니다.
2. 클릭 **테이블 데이터 표시** 작업의 toosee hello 출력 합니다.
   
    ![서버 탐색기의 "테이블 데이터 표시" 선택 항목](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Azure Stream Analytics 작업 규모 지정
Azure 스트림 분석은 설계 된 많은 양의 데이터를 처리할 수 있도록 tooelastically의 크기를 조정 합니다. hello Azure 스트림 분석 쿼리를 사용할 수는 **PARTITION BY** 절 tootell hello 시스템이이 단계는 확장입니다. **PartitionId** hello 입력 (이벤트 허브)의 toomatch hello 파티션 ID를 추가 하는 시스템 hello 특수 열이 있습니다.

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. 중지 hello 현재 작업을 hello에 업데이트 hello 쿼리 **쿼리** 탭을 선택한 열려 hello **설정** hello 작업 대시보드에 기어 합니다. **크기 조정**을 클릭합니다.
   
    **스트리밍 단위** 정의 hello 양을 작업 hello 계산 능력을 받을 수 있습니다.
2. 변경 hello 드롭 다운 6에서 1에서입니다.
   
    ![6개의 스트리밍 단위를 선택하는 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Toohello 이동 **출력** 탭 하 고 hello SQL 테이블의 hello 이름을 너무 변경**TollDataTumblingCountPartitioned**합니다.

Hello 작업을 시작할 이제 Azure 스트림 분석 더 많은 컴퓨팅 리소스 간에 작업을 분산 하 고 처리량을 높일 수 있습니다. 해당 hello TollApp 응용 프로그램 TollId로 분할 하는 이벤트를 보내는 note 하십시오.

## <a name="monitor"></a>모니터
hello **모니터** 영역 작업을 실행 하는 hello에 대 한 통계를 포함 합니다. 구성은 처음으로 필요한 hello에 toouse hello 저장소 계정이 동일한 지역 (이 문서의 나머지 부분 hello와 같은 이름 유료).   

![모니터링 스크린샷](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

에 액세스할 수 있습니다 **활동 로그** hello 작업 대시보드에서 **설정을** 영역도 있습니다.


## <a name="conclusion"></a>결론
이 자습서에서는 Azure 스트림 분석 서비스를 toohello 도입 되었습니다. 그 tooconfigure 입력 및 출력을 스트림 분석 작업 hello 방법을 보여 줍니다. Hello 자습서 hello 요금 데이터 시나리오를 사용 하 여 일반적인 유형의 동작 및 해결 방법에서 Azure 스트림 분석에서 간단한 SQL과 비슷한 쿼리를 사용 하 여 데이터의 hello 공간에서 발생 하는 문제를 설명 합니다. hello 자습서 임시 데이터로 작업 하기 위한 SQL 확장 구문을 설명 합니다. 어떻게 toojoin 데이터 스트림, 정적 참조 데이터로 tooenrich hello 데이터 스트림 방법 등에 대해 알아보았습니다 tooscale 쿼리 tooachieve 더 높은 처리량 아웃 합니다.

이 자습서가 개요에 해당하는 내용을 잘 소개하고는 있지만 완전하지는 않습니다. Hello SAQL 언어에서 사용 하 여 더 많은 쿼리 패턴을 찾을 수 있습니다 [일반적인 스트림 분석 사용 패턴에 대 한 예제 쿼리](stream-analytics-stream-analytics-query-patterns.md)합니다.
Toohello 참조 [온라인 설명서](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn Azure 스트림 분석에 대 한 자세한 합니다.

## <a name="clean-up-your-azure-account"></a>Azure 계정 정리
1. Hello Azure 포털의에서 hello 스트림 분석 작업을 중지 합니다.
   
    hello Setup.ps1 스크립트는 두 개의 이벤트 허브 및 SQL 데이터베이스를 만듭니다. hello 지침 도움말 hello 자습서의 hello 끝에 리소스를 정리를 수행 합니다.
2. PowerShell 창에 입력 **.\\ Cleanup.ps1** hello 자습서에 사용 되는 리소스를 삭제 하는 toostart hello 스크립트입니다.
   
   > [!NOTE]
   > 리소스는 hello 이름으로 식별 됩니다. 제거를 확인하기 전에 각 항목을 신중하게 검토해야 합니다.
   > 
   > 


