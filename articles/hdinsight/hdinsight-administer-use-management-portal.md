---
title: "HDInsight를 사용 하 여의 aaaManage Windows 기반 Hadoop 클러스터 hello Azure 포털 | Microsoft Docs"
description: "자세한 내용은 방법 tooadminister HDInsight 서비스입니다. HDInsight 클러스터, 대화형 JavaScript 콘솔 열기 hello 및 열기 hello Hadoop 명령 콘솔을 만듭니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 HDInsight의 Hadoop Windows 기반 클러스터를 관리 합니다.

Hello를 사용 하 여 [Azure 포털][azure-portal]프로토콜 RDP (원격 데스크톱)를 사용 하도록 설정에 액세스할 수 있도록 hello Hadoop 및 Azure HDInsight의 Hadoop Windows 기반 클러스터를 만들, Hadoop 사용자 암호를 변경할 수 있습니다, hello 클러스터에서 명령 콘솔입니다.

이 문서의 정보 hello에 tooWindow 기반 HDInsight 클러스터에만 적용 됩니다. Linux 기반 클러스터 관리에 대 한 자세한 내용은 참조 하십시오. [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello](hdinsight-administer-use-portal-linux.md)합니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.


## <a name="prerequisites"></a>필수 조건

이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.
* **Azure 저장소 계정** -는 HDInsight 클러스터 hello 기본 파일 시스템으로 Azure Blob 저장소 컨테이너를 사용 합니다. Azure Blob 저장소가 HDInsight 클러스터에서 매끄럽게 작동하는 방식에 대한 자세한 내용은 [HDInsight에서 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요. Azure 저장소 계정을 만드는 방법에 대 한 세부 정보를 참조 하십시오. [어떻게 tooCreate 저장소 계정](../storage/common/storage-create-storage-account.md)합니다.

## <a name="open-hello-portal"></a>Hello 포털 열기
1. 역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.
2. Hello 포털을 연 후 다음 작업을 수행할 수 있습니다.

   * 클릭 **새로** hello 왼쪽된 메뉴 toocreate 새 클러스터에서에서:

       ![새 HDInsight 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다.

       ![Azure 포털 HDInsight 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     경우 **HDInsight** hello 왼쪽된 메뉴에 표시를 클릭 하지 **찾아보기**합니다.

     ![Azure Portal 찾아보기 클러스터 단추](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>클러스터 만들기
Hello 만들기 hello 포털을 사용 하 여 지침은 [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.

HDInsight는 다양한 Hadoop 구성 요소에서 작동합니다. Hello 구성 요소 확인 및 지원 된 hello 목록에 대 한 참조 [Azure HDInsight의 Hadoop의 어떤 버전은](hdinsight-component-versioning.md)합니다. Hello 다음 옵션 중 하나를 사용 하 여 HDInsight를 사용자 지정할 수 있습니다.

* 사용 하 여 작업 스크립팅 toorun 사용자 지정 스크립트 클러스터 tooeither를 사용자 지정할 수 있는 클러스터 구성을 변경 하거나 Giraph 또는 Solr 같은 사용자 지정 구성 요소를 설치 합니다. 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster.md)(영문)을 참조하세요.
* 클러스터를 만드는 동안 hello HDInsight.NET SDK 또는 Azure PowerShell에서 hello 클러스터 사용자 지정 매개 변수를 사용 합니다. 이러한 구성 변경 내용을 다음 hello 클러스터의 hello 수명을 통해 보존 됩니다 및 유지 관리를 위해 Azure 플랫폼 주기적으로 수행 하는 클러스터 노드 reimages 영향을 받지 않습니다. Hello 클러스터에 대 한 사용자 지정 매개 변수를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.
* Mahout 및 Cascading와 같은 일부 네이티브 Java 구성 요소가 JAR 파일로 hello 클러스터에서 실행할 수 있습니다. 이러한 JAR 파일 분산된 tooAzure Blob 저장소 일 수 있습니다 및 tooHDInsight 클러스터 Hadoop 작업 전송 메커니즘을 통해 전송 합니다. 자세한 내용은 [프로그래밍 방식으로 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.

  > [!NOTE]
  > JAR 파일 tooHDInsight 클러스터 배포 문제 또는 문의 HDInsight 클러스터에서 JAR 파일을 호출할 경우 [Microsoft 지원](https://azure.microsoft.com/support/options/)합니다.
  >
  > Cascading은 HDInsight에서 지원되지 않으며 Microsoft 지원 대상이 아닙니다. 지원 되는 구성의 목록에 대 한 참조 [HDInsight에서 제공 하는 hello 클러스터 버전의 새로운 기능](hdinsight-component-versioning.md)합니다.
  >
  >

원격 데스크톱 연결을 사용 하 여 hello 클러스터에 있는 사용자 지정 소프트웨어 설치는 지원 되지 않습니다. Toore 해야 할 경우 삭제 될 것으로 hello 헤드 노드의 hello 드라이브에 모든 파일을 저장 하지 않아야-hello 클러스터를 만듭니다. Azure Blob 저장소에 파일을 저장하는 것이 좋습니다. Blob 저장소는 영구적입니다.

## <a name="list-and-show-clusters"></a>클러스터 나열 및 표시
1. 역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.
2. 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다.
3. Hello 클러스터 이름을 클릭 합니다. Hello 클러스터 목록이 긴 경우에 hello hello 페이지 위쪽에 필터를 사용할 수 있습니다.
4. Hello 목록 tooshow hello 세부 정보에서 클러스터를 두 번 클릭 합니다.

    **메뉴 및 요점**:

    ![Azure Portal HDInsight 클러스터 요점](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * toocustomize hello 메뉴 hello 메뉴에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 한 다음 클릭 **사용자 지정**합니다.
   * **설정** 및 **모든 설정을**: 표시 hello **설정을** 블레이드 tooaccess 수 있는 hello 클러스터에 대 한 자세한 hello 클러스터에 대 한 구성 정보입니다.
   * **대시보드**, **클러스터 대시보드** 및 **URL: 모든 방법으로 tooaccess hello 클러스터 대시보드 Linux 기반 클러스터용 Ambari Web 즉 이들은 합니다. -**보안 셸 * *: hello 지침 tooconnect toohello 클러스터를 SSH (보안 셸) 연결을 사용 하 여 보여 줍니다.
   * **클러스터의 크기를 조정**:이 클러스터에 대 한 toochange hello 작업자 노드 수를 허용 합니다.
   * **삭제**: hello 클러스터를 삭제 합니다.
   * **빠른 시작**: HDInsight를 사용하여 시작하는 데 도움이 되는 정보를 표시합니다.
   * * * 사용자: 있습니다에 대 한 권한을 tooset *포털 관리* Azure 구독에서 다른 사용자에 대 한이 클러스터의 합니다.

     > [!IMPORTANT]
     > 이 *만* hello Azure 포털에에서 대 한 액세스 권한과 toothis 클러스터 미치며 tooor 전송 작업 toohello HDInsight 클러스터를 연결할 수 있는 사용자에 아무 효과가 없습니다.
     >
     >
   * **태그**: 태그 있습니다 tooset 키/값 쌍 toodefine 클라우드 서비스의 사용자 정의 분류를 사용 합니다. 예를 들어 **project**라는 키를 만든 다음 특정 프로젝트와 연결된 모든 서비스에 공통 값을 사용할 수 있습니다.
   * **Ambari 뷰**: tooAmbari 웹 연결 합니다.

     > [!IMPORTANT]
     > HDInsight 클러스터 hello에서 toomanage hello 서비스 제공, Ambari Web을 사용 하거나 REST API Ambari hello 해야 합니다. Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.
     >
     >

     **사용 현황**

     ![Azure Portal HDInsight 클러스터 사용 현황](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. **설정**을 클릭합니다.

    ![Azure Portal HDInsight 클러스터 사용 현황](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **속성**: hello 클러스터 속성을 확인 합니다.
   * **클러스터 AAD ID**:
   * **Azure 저장소 키**: hello 기본 저장소 계정 및 키를 확인 합니다. hello 저장소 계정은 hello 클러스터를 만드는 프로세스 동안 구성입니다.
   * **로그인 클러스터**: hello 클러스터 HTTP 사용자 이름 및 암호를 변경 합니다.
   * **외부 Metastore**: hello Hive 및 Oozie metastore를 확인 합니다. hello metastore hello 클러스터를 만드는 프로세스 동안만 구성할 수 있습니다.
   * **클러스터의 크기를 조정**: 증가 및 감소 hello 클러스터 작업자 노드 수입니다.
   * **원격 데스크톱**: 설정 및 원격 데스크톱 (RDP) 액세스를 사용 하지 않도록 설정 및 hello RDP 사용자 이름을 구성 합니다.  hello RDP 사용자 이름은 hello HTTP 사용자 이름은 달라 야 합니다.
   * **공식 파트너**:

     > [!NOTE]
     > 이것은 사용 가능한 설정의 일반적인 목록이며 여기의 모든 설정이 모든 클러스터 유형에 제공되는 것은 아닙니다.
     >
     >
6. **속성**을 클릭합니다.

    hello 속성 섹션 hello 다음을 나열합니다.

   * **호스트 이름**: 클러스터 이름입니다.
   * **클러스터 URL**.
   * **상태**: 중단됨, 수락됨, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, 운영, 실행 중, 오류, 삭제 중, 삭제됨, 시간 초과됨, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization를 포함합니다.
   * **지역**: Azure 위치입니다. 목록이 지원 되는 Azure 위치에 대 한 참조 hello **지역** 드롭다운 목록 상자 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.
   * **생성된 데이터**.
   * **운영 체제**: **Windows** 또는 **Linux**입니다.
   * **형식**: Hadoop, HBase, Storm, Spark.
   * **버전**. [HDInsight 버전](hdinsight-component-versioning.md)
   * **구독**: 구독 이름입니다.
   * **구독 ID**.
   * **주 데이터 원본**. Azure Blob 저장소 계정 hello Hadoop 파일 시스템 hello 기본값으로 사용 됩니다.
   * **작업자 노드 가격 책정 계층**.
   * **헤드 노드 가격 책정 계층**.

## <a name="delete-clusters"></a>클러스터 삭제
Hello 기본 저장소 계정 또는 연결 된 저장소 계정을 삭제 하는 클러스터 삭제 되지 않습니다. 사용 하 여 hello 클러스터를 다시 만들 수 있습니다 hello 동일한 저장소 계정 및 동일한 metastore hello 합니다.

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.
3. 클릭 **삭제** hello 위쪽 메뉴에서 다음 hello 지침을 따릅니다.

참고 항목: [클러스터 일시 중지/종료](#pauseshut-down-clusters)

## <a name="scale-clusters"></a>클러스터 크기 조정
hello 클러스터 기능을 확장 하면 toochange hello toore 필요 없이 Azure HDInsight에서 실행 되는 클러스터에서 사용 하는 작업자 노드 수-hello 클러스터를 만듭니다.

> [!NOTE]
> HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다. 클러스터의 hello 버전을 잘 모를 경우 hello 속성 페이지를 확인할 수 있습니다.  [클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.
>
>

hello HDInsight에서 지원 되는 클러스터의 각 형식에 대 한 데이터 노드 수를 변경 하는 hello 미치는 영향:

* Hadoop은

    원활 하 게 hello 보류 중 또는 실행 중인 작업이 모두 영향을 주지 않고 실행 되는 Hadoop 클러스터의 작업자 노드 수를 늘릴 수 있습니다. Hello 작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다. 크기 조정 작업의 오류는 hello 클러스터는 항상를 작동 상태로 남아 있도록 정상적으로 처리 됩니다.

    Hadoop 클러스터는 hello 데이터 노드 수를 줄여 규모 축소, hello 클러스터의 hello 서비스 중 일부를 다시 시작 됩니다. 이렇게 하면 실행 중인 모든와 hello hello 크기 조정 작업이 완료 될 때 작업 toofail 보류 중. 그러나 hello 작업이 완료 되 면 hello 작업을 다시 전송할을 수 있습니다.
* HBase

    원활 하 게 추가 하거나 실행 하는 동안 노드 tooyour HBase 클러스터를 제거할 수 있습니다. 지역 서버는 hello 크기 조정 작업을 완료 하는 몇 분 안에 자동으로 균형이 조정 됩니다. 그러나 명령을 명령 프롬프트 창에서 다음 실행 중인 hello와 클러스터의 헤드 노드에 hello에 로그인 하 여 hello 지역 서버를 수동으로 분산 시킬 수 있습니다 있습니다.

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Hello HBase 셸을 사용 하 여에 대 한 자세한 내용은 참조 하십시오.
* Storm

    원활 하 게 추가 하거나 실행 하는 동안 데이터 노드 tooyour Storm 클러스터를 제거할 수 있습니다. 하지만 hello 크기 조정 작업을 성공적으로 완료 한 후 toorebalance hello 토폴로지를 해야 합니다.

    다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.

  * Storm 웹 UI
  * 명령줄 인터페이스(CLI) 도구

    Toohello를 참조 하십시오 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 자세한 세부 정보에 대 한 합니다.

    hello 스톰 웹 UI hello HDInsight 클러스터에서 제공 됩니다.

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    다음은 예제 어떻게 toouse hello CLI 명령을 toorebalance hello 스톰 토폴로지:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale 클러스터**

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.
3. 클릭 **설정** hello 상단 메뉴에서 **배율 클러스터**합니다.
4. **작업자 노드 수**를 입력합니다. 클러스터 노드의 hello 수 제한을 15 hello Azure 구독 마다 다릅니다. 청구 지원 tooincrease hello 제한을 문의할 수 있습니다.  hello 비용 정보 hello 변경 사항을 toohello 노드 수를 반영 합니다.

    ![HDinsight Hadoop Hbase Storm Spark 크기 조정](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>클러스터 일시 중지/종료
대부분의 Hadoop 작업은 이따금 실행되는 일괄 처리 작업입니다. 대부분의 Hadoop 클러스터에 대 한는 오랜 시간 해당 hello 클러스터 사용 하지 않는 처리를 위해 합니다. HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.
HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다. Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다.

여러 가지 방법으로 hello 프로세스를 프로그래밍할 수 있습니다.

* 사용자 Azure 데이터 팩터리. 주문형 및 자체 정의 HDInsight 연결된 서비스는 [Azure HDInsight 연결된 서비스](../data-factory/data-factory-compute-linked-services.md) 및 [Azure 데이터 팩터리를 사용한 분석 및 변환](../data-factory/data-factory-data-transformation-activities.md)을 참조하세요.
* Azure PowerShell 사용  [비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)을 참조하세요.
* Azure CLI 사용 [Azure CLI를 사용하여 HDInsight 클러스터 관리](hdinsight-administer-use-command-line.md)를 참조하세요.
* HDInsight .NET SDK 사용 [Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.

가격 책정 정보는 hello에 대 한 참조 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다. hello 포털에서에서 클러스터 toodelete 참조 [클러스터를 삭제 합니다.](#delete-clusters)

## <a name="change-cluster-username"></a>클러스터 사용자 이름 변경
HDInsight 클러스터마다 두 개의 사용자 계정이 포함될 수 있습니다. HDInsight 클러스터 사용자 계정 hello hello 만들기 프로세스 중 생성 됩니다. 또한 RDP 통해 hello 클러스터에 액세스 하기 위한 RDP 사용자 계정을 만들 수 있습니다. [원격 데스크톱 사용](#connect-to-hdinsight-clusters-by-using-rdp)을 참조하세요.

**toochange hello HDInsight 클러스터 사용자 이름 및 암호**

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.
3. 클릭 **설정** hello 상단 메뉴에서 **클러스터 로그인**합니다.
4. 경우 **클러스터 로그인** 되었습니다 클릭 해야 사용 하도록 설정 **사용 하지 않도록 설정**, 클릭 하 고 **사용** hello 사용자 이름 및 암호를 변경할 수 있습니다...
5. 변경 hello **클러스터 로그인 이름** hello 및/또는 **클러스터 로그인 암호**, 클릭 하 고 **저장**합니다.

    ![HDinsight 변경 클러스터 사용자 사용자 이름 암호 http 사용자](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>액세스 권한 부여/해지
HDInsight 클러스터에는 HTTP 웹 서비스 (모든 이러한 서비스는 RESTful 끝점)를 수행 하는 hello:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다. 있습니다 수 revoke/부여 hello 액세스 hello Azure 포털에서에서 합니다.

> [!NOTE]
> Hello 액세스 권한을 부여/취소를 하 여 hello 클러스터 사용자 이름 및 암호를 설정 합니다.
>
>

**HTTP toogrant/revoke 웹 서비스 액세스**

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.
3. 클릭 **설정** hello 상단 메뉴에서 **클러스터 로그인**합니다.
4. 경우 **클러스터 로그인** 되었습니다 클릭 해야 사용 하도록 설정 **사용 하지 않도록 설정**, 클릭 하 고 **사용** hello 사용자 이름 및 암호를 변경할 수 있습니다...
5. 에 대 한 **클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**, hello 클러스터에 대 한 hello 새 사용자 이름 및 암호를 각각 입력 합니다.
6. **저장**을 클릭합니다.

    ![HDinsight 총합계 제거 http 웹 서비스 액세스](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Hello 기본 저장소 계정 찾기
각 HDInsight 클러스터에는 기본 저장소 계정이 있습니다. 아래에 표시 하는 클러스터에 대 한 기본 저장소 계정 및 해당 키를 hello **설정**/**속성**/**Azure 저장소 키**합니다. [클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.

## <a name="find-hello-resource-group"></a>Hello 리소스 그룹 찾기
Hello Azure 리소스 관리자 모드에서 각 HDInsight 클러스터는 Azure 리소스 그룹으로 만들어집니다. 클러스터에 tooappears 속하는 hello Azure 리소스 그룹:

* hello 클러스터 목록에는 **리소스 그룹** 열입니다.
* 클러스터 **Essential** 타일.  

[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.

## <a name="open-hdinsight-query-console"></a>HDInsight 쿼리 콘솔 열기
hello HDInsight 쿼리 콘솔 hello 같은 기능에 포함 됩니다.

* **Hive 편집기**: Hive 작업 제출을 위한 GUI 웹 인터페이스입니다.  참조 [실행 하이브 쿼리를 사용 하 여 hello 쿼리 콘솔](hdinsight-hadoop-use-hive-query-console.md)합니다.

    ![HDInsight 포털 Hive 편집기](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **작업 내역**: Hadoop 작업을 모니터링합니다.  

    ![HDInsight 포털 작업 내역](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    클릭 **쿼리 이름** tooshow hello 작업 속성을 비롯 한 세부 정보 **작업 쿼리**, 및 * * 작업 출력 합니다. Hello 쿼리와 hello 출력 tooyour 워크스테이션 다운로드할 수 있습니다.
* **브라우저 파일**: hello 기본 저장소 계정 찾아보기 및 연결 된 저장소 계정을 hello 합니다.

    ![HDInsight 포털 파일 브라우저 찾아보기](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    Hello 스크린 샷에 hello  **<Account>**  형식은 hello 항목은 Azure 저장소 계정을 나타냅니다.  Hello 계정 이름 toobrowse hello 파일을 클릭 합니다.
* **Hadoop UI**.

    ![HDInsight 포털 Hadoop UI](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    **Hadoop UI*에서 파일을 찾아보고 로그를 확인할 수 있습니다.
* **Yarn UI**.

    ![HDInsight 포털 YARN UI](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Hive 쿼리 실행
tooran 하이브 작업은 hello 포털에서에서 클릭 **하이브 편집기** hello HDInsight 쿼리 콘솔. [HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.

## <a name="monitor-jobs"></a>작업 모니터링
toomonitor 작업은 hello 포털에서에서 클릭 **작업 기록** hello HDInsight 쿼리 콘솔. [HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.

## <a name="browse-files"></a>파일 찾아보기
toobrowse 파일 hello 기본 저장소 계정에 저장 하 고 연결 된 저장소 계정을 hello, 클릭 **파일 브라우저** hello HDInsight 쿼리 콘솔. [HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.

Hello를 사용할 수도 있습니다 **hello 파일 시스템 검색** hello에서 유틸리티 **Hadoop UI** hello HDInsight 콘솔에서.  [HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.

## <a name="monitor-cluster-usage"></a>클러스터 사용 현황 모니터링
hello **사용** hello HDInsight 클러스터 블레이드의 섹션에는 hello HDInsight 함께 사용할 사용 가능한 tooyour 구독 코어 수가 hello toothis 클러스터 하 게 하는 방법을 할당 하는 코어 수에 대 한 정보가 표시 됩니다. 이 클러스터 내에서 hello 노드에 대 한 할당. [클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.

> [!IMPORTANT]
> HDInsight 클러스터 hello에서 toomonitor hello 서비스 제공, Ambari Web을 사용 하거나 REST API Ambari hello 해야 합니다. Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Hadoop UI 열기
toomonitor hello 클러스터, 찾아보기 hello 파일 시스템 및 로그를 확인 하 고, 클릭 **Hadoop UI** hello HDInsight 쿼리 콘솔. [HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.

## <a name="open-yarn-ui"></a>Yarn UI 열기
toouse Yarn 사용자 인터페이스를 클릭 하 여 **Yarn UI** hello HDInsight 쿼리 콘솔. [HDInsight 쿼리 콘솔 열기](#open-hdinsight-query-console)를 참조하세요.

## <a name="connect-tooclusters-using-rdp"></a>Tooclusters RDP를 사용 하 여 연결
생성 시 사용자가 제공한 hello 클러스터에 대 한 자격 증명 hello hello 클러스터 있지만 하지 toohello 클러스터 자체 원격 데스크톱을 통해 toohello 서비스 액세스를 부여 합니다. 클러스터를 프로비전할 때 또는 클러스터가 프로비전된 후 원격 데스크톱 액세스를 켤 수 있습니다. Hello 생성 시 원격 데스크톱을 사용 하는 방법에 대 한 지침은 [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.

**원격 데스크톱 tooenable**

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.
3. 클릭 **설정** hello 상단 메뉴에서 **원격 데스크톱**합니다.
4. **만료 날짜**, **원격 데스크톱 사용자 이름** 및 **원격 데스크톱 암호**를 입력한 다음 **사용**을 클릭합니다.

    ![HDInsight에서 원격 데스크톱 비활성화 구성 해제](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    만료에 대 한 hello 기본값은 1 주일입니다.

   > [!NOTE]
   > 클러스터에 hello HDInsight.NET SDK tooenable 원격 데스크톱을 사용할 수도 있습니다. 사용 하 여 hello **EnableRdp** hello 방식으로 다음에 hello HDInsight 클라이언트 개체에서 메서드: **클라이언트입니다. EnableRdp (clustername, 위치, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**합니다. 마찬가지로, hello 클러스터에 원격 데스크톱을 toodisable를 사용할 수 있습니다 **클라이언트입니다. (Clustername, 위치) DisableRdp**합니다. 이러한 메서드에 대한 자세한 내용은 [HDInsight .NET SDK 참조](http://go.microsoft.com/fwlink/?LinkId=529017)를 참조하세요. Windows에서 실행되는 HDInsight 클러스터에만 적용됩니다.
   >
   >

**RDP를 사용 하 여 tooconnect tooa 클러스터**

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **모두 찾아보기** hello 왼쪽된 메뉴에서 클릭 **HDInsight 클러스터**, 클러스터 이름을 클릭 합니다.
3. 클릭 **설정** hello 상단 메뉴에서 **원격 데스크톱**합니다.
4. 클릭 **연결** hello 지침을 따릅니다. 연결이 사용 안함인 경우 먼저 활성화해야 합니다. Hello 원격 데스크톱 사용자 이름과 암호를 사용 하 여 했는지 확인 합니다.  Hello 클러스터 사용자 자격 증명을 사용할 수 없습니다.

## <a name="open-hadoop-command-line"></a>Hadoop 명령줄 열기
원격 데스크톱을 사용 하 여 hello Hadoop 명령줄을 사용 하 여 tooconnect toohello 클러스터를 먼저 설정 해야 원격 데스크톱 액세스 toohello 클러스터 hello 이전 섹션에 설명 된 대로 합니다.

**tooopen Hadoop 명령줄**

1. 원격 데스크톱을 사용 하 여 toohello 클러스터에 연결 합니다.
2. Hello 바탕 화면에서 두 번 클릭 **Hadoop 명령줄**합니다.

    ![HDI.HadoopCommandLine][image-hadoopcommandline]

    Hadoop 명령에 대한 자세한 내용은 [Hadoop 명령 참조](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html)(영문)를 참조하세요.

Hello 이전 스크린 샷 hello 폴더 이름에는 내장 된 hello Hadoop 버전 번호를 있습니다. hello 버전 번호 수에 따라 hello 변경 된 버전의 hello Hadoop 구성 요소가 hello 클러스터에 설치 합니다. Hadoop 환경 변수 toorefer toothose 폴더를 사용할 수 있습니다. 예:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>다음 단계
이 문서에서는 방법을 사용 하 여 HDInsight 클러스터 toocreate hello 포털 및 tooopen Hadoop 명령줄 도구를 hello 하는 방법을 배웠습니다. 더 toolearn hello 다음 문서를 참조:

* [Azure PowerShell을 사용하여 HDInsight 관리](hdinsight-administer-use-powershell.md)
* [Azure CLI를 사용하여 HDInsight 관리](hdinsight-administer-use-command-line.md)
* [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)
* [프로그래밍 방식으로 Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Azure HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Azure HDInsight에 포함된 Hadoop 버전](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Hadoop 명령줄"
