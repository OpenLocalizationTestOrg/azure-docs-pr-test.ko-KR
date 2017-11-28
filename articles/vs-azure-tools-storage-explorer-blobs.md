---
title: "저장소 탐색기 (미리 보기)를 사용 하 여 Azure Blob 저장소 리소스 aaaManage | Microsoft Docs"
description: "저장소 탐색기(미리 보기)를 사용하여 Azure Blob 컨테이너 및 Blobs 관리"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="18d69-103">저장소 탐색기(미리 보기)를 사용하여 Blob 저장소 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="18d69-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="18d69-104">개요</span><span class="sxs-lookup"><span data-stu-id="18d69-104">Overview</span></span>
<span data-ttu-id="18d69-105">[Azure Blob 저장소](storage/blobs/storage-dotnet-how-to-use-blobs.md) 는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 데이터를 저장 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="18d69-106">Blob 저장소 tooexpose 데이터 사용 하 여 공개적으로 toohello 권역 또는 toostore 응용 프로그램 데이터 개인적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="18d69-107">이 문서에서는 알아봅니다 어떻게 toouse 저장소 탐색기 (미리 보기) toowork blob 컨테이너 및 blob와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18d69-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="18d69-108">Prerequisites</span></span>
<span data-ttu-id="18d69-109">이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="18d69-110">저장소 탐색기(미리 보기) 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="18d69-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="18d69-111">Tooa Azure 저장소 계정 또는 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="18d69-112">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="18d69-112">Create a blob container</span></span>
<span data-ttu-id="18d69-113">모든 blob은 단지 blob의 논리적 그룹화인 blob 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="18d69-114">한 계정에 포함될 수 있는 컨테이너 수에 제한이 없으며, 각 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="18d69-115">hello 아래 단계에 설명 방법을 toocreate 저장소 탐색기 (미리 보기) 내에서 blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="18d69-116">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-117">Hello 왼쪽된 창에서 원하는 toocreate hello blob 컨테이너는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="18d69-118">마우스 오른쪽 단추로 클릭 **Blob 컨테이너**, 및-hello 상황에 맞는 메뉴-선택 **Create Blob Container**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 만들기][0]
4. <span data-ttu-id="18d69-120">Hello 아래 텍스트 상자에 표시 될 **Blob 컨테이너** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="18d69-121">Blob 컨테이너에 대 한 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="18d69-122">Hello 참조 [컨테이너 명명 규칙](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) 명명 blob 컨테이너에 대 한 제한 규칙의 목록에 대 한 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Blob 컨테이너 텍스트 상자 만들기][1]
5. <span data-ttu-id="18d69-124">키를 눌러 **Enter** 끝나면 toocreate hello blob 컨테이너 또는 **Esc** toocancel 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="18d69-125">Hello blob 컨테이너 성공적으로 만든 후 그 아래에 표시 됩니다 hello **Blob 컨테이너** 폴더 hello에 대 한 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![만든 Blob 컨테이너][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="18d69-127">Blob 컨테이너 내용 보기</span><span class="sxs-lookup"><span data-stu-id="18d69-127">View a blob container's contents</span></span>
<span data-ttu-id="18d69-128">Blob 컨테이너는 blob 및 폴더(blob도 포함할 수 있음)를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="18d69-129">hello 아래 단계에 설명 방법을 저장소 탐색기 (미리 보기) 내에서 blob 컨테이너의 tooview hello 내용:</span><span class="sxs-lookup"><span data-stu-id="18d69-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="18d69-130">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-131">Hello 왼쪽된 창에서 원하는 tooview hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="18d69-132">Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="18d69-133">Hello blob 컨테이너를 마우스 오른쪽 단추로 클릭 tooview, 원하는-hello 상황에 맞는 메뉴-선택한 **Blob 컨테이너 편집기 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="18d69-134">원하는 tooview hello blob 컨테이너를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![blob 컨테이너 편집기 상황에 맞는 메뉴 열기][19]
5. <span data-ttu-id="18d69-136">hello 주 창에는 hello blob 컨테이너의 내용을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-136">hello main pane will display hello blob container's contents.</span></span>

   ![Blob 컨테이너 편집기][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="18d69-138">Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="18d69-138">Delete a blob container</span></span>
<span data-ttu-id="18d69-139">필요에 따라 Blob 컨테이너를 쉽게 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="18d69-140">(toodelete 개별 blob toosee toohello 섹션을 참조 하십시오. [blob 컨테이너에 blob 관리](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="18d69-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="18d69-141">hello 아래 단계에 설명 방법을 toodelete 저장소 탐색기 (미리 보기) 내에서 blob 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="18d69-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="18d69-142">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-143">Hello 왼쪽된 창에서 원하는 tooview hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="18d69-144">Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="18d69-145">Hello blob 컨테이너를 마우스 오른쪽 단추로 클릭 toodelete, 원하는-hello 상황에 맞는 메뉴-선택한 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="18d69-146">또한 누르면 **삭제** toodelete hello 현재 선택 된 blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 삭제][4]
5. <span data-ttu-id="18d69-148">선택 **예** toohello 확인 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="18d69-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Blob 컨테이너 확인 삭제][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="18d69-150">Blob 컨테이너 복사</span><span class="sxs-lookup"><span data-stu-id="18d69-150">Copy a blob container</span></span>
<span data-ttu-id="18d69-151">저장소 탐색기 (미리 보기)을 사용 하면 blob 컨테이너 toohello 클립보드 toocopy 및 다른 저장소 계정에 컨테이너 blob 후 붙여넣습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="18d69-152">(toocopy 개별 blob toosee toohello 섹션을 참조 하십시오. [blob 컨테이너에 blob 관리](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="18d69-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="18d69-153">단계를 수행 하는 hello toocopy 하나의 저장소에서 blob 컨테이너 tooanother를 고려 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="18d69-154">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-155">Hello 왼쪽된 창에서 원하는 toocopy hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="18d69-156">Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="18d69-157">Hello blob 컨테이너를 마우스 오른쪽 단추로 클릭 toocopy, 원하는-hello 상황에 맞는 메뉴-선택한 **복사 Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 복사][6]
5. <span data-ttu-id="18d69-159">toopaste hello blob 컨테이너를 한-hello 상황에 맞는 메뉴-선택 hello 원하는 "대상" 저장소 계정을 마우스 오른쪽 단추로 **붙여넣기 Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 붙여넣기][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="18d69-161">Blob 컨테이너에 대 한 SAS hello 가져오기</span><span class="sxs-lookup"><span data-stu-id="18d69-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="18d69-162">A [공유 액세스 서명 (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) 저장소 계정의 tooresources 위임 된 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="18d69-163">이 계정 액세스 키를 공유 하지 않고 시간 및 지정한 사용 권한 집합이 지정된 된 기간에 대 한 제한 된 저장소 계정에 사용 권한을 tooobjects 클라이언트에 부여할 수 있는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="18d69-164">hello 아래 단계에 설명 방법을 toocreate blob 컨테이너에 대 한 SAS:</span><span class="sxs-lookup"><span data-stu-id="18d69-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="18d69-165">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-166">Hello 왼쪽된 창에서 확장 hello 저장소 계정을 원하는 tooget SAS hello blob 컨테이너를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="18d69-167">Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="18d69-168">Hello 원하는 blob 컨테이너를 마우스 오른쪽 단추로 클릭 하 고-hello 상황에 맞는 메뉴-선택 **공유 액세스 서명을 가져올**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![SAS 상황에 맞는 메뉴 가져오기][8]
5. <span data-ttu-id="18d69-170">Hello에 **공유 액세스 서명을** 대화 상자에서 hello 정책, 시작 및 만료 날짜, 표준 시간대를 지정 하 고 수준을 hello 리소스에 대 한 액세스.</span><span class="sxs-lookup"><span data-stu-id="18d69-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![SAS 옵션 가져오기][9]
6. <span data-ttu-id="18d69-172">Hello SAS 옵션을 지정 하 고 완료 되 면, 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="18d69-173">두 번째 **공유 액세스 서명을** 목록 hello hello URL 따라 blob 컨테이너 및 저장소 리소스를 hello QueryStrings tooaccess를 사용할 수 있습니다에 다음 대화 상자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="18d69-174">선택 **복사** toocopy toohello 클립보드 원하는 다음 toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![SAS Url 복사][10]
8. <span data-ttu-id="18d69-176">완료되면 **닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="18d69-177">Blob 컨테이너에 대한 액세스 정책 관리</span><span class="sxs-lookup"><span data-stu-id="18d69-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="18d69-178">hello 아래 단계에 설명 방법을 toomanage (추가 및 제거) 액세스 한 blob 컨테이너에 대 한 정책:</span><span class="sxs-lookup"><span data-stu-id="18d69-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="18d69-179">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-180">Hello 왼쪽된 창에서 hello 저장소 계정 blob 컨테이너 hello toomanage 원하는 액세스 정책이 포함 된를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="18d69-181">Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="18d69-182">Hello 원하는 blob 컨테이너를 선택 하 고-hello 상황에 맞는 메뉴-선택 **액세스 정책 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![액세스 정책 상황에 맞는 메뉴 관리][11]
5. <span data-ttu-id="18d69-184">hello **액세스 정책을** 대화 이미 만든 hello 선택한 blob 컨테이너에 대 한 모든 액세스 정책 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![액세스 정책 옵션][12]        
6. <span data-ttu-id="18d69-186">Hello 액세스 정책 관리 작업에 따라 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="18d69-187">**새 액세스 정책 추가** - **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="18d69-188">생성 되 면 hello **액세스 정책을** hello 새로 추가 된 대화 상자가 표시 됩니다 (기본 설정)으로 정책에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="18d69-189">**액세스 정책 편집** -원하는 편집을 모두 마치고, **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="18d69-190">**액세스 정책을 제거** -선택 **제거** tooremove 원하는 다음 toohello 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="18d69-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="18d69-191">Blob 컨테이너에 대 한 공용 액세스 수준을 hello 설정</span><span class="sxs-lookup"><span data-stu-id="18d69-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="18d69-192">모든 blob 컨테이너가 너무 설정 기본적으로 "공용 액세스 권한이"입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="18d69-193">hello 아래 단계에 설명 공용 액세스 하는 toospecify 방법을 blob 컨테이너에 대 한 수준.</span><span class="sxs-lookup"><span data-stu-id="18d69-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="18d69-194">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-195">Hello 왼쪽된 창에서 hello 저장소 계정 blob 컨테이너 hello toomanage 원하는 액세스 정책이 포함 된를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="18d69-196">Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="18d69-197">Hello 원하는 blob 컨테이너를 선택 하 고-hello 상황에 맞는 메뉴-선택 **공용 액세스 수준을 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![공용 액세스 수준 상황에 맞는 메뉴 설정][13]
5. <span data-ttu-id="18d69-199">Hello에 **컨테이너 공용 액세스 수준을 설정** 대화 상자에서 원하는 hello 액세스 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![공용 액세스 수준 옵션 설정][14]
6. <span data-ttu-id="18d69-201">**적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="18d69-202">blob 컨테이너의 blob 관리</span><span class="sxs-lookup"><span data-stu-id="18d69-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="18d69-203">Blob 컨테이너를 만든 후 blob toothat blob 컨테이너에 업로드 blob tooyour 로컬 컴퓨터에 다운로드을 로컬 컴퓨터에 더 많은 blob을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="18d69-204">단계를 수행 하는 hello를 toomanage blob 컨테이너 내의 blob (및 폴더)을 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="18d69-205">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="18d69-206">Hello 왼쪽된 창에서 원하는 toomanage hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="18d69-207">Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="18d69-208">원하는 tooview hello blob 컨테이너를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="18d69-209">hello 주 창에는 hello blob 컨테이너의 내용을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-209">hello main pane will display hello blob container's contents.</span></span>

   ![Blob 컨테이너 보기][3]
6. <span data-ttu-id="18d69-211">hello 주 창에는 hello blob 컨테이너의 내용을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="18d69-212">Tooperform 원하는 hello 작업에 따라 다음이 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="18d69-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="18d69-213">**파일 tooa blob 컨테이너를 업로드 합니다.**</span><span class="sxs-lookup"><span data-stu-id="18d69-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="18d69-214">Hello 주 창 도구 모음 선택 **업로드**, 차례로 **파일 업로드** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![파일 메뉴 업로드][15]
     2. <span data-ttu-id="18d69-216">Hello에 **파일 업로드** 대화 상자에서 선택 hello 줄임표 (**... **)의 hello hello 오른쪽 단추를 **파일** 텍스트 상자에 원하는 tooupload tooselect hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![파일 옵션 업로드][16]
     3. <span data-ttu-id="18d69-218">Hello 유형의 지정 **유형 Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="18d69-219">hello 문서 [.NET을 사용 하 여 Azure Blob 저장소 시작](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) 다양 한 blob 종류 hello hello 차이점에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="18d69-220">필요에 따라 hello 선택한 파일은 업로드 대상 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="18d69-221">Hello 대상 폴더가 존재 하지 않는 경우 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="18d69-222">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-222">Select **Upload**.</span></span>
   * <span data-ttu-id="18d69-223">**폴더 tooa blob 컨테이너를 업로드 합니다.**</span><span class="sxs-lookup"><span data-stu-id="18d69-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="18d69-224">Hello 주 창 도구 모음 선택 **업로드**, 차례로 **폴더 업로드** hello 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![폴더 메뉴 업로드][17]
     2. <span data-ttu-id="18d69-226">Hello에 **업로드 폴더** 대화 상자에서 선택 hello 줄임표 (**... **)의 hello hello 오른쪽 단추를 **폴더** 텍스트 상자 tooselect hello 내용을 폴더 tooupload 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![폴더 옵션 업로드][18]
     3. <span data-ttu-id="18d69-228">Hello 유형의 지정 **유형 Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="18d69-229">hello 문서 [.NET을 사용 하 여 Azure Blob 저장소 시작](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) 다양 한 blob 종류 hello hello 차이점에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="18d69-230">필요에 따라 어떤 hello에 선택한 폴더의 내용을 업로드할 수는 대상 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="18d69-231">Hello 대상 폴더가 존재 하지 않는 경우 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="18d69-232">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-232">Select **Upload**.</span></span>
   * <span data-ttu-id="18d69-233">**Blob tooyour 로컬 컴퓨터에 다운로드**</span><span class="sxs-lookup"><span data-stu-id="18d69-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="18d69-234">원하는 toodownload hello blob을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="18d69-235">Hello 주 창 도구 모음 선택 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="18d69-236">Hello에 **toosave hello blob를 다운로드 하는 위치 지정** 대화 상자에서 hello blob를 다운로드 한 저장할 hello 위치를 지정 하 고 toogive 이름 hello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="18d69-237">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-237">Select **Save**.</span></span>
   * <span data-ttu-id="18d69-238">**로컬 컴퓨터에서 blob 열기**</span><span class="sxs-lookup"><span data-stu-id="18d69-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="18d69-239">원하는 tooopen hello blob을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="18d69-240">Hello 주 창 도구 모음 선택 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="18d69-241">hello blob 다운로드 되 고 hello blob의 기본 파일 형식과 연결 된 hello 응용 프로그램을 사용 하 여 열립니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="18d69-242">**Blob toohello 클립보드에 복사**</span><span class="sxs-lookup"><span data-stu-id="18d69-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="18d69-243">원하는 toocopy hello blob을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="18d69-244">Hello 주 창 도구 모음 선택 **복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="18d69-245">Hello 왼쪽된 창에서 tooanother blob 컨테이너를 찾아 두 번 클릭 tooview hello 주 창에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="18d69-246">Hello 주 창 도구 모음 선택 **붙여넣기** toocreate hello blob의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="18d69-247">**Blob 삭제**</span><span class="sxs-lookup"><span data-stu-id="18d69-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="18d69-248">원하는 toodelete hello blob을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="18d69-249">Hello 주 창 도구 모음 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="18d69-250">선택 **예** toohello 확인 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="18d69-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18d69-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18d69-251">Next steps</span></span>
* <span data-ttu-id="18d69-252">보기 hello [최신 저장소 탐색기 (미리 보기) 릴리스 정보 및 비디오](http://www.storageexplorer.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="18d69-253">너무 방법에 대해 알아봅니다[Azure blob, 테이블, 큐 및 파일을 사용 하 여 응용 프로그램을 만들](https://azure.microsoft.com/documentation/services/storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="18d69-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
