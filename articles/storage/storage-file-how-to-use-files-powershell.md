---
title: "PowerShell을 사용하여 Azure File storage를 관리하는 방법 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure File Storage를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 148375b156c4ae1aa4bf203d215f7ed607a71b89
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="ddd5a-103">PowerShell을 사용하여 Azure File storage를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ddd5a-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="ddd5a-104">Azure PowerShell을 사용하여 파일 공유를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="ddd5a-105">Azure 저장소에 대한 PowerShell cmdlet 설치</span><span class="sxs-lookup"><span data-stu-id="ddd5a-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="ddd5a-106">PowerShell 사용을 준비하려면 Azure PowerShell cmdlet을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ddd5a-107">설치 지점 및 설치 지침에 대해서는 [Azure PowerShell 설치 및 구성 방법](/powershell/azureps-cmdlets-docs) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="ddd5a-108">최신 Azure PowerShell 모듈을 다운로드하여 설치하거나 최신 모듈로 업그레이드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="ddd5a-109">**시작**을 클릭하고 **Windows PowerShell**을 입력하여 Azure PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="ddd5a-110">PowerShell 창에 Azure Powershell 모듈이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="ddd5a-111">저장소 계정 및 키에 대한 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="ddd5a-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="ddd5a-112">저장소 계정 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-112">Create the storage account context.</span></span> <span data-ttu-id="ddd5a-113">이 컨텍스트는 저장소 계정 이름 및 계정 키를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="ddd5a-114">[Azure Portal](https://portal.azure.com)에서 계정 키를 복사하는 방법에 대한 지침은 [저장소 액세스 키 보기 및 복사](storage-create-storage-account.md#view-and-copy-storage-access-keys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="ddd5a-115">다음 예제에서 `storage-account-name` 및 `storage-account-key`을(를) 본인의 저장소 계정 이름 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="ddd5a-116">새 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="ddd5a-116">Create a new file share</span></span>
<span data-ttu-id="ddd5a-117">`logs`라는 새 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="ddd5a-118">이제 파일 저장소에 파일 공유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-118">You now have a file share in File storage.</span></span> <span data-ttu-id="ddd5a-119">다음에는 디렉터리와 파일을 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddd5a-120">파일 공유의 이름은 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="ddd5a-121">파일 공유 및 파일 이름 지정에 대한 자세한 내용은 [공유, 디렉터리, 파일 및 메타데이터 이름 지정 및 참조](https://msdn.microsoft.com/library/azure/dn167011.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="ddd5a-122">파일 공유에 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="ddd5a-122">Create a directory in the file share</span></span>
<span data-ttu-id="ddd5a-123">공유에 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-123">Create a directory in the share.</span></span> <span data-ttu-id="ddd5a-124">다음 예제에서 디렉터리 이름은 `CustomLogs`입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="ddd5a-125">디렉터리에 로컬 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ddd5a-125">Upload a local file to the directory</span></span>
<span data-ttu-id="ddd5a-126">이제 디렉터리에 로컬 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="ddd5a-127">다음 예제에서는 `C:\temp\Log1.txt`에서 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="ddd5a-128">로컬 컴퓨터의 유효한 파일을 가리키도록 파일 경로를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="ddd5a-129">디렉터리의 파일 나열</span><span class="sxs-lookup"><span data-stu-id="ddd5a-129">List the files in the directory</span></span>
<span data-ttu-id="ddd5a-130">디렉터리의 파일을 보려면 디렉터리의 파일을 모두 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="ddd5a-131">이 명령은 CustomLogs 디렉터리에서 파일 및 하위 디렉터리(있는 경우)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="ddd5a-132">Get-AzureStorageFile은 디렉터리 개체가 전달되는 파일 및 디렉터리의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="ddd5a-133">"Get-AzureStorageFile -Share $s"는 루트 디렉터리에 파일 및 디렉터리의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="ddd5a-134">하위 디렉터리에 있는 파일의 목록을 가져오려면 Get-AzureStorageFile에 하위 디렉터리를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="ddd5a-135">즉, 파이프에 대한 명령의 첫 번째 부분은 CustomLogs 하위 디렉터리의 디렉터리 인스턴스를 반환하는 기능을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="ddd5a-136">그런 다음 Get-AzureStorageFile에 전달되고 이는 CustomLogs에 파일 및 디렉터리를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="ddd5a-137">파일 복사</span><span class="sxs-lookup"><span data-stu-id="ddd5a-137">Copy files</span></span>
<span data-ttu-id="ddd5a-138">Azure PowerShell 버전 0.9.7부터 파일을 다른 파일로, 파일을 Blob으로 또는 Blob을 파일로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="ddd5a-139">아래에는 PowerShell Cmdlet을 사용하여 이러한 복사 작업을 수행하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="ddd5a-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddd5a-140">Next steps</span></span>
<span data-ttu-id="ddd5a-141">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd5a-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="ddd5a-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="ddd5a-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="ddd5a-143">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ddd5a-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)