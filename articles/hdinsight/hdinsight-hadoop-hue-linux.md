---
title: "HDInsight Linux 기반 클러스터-Azure에서 Hadoop으로 aaaHue | Microsoft Docs"
description: "HDInsight의 색상을 나타내는 tooinstall 클러스터 방법을 알아보고 tooroute hello 요청 tooHue 터널링을 사용 합니다. 색상 toobrowse 저장소를 사용 하 고 하이브 또는 Pig를 실행 합니다."
keywords: hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>HDInsight Hadoop 클러스터에 Hue 설치 및 사용

HDInsight의 색상을 나타내는 tooinstall 클러스터 방법을 알아보고 tooroute hello 요청 tooHue 터널링을 사용 합니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="what-is-hue"></a>Hue 정의
색상은 Hadoop 클러스터 toointeract를 사용 하는 웹 응용 프로그램 집합입니다. Hadoop 클러스터 (HDInsight 클러스터의 hello 대/소문자 WASB)와 연결 된 색상을 나타내는 toobrowse hello 저장소를 사용 하 고, 작업 Hive 및 Pig 스크립트를 실행 하 고, 등 수입니다. hello 다음 구성 요소가 HDInsight Hadoop 클러스터에서 색상 설치와 함께 사용할 수 있습니다.

* Beeswax Hive 편집기
* Pig
* 메타스토어 관리자
* Oozie
* FileBrowser (있음 tooWASB 기본 컨테이너 발언)
* 작업 브라우저

> [!WARNING]
> Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원를 Microsoft 지원 tooisolate는 데 도움이 되며 관련된 toothese 구성 요소 문제를 해결 합니다.
>
> 사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다. 이 hello 문제를 해결 하거나 hello에 대 한 사용 가능한 채널 tooengage 열면 해당 기술에 대 한 심층 전문 지식이 있는 소스 기술을 요청 될 수 있습니다. 예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).
>
>

## <a name="install-hue-using-script-actions"></a>스크립트 동작을 사용하여 Hue 설치

hello 스크립트 tooinstall Linux 기반 HDInsight 클러스터에서 색상은 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh에서 사용할 수 있습니다. 기본 저장소로 Azure 저장소 Blob (WASB) 또는 Azure 데이터 레이크 저장소 클러스터에서이 스크립트 tooinstall 색상을 사용할 수 있습니다.

이 섹션에서는 hello Azure 포털을 사용 하 여 hello 클러스터를 프로 비전 할 때 스크립트 toouse hello 하는 방법에 대 한 지침을 제공 합니다.

> [!NOTE]
> Azure PowerShell, hello Azure CLI, hello HDInsight.NET SDK 또는 Azure 리소스 관리자 템플릿을 사용 하는 tooapply 스크립트 동작 될 수도 있습니다. 클러스터를 실행 하는 스크립트 작업 tooalready를 적용할 수 있습니다. 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.
>
>

1. hello 단계를 사용 하 여 클러스터를 프로 비전 시작 [Linux 클러스터로 프로 비전 HDInsight](hdinsight-hadoop-provision-linux-clusters.md), 하지만 프로 비전을 완료 하지 않습니다.

   > [!NOTE]
   > HDInsight의 색상을 나타내는 tooinstall 클러스터, hello 헤드 노드에 권장된 크기는 적어도 A4 (8 코어, 14GB 메모리).
   >
   >
2. Hello에 **옵션 구성** 블레이드를 **스크립트 동작**, 아래와 같이 hello 정보를 제공 합니다.

    ![색상에 대한 스크립트 작업 매개 변수 제공](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "색상에 대한 스크립트 작업 매개 변수 제공")

   * **이름**: hello 스크립트 동작에 대 한 이름을 입력 합니다.
   * **SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **HEAD**: 이 옵션 선택
   * **작업자**: 이 옵션을 비워둡니다.
   * **ZOOKEEPER**: 이 옵션을 비워둡니다.
   * **PARAMETERS**: 이 옵션을 비워둡니다.
3. Hello hello 맨 아래에 **스크립트 동작**, hello를 사용 하 여 **선택** 단추 toosave hello 구성 합니다. 마지막으로 hello를 사용 하 여 **선택** hello 아래쪽 hello의 단추 **선택적 구성** 블레이드 toosave hello 선택적 구성 정보입니다.
4. 에 설명 된 대로 hello 클러스터를 프로 비전 계속 [Linux 클러스터로 프로 비전 HDInsight](hdinsight-hadoop-provision-linux-clusters.md)합니다.

