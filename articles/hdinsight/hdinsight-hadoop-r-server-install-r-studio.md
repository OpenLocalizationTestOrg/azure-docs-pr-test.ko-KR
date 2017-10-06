---
title: "Azure HDInsight에 R server RStudio aaaInstall | Microsoft Docs"
description: "어떻게 tooinstall HDInsight에 R server RStudio 합니다."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>HDInsight의 R Server를 사용하여 RStudio 설치

이 문서에서는 tooinstall 커뮤니티 (무료) 버전의 hello 하는 방법을 설명 [RStudio 서버](https://www.rstudio.com/products/rstudio-server/) hello 가장자리 노드는 사용자 지정 스크립트를 사용 하는 클러스터에 있습니다. RStudio Server는 원격 클라이언트에서 사용할 브라우저 기반 IDE를 제공하며 Linux에서 널리 사용되고 있습니다. 오늘날 다음을 포함해 R에 사용 가능한 여러 IDE(통합된 개발 환경)가 있습니다.

- Microsoft용 [Visual Studio용 R 도구](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx)(RTVS) 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- Walware의 Eclipse 기반 [StatET](http://www.walware.de/goto/statet)

HDInsight 클러스터의 hello 가장자리 노드에서 RStudio 서버를 설치할 hello 장점은 제공 하는 전체 IDE 환경을 hello 개발 및 R 스크립트의 실행에 대 한 R server hello 클러스터입니다. 이 구성은 hello R 콘솔의 기본 사용 보다 훨씬 더 생산적 수 있습니다.

> [!NOTE]
> 이 문서에서 설명 하는 hello 절차는 클러스터를 프로 비전 할 때 tooinstall RStudio 서버 community 버전을 선택 하지 않은 경우 해당만 합니다. 프로 비전에서 추가한 경우 hello에서 클릭 것 tooaccess 다음 **R Server 대시보드** hello 클러스터에 대 한 다음 hello에서 Azure 포털 항목에서에서 타일 **R Studio 서버** 바둑판식으로 배열입니다. 

Hello 설치 지침을 따라야 RStudio 서버의 toouse 상업적으로 사용이 허가 된 hello Pro 버전을 원하는 경우 [RStudio 서버](https://www.rstudio.com/products/rstudio/download-server/)합니다.

> [!NOTE]
> R가 설치 hello를 사용 하 여 HDInsight 클러스터를 사용 하는 경우 [설치 R 스크립트 작업](hdinsight-hadoop-r-scripts-linux.md),이 문서의 단계 hello 작동 하지 것입니다는 R 서버 hello HDInsight 클러스터에 필요한 대로 제대로 합니다.
>
> 

## <a name="prerequisites"></a>필수 조건

* R 서버가 설치된 Azure HDInsight 클러스터. 자세한 내용은 [HDInsight 클러스터에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요.
* SSH 클라이언트. Macintosh OS X, Linux 및 Unix 배포에 대 한 hello `ssh` 명령은 hello 운영 체제와 함께 제공 됩니다. Windows의 경우 권장 [Cygwin](http://www.redhat.com/services/custom/cygwin/) hello로 [OpenSSH 옵션](https://www.youtube.com/watch?v=CwYSvvGaiWU), 또는 [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)합니다.  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>사용자 지정 스크립트를 사용 하 여 hello 클러스터에 RStudio를 설치 합니다.

Hello 단계는 다음과 같습니다.

1. Hello 클러스터의 hello 가장자리 노드를 식별 합니다. R server는 HDInsight 클러스터에 대 한 다음은 헤드 노드 및 가장자리 노드 hello 명명 규칙입니다.
   * 헤드 노드: `CLUSTERNAME-ssh.azurehdinsight.net`
   * 에지 노드: `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. 1 단계에서 제공 하는 hello 명명 패턴을 사용 하 여 hello 클러스터의 hello 가장자리 노드로 SSH 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

3. 연결 되 면 hello 클러스터 상의 루트 사용자 됩니다. Hello SSH 세션에서 다음 명령을 hello를 사용 합니다.

        sudo su -

4. 사용자 지정 스크립트 tooinstall hello RStudio를 다운로드 합니다. 다음 명령을 사용 하 여 hello:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Hello 사용자 지정 스크립트 파일에 대 한 hello 권한을 변경 하 고 hello 스크립트를 실행 합니다. 다음 명령을 사용 하 여 hello:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. R server는 HDInsight 클러스터를 만드는 동안 SSH 암호를 사용 하는 경우이 단계를 건너뛰고 toohello 다음 계속 수 있습니다. SSH 키 대신 toocreate hello 클러스터를 사용한 경우 SSH 사용자에 대 한 암호를 설정 해야 합니다. TooRStudio 연결할 때이 암호가 필요 합니다. Hello 다음 명령을 실행 합니다.

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. **현재 Kerberos 암호**를 묻는 메시지가 표시되면 **Enter** 키를 누르면 됩니다.  `USERNAME` 을(를) HDInsight 클러스터에 대한 SSH 사용자로 교체해야 합니다. 암호를 성공적으로 설정 hello 메시지의 뒤에 표시 되어야 합니다.

        passwd: password updated successfully

    Hello SSH 세션을 종료 합니다.

8. 매핑 SSH 터널 toohello 클러스터를 만드는 `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello HDInsight 클러스터에서 toohello 클라이언트 컴퓨터입니다. 새 브라우저 세션을 열기 전에 SSH 터널을 만들어야 합니다.

   * Linux 클라이언트 또는 사용 하 여 Windows 클라이언트에서 [Cygwin](http://www.redhat.com/services/custom/cygwin/)터미널 세션을 열고 다음 명령을 hello를 사용 하 여:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       대체 **USERNAME** HDInsight 클러스터와 바꾸기에 대 한 SSH 사용자 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.
       `-i id_rsa_key`를 추가하여 암호가 이닌 SSH 키를 사용할 수도 있습니다.        
   * PuTTY와 Windows 클라이언트를 사용하는 경우

     1. PuTTY를 열고 연결 정보를 입력합니다.
     2. Hello에 **범주** 섹션 toohello hello 대화의 왼쪽, 확장 **연결**를 확장 하 고 **SSH**를 선택한 후 **터널**합니다.
     3. Hello hello에 다음 정보를 제공 **SSH에 대 한 옵션 포트 전달** 형식:

        * **원본 포트** -hello tooforward 한다고 hello 클라이언트에는 포트입니다. 예를 들면 **8787**과 같습니다.
        * **대상** -hello 해야 하는 대상 매핑된 toohello 로컬 클라이언트 컴퓨터입니다. 예를 들면 **localhost:8787**과 같습니다.

            ![SSH 터널 만들기](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "SSH 터널 만들기")

     4. 클릭 **추가** tooadd hello 설정 하 고 클릭 **열려** tooopen SSH 연결 합니다.
     5. 대화 상자가 나타나면 toohello 서버 tooestablish SSH 세션을 사용 하도록 설정한 hello 터널이 기록 합니다.

9. 웹 브라우저를 열고 hello hello 포트 hello 터널에 대 한 입력에 따라 url을 입력 합니다.

        http://localhost:8787/ 

10. 입력 정보 요청된 tooenter hello SSH 사용자 이름 및 암호 tooconnect toohello 클러스터 됩니다. SSH 키를 사용 하는 hello 클러스터를 만드는 동안 경우 5 단계에서 만든 hello 암호를 입력 해야 합니다.

    ![Studio tooR 연결](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "SSH 터널을 만들어")

11. tootest hello RStudio 설치 성공 여부, hello 클러스터에서 R 기반 Spark 및 MapReduce 작업을 실행 하는 테스트 스크립트를 실행할 수 있습니다. RStudio, toodownload hello 테스트 스크립트 toorun toohello SSH 콘솔 돌아가서 hello 다음 명령을 입력 합니다.

    *    R이 설치된 Hadoop 클러스터를 만든 경우 다음 명령을 사용합니다.

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    R이 설치된 Spark 클러스터를 만든 경우 다음 명령을 사용합니다.

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. RStudio, 다운로드 한 스크립트를 테스트 하는 hello를 볼 수 있습니다. Hello 파일 tooopen hello 파일의 hello 내용을 선택 하 고 클릭 한 다음를 두 번 클릭 **실행**합니다. Hello에 hello 출력이 **콘솔** 창:

   ![Hello 설치 테스트](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "hello 설치 테스트")

또 다른 옵션 tootype 것 `source(testhdi.r)` 또는 `source(testhdi_spark.r)` tooexecute hello 스크립트입니다.

## <a name="see-also"></a>참고 항목

* [HDInsight 클러스터의 R 서버에 대한 계산 컨텍스트 옵션](hdinsight-hadoop-r-server-compute-contexts.md)
* [HDInsight에서 R Server의 Azure Storage 옵션](hdinsight-hadoop-r-server-storage.md)

