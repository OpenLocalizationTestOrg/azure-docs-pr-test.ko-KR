---
title: "aaaDeploy HDInsight의 Apache Storm 토폴로지를 관리할 및 | Microsoft Docs"
description: "Toodeploy를 모니터링 하 고 hello 스톰 대시보드를 사용 하 여 HDInsight의 Apache Storm 토폴로지를 관리 하는 방법에 대해 알아봅니다. Visual Studio용 Hadoop 도구를 사용합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Windows 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리

hello 스톰 대시보드 tooeasily을 사용 하면 배포 하 고 웹 브라우저를 사용 하 여 Apache Storm 토폴로지 tooyour HDInsight 클러스터를 실행 합니다. 대시보드 toomonitor hello를 사용 하 고 실행 중인 토폴로지를 관리할 수도 있습니다. Visual Studio를 사용 하는 경우 hello HDInsight Tools for Visual Studio는 Visual Studio에서 비슷한 기능을 제공 합니다.

hello 스톰 대시보드와 hello 스톰 기능 hello HDInsight 도구에에서 사용 hello 스톰 REST API를 사용 하는 toocreate 될 수 있는 사용자 고유의 솔루션 모니터링 및 관리 합니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Windows hello 운영 체제로 사용 하 여 HDInsight 클러스터에서 Storm이 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.
>
> Linux를 사용하는 HDInsight 클러스터에서 Storm 토폴로지 배포 및 관리에 대한 자세한 내용은 [Linux 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

* **HDInsight의 Apache Storm** - 클러스터를 만드는 단계는 [HDInsight에서 Apache Storm 시작](hdinsight-apache-storm-tutorial-get-started.md)을 참조하세요.

* Hello에 대 한 **스톰 대시보드**: 지 원하는 HTML5 최신 웹 브라우저입니다.

* 에 대 한 **Visual Studio** -Azure SDK 2.5.1 나 최신 Visual Studio 용 HDInsight 도구 hello 및 합니다. 참조 [Visual Studio 용 HDInsight 도구를 사용 하 여 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall 및 Visual Studio에 대 한 hello HDInsight 도구를 구성 합니다.

    다음 버전의 Visual Studio hello 중 하나입니다.

  * Visual Studio 2012 업데이트 4

  * Visual Studio 2013 업데이트 4 또는 Visual Studio 2013 Community

  * Visual Studio 2015(모든 버전)

  * Visual Studio 2017(모든 버전)

## <a name="storm-dashboard"></a>Storm 대시보드

hello 스톰 대시보드는 Storm 클러스터에서 사용할 수 있는 웹 페이지입니다. hello URL은 **https://&lt;clustername >.azurehdinsight.net/**여기서 **clustername** HDInsight 클러스터에서 프로그램 스톰 hello 이름입니다.

Hello 스톰 대시보드의 hello 위에서 선택 **제출 토폴로지**합니다. Hello 페이지 toorun 샘플 토폴로지에 대 한 hello 지침 또는 tooupload 따르고 만든 토폴로지를 실행 합니다.

![hello 제출 토폴로지 페이지][storm-dashboard-submit]

### <a name="storm-ui"></a>Storm UI

Hello 스톰 대시보드, 선택 hello **스톰 UI** 링크 합니다. 이 토폴로지를 실행 하는 추가 tooany hello 클러스터에 대 한 정보가 표시 됩니다.

![hello 스톰 ui][storm-dashboard-ui]

> [!NOTE]
> 일부 버전의 Internet Explorer와 처음 방문한 후 스톰 UI를 새로 고치지 않습니다 해당 hello를 검색할 수 있습니다. 예를 들어이 나타나지 않을 수 있습니다 hello 새 토폴로지 전송한 또는 이전에 비활성화 될 때 활성으로 토폴로지를 표시할 수 있습니다. Microsoft는 이 문제를 알고 있으며 해결 방법을 찾기 위해 노력하고 있습니다.

#### <a name="main-page"></a>기본 페이지

hello 스톰 UI의 기본 페이지 hello hello를 다음 정보를 제공 합니다.

* **클러스터 요약**: hello Storm 클러스터에 대 한 기본 정보입니다.

* **토폴로지 요약**: 실행 중인 토폴로지 목록입니다. 자세한 내용은이 섹션 tooview의 hello 링크 사용 하 여 특정 토폴로지에 대 한 합니다.

* **요약 감독자**: hello 스톰 감독자에 대 한 정보입니다.

* **Nimbus 구성**: hello 클러스터에 대 한 Nimbus 구성 합니다.

#### <a name="topology-summary"></a>토폴로지 요약

Hello에서 링크를 선택 하면 **토폴로지 요약** hello hello 토폴로지에 대 한 정보를 다음 섹션에 표시 됩니다.

* **토폴로지 요약**: hello 토폴로지에 대 한 기본 정보입니다.

* **토폴로지 작업**: hello 토폴로지에 대해 수행할 수 있는 관리 작업입니다.

  * **활성화**- 비활성화된 토폴로지 처리를 다시 시작합니다.

  * **비활성화**- 실행 중인 토폴로지를 일시 중지합니다.

  * **균형을 다시 조정할**: hello 토폴로지의 hello 병렬 처리를 조정 합니다. 하면 해야 균형을 다시 조정 실행 중인 토폴로지 hello hello 클러스터의 노드 수를 변경한 후 합니다. 이렇게 하면 hello 토폴로지 tooadjust 병렬 처리 수준 toocompensate hello에 대 한 값 만큼 증가 하거나 감소 하는 hello 클러스터의 노드 수 있습니다.

      자세한 내용은 참조 [스톰 토폴로지 (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)의 hello 병렬 처리 수준이 이해](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)합니다.

  * **Kill**: hello 제한 시간을 지정한 후 스톰 토폴로지를 종료 합니다.

* **토폴로지 통계**: hello 토폴로지에 대 한 통계입니다. Hello 링크를 사용 하 여 hello에 **창** hello 페이지에 항목이 남아 있는 hello에 대 한 열 tooset hello 기간입니다.

* **Spouts**: hello spouts hello 토폴로지에서 사용 합니다. 특정 spouts에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.

* **쐐기**: hello 볼트 hello 토폴로지에서 사용 합니다. 특정 볼트에 대 한 자세한 내용은이 섹션 tooview의 hello 링크를 사용 합니다.

* **토폴로지 구성**: 선택한 hello 토폴로지의 hello 구성 합니다.

#### <a name="spout-and-bolt-summary"></a>Spout 및 Bolt 요약

배출구 hello에서 선택 하면 **Spouts** 또는 **쐐기** hello 다음 hello 선택 항목에 대 한 정보를 표시 하는 섹션:

* **구성 요소 요약**: hello 배출구 또는 번개에 대 한 기본 정보입니다.

* **Stats 배출구/볼트**: hello에 대 한 통계 spout 또는 볼트 합니다. Hello 링크를 사용 하 여 hello에 **창** hello 페이지에 항목이 남아 있는 hello에 대 한 열 tooset hello 기간입니다.

* **Stats 입력** (볼트): hello에 대 한 정보 입력 스트림을 hello 볼트에서 사용 합니다.

* **통계를 출력**:이에서 내보내는 hello 스트림에 대 한 정보 spout 또는 볼트 합니다.

* **단일 실행**: hello 배출구 또는 볼트의 인스턴스를 hello에 대 한 정보입니다. 선택 hello **포트** 이 인스턴스에 대 한 특정 실행자 tooview에 대 한 항목 진단 정보에 대 한 로그를 생성 합니다.

* **오류**: 이 Spout 또는 Bolt에 대한 오류 정보입니다.

## <a name="hdinsight-tools-for-visual-studio"></a>Visual Studio용 HDInsight 도구

hello HDInsight 도구에 사용 되는 toosubmit C# 또는 하이브리드 토폴로지에 tooyour Storm 클러스터 될 수 있습니다. 샘플 응용 프로그램을 사용 하는 hello 단계를 수행 합니다. Hello HDInsight 도구를 사용 하 여 사용자 고유의 토폴로지를 만드는 방법은 참조 [hello HDInsight 도구를 사용 하 여 Visual Studio에 대 한 개발 C# 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.

Hello 단계 toodeploy 샘플 tooyour 스톰 HDInsight 클러스터에서 다음을 사용 하 여 다음 보고 하 고 hello 토폴로지를 관리 합니다.

1. Visual Studio 용 hello 최신 버전의 hello HDInsight 도구를 아직 설치 하지 있을 경우 참조 [Visual Studio 용 HDInsight 도구를 사용 하 여 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.

2. Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.

3. Hello에 **새 프로젝트** 대화 상자에서 **설치 됨** > **템플릿**를 선택한 후 **HDInsight**합니다. Hello 템플릿 목록에서 선택 **스톰 샘플**합니다. Hello 대화 상자의 hello 아래쪽 hello 응용 프로그램에 대 한 이름을 입력 합니다.

    ![이미지](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. **솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **HDInsight의 tooStorm 제출**합니다.

   > [!NOTE]
   > 메시지가 표시 되 면 Azure 구독에 대 한 hello 로그인 자격 증명을 입력 합니다. 구독이 둘 이상 있는 경우 프로그램 스톰 HDInsight 클러스터에 포함 된 toohello에 로그인 합니다.

5. Hello에서 HDInsight 클러스터에서 프로그램 스톰 선택 **Storm 클러스터** 드롭 다운 목록에서 선택한 후 **전송**합니다. Hello 제출은 hello를 사용 하 여 성공 여부를 모니터링할 수 있습니다 **출력** 창.

6. Hello 토폴로지 성공적으로 제출 되 면 hello **스톰 토폴로지** hello 클러스터 표시 해야 합니다. 토폴로지를 실행 하는 hello에 대 한 hello 목록 tooview 정보에서 hello 토폴로지를 선택 합니다.

    ![VISUAL STUDIO 모니터](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > **Azure** > **HDInsight**를 확장한 다음 HDInsight의 Storm 클러스터를 마우스 오른쪽 단추로 클릭하고 **Storm 토폴로지 보기**를 선택하여 **서버 탐색기**에서 **Storm 토폴로지**를 볼 수도 있습니다.

    Hello spouts 또는 쐐기 이러한 구성 요소에 대 한 tooview 정보에 대 한 hello 셰이프를 선택 합니다. 선택한 각 항목에 대해 새 창이 열립니다.

   > [!NOTE]
   > hello hello 토폴로지 이름이 hello 토폴로지의 hello 클래스 이름 (이 경우 `HelloWord`,) 타임 스탬프를 추가 합니다.

7. Hello에서 **토폴로지 요약** 뷰의 **Kill** toostop hello 토폴로지입니다.

   > [!NOTE]
   > Storm 토폴로지는 중지 하거나 hello 클러스터를 삭제할 때까지 실행을 계속 합니다.


## <a name="rest-api"></a>REST API

hello 스톰 UI 비슷한 관리 및 모니터링 기능 hello REST API를 사용 하 여 수행할 수 있도록 hello REST API를 기반으로 만들어집니다. 관리 및 모니터링 스톰 토폴로지 hello REST API toocreate 사용자 지정 도구를 사용할 수 있습니다.

자세한 내용은 [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md)를 참조하세요. hello 다음 정보는 특정 toousing hello HDInsight의 Apache Storm를 사용 하 여 REST API입니다.

### <a name="base-uri"></a>기본 URI

HDInsight 클러스터에서 REST API hello에 대 한 기본 URI는 hello **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**여기서 **clustername** 에 프로그램 Storm의 hello 이름인 HDInsight 클러스터입니다.

### <a name="authentication"></a>인증

REST API를 사용 해야 하는 요청 toohello **기본 인증**이므로 hello HDInsight 클러스터 관리자 이름 및 암호를 사용 합니다.

> [!NOTE]
> 일반 텍스트를 사용 하 여 기본 인증 보내지므로 해야 **항상** hello 클러스터와 toosecure HTTPS 통신을 사용 합니다.

### <a name="return-values"></a>반환 값

REST API만 hello 클러스터 내에서 사용할 수 있습니다 또는 가상 컴퓨터에 hello 클러스터와 동일한 Azure 가상 네트워크를 환영 hello에서 반환 되는 정보입니다. 예를 들어 hello 정규화 된 도메인 이름 (FQDN) 사육 서버에 대해 반환 되는 hello 인터넷에서에서 액세스할 수 없습니다.

## <a name="next-steps"></a>다음 단계

이제 toodeploy / 모니터 토폴로지를 사용 하 여 스톰 대시보드 hello 하는 방법을 배운, 자세히 배울 방법:

* [Visual Studio 용 HDInsight 도구 hello를 사용 하 여 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Maven을 사용하여 Java 기반 토폴로지 개발](hdinsight-storm-develop-java-topology.md)

추가 예제 토폴로지 목록은 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하세요.

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
