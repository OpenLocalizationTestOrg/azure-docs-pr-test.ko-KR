---
title: "AzCopy를 사용 하 여 Azure Blob 저장소에서 데이터 tooand aaaMove | Microsoft Docs"
description: "AzCopy를 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>AzCopy를 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동
AzCopy는 업로드, 다운로드, 및 Microsoft Azure blob, 파일 및 테이블 저장소에서 데이터 tooand 복사 하기 위한 명령줄 유틸리티입니다.

AzCopy 및 추가 정보를 Azure 플랫폼 hello 사용에 설치 하는 방법에 지침은 [hello AzCopy 명령줄 유틸리티 시작](../storage/common/storage-use-azcopy.md)합니다.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> 제공 된 hello 스크립트를 사용 하 여 설정 된 VM을 사용 하는 경우 [Azure의 데이터 과학 가상 컴퓨터](machine-learning-data-science-virtual-machines.md), 다음 AzCopy hello VM에 이미 설치 되어 있습니다.
> 
> [!NOTE]
> 전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 너무[Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 문서에서는 Azure 구독을 저장소 계정 있고 해당 계정에 대 한 저장소 키를 해당 hello를 가정 합니다. 데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.

* 한 Azure 구독을 tooset 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.
* 저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.

## <a name="run-azcopy-commands"></a>AzCopy 명령 실행
toorun는 AzCopy 명령, 명령 창을 열고 hello AzCopy.exe 실행 파일이 위치한 컴퓨터에 toohello AzCopy 설치 디렉터리를 이동 합니다. 

hello 기본는 AzCopy 명령 구문은 다음과 같습니다.

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> Hello AzCopy 설치 위치 tooyour 시스템 경로 추가 하 고 원하는 디렉터리에서 hello 명령을 실행 합니다. 기본적으로 AzCopy가 설치 되어 너무*%ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* 또는 *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*합니다.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>파일 tooan Azure blob 업로드
tooupload 파일에 다음 명령을 사용 하 여 hello:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Azure blob에서 파일 다운로드
다음 명령을 사용 하 여 hello Azure blob에서 파일 toodownload:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Azure 컨테이너 간 Blob 전송
Azure 컨테이너 간에 tootransfer blob hello 다음 명령을 사용 합니다.

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>AzCopy 사용에 대한 팁
> [!TIP]
> 1. 파일을 **업로드** 하는 경우 */S* 는 파일을 재귀적으로 업로드합니다. 이 매개 변수가 없으면 하위 디렉터리의 파일이 업로드되지 않습니다.  
> 2. 때 **다운로드** 파일인 */S* 검색 hello 지정 된 디렉터리 및 하위 디렉터리의 모든 파일 될 때까지 컨테이너 재귀적으로 hello 또는 일치 하는 모든 파일에 지정 된 hello에서 지정 된 패턴과 hello 디렉터리 및 하위 디렉터리에 다운로드 됩니다.  
> 3. 지정할 수 없습니다는 **특정 blob 파일** hello를 사용 하 여 toodownload */소스* 매개 변수입니다. 특정 파일을 toodownload hello blob 파일 이름 toodownload hello를 사용 하 여 지정 *패턴/* 매개 변수입니다. **/S** 매개 변수는 파일 이름 패턴 재귀적으로 사용 되는 toohave AzCopy 모양을 수 있습니다. Hello pattern 매개 변수 없이 AzCopy는 해당 디렉터리의 모든 파일을 다운로드합니다.
> 
> 

