---
title: "공유 액세스 서명-Azure HDInsight를 사용 하 여 aaaRestrict 액세스 | Microsoft Docs"
description: "공유 액세스 서명 toorestrict toouse HDInsight toodata Azure 저장소 blob에 저장 된 액세스 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Azure 저장소 공유 액세스 서명 toorestrict 액세스 toodata를 사용 하 여 HDInsight의

HDInsight 대 한 모든 권한을 toodata hello 클러스터와 연결 된 hello Azure 저장소 계정에 저장 합니다. 공유 액세스 서명 hello blob 컨테이너 toorestrict 액세스 toohello 데이터에 사용할 수 있습니다. 예를 들어 tooprovide 읽기 전용 액세스 toohello 데이터입니다. 공유 액세스 서명 (SAS)는 Azure 저장소 계정의 toolimit 액세스 toodata 수 있는 기능. 예를 들어 toodata 읽기 전용 액세스를 제공합니다.

> [!IMPORTANT]
> Apache Ranger를 사용하는 솔루션의 경우 도메인에 가입된 HDInsight를 사용하는 것이 좋습니다. 자세한 내용은 참조 hello [도메인에 가입 된 HDInsight 구성](hdinsight-domain-joined-configure.md) 문서.

> [!WARNING]
> HDInsight에 대 한 모든 권한을 toohello 기본 저장소 hello 클러스터에 있어야 합니다.

## <a name="requirements"></a>요구 사항

* Azure 구독
* C# 또는 Python. C# 예제 코드가 Visual Studio 솔루션으로 제공됩니다.

  * Visual Studio는 버전 2013, 2015 또는 2017이어야 합니다.
  * Python은 버전 2.7 이상이어야 합니다.

* Linux 기반 HDInsight 클러스터 또는 [Azure PowerShell] [ powershell] -Linux 기반 기존 클러스터를 설정한 경우 Ambari tooadd 공유 액세스 서명을 toohello 클러스터를 사용할 수 있습니다. 그렇지 않은 경우 Azure PowerShell toocreate 클러스터를 사용 하 고 클러스터를 만드는 동안 공유 액세스 서명을 추가할 수 있습니다.

    > [!IMPORTANT]
    > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* 예를 들어 파일에서 hello [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature)합니다. 이 저장소는 다음 항목 hello를 포함 되어 있습니다.

  * HDInsight에 사용할 저장소 컨테이너, 저장된 정책 및 SAS를 만들 수 있는 Visual Studio 프로젝트
  * HDInsight에 사용할 저장소 컨테이너, 저장된 정책 및 SAS를 만들 수 있는 Python 스크립트
  * PowerShell 스크립트는 HDInsight를 만들 수 있는 클러스터 및 toouse hello SAS를 구성 합니다.

## <a name="shared-access-signatures"></a>공유 액세스 서명

두 가지 형태의 공유 액세스 서명이 있습니다.

* 임시: hello 시작 시간, 만료 시간 및 SAS hello SAS URI에 지정 된 모든 hello에 대 한 권한.

* 저장된 액세스 정책: 저장된 액세스 정책은 Blob 컨테이너 같은 리소스 컨테이너에서 정의됩니다. 정책에는 하나 이상의 공유 액세스 서명에 대 한 제약 조건을 사용 하는 toomanage 될 수 있습니다. 저장 된 액세스 정책을 사용 하 여 SAS를 연결 하면 hello SAS hello 제약 조건을 상속-hello 시작 시간, 만료 시간 및 사용 권한-hello 저장 된 액세스 정책을 정의 합니다.

hello hello 두 형식의 차이 한 가지 주요 시나리오에 대 한 중요: 해지 합니다. SAS URL을 이므로 모든 사용자에 게 SAS hello 가져옵니다 צ ְ ײ, 요청한 사용자에 관계 없이 toobegin. SAS를 공개적으로 게시 하는 경우에 hello world의 다른 사용자가 사용할 수 있습니다. 분산된 SAS는 다음 네 가지 중 하나에 해당할 때까지 유효합니다.

