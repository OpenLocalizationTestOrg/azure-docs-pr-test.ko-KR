---
title: "데이터 레이크 도구를 사용 하 여 Visual Studio 용 HDInsight aaaConnect tooAzure | Microsoft Docs"
description: "Azure HDInsight 및 하이브 쿼리 실행된에서 tooinstall 및 사용 데이터 레이크 Tools for Visual Studio tooconnect tooHadoop 클러스터 되는 방법에 대해 알아봅니다."
keywords: "Hadoop 도구, Hive 쿼리, Visual Studio, Visual Studio Hadoop Hive"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>TooAzure HDInsight를 연결 하 고 Visual Studio에 대 한 데이터 레이크 도구를 사용 하는 하이브 쿼리를 실행 합니다.

Visual Studio tooconnect tooHadoop에 대 한 데이터 레이크 도구 toouse 클러스터 되는 방법을 알아보려면 [Azure HDInsight](hdinsight-hadoop-introduction.md) 및 하이브 쿼리를 제출 합니다. HDInsight를 사용 하는 방법에 대 한 자세한 내용은 참조 [소개 tooHDInsight](hdinsight-hadoop-introduction.md) 및 [HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)합니다. Tooa Storm 클러스터를 연결 하는 방법에 대 한 자세한 내용은 참조 [Visual Studio를 사용 하 여 HDInsight의 Apache Storm의 개발 C# 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.

데이터 레이크 Tools for Visual Studio에 사용 되는 tooaccess 수 Data Lake 분석 및 HDInsight 모두 합니다.  데이터 레이크 도구에 대 한 hello 내용은 [자습서: 데이터 레이크 도구를 사용 하 여 Visual Studio 용 U-SQL 스크립트를 개발](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md)합니다.

**필수 구성 요소**

Visual Studio에서이 자습서 및 사용 하 여 hello 데이터 레이크 도구 toocomplete, hello 다음이 필요 합니다.

* Azure HDInsight 클러스터: toocreate 하나, 참조 [Linux 기반 HDInsight를 사용 하 여 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
* 다음 소프트웨어 hello로 워크스테이션 합니다.
  
  * Windows 10, Windows 8.1, Windows 8 또는 Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > 현재 Visual Studio에 대 한 hello 데이터 레이크 도구 hello 영어 버전 에서만 제공 됩니다.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Visual Studio용 Data Lake 도구 설치

Data Lake Tools은 Visual Studio 2017에 기본적으로 설치됩니다. 이전 버전에 대 한 hello를 사용 하 여 설치할 수 있습니다 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/)합니다. Visual Studio 버전에 일치 하는 hello를 선택 해야 합니다. 설치 된 Visual Studio가 없는 경우 설치할 수 있습니다 hello를 사용 하 여 최신 Visual Studio Community 및 Azure SDK hello [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/):

![데이터 레이크 Tools for Visual Studio 웹 플랫폼 설치 관리자입니다. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "사용 하 여 웹 플랫폼 설치 관리자 tooinstall 데이터 레이크 Tools for Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>TooAzure 구독 연결
데이터 레이크 도구 Visual Studio에서는 tooconnect tooyour HDInsight 클러스터에 대 한 몇 가지 기본 관리 작업을 수행 하며 하이브 쿼리를 실행 합니다.

> [!NOTE]
> 연결 tooa 일반 Hadoop 클러스터에 대 한 자세한 내용은 참조 [작성 및 Visual Studio를 사용 하는 하이브 쿼리를 제출](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx)합니다.
> 
> 

**tooconnect tooyour Azure 구독**

1. Visual Studio를 엽니다.
2. Hello에서 **보기** 메뉴를 클릭 하 여 **서버 탐색기** tooopen hello 서버 탐색기 창입니다.
3. **Azure**를 확장한 다음 **HDInsight**를 확장합니다.
   
   > [!NOTE]
   > 공지 hello **HDInsight 작업 목록** 창이 열려 있어야 합니다. 표시 되지 않는 경우 클릭 **다른 창** hello에서 **보기** 메뉴를 차례로 클릭 **HDInsight 작업 목록 창**합니다.  
   > 
   > 
4. Azure 구독 자격 증명을 입력한 후 **로그인**을 클릭합니다. 이만 toohello Azure 구독을 연결한 적이 없는 한이 워크스테이션에서 Visual Studio가 필요 합니다.
5. 서버 탐색기에서 기존 HDInsight 클러스터 목록이 표시됩니다. 모든 클러스터를 설정 하지 않은 경우에 hello Azure 포털, Azure PowerShell 또는 hello HDInsight SDK를 사용 하 여 만들 수 있습니다. 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.
   
   ![Data Lake Tools for Visual Studio 서버 탐색기- 클러스터 목록](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Data Lake Tools for Visual Studio 서버 탐색기")
6. HDInsight 클러스터를 확장합니다. **Hive 데이터베이스**, 기본 저장소 계정, 연결 저장소 계정 및 **Hadoop 서비스 로그**가 표시됩니다. Hello 엔터티를 추가로 확장할 수 있습니다.

Tooyour Azure 구독을 연결 하 고 나면 수 toodo hello 다음 수 있습니다.

**tooconnect toohello Visual Studio에서 Azure 포털**

* 서버 탐색기에서 **Azure** > **HDInsight**를 확장하고, HDInsight 클러스터를 마우스 오른쪽 단추로 클릭한 후 **Azure Portal에서 클러스터 관리**를 클릭합니다.

**tooask 질문 하 고 Visual Studio에서 피드백을 제공 합니다.**

* Hello에서 **도구** 메뉴를 클릭 **HDInsight**, 클릭 하 고 **MSDN 포럼** tooask 질문 하거나 클릭 **의견 제공**합니다.

## <a name="navigate-hello-linked-resources"></a>Hello 연결 된 리소스를 이동 합니다.
서버 탐색기에서 hello 기본 저장소 계정 및 모든 연결 된 저장소 계정을 볼 수 있습니다. Hello 기본 저장소 계정, 확장 하는 경우에 hello 저장소 계정에서 hello 컨테이너를 볼 수 있습니다. hello 기본 저장소 계정 및 hello 기본 컨테이너 표시 됩니다. 스키마 hello 컨테이너 tooview hello 내용 중 하나입니다.

![Data Lake Tools for Visual Studio 서버 탐색기 - 연결된 리소스 목록](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "연결된 리소스 목록")

컨테이너를 연 후 다음 단추 tooupload, 삭제 및 다운로드 blob hello를 사용할 수 있습니다.

![Data Lake Tools for Visual Studio 서버 탐색기 - Blob 작업](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "Blob 업로드, 삭제 및 다운로드")

## <a name="run-a-hive-query"></a>HIVE 쿼리 실행
[Apache Hive](http://hive.apache.org)는 데이터 요약, 쿼리 및 분석을 제공하기 위해 Hadoop을 기반으로 하는 데이터 웨어하우스 인프라입니다. Visual Studio용 Data Lake 도구는 Visual Studio에서 Hive 쿼리를 실행하도록 지원합니다. Hive에 대한 자세한 내용은 [HDInsight에서 Hive 사용](hdinsight-use-hive.md)을 참조하세요.

HDInsight 클러스터에 대해 많은 시간이 소요 tootest 하이브 스크립트는 몇 분 이상 걸릴 수 있습니다. 데이터 레이크 Tools for Visual Studio는 tooa 라이브 클러스터를 연결 하지 않고 로컬 하이브 스크립트를 유효성 검사할 수 있습니다.

또한 데이터 레이크 Tools for Visual Studio에서 수집 하 고 특정 하이브 작업의 hello YARN 로그에서 표시가 hello 하이브 작업 내의 이란 사용자가 toosee 있습니다.

### <a name="view-hello-hivesampletable"></a>보기 hello **hivesampletable**
모든 HDInsight 클러스터에는 *hivesampletable*이라는 샘플 Hive 테이블이 함께 제공됩니다. 이 테이블 tooshow 있습니다 toolist 하이브 테이블 hello 테이블 스키마를 보려면의 hello 행을 나열 하는 방법 hello 하이브에서는 테이블입니다.

**toolist 하이브 테이블 및 뷰 하이브 테이블 스키마**

1. **서버 탐색기**를 확장 하 고 **Azure** > **HDInsight** > 선택한 hello 클러스터 > **하이브 데이터베이스**  >  **기본** > **hivesampletable** toosee hello 테이블 스키마입니다.
2. 마우스 오른쪽 단추로 클릭 **hivesampletable**, 클릭 하 고 **보기 Top 100 Rows** toolist hello 행. 다음 하이브 ODBC 드라이버를 사용 하 여 하이브 쿼리에서 해당 toorunning hello입니다.
   
     SELECT * FROM hivesampletable LIMIT 100
   
   Hello 행 수를 사용자 지정할 수 있습니다.
   
   ![Data Lake Tools: HDInsight Hive Visual Studio - 스키마 쿼리](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Hive 쿼리 결과")

### <a name="create-hive-tables"></a>Hive 테이블 만들기
Hello GUI toocreate Hive 테이블을 사용 하거나 하이브 쿼리를 사용할 수 있습니다. Hive 쿼리 사용에 대한 자세한 내용은 [Hive 쿼리 실행](#run.queries)을 참조하세요.

**toocreate Hive 테이블**

1. **서버 탐색기**에서 **Azure** > **HDInsight 클러스터** HDInsight 클러스터 > **Hive 데이터베이스**를 확장한 후 **기본값**을 마우스 오른쪽 단추로 클릭하고 **테이블 만들기**를 클릭합니다.
2. Hello 테이블을 구성 합니다.
3. 클릭 **Create Table** toosubmit hello 작업 toocreate hello 새 Hive 테이블입니다.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools - Hive 테이블 만들기](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Hive 테이블 만들기")

### <a name="run.queries"></a>Hive 쿼리 유효성 검사 및 실행
두 가지 방법으로 toocreate 및 실행된 된 Hive 쿼리 가지가 있습니다.

* 임시 쿼리 만들기
* Hive 응용 프로그램 만들기

**toocreate, 유효성 검사 및 임시 쿼리를 실행 합니다.**

1. **서버 탐색기**에서 **Azure**를 확장한 후 **HDInsight 클러스터**를 확장합니다.
2. 마우스 오른쪽 단추로 클릭 hello 클러스터 toorun hello 쿼리 하려고 하 고 클릭 **는 하이브 쿼리를 작성할**합니다.
3. Hello 하이브 쿼리를 입력 합니다. 공지 hello 하이브 편집기는 IntelliSense를 지원합니다. 데이터 레이크 도구를 로드 하는 Visual Studio 지원에 대 한 하이브 스크립트를 편집 하는 경우 원격 메타 데이터를 hello 합니다. 예를 들어 "SELECT * FROM", IntelliSense에 나열 된 hello 입력 모든 제안된 테이블 이름 hello 합니다. 테이블 이름이 지정 되 면 hello 열 이름은 hello IntelliSense 별로 나열 됩니다. hello 도구는 거의 모든 하이브 DML 문의 하위 쿼리를 지원 하 고 기본 제공 Udf hello.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools - IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Data Lake Tools: HDInsight Visual Studio Tools - IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > Hello의 메타 데이터만 hello 클러스터 HDInsight 도구 모음에서 선택 되어 있는 제안 합니다.
   > 
   > 
4. (선택 사항): 클릭 **스크립트의 유효성을 검사** toocheck hello 스크립트 구문 오류입니다.
   
    ![Data Lake Tools: Data Lake Tools for Visual Studio - 로컬 유효성 검사](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "스크립트 유효성 검사")
5. **제출** 또는 **제출(고급)**을 클릭합니다. Hello 고급 전송 옵션을로 구성 합니다 **작업 이름**, **인수**, **추가 구성을**, 및 **상태 디렉터리**hello 스크립트:
   
    ![HDInsight Hadoop - Hive 쿼리](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "쿼리 제출")
   
    Hello 작업을 제출 하면 참조는 **작업 요약 하이브** 창.
   
    ![HDInsight Hadoop - Hive 쿼리 요약](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Hive 작업 요약")
6. 사용 하 여 hello **새로 고침** 너무 hello 작업 상태가 변경 될 때까지 tooupdate hello 상태 단추**Completed**합니다.
7. Hello hello 아래쪽 toosee hello 다음 링크 클릭: **작업 쿼리**, **작업 출력**, **작업 로그**, 또는 **Yarn 로그**합니다.

**toocreate 및 하이브 솔루션 실행**

1. Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.
2. 선택 **HDInsight** hello 왼쪽된 창에서 선택 **하이브 응용 프로그램** hello 가운데 창에서 hello 속성을 입력 한 다음 클릭 **확인**합니다.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools - 새 Hive 프로젝트](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Visual Studio에서 Hive 응용 프로그램 만들기")
3. **솔루션 탐색기**를 두 번 클릭 **Script.hql** tooopen 것입니다.
4. toovalidate hello 하이브 스크립트를 클릭할 수 있는 hello **스크립트의 유효성을 검사** 단추, 또는 hello 스크립트 hello 하이브 편집기에서 마우스 오른쪽 단추로 클릭 한 다음 클릭 **스크립트의 유효성을 검사** hello 상황에 맞는 메뉴에서입니다.

### <a name="view-hive-jobs"></a>Hive 작업 보기
Hive 작업에 대한 작업 쿼리, 작업 출력, 작업 로그 및 Yarn 로그를 볼 수 있습니다. 자세한 내용은 hello 이전 스크린샷을 참조 합니다.

hello hello 도구의 최신 릴리스를 수집 및 YARN 로그에서 표시가 여 하이브 작업 안에 무엇이 toosee가 있습니다. YARN 로그를 사용하여 성능 문제를 조사할 수 있습니다. HDInsight에서 YARN 로그를 수집하는 방법에 대한 자세한 내용은 [프로그래밍 방식으로 HDInsight 응용 프로그램 로그에 액세스](hdinsight-hadoop-access-yarn-app-logs.md)를 참조하세요.

**tooview 하이브 작업**

1. **서버 탐색기**에서 **Azure**를 확장한 후 **HDInsight**를 확장합니다.
2. HDInsight 클러스터를 마우스 오른쪽 단추로 클릭한 다음 **작업 보기**를 클릭합니다. Hello 클러스터에서 실행 한 작업을 하이브 hello 목록이 표시 됩니다.
3. 작업 목록 tooselect hello에서에서 작업을 클릭 한 다음 클릭 사용 하 여 hello **작업 요약 하이브** 창 tooopen **작업 쿼리**, **작업 출력**, **작업 로그**, 또는 **Yarn 로그**합니다.
   
    ![Data Lake Tools: HDInsight Visual Studio Tools - Hive 작업 보기](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Hive 작업 보기")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>HiveServer2를 통해 더 빠른 경로 하이브 실행
> [!NOTE]
> 이 기능은 HDInsight 클러스터 버전 3.2 이상에만 적용됩니다.
> 
> 

toosubmit Hive 작업을 사용 하는 hello 데이터 레이크 도구 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (Templeton이 라고도 함). 데 걸린 시간이 오래 tooreturn 작업 세부 정보 및 오류 정보입니다.
순서 toosolve 이러한 성능 문제를 데이터 레이크 도구를 실행 하는 hello RDP/SSH를 무시 되도록 HiveServer2 통해 hello 클러스터에서 직접 작업을 하이브입니다.
또한 toobetter 성능에서 사용자가 볼 수 하이브 Tez 그래프에 있고 hello 작업 세부 정보입니다.

HDInsight 클러스터 버전 3.2 이상의 경우 **HiveServer2를 통해 실행** 단추를 볼 수 있습니다.

![Data Lake Visual Studio Tools - HiveServer2를 통한 실행](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "HiveServer2를 사용하여 Hive 쿼리 실행")

및에 실시간 스트리밍 hello 로그를 확인 하 고 hello 하이브 쿼리 Tez에서 실행 되 면 hello 작업 그래프를 볼 수 있습니다.

![Data Lake Visual Studio Tools - 빠른 경로 Hive 실행](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "작업 그래프 보기")

**HiveServer2를 통한 쿼리 실행과 WebHCat을 통한 쿼리 제출 간의 차이**

HiveServer2를 통한 쿼리 실행에 다양한 성능 이점이 있지만 몇 가지 제한 사항이 있습니다. 몇몇 제한 사항이 적용 hello 프로덕션용으로 사용할 적합 하지 않습니다. hello 아래 표에 나와 hello 차이.

|  | HiveServer2를 통한 실행 | WebHCat을 통한 제출 |
| --- | --- | --- |
| 쿼리 실행 |WebHCat (실행 되며 MapReduce 작업 이름: "TempletonControllerJob")의 hello 오버 헤드를 제거 합니다. |WebHCat을 통해 쿼리를 실행하는 한 WebHCat은 추가 대기 시간을 도입하는 MapReduce 작업을 시작합니다. |
| 로그 다시 스트리밍 |거의 실시간으로. |hello 작업 실행 로그는 hello 작업이 완료 되는 경우에 사용할 수 있습니다. |
| 작업 기록 보기 |HiveServer2를 통해 쿼리를 실행하는 경우 작업 기록(작업 로그, 작업 출력)은 유지되지 않습니다. hello 응용 프로그램 제한 된 정보로 YARN UI에서 볼 수 있습니다. |WebHCat을 통해 쿼리를 실행하는 경우 작업 기록(작업 로그, 작업 출력)은 유지되고 Visual Studio/HDInsight SDK/PowerShell을 사용하여 볼 수 있습니다. |
| 창 닫기 |HiveServer2를 통해 실행 방법은 "동기" 열려 있던 windows hello를 유지 해야 하므로 hello 창이 닫힌 hello 쿼리 실행 취소 됩니다. |WebHCat을 통해 전송 방법은 "비동기" WebHCat 통해 hello 쿼리를 제출 하 고 Visual Studio를 닫을 수 있도록 합니다. 다시 시도 하 고 언제 든 지 hello 결과 확인할 수 있습니다. |

### <a name="tez-hive-job-performance-graph"></a>Tez Hive 작업 성능 그래프
하이브 작업 hello에 대 한 성능 그래프를 보여 주는 hello 데이터 레이크 도구 지원 hello Tez 실행 엔진에서 실행 했습니다. Tez를 사용하도록 설정하는 방법에 대한 자세한 내용은 [HDInsight에서 Hive 사용](hdinsight-use-hive.md)을 참조하세요. 제출 하면 hello 작업이 완료 될 때 그래프를 hello 하이브 Visual Studio, Visual Studio에서에서 작업의 수를 보여 줍니다.  Tooclick hello 해야 **새로 고침** 단추 tooget hello 최신 작업 상태입니다.

> [!NOTE]
> 이 기능은 HDInsight 클러스터의 3.2.4.593 상위 버전에서만 사용할 수 있으며 완료된 작업에 대해서만 작동합니다.(WebHCat을 통해 작업을 제출한 경우, 이 그래프는 HiveServer2를 통해 쿼리를 실행한 경우에만 표시됩니다.) Windows 및 Linux 기반 클러스터 모두에 대해 동작합니다.
> 
> 

![hadoop hive tez 성능 그래프](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "작업 상태")

프로그램 하이브 이해 toohelp 더 나은 쿼리, hello 도구는이 릴리스에서 hello 하이브 연산자 뷰를 추가 합니다. Hello 작업 그래프의 hello 꼭 짓 toodouble 클릭 하기만 하면 및 hello 꼭지점 내 모든 hello 연산자를 볼 수 있습니다. 이 연산자의 자세한 내용은 특정 연산자 tooview에 가져가면 수도 있습니다.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Tez의 Hive 작업을 위한 작업 실행 보기
하이브 Tez 작업에 사용 될 수 있는 작업 실행 보기 hello tooget 구조화 & 하이브 작업에 대 한 정보를 시각화 및 더 많은 작업 세부 정보를 가져옵니다. 성능 문제가 있는 경우에 hello 보기 tooget에 대 한 세부 정보를 사용할 수 있습니다. 예를 들어 각 작업은 작동 방법과 hello 자세한 정보 (데이터 읽기/쓰기, 일정/시작/종료 시간, 등)에 각 작업에 대 한 작업 구성 또는 시각화 hello 정보에 따라 시스템 아키텍처를 조정할 수 있도록 합니다.

![Data Lake Visual Studio Tools - 작업 실행 보기](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "작업 실행 보기")

## <a name="run-pig-scripts"></a>Pig 스크립트 실행
데이터 레이크 Tools for Visual Studio에서는 만들 및 Pig 스크립트 tooHDInsight 클러스터를 제출 합니다. 사용자가 서식 파일에서 Pig 프로젝트를 만들고 hello 스크립트 tooHDInsight 클러스터를 제출할 수 있습니다.

## <a name="feedbacks--known-issues"></a>피드백 및 알려진 문제
* 현재 HiveServer2 결과는 일반 텍스트 버전으로 표시되며, 이것은 바람직하지 않습니다. 이 문제를 해결하기 위해 개발 중에 있습니다.
* Hello 결과 NULL 값을 시작 하는 경우 현재 hello 결과 표시 되지 않습니다. 이 문제를 해결 하 고 있다고 생각 무료 toodrop 지원 전자 메일 또는 연락처 우리는 팀이이 문제에 대해 차단 된 경우.
* Visual Studio에서 만든 hello hql로 변환 스크립트는 사용자의 지역 설정에 따라 인코딩됩니다. 사용자는 hello 스크립트 toocluster 이진으로 업로드 하는 경우 올바르게 실행 되지 않을 수도 있습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 tooconnect tooHDInsight hello 데이터 레이크 (HDInsight)를 사용 하 여 Visual Studio에서 클러스터 하는 방법을 배운 도구 패키지를 방법과 toorun Hive 쿼리 합니다. 자세한 내용은 다음을 참조하세요.

* [HDInsight에서 Hadoop Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
* [HDInsight에서 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)
* [HDInsight에서 Hadoop으로 Twitter 데이터 분석](hdinsight-analyze-twitter-data.md)

