---
title: "Hortonworks 샌드박스-Azure HDInsight와 Visual Studio 용 aaaData 호수 도구 | Microsoft Docs"
description: "어떻게 toouse hello Azure 데이터 레이크 tools for Visual Studio 로컬 VM에서 실행 하는 hello Hortonworks 샌드박스를 알아봅니다. 이러한 도구를 통해 만들 하 고 hello 샌드박스 및 작업 출력 보기 및 기록에 Hive 및 Pig 작업을 실행할 수 있습니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Visual Studio에 대 한 hello Azure 데이터 레이크 도구를 사용 하 여 hello Hortonworks 샌드박스로

Azure Data Lake는 제네릭 Hadoop 클러스터를 사용하기 위한 도구를 포함합니다. 이 문서 필요한 toouse hello 데이터 레이크 도구와 hello 로컬 가상 컴퓨터에서 실행 중인 Hortonworks 샌드박스 hello 단계를 제공 합니다.

Hello Hortonworks 샌드박스를 사용 하 여 로컬 개발 환경에서 Hadoop으로 toowork가 있습니다. 원하는 toodeploy를 솔루션을 개발한 후 그 tooan HDInsight 클러스터를 옮길 수 배율을 사용할 때.

## <a name="prerequisites"></a>필수 조건

* hello Hortonworks 샌드박스, 개발 환경에서 가상 컴퓨터에서 실행 합니다. 이 문서 작성 하 고 Oracle VirtualBox에서 실행 되는 hello 샌드박스를 사용 하 여 테스트 되었습니다. Hello 샌드박스를 설정에 대 한 자세한 내용은 참조 hello [hello Hortonworks 샌드박스 시작 합니다.](hdinsight-hadoop-emulator-get-started.md) 문서를 참조하세요.

* Visual Studio 2013, Visual Studio 2015 또는 Visual Studio 2017(모든 에디션)

* hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/) 2.7.1 이상.

