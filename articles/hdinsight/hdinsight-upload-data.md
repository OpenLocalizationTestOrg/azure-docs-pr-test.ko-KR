---
title: "HDInsight에서 Hadoop 작업에 대 한 데이터 aaaUpload | Microsoft Docs"
description: "사용 하 여 HDInsight에서 Hadoop 작업에 대 한 데이터에 액세스 하 tooupload Azure CLI, Azure 저장소 탐색기, Azure PowerShell, hello Hadoop 명령줄 또는 Sqoop hello 하는 방법에 대해 알아봅니다."
keywords: "etl hadoop, hadoop으로 데이터 가져오기, hadoop 데이터 로드"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>HDInsight에서 Hadoop 작업용 데이터 업로드
Azure HDInsight는 Azure Blob 저장소를 통해 모든 기능을 갖춘 HDFS(Hadoop Distributed File System)를 제공합니다. 기능은로 원활 하 게 HDFS 확장 tooprovide toocustomers 발생 합니다. 관리 하는 hello 데이터에서 직접 hello Hadoop 생태계 toooperate의 구성 요소 중 일부만을 hello 수 있습니다. Azure Blob 저장소와 HDFS는 데이터의 저장소 및 해당 데이터의 계산을 최적화하는 별개의 파일 시스템입니다. Azure Blob 저장소를 사용 하 여 hello 이점에 대 한 정보를 참조 하십시오. [HDInsight 사용 하 여 Azure Blob 저장소][hdinsight-storage]합니다.

**필수 구성 요소**

시작 하기 전에 요구 사항을 다음 참고 hello:

* Azure HDInsight 클러스터를 만듭니다. 자세한 내용은 [Azure HDInsight 시작][hdinsight-get-started] 또는 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요.

## <a name="why-blob-storage"></a>Blob 저장소
Azure HDInsight 클러스터는 일반적으로 toorun MapReduce 작업을 배포 하 고 hello 클러스터는 이러한 작업이 완료 된 후 삭제 됩니다. 계산이 완료 되 면 hello HDFS 클러스터에서 hello 데이터를 유지 하면이 데이터의 비용으로 toostore 것입니다. Azure Blob 저장소는 고가용성, 확장성, 높은 용량, 데이터 toobe HDInsight를 사용 하 여 처리에 대 한 저렴 한 비용, 및 공유할 수 있는 저장소 옵션에는 합니다. Blob에 데이터를 저장할 데이터의 손실 없이 안전 하 게 해제 계산 toobe에 사용 되는 HDInsight 클러스터를 hello 수 있습니다.

### <a name="directories"></a>디렉터리
Azure Blob 저장소 컨테이너는 키/값 쌍으로 데이터를 저장하며, 디렉터리 계층 구조는 없습니다. 그러나 hello "/" 문자는 것으로 표시 된 파일이 디렉터리 구조에 저장 됩니다 처럼 hello 키 이름 toomake 내에서 사용할 수 있습니다. HDInsight는 실제 디렉토리처럼 볼 수 있습니다.

예를 들어 Blob의 키 이름을 *input/log1.txt*로 지정할 수 있습니다. 실제 없음 "입력된" 디렉터리가 있는 인해 hello의 toohello 존재 하지만 "/" 문자 파일 경로의 hello 모양에 hello 키 이름입니다.

이 때문에, Azure 탐색기 도구를 사용하면 몇몇 0바이트 파일을 발견할 수 있습니다. 이러한 파일의 목적은 두 가지입니다.

* 빈 폴더에 있는 경우 hello 폴더의 hello 표시 합니다. Azure Blob 저장소는 라는 폴더 이므로 foo/표시줄 이라는 blob이 있는 경우 효과적인 충분히 tooknow **foo**합니다. 빈 폴더를 호출 하는 유일한 방법은 toosignify hello 하지만 **foo** 하는 위치에이 특별 한 0 바이트 파일을 것입니다.
* 특별 한 메타 데이터를 필요한 여 hello Hadoop 파일 시스템, 특히 hello 권한과 hello 폴더에 대 한 소유자 포함 됩니다.

## <a name="command-line-utilities"></a>명령줄 유틸리티
Microsoft은 Azure Blob 저장소와 유틸리티 toowork 다음 hello를 제공 합니다.

