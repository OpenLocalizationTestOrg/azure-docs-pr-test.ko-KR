---
title: "Azure 파일 저장소 aaaHow toouse PowerShell toomanage | Microsoft Docs"
description: "Toouse PowerShell toomanage Azure 파일 저장소에 알아봅니다."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>어떻게 toouse PowerShell toomanage Azure 파일 저장소
Azure PowerShell toocreate를 사용 하 고 파일 공유를 관리할 수 있습니다.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Azure 저장소에 대 한 hello PowerShell cmdlet을 설치 합니다.
tooprepare toouse PowerShell 다운로드 하 여 hello Azure PowerShell cmdlet을 설치 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) hello에 대 한 지점 및 설치 지침을 설치 합니다.

> [!NOTE]
> 다운로드 및 설치 하거나 업그레이드 toohello 최신 Azure PowerShell 모듈 것이 좋습니다.
> 
> 

**시작**을 클릭하고 **Windows PowerShell**을 입력하여 Azure PowerShell 창을 엽니다. hello PowerShell 창을 hello Azure Powershell 모듈을 로드 합니다.

## <a name="create-a-context-for-your-storage-account-and-key"></a>저장소 계정 및 키에 대한 컨텍스트 만들기
Hello 저장소 계정 컨텍스트를 만듭니다. hello 컨텍스트 hello 저장소 계정 이름 및 계정 키를 캡슐화합니다. Hello에서 계정 키를 복사에 대 한 지침은 [Azure 포털](https://portal.azure.com), 참조 [저장소 액세스 키 보기 및 복사](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)합니다.

대체 `storage-account-name` 및 `storage-account-key` 저장소 계정 이름 및 키 hello 다음 예제에에서 사용 합니다.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>새 파일 공유 만들기
명명 된 hello 새 공유 만들기 `logs`합니다.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

이제 파일 저장소에 파일 공유가 있습니다. 다음에는 디렉터리와 파일을 추가할 것입니다.

> [!IMPORTANT]
> 파일 공유 hello 이름이 모두 소문자 여야 합니다. 파일 공유 및 파일 이름 지정에 대한 자세한 내용은 [공유, 디렉터리, 파일 및 메타데이터 이름 지정 및 참조](https://msdn.microsoft.com/library/azure/dn167011.aspx)를 참조하세요.
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Hello 파일 공유에서 디렉터리 만들기
Hello 공유의 디렉터리를 만듭니다. 다음 예제는 hello, hello 디렉터리 이름은 `CustomLogs`합니다.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>로컬 파일 toohello 디렉터리를 업로드 합니다.
이제 로컬 파일 toohello 디렉터리를 업로드 합니다. hello 다음 예제에서는 파일을 업로드에서 `C:\temp\Log1.txt`합니다. 로컬 컴퓨터에 유효한 파일이 tooa 가리키도록 hello 파일 경로 편집 합니다.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Hello 디렉터리에 hello 파일 나열
hello 디렉터리에 toosee hello 파일인 hello 디렉터리의 파일을 모두를 나열할 수 있습니다. 이 명령은 hello 파일 및 하위 디렉터리 (있는 경우)의 반환 hello CustomLogs 디렉터리입니다.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile은 디렉터리 개체가 전달되는 파일 및 디렉터리의 목록을 반환합니다. "Get AzureStorageFile-$s 공유" hello 루트 디렉터리에 파일 및 디렉터리의 목록을 반환 합니다. 하위 디렉터리에 파일 목록이 tooget toopass hello 하위 디렉터리 tooGet AzureStorageFile 해야합니다. 즉,이-hello toohello 파이프를 hello 명령의 첫 번째 부분은 hello 하위 디렉터리 CustomLogs의 디렉터리 인스턴스를 반환 합니다. 그런 다음 Get AzureStorageFile CustomLogs에 hello 파일 및 디렉터리를 반환 하는 전달 되는 합니다.

## <a name="copy-files"></a>파일 복사
Azure PowerShell 0.9.7 버전부터, 파일 tooanother 파일, 파일 tooa blob 또는 blob tooa 파일을 복사할 수 있습니다. 아래에 대해서도 설명 tooperform 이러한 복사 방법 PowerShell cmdlet을 사용 하 여 작업 합니다.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>다음 단계
Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.

* [FAQ](../storage-files-faq.md)
* [Windows에서 문제 해결](storage-troubleshoot-windows-file-connection-problems.md)      
* [Linux에서 문제 해결](storage-troubleshoot-linux-file-connection-problems.md)    