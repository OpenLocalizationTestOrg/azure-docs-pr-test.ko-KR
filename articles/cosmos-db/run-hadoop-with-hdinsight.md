---
title: "Hadoop aaaRun Azure Cosmos DB 및 HDInsight를 사용 하 여 작업 | Microsoft Docs"
description: "Cosmos DB Azure 및 Azure HDInsight toorun 간단한 Hive, Pig 및 MapReduce 작업 하는 방법에 대해 알아봅니다."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Azure Cosmos DB 및 HDInsight를 사용하여 Apache Hive, Pig 또는 Hadoop 작업 실행
이 자습서에서는 어떻게 toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], 및 [Apache Hadoop] [ apache-hadoop] Cosmos DB Hadoop 커넥터와 함께 Azure HDInsight의 MapReduce 작업 합니다. Cosmos DB의 Hadoop 커넥터는 소스 및 Hive, Pig 및 MapReduce 작업에 대 한 싱크 Cosmos DB tooact을 수 있습니다. 이 자습서는 Hadoop 작업에 대 한 hello 데이터 원본 및 대상으로 Cosmos DB를 사용 합니다.

이 자습서를 완료 하면 다음 질문 수 tooanswer hello 수 있습니다.

* Hive, Pig 또는 MapReduce 작업을 사용하여 Cosmos DB에서 데이터를 로드하려면 어떻게 하나요?
* Hive, Pig 또는 MapReduce 작업을 사용하여 Cosmos DB에 데이터를 저장하려면 어떻게 하나요?

다음 비디오에서는 Cosmos DB 및 HDInsight를 사용 하 여 하이브 작업을 통해 실행 위치 hello를 시청 하 여 시작 하는 것이 좋습니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

에서 반환 toothis 문서 hello Cosmos DB 데이터에 분석 작업을 실행 하는 방법을 대 한 전체 세부 정보를 받을 수 있습니다.

> [!TIP]
> 이 자습서에서는 사용자가 이전에 Apache Hadoop, Hive 및/또는 Pig를 사용한 경험이 있다고 가정합니다. 새 tooApache Hadoop, Hive, 및 Pig 인 경우 hello 방문 하는 것이 좋습니다 [Apache Hadoop 설명서][apache-hadoop-doc]합니다. 또한 이 자습서에서는 이전에 Cosmos DB를 사용한 경험이 있으며 Cosmos DB 계정이 있다고 가정합니다. 새 tooCosmos DB 인지는 Cosmos DB 계정이 없는 경우 확인 하세요 우리의 [시작] [ getting-started] 페이지.
>
>

자습서 hello 및 Hive, Pig 및 MapReduce tooget hello 전체 샘플 PowerShell 스크립트를 원하는 시간 toocomplete 없습니까? [여기][hdinsight-samples]에서 가져오세요. hello 다운로드에는 이러한 예제에 대 한 hello hql로 변환, pig 및 java 파일이 포함 되어 있습니다.

## <a name="NewestVersion"></a>최신 버전
<table border='1'>
    <tr><th>Hadoop 커넥터 버전</th>
        <td>1.2.0</td></tr>
    <tr><th>스크립트 URI</th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>수정한 날짜</th>
        <td>2016년 4월 26일</td></tr>
    <tr><th>지원되는 HDInsight 버전</th>
        <td>3.1, 3.2</td></tr>
    <tr><th>변경 로그</th>
        <td>Azure DB Cosmos Java SDK too1.6.0 업데이트</br>
            원본 및 싱크로 분할된 컬렉션에 대한 추가 지원</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>필수 조건
이 자습서에서는 hello 지침을 수행 하기 전에 hello 다음 있는지를 확인 합니다.

