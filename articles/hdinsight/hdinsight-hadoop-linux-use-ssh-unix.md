---
title: "Azure HDInsight에서 Hadoop으로 SSH aaaUse | Microsoft Docs"
description: "SSH(보안 셸)를 사용하여 HDInsight에 액세스할 수 있습니다. 이 문서에서는 Windows, Linux, Unix, 또는 macOS 클라이언트에서 사용 하 여 hello ssh tooHDInsight scp 명령과 연결 설명 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "Linux의 Hadoop 명령, Hadoop Linux 명령, Hadoop macOS, SSH Hadoop, SSH Hadoop 클러스터"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>TooHDInsight (Hadoop) SSH를 사용 하 여 연결

자세한 내용은 방법 toouse [SSH (보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely tooHadoop Azure HDInsight에 연결 합니다. 

HDInsight은 hello Hadoop 클러스터 내에서 노드에 대 한 hello 운영 체제로 Linux (Ubuntu)를 사용할 수 있습니다. hello 다음 표에서 tooLinux 기반 HDInsight SSH 클라이언트를 사용 하 여 연결할 때 필요한 hello 주소와 포트 정보.

| 주소 | 포트 | 다음에 연결... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | 에지 노드(HDInsight의 R Server) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | 에지 노드(에지 노드가 있는 경우 다른 클러스터 형식) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | 기본 헤드 노드 |
| `<clustername>-ssh.azurehdinsight.net` | 23 | 보조 헤드 노드 |

> [!NOTE]
> 대체 `<edgenodename>` hello hello 가장자리 노드 이름을 사용 합니다.
>
> 대체 `<clustername>` 클러스터의 hello 이름을 사용 합니다.
>
> 좋습니다 가장자리 노드 클러스터에 있으면, 있습니다 __toohello 가장자리 노드는 항상 연결__ SSH를 사용 하 여 합니다. hello 헤드 노드는 Hadoop의 중요 한 toohello 상태 있는 서비스를 호스트 합니다. hello 가장자리 노드에 보관할 내용은 실행 됩니다.
>
> 에지 노드를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 에지 노드 사용](hdinsight-apps-use-edge-node.md#access-an-edge-node)을 참조하세요.

## <a name="ssh-clients"></a>SSH 클라이언트

Linux, Unix 및 macOS 시스템 제공 hello `ssh` 및 `scp` 명령입니다. hello `ssh` 클라이언트는 자주 사용 되는 toocreate 원격 명령줄 세션 Linux 또는 Unix 기반 시스템입니다. hello `scp` 클라이언트는 클라이언트와 hello 원격 시스템 간에 사용 되는 toosecurely 복사본 파일입니다.

Microsoft Windows는 기본적으로 SSH 클라이언트를 제공하지 않습니다. hello `ssh` 및 `scp` 클라이언트는 패키지를 다음 hello를 통해 Windows에 사용할 수 있습니다.

* [Azure 클라우드 셸](../cloud-shell/quickstart.md): 브라우저에서 Bash 환경을 제공 하 고 hello를 제공 하는 hello 클라우드 셸 `ssh`, `scp`, 및 기타 공통 Linux 명령입니다.

* [Windows 10에서 Ubuntu를 이용한 적](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` 및 `scp` Windows 명령줄에서 Bash hello를 통해 사용할 수 있습니다.

* [Git (https://git-scm.com/)](https://git-scm.com/): hello `ssh` 및 `scp` hello GitBash 명령줄을 통해 사용할 수 있습니다.

* [GitHub 데스크톱 (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` 및 `scp` hello GitHub 셸의 명령줄을 통해 사용할 수 있습니다. GitHub 데스크톱 Git 셸 hello에 대 한 hello 명령줄으로 구성 된 toouse Bash, hello Windows 명령 프롬프트에서 또는 PowerShell을 수 있습니다.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell 팀 OpenSSH tooWindows 이식 되 고 테스트 릴리스에서 제공 합니다.

    > [!WARNING]
    > hello SSH 서버 구성 요소를 포함 하는 hello OpenSSH 패키지 `sshd`합니다. 이 구성 요소는 다른 사람들이 시스템에 SSH 서버를 시작 tooconnect tooit 합니다. 시스템에서 toohost SSH 서버를 원하는 경우 포트 22를 열지 하거나이 구성 요소를 구성 하지 마십시오. HDInsight와 필요한 toocommunicate 아닙니다.

[PuTTY(http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) 및 [MobaXterm(http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/)과 같은 몇 가지 그래픽 SSH 클라이언트가 있습니다. 이러한 클라이언트에 사용 되는 tooconnect tooHDInsight 수 있지만, 연결 하는 hello 프로세스 hello를 사용 하 여 보다 차이가 `ssh` 유틸리티입니다. 자세한 내용은 사용 중인 hello 그래픽 클라이언트 hello 설명서를 참조 하십시오.

## <a id="sshkey"></a>인증: SSH 키

SSH 키는 사용 하 여 [공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH 세션입니다. SSH 키 암호 보다 더 안전 하 고 쉽게 toosecure 액세스 tooyour Hadoop 클러스터를 제공 합니다.

SSH 계정 키를 사용 하 여 보호를 연결 하는 경우 개인 키와 일치 하는 hello hello 클라이언트에 제공 해야 합니다.

* 대부분의 클라이언트 구성된 toouse 수는 __기본 키__합니다. 예를 들어 hello `ssh` 에 개인 키에 대 한 클라이언트 찾습니다 `~/.ssh/id_rsa` 에서 Linux 및 Unix 환경에 있습니다.

* Hello를 지정할 수 있습니다 __경로 tooa 개인 키__합니다. Hello로 `ssh` client, 안녕하세요 `-i` 매개 변수는 사용 되는 toospecify hello 경로 tooprivate 키입니다. 예: `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* 서로 다른 서버에서 사용할 수 있는 __여러 개의 개인 키__가 있는 경우 [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent)와 같은 유틸리티를 사용하는 것이 좋습니다. hello `ssh-agent` 유틸리티 대 한 SSH 세션을 설정할 때 사용 되는 tooautomatically 선택 hello 키 toouse 될 수 있습니다.

> [!IMPORTANT]
>
> 암호와 개인 키를 보호 하는 경우에 hello 키를 사용할 때 hello 암호를 입력 해야 합니다. 와 같은 유틸리티 `ssh-agent` 편의 위해 hello 암호를 캐시할 수 있습니다.

### <a name="create-an-ssh-key-pair"></a>SSH 키 쌍 만들기

사용 하 여 hello `ssh-keygen` 명령 toocreate 공용 및 개인 키 파일입니다. hello 다음 명령은 생성 HDInsight와 사용할 수 있는 2048 비트 RSA 키 쌍:

    ssh-keygen -t rsa -b 2048

Hello 키 생성 프로세스 중에 정보를 묻는 메시지가 나타납니다. 예를 들어 hello 키 저장 되는 위치 또는 여부 toouse 암호입니다. Hello 프로세스를 완료 한 후에 두 개의 파일이 만들어집니다. 공개 키와 개인 키를 제공 합니다.

* hello __공개 키__ toocreate 사용 되는 HDInsight 클러스터 됩니다. hello 공개 키의 확장명은 `.pub`합니다.

* hello __개인 키__ 클라이언트 toohello HDInsight 클러스터에 사용 되는 tooauthenticate 됩니다.

> [!IMPORTANT]
> 암호를 사용하여 키를 보호할 수 있습니다. 암호는 사실상 개인 키의 암호입니다. 다른 사람이 사용자의 개인 키가를 입수 하는 경우에 hello 암호 toouse hello 키를 가져야 합니다.

### <a name="create-hdinsight-using-hello-public-key"></a>HDInsight hello 공개 키를 사용 하 여 만들기

| 생성 방법 | 어떻게 toouse hello 공개 키 |
| ------- | ------- |
| **Azure 포털** | 선택을 취소 __동일한 암호를 사용 하 여 클러스터 로그인으로__를 선택한 후 __공개 키__ hello SSH 인증 유형으로 합니다. 마지막으로, hello 공개 키 파일 선택 하거나 hello에 hello 파일의 hello 텍스트 내용을 붙여 __SSH 공개 키__ 필드입니다.</br>![HDInsight 클러스터 생성의 SSH 공개 키 대화 상자](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | 사용 하 여 hello `-SshPublicKey` hello의 매개 변수 `New-AzureRmHdinsightCluster` hello 공개 키를 문자열로 hello 내용을 cmdlet 및 통과 합니다.|
| **Azure CLI 1.0** | 사용 하 여 hello `--sshPublicKey` hello의 매개 변수 `azure hdinsight cluster create` 명령 및 hello 공개 키의 hello 내용을 문자열로 전달 합니다. |
| **Resource Manager 템플릿** | 템플릿에서 SSH 키를 사용하는 예제는 [SSH 키를 사용하여 Linux에서 HDInsight 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/)를 참조하세요. hello `publicKeys` hello 요소 [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) 파일은 사용 되는 toopass hello 키 tooAzure hello 클러스터를 만들 때. |

## <a id="sshpassword"></a>인증: 암호

SSH 계정은 암호를 사용하여 보호될 수 있습니다. TooHDInsight SSH를 사용 하 여 연결할 때 메시지 표시 tooenter hello 암호 됩니다.

> [!WARNING]
> SSH에 대한 암호 인증을 사용하는 것은 권장되지 않습니다. 암호 추측할 수 있으며 대입 공격 취약 toobrute 됩니다. 대신 [인증하기 위한 SSH 키](#sshkey)를 사용하는 것이 좋습니다.

### <a name="create-hdinsight-using-a-password"></a>암호를 사용하여 HDInsight 만들기

| 생성 방법 | Toospecify 암호 hello 하는 방법 |
| --------------- | ---------------- |
| **Azure 포털** | 기본적으로 hello SSH 사용자 계정에 hello hello 클러스터 로그인 계정과 동일한 암호로 합니다. toouse 다른 암호를 선택 취소 __동일한 암호를 사용 하 여 클러스터 로그인으로__, 다음 hello에 hello 암호를 입력 하 고 __SSH 암호__ 필드입니다.</br>![HDInsight 클러스터 생성의 SSH 암호 대화 상자](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | 사용 하 여 hello `--SshCredential` hello의 매개 변수 `New-AzureRmHdinsightCluster` cmdlet 전달는 `PSCredential` hello SSH 사용자 계정 이름 및 암호를 포함 하는 개체입니다. |
| **Azure CLI 1.0** | 사용 하 여 hello `--sshPassword` hello의 매개 변수 `azure hdinsight cluster create` 명령 고 hello 암호 값을 제공 합니다. |
| **Resource Manager 템플릿** | 템플릿에서 암호를 사용하는 예제는 [SSH 암호를 사용하여 Linux에서 HDInsight 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)를 참조하세요. hello `linuxOperatingSystemProfile` hello 요소 [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) 파일은 사용 되는 toopass는 hello SSH 계정 이름 및 암호 tooAzure hello 클러스터를 만들 때.|

### <a name="change-hello-ssh-password"></a>Hello SSH 암호 변경

Hello SSH 사용자 계정 암호를 변경 하는 방법에 대 한 정보를 참조 hello __암호 변경__ hello의 섹션 [관리할 HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) 문서.

## <a id="domainjoined"></a>인증: 도메인에 조인된 HDInsight

사용 하는 경우는 __도메인에 가입 된 HDInsight 클러스터__, hello를 사용 해야 `kinit` SSH로 연결한 후에 명령 합니다. 이 명령은 도메인 사용자 및 암호를 묻는 메시지를 표시 하 고 hello 클러스터와 연결 된 hello Azure Active Directory 도메인을 사용 하 여 세션이 인증.

자세한 내용은 [도메인에 조인된 HDInsight 구성](hdinsight-domain-joined-configure.md)을 참조하세요.

## <a name="connect-toonodes"></a>Toonodes 연결

헤드 노드 및 가장자리 노드 (있는 경우) hello hello를 통해 액세스할 수 포트 22 및 23 인터넷 합니다.

* Toohello 연결할 때 __헤드 노드__, 포트를 사용 하 여 __22__ tooconnect toohello 기본 헤드 노드 및 포트 __23__ tooconnect toohello 보조 헤드 노드. hello 정규화 된 도메인 이름 toouse은 `clustername-ssh.azurehdinsight.net`여기서 `clustername` hello 클러스터 이름입니다.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* 때 connectiung toohello __가장자리 노드__, 포트 22를 사용 합니다. hello 정규화 된 도메인 이름이 `edgenodename.clustername-ssh.azurehdinsight.net`여기서 `edgenodename` hello 가장자리 노드 만들 때 제공 된 이름입니다. `clustername`hello hello 클러스터 이름이입니다.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> hello 이전 예제에는 암호 인증을 사용 하는 또는 인증서 인증이 자동으로 발생 하는 가정 합니다. Hello를 사용 하 여 인증을 위해 SSH 키 쌍을 사용 하는 경우 hello 인증서 자동으로 사용 되지 않습니다. `-i` 매개 변수 toospecify hello에 대 한 개인 키입니다. 예: `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

연결 되 면 hello 프롬프트가 tooindicate hello SSH 사용자 이름 및 hello 노드에 연결 되어 변경 됩니다. 예를 들어, 연결 된 경우 toohello 기본 헤드 노드를 `sshuser`, hello 프롬프트가 `sshuser@hn0-clustername:~$`합니다.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Tooworker 및 사육 노드를 연결 합니다.

hello 작업자 노드 및 노드에서 직접 액세스할 수 없는 사육 hello 인터넷 합니다. Hello 클러스터 헤드 노드 또는 노드 가장자리에서 액세스할 수 있습니다. hello 다음은 hello 일반적인 단계 tooconnect tooother 노드.

1. SSH tooconnect tooa 또는 가장자리에서 헤드 노드를 사용 하 여:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Hello를 사용 하 여 SSH 연결 toohello 헤드 hello 또는 가장자리 노드 `ssh` hello 클러스터의 명령 tooconnect tooa 작업자 노드:

        ssh sshuser@wn0-myhdi

    tooretrieve hello hello 클러스터 노드 hello 도메인 이름 목록은 참조 hello [관리할 HDInsight를 사용 하 여 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) 문서.

SSH 계정 hello를 사용 하 여 보호 되는 경우는 __암호__를 연결할 때 hello 암호를 입력 합니다.

SSH 계정 hello를 사용 하 여 보호 되는 경우 __SSH 키__, SSH 전달 hello 클라이언트에서 활성화 되어 있는지 확인 합니다.

> [!NOTE]
> Toodirectly hello 클러스터의 모든 노드에 액세스 하는 또 다른 방법은 tooinstall을 Azure 가상 네트워크로 HDInsight는 합니다. 그런 다음 원격 컴퓨터 toohello 조인할 수 있습니다 동일한 가상 네트워크 및 hello 클러스터의 모든 노드에 직접 액세스 합니다.
>
> 자세한 내용은 [HDInsight와 함께 가상 네트워크 사용](hdinsight-extend-hadoop-virtual-network.md)을 참조하십시오.

### <a name="configure-ssh-agent-forwarding"></a>SSH 에이전트 전달 구성

> [!IMPORTANT]
> hello 다음 단계는 Linux 또는 UNIX 기반 시스템 및 가정 Bash Windows 10에서 작동 합니다. 시스템에 대 한 이러한 단계가 작동 하지 않습니다, 경우에 SSH 클라이언트에 대 한 tooconsult hello 설명서를 할 수 있습니다.

1. 텍스트 편집기를 사용하여 `~/.ssh/config`를 엽니다. 이 파일이 존재하지 않으면 명령줄에 `touch ~/.ssh/config`를 입력하여 만들 수 있습니다.

2. 다음 텍스트 toohello hello 추가 `config` 파일입니다.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Hello 대체 __호스트__ 정보 toousing SSH hello 노드의 hello 주소와 연결 합니다. hello 앞의 예제는 hello 가장자리 노드를 사용합니다. 이 항목에 지정 된 노드 hello에 대 한 전달 SSH 에이전트를 구성 합니다.

3. 테스트 SSH 에이전트 hello 터미널 hello에서 다음 명령을 사용 하 여 전달 합니다.

        echo "$SSH_AUTH_SOCK"

    이 명령은 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    아무 것도 반환되지 않으면 `ssh-agent`가 실행되지 않는 것입니다. 자세한 내용은 hello 에이전트 시작 스크립트에서 정보를 참조 하십시오. [를 사용 하 여 ssh-에이전트와 ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) 또는 SSH 클라이언트 설명서를 참조 하십시오.

4. 확인 한 후 **ssh-에이전트** SSH 개인 키 toohello 에이전트를 실행 하 고 사용 하 여 hello tooadd 다음 됩니다:

        ssh-add ~/.ssh/id_rsa

    개인 키로 다른 파일에 저장 되 면 대체 `~/.ssh/id_rsa` hello toohello 파일 경로 사용 합니다.

5. Toohello 클러스터 가장자리 노드 또는 SSH를 사용 하 여 헤드 노드를 연결 합니다. Hello SSH 명령 tooconnect tooa 작업자 또는 사육 노드를 사용 합니다. 전달 하는 hello 키를 사용 하 여 hello 연결이 설정 됩니다.

## <a name="copy-files"></a>파일 복사

hello `scp` 유틸리티 hello 클러스터의 개별 노드 모두에서 사용 되는 toocopy 파일 tooand 될 수 있습니다. 예를 들어 다음 명령은 복사본 hello hello `test.txt` hello 로컬 시스템 toohello 기본 헤드 노드에서 디렉터리:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Hello 후 지정 된 경로가 있으므로 `:`, hello 파일은 hello `sshuser` 홈 디렉터리입니다.

다음 예에서는 복사본 hello hello `test.txt` hello에서 파일 `sshuser` hello 기본 헤드 노드 toohello 로컬 시스템에 홈 디렉터리:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`hello 클러스터 내에서 개별 노드의 hello 파일 시스템만 액세스할 수 있습니다. Hello 클러스터에 대 한 hello HDFS 호환 저장소에서 사용 되는 tooaccess 데이터 수 없습니다.
>
> 사용 하 여 `scp` 대 한 SSH 세션에서 사용 하기 위해 리소스 tooupload 중지 해야 합니다. 예를 들어 Python 스크립트를 업로드 하 고 한 SSH 세션에서 hello 스크립트를 실행 합니다.
>
> Hello HDFS 호환 저장소에 데이터를 직접 로드에 대 한 내용은 다음 문서는 hello 참조:
>
> * [Azure Storage를 사용하는 HDInsight](hdinsight-hadoop-use-blob-storage.md)
>
> * [Azure Data Lake Store를 사용하는 HDInsight](hdinsight-hadoop-use-data-lake-store.md)

## <a name="next-steps"></a>다음 단계

* [HDInsight와 함께 SSH 터널링 사용](hdinsight-linux-ambari-ssh-tunnel.md)
* [HDInsight와 함께 가상 네트워크 사용](hdinsight-extend-hadoop-virtual-network.md)
* [HDInsight에서 에지 노드 사용](hdinsight-apps-use-edge-node.md#access-an-edge-node)