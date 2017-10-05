---
title: "저장소 탐색기(미리 보기)를 사용하여 Azure Blob Storage 리소스 관리 | Microsoft Docs"
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
ms.openlocfilehash: f833027203441e12340bd93f3570de073d297223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="be5fe-103">저장소 탐색기(미리 보기)를 사용하여 Blob 저장소 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="be5fe-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="be5fe-104">개요</span><span class="sxs-lookup"><span data-stu-id="be5fe-104">Overview</span></span>
<span data-ttu-id="be5fe-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md)는 HTTP 또는 HTTPS를 통해 전 세계 어디에서든 액세스할 수 있는 다량의 구조화되지 않은 데이터(예: 텍스트 또는 이진 데이터)를 저장할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span>
<span data-ttu-id="be5fe-106">Blob 저장소를 사용하여 세상에 공개적으로 표시하거나 응용 프로그램 데이터를 비공개적으로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-106">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="be5fe-107">이 문서에서는 저장소 탐색기(미리 보기)를 사용하여 blob 컨테이너 및 blob 작업을 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-107">In this article, you'll learn how to use Storage Explorer (Preview) to work with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be5fe-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="be5fe-108">Prerequisites</span></span>
<span data-ttu-id="be5fe-109">이 문서의 단계를 완료하려면 다음과 같이 하는 것이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-109">To complete the steps in this article, you'll need the following:</span></span>

