---
title: "Azure Storage 탐색기를 사용하여 Blob Storage의 데이터 이동 | Microsoft Docs"
description: "Azure 저장소 탐색기를 사용하여 Azure Blob 저장소의 데이터 이동"
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
ms.openlocfilehash: 0943bfcf51a1196e3e4ae7b2145708aa26d52190
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azure-storage-explorer"></a><span data-ttu-id="63e52-103">Azure Storage 탐색기를 사용하여 Azure Blob Storage 간에 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="63e52-103">Move data to and from Azure Blob Storage using Azure Storage Explorer</span></span>
<span data-ttu-id="63e52-104">Azure Storage 탐색기는 Windows, macOS 및 Linux에서 Azure Storage 데이터 작업 시에 사용할 수 있는 Microsoft의 무료 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-104">Azure Storage Explorer is a free tool from Microsoft that allows you to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="63e52-105">이 항목에서는 Azure Storage Explorer를 사용하여 Azure Blob 저장소에서 데이터를 업로드 및 다운로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-105">This topic describes how to use it to upload and download data from Azure blob storage.</span></span> <span data-ttu-id="63e52-106">이 도구는 [Microsoft Azure Storage 탐색기](http://storageexplorer.com/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-106">The tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="63e52-107">[Azure의 데이터 과학 가상 컴퓨터](machine-learning-data-science-virtual-machines.md)에서 제공하는 스크립트를 통해 설정된 VM을 사용하는 경우 Azure 저장소 탐색기가 VM에 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-107">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then Azure Storage Explorer is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="63e52-108">Azure Blob Storage에 대한 전체 소개 내용은 [Azure Blob 기본 사항](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 및 [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63e52-108">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>   
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="63e52-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="63e52-109">Prerequisites</span></span>
<span data-ttu-id="63e52-110">이 문서에서는 사용자에게 Azure 구독, 저장소 계정 및 계정에 해당하는 저장소 키가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-110">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="63e52-111">데이터를 업로드/다운로드하려면 Azure 저장소 계정 이름 및 계정 키를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-111">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span> 

* <span data-ttu-id="63e52-112">Azure 구독을 설정하려면 [1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63e52-112">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="63e52-113">저장소 계정을 만들고 계정 및 키 정보를 가져오는 방법에 대한 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63e52-113">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="63e52-114">저장소 계정의 선택키를 적어 두세요. Azure 저장소 탐색기 도구를 사용하여 계정에 연결하려면 이 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-114">Make a note the access key for your storage account as you need this key to connect to the account with the Azure Storage Explorer tool.</span></span>
* <span data-ttu-id="63e52-115">Azure Storage 탐색기 도구는 [Microsoft Azure Storage 탐색기](http://storageexplorer.com/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-115">The Azure Storage Explorer tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="63e52-116">설치 중에 표시되는 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-116">Accept the defaults during install.</span></span>

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a><span data-ttu-id="63e52-117">Azure 저장소 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="63e52-117">Use Azure Storage Explorer</span></span>
<span data-ttu-id="63e52-118">다음 단계에서는 Azure 저장소 탐색기를 사용하여 데이터를 업로드/다운로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-118">The following steps document how to upload/download data using Azure Storage Explorer.</span></span> 

1. <span data-ttu-id="63e52-119">Microsoft Azure Storage 탐색기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-119">Launch Microsoft Azure Storage Explorer.</span></span>
2. <span data-ttu-id="63e52-120">**계정에 로그인...** 마법사를 실행하려면 **Azure 계정 설정** 아이콘을 선택하고 **계정 추가**를 선택한 후에 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-120">To bring up the **Sign in to your account...** wizard, select **Azure account settings** icon, then **Add an account** and enter you credentials.</span></span> <span data-ttu-id="63e52-121">![Azure Storage 계정 추가](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span><span class="sxs-lookup"><span data-stu-id="63e52-121">![Add an Azure storage account](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span></span>
3. <span data-ttu-id="63e52-122">**Azure Storage에 연결** 마법사를 실행하려면 **Azure Storage에 연결** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-122">To bring up the **Connect to Azure Storage** wizard, select the **Connect to Azure storage** icon.</span></span> <span data-ttu-id="63e52-123">![Azure Storage에 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span><span class="sxs-lookup"><span data-stu-id="63e52-123">![Connect to Azure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span></span>
4. <span data-ttu-id="63e52-124">**Azure Storage에 연결** 마법사에서 Azure Storage 계정의 선택키를 입력한 후에 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-124">Enter the access key from your Azure storage account on the **Connect to Azure Storage** wizard and then **Next**.</span></span> <span data-ttu-id="63e52-125">![Azure Storage에 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span><span class="sxs-lookup"><span data-stu-id="63e52-125">![Connect to Azure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span></span>
5. <span data-ttu-id="63e52-126">**계정 이름** 상자에 저장소 계정 이름을 입력한 후에 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-126">Enter storage account name in the **Account name** box and then select **Next**.</span></span> <span data-ttu-id="63e52-127">![외부 저장소 연결](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span><span class="sxs-lookup"><span data-stu-id="63e52-127">![Attach external storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span></span>
6. <span data-ttu-id="63e52-128">그러면 추가한 저장소 계정이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-128">The storage account added should now be listed.</span></span> <span data-ttu-id="63e52-129">저장소 계정에서 Blob 컨테이너를 만들려면 해당 계정의 **Blob 컨테이너** 노드를 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 선택한 후에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-129">To create a blob container in a storage account, right-click the **Blob Containers** node in that account, select **Create Blob Container**, and enter a name.</span></span>
7. <span data-ttu-id="63e52-130">컨테이너에 데이터를 업로드하려면 대상 컨테이너를 선택하고 **업로드** 단추를 클릭합니다.![저장소 계정](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="63e52-130">To upload data to a container, select the target container and click the **Upload** button.![Storage accounts](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span></span>
8. <span data-ttu-id="63e52-131">**파일** 상자 오른쪽의 **...**를 클릭하고 파일 시스템에서 업로드할 파일을 하나 이상 선택한 후에 **업로드**를 클릭하여 파일 업로드를 시작합니다.![파일 업로드](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="63e52-131">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span></span>
9. <span data-ttu-id="63e52-132">데이터를 다운로드하려면 해당 컨테이너에서 다운로드하려는 Blob를 선택한 후에 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63e52-132">To download data, selecting the blob in the corresponding container to download and click **Download**.</span></span> <span data-ttu-id="63e52-133">![파일 다운로드](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span><span class="sxs-lookup"><span data-stu-id="63e52-133">![Download files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span></span>

