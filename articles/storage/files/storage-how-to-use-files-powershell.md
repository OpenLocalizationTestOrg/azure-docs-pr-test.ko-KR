---
title: "Azure 파일 저장소 aaaHow toouse PowerShell toomanage | Microsoft Docs"
description: "Toouse PowerShell toomanage Azure 파일 저장소에 알아봅니다."
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="dc87b-103">어떻게 toouse PowerShell toomanage Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="dc87b-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="dc87b-104">Azure PowerShell toocreate를 사용 하 고 파일 공유를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="dc87b-105">Azure 저장소에 대 한 hello PowerShell cmdlet을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="dc87b-106">tooprepare toouse PowerShell 다운로드 하 여 hello Azure PowerShell cmdlet을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="dc87b-107">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) hello에 대 한 지점 및 설치 지침을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="dc87b-108">다운로드 및 설치 하거나 업그레이드 toohello 최신 Azure PowerShell 모듈 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="dc87b-109">**시작**을 클릭하고 **Windows PowerShell**을 입력하여 Azure PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="dc87b-110">hello PowerShell 창을 hello Azure Powershell 모듈을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="dc87b-111">저장소 계정 및 키에 대한 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="dc87b-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="dc87b-112">Hello 저장소 계정 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-112">Create hello storage account context.</span></span> <span data-ttu-id="dc87b-113">hello 컨텍스트 hello 저장소 계정 이름 및 계정 키를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="dc87b-114">Hello에서 계정 키를 복사에 대 한 지침은 [Azure 포털](https://portal.azure.com), 참조 [저장소 액세스 키 보기 및 복사](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="dc87b-115">대체 `storage-account-name` 및 `storage-account-key` 저장소 계정 이름 및 키 hello 다음 예제에에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="dc87b-116">새 파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="dc87b-116">Create a new file share</span></span>
<span data-ttu-id="dc87b-117">명명 된 hello 새 공유 만들기 `logs`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="dc87b-118">이제 파일 저장소에 파일 공유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-118">You now have a file share in File storage.</span></span> <span data-ttu-id="dc87b-119">다음에는 디렉터리와 파일을 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc87b-120">파일 공유 hello 이름이 모두 소문자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="dc87b-121">파일 공유 및 파일 이름 지정에 대한 자세한 내용은 [공유, 디렉터리, 파일 및 메타데이터 이름 지정 및 참조](https://msdn.microsoft.com/library/azure/dn167011.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc87b-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="dc87b-122">Hello 파일 공유에서 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="dc87b-122">Create a directory in hello file share</span></span>
<span data-ttu-id="dc87b-123">Hello 공유의 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-123">Create a directory in hello share.</span></span> <span data-ttu-id="dc87b-124">다음 예제는 hello, hello 디렉터리 이름은 `CustomLogs`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="dc87b-125">로컬 파일 toohello 디렉터리를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="dc87b-126">이제 로컬 파일 toohello 디렉터리를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="dc87b-127">hello 다음 예제에서는 파일을 업로드에서 `C:\temp\Log1.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="dc87b-128">로컬 컴퓨터에 유효한 파일이 tooa 가리키도록 hello 파일 경로 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="dc87b-129">Hello 디렉터리에 hello 파일 나열</span><span class="sxs-lookup"><span data-stu-id="dc87b-129">List hello files in hello directory</span></span>
<span data-ttu-id="dc87b-130">hello 디렉터리에 toosee hello 파일인 hello 디렉터리의 파일을 모두를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="dc87b-131">이 명령은 hello 파일 및 하위 디렉터리 (있는 경우)의 반환 hello CustomLogs 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="dc87b-132">Get-AzureStorageFile은 디렉터리 개체가 전달되는 파일 및 디렉터리의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="dc87b-133">"Get AzureStorageFile-$s 공유" hello 루트 디렉터리에 파일 및 디렉터리의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="dc87b-134">하위 디렉터리에 파일 목록이 tooget toopass hello 하위 디렉터리 tooGet AzureStorageFile 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="dc87b-135">즉,이-hello toohello 파이프를 hello 명령의 첫 번째 부분은 hello 하위 디렉터리 CustomLogs의 디렉터리 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="dc87b-136">그런 다음 Get AzureStorageFile CustomLogs에 hello 파일 및 디렉터리를 반환 하는 전달 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="dc87b-137">파일 복사</span><span class="sxs-lookup"><span data-stu-id="dc87b-137">Copy files</span></span>
<span data-ttu-id="dc87b-138">Azure PowerShell 0.9.7 버전부터, 파일 tooanother 파일, 파일 tooa blob 또는 blob tooa 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="dc87b-139">아래에 대해서도 설명 tooperform 이러한 복사 방법 PowerShell cmdlet을 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="dc87b-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc87b-140">Next steps</span></span>
<span data-ttu-id="dc87b-141">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dc87b-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="dc87b-142">FAQ</span><span class="sxs-lookup"><span data-stu-id="dc87b-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="dc87b-143">Windows에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dc87b-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="dc87b-144">Linux에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dc87b-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    