## <a name="use-hue-with-hdinsight-clusters"></a>HDInsight 클러스터로 Hue 사용

SSH 터널링 실행 되 면 hello 유일한 방법은 tooaccess 색상 hello 클러스터입니다. SSH를 통해 터널링 toohello 헤드 노드에 hello의 색상을 나타내는 실행 중인 클러스터 직접 hello 트래픽 toogo를 수 있습니다. Hello 클러스터 프로 비전 완료 되 면 hello 단계 toouse 색상 HDInsight Linux 클러스터에서 다음을 사용 합니다.

> [!NOTE]
> 아래 Firefox 웹 브라우저 toofollow hello 지침을 사용 하는 것이 좋습니다.
>
>

1. Hello 정보에 사용 하 여 [사용 하 여 SSH 터널링 tooaccess Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie, 및 기타 웹 UI](hdinsight-linux-ambari-ssh-tunnel.md) toocreate는 SSH 터널링 클라이언트 시스템 toohello HDInsight 클러스터에서 한 다음 구성 사용자 웹 브라우저 toouse hello SSH 터널을 프록시로 합니다.

2. SSH 터널을 생성 하 고이 통해 브라우저 tooproxy 트래픽의 구성 후 hello 호스트 이름의 hello 기본 헤드 노드를 찾아야 합니다. SSH를 사용 하 여 포트 22에서 toohello 클러스터를 연결 하 여이 수행할 수 있습니다. 예를 들어 `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` 여기서 **USERNAME** 은 SSH 사용자 이름 및 **CLUSTERNAME** hello 클러스터 이름입니다.

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

3. 연결 되 면 hello 기본 헤드 노드에 명령 tooobtain hello 정규화 된 도메인 이름 뒤 hello를 사용 합니다.

        hostname -f

    이 이름이 비슷한 toohello 다음을 반환 합니다.

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Hello 색상 웹 사이트 위치한 hello 기본 헤드 노드에의 hello 호스트 이름입니다.
4. Http://HOSTNAME:8888에 hello 브라우저 tooopen hello 색상 포털을 사용 합니다. 호스트 이름을 hello 이전 단계에서 얻은 hello 이름을 바꿉니다.

   > [!NOTE]
   > 에 로그인 할 때 hello에 대 한 처음으로, 입력 정보 요청된 toocreate toohello 색상 포털에는 계정 toolog 됩니다. 여기에서 지정 하는 hello 자격 증명을 제한 toohello 포털 되며은 관련된 toohello 관리자 또는 hello 클러스터 프로 비전 하는 동안 지정 된 SSH 사용자 자격 증명.
   >
   >

    ![로그인 toohello 색상 포털](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "색상 포털에 대 한 자격 증명 지정")

