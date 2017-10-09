---
title: "HDInsight에서 HBase 스톰와 시간이 지남에 따라 aaaCorrelate 이벤트"
description: "자세한 내용은 방법 HDInsight의 Storm 및 HBase를 사용 하 여 서로 다른 시간에 도착 하는 toocorrelate 이벤트입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Storm 및 HBase를 사용하여 다른 시간에 도착하는 이벤트의 상관 관계 지정

Apache Storm으로 영구적인 데이터 저장소를 사용하여 다른 시간에 도착하는 데이터 항목의 상관 관계를 지정할 수 있습니다. 예를 들어 사용자 세션 toocalculate에 대 한 로그인 및 로그 아웃 이벤트 시간 hello 세션 어떻게 연결 동안 지속 됩니다.

이 문서에 알아봅니다 어떻게 toocreate 사용자 세션에 대 한 로그인 및 로그 아웃 이벤트를 추적 하 고 hello hello 세션 기간을 계산 하는 기본 C# 스톰 토폴로지입니다. hello 토폴로지는 영구 데이터 저장소도 HBase를 사용합니다. HBase 통해 수도 tooperform 일괄 처리 쿼리 추가로 insights를 tooproduce hello 기록 데이터에 있습니다. 예를 들면 특정 기간에 얼마나 많은 사용자 세션이 시작 또는 종료했는지와 같은 정보입니다.

## <a name="prerequisites"></a>필수 조건

