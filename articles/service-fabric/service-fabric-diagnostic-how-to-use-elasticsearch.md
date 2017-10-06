---
title: "서비스 패브릭 응용 프로그램 추적 저장소로 Elasticsearch aaaUsing | Microsoft Docs"
description: "Elasticsearch 및 Kibana toostore, 인덱스 및 응용 프로그램 추적 (로그)을 통해 검색 서비스 패브릭 응용 프로그램에서 사용 하 여 방법 설명"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>서비스 패브릭 응용 프로그램 추적 저장소로 ElasticSearch 사용
## <a name="introduction"></a>소개
이 문서에서는 [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) 응용 프로그램이 프로그램 추적 저장소, 인덱싱 및 검색을 위해 **Elasticsearch** 및 **Kibana**를 사용할 수 있는 방법에 대해 설명합니다. [Elasticsearch](https://www.elastic.co/guide/index.html)는 이 작업에 적합한 공개 소스, 분산 및 확장 가능한 실시간 검색 및 분석 엔진이며 Microsoft Azure에서 실행되는 Windows 및 Linux 가상 컴퓨터에 설치할 수 있습니다. Elasticsearch는 **ETW(Windows용 이벤트 추적)**와 같은 기술을 사용하여 생성된 *구조화된* 추적을 효율적으로 처리할 수 있습니다.

ETW는 서비스 패브릭 런타임에서 toosource 진단 정보 (추적)에서 사용 됩니다. Hello 권장 되는 방법에 대 한 서비스 패브릭 응용 프로그램 toosource의 진단 정보를 너무 이며 런타임에서 제공 하 고 응용 프로그램에서 제공 하는 추적 및 쉽게 관련 된 문제 해결 간의 상관 관계에 대 한 동일한 메커니즘을 사용 하면 hello를 사용 합니다. 로깅 API를 포함 하는 Visual Studio에서 서비스 패브릭 프로젝트 템플릿 (hello.NET 기반 **EventSource** 클래스)는가 기본적으로 ETW 추적을 내보냅니다. ETW를 사용한 서비스 패브릭 응용 프로그램 추적에 대한 일반적인 개요는 [로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)를 참조하세요.

Hello 추적 tooshow를에서 Elasticsearch에 대 한 toobe (hello 응용 프로그램 실행 중) 실시간으로 hello 서비스 패브릭 클러스터 노드에서 캡처된 및 tooan Elasticsearch 끝점으로 전송 해야 합니다. 추적 캡처에 대한 두 가지 주요 옵션이 있습니다.

* **In Process 추적 캡처**  
  hello 응용 프로그램 또는 서비스 프로세스를 보다 정확 하 게 hello 진단 데이터 toohello 추적 저장소 (Elasticsearch)을 보내는 담당 합니다.
* **Out of Process 추적 캡처**  
  별도 에이전트 hello 서비스 프로세스 또는 프로세스에서 추적을 캡처할 이며 toohello 추적 저장소 보내기.

아래 tooset Azure에서 Elasticsearch 논의 hello 전문가 방법과 단점 모두에 대 한 옵션을 캡처하고 tooconfigure 서비스 패브릭 toosend 데이터 tooElasticsearch를 서비스 하는 방법에 대해 설명 설명 합니다.

## <a name="set-up-elasticsearch-on-azure"></a>Azure에 Elasticsearch 설정
hello Azure에서 Elasticsearch 서비스 hello 가장 간단한 방법은 tooset 방식은 [ **Azure 리소스 관리자 템플릿을**](../azure-resource-manager/resource-group-overview.md)합니다. 포괄적인 [Elasticsearch에 대한 빠른 시작 Azure 리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) 은 Azure 빠른 시작 템플릿 리포지토리에서 사용할 수 있습니다. 이 템플릿에서는 규모 단위(노드 그룹)에 대한 별도의 저장소 계정을 사용합니다. 또한 서로 다른 구성 및 여러 개의 연결된 데이터 디스크를 사용하여 별개의 클라이언트 및 서버 노드를 프로비전할 수 있습니다.

여기서 이라는 다른 서식 파일 사용 **ES MultiNode** hello에서 [진단 도구를 Azure 저장소](https://github.com/Azure/azure-diagnostics-tools)합니다. 이 서식 파일은 쉽게 toouse 하 고 HTTP 기본 인증으로 보호 하는 Elasticsearch 클러스터를 만듭니다. 계속 진행 하기 전에 hello 리포지토리 복제 또는 zip 파일 다운로드) 하는 것 (여 hello 리포지토리 GitHub tooyour 컴퓨터에서 다운로드 합니다. hello로 hello 폴더에 있는 hello ES MultiNode 템플릿을 동일한 이름입니다.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>컴퓨터 toorun Elasticsearch 설치 스크립트 준비
hello 가장 쉬운 방법은 toouse hello ES MultiNode 서식 파일은 호출 하는 제공 된 Azure PowerShell 스크립트를 통해 `CreateElasticSearchCluster`합니다. toouse tooinstall PowerShell 모듈 및 도구가 필요한이 스크립트 **openssl**합니다. 후자의 hello Elasticsearch 클러스터 tooadminister 사용된 될 수 있는 SSH 키를 원격으로 만드는 데 필요 합니다.

`CreateElasticSearchCluster`스크립트는 Windows 컴퓨터의 hello ES MultiNode 템플릿으로 사용 편의성을 위해 설계 되었습니다. 비 Windows 컴퓨터에서 가능한 toouse hello 템플릿을 이지만 시나리오는이 문서의 hello 다루지 않습니다.

1. 아직 설치하지 않은 경우 [**Azure PowerShell 모듈**](http://aka.ms/webpi-azps)을 설치합니다. 메시지가 표시되면 **실행**을 클릭한 다음 **설치**합니다. Azure PowerShell 1.3 이상이 필요합니다.
2. hello **openssl** 도구의 hello 배포에 포함 되어 [ **Windows 용 Git**](http://www.git-scm.com/downloads)합니다. [Windows용 GIT](http://www.git-scm.com/downloads) 를 아직 설치하지 않은 경우 지금 설치하세요. (hello 기본 설치 옵션은 확인 합니다.)
3. Git 설치 되었지만 hello 시스템 경로에 포함 되지 않은 가정할 Microsoft Azure PowerShell 창을 열고 다음 명령 hello를 실행 합니다.
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Hello 대체 `<Git installation folder>` hello 기본값은 시스템에서 hello Git 위치와 **"C:\Program Files\Git"**합니다. 첫 번째 경로 hello의 hello 시작 부분에서 세미콜론 문자 hello note 합니다.
4. TooAzure 로그온 되어 있는지 확인 (통해 [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) toocreate 탄력적 검색 클러스터 사용 되어야 하는 hello 구독을 선택 합니다. `Get-AzureRmContext` 및 `Get-AzureRmSubscription` cmdlet를 사용하여 올바른 구독을 선택했는지 확인할 수 있습니다.
5. 아직 수행 하지 않은 경우 hello 현재 디렉터리 toohello ES MultiNode 폴더를 변경 합니다.

### <a name="run-hello-createelasticsearchcluster-script"></a>Hello CreateElasticSearchCluster 스크립트 실행
Hello 스크립트를 실행 하기 전에 hello 열고 `azuredeploy-parameters.json` 파일을 확인 하거나 hello 스크립트 매개 변수 값을 제공 합니다. hello 매개 변수 뒤에 제공 됩니다.

| 매개 변수 이름 | 설명 |
| --- | --- |
| dnsNameForLoadBalancerIP |hello 이름 (hello Azure 지역 도메인 제공 toohello 이름 추가) 하 여 hello 탄력적 검색 클러스터에 대 한 사용 되는 toocreate hello 공개적으로 표시 DNS 이름입니다. 예를 들어이 매개 변수 값은 "myBigCluster" 하는 경우 Azure 지역을 선택 하는 hello는 미국 서 부 hello hello 클러스터 결과 DNS 이름은 myBigCluster.westus.cloudapp.azure.com입니다. <br /><br />이 이름은 데이터 노드 이름 예: hello 탄력적 검색 클러스터와 연결 된 여러 아티팩트에 대 한 루트 이름으로도 사용 됩니다. |
| adminUsername |hello 탄력적 검색 클러스터를 관리 하기 위한 hello 관리자 계정의 hello 이름 (해당 SSH 키는 자동으로 생성 되며 않음). |
| dataNodeCount |hello hello 탄력적 검색 클러스터의 노드 수입니다. hello hello 스크립트의 현재 버전에서 데이터 및 쿼리 노드; 구분 하지 않습니다. 모든 노드가 두 역할을 수행 합니다. 기본값 too3 노드입니다. |
| dataDiskSize |각 데이터 노드에 대해 할당 되는 (GB)에 있는 데이터 디스크의 hello 크기입니다. 4 데이터 디스크를 단독으로 전용된 tooElastic 검색 서비스를 수신 하는 각 노드에 있습니다. |
| region |hello 이름 여기서 hello 탄력적 검색 클러스터를 배치 해야 하는 Azure 지역입니다. |
| esUserName |hello hello 사용자의 사용자 이름 구성 toohave 액세스 tooES 클러스터 (제목 tooHTTP 기본 인증). hello 암호 매개 변수 파일의 일부가 아니며 제공 해야 합니다 `CreateElasticSearchCluster` 스크립트를 호출 합니다. |
| vmSizeDataNodes |hello 탄력적 검색 클러스터 노드에 대 한 Azure 가상 컴퓨터 크기입니다. 기본값 tooStandard_D2 합니다. |

이제 준비 toorun hello 스크립트 됩니다. Hello 다음 명령을 실행 합니다.

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

여기서, 

| 매개 변수 이름 | 설명 |
| --- | --- |
| `<es-group-name>` |탄력적 검색 클러스터 리소스를 모두 포함 될 hello Azure 리소스 그룹의 hello 이름입니다. |
| `<azure-region>` |hello 이름 hello hello 탄력적 검색 클러스터를 만들 Azure 지역입니다. |
| `<es-password>` |hello 탄력적 검색 사용자에 대 한 hello 암호입니다. |

> [!NOTE]
> TooAzure에 toolog 잊은 hello 테스트 AzureResourceGroup cmdlet에서 NullReferenceException을 받아야 하는 경우 (`Add-AzureRmAccount`).
> 
> 

Hello 매개 변수 파일을 수정 hello 스크립트 실행에서 오류가 발생 하는 hello ц 잘못 된 템플릿 매개 변수 값을 판단 하는 경우에 다른 리소스 그룹 이름으로 hello 스크립트를 다시 실행 하십시오. 다시 사용할 수도 hello를 추가 하 여 hello 스크립트 이전과 hello 정리 했으며 동일한 리소스 그룹 이름 hello `-RemoveExistingResourceGroup` toohello 매개 변수에서의 스크립트 호출 합니다.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Hello CreateElasticSearchCluster 스크립트 실행의 결과
Hello를 실행 한 후 `CreateElasticSearchCluster` 스크립트를 다음 주 아티팩트 hello 생성 됩니다. 이 예에서는 "myBigCluster" hello의 hello 값으로 사용 했다고 가정 `dnsNameForLoadBalancerIP` 매개 변수 및 해당 hello 지역 hello 클러스터를 만들 위치는 West US입니다.

| 아티팩트 | 이름, 위치 및 설명 |
| --- | --- |
| 원격 관리를 위한 SSH 키 |myBigCluster.key 파일 (hello는 hello CreateElasticSearchCluster가 실행 디렉터리에에서). <br /><br />이 키 파일에 사용 되는 tooconnect toohello 관리 노드일 수 있습니다 (관리자 노드를 hello)를 통해 및 hello 클러스터의 toodata 노드. |
| 관리 노드 |myBigCluster-admin.westus.cloudapp.azure.com  <br /><br />외부 SSH 연결을 허용 하는 원격 Elasticsearch 클러스터 관리-하나만 hello에 대 한 전용된 VM입니다. 모든 Elasticsearch 서비스를 실행 하지 않는 모든 hello Elasticsearch 클러스터 않지만와 동일한 가상 네트워크 hello 실행 됩니다. |
| 데이터 노드 |myBigCluster1 … myBigCluster*N* <br /><br />Elasticsearch 및 Kibana 서비스를 실행하는 데이터 노드입니다. SSH tooeach 노드를 통해 하지만 hello 관리자 노드를 통해서만 연결할 수 있습니다. |
| Elasticsearch 클러스터 |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />hello hello Elasticsearch 클러스터 (참고 hello /es 접미사)에 대 한 기본 끝점입니다. 기본 HTTP 인증으로 보호 됩니다 (hello 자격 증명의 hello ES MultiNode 템플릿의 esUserName/esPassword 매개 변수를 지정 하는 hello 때문). 기본 클러스터 관리에 대 한 hello 클러스터에 hello h e a d 플러그 인 설치 (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head)도 있습니다. |
| Kibana 서비스 |http://myBigCluster.westus.cloudapp.azure.com <br /><br />hello Kibana 서비스에서 Elasticsearch 클러스터를 만든 hello tooshow 데이터 설정 되어 있습니다. Hello로 보호 됩니다 hello와 같은 인증 자격 증명 자체를 클러스터 합니다. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>In-proces와 out-of-process 추적 캡처 비교
진단 데이터 수집의 두 가지 기본 방법의 hello 소개에서에서 설명한: in-process 및 out-of-process-합니다. 각각은 강점 및 약점이 있습니다.

Hello의 장점 **프로세스 추적 캡처** 포함:

1. *쉬운 구성 및 배포*
   
   * 진단 데이터 수집의 hello 구성은 hello 응용 프로그램 구성의 일부입니다. 것 hello 응용 프로그램의 놓을 것 "동기화" hello로 쉽게 tooalways 유지 합니다.
   * 응용 프로그램당 또는 서비스당 구성은 쉽게 달성할 수 있습니다.
   * 작업 중이 아닌 추적에서 캡처에 별도 배포 및 구성을 추가 관리 작업 및 오류의 잠재적 소스 hello 진단 에이전트의 일반적으로 필요 합니다. hello 에이전트에 따라 기술에는 종종 hello 에이전트 당 가상 컴퓨터 (노드)의 인스턴스가 하나만 있습니다. 즉, 해당 구성을 hello 컬렉션 hello 진단 구성의 모든 응용 프로그램 간에 공유 되 고 해당 노드에서 실행 되는 서비스.
2. *유연성*
   
   * hello 응용 프로그램 데이터 보낼 수 있습니다 hello toogo, 필요한 경우 항상으로 hello 대상 데이터 저장소 시스템을 지 원하는 수 있는 클라이언트 라이브러리입니다. 새로운 싱크를 원하는 대로 추가할 수 있습니다.
   * 복잡한 캡처, 필터링 및 데이터 집계 규칙을 구현할 수 있습니다.
   * 캡처하는 작업 중이 아닌 추적 에이전트 지원 hello hello 데이터 싱크에 종종 제한 됩니다. 일부 에이전트는 확장할 수 있습니다.
3. *액세스 toointernal 응용 프로그램 데이터와 컨텍스트*
   
   * hello 진단 하위 시스템 hello 응용 프로그램/서비스 프로세스 내에서 실행 컨텍스트 정보를 사용 하 여 hello 추적을 쉽게 강화할 수 있습니다.
   * Hello 작업 중이 아닌 경우에서 hello 데이터 전송 해야 tooan 에이전트 일부 프로세스 간 통신 메커니즘을 통해 Windows 용 이벤트 추적 등입니다. 이 메커니즘에 따라 추가 제한 사항이 적용될 수 있습니다.

Hello의 장점 **out-of-process-추적 캡처** 포함:

1. *크래시 덤프를 수집 하 고 hello 기능 toomonitor hello 응용 프로그램*
   
   * 캡처 프로세스에서 추적 실패할 수 있습니다 hello 응용 프로그램 toostart 못하거나가 충돌 합니다. 독립 에이전트는 중요한 문제 해결 정보를 캡처할 가능성이 훨씬 큽니다.<br /><br />
2. *완성도, 견고성 및 검증된 성능*
   
   * 에이전트 (예: Microsoft Azure 진단 에이전트가) 플랫폼 공급 업체에서 개발 된 주체 toorigorous 테스트 및 전투 강화 되었습니다.
   * 캡처 프로세스에서 추적을으로 주의 해야 tooensure 응용 프로그램 프로세스에서 진단 데이터를 보내는 hello 활동 hello 응용 프로그램의 주요 작업에 방해가 하거나 타이밍 또는 성능 문제가 발생 하지 않습니다. 독립적으로 실행 중인 에이전트 발생할 가능성이 적으므로 toothese 문제 이며 특별히 디자인 된 toolimit hello 시스템에 미치는 영향입니다.

두 방법 중 하나를 혜택 및 가능한 toocombine 않습니다. 실제로 대부분의 응용 프로그램에 대 한 최상의 솔루션 hello 수도 있습니다.

여기서 hello 사용 **Microsoft.Diagnostic.Listeners 라이브러리** 및 서비스 패브릭 응용 프로그램 tooan Elasticsearch 클러스터에서 toosend 데이터 캡처 hello 프로세스에서 추적 합니다.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Hello 수신기 라이브러리 toosend tooElasticsearch 진단 데이터를 사용 하 여
hello Microsoft.Diagnostic.Listeners 라이브러리는 PartyCluster 샘플 서비스 패브릭 응용 프로그램의 일부입니다. toouse 하기:

1. 다운로드 [hello PartyCluster 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) GitHub에서 합니다.
2. Hello Microsoft.Diagnostics.Listeners 및 Microsoft.Diagnostics.Listeners.Fabric 프로젝트 (전체 폴더) hello PartyCluster 샘플 디렉터리 toohello 솔루션의 폴더에서 복사 toosend hello 데이터 tooElasticsearch 되어 있는 hello 응용 프로그램 .
3. Hello 대상 솔루션을 열고 hello 솔루션 탐색기에서에서 hello 솔루션 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **기존 프로젝트 추가**합니다. Hello Microsoft.Diagnostics.Listeners 프로젝트 toohello 솔루션을 추가 합니다. 반복을 hello hello Microsoft.Diagnostics.Listeners.Fabric 프로젝트에 대해 동일 합니다.
4. 서비스는 프로젝트가 toohello 두 개의 추가 된 프로젝트에서 프로젝트 참조를 추가 합니다. (Toosend 데이터 tooElasticsearch 되어 있는 각 서비스를 참조 해야 Microsoft.Diagnostics.EventListeners 및 Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![프로젝트에서 tooMicrosoft.Diagnostics.EventListeners 및 Microsoft.Diagnostics.EventListeners.Fabric 라이브러리 참조][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>서비스 패브릭 일반 공급 릴리스 및 Microsoft.Diagnostics.Tracing Nuget 패키지
서비스 패브릭 일반 공급 릴리스(2.0.135, 2016년 3월 31일 출시)를 사용하여 빌드한 응용 프로그램은 **.NET Framework 4.5.2**를 대상으로 합니다. 이 버전에는 hello hello GA 릴리스의 hello 시 Azure에서 지 원하는.NET Framework의 hello 가장 높은 버전이입니다. 그러나이 버전의 hello framework 특정 EventListener Api 해당 hello 라이브러리가 Microsoft.Diagnostics.Listeners에 부족 합니다. EventSource (패브릭 응용 프로그램에서 Api 로깅 hello 기본을 형성 하는 hello 구성) 및 EventListener 밀접 하 게 결합 된 hello Microsoft.Diagnostics.Listeners 라이브러리를 사용 하는 모든 프로젝트의 대체 구현을 사용 해야 EventSource 합니다. 이 구현 hello **Microsoft.Diagnostics.Tracing Nuget 패키지**, Microsoft에서 작성 합니다. hello 패키지에에서 포함 되어 있으면 hello 프레임 워크 코드 변경 없이 참조 네임 스페이스 변경 외 필요가 EventSource와 완벽 하 게 이전 버전과 호환은입니다.

toostart toosend 데이터 tooElasticsearch 필요한 각 서비스 프로젝트에 대해 다음이 단계를 수행 hello Microsoft.Diagnostics.Tracing 구현의 hello EventSource 클래스를 사용 하 여:

1. Hello 서비스 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **Nuget 패키지 관리**합니다.
2. (선택 되지 않은 이미) 하는 경우 toohello nuget.org 패키지 원본 및 검색에 대 한 전환 "**Microsoft.Diagnostics.Tracing**"입니다.
3. Hello 설치 `Microsoft.Diagnostics.Tracing.EventSource` 패키지 (및 해당 종속성).
4. 열기 hello **ServiceEventSource.cs** 또는 **ActorEventSource.cs** 서비스 프로젝트에서 파일 및 hello 바꾸기 `using System.Diagnostics.Tracing` hello로 hello 파일 맨 위에 지시문 `using Microsoft.Diagnostics.Tracing` 지시문입니다.

이러한 단계는 필요한 됩니다 한 번 hello **.NET Framework 4.6** Microsoft Azure에서 지원 합니다.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Elasticsearch 수신기 인스턴스화 및 구성
hello tooElasticsearch 진단 데이터를 보내기 위한 마지막 단계 toocreate의 인스턴스가 `ElasticSearchListener` 고 Elasticsearch 연결 데이터를 구성 합니다. hello 수신기는 자동으로 hello 서비스 프로젝트에 정의 된 EventSource 클래스를 통해 발생 하는 모든 이벤트를 캡처합니다. 필요한 toobe hello 서비스의 hello 수명 동안 활성 상태로 hello 최상의 toocreate hello 서비스 초기화 코드에 배치 합니다. 상태 비저장 서비스에 대 한 hello 초기화 코드 hello 필요한 변경 된 후 방식을 보여 줍니다 다음과 같습니다 (추가부터 시작 하는 주석에서 지적 `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Elasticsearch 연결 데이터 hello 서비스 구성 파일에서 별도 섹션에 저장 되어야 합니다 (**PackageRoot\Config\Settings.xml**). hello 섹션의 hello 이름 toohello 전달 된 값이 toohello 일치 해야 `FabricConfigurationProvider` 생성자 예:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
값을 hello `serviceUri`, `userName` 및 `password` 매개 변수 toohello Elasticsearch 클러스터 끝점 주소, Elasticsearch 사용자 이름 및 암호를 해당 각각. `indexNamePrefix`Elasticsearch 인덱스;에 대 한 hello 접두사 hello Microsoft.Diagnostics.Listeners 라이브러리는 매일의 데이터에 대 한 새 인덱스를 만듭니다.

### <a name="verification"></a>확인
이것으로 끝입니다. 이제 hello 서비스가 실행 될 때마다 시작 hello 구성에 지정 된 추적 toohello Elasticsearch 서비스를 전송 합니다. Opening hello Kibana UI hello 대상 Elasticsearch 인스턴스와 연관 하 여이 확인할 수 있습니다. 예에서 hello 페이지 주소 http://myBigCluster.westus.cloudapp.azure.com/는입니다. Hello에 대 한 선택 hello 이름 접두사를 사용 하 여 인덱스 검사 `ElasticSearchListener` 인스턴스 실제로 생성 되어 데이터로 채워집니다.

![PartyCluster 응용 프로그램 이벤트를 보여 주는 Kibana][2]

## <a name="next-steps"></a>다음 단계
* [서비스 패브릭 서비스 진단 및 모니터링에 대한 자세한 정보](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