* [<span data-ttu-id="be5fe-110">저장소 탐색기(미리 보기) 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="be5fe-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="be5fe-111">Azure 저장소 계정 또는 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="be5fe-111">Connect to a Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="be5fe-112">Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="be5fe-112">Create a blob container</span></span>
<span data-ttu-id="be5fe-113">모든 blob은 단지 blob의 논리적 그룹화인 blob 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="be5fe-114">한 계정에 포함될 수 있는 컨테이너 수에 제한이 없으며, 각 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="be5fe-115">다음 단계에서는 저장소 탐색기(미리 보기) 내에서 blob 컨테이너를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-115">The following steps illustrate how to create a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="be5fe-116">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-117">왼쪽 창에서 blob 컨테이너를 만들고자 하는 곳의 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-117">In the left pane, expand the storage account within which you wish to create the blob container.</span></span>
3. <span data-ttu-id="be5fe-118">마우스 오른쪽 단추로 **Blob 컨테이너**를 클릭하고, 상황에 맞는 메뉴에서 **Blob 컨테이너 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-118">Right-click **Blob Containers**, and - from the context menu - select **Create Blob Container**.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 만들기][0]
4. <span data-ttu-id="be5fe-120">텍스트 상자가 **Blob 컨테이너** 폴더 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-120">A text box will appear below the **Blob Containers** folder.</span></span> <span data-ttu-id="be5fe-121">Blob 컨테이너에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-121">Enter the name for your blob container.</span></span> <span data-ttu-id="be5fe-122">Blob 컨테이너 이름 명명 규칙 및 제한 사항 목록은 [컨테이너 이름 명명 규칙](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="be5fe-122">See the [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Blob 컨테이너 텍스트 상자 만들기][1]
5. <span data-ttu-id="be5fe-124">Blob 컨테이너 만들기가 끝나면 **Enter** 키를 누르거나 **Esc** 키를 눌러 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-124">Press **Enter** when done to create the blob container, or **Esc** to cancel.</span></span> <span data-ttu-id="be5fe-125">Blob 컨테이너가 성공적으로 만들어졌다면 선택한 저장소 계정에 대해 **Blob 컨테이너** 폴더 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-125">Once the blob container has been successfully created, it will be displayed under the **Blob Containers** folder for the selected storage account.</span></span>

   ![만든 Blob 컨테이너][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="be5fe-127">Blob 컨테이너 내용 보기</span><span class="sxs-lookup"><span data-stu-id="be5fe-127">View a blob container's contents</span></span>
<span data-ttu-id="be5fe-128">Blob 컨테이너는 blob 및 폴더(blob도 포함할 수 있음)를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="be5fe-129">다음 단계에서는 저장소 탐색기(미리 보기) 내에서 blob 컨테이너 내용 보기 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-129">The following steps illustrate how to view the contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="be5fe-130">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-131">왼쪽 창에서 보려는 blob 컨테이너가 들어 있는 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-131">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="be5fe-132">저장소 계정의 **Blob 컨테이너**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-132">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="be5fe-133">마우스 오른쪽 단추로 보려는 Blob 컨테이너를 클릭하고, 상황에 맞는 메뉴에서 **Blob 컨테이너 편집기 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-133">Right-click the blob container you wish to view, and - from the context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="be5fe-134">또한 보려는 blob 컨테이너를 두 번 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-134">You can also double-click the blob container you wish to view.</span></span>

   ![blob 컨테이너 편집기 상황에 맞는 메뉴 열기][19]
5. <span data-ttu-id="be5fe-136">기본 창에 blob 컨테이너 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-136">The main pane will display the blob container's contents.</span></span>

   ![Blob 컨테이너 편집기][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="be5fe-138">Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="be5fe-138">Delete a blob container</span></span>
<span data-ttu-id="be5fe-139">필요에 따라 Blob 컨테이너를 쉽게 만들고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="be5fe-140">(개별 Blob 삭제 방법에 대한 자세한 내용은 [Blob 컨테이너의 Blob 관리](#managing-blobs-in-a-blob-container)섹션을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="be5fe-140">(To see how to delete individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="be5fe-141">다음 단계에서는 저장소 탐색기(미리 보기) 내에서 blob 컨테이너를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-141">The following steps illustrate how to delete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="be5fe-142">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-143">왼쪽 창에서 보려는 blob 컨테이너가 들어 있는 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-143">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="be5fe-144">저장소 계정의 **Blob 컨테이너**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-144">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="be5fe-145">마우스 오른쪽 단추로 삭제하려는 Blob 컨테이너를 클릭하고, 상황에 맞는 메뉴에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-145">Right-click the blob container you wish to delete, and - from the context menu - select **Delete**.</span></span>
   <span data-ttu-id="be5fe-146">또한 현재 선택된 blob 컨테이너를 삭제하려면 **삭제** 를 누를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-146">You can also press **Delete** to delete the currently selected blob container.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 삭제][4]
5. <span data-ttu-id="be5fe-148">확인 대화 상자에서 **확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-148">Select **Yes** to the confirmation dialog.</span></span>

   ![Blob 컨테이너 확인 삭제][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="be5fe-150">Blob 컨테이너 복사</span><span class="sxs-lookup"><span data-stu-id="be5fe-150">Copy a blob container</span></span>
<span data-ttu-id="be5fe-151">저장소 탐색기(미리 보기)를 사용하여 blob 컨테이너를 클립보드에 복사한 다음 다른 저장소 계정에 붙여넣기 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-151">Storage Explorer (Preview) enables you to copy a blob container to the clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="be5fe-152">(개별 Blob 복사 방법에 대한 자세한 내용은 [Blob 컨테이너의 Blob 관리](#managing-blobs-in-a-blob-container)섹션을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="be5fe-152">(To see how to copy individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="be5fe-153">다음 단계에서는 한 저장소 계정에서 다른 계정으로 blob 컨테이너를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-153">The following steps illustrate how to copy a blob container from one storage account to another.</span></span>

1. <span data-ttu-id="be5fe-154">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-155">왼쪽 창에서 복사하려는 blob 컨테이너가 들어 있는 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-155">In the left pane, expand the storage account containing the blob container you wish to copy.</span></span>
3. <span data-ttu-id="be5fe-156">저장소 계정의 **Blob 컨테이너**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-156">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="be5fe-157">마우스 오른쪽 단추로 복사하려는 Blob 컨테이너를 클릭하고, 상황에 맞는 메뉴에서 **Blob 컨테이너 복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-157">Right-click the blob container you wish to copy, and - from the context menu - select **Copy Blob Container**.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 복사][6]
5. <span data-ttu-id="be5fe-159">마우스 오른쪽 단추로 blob 컨테이너를 붙여 넣을 원하는 "대상" 저장소 계정을 클릭하고, 상황에 맞는 메뉴에서 **Blob 컨테이너 붙여넣기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-159">Right-click the desired "target" storage account into which you want to paste the blob container, and - from the context menu - select **Paste Blob Container**.</span></span>

   ![Blob 컨테이너 상황에 맞는 메뉴 붙여넣기][7]

## <a name="get-the-sas-for-a-blob-container"></a><span data-ttu-id="be5fe-161">Blob 컨테이너에 대한 SAS 가져오기</span><span class="sxs-lookup"><span data-stu-id="be5fe-161">Get the SAS for a blob container</span></span>
<span data-ttu-id="be5fe-162">[SAS(공유 액세스 서명)](storage/common/storage-dotnet-shared-access-signature-part-1.md)는 저장소 계정의 리소스에 대한 위임된 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access to resources in your storage account.</span></span>
<span data-ttu-id="be5fe-163">즉, 계정 액세스 키를 공유할 필요 없이 지정된 권한 집합을 사용하여 지정된 기간 동안 클라이언트에게 저장소 계정의 개체에 대한 제한된 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-163">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="be5fe-164">다음 단계에서는 Blob 컨테이너에 대한 SAS를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-164">The following steps illustrate how to create a SAS for a blob container:</span></span>

1. <span data-ttu-id="be5fe-165">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-166">왼쪽 창에서 SAS 가져오기를 하려는 blob 컨테이너가 들어 있는 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-166">In the left pane, expand the storage account containing the blob container for which you wish to get a SAS.</span></span>
3. <span data-ttu-id="be5fe-167">저장소 계정의 **Blob 컨테이너**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-167">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="be5fe-168">마우스 오른쪽 단추로 원하는 blob 컨테이너를 클릭하고, 상황에 맞는 메뉴에서 **공유 액세스 서명 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-168">Right-click the desired blob container, and - from the context menu - select **Get Shared Access Signature**.</span></span>

   ![SAS 상황에 맞는 메뉴 가져오기][8]
5. <span data-ttu-id="be5fe-170">**공유 액세스 서명** 대화 상자에서 정책, 시작 및 만료 날짜, 표준 시간대, 리소스에 적용할 액세스 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-170">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

   ![SAS 옵션 가져오기][9]
6. <span data-ttu-id="be5fe-172">SAS 옵션 지정하기를 마치면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-172">When you're finished specifying the SAS options, select **Create**.</span></span>
7. <span data-ttu-id="be5fe-173">Blob 컨테이너와 함께 저장소 리소스에 액세스하는 데 사용할 수 있는 URL 및 쿼리 문자열이 나열되는 두 번째 **공유 액세스 서명** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-173">A second **Shared Access Signature** dialog will then display that lists the blob container along with the URL and QueryStrings you can use to access the storage resource.</span></span>
   <span data-ttu-id="be5fe-174">클립보드에 복사할 URL 옆에 있는 **복사** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-174">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>

   ![SAS Url 복사][10]
8. <span data-ttu-id="be5fe-176">완료되면 **닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="be5fe-177">Blob 컨테이너에 대한 액세스 정책 관리</span><span class="sxs-lookup"><span data-stu-id="be5fe-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="be5fe-178">다음 단계에서는 Blob 컨테이너에 대한 액세스 정책을 관리(추가 및 제거)하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-178">The following steps illustrate how to manage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="be5fe-179">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-180">왼쪽 창에서 액세스 정책을 관리하려는 blob 컨테이너가 들어 있는 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-180">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="be5fe-181">저장소 계정의 **Blob 컨테이너**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-181">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="be5fe-182">원하는 blob 컨테이너를 선택하고, 상황에 맞는 메뉴에서 **액세스 정책 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-182">Select the desired blob container, and - from the context menu - select **Manage Access Policies**.</span></span>

   ![액세스 정책 상황에 맞는 메뉴 관리][11]
5. <span data-ttu-id="be5fe-184">**액세스 정책** 대화 상자는 선택된 blob 컨테이너에 대해 이미 만들어진 모든 액세스 정책을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-184">The **Access Policies** dialog will list any access policies already created for the selected blob container.</span></span>

   ![액세스 정책 옵션][12]        
6. <span data-ttu-id="be5fe-186">액세스 정책 관리 작업에 따라 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="be5fe-186">Follow these steps depending on the access policy management task:</span></span>

   * <span data-ttu-id="be5fe-187">**새 액세스 정책 추가** - **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="be5fe-188">생성되었다면 **액세스 정책** 대화 상자는 (기본 설정을 사용하여) 새로 추가된 액세스 정책을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-188">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="be5fe-189">**액세스 정책 편집** -원하는 편집을 모두 마치고, **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="be5fe-190">**액세스 정책 제거** - 제거하려는 액세스 정책 옆에 있는 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-190">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

## <a name="set-the-public-access-level-for-a-blob-container"></a><span data-ttu-id="be5fe-191">Blob 컨테이너에 대한 공용 액세스 수준 설정</span><span class="sxs-lookup"><span data-stu-id="be5fe-191">Set the Public Access Level for a blob container</span></span>
<span data-ttu-id="be5fe-192">기본적으로 모든 blob 컨테이너는 “공용 액세스 없음”으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-192">By default, every blob container is set to "No public access".</span></span>

<span data-ttu-id="be5fe-193">다음 단계에서는 Blob 컨테이너에 대한 공용 액세스 수준을 지정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-193">The following steps illustrate how to specify a public access level for a blob container.</span></span>

1. <span data-ttu-id="be5fe-194">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-195">왼쪽 창에서 액세스 정책을 관리하려는 blob 컨테이너가 들어 있는 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-195">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="be5fe-196">저장소 계정의 **Blob 컨테이너**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-196">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="be5fe-197">원하는 blob 컨테이너를 선택하고, 상황에 맞는 메뉴에서 **공용 액세스 수준 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-197">Select the desired blob container, and - from the context menu - select **Set Public Access Level**.</span></span>

   ![공용 액세스 수준 상황에 맞는 메뉴 설정][13]
5. <span data-ttu-id="be5fe-199">**컨테이너 공용 액세스 수준 설정** 대화 상자에서 원하는 액세스 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-199">In the **Set Container Public Access Level** dialog, specify the desired access level.</span></span>

   ![공용 액세스 수준 옵션 설정][14]
6. <span data-ttu-id="be5fe-201">**적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="be5fe-202">blob 컨테이너의 blob 관리</span><span class="sxs-lookup"><span data-stu-id="be5fe-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="be5fe-203">Blob 컨테이너를 만들었다면 blob 컨테이너에 blob 업로드, 로컬 컴퓨터에 blob 다운로드, 로컬 컴퓨터에서 blob 열기 등 많은 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-203">Once you've created a blob container, you can upload a blob to that blob container, download a blob to your local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="be5fe-204">다음 단계에서는 Blob 컨테이너 내에서 blobs (및 폴더)를 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-204">The following steps illustrate how to manage the blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="be5fe-205">저장소 탐색기(미리 보기)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="be5fe-206">왼쪽 창에서 관리하려는 blob 컨테이너가 들어 있는 저장소 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-206">In the left pane, expand the storage account containing the blob container you wish to manage.</span></span>
3. <span data-ttu-id="be5fe-207">저장소 계정의 **Blob 컨테이너**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-207">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="be5fe-208">보려는 blob 컨테이너를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-208">Double-click the blob container you wish to view.</span></span>
5. <span data-ttu-id="be5fe-209">기본 창에 blob 컨테이너 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-209">The main pane will display the blob container's contents.</span></span>

   ![Blob 컨테이너 보기][3]
6. <span data-ttu-id="be5fe-211">기본 창에 blob 컨테이너 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-211">The main pane will display the blob container's contents.</span></span>
7. <span data-ttu-id="be5fe-212">수행하려는 작업에 따라서 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="be5fe-212">Follow these steps depending on the task you wish to perform:</span></span>

   * <span data-ttu-id="be5fe-213">**Blob 컨테이너에 파일 업로드**</span><span class="sxs-lookup"><span data-stu-id="be5fe-213">**Upload files to a blob container**</span></span>

     1. <span data-ttu-id="be5fe-214">기본 창 도구 모음에서 **업로드**를 선택하고, 드롭 다운 메뉴에서 **파일 업로드**를 합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-214">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![파일 메뉴 업로드][15]
     2. <span data-ttu-id="be5fe-216">**파일 업로드** 대화 상자에서 **파일** 텍스트 상자 오른쪽에 있는 줄임표(**…**) 단추를 선택하여 업로드할 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-216">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![파일 옵션 업로드][16]
     3. <span data-ttu-id="be5fe-218">**Blob 유형**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-218">Specify the type of **Blob type**.</span></span> <span data-ttu-id="be5fe-219">[.NET을 사용하여 Azure Blob 저장소 시작](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) 문서는 다양한 Blob 유형 간의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-219">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="be5fe-220">필요에 따라 선택한 파일을 업로드할 대상 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-220">Optionally, specify a target folder into which the selected file(s) will be uploaded.</span></span> <span data-ttu-id="be5fe-221">대상 폴더가 없다면 폴더가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-221">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="be5fe-222">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-222">Select **Upload**.</span></span>
   * <span data-ttu-id="be5fe-223">**Blob 컨테이너에 폴더 업로드**</span><span class="sxs-lookup"><span data-stu-id="be5fe-223">**Upload a folder to a blob container**</span></span>

     1. <span data-ttu-id="be5fe-224">기본 창 도구 모음에서 **업로드**를 선택하고, 드롭 다운 메뉴에서 **폴더 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-224">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![폴더 메뉴 업로드][17]
     2. <span data-ttu-id="be5fe-226">**폴더 업로드** 대화 상자에서 **폴더** 텍스트 상자 오른쪽에 있는 줄임표(**…**) 단추를 선택하여 내용을 업로드할 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-226">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        ![폴더 옵션 업로드][18]
     3. <span data-ttu-id="be5fe-228">**Blob 유형**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-228">Specify the type of **Blob type**.</span></span> <span data-ttu-id="be5fe-229">[.NET을 사용하여 Azure Blob 저장소 시작](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) 문서는 다양한 Blob 유형 간의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-229">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="be5fe-230">필요에 따라 선택한 폴더 내용을 업로드할 대상 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-230">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="be5fe-231">대상 폴더가 없다면 폴더가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-231">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="be5fe-232">**업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-232">Select **Upload**.</span></span>
   * <span data-ttu-id="be5fe-233">**로컬 컴퓨터에 blob 다운로드**</span><span class="sxs-lookup"><span data-stu-id="be5fe-233">**Download a blob to your local computer**</span></span>

     1. <span data-ttu-id="be5fe-234">다운로드하려는 blob을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-234">Select the blob you wish to download.</span></span>
     2. <span data-ttu-id="be5fe-235">기본 창 도구 모음에서 **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-235">On the main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="be5fe-236">**다운로드한 blob을 저장할 위치 지정** 대화 상자에서 blob을 다운로드할 위치와 명명하려는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-236">In the **Specify where to save the downloaded blob** dialog, specify the location where you want the blob downloaded, and the name you wish to give it.</span></span>  
     4. <span data-ttu-id="be5fe-237">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-237">Select **Save**.</span></span>
   * <span data-ttu-id="be5fe-238">**로컬 컴퓨터에서 blob 열기**</span><span class="sxs-lookup"><span data-stu-id="be5fe-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="be5fe-239">열려는 blob을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-239">Select the blob you wish to open.</span></span>
     2. <span data-ttu-id="be5fe-240">기본 창 도구 모음에서 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-240">On the main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="be5fe-241">Blob은 blob의 기본 파일 형식과 연결된 응용 프로그램을 사용하여 다운로드하고 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-241">The blob will be downloaded and opened using the application associated with the blob's underlying file type.</span></span>
   * <span data-ttu-id="be5fe-242">**blob을 클립보드에 복사**</span><span class="sxs-lookup"><span data-stu-id="be5fe-242">**Copy a blob to the clipboard**</span></span>

     1. <span data-ttu-id="be5fe-243">복사하려는 blob을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-243">Select the blob you wish to copy.</span></span>
     2. <span data-ttu-id="be5fe-244">기본 창 도구 모음에서 **복사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-244">On the main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="be5fe-245">왼쪽 창에서 또 다른 blob 컨테이너로 이동하고 기본 창에서 보려면 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-245">In the left pane, navigate to another blob container, and double-click it to view it in the main pane.</span></span>
     4. <span data-ttu-id="be5fe-246">기본 창 도구 모음에서 blob의 복사본을 만들려면 **붙여넣기** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-246">On the main pane's toolbar, select **Paste** to create a copy of the blob.</span></span>
   * <span data-ttu-id="be5fe-247">**Blob 삭제**</span><span class="sxs-lookup"><span data-stu-id="be5fe-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="be5fe-248">삭제하려는 blob을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-248">Select the blob you wish to delete.</span></span>
     2. <span data-ttu-id="be5fe-249">기본 창 도구 모음에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-249">On the main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="be5fe-250">확인 대화 상자에서 **확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be5fe-250">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be5fe-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="be5fe-251">Next steps</span></span>
* <span data-ttu-id="be5fe-252">[최신 저장소 탐색기(미리 보기) 릴리스 정보 및 비디오](http://www.storageexplorer.com)를 보세요.</span><span class="sxs-lookup"><span data-stu-id="be5fe-252">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="be5fe-253">[Azure blob, 테이블, 큐 및 파일을 사용하여 응용 프로그램을 작성](https://azure.microsoft.com/documentation/services/storage/)하는 방법 알아보기.</span><span class="sxs-lookup"><span data-stu-id="be5fe-253">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

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
