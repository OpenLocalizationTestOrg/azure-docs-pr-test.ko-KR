---
title: "Windows 기반 HDInsight에서 aaaMigrate tooLinux 기반 HDInsight-Azure | Microsoft Docs"
description: "Windows 기반 HDInsight에서 toomigrate tooa Linux 기반 HDInsight 클러스터를 클러스터 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Windows 기반 HDInsight 클러스터 tooa Linux 기반 클러스터에서 마이그레이션하십시오

Windows 및 Linux에서 HDInsight와 방법에 대 한 지침 hello 차이점에 자세히 설명 하는이 문서 toomigrate 기존 작업 tooa Linux 기반 클러스터입니다.

Windows 기반 HDInsight 쉽게 toouse hello 클라우드에서 Hadoop을 제공 하지만 toomigrate tooa Linux 기반 클러스터를 할 수 있습니다. 예를 들어 Linux 기반 도구와 기술 솔루션에 필요한 tootake 활용 합니다. Hello Hadoop 에코 시스템의 다양 한 개체는 Linux 기반 시스템에서 개발 하며 Windows 기반 HDInsight 사용할 수 수 없습니다. 또한 많은 책, 동영상 및 기타 교육 자료에서 Hadoop 작업 시 Linux 시스템을 사용한다고 가정합니다.

> [!NOTE]
> HDInsight 클러스터는 hello 클러스터의 노드 hello에 대 한 hello 운영 체제와 Ubuntu 장기 지원 (LTS)를 사용 합니다. 다른 구성 요소 버전 관리 정보와 함께, HDInsight와 Ubuntu의 hello 버전에 대 한 정보를 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다.

## <a name="migration-tasks"></a>마이그레이션 작업

hello 일반적인 마이그레이션 워크플로 다음과 같습니다.

