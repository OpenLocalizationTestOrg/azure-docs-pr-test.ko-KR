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
# <a name="create-a-file-share-in-azure-file-storage"></a><span data-ttu-id="f3116-103">Azure File Storage에 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="f3116-103">Create a File Share in Azure File storage</span></span>
<span data-ttu-id="f3116-104">사용 하 여 Azure 파일 공유를 만들 수 있습니다 [Azure 포털](https://portal.azure.com/)hello Azure 저장소 PowerShell cmdlet, Azure 저장소 클라이언트 라이브러리를 hello 또는 hello Azure 저장소 REST API입니다. 이 자습서에서는 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-104">You can create Azure File shares using [Azure portal](https://portal.azure.com/), hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>
* [<span data-ttu-id="f3116-105">Hello Azure 포털을 사용 하 여 toocreate Azure 파일을 공유 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f3116-105">How toocreate an Azure File share using hello Azure portal</span></span>](#Create file share through hello Portal)
* [<span data-ttu-id="f3116-106">어떻게 toocreate Azure 파일 공유 Powershell을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f3116-106">How toocreate an Azure File share using Powershell</span></span>](#Create file share using PowerShell)
* [<span data-ttu-id="f3116-107">어떻게 toocreate Azure 파일 공유 CLI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f3116-107">How toocreate an Azure File share using CLI</span></span>](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a><span data-ttu-id="f3116-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f3116-108">Prerequisites</span></span>
<span data-ttu-id="f3116-109">Azure 파일 공유 toocreate 이미 존재 하는 저장소 계정을 사용할 수 있습니다 또는 [새 Azure 저장소 계정 만들기](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-109">toocreate an Azure File share, you can use a storage account that already exists, or [create a new Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span> <span data-ttu-id="f3116-110">PowerShell 사용 하 여 Azure 파일 공유 toocreate hello 계정 키와 저장소 계정의 이름이 필요 합니다...</span><span class="sxs-lookup"><span data-stu-id="f3116-110">toocreate an Azure File share with PowerShell, you will need hello account key and name of your storage account..</span></span> <span data-ttu-id="f3116-111">저장소 계정 키 toouse Powershell 또는 CLI를 계획 하는 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-111">You will need Storage account key if you plan toouse Powershell or CLI.</span></span>

## <a name="create-file-share-through-hello-portal"></a><span data-ttu-id="f3116-112">Hello 포털을 통해 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="f3116-112">Create file share through hello Portal</span></span>
1. <span data-ttu-id="f3116-113">**Azure 포털에서 이동 tooStorage 계정 블레이드**:</span><span class="sxs-lookup"><span data-stu-id="f3116-113">**Go tooStorage Account blade on Azure Portal**:</span></span>    
    <span data-ttu-id="f3116-114">![저장소 계정 블레이드](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span><span class="sxs-lookup"><span data-stu-id="f3116-114">![Storage Account Blade](./media/storage-how-to-create-file-share/create-file-share-portal1.png)</span></span>

2. <span data-ttu-id="f3116-115">**파일 공유 추가 단추를 클릭합니다**.</span><span class="sxs-lookup"><span data-stu-id="f3116-115">**Click on add File Share button**:</span></span>    
    <span data-ttu-id="f3116-116">![Hello 클릭 하 여 파일 공유 단추를 추가 합니다.](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span><span class="sxs-lookup"><span data-stu-id="f3116-116">![Click hello add file share button](./media/storage-how-to-create-file-share/create-file-share-portal2.png)</span></span>

3. <span data-ttu-id="f3116-117">**이름과 할당량을 제공합니다. 할당량은 현재 최대 5TB일 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="f3116-117">**Provide Name and Quota. Quota currently can be maximum 5TB**:</span></span>    
    <span data-ttu-id="f3116-118">![Hello 새 파일 공유에 대 한 이름 및 원하는 할당량 지정](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span><span class="sxs-lookup"><span data-stu-id="f3116-118">![Provide a name and a desired quota for hello new file share](./media/storage-how-to-create-file-share/create-file-share-portal3.png)</span></span>

4. <span data-ttu-id="f3116-119">**새 파일 공유를 확인합니다**. ![새 파일 공유 보기](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span><span class="sxs-lookup"><span data-stu-id="f3116-119">**View your new file share**:  ![View your new file share](./media/storage-how-to-create-file-share/create-file-share-portal4.png)</span></span>

5. <span data-ttu-id="f3116-120">**파일을 업로드합니다**. ![파일 업로드](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span><span class="sxs-lookup"><span data-stu-id="f3116-120">**Upload a file**:  ![Upload a file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)</span></span>

6. <span data-ttu-id="f3116-121">**파일 공유를 찾아보고 디렉터리와 파일을 관리합니다**. ![파일 공유 찾아보기](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span><span class="sxs-lookup"><span data-stu-id="f3116-121">**Browse into your file share and manage your directories and files**:  ![Browse file share](./media/storage-how-to-create-file-share/create-file-share-portal6.png)</span></span>


## <a name="create-file-share-through-powershell"></a><span data-ttu-id="f3116-122">PowerShell 통해 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="f3116-122">Create file share through PowerShell</span></span>
<span data-ttu-id="f3116-123">tooprepare toouse PowerShell 다운로드 하 여 hello Azure PowerShell cmdlet을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-123">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f3116-124">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) hello에 대 한 지점 및 설치 지침을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-124">See [How tooinstall and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) for hello install point and installation instructions.</span></span>

> [!Note]  
> <span data-ttu-id="f3116-125">다운로드 및 설치 하거나 업그레이드 toohello 최신 Azure PowerShell 모듈 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-125">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>

1. <span data-ttu-id="f3116-126">**저장소 계정 및 키에 대 한 컨텍스트를 만들어** hello 컨텍스트 hello 저장소 계정 이름 및 계정 키를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-126">**Create a context for your storage account and key** hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="f3116-127">[Azure Portal](https://portal.azure.com/)에서 계정 키를 복사하는 방법에 대한 지침은 [저장소 액세스 키 보기 및 복사](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3116-127">For instructions on copying your account key from the [Azure portal](https://portal.azure.com/), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. <span data-ttu-id="f3116-128">**새 파일 공유를 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="f3116-128">**Create a new file share**:</span></span>    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> <span data-ttu-id="f3116-129">파일 공유 hello 이름이 모두 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-129">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="f3116-130">파일 공유 및 파일 이름 지정에 대한 자세한 내용은 [공유, 디렉터리, 파일 및 메타데이터 이름 지정 및 참조](https://msdn.microsoft.com/library/azure/dn167011.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3116-130">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>

## <a name="create-file-share-through-command-line-interface-cli"></a><span data-ttu-id="f3116-131">CLI(명령줄 인터페이스)를 통해 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="f3116-131">Create file share through Command Line Interface (CLI)</span></span>
1. <span data-ttu-id="f3116-132">**tooprepare toouse 명령줄 인터페이스 (CLI)를 다운로드 하 여 hello Azure CLI를 설치 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f3116-132">**tooprepare toouse a Command Line Interface (CLI), download and install hello Azure CLI.**</span></span>  
    <span data-ttu-id="f3116-133">[Azure CLI 2.0 설치](/cli/azure/install-az-cli2.md) 및 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3116-133">See [Install Azure CLI 2.0](/cli/azure/install-az-cli2.md) and [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span>

2. <span data-ttu-id="f3116-134">**Toocreate hello 공유 저장할 연결 문자열 toohello 저장소 계정을 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="f3116-134">**Create a connection string toohello storage account where you want toocreate hello share.**</span></span>  
    <span data-ttu-id="f3116-135">대체 ```<storage-account>``` 및 ```<resource_group>``` hello 다음 예제에서에서 저장소 계정 이름과 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-135">Replace ```<storage-account>``` and ```<resource_group>``` with your storage account name and resource group in hello following example.</span></span>

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. <span data-ttu-id="f3116-136">**파일 공유를 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="f3116-136">**Create file share**</span></span>
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a><span data-ttu-id="f3116-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f3116-137">Next steps</span></span>
* [<span data-ttu-id="f3116-138">파일 공유 연결 및 탑재 - Windows</span><span class="sxs-lookup"><span data-stu-id="f3116-138">Connect and Mount File Share - Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="f3116-139">파일 공유 연결 및 탑재 - Linux</span><span class="sxs-lookup"><span data-stu-id="f3116-139">Connect and Mount File Share - Linux</span></span>](../storage-how-to-use-files-linux.md)
* [<span data-ttu-id="f3116-140">파일 공유 연결 및 탑재 - macOS</span><span class="sxs-lookup"><span data-stu-id="f3116-140">Connect and Mount File Share - macOS</span></span>](storage-how-to-use-files-mac.md)

<span data-ttu-id="f3116-141">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f3116-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="f3116-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="f3116-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="f3116-143">Windows에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f3116-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="f3116-144">Linux에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f3116-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   