1. SAS에 도달 하는 hello에 지정 된 만료 시간을 hello입니다.

2. SAS에 도달 하는 hello에서 참조 하는 hello 저장 된 액세스 정책에 지정 된 만료 시간을 hello입니다. hello 다음과 같은 시나리오를 사용 하면 hello 만료 시간에 도달 toobe:

    * hello 시간 간격이 경과 합니다.
    * hello 저장 된 액세스 정책은 수정 된 toohave hello 과거에 만료 시간입니다. 한 가지 방법은 toorevoke hello SAS는 hello 만료 시간을 변경 합니다.

3. hello 저장 하는 또 다른 방법은 toorevoke hello SAS SAS 삭제 되 면 hello에서 참조 하는 액세스 정책. 동일한 이름, 모든 SAS 토큰에 대 한 hello로 hello 저장 된 액세스 정책을 다시 만드는 경우 hello 이전 정책은 유효 (hello에 hello 만료 시간 SAS을 지나치지 않은) 합니다. Toorevoke hello SAS를 가져오려는 경우 수 있는지 toouse 다른 이름을 hello 액세스 정책 만료 시간이 hello 나중에 다시 만드는 경우.

4. 사용 하는 toocreate hello SAS hello 계정 키 다시 생성 됩니다. Hello 키 다시 생성 하면 이전 키 toofail 인증 hello를 사용 하는 모든 응용 프로그램. 모든 구성 요소 toohello 새 키를 업데이트 합니다.

> [!IMPORTANT]
> 공유 액세스 서명 URI hello 계정 키 사용 되는 toocreate hello 서명과 사용 하 여 연결 되며 hello (있는 경우) 저장 된 액세스 정책에 연결 합니다. 저장 된 액세스 정책이 없는 지정, hello만 방법은 toorevoke 공유 액세스 서명을 toochange hello 계정 키입니다.

항상 저장된 액세스 정책을 사용하는 것이 좋습니다. 저장 된 정책을 사용 하는 경우 서명을 취소 하거나 필요에 따라 hello 만료 날짜를 연장 수 있습니다. 이 문서의 단계 hello 저장 된 액세스 정책을 toogenerate SAS를 사용합니다.

공유 액세스 서명에 대 한 자세한 내용은 참조 하십시오. [hello SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md)합니다.

### <a name="create-a-stored-policy-and-sas-using-c"></a>C\#을 사용하여 저장된 정책 및 SAS 만들기

1. Visual Studio에서 hello 솔루션을 엽니다.

2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **SASToken** 프로젝트를 마우스 선택 **속성**합니다.

3. 선택 **설정** hello 항목 다음에 대 한 값 추가:

   * StorageConnectionString: hello 연결 문자열 toocreate 원하는 hello 저장소 계정에 대 한 저장 된 정책 및에 대 한 SAS입니다. hello 형식을 해야 `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` 여기서 `myaccount` hello 저장소 계정의 이름입니다 및 `mykey` hello 저장소 계정에 대 한 hello 키입니다.

   * 에 액세스 하려면 toorestrict hello 저장소 계정에서 ContainerName: hello 컨테이너입니다.

   * SASPolicyName: hello에 대 한 이름 toouse hello 정책 toocreate를 저장 합니다.

   * FileToUpload: hello 경로 tooa 파일 업로드 toohello 컨테이너입니다.

4. Hello 프로젝트를 실행 합니다. 다음 텍스트 정보 비슷한 toohello hello SAS 생성 되 면 표시 됩니다.

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Hello SAS 정책 토큰이, 저장소 계정 이름과 컨테이너 이름을 저장 합니다. 이러한 값은 hello 저장소 계정이 HDInsight 클러스터와 연결할 때 사용 됩니다.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Python을 사용하여 저장된 정책 및 SAS 만들기

