---
title: "aaaMonitor Ambari 웹 UI를 사용 하 여 Azure HDInsight 관리 및 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Ambari toomonitor Linux 기반 HDInsight 클러스터를 관리 하 고 있습니다. 이 문서에서는 toouse hello Ambari 웹 UI에 포함 된 HDInsight 클러스터 방법을 배웁니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>Hello Ambari 웹 UI를 사용 하 여 HDInsight 클러스터를 관리 합니다.

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari hello 관리 및 쉽게 toouse 웹 UI 및 REST API를 제공 하 여 Hadoop 클러스터의 모니터링을 간소화 합니다. Ambari는 Linux 기반 HDInsight 클러스터에 포함 되 고 사용 되는 toomonitor hello 클러스터 구성 변경 됩니다.

이 문서에서는 HDInsight 클러스터와 toouse Ambari 웹 UI hello 하는 방법을 배웁니다.

## <a id="whatis"></a>Ambari 정의

[Apache Ambari](http://ambari.apache.org)는 사용하기 쉬운 웹 UI를 제공하여 Hadoop 관리를 단순화합니다. Ambari를 사용하여 Hadoop 클러스터를 생성, 관리 및 모니터링할 수 있습니다. 개발자 hello를 사용 하 여 응용 프로그램에 이러한 기능을 통합할 수 [Ambari REST Api](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)합니다.

Ambari 웹 UI hello hello Linux 운영 체제를 사용 하는 HDInsight 클러스터를 사용 하 여 기본적으로 제공 됩니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. 

## <a name="connectivity"></a>연결

hello Ambari 웹 UI를 HTTPS://CLUSTERNAME.azurehdidnsight.net에서 HDInsight 클러스터에 사용할 수 있는 **CLUSTERNAME** hello 클러스터 이름입니다.

> [!IMPORTANT]
> HTTPS 필요 tooAmbari HDInsight에 연결 합니다. 인증에 대 한 메시지가 표시 되 면 hello 관리자 계정 이름 및 hello 클러스터를 만들 때 지정한 암호를 사용 합니다.

## <a name="ssh-tunnel-proxy"></a>SSH 터널(프록시)

Hello 인터넷을 통해 직접 액세스할 수 있는 클러스터에 대해 Ambari 동안 (예: toohello JobTracker) Ambari 웹 UI에 노출 되지 않으므로 hello에서 일부 링크는 인터넷 hello 합니다. 이러한 서비스 tooaccess, SSH 터널을 만들어야 합니다. 자세한 내용은 [HDInsight와 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md)을 참조하세요.

## <a name="ambari-web-ui"></a>Ambari 웹 UI

Toohello Ambari 웹 UI에 연결할 때 메시지 표시 tooauthenticate toohello 페이지입니다. Hello 클러스터 admin 사용자 (Admin 기본값) 및 클러스터를 만드는 동안 사용 되는 암호를 사용 합니다.

Hello 페이지가 열립니다 때 hello 위쪽에 참고 hello 모음. 이 모음 포함 hello 다음 정보와 컨트롤:

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Ambari 로고** -열립니다 hello 대시보드를 사용 하는 toomonitor hello 클러스터가 될 수 있습니다.

* **클러스터 이름 # ops** -hello 지속적인 Ambari 작업 수를 표시 합니다. 선택 hello 클러스터 이름 또는 **# ops** 백그라운드 작업의 목록이 표시 됩니다.

* **# 경고** -hello 클러스터에 대 한 경고 또는 위험 경고를 표시 합니다.

* **대시보드** -hello 대시보드에 표시 됩니다.

* **서비스** -hello 클러스터에서 hello 서비스에 대 한 정보 및 구성 설정입니다.

* **호스트** -hello 클러스터의 노드 hello에 대 한 정보 및 구성 설정입니다.

* **Alerts** - 정보, 경고 및 중요한 알림에 대한 로그입니다.

* **관리자** -소프트웨어 스택/서비스 hello 클러스터, 서비스 계정 정보 및 Kerberos 보안에 설치 됩니다.

* **Admin 단추** - Ambari 관리, 사용자 설정 및 로그 아웃입니다.

## <a name="monitoring"></a>모니터링

### <a name="alerts"></a>경고

hello 다음 목록에 포함 되어 Ambari에서 사용 하는 hello 일반적인 경고 상태:

* **OK**
* **Warning**
* **CRITICAL**
* **UNKNOWN**

경고 이외의 **확인** hello 인해 **# 경고** hello 위쪽 경고 hello 페이지 toodisplay hello 수의 항목입니다. 이 항목을 선택 하면 hello 경고 및 상태를 표시 합니다.

경고 hello에서 볼 수 있는 여러 기본 그룹으로 구성 됩니다 **경고** 페이지.

![경고 페이지](./media/hdinsight-hadoop-manage-ambari/alerts.png)

Hello를 사용 하 여 hello 그룹을 관리할 수 **동작** 메뉴에서 **경고 그룹 관리**합니다.

![경고 그룹 관리 대화 상자](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

또한 경고 방법을 직접 관리 하 고 hello에서 경고 알림을 만들 수 있습니다 **동작** 메뉴를 선택 하 여 __경고 알림을 관리__합니다. 모든 현재 알림이 표시됩니다. 여기에서 알림을 만들 수도 있습니다. 특정 경고/심각도 조합이 발생하면 **전자 메일** 또는 **SNMP**를 통해 알림을 보낼 수 있습니다. 예를 들어 hello에 때 hello 경고 전자 메일 메시지를 보낼 수 있습니다 **YARN 기본** 그룹을 너무 설정**위험**합니다.

![경고 만들기 대화 상자](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

마지막으로,을 선택 하면 __경고 설정 관리__ hello에서 __동작__ 메뉴 있습니다 tooset hello 횟수 경고 알림을 전송 되기 전에 발생 해야 합니다. 일시적인 오류에 대 한 사용된 tooprevent 알림을 설정할 수 있습니다.

### <a name="cluster"></a>프로비전

hello **메트릭** hello 대시보드 탭 일련의 클러스터의 쉽게 toomonitor hello 상태를 한 눈에 확인 하는 위젯 포함 합니다. **CPU Usage**와 같은 여러 위젯은 클릭하면 추가 정보를 제공합니다.

![메트릭이 표시된 대시보드](./media/hdinsight-hadoop-manage-ambari/metrics.png)

hello **Heatmaps** 탭 하 여 메트릭을 녹색 toored에서 이동 하는 색이 지정 된 heatmaps로 표시 됩니다.

![히트맵이 표시된 대시보드](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Hello 클러스터 내의 hello 노드에 대 한 자세한 내용은 선택 **호스트**합니다. 다음에 관심이 있는 hello 특정 노드를 선택 합니다.

![호스트 세부 정보](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Services

hello **서비스** hello 대시보드에서 사이드바 hello 클러스터에서 실행 되는 hello 서비스의 hello 상태에 대 한 빠른 정보를 제공 합니다. 다양 한 아이콘은 사용 되는 tooindicate 상태 또는 수행 해야 하는 작업입니다. 예를 들어, 서비스가 필요한 toobe 재활용 하는 경우 노란색 재활용 기호가 표시 됩니다.

![서비스 세로 막대](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> 표시 된 hello 서비스 HDInsight 클러스터 유형 및 버전 간에 서로 다릅니다. 여기에 표시 된 hello 서비스는 클러스터에 대해 표시 된 hello 서비스 보다 다를 수 있습니다.

서비스를 선택 하면 hello 서비스에 보다 자세한 정보가 표시 됩니다.

![서비스 요약 정보](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>빠른 링크

일부 서비스 표시는 **빠른 링크** hello hello 페이지 맨 아래에 링크 합니다. 이 사용 되는 tooaccess 서비스 관련 웹 ui를 사용 해도 같은 수 있습니다.

* **Job History** - MapReduce 작업 기록
* **Resource Manager** - YARN ResourceManager UI
* **NameNode** - HDFS(Hadoop Distributed File System) NameNode UI
* **Oozie Web UI** - Oozie UI

이 링크를 선택 하면 hello 선택한 페이지를 표시 하는 브라우저에서 새 탭이 열립니다.

> [!NOTE]
> 선택 hello **빠른 링크** 서비스에 대 한 항목 "서버를 찾을 수 없습니다." 오류를 반환할 수 있습니다. Hello를 사용 하는 경우 SSH 터널을 사용 해야이 오류가 발생 하면 **빠른 링크** 이 서비스에 대 한 항목입니다. 자세한 내용은 [HDInsight와 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md)을 참조하세요.

## <a name="management"></a>관리

### <a name="ambari-users-groups-and-permissions"></a>Ambari 사용자, 그룹 및 사용 권한

[도메인 가입](hdinsight-domain-joined-introduction.md) HDInsight 클러스터를 사용할 때 사용자, 그룹 및 권한을 사용하는 작업이 지원됩니다. 참조에 hello Ambari 관리 UI를 사용 하 여 도메인에 가입 된 클러스터에 대 한 내용은 [도메인에 가입 된 HDInsight 클러스터를 관리](hdinsight-domain-joined-introduction.md)합니다.

> [!WARNING]
> Linux 기반 HDInsight 클러스터에 hello Ambari 감시 (hdinsightwatchdog)의 hello 암호를 변경 하지 마십시오. Hello 암호 구분선 변경 기능 toouse 스크립트 동작 hello 또는 클러스터를 사용 하 여 크기 조정 작업을 수행 합니다.

### <a name="hosts"></a>호스트

hello **호스트** 페이지 hello 클러스터의 모든 호스트를 나열 합니다. toomanage 호스트는 다음이 단계를 수행 합니다.

![호스트 페이지](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> 호스트 추가, 서비스 해제 및 서비스 등록은 HDInsight 클러스터에서 사용할 수 없습니다.

1. 원하는 toomanage hello 호스트를 선택 합니다.

2. 사용 하 여 hello **동작** tooperform 원하는 메뉴 tooselect hello 작업:

   * **모든 구성 요소 시작** -hello 호스트에서 모든 구성 요소를 시작 합니다.

   * **모든 구성 요소도 중지** -hello 호스트에서 모든 구성 요소를 중지 합니다.

   * **모든 구성 요소를 다시 시작** 중지-hello 호스트에서 모든 구성 요소를 시작 하 고 있습니다.

   * **유지 관리 모드를 켜고** -hello 호스트에 대 한 경고를 표시 하지 않습니다. 경고를 생성하는 작업을 수행하는 경우 이 모드를 활성화해야 합니다. 예를 들어 서비스를 중지하고 시작합니다.

   * **유지 관리 모드를 해제** -반환 hello 호스트 toonormal 경고 합니다.

   * **중지** -중지 DataNode 또는 NodeManagers hello 호스트에 있습니다.

   * **시작** -시작 DataNode 또는 NodeManagers hello 호스트에 있습니다.

   * **다시 시작** -중지 및 시작 DataNode 또는 NodeManagers hello 호스트에 있습니다.

   * **서비스 해제** -hello 클러스터에서 호스트를 제거 합니다.

     > [!NOTE]
     > HDInsight 클러스터에서는 이 작업을 사용하지 마세요.

   * **Recommission** -이전에 서비스 해제 된 호스트 toohello 클러스터에 추가 합니다.

     > [!NOTE]
     > HDInsight 클러스터에서는 이 작업을 사용하지 마세요.

### <a id="service"></a>Services

Hello에서 **대시보드** 또는 **서비스** 페이지에서 hello를 사용 하 여 **동작** hello 서비스 toostop hello 목록 맨 아래에 단추 및 모든 서비스를 시작 합니다.

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> 동안 **서비스 추가** 나열 되어 사용 되는 tooadd 서비스 toohello HDInsight 클러스터 수 없도록이 메뉴에 있습니다. 클러스터를 프로비전하는 동안 스크립트 작업을 사용하여 새 서비스를 추가해야 합니다. 스크립트 작업에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.

Hello 동안 **동작** 단추 모든 서비스를 다시 시작할 수, 종종 원하는 toostart, 중지 또는 특정 서비스를 다시 시작 합니다. Hello tooperform 작업 단계에 나오는 개별 서비스에 사용 합니다.

1. Hello에서 **대시보드** 또는 **서비스** 페이지에서 서비스를 선택 합니다.

2. Hello의 hello 위에서 **요약** 탭에서 hello를 사용 하 여 **서비스 작업** 단추와 선택 hello 동작 tootake 합니다. 모든 노드에서 hello 서비스를 다시 시작 합니다.

    ![서비스 작업](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Hello 클러스터에서 실행 되는 동안 일부 서비스를 다시 시작 경고를 생성할 수 있습니다. tooavoid 경고 hello를 사용할 수 있습니다 **서비스 작업** 단추 tooenable **유지 관리 모드** hello를 다시 시작을 수행 하기 전에 hello 서비스에 대 한 합니다.

3. 작업을 선택 하 고 나면 hello **# op** 백그라운드 작업이 발생 하는 hello 페이지 단위로 tooshow hello 위쪽에 있는 항목입니다. Toodisplay 구성 된 경우 백그라운드 작업의 hello 목록이 표시 됩니다.

   > [!NOTE]
   > 사용 하도록 설정한 경우 **유지 관리 모드** 기억 toodisable hello 서비스에 대 한 hello를 사용 하 여 **서비스 작업** hello 작업이 완료 되 면 단추입니다.

서비스를 tooconfigure 단계를 수행 하는 hello를 사용 합니다.

1. Hello에서 **대시보드** 또는 **서비스** 페이지에서 서비스를 선택 합니다.

2. 선택 hello **Configs** 탭 hello 현재 구성이 표시 됩니다. 이전 구성의 목록도 표시됩니다.

    ![구성](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Hello 표시 되는 필드 toomodify hello 구성을 사용 하 여 선택한 후 **저장**합니다. 또는 이전 구성을 선택한 다음 선택 **현재** tooroll toohello 이전 설정으로 리셋합니다.

## <a name="ambari-views"></a>Ambari 뷰

Ambari 뷰를 사용 하면 개발자가 tooplug UI 요소 hello Ambari 웹 UI에 hello를 사용 하 여 [Ambari 보기 프레임 워크](https://cwiki.apache.org/confluence/display/AMBARI/Views)합니다. HDInsight은 Hadoop 클러스터 종류를 사용 하 여 뷰를 수행 하는 hello를 제공 합니다.

* 큐 관리자 yarn: hello 큐 관리자 보기 및 수정 YARN 큐에 대 한 간단한 UI를 제공 합니다.

* 하이브 보기: 보기 하이브 hello가 있습니다 웹 브라우저에서 직접 toorun 하이브 쿼리를. 쿼리 저장 결과 확인 또는 결과 toohello 클러스터 저장소에 저장 결과 tooyour 로컬 시스템을 다운로드할 수 있습니다. Hive 뷰 사용에 대한 자세한 내용은 [HDInsight와 함께 Hive 뷰 사용](hdinsight-hadoop-use-hive-ambari-view.md)을 참조하세요.

* Tez 보기: hello Tez 보기 있습니다 toobetter 이해 하 고 작업을 최적화 합니다. Tez 작업 실행 방법 및 사용되는 리소스에 대한 정보를 볼 수 있습니다.
