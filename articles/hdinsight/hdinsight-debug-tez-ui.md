---
title: "Windows 기반 HDInsight-Azure와 Tez UI aaaUse | Microsoft Docs"
description: "Windows 기반 HDInsight HDInsight에서 toouse hello Tez UI toodebug Tez 작업 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Windows 기반 HDInsight의 hello Tez I toodebug Tez 작업을 사용 하 여
hello Tez UI는 Windows 기반 HDInsight 클러스터에서 hello 실행 엔진으로 Tez를 사용 하는 사용 되는 toounderstand 및 디버그 작업이 될 수 있는 웹 페이지입니다. hello Tez UI 있습니다 toovisualize hello 작업이 연결 된 항목에 대 한 그래프는 각 항목을 더 자세히 분석 하 고 통계 및 로깅 정보를 검색 합니다.

> [!IMPORTANT]
> 이 문서의 단계 hello 창을 사용 하 여 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
* Windows 기반 HDInsight 클러스터입니다. 새 클러스터를 만드는 단계는 [Windows 기반 HDInsight 사용 시작](hdinsight-hadoop-tutorial-get-started-windows.md)을 참조하세요.

  > [!IMPORTANT]
  > hello Tez UI은 2016 년 2 월 8 일 이후 만들어진 Windows 기반 HDInsight 클러스터에서 사용할 수만 있습니다.
  >
  >
* Windows 기반 원격 데스크톱 클라이언트입니다.

## <a name="understanding-tez"></a>Tez 이해
Tez는 기존의 MapReduce 처리보다 빠른 속도를 제공하는 Hadoop의 데이터 처리에 대해 확장 가능한 프레임워크입니다. Windows 기반 HDInsight 클러스터에 대 한는 hello 하이브 쿼리의 일환으로 다음 명령을 사용 하 여 하이브에 사용할 수 있는 선택적 엔진:

    set hive.execution.engine=tez;

작업이 제출 된 tooTez 때 전달 된 비순환 그래프 (DAG) hello hello 작업에서 요구 하는 hello 작업의 실행 순서를 설명 하는 만듭니다. 개별 작업 꼭지점 라고 하며 실행 hello에 조각의 전체 작업 합니다. hello 꼭지점에서 설명 하는 hello 작업의 실제 실행 작업을 라고 및 hello 클러스터의 여러 노드에 배포할 수 있습니다.

### <a name="understanding-hello-tez-ui"></a>이해 hello Tez UI
hello Tez UI는 웹 페이지에서 제공 하는 현재 실행 중이거나 있어야 하는 프로세스에 대 한 정보는 Tez를 사용 하 여 이전에 실행 합니다. Tooview hello Tez에 의해 생성 된 DAG 허용 즉, 작업 및 꼭 짓 점, 오류 정보에서 사용 하는 메모리 카운터, 클러스터 간에 배포 합니다. Hello 다음 시나리오에에서 유용한 정보를 제공할 수 있습니다.

* 장기 실행 프로세스, 보기 모니터링 hello 지도의 진행률 및 감소 작업 합니다.
* 실패 한 이유 또는 처리 개선할 수 있는 방법을 toolearn 성공 또는 실패 한 프로세스에 대 한 데이터를 분석 합니다.

## <a name="generate-a-dag"></a>DAG 생성
hello Tez UI 사용 하는 작업 hello Tez 엔진이 현재 실행 중이거나 hello 이전에 실행 된 경우에 데이터를 포함 됩니다. 간단한 Hive 쿼리는 Tez를 사용하지 않고 해결될 수 있지만 필터링, 그룹화, 정렬, 조인 등을 수행하는 복잡한 쿼리는 Tez가 필요합니다.

다음 단계 toorun Tez를 사용 하 여를 실행 하는 하이브 쿼리 hello를 사용 합니다.

1. 웹 브라우저에서 탐색 toohttps://CLUSTERNAME.azurehdinsight.net, 여기서 **CLUSTERNAME** HDInsight 클러스터의 hello 이름입니다.
2. Hello hello 페이지의 hello 위쪽 메뉴에서 선택 hello **하이브 편집기**합니다. 다음 예제 쿼리에서 hello로는 페이지가 표시 됩니다.

        Select * from hivesampletable

    Hello 예제 쿼리를 지우고 hello 다음과 같이 바꿉니다.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. 선택 hello **전송** 단추입니다. hello **작업 세션** hello 페이지의 hello 아래쪽 섹션에는 hello 쿼리의 hello 상태가 표시 됩니다. 한 번만 상태가 변경 될 너무 hello**완료 됨**선택, hello **세부 정보 보기** tooview hello 결과 연결 합니다. hello **작업 출력** toohello 다음과 유사 합니다.

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Hello Tez UI를 사용 하 여
> [!NOTE]
> hello Tez UI 에서만 사용 가능 hello 클러스터 헤드 노드 hello 바탕 화면에서 원격 데스크톱 tooconnect toohello 헤드 노드를 사용 해야 합니다.
>
>

1. Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터를 선택 합니다. Hello HDInsight 블레이드의 hello 위에서 hello 선택 **원격 데스크톱** 아이콘입니다. 원격 데스크톱 블레이드 hello 표시 됩니다.

    ![원격 데스크톱 아이콘](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. Hello 원격 데스크톱 블레이드에서 선택 **연결** tooconnect toohello 클러스터 헤드 노드. 메시지가 표시 되 면 hello 클러스터 원격 데스크톱 사용자 이름 및 암호 tooauthenticate hello 연결을 사용 합니다.

    ![원격 데스크톱 연결 아이콘](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > 원격 데스크톱 연결을 설정 하지 않은 경우 사용자 이름, 암호 및 만료 날짜를 입력 한 다음 선택 **사용** tooenable 원격 데스크톱입니다. 이 활성화 된 이전 단계 tooconnect hello를 사용 합니다.
   >
   >
3. 연결 되 면 hello 원격 데스크톱을 hello 오른쪽 상단의 hello 브라우저에서 선택 hello 기어 아이콘에서 Internet Explorer를 열고 선택한 후 **호환성 보기 설정**합니다.
4. Hello 아래에서 **호환성 보기 설정**일반 hello에 대 한 확인란 **호환성 보기에서 인트라넷 사이트 표시** 및 **호환성 목록을 사용 하 여 Microsoft**, 선택한 후 **닫기**합니다.
5. Internet Explorer에서 toohttp://headnodehost:8188 찾아보기/tezui / #/ 합니다. Hello Tez UI가 표시 됩니다.

    ![Tez UI](./media/hdinsight-debug-tez-ui/tezui.png)

    Hello Tez UI가 로드 될 때 현재 실행 중인 이거나 받아야 하는 Dag 목록이 hello 클러스터에서 실행 표시 됩니다. hello 기본 보기에는 hello Dag 이름, Id, 제출자, 상태, 시작 시간, 종료 시간, 기간, 응용 프로그램 ID 및 큐 포함 되어 있습니다. Hello hello 페이지의 오른쪽에 hello 기어 아이콘을 사용 하 여 더 많은 열을 추가할 수 있습니다.

    항목이 하나만 있는 경우 hello 이전 섹션에서를 실행 하는 hello 쿼리의 됩니다. 항목이 여러 개 있는 경우에 Dag hello 위에 hello 필드에 검색 조건을 입력 하 여 검색 다음 도달할 수 있습니다 **Enter**합니다.
6. 선택 hello **Dag 이름** hello 가장 최근의 DAG 항목에 대 한 합니다. 이 hello 옵션 toodownload DAG hello에 대 한 정보를 포함 하는 JSON 파일의 zip DAG hello에 대 한 정보가 표시 됩니다.

    ![DAG 세부 정보](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Hello 위에 **DAG 세부 정보** DAG hello에 대 한 정보를 사용 하는 toodisplay 수 있는 몇 가지 링크 됩니다.

   * **DAG 카운터**는 해당 DAG에 대한 카운터 정보를 표시합니다.
   * **그래픽 보기**는 해당 DAG의 그래픽 표시를 나타냅니다.
   * **모든 꼭 짓 점에** 이 DAG에 hello 꼭지점 목록이 표시 됩니다.
   * **모든 작업** 이 DAG에 모든 꼭 짓 점에 대해 hello 작업 목록이 표시 됩니다.
   * **모든 TaskAttempts** hello에 대 한 정보를 표시가이 DAG에 toorun 작업을 시도 합니다.

     > [!NOTE]
     > 있으며 tooview 링크 꼭지점, 작업 및 TaskAttempts에 대 한 hello 열 표시 스크롤하면 **카운터** 및 **보거나 로그를 다운로드할** 각 행에 대 한 합니다.
     >
     >

     Hello 작업과 오류가 발생 한, hello DAG 세부 정보는 실패 상태를 hello 실패 한 작업에 대 한 링크 tooinformation 함께 표시 됩니다. 진단 정보는 hello DAG 세부 정보 아래에 표시 됩니다.
8. **그래픽 보기**를 선택합니다. Hello DAG 그래픽으로 표시 됩니다. Hello에 대 한 toodisplay 정보 보기에서에서 각 꼭 짓 점 위로 마우스 hello를 배치할 수 있습니다.

    ![그래픽 보기](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. 꼭 짓 점 클릭 하면 hello가 로드 **꼭지점 정보** 해당 항목에 대 한 합니다. Hello 클릭 **지도 1** 이 항목에 대 한 꼭지점 toodisplay 정보입니다. 선택 **확인** tooconfirm hello 탐색 합니다.

    ![꼭짓점 세부 정보](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Note 해야 한다는 관련된 toovertices 및 작업 하는 hello hello 페이지 위쪽에 링크 합니다.

    > [!NOTE]
    > 너무 다시 이동 하 여이 페이지에도 도착할 수 있습니다**DAG 세부 정보**선택한 **꼭지점 정보**, hello를 선택 하 고 **지도 1** 꼭 짓 점입니다.
    >
    >

    * **꼭짓점 카운터**는 이 꼭짓점에 대한 카운터 정보를 표시합니다.
    * **태스크**는 이 꼭짓점에 대한 태스크를 표시합니다.
    * **작업 시도** 이 꼭 짓이 점에 대해 시도 toorun 작업에 대 한 정보를 표시 합니다.
    * **원본 및 싱크**는 이 꼭짓점에 대한 데이터 원본 및 싱크를 표시합니다.

      > [!NOTE]
      > Hello 이전 메뉴와 작업에 대 한 hello 열 디스플레이 스크롤하면 수, 작업 시도 및 소스 & Sinks__ toodisplay 각 항목에 대 한 toomore 정보를 연결 합니다.
      >
      >
11. 선택 **작업**, 선택 hello 항목 명명 된 다음 **00_000000**합니다. 이 태스크에 대한 **태스크 세부 정보**를 표시합니다. 이 화면에서 **태스크 카운터** 및 **태스크 시도**를 볼 수 있습니다.

    ![태스크 세부 정보](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>다음 단계
이제 toouse hello Tez 보는 방법을 배웠습니다를 보다 자세히 배울에 대 한 [를 사용 하 여 HDInsight의 Hive](hdinsight-use-hive.md)합니다.

Tez 대 한 기술 정보를 자세한 참조 hello [Hortonworks Tez 페이지](http://hortonworks.com/hadoop/tez/)합니다.