1. Hello SASToken.py 파일을 열고 hello 다음 값을 변경 합니다.

   * 정책\_이름: hello에 대 한 이름 toouse hello 정책 toocreate 저장 합니다.

   * 저장소\_계정\_이름: hello 사용자의 저장소 계정 이름입니다.

   * 저장소\_계정\_키: hello hello 저장소 계정의 키입니다.

   * 저장소\_컨테이너\_이름: hello toorestrict에 대 한 액세스를 원하는 hello 저장소 계정의 컨테이너입니다.

   * 예제\_파일\_경로: hello tooa 파일 경로 업로드 된 toohello 컨테이너입니다.

2. Hello 스크립트를 실행 합니다. Hello SAS 토큰 비슷한 toohello를 hello 스크립트가 완료 되 면 텍스트를 다음으로 표시 됩니다.

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Hello SAS 정책 토큰이, 저장소 계정 이름과 컨테이너 이름을 저장 합니다. 이러한 값은 hello 저장소 계정이 HDInsight 클러스터와 연결할 때 사용 됩니다.

## <a name="use-hello-sas-with-hdinsight"></a>HDInsight와 hello SAS를 사용 하 여

HDInsight 클러스터를 만들 때 기본 저장소 계정을 지정해야 하며 필요에 따라 추가 저장소 계정을 지정할 수 있습니다. 저장소를 추가 하는 두이 방법 모두에 대 한 모든 권한 toohello 저장소 계정 및 사용 되는 컨테이너 필요 합니다.

공유 액세스 서명을 toolimit 액세스 tooa 컨테이너 toouse 추가 사용자 지정 항목 toohello **핵심 사이트** hello 클러스터에 구성 합니다.

* 에 대 한 **Windows 기반** 또는 **Linux 기반** HDInsight 클러스터, PowerShell을 사용 하 여 클러스터를 만드는 동안 hello 항목을 추가할 수 있습니다.
* 에 대 한 **Linux 기반** HDInsight 클러스터를 Ambari를 사용 하 여 클러스터를 만든 후 hello 구성을 변경 합니다.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Hello SAS를 사용 하는 클러스터 만들기

사용 하 여 hello SAS hello에 포함 된 HDInsight 클러스터를 만드는 예 `CreateCluster` hello 리포지토리의 디렉터리입니다. toouse 설명 해 다음 사용 하 여 hello:

1. 열기 hello `CreateCluster\HDInsightSAS.ps1` 텍스트 편집기에서 파일 및 hello 다음 hello 문서의 hello 시작 부분에 값을 수정 합니다.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    예를 들어 변경 `'mycluster'` toohello 이름 toocreate hello 클러스터의 원하는 합니다. 저장소 계정 및 SAS 토큰을 만들 때 hello SAS 값 hello 이전 단계에서 hello 값을 일치 해야 합니다.

    Hello 값을 변경 되 면 hello 파일을 저장 합니다.

2. 새 Azure PowerShell 프롬프트를 엽니다. Azure PowerShell에 익숙하지 않거나 설치되지 않은 경우 [Azure PowerShell 설치 및 구성][powershell]을 참조하세요.

1. Hello 프롬프트에서 명령을 tooauthenticate tooyour Azure 구독을 다음 hello를 사용 합니다.

    ```powershell
    Login-AzureRmAccount
    ```

    메시지가 표시 되 면 Azure 구독에 대 한 hello 계정으로 로그인 합니다.

    계정이 여러 Azure 구독과 연결 된 경우 toouse 할 수 있습니다 `Select-AzureRmSubscription` toouse 원하는 tooselect hello 구독 합니다.

