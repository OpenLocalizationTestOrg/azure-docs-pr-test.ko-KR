---
title: "Linux 기반 HDInsight-Azure와 aaaScript 액션 개발 | Microsoft Docs"
description: "Toouse Bash toocustomize Linux 기반 HDInsight 클러스터를 스크립트 하는 방법에 대해 알아봅니다. hello 스크립트 동작 hdinsight 기능은 toorun 스크립트 중 또는 클러스터를 만든 후입니다. 스크립트 추가 소프트웨어를 설치 또는 클러스터 구성 설정을 사용 하는 toochange를 수 있습니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>HDInsight를 사용하여 스크립트 작업 개발

자세한 내용은 toocustomize를 이용한 적 사용 하 여 HDInsight 클러스터 어떻게 스크립트입니다. 스크립트 작업 중 이나 후 클러스터를 만드는 방법을 toocustomize HDInsight은입니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

## <a name="what-are-script-actions"></a>스크립트 작업 정의

스크립트 작업은 Azure hello 클러스터 노드 toomake 구성 변경에서 실행 되는 Bash 스크립트 하거나 소프트웨어를 설치 합니다. 스크립트 작업을 루트로, 실행 되 고 권한 toohello 클러스터 노드 전체 액세스를 제공 합니다.

스크립트 동작 메서드를 다음 hello를 통해 적용할 수 있습니다.

| 이 메서드 tooapply 스크립트를 사용 함 | 클러스터를 생성하는 동안... | 실행 중인 클러스터에서... |
| --- |:---:|:---:|
| Azure 포털 |✓ |✓ |
| Azure PowerShell |✓ |✓ |
| Azure CLI |&nbsp; |✓ |
| HDInsight .NET SDK |✓ |✓ |
| Azure Resource Manager 템플릿 |✓ |&nbsp; |

이러한 메서드 tooapply 스크립트 동작을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md)합니다.

## <a name="bestPracticeScripting"></a>스크립트 개발을 위한 모범 사례

HDInsight 클러스터에 대 한 사용자 지정 스크립트를 개발할 때 염두에 몇 가지 모범 사례 tookeep 가지 있습니다.

