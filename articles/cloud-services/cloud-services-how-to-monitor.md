---
title: "aaaHow toomonitor 클라우드 서비스 | Microsoft Docs"
description: "Toomonitor hello Azure 클래식 포털을 사용 하 여 서비스를 클라우드 하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>TooMonitor 클라우드 서비스 하는 방법
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

모니터링할 수 있습니다 `key` hello Azure 클래식 포털에서에서 클라우드 서비스에 대 한 성능 메트릭을 합니다. 표시 되는 모니터링 하는 hello를 사용자 지정할 수 있습니다 및 toominimal 모니터링의 수준과 각 서비스 역할에 대 한 자세한 정보 표시 hello를 설정할 수 있습니다. 자세한 정보 표시 모니터링 데이터 hello 포털 외부에 액세스할 수 있는 저장소 계정에 저장 됩니다. 

Hello Azure 클래식 포털에서에서 모니터링 디스플레이 매우 구성할 수 있습니다. Hello 메트릭을 선택할 수 있습니다 toomonitor hello hello 메트릭 목록에서 원하는 **모니터** 페이지에서 선택할 수도 있습니다는 메트릭 tooplot 메트릭 차트 hello에 있는 **모니터** 페이지 및 hello 대시보드에. 

## <a name="concepts"></a>개념
기본적으로 최소 모니터링 hello 역할 인스턴스 (가상 컴퓨터)에 대 한 hello 호스트 운영 체제에서 수집 된 성능 카운터를 사용 하 여 새 클라우드 서비스에 제공 됩니다. hello 최소 메트릭은 제한 tooCPU 비율, 데이터, 데이터 출력, 디스크 읽기 처리량 및 디스크 쓰기 처리량입니다. 자세한 정보 표시 모니터링을 구성 하 여 hello 가상 컴퓨터 (역할 인스턴스) 내에서 성능 데이터를 기반으로 추적을 받을 수 있습니다. 자세한 정보 표시 메트릭을 hello 응용 프로그램 작업 중 발생 하는 문제를 보다 자세하게 분석을 사용 하도록 설정 합니다.

기본적으로 역할 인스턴스에서 성능 카운터 데이터 샘플링 하 고 hello 역할 인스턴스에서 3 분 간격으로 전송 됩니다. 자세한 정보 표시 모니터링을 사용 하도록 설정 하면 hello 원시 성능 카운터 데이터는 1 시간 및 12 시간 동안 5 분 간격으로 각 역할에 대 한 역할 인스턴스 및 각 역할 인스턴스에 대 한 집계 됩니다. hello 집계 된 데이터는 제거 10 일 후.

집계 hello 자세한 정보 표시 모니터링을 사용 하면 저장소 계정의 테이블에 모니터링 데이터가 저장 됩니다. tooenable 자세한 정보 표시 하는 역할에 대 한 모니터링을 toohello 저장소 계정을 연결 하는 진단 연결 문자열을 구성 해야 합니다. 역할에 따라 다른 저장소 계정을 사용할 수 있습니다.

저장소 비용 toodata 저장소, 데이터 전송 및 저장소 트랜잭션 관련 된 자세한 정보 표시 모니터링 증가 사용 하도록 설정 합니다. 최소 모니터링에는 저장소 계정이 필요하지 않습니다. hello tooverbose 수준 모니터링을 설정 하는 경우에 hello 데이터 hello 최소 모니터링 수준에 노출 되는 hello 메트릭에 대 한 저장소 계정에 저장 되지 않습니다.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>방법: Cloud Services에 대한 모니터링 구성
다음 프로시저 tooconfigure hello Azure 클래식 포털에서에서 모니터링 최소 또는 자세한 정보는 hello를 사용 합니다. 

### <a name="before-you-begin"></a>시작하기 전에
* 만들기는 *클래식* 저장소 계정 toostore hello 데이터를 모니터링 합니다. 역할에 따라 다른 저장소 계정을 사용할 수 있습니다. 자세한 내용은 참조 [어떻게 toocreate 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)합니다.
* 클라우드 서비스 역할에 대해 Azure 진단을 사용하도록 설정합니다. [Cloud Services에 대한 진단 구성](cloud-services-dotnet-diagnostics.md)을 참조하십시오.

Hello 진단 연결 문자열 hello 역할 구성에 있는지 확인 합니다. Azure 진단을 사용 하도록 설정 하 고 진단 연결 문자열 hello 역할 구성에 포함 될 때까지 자세한 정보 표시 모니터링 켤 수 없습니다.   

> [!NOTE]
> Azure SDK 2.5를 대상으로 하는 프로젝트 자동으로에 포함 하지 않은 hello 진단 연결 문자열 hello 프로젝트 템플릿을 합니다. 이러한 프로젝트에 대해 toomanually 해야 hello 진단 연결 문자열 toohello 역할 구성을 추가 합니다.
> 
> 

**toomanually 진단 연결 문자열 tooRole 구성 추가**

