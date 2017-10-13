---
title: "HDInsight의 R Server를 사용하여 RStudio 설치 - Azure | Microsoft Docs"
description: "HDInsight에서 R Server를 사용하여 RStudio를 설치하는 방법입니다."
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
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>HDInsight의 R Server를 사용하여 RStudio 설치

이 문서에서는 사용자 지정 스크립트를 사용하여 클러스터의 에지 노드에 [RStudio Server](https://www.rstudio.com/products/rstudio-server/)의 커뮤니티(무료) 버전을 설치하는 방법을 알아봅니다. RStudio Server는 원격 클라이언트에서 사용할 브라우저 기반 IDE를 제공하며 Linux에서 널리 사용되고 있습니다. 오늘날 다음을 포함해 R에 사용 가능한 여러 IDE(통합된 개발 환경)가 있습니다.

- Microsoft용 [Visual Studio용 R 도구](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx)(RTVS) 
- [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 
- Walware의 Eclipse 기반 [StatET](http://www.walware.de/goto/statet)

RStudio Server를 HDInsight 클러스터의 에지 노드에 설치하는 이점은 클러스터의 R Server를 사용하여 R 스크립트를 개발 및 실행할 수 있는 완벽한 IDE 환경이 제공한다는 점입니다. 이 구성은 R 콘솔의 기본 용도보다 상당히 생산성이 높을 수 있습니다. 

> [!NOTE]
> 이 문서에서 설명하는 절차는 클러스터를 프로비전할 때 RStudio Server 커뮤니티 에디션을 설치하도록 선택하지 않은 경우에만 해당됩니다. 프로비전 중에 추가한 경우 클러스터의 Azure Portal 항목에서 **R Server 대시보드** 타일을 클릭한 다음 **R Studio Server** 타일을 클릭하여 액세스합니다. 

상업적으로 사용이 허가된 Pro 버전의 RStudio 서버를 사용하려면 [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/)에서 제공하는 설치 지침을 따라야 합니다.

> [!NOTE]
> [R 스크립트 작업 설치](hdinsight-hadoop-r-scripts-linux.md)를 사용하여 R이 설치된 HDInsight 클러스터를 사용하는 경우 HDInsight 클러스터의 R Server가 필요하므로 이 단계의 단계가 제대로 작동하지 않습니다.
>
> 

## <a name="prerequisites"></a>필수 조건

* R 서버가 설치된 Azure HDInsight 클러스터. 자세한 내용은 [HDInsight 클러스터에서 R 서버 시작](hdinsight-hadoop-r-server-get-started.md)을 참조하세요.
* SSH 클라이언트. Linux 및 Unix 배포 또는 Macintosh OS X의 경우 `ssh` 명령은 운영 체제에 제공됩니다. Windows의 경우 [OpenSSH 옵션](https://www.youtube.com/watch?v=CwYSvvGaiWU) 또는 [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)와 함께 [Cygwin](http://www.redhat.com/services/custom/cygwin/)를 사용하는 것이 좋습니다.  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a>사용자 지정 스크립트를 사용하여 클러스터에 RStudio 설치

단계는 다음과 같습니다.

1. 클러스터의 에지 노드를 식별합니다. R 서버가 설치된 HDInsight 클러스터의 경우 헤드 노드와 에지 노드에 대한 명명 규칙은 다음과 같습니다.
   * 헤드 노드: `CLUSTERNAME-ssh.azurehdinsight.net`
   * 에지 노드: `CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. 1단계에 제공된 명명 패턴을 사용하여 클러스터의 에지 노드로 SSH를 실행합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

3. 연결이 완료되면 클러스터의 루트 사용자가 됩니다. SSH 세션에서 다음 명령을 사용합니다.

        sudo su -

4. 사용자 지정 스크립트를 다운로드하여 RStudio를 설치합니다. 다음 명령을 사용합니다.

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. 사용자 지정 스크립트 파일에 대한 권한을 변경하고 스크립트를 실행합니다. 다음 명령을 사용합니다.

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. R 서버가 설치된 HDInsight 클러스터를 만드는 동안 SSH 암호를 사용한 경우 이 단계를 건너뛰고 다음 단계로 진행할 수 있습니다. 그렇지 않고 SSH 키를 사용하여 클러스터를 만든 경우 SSH 사용자에 대한 암호를 설정해야 합니다. RStudio에 연결할 때 이 암호가 필요합니다. 다음 명령을 실행합니다.

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. **현재 Kerberos 암호**를 묻는 메시지가 표시되면 **Enter** 키를 누르면 됩니다.  `USERNAME` 을(를) HDInsight 클러스터에 대한 SSH 사용자로 교체해야 합니다. 암호가 성공적으로 설정된 경우 다음과 같은 메시지가 표시됩니다.

        passwd: password updated successfully

    SSH 세션을 종료합니다.

8. HDInsight 클러스터에서 `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` 을 클라이언트 컴퓨터에 매핑하여 클러스터에 대한 SSH 터널을 만듭니다. 새 브라우저 세션을 열기 전에 SSH 터널을 만들어야 합니다.

   * [Cygwin](http://www.redhat.com/services/custom/cygwin/)을 사용하는 Linux 클라이언트 또는 Windows 클라이언트에서 터미널 세션을 열고 다음 명령을 사용합니다.

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       **USERNAME**을 HDInsight 클러스터에 대한 SSH 사용자로 바꾸고 **CLUSTERNAME**을 HDInsight 클러스터의 이름으로 바꿉니다.
       `-i id_rsa_key`를 추가하여 암호가 이닌 SSH 키를 사용할 수도 있습니다.        
   * PuTTY와 Windows 클라이언트를 사용하는 경우

     1. PuTTY를 열고 연결 정보를 입력합니다.
     2. 대화 상자의 왼쪽에 있는 **Category** 섹션에서 **Connection**, **SSH**를 차례로 확장한 다음 **Tunnels**를 선택합니다.
     3. **Options controlling SSH port forwarding** 양식에 다음 정보를 제공합니다.

        * **Source port** - 전달하려는 클라이언트의 포트입니다. 예를 들면 **8787**과 같습니다.
        * **Destination** - 로컬 클라이언트 컴퓨터에 매핑해야 하는 대상입니다. 예를 들면 **localhost:8787**과 같습니다.

            ![SSH 터널 만들기](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "SSH 터널 만들기")

     4. **Add**를 클릭하여 설정을 추가한 다음 **Open**을 클릭하여 SSH 연결을 엽니다.
     5. 메시지가 표시되면 서버에 로그인하여 SSH 세션을 설정하고 터널을 활성화합니다.

9. 웹 브라우저를 열고 터널에 대해 입력한 포트에 따라 다음 URL을 입력합니다.

        http://localhost:8787/ 

10. 클러스터에 연결할 SSH 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다. 클러스터를 만드는 동안 SSH 키를 사용한 경우 5단계에서 만든 암호를 입력해야 합니다.

    ![R 스튜디오에 연결](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "R 스튜디오에 연결")

11. RStudio 설치의 성공 여부를 테스트하려면 클러스터에서 R 기반 MapReduce 및 Spark 작업을 실행하는 테스트 스크립트를 실행하면 됩니다. RStudio에서 실행할 테스트 스크립트를 다운로드하려면 SSH 콘솔로 돌아가 다음 명령을 입력하세요.

    *    R이 설치된 Hadoop 클러스터를 만든 경우 다음 명령을 사용합니다.

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    R이 설치된 Spark 클러스터를 만든 경우 다음 명령을 사용합니다.

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. RStudio에 다운로드한 테스트 스크립트가 표시됩니다. 파일을 두 번 클릭하여 열고 파일의 내용을 선택한 다음 **Run**을 클릭합니다. **Console** 창에 출력이 표시됩니다.

   ![설치 테스트](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "설치 테스트")

또 다른 옵션은 `source(testhdi.r)` 또는 `source(testhdi_spark.r)`을(를) 입력하여 스크립트를 실행하는 것입니다.

## <a name="see-also"></a>참고 항목

* [HDInsight 클러스터의 R 서버에 대한 계산 컨텍스트 옵션](hdinsight-hadoop-r-server-compute-contexts.md)
* [HDInsight에서 R Server의 Azure Storage 옵션](hdinsight-hadoop-r-server-storage.md)

