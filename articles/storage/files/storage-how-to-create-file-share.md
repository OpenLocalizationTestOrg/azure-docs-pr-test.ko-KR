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
ms.openlocfilehash: b81701e2544ace092f007e5d98b3141e1f7da724
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="7cd47-103">Azure File Storage에 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="7cd47-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="7cd47-104">[Azure Portal](https://portal.azure.com/), Azure Storage PowerShell cmdlet, Azure Storage 클라이언트 라이브러리 또는 Azure Storage REST API를 사용하여 Azure 파일 공유를 만들 수 있습니다. 이 자습서에서는 다음 항목에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="7cd47-105">Azure Portal을 사용하여 Azure 파일 공유를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="7cd47-105">How to create an Azure File share using the Azure portal</span></span>](#Create file share through the Portal)
* [<span data-ttu-id="7cd47-106">Powershell을 사용하여 Azure 파일 공유를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="7cd47-106">How to create an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="7cd47-107">CLI를 사용하여 Azure 파일 공유를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="7cd47-107">How to create an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="7cd47-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7cd47-108">Prerequisites</span></span>
<span data-ttu-id="7cd47-109">Azure 파일 공유를 만들려면 이미 존재하는 저장소 계정을 사용하거나 [새 Azure 저장소 계정을 만들 수 있습니다](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7cd47-109">To create an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="7cd47-110">PowerShell을 사용하여 Azure 파일 공유를 만들려면 저장소 계정의 계정 키와 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-110">To create an Azure File share with PowerShell, you will need the account key and name of your storage account..</span></span> <span data-ttu-id="7cd47-111">Powershell 또는 CLI를 사용하려면 저장소 계정 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-111">You will need Storage account key if you plan to use Powershell or CLI.</span></span>

## <a name="create-file-share-through-the-portal"></a><span data-ttu-id="7cd47-112">포털을 통해 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="7cd47-112">Create file share through the Portal</span></span>
1. <span data-ttu-id="7cd47-113">**Azure Portal에서 저장소 계정 블레이드로 이동합니다**.</span><span class="sxs-lookup"><span data-stu-id="7cd47-113">**Go to Storage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="7cd47-114">![저장소 계정 블레이드](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="7cd47-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="7cd47-115">**파일 공유 추가 단추를 클릭합니다**.</span><span class="sxs-lookup"><span data-stu-id="7cd47-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="7cd47-116">![파일 공유 추가 단추 클릭](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="7cd47-116">![Click the add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="7cd47-117">**이름과 할당량을 제공합니다. 할당량은 현재 최대 5TB일 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="7cd47-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="7cd47-118">![새 파일 공유에 대한 이름과 원하는 할당량 제공](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="7cd47-118">![Provide a name and a desired quota for the new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="7cd47-119">**새 파일 공유를 확인합니다**. ![새 파일 공유 보기](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="7cd47-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="7cd47-120">**파일을 업로드합니다**. ![파일 업로드](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="7cd47-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="7cd47-121">**파일 공유를 찾아보고 디렉터리와 파일을 관리합니다**. ![파일 공유 찾아보기](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="7cd47-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="7cd47-122">PowerShell 통해 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="7cd47-122">Create file share through PowerShell</span></span>
<span data-ttu-id="7cd47-123">PowerShell 사용을 준비하려면 Azure PowerShell cmdlet을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-123">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="7cd47-124">설치 지점 및 설치 지침에 대해서는 [Azure PowerShell 설치 및 구성 방법](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cd47-124">See [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for the install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="7cd47-125">최신 Azure PowerShell 모듈을 다운로드하여 설치하거나 최신 모듈로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-125">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="7cd47-126">**저장소 계정 및 키에 대한 컨텍스트를 만듭니다**. 컨텍스트는 저장소 계정 이름과 계정 키를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-126">**Create a context for your storage account and key** The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="7cd47-127">[Azure Portal](https://portal.azure.com/)에서 계정 키를 복사하는 방법에 대한 지침은 [저장소 액세스 키 보기 및 복사](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cd47-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="7cd47-128">**새 파일 공유를 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="7cd47-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="7cd47-129">파일 공유의 이름은 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-129">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="7cd47-130">파일 공유 및 파일 이름 지정에 대한 자세한 내용은 [공유, 디렉터리, 파일 및 메타데이터 이름 지정 및 참조](https://msdn.microsoft.com/library/azure/dn167011.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cd47-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="7cd47-131">CLI(명령줄 인터페이스)를 통해 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="7cd47-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="7cd47-132">**명령줄 인터페이스(CLI)를 사용하도록 준비하려면 Azure CLI를 다운로드하여 설치합니다.**</span><span class="sxs-lookup"><span data-stu-id="7cd47-132">**To prepare to use a Command Line Interface (CLI), download and install the Azure CLI.**</span></span>  
    <span data-ttu-id="7cd47-133">[Azure CLI 2.0 설치](/cli/azure/install-az-cli2.md) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cd47-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="7cd47-134">**공유를 만들 저장소 계정에 연결 문자열을 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="7cd47-134">**Create a connection string to the storage account where you want to create the share.**</span></span>  
    <span data-ttu-id="7cd47-135">다음 예제에서는 ```<storage-account>``` 및 ```<resource_group>```을 사용자의 저장소 계정 이름 및 리소스 그룹으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in the following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve the connection string."
    fi
    ```

3. <span data-ttu-id="7cd47-136">**파일 공유를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="7cd47-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="7cd47-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7cd47-137">Next steps</span></span>
* [<span data-ttu-id="7cd47-138">파일 공유 연결 및 탑재 - Windows</span><span class="sxs-lookup"><span data-stu-id="7cd47-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="7cd47-139">파일 공유 연결 및 탑재 - Linux</span><span class="sxs-lookup"><span data-stu-id="7cd47-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="7cd47-140">파일 공유 연결 및 탑재 - macOS</span><span class="sxs-lookup"><span data-stu-id="7cd47-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="7cd47-141">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7cd47-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="7cd47-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="7cd47-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="7cd47-143">Windows에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7cd47-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="7cd47-144">Linux에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7cd47-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   