* [Hello Hadoop 버전 대상](#bPS1)
* [대상 hello OS 버전](#bps10)
* [안정적인 tooscript 리소스 링크를 제공 합니다.](#bPS2)
* [사전 컴파일한 리소스 사용](#bPS4)
* [Hello 클러스터 사용자 지정 스크립트가 idempotent 인지 확인](#bPS3)
* [Hello 클러스터 아키텍처의 고가용성을 보장](#bPS5)
* [Hello 사용자 지정 구성 요소 toouse Azure Blob 저장소 구성](#bPS6)
* [쓰기 정보 tooSTDOUT 및 STDERR](#bPS7)
* [줄 끝을 LF인 파일을 ASCII로 저장](#bps8)
* [일시적인 오류 다시 시도 논리 toorecover를 사용 하 여](#bps9)

> [!IMPORTANT]
> 스크립트 동작 60 분 내에 완료 되어야 하거나 hello 프로세스가 실패 합니다. 노드 프로 비전 시 hello 스크립트는 다른 설치 및 구성 프로세스와 동시에 실행 됩니다. CPU 시간 또는 네트워크 대역폭 등의 리소스에 대 한 경합은 hello 스크립트 tootake 긴 toofinish 개발 환경에서 사용 하지 않고 발생할 수 있습니다.

### <a name="bPS1"></a>Hello Hadoop 버전 대상

HDInsight의 서로 다른 버전에는 설치된 Hadoop 서비스 및 구성 요소의 서로 다른 버전이 있습니다. 스크립트는 특정 버전의 서비스 또는 구성 요소에는 하는 경우에 hello 필수 구성 요소를 포함 하는 HDInsight의 hello 버전과 hello 스크립트를 사용 해야 합니다. 자세한 내용은 HDInsight에 포함 된 구성 요소 버전에 hello를 사용 하 여 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md) 문서.

### <a name="bps10"></a>대상 hello OS 버전

Linux 기반 HDInsight hello Ubuntu Linux 배포판을 기반으로 합니다. HDInsight는 버전이 다르면 다른 버전의 Ubuntu에 의존하는데 이는 스크립트 동작 방식을 변경할 수 있습니다. 예를 들어 HDInsight 3.4 이전 버전은 Upstart를 사용하는 Ubuntu 버전을 기반으로 합니다. 버전 3.5는 Systemd를 사용하는 Ubuntu 16.04를 기반으로 합니다. 스크립트 둘 다와 함께 toowork 작성 해야 하므로 다양 한 명령이 Systemd와 Upstart 사용 합니다.

HDInsight 3.4 및 3.5 간의 또 다른 중요 한 차이점은 `JAVA_HOME` tooJava 8 가리키게 합니다.

사용 하 여 hello OS 버전을 확인 하면 `lsb_release`합니다. hello 다음 코드에서는 방법을 toodetermine 경우 hello 스크립트 Ubuntu 14 또는 16에서 실행 되 고 있습니다.

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

이러한 조각은 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh에 포함 된 hello 전체 스크립트를 찾을 수 있습니다.

HDInsight에서 사용 되는 Ubuntu hello 버전에서는 참조 hello [HDInsight 구성 요소 버전](hdinsight-component-versioning.md) 문서.

toounderstand hello와의 차이점 Systemd Upstart, 참조 [Upstart 사용자에 대 한 Systemd](https://wiki.ubuntu.com/SystemdForUpstartUsers)합니다.

### <a name="bPS2"></a>안정적인 tooscript 리소스 링크를 제공 합니다.

hello 스크립트와 관련 된 리소스가 유지 되어야 hello 수명의 hello 클러스터 전체에서 사용 가능 합니다. 이러한 리소스를 새 노드를 작업 크기 조정 하는 동안 toohello 클러스터를 추가 합니다.

hello 가장 좋은 방법은 toodownload 이며 구독에는 Azure 저장소 계정에 모든 항목을 보관 합니다.

> [!IMPORTANT]
> 사용 된 hello 저장소 계정에는 다른 저장소 계정에 hello 클러스터 또는 공용, 읽기 전용 컨테이너에 대 한 되는 hello 기본 저장소 계정 이어야 합니다.

Microsoft에서 제공 하는 hello 예제 hello에 저장 됩니다는 예를 들어 [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) 저장소 계정입니다. 이 hello HDInsight 팀에서 유지 관리 하는 공용, 읽기 전용 컨테이너입니다.

### <a name="bPS4"></a>사전 컴파일한 리소스 사용

tooreduce hello 하나 toorun hello 스크립트 시간, 소스 코드에서 리소스를 컴파일 하는 작업을 방지 합니다. 예를 들어 리소스 선컴파일하도록 하 고 hello에 Azure 저장소 계정 blob 보관해 HDInsight와 동일한 데이터 센터입니다.

### <a name="bPS3"></a>Hello 클러스터 사용자 지정 스크립트가 idempotent 인지 확인

스크립트는 idempotent여야 합니다. 반환 해야 하는 경우 hello 스크립트가 여러 번 실행 되 면 hello 클러스터 toohello 될 때마다 동일한 상태입니다.

예를 들어 구성 파일을 수정하는 스크립트는 여러 번 실행하는 경우 중복 항목을 추가해서는 안됩니다.

### <a name="bPS5"></a>Hello 클러스터 아키텍처의 고가용성을 보장

Linux 기반 HDInsight 클러스터 hello 클러스터 내에서 활성화 되어 있는 두 개의 헤드 노드를 제공 하 고 두 노드 모두에서 스크립트 동작 실행. 설치 하는 hello 구성 요소에 예상 되는 헤드 노드를 하나만 있으면 두 헤드 노드에서 hello 구성 요소를 설치 하지 마십시오.

> [!IMPORTANT]
> 서비스 HDInsight의 일부로 제공 되는 디자인 된 toofail 통해 hello 두 헤드 노드 사이의 필요에 따라 합니다. 이 기능은 toocustom 구성 요소가 스크립트 동작을 통해 설치 된 연장 되지 않습니다. 사용자 지정 구성 요소에 대한 고가용성이 필요한 경우 사용자 고유의 장애 조치 메커니즘을 구현해야 합니다.

### <a name="bPS6"></a>Hello 사용자 지정 구성 요소 toouse Azure Blob 저장소 구성

Hello 클러스터에 설치 하는 구성 요소는 Hadoop 분산 파일 시스템 (HDFS) 저장소를 사용 하는 기본 구성을 할 수 있습니다. HDInsight은 hello 기본 저장소로 Azure 저장소 서비스 또는 데이터 레이크 저장소 중 하나를 사용합니다. 둘 다 hello 클러스터를 삭제할 경우에 데이터를 유지 하는 HDFS 호환 되는 파일 시스템을 제공 합니다. WASB 또는 HDFS 대신 ADL toouse 설치 tooconfigure 구성 요소를 할 수 있습니다.

대부분의 작업에 대 한 toospecify hello 파일 시스템이 필요 하지 않습니다. 예를 들어 hello 다음 hello 로컬 파일 시스템 toocluster 저장소에서 hello giraph examples.jar 파일을 복사합니다.

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

이 예제에서는 hello `hdfs` 명령은 hello 기본 저장소 클러스터에 투명 하 게 사용 하 여 합니다. 일부 작업에 대 한 toospecify hello URI를 할 수 있습니다. 예를 들어 Data Lake Store에 대해 `adl:///example/jars`를 또는 Azure Storage에 대해 `wasb:///example/jars`를 지정합니다.

### <a name="bPS7"></a>쓰기 정보 tooSTDOUT 및 STDERR

HDInsight은 스크립트 출력을 쓸된 tooSTDOUT 및 STDERR를 로그 합니다. Hello Ambari web UI를 사용 하 여이 정보를 볼 수 있습니다.

> [!NOTE]
> Ambari은 hello 클러스터를 성공적으로 만들 경우 사용할 수만 있습니다. 클러스터 만들기 및 만들기 실패 하는 동안 스크립트 작업을 사용 하는 경우 참조 문제 해결 섹션 hello [HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) 로깅되는 정보에 액세스 하는 다른 방법에 대 한 합니다.

유틸리티 및 설치 패키지를 대부분 이미 쓸 정보 tooSTDOUT 및 STDERR를 되었지만 tooadd 추가 로깅을 지정할 수 있습니다. toosend 텍스트 tooSTDOUT 사용 `echo`합니다. 예:

```bash
echo "Getting ready tooinstall Foo"
```

기본적으로 `echo` 보냅니다 hello 문자열 tooSTDOUT 합니다. toodirect 것 tooSTDERR, 추가 `>&2` 전에 `echo`합니다. 예:

```bash
>&2 echo "An error occurred installing Foo"
```

이 tooSTDOUT tooSTDERR (2)를 대신 기록 된 정보를 리디렉션합니다. IO 리디렉션에 대한 자세한 내용은 [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html)를 참조하세요.

스크립트 동작에서 기록된 정보 보기에 대한 자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a> 줄 끝을 LF인 파일을 ASCII로 저장

Bash 스크립트는 LF에서 종료한 줄을 사용하여 ASCII 형식으로 저장되어야 합니다. 파일 또는 u t F-8로 저장 된 CRLF hello 줄 끝으로 사용한 다음 오류가 hello로 실패할 수 있습니다.

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>일시적인 오류 다시 시도 논리 toorecover를 사용 하 여

파일을 다운로드할 때 인터넷 hello apt get 또는 통해 데이터를 전송 하는 다른 작업을 사용 하 여 패키지를 설치, hello 동작 tootransient 네트워킹 오류로 인해 실패할 수 있습니다. 예를 들어 hello 원격 리소스와 통신 하는 tooa 백업 노드를 통해 실패의 hello 프로세스 수 있습니다.

toomake 스크립트 탄력적인 tootransient 오류를 재시도 논리를 구현할 수 있습니다. hello 함수 다음 tooimplement 다시 시도 하는 논리를 보여 줍니다. 세 번 실패 하기 전에 hello 작업을 다시 시도 합니다.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

hello 다음 예제에 나와 방법을 toouse이이 함수입니다.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>사용자 지정 스크립트에 대한 도우미 메서드

스크립트 작업 도우미 메서드는 사용자 지정 스크립트를 쓰는 동안 사용할 수 있는 유틸리티입니다. 이러한 메서드는 [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) 스크립트에 포함되어 있습니다. Hello toodownload를 수행 하 고 스크립트의 일부로 사용:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

다음 스크립트에 사용할 수 있는 도우미 hello:

| 도우미 사용 | 설명 |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Hello 소스 URI toohello 지정 된 파일 경로에서 파일을 다운로드 합니다. 기본적으로 기존 파일을 덮어쓰지 않습니다. |
| `untar_file TARFILE DESTDIR` |Tar 파일 추출 (사용 하 여 `-xf`) toohello 대상 디렉터리입니다. |
| `test_is_headnode` |클러스터 헤드 노드에서 실행한 경우 1을 반환하고 그렇지 않으면 0을 반환합니다. |
| `test_is_datanode` |Hello 현재 노드 (작업자) 데이터 노드인 경우 1; 반환 그렇지 않으면 0입니다. |
| `test_is_first_datanode` |노드 (명명 된 workernode0) 1; 반환 hello 현재 노드가 hello 첫 번째 데이터 (작업자) 이면 그렇지 않으면 0입니다. |
| `get_headnodes` |Hello 클러스터의 hello headnodes의 hello 정규화 된 도메인 이름을 반환 합니다. 이름은 쉼표로 구분됩니다. 빈 문자열이 오류에 반환됩니다. |
| `get_primary_headnode` |기본 헤드 노드에 hello의 hello 정규화 된 도메인 이름을 가져옵니다. 빈 문자열이 오류에 반환됩니다. |
| `get_secondary_headnode` |Hello 보조 헤드 노드에의 hello 정규화 된 도메인 이름을 가져옵니다. 빈 문자열이 오류에 반환됩니다. |
| `get_primary_headnode_number` |기본 헤드 노드에 hello의 hello 숫자 접미사를 가져옵니다. 빈 문자열이 오류에 반환됩니다. |
| `get_secondary_headnode_number` |Hello 보조 헤드 노드에의 hello 숫자 접미사를 가져옵니다. 빈 문자열이 오류에 반환됩니다. |

## <a name="commonusage"></a>일반적인 사용 패턴

이 섹션에서 사용자 고유의 사용자 지정 스크립트를 작성 하는 동안에 실행 될 수 있는 hello 일반적인 사용 패턴을 구현 지침을 제공 합니다.

### <a name="passing-parameters-tooa-script"></a>Tooa 스크립트 매개 변수 전달

경우에 따라 스크립트에 매개 변수가 필요할 수 있습니다. 예를 들어 hello Ambari REST API를 사용 하는 경우 hello 클러스터에 대 한 hello 관리자 암호를 할 수 있습니다.

Toohello 스크립트에 전달 된 매개 변수 라고 *위치 매개 변수*, 너무 할당 된`$1` hello 첫 번째 매개 변수에 대 한 `$2` 두 번째 및 하므로 on hello에 대 한 합니다. `$0`hello 스크립트 자체의 hello 이름을 포함합니다.

Toohello 스크립트 매개 변수로 전달 된 값을 작은따옴표 (')으로 묶어야 합니다. 이렇게 하면 값이 전달 되는 hello 리터럴로 처리 됩니다.

### <a name="setting-environment-variables"></a>환경 변수 설정

환경 변수를 설정 hello 문 다음에 의해 수행 됩니다.

    VARIABLENAME=value

여기서 VARIABLENAME는 hello hello 변수 이름입니다. tooaccess hello 변수를 사용 하 여 `$VARIABLENAME`합니다. 예를 들어 tooassign 라는 암호 환경 변수로 위치 매개 변수에서 제공 하는 값, 문 다음 hello를 사용 합니다.

    PASSWORD=$1

후속 액세스 toohello 정보를 유도할 수 `$PASSWORD`합니다.

Hello 스크립트 내에서 설정한 환경 변수가 hello 스크립트의 hello 범위 내 에서만 존재 합니다. 경우에 따라 hello 스크립트가 완료 된 후 지속 되는 tooadd 시스템 수준 환경 변수를 할 수 있습니다. tooadd 시스템 수준 환경 변수는 hello 변수를 너무 추가`/etc/environment`합니다. Hello 문 다음의 추가 예를 들어 `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Hello 사용자 지정 스크립트를 저장할 toolocations 액세스

사용 되는 스크립트 toocustomize 클러스터 toobe hello 다음 위치 중 하나에 저장 해야 합니다.

* __Azure 저장소 계정__ hello 클러스터와 연결 된 합니다.

* __추가 저장소 계정__ hello 클러스터와 연결 된 합니다.

* __공개적으로 읽을 수 있는 URI__ 예를 들어 한 URL toodata OneDrive, Dropbox, 또는 서비스를 호스트 하는 다른 파일에 저장 합니다.

* __Azure 데이터 레이크 저장소 계정__ hello HDInsight 클러스터와 연결 된 합니다. HDInsight와 함께 Azure Data Lake Store를 사용하는 방법에 대한 자세한 내용은 [Data Lake Store를 사용하여 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요.

    > [!NOTE]
    > hello 서비스 보안 주체 HDInsight 사용 하 여 tooaccess Data Lake 저장소에 대 한 읽기 액세스 toohello 스크립트가 있어야 합니다.

또한 hello 스크립트에 의해 사용 되는 리소스 공개적으로 사용할 수 있어야 합니다.

Hello Azure 네트워크 내에서 둘 다로 신속 하 게 액세스할을 제공 hello 파일을 Azure 저장소 계정 또는 Azure 데이터 레이크 저장소에 저장 합니다.

> [!NOTE]
> hello URI 사용 하는 형식 tooreference hello 스크립트 사용 중인 hello 서비스에 따라 달라 집니다. Hello HDInsight 클러스터와 연결 된 저장소 계정에 대해 사용 하 여 `wasb://` 또는 `wasbs://`합니다. 공개적으로 읽을 수 있는 URI의 경우 `http://` 또는 `https://`를 사용합니다. Data Lake Store의 경우 `adl://`을 사용합니다.

### <a name="checking-hello-operating-system-version"></a>Hello 운영 체제 버전 확인

HDInsight의 다른 버전들은 Ubuntu의 특정 버전에 의존합니다. 스크립트에서 확인해야 하는 OS 버전 간의 차이가 있을 수 있습니다. 예를 들어 tooinstall Ubuntu의 제한은 toohello 버전이 있는 이진 파일을 할 수 있습니다.

toocheck hello OS 버전을 사용 하 여 `lsb_release`합니다. 예를 들어 다음 스크립트는 hello hello OS 버전에 따라 tooreference 특정 tar 파일 하는 방법을 보여 줍니다.

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>스크립트 작업 배포를 위한 검사 목록

이러한 스크립트 toodeploy를 준비할 때 했습니다 hello 단계는 다음과 같습니다.

* Hello 배포 하는 동안 hello 클러스터 노드에서 액세스할 수 있는 위치에서 사용자 지정 스크립트를 포함 하는 hello 파일을 넣습니다. 예를 들어 hello hello 클러스터에 대 한 기본 저장소입니다. 공개적으로 읽을 수 있는 호스팅 서비스에 파일을 저장할 수도 있습니다.
* Hello 스크립트 강력한 인지 확인 합니다. 이 통해 hello 스크립트 toobe 여러 번 실행 hello에 동일한 노드.
* 임시 파일 디렉터리 /tmp tookeep hello 사용 하 여 hello 스크립트에 의해 사용 되는 파일을 다운로드 하 여 다음 스크립트를 실행 한 후를 정리 합니다.
* 운영 체제 수준을 설정 또는 Hadoop 서비스 구성 파일 변경 되 면 toorestart HDInsight 서비스 수도 있습니다.

## <a name="runScriptAction"></a>어떻게 toorun 스크립트 동작

메서드를 다음 hello를 사용 하 여 스크립트 작업 toocustomize HDInsight 클러스터를 사용할 수 있습니다.

* Azure portal
* Azure PowerShell
* Azure 리소스 관리자 템플릿
* hello HDInsight.NET SDK입니다.

각 메서드를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [toouse 작업을 스크립팅 하는 방법을](hdinsight-hadoop-customize-cluster-linux.md)합니다.

## <a name="sampleScripts"></a>사용자 지정 스크립트 샘플

Microsoft은 HDInsight 클러스터에서 예제 스크립트 tooinstall 구성 요소를 제공 합니다. 자세한 예제 스크립트 동작에 대 한 링크를 따라 hello를 참조 하십시오.

* [HDInsight에서 Hue 설치 및 사용](hdinsight-hadoop-hue-linux.md)
* [HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install-linux.md)
* [HDInsight 클러스터에 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install-linux.md)
* [HDInsight 클러스터에 Mono 설치 또는 업그레이드](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>문제 해결

hello 다음은 오류가 개발한 스크립트를 사용 하는 경우 발생할 수 있습니다.

**오류**: `$'\r': command not found`. 때로는 `syntax error: unexpected end of file`이 이어집니다.

*원인*: 스크립트에서 줄 hello CRLF 끝나야 하는 경우이 오류는 발생 합니다. Unix 시스템 hello 줄 끝 LF만 필요로 합니다.

이 문제가 가장 자주 발생 hello 스크립트는 Windows 환경에 대해 작성 되어 CRLF은 Windows에서 많은 텍스트 편집기를 종료 하는 일반적인 선으로 합니다.

*해결 방법*: 텍스트 편집기에서 옵션이 면 hello 줄 끝에 대 한 Unix 형식 또는 LF 선택 합니다. Hello 나오는 Unix 시스템 toochange hello CRLF tooan LF에 명령을 사용할 수도 있습니다.

> [!NOTE]
> hello 다음 명령은 동일 대략 hello CRLF 줄 끝 tooLF를 변경 해야 합니다. 시스템에서 사용할 수 있는 hello 유틸리티에 따라 하나를 선택 합니다.

| 명령 | 참고 사항 |
| --- | --- |
| `unix2dos -b INFILE` |원본 파일 hello와 함께 백업 됩니다는 합니다. BAK 확장 |
| `tr -d '\r' < INFILE > OUTFILE` |OUTFILE은 끝이 LF인 버전만 포함합니다. |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Hello 파일을 직접 수정 |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |OUTFILE은 끝이 LF인 버전만 포함합니다. |

**오류**: `line 1: #!/usr/bin/env: No such file or directory`.

*원인*: 경우이 오류가 발생 hello 스크립트는 바이트 순서 표시가 (BOM) u t F-8로 저장 되었다는 합니다.

*해결 방법*: hello 파일 ASCII로 또는 BOM 없이 u t F-8로 저장 합니다. Hello hello BOM 없이 파일은 Linux 또는 Unix 시스템 toocreate에서 다음 명령을 사용할 수도 있습니다.

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

대체 `INFILE` hello 파일에 BOM hello 포함 합니다. `OUTFILE`hello BOM 없이 hello 스크립트가 들어 있는 새 파일 이름 이어야 합니다.

## <a name="seeAlso"></a>다음 단계

* 너무 방법에 대해 알아봅니다[HDInsight 사용자 지정 스크립트 동작을 사용 하는 클러스터](hdinsight-hadoop-customize-cluster-linux.md)
* 사용 하 여 hello [HDInsight.NET SDK 참조](https://msdn.microsoft.com/library/mt271028.aspx) toolearn HDInsight를 관리 하는.NET 응용 프로그램을 만드는 방법에 대 한 자세한
* 사용 하 여 hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn toouse REST tooperform 관리 작업에서 HDInsight 클러스터 방법입니다.