1. Visual Studio에서 열기 hello 클라우드 서비스 프로젝트
2. Hello에 두 번 클릭 **역할** tooopen 역할 디자이너 hello 선택한 hello **설정을** 탭
3. **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**이라는 설정을 찾습니다. 
4. 이 설정이 없으면 클릭 hello **설정 추가** 단추 tooadd 것 toohello 구성과 변경 hello hello 새 설정이 너무에 대 한 형식을**ConnectionString**
5. Hello를 클릭 하 여 연결 문자열 hello에 대 한 hello 값을 설정 **...**  단추입니다. 그러면 열립니다 tooselect을 수 있는 대화 상자를 저장소 계정.
   
    ![Visual Studio 설정](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>모니터링 수준 tooverbose toochange hello / 최소
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/)개방형 hello **구성** hello 클라우드 서비스 배포에 대 한 페이지입니다.
2. **수준**에서 **자세히** 또는 **최소**를 클릭합니다. 
3. **Save**를 클릭합니다.

자세한 정보 표시 모니터링을 설정 하면 후 hello 시간이 내의 hello Azure 클래식 포털에서에서 데이터를 모니터링 하는 hello 보기를 시작 해야 합니다.

hello 원시 성능 카운터 데이터 및 모니터링 데이터를 집계 된 hello 역할에 대 한 배포 ID hello로 정규화 된 테이블의 hello 저장소 계정에 저장 됩니다. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>방법: 클라우드 서비스 메트릭에 대한 경고 받기
클라우드 서비스 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다. Hello에 **관리 서비스** 페이지 hello Azure 클래식 포털을 만들 수 있습니다 규칙 tootrigger 경고 hello 메트릭을 선택 하면 사용자가 지정한 값에 도달 하는 경우. 또한 hello 경고가 트리거될 때 전송 toohave 전자 메일을 선택할 수 있습니다. 자세한 내용은 [방법: Azure에서 경고 알림 받기 및 경고 규칙 관리](http://go.microsoft.com/fwlink/?LinkId=309356)를 참조하세요.

## <a name="how-to-add-metrics-toohello-metrics-table"></a>방법: 메트릭 toohello 메트릭 테이블 추가
1. Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/)개방형 hello **모니터** hello 클라우드 서비스에 대 한 페이지입니다.
   
    기본적으로 hello 메트릭 테이블 hello 사용 가능한 메트릭의 하위 집합을 표시합니다. hello 그림 hello 역할 수준에서 집계 데이터와 함께 기본 hello 제한 toohello Memory\Available MBytes 성능 카운터는 클라우드 서비스에 대 한 자세한 정보 표시 메트릭을 보여 줍니다. 사용 하 여 **메트릭 추가** tooselect 추가 집계 및에 대 한 역할 수준 메트릭 toomonitor hello Azure 클래식 포털입니다.
   
    ![자세한 표시](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. tooadd 메트릭 toohello 메트릭 테이블:
   
   1. 클릭 **메트릭 추가** tooopen **메트릭 선택**, 다음과 같이 합니다.
      
       첫 번째 사용 가능한 메트릭을 hello에는 사용할 수 있는 확장 된 tooshow 옵션입니다. Hello 위쪽 옵션 각 메트릭에 대 한 모든 역할에 대해 집계 모니터링 데이터를 표시합니다. 또한 toodisplay 데이터에 대 한 개별 역할을 선택할 수 있습니다.
      
       ![메트릭 추가](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect 메트릭 toodisplay
      
      * 모니터링 옵션 hello 메트릭 tooexpand hello 하 여 hello 아래쪽 화살표를 클릭 합니다.
      * 각각에 대 한 확인란을 선택 hello toodisplay 원하는 옵션을 모니터링 합니다.
        
        Hello 메트릭 표에 too50 메트릭을를 표시할 수 있습니다.
        
        > [!TIP]
        > 자세한 정보 표시 모니터링 hello 메트릭 목록 메트릭 수십 포함할 수 있습니다. scrollbar toodisplay hello hello 대화 상자의 오른쪽 위로 가져갑니다. toofilter hello 목록 hello 검색 아이콘을 클릭 하 고 아래와 같이 hello 검색 상자에 텍스트를 입력 합니다.
        > 
        > 
        
        ![메트릭 검색 추가](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. 메트릭 선택을 마치면 확인(확인 표시)을 클릭합니다.
   
    hello 선택한 메트릭을 추가 하 toohello 메트릭 테이블에서 다음과 같이 합니다.
   
    ![모니터 메트릭](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete hello 메트릭 테이블에서 메트릭을 클릭 hello 메트릭 tooselect, 클릭 **메트릭을 삭제**합니다. 메트릭을 선택한 경우에만 **메트릭 삭제** 이 표시됩니다.

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tooadd 사용자 지정 메트릭 toohello 메트릭 테이블
hello **Verbose** hello 포털에서 모니터링할 수 있는 기본 메트릭 목록을 제공 수준을 모니터링 합니다. 또한 toothese 모든 사용자 지정 메트릭 또는 hello 포털을 통해 응용 프로그램에서 정의 하는 성능 카운터를 모니터링할 수 있습니다.

hello 다음 단계에서는 가정를 설정한 **Verbose** 모니터링 수준 및 응용 프로그램 toocollect 및 전송 사용자 지정 성능 카운터의 구성 합니다. 

toodisplay hello 사용자 지정 성능 카운터에 hello wad 컨트롤 컨테이너에서 hello 구성 tooupdate 필요한 포털:

1. 진단 저장소 계정에서 hello wad 컨트롤 컨테이너 blob을 엽니다. Visual Studio 또는 기타 저장소 탐색기 toodo 사용할 수 있습니다이 있습니다.
   
    ![Visual Studio 서버 Explorer](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Hello 패턴을 사용 하 여 hello blob 경로 탐색 **DeploymentId/RoleName/RoleInstance** 역할 인스턴스에 대 한 toofind hello 구성 합니다. 
   
    ![Visual Studio 저장소 Explorer](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. 역할 인스턴스에 대 한 hello 구성 파일을 다운로드 하 고 업데이트 tooinclude 모든 사용자 지정 성능 카운터입니다. 예를 들어 toomonitor *Disk Write Bytes/sec* hello에 대 한 *C 드라이브* hello 다음에서 추가 **PerformanceCounters\Subscriptions** 노드
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Hello 변경 내용 및 업로드 hello 구성 파일 백 toohello 저장 hello blob에서 기존 파일을 hello 동일한 위치 덮어씁니다.
5. Azure 클래식 포털 구성 hello에 tooVerbose 모드를 설정/해제 합니다. 자세한 정보 표시 모드에 이미 있던 경우 tootoggle toominimal 및 뒤로 tooverbose를 해야 합니다.
6. 사용자 지정 성능 카운터를 hello 이제 hello에 사용할 수 **메트릭 추가** 대화 상자. 

## <a name="how-to-customize-hello-metrics-chart"></a>방법: hello 메트릭 차트를 사용자 지정
1. Hello 메트릭 표에 hello 메트릭 차트에 메트릭 tooplot too6 선택 합니다. 메트릭을 tooselect 왼쪽된 면에 hello 확인란을 클릭 합니다. tooremove hello 메트릭 차트에서 메트릭을 hello 메트릭 테이블에서 해당 확인란의 선택을 취소 합니다.
   
    메트릭 hello 메트릭 테이블을 선택 하면 hello 메트릭은 toohello 메트릭 차트를 추가 됩니다. 좁은 디스플레이에 **자세한 n** 드롭 다운 목록 hello 디스플레이 맞지 않는 메트릭 헤더를 포함 합니다.
2. tooswitch 상대 값 (각 메트릭에 대해만 최종 값)과 절대 값 (Y 축 표시), 표시 간의 상대 또는 절대 hello 차트의 hello 위쪽을 선택 합니다.
   
    ![상대 또는 절대](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. toochange hello 시간 범위 hello 메트릭 차트 hello 차트의 위쪽 hello에 1 시간, 24 시간 또는 7 일을 선택 합니다.
   
    ![모니터 표시 기간](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    Hello 대시보드 메트릭 차트에 그리기 메트릭에 대 한 hello 메서드 차이가 있습니다. 표준 메트릭 집합을 사용할 수는 및 메트릭을 추가 하거나 hello 메트릭 헤더를 선택 하 여 제거 합니다.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>hello 대시보드에서 toocustomize hello 메트릭 차트
1. Hello 클라우드 서비스에 대 한 hello 대시보드를 엽니다.
2. 추가 하거나 hello 차트에서 메트릭을 제거:
   
   * tooplot hello 차트 헤더에서 hello 메트릭에 대 한 새 메트릭, 선택 hello 확인란 합니다. 좁은 표시 되는 아래쪽 화살표에서 hello 클릭  ***n* ?? 메트릭** tooplot 메트릭 hello 차트 머리글 영역을 표시할 수 없습니다.
   * 해당 헤더에 의해 확인란 선택을 취소 hello hello 차트에 메트릭 toodelete 합니다.
   
3. **상대** 및 **절대** 표시를 전환합니다.
4. 1 시간, 24 시간 또는 7 일간의 데이터 toodisplay 선택 합니다.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>방법: hello Azure 클래식 포털 외부 자세한 정보 표시 모니터링 데이터에 액세스
자세한 정보 표시 모니터링 데이터는 각 역할에 대해 지정 하는 hello 저장소 계정에서 테이블에 저장 됩니다. 각 클라우드 서비스 배포에 대 한 hello 역할에 대 한 6 개의 테이블이 만들어집니다. 각각(5분, 1시간 및 12시간)에 대해 두 개의 테이블이 만들어집니다. 역할 수준 집계; 저장 이러한 테이블 중 하나 역할 인스턴스에 대 한 다른 테이블 저장소 집계 hello 합니다. 

hello 테이블 이름에는 형식에 따라 hello:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

설명:

* *deploymentID* 는 hello toohello 클라우드 서비스 배포에 할당 된 GUID
* *aggregation_interval* = 5M, 1H 또는 12H
* 역할 수준 집계 = R
* 역할 인스턴스에 대한 집계 = RI

예를 들어 hello 다음 테이블은 저장 1 시간 간격으로 집계 하는 자세한 정보 표시 모니터링 데이터:

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
