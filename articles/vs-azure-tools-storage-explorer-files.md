---
title: "aaaUsing Azure 파일 저장소와 저장소 탐색기 (미리 보기) | Microsoft Docs"
description: "자세한 내용은 toouse 저장소 탐색기 (미리 보기) toowork 파일과 함께 공유 하 고 파일 하는 방법을 알아보려면 어떻게 합니다."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="d540e-103">Azure 파일 저장소와 함께 저장소 탐색기(미리 보기) 사용</span><span class="sxs-lookup"><span data-stu-id="d540e-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="d540e-104">Azure 파일 저장소 hello 클라우드 사용 하 여 공유 파일을 제공 하는 서비스는 hello 표준 서버 메시지 블록 (SMB) 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="d540e-105">SMB 2.1과 SMB 3.0 모두를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="d540e-106">Azure 파일 저장소를 신속 하 고 비용이 많이 드는 다시 작성 하지 않고도 파일 공유 tooAzure에 의존 하는 레거시 응용 프로그램을 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="d540e-107">파일 저장소 tooexpose 데이터 사용 하 여 공개적으로 toohello 권역 또는 toostore 응용 프로그램 데이터 개인적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="d540e-108">이 문서에서는 toouse 저장소 탐색기 (미리 보기) toowork 파일과 함께 공유 하 고 파일 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d540e-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d540e-109">Prerequisites</span></span>

<span data-ttu-id="d540e-110">이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="d540e-111">저장소 탐색기(미리 보기) 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="d540e-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="d540e-112">Tooa Azure 저장소 계정 또는 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="d540e-113">파일 공유 만들기</span><span class="sxs-lookup"><span data-stu-id="d540e-113">Create a File Share</span></span>