4. Hello 프롬프트에서 디렉터리 toohello 변경 `CreateCluster` hello HDInsightSAS.ps1 파일이 포함 된 디렉터리입니다. 다음 명령 toorun hello 스크립트 다음 hello를 사용 하 여

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Hello 스크립트 실행 될 때를 기록 출력 toohello PowerShell 프롬프트를 hello 리소스 그룹 및 저장소 계정을 만듭니다. Hello HDInsight 클러스터에 대 한 증명된 tooenter hello HTTP 사용자 됩니다. 이 계정은 사용 되는 toosecure HTTP/s 액세스 toohello 클러스터입니다.

    Linux 기반 클러스터를 만드는 경우 SSH 사용자 계정 이름 및 암호를 묻는 메시지가 표시됩니다. 이 계정은 toohello 클러스터에 사용 되는 tooremotely 로그입니다.

   > [!IMPORTANT]
   > HTTP/s hello 또는 SSH 사용자 이름 및 암호에 대 한 메시지가 표시 되 면 hello 다음 조건을 충족 하는 암호를 제공 해야 합니다.
   >
   > * 길이가 10자 이상이어야 함
   > * 숫자를 1개 이상 포함해야 함
   > * 영숫자가 아닌 문자를 1개 이상 포함해야 함
   > * 대문자 또는 소문자를 1개 이상 포함해야 함

일반적으로 약 15 분이 스크립트 toocomplete 시간이 걸립니다. Hello 스크립트가 오류 없이 완료 되 면 hello 클러스터를 만들었습니다.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Hello SAS를 사용 하 여 기존 클러스터와

Linux 기반 기존 클러스터를 설정한 경우에 hello SAS toohello을 추가할 수 있습니다 **핵심 사이트** 단계를 수행 하는 hello를 사용 하 여 구성 합니다.

1. 클러스터에 대 한 hello Ambari web UI를 엽니다. 이 페이지에 대 한 hello 주소 https://YOURCLUSTERNAME.azurehdinsight.net 됩니다. 대화 상자가 나타나면 인증 hello 관리자 이름 (admin)를 사용 하 여 toohello 클러스터 고 hello 클러스터를 만드는 경우 사용 되는 암호입니다.

2. Hello hello Ambari web UI의 왼쪽에서 선택 **HDFS** 선택한 후 hello **Configs** hello 중간 hello 페이지의 탭 합니다.

3. 선택 hello **고급** 탭을 선택한 다음 hello를 찾을 때까지 스크롤 **사용자 지정 핵심 사이트** 섹션.

4. Hello 확장 **사용자 지정 핵심 사이트** 다음 스크롤 toohello 끝 섹션과 선택 hello **속성을 추가 중...**  링크 합니다. Hello에 대 한 값을 사용 하 여 hello 다음 **키** 및 **값** 필드:

   * **키**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **값**: hello 이전에 실행 하는 C#, Python 응용 프로그램에서 반환 된 SAS hello

     대체 **CONTAINERNAME** hello C# 또는 SAS 응용 프로그램과 함께 사용 hello 컨테이너 이름을 사용 합니다. 대체 **STORAGEACCOUNTNAME** hello 저장소 계정 이름을 사용 합니다.

5. Hello 클릭 **추가** toosave이 키 및 값을 단추 클릭 hello **저장** toosave hello에 대 한 구성 변경 내용을 단추입니다. 메시지가 표시 되 면 hello 변경 ("추가 SAS 저장소 액세스" 예를 들어)에 대 한 설명을 추가 하 고 클릭 **저장**합니다.

    클릭 **확인** hello 변경을 완료 한 경우.

   > [!IMPORTANT]
   > Hello 변경 내용이 적용 되기 전에 몇 가지 서비스를 다시 시작 해야 합니다.

6. Hello Ambari 웹 UI에서에서 선택 **HDFS** hello hello 왼쪽, 선택한 후 목록에서 **모든 다시 시작** hello에서 **서비스 작업** 드롭 다운 목록 hello 오른쪽에 있습니다. 메시지가 나타나면 **Turn on maintenance mode**을 선택한 다음 __Conform Restart All"을 선택합니다.

    MapReduce2 및 YARN에 대해 이 프로세스를 반복합니다.