* Visual Studio 용 HDInsight 도구는 visual Studio 및 hello 합니다. 자세한 내용은 참조 [hello HDInsight 도구를 사용 하 여 Visual Studio 용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.

* HDInsight 클러스터의 Apache Storm(Windows 기반).

  > [!WARNING]
  > SCP.NET 토폴로지는 2016 년 10 월 28 일 후에 만든 Linux 기반 Storm 클러스터에서 지원 되지만, 10/28/2016부터 사용할 수는.NET 패키지에 대 한 hello HBase SDK 올바로 작동 하지 않는 Linux 기반 HDInsight의

* HDInsight 클러스터에서 Apache HBase(Linux 또는 Windows 기반)

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* 개발 환경에서 [Java](https://java.com) 1,7 이상 - Java 제출 된 toohello HDInsight 클러스터를 되었을 때 사용 되는 toopackage hello 토폴로지는입니다.

  * hello **JAVA_HOME** Java 포함 되어 있는 환경 변수 해야 지점 toohello 디렉터리입니다.
  * hello **%JAVA_HOME%/bin** 디렉터리 hello 경로에 있어야 합니다.

## <a name="architecture"></a>아키텍처

![Hello 토폴로지를 통해 hello 데이터 흐름 다이어그램](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

이벤트의 상관 관계 지정 hello 이벤트 소스에 대 한 공통 식별자가 필요 합니다. 예를 들어 사용자 ID, 세션 ID 또는 기타 데이터의 되는) 고유 하 고 b) 모든 전송 되는 데이터 tooStorm에 포함 된. 이 예에서는 GUID 값 toorepresent 세션 id입니다.

이 예제는 다음 두 개의 HDInsight 클러스터로 이루어져 있습니다.

* HBase: 기록 데이터에 대한 영구 데이터 저장소
* Storm: tooingest 들어오는 데이터를 사용합니다.

hello 데이터 hello 스톰 토폴로지에서 임의로 생성 하 고 다음 항목 hello 구성:

* 세션 ID: 각 세션을 고유하게 식별하는 GUID
* 이벤트: 이벤트 시작(START) 또는 종료(END) 이 예에서는 START가 항상 END 전에 발생합니다.
* Hello 이벤트의 시간: hello 시간입니다.

이 데이터는 HBase에서 처리 및 저장됩니다.

### <a name="storm-topology"></a>Storm 토폴로지

세션이 시작 되는 **시작** 이벤트 hello 토폴로지에서 수신 되 고 tooHBase를 기록 합니다. 때는 **끝** 이벤트를 받을, hello 토폴로지 검색 hello **시작** 이벤트 hello 두 이벤트는 hello 간격을 계산 합니다. 이 **기간** HBase에 다음 값이 저장 hello 함께 **끝** 이벤트 정보입니다.

> [!IMPORTANT]
> 이 토폴로지 hello 기본 패턴에서 설명 하는 동안 프로덕션 솔루션 hello 다음 시나리오에 대 한 tootake 디자인이 필요 합니다.
>
> * 이벤트가 잘못된 순서로 도착
> * 중복된 이벤트
> * 삭제된 이벤트

hello 샘플 토폴로지 다음과 같은 구성 요소가 hello로 이루어져 있습니다.

* Session.cs: 시작 시간과 기간 hello 세션 지속 임의 세션 ID를 만들어 사용자 세션을 시뮬레이션 합니다.

* Spout.cs: 100 세션을 만들어, 시작 이벤트를 내보냅니다, 그리고 각 세션의 hello 임의 시간 초과 될 때까지 대기 및 종료 이벤트를 내보냅니다. 그런 다음 재활용 세션 toogenerate를 새로 종료 되었습니다.

* HBaseLookupBolt.cs: hello 세션 ID toolook HBase에서 세션 정보를 사용합니다. 종료 이벤트를 처리할 때 해당 시작 이벤트 hello 찾아서 hello hello 세션 기간을 계산 합니다.

* HBaseBolt.cs: HBase에 정보를 저장합니다.

* TypeHelper.cs: 형식 변환에서 읽기 / 쓰기 tooHBase 경우에 도움이 됩니다.

### <a name="hbase-schema"></a>HBase 스키마

HBase에서 다음 스키마/설정 hello로 hello 데이터는 테이블에 저장 됩니다.

* 행 키: hello 세션 ID가이 테이블의 행에 대 한 hello 키로 사용 합니다.

* 열 제품군: hello 성이 'cf'. 이 제품군에 저장되는 열은:

  * 이벤트: START 또는 END

  * 시간: hello 시간 (밀리초) hello 이벤트 발생 했습니다.

  * 기간: hello 시작 및 종료 이벤트 사이의 길이입니다.

* 버전: hello 'cf' 제품군에는 각 행의 버전 5 tooretain 설정 됩니다.

  > [!NOTE]
  > 버전은 특정 행의 키에 대해 저장된 이전 값의 로그입니다. 기본적으로 HBase hello 행의 가장 최신 버전에 대 한 hello 값만 반환합니다. 이 경우 hello 같은 행은 이벤트에 사용 모든 (시작, 종료 됩니다.)는 행의 각 버전 hello 타임 스탬프 값으로 식별 됩니다. 버전은 특정 ID에 대해 기록된 이벤트의 기록 보기를 제공합니다.

## <a name="download-hello-project"></a>Hello 프로젝트 다운로드

hello 예제 프로젝트에서 다운로드할 수 있습니다 [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation)합니다.

이 다운로드는 다음 C# 프로젝트 hello를 포함 되어 있습니다.

* CorrelationTopology: 사용자 세션에 대해 시작 및 종료 이벤트를 임의로 내보내는 C# Storm 토폴로지입니다. 각 세션은 1분에서 5분 사이까지 지속됩니다.

* SessionInfo: C# 콘솔 응용 프로그램 hello HBase 테이블을 만들고 tooreturn 정보 저장 된 세션 데이터에 대 한 쿼리 예제를 제공 합니다.

## <a name="create-hello-table"></a>Hello 테이블 만들기

1. 열기 hello **SessionInfo** Visual Studio에서 프로젝트.

2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **SessionInfo** 프로젝트를 마우스 선택 **속성**합니다.

    ![선택한 속성을 가진 메뉴의 스크린샷](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. 선택 **설정을**, 집합 hello 다음 값에는 다음:

   * HBaseClusterURL: hello URL tooyour HBase 클러스터입니다. 예를 들어 https://myhbasecluster.azurehdinsight.net입니다.

   * 클러스터에 대해 HBaseClusterUserName: hello 관리자/HTTP 사용자 계정

   * HBaseClusterPassword: hello hello 관리자/HTTP 사용자 계정의 암호를

   * 이 예제와 hello 테이블 toouse의 HBaseTableName: hello 이름

   * HBaseTableColumnFamily: hello 열 제품군 이름

     ![설정 대화 상자 이미지](./media/hdinsight-storm-correlation-topology/settings.png)

4. Hello 솔루션을 실행 합니다. 대화 상자가 나타나면 HBase 클러스터에 hello 'c' 키 toocreate hello 테이블을 선택 합니다.

## <a name="build-and-deploy-hello-storm-topology"></a>빌드 및 배포 hello 스톰 토폴로지

1. 열기 hello **CorrelationTopology** Visual Studio에서 솔루션입니다.

2. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **CorrelationTopology** 프로젝트 속성을 선택 합니다.

3. Hello 속성 창에서 선택 **설정** 이 프로젝트에 대 한 hello 구성 값을 입력 합니다. hello 처음 5는 hello에서 동일한 값이 사용 하는 hello **SessionInfo** 프로젝트:

   * HBaseClusterURL: hello URL tooyour HBase 클러스터입니다. 예를 들어 https://myhbasecluster.azurehdinsight.net입니다.

   * Hello 관리자/HTTP 사용자 계정을 클러스터에 대해 HBaseClusterUserName: 하 고 있습니다.

   * HBaseClusterPassword: hello hello 관리자/HTTP 사용자 계정의 암호입니다.

   * 이 예제와 hello 테이블 toouse의 HBaseTableName: hello 이름입니다. 이 값이 동일한 hello은 hello SessionInfo 프로젝트에서 사용 되는 테이블 이름입니다.

   * HBaseTableColumnFamily: hello 열 패밀리 이름입니다. 이 값이 동일한 hello은 hello SessionInfo 프로젝트에서 사용 되는 열 제품군 이름입니다.

   > [!IMPORTANT]
   > Hello 기본값은에서 사용 하는 hello 이름으로 HBaseTableColumnNames, hello를 변경 하지 않는 **SessionInfo** tooretrieve 데이터입니다.

4. Hello 속성을 저장 한 후 hello 프로젝트를 빌드하십시오.

5. **솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **HDInsight의 tooStorm 제출**합니다. 메시지가 표시 되 면 Azure 구독에 대 한 hello 자격 증명을 입력 합니다.

   ![이미지의 hello toostorm 메뉴 항목 제출](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. Hello에 **제출 토폴로지** 대화 상자에서 선택 hello Storm 클러스터 toodeploy이이 토폴로지를 선택 합니다.

   > [!NOTE]
   > hello 토폴로지를 전송 하는 처음으로 걸릴 수 있습니다 몇 초 정도 HDInsight 클러스터의 tooretrieve hello 이름입니다.

7. Hello 토폴로지 toohello 업로드 및 제출 된 클러스터, 되 면 hello **스톰 토폴로지 보기** 열리고 토폴로지를 실행 하는 hello 표시 됩니다. toorefresh hello 데이터 선택 hello **CorrelationTopology** hello hello 새로 고침 단추를 사용 하 여 hello 페이지의 오른쪽 위에 있습니다.

   ![Hello 토폴로지 보기의 이미지](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Hello 토폴로지 데이터 생성을 시작할 때 hello hello 값 **Emitted** 열 씩 증가 합니다.

   > [!NOTE]
   > 경우 hello **스톰 토폴로지 보기** 자동으로 열리지, 사용 되지 않는 단계 tooopen 다음 hello:
   >
   > 1. **솔루션 탐색기**에서 **Azure**를 확장하고 **HDInsight**를 확장합니다.
   > 2. 토폴로지 hello 마우스 오른쪽 단추로 클릭 hello Storm 클러스터를 실행 하 고 다음 선택 **스톰 토폴로지 보기**

## <a name="query-hello-data"></a>Hello 데이터 쿼리

데이터를 내보낸 후 다음 단계 tooquery hello 데이터 hello를 사용 합니다.

1. Toohello 반환 **SessionInfo** 프로젝트. 실행되고 있지 않다면 새로운 인스턴스를 시작합니다.

2. 메시지가 나타나면 선택 **s** toosearch 시작 이벤트에 대 한 합니다. 메시지 표시 tooenter 시작 하 고 시간 toodefine-시간 범위를 종료 합니다. 이러한 두 시간 사이의 이벤트만 반환 됩니다.

    사용 하 여 hello 다음 hello 시작을 입력할 때 형식을 지정 하 고 종료 시간: hh: mm 및 'am' 또는 'pm'. 예: 11:20pm.

    기록 tooreturn 이벤트 스톰 토폴로지 배포 된 hello 앞에서 시작 시간 및 종료 시간을 지금 사용 합니다. hello 반환 데이터 항목 비슷한 toohello를 텍스트 다음 포함 되어 있습니다.

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

검색 종료 이벤트 works hello에 대 한 동일한 시작 이벤트로 합니다. 그러나 hello 시작 이벤트가 발생 한 후 1, 5 분 사이 종료 이벤트를 임의로 생성 됩니다. Tootry toofind hello 종료 이벤트에 대 한 몇 가지의 시간 범위를 할 수 있습니다. 종료 이벤트는 hello 세션-hello 시작 이벤트 시간 및 종료 이벤트 시간 사이의 hello 차이 hello 기간도 포함 합니다. 다음은 END 이벤트에 대한 데이터 예제입니다.

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> 입력 한 hello 시간 값은 현지 시간으로, hello hello 쿼리에서 반환 된 시간은 utc에서입니다.

## <a name="stop-hello-topology"></a>Hello 토폴로지를 중지 합니다.

준비 toostop hello 토폴로지를 모두 반환 toohello **CorrelationTopology** Visual Studio에서 프로젝트. Hello에 **스톰 토폴로지 보기**hello 토폴로지를 선택 하 고 hello를 사용 하 여 **Kill** hello 위쪽 hello 토폴로지 보기에는 단추입니다.

## <a name="delete-your-cluster"></a>클러스터 삭제

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>다음 단계

더 많은 Storm 예제는 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하십시오.
