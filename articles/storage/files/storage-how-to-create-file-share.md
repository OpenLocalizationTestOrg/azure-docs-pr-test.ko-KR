---
title: "aaaHow toocreate Azure 파일 공유 | Microsoft Docs"
description: "Toocreate Azure 파일의에서 공유 어떻게 hello Azure 포털, PowerShell 및 Azure CLI hello를 사용 하 여 Azure 파일 저장소."
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
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Azure File Storage에 파일 공유 만들기
사용 하 여 Azure 파일 공유를 만들 수 있습니다 [Azure 포털](https://portal.azure.com/)hello Azure 저장소 PowerShell cmdlet, Azure 저장소 클라이언트 라이브러리를 hello 또는 hello Azure 저장소 REST API입니다. 이 자습서에서는 배웁니다.
* [Hello Azure 포털을 사용 하 여 toocreate Azure 파일을 공유 하는 방법](#Create file share through hello Portal)
* [어떻게 toocreate Azure 파일 공유 Powershell을 사용 하 여](#Create file share using PowerShell)
* [어떻게 toocreate Azure 파일 공유 CLI를 사용 하 여](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>필수 조건
Azure 파일 공유 toocreate 이미 존재 하는 저장소 계정을 사용할 수 있습니다 또는 [새 Azure 저장소 계정 만들기](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)합니다. PowerShell 사용 하 여 Azure 파일 공유 toocreate hello 계정 키와 저장소 계정의 이름이 필요 합니다... 저장소 계정 키 toouse Powershell 또는 CLI를 계획 하는 경우 필요 합니다.

## <a name="create-file-share-through-hello-portal"></a>Hello 포털을 통해 파일 공유 만들기
1. **Azure 포털에서 이동 tooStorage 계정 블레이드**:    
    ![저장소 계정 블레이드](./media/storage-how-to-create-file-share/create-file-share-portal1.png)

2. **파일 공유 추가 단추를 클릭합니다**.    
    ![Hello 클릭 하 여 파일 공유 단추를 추가 합니다.](./media/storage-how-to-create-file-share/create-file-share-portal2.png)

3. **이름과 할당량을 제공합니다. 할당량은 현재 최대 5TB일 수 있습니다**.    
    ![Hello 새 파일 공유에 대 한 이름 및 원하는 할당량 지정](./media/storage-how-to-create-file-share/create-file-share-portal3.png)

4. **새 파일 공유를 확인합니다**. ![새 파일 공유 보기](./media/storage-how-to-create-file-share/create-file-share-portal4.png)

5. **파일을 업로드합니다**. ![파일 업로드](./media/storage-how-to-create-file-share/create-file-share-portal5.png)

6. **파일 공유를 찾아보고 디렉터리와 파일을 관리합니다**. ![파일 공유 찾아보기](./media/storage-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>PowerShell 통해 파일 공유 만들기
tooprepare toouse PowerShell 다운로드 하 여 hello Azure PowerShell cmdlet을 설치 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) hello에 대 한 지점 및 설치 지침을 설치 합니다.

> [!Note]  
> 다운로드 및 설치 하거나 업그레이드 toohello 최신 Azure PowerShell 모듈 것이 좋습니다.

1. **저장소 계정 및 키에 대 한 컨텍스트를 만들어** hello 컨텍스트 hello 저장소 계정 이름 및 계정 키를 캡슐화 합니다. [Azure Portal](https://portal.azure.com/)에서 계정 키를 복사하는 방법에 대한 지침은 [저장소 액세스 키 보기 및 복사](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)를 참조하세요.

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **새 파일 공유를 만듭니다**.    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> 파일 공유 hello 이름이 모두 소문자 여야 합니다. 파일 공유 및 파일 이름 지정에 대한 자세한 내용은 [공유, 디렉터리, 파일 및 메타데이터 이름 지정 및 참조](https://msdn.microsoft.com/library/azure/dn167011.aspx)를 참조하세요.

## <a name="create-file-share-through-command-line-interface-cli"></a>CLI(명령줄 인터페이스)를 통해 파일 공유 만들기
1. **tooprepare toouse 명령줄 인터페이스 (CLI)를 다운로드 하 여 hello Azure CLI를 설치 합니다.**  
    [Azure CLI 2.0 설치](/cli/azure/install-az-cli2.md) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md)을 참조하세요.

2. **Toocreate hello 공유 저장할 연결 문자열 toohello 저장소 계정을 만듭니다.**  
    대체 ```<storage-account>``` 및 ```<resource_group>``` hello 다음 예제에서에서 저장소 계정 이름과 리소스 그룹을 사용 합니다.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **파일 공유를 만듭니다.**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>다음 단계
* [파일 공유 연결 및 탑재 - Windows](storage-how-to-use-files-windows.md)
* [파일 공유 연결 및 탑재 - Linux](../storage-how-to-use-files-linux.md)
* [파일 공유 연결 및 탑재 - macOS](storage-how-to-use-files-mac.md)

Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.

* [FAQ](../storage-files-faq.md)
* [Windows에서 문제 해결](storage-troubleshoot-windows-file-connection-problems.md)      
* [Linux에서 문제 해결](storage-troubleshoot-linux-file-connection-problems.md)   