7. Hello 서비스를 다시 시작한 후 각 하나를 선택 하 고 hello에서 유지 관리 모드를 사용 하지 않도록 설정 **서비스 작업** 드롭 다운 합니다.

## <a name="test-restricted-access"></a>제한된 액세스 테스트

액세스를 사용 하 여 hello 다음 메서드를 제한 한 tooverify:

* 에 대 한 **Windows 기반** HDInsight 클러스터를 원격 데스크톱 tooconnect toohello 클러스터를 사용 합니다. 자세한 내용은 참조 [tooHDInsight RDP를 사용 하 여 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.

    연결 되 면 hello를 사용 하 여 **명령줄 Hadoop** hello 데스크톱 tooopen 명령 프롬프트에서 아이콘입니다.

* 에 대 한 **Linux 기반** HDInsight 클러스터를 SSH tooconnect toohello 클러스터를 사용 합니다. 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

Toohello 클러스터 연결 되 면 다음 단계 tooverify hello SAS 저장소 계정에만 읽기 및 목록 항목을 할 수 있는 hello를 사용 합니다.

1. hello 컨테이너의 toolist hello 내용을 hello hello 프롬프트에서 다음 명령을 사용 합니다. 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    대체 **SASCONTAINER** hello SAS 저장소 계정에 대해 생성 하는 hello 컨테이너의 hello 이름의 합니다. 대체 **SASACCOUNTNAME** hello SAS에 사용 되는 hello 저장소 계정의 hello 이름의 합니다.

    hello 목록 hello 파일을 업로드 hello 컨테이너와 SAS를 만들 때 포함 됩니다.

2. 사용 하 여 hello 다음 명령은 tooverify hello 파일의 hello 내용을 읽을 수 있습니다. Hello 대체 **SASCONTAINER** 및 **SASACCOUNTNAME** hello 이전 단계에서 설명한 대로 합니다. 대체 **FILENAME** hello 이전 명령에 표시 된 hello 파일의 hello 이름의:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    이 명령은 hello 파일의 내용을 hello를 나열합니다.

3. 다음 명령 toodownload hello 파일 toohello 로컬 파일 시스템 hello를 사용 합니다.

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    이 명령은 다운로드 hello 라는 파일 tooa 로컬 파일 **testfile.txt**합니다.

4. 사용 하 여 hello 다음 명령은 tooupload hello 로컬 파일 tooa 라는 새 파일 **testupload.txt** hello SAS 저장소에:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    텍스트 다음 메시지와 비슷한 toohello를 나타납니다.

        put: java.io.IOException

    이 오류는 hello 저장소 위치는 읽기 + 목록만 때문에 발생 합니다. 에 나오는 명령 tooput hello 데이터에 따라 쓰기 가능한 hello 클러스터에 대 한 기본 저장소 hello hello를 사용 합니다.

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    이 시간 hello 작업이 성공적으로 완료 됩니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="a-task-was-canceled"></a>작업이 취소됨

**증상**: hello PowerShell 스크립트를 사용 하는 클러스터를 만들 때는 hello 다음과 같은 오류 메시지가 나타날 수 있습니다.

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**원인**: hello 관리자/HTTP 사용자 hello 클러스터에 대 한 또는 (Linux 기반 클러스터)에 대 한 암호를 사용 하는 경우이 오류가 발생할 수 hello SSH 사용자입니다.

**해결 방법**: hello 다음 조건을 충족 하는 암호를 사용 하 여:

* 길이가 10자 이상이어야 함
* 숫자를 1개 이상 포함해야 함
* 영숫자가 아닌 문자를 1개 이상 포함해야 함
* 대문자 또는 소문자를 1개 이상 포함해야 함

## <a name="next-steps"></a>다음 단계

배웠습니다 했으므로 tooadd 액세스가 제한 된 저장소 tooyour HDInsight 클러스터를 클러스터에 데이터와 다른 방법으로 toowork에 알아봅니다.

* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight와 함께 MapReduce 사용](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