* Cosmos DB 계정, 데이터베이스 및 내부 문서가 포함된 컬렉션. 자세한 내용은 [Cosmos DB 시작하기][getting-started]를 참조하세요. Hello Cosmos DB 계정에 샘플 데이터를 가져올 [Cosmos DB 가져오기 도구][import-data]합니다.
* 처리량. HDInsight에서의 읽기 및 쓰기는 해당 컬렉션에 할당된 요청 단위로 계산됩니다.
* 각 출력 컬렉션 내의 추가 저장 프로시저 용량. hello 저장 프로시저 결과 문서를 전송 하는 데 사용 됩니다.
* Hello Hive, Pig, 또는 MapReduce 작업의 결과 문서 hello에 대 한 용량입니다.
* [*선택 사항*] 추가 컬렉션의 용량입니다.

> [!WARNING]
> 순서 tooavoid hello hello 작업 동안 새 컬렉션을 만드는에 hello 결과 toostdout 인쇄, hello 출력 tooyour WASB 컨테이너에 저장 하거나 이미 기존 컬렉션을 지정 합니다. 기존 컬렉션을 지정 하는 hello 경우, 새 문서 hello 컬렉션 내 만들어지고 이미 기존 문서에서 충돌 하는 경우에 적용 될 *id*합니다. **hello 커넥터 id 충돌이 있는 기존 문서를 자동으로 덮어쓰기 때문**합니다. Hello upsert 옵션 toofalse를 설정 하 여이 기능을 해제할 수 있습니다. Upsert가 false이 고 hello Hadoop 작업이 실패 합니다; 충돌이 발생 하는 경우 id 충돌 오류를 보고 합니다.
>
>

## <a name="ProvisionHDInsight"></a>1단계: 새 HDInsight 클러스터 만들기
이 자습서에서는 스크립트 작업 hello Azure 포털 toocustomize에서 HDInsight 클러스터에 있습니다. 이 자습서에서는 hello Azure 포털 toocreate HDInsight 클러스터에 사용 합니다. Toouse PowerShell cmdlet 또는 hello HDInsight.NET SDK 확인 하는 방법에 대 한 지침은 [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터] [ hdinsight-custom-provision] 문서.

1. Toohello 로그인 [Azure 포털][azure-portal]합니다.
2. 클릭 **+ 새로 만들기** hello 맨 왼쪽 탐색 hello에서 검색 한 **HDInsight** hello 새 블레이드의 hello 검색 표시줄에 있습니다.
3. **HDInsight** 공개한 **Microsoft** hello hello 결과 위쪽에 표시 됩니다. 클릭한 다음 **만들기**를 클릭합니다.
4. Hello 새 HDInsight 클러스터에 만드는 블레이드를 입력 하면 **클러스터 이름** 선택 hello 및 **구독** tooprovision 아래에서이 리소스를 원하는 합니다.

    <table border='1'>
        <tr><td>클러스터 이름</td><td>Hello 클러스터 이름입니다.<br/>
DNS 이름은 영숫자 문자로 시작 및 끝나야 하고 대시를 포함할 수 있습니다.<br/>
hello 필드는 3 ~ 63 자 사이의 문자열 이어야 합니다.</td></tr>
        <tr><td>구독 이름</td>
            <td>둘 이상의 Azure 구독을 보유 하는 경우 HDInsight 클러스터를 호스팅하는 hello 구독을 선택 합니다. </td></tr>
    </table>
5.클릭 **클러스터 유형 선택** 집합 hello 속성 toohello 다음 값을 지정 합니다.

    <table border='1'>
        <tr><td>클러스터 유형</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>클러스터 계층</td><td><strong>Standard</strong></td></tr>
        <tr><td>운영 체제</td><td><strong>Windows</strong></td></tr>
        <tr><td>버전</td><td>최신 버전</td></tr>
    </table>

    이제 **선택**을 클릭합니다.

    ![Hadoop HDInsight 초기 클러스터 세부 정보 제공][image-customprovision-page1]
6. 클릭 **자격 증명** tooset 로그인 및 원격 액세스 자격 증명입니다. **클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**를 선택합니다.

    클러스터에 tooremote 하려는 경우 선택 *예* hello hello 블레이드 맨 아래에 사용자 이름 및 암호를 제공 합니다.
7. 클릭 **데이터 원본** tooset 데이터에 대 한 기본 위치에 액세스 합니다. Hello 선택 **선택 방법을** 하 고 이미 기존 저장소 계정을 지정 하거나 새로 만듭니다.
8. 동일한 블레이드 hello, 지정 된 **기본 컨테이너** 및 **위치**합니다. 그리고 **선택**을 클릭합니다.

   > [!NOTE]
   > 위치 닫기 tooyour 성능 향상을 위해 Cosmos DB 계정 영역을 선택 합니다.
   >
   >
9. 클릭 **가격 책정** tooselect hello의 노드 수와 종류입니다. Hello 기본 구성 및 크기 조정 hello 작업자 노드 수를 나중에 유지할 수 있습니다.
10. 클릭 **옵션 구성**, 다음 **스크립트 동작** 선택적 구성 블레이드 hello에 있습니다.

     스크립트 동작에서 다음 정보 toocustomize hello HDInsight 클러스터에 입력 합니다.

     <table border='1'>
         <tr><th>속성</th><th>값</th></tr>
         <tr><td>이름</td>
             <td>Hello 스크립트 동작에 대 한 이름을 지정 합니다.</td></tr>
         <tr><td>스크립트 URI</td>
             <td>가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다.</br></br>
다음을 입력합니다. </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>헤드</td>
             <td>Hello 확인란 toorun hello hello 헤드 노드에 대 한 PowerShell 스크립트를 클릭 합니다.</br></br>
             <strong>이 확인란을 선택합니다</strong>.</td></tr>
         <tr><td>작업자</td>
             <td>Hello 작업자 노드에 hello 확인란 toorun hello PowerShell 스크립트를 클릭 합니다.</br></br>
             <strong>이 확인란을 선택합니다</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Hello 사육에 hello 확인란 toorun hello PowerShell 스크립트를 클릭 합니다.</br></br>
             <strong>필요하지 않습니다</strong>.
             </td></tr>
         <tr><td>매개 변수</td>
             <td>Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</br></br>
             <strong>필요한 매개 변수가 없습니다</strong>.</td></tr>
     </table>
11. Azure 구독에서 새 **리소스 그룹**을 만들거나 기존 리소스 그룹을 사용합니다.
12. 이제, 확인 **Pin toodashboard** tootrack 누른 배포 **만들기**!

## <a name="InstallCmdlets"></a>2단계: Azure PowerShell 설치 및 구성
1. Azure PowerShell을 설치합니다. 자세한 내용은 [여기][powershell-install-configure]에서 확인할 수 있습니다.

   > [!NOTE]
   > 또는 Hive 쿼리만 해당하는 경우 HDInsight의 온라인 Hive 편집기를 사용할 수 있습니다. 따라서 toohello toodo에 로그인 [Azure 포털][azure-portal], 클릭 **HDInsight** on hello 왼쪽된 창 tooview HDInsight 클러스터의 목록 합니다. Hello 클러스터 toorun 하이브 쿼리를 원하는 하 고 클릭 한 다음 클릭 **쿼리 콘솔**합니다.
   >
   >
2. Azure PowerShell 통합 스크립팅 환경 hello를 엽니다.

   * Windows 8 또는 Windows Server 2012 이상을 실행 하는 컴퓨터에서 기본 제공 hello를 사용할 수 있습니다 검색 합니다. Hello 시작 화면에서 입력 **powershell ise** 클릭 **Enter**합니다.
   * Windows 8 또는 Windows Server 2012 이전 버전을 실행 하는 컴퓨터에서 hello 시작 메뉴를 사용 합니다. Hello 시작 메뉴에서 입력 **명령 프롬프트** hello 검색 상자에 다음 hello 결과 목록에서 클릭 **명령 프롬프트**합니다. Hello 명령 프롬프트에에서 입력 **powershell_ise** 클릭 **Enter**합니다.
3. Azure 계정을 추가합니다.

   1. Hello 콘솔 창에에서 입력 **Add-azureaccount** 클릭 **Enter**합니다.
   2. Azure 구독에 연결 된 hello 전자 메일 주소에 입력 하 고 클릭 **계속**합니다.
   3. Azure 구독에 대 한 hello 암호를 입력 합니다.
   4. **로그인**을 클릭합니다.
