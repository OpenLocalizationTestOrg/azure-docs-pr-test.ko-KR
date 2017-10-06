---
title: "Azure 저장소 탐색기와 Blob 저장소에서 데이터 tooand aaaMove | Microsoft Docs"
description: "Azure 저장소 탐색기를 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Azure 저장소 탐색기를 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동
Azure 저장소 탐색기는 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 toowork 수 있는 Microsoft의 무료 도구입니다. 이 항목에서는 설명 어떻게 toouse 것 tooupload 및 다운로드 데이터를 Azure blob 저장소입니다. hello 도구에서 다운로드할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> 제공 된 hello 스크립트를 사용 하 여 설정 된 VM을 사용 하는 경우 [Azure의 데이터 과학 가상 컴퓨터](machine-learning-data-science-virtual-machines.md), 다음 Azure 저장소 탐색기 hello VM에 이미 설치 되어 있습니다.
> 
> [!NOTE]
> 전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 [Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.   
> 
> 

## <a name="prerequisites"></a>필수 조건
이 문서는 Azure 구독, 저장소 계정 및 해당 계정에 대 한 해당 저장소 키 hello 있다고 가정 합니다. 데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다. 

* 한 Azure 구독을 tooset 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.
* 저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요. 이 키 tooconnect toohello 계정 hello Azure 저장소 탐색기 도구 필요에 따라 저장소 계정에 대 한 참고 hello 액세스 키를 확인 합니다.
* hello Azure 저장소 탐색기 도구를 다운로드할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다. 설치 하는 동안 hello 기본값을 적용 합니다.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Azure 저장소 탐색기 사용
단계 문서 방법을 따르는 hello Azure 저장소 탐색기를 사용 하 여 데이터 tooupload/다운로드 합니다. 

1. Microsoft Azure Storage 탐색기를 시작합니다.
2. hello toobring **tooyour 계정에 로그인...**  선택 마법사 **Azure 계정 설정** 아이콘을 다음 **계정 추가** 자격 증명을 입력 합니다. ![Azure Storage 계정 추가](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. hello toobring **tooAzure 저장소 연결** 마법사, 선택 hello **tooAzure 저장소 연결** 아이콘입니다. ![TooAzure 저장소에 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Hello에 Azure 저장소 계정에서 hello 액세스 키를 입력 **tooAzure 저장소 연결** 마법사 차례로 **다음**합니다. ![TooAzure 저장소에 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Hello에 저장소 계정 이름 입력 **계정 이름** 상자 선택한 후 **다음**합니다. ![외부 저장소 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. 이제 hello 저장소 계정 추가 나열 합니다. 저장소 계정에서 blob 컨테이너 toocreate hello를 마우스 오른쪽 단추로 클릭 **Blob 컨테이너** 에서 해당 계정에 선택 노드 **Create Blob Container**, 이름을 입력 합니다.
7. tooupload 데이터 tooa 컨테이너, 선택 hello 대상 컨테이너와 클릭 hello **업로드** 단추.![ 저장소 계정](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Hello 클릭 **...**  hello의 오른쪽 toohello **파일** 상자 hello 파일 시스템에서 하나 또는 여러 개의 파일 tooupload를 선택 하 고 클릭 **업로드** toobegin hello 파일을 업로드 합니다.![ 파일 업로드](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. hello를 선택 하면 toodownload 데이터 hello 해당 컨테이너 toodownload의 blob 및 클릭 **다운로드**합니다. ![파일 다운로드](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

