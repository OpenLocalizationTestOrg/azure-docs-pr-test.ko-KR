---
title: "Windows에서 aaaMount Azure 파일 공유 및 액세스 hello 공유 | Microsoft Docs"
description: "Azure 파일 공유와 windows에서 hello 공유 액세스를 탑재 합니다."
services: storage
documentationcenter: na
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
ms.openlocfilehash: eb6d58ad391adb6c06703ad694150534ccf44ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Azure 파일 공유 및 액세스 hello 공유 창에 탑재
[Azure 파일 저장소](../storage-dotnet-how-to-use-files.md) 는 Microsoft의 쉬운 toouse 클라우드 파일 시스템입니다. Azure 파일 공유는 Windows 및 Windows Server에 탑재할 수 있습니다. 이 문서에서는 세 가지 방법으로 toomount Azure 파일 공유에서 Windows: PowerShell을 통해 및 hello 명령 프롬프트를 통해 파일 탐색기 UI hello로 합니다. 

Azure 파일 공유 hello 외부, 같은 온-프레미스 또는 다른 Azure 지역에 호스팅되는 Azure 지역 순서 toomount에서 OS hello SMB 3.0을 지원 해야 합니다. 

Azure 파일 공유는 OS 버전에 따라 온-프레미스 또는 Azure VM의 Windows 컴퓨터에 탑재할 수 있습니다. 아래 표에서 hello를 보여 줍니다. 

| Windows 버전        | SMB 버전 |Azure VM에 탑재 가능|온-프레미스에 탑재 가능|
|------------------------|-------------|---------------------|---------------------|
| 윈도우 7              | SMB 2.1     | 예                 | 아니요                  |
| Windows Server 2008 R2 | SMB 2.1     | 예                 | 아니요                  |
| Windows 8              | SMB 3.0     | 예                 | 예                 |
| Windows Server 2012    | SMB 3.0     | 예                 | 예                 |
| Windows Server 2012 R2 | SMB 3.0     | 예                 | 예                 |
| Windows 10             | SMB 3.0     | 예                 | 예                 |

> [!Note]  
> 항상 기록 권장 사용자의 Windows 버전에 대 한 가장 최근의 KB hello 합니다.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Windows에 Azure 파일 공유를 탑재하기 위한 필수 구성 요소 
* **저장소 계정 이름**: toomount Azure 파일 공유, hello 저장소 계정의 이름을 hello 필요 합니다.

* **저장소 계정 키**: toomount Azure 파일 공유, 기본 (또는 보조) 저장소 키 hello 필요 합니다. SAS 키는 현재 탑재를 지원하지 않습니다.

* **445 포트가 열려 있는지 확인**: Azure File Storage는 SMB 프로토콜을 사용합니다. Toosee 방화벽이 클라이언트 컴퓨터에서 TCP 포트 445를 차단 하지 않는지 선택 SMB TCP 포트 445-를 통해 통신 합니다.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>파일 탐색기로 hello Azure 파일 공유를 탑재 합니다.
> [!Note]  
> 지침에 따라 hello는 Windows 10에서 표시 되 고 이전 버전에서 약간 다를 수 있습니다. 

1. **파일 탐색기를 열고**: hello 시작 메뉴에서에서 열어 또는 Win + E 바로 가기 키를 눌러이 수행할 수 있습니다.

2. **Hello 창의 hello 왼쪽에 toohello "이 PC" 항목을 이동 합니다. 이렇게 하면 hello 리본 메뉴에서 사용할 수 있는 hello 메뉴 변경 됩니다. Hello 컴퓨터 메뉴에서 "네트워크 드라이브 맵"를 선택**합니다.
    
    ![Hello "네트워크 드라이브 맵" 드롭다운 메뉴의 스크린 샷](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Hello hello Azure 포털의에서 hello "연결" 창에서 UNC 경로 복사**: 자세한 설명은 어떻게 toofind이 내용은 [여기](storage-how-to-use-files-portal.md#connect-to-file-share)합니다.

    ![hello Azure 파일 저장소 연결 창에서 hello UNC 경로](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. **Hello 드라이브 문자를 선택 하 고 hello UNC 경로 입력 합니다.** 
    
    ![Hello "네트워크 드라이브 맵" 대화 상자 스크린 샷](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. **앞에 추가 하는 저장소 계정 이름을 사용 하 여 hello `Azure\` hello 사용자 이름 및 암호 hello와 저장소 계정 키입니다.**
    
    ![Hello 네트워크 자격 증명 대화 상자의 스크린 샷](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Azure 파일 공유를 원하는 대로 사용합니다**.
    
    ![현재 탑재된 Azure 파일 공유](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. **준비 toodismount (하거나 때 연결 끊기) hello Azure 파일 공유를 하면 파일 탐색기에서 "네트워크 위치" hello 아래 hello 공유에 대 한 hello 항목을 마우스 오른쪽 단추로 클릭 하 고 "연결 끊기"를 선택 하 여**합니다.

## <a name="mount-hello-azure-file-share-with-powershell"></a>PowerShell과 함께 hello Azure 파일 공유를 탑재 합니다.
1. **사용 하 여 hello 다음 명령은 toomount hello Azure 파일 공유**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello 적절 한 정보입니다.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **필요에 따라 사용 하 여 hello Azure 파일 공유**합니다.

3. **작업을 완료 하는 경우 다음 명령을 hello를 사용 하 여 hello Azure 파일 공유를 분리**합니다.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Hello를 사용할 수 있습니다 `-Persist` 매개 변수와 `New-PSDrive` toomake hello Azure 파일 공유 표시 toohello 나머지 hello 탑재 하는 동안 운영 체제.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>명령 프롬프트와 hello Azure 파일 공유를 탑재 합니다.
1. **사용 하 여 hello 다음 명령은 toomount hello Azure 파일 공유**: tooreplace 기억 `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` hello 적절 한 정보입니다.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **필요에 따라 사용 하 여 hello Azure 파일 공유**합니다.

3. **작업을 완료 하는 경우 다음 명령을 hello를 사용 하 여 hello Azure 파일 공유를 분리**합니다.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Windows에서 hello 자격 증명을 유지 하 여을 다시 시작할 때 hello Azure 파일 공유 tooautomatically 다시 연결을 구성할 수 있습니다. 다음 명령을 hello hello 자격 증명을 유지 됩니다.
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>다음 단계
Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.

* [FAQ](../storage-files-faq.md)
* [Windows에서 문제 해결](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a>개념 문서 및 비디오
* [Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [어떻게 toouse Linux로 Azure 파일 저장소](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Azure File Storage용 도구 지원
* [어떻게 toouse AzCopy Microsoft Azure 저장소](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Hello Azure CLI를 사용 하 여 Azure 저장소](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Azure File Storage 문제 해결 - Windows](storage-troubleshoot-windows-file-connection-problems.md)
* [Azure File Storage 문제 해결 - Linux](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>블로그 게시물
* [Azure 파일 저장소 일반적으로 사용 가능(영문)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure File Storage 내부 구조(영문)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 파일 서비스 소개](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [마이그레이션 데이터 tooAzure 파일](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>참조
* [Storage Client Library for .NET 참조](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [파일 서비스 REST API 참조](http://msdn.microsoft.com/library/azure/dn167006.aspx)
