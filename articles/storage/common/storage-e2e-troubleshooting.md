---
title: "진단 및 메시지 분석기 aaaTroubleshooting Azure 저장소 | Microsoft Docs"
description: "Azure 저장소 분석, AzCopy 및 Microsoft Message Analyzer를 사용한 종단 간 문제 해결을 보여 주는 자습서"
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 643372a3-1c07-4e88-b4ef-042512a43086
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/15/2017
ms.author: robinsh
ms.openlocfilehash: 2d7a2a14b2e8da01b566ac3dec19996f0ef88cc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Azure Storage 메트릭 및 로깅, AzCopy 및 메시지 분석기를 사용한 종단 간 문제 해결
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../../includes/storage-selector-portal-e2e-troubleshooting.md)]

진단 및 문제 해결은 Microsoft Azure 저장소를 사용하는 클라이언트 응용 프로그램을 빌드 및 지원하기 위한 핵심 기술입니다. Azure 응용 프로그램에서는 분산 toohello 이기 때문 진단 하 고 오류 및 성능 문제를 해결 기존 환경에서는 보다 훨씬 복잡할 수 있습니다.

이 자습서에서는 대해서도 설명 방법을 tooidentify 성능에 영향을 종단 간에서 이러한 오류를 해결 수 있는 특정 오류 순서 toooptimize hello 클라이언트 응용 프로그램에서 Azure 저장소 및 Microsoft에서 제공 하는 도구를 사용 합니다.

이 자습서는 종단 간 문제 해결 시나리오의 실습 탐색을 제공합니다. 개념에 대해 자세하게 설명 tootroubleshooting Azure 저장소 응용 프로그램에 대 한 참조 [모니터, 진단 및 해결 Microsoft Azure 저장소](storage-monitoring-diagnosing-troubleshooting.md)합니다.

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Azure 저장소 응용 프로그램 문제 해결 도구
Microsoft Azure 저장소를 사용 하 여 tootroubleshoot 클라이언트 응용 프로그램을 어떤 hello hello 문제의 원인일 수 있습니다 및 도구 toodetermine 문제가 발생 했을 때의 조합을 사용할 수 있습니다. 이러한 도구로는 다음이 있습니다.

* **Azure 저장소 분석**. [Azure 저장소 분석](/rest/api/storageservices/Storage-Analytics) 은 Azure 저장소에 대한 로깅 및 메트릭을 제공합니다.
  
  * **저장소 메트릭** 은 저장소 계정에 대한 트랜잭션 메트릭 및 용량 메트릭을 추적합니다. 메트릭을 사용 하 여, 응용 프로그램에 따라 tooa 다양 한 서로 다른 조치를 수행 되는 방법을 결정할 수 있습니다. 참조 [저장소 분석 통계 테이블 스키마](/rest/api/storageservices/Storage-Analytics-Metrics-Table-Schema) hello 유형의 메트릭 Storage Analytics에서 추적에 대 한 자세한 내용은 합니다.
  * **저장소 로깅** 각 요청 toohello Azure 저장소 서비스 tooa 서버 쪽 로그를 기록 합니다. hello 로그 트랙 hello 작업을 포함 하 여 각 요청에 대 한 자세한 데이터 수행 hello 상태 hello 작업 및 대기 시간 정보. 참조 [저장소 분석 로그 형식](/rest/api/storageservices/Storage-Analytics-Log-Format) toohello 로그 Storage Analytics에서 작성 된 hello 요청 및 응답 데이터에 대 한 자세한 내용은 합니다.

> [!NOTE]
> 저장소 계정 영역 중복 저장소 (ZRS)의 복제 형식과 hello 메트릭 또는 로깅 기능을 현재 사용 권한이 없습니다. 
> 
> 

* **Azure Portal**. Hello에서 저장소 계정에 대 한 메트릭 및 로깅을 구성할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 차트 및 응용 프로그램 시간이 지남에 따라 수행 되는 방법을 보여 주는 그래프를 볼 수 있고 응용 프로그램 보다 다르게 수행 하는 경우 지정 된 메트릭에 대 한 예상 경고 toonotify 구성 수도 있습니다.
  
    참조 [hello Azure 포털에서에서 저장소 계정을 모니터링](storage-monitor-storage-account.md) hello Azure 포털에서에서 모니터링을 구성 하는 방법에 대 한 정보에 대 한 합니다.
