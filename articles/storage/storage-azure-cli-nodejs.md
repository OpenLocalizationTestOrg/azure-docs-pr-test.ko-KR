---
title: "Azure 저장소와 Azure CLI 1.0 aaaUsing hello | Microsoft Docs"
description: "Toouse를 Azure CLI (명령줄 인터페이스 Azure) 1.0와 Azure 저장소 toocreate hello 및 저장소 계정 관리 및 Azure blob와 파일을 작동 방법에 대해 알아봅니다. hello Azure CLI는 플랫폼 간 도구"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>Hello Azure CLI 1.0을 사용 하 여 Azure 저장소

## <a name="overview"></a>개요

hello Azure CLI hello Azure 플랫폼을 다루기 위한 크로스 플랫폼 명령 집합이 한 오픈 소스를 제공 합니다. Hello hello에 있는 동일한 기능을 많이 제공 [Azure 포털](https://portal.azure.com) 도 같이 다양 한 데이터 기능에 액세스 합니다.

이 가이드에서는 살펴볼 것 어떻게 toouse [Azure CLI (명령줄 인터페이스 Azure)](../cli-install-nodejs.md) tooperform 다양 한 Azure 저장소와 개발 및 관리 작업입니다. 다운로드 및 설치 하거나 업그레이드 toohello 권장이 가이드를 사용 하기 전에 최신 Azure CLI 합니다.

이 가이드 hello Azure 저장소의 기본 개념을 이해 해야 하는 것으로 가정 합니다. hello 가이드의 hello Azure 저장소와 Azure CLI toodemonstrate hello 사용 스크립트의 수를 제공합니다. 있는지 tooupdate 각 스크립트를 실행 하기 전에 구성에 따라 hello 스크립트 변수 여야 합니다.

> [!NOTE]
> hello 가이드 클래식 저장소 계정에 대 한 hello Azure CLI 명령 및 스크립트 예제를 제공합니다. 참조 [Mac, Linux 및 Windows Azure 리소스 관리에 대 한 Azure CLI를 사용 하 여 hello](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) 리소스 관리자 저장소 계정에 대 한 Azure CLI 명령에 대 한 합니다.
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>5 분 이내에 Azure 저장소 및 Azure CLI hello 시작
이 가이드에서는 예제를 보려면 Ubuntu를 사용하며 다른 OS 플랫폼에서도 유사하게 수행되어야 합니다.

**새 tooAzure:** Microsoft Azure 구독 및 해당 구독과 연결 된 Microsoft 계정을 가져옵니다. Azure 구입 옵션에 대한 자세한 내용은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/), [구입 옵션](https://azure.microsoft.com/pricing/purchase-options/) 및 [회원 제안](https://azure.microsoft.com/pricing/member-offers/)(MSDN, Microsoft 파트너 네트워크, BizSpark 및 기타 Microsoft 프로그램의 회원인 경우)을 참조하세요.

Azure 구독에 대한 자세한 내용은 [Azure AD(Azure Active Directory)에서 관리자 역할 할당](https://msdn.microsoft.com/library/azure/hh531793.aspx) 을 참조하세요.

**Microsoft Azure 구독 및 계정을 만든 후:**

1. 다운로드 및 설치에 설명 된 지침을 진행 hello Azure CLI hello [설치 hello Azure CLI](../cli-install-nodejs.md)합니다.
2. Hello Azure CLI 설치가 완료 된 후 수 toouse 수 hello azure 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트) tooaccess hello Azure CLI 명령 명령입니다. 형식 hello _azure_ 명령을 hello 출력 뒤에 표시 됩니다.

    ![Azure 명령 출력][Image1]
3. Hello 명령줄 인터페이스에서 입력 `azure storage` toolist 모든 azure 저장소 명령을 hello 및 Azure CLI 제공 hello 기능 hello의 첫 번째 인상을 가져오기. 으로 명령 이름을 입력할 수 **-h** 매개 변수 (예를 들어 `azure storage share create -h`) 명령 구문의 toosee 세부 정보입니다.
4. 이제 기본 Azure CLI 명령을 tooaccess Azure 저장소를 보여 주는 간단한 스크립트를 하겠습니다. hello 스크립트 먼저 묻습니다 tooset 두 변수 저장소 계정 및 키에 대 한 합니다. 그런 다음 hello 스크립트는 새 컨테이너를이 새 저장소 계정에서 만들고 기존 이미지 파일 (blob) toothat 컨테이너를 업로드 합니다. 해당 컨테이너의 모든 blob를 나열 하는 hello 스크립트, 후 hello 이미지 파일 toohello 대상 디렉터리 hello 로컬 컴퓨터에 있는 다운로드 됩니다.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. 로컬 컴퓨터에서 원하는 텍스트 편집기(예: vim)를 엽니다. 위의 스크립트는 hello 텍스트 편집기에 입력 합니다.
6. 이제, 구성 설정에 기반 하 여 tooupdate hello 스크립트 변수 해야 합니다.

   * **< Storage_account_name >** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 저장소 계정에 대 한 새 이름을 입력 합니다. **중요:** hello hello 저장소 계정의 이름으로 Azure에서 고유 해야 합니다. 소문자여야 합니다.
   * **< storage_account_key >** hello 선택 키의 저장소 계정입니다.
   * **< Container_name >** hello 스크립트에 이름이 지정 된 hello를 사용 하거나 컨테이너에 대해 새 이름을 입력 합니다.
   * **< Image_to_upload >** 로컬 컴퓨터에 같은 경로 tooa 그림을 입력: "~ / images/HelloWorld.png"입니다.
   * **< Destination_folder >** Enter와 같은 Azure 저장소에서 다운로드 경로 tooa 로컬 디렉터리 toostore 파일: "~/downloadImages"입니다.
7. Hello vim에서 필요한 변수를 업데이트 한 후 키 조합을 눌러 `ESC`, `:`, `wq!` toosave hello 스크립트입니다.
8. toorun이이 스크립트를 단순히 hello 스크립트 파일의에서 형식 이름은 hello bash 콘솔. 이 스크립트를 실행 한 후 다운로드 한 hello 이미지 파일을 포함 하는 로컬 대상 폴더가 있어야 합니다. 다음 스크린 샷 hello 출력을 예를 보여 줍니다.

Hello 스크립트를 실행 한 후 다운로드 한 hello 이미지 파일을 포함 하는 로컬 대상 폴더가 있어야 합니다.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Hello Azure CLI가 있는 저장소 계정 관리
### <a name="connect-tooyour-azure-subscription"></a>Tooyour Azure 구독 연결
대부분의 hello 저장소 명령은, Azure 구독 없이 작동 하는 동안 Azure CLI hello에서 tooconnect tooyour 구독을 하는 것이 좋습니다. 구독에 tooconfigure hello Azure CLI toowork hello 단계에 따라 [hello Azure CLI에서에서 tooan Azure 구독 연결](../xplat-cli-connect.md)합니다.

### <a name="create-a-new-storage-account"></a>새 저장소 계정 만들기
Azure 저장소 toouse 저장소 계정이 필요 합니다. 컴퓨터 tooconnect tooyour 구독을 구성한 후 새 Azure 저장소 계정을 만들 수 있습니다.

```azurecli
azure storage account create <account_name>
```

저장소 계정의 hello 이름 길이가 3 ~ 24 자 사이 여야 하 고 숫자 및 소문자만 사용 해야 합니다.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>환경 변수에서 기본 Azure 저장소 계정 설정
구독에서 여러 저장소 계정을 사용할 수 있습니다. 그 중 하나를 선택할 수 있으며에 설정 hello 환경 변수 동일 hello에서 모든 hello 저장소 명령에 대 한 세션입니다. 이렇게 하면 toorun hello Azure CLI 저장소 hello 저장소를 지정 하지 않고 명령 계정 및 키를 명시적으로 있습니다.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

또 다른 방법은 tooset 기본 저장소 계정 연결 문자열을 사용 중입니다. 먼저 명령 여 hello 연결 문자열을 가져옵니다.

```azurecli
azure storage account connectionstring show <account_name>
```

다음 hello 출력 연결 문자열을 복사 하 고 tooenvironment 변수를 설정 합니다.

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Blob 만들기 및 관리
Azure Blob 저장소는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다. 이 섹션에서는 hello Azure Blob 저장소 개념에 익숙하다고 이미 한다고 가정 합니다. 자세한 내용은 [.NET을 사용하여 Azure Blob Storage 시작](storage-dotnet-how-to-use-blobs.md) 및 [Blob Service 개념](http://msdn.microsoft.com/library/azure/dd179376.aspx)을 참조하세요.

### <a name="create-a-container"></a>컨테이너 만들기
Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다. Hello를 사용 하 여 개인 컨테이너를 만들 수 있습니다 `azure storage container create` 명령:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> 익명 읽기 액세스의 세가지 수준은 **해제**, **Blob** 및 **컨테이너**입니다. 익명 tooprevent tooblobs, 집합 hello 권한 매개 변수를 너무 액세스**오프**합니다. 기본적으로 hello 새 컨테이너는 전용 포트 이며 hello 계정 소유자만 액세스할 수 있습니다. tooallow 익명 공용 읽기 tooblob 리소스에 액세스 하지만 toocontainer 메타 데이터 또는 toohello 목록이 아니라 hello 컨테이너의 blob, hello 권한 매개 변수를 너무 설정**Blob**합니다. tooallow 전체 공용 읽기 액세스 tooblob 리소스, 컨테이너 메타 데이터 및 hello hello 컨테이너의 blob 목록, hello 권한 매개 변수를 너무 설정**컨테이너**합니다. 자세한 내용은 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](storage-manage-access-to-resources.md)합니다.
>
>

### <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
Azure Blob 저장소는 블록 Blob 및 페이지 Blob을 지원합니다. 자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.

tooupload blob tooa 컨테이너에서 hello를 사용할 수 있습니다 `azure storage blob upload`합니다. 기본적으로이 명령은 hello 로컬 파일 tooa 블록 blob을 업로드합니다. toospecify hello 유형 hello blob hello를 사용할 수 있습니다 `--blobtype` 매개 변수입니다.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>컨테이너에서 Blob 다운로드
다음 예제는 hello toodownload 컨테이너에서 blob 하는 방법을 보여 줍니다.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Blob 복사
저장소 계정 및 지역 내 또는 전체에 걸쳐 비동기적으로 Blob을 복사할 수 있습니다.

hello 다음 예제에서는 하나의 저장소에서 blob toocopy tooanother를 고려 하는 방법 이 샘플에서는 blob을 공개적으로 하는 컨테이너 만들어 익명으로 액세스할 수 있습니다.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

이 예제에서는 비동기 복사를 수행합니다. Hello를 실행 하 여 각 복사 작업의 hello 상태를 모니터링할 수 있습니다 `azure storage blob copy show` 작업 합니다.

Note hello 복사 작업에 제공 된 hello 소스 URL 해야 공개적으로 액세스할 수 없거나 SAS (공유 액세스 서명) 토큰을 포함 합니다.

### <a name="delete-a-blob"></a>Blob 삭제
blob toodelete 명령 아래의 hello를 사용 합니다.

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>파일 공유 만들기 및 관리
Azure 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 응용 프로그램에 대 한 공유 저장소를 제공 합니다. Microsoft Azure 가상 컴퓨터 및 클라우드 서비스 그리고 온-프레미스 응용 프로그램은 탑재된 공유를 통해 파일 데이터를 공유할 수 있습니다. 파일 공유 및 파일 데이터 hello Azure CLI를 통해 관리할 수 있습니다. Azure 파일 저장소에 대 한 자세한 내용은 참조 하십시오. [Windows에서 Azure 파일 저장소 시작](storage-dotnet-how-to-use-files.md) 또는 [어떻게 toouse Azure 파일 저장소와 Linux](storage-how-to-use-files-linux.md)합니다.

### <a name="create-a-file-share"></a>파일 공유 만들기
Azure에서 Azure 파일 공유는 SMB 파일 공유입니다. 모든 디렉터리 및 파일을 파일 공유에서 만들어야 합니다. 계정에 공유를 개수에 제한 없이 포함 될 수 있습니다 및 공유 파일 toohello hello 저장소 계정의 용량 한도를 개수에 제한 없이 저장할 수 있습니다. hello 다음 예제에서는 라는 파일 공유 **myshare**합니다.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>디렉터리 만들기
디렉터리는 Azure 파일 공유에 대한 선택적 계층적 구조를 제공합니다. hello 다음 예에서는 라는 디렉터리를 만듭니다 **myDir** hello 파일 공유에 있습니다.

```azurecli
azure storage directory create myshare myDir
```

해당 디렉터리 경로에 여러 수준이 포함 될 수 있습니다( *예:***a/b**). 그러나 모든 부모 디렉터리가 존재하는지 확인해야 합니다. 예를 들어, 경로 **a/b**의 경우, 먼저 디렉터리 **a**를 만든 다음, **b** 디렉터리를 만듭니다.

### <a name="upload-a-local-file-toodirectory"></a>로컬 파일 toodirectory 업로드
hello 다음 예제에서는 파일을 업로드에서 **~/temp/samplefile.txt** toohello **myDir** 디렉터리입니다. 로컬 컴퓨터에 유효한 파일이 tooa 가리키도록 hello 파일 경로 편집 합니다.

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

크기가 too1 TB를 hello 공유에 있는 파일 수 수 있는지 확인 합니다.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Hello 공유 루트 디렉터리 또는 hello 파일 나열
Hello 파일 및 공유 루트 또는 hello 다음 명령을 사용 하 여 디렉터리에 하위 디렉터리를 나열할 수 있습니다.

```azurecli
azure storage file list myshare myDir
```

Note hello 디렉터리 이름은 해당 hello 나열 작업에 대 한 선택 사항입니다. 생략 하면 hello 명령은 hello 공유의 hello 루트 디렉터리의 hello 내용을 나열 합니다.

### <a name="copy-files"></a>파일 복사
버전 0.9.8 Azure cli 부터는 파일 tooanother 파일, 파일 tooa blob 또는 blob tooa 파일을 복사할 수 있습니다. 아래에 대해서도 설명 tooperform 이러한 복사 방법 CLI 명령을 사용 하 여 작업 합니다. toocopy toohello 있는 새 파일 디렉터리:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy blob tooa 파일 디렉터리:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>다음 단계

여기 있는 저장소 리소스와 함께 사용할 수 있는 Azure CLI 1.0 명령 참조를 찾을 수 있습니다.

* [Resource Manager 모드에서 Azure CLI 명령](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Azure 서비스 관리 모드의 Azure CLI 명령](../cli-install-nodejs.md)

Tootry hello 또한 수 원하는 [Azure CLI 2.0](storage-azure-cli.md), Python, hello 리소스 관리자 배포 모델에 사용 하기 위해 작성 된 차세대 CLI 취급 합니다.

[Image1]: ./media/storage-azure-cli/azure_command.png