4. 다음 다이어그램 hello hello Azure PowerShell 스크립팅 환경을의 중요 한 부분을 식별 합니다.

    ![Azure PowerShell에 대한 다이어그램][azure-powershell-diagram]

## <a name="RunHive"></a>3단계: Cosmos DB 및 HDInsight를 사용하여 Hive 작업 실행
> [!IMPORTANT]
> < >로 표시된 모든 변수는 구성 설정을 사용하여 입력해야 합니다.
>
>

1. Hello 다음 PowerShell 스크립트 창에서 변수를 설정 합니다.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>쿼리 문자열 생성부터 시작합니다. 모든 문서 시스템 생성 타임 스탬프 (_ts) 및 Azure Cosmos DB 컬렉션에서 고유 id (_rid)는 모든 문서 hello 분 단위로 계산 하 고 다음 새 Azure Cosmos DB 컬렉션에 다시 hello 결과 저장 하는 하이브 쿼리를 작성 합니다.</p>

    <p>먼저 Azure Cosmos DB 컬렉션에서 Hive 테이블을 만듭니다. 다음 코드 조각 toohello PowerShell 스크립트 창 hello 추가 <strong>후</strong> # 1에서 hello 코드 조각입니다. 자사 문서 toojust _ts 및 _rid hello 선택적 DocumentDB.query 매개 변수 t 트림 포함 되어 있는지 확인 합니다.</p>

   > [!NOTE]
   > **DocumentDB.inputCollections 이름 지정은 실수가 아니었습니다.** 입력으로 여러 컬렉션을 추가할 수 있도록 허용합니다. </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. 다음으로 hello 출력 컬렉션에 대 한 하이브 테이블을 만들어 보겠습니다. hello 출력 문서 속성 hello 월, 일, 시간, 분 및 hello 총 항목 수가 됩니다.

   > [!NOTE]
   > **하지만 다시 DocumentDB.outputCollections 이름 지정은 실수가 아니었습니다.** 출력으로 여러 컬렉션을 추가할 수 있도록 허용합니다. </br>
   > '*DocumentDB.outputCollections*' = '*\<DocumentDB 출력 컬렉션 이름 1\>*,*\<DocumentDB 출력 컬렉션 이름 2\>*' </br> hello 컬렉션 이름은 단일 쉼표만 사용 하 여 공백 없이 구분 됩니다. </br></br>
   > 문서는 여러 컬렉션 간에 라운드 로빈 방식으로 분산됩니다. 문서 일괄 처리 한 컬렉션에 저장 될 다음 문서의 두 번째 일괄 처리 등 hello 다음 컬렉션에 저장 됩니다.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. 마지막으로, 보겠습니다 월, 일, 시간 및 분 및 삽입 hello 결과 hello로 다시 여 집계 hello 문서 출력 Hive 테이블입니다.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Hello 스크립트 조각 toocreate 하이브 작업 정의 hello 이전 쿼리에서 다음을 추가 합니다.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    사용할 수도 있습니다 hello-파일 전환 toospecify HDFS에 HiveQL 스크립트 파일입니다.
4. 다음 코드 조각 toosave hello 시작 시간 hello를 추가 하 고 hello 하이브 작업을 제출 합니다.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. 하이브 작업 toocomplete hello에 대 한 toowait 다음 hello를 추가 합니다.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Hello tooprint hello 표준 출력 및 hello 시작 다음을 추가 하 고 종료 시간입니다.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **실행** 합니다. **클릭** hello 녹색 단추를 실행 합니다.
8. Hello 결과 확인 합니다. Hello에 로그인 [Azure 포털][azure-portal]합니다.

   1. 클릭 <strong>찾아보기</strong> hello 왼쪽 패널에 있습니다. </br>
   2. 클릭 <strong>모든</strong> hello top-hello 찾아보기 패널의 오른쪽에 있습니다. </br>
   3. <strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다. </br>
   4. 다음으로 찾을 프로그램 <strong>Azure Cosmos DB 계정</strong>, 다음 <strong>Azure Cosmos DB 데이터베이스</strong> 하였고 <strong>Azure Cosmos DB 컬렉션</strong> hello 출력 컬렉션에 지정 된 연관 하이브 쿼리 합니다.</br>
   5. 끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</br></p>

   하이브 쿼리 hello 결과가 표시 됩니다.

   ![Hive 쿼리 결과][image-hive-query-results]