* **AzCopy**. Microsoft 메시지 분석기를 사용 하 여 분석에 대 한 AzCopy toocopy hello 로그 blob tooa 로컬 디렉터리를 사용할 수 있도록 Azure 저장소에 대 한 서버 로그를 blob으로 저장 됩니다. 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md) AzCopy에 대 한 자세한 내용은 합니다.
* **Microsoft Message Analyzer**. Message Analyzer는 로그 파일을 사용 하 고 쉽게 toofilter, 검색 및 그룹 tooanalyze 오류 및 성능 문제를 사용할 수 있는 유용한 집합으로 데이터를 기록 하는 시각적 형식 로그 데이터를에서 표시 하는 도구입니다. Message Analyzer에 대한 자세한 내용은 [Microsoft Message Analyzer 운영 가이드](http://technet.microsoft.com/library/jj649776.aspx)를 참조하세요.

## <a name="about-hello-sample-scenario"></a>Hello 샘플 시나리오에 대 한
이 자습서에서는 Azure 저장소 메트릭이 Azure 저장소를 호출하는 응용 프로그램에 대한 낮은 성공률을 나타내는 시나리오를 살펴보겠습니다. 낮은 성공 백분율 속도 메트릭을 hello (으로 표시 **PercentSuccess** hello에 [Azure 포털](https://portal.azure.com) 및 hello 메트릭 테이블)를 수행할 수 있지만 큰는 HTTP 상태 코드를 반환 하는 작업을 추적 보다 299 합니다. Hello 서버 쪽 저장소 로그 파일의 이러한 작업의 트랜잭션 상태와 함께 기록 됩니다 **ClientOtherErrors**합니다. Hello 낮은 성공 백분율 메트릭에 대 한 자세한 내용은 참조 하십시오. [메트릭에서 낮은 PercentSuccess 또는 분석 로그 항목 마다 ClientOtherErrors의 트랜잭션 상태와 함께 작업이](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success)합니다.

Azure 저장소 작업은 299보다 큰 HTTP 상태 코드를 정상적인 기능의 일부로 반환할 수 있습니다. 하지만 일부 경우 이러한 오류가 표시 있습니다 수 있다고 수 toooptimize 클라이언트 응용 프로그램에 대 한 향상 된 성능을 제공 합니다.

이 시나리오에서는 것 이라고 생각 낮은 성공 백분율 속도 toobe 100% 미만인 합니다. 그러나 Tooyour 요구에 따라 다른 메트릭 수준, 선택할 수 있습니다. 응용 프로그램을 테스트하는 동안 주요 성능 메트릭에 대해 기준 허용 오차를 설정하는 것이 좋습니다. 예를 들어 테스트에 따라 응용 프로그램이 90% 또는 85%의 일관된 성공률(백분율)을 유지해야 한다고 결정할 수 있습니다. 메트릭 데이터 hello 응용 프로그램에서 해당 숫자 벗어난은 표시 되 면 hello 증가 일으키는 원인을 조사할 수 있습니다.

샘플 시나리오에 대 한 hello 성공 백분율 속도 메트릭을 100%, toohello 메트릭, 상관 관계를 지정 하는 hello 로그 toofind hello 오류를 검사 하 고 사용 합니다 설정 했으므로 म toofigure 기능으로 인해 hello 낮은 백분율 성공률을 보입니다. Hello 400 범위에서 오류에 맞게 살펴보겠습니다. 그런 다음 404(찾을 수 없음) 오류를 더욱 자세하게 조사합니다.

### <a name="some-causes-of-400-range-errors"></a>400번대 오류의 몇 가지 원인
아래의 hello 예제에서는 Azure Blob 저장소에 대 한 요청에 대 한 일부 400 범위 오류 및 가능한 원인이 샘플링을 보여 줍니다. Hello 300 범위 및 hello 500 범위 오류 뿐 아니라 이러한 오류 중 하나는 tooa 낮은 백분율 성공률을 기여할 수 있습니다.

아래 hello 목록은 완료 멀리 떨어져 있는 참고 합니다. 참조 [상태 및 오류 코드](http://msdn.microsoft.com/library/azure/dd179382.aspx) hello 저장소 서비스의 특정 tooeach 오류 및 일반적인 Azure 저장소 오류에 대 한 세부 정보에 대 한 MSDN에 있습니다.

**상태 코드 404(찾을 수 없음) 예제**

Hello blob 또는 컨테이너 없기 때문에 컨테이너 또는 blob에 대 한 읽기 작업이 실패할 때 발생 합니다.

* 이 요청 이전에 다른 클라이언트가 컨테이너 또는 Blob을 삭제한 경우에 발생합니다.
* 있는지 확인 한 후 hello 컨테이너 또는 blob을 만드는 API 호출을 사용 하는 경우 발생 합니다. 경고는 CreateIfNotExists Api hello hello 컨테이너 또는 blob; hello 있는지에 대 한 첫 번째 toocheck 호출 헤드 확인 존재 하지 않는 경우 404 오류는 반환 되 고 두 번째 PUT 호출 toowrite hello 컨테이너 또는 blob입니다.

**상태 코드 409(충돌) 예제**

* 컨테이너 또는 blob 이름이 이미 있습니다. 있는지 먼저 확인 하지 않고 API 만들기 toocreate 새 컨테이너 또는 blob을 사용할 경우 발생 합니다.
* 컨테이너를 삭제 하는 경우 toocreate hello hello 삭제 작업이 완료 되기 전에 이름과 같은 이름을 사용 하 여 새 컨테이너를 시도 하면 발생 합니다.
* 컨테이너 또는 Blob에서 임대를 지정하는데 임대가 이미 존재하는 경우에 발생합니다.

**상태 코드 412(전제 조건 실패) 예제**

* 조건부 헤더에 의해 지정 된 hello 조건이 충족 되지 않았습니다 때 발생 합니다.
* 지정 된 임대 ID를 hello hello 컨테이너 또는 blob에서 임대 ID를 hello 일치 하지 않을 때 발생 합니다.

## <a name="generate-log-files-for-analysis"></a>분석에 대한 로그 파일 생성
이 자습서에서는 메시지 분석기 toowork 세 가지 유형의 로그 파일 사용 toowork이 중 하나를 선택할 수 있지만:

* hello **서버 로그**, Azure 저장소 로깅을 사용 하도록 설정 하면 생성 됩니다. hello 서버 로그 hello Azure 저장소 서비스-blob, 큐, 테이블 및 파일 중 하나에 대해 호출 하는 각 작업에 대 한 데이터를 포함 합니다. hello 서버 로그는 작업이 호출 된 어떤 상태 코드는 hello 요청 및 응답에 대 한 세부 정보를 반환 된, 뿐만 아니라 다른 나타냅니다.
* hello **.NET 클라이언트 로그**,.NET 응용 프로그램 내에서 클라이언트 쪽 로그를 사용 하도록 설정 하면 생성 됩니다. hello 클라이언트 로그 hello 클라이언트 hello 요청을 준비 하 고 받고 하는 방법 hello 응답을 처리 하는 방법에 대 한 자세한 정보를 포함 합니다.
* hello **HTTP 네트워크 추적 로그**, Azure 저장소에 대 한 작업을 포함 하 여 HTTP/HTTPS 요청 및 응답 데이터에서 데이터를 수집 합니다. 이 자습서에서는 메시지 분석기를 통해 hello 네트워크 추적을 생성 합니다.

### <a name="configure-server-side-logging-and-metrics"></a>서버 쪽 로깅 및 메트릭 구성
첫째, 해야 tooconfigure Azure 저장소 로깅 및 메트릭 데이터 hello 클라이언트 응용 프로그램 tooanalyze에서 할 수 있도록 합니다. 다양 한 방법으로-hello 통해에서 로깅 및 메트릭을 구성할 수 있습니다 [Azure 포털](https://portal.azure.com), PowerShell을 사용 하 여 또는 프로그래밍 방식으로 합니다. 로깅 및 메트릭 구성에 대한 자세한 내용은 MSDN에서 [저장소 메트릭 사용 및 메트릭 데이터 보기](http://msdn.microsoft.com/library/azure/dn782843.aspx) 및 [저장소 로깅 사용 및 로그 데이터 액세스](http://msdn.microsoft.com/library/azure/dn782840.aspx)를 참조하세요.

**Hello Azure 포털을 통해**

tooconfigure 로깅 및 메트릭을 사용 하 여 저장소 계정에 대 한 hello [Azure 포털](https://portal.azure.com), hello 지침에 따라 [hello Azure 포털에서에서 저장소 계정을 모니터링](storage-monitor-storage-account.md)합니다.

> [!NOTE]
> Hello Azure 포털을 사용 하 여 가능한 tooset 분 메트릭을 없습니다. 그러나 설정 않는 해당 응용 프로그램과 함께 성능 문제를 조사 하는 데 하 고이 자습서의 hello 위해 하는 것이 좋습니다. 분 메트릭, 아래와 같이 PowerShell을 사용 하 여 또는 프로그래밍 방식으로 hello 저장소 클라이언트 라이브러리를 사용 하 여 설정할 수 있습니다.
> 
> Note 해당 hello Azure 포털 분 메트릭, 매시간 메트릭만 표시할 수 없습니다.
> 
> 

**PowerShell을 통해**

Azure에 대 한 PowerShell 시작 tooget 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

1. 사용 하 여 hello [Add-azureaccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) cmdlet tooadd Azure 사용자 계정 toohello PowerShell 창:
   
    ```powershell
    Add-AzureAccount
    ```

2. Hello에 **tooMicrosoft Azure에에서 로그인** 창과 hello 전자 메일 주소를 입력 하면 계정과 연결 된 암호입니다. Azure 인증 및 hello 자격 증명 정보를 저장 하 고 hello 창을 닫습니다.
3. Hello PowerShell 창에서 이러한 명령을 실행 하 여 hello 자습서에 사용 하는 hello 기본 저장소 계정 toohello 저장소 계정을 설정 합니다.
   
    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. 저장소 Blob 서비스 hello에 대 한 로깅을 사용 하도록 설정:
   
    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Blob 서비스를 만드는 있는지 tooset hello에 대 한 저장소 메트릭을 사용 하도록 설정 **-MetricsType** 너무`Minute`:
   
    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>.NET 클라이언트 쪽 로깅 구성
클라이언트 쪽.NET 응용 프로그램에 대 한 로깅을 tooconfigure hello 응용 프로그램의 구성 파일 (web.config 또는 app.config)에.NET 진단을 사용 하도록 설정 합니다. 참조 [클라이언트 hello.NET 저장소 클라이언트 라이브러리를 사용 하 여 로깅](http://msdn.microsoft.com/library/azure/dn782839.aspx) 및 [클라이언트 hello Java 용 Microsoft Azure 저장소 SDK를 사용 하 여 로깅](http://msdn.microsoft.com/library/azure/dn782844.aspx) 대 한 자세한 내용은 MSDN에서 합니다.

클라이언트 쪽 로그 hello hello 클라이언트 hello 요청을 준비 하 고 받고 하는 방법 hello 응답을 처리 하는 방법에 대 한 자세한 정보를 포함 합니다.

저장소 클라이언트 라이브러리 hello hello 응용 프로그램의 구성 파일 (web.config 또는 app.config)에 지정 된 hello 위치에 클라이언트 쪽 로그 데이터를 저장 합니다.

### <a name="collect-a-network-trace"></a>네트워크 추적 수집
클라이언트 응용 프로그램을 실행 하는 동안 메시지 분석기 toocollect HTTP/HTTPS 네트워크 추적을 사용할 수 있습니다. 메시지 분석기 사용 하 여 [Fiddler](http://www.telerik.com/fiddler) hello에 백 엔드 합니다. Hello 네트워크 추적을 수집 하려면 먼저 Fiddler toorecord 암호화 하지 않고 HTTPS 트래픽을 구성 하는 것이 좋습니다.

1. [Fiddler](http://www.telerik.com/download/fiddler)를 설치합니다.
2. Fiddler를 시작합니다.
3. **도구 | Fiddler 옵션**을 선택합니다.
4. Hello 옵션 대화 상자에서 **HTTPS CONNECTs 캡처** 및 **HTTPS 트래픽을 암호를 해독** 모두 선택 다음과 같이 합니다.

![Fiddler 옵션 구성](./media/storage-e2e-troubleshooting/fiddler-options-1.png)

Hello 자습서에 대 한 수집 하 고 메시지 분석기에서 먼저 네트워크 추적을 저장 한 다음는 분석 세션 tooanalyze hello 추적 만들고 로그 hello 합니다. 메시지 분석기에 네트워크 추적 toocollect:

1. Message Analyzer에서 **파일 | 빠른 추적 | 암호화되지 않은 HTTPS**를 선택합니다.
2. hello 추적 즉시 시작 됩니다. 선택 **중지** toostop hello 추적 tootrace 저장소 트래픽을 구성할 수 있습니다.
3. 선택 **편집** tooedit hello 추적 세션입니다.
4. 선택 hello **구성** hello의 오른쪽 toohello 연결 **WebProxy Pef-Microsoft-** ETW 공급자입니다.
5. Hello에 **고급 설정** 대화 상자에서 hello 클릭 **공급자** 탭 합니다.
6. Hello에 **호스트 이름 필터** 필드를 공백으로 구분 하 여 저장소 끝점을 지정 합니다. 다음과 같이; 끝점을 지정할 수는 예를 들어 변경 `storagesample` toohello 사용자의 저장소 계정 이름:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Hello 대화 상자를 종료 하 고 클릭 **다시 시작** toobegin Azure 저장소 네트워크 트래픽만 hello 추적에 포함 되도록 hello 호스트 이름 필터를 적용 된 hello 추적을 수집 합니다.

> [!NOTE]
> 네트워크 추적을 수집을 완료 한 후 Fiddler toodecrypt HTTPS 트래픽이 변경 않은 hello 설정이 되돌릴 하는 것이 좋습니다. Hello Fiddler 옵션 대화 상자에서 hello의 선택을 취소 **HTTPS CONNECTs 캡처** 및 **해독 HTTPS 트래픽을** 확인란을 선택 합니다.
> 
> 

참조 [hello 네트워크 추적 기능을 사용 하 여](http://technet.microsoft.com/library/jj674819.aspx) 자세한 내용은 Technet의 합니다.

## <a name="review-metrics-data-in-hello-azure-portal"></a>Hello Azure 포털에서에서 메트릭 데이터를 검토 합니다.
응용 프로그램 시간 동안 실행 되 면 hello 나타나는 hello 메트릭 차트를 검토할 수 있습니다 [Azure 포털](https://portal.azure.com) tooobserve 서비스 수행 된 방식입니다.

첫째, hello Azure 포털에서에서 저장소 계정을 tooyour 이동 합니다. 기본적으로 hello로 차트는 모니터링 **성공률이** hello 계정 블레이드에서 메트릭을 표시 됩니다. Hello 차트 toodisplay 가지 다른 메트릭으로 이전에 수정 하는 경우 추가 hello **성공률이** 메트릭.

이제 표시 **성공률이** hello 모니터링 차트를에 다른 메트릭과 함께 추가 하는입니다. 메시지 분석기에서 hello 로그를 분석 하 여 다음 조사 합니다 hello 시나리오에서는 hello 백분율 성공률을 보입니다는 100% 미만입니다.

메트릭 차트 추가 및 사용자 지정에 대한 자세한 내용은 [메트릭 차트 사용자 지정](storage-monitor-storage-account.md#customize-metrics-charts)을 참조하세요.

> [!NOTE]
> 저장소 메트릭을 사용 하도록 설정한 후 hello Azure 포털에서에서 메트릭 데이터 tooappear 약간의 시간이 걸릴 수 있습니다. 즉, 현재 시간에서 경과 된 hello 될 때까지 이전 시간 hello에 대 한 시간 메트릭 hello Azure 포털에에서 표시 되지 않습니다. 또한, 분 메트릭 hello Azure 포털에에서 현재 표시 되지 않습니다. 메트릭을 사용 하도록 설정에 따라 지금 tootwo 시간 toosee 메트릭 데이터를 걸릴 수 있습니다.
> 
> 

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>AzCopy toocopy 서버 로그 tooa 로컬 디렉터리를 사용 하 여
Azure 저장소 메트릭 tootables 작성 하는 동안 서버 로그 데이터 tooblobs를 기록 합니다. 로그 blob는 잘 알려진 hello에서 사용할 수 있는 `$logs` 저장소 계정에 대 한 컨테이너입니다. 로그 blob 이름은 계층적으로 연도, 월, 일, 시간, tooinvestigate 관리할 기간과 hello 범위를 쉽게 찾을 수 있도록 합니다. 예를 들어 hello에에서 `storagesample` 계정이, 01/02/2015의 경우에서 8-오전 9 시, hello 로그 blob에 대 한 hello 컨테이너 `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`합니다. 부터는이 컨테이너에서 hello 개별 blob 순차적으로 라는 `000000.log`합니다.

로컬 컴퓨터의 hello AzCopy 명령줄 도구 toodownload 원하는 이러한 서버 쪽 로그 파일 tooa 위치를 사용할 수 있습니다. 예를 들어 hello에 배치 하는 blob 작업에 대 한 다음 명령 toodownload hello 로그 파일이 사용할 수 있습니다 2015 년 1 월 2 일 toohello 폴더 `C:\Temp\Logs\Server`; 대체 `<storageaccountname>` hello 저장소 계정의 이름으로 및 `<storageaccountkey>` 와 사용자 계정 액세스 키:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```
AzCopy는 hello에서 다운로드할 수 있는 [Azure 다운로드](https://azure.microsoft.com/downloads/) 페이지. AzCopy를 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.

서버 쪽 로그를 다운로드하는 방법에 대한 자세한 내용은 [저장소 로깅 로그 데이터 다운로드](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata)를 참조하세요.

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Microsoft 메시지 분석기 tooanalyze 로그 데이터를 사용 하 여
Microsoft Message Analyzer는 문제 해결 및 진단 시나리오에서 프로토콜 메시징 트래픽, 이벤트 및 기타 시스템 또는 응용 프로그램 메시지를 캡처, 표시 및 분석하는 도구입니다. Message Analyzer 또한 tooload, aggregate, 및 로그에서 데이터를 분석 있으며 추적 파일을 저장 합니다. Message Analyzer에 대한 자세한 내용은 [Microsoft Message Analyzer 운영 가이드(영문)](http://technet.microsoft.com/library/jj649776.aspx)를 참조하세요.

Message Analyzer tooanalyze 서버, 클라이언트 및 네트워크 로그 수 있는 Azure 저장소에 대 한 자산을 포함 합니다. 이 섹션에 대해 설명 합니다 방법을 toouse 이러한 도구 tooaddress hello에 낮은 성공 백분율의 문제 저장소 로그 hello 합니다.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>다운로드 하 고 메시지 분석기와 Azure 저장소 자산 hello를 설치 합니다.
1. 다운로드 [Message Analyzer](http://www.microsoft.com/download/details.aspx?id=44226) hello Microsoft 다운로드 센터에서 및 hello 설치 관리자를 실행 합니다.
2. Message Analyzer를 시작합니다.
3. Hello에서 **도구** 메뉴 선택 **자산 관리자**합니다. Hello에 **자산 관리자** 대화 상자에서 **다운로드**, 그런 다음 필터링 **Azure 저장소**합니다. Hello Azure 저장소 자산 아래 hello 그림에 나와 있는 것 처럼 표시 됩니다.
4. 클릭 **동기화 모든 표시 항목** tooinstall hello Azure 저장소 자산입니다. 사용 가능한 자산 hello 다음과 같습니다.
   * **Azure 저장소 색 규칙:** 및 글꼴 스타일 추적에 대 한 특정 정보를 포함 하는 toohighlight 메시지를 Azure 저장소 색 규칙 toodefine 텍스트 색을 사용 하는 특별 한 필터를 사용 합니다.
   * **Azure 저장소 차트:** Azure 저장소 차트는 서버 로그 데이터를 그래프로 표시하는 미리 정의된 차트입니다. 이 이번에 toouse Azure 저장소 차트, 다음과 같은 행위는 hello 서버 로그만 로드 hello 분석 눈금에 note 합니다.
   * **Azure 저장소 파서:** hello Azure 저장소 파서 구문 분석 hello Azure 저장소 클라이언트, 서버 및 HTTP가 로그인 순서 toodisplay로 hello 분석 눈금에에서 있습니다.
   * **Azure 저장소 필터:** Azure 저장소 필터는 사용할 수 있는 tooquery 데이터 hello 분석 그리드에서에서 미리 정의 된 조건입니다.
   * **Azure 저장소 보기 레이아웃:** Azure 저장소 보기 레이아웃은 미리 정의 된 열 레이아웃 및 hello 분석 눈금의에서 그룹화 합니다.
5. Hello 자산을 설치한 후 Message Analyzer를 다시 시작 합니다.

![메시지 분석기 자산 관리자](./media/storage-e2e-troubleshooting/mma-start-page-1.png)

> [!NOTE]
> 이 자습서의 hello 목적을 위해 표시 된 hello Azure 저장소 자산을 모두 설치 합니다.
> 
> 

### <a name="import-your-log-files-into-message-analyzer"></a>Message Analyzer로 로그 파일 가져오기
Microsoft Message Analyzer에서 분석을 위해 저장된 모든 로그 파일(서버 쪽, 클라이언트 쪽 및 네트워크)을 단일 세션으로 가져올 수 있습니다.

1. Hello에 **파일** Microsoft 메시지 분석기에서 메뉴를 클릭 **새 세션**, 클릭 하 고 **빈 세션**합니다. Hello에 **새 세션** 대화 상자에서 분석 세션에 대 한 이름을 입력 합니다. Hello에 **세션 정보** 패널에서 hello 클릭 **파일** 단추입니다.
2. 메시지 분석기에서 생성 된 tooload hello 네트워크 추적 데이터에서 클릭 **파일 추가**toohello 웹 추적 세션을 선택 hello.matp 파일에서.matp 파일을 저장 한 위치로 이동한 클릭 **열**.
3. tooload hello 서버 쪽 로그 데이터를 클릭할 **파일 추가**누르고 tooanalyze을 원하는 시간 범위 동안 hello hello 로그 파일 선택를 찾아보고 서버 쪽 로그 다운로드 toohello 위치 **열고**. 그런 다음, hello **세션 정보** 패널, 집합 hello **텍스트 로그 구성** 드롭 다운 각 서버 쪽 로그 파일에 대 한 너무**AzureStorageLog** tooensure는 Microsoft가 Message Analyzer 수 올바르게 구문 분석 hello 로그 파일입니다.
4. tooload hello 클라이언트 쪽 로그 데이터를 클릭할 **파일 추가**클라이언트 쪽 로그를 저장 한 toohello 위치를 찾아보고 누르고 tooanalyze를 원하는 로그 파일을 hello **열려**합니다. 그런 다음, hello **세션 정보** 패널, 집합 hello **텍스트 로그 구성** 드롭 다운 각 클라이언트 쪽 로그 파일에 대해 너무**AzureStorageClientDotNetV4** tooensure입니다 Microsoft 메시지 분석기 수 올바르게 구문 분석 hello 로그 파일입니다.
5. 클릭 **시작** hello에 **새 세션** 대화 tooload 및 구문 분석 hello 로그 데이터입니다. 데이터를 기록 하는 hello hello 메시지 분석기 분석 눈금에에서 표시 됩니다.

아래 hello 그림에서는 서버, 클라이언트 및 네트워크 추적 로그 파일을 사용 하 여 구성 하는 예에서는 세션을 보여 줍니다.

![Message Analyzer 세션 구성](./media/storage-e2e-troubleshooting/configure-mma-session-1.png)

Message Analyzer는 로그 파일을 메모리에 로드합니다. Toofilter 원하는 다양 한 로그 데이터를 설정한 경우에 순서 tooget hello 메시지 분석기에서 최상의 성능을 합니다.

첫째, 검토에 관심이 있는 hello 기간을 확인 하 고이 기간을 가능한 한 작게 유지 하십시오. 대부분의 경우에서 분 단위 또는 시간에서 최대의 tooreview 해야 합니다. 사용자의 요구를 충족할 수 있는 로그의 hello 가능한 한 작은 집합을 가져옵니다.

아직 많은 양의 데이터를 기록 하는 경우 다음 좋습니다 toospecify 세션 필터 toofilter 로그 데이터 로드 하기 전에. Hello에 **세션 필터** 상자, 선택 hello **라이브러리** toochoose 미리 정의 된 필터 단추; 예를 들어 선택 **글로벌 시간 필터 I** hello 필터링 하는 Azure 저장소에서 시간 간격에 toofilter 합니다. 다음 시작 하는 hello 필터 조건 toospecify hello 편집한 toosee 원하는 hello 간격에 대 한 타임 스탬프를 종료 합니다. 특정 상태 코드;에 필터링 할 수 있습니다. 예를 들어 hello 상태 코드 404 인 tooload만 로그 항목을 선택할 수 있습니다.

로그 데이터를 Microsoft Message Analyzer로 가져오는 방법에 대한 자세한 내용은 TechNet에서 [메시지 데이터 검색(영문)](http://technet.microsoft.com/library/dn772437.aspx) 을 참조하세요.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Hello 클라이언트 요청 ID toocorrelate 로그 파일 데이터를 사용 하 여
hello Azure 저장소 클라이언트 라이브러리는 자동으로 모든 요청에 대 한 고유한 클라이언트 요청 ID를 생성합니다. 이 값은 작성 된 toohello 클라이언트 로그, hello 서버 로그 hello 네트워크 추적 메시지 분석기 내에서 모든 세 로그에서 toocorrelate 데이터 사용할 수 있습니다. 참조 [클라이언트 요청 ID](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) hello 클라이언트에 대 한 추가 정보에 대 한 요청 id입니다.

아래 hello 섹션에서 설명 하는 방법을 toouse 미리 구성 된 사용자 지정 레이아웃 toocorrelate 및 그룹 데이터에 따라 및 보기가 hello 클라이언트 요청 id입니다.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>보기 레이아웃 toodisplay hello 분석 그리드에서 선택
메시지 분석기에 대 한 hello 저장소 자산에는 Azure 저장소 보기 레이아웃을 사용할 수 있는 toodisplay 데이터 유용한 그룹화과 열이 있는 여러 시나리오에 대해 미리 구성 된 보기가 포함 됩니다. 또한, 사용자 지정 보기 레이아웃을 생성하고 다시 사용하기 위해 저장할 수도 있습니다.

hello 아래 그림과 hello **뷰 레이아웃** 선택 하 여 사용할 수 있는 메뉴 **뷰 레이아웃** hello 도구 모음 리본에서 합니다. Azure 저장소에 대 한 hello 보기 레이아웃 hello 그룹화 되어 **Azure 저장소** hello 메뉴에서 노드. 검색할 수 있습니다 `Azure Storage` Azure 저장소에서 검색 상자 toofilter hello 레이아웃만 확인 합니다. Hello 별모양 다음 tooa 보기 레이아웃 toomake 선택할 수도 있습니다 즐겨찾기는 hello 메뉴의 hello 위쪽에 표시 합니다.

![보기 레이아웃 메뉴](./media/storage-e2e-troubleshooting/view-layout-menu.png)

select와 함께 toobegin **ClientRequestID 및 모듈 별로 그룹화 되어**합니다. 이 보기 레이아웃은 먼저 세 로그 모두의 로그 데이터를 클라이언트 요청 ID별로 그룹화한 후 원본 로그 파일(또는 Message Analyzer의 **모듈** )별로 그룹화합니다. 이 보기를 사용하여 특정 클라이언트 요청 ID로 드릴다운하고 해당 클라이언트 요청 ID에 대한 세 로그 파일 모두의 데이터를 볼 수 있습니다.

아래 hello 그림에는이 레이아웃 보기 적용 toohello 샘플 로그 데이터를 표시 된 열의 하위 집합을 보여 줍니다. 특정 클라이언트 요청 ID에 대 한 hello 분석 눈금 표시 hello 클라이언트 로그 및 서버 로그 및 네트워크 추적 데이터를 볼 수 있습니다.

![Azure 저장소 보기 레이아웃](./media/storage-e2e-troubleshooting/view-layout-client-request-id-module.png)

> [!NOTE]
> 서로 다른 파일 서로 다른 열이 있어야 하므로 일부 열 여러 로그 파일의에서 데이터는 hello 분석 눈금에에서 표시 되 면 지정된 된 행에 대 한 데이터를 포함 하지 않을 수 있습니다. 예를 들어 위 hello 그림에는 클라이언트 로그 행 표시 안 함 hello에 대 한 데이터 **타임 스탬프**, **TimeElapsed**, **소스**, 및 **대상** 열 때문에 이러한 열 hello 클라이언트 로그에 존재 하지 않지만 hello 네트워크 추적에도 합니다. 마찬가지로, hello **타임 스탬프** 열 hello 서버 로그에서 타임 스탬프 데이터를 표시 하지만 hello에 대 한 데이터는 **TimeElapsed**, **소스**, 및  **대상** hello 서버 로그의 일부분이 아닌 있는 열입니다.
> 
> 

또한 toousing hello Azure 저장소 보기 레이아웃을 정의 하 고 수도 있습니다 직접 보기 레이아웃을 저장 합니다. 데이터 그룹화에 대 한 기타 필드를 선택 하 고 사용자 지정 레이아웃의 일환으로 hello 그룹화를 저장할 수 있습니다.

### <a name="apply-color-rules-toohello-analysis-grid"></a>색 규칙 toohello 분석 그리드를 적용 합니다.
hello 저장소 자산은 또한 시각적 의미 tooidentify 여러 유형의 hello 분석 그리드에서에서 오류를 제공 하는 색 규칙을 포함 합니다. hello 미리 정의 된 색 규칙 적용 tooHTTP 오류 없으므로 hello 서버 추적 로그와 네트워크에 대해서만 표시 됩니다.

tooapply 색 규칙 선택 **색 규칙** hello 도구 모음 리본에서 합니다. Hello Azure 저장소 색 규칙 hello 메뉴에 표시 됩니다. Hello 자습서에 대 한 선택 **클라이언트 오류 (StatusCode 400에서 499 사이)**아래 hello 그림에 나온 것 처럼 합니다.

![Azure 저장소 보기 레이아웃](./media/storage-e2e-troubleshooting/color-rules-menu.png)

또한 toousing hello Azure 저장소 색 규칙을 정의 하 고 사용자 고유의 색 규칙을 저장할 수도 있습니다.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>그룹화 및 필터링 로그 데이터 toofind 400 범위 오류
다음으로 그룹 알아보고 hello 로그 데이터 toofind hello 400 범위에서 모든 오류를 필터링 하겠습니다.

1. Hello 찾을 **StatusCode** hello 분석 눈금을 마우스 오른쪽 단추로 클릭 hello 열 머리글과 선택에서 열 **그룹**합니다.
2. 다음으로 그룹 hello에 **ClientRequestId** 열입니다. Hello 분석 눈금은 이제 기준으로 상태 구성의 hello 데이터 코드 및 id입니다. 클라이언트 요청에 의해 표시 됩니다.
3. 아직 표시 되지 않은 경우 hello 뷰 필터 도구 창을 표시 합니다. Hello 도구 모음 리본에서 선택 **도구 창**, 다음 **뷰 필터**합니다.
4. toofilter hello 로그 데이터 toodisplay 범위만 400 오류 추가 필터 조건을 toohello 다음 hello **뷰 필터** 창과 클릭 **적용**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

아래 hello 그림이 그룹화 및 필터의 hello 결과 보여 줍니다. 확장 hello **ClientRequestID** 해당 상태 코드가 발생 하는 작업에서는 상태 코드 409, 예를 들어에 대 한 그룹화 hello 아래에 있는 필드입니다.

![Azure 저장소 보기 레이아웃](./media/storage-e2e-troubleshooting/400-range-errors1.png)

이 필터를 적용 한 후 표시 hello 클라이언트 로그에서 행은 제외 됩니다, hello로 클라이언트 로그 포함 되지 않습니다는 **StatusCode** 열입니다. hello 서버 및 네트워크 추적 로그 toolocate 404 오류를 검토 합니다와 toobegin, 및 toohello 클라이언트 로그 tooexamine hello 클라이언트 작업 toothem 발생 시킨 다음 반환 합니다.

> [!NOTE]
> Hello 필터링 할 수 있습니다 **StatusCode** hello 상태 코드는 null 로그 항목을 포함 하는 식 toohello 필터를 추가 하는 경우 열 및 데이터를 포함 하 여 모든 3 개의 로그 표시 hello 클라이언트 로그 합니다. tooconstruct이 필터 식에서 사용 하 여:
> 
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
> 
> 이 필터 모든 행에서에서 반환 hello 클라이언트 로그와 hello 서버 로그와 HTTP 로그의 행만 hello 상태 코드는 400을 초과 합니다. 적용 하는 경우 클라이언트 요청 ID 및 모듈 별로 그룹화 되어 toohello 보기 레이아웃을 검색할 수 있습니다 또는 hello 통해 스크롤 로그 항목 toofind 하십시오. 3 개의 로그를 모두 표시 됩니다.   
> 
> 

### <a name="filter-log-data-toofind-404-errors"></a>로그 데이터 toofind 404 오류 필터링
hello 저장소 자산 toonarrow 로그 데이터 toofind hello 오류 또는 원하는 추세를 사용할 수 있는 미리 정의 된 필터를 포함 합니다. 다음으로, 두 개의 미리 정의 된 필터를 적용 합니다 우리: hello 서버 및 404 오류에 대 한 네트워크 추적 로그를 필터링 하는 생성자와 지정된 된 시간 범위에 hello 데이터를 필터링 하 합니다.

1. 아직 표시 되지 않은 경우 hello 뷰 필터 도구 창을 표시 합니다. Hello 도구 모음 리본에서 선택 **도구 창**, 다음 **뷰 필터**합니다.
2. Hello 보기 필터 창에서 선택한 **라이브러리**, 검색 및 `Azure Storage` toofind hello Azure 저장소를 필터링 합니다. 에 대 한 선택 hello 필터 **404 (찾을 수 없음)이 모든 로그에서 메시지**합니다.
3. 디스플레이 hello **라이브러리** 메뉴 다시 찾아서 hello 선택 **글로벌 시간 필터**합니다.
4. 원하는 tooview hello 필터 toohello 범위에 표시 된 hello 타임 스탬프를 편집 합니다. 이 데이터 tooanalyze toonarrow hello 범위를 도움이 됩니다.
5. 필터에는 아래와 유사한 toohello 예제 표시 되어야 합니다. 클릭 **적용** tooapply hello 필터 toohello 분석 눈금.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

    ![Azure 저장소 보기 레이아웃](./media/storage-e2e-troubleshooting/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>로그 데이터 분석
그룹화 하 고 데이터를 필터링 했으므로 404 오류를 생성 하는 개별 요청에 대 한 hello 세부 정보를 검사할 수 있습니다. 현재 보기 레이아웃 hello hello 데이터는 다음 로그 소스에서 클라이언트 요청 ID로 그룹화 됩니다. 별로 필터링 요청에 hello StatusCode 필드 404이 들어 있는, 이후 hello 서버 및 네트워크 추적 데이터, 클라이언트 로그 데이터가 아닌 hello 보겠습니다.

아래 hello 그림 hello blob이 존재 하지 않기 때문에 Blob 가져오기 작업에서 404 생성 하는 위치는 특정 요청을 보여 줍니다. 참고는 일부 열 hello 순서 toodisplay hello 관련 데이터의 표준 보기에서 제거 되었습니다.

![필터링 된 서버 및 네트워크 추적 로그](./media/storage-e2e-troubleshooting/server-filtered-404-error.png)

다음으로, म 합니다 관련이 있어서이 클라이언트 요청 ID를 hello 클라이언트 로그 데이터 toosee hello 오류가 발생 했을 때 어떤 작업 hello 클라이언트가 수강. 이 세션 tooview hello 클라이언트 로그 데이터에 대 한 두 번째 탭에서 열립니다 새 분석 그리드 보기를 표시할 수 있습니다.

1. 첫째, hello의 hello 값을 복사 **ClientRequestId** 필드 toohello 클립보드 합니다. 이렇게 하려면 행 중 하나를 선택 하 여 hello 찾기 **ClientRequestId** hello 데이터 값을 마우스 오른쪽 단추로 클릭 하 고 선택 필드 **복사 'ClientRequestId'**합니다.
2. Hello 도구 모음 리본에서 선택 **새 뷰어**을 선택한 후 **분석 그리드** tooopen 새 탭 hello 새 탭 모든 데이터를 표시, 그룹화, 필터링 또는 색 규칙 없이 로그 파일에 있습니다.
3. Hello 도구 모음 리본에서 선택 **뷰 레이아웃**을 선택한 후 **모든.NET 클라이언트 열** hello에서 **Azure 저장소** 섹션. 이 보기 레이아웃은 서버 및 네트워크 추적 로그 hello와 hello 클라이언트 로그에서 데이터를 표시합니다. 기본적으로 hello에 정렬 됩니다 **MessageNumber** 열입니다.
4. 그런 다음 검색 hello 클라이언트 로그 hello 클라이언트 요청 id입니다. Hello 도구 모음 리본에서 선택 **메시지 찾기**, 다음 hello에 hello 클라이언트 요청 ID에서 사용자 지정 필터를 지정 **찾을** 필드입니다. 고유한 클라이언트 요청 ID를 지정 하는 hello 필터에 대 한이 구문을 사용 합니다.

    ```
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

Message Analyzer를 찾아서 hello 검색 조건을 hello 클라이언트 요청 ID와 일치 하는 hello 첫 번째 로그 항목을 선택 합니다. Hello 클라이언트 로그에 있는 각 클라이언트 요청 ID에 대 한 여러 항목이 toogroup 할 수 있습니다 hello에서 **ClientRequestId** 필드 toomake 것 보다 쉽게 toosee 모두 함께 해당 합니다. hello 그림 hello 클라이언트에서 hello 메시지의 모든 로그 hello에 대 한 다음 지정한 클라이언트 요청 id입니다.

![404 오류를 표시하는 클라이언트 로그 ](./media/storage-e2e-troubleshooting/client-log-analysis-grid1.png)

이 두 탭에서 hello 보기 레이아웃에 표시 된 hello 데이터를 사용 하 여 hello 요청 데이터 toodetermine를 분석할 구성할 수 수 있는 오류를 일으킨 hello 수 있습니다. 이전 이벤트 toohello 404 오류를 야기 될 수 있습니다 하는 경우이 하나의 toosee 앞에 요청을 살펴볼 수도 있습니다. 예를 들어 hello blob 삭제 여부 hello 오류 기한 toohello 클라이언트 응용 프로그램 컨테이너 또는 blob에서 경고는 CreateIfNotExists API를 호출 하는 경우이 클라이언트 요청 ID toodetermine 앞 hello 클라이언트 로그 항목을 검토할 수 있습니다. Hello 클라이언트 로그에 hello에 hello blob의 주소를 찾을 수 **설명** 필드; hello 서버 및 네트워크 추적 로그에서이 정보에 hello 표시 **요약** 필드입니다.

Hello 404 오류를 생성 하는 hello blob의 hello 주소를 알게 되 면 있습니다는 더 조사할 수 있습니다. 와 관련 된 다른 메시지에 대 한 hello 로그 항목을 검색 하는 경우 동일한 blob hello에 대 한 작업, hello 클라이언트 hello 엔터티를 이전에 삭제 여부를 확인할 수 있습니다.

## <a name="analyze-other-types-of-storage-errors"></a>다른 유형의 저장소 오류 분석
다른 유형의 보기를 사용 하 여 오류를 분석할 수 사용 하 여 메시지 분석기 tooanalyze 로그 데이터에 익숙한 했으므로 레이아웃, 색 규칙 및 검색 하 고 필터링 합니다. hello 테이블 아래의 목록은 몇 가지 문제가 발생 하 고 hello 필터 조건 toolocate를 사용할 수 있습니다 이러한. 필터 및 hello 메시지 분석기 생성에 대 한 자세한 내용은 참조 언어에서 필터링 [메시지 데이터 필터링](http://technet.microsoft.com/library/jj819365.aspx)합니다.

| tooInvestigate 중... | 필터 식 사용... | 적용 대상 tooLog 식 (클라이언트, 서버, 네트워크, 모두) |
| --- | --- | --- |
| 큐에서 메시지 배달의 예기치 않은 지연 |AzureStorageClientDotNetV4.Description은 "다시 시도 중 작업이 실패 했습니다."를 포함 |클라이언트 |
| PercentThrottlingError에서 HTTP 증가 |HTTP.Response.StatusCode   == 500 &#124;&#124; HTTP.Response.StatusCode == 503 |네트워크 |
| PercentTimeoutError의 증가 |HTTP.Response.StatusCode   == 500 |네트워크 |
| PercentTimeoutError의 증가(모두) |*StatusCode   == 500 |모두 |
| PercentNetworkError의 증가 |AzureStorageClientDotNetV4.EventLogEntry.Level   < 2 |클라이언트 |
| HTTP 403(사용할 수 없음) 메시지 |HTTP.Response.StatusCode   == 403 |네트워크 |
| HTTP 404(찾을 수 없음) 메시지 |HTTP.Response.StatusCode   == 404 |네트워크 |
| 404(모두) |*StatusCode   == 404 |모두 |
| SAS(공유 액세스 서명) 권한 부여 문제 |AzureStorageLog.RequestStatus ==  "SASAuthorizationError" |네트워크 |
| HTTP 409(충돌) 메시지 |HTTP.Response.StatusCode   == 409 |네트워크 |
| 409(모두) |*StatusCode   == 409 |모두 |
| PercentSuccess가 낮게 표시되거나 분석 로그 항목에 트랜잭션 상태가 ClientOtherErrors 상태인 작업이 있음 |AzureStorageLog.RequestStatus ==   "ClientOtherError" |서버 |
| Nagle 경고 |((AzureStorageLog.EndToEndLatencyMS   - AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS *   1.5)) 및 (AzureStorageLog.RequestPacketSize <1460) 및 (AzureStorageLog.EndToEndLatencyMS -   AzureStorageLog.ServerLatencyMS >= 200) |서버 |
| 서버 및 네트워크 로그의 시간 범위 |#Timestamp   >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39 |서버, 네트워크 |
| 서버 로그의 시간 범위 |AzureStorageLog.Timestamp   >= 2014-10-20T16:36:38 및 AzureStorageLog.Timestamp <=   2014-10-20T16:36:39 |서버 |

## <a name="next-steps"></a>다음 단계
Azure 저장소의 종단 간 시나리오 문제 해결에 대한 자세한 내용은 다음 리소스를 참조하세요.

* [Microsoft Azure 저장소 모니터링, 진단 및 문제 해결](storage-monitoring-diagnosing-troubleshooting.md)
* [저장소 분석](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Hello Azure 포털에서에서 저장소 계정을 모니터링합니다](storage-monitor-storage-account.md)
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](storage-use-azcopy.md)
* [Microsoft Message Analyzer 운영 가이드](http://technet.microsoft.com/library/jj649776.aspx)
