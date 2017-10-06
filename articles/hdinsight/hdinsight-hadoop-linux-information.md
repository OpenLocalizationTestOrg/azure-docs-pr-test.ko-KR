---
title: "Linux 기반 HDInsight-Azure의 Hadoop을 사용 하기 위한 aaaTips | Microsoft Docs"
description: "Linux 기반 HDInsight (Hadoop) 클러스터에서 Azure 클라우드 hello 실행 중인 Linux 친숙 한 환경에서 사용 하기 위한 구현 팁을 가져옵니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Linux에서 HDInsight 사용에 관한 정보

Azure HDInsight 클러스터 hello Azure 클라우드에에서 실행 되는 친숙 한 Linux 환경에서 Hadoop을 제공 합니다. 대부분의 작업에 대해 Linux 설치에서 모든 다른 Hadoop으로 정확하게 작동해야 합니다. 이 문서를 알고 있어야 하는 특정 차이점을 호출합니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

대부분이 문서의 단계 hello hello 다음 toobe 시스템에 설치 해야 할 수 있는 유틸리티를 사용 합니다.

* [cURL](https://curl.haxx.se/) -웹 기반 서비스와 toocommunicate 사용
* [jq](https://stedolan.github.io/jq/) -tooparse JSON 문서를 사용 합니다.
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (미리 보기)-tooremotely 사용 되는 Azure 서비스 관리

## <a name="users"></a>사용자

[도메인에 가입](hdinsight-domain-joined-introduction.md)되어 있지 않으면 HDInsight를 **단일 사용자** 시스템으로 간주하기 때문에 Hello 클러스터 관리자의 권한 가진 단일 SSH 사용자 계정을 생성 됩니다. 추가 SSH 계정을 만들 수 있지만 관리자 액세스 toohello 클러스터도 가집니다.

도메인 가입 HDInsight에서는 여러 사용자와 세분화된 권한 및 역할 설정을 지원합니다. 자세한 내용은 [도메인 가입 HDInsight 클러스터 구성](hdinsight-domain-joined-manage.md)을 참조하세요.

## <a name="domain-names"></a>도메인 이름

hello 정규화 된 도메인 이름 (FQDN) toouse toohello 클러스터 hello은 인터넷에서 연결할 때  **&lt;clustername >. azurehdinsight.net** 또는 SSH에만 해당) (용  **&lt;clustername-ssh >. azurehdinsight.net**합니다.

내부적으로 hello 클러스터의 각 노드 이름이 지정 된 클러스터 구성 중에 할당 합니다. toofind hello 클러스터 이름 참조 hello **호스트** hello Ambari 웹 UI에는 페이지입니다. 또한 hello tooreturn hello Ambari REST API에서에서 호스트를 목록은 다음을 사용할 수 있습니다.

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

대체 **암호** hello 관리자 계정의 hello 암호로 및 **CLUSTERNAME** 클러스터의 hello 이름의 합니다. 이 명령은 hello 클러스터에서 hello 호스트의 목록을 포함 하는 JSON 문서를 반환 합니다. 사용 되는 tooextract hello Jq `host_name` 각 호스트에 대 한 요소 값입니다.

특정 서비스에 대 한 hello 노드의 toofind hello 이름을 해야 할 경우에 해당 구성 요소에 대 한 Ambari를 쿼리할 수 있습니다. 예를 들어 hello HDFS 이름 노드에 대 한 toofind hello 호스트 hello 다음 명령을 사용 합니다.

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

이 명령은 hello 서비스를 설명 하는 JSON 문서를 반환 하 고 다음 jq 추출만 hello `host_name` hello 호스트에 대 한 값입니다.

## <a name="remote-access-tooservices"></a>원격 액세스 tooservices

* **Ambari(웹)** - https://&lt;clustername>.azurehdinsight.net

    Hello 클러스터 관리자 사용자와 암호를 사용 하 여 인증 하 고 tooAmbari 로그인.

    인증은 일반 텍스트로-항상 사용 하 여 HTTPS toohelp hello 연결이 안전한을 확인 합니다.

    > [!IMPORTANT]
    > 일부의 hello 웹 Ui 내부 도메인 이름을 사용 하 여 Ambari 액세스 노드를 통해 사용할 수 있습니다. 내부 도메인 이름을 통해 공개적으로 액세스할 수 없는 인터넷 hello 합니다. Hello 인터넷을 통해 tooaccess 일부 기능을 시도할 때 "서버를 찾을 수 없습니다." 오류가 발생할 수 있습니다.
    >
    > toouse hello hello Ambari web UI의 전체 기능 SSH 터널 tooproxy 웹 트래픽 toohello 클러스터 헤드 노드 사용. 참조 [사용 하 여 SSH 터널링 tooaccess Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie, 및 기타 웹 Ui](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari(REST)** - https://&lt;clustername>.azurehdinsight.net/ambari

    > [!NOTE]
    > Hello 클러스터 관리자가 사용자 및 암호를 사용 하 여 인증 합니다.
    >
    > 인증은 일반 텍스트로-항상 사용 하 여 HTTPS toohelp hello 연결이 안전한을 확인 합니다.

* **WebHCat(Templeton)** - https://&lt;clustername>.azurehdinsight.net/templeton

    > [!NOTE]
    > Hello 클러스터 관리자가 사용자 및 암호를 사용 하 여 인증 합니다.
    >
    > 인증은 일반 텍스트로-항상 사용 하 여 HTTPS toohelp hello 연결이 안전한을 확인 합니다.

* **SSH** - &lt;clustername >-ssh.azurehdinsight.net(포트 22 또는 23). 22 포트가 사용 되는 tooconnect toohello 기본 헤드 노드에, 23는 보조 사용 되는 tooconnect toohello입니다. Hello 헤드 노드에 대 한 자세한 내용은 참조 하십시오. [HDInsight에서 Hadoop의 가용성 및 안정성 클러스터](hdinsight-high-availability-linux.md)합니다.

    > [!NOTE]
    > 클라이언트 컴퓨터에서 SSH를 통해 hello 클러스터 헤드 노드만 액세스할 수 있습니다. 연결 되 면 hello 작업자 노드는 헤드 노드에에서 SSH를 사용 하 여 액세스할 수 있습니다.

## <a name="file-locations"></a>파일 위치

Hadoop 관련 파일에 대 한 hello 클러스터 노드에서 있습니다 `/usr/hdp`합니다. 이 디렉터리에 하위 디렉터리를 다음 hello를 포함 되어 있습니다.

* **2.2.4.9-1**: hello 디렉터리 이름이 hello 버전의 hello Hortonworks Data Platform HDInsight에서 사용 되었습니다. 클러스터에 hello 번호 hello 여기에 나열 된 하나 보다 다를 수 있습니다.
* **현재**:이 디렉터리에 hello 아래 링크 toosubdirectories **2.2.4.9-1** 디렉터리입니다. 이 디렉터리가 tooremember hello 버전 번호가 없는 있도록 있습니다.

예제 데이터 및 JAR 파일은 `/example` 및 `/HdiSamples`의 HDFS(Hadoop 분산 파일 시스템)에서 찾을 수 있습니다.

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS, Azure Storage 및 Data Lake Store

대부분의 Hadoop 배포에서 HDFS hello 클러스터의 hello 컴퓨터에서 로컬 저장소에서 지원 됩니다. 계산 리소스에 대해 시간당 또는 분당 비용이 부과되는 클라우드 기반 솔루션의 경우 로컬 저장소를 사용하면 비용이 많이 들 수 있습니다.

HDInsight은 hello 기본 저장소로 Azure 저장소에서 blob 또는 Azure 데이터 레이크 저장소를 사용합니다. 이러한 서비스 혜택을 따라 hello를 제공 합니다.

* 저렴한 장기 저장소
* 웹 사이트, 파일 업로드/다운로드 유틸리티, 다양한 언어 SDK 및 웹 브라우저와 같은 외부 서비스에 액세스할 수 있음

> [!WARNING]
> HDInsight는 __범용__ Azure Storage 계정만 지원합니다. Hello 현재 지원 하지 않는 __Blob 저장소__ 계정 유형입니다.

각 blob (또는 HDInsight 관점에서 파일) 으로만 too195 GB를 이동할 수 있지만 Azure 저장소 계정이 too4.75 TB 보유할 수 있습니다. Azure 데이터 레이크 저장소 동적으로 늘릴 수 toohold trillions의 파일을 개별 파일로 페타바이트 보다 큰 합니다. 자세한 내용은 [Blob 이해](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 및 [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)를 참조하세요.

Azure 저장소 서비스 또는 데이터 레이크 저장소 중 하나를 사용할 때 않아도 toodo HDInsight tooaccess hello 데이터에서 특별 한 됩니다. 다음 명령을 hello hello에 파일을 나열 하는 예를 들어 `/example/data` 데이터 레이크 저장소 또는 Azure 저장소에 저장 되어 있는지 여부에 관계 없이 폴더:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>URI 및 구성표

일부 명령은 해야 toospecify hello 구성표 hello URI의 일환으로 파일에 액세스할 때. 예를 들어 hello 스톰 HDFS 구성 하려면 toospecify hello 구성표 합니다. 기본이 아닌 저장소 ("추가" 저장소 toohello 클러스터로 추가 된 저장소)를 사용 하는 경우에 hello URI의 일부로 항상 hello 체계를 사용 해야 합니다.

사용 하는 경우 __Azure 저장소__, hello URI 체계를 다음 중 하나를 사용 합니다.

* `wasb:///`: 암호화되지 않은 통신을 사용하여 기본 저장소에 액세스합니다.

* `wasbs:///`: 암호화된 통신을 사용하여 기본 저장소에 액세스합니다.  hello wasbs 구성표는 HDInsight 버전 3.6부터 에서만에서 지원 됩니다.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: 기본이 아닌 저장소 계정과 통신할 때 사용됩니다. 예를 들어 추가 저장소 계정이 있거나 공개적으로 액세스할 수 있는 저장소 계정에 저장된 데이터에 액세스하는 경우입니다.

사용 하는 경우 __데이터 레이크 저장소__, hello URI 체계를 다음 중 하나를 사용 합니다.

* `adl:///`: Hello 클러스터에 대 한 hello 기본 데이터 레이크 저장소에 액세스 합니다.

* `adl://<storage-name>.azuredatalakestore.net/`: 기본이 아닌 Data Lake Store와 통신할 때 사용됩니다. HDInsight 클러스터의 hello 루트 디렉터리 외부에 있는 tooaccess 데이터도 사용 됩니다.

> [!IMPORTANT]
> HDInsight에 대 한 hello 기본 저장소로 데이터 레이크 저장소를 사용할 경우 HDInsight 저장소의 hello 루트로 hello 저장소 toouse 내의 경로 지정 해야 합니다. hello 기본 경로 `/clusters/<cluster-name>/`합니다.
>
> 사용 하는 경우 `/` 또는 `adl:///` tooaccess 데이터만 액세스할 수 있습니다 hello 루트에 저장 된 데이터 (예를 들어 `/clusters/<cluster-name>/`) hello 클러스터의 합니다. hello를 사용 하 여 hello 저장소에서 아무 곳 이나 tooaccess 데이터 `adl://<storage-name>.azuredatalakestore.net/` 형식입니다.

### <a name="what-storage-is-hello-cluster-using"></a>저장소는 hello 사용 하 여 클러스터

Hello 클러스터에 대 한 Ambari tooretrieve hello 기본 저장소 구성을 사용할 수 있습니다. 사용 하 여 hello 다음 tooretrieve HDFS 구성 정보 curl을 사용 하 여 명령을 사용 하 여 필터링 [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> 첫 번째 적용 된 구성을 toohello 서버 hello를 반환 합니다. (`service_config_version=1`),이 정보를 포함 하 합니다. Toolist toofind hello 최신 구성 버전을 모두 할 수 있습니다.

이 명령은 다음 Uri 값 비슷한 toohello를 반환 합니다.

* `wasb://<container-name>@<account-name>.blob.core.windows.net` - Azure Storage 계정을 사용하는 경우

    hello 계정 이름은 hello Azure 저장소 계정 이름을 hello를 hello 컨테이너 이름을 hello blob 컨테이너는 hello 클러스터 저장소의 hello 루트는 합니다.

* `adl://home` - Azure Data Lake Store를 사용하는 경우 tooget hello Data Lake 저장소 이름 REST 호출 다음 hello를 사용 합니다.

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    이 명령은 호스트 이름 뒤에 나오는 hello 반환: `<data-lake-store-account-name>.azuredatalakestore.net`합니다.

    HDInsight 사용 하 여 hello REST 호출 다음에 대 한 hello 루트는 hello 저장소 내의 tooget hello 디렉터리:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    이 명령은 경로 경로 비슷한 toohello 반환: `/clusters/<hdinsight-cluster-name>/`합니다.

Azure 포털 hello를 사용 하 여 단계를 수행 하는 hello를 사용 하 여 hello 저장소 정보를 찾을 수 있습니다.

1. Hello에 [Azure 포털](https://portal.azure.com/)를 HDInsight 클러스터를 선택 합니다.

2. Hello에서 **속성** 섹션에서 **저장소 계정은**합니다. hello 클러스터에 대 한 hello 저장소 정보가 표시 됩니다.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>HDInsight 외부에서 파일에 액세스하는 방법

외부 hello HDInsight 클러스터에서 tooaccess 데이터는 다양 한 방법입니다. hello 다음은 몇 가지 링크 tooutilities 및 데이터와 함께 사용 되는 toowork 일 수 있는 Sdk입니다.

사용 하는 경우 __Azure 저장소__, 데이터에 액세스할 수 있도록 하는 방법에 대 한 링크를 따라 hello를 참조 하세요.

* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): Azure로 작업하기 위한 명령줄 인터페이스 명령입니다. 를 설치한 후 hello를 사용 하 여 `az storage` 저장소 사용에 대 한 도움말 명령을 또는 `az storage blob` blob 관련 명령에 대 한 합니다.
* [blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): Azure 저장소의 Blob 작업을 위한 python 스크립트입니다.
* 다양한 SDK:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.JS](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [저장소 REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx)

사용 하는 경우 __Azure 데이터 레이크 저장소__, 데이터에 액세스할 수 있도록 하는 방법에 대 한 링크를 따라 hello를 참조 하세요.

* [웹 브라우저](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Azure CLI 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [WebHDFS REST API](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>클러스터 크기 조정

기능을 확장 하는 hello 클러스터에서는 클러스터에 의해 사용 되는 데이터 노드 수가 변경 hello toodynamically 있습니다. 클러스터에서 다른 작업 또는 프로세스가 실행되는 동안 크기 조정 작업을 수행할 수 있습니다.

hello 다른 클러스터 종류는 다음과 같이 확장 하 여 영향을 받습니다.

* **Hadoop**: hello 클러스터에서 hello 서비스의 일부 hello 클러스터의 노드 수를 줄일 때는 다시 시작 됩니다. 실행 중이거나 toofail hello hello 크기 조정 작업이 완료 될 때 보류 중인 작업을 크기 조정 작업이 발생할 수 있습니다. Hello 작업이 완료 되 면 hello 작업을 다시 전송할 수 있습니다.
* **HBase**: 지역 서버 hello 크기 조정 작업이 완료 된 후 몇 분 안에 자동으로 균형이 조정 됩니다. toomanually 균형 지역 서버 hello 다음 단계를 사용 합니다.

    1. SSH를 사용 하 여 toohello HDInsight 클러스터를 연결 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

    2. Hello 다음 toostart hello HBase 셸을 사용 합니다.

            hbase shell

    3. HBase 셸 hello 로드 되 면 다음 toomanually 균형 hello 지역 서버 hello를 사용 합니다.

            balancer

* **Storm**: 크기 조정 작업을 수행한 후 실행 중인 모든 Storm 토폴로지 균형을 다시 맞추어야 합니다. 균형 조정 hello 새 hello 클러스터의 노드 수에 따라 hello 토폴로지 tooreadjust 병렬 처리 수준 설정 수 있습니다. toorebalance 토폴로지, 실행 hello 다음 옵션 중 하나를 사용 합니다.

    * **SSH**: toohello 서버 연결 및 사용 하 여 hello 다음 명령은 toorebalance 토폴로지:

            storm rebalance TOPOLOGYNAME

        원래 hello 토폴로지에서 제공 하는 매개 변수 toooverride hello 병렬 처리 수준 힌트를 지정할 수 있습니다. 예를 들어 `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` 다시 구성 합니다. hello 토폴로지 too5 작업자 프로세스, hello 배출구 파랑 구성 요소에 대 한 3 executor 및 hello 노란색 볼트 구성 요소에 대 한 단일 한 10 실행 합니다.

    * **Storm UI**: 사용 하 여 hello 다음 단계 toorebalance hello 스톰 UI를 사용 하는 토폴로지입니다.

        1. 열기 **https://CLUSTERNAME.azurehdinsight.net/stormui** 여기서 CLUSTERNAME은 hello 이름 Storm 클러스터의 웹 브라우저에서 합니다. 메시지가 표시 되 면 hello HDInsight 클러스터 (관리) 관리자 이름과 hello 클러스터를 만들 때 지정한 암호를 입력 합니다.
        2. Toorebalance, 원하는 선택한 다음 하면 hello hello 토폴로지를 선택 **균형을 다시 조정할** 단추입니다. Hello를 리 밸런스 작업이 수행 되기 전에 hello 지연 시간을 입력 합니다.

HDInsight 클러스터 크기 조정에 대한 자세한 내용은 다음을 참조하세요.

* [Hello Azure 포털을 사용 하 여 HDInsight의 Hadoop 클러스터를 관리 합니다.](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터 관리](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Hue(또는 다른 Hadoop 구성 요소)를 어떻게 설치합니까?

HDInsight는 관리 서비스입니다. Azure에서 hello 클러스터 문제를 발견 하면 hello 노드 실패를 삭제 하 고 노드 tooreplace를 만들 수 있습니다 것입니다. Hello 클러스터에서 작업을 수동으로 설치 하면이 작업이 수행 될 때 보관 되지 않습니다. 대신 [HDInsight 스크립트 동작](hdinsight-hadoop-customize-cluster.md)을 사용합니다. 스크립트 동작 변경 내용에 따라 사용 되는 toomake hello 될 수 있습니다.

* Spark 또는 Hue와 같은 서비스 또는 웹 사이트를 설치하고 구성합니다.
* 설치 및 구성 하려면 hello 클러스터의 여러 노드에 구성을 변경 해야 하는 구성 요소. 예를 들어 필수 환경 변수, 로깅 디렉터리 만들기 또는 구성 파일 만들기입니다.

스크립트 동작은 Bash 스크립트입니다. hello 스크립트 클러스터 프로 비전 중에 실행 사용된 tooinstall과 가능 hello 클러스터에서 추가 구성 요소를 구성 합니다. 예제 스크립트는 다음과 같은 구성 요소가 hello를 설치 하기 위한 제공 됩니다.

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

사용자 고유의 스크립트 작업 개발에 대한 정보는 [HDInsight를 사용하여 스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.

### <a name="jar-files"></a>Jar 파일

일부 Hadoop 기술은 MapReduce 작업의 일부로 사용되거나 Pig 또는 Hive 내부에서 사용되는 함수를 포함하는 자체 포함된 jar 파일에 제공되어 있습니다. 이러한 스크립트 동작을 사용 하 여 설치할 수 있습니다, 종종 모든 설치에 필요 하지 않습니다 및 수 업로드 된 toohello 클러스터 프로 비전 한 후 있으며 직접 사용 합니다. 후에 유지 되는 toomake 있는지 hello 구성 요소에는 hello 클러스터의 이미지로 다시 설치 합니다 (WASB 또는 ADL) 클러스터에 대 한 hello jar 파일 hello 기본 저장소에 저장할 수 있습니다.

예를 들어, toouse 최신 버전의 hello [DataFu](http://datafu.incubator.apache.org/), hello 프로젝트를 포함 하는 jar를 다운로드 하 고 toohello HDInsight 클러스터를 업로드할 수 있습니다. 다음 방법에 hello DataFu 설명서에 따라 toouse에서 Pig 또는 Hive 합니다.

> [!IMPORTANT]
> 일부 구성 요소를 독립 실행형 jar 파일 HDInsight에 함께 제공 되 있지만 hello 경로에 되지는 않습니다. 특정 구성 요소에 대 한 원하는 경우에 클러스터에에 대 한 hello 따라 toosearch를 사용할 수 있습니다.
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> 이 명령은 모든 일치 하는 jar 파일의 hello 경로 반환합니다.

toouse 다른 버전의 구성 요소를 업로드 hello 버전 및 작업에 사용 해야 합니다.

> [!WARNING]
> Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원 하 고 Microsoft 지원 tooisolate 도와 관련된 toothese 구성 요소 문제를 해결 합니다.
>
> 사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다. 이 hello 문제를 해결 하거나 hello에 대 한 사용 가능한 채널 tooengage 열면 해당 기술에 대 한 심층 전문 지식이 있는 소스 기술을 요청 될 수 있습니다. 예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. 또한 Apache 프로젝트에는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/)).

## <a name="next-steps"></a>다음 단계

* [Windows 기반 HDInsight tooLinux 기반에서 마이그레이션](hdinsight-migrate-from-windows-to-linux.md)
* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 MapReduce 작업 사용](hdinsight-use-mapreduce.md)