## <a name="RunPig"></a>4단계: Cosmos DB 및 HDInsight를 사용하여 Pig 작업 실행
> [!IMPORTANT]
> < >로 표시된 모든 변수는 구성 설정을 사용하여 입력해야 합니다.
>
>

1. Hello 다음 PowerShell 스크립트 창에서 변수를 설정 합니다.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>쿼리 문자열 생성부터 시작합니다. 모든 문서 시스템 생성 타임 스탬프 (_ts) 및 Azure Cosmos DB 컬렉션에서 고유 id (_rid)는 모든 문서 hello 분 단위로 계산 하 고 다음 새 Azure Cosmos DB 컬렉션에 다시 hello 결과 저장 하는 Pig 쿼리를 작성 합니다.</p>
    <p>먼저 Cosmos DB의 문서를 HDInsight에 로드합니다. 다음 코드 조각 toohello PowerShell 스크립트 창 hello 추가 <strong>후</strong> # 1에서 hello 코드 조각입니다. Tooadd는 DocumentDB 쿼리 toohello 선택적 DocumentDB 쿼리 매개 변수 tootrim 우리의 문서 toojust _ts 및 _rid 있는지 확인 합니다.</p>

   > [!NOTE]
   > 입력으로 여러 컬렉션을 추가할 수 있도록 허용합니다. </br>
   > '*\<DocumentDB 입력 컬렉션 이름 1\>*,*\<DocumentDB 입력 컬렉션 이름 2\>*'</br> hello 컬렉션 이름은 단일 쉼표만 사용 하 여 공백 없이 구분 됩니다. </b>
   >
   >

    문서는 여러 컬렉션 간에 라운드 로빈 방식으로 분산됩니다. 문서 일괄 처리 한 컬렉션에 저장 될 다음 문서의 두 번째 일괄 처리 등 hello 다음 컬렉션에 저장 됩니다.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. 다음으로, 보겠습니다 hello 월, 일, 시간, 분 및 발생 빈도의 총 hello 하 여 hello 문서 수를 셉니다.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. 마지막으로, 새 출력 컬렉션에 저장할 hello 결과 보겠습니다.

   > [!NOTE]
   > 출력으로 여러 컬렉션을 추가할 수 있도록 허용합니다. </br>
   > '\<DocumentDB 출력 컬렉션 이름 1\>,\<DocumentDB 출력 컬렉션 이름 2\>'</br> hello 컬렉션 이름은 단일 쉼표만 사용 하 여 공백 없이 구분 됩니다.</br>
   > 에 대해 설명 합니다 여러 컬렉션 hello 간에 분산된 라운드 로빈을 해야 합니다. 문서 일괄 처리 한 컬렉션에 저장 될 다음 문서의 두 번째 일괄 처리 등 hello 다음 컬렉션에 저장 됩니다.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Hello 스크립트 조각 toocreate Pig 작업 정의 hello 이전 쿼리에서 다음을 추가 합니다.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    사용할 수도 있습니다 hello-파일 전환 toospecify HDFS에서 Pig 스크립트 파일입니다.
