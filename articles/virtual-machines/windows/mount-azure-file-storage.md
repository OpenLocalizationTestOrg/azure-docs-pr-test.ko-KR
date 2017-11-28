---
title: "Windows Azure VM에서 Azure 파일 저장소 aaaMount | Microsoft Docs"
description: "Hello 클라우드 Azure 파일 저장소에 파일을 저장 하 고 Azure 가상 컴퓨터 (VM)에서 클라우드 파일 공유를 탑재 합니다."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="f5a8b-103">Windows VM과 Azure 파일 공유 사용</span><span class="sxs-lookup"><span data-stu-id="f5a8b-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="f5a8b-104">Vm에서 방법은 toostore 및 액세스 파일로 Azure 파일 공유를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="f5a8b-105">예를 들어 스크립트 또는 프로그램의 모든 Vm tooshare 되도록 응용 프로그램 구성 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="f5a8b-106">이 항목에서는 보여줍니다 toocreate 및 탑재 Azure 파일 공유, 방법 등에 tooupload 파일과 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="f5a8b-107">VM에서 tooa 파일 공유에 연결</span><span class="sxs-lookup"><span data-stu-id="f5a8b-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="f5a8b-108">이 섹션에서는 파일을 tooconnect 원하는 공유를 이미 있으면 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="f5a8b-109">하나는 toocreate 필요한 경우 참조 [파일 공유 만들기](#create-a-file-share) 이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="f5a8b-110">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5a8b-111">Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f5a8b-112">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="f5a8b-112">Choose your storage account.</span></span>
4. <span data-ttu-id="f5a8b-113">Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f5a8b-114">파일 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-114">Select a file share.</span></span>
6. <span data-ttu-id="f5a8b-115">클릭 **연결** tooopen Windows 또는 Linux에서 탑재 hello 파일 공유에 대 한 hello 명령줄 구문을 보여 주는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="f5a8b-116">Hello 명령 구문을 hello를 강조 표시 하 고 메모장 이나 다른 쉽게 액세스할 수 있는 순서에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="f5a8b-117">Hello 구문 tooremove hello 앞에 오는 편집 * * > * * 및 바꾸기 *[드라이브 문자]* hello 드라이브 문자 (예를 들어 **y:**) 넣을 toomount hello 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="f5a8b-118">Tooyour VM을 연결 하 고 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="f5a8b-119">Hello에 붙여넣기 연결 구문을 편집 하 고 적중 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="f5a8b-120">Hello 연결을 만들면 메시지가 hello **hello 명령이 성공적으로 완료 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f5a8b-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="f5a8b-121">Hello 드라이브 문자 tooswitch toothat 드라이브에 입력 하 여 hello 연결을 확인 한 다음 입력 **dir** hello 파일 공유의 toosee hello 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="f5a8b-122">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="f5a8b-122">Create a file share</span></span> 
1. <span data-ttu-id="f5a8b-123">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5a8b-124">Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f5a8b-125">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="f5a8b-125">Choose your storage account.</span></span>
4. <span data-ttu-id="f5a8b-126">Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f5a8b-127">Hello 파일 서비스 페이지에서 클릭 **+ 파일 공유** toocreate 첫 번째 파일을 공유 합니다. \ \\</span><span class="sxs-lookup"><span data-stu-id="f5a8b-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="f5a8b-128">Hello 파일 공유 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-128">Fill in hello file share name.</span></span> <span data-ttu-id="f5a8b-129">파일 공유 이름은 소문자, 숫자 및 단일 하이픈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="f5a8b-130">hello 이름은 하이픈으로 시작할 수 없습니다 및 여러를 사용할 수 없는 연속 된 하이픈입니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="f5a8b-131">Hello 파일 크기에서 제한에 대 한 채우기 too5120 GB를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="f5a8b-132">클릭 **확인** toodeploy hello 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="f5a8b-133">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f5a8b-133">Upload files</span></span>
1. <span data-ttu-id="f5a8b-134">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5a8b-135">Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f5a8b-136">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="f5a8b-136">Choose your storage account.</span></span>
4. <span data-ttu-id="f5a8b-137">Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f5a8b-138">파일 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-138">Select a file share.</span></span>
6. <span data-ttu-id="f5a8b-139">클릭 **업로드** tooopen hello **파일 업로드** 페이지.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="f5a8b-140">Hello 폴더 아이콘 toobrowse 로컬 파일 시스템 파일 tooupload 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="f5a8b-141">클릭 **업로드** tooupload hello 파일 toohello 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="f5a8b-142">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="f5a8b-142">Download files</span></span>
1. <span data-ttu-id="f5a8b-143">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5a8b-144">Hello 왼쪽된 메뉴에서 클릭 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f5a8b-145">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="f5a8b-145">Choose your storage account.</span></span>
4. <span data-ttu-id="f5a8b-146">Hello에 **개요** 페이지의 **서비스**선택, **파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f5a8b-147">파일 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-147">Select a file share.</span></span>
6. <span data-ttu-id="f5a8b-148">Hello 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **다운로드** toodownload 것 tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="f5a8b-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5a8b-149">Next steps</span></span>

<span data-ttu-id="f5a8b-150">또한 PowerShell을 사용하여 파일 공유를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="f5a8b-151">자세한 내용은 [Windows에서 Azure File storage 시작](../../storage/files/storage-dotnet-how-to-use-files.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5a8b-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
