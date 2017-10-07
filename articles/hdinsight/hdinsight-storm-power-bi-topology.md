---
title: "Power bi-Azure HDInsight의 Apache Storm aaaUse | Microsoft Docs"
description: "HDInsight의 Apache Storm 클러스터에서 실행 중인 C# 토폴로지로부터 데이터를 사용하여 Power BI 보고서를 만듭니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Apache Storm 토폴로지에서 Power BI toovisualize 데이터 사용

Power BI 보고서로 데이터를 표시 하는 toovisually를 허용 합니다. 이 문서는 방법의 예에서는 Power BI에 대 한 HDInsight toogenerate 데이터에서 Apache Storm toouse 합니다.

> [!NOTE]
> hello이 문서의 단계에 의존 Visual Studio와 함께 Windows 개발 환경입니다. hello 컴파일된 프로젝트 제출 된 tooa Linux 기반 HDInsight 클러스터 될 수 있습니다. 2016년 10월 28일 이후 생성된 Linux 기반 클러스터만 SCP.NET 토폴로지를 지원합니다.
>
> Linux 기반 클러스터에서 업데이트 hello 프로젝트 tooversion 0.10.0.6 프로그램에서 사용 되는 또는 더 높은 Microsoft.SCP.Net.SDK NuGet 패키지는 C# 토폴로지 toouse 합니다. 또한 hello 버전의 hello 패키지 hello HDInsight에 설치 된 Storm의 주 버전을 일치 해야 합니다. 예를 들어 HDInsight에서 Storm 버전 3.3 및 3.4는 Storm 버전 0.10.x를 사용하는 반면, HDInsight 3.5는 Storm 1.0.x를 사용합니다.
>
> Linux 기반 클러스터에서 C# 토폴로지는.NET 4.5를 사용 하 고 모노 toorun hello HDInsight 클러스터에서 사용 해야 합니다. 대부분의 항목이 작동합니다. 하지만 Hello를 확인 해야 [모노 호환성](http://www.mono-project.com/docs/about-mono/compatibility/) 잠재적인 호환성 문제에 대 한 문서입니다.
>
> Linux 기반 또는 Windows 기반 HDInsight로 작동하는 이 프로젝트의 Java 버전에 대해서는 [HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리(Java)](hdinsight-storm-develop-java-event-hub-topology.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

* [Power BI](https://powerbi.com) 액세스 권한이 있는 Azure Active Directory 사용자
* HDInsight 클러스터. 자세한 내용은 [HDInsight에서 Storm 시작](hdinsight-apache-storm-tutorial-get-started-linux.md)을 참조하세요.

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* Visual Studio (hello 버전을 다음 중 하나)

  * Visual Studio 2012 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=44921) 또는 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017(모든 버전)

* Visual Studio 용 HDInsight 도구 hello: 참조 [hello HDInsight 도구를 사용 하 여 Visual Studio 용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) 설치 정보에 대 한 내용은 합니다.

## <a name="how-it-works"></a>작동 방법

이 예제에서는 IIS(인터넷 정보 서비스) 로그 데이터를 무작위로 생성하는 C# Storm 토폴로지를 포함합니다. 이 데이터 tooa SQL 데이터베이스에 기록 되며 여기에서 Power BI에서 사용 되는 toogenerate 보고서 있습니다.

이 예의 파일 구현 hello 주요 기능을 다음 hello:

* **SqlAzureBolt.cs**: hello 스톰 토폴로지 tooSQL 데이터베이스에서에서 생성 한 정보를 씁니다.
* **IISLogsTable.sql**: hello 데이터에 저장 되어 있는 hello Transact SQL 문 사용 toogenerate hello 데이터베이스입니다.

> [!WARNING]
> SQL 데이터베이스에서 HDInsight 클러스터에서 hello 토폴로지를 시작 하기 전에 hello 테이블을 만듭니다.

## <a name="download-hello-example"></a>Hello 예제를 다운로드 합니다.

Hello 다운로드 [HDInsight C# 스톰 Power BI 예제](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi)합니다. toodownload, 하거나 포크/복제를 사용 하 여 [git](http://git-scm.com/), 하거나 hello를 사용 하 여 **다운로드** 링크 toodownload hello 보관의.zip 합니다.

## <a name="create-a-database"></a>데이터베이스 만들기

1. 데이터베이스 toocreate hello 단계를 사용 하 여 hello에 [SQL 데이터베이스 자습서](../sql-database/sql-database-get-started.md) 문서.

2. Hello에서 단계를 다음 hello 하 여 연결 toohello 데이터베이스 [Visual Studio를 사용 하 여 tooa SQL 데이터베이스 연결](../sql-database/sql-database-connect-query.md) 문서.

3. 개체 탐색기에서 hello 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 **새 쿼리**합니다. Hello의 hello 내용 붙여넣기 **IISLogsTable.sql** hello에 포함 된 파일 hello 쿼리 창에 프로젝트를 다운로드 한 다음 Ctrl + Shift + E tooexecute hello 쿼리 합니다. Hello 명령을 성공적으로 완료 하는 메시지를 받아야 합니다.

## <a name="configure-hello-sample"></a>Hello 샘플 구성

1. Hello에서 [Azure 포털](https://portal.azure.com), SQL 데이터베이스를 선택 합니다. Hello에서 **Essentials** hello SQL 데이터베이스 블레이드, 선택의 섹션 **데이터베이스 연결 문자열 표시**합니다. Hello 목록이 표시 되 면 복사 hello **ADO.NET (SQL 인증)** 정보입니다.

2. Visual Studio에서 hello 샘플을 엽니다. **솔루션 탐색기**개방형 hello **App.config** 파일을 선택한 다음 hello 다음 항목을 찾습니다.

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Hello 대체 **# # TOBEFILLED # #** hello 이전 단계에서 복사한 값 hello 데이터베이스 연결 문자열을 사용 합니다. 대체 **{프로그램\_사용자 이름}** 및 **{프로그램\_암호}** hello 이름과 hello 데이터베이스에 대 한 암호입니다.

3. 저장 하 고 hello 파일을 닫습니다.

## <a name="deploy-hello-sample"></a>Hello 예제 배포

1. **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **StormToSQL** 프로젝트를 마우스 선택 **HDInsight의 tooStorm 제출**합니다. Hello에서 HDInsight 클러스터를 선택 hello **Storm 클러스터** 드롭다운 대화입니다.

   > [!NOTE]
   > Hello에 대 한 몇 초 정도 **Storm 클러스터** 드롭다운 toopopulate 서버 이름으로 합니다.
   >
   > 메시지가 표시 되 면 Azure 구독에 대 한 hello 로그인 자격 증명을 입력 합니다. 구독이 둘 이상 있는 경우 프로그램 스톰 HDInsight 클러스터에 포함 된 toohello에 로그인 합니다.

2. Hello 토폴로지가 제출 될 때 hello __토폴로지 뷰어__ 나타납니다. tooview이 토폴로지, hello 목록에서 선택 hello SqlAzureWriterTopology 항목입니다.

    ![선택한 hello 토폴로지 hello 토폴로지](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    이 보기 toosee 정보를 사용 하 여 hello 토폴로지에서 하거나 hello 토폴로지는 항목 (예: hello SqlAzureBolt) toosee 정보 특정 tooa 구성 요소를 두 번 클릭 수 있습니다.

3. Hello 후 토폴로지 실행 몇 분 동안 반환 toohello SQL 쿼리 창 toocreate hello 데이터베이스를 사용 합니다. 다음 쿼리에서 hello hello 기존 문을 바꿉니다.

        select * from iislogs;

    Ctrl + Shift를 사용 하 여 + E tooexecute hello 쿼리의 결과 유사한 toohello 같은 데이터가 수신 해야 합니다.

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    이 데이터 hello 스톰 토폴로지에서 작성 되었습니다.

## <a name="create-a-report"></a>보고서 만들기

1. Toohello 연결 [Azure SQL 데이터베이스 커넥터](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) Power BI에 대 한 합니다. 

2. **데이터베이스** 내에서 **가져오기**를 선택합니다.

3. **Azure SQL Database**를 선택한 다음 **연결**을 선택합니다.

    > [!NOTE]
    > Toodownload hello Power BI Desktop toocontinue를 메시지가 나타날 수 있습니다. 이 경우 다음 단계 tooconnect hello를 사용 합니다.
    >
    > 1. Power BI Desktop을 열고 __Get Data__를 선택합니다.
    > 2  __Azure__를 선택한 다음 __Azure SQL Database__를 선택합니다.

4. Hello 정보 tooconnect tooyour Azure SQL 데이터베이스를 입력 합니다. Hello를 방문 하 여이 정보를 찾을 수 [Azure 포털](https://portal.azure.com) SQL 데이터베이스를 선택 하 고 있습니다.

   > [!NOTE]
   > 사용 하 여 사용자 지정 필터 및 hello 새로 고침 간격을 설정할 수도 있습니다 **고급 옵션을 사용 하도록 설정** hello에서 대화를 연결 합니다.

5. 를 연결한 후 새 데이터 집합 이름과 같은 이름을 hello 데이터베이스에 연결 하는 hello로 표시 됩니다. Hello dataset toobegin 보고서 디자인을 선택 합니다.

6. **필드**, hello 확장 **IISLOGS** 항목입니다. hello 확인란을 선택 하는 보고서 목록 hello URI는 형태소 분석 toocreate **URISTEM**합니다.

    ![보고서 만들기](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. 다음으로 끌어 **메서드** toohello 보고서입니다. hello 보고서 업데이트 toolist hello 생기고 hello 해당 HTTP 메서드 hello HTTP 요청에 사용 됩니다.

    ![hello 메서드 데이터를 추가합니다.](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Hello에서 **시각화** 열, 선택 hello **필드** 아이콘을 선택한 후 hello 아래쪽 화살표 옆 너무**메서드** hello에 **값**섹션. URI에 몇 번의 개수에 액세스 하는 toodisplay 선택 **Count**합니다.

    ![메서드의 tooa 수 변경](./media/hdinsight-storm-power-bi-topology/count.png)

9. Hello를 다음으로, 선택 **누적 세로 막대형 차트** toochange 어떻게 hello 정보가 표시 됩니다.

    ![변경 tooa 누적된 차트](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. 선택 toosave hello 보고서 **저장** hello 보고서에 대 한 이름을 입력 합니다.

## <a name="stop-hello-topology"></a>Hello 토폴로지를 중지 합니다.

hello 토폴로지는 중지 하거나 hello 스톰 HDInsight 클러스터에서 삭제 될 때까지 toorun를 계속 합니다. toostop은 토폴로지 hello에 hello 다음 단계를 수행 합니다.

1. Visual Studio에서 toohello 토폴로지 뷰어를 반환 하 고 hello 토폴로지를 선택 합니다.

2. 선택 hello **Kill** 단추 toostop hello 토폴로지입니다.

    ![Kill hello 토폴로지 요약에서 단추](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>클러스터 삭제

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>다음 단계

이 문서에서 배운 어떻게 스톰 토폴로지 tooSQL 데이터베이스에서에서 toosend 데이터를 시각화 하 여 Power BI를 사용 하 여 hello 데이터입니다. 방법에 대 한 HDInsight에서 Storm를 사용 하 여 다른 Azure 기술로 toowork hello 다음 문서를 참조 하세요.

* [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)