6. 다음 코드 조각 toosave hello 시작 시간 hello를 추가 하 고 hello Pig 작업을 제출 합니다.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Hello toowait Pig 작업 toocomplete hello에 대 한 다음 추가 합니다.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Hello tooprint hello 표준 출력 및 hello 시작 다음을 추가 하 고 종료 시간입니다.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **실행** 합니다. **클릭** hello 녹색 단추를 실행 합니다.
10. Hello 결과 확인 합니다. Hello에 로그인 [Azure 포털][azure-portal]합니다.

    1. 클릭 <strong>찾아보기</strong> hello 왼쪽 패널에 있습니다. </br>
    2. 클릭 <strong>모든</strong> hello top-hello 찾아보기 패널의 오른쪽에 있습니다. </br>
    3. <strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다. </br>
    4. 다음으로 찾을 프로그램 <strong>Azure Cosmos DB 계정</strong>, 다음 <strong>Azure Cosmos DB 데이터베이스</strong> 하였고 <strong>Azure Cosmos DB 컬렉션</strong> hello 출력 컬렉션에 지정 된 연관 Pig 쿼리 합니다.</br>
    5. 끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.</br></p>

    Hello Pig 쿼리 결과가 표시 됩니다.

    ![Pig 쿼리 결과][image-pig-query-results]

## <a name="RunMapReduce"></a>5단계: Azure Cosmos DB 및 HDInsight를 사용하여 MapReduce 작업 실행
1. Hello 다음 PowerShell 스크립트 창에서 변수를 설정 합니다.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Hello Azure Cosmos DB 컬렉션에서 각 문서 속성에 대해 발생 수를 계산 하는 MapReduce 작업을 실행 합니다. 이 스크립트 조각을 추가 **후** 위의 hello 코드 조각입니다.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar hello Cosmos DB Hadoop 커넥터의 사용자 지정 설치 hello 함께 제공 됩니다.
   >
   >
3. 명령 toosubmit hello MapReduce 작업을 수행 하는 hello를 추가 합니다.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    또한 toohello MapReduce 작업 정의 입력 해야 hello HDInsight 클러스터 이름을 toorun hello MapReduce 작업 및 hello 자격 증명. hello Start-azurehdinsightjob은 비동기식된 호출 합니다. hello 작업을 사용 하 여 hello toocheck hello 완료 *Wait-azurehdinsightjob* cmdlet.
4. 다음 명령은 toocheck hello 실행 중인 hello MapReduce 작업을 사용 하 여 모든 오류를 추가 합니다.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **실행** 합니다. **클릭** hello 녹색 단추를 실행 합니다.
6. Hello 결과 확인 합니다. Hello에 로그인 [Azure 포털][azure-portal]합니다.

   1. 클릭 <strong>찾아보기</strong> hello 왼쪽 패널에 있습니다.
   2. 클릭 <strong>모든</strong> hello top-hello 찾아보기 패널의 오른쪽에 있습니다.
   3. <strong>Azure Cosmos DB 계정</strong>을 찾아서 클릭합니다.
   4. 다음으로 찾을 프로그램 <strong>Azure Cosmos DB 계정</strong>, 다음 <strong>Azure Cosmos DB 데이터베이스</strong> 하였고 <strong>Azure Cosmos DB 컬렉션</strong> hello 출력 컬렉션에 지정 된 연관 MapReduce 작업 합니다.
   5. 끝으로, <strong>개발자 도구</strong> 아래에서 <strong>문서 탐색기</strong>를 클릭합니다.

      MapReduce 작업의 hello 결과가 표시 됩니다.

      ![MapReduce 쿼리 결과][image-mapreduce-query-results]

## <a name="NextSteps"></a>다음 단계
축하합니다. 지금까지 Azure Cosmos DB 및 HDInsight를 사용해서 첫 번째 Hive, Pig 및 MapReduce 작업을 실행했습니다.

Hadoop 커넥터는 소스가 공개되어 있습니다. 관심이 있으면 [GitHub][github]에서 참여할 수 있습니다.

더 toolearn hello 다음 문서를 참조:

* [Documentdb로 Java 응용 프로그램 개발][documentdb-java-application]
* [HDInsight의 Hadoop용 Java MapReduce 프로그램 개발][hdinsight-develop-deploy-java-mapreduce]
* [HDInsight tooanalyze 모바일 송수화기 사용 중인 Hadoop 하이브 사용을 시작.][hdinsight-get-started]
* [HDInsight와 함께 MapReduce 사용][hdinsight-use-mapreduce]
* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]
* [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
