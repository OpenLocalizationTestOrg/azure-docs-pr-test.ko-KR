---
title: "Azure Windows VM에서 Azure File Storage 탑재 | Microsoft Docs"
description: "Azure File Storage를 사용하여 클라우드에 파일을 저장하고 Azure VM(Virtual Machine)에서 클라우드 파일 공유를 탑재합니다."
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
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="1932d-103">Windows VM과 Azure 파일 공유 사용</span><span class="sxs-lookup"><span data-stu-id="1932d-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="1932d-104">VM에서 파일을 저장하고 액세스하는 방법으로 Azure 파일 공유를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="1932d-105">예를 들어 모든 VM을 공유하려는 스크립트 또는 응용 프로그램 구성 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="1932d-106">이 토픽에서는 Azure 파일 공유를 만들고 탑재하는 방법과 파일을 업로드 및 다운로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="1932d-107">VM에서 파일 공유에 연결</span><span class="sxs-lookup"><span data-stu-id="1932d-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="1932d-108">이 섹션에서는 연결하려는 파일 공유가 이미 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="1932d-109">하나 만들어야 하는 경우 이 토픽의 뒷부분에 나오는 [파일 공유 만들기](#create-a-file-share)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1932d-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="1932d-110">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1932d-111">왼쪽 메뉴에서 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="1932d-112">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="1932d-112">Choose your storage account.</span></span>
4. <span data-ttu-id="1932d-113">**개요** 페이지에 있는 **서비스**에서 **파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="1932d-114">파일 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-114">Select a file share.</span></span>
6. <span data-ttu-id="1932d-115">**연결**을 클릭하여 Windows 또는 Linux에서 파일 공유를 탑재하는 명령줄 구문을 보여 주는 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="1932d-116">명령 구문을 강조 표시하고 메모장이나 쉽게 액세스할 수 있는 다른 곳에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="1932d-117">구문을 편집하여 선행하는 **> **를 제거하고 *[드라이브 문자]*를 파일 공유를 탑재하려는 드라이브 문자(예: **Y:**)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="1932d-118">VM에 연결하고 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="1932d-119">편집된 연결 구문에 붙여넣고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="1932d-120">연결이 생성되면 **명령이 성공적으로 완료되었습니다.**라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="1932d-121">해당 드라이브로 전환되도록 드라이브 문자를 입력하여 연결을 확인하고, **dir**를 입력하여 파일 공유의 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="1932d-122">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="1932d-122">Create a file share</span></span> 
1. <span data-ttu-id="1932d-123">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1932d-124">왼쪽 메뉴에서 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="1932d-125">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="1932d-125">Choose your storage account.</span></span>
4. <span data-ttu-id="1932d-126">**개요** 페이지에 있는 **서비스**에서 **파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="1932d-127">파일 서비스 페이지에서 **+ 파일 공유**를 클릭하여 첫 번째 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="1932d-128">파일 공유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-128">Fill in the file share name.</span></span> <span data-ttu-id="1932d-129">파일 공유 이름은 소문자, 숫자 및 단일 하이픈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="1932d-130">이름은 하이픈으로 시작할 수 없으며 여러 개 하이픈을 연속하여 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="1932d-131">최대 5120GB까지 파일 크기에 관한 제한을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="1932d-132">**확인**을 클릭하여 파일 공유를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="1932d-133">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="1932d-133">Upload files</span></span>
1. <span data-ttu-id="1932d-134">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1932d-135">왼쪽 메뉴에서 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="1932d-136">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="1932d-136">Choose your storage account.</span></span>
4. <span data-ttu-id="1932d-137">**개요** 페이지에 있는 **서비스**에서 **파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="1932d-138">파일 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-138">Select a file share.</span></span>
6. <span data-ttu-id="1932d-139">**업로드**를 클릭하여 **파일 업로드** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="1932d-140">폴더 아이콘을 클릭하여 업로드할 파일에 대한 로컬 파일 시스템을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="1932d-141">**업로드**를 클릭하여 파일 공유에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="1932d-142">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="1932d-142">Download files</span></span>
1. <span data-ttu-id="1932d-143">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1932d-144">왼쪽 메뉴에서 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="1932d-145">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="1932d-145">Choose your storage account.</span></span>
4. <span data-ttu-id="1932d-146">**개요** 페이지에 있는 **서비스**에서 **파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="1932d-147">파일 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-147">Select a file share.</span></span>
6. <span data-ttu-id="1932d-148">파일 하나를 마우스 오른쪽 단추로 클릭하고 **다운로드**를 선택하여 로컬 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="1932d-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1932d-149">Next steps</span></span>

<span data-ttu-id="1932d-150">또한 PowerShell을 사용하여 파일 공유를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1932d-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="1932d-151">자세한 내용은 [Windows에서 Azure File storage 시작](../../storage/files/storage-dotnet-how-to-use-files.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1932d-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