| 도구 | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Azure 명령줄 인터페이스][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Hadoop 명령](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Hello Azure CLI, Azure PowerShell 및 AzCopy 모두 일 수 동안 외부 Azure hello Hadoop 명령 hello HDInsight 클러스터에서 제공 되 고 허용 hello 로컬 파일 시스템에서 데이터를 Azure Blob 저장소로 로드에서 사용할 수 있습니다.
>
>

### <a id="xplatcli"></a>Azure CLI
hello Azure CLI toomanage Azure 수 있는 플랫폼 간 도구는 서비스입니다. 다음 단계 tooupload 데이터 tooAzure Blob 저장소 hello를 사용 합니다.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [설치 하 고 Mac, Linux 및 Windows hello Azure CLI 구성](../cli-install-nodejs.md)합니다.
2. 명령 프롬프트, bash, 또는 다른 셸을 열고 tooauthenticate tooyour Azure 구독에 따라 hello를 사용 합니다.

        azure login

    메시지가 표시 되 면 구독에 대 한 hello 사용자 이름 및 암호를 입력 합니다.
3. Hello 명령 toolist hello 저장소 계정을 구독에 대해 다음을 입력 합니다.

        azure storage account list
4. Toowork, 원하는 hello blob이 포함 된 hello 저장소 계정을 선택 후 다음이 계정에 대 한 명령 tooretrieve hello 키 hello를 사용 합니다.

        azure storage account keys list <storage-account-name>

    **기본** 및 **보조** 키가 반환되어야 합니다. 복사 hello **기본** hello 다음 단계에서 사용 되므로 키 값입니다.
5. 다음 명령 tooretrieve hello 저장소 계정 내에서 blob 컨테이너 목록이 hello를 사용 합니다.

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Toohello blob 파일을 다운로드 및 명령을 tooupload 다음 hello 사용:

   * tooupload 파일:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload 파일:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> 수행 하는 경우 하면 항상 hello와 동일한 저장소 계정 hello 계정을 지정 하는 대신 환경 변수를 다음 hello를 모든 명령에 대 한 키:
>
> * **AZURE\_저장소\_계정**: hello 저장소 계정 이름
> * **AZURE\_저장소\_액세스\_키**: hello 저장소 계정 키
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell은 toocontrol를 사용 하 고 Azure에서 작업의 hello 배포 및 관리를 자동화할 수 있는 스크립팅 환경입니다. 사용자 워크스테이션 toorun Azure PowerShell을 구성 하는 방법에 대 한 정보를 참조 하십시오. [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload 로컬 파일 tooAzure Blob 저장소**

1. 에 설명 된 대로 Azure PowerShell 콘솔을 열고 hello [설치 Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
2. 다음 스크립트는 hello에 hello hello 값 처음 다섯 개의 변수를 설정 합니다.

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. 붙여넣기 hello 스크립팅해야 hello Azure PowerShell 콘솔 toorun에 toocopy hello 파일입니다.

예를 들어 HDInsight와 PowerShell 생성 된 스크립트 toowork 참조 [HDInsight 도구](https://github.com/blackmist/hdinsight-tools)합니다.

### <a id="azcopy"></a>AzCopy
AzCopy는 명령줄 도구를 설계 toosimplify hello 작업 내부 / 외부로 Azure 저장소 계정 데이터를 전송 합니다. 이 유틸리티는 독립 실행형 도구로 사용할 수도 있고 기존 응용 프로그램에 통합할 수도 있습니다. [AzCopy를 다운로드][azure-azcopy-download]하세요.

다음은 hello AzCopy 구문입니다.

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

자세한 내용은 [AzCopy - Azure Blob용 파일 업로드/다운로드][azure-azcopy]를 참조하세요.

### <a id="commandline"></a>Hadoop 명령줄
hello Hadoop 명령줄 hello 데이터 hello 클러스터 헤드 노드에 이미 있는 경우 blob 저장소로 데이터를 저장 하는 데만 유용 합니다.

순서 toouse hello Hadoop 명령, 먼저 toohello 헤드 노드에 hello 메서드를 다음 중 하나를 사용 하 여 연결 해야 합니다.

* **Windows 기반 HDInsight**: [원격 데스크톱을 사용하여 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **Linux 기반 HDInsight**: SSH를 사용 하 여 연결 ([SSH 명령 hello](hdinsight-hadoop-linux-use-ssh-unix.md) 또는 [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

연결 되 면 다음 구문 tooupload 파일 toostorage hello를 사용할 수 있습니다.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

예를 들어 `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Azure Blob 저장소에 HDInsight에 대 한 기본 파일 시스템 hello 이므로 /example/data.txt Azure Blob 저장소에 실제로 합니다. 또한 toohello 파일을 참조할 수 있습니다.

    wasb:///example/data/data.txt

또는

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

파일과 함께 작동하는 다른 Hadoop 명령의 목록은 [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> HBase 클러스터 hello 기본 블록 크기는 256KB 데이터를 쓰는 경우 사용 합니다. Hello를 사용 하 여이 기능이 제대로 작동 HBase Api 또는 REST Api를 사용 하는 경우, 동안 `hadoop` 또는 `hdfs dfs` ~ 12 GB 보다 큰 toowrite 데이터 명령을 실행 하면 오류가 발생 합니다. Hello 참조 [blob에 쓰기를 위해 저장소 예외](#storageexception) 자세한 내용은 아래 섹션.
>
>

## <a name="graphical-clients"></a>그래픽 클라이언트
Azure 저장소를 사용하기 위한 그래픽 인터페이스를 제공하는 몇몇 응용 프로그램이 있습니다. hello 다음은 몇 가지 이러한 응용 프로그램의 목록입니다.

| 클라이언트 | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [HDInsight 용 Microsoft Visual Studio Tools](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure 저장소 탐색기](http://storageexplorer.com/) |✔ |✔ |✔ |
| [클라우드 저장소 스튜디오 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure 탐색기](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>HDInsight 용 Visual Studio Tools
자세한 내용은 참조 [연결 된 리소스 탐색 hello](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources)합니다.

### <a id="storageexplorer"></a>Azure 저장소 탐색기
*Azure 저장소 탐색기* 검사 하 고 blob의 hello 데이터 변경에 대 한 유용한 도구입니다. [http://storageexplorer.com/](http://storageexplorer.com/)에서 다운로드할 수 있는 무료 오픈 소스 도구입니다. hello 소스 코드가 다음이 링크에서 제공 됩니다.

Hello 도구를 사용 하기 전에 Azure 저장소 계정 이름 및 계정 키를 알고 있어야 합니다. 이 정보에 대 한 자세한 내용은 hello "방법: 보기, 복사 및 다시 생성 저장소 액세스 키" 섹션의 [만들기, 관리 또는 저장소 계정을 삭제][azure-create-storage-account]합니다.

1. Azure 저장소 탐색기를 실행합니다. 이 hello 처음으로 hello 저장소 탐색기를 실행 한 면 hello에 대 한 나타납니다 **(_s) 계정 이름** 및 **저장소 계정 키**합니다. Hello를 사용 하 여 이전을 실행 한 경우 **추가** tooadd 새 저장소 계정 이름 및 키 단추입니다.

    이름 및 HDInsight 클러스터에서 사용 하는 hello 저장소 계정에 대 한 키 및 선택 hello 입력 **저장 및 열기**합니다.

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. Hello 인터페이스의 컨테이너 toohello 왼쪽의 hello 목록에서 HDInsight 클러스터와 연결 된 hello 컨테이너의 hello 이름을 클릭 합니다. 기본적으로이 hello 이름 hello HDInsight 클러스터의 이지만 hello 클러스터를 만들 때 특정 이름을 입력 한 경우 달라질 수 있습니다.
3. Hello 도구 모음에서 hello 업로드 아이콘을 선택 합니다.

    ![업로드 아이콘이 강조 표시된 도구 모음](./media/hdinsight-upload-data/toolbar.png)
4. 파일 tooupload 지정 하 고 클릭 **열려**합니다. 메시지가 나타나면 선택 **업로드** hello 저장소 컨테이너의 tooupload hello 파일 toohello 루트입니다. Tooupload hello 파일 tooa 특정 경로 사용할 경우 경로 입력 hello hello **대상** 필드를 클릭 한 **업로드**합니다.

    ![파일 업로드 대화 상자](./media/hdinsight-upload-data/fileupload.png)

    Hello 파일 업로드 완료 되 면 hello HDInsight 클러스터에 대 한 작업에서 사용할 수 있습니다.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Azure Blob 저장소를 로컬 드라이브로 탑재
[Azure Blob 저장소를 로컬 드라이브로 탑재](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx)를 참조하세요.

## <a name="services"></a>서비스
### <a name="azure-data-factory"></a>Azure 데이터 팩터리
hello Azure 데이터 팩터리 서비스는 간소화 하 고 확장 가능한 신뢰할 수 있는 데이터 프로덕션 파이프라인에 데이터 저장소, 데이터 처리 및 데이터 이동 서비스를 작성 하기 위한 완전히 관리 되는 서비스입니다.

Azure 데이터 팩터리에 Azure Blob 저장소로 사용 되는 toomove 데이터 또는 수 toocreate 데이터 파이프라인 직접 등 HDInsight 기능을 사용 하는 Hive 및 Pig.

자세한 내용은 참조 hello [Azure Data Factory 설명서](https://azure.microsoft.com/documentation/services/data-factory/)합니다.

### <a id="sqoop"></a>Apache Sqoop
Sqoop은 Hadoop 및 관계형 데이터베이스 간에 설계 된 도구 tootransfer 데이터입니다. 사용할 수 있습니다 (RDBMS) 관계형 데이터베이스 관리 시스템에서 tooimport 데이터와 같은 SQL Server, MySQL 또는 hello distributed Hadoop 파일 시스템 (HDFS)에 Oracle에서 Hadoop MapReduce 또는 하이브를 hello 데이터 변환한 다음에 다시 hello 데이터를 내보낼는 RDBMS 합니다.

자세한 내용은 [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]을 참조하세요.

## <a name="development-sdks"></a>개발 SDK
Azure Blob 저장소에서 프로그래밍 언어를 다음 hello Azure SDK를 사용 하 여 액세스할 수 있습니다.

* .NET
* Java
* Node.js
* PHP
* Python
* 루비

Hello Azure Sdk를 설치 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 다운로드](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>문제 해결
### <a id="storageexception"></a>Blob에서 쓰기를 위한 저장소 예외
**증상**: hello를 사용 하는 경우 `hadoop` 또는 `hdfs dfs` toowrite 파일을 주석은 ~ 12 GB에서 HBase 클러스터를 더 큰 또는 hello 다음 오류가 발생할 수 있습니다.

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**원인**: tooAzure 저장소를 작성할 때 HDInsight에서 HBase 클러스터 256kb 기본 tooa 블록 크기입니다. Hello를 사용 하는 경우 오류가 발생 합니다 HBase Api 또는 REST Api에 대 한이 작동 하는 동안 `hadoop` 또는 `hdfs dfs` 명령줄 유틸리티입니다.

**해상도**: 사용 `fs.azure.write.request.size` toospecify 더 큰 블록 크기입니다. Hello를 사용 하 여 기본 사용 별로 이렇게 하려면 `-D` 매개 변수입니다. hello 다음은이 매개 변수를 사용 하 여 hello로 `hadoop` 명령:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

Hello 값을 늘릴 수 있습니다 `fs.azure.write.request.size` Ambari를 사용 하 여 전역적으로 합니다. hello 다음 단계 수 hello Ambari 웹 UI에서에서 toochange hello 값을 사용 합니다.

1. 브라우저에서 클러스터에 대해 toohello Ambari 웹 UI를 이동 합니다. 이 https://CLUSTERNAME.azurehdinsight.net, 여기서 **CLUSTERNAME** hello 클러스터 이름입니다.

    메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 이름 및 암호를 입력 합니다.
2. Hello hello 화면의 왼쪽에서 선택 **HDFS**를 선택한 후 hello **Configs** 탭 합니다.
3. Hello에 **필터...**  필드에, 입력 `fs.azure.write.request.size`합니다. 이 hello 필드 및 현재 값 hello 페이지의 hello 가운데에 표시 됩니다.
4. 262144 (256KB) toohello 새 값에서 hello 값을 변경 합니다. 예를 들면, 4194304(4MB)입니다.

![Ambari 웹 UI를 통해 hello 값 변경의 이미지](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Ambari를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [hello Ambari 웹 UI를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)합니다.

## <a name="next-steps"></a>다음 단계
이해 했으므로 tooget 데이터 HDInsight 읽는 방법 어떻게 문서 toolearn 다음 hello tooperform 분석:

* [Azure HDInsight 시작][hdinsight-get-started]
* [프로그래밍 방식으로 Hadoop 작업 제출][hdinsight-submit-jobs]
* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
