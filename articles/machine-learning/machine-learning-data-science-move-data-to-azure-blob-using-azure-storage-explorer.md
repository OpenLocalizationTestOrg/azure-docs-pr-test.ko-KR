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
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a><span data-ttu-id="2ec25-103">Azure 저장소 탐색기를 사용 하 여 Azure Blob 저장소에서 데이터 tooand 이동</span><span class="sxs-lookup"><span data-stu-id="2ec25-103">Move data tooand from Azure Blob Storage using Azure Storage Explorer</span></span>
<span data-ttu-id="2ec25-104">Azure 저장소 탐색기는 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 toowork 수 있는 Microsoft의 무료 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-104">Azure Storage Explorer is a free tool from Microsoft that allows you toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="2ec25-105">이 항목에서는 설명 어떻게 toouse 것 tooupload 및 다운로드 데이터를 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-105">This topic describes how toouse it tooupload and download data from Azure blob storage.</span></span> <span data-ttu-id="2ec25-106">hello 도구에서 다운로드할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-106">hello tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="2ec25-107">제공 된 hello 스크립트를 사용 하 여 설정 된 VM을 사용 하는 경우 [Azure의 데이터 과학 가상 컴퓨터](machine-learning-data-science-virtual-machines.md), 다음 Azure 저장소 탐색기 hello VM에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-107">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then Azure Storage Explorer is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="2ec25-108">전체 소개 tooAzure blob 저장소에 대 한 참조 너무[Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 [Azure Blob 서비스](https://msdn.microsoft.com/library/azure/dd179376.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-108">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>   
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2ec25-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2ec25-109">Prerequisites</span></span>
<span data-ttu-id="2ec25-110">이 문서는 Azure 구독, 저장소 계정 및 해당 계정에 대 한 해당 저장소 키 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-110">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="2ec25-111">데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-111">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span> 

* <span data-ttu-id="2ec25-112">한 Azure 구독을 tooset 참조 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-112">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2ec25-113">저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ec25-113">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="2ec25-114">이 키 tooconnect toohello 계정 hello Azure 저장소 탐색기 도구 필요에 따라 저장소 계정에 대 한 참고 hello 액세스 키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-114">Make a note hello access key for your storage account as you need this key tooconnect toohello account with hello Azure Storage Explorer tool.</span></span>
* <span data-ttu-id="2ec25-115">hello Azure 저장소 탐색기 도구를 다운로드할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-115">hello Azure Storage Explorer tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="2ec25-116">설치 하는 동안 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-116">Accept hello defaults during install.</span></span>

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a><span data-ttu-id="2ec25-117">Azure 저장소 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="2ec25-117">Use Azure Storage Explorer</span></span>
<span data-ttu-id="2ec25-118">단계 문서 방법을 따르는 hello Azure 저장소 탐색기를 사용 하 여 데이터 tooupload/다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-118">hello following steps document how tooupload/download data using Azure Storage Explorer.</span></span> 

1. <span data-ttu-id="2ec25-119">Microsoft Azure Storage 탐색기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-119">Launch Microsoft Azure Storage Explorer.</span></span>
2. <span data-ttu-id="2ec25-120">hello toobring **tooyour 계정에 로그인...**  선택 마법사 **Azure 계정 설정** 아이콘을 다음 **계정 추가** 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-120">toobring up hello **Sign in tooyour account...** wizard, select **Azure account settings** icon, then **Add an account** and enter you credentials.</span></span> <span data-ttu-id="2ec25-121">![Azure Storage 계정 추가](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span><span class="sxs-lookup"><span data-stu-id="2ec25-121">![Add an Azure storage account](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span></span>
3. <span data-ttu-id="2ec25-122">hello toobring **tooAzure 저장소 연결** 마법사, 선택 hello **tooAzure 저장소 연결** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-122">toobring up hello **Connect tooAzure Storage** wizard, select hello **Connect tooAzure storage** icon.</span></span> <span data-ttu-id="2ec25-123">![TooAzure 저장소에 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span><span class="sxs-lookup"><span data-stu-id="2ec25-123">![Connect tooAzure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span></span>
4. <span data-ttu-id="2ec25-124">Hello에 Azure 저장소 계정에서 hello 액세스 키를 입력 **tooAzure 저장소 연결** 마법사 차례로 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-124">Enter hello access key from your Azure storage account on hello **Connect tooAzure Storage** wizard and then **Next**.</span></span> <span data-ttu-id="2ec25-125">![TooAzure 저장소에 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span><span class="sxs-lookup"><span data-stu-id="2ec25-125">![Connect tooAzure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span></span>
5. <span data-ttu-id="2ec25-126">Hello에 저장소 계정 이름 입력 **계정 이름** 상자 선택한 후 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-126">Enter storage account name in hello **Account name** box and then select **Next**.</span></span> <span data-ttu-id="2ec25-127">![외부 저장소 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span><span class="sxs-lookup"><span data-stu-id="2ec25-127">![Attach external storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span></span>
6. <span data-ttu-id="2ec25-128">이제 hello 저장소 계정 추가 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-128">hello storage account added should now be listed.</span></span> <span data-ttu-id="2ec25-129">저장소 계정에서 blob 컨테이너 toocreate hello를 마우스 오른쪽 단추로 클릭 **Blob 컨테이너** 에서 해당 계정에 선택 노드 **Create Blob Container**, 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-129">toocreate a blob container in a storage account, right-click hello **Blob Containers** node in that account, select **Create Blob Container**, and enter a name.</span></span>
7. <span data-ttu-id="2ec25-130">tooupload 데이터 tooa 컨테이너, 선택 hello 대상 컨테이너와 클릭 hello **업로드** 단추.![ 저장소 계정](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="2ec25-130">tooupload data tooa container, select hello target container and click hello **Upload** button.![Storage accounts](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span></span>
8. <span data-ttu-id="2ec25-131">Hello 클릭 **...**  hello의 오른쪽 toohello **파일** 상자 hello 파일 시스템에서 하나 또는 여러 개의 파일 tooupload를 선택 하 고 클릭 **업로드** toobegin hello 파일을 업로드 합니다.![ 파일 업로드](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="2ec25-131">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span></span>
9. <span data-ttu-id="2ec25-132">hello를 선택 하면 toodownload 데이터 hello 해당 컨테이너 toodownload의 blob 및 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec25-132">toodownload data, selecting hello blob in hello corresponding container toodownload and click **Download**.</span></span> <span data-ttu-id="2ec25-133">![파일 다운로드](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span><span class="sxs-lookup"><span data-stu-id="2ec25-133">![Download files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span></span>

