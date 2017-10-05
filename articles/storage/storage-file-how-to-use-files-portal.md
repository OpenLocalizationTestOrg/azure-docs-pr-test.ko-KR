---
title: "Azure Portal에서 Azure File Storage를 관리하는 방법 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure File Storage를 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: d8ffb4359b0efe8da2f3bccb81c987bdeedf1a39
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="95b16-103">Azure Portal에서 Azure File Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="95b16-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="95b16-104">[Azure Portal](https://portal.azure.com)에서는 Azure File Storage를 관리하기 위한 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="95b16-105">웹 브라우저에서 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="95b16-106">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="95b16-106">Create a File Share</span></span>
* <span data-ttu-id="95b16-107">파일 공유에 대해 파일 업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="95b16-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="95b16-108">각 파일 공유의 실제 사용량 모니터링</span><span class="sxs-lookup"><span data-stu-id="95b16-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="95b16-109">파일 공유 크기 할당량 조정</span><span class="sxs-lookup"><span data-stu-id="95b16-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="95b16-110">Windows 또는 Linux 클라이언트에서 파일 공유를 탑재하는 데 사용할 탑재 명령 복사</span><span class="sxs-lookup"><span data-stu-id="95b16-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="95b16-111">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="95b16-111">Create file share</span></span>
1. <span data-ttu-id="95b16-112">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="95b16-113">탐색 메뉴에서 **저장소 계정** 또는 **저장소 계정(클래식)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![포털에서 파일 공유를 만드는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="95b16-115">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="95b16-115">Choose your storage account.</span></span>

    ![포털에서 파일 공유를 만드는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="95b16-117">"파일" 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-117">Choose "Files" service.</span></span>

    ![포털에서 파일 공유를 만드는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="95b16-119">"파일 공유"를 클릭하고 링크를 따라 첫 번째 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![포털에서 파일 공유를 만드는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="95b16-121">파일 공유 이름 및 파일 공유 파일의 크기(최대 5120GB)를 입력하여 첫 번째 파일 공유를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="95b16-122">파일 공유가 만들어지면 SMB 2.1 또는 SMB 3.0을 지원하는 모든 파일 시스템에서 마운트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="95b16-123">파일 공유의 **할당량**을 클릭하여 파일 크기를 최대 5,120GB까지 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="95b16-124">Azure File Storage를 사용하는 저장소 비용을 예측하려면 [Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95b16-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![포털에서 파일 공유를 만드는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="95b16-126">파일 업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="95b16-126">Upload and download files</span></span>
1. <span data-ttu-id="95b16-127">이미 만든 파일 공유 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-127">Choose one file share your have already created.</span></span>

    ![포털에서 파일을 업로드 및 다운로드하는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="95b16-129">**업로드** 를 클릭하여 업로드하는 파일에 대한 사용자 인터페이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![포털에서 파일을 업로드하는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="95b16-131">파일 공유에 연결</span><span class="sxs-lookup"><span data-stu-id="95b16-131">Connect to file share</span></span>
-  <span data-ttu-id="95b16-132">**연결**을 클릭하여 Windows 및 Linux에서 파일 공유를 탑재하기 위한 명령줄을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="95b16-133">Linux 사용자의 경우 다른 Linux 배포에 대한 자세한 탑재 지침은 [Linux에서 Azure File storage 사용 방법](storage-how-to-use-files-linux.md)도 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![파일 공유를 마운트하는 방법을 보여주는 스크린 샷](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="95b16-135">Windows 또는 Linux에서 파일 공유를 탑재하기 위한 명령을 복사하고 Azure VM 또는 온-프레미스 컴퓨터에서 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Windows 및 Linux용 탑재 명령을 보여주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="95b16-137">**팁:**</span><span class="sxs-lookup"><span data-stu-id="95b16-137">**Tip:**</span></span>  
<span data-ttu-id="95b16-138">탑재할 저장소 계정 액세스 키를 찾으려면 연결 페이지 아래쪽에서 **이 저장소 계정에 대한 액세스 키 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="95b16-139">참고 항목</span><span class="sxs-lookup"><span data-stu-id="95b16-139">See also</span></span>
<span data-ttu-id="95b16-140">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="95b16-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="95b16-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="95b16-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="95b16-142">문제 해결</span><span class="sxs-lookup"><span data-stu-id="95b16-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)