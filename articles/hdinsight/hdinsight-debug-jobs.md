---
title: "HDInsight에서 Hadoop 디버그: 로그 보기 및 오류 메시지 해석 - Azure | Microsoft Docs"
description: "HDInsight PowerShell 및 toorecover 수행할 수 있는 단계를 사용 하 여 관리 하는 경우 표시 될 수 있습니다 hello 오류 메시지에 알아봅니다."
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>HDInsight 로그 분석
Azure HDInsight의 Hadoop 클러스터 각 hello 기본 파일 시스템으로 사용 되는 Azure 저장소 계정을 있습니다. hello 저장소 계정 기본 저장소 계정 hello 라고 합니다. 클러스터 로그 사용 하 여 hello Azure 테이블 저장소 및 Blob 저장소 hello hello 기본 저장소 계정 toostore에 해당 합니다.  클러스터에 대 한 기본 저장소 계정을 hello toofind 참조 [HDInsight 클러스터를 관리 하는 Hadoop](hdinsight-administer-use-management-portal.md#find-the-default-storage-account)합니다. hello 로그 hello 클러스터를 삭제 한 후에 hello 저장소 계정에에서 유지 합니다.

## <a name="logs-written-tooazure-tables"></a>로그를 기록 tooAzure 테이블
hello 로그를 기록 tooAzure 테이블 한 수준의 제공할 HDInsight 클러스터와 발생 하는 작업에 대 한 정보입니다.

HDInsight 클러스터를 만들 때 6 테이블 Linux 기반 클러스터용으로 hello 기본 테이블 저장소에 자동으로 생성 됩니다.

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

Windows 기반 클러스터에 3개의 테이블을 만듭니다.

* setuplog: HDInsight 클러스터를 프로비전/설정할 때 발생한 이벤트/예외의 로그입니다.
* hadoopinstalllog: 로그의 이벤트/예외 hello 클러스터에서 Hadoop을 설치할 때 발생 합니다. 이 테이블 문제를 디버깅 하는 데 유용 관련 사용자 지정 매개 변수를 사용 하 여 만든 tooclusters 합니다.
* hadoopservicelog: 모든 Hadoop 서비스에 의해 기록된 이벤트/예외의 로그입니다. 이 테이블 문제 관련된 toojob 오류 HDInsight 클러스터에서 디버깅에 유용 합니다.

hello 테이블 파일 이름에는 **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**합니다.

이러한 테이블 hello를 다음 필드가 포함 되어 있습니다.

* ClusterDnsName
* ComponentName
* EventTimestamp
* 호스트
* MALoggingHash
* Message
* N
* PreciseTimeStamp
* 역할
* RowIndex
* 테넌트
* TIMESTAMP
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Hello 로그에 액세스 하기 위한 도구
이 테이블의 데이터에 액세스하기 위해 사용할 수 있는 여러 도구가 있습니다.

* Visual Studio
* Azure 저장소 탐색기
* Excel용 파워 쿼리

#### <a name="use-power-query-for-excel"></a>Excel용 파워 쿼리 사용
파워 쿼리는 [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379)에서 설치될 수 있습니다. Hello 다운로드 hello 시스템 요구 사항에 대 한 페이지를 참조 하십시오.

**파워 쿼리 tooopen toouse hello 서비스 로그를 분석 하 고**

1. **Microsoft Excel**을 엽니다.
2. Hello에서 **파워 쿼리** 메뉴를 클릭 하 여 **에서 Azure**, 클릭 하 고 **에서 Microsoft Azure 테이블 저장소**합니다.
   
    ![HDInsight Hadoop Excel 파워 쿼리는 Azure 테이블 저장소를 엽니다](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Hello 저장소 계정 이름을 입력 합니다. 이 hello 짧은 이름 또는 FQDN hello 수 있습니다.
4. Hello 저장소 계정 키를 입력 합니다. 테이블의 목록이 표시됩니다.
   
    ![Azure 테이블 저장소에 저장된 HDInsight Hadoop 로그](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Hello에 hello hadoopservicelog 테이블을 마우스 오른쪽 단추로 클릭 **탐색기** 창과 선택 **편집**합니다. 4개의 열이 표시됩니다. 필요에 따라 hello 삭제 **파티션 키**, **행 키**, 및 **타임 스탬프** 열을 선택한 다음 클릭 하 여 **열 제거** hello 리본에 hello 옵션입니다.
6. Hello 클릭 hello에 아이콘을 확장 tooimport hello Excel 스프레드시트에 원하는 열 toochoose hello 열 내용입니다. 이 데모에서 TraceLevel 및 ComponentName을 선택한 경우 문제가 있는 구성 요소에 대한 일부 기본 정보를 줄 수 있습니다.
   
    ![HDInsight Hadoop 로그는 열을 선택합니다](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. 클릭 **확인** tooimport hello 데이터입니다.
8. 선택 hello **TraceLevel**, 역할 및 **ComponentName** 열 및 클릭 **Group By** hello 리본 메뉴의 컨트롤입니다.
9. 클릭 **확인** hello Group By 대화 상자
10. ** 적용 및 닫기**를 클릭합니다.

필요에 따라 Excel toofilter 및 정렬을 사용할 수 있습니다. 물론, 할 수 있습니다 tooinclude 순서 toodrill 아래쪽에 있는 다른 열 (예: 메시지)에 문제가 발생 하지만 선택 하 여 위에서 설명한 hello 열 그룹화의 Hadoop 서비스와 상황에 대 한 훌륭한 그림을 제공 하는 경우. hello 동일한 개념 수 적용된 toohello setuplog 및 hadoopinstalllog 테이블.

#### <a name="use-visual-studio"></a>Visual Studio 사용
**Visual Studio toouse**

1. Visual Studio를 엽니다.
2. Hello에서 **보기** 메뉴를 클릭 하 여 **클라우드 탐색기**합니다. 또는 **CTRL+\, CTRL+X**를 클릭하면 됩니다.
3. **클라우드 탐색기**에서 **리소스 유형**을 선택합니다.  hello 사용 가능한 다른 옵션은 **리소스 그룹**합니다.
4. 확장 **저장소 계정은**, 클러스터에 대 한 기본 저장소 계정 hello 차례로 **테이블**합니다.
5. **hadoopservicelog**를 두 번 클릭합니다.
6. 필터를 추가합니다. 예:
   
        TraceLevel eq 'ERROR'
   
    ![HDInsight Hadoop 로그는 열을 선택합니다](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    필터를 생성 하는 방법에 대 한 자세한 내용은 참조 [hello 테이블 디자이너에 대 한 필터 문자열 생성](../vs-azure-tools-table-designer-construct-filter-strings.md)합니다.

## <a name="logs-written-tooazure-blob-storage"></a>로그 쓰기 tooAzure Blob 저장소
[서 면된 tooAzure 테이블을 기록 하는 hello](#log-written-to-azure-tables) 한 수준의 HDInsight 클러스터와 발생 하는 작업에 대 한 정보를 제공 합니다. 그러나 이러한 테이블은 문제 발생 시에 추가 드릴에 도움이 될 수 있는 작업 수준의 로그를 제공하지 않습니다. tooprovide이 다음 수준의 세부 정보를 HDInsight 클러스터는 Templeton을 통해 전송 된 모든 작업에 대 한 toowrite 작업 로그 tooyour Blob 저장소 계정 구성. 실제로,이 작업 hello Microsoft Azure PowerShell cmdlet 또는.NET 작업 전송 Api를 통해 RDP/명령줄 액세스 toohello 클러스터 제출 하는 작업 하지 hello를 사용 하 여 전송할 것을 의미 합니다. 

tooview hello 로그 참조 [Linux 기반 HDInsight에 대 한 액세스 YARN 응용 프로그램 로그](hdinsight-hadoop-access-yarn-app-logs-linux.md)합니다.

응용 프로그램 로그에 대한 자세한 내용은 [YARN에서 사용자 로그 관리 및 액세스 단순화](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/)를 참조하세요.

## <a name="view-cluster-health-and-job-logs"></a>클러스터 상태 및 작업 로그 보기
### <a name="access-hadoop-ui"></a>Hadoop UI에 액세스
Hello Azure 포털에서에서 HDInsight 클러스터 이름을 tooopen hello 클러스터 블레이드를 클릭 합니다. Hello 클러스터 블레이드에서 클릭 **대시보드**합니다.

![클러스터 대시보드 시작](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

메시지가 표시 되 면 hello 클러스터 관리자 자격 증명을 입력 합니다. Hello 열리는 쿼리 콘솔에서에서 클릭 **Hadoop UI**합니다.

![Hadoop UI 시작](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Hello Yarn UI에 액세스
Hello Azure 포털에서에서 HDInsight 클러스터 이름을 tooopen hello 클러스터 블레이드를 클릭 합니다. Hello 클러스터 블레이드에서 클릭 **대시보드**합니다. 메시지가 표시 되 면 hello 클러스터 관리자 자격 증명을 입력 합니다. Hello 열리는 쿼리 콘솔에서에서 클릭 **YARN UI**합니다.

Hello YARN UI toodo hello 다음을 사용할 수 있습니다.

* **클러스터 상태를 가져옵니다**. Hello 왼쪽된 창에서 확장 **클러스터**를 클릭 하 고 **에 대 한**합니다. 이 현재 클러스터 총 할당 된 메모리, 코어를 사용 하는 hello 클러스터 리소스 관리자의 상태와 같은 상태 세부 정보, 클러스터 버전 등입니다.
  
    ![클러스터 대시보드 시작](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **노드 상태를 가져옵니다**. Hello 왼쪽된 창에서 확장 **클러스터**를 클릭 하 고 **노드**합니다. 이 모든 hello 노드 hello 클러스터, 각 노드, 리소스 할당 된 tooeach 노드 등의 HTTP 주소를 나열 합니다.
* **작업 상태를 모니터링**합니다. Hello 왼쪽된 창에서 확장 **클러스터**, 클릭 하 고 **응용 프로그램** toolist 모든 hello hello 클러스터에서 작업 합니다. 특정에서 작업에 toolook 하려는 경우 아래의 hello 적절 한 링크를 클릭 하는 상태 (예: 새 전송된, 실행, 등) **응용 프로그램**합니다. 추가로 hello 작업 이름 toofind hello 출력, 로그, 등을 비롯 하 여 이러한 hello 작업에 대 한 자세한 내용을 클릭할 수 있습니다.

### <a name="access-hello-hbase-ui"></a>Hello HBase UI에 액세스
Hello Azure 포털에서에서 HDInsight HBase 클러스터 이름 tooopen hello 클러스터 블레이드를 클릭 합니다. Hello 클러스터 블레이드에서 클릭 **대시보드**합니다. 메시지가 표시 되 면 hello 클러스터 관리자 자격 증명을 입력 합니다. Hello 열리는 쿼리 콘솔에서에서 클릭 **HBase UI**합니다.

## <a name="hdinsight-error-codes"></a>HDInsight 오류 코드
hello 오류 메시지가이 섹션에 항목별로 제공 되며 Azure HDInsight에서 Hadoop의 toohelp hello 사용자가 Azure PowerShell을 tooadvise를 사용 하 여 hello 서비스를 관리 하는 경우에 도달할 수 있는 가능한 오류 조건을 이해 hello 단계에서 toorecover hello 오류에서 수행할 수 있는 합니다.

이러한 오류 메시지의 일부도 볼 수 있습니다 hello Azure 포털에서에서 HDInsight 클러스터에 사용 되는 toomanage 되었을 때. 하지만 발생할 수 있는 다른 오류 메시지는 덜 세분화 된 hello 조치 가능한이 컨텍스트에 대 한 toohello 제약 조건 때문입니다. 다른 오류 메시지는 hello 완화는 확실 한 hello 컨텍스트에서만에서 제공 됩니다. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **설명**: 하십시오 순서 toouse에 적어도 하나의 구성 요소에 대 한 Azure SQL 데이터베이스 정보를 Hive 및 Oozie metastore의 사용자 지정 설정을 제공 합니다.
* **완화**: hello 사용자 toosupply 유효한 SQL Azure metastore, 다시 시도 hello 요청이 필요 합니다.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **설명**: *nameOfYourRegion*지역에서 클러스터를 만들 수 없습니다. 올바른 HDInsight 지역을 사용하여 요청을 다시 시도하세요.
* **완화**: 고객 현재 지 원하는 hello 클러스터 지역 만들어야: 동남 아시아, 서 부 유럽, 유럽 북부, 미국 동부 또는 미국 서 부 합니다.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **설명**: hello 서버를 찾을 수 없습니다 hello 클러스터 레코드를 요청 합니다.  
* **완화**: hello 작업을 다시 시도 합니다.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **설명**: *yourDnsName* 클러스터 DNS 이름이 잘못되었습니다. 이름이 영숫자로 시작하고 끝나는지 확인하세요. 이름에는 '-' 특수 문자만 포함할 수 있습니다.  
* **완화**: hello 대시 아닌 다른 클러스터 시작 하 고 영숫자로 끝나는 포함 특수 문자에 대 한 올바른 DNS 이름이 사용 되도록 '-' hello 작업을 다시 시도 합니다.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **설명**: *yourClusterName* 클러스터 이름을 사용할 수 없습니다. 다른 이름을 선택하세요.  
* **완화**: hello 사용자 해야 고유한 clustername 지정 및 않습니다 하지 존재 하 고 다시 시도 하십시오. Hello 사용자 포털 hello를 사용 하는 경우 UI는 알리는 hello 하는 동안 클러스터 이름이 이미 사용 중인 경우 hello 단계를 만듭니다.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **설명**: 클러스터 암호가 잘못되었습니다. 암호 숫자, 대문자, 소문자 및 공백 없이 특수 문자를 포함 해야 및 hello 사용자 이름에 포함 되 면 안 최소 10 자 여야 합니다.  
* **완화**: 유효한 클러스터 암호를 제공 하 고 hello 작업을 다시 시도 합니다.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **설명**: 클러스터 사용자 이름이 잘못되었습니다. 사용자 이름에 특수 문자 또는 공백이 포함되지 않았는지 확인하세요.  
* **완화**: 유효한 클러스터 사용자 이름을 제공 하 고 hello 작업을 다시 시도 합니다.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **설명**: *yourDnsClusterName* 클러스터 DNS 이름이 잘못되었습니다. 이름이 영숫자로 시작하고 끝나는지 확인하세요. 이름에는 '-' 특수 문자만 포함할 수 있습니다.  
* **완화**: 유효한 DNS 클러스터 사용자 이름을 제공 하 고 hello 작업을 다시 시도 합니다.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **설명**: 컨테이너 이름 URI에 *yourcontainerURI* 및 DNS 이름을 *yourDnsName* 요청에서 본문 해야 수 hello 동일 합니다.  
* **완화**: 컨테이너 이름 및 DNS 이름을 동일 hello 되 고 hello 작업을 다시 시도 있는지 확인 합니다.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **설명**: 클러스터 구성이 잘못되었습니다. Toofind 수 없습니다 노드 크기에서 모든 데이터 노드 정의 합니다.  
* **완화**: hello 작업을 다시 시도 합니다.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **설명**: hello 클러스터에 대 한 배포를 삭제 하지 못했습니다.  
* **완화**: hello 삭제 작업을 다시 시도 하십시오.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **설명**: 서비스 구성 오류입니다. 필수 DNS 매핑 정보를 찾지 못했습니다.  
* **해결 방법**: 클러스터를 삭제하고 새 클러스터를 만드세요.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **설명**: 클러스터 컨테이너 만들기 시도가 중복되었습니다. *컨테이너이름* 의 레코드가 존재하지만 Etags가 일치하지 않습니다.
* **완화**: hello 컨테이너와 재시도 hello 만들기 작업에 대 한 고유 이름을 제공 합니다.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **설명**: 호스티드 서비스 *nameOfYourHostedService* 에 이미 클러스터가 포함되어 있습니다. 호스티드 서비스에는 여러 클러스터를 포함할 수 없습니다.  
* **완화**: 다른 호스트 hello 클러스터 호스 티 드 서비스입니다.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **설명**: hello 서버 hello 클러스터 배포의 hello 상태를 업데이트할 수 없습니다.  
* **완화**: hello 작업을 다시 시도 합니다. 이 오류가 여러 번 발생하는 경우 CSS에 문의하세요.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **설명**: *yourClusterName* 클러스터가 유지 관리 과정에서 삭제되었습니다. Hello 클러스터를 다시 만드십시오.
* **완화**: hello 클러스터 다시 만들기.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **설명**: 클러스터 구성이 잘못되었습니다. 노드 크기에서 필수 헤드 노드 구성을 찾을 수 없습니다.
* **완화**: hello 작업을 다시 시도 합니다.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **설명**: 수 없습니다 toocreate 호스 티 드 서비스 *nameOfYourHostedService*합니다. 요청을 다시 시도하세요.  
* **완화**: hello 요청을 다시 시도 합니다.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **설명**: 호스티드 서비스 *nameOfYourHostedService* 에 이미 프로덕션 배포가 있습니다. 호스티드 서비스에는 여러 프로덕션 배포를 포함할 수 없습니다. 다른 클러스터 이름을 사용 하 여 hello 요청을 다시 시도 하십시오.
* **완화**: 다른 클러스터 이름을 사용 하 고 hello 요청을 다시 시도 합니다.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **설명**: 호스 티 드 서비스 *nameOfYourHostedService* 을 hello 클러스터를 찾을 수 없습니다.  
* **완화**: hello 클러스터 오류 상태에 있으면 삭제 한 후 다시 시도 하십시오.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **설명**: *nameOfYourHostedService* 호스티드 서비스에 연결된 배포가 없습니다.  
* **완화**: hello 클러스터 오류 상태에 있으면 삭제 한 후 다시 시도 하십시오.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **설명**: SubscriptionId hello *yourSubscriptionId* 코어 왼쪽된 toocreate 클러스터 없는 *yourClusterName*합니다. 필수: *resourcesRequired*, 사용 가능: *resourcesAvailable*.  
* **완화**: 구독에서 리소스를 확보 hello 리소스 사용 가능한 toohello 구독 늘린 toocreate hello 클러스터를 다시 시도 하십시오.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **설명**: 구독 ID *yourSubscriptionId* 새 HostedService toocreate 클러스터에 대 한 할당량이 없는 *yourClusterName*합니다.  
* **완화**: 구독에서 리소스를 확보 hello 리소스 사용 가능한 toohello 구독 늘린 toocreate hello 클러스터를 다시 시도 하십시오.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **설명**: hello 서버에 내부 오류가 발생 했습니다. 요청을 다시 시도하세요.  
* **완화**: hello 요청을 다시 시도 합니다.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **설명**: Azure 저장소 위치인 *dataRegionName* 이(가) 올바른 위치가 아닙니다. Hello 영역 올바른지 확인 하 고 요청을 다시 시도 하십시오.
* **완화**: HDInsight를 지 원하는 저장소 위치를 선택 하 고 같은 위치에 배치 클러스터 인지 확인 hello 작업을 다시 시도 합니다.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **설명**: 데이터 노드의 VM 크기가 잘못되었습니다. '모든 데이터 노드에서 큰 VM' 크기만 지원됩니다.  
* **완화**: hello 데이터 노드에 대 한 지원 hello 노드 크기를 지정 하 고 hello 작업을 다시 시도 합니다.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **설명**: 헤드 노드의 VM 크기가 잘못되었습니다. 헤드 노드에서는 '매우 큰 VM' 크기만 지원됩니다.  
* **완화**: hello 헤드 노드에 대 한 지원 hello 노드 크기를 지정 하 고 hello 작업을 다시 시도

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **설명**: 구독 ID *yourSubscriptionId* 사용 중인 없는 클러스터에 대 한 충분 한 사용 권한을 tooexecute 삭제 작업이 *yourClusterName*합니다.  
* **완화**: hello 클러스터 오류 상태에 있으면 삭제 한 후 다시 시도 하십시오.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **설명**: 외부 저장소 계정 blob 컨테이너 이름 *yourContainerName* 이(가) 잘못되었습니다. 이름이 문자로 시작되며 이름에 소문자, 숫자 및 대시만 포함되어 있는지 확인하세요.  
* **완화**: 유효한 저장소 계정 blob 컨테이너 이름을 지정 하 고 hello 작업을 다시 시도 합니다.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **설명**: 외부 저장소 계정에 대 한 구성을 *yourStorageAccountName* 필요한 toohave 비밀 키 정보는 toobe 집합입니다.  
* **완화**: hello 저장소 계정에 대 한 유효한 비밀 키를 지정 하 고 hello 작업을 다시 시도 합니다.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **설명**: 버전 헤더 *yourVersionHeader* 이(가) 올바른 형식(yyyy-mm-dd)이 아닙니다.  
* **완화**: hello 버전 헤더에 대 한 올바른 형식 지정 및 hello 요청을 다시 시도 합니다.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **설명**: 클러스터 구성이 잘못되었습니다. 헤드 노드 구성이 두 개 이상 검색되었습니다.  
* **완화**: 편집 hello 구성 한 헤드 노드만 지정 되도록 합니다.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **설명**: hello 최대 다시 시도 가능한 또는 hello 허용 시간 안에 hello 작업을 완료할 수 없습니다. 요청을 다시 시도하세요.  
* **완화**: hello 요청을 다시 시도 합니다.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **설명**: *yourParameterName* 매개 변수는 Null이거나 비워 둘 수 없습니다.  
* **완화**: hello 매개 변수에 대 한 올바른 값을 지정 합니다.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **설명**: hello 클러스터 만들기 요청 입력 중 하나 이상이 올바르지 않습니다. 입력된 값 hello 올바른지, 그리고 요청을 다시 시도 있는지 확인 합니다.  
* **완화**: hello 입력된 값이 올바른지 한 요청을 다시 시도 하십시오.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **설명**: *yourRegionName* 지역 및 *yourSubscriptionId* 구독 ID에서 사용할 수 없는 지역 정보 값입니다.  
* **해결 방법**: HDInsight 클러스터를 지원하는 지역을 지정하세요. 공개적으로 지원 되는 hello 영역은: 동남 아시아, 서 부 유럽, 유럽 북부, 미국 동부 또는 미국 서 부 합니다.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **설명**: *yourStorageAccountName* 저장소 계정이 *currentRegionName* 지역에 있습니다. Hello 클러스터 지역과 동일 해야 *yourClusterRegionName*합니다.  
* **완화**: 저장소 계정을 지정 하거나 hello 클러스터가 동일한 지역 또는 데이터 hello 저장소 계정에 이미 있으면 hello에 새 클러스터를 만들 hello 기존 저장소 계정과 동일한 지역입니다. Hello 포털을 사용 하는 경우 hello UI는 알려 서이 문제의 미리 합니다.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **설명**: 지정된 구독 ID *yourSubscriptionId* 이(가) 활성이 아닙니다.  
* **해결 방법**: 구독을 다시 활성화하거나 올바른 새 구독을 가져오세요.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **설명**: 구독 ID인 *yourSubscriptionId* 을(를) 찾을 수 없습니다.  
* **완화**: 구독 ID가 유효한 지 확인 하 고 hello 작업을 다시 시도 합니다.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **설명**: 수 없습니다 tooresolve DNS *yourDnsUrl*합니다. Hello blob 끝점 제공에 대 한 hello 정규화 된 URL을 확인 하십시오.  
* **해결 방법**: 올바른 Blob URL을 제공하세요. URL 해야 하는 hello 수 완벽 하 게 유효한로 시작 하는 포함 하 여 *http://* 와 끝 *.com*합니다.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **설명**: 리소스의 수 없습니다 tooverify 위치 *yourDnsUrl*합니다. Hello blob 끝점 제공에 대 한 hello 정규화 된 URL을 확인 하십시오.  
* **해결 방법**: 올바른 Blob URL을 제공하세요. URL 해야 하는 hello 수 완벽 하 게 유효한로 시작 하는 포함 하 여 *http://* 와 끝 *.com*합니다.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **설명**: *specifiedVersion* 버전 및 *yourSubscriptionId* 구독 ID에서 사용할 수 없는 버전 정보 값입니다.  
* **완화**: 사용할 수 있는 버전을 선택 하 고 hello 작업을 다시 시도 합니다.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **설명**: *specifiedVersion* 버전은 지원되지 않습니다.
* **완화**: 지원 되는 버전을 선택 하 고 hello 작업을 다시 시도 합니다.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **설명**: *specifiedVersion* 버전은 *specifiedRegion* Azure 지역에서 사용할 수 없습니다.  
* **완화**: 지정 된 hello 영역에서 지원 되는 버전을 선택 하 고 hello 작업을 다시 시도 합니다.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **설명**: 클러스터 구성이 잘못되었습니다. 필수 WASB 계정 구성을 외부 계정에서 찾을 수 없습니다.  
* **완화**: hello 계정 있고 제대로 구성 및 다시 시도 hello 작업에 지정 되어 있는지 확인 하십시오.

## <a name="next-steps"></a>다음 단계
* [Ambari 뷰 toodebug Tez 작업을 사용 하 여 HDInsight의](hdinsight-debug-ambari-tez-view.md)
* [Linux 기반 HDInsight에서 Hadoop 서비스에 힙 덤프 사용](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Hello Ambari 웹 UI를 사용 하 여 HDInsight 클러스터를 관리 합니다.](hdinsight-hadoop-manage-ambari.md)