<span data-ttu-id="d540e-114">모든 파일은 단지 파일의 논리적 그룹화인 파일 공유에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="d540e-115">한 계정에 포함될 수 있는 파일 공유 수에 제한이 없으며, 각 공유에 저장될 수 있는 파일 수에도 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="d540e-116">단계를 수행 하는 hello 어떻게 toocreate 파일은 내 저장소 탐색기 (미리 보기)을 공유 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="d540e-117">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="d540e-118">Hello 왼쪽된 창에서 원하는 toocreate hello 파일 공유는 hello 저장소 계정의 확장</span><span class="sxs-lookup"><span data-stu-id="d540e-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="d540e-119">마우스 오른쪽 단추로 클릭 **파일 공유**, 및-hello 상황에 맞는 메뉴-선택 **파일 공유 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![파일 공유 만들기](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="d540e-121">Hello 아래 텍스트 상자에 표시 될 **파일 공유** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="d540e-122">파일 공유에 대 한 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-122">Enter hello name for your file share.</span></span> <span data-ttu-id="d540e-123">Hello 참조 [명명 규칙 공유](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) 섹션 목록에 대 한 규칙 및 파일 공유 이름 지정에 대 한 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Hello 공유 이름 지정](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="d540e-125">키를 눌러 **Enter** 완료 toocreate hello 파일 공유 하는 경우 또는 **Esc** toocancel 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="d540e-126">파일 공유 hello 성공적으로 만든 후 그 아래에 표시 됩니다 hello **파일 공유** 폴더 hello에 대 한 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![hello 새 공유](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="d540e-128">파일 공유의 내용 보기</span><span class="sxs-lookup"><span data-stu-id="d540e-128">View a file share's contents</span></span>

<span data-ttu-id="d540e-129">파일 공유는 파일 및 폴더(파일을 포함할 수도 있음)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="d540e-130">hello 아래 단계에 설명 된 파일의 tooview hello 내용을 저장소 탐색기 (미리 보기) 내에서 공유 하는 방법: +</span><span class="sxs-lookup"><span data-stu-id="d540e-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="d540e-131">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="d540e-132">Hello 왼쪽된 창에서 원하는 tooview hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="d540e-133">Hello 저장소 계정의 확장 **파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="d540e-134">Hello 파일 공유를 마우스 오른쪽 단추로 클릭 tooview, 원하는-hello 상황에 맞는 메뉴-선택한 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="d540e-135">원하는 tooview hello 파일 공유를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-135">You can also double-click hello file share you wish tooview.</span></span>

    ![공유 열기](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="d540e-137">hello 주 창에는 hello 파일 공유의 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-137">hello main pane will display hello file share's contents.</span></span>
    
    ![hello 공유의 내용](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="d540e-139">파일 공유 삭제</span><span class="sxs-lookup"><span data-stu-id="d540e-139">Delete a file share</span></span>

<span data-ttu-id="d540e-140">필요에 따라 파일 공유를 쉽게 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="d540e-141">(toosee toodelete 개별 파일 toohello 섹션을 참조 하는 방법 [파일 공유에서 파일 관리](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="d540e-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="d540e-142">단계를 수행 하는 hello를 어떻게 toodelete 파일 공유 저장소 탐색기 (미리 보기)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="d540e-143">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="d540e-144">Hello 왼쪽된 창에서 원하는 tooview hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="d540e-145">Hello 저장소 계정의 확장 **파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="d540e-146">Hello 파일 공유를 마우스 오른쪽 단추로 클릭 toodelete, 원하는-hello 상황에 맞는 메뉴-선택한 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="d540e-147">또한 누르면 **삭제** toodelete hello 현재 선택 된 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![삭제](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="d540e-149">선택 **예** toohello 확인 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d540e-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![확인 대화 상자](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="d540e-151">파일 공유 복사</span><span class="sxs-lookup"><span data-stu-id="d540e-151">Copy a file share</span></span>

<span data-ttu-id="d540e-152">저장소 탐색기 (미리 보기) toocopy 파일 공유 toohello 클립보드를 사용 하면 한 다음 다른 저장소 계정에 해당 파일 공유를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="d540e-153">(toosee toocopy 개별 파일 toohello 섹션을 참조 하는 방법 [파일 공유에서 파일 관리](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="d540e-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="d540e-154">단계를 수행 하는 hello toocopy 파일 한 저장소 계정 tooanother에서 공유 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="d540e-155">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="d540e-156">Hello 왼쪽된 창에서 원하는 toocopy hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="d540e-157">Hello 저장소 계정의 확장 **파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="d540e-158">Hello 파일 공유를 마우스 오른쪽 단추로 클릭 toocopy, 원하는-hello 상황에 맞는 메뉴-선택한 **복사본 파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![파일 공유 복사](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="d540e-160">toopaste hello 파일 공유를 한-hello 상황에 맞는 메뉴-선택 hello 원하는 "대상" 저장소 계정을 마우스 오른쪽 단추로 **붙여넣기 파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![파일 공유 붙여넣기](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="d540e-162">파일 공유에 대 한 SAS hello 가져오기</span><span class="sxs-lookup"><span data-stu-id="d540e-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="d540e-163">A [공유 액세스 서명 (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) 저장소 계정의 tooresources 위임 된 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="d540e-164">이 클라이언트가 시간 및 지정한 사용 권한 집합이 지정된 된 기간에 대 한 저장소 계정에 사용 권한을 tooobjects tooshare 계정 액세스 키 필요 없이 제한에 부여할 수 있는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="d540e-165">hello 아래 단계에 설명 파일에 대 한 SAS를 공유 하는 toocreate 어떻게: +</span><span class="sxs-lookup"><span data-stu-id="d540e-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="d540e-166">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="d540e-167">Hello 왼쪽된 창에서 확장 hello 저장소 계정 hello 파일 공유를 원하는 tooget SAS를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="d540e-168">Hello 저장소 계정의 확장 **파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="d540e-169">Hello 원하는 파일 공유를 마우스 오른쪽 단추로 클릭 하 고-hello 상황에 맞는 메뉴-선택 **공유 액세스 서명을 가져올**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![공유 액세스 서명 가져오기](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="d540e-171">Hello에 **공유 액세스 서명을** 대화 상자에서 hello 정책, 시작 및 만료 날짜, 표준 시간대를 지정 하 고 수준을 hello 리소스에 대 한 액세스.</span><span class="sxs-lookup"><span data-stu-id="d540e-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![SAS 대화 상자](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="d540e-173">Hello SAS 옵션을 지정 하 고 완료 되 면, 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="d540e-174">두 번째 **공유 액세스 서명을** 목록 hello hello URL 따라 파일 공유 및 저장소 리소스를 hello QueryStrings tooaccess를 사용할 수 있습니다에 다음 대화 상자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="d540e-175">선택 **복사** toocopy toohello 클립보드 원하는 다음 toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![두 번째 SAS 대화 상자](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="d540e-177">완료되면 **닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="d540e-178">파일 공유에 대한 액세스 정책 관리</span><span class="sxs-lookup"><span data-stu-id="d540e-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="d540e-179">hello 아래 단계에 설명 방법을 toomanage (추가 및 제거) 액세스 파일 공유에 대 한 정책: + 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="d540e-180">사용자 צ ְ ײ tooaccess hello 저장소 파일 리소스 정의 된 기간 동안 SAS Url 생성을 위한 hello 액세스 정책 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="d540e-181">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="d540e-182">Hello 왼쪽된 창에서 확장 hello 저장소 계정 액세스 정책이 toomanage 원하는 hello 파일 공유를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="d540e-183">Hello 저장소 계정의 확장 **파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="d540e-184">Hello 원하는 파일 공유를 선택 하 고-hello 상황에 맞는 메뉴-선택 **액세스 정책 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![액세스 정책 상황에 맞는 메뉴 관리](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="d540e-186">hello **액세스 정책을** 대화 이미 만든 hello 선택한 파일 공유에 대 한 모든 액세스 정책 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![액세스 정책](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="d540e-188">Hello 액세스 정책 관리 작업에 따라 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="d540e-189">**새 액세스 정책 추가** - **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="d540e-190">생성 되 면 hello **액세스 정책을** hello 새로 추가 된 대화 상자가 표시 됩니다 (기본 설정)으로 정책에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="d540e-191">**액세스 정책 편집** - 원하는 편집을 모두 마치고, **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="d540e-192">**액세스 정책을 제거** -선택 **제거** tooremove 원하는 다음 toohello 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="d540e-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="d540e-193">앞에서 만든 액세스 정책 hello를 사용 하 여 새 SAS URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![SAS 가져오기](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS 이름 및 속성](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="d540e-196">파일 공유에서 파일 관리</span><span class="sxs-lookup"><span data-stu-id="d540e-196">Managing files in a file share</span></span>

<span data-ttu-id="d540e-197">파일 공유를 만든 후 업로드 파일 toothat 파일 공유 파일 tooyour 로컬 컴퓨터에 다운로드을 등과 로컬 컴퓨터에 파일을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="d540e-198">hello 아래 단계에 설명 toomanage hello 파일 및 폴더 파일 내에서 공유 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="d540e-199">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="d540e-200">Hello 왼쪽된 창에서 원하는 toomanage hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="d540e-201">Hello 저장소 계정의 확장 **파일 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="d540e-202">원하는 tooview hello 파일 공유를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="d540e-203">hello 주 창에는 hello 파일 공유의 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-203">hello main pane will display hello file share's contents.</span></span>

    ![hello 공유의 내용](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="d540e-205">hello 주 창에는 hello 파일 공유의 내용이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="d540e-206">Tooperform 원하는 hello 작업에 따라 다음이 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="d540e-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="d540e-207">**업로드 파일 tooa 파일 공유**</span><span class="sxs-lookup"><span data-stu-id="d540e-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="d540e-208">a.</span><span class="sxs-lookup"><span data-stu-id="d540e-208">a.</span></span>  <span data-ttu-id="d540e-209">Hello 주 창 도구 모음 선택 **업로드**, 차례로 **파일 업로드** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![파일 업로드](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="d540e-211">b.</span><span class="sxs-lookup"><span data-stu-id="d540e-211">b.</span></span> <span data-ttu-id="d540e-212">Hello에 **파일 업로드** 대화 상자에서 선택 hello 줄임표 (**...** )의 hello hello 오른쪽 단추를 **파일** 텍스트 상자에 원하는 tooupload tooselect hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![파일 추가](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="d540e-214">c.</span><span class="sxs-lookup"><span data-stu-id="d540e-214">c.</span></span> <span data-ttu-id="d540e-215">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-215">Select **Upload**.</span></span>

    - <span data-ttu-id="d540e-216">**폴더 tooa 파일 공유를 업로드 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d540e-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="d540e-217">a.</span><span class="sxs-lookup"><span data-stu-id="d540e-217">a.</span></span> <span data-ttu-id="d540e-218">Hello 주 창 도구 모음 선택 **업로드**, 차례로 **폴더 업로드** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![폴더 메뉴 업로드](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="d540e-220">b.</span><span class="sxs-lookup"><span data-stu-id="d540e-220">b.</span></span> <span data-ttu-id="d540e-221">Hello에 **업로드 폴더** 대화 상자에서 선택 hello 줄임표 (**...** )의 hello hello 오른쪽 단추를 **폴더** 텍스트 상자 tooselect hello 내용을 폴더 tooupload 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="d540e-222">c.</span><span class="sxs-lookup"><span data-stu-id="d540e-222">c.</span></span> <span data-ttu-id="d540e-223">필요에 따라 어떤 hello에 선택한 폴더의 내용을 업로드할 수는 대상 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="d540e-224">Hello 대상 폴더가 존재 하지 않는 경우 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="d540e-225">d.</span><span class="sxs-lookup"><span data-stu-id="d540e-225">d.</span></span> <span data-ttu-id="d540e-226">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-226">Select **Upload**.</span></span>

    - <span data-ttu-id="d540e-227">**다운로드 파일 tooyour 로컬 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="d540e-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="d540e-228">a.</span><span class="sxs-lookup"><span data-stu-id="d540e-228">a.</span></span> <span data-ttu-id="d540e-229">Toodownload hello 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="d540e-230">b.</span><span class="sxs-lookup"><span data-stu-id="d540e-230">b.</span></span> <span data-ttu-id="d540e-231">Hello 주 창 도구 모음 선택 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="d540e-232">c.</span><span class="sxs-lookup"><span data-stu-id="d540e-232">c.</span></span> <span data-ttu-id="d540e-233">Hello에 **지정 toosave hello 파일을 다운로드 한** 대화 상자에서 hello 파일 다운로드를 저장할 hello 위치를 지정 하 고 toogive 이름 hello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="d540e-234">d.</span><span class="sxs-lookup"><span data-stu-id="d540e-234">d.</span></span> <span data-ttu-id="d540e-235">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-235">Select **Save**.</span></span>

    - <span data-ttu-id="d540e-236">**로컬 컴퓨터에서 파일 열기**</span><span class="sxs-lookup"><span data-stu-id="d540e-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="d540e-237">a.</span><span class="sxs-lookup"><span data-stu-id="d540e-237">a.</span></span>  <span data-ttu-id="d540e-238">Tooopen hello 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="d540e-239">b.</span><span class="sxs-lookup"><span data-stu-id="d540e-239">b.</span></span>  <span data-ttu-id="d540e-240">Hello 주 창 도구 모음 선택 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="d540e-241">c.</span><span class="sxs-lookup"><span data-stu-id="d540e-241">c.</span></span>  <span data-ttu-id="d540e-242">hello 파일 다운로드 되 고 hello 파일의 원본으로 사용 하는 파일 형식과 연결 된 hello 응용 프로그램을 사용 하 여 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="d540e-243">**파일 toohello 클립보드로 복사**</span><span class="sxs-lookup"><span data-stu-id="d540e-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="d540e-244">a.</span><span class="sxs-lookup"><span data-stu-id="d540e-244">a.</span></span> <span data-ttu-id="d540e-245">Toocopy hello 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="d540e-246">b.</span><span class="sxs-lookup"><span data-stu-id="d540e-246">b.</span></span> <span data-ttu-id="d540e-247">Hello 주 창 도구 모음 선택 **복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="d540e-248">c.</span><span class="sxs-lookup"><span data-stu-id="d540e-248">c.</span></span> <span data-ttu-id="d540e-249">Hello 왼쪽된 창에서 tooanother 파일 공유를 찾아 두 번 클릭 tooview hello 주 창에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="d540e-250">d.</span><span class="sxs-lookup"><span data-stu-id="d540e-250">d.</span></span> <span data-ttu-id="d540e-251">Hello 주 창 도구 모음 선택 **붙여넣기** toocreate hello 파일의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="d540e-252">**파일 삭제**</span><span class="sxs-lookup"><span data-stu-id="d540e-252">**Delete a file**</span></span>

        <span data-ttu-id="d540e-253">a.</span><span class="sxs-lookup"><span data-stu-id="d540e-253">a.</span></span> <span data-ttu-id="d540e-254">Toodelete hello 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="d540e-255">b.</span><span class="sxs-lookup"><span data-stu-id="d540e-255">b.</span></span> <span data-ttu-id="d540e-256">Hello 주 창 도구 모음 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="d540e-257">c.</span><span class="sxs-lookup"><span data-stu-id="d540e-257">c.</span></span> <span data-ttu-id="d540e-258">선택 **예** toohello 확인 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d540e-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d540e-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d540e-259">Next steps</span></span>

- <span data-ttu-id="d540e-260">보기 hello [최신 저장소 탐색기 (미리 보기) 릴리스 정보 및 비디오](http://www.storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="d540e-261">너무 방법에 대해 알아봅니다[Azure blob, 테이블, 큐 및 파일을 사용 하 여 응용 프로그램을 만들](https://azure.microsoft.com/documentation/services/storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d540e-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