### <a name="run-a-hive-query"></a>HIVE 쿼리 실행
1. Hello 색상 포털에서 클릭 **쿼리 편집기**, 클릭 하 고 **하이브** tooopen hello 하이브 편집기입니다.

    ![Hive 사용](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Hive 사용")
2. Hello에 **Assist** 탭의 **데이터베이스**, 나타납니다 **hivesampletable**합니다. HDInsight에서 모든 Hadoop 클러스터로 제공되는 예제 테이블입니다. Hello 오른쪽 창에서 예제 쿼리를 입력 하 고 hello에 hello 출력을 참조 하십시오. **결과** hello 화면 캡처에 나와 있는 것 처럼, 아래의 hello 창에서 탭 합니다.

    ![Hive 쿼리 실행](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Hive 쿼리 실행")

    Hello를 사용할 수도 있습니다 **차트** toosee을 시각적으로 hello 결과 탭 합니다.

### <a name="browse-hello-cluster-storage"></a>Hello 클러스터 저장소 찾아보기
1. Hello 색상 포털에서 클릭 **파일 브라우저** hello 메뉴 표시줄의 hello 오른쪽 위 모서리에 있습니다.
2. 기본적으로 hello에 hello 파일 브라우저가 열립니다 **/사용자/myuser** 디렉터리입니다. Hello 클러스터와 연결 된 hello Azure storage 컨테이너의 hello 경로 toogo toohello 루트에서 hello 사용자 디렉터리 직전 hello 앞에 슬래시를 클릭 합니다.

    ![파일 브라우저 사용](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "파일 브라우저 사용")
3. 파일 또는 폴더 toosee hello 사용 가능한 작업을 마우스 오른쪽 단추로 클릭 합니다. 사용 하 여 hello **업로드** 단추 hello 오른쪽 모서리 tooupload 파일 toohello 현재 디렉터리에 있습니다. 사용 하 여 hello **새로** 단추 toocreate 새 파일 또는 디렉터리입니다.

> [!NOTE]
> hello 색상을 나타내는 파일 브라우저 hello HDInsight 클러스터와 연결 된 hello 기본 컨테이너의 hello 내용을 하나만 표시할 수 있습니다. 추가 저장소 계정/컨테이너 hello 클러스터와 연결 된 hello 파일 탐색기를 사용 하 여 액세스할 수 없습니다. 그러나 hello 클러스터와 연결 된 hello 추가 컨테이너 항상 hello 하이브 작업에 대 한 액세스할 수 있습니다. 예를 들어 hello 명령을 입력 하면 `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` hello 하이브 편집기에서 추가 컨테이너도의 hello 내용을 볼 수 있습니다. 이 명령에서 **newcontainer** 클러스터와 연결 된 hello 기본 컨테이너 않습니다.
>
>

## <a name="important-considerations"></a>중요 고려 사항
1. hello 사용 되는 스크립트 tooinstall 색상 hello 클러스터의 기본 헤드 노드에 hello에만 설치 합니다.

2. 설치 하는 동안 여러 Hadoop 서비스 (HDFS, YARN, MR2, Oozie) hello 구성을 업데이트 하는 것에 대 한 다시 시작 됩니다. Hello 스크립트 색상 설치 완료 되 면이 걸릴 수도 있습니다 Hadoop 서비스 toostart 다른 약간의 시간이 됩니다. 처음에 Hue의 성능이 달라질 수 있습니다. 모든 서비스를 시작하면 Hue는 완벽하게 작동합니다.
3. 색상을 인식 하지 못하는 Tez 작업 hello 하이브에 대 한 현재 기본값입니다. Hello 하이브 실행 엔진으로 toouse MapReduce를 원하는 경우 다음 스크립트에 명령을 hello 스크립트 toouse hello를 업데이트 합니다.

        set hive.execution.engine=mr;

4. Linux 클러스터 서비스가 실행 되 고 있는 hello 기본 헤드 노드에에서 리소스 관리자 hello hello 보조에서 실행 될 수 하는 동안 시나리오를 사용할 수 있습니다. 이러한 시나리오 hello 클러스터에서 실행 중인 작업의 색상을 나타내는 tooview 세부 정보를 사용 하는 경우 (아래 참조) 오류가 발생할 수 있습니다. 그러나 hello 작업이 완료 되 면 hello 작업 세부 정보를 볼 수 있습니다.

   ![Hue 포털 오류](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue 포털 오류")

   원인인 tooa 알려진 문제가 있습니다. 이 문제를 해결 hello 활성 리소스 관리자도 실행 되도록 기본 헤드 노드에 hello에 Ambari를 수정 합니다.
5. `wasb://`을 사용하여 HDInsight 클러스터가 Azure 저장소를 사용하는 동안 Hue는 WebHDFS를 이해합니다. 따라서 스크립트 동작에 사용할 사용자 지정 스크립트를 hello tooWASB 통신에 WebHDFS 호환 서비스인 WebWasb를 설치 합니다. 따라서 hello 색상 포털 HDFS 위치에 표시 하는 경우에 (hello 위로 마우스를 이동 하면 같은 **파일 브라우저**), WASB으로 해석 해야 합니다.

## <a name="next-steps"></a>다음 단계
* [HDInsight 클러스터에 Giraph 설치](hdinsight-hadoop-giraph-install-linux.md). 클러스터 사용자 지정 tooinstall Giraph에 HDInsight Hadoop 클러스터를 사용 합니다. Giraph tooperform 그래프 Hadoop를 사용 하 여 처리를 허용 하 고 Azure HDInsight를 사용할 수 있습니다.
* [HDInsight 클러스터에 Solr 설치](hdinsight-hadoop-solr-install-linux.md). 클러스터 사용자 지정 tooinstall Solr에 HDInsight Hadoop 클러스터를 사용 합니다. Solr 저장 된 데이터에 tooperform 강력한 검색 작업을 허용 합니다.
* [HDInsight 클러스터에 R 설치](hdinsight-hadoop-r-scripts-linux.md). HDInsight Hadoop 클러스터에서 클러스터 사용자 지정 tooinstall R을 사용 합니다. R은 통계 계산을 위한 오픈 소스 언어 및 환경입니다. 수백 개의 기본 제공 통계 함수와 기능 및 개체 지향 프로그래밍의 측면을 결합하는 고유한 프로그래밍 언어를 제공합니다. 또한 광범위한 그래픽 기능도 제공합니다.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