* hello [Azure 데이터 레이크 l Visual Studio 용 도구](https://www.microsoft.com/download/details.aspx?id=49504)합니다.

## <a name="configure-passwords-for-hello-sandbox"></a>Hello 샌드박스에 대 한 암호 구성

해당 hello Hortonworks 샌드박스 실행 되 고 있는지 확인 하십시오. Hello에서 hello 단계를 수행 [hello Hortonworks 샌드박스에서](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) 문서. 이러한 단계는 hello SSH에 대 한 hello 암호 구성 `root` 계정을 한 Ambari hello `admin` 계정. 이 암호는 Visual Studio에서 toohello 샌드박스를 연결할 때 사용 됩니다.

## <a name="connect-hello-tools-toohello-sandbox"></a>Hello 도구 toohello 샌드박스 연결

1. Visual Studio를 열고 **보기** 및 **서버 탐색기**를 차례로 선택합니다.

2. **서버 탐색기**, 마우스 오른쪽 단추로 클릭 hello **HDInsight** 항목을 선택한 후 **tooHDInsight 에뮬레이터 연결**합니다.

    ![스크린샷의 서버 탐색기와 연결 tooHDInsight 강조 표시 하는 에뮬레이터](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. Hello에서 **tooHDInsight 에뮬레이터 연결** 대화 상자 Ambari를 위해 구성 된 hello 암호를 입력 합니다.

    ![암호 텍스트 상자가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    선택 **다음** toocontinue 합니다.

4. 사용 하 여 hello **암호** hello에 대 한 구성 필드 tooenter hello 암호 `root` 계정. Hello hello 기본값에 다른 필드를 둡니다.

    ![암호 텍스트 상자가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    선택 **다음** toocontinue 합니다.

5. Hello 서비스 toofinish의 유효성 검사 될 때까지 기다립니다. 경우에 따라 유효성 검사 실패 하 고 tooupdate hello 구성 메시지를 표시 합니다. 유효성 검사에 실패할 경우 선택 **업데이트**, hello 구성 및 서비스 toofinish hello에 대 한 확인을 기다립니다.

    ![업데이트 단추가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > hello 업데이트 프로세스 Ambari toomodify hello Hortonworks 샌드박스 구성 toowhat에서 예상 하는 hello 데이터 레이크 tools for Visual Studio를 사용 합니다.

6. 유효성 검사 완료 되 면 선택 **마침** toocomplete 구성 합니다.
    ![마침 단추가 강조 표시된 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > 개발 환경 및 hello toohello 가상 컴퓨터를 할당 된 메모리 크기의 hello 속도 따라 수 몇 분 tooconfigure 수행 하 고 hello 서비스의 유효성을 검사 합니다.

다음이 단계를 따른 후 해야는 **HDInsight 로컬 클러스터** hello에서 서버 탐색기의 항목 **HDInsight** 섹션.

## <a name="write-a-hive-query"></a>Hive 쿼리 작성

Hive에서는 구조화된 데이터로 작업하기 위한 SQL과 유사한 쿼리 언어(HiveQL)를 제공합니다. 사용 하 여 hello 다음 toolearn hello 로컬 클러스터에 대 한 주문형 toorun 쿼리 하는 방법을 안내 합니다.

1. **서버 탐색기**를 이전에 추가한 hello 로컬 클러스터에 대 한 hello 항목을 마우스 오른쪽 단추로 클릭 한 다음 선택 **는 하이브 쿼리를 작성할**합니다.

    ![Hive 쿼리 작성이 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    새 쿼리 창이 표시됩니다. 신속 하 게 수 여기 쓰고 쿼리 toohello 로컬 클러스터에 제출 합니다.

2. 새 쿼리 창 hello hello 다음 명령을 입력 합니다.

        select count(*) from sample_08;

    toorun hello 쿼리의 **전송** hello 창의 위쪽에 hello 합니다. Hello 다른 값을 둡니다 (**일괄 처리** 서버 이름과) hello 기본값입니다.

    ![Hello 전송 단추가 강조 표시 된 쿼리 창의 스크린 샷](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    또한도 사용할 수 있습니다 hello 드롭 다운 메뉴 다음**전송** tooselect **고급**합니다. 고급 옵션을 사용 하면 추가 옵션 tooprovide hello 작업을 제출 하는 경우.

    ![스크립트 제출 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Hello 쿼리를 제출 하면 hello 작업 상태가 표시 됩니다. hello 작업 상태는 hadoop 처리는 hello 작업에 대 한 정보를 표시 합니다. **작업 상태** hello hello 작업 상태를 제공 합니다. hello 상태 새로 고침 아이콘 toorefresh hello를 수동으로 진행할 수 있습니다 또는 hello 상태는 주기적으로 업데이트 됩니다.

    ![작업 상태가 강조 표시된 작업 보기 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Hello 후 **작업 상태** 쪽 변경**마침**, 전달 된 비순환 그래프 (DAG) 표시 됩니다. 이 다이어그램에서는 hello 하이브 쿼리를 처리할 때 Tez에 의해 결정 된 hello 실행 경로 설명 합니다. Tez는 hello 로컬 클러스터에 Hive 위한 되는 hello 기본 실행 엔진입니다.

    > [!NOTE]
    > Tez는 Linux 기반 HDInsight 클러스터를 사용 하는 경우 hello 기본값 이기도 합니다. Windows 기반 HDInsight의 hello 기본 않습니다. toouse 것 hello 줄을 추가 해야 하는, `set hive.execution.engine = tez;` 하이브 쿼리 toohello 시작 합니다.

    사용 하 여 hello **작업 출력** tooview hello 출력을 연결 합니다. 이 경우,이 823 hello hello sample_08 테이블의 행 수입니다. Hello를 사용 하 여 hello 작업에 대 한 진단 정보를 볼 수 **작업 로그** 및 **YARN 로그 다운로드** 링크 합니다.

4. Hello를 변경 하 여 하이브 작업을 대화형으로 실행할 수도 있습니다 **일괄 처리** 너무 필드**Interactive'**합니다. **실행**을 선택합니다.

    ![대화형 및 실행 단추가 강조 표시된 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    스트림을 hello toohello 처리 중에 생성 된 출력 로그는 대화형 쿼리 **HiveServer2 출력** 창.

    > [!NOTE]
    > hello 정보는 hello hello에서 사용할 수 있는 동일한 **작업 로그** 작업이 완료 된 후 연결 합니다.

    ![출력 로그의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Hive 프로젝트 만들기

또한 여러 Hive 스크립트를 포함하는 프로젝트를 만들 수 있습니다. 스크립트와 관련 된 또는 버전 제어 시스템에 toostore 스크립트를 원하는 경우 프로젝트를 사용 합니다.

1. Visual Studio에서 **파일**, **새로 만들기** 및 **프로젝트**를 차례로 선택합니다.

2. 프로젝트의 hello 목록에서 확장 **템플릿**, 확장 **Azure 데이터 레이크**를 선택한 후 **하이브 (HDInsight)**합니다. Hello 템플릿 목록에서 선택 **하이브 샘플**합니다. 이름과 위치를 입력한 다음 **확인**을 선택합니다.

    ![Azure Data Lake, HIVE, Hive 예제 및 확인이 강조 표시된 새 프로젝트 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

hello **하이브 샘플** 프로젝트에 두 개의 스크립트 **WebLogAnalysis.hql** 및 **SensorDataAnalysis.hql**합니다. 이러한 스크립트를 사용 하 여 hello 동일 제출할 수 **전송** hello hello 창 위쪽에 단추입니다.

## <a name="create-a-pig-project"></a>Pig 프로젝트 만들기

Hive에서는 구조화된 데이터로 작업하기 위한 SQL과 유사한 쿼리 언어(HiveQL)를 제공하지만 Pig는 데이터에 대한 변환을 수행하는 방식으로 작동합니다. Pig 변환의 파이프라인 toodevelop를 허용 하는 언어 (Pig 라틴 문자)를 제공 합니다. toouse Pig hello 로컬 클러스터와 다음이 단계를 따르십시오.

1. Visual Studio를 열고 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다. 프로젝트의 hello 목록에서 확장 **템플릿**, 확장 **Azure 데이터 레이크**를 선택한 후 **Pig (HDInsight)**합니다. Hello 템플릿 목록에서 선택 **Pig 응용 프로그램**합니다. 이름과 위치를 입력한 다음 **확인**을 선택합니다.

    ![Azure Data Lake, Pig, Pig 예제 및 확인이 강조 표시된 새 프로젝트 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. 콘텐츠로 사용 hello hello 텍스트를 다음 hello 입력 **script.pig** 이 프로젝트를 사용 하 여 만든 파일입니다.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    다른 언어를 사용 하 여 하이브 보다 Pig, hello 작업을 실행 하는 방법에 일관성이 hello 통해 두 언어 간 **전송** 단추입니다. 선택 hello 옆에 있는 드롭 다운 **전송** Pig에 대 한 고급 전송 대화 상자를 표시 합니다.

    ![스크립트 제출 대화 상자의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. hello 작업 상태 및 출력도 표시 됩니다, 그리고 Hive 쿼리도 hello 동일 합니다.

    ![완료된 Pig 작업의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>작업 보기

데이터 레이크 도구 tooeasily Hadoop에서 실행 된 작업에 대 한 정보 보기 수 있습니다. Hello 로컬 클러스터에서 실행 하는 단계 toosee hello 작업을 수행 하는 hello를 사용 합니다.

1. **서버 탐색기**를 hello 로컬 클러스터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **작업 보기**합니다. 제출 된 toohello 클러스터 된 작업 목록이 표시 됩니다.

    ![작업 보기가 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. 작업의 hello 목록에서 하나를 선택 tooview hello에 대 한 작업 세부 정보.

    ![스크린샷의 작업을 사용 하 여 브라우저 강조 표시 하는 hello 작업 중 하나](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    비슷한 toowhat 링크 tooview hello 출력 및 로그 정보를 포함 하 여 하이브 또는 Pig 쿼리를 실행 한 후 참조에 hello 정보가 표시 됩니다.

3. 또한 수정할 수 있으며 여기에서 hello 작업을 다시 제출 하십시오.

## <a name="view-hive-databases"></a>Hive 데이터베이스 보기

1. **서버 탐색기**, hello 확장 **HDInsight 로컬 클러스터** 항목을 확장 한 후 **하이브 데이터베이스**합니다. hello **기본** 및 **xademo** 데이터베이스 hello 로컬 클러스터에 표시 됩니다. 데이터베이스를 확장할 hello 데이터베이스 내에서 hello 테이블을 보여 줍니다.

    ![데이터베이스가 확장된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. 테이블을 확장에 해당 테이블에 대 한 hello 열이 표시 됩니다. tooquickly 뷰 hello 데이터 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **보기 Top 100 Rows**합니다.

    ![테이블이 확장되고 상위 100개 행 보기가 선택된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>데이터베이스 및 테이블 속성

데이터베이스 또는 테이블의 hello 속성을 볼 수 있습니다. 선택 하면 **속성** hello 속성 창에서 선택한 hello 항목에 대 한 세부 정보를 표시 합니다. 예를 들어 hello 스크린 샷 뒤에 표시 된 hello 정보 참조:

![속성 창의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>테이블 만들기

toocreate 테이블을 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **Create Table**합니다.

![테이블 만들기가 강조 표시된 서버 탐색기의 스크린샷](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

그런 다음 폼을 사용 하는 hello 테이블을 만들 수 있습니다. 다음 스크린 샷 hello의 hello 맨 아래에 볼 수 있습니다는 사용 되는 toocreate hello 테이블 원시 HiveQL hello 합니다.

![Toocreate 테이블을 사용 하는 hello 폼의 스크린 샷](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>다음 단계

* [Hello Hortonworks 샌드박스의 hello ropes 학습](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop 자습서 - HDP 시작](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
