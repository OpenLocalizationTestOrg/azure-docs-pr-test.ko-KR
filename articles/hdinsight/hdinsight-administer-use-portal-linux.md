---
title: "Azure 포털을 사용 하 여 HDInsight 클러스터를 aaaManage Hadoop | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Azure 포털을 사용 하 여 HDInsight 클러스터를 관리 하 고 있습니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 HDInsight의 Hadoop 클러스터를 관리 합니다.
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Hello를 사용 하 여 [Azure 포털][azure-portal], Azure HDInsight의 Hadoop 클러스터를 관리할 수 있습니다. 다른 도구를 사용 하 여 HDInsight의 Hadoop 클러스터 관리에 대 한 내용은 hello 탭 선택기를 사용 합니다.

**필수 구성 요소**

이 문서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

## <a name="open-hello-portal"></a>열기 hello 포털
1. 역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.
2. Hello 포털을 연 후 다음 작업을 수행할 수 있습니다.

   * 클릭 **새로** hello 왼쪽된 메뉴 toocreate 새 클러스터에서에서:

       ![새 HDInsight 클러스터 단추](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * 클릭 **HDInsight 클러스터** hello에서 왼쪽된 메뉴 toolist hello 기존 클러스터

       ![Azure 포털 HDInsight 클러스터 단추](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       HDInsight 클러스터를 클릭 하 여 표시 되지 않으면 **더 많은 서비스** hello 목록의 아래쪽 hello 되 고 클릭 **HDInsight 클러스터** hello에서 **인텔리전스 + 분석** 단원을 참조 하십시오입니다.


## <a name="create-clusters"></a>클러스터 만들기
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight는 다양한 Hadoop 구성 요소에서 작동합니다. Hello 구성 요소 확인 및 지원 된 hello 목록에 대 한 참조 [Azure HDInsight의 Hadoop의 어떤 버전은](hdinsight-component-versioning.md)합니다. Hello 일반 클러스터 만든 정보를 참조 하십시오. [HDInsight 클러스터를 만드는 Hadoop](hdinsight-hadoop-provision-linux-clusters.md)합니다.

### <a name="access-control-requirements"></a>액세스 제어 요구 사항

HDInsight 클러스터를 만들 때 Azure 구독을 지정해야 합니다. 새 Azure 리소스 그룹 또는 기존 리소스 그룹에서 이 클러스터를 만들 수 있습니다. HDInsight 클러스터를 만들기 위한 다음 단계 tooverify hello 사용 권한을 사용할 수 있습니다.

- toouse 기존 리소스 그룹입니다.

    1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
    2. 클릭 **리소스 그룹** hello 왼쪽된 메뉴 toolist hello 리소스 그룹에서 합니다.
    3. HDInsight 클러스터를 만들기 위한 toouse 원하는 hello 리소스 그룹을 클릭 합니다.
    4. 클릭 **액세스 제어 (IAM)**, 되어 있는지 확인 하 고 사용자 (또는 사용자가 속한 그룹)가 적어도 참가자 액세스 toohello 리소스 그룹을 hello 합니다.

- toocreate 새 리소스 그룹

    1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
    2. 클릭 **구독** hello 왼쪽된 메뉴에서 합니다. 노란색 키 아이콘이 있습니다. 구독의 목록이 표시됩니다.
    3. Toocreate 클러스터를 사용 하는 hello 구독을 클릭 합니다. 
    4. **내 사용 권한**을 클릭합니다.  표시 프로그램 [역할](../active-directory/role-based-access-control-what-is.md#built-in-roles) hello 가입 합니다. 최소한 필요한 참가자 액세스 toocreate HDInsight 클러스터입니다.

Hello NoRegisteredProviderFound 오류 또는 hello MissingSubscriptionRegistration 오류를 표시 되 면 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](../azure-resource-manager/resource-manager-common-deployment-errors.md)합니다.

## <a name="list-and-show-clusters"></a>클러스터 나열 및 표시
1. 역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.
2. 클릭 **HDInsight 클러스터** hello에서 왼쪽된 메뉴 toolist hello 기존 클러스터입니다.
3. Hello 클러스터 이름을 클릭 합니다. Hello 클러스터 목록이 긴 경우에 hello hello 페이지 위쪽에 필터를 사용할 수 있습니다.
4. Hello 목록 toosee hello 개요 페이지에서 클러스터를 클릭 합니다.

    ![Azure Portal HDInsight 클러스터 요점](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **대시보드**: Linux 기반 클러스터용 Ambari Web 즉 열립니다 hello 클러스터 대시보드 합니다.
    * **Secure Shell**: SSH (보안 셸) 연결을 사용 하 여 표시 hello 지침 tooconnect toohello 클러스터입니다.
    * **클러스터의 크기를 조정**:이 클러스터에 대 한 toochange hello 작업자 노드 수를 허용 합니다.
    * **삭제**: hello 클러스터를 삭제 합니다.
    * **활동 로그**: 활동 로그를 표시하고 쿼리합니다.
    * **Access Control(IAM)**: 역할 할당을 사용합니다.  참조 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)합니다.
    * **태그**: 있습니다 tooset 키/값 쌍 toodefine 클라우드 서비스의 사용자 정의 분류를 허용 합니다. 예를 들어 **project**라는 키를 만든 다음 특정 프로젝트와 연결된 모든 서비스에 공통 값을 사용할 수 있습니다.
    * **문제 진단 및 해결**: 문제 해결 정보를 표시합니다.
    * **Locks**: 수정 되거나 삭제 잠금 tooprevent hello 클러스터 되 고 추가 합니다.
    * **자동화 스크립트**: hello 클러스터에 대 한 hello Azure 리소스 관리자 템플릿을 표시 및 내보내기. 현재 hello 종속 Azure 저장소 계정만 내보낼 수 있습니다. [Azure Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md)를 참조하세요.
    * **빠른 시작**: HDInsight를 사용하여 시작하는 데 도움이 되는 정보를 표시합니다.
    * **HDInsight용 도구**: HDInsight 관련 도구에 대한 도움말 정보입니다.
    * **로그인 클러스터**: hello 클러스터 로그인 정보를 표시 합니다.
    * **구독 코어 사용량**: 디스플레이 hello 구독에 대 한 사용 되지 않으며 사용 가능한 코어입니다.
    * **클러스터의 크기를 조정**: 증가 및 감소 hello 클러스터 작업자 노드 수입니다. [클러스터 크기 조정](hdinsight-administer-use-management-portal.md#scale-clusters)을 참조하세요.
    * **Secure Shell**: SSH (보안 셸) 연결을 사용 하 여 표시 hello 지침 tooconnect toohello 클러스터입니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.
    * **HDInsight 파트너**: 현재 HDInsight 파트너를 hello 추가/제거 합니다.
    * **외부 Metastore**: hello Hive 및 Oozie metastore를 확인 합니다. hello metastore hello 클러스터를 만드는 프로세스 동안만 구성할 수 있습니다. [Hive/Oozie metastore 사용](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore)을 참조하세요.
    * **스크립트 작업을**: hello 클러스터에서 스크립트를 이용한 적 실행 합니다. [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.
    * **응용 프로그램**: HDInsight 응용 프로그램을 추가/제거합니다.  [사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md)를 참조하세요.
    * **속성**: hello 클러스터 속성을 확인 합니다.
    * **저장소 계정**: hello 저장소 계정 및 hello 키를 확인 합니다. hello 저장소 계정은 hello 클러스터를 만드는 프로세스 동안 구성 됩니다.
    * **클러스터 AAD ID**:
    * **새로운 지원 요청**: toocreate Microsoft 지원에 지원 티켓을 허용 합니다.
    
6. **속성**을 클릭합니다.

    hello 속성은 같습니다.

   * **호스트 이름**: 클러스터 이름입니다.
   * **클러스터 URL**. hello Ambari 웹 인터페이스에 대 한 hello URL입니다.
   * **상태**: 중단됨, 수락됨, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, 운영, 실행 중, 오류, 삭제 중, 삭제됨, 시간 초과됨, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization를 포함합니다.
   * **지역**: Azure 위치입니다. 목록이 지원 되는 Azure 위치에 대 한 참조 hello **지역** 드롭다운 목록 상자 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.
   * **만든 날짜**
   * **운영 체제**: **Windows** 또는 **Linux**입니다.
   * **형식**: Hadoop, HBase, Storm, Spark.
   * **버전**. [HDInsight 버전](hdinsight-component-versioning.md)
   * **구독**: 구독 이름입니다.
   * **기본 데이터 원본을**: hello 기본 클러스터 파일 시스템입니다.
   * **작업자 노드 크기**
   * **헤드 노드 크기**

## <a name="delete-clusters"></a>클러스터 삭제
클러스터를 삭제 해도 hello 기본 저장소 계정 또는 연결 된 저장소 계정을 사용 하는 삭제 되지 않습니다. 사용 하 여 hello 클러스터를 다시 만들 수 있습니다 hello 동일한 저장소 계정 및 동일한 metastore hello 합니다. hello 클러스터를 다시 만들 때 toouse 새 기본 Blob 컨테이너를 권장 합니다.

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다. **HDInsight 클러스터**가 표시되지 않으면 먼저 **추가 서비스**를 클릭합니다.
3. Toodelete hello 클러스터를 클릭 합니다.
4. 클릭 **삭제** hello 위쪽 메뉴에서 다음 hello 지침을 따릅니다.

참고 항목: [클러스터 일시 중지/종료](#pauseshut-down-clusters)

## <a name="add-additional-storage-accounts"></a>추가 저장소 계정 추가

클러스터를 만든 후 Azure Storage 계정 및 Azure Data Lake Store 계정을 더 추가할 수 있습니다. 자세한 내용은 참조 [추가 저장소 계정을 tooHDInsight 추가](./hdinsight-hadoop-add-storage.md)합니다.

## <a name="scale-clusters"></a>클러스터 크기 조정
hello 클러스터 기능을 확장 하면 toochange hello toore 필요 없이 Azure HDInsight에서 실행 되는 클러스터에서 사용 하는 작업자 노드 수-hello 클러스터를 만듭니다.

> [!NOTE]
> HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다. 클러스터의 hello 버전을 잘 모를 경우 hello 속성 페이지를 확인할 수 있습니다.  [클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.
>
>

hello HDInsight에서 지원 되는 클러스터의 각 형식에 대 한 데이터 노드 수를 변경 하는 hello 미치는 영향:

* Hadoop은

    원활 하 게 hello 보류 중 또는 실행 중인 작업이 모두 영향을 주지 않고 실행 되는 Hadoop 클러스터의 작업자 노드 수를 늘릴 수 있습니다. Hello 작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다. 크기 조정 작업의 오류는 hello 클러스터는 항상를 작동 상태로 남아 있도록 정상적으로 처리 됩니다.

    Hadoop 클러스터는 hello 데이터 노드 수를 줄여 규모 축소, hello 클러스터의 hello 서비스 중 일부를 다시 시작 됩니다. 이 동작은 실행 중인 모든 및 hello hello 크기 조정 작업이 완료 될 때 작업 toofail 보류 중. 그러나 hello 작업이 완료 되 면 hello 작업을 다시 전송할을 수 있습니다.
* HBase

    원활 하 게 추가 하거나 실행 하는 동안 노드 tooyour HBase 클러스터를 제거할 수 있습니다. 지역 서버는 hello 크기 조정 작업을 완료 하는 몇 분 안에 자동으로 균형이 조정 됩니다. 그러나 명령을 명령 프롬프트 창에서 다음 실행 중인 hello와 클러스터의 헤드 노드에 toohello에 로그인 하 여 hello 지역 서버를 수동으로 분산 시킬 수 있습니다 있습니다.

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Hello HBase 셸을 사용 하 여에 대 한 자세한 내용은 참조 하십시오.
* Storm

    원활 하 게 추가 하거나 실행 하는 동안 데이터 노드 tooyour Storm 클러스터를 제거할 수 있습니다. 하지만 hello 크기 조정 작업을 성공적으로 완료 한 후 toorebalance hello 토폴로지를 해야 합니다.

    다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.

  * Storm 웹 UI
  * 명령줄 인터페이스(CLI) 도구

    Toohello 참조 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 내용을 확인 합니다.

    hello 스톰 웹 UI hello HDInsight 클러스터에서 제공 됩니다.

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    다음은 예제 어떻게 toouse hello CLI 명령을 toorebalance hello 스톰 토폴로지:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale 클러스터**

1. Toohello 로그인 [포털][azure-portal]합니다.
2. 클릭 **HDInsight 클러스터** hello 왼쪽된 메뉴에서 합니다.
3. Tooscale hello 클러스터를 클릭 합니다.
3. **클러스터 크기 조정**을 클릭합니다.
4. **작업자 노드 수**를 입력합니다. 클러스터 노드의 hello 수 제한을 15 hello Azure 구독 마다 다릅니다. 청구 지원 tooincrease hello 제한을 문의할 수 있습니다.  hello 비용 정보 hello 변경 사항을 toohello 노드 수를 반영 합니다.

    ![HDinsight Hadoop Hbase Storm Spark 크기 조정](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>클러스터 일시 중지/종료

대부분의 Hadoop 작업은 이따금 실행되는 일괄 처리 작업입니다. 대부분의 Hadoop 클러스터에 대 한는 오랜 시간 해당 hello 클러스터 사용 하지 않는 처리를 위해 합니다. HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.
HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다. Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다.

여러 가지 방법으로 hello 프로세스를 프로그래밍할 수 있습니다.

* 사용자 Azure 데이터 팩터리. 주문형 HDInsight 연결된 서비스 만들기는 [Azure Data Factory를 사용하여 HDInsight에서 주문형 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-adf.md) 를 참조하세요.
* Azure PowerShell 사용  [비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)을 참조하세요.
* Azure CLI 사용 [Azure CLI를 사용하여 HDInsight 클러스터 관리](hdinsight-administer-use-command-line.md)를 참조하세요.
* HDInsight .NET SDK 사용 [Hadoop 작업 제출](hdinsight-submit-hadoop-jobs-programmatically.md)을 참조하세요.

가격 책정 정보는 hello에 대 한 참조 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다. hello 포털에서에서 클러스터 toodelete 참조 [클러스터를 삭제 합니다.](#delete-clusters)


## <a name="upgrade-clusters"></a>클러스터 업그레이드

참조 [업그레이드 HDInsight 클러스터 tooa 최신 버전이](./hdinsight-upgrade-cluster.md)합니다.

## <a name="change-passwords"></a>암호 변경
HDInsight 클러스터마다 두 개의 사용자 계정이 포함될 수 있습니다. HDInsight 클러스터 사용자 계정 (규칙 하위 hello HTTP 사용자 계정) 하 고 hello 만드는 프로세스 동안 hello SSH 사용자 계정이 만들어집니다. Hello Ambari 웹 UI toochange hello 클러스터 사용자 계정 사용자 이름 및 암호와 스크립트 동작 toochange hello SSH 사용자 계정 사용할 수 있습니다.

### <a name="change-hello-cluster-user-password"></a>Hello 클러스터 사용자 암호 변경
Hello Ambari 웹 UI toochange hello 클러스터 사용자 암호를 사용할 수 있습니다. tooAmbari에 toolog, hello 기존 클러스터 사용자 이름 및 암호 사용 해야 합니다.

> [!NOTE]
> Hello 클러스터 사용자 (관리자) 암호를 변경할이 클러스터 toofail에 대 한 작업을 실행 하는 스크립트를 발생할 수 있습니다. 작업자 노드를 대상으로 하는 지속형된 스크립트 동작을 설정한 경우 이러한 스크립트는 크기 조정 작업을 통해 toohello 클러스터 노드를 추가 하면 실패할 수 있습니다. 스크립트 작업에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.
>
>

1. Toohello Ambari 웹 UI를 사용 하 여 로그인 hello HDInsight 클러스터에 대 한 사용자 자격 증명입니다. hello 기본 사용자 이름은 **admin**. URL은 hello **https://&lt;HDInsight 클러스터 이름 > azurehdinsight.net**합니다.
2. 클릭 **Admin** hello 상단 메뉴에서 다음 "관리 Ambari"를 클릭 합니다.
3. Hello 왼쪽된 메뉴에서 클릭 **사용자**합니다.
4. **Admin**을 클릭합니다.
5. **암호 변경**을 클릭합니다.

Ambari는 hello 클러스터의 모든 노드에서 hello 암호를 변경합니다.

### <a name="change-hello-ssh-user-password"></a>Hello SSH 사용자 암호 변경
1. Hello 이라는 파일로 텍스트를 다음 텍스트 편집기를 사용 하 여 저장할 **changepassword.sh**합니다.

   > [!IMPORTANT]
   > Hello 줄 끝으로 LF를 사용 하는 편집기를 사용 해야 합니다. Hello 편집기에서는 CRLF hello 스크립트 작동 하지 않습니다.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. HTTP 또는 HTTPS 주소를 사용 하 여 HDInsight에서 액세스할 수 있는 hello 파일 tooa 저장 위치를 업로드 합니다. 예를 들어 OneDrive 또는 Azure Blob 저장소와 같은 공용 파일 저장소입니다. 이 URI는 hello 다음 단계에서 필요에 따라 hello URI (HTTP 또는 HTTPS 주소) toohello 파일을 저장 합니다.
3. Hello Azure 포털에서에서 클릭 **HDInsight 클러스터**합니다.
4. HDInsight 클러스터를 클릭합니다.
4. **스크립트 작업**을 클릭합니다.
4. Hello에서 **스크립트 동작** 블레이드를 **새 제출**합니다. Hello 때 **스크립트 동작을 제출** 블레이드 나타나면 hello 다음 정보를 입력 합니다.

   | 필드 | 값 |
   | --- | --- |
   | Name |SSH 암호 변경 |
   | Bash 스크립트 URI |hello URI toohello changepassword.sh 파일 |
   | 노드(헤드, 작업자, Nimbus, 감독자, Zookeeper 등) |나열된 모든 노드 형식에 대한 ✓ |
   | 매개 변수 |Hello SSH 사용자 이름이 고 hello 새 암호를 입력 합니다. Hello 사용자 이름 및 암호 hello 사이 공백을 하나 있어야 합니다. |
   | 이 스크립트 작업을 유지... |이 필드는 선택 취소로 둡니다. |
5. 선택 **만들기** tooapply hello 스크립트입니다. Hello 스크립트 완료 SSH를 사용 하 여 hello 새 암호로 수 tooconnect toohello 클러스터 됩니다.

## <a name="grantrevoke-access"></a>액세스 권한 부여/해지
HDInsight 클러스터에는 HTTP 웹 서비스 (모든 이러한 서비스는 RESTful 끝점)를 수행 하는 hello:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다. 있습니다 수 revoke/부여 사용 하 여 hello 액세스 [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) 및 [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access)합니다.

## <a name="find-hello-subscription-id"></a>Hello 구독 ID 찾기

**toofind Azure 구독 Id**

1. Toohello 로그인 [포털][azure-portal]합니다.
2. **구독**을 클릭합니다. 각 구독에는 이름 및 ID가 있습니다.

각 클러스터는 동 점된 tooan Azure 구독. hello 클러스터에 ID를 표시 하는 구독 hello **필수** 바둑판식으로 배열입니다. [클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.

## <a name="find-hello-resource-group"></a>Hello 리소스 그룹 찾기
Hello Azure 리소스 관리자 모드에서 각 HDInsight 클러스터는 Azure 리소스 관리자 그룹이 생성 됩니다. 클러스터에 tooappears 속해 있는 hello 리소스 관리자 그룹:

* hello 클러스터 목록에는 **리소스 그룹** 열입니다.
* 클러스터 **Essential** 타일.  

[클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.

## <a name="find-hello-default-storage-account"></a>Hello 기본 저장소 계정 찾기
각 HDInsight 클러스터에는 기본 저장소 계정이 있습니다. 아래에 표시 하는 클러스터에 대 한 기본 저장소 계정 및 해당 키를 hello **저장소 계정은**합니다. [클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.

## <a name="run-hive-queries"></a>Hive 쿼리 실행
Hello Azure 포털에서 직접 하이브 작업을 실행할 수 없습니다 되지만 hello Ambari 웹 UI에서 하이브 보기를 사용할 수 있습니다.

**Ambari 하이브 보기를 사용 하 여 toorun 하이브 쿼리**

1. Toohello Ambari 웹 UI를 사용 하 여 로그인 hello HDInsight 클러스터에 대 한 사용자 자격 증명입니다. hello 기본 사용자 이름은 **admin**. URL은 hello **https://&lt;HDInsight 클러스터 이름 > azurehdinsight.net**합니다.
2. Hello 스크린 샷 뒤에 표시 된 대로 하이브 보기를 엽니다.  

    ![HDInsight Hive 보기](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. 클릭 **쿼리** hello 상단 메뉴에서 합니다.
4. **쿼리 편집기**에서 Hive 쿼리를 입력한 다음 **실행**을 클릭합니다.

## <a name="monitor-jobs"></a>작업 모니터링
참조 [hello Ambari 웹 UI를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md#monitoring)합니다.

## <a name="browse-files"></a>파일 찾아보기
Hello Azure 포털을 사용 하 여 hello 기본 컨테이너의 hello 내용을 찾아볼 수 있습니다.

1. 역시 로그인[https://portal.azure.com](https://portal.azure.com)합니다.
2. 클릭 **HDInsight 클러스터** hello에서 왼쪽된 메뉴 toolist hello 기존 클러스터입니다.
3. Hello 클러스터 이름을 클릭 합니다. Hello 클러스터 목록이 긴 경우에 hello hello 페이지 위쪽에 필터를 사용할 수 있습니다.
4. 클릭 **저장소 계정은** hello 클러스터 왼쪽된 메뉴에서 합니다.
5. Storage 계정을 클릭합니다.
7. Hello 클릭 **Blob** 바둑판식으로 배열입니다.
8. Hello 기본 컨테이너 이름을 클릭 합니다.

## <a name="monitor-cluster-usage"></a>클러스터 사용 현황 모니터링
hello **사용** hello HDInsight 클러스터 블레이드의 섹션에는 hello HDInsight 함께 사용할 사용 가능한 tooyour 구독 코어 수가 hello toothis 클러스터 하 게 하는 방법을 할당 하는 코어 수에 대 한 정보가 표시 됩니다. 이 클러스터 내에서 hello 노드에 대 한 할당. [클러스터 나열 및 표시](#list-and-show-clusters)를 참조하세요.

> [!IMPORTANT]
> HDInsight 클러스터 hello에서 toomonitor hello 서비스 제공, Ambari Web을 사용 하거나 REST API Ambari hello 해야 합니다. Ambari 사용에 대한 자세한 내용은 [Ambari를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Tooa 클러스터에 연결

* [HDInsight에서 Hive 사용](hdinsight-hadoop-use-hive-ambari-view.md)
* [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>다음 단계
이 문서에서는 몇 가지 기본 관리 함수에 대해 배웠습니다. 더 toolearn hello 다음 문서를 참조:

* [Azure PowerShell을 사용하여 HDInsight 관리](hdinsight-administer-use-powershell.md)
* [Azure CLI를 사용하여 HDInsight 관리](hdinsight-administer-use-command-line.md)
* [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)
* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 Sqoop 사용](hdinsight-use-sqoop.md)
* [Azure HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Azure HDInsight에 포함된 Hadoop 버전](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Hadoop 명령줄"
