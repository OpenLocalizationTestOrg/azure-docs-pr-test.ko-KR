---
title: "aaaHow toomanage hello Azure 포털에서에서 Azure 파일 저장소 | Microsoft Docs"
description: "Toouse hello Azure 포털 toomanage Azure 파일 저장소에 알아봅니다."
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
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="ca715-103">Toouse Azure 파일 저장소에서 Azure 포털을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ca715-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="ca715-104">hello [Azure 포털](https://portal.azure.com) Azure 파일 저장소 관리를 위한 사용자 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="ca715-105">웹 브라우저에서 작업을 수행 하는 hello를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="ca715-106">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="ca715-106">Create a File Share</span></span>
* <span data-ttu-id="ca715-107">업로드 한 파일 tooand 파일 공유에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="ca715-108">각 파일 공유의 hello 실제 사용을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="ca715-109">Hello 파일 공유 크기 할당량을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="ca715-110">Windows 또는 Linux 클라이언트에서 파일을 공유 하는 hello 탑재 명령을 toouse toomount를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="ca715-111">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="ca715-111">Create file share</span></span>
1. <span data-ttu-id="ca715-112">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="ca715-113">Hello 탐색 메뉴에서 클릭 **저장소 계정은** 또는 **저장소 계정 (클래식)**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="ca715-115">저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="ca715-115">Choose your storage account.</span></span>

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="ca715-117">"파일" 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-117">Choose "Files" service.</span></span>

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="ca715-119">"파일 공유"를 클릭 하 고 첫 번째 파일을 공유 하는 hello 링크 toocreate를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="ca715-121">Hello 파일 공유 이름 및 입력 파일 (too5120 GB)를 공유 toocreate hello의 hello 크기 첫 번째 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="ca715-122">Hello 파일 공유를 만든 후에 SMB 2.1 또는 SMB 3.0을 지 원하는 모든 파일 시스템에서 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="ca715-123">클릭할 수 **할당량** too5120 GB hello 파일의 hello 파일 공유 toochange hello 크기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="ca715-124">너무를 참조 하십시오[Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/) tooestimate hello 저장 비용은 Azure 파일 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Hello 포털에서 toocreate 파일을 공유 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="ca715-126">파일 업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="ca715-126">Upload and download files</span></span>
1. <span data-ttu-id="ca715-127">이미 만든 파일 공유 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-127">Choose one file share your have already created.</span></span>

    ![파일을 다운로드 하 고 tooupload 포털 hello 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="ca715-129">클릭 **업로드** 파일 업로드에 대 한 hello 사용자 인터페이스를 열려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Hello 포털에서 tooupload 파일 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="ca715-131">Toofile 공유를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-131">Connect toofile share</span></span>
-  <span data-ttu-id="ca715-132">클릭 **연결** 탑재 hello 파일 공유에 대 한 Windows 및 Linux에서 hello 명령줄을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="ca715-133">Linux 사용자를 참조할 수도 있습니다 너무[어떻게 toouse Azure 파일 저장소와 Linux](storage-how-to-use-files-linux.md) 다른 Linux 배포판에 대 한 자세한 설치 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Toomount 파일 공유를 hello 하는 방법을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="ca715-135">파일을 탑재 명령은 Windows 또는 Linux에서 공유 하 고 Azure VM 또는 온-프레미스 컴퓨터에서 실행할 hello를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Windows 및 Linux 용 hello 탑재 명령을 보여 주는 스크린샷](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="ca715-137">**팁:**</span><span class="sxs-lookup"><span data-stu-id="ca715-137">**Tip:**</span></span>  
<span data-ttu-id="ca715-138">toofind hello 저장소 계정 액세스 키를 탑재에 대 한 클릭 **이 저장소 계정에 대 한 보기 액세스 키** hello hello 맨 아래에 연결 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="ca715-139">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ca715-139">See also</span></span>
<span data-ttu-id="ca715-140">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ca715-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="ca715-141">FAQ</span><span class="sxs-lookup"><span data-stu-id="ca715-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="ca715-142">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ca715-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)