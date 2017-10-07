---
title: "Azure HDInsight에 R Server 시작 aaaGet | Microsoft Docs"
description: "어떻게 toocreate는 Apache는 R 서버를 포함 하는 HDInsight 클러스터에서을 멤버 알아보고 hello 클러스터에서 R 스크립트를 제출 합니다."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>HDInsight에서 R 서버 사용 시작

HDInsight는 HDInsight 클러스터에 통합 하는 R Server 옵션 toobe 포함 되어 있습니다. 이 옵션을 사용 하면 R 스크립트 toouse Spark 및 MapReduce distributed toorun 계산 합니다. 이 문서에서는 HDInsight 클러스터와 용 Spark를 사용 하 여 보여 주는 실행 R 스크립트에는 R 서버 toocreate R 계산을 분산 하는 방법을 배웁니다.


## <a name="prerequisites"></a>필수 조건

* **Azure 구독**: 이 자습서를 시작하기 전에 Azure 구독이 있어야 합니다. 이동 toohello 문서 [Get Microsoft Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) 자세한 정보에 대 한 합니다.
* **SSH (보안 셸) 클라이언트**: 프로그램의 SSH 클라이언트를 사용 하 tooremotely toohello HDInsight 클러스터에 연결 하 고 hello 클러스터에서 직접 명령을 실행 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.
* **SSH 키 (선택 사항)**: 암호 또는 공개 키 중 하나를 사용 하 여 hello SSH 사용 되는 계정 tooconnect toohello 클러스터를 보호할 수 있습니다. 암호를 사용 하 여 보다 쉽게 이며 허용 toocreate 공개/개인 키 쌍을 필요 없이 tooget 하기 시작 합니다. 하지만 키를 사용하는 것이 더 안전합니다.

> [!NOTE]
> 이 문서에 hello 단계는 암호를 사용 하는 것을 가정 합니다.


## <a name="automated-cluster-creation"></a>자동화된 클러스터 생성

Azure 리소스 관리자 템플릿, SDK, hello 및 또한 PowerShell을 사용 하 여 HDInsight R 서버 hello 만들기를 자동화할 수 있습니다.

* Azure 리소스 관리 템플릿을 사용 하는 R 서버 toocreate 참조 [R 서버 HDInsight 클러스터를 배포할](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/)합니다.
* hello.NET SDK를 사용 하 여 R 서버는 toocreate 참조 [hello.NET SDK를 사용 하 여 HDInsight의 Linux 기반 클러스터를 만듭니다.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* R 서버 toodeploy에 hello 문서를 참조 powershell을 사용 하 여 [HDInsight powershell에 R 서버 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)합니다.


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 hello 클러스터 만들기

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. **새로 만들기** -> **인텔리전스 + 분석** -> **HDInsight**를 차례로 선택합니다.

    ![새 클러스터를 만드는 과정의 이미지](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. Hello에 **빨리 만들기** 경험 hello에 hello 클러스터에 대 한 이름을 입력 하십시오 **클러스터 이름** 필드입니다. Hello를 사용 하 여 여러 Azure 구독이 있는 경우 **구독** 항목 tooselect hello 하나 toouse 원하는 합니다.

    ![클러스터 이름 및 구독 선택](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. 선택 **형식 클러스터** tooopen hello **클러스터 구성** 블레이드입니다. Hello에 **클러스터 구성** 블레이드에서 다음 옵션 선택 hello:

    * **클러스터 유형**: R Server
    * **버전**: R Server tooinstall hello 클러스터에서의 select hello 버전입니다. 현재 사용 가능한 hello 버전은 ***R 서버 (HDI 3.6) 9.1***합니다. 사용할 수 있는 버전의 R Server hello에 대 한 릴리스 정보는 사용할 수 있는 [여기](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)합니다.
    * **R 서버에 대 한 R Studio community edition**:이 브라우저 기반 IDE hello 가장자리 노드에 기본적으로 설치 됩니다. Toonot 않으려면 hello 확인란의 선택을 취소 한 다음 설치 합니다. Toohave를 선택 하는 경우이 앱 설치, RStudio 서버 로그인이 만들어지면 클러스터에 대 한 포털 응용 프로그램 블레이드에서 발견 된 hello에 액세스 하기 위한 hello URL.
    * Hello 기본값 hello 다른 옵션을 그대로 사용 하 고 hello를 사용 하 여 **선택** toosave hello 클러스터 유형 단추입니다.

        ![클러스터 유형 블레이드 스크린샷](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. **클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**를 입력합니다.

    **SSH 사용자 이름**을 지정합니다. SSH가 사용 되는 tooremotely toohello 클러스터 사용 하 여 연결 된 **SSH (보안 셸)** 클라이언트입니다. 이 대화 상자에 나 hello 클러스터 (hello hello 클러스터에 대 한 구성 탭)에서 만들어진 후 hello SSH 사용자를 지정할 수 있습니다. R 서버는 구성 된 tooexpect는 **SSH 사용자 이름이** "remoteuser"입니다.  **다른 사용자 이름을 사용 하는 경우에 hello 클러스터가 생성 된 후 추가 단계를 수행 해야 합니다.**

    Leave hello 상자에 대 한 검사 **동일한 암호를 사용 하 여 클러스터 로그인으로** toouse **암호** hello 인증 유형으로 공개 키의 사용을 선호 하지 않는 한 합니다.  예를 들어 RTVS, RStudio 또는 데스크톱 다른 IDE로 원격 클라이언트를 통해 hello 클러스터에 공개/개인 키 쌍 tooaccess R Server 필요합니다. Hello RStudio Server community edition을 설치 하는 경우 toochoose SSH 암호가 필요 합니다.     

    공개/개인 키 쌍을 사용 하 여 toocreate의 선택을 취소 **동일한 암호를 사용 하 여 클러스터 로그인으로** 선택한 후 **공개 키** 다음과 같이 계속 합니다. 이러한 지침에서는 ssh-keygen을 포함한 Cygwin 또는 이와 동등한 프로그램이 설치되어 있다고 가정합니다.

    * 노트북에 hello 명령 프롬프트에서 공개/개인 키 쌍을 생성 합니다.

        ssh-keygen -t rsa -b 2048

    * Hello 프롬프트 tooname 키 파일을 따르고 보안 강화를 위해 암호를 입력 합니다. 다음 이미지는 hello와 같은 화면이 표시:

        ![Windows의 SSH 명령줄](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * 이 명령은 개인 키 파일을 만들고 hello 이름 < 개인 키 파일 >.pub furiosa 및 furiosa.pub 예를 들어 아래에서 공개 키 파일을 만듭니다.

        ![SSH 디렉터리](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Hello 공개 키 파일 (&#42; 그런 다음 지정. pub) 할당 HDI 클러스터 자격 증명 하 고 마지막으로 리소스 그룹 및 지역 및 선택을 확인 하는 경우 **다음**합니다.

        ![자격 증명 블레이드](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * 노트북에 개인 키 파일 hello에 대 한 권한을 변경 합니다.

        chmod 600 <private-key-filename>

   * 원격 로그인에 대 한 SSH 함께 hello 개인 키 파일을 사용.

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      또는 Hadoop Spark의 부품 hello 정의 컨텍스트 R Server에 대 한 hello 클라이언트에서 계산 합니다. Hello 참조 **Hadoop 클라이언트와 Microsoft R Server를 사용 하 여** 에 하위 단원 [Spark에 대 한 계산 컨텍스트를 만들어](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark)합니다.

6. hello 빨리 만들기 toohello를 전환 **저장소** 블레이드 tooselect hello 저장소 계정 설정을 toobe hello hello의 기본 위치에 사용 되는 HDFS 파일 hello 클러스터에서 사용 하는 시스템입니다. 새 또는 기존 Azure Storage 계정이나 기존 Data Lake Storage 계정을 선택합니다.

    - 기존 저장소 계정을 선택 하 여 선택은 Azure 저장소 계정을 선택 하는 경우 **저장소 계정을 선택** 다음 hello 관련 계정을 선택 하 고 있습니다. Hello를 사용 하 여 새 계정 만들기 **새로 만들기** hello에 대 한 링크 **저장소 계정을 선택** 섹션.

      > [!NOTE]
      > 선택 하는 경우 **새로** hello 새 저장소 계정에 대 한 이름을 입력 해야 합니다. 녹색 확인 표시가 hello 이름이 수락 된 경우에 나타납니다.

      hello **기본 컨테이너** hello 클러스터의 기본값 toohello 이름입니다. Hello 값으로이 기본값을 그대로 둡니다.

      새 저장소 계정 옵션을 선택한 경우 프롬프트 tooselect **위치** 은 tooselect 제공 되는 영역 toocreate hello 저장소 계정입니다.  

         ![데이터 원본 블레이드](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Hello HDInsight 클러스터의 hello 위치를 설정 hello 기본 데이터 원본에 대 한 hello 위치를 선택 하면 됩니다. hello 클러스터와 기본 데이터 원본에에서 있어야 hello 동일한 지역입니다.

    - 선택 합니다 ADLS 저장소 계정 toouse hello 및 hello 클러스터를 추가 하려는 경우 기존 데이터 레이크 저장소 toouse, *추가* id tooyour 클러스터 tooallow 액세스 toohello 저장소입니다. 이 프로세스에 대한 자세한 내용은 [Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal)를 참조하세요.

    사용 하 여 hello **선택** 단추 toosave hello 데이터 소스 구성 합니다.


7. hello **요약** 블레이드 다음 표시 toovalidate 모든 설정 합니다. 변경할 수는 여기에 **클러스터 크기** toomodify hello 클러스터의 서버 수 및는 지정 **스크립트 작업을** toorun 원하는 합니다. 더 큰 클러스터를 사용 해야 하는 모른다면 hello 기본값인에 hello 작업자 노드 수를 두고 `4`합니다. hello 예상 비용 hello 클러스터의 hello 블레이드 내에서 표시 됩니다.

    ![클러스터 요약](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > 필요에 따라 hello 포털을 통해 나중에 클러스터 크기를 조정할 수 있습니다 (**클러스터** -> **설정** -> **배율 클러스터**) tooincrease 또는 hello 작업자 노드 수를 줄입니다.  이 크기를 조정 하는 것은 hello 클러스터 사용에 없는 경우 아래로 유휴 또는 용량 toomeet hello 요구 사항 보다 큰 작업을 추가 하는 데 유용할 수 있습니다.
   >
   >

   클러스터, hello 데이터 노드 및 hello 가장자리 노드 크기를 조정할 때 염두에서에 몇 가지 요인 tookeep 다음과 같습니다.  

   * hello 성능 Spark에 분산 된 R 서버 분석에 비례 toohello 작업자 노드 수 있으면 hello 데이터가 큽니다.  

   * R 서버 분석의 hello 성능은 분석 중인 데이터의 hello 크기에 비례 합니다. 예:  

     * 작은 toomodest 데이터에 대 한 성능이 hello 가장자리 노드에 대 한 로컬 계산 컨텍스트를 분석 하는 경우에 가장 좋습니다.  로컬 hello 및 Spark 계산 컨텍스트는 hello 시나리오에 대 한 자세한 내용은 적합 HDInsight에 R Server에 대 한 계산 컨텍스트 옵션을 참조 하십시오.<br>
     * Toohello 가장자리 노드에 로그인 하 고 R 스크립트 실행 후 실행 hello ScaleR rx 함수를 제외한 모든 <strong>로컬로</strong> hello 가장자리 노드에서 합니다. 따라서 메모리 hello 및 hello 가장자리 노드의 코어 수 적절 하 게 조정 해야 합니다. hello를 사용 하는 경우 R Server HDI에 원격 연산 컨텍스트로 랩톱에서에 마찬가지입니다.

     ![노드 가격 책정 계층 블레이드](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     사용 하 여 hello **선택** 단추 toosave hello 노드 가격 구성 합니다.

   **템플릿 및 매개 변수 다운로드**에 대한 링크도 있습니다. 선택한 구성 hello 사용 하 여 클러스터의 사용된 tooautomate hello 생성 될 수 있는이 링크 toodisplay 스크립트를 클릭 합니다. 만든 후에 이러한 스크립트 hello 클러스터에 대 한 Azure 포털 항목에서에서 사용할 수 있습니다.

   > [!NOTE]
   > 일반적으로 약 20 분을 만든 hello 클러스터 toobe에 몇 시간이 걸립니다. Hello 타일 hello 시작 보드를 사용 하거나 hello **알림** hello 페이지 toocheck의 hello 만들기 프로세스에 남아 있는 hello에 대 한 항목입니다.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>TooRStudio 서버 연결

설치에서 tooinclude RStudio 서버 community 버전을 선택 했으면 두 가지 방법을 통해 hello RStudio 로그인을 액세스할 수 있습니다.

1. Url toohello 이동 (여기서 **CLUSTERNAME** hello 클러스터를 만든 후의 hello 이름인):

    https://**CLUSTERNAME**.azurehdinsight.net/rstudio/

2. 클러스터에 대 한 hello 항목 선택 hello hello Azure 포털에서에서 열기 **R Server 대시보드** 빠른 연결을 선택한 다음 hello **R Studio 대시보드**:

     ![Hello R studio 대시보드 액세스](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Hello R studio 대시보드 액세스](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > 사용 되는 hello 방법에 관계 없이 hello 처음으로 로그인 해야 tooauthenticate 두 번 합니다.  Hello 첫 번째 인증에 hello 제공 *Admin userid 클러스터* 및 *암호*합니다. Hello 두 번째 프롬프트 hello 제공 *SSH userid* 및 *암호*합니다. 후속 로그 기능 하기만 hello *SSH 암호가* 및 *userid*합니다.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Toohello R Server 가장자리 노드를 연결 합니다.

SSH를 사용 하 여 hello 명령을 사용 하 여 hello HDInsight 클러스터의 서버 가장자리 노드 tooR 연결:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Hello를 찾을 수 있습니다 `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello 후 클러스터를 선택 하 여 Azure 포털에서에서 주소 **모든 설정을** -> **앱** -> **은 RServer**. Hello hello 가장자리 노드에 대 한 SSH 끝점 정보를 표시 합니다.
>
> ![Hello 가장자리 노드에 대 한 SSH 끝점 hello의 이미지](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

입력 정보 요청된 tooenter 모르는 암호 toosecure을 SSH 사용자 계정을 사용 하는 경우 것입니다. 공개 키를 사용한 경우 toouse hello `-i` 매개 변수 toospecify hello 일치 하는 개인 키입니다. 예:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

자세한 내용은 참조 [tooHDInsight (Hadoop) SSH를 사용 하 여 연결](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.

연결 된 후 본사에 도착 하면 프롬프트 비슷한 toohello 다음:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>여러 동시 사용자 사용

Hello 가장자리 노드 버전이 실행 되는 hello RStudio 커뮤니티에 대 한 더 많은 사용자를 추가 하 여 여러 동시 사용자가 사용할 수 있습니다.

HDInsight 클러스터를 만들 때 다음과 같이 두 사용자, 즉 HTTP 사용자와 SSH 사용자를 제공해야 합니다.

![동시 사용자 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **클러스터 로그인 사용자 이름과**: 사용자가 만든는 HTTP 사용자에 게는 사용 되는 tooprotect hello HDInsight hello HDInsight 게이트웨이 통해 인증 클러스터입니다. 이 HTTP 사용자는 다른 UI 구성 요소 뿐만 아니라 사용 되는 tooaccess hello Ambari UI, YARN UI가 있습니다.
- **SSH 사용자 이름 보안**: 셸 보안을 통해는 SSH 사용자 tooaccess hello 클러스터입니다. 이 사용자는 hello hello 헤드 노드, 작업자 노드 및 가장자리 노드 모두에 대 한 Linux 시스템의에서 사용자입니다. 사용할 수 있도록 보안 셸 tooaccess hello 노드 중 하나가 원격 클러스터에 있습니다.

HDInsight 유형 클러스터에서 Microsoft R Server hello에 사용 되는 hello R Studio Server 커뮤니티 버전 로그인 메커니즘으로 서 Linux 사용자 이름 및 암호를 허용 합니다. 토큰 전달은 지원하지 않습니다. 따라서 toouse R 스튜디오 tooaccess 고 새 클러스터를 만든 경우, 필요한 toolog에 두 번입니다.

- 먼저 hello HDInsight 게이트웨이 통해 HTTP hello 사용자 자격 증명을 사용 하 여 로그인: 

    ![동시 사용자 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- SSH 사용자 자격 증명 toolog hello를 사용 하 여 tooRStudio에서.
  
    ![동시 사용자 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

현재 HDInsight 클러스터를 프로비전할 때 SSH 사용자 계정 하나만 만들 수 있습니다. Tooenable 여러 사용자가 tooaccess HDInsight에 대 한 Microsoft R Server를 클러스터 하도록 hello Linux 시스템에서에서 추가 사용자 toocreate 필요 합니다.

RStudio Server 커뮤니티를 hello 클러스터 가장자리 노드에서 실행 되므로 여기에서 몇 가지 단계:

1. 만든 hello SSH 사용자 toolog toohello 가장자리 노드 사용
2. 에지 노드에 더 많은 Linux 사용자 추가
3. Hello 사용자가 만든 RStudio 커뮤니티 버전 사용

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>1 단계: toohello 가장자리 노드에서 만든 hello SSH 사용자 toolog 사용

모든 SSH 도구 (예: Putty)를 다운로드 하 고 hello 기존 SSH 사용자 toolog에서 사용 하 여 키를 누릅니다. 제공 하는 hello 지침에 따라 [tooHDInsight (Hadoop) SSH를 사용 하 여 연결](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello 가장자리 노드. HDInsight 클러스터에서 hello 가장자리 노드 주소가 R 서버에 대 한: *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>2단계: 에지 노드에 더 많은 Linux 사용자 추가

사용자 toohello 가장자리 노드 tooadd hello 명령을 실행 합니다.

    sudo useradd yournewusername -m
    sudo passwd yourusername

다음 항목을 반환 하는 hello를 표시 되어야 합니다. 

![동시 사용자 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

에 대 한 메시지가 표시 되 면 "현재 Kerberos 암호:", 누르기만 **Enter** tooignore 것입니다. hello `-m` 옵션 `useradd` 명령은 hello 시스템에서 RStudio 커뮤니티 버전에 필요한 hello 사용자에 대 한 홈 폴더를 만듦을 나타냅니다.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>사용자가 만든 hello와 3 단계: 사용 RStudio 커뮤니티 버전

사용자가 만든 toolog hello를 사용 하 여 tooRStudio에서:

![동시 사용자 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

RStudio 있음을 나타내도록 hello 새 사용자를 사용 하는 알림 (여기에서는 예를 들어 *sshuser6*) toolog hello 클러스터에서: 

![동시 사용자 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

Hello 원래 자격 증명을 사용 하 여 로그인 할 수 있습니다 (기본적으로 *sshuser*) 다른 브라우저 창에서 동시에 합니다.

scaleR 함수를 사용하여 작업을 제출할 수 있습니다. 다음 hello 사용 되는 명령 toorun의 예는 작업은:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


YARN UI에서 다른 사용자 이름 아래에서 제출 하는 hello 작업이 않았는지 확인 합니다.

![동시 사용자 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

또한 해당 hello 새로 추가 된 사용자가 루트 권한을 Linux 시스템에서 필요는 없지만 이러한 않습니다는 hello 동일한 참고 hello 원격 HDFS와 WASB 저장소에 tooall hello 파일에 액세스할 합니다.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Hello R 콘솔을 사용 하 여

1. Hello SSH 세션에서 다음 명령 toostart hello R 콘솔 hello를 사용 합니다.  

        R

2. 유사한 toohello 다음 출력이 표시 되어야 합니다.
    
    R 3.2.2 (2015-08-14)-버전 "화재 안전" Copyright (C) 2015 통계 컴퓨팅 플랫폼에 대 한 R Foundation hello: x86_64-pc-linux-gnu (64 비트)

    R은 평가판 소프트웨어이며 절대로 어떠한 보증도 제공되지 않습니다.
    시작 tooredistribute는 특정 조건에 해당 합니다.
    배포에 대한 자세한 내용을 보려면 'license()' 또는 'licence()'를 입력하세요.

    자연어가 지원되지만 영어 로캘로 실행됩니다.

    R은 많은 참가자가 함께한 공동 프로젝트입니다.
    게시에서 toocite R 또는 R 패키지 하는 방법에 대 한 자세한 내용과 'citation()' 'contributors()'를 입력 합니다.

    일부 데모, 온라인 도움말에 대 한 ' help()' 또는 'help.start()' HTML 브라우저 인터페이스 toohelp에 대 한 'demo()'를 입력 합니다.
    'Q()' tooquit 오른쪽 입력

    Microsoft R Server 버전 8.0: R Microsoft 패키지의 향상된 배포 Copyright (C) 2016 Microsoft Corporation

    릴리스 정보를 보려면 'readme()'를 입력하세요.
    >

3. Hello에서 `>` 프롬프트 R 코드를 입력할 수 있습니다. R 서버 tooeasily를 허용 하는 패키지에 포함 되어 Hadoop으로 상호 작용 하 고 분산 된 계산을 실행 합니다. 예를 들어 다음 hello HDInsight 클러스터에 대 한 hello 기본 파일 시스템의 명령 tooview hello 루트 hello를 사용 합니다.

    rxHadoopListFiles("/")

4. Hello WASB 스타일 주소 지정을 사용할 수 있습니다.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Microsoft R Server 또는 Microsoft R 클라이언트의 원격 인스턴스에서 HDI의 R Server 사용

Microsoft R Server 또는 데스크톱 또는 랩톱에서 실행 되는 Microsoft R 클라이언트의 원격 인스턴스에서 액세스 toohello HDI Hadoop Spark 계산 컨텍스트를 가능한 tooset 것 합니다. 참조 **Hadoop 클라이언트와 Microsoft R Server를 사용 하 여** hello에 하위 섹션 [Spark에 대 한 계산 컨텍스트를 만드는](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md)합니다. toodo toospecify hello 노트북에 hello RxSpark 계산 컨텍스트를 정의할 때 다음 옵션을 필요한 따라서: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, 및 sshProfileScript 합니다. 예:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>계산 컨텍스트 사용

계산 컨텍스트가 있습니다 toocontrol을 계산을 hello HDInsight 클러스터의 hello 노드에 분산 여부 hello 가장자리 노드에서 로컬로 수행 됩니다.

1. RStudio 서버나 (에 대 한 SSH 세션) hello R 콘솔에서 hello 기본 저장소에 HDInsight에 대 한 코드 tooload 예제 데이터를 다음 hello를 사용 합니다.

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. 다음으로, 보겠습니다 일부 데이터 정보를 만들고 म hello 데이터로 작업할 수 있도록 두 개의 데이터 소스를 정의 합니다.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Hello 로컬 계산 컨텍스트를 사용 하 여 hello 데이터에 대해 로지스틱 회귀를 실행 해 보겠습니다.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    출력 줄 비슷한 toohello 다음으로 끝나는 표시 되어야 합니다.

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. 그런 다음 확인해 보겠습니다 hello Spark 컨텍스트를 사용 하 여 동일한 로지스틱 회귀 hello 합니다. hello Spark 컨텍스트 hello hello HDInsight 클러스터의 모든 hello 작업자 노드를 통해 처리를 배포 합니다.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > 또한 클러스터 노드에서 MapReduce toodistribute 계산을 사용할 수 있습니다. 계산 컨텍스트에 대한 자세한 내용은 [HDInsight에서 R Server의 Compute 컨텍스트 옵션](hdinsight-hadoop-r-server-compute-contexts.md)을 참조하세요.


## <a name="distribute-r-code-toomultiple-nodes"></a>R 코드 toomultiple 노드 배포

R server 쉽게 기존 R 코드를 사용 하 고 수를 사용 하 여 hello 클러스터의 여러 노드에서 실행 `rxExec`합니다. 이 함수는 매개 변수 비우기 또는 시뮬레이션을 수행할 때 유용합니다. hello 다음 코드는 방법의 예로 toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

여전히 Spark hello 또는 MapReduce 컨텍스트를 사용 하는 경우이 명령은 값을 반환 hello nodename hello 작업자 노드에 대 한 해당 hello 코드 `(Sys.info()["nodename"])` 에서 실행 됩니다. 예를 들어 4 개 노드 클러스터에서 예상 tooreceive toohello 다음과 유사한 출력:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Hive 및 Parquet의 데이터 액세스

R 서버 9.1에서 제공 되는 기능에는 hello Spark 계산 컨텍스트에서 ScaleR 함수에서 사용 하기 위해 Hive 및 Parquet에 대 한 직접 액세스 toodata를 수 있습니다. 이러한 기능을 기능을 통해 새 ScaleR 데이터 소스 RxHiveData 및 RxParquetData 라는 Spark 데이터 프레임이 ScaleR에 따라 분석에 직접 Spark SQL tooload 데이터의 사용을 통해 작동 하는 사용할 수 있습니다.  

hello 코드 다음 몇 가지 샘플 코드 hello 새 기능을 사용 하는 제공 합니다.

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


이 새 함수에 대 한 추가 정보에 대 한 hello 사용 하 여 R Server에 hello 온라인 도움말을 참조 `?RxHivedata` 및 `?RxParquetData` 명령입니다.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Hello 가장자리 노드에 추가 R 패키지를 설치 합니다.

Hello 가장자리 노드에서 tooinstall 추가 R 패키지를 선택 하는 경우 사용할 수 있습니다 `install.packages()` 직접 내에서 R 콘솔 연결된 toohello SSH 통해 노드 가장자리 때 hello 합니다. 그러나 hello 클러스터의 작업자 노드 hello에 tooinstall R 패키지를 해야 하는 경우에 스크립트 작업을 사용 해야 합니다.

스크립트 동작 하는 사용 되는 toomake 구성 변경 내용을 toohello HDInsight 클러스터 또는 tooinstall 추가 같은 소프트웨어를 추가 R 패키지는 Bash 스크립트. 스크립트 동작을 사용 하 여 tooinstall 추가 패키지 단계를 수행 하는 hello를 사용 합니다.

> [!IMPORTANT]
> 스크립트 동작 tooinstall 추가 R 패키지를 사용 하 여만 사용할 수 있습니다 hello 클러스터를 만든 후. Hello 스크립트에서는 R Server 완전히 설치 및 구성 하는 대로 클러스터를 만드는 동안이 절차를 사용 하지 마십시오.
>
>

1. Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터에서 R 서버를 선택 합니다.

2. Hello에서 **설정** 블레이드를 **스크립트 동작** 차례로 **새 제출** toosubmit 새 스크립트 동작이 있습니다.

   ![스크립트 작업 블레이드의 이미지](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. Hello에서 **스크립트 동작을 제출** 블레이드에서 hello 다음 정보를 제공 합니다.

   * **이름**: 친숙 한 이름을 tooidentify이이 스크립트

   * **Bash 스크립트 URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **헤드**: **선택 취소**여야 함

   * **작업자**: **선택**이어야 함

   * **에지 노드**: **선택 취소**여야 함

   * **Zookeeper**: **선택 취소**여야 함

   * **매개 변수**: hello R 패키지 설치 toobe 합니다. 예를 들어 `bitops stringr arules`

   * **이 스크립트 유지...**: **선택**이어야 함  

   > [!NOTE]
   > 1. 기본적으로 hello Microsoft MRAN 리포지토리의 hello 버전의 설치 된 R Server와 일관 된 스냅숏에서 모든 R 패키지가 설치 됩니다. 최신 버전의 패키지 tooinstall 하려는 경우 다음 위험은 일부의 비 호환성입니다. 그러나이 설치 유형은 수를 지정 하 여 `useCRAN` hello로 hello 패키지의 첫 번째 요소 목록, 예를 들어 `useCRAN bitops, stringr, arules`합니다.  
   > 2. 일부 R 패키지에는 추가 Linux 시스템 라이브러리가 필요합니다. 편의 위해 우리는 사전 설치 된 hello 상위 100 가장 인기 있는 R 패키지에 필요한 hello 종속성. 그러나 이러한 보다 더 많은 라이브러리를 필요 hello R 패키지를 설치한 경우 다음 여기에 hello 기본 스크립트를 다운로드 하며 단계 tooinstall hello 시스템 라이브러리를 추가 합니다. 업로드 수정 hello 스크립트 tooa 공용 Azure 저장소 컨테이너에에서 blob 하 고 수정 하는 hello 스크립트 tooinstall hello 패키지를 사용 해야 합니다.
   >    스크립트 작업 개발에 대한 자세한 내용은 [스크립트 작업 개발](hdinsight-hadoop-script-actions-linux.md)을 참조하세요.  
   >
   >

   ![스크립트 작업 추가](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. 선택 **만들기** toorun hello 스크립트입니다. Hello 스크립트가 완료 되 면 hello R 패키지는 모든 작업자 노드에 사용할 수 있습니다.


## <a name="using-microsoft-r-server-operationalization"></a>Microsoft R Server 조작화 사용

데이터 모델링 완료 되 면 hello 모델 toomake 예측 실제로 운영할 수 있습니다. Microsoft R Server 화에 대 한 tooconfigure hello 다음 단계를 수행 합니다.

첫째, ssh hello 가장자리 노드로 합니다. 예를 들면 다음과 같습니다. 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

사용 하 여 ssh를 hello 관련 버전 및 sudo hello dotnet dll에 대 한 디렉터리를 변경 합니다. 

- Microsoft R Server 9.1의 경우:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Microsoft R Server 9.0의 경우:

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

한 기본 구성 사용 하 여 Microsoft R Server 해결해줍니다 tooconfigure 다음 hello지 않습니다.

1. [R Server 조작화 구성]을 선택합니다.
2. “A. One-box(웹 + 계산 노드)”를 선택합니다.
3. Hello에 대 한 암호를 입력 **admin** 사용자

![one-box 조작화](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

선택적 단계로 다음과 같이 진단 테스트를 실행하여 진단 검사를 수행할 수 있습니다.

1. “6. 진단 테스트 실행”을 선택합니다.
2. “A. 구성 테스트”를 선택합니다.
3. 이전 구성 단계에서 사용자 이름("admin")과 암호를 입력합니다.
4. Confirm Overall Health(전체 상태 확인)이 pass(합격)인지 확인합니다.
5. 종료 hello 관리 유틸리티
6. SSH를 종료합니다.

![조작화에 대한 진단](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Spark에 웹 서비스를 이용할 때 긴 지연**
>
>Spark 계산 컨텍스트에서 mrsdeploy 함수를 사용 하 여 만든 웹 서비스 tooconsume 동안 오래 지연 발생 하면 일부 누락 된 폴더에 tooadd 할 수 있습니다. hello Spark 응용 프로그램 이라는 tooa 사용자 속해 '*rserve2*' 때마다 mrsdeploy 함수를 사용 하는 웹 서비스에서 호출 됩니다. 이 문제를 해결 toowork:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


이 단계에서 화에 대 한 hello 구성이 완료 되었습니다. 사용할 수 있습니다 이제 'hello 'mrsdeploy 가장자리 노드 여 RClient tooconnect toohello 화에 패키지 하 고과 같은 해당 기능을 사용 하 여 시작 [원격 실행](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) 및 [웹 서비스](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette)합니다. 설정에 따라 여부 클러스터 가상 네트워크에 여부, tooset SSH 로그인을 통해 포트 전달 터널링을 할 수 있습니다. hello 다음 섹션에서는 어떻게 tooset이이 터널이 설정 합니다.

### <a name="rserver-cluster-on-virtual-network"></a>가상 네트워크의 RServer 클러스터

포트 12800 toohello 가장자리 노드를 통해 트래픽을 허용 하는지 확인 합니다. 이런 방식으로 hello 가장자리 노드 tooconnect toohello 화 기능을 사용할 수 있습니다.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


경우 hello `remoteLogin()` 없습니다 toohello 가장자리 노드를 연결 하지만 SSH toohello 가장자리 노드 수 해야 합니다 tooverify 제대로 또는 하지 hello 규칙 tooallow 트래픽 12800 포트에서 설정 된 여부. Tooface hello 문제를 계속 진행 하면 SSH를 통해 정방향 터널링 포트를 설정 하 여 해결할 수 있습니다. Hello 다음 단원을 참조 하십시오.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>가상 네트워크에 설정되지 않은 RServer 클러스터

클러스터가 VNet에 설정되지 않았거나 VNet을 통한 연결에 문제가 있는 경우 SSH 포트 전달 터널링을 사용할 수 있습니다.

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Putty에서도 이 터널링을 설정할 수 있습니다.

![Putty ssh 연결](./media/hdinsight-hadoop-r-server-get-started/putty.png)

SSH 세션이 활성 상태인 컴퓨터의 포트 12800 hello 트래픽은 toohello 가장자리 노드 포트 12800 SSH 세션을 통해 전달 됩니다. `remoteLogin()` 메서드에서 `127.0.0.1:12800`을 사용해야 합니다. 이 포트 전달을 통해 toohello 가장자리 노드 화에 기록 됩니다.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Microsoft R Server 해결해줍니다 tooscale HDInsight 작업자 노드에 있는 노드를 계산 하는 방법

### <a name="decommission-hello-worker-nodes"></a>Hello 작업자 노드를 서비스 해제

Microsoft R Server는 현재 Yarn을 통해 관리되지 않습니다. Hello 작업자 노드를 서비스 해제 없는 hello Yarn 리소스 관리자의 hello 서버에서 차지 하는 hello 리소스 인식 되지 않습니다 때문에 예상 대로 작동 하지 않습니다. 순서 tooavoid이이 경우 권장 hello 계산 노드를 확장 하기 전에 hello 작업자 노드를 서비스 해제 합니다.

단계 toodecommissioning 작업자 노드:

* Ambari 콘솔 tooHDI 클러스터를 로그인 하 고 "호스트" 탭을 클릭
* 작업자 노드 (toobe 서비스 해제) 선택 "작업"를 클릭 하십시오. > "선택한 호스트" > "호스트" > "ON 유지 관리 모드 설정"을 클릭 합니다. 예를 들어 다음 이미지는 hello म wn3 및 wn4 toodecommission을 선택 했습니다.  

   ![작업자 노드 서비스 해제](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* **작업** > **선택한 호스트** > **DataNodes**를 선택하고 > **서비스 해제**를 클릭합니다.
* **작업** > **선택한 호스트** > **NodeManagers**를 선택하고 > **서비스 해제**를 클릭합니다.
* **작업** > **선택한 호스트** > **DataNodes**를 선택하고 > **중지**를 클릭합니다.
* **작업** > **선택한 호스트** > **NodeManagers**를 선택하고 > **중지**를 클릭합니다.
* **작업** > **선택한 호스트** > **호스트**를 선택하고 > **모든 구성 요소 중지**를 클릭합니다.
* Hello 헤드 노드를 선택 하 고 hello 작업자 노드를 선택 취소 합니다.
* **작업** > **선택한 호스트** > "**호스트** > **모든 구성 요소 다시 시작**을 선택합니다.

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>서비스 해제된 작업자 노드 각각에 Compute 노드 구성

1. SSH를 서비스 해제된 각 작업자 노드로 실행합니다.
2. `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`을 사용하여 관리 유틸리티를 실행합니다.
3. "1" tooselect 옵션 "구성 R 서버에 대 한 해결해줍니다"를 입력 합니다.
4. 입력 "c" tooselect 옵션 "3. Compute 노드" 옵션을 선택합니다. 그러면 hello 작업자 노드 hello 계산 노드를 구성 됩니다.
5. 종료 hello 관리 유틸리티입니다.

### <a name="add-compute-nodes-details-on-web-node"></a>웹 노드에 계산 노드 세부 정보 추가

모든 서비스가 해제 된 작업자 노드 구성 되 면 toorun 계산 노드, hello 가장자리 노드에서 돌아와 hello Microsoft R Server 웹 노드 구성에서 폐기 된 작업자 노드 IP 주소 추가:

* Hello 가장자리 노드로 SSH 합니다.
* `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`을 실행합니다.
* Hello "Uri" 섹션을 살펴보고 작업자 노드 IP 및 포트 세부 정보를 추가 합니다.

    ![작업자 노드 서비스 해제 명령줄](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.


## <a name="next-steps"></a>다음 단계

이제 새 HDInsight 클러스터를 사용 하 여 hello R 서버 및 hello 기본 사항 toocreate 대 한 SSH 세션에서 R 콘솔 hello 하는 방법을 이해 해야 합니다. hello 다음 항목에서는 설명 관리 하 고 HDInsight에 R server 작업의 다른 방법:

* [RStudio 서버 tooHDInsight 추가 (클러스터를 만드는 동안 설치 되지 않은) 하는 경우](hdinsight-hadoop-r-server-install-r-studio.md)
* [HDInsight의 R 서버에 대한 Compute 컨텍스트 옵션](hdinsight-hadoop-r-server-compute-contexts.md)
* [HDInsight에서 R Server의 Azure Storage 옵션](hdinsight-hadoop-r-server-storage.md)