![마이그레이션 워크플로 다이어그램](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. 기존 워크플로, 작업, 등 tooa Linux 기반 클러스터를 마이그레이션할 때 필요할 수 있는 toounderstand 변경 내용을이 문서의 각 섹션을 읽습니다.

2. 테스트/품질 보증 환경으로 Linux 기반 클러스터를 만듭니다. Linux 기반 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.

3. 기존 작업, 데이터 원본 및 싱크 toohello 새 환경 복사본입니다.

4. Toomake 작업 hello 새 클러스터에서 예상 대로 작동 하는지 테스트 하는 유효성 검사를 수행 합니다.

예상 대로 작동 하는 것을 확인 한 후 hello 마이그레이션에 대 한 가동 중지 시간을 예약 합니다. 이 작동 중단이 시간 동안 hello 다음 작업을 수행 합니다.

1. Hello 클러스터 노드에서 로컬에 저장 된 임시 데이터를 백업 합니다. 예를 들어 헤드 노드에 직접 저장된 데이터가 있는 경우입니다.

2. Hello Windows 기반 클러스터를 삭제 합니다.

3. 동일한 기본 데이터 저장소에 사용 되는 Windows 기반 클러스터 hello hello를 사용 하 여 Linux 기반 클러스터를 만듭니다. hello Linux 기반 클러스터 기존 프로덕션 데이터에 대해 작업을 계속할 수 있습니다.

4. 백업한 모든 임시 데이터를 가져옵니다.

5. 시작 작업/계속 hello 새 클러스터를 사용 하 여 처리 합니다.

### <a name="copy-data-toohello-test-environment"></a>복사본 데이터 toohello 테스트 환경

하지만 많은 방법 toocopy hello 데이터 및 작업, 두 hello이이 섹션에서 설명 hello 가장 간단한 방법 toodirectly 이동 파일 tooa 클러스터 테스트.

#### <a name="hdfs-copy"></a>HDFS 복사

Hello 단계 toocopy 데이터 hello 프로덕션 클러스터 toohello 테스트 클러스터에서 다음을 사용 합니다. 이 단계 사용 hello `hdfs dfs` HDInsight에 포함 된 유틸리티입니다.

1. 기존 클러스터에 대 한 hello 저장소 계정 및 기본 컨테이너 정보를 찾습니다. 다음 예제는 hello PowerShell tooretrieve이이 정보를 사용 합니다.

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. 테스트 환경 toocreate HDInsight 문서에서 만드는 Linux 기반 클러스터 hello hello 단계를 따릅니다. Hello 클러스터를 만들기 전에 중지 하 고 대신 선택 **선택적 구성**합니다.

3. Hello 선택적 구성 블레이드에서 선택 **연결 된 저장소 계정**합니다.

4. 선택 **저장소 키를 추가**, 메시지가 표시 되 면 hello 1 단계에서 PowerShell 스크립트에서 반환 된 hello 저장소 계정을 선택 합니다. 각 블레이드에서 **선택**을 클릭합니다. 마지막으로 hello 클러스터를 만듭니다.

5. Hello 클러스터를 만든 후 다음을 사용 하 여 tooit 연결 **SSH 합니다.** 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

6. Hello SSH 세션에서 연결 된 hello 저장소 계정 toohello 새 기본 저장소 계정에서 다음 명령을 toocopy 파일이 hello를 사용 합니다. 컨테이너 PowerShell에서 반환 된 hello 컨테이너 정보로 대체 합니다. 대체 __계정__ hello 계정 이름입니다. Hello 경로 toodata를 hello 경로 tooa 데이터 파일로 바꿉니다.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Hello 데이터를 포함 하는 hello 디렉터리 구조 hello 테스트 환경에 없는 경우 다음 명령을 hello를 사용 하 여 만들 수 있습니다.

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    hello `-p` 스위치 hello hello 경로에 모든 디렉터리를 만들 수 있음.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Azure Storage Blob 간 직접 복사

또는 toouse hello 경우가 `Start-AzureStorageBlobCopy` HDInsight 외부 저장소 계정 간에 Azure PowerShell cmdlet toocopy blob입니다. 자세한 내용은 참조 hello 어떻게 toomanage의 Azure 저장소와 Azure PowerShell을 사용 하 여 Azure Blob 섹션.

## <a name="client-side-technologies"></a>클라이언트 쪽 기술

와 같은 클라이언트 쪽 기술과 [Azure PowerShell cmdlet](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), 또는 hello [Hadoop에 대 한.NET SDK](https://hadoopsdk.codeplex.com/) toowork Linux 기반 클러스터를 계속 합니다. 이러한 기술을 REST 클러스터 운영 체제 유형에 모두에서 동일 hello는 Api에 의존 합니다.

## <a name="server-side-technologies"></a>서버 쪽 기술

다음 표에서 hello 마이그레이션 서버 쪽 구성 요소에 Windows 관련 지침을 제공 합니다.

| 사용 기술 | 수행 작업 |
| --- | --- |
| **PowerShell** (서버 쪽 스크립트, 클러스터 생성 중 사용한 스크립트 동작 포함) |Bash 스크립트로 다시 작성합니다. 스크립트 동작의 경우 [스크립트 동작에서 Linux 기반 HDInsight 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md) 및 [Linux 기반 HDInsight에 대한 스크립트 동작 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요. |
| **Azure CLI** (서버 쪽 스크립트) |Hello Azure CLI Linux에서 사용할 수 있는 동안 오지 않는 사전 설치 된 hello HDInsight 클러스터 헤드 노드에 있습니다. Hello Azure CLI를 설치 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)합니다. |
| **.NET 구성 요소** |.NET은 Linux 기반 HDInsight 클러스터에서 [Mono](https://mono-project.com)를 통해 완전히 지원되지 않습니다. 자세한 내용은 참조 [마이그레이션할.NET 솔루션 tooLinux 기반 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)합니다. |
| **Win32 구성 요소 또는 기타 Windows 전용 기술** |지침은 hello 구성 요소 또는 기술에 따라 달라 집니다. 수 toofind Linux와 호환 되는 버전 하거나 대체 솔루션 toofind 필요 하거나이 구성 요소를 다시 작성 해야 합니다. |

> [!IMPORTANT]
> hello HDInsight 관리 SDK 모노와 완벽 하 게 호환 되지 않습니다. 솔루션의 일부분 지금은 toohello HDInsight 클러스터를 배포 하지 사용 해야 합니다.

## <a name="cluster-creation"></a>클러스터 만들기

이 섹션에서는 클러스터 만들기의 차이에 대한 정보를 제공합니다.

### <a name="ssh-user"></a>SSH 사용자

Linux 기반 HDInsight 클러스터 hello를 사용 하 여 **SSH (보안 셸)** tooprovide 원격 액세스 toohello 클러스터 노드 프로토콜입니다. Window 기반 클러스터용 원격 데스크톱과 달리, 대부분의 SSH 클라이언트는 그래픽 사용자 경험을 제공하지 않습니다. 대신, SSH 클라이언트 hello 클러스터에서 toorun 명령을 허용 하는 명령줄을 제공 합니다. 일부 클라이언트 (예: [MobaXterm](http://mobaxterm.mobatek.net/)) 더하기 tooa 원격 명령줄에서 그래픽 파일 시스템 브라우저를 제공 합니다.

클러스터를 생성하는 동안 인증을 위해 SSH 사용자와 더불어 **암호** 또는 **공개 키 인증서** 중 하나를 제공해야 합니다.

암호보다는 공개 키 인증서가 더 안전하므로 공개 키 인증서를 사용하는 것이 좋습니다. 인증서 인증 서명 된 공개/개인 키 쌍을 생성 한 다음 hello 클러스터를 만들 때 hello 공개 키를 제공 하 여 작동 합니다. SSH를 사용 하 여 toohello 서버에 연결할 때 클라이언트 hello에 개인 키 hello hello 연결에 대 한 인증을 제공 합니다.

자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

### <a name="cluster-customization"></a>클러스터 사용자 지정

**스크립트 동작** 은 Bash 스크립트에서 작성해야 합니다. 스크립트 동작 실행 되 고 Linux 기반 클러스터를 클러스터 된 후 tooperform 사용 되는 사용자 지정 있을 수도 있습니다에 대 한 클러스터를 만드는 동안 사용할 수 있지만 합니다. 자세한 내용은 [스크립트 동작에서 Linux 기반 HDInsight 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md) 및 [Linux 기반 HDInsight에 대한 스크립트 동작 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.

다른 사용자 지정 기능은 **부트스트랩**입니다. Windows 클러스터의 경우이 기능은 하이브와 함께 사용할 추가 라이브러리의 toospecify hello 위치입니다. 클러스터를 만든 후 이러한 라이브러리는 자동으로 함께 사용할 수 있는 hello 필요 toouse 없이 하이브 쿼리 `ADD JAR`합니다.

Linux 기반 클러스터용 hello 부트스트랩 기능과이 기능을 제공 하지 않습니다. 대신 [클러스터 생성 중 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md)에 설명된 스크립트 동작을 사용합니다.

### <a name="virtual-networks"></a>가상 네트워크

Windows 기반 HDInsight 클러스터는 클래식 가상 네트워크에서만 작동하는 반면 Linux 기반 HDInsight 클러스터는 리소스 관리자 가상 네트워크가 필요합니다. Hello Linux HDInsight 클러스터는 클래식 가상 네트워크에 연결 해야, 참조 리소스가 있는 경우 [클래식 가상 네트워크 tooa 리소스 관리자 가상 네트워크 연결](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)합니다.

HDInsight에서 Azure 가상 네트워크를 사용하기 위한 구성 요구 사항에 대한 자세한 내용은 [가상 네트워크를 사용하여 HDInsight 기능 확장](hdinsight-extend-hadoop-virtual-network.md)을 참조하세요.

## <a name="management-and-monitoring"></a>관리 및 모니터링

Ambari를 통해 사용할 수는 많이 한 hello 웹 Ui 작업 기록 또는 Yarn UI와 같은 Windows 기반 HDInsight에 사용한 경우일 수 있습니다. 또한 hello Ambari 하이브 보기 웹 브라우저를 사용 하 여 하이브 쿼리 방법을 toorun를 제공 합니다. hello Ambari 웹 UI에서 https://CLUSTERNAME.azurehdinsight.net Linux 기반 클러스터에서 제공 됩니다.

Ambari 사용한 작업에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [Ambari 웹](hdinsight-hadoop-manage-ambari.md)
* [Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Ambari 경고

Ambari의 hello 클러스터에 문제가 발생할 가능성을 확인할 수 있는 경고는 시스템을 있습니다. 하지만 경고는 hello REST API를 통해 검색할 수 있습니다 hello Ambari 웹 UI에서에서 빨간색 또는 노란색 항목으로 나타납니다.

> [!IMPORTANT]
> Ambari 경고는 문제가 *있을 수 있다*라는 의미이며, 문제가 *있다*는 것은 아닙니다. 예를 들어 평소처럼 액세스할 수 있는데도 HiveServer2에 액세스할 수 없다는 경고가 나타날 수 있습니다.
>
> 많은 경고는 서비스에서 간격 기반 쿼리로 구현되므로 특정 시간 프레임 내에서 응답을 기대합니다. 따라서 hello 경고 반드시 의미 hello 서비스가 중지 되었습니다, 그리고 just hello 예상 된 시간 안에 결과 반환 하지 않았습니다.

사용자는 조치를 취하기 전에 경고가 오랜 시간 동안 발생했는지 또는 이전에 보고되었던 사용자 문제를 반영하는지 여부를 평가해야 합니다.

## <a name="file-system-locations"></a>파일 시스템 위치

Linux 클러스터 파일 시스템 hello Windows 기반 HDInsight 클러스터와는 다르게 배치 됩니다. 다음 테이블 toofind 일반적으로 사용 되는 파일이 hello를 사용 합니다.

| Toofind... 필요 | 위치 |
| --- | --- |
| 구성 |`/etc`. 예: `/etc/hadoop/conf/core-site.xml` |
| 로그 파일 |`/var/logs` |
| HDP(Hortonworks Data Platform) |`/usr/hdp`. 두 디렉터리 여기에 있는, 하나는 현재 HDP 버전 hello 및 `current`합니다. hello `current` 디렉터리 기호화 된 링크 toofiles 및 hello 버전 번호 디렉터리에 디렉터리를 포함 합니다. hello `current` 디렉터리는 버전은 업데이트 hello 버전 번호 변경 HDP hello 대로 이후 HDP 파일에 액세스 하는 편리한 방법으로 제공 합니다. |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

일반적으로 hello 파일의 hello 이름을 알고 있는 경우에 hello SSH 세션 toofind hello 파일 경로에서 다음 명령을 사용할 수 있습니다.

    find / -name FILENAME 2>/dev/null

또한 hello 파일 이름에 와일드 카드를 사용할 수 있습니다. 예를 들어 `find / -name *streaming*.jar 2>/dev/null` hello 경로 tooany '스트리밍' hello 파일 이름의 일부로 hello 단어를 포함 하는 jar 파일을 반환 합니다.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig 및 MapReduce

Pig 및 MapReduce 워크로드는 Linux 기반 클러스터에서 매우 유사합니다. 하지만 Linux 기반 HDInsight 클러스터는 Hadoop, Hive, Pig의 최신 버전을 사용하여 만들 수 있습니다. 이러한 버전 차이로 인해 기존 솔루션이 작동하는 방식이 달라질 수 있습니다. Hello 버전의 HDInsight에 포함 된 구성 요소에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)합니다.

Linux 기반 HDInsight는 원격 데스크톱 기능을 제공하지 않습니다. 대신, SSH를 사용할 수 있습니다 tooremotely toohello 클러스터 헤드 노드를 연결 합니다. 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [SSH와 함께 Hive 사용](hdinsight-hadoop-use-hive-ssh.md)
* [SSH와 함께 Pig 사용](hdinsight-hadoop-use-pig-ssh.md)
* [SSH와 함께 MapReduce 사용](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> 외부 하이브 metastore를 사용 하는 경우 Linux 기반 HDInsight와 사용 하기 전에 hello metastore를 백업 해야 있습니다. Linux 기반 HDInsight는 최신 버전의 Hive에서 사용할 수 있으며, 이 경우 이전 버전에서 만든 메타스토어와 호환되지 않을 수 있습니다.

다음 차트 hello 하이브 작업 마이그레이션하는 방법에 지침을 제공 합니다.

| Windows 기반 | Linux 기반에서... |
| --- | --- |
| **Hive 편집기** |[Ambari에서 Hive 보기](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez는 Linux 기반 클러스터용 hello 기본 실행 엔진, hello에 실행할 문을 설정 되므로 더 이상 필요 합니다. |
| C# 사용자 정의 함수 | Linux 기반 HDInsight와 C# 구성 요소 유효성 검사에 대 한 자세한 내용은 참조 하세요. [마이그레이션할.NET 솔루션 HDInsight tooLinux 기반](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD 파일 서버에서 나 스크립트 hello 하이브 작업의 일부로 실행 |Bash 스크립트 사용 |
| `hive` 명령 |[SSH 세션에서 Hive](hdinsight-hadoop-use-hive-ssh.md) 또는 [Beeline](hdinsight-hadoop-use-hive-beeline.md) 사용 |

### <a name="pig"></a>Pig

| Windows 기반 | Linux 기반에서... |
| --- | --- |
| C# 사용자 정의 함수 | Linux 기반 HDInsight와 C# 구성 요소 유효성 검사에 대 한 자세한 내용은 참조 하세요. [마이그레이션할.NET 솔루션 HDInsight tooLinux 기반](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD 파일 서버에서 나 스크립트 hello Pig 작업의 일부로 실행 |Bash 스크립트 사용 |

### <a name="mapreduce"></a>MapReduce

| Windows 기반 | Linux 기반에서... |
| --- | --- |
| C# 매퍼 및 리듀서 구성 요소 | Linux 기반 HDInsight와 C# 구성 요소 유효성 검사에 대 한 자세한 내용은 참조 하세요. [마이그레이션할.NET 솔루션 HDInsight tooLinux 기반](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD 파일 서버에서 나 스크립트 hello 하이브 작업의 일부로 실행 |Bash 스크립트 사용 |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> 외부 Oozie metastore를 사용 하는 경우 Linux 기반 HDInsight와 사용 하기 전에 hello metastore를 백업 해야 있습니다. Linux 기반 HDInsight는 최신 버전의 Oozie에서 사용할 수 있으며, 이 경우 이전 버전에서 만든 메타스토어와 호환되지 않을 수 있습니다.

Oozie 워크플로에서는 셸 작업이 가능합니다. 셸 작업 hello 운영 체제 toorun 명령줄 명령에 대 한 hello 기본 셸을 사용합니다. Windows 셸 hello를 사용 하는 Oozie 워크플로 설정한 경우 hello 워크플로 toorely hello Linux 셸 환경 (Bash)에 다시 작성 해야 합니다. Oozie와 함께 셸 작업을 사용하는 방법에 대한 자세한 내용은 [Oozie 셸 작업 확장](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html)을 참조하세요.

셸 작업을 통해 호출된 C# 응용 프로그램에 의존하는 Oozie 워크플로가 있는 경우 Linux 환경에서 이러한 응용 프로그램을 검증해야 합니다. 자세한 내용은 참조 [마이그레이션할.NET 솔루션 tooLinux 기반 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)합니다.

## <a name="storm"></a>Storm

| Windows 기반 | Linux 기반에서... |
| --- | --- |
| Storm 대시보드 |hello 스톰 대시보드를 사용할 수 없는 경우 참조 [Linux 기반 HDInsight의 배포 및 관리 스톰 토폴로지](hdinsight-storm-deploy-monitor-topology-linux.md) 방법 toosubmit 토폴로지에 대 한 |
| Storm UI |hello 스톰 UI https://CLUSTERNAME.azurehdinsight.net/stormui에서 제공 됩니다. |
| Visual Studio toocreate 배포 하 고 C# 또는 하이브리드 토폴로지를 관리 합니다. |Visual Studio 사용한 toocreate 수 하 고 배포 하 고 C# (SCP.NET) 또는 2016 년 10 월 28 일 이후에 작성 하는 HDInsight 클러스터에서 Linux 기반 스톰에 하이브리드 토폴로지를 관리할 수 있습니다. |

## <a name="hbase"></a>HBase

Linux 기반 클러스터에서 HBase에 대 한 hello znode 부모는 `/hbase-unsecure`합니다. 네이티브 HBase Java API를 사용 하는 모든 Java 클라이언트 응용 프로그램에 대 한 hello 구성에서이 값을 설정 합니다.

이 값을 설정하는 예제 클라이언트에 대한 내용은 [Java 기반 HBase 응용 프로그램 빌드](hdinsight-hbase-build-java-maven.md) 를 참조하세요.

## <a name="spark"></a>Spark

Spark 클러스터는 미리 보기 중 Windows 클러스터에서 사용 가능했지만 Spark GA은 Linux 기반 클러스터에서만 사용 가능합니다. Windows 기반 Spark 클러스터 tooa 미리 보기 릴리스 Linux 기반 Spark 클러스터에서 마이그레이션 경로가 없습니다.

## <a name="known-issues"></a>알려진 문제

### <a name="azure-data-factory-custom-net-activities"></a>Azure Data Factory 사용자 지정 .NET 작업

Azure Data Factory 사용자 지정 .NET 작업은 현재 Linux 기반 HDInsight 클러스터에서 지원되지 않습니다. 대신, hello ADF 파이프라인의 일부로 메서드 tooimplement 사용자 지정 활동을 다음 중 하나를 사용 해야 합니다.

* Azure 배치 풀에서 .NET 작업을 실행합니다. hello 사용 하 여 Azure 배치 연결 된 서비스 섹션을 참조 [Azure 데이터 팩터리 파이프라인에서 사용자 지정 활동 사용](../data-factory/data-factory-use-custom-activities.md)
* MapReduce 작업으로 hello 활동을 구현 합니다. 자세한 내용은 [데이터 팩터리에서 MapReduce 프로그램 호출](../data-factory/data-factory-map-reduce.md)을 참조하세요.

### <a name="line-endings"></a>줄 끝

일반적으로 Windows 기반 시스템에서는 줄 끝으로 CRLF를 사용하며, Linux 기반 시스템에서는 LF를 사용합니다. 생성 또는 CRLF 줄 끝을 사용 하 여 데이터에 예상 되는 경우 toomodify hello 생산자 또는 소비자 toowork hello LF 줄 끝으로 할 수 있습니다.

Windows 기반 클러스터에서 HDInsight CRLF 사용 하 여 데이터를 반환 하는 예를 들어 tooquery Azure PowerShell을 사용 하 여 합니다. hello Linux 기반으로 하는 클러스터로 동일한 쿼리에 반환 LF 합니다. Hello 줄 끝 마이그레이션을 수행 하기 전에 프로그램 solutuion에 문제가 발생 하는 경우에 toosee를 테스트 해야 tooa Linux 기반 클러스터입니다.

Hello Linux 클러스터 노드에서 직접 실행 되는 스크립트를 사용 하도록 설정한 경우에 hello 줄 끝으로 항상 LF를 사용 해야 합니다. CRLF를 사용 하는 경우 Linux 기반 클러스터에서 hello 스크립트를 실행할 때 오류가 표시 될 수 있습니다.

Hello 스크립트가 포함 된 CR 문자를 사용 하 여 문자열에 포함 되지 않도록를 알고 있으면 변경 hello 줄 끝 hello 메서드를 다음 중 하나를 사용 하 여 대량 수 있습니다.

* **Toohello 클러스터를 업로드 하기 전에**: hello 스크립트 toohello 클러스터를 업로드 하기 전에 PowerShell 문을 toochange hello 줄 끝 CRLF tooLF에서 다음 사용 하 여 hello 합니다.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Toohello 클러스터 업로드 한 후**: SSH 세션 toohello Linux 기반 클러스터 toomodify hello 스크립트에서에서 사용 하 여 hello 다음 명령은 합니다.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>다음 단계

* [어떻게 toocreate Linux 기반 HDInsight 클러스터에 대해 알아봅니다](hdinsight-hadoop-provision-linux-clusters.md)
* [SSH tooconnect tooHDInsight를 사용 하 여](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Ambari를 사용하여 Linux 기반 클러스터 관리](hdinsight-hadoop-manage-ambari.md)
