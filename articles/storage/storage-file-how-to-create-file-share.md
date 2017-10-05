---
title: "Azure 파일 공유를 만드는 방법 | Microsoft Docs"
description: "Azure Portal, PowerShell 및 Azure CLI를 사용하여 Azure File Storage에 Azure 파일 공유를 만드는 방법입니다."
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
ms.openlocfilehash: 10da4d903eaab290a6cca2c4f674548a43a70c53
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Azure File Storage에 파일 공유 만들기
[Azure Portal](https://portal.azure.com/), Azure Storage PowerShell cmdlet, Azure Storage 클라이언트 라이브러리 또는 Azure Storage REST API를 사용하여 Azure 파일 공유를 만들 수 있습니다. 이 자습서에서는 다음 항목에 대해 알아봅니다.
* [Azure Portal을 사용하여 Azure 파일 공유를 만드는 방법](#Create file share through the Portal)
* [Powershell을 사용하여 Azure 파일 공유를 만드는 방법](#Create file share using PowerShell)
* [CLI를 사용하여 Azure 파일 공유를 만드는 방법](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>필수 조건
Azure 파일 공유를 만들려면 이미 존재하는 저장소 계정을 사용하거나 [새 Azure 저장소 계정을 만들 수 있습니다](storage-create-storage-account.md). PowerShell을 사용하여 Azure 파일 공유를 만들려면 저장소 계정의 계정 키와 이름이 필요합니다. Powershell 또는 CLI를 사용하려면 저장소 계정 키가 필요합니다.

## <a name="create-file-share-through-the-portal"></a>포털을 통해 파일 공유 만들기
1. **Azure Portal에서 저장소 계정 블레이드로 이동합니다**.    
    ![저장소 계정 블레이드](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **파일 공유 추가 단추를 클릭합니다**.    
    ![파일 공유 추가 단추 클릭](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **이름과 할당량을 제공합니다. 할당량은 현재 최대 5TB일 수 있습니다**.    
    ![새 파일 공유에 대한 이름과 원하는 할당량 제공](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **새 파일 공유를 확인합니다**. ![새 파일 공유 보기](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **파일을 업로드합니다**. ![파일 업로드](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **파일 공유를 찾아보고 디렉터리와 파일을 관리합니다**. ![파일 공유 찾아보기](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>PowerShell 통해 파일 공유 만들기
PowerShell 사용을 준비하려면 Azure PowerShell cmdlet을 다운로드하여 설치합니다. 설치 지점 및 설치 지침에 대해서는 [Azure PowerShell 설치 및 구성 방법](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 을 참조하세요.

> [!Note]  
> 최신 Azure PowerShell 모듈을 다운로드하여 설치하거나 최신 모듈로 업그레이드하는 것이 좋습니다.

1. **저장소 계정 및 키에 대한 컨텍스트를 만듭니다**. 컨텍스트는 저장소 계정 이름과 계정 키를 캡슐화합니다. [Azure Portal](https://portal.azure.com/)에서 계정 키를 복사하는 방법에 대한 지침은 [저장소 액세스 키 보기 및 복사](storage-create-storage-account.md#view-and-copy-storage-access-keys)를 참조하세요.

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **새 파일 공유를 만듭니다**.    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> 파일 공유의 이름은 모두 소문자여야 합니다. 파일 공유 및 파일 이름 지정에 대한 자세한 내용은 [공유, 디렉터리, 파일 및 메타데이터 이름 지정 및 참조](https://msdn.microsoft.com/library/azure/dn167011.aspx)를 참조하세요.

## <a name="create-file-share-through-command-line-interface-cli"></a>CLI(명령줄 인터페이스)를 통해 파일 공유 만들기
1. **명령줄 인터페이스(CLI)를 사용하도록 준비하려면 Azure CLI를 다운로드하여 설치합니다.**  
    [Azure CLI 2.0 설치](/cli/azure/install-az-cli2.md) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md)을 참조하세요.

2. **공유를 만들 저장소 계정에 연결 문자열을 만듭니다.**  
    다음 예제에서는 ```<storage-account>``` 및 ```<resource_group>```을 사용자의 저장소 계정 이름 및 리소스 그룹으로 바꿉니다.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. **파일 공유를 만듭니다.**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>다음 단계
* [파일 공유 연결 및 탑재 - Windows](storage-file-how-to-use-files-windows.md)
* [파일 공유 연결 및 탑재 - Linux](storage-how-to-use-files-linux.md)
* [파일 공유 연결 및 탑재 - macOS](storage-file-how-to-use-files-mac.md)

Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.

* [FAQ](storage-files-faq.md)
* [문제 해결](storage-troubleshoot-file-connection-problems.md)