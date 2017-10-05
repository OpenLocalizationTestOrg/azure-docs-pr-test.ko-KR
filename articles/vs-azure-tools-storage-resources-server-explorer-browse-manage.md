---
title: "서버 탐색기로 저장소 리소스 찾아보기 및 관리 | Microsoft Docs"
description: "서버 탐색기로 저장소 리소스 찾아보기 및 관리"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: 43ab501c69c0c1e3271dbfcf08e5342a3507ab82
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a><span data-ttu-id="85b41-103">서버 탐색기로 저장소 리소스 찾아보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="85b41-103">Browsing and Managing Storage Resources with Server Explorer</span></span>
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a><span data-ttu-id="85b41-104">개요</span><span class="sxs-lookup"><span data-stu-id="85b41-104">Overview</span></span>
<span data-ttu-id="85b41-105">Microsoft Visual Studio용 Azure 도구를 설치한 경우 Azure 저장소 계정에서 Blob, 큐, 테이블 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-105">If you've installed the Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span></span> <span data-ttu-id="85b41-106">서버 탐색기의 Azure 저장소 노드는 로컬 저장소 에뮬레이터 계정 및 다른 Azure 저장소 계정에 있는 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-106">The Azure Storage node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span></span>

<span data-ttu-id="85b41-107">Visual Studio에서 서버 탐색기를 보려면, 메뉴 모음에서 **보기**, **서버 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-107">To view Server Explorer in Visual Studio, on the menu bar, choose **View**, **Server Explorer**.</span></span> <span data-ttu-id="85b41-108">저장소 노드는 연결된 Azure 구독/인증서 아래에 존재하는 모든 저장소 계정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-108">The storage node shows all of the storage accounts that exist under each Azure subscription/certificate you're connected to.</span></span> <span data-ttu-id="85b41-109">저장소 계정이 나타나지 않으면 [이 항목의 뒷부분에 나오는](#add-storage-accounts-by-using-server-explorer)다음의 지침을 따라 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-109">If your storage account doesn't appear, you can add it by following the instructions [later in this topic](#add-storage-accounts-by-using-server-explorer).</span></span>

<span data-ttu-id="85b41-110">Azure SDK 2.7부터 새로운 클라우드 탐색기를 사용해 Azure 리소스를 확인 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-110">Starting in Azure SDK 2.7, you can also use the new Cloud Explorer to view and manage your Azure resources.</span></span> <span data-ttu-id="85b41-111">자세한 내용은 [클라우드 탐색기를 사용하여 Azure 리소스 관리](vs-azure-tools-resources-managing-with-cloud-explorer.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-111">See [Managing Azure Resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) for more information.</span></span>

## <a name="view-and-manage-storage-resources-in-visual-studio"></a><span data-ttu-id="85b41-112">Visual Studio에서 저장소 리소스를 확인 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-112">View and manage storage resources in Visual Studio</span></span>
<span data-ttu-id="85b41-113">서버 탐색기는 저장소 에뮬레이터 계정에 있는 Blob, 큐, 테이블 목록을 자동으로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span></span> <span data-ttu-id="85b41-114">저장소 에뮬레이터 계정은 저장소 노드의 서버 탐색기에 **개발** 노드로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-114">The storage emulator account is listed in Server Explorer under the Storage node as the **Development** node.</span></span>

<span data-ttu-id="85b41-115">저장소 에뮬레이터 계정의 리소스를 보려면 **개발** 노드를 확장하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-115">To see the storage emulator account’s resources, expand the **Development** node.</span></span> <span data-ttu-id="85b41-116">**개발** 노드를 확장했을 때 저장소 에뮬레이터가 시작하지 않으면, 자동으로 시작될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-116">If the storage emulator hasn’t been started when you expand the **Development** node, it will automatically start.</span></span> <span data-ttu-id="85b41-117">이 작업은 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-117">This can take several seconds.</span></span> <span data-ttu-id="85b41-118">저장소 에뮬레이터가 시작하는 동안 Visual Studio의 다른 영역에서 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-118">You can continue to work in other areas of Visual Studio while the storage emulator starts.</span></span>

<span data-ttu-id="85b41-119">저장소 계정의 리소스를 보려면 서버 탐색기에서 저장소 계정의 노드를 확장하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-119">To view resources in a storage account, expand the storage account’s node in Server Explorer.</span></span> <span data-ttu-id="85b41-120">다음의 하위 노드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-120">The following sub-nodes appear:</span></span>

* <span data-ttu-id="85b41-121">Blob</span><span class="sxs-lookup"><span data-stu-id="85b41-121">Blobs</span></span>
* <span data-ttu-id="85b41-122">큐</span><span class="sxs-lookup"><span data-stu-id="85b41-122">Queues</span></span>
* <span data-ttu-id="85b41-123">테이블</span><span class="sxs-lookup"><span data-stu-id="85b41-123">Tables</span></span>

## <a name="work-with-blob-resources"></a><span data-ttu-id="85b41-124">Blob 리소스로 작업</span><span class="sxs-lookup"><span data-stu-id="85b41-124">Work with Blob Resources</span></span>
<span data-ttu-id="85b41-125">Blob 노드는 선택된 저장소 계정의 컨테이너 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-125">The Blobs node displays a list of containers for the selected storage account.</span></span> <span data-ttu-id="85b41-126">Blob 컨테이너는 Blob 파일을 포함하고 있으며 이러한 Blob을 폴더와 하위 폴더로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-126">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span></span> <span data-ttu-id="85b41-127">자세한 내용은 [.NET에서 Blob 저장소를 사용하는 방법](storage/blobs/storage-dotnet-how-to-use-blobs.md) (영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-127">See [How to use Blob Storage from .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information.</span></span>

### <a name="to-create-a-blob-container"></a><span data-ttu-id="85b41-128">Blob 컨테이너를 생성하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-128">To create a blob container</span></span>
1. <span data-ttu-id="85b41-129">**Blob** 노드에 대한 바로 가기 메뉴를 열고 **Blob 컨테이너 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-129">Open the shortcut menu for the **Blobs** node, and then choose **Create Blob Container**.</span></span>
2. <span data-ttu-id="85b41-130">**Blob 컨테이너 만들기** 대화 상자에서 새 컨테이너 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-130">In the **Create Blob Container** dialog box, enter the name of the new container.</span></span>  
3. <span data-ttu-id="85b41-131">키보드에서 **Enter** 키를 누르거나 이름 필드 외부를 클릭하거나 탭하여 Blob 컨테이너를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-131">Press **ENTER** on your keyboard or you can click or tap outside of the name field to save the blob container.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="85b41-132">Blob 컨테이너 이름은 숫자 (0-9) 또는 소문자 (a-z)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-132">The blob container name must begin with a number (0-9) or lowercase letter (a-z).</span></span>
   > 
   > 

### <a name="to-delete-a-blob-container"></a><span data-ttu-id="85b41-133">Blob 컨테이너를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-133">To delete a blob container</span></span>
* <span data-ttu-id="85b41-134">제거하려는 Blob 컨테이너에 대한 바로 가기 메뉴를 열고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-134">Open the shortcut menu for the blob container you want to remove and then choose **Delete**.</span></span>

### <a name="to-display-a-list-of-the-items-contained-in-a-blob-container"></a><span data-ttu-id="85b41-135">Blob 컨테이너에 포함된 항목의 목록을 표시하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-135">To display a list of the items contained in a blob container</span></span>
* <span data-ttu-id="85b41-136">목록에서 Blob 컨테이너 이름의 바로 가기 메뉴를 연 다음 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-136">Open the shortcut menu for a blob container name in the list and then choose **Open**.</span></span>
  
    <span data-ttu-id="85b41-137">Blob 컨테이너의 내용은 Blob 컨테이너 보기라는 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-137">When you view the contents of a blob container, it appears in a tab known as the blob container view.</span></span>
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    <span data-ttu-id="85b41-139">Blob 컨테이너 보기의 오른쪽에 있는 단추를 사용하여 Blob에서 다음의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-139">You can perform the following operations on blobs by using the buttons in the top-right corner of the blob container view:</span></span>
  
  * <span data-ttu-id="85b41-140">필터 값을 입력 및 적용하기</span><span class="sxs-lookup"><span data-stu-id="85b41-140">Enter a filter value and apply it</span></span>
  * <span data-ttu-id="85b41-141">컨테이너의 Blob 목록 새로 고침</span><span class="sxs-lookup"><span data-stu-id="85b41-141">Refresh the list of blobs in the container</span></span>
  * <span data-ttu-id="85b41-142">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="85b41-142">Upload a file</span></span>
  * <span data-ttu-id="85b41-143">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="85b41-143">Delete a blob</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="85b41-144">Blob 컨테이너에서 파일을 삭제해도 기본 파일은 삭제되지 않으며, 해당 Blob 컨테이너에서만 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-144">Deleting a file from a blob container doesn’t delete the underlying file; it only removes it from the blob container.</span></span>
    > 
    > 
  * <span data-ttu-id="85b41-145">Blob 열기</span><span class="sxs-lookup"><span data-stu-id="85b41-145">Open a blob</span></span>
  * <span data-ttu-id="85b41-146">로컬 컴퓨터에 Blob 저장</span><span class="sxs-lookup"><span data-stu-id="85b41-146">Save a blob to the local computer</span></span>

### <a name="to-create-a-folder-or-subfolder-in-a-blob-container"></a><span data-ttu-id="85b41-147">Blob 컨테이너에 폴더 또는 하위 폴더를 만들려면</span><span class="sxs-lookup"><span data-stu-id="85b41-147">To create a folder or subfolder in a blob container</span></span>
1. <span data-ttu-id="85b41-148">클라우드 탐색기에서 Blob 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-148">Choose the blob container in Cloud Explorer.</span></span> <span data-ttu-id="85b41-149">컨테이너 창에서 **Blob 업로드** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-149">In the container window, choose the **Upload Blob** button.</span></span>
   
    ![Blob 폴더에 파일 업로드하기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. <span data-ttu-id="85b41-151">**새 파일 업로드** 대화 상자에서 **찾아보기** 단추를 선택하여 업로드하려는 파일을 지정한 후 **폴더(선택 사항)** 상자에 폴더 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-151">In the **Upload New File** dialog box, choose the **Browse** button to specify the file you want to upload, and then enter a folder name in the **Folder (optional)** box.</span></span>
   
    <span data-ttu-id="85b41-152">동일한 절차를 수행하여 컨테이너 폴더에 하위 폴더를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-152">You can add subfolders in container folders by following the same procedure.</span></span> <span data-ttu-id="85b41-153">폴더 이름을 지정하지 않으면 파일은 Blob 컨테이너의 최상위 수준으로 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-153">If you don’t specify a folder name, the file will be uploaded to the top level of the blob container.</span></span> <span data-ttu-id="85b41-154">파일은 컨테이너의 지정된 폴더에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-154">The file appears in the specified folder in the container.</span></span>
   
    ![Blob 컨테이너에 폴더 추가하기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. <span data-ttu-id="85b41-156">폴더를 두 번 클릭하거나 Enter 키를 눌러 폴더의 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-156">Double-click the folder or press ENTER to see the contents of the folder.</span></span> <span data-ttu-id="85b41-157">컨테이너 폴더에 있는 경우 **부모 디렉터리 열기** (위쪽 화살표) 단추를 선택하여 컨테이너의 루트로 다시 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-157">When you’re in the container’s folder, you can navigate back to the root of the container by choosing the **Open Parent Directory** (up arrow) button.</span></span>

### <a name="to-delete-a-container-folder"></a><span data-ttu-id="85b41-158">컨테이너 폴더를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-158">To delete a container folder</span></span>
* <span data-ttu-id="85b41-159">폴더의 파일을 모두 삭제합니다</span><span class="sxs-lookup"><span data-stu-id="85b41-159">Delete all of the files in the folder</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="85b41-160">Blob 컨테이너의 폴더는 가상 폴더이기 때문에 빈 폴더를 만들거나 파일 내용을 삭제하기 위해 폴더를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-160">Because folders in blob containers are virtual folders, you can’t create an empty folder, nor can you delete a folder to delete its file contents.</span></span> <span data-ttu-id="85b41-161">폴더를 삭제하려면 폴더의 전체 내용을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-161">You have to delete the entire contents of a folder to delete the folder.</span></span>
  > 
  > 

### <a name="to-filter-blobs-in-a-container"></a><span data-ttu-id="85b41-162">컨테이너의 Blob를 필터링하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-162">To filter blobs in a container</span></span>
<span data-ttu-id="85b41-163">공통 접두사를 지정하여 표시되는 Blob를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-163">You can filter the blobs that are displayed by specifying a common prefix.</span></span>

<span data-ttu-id="85b41-164">예를 들어 필터 텍스트 상자에 접두사 `hello`를 입력한 후 **실행**(**!**) 단추를 선택하면 ‘hello’로 시작하는 Blob만 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-164">For example, if you enter the prefix `hello` in the filter text box and then choose the **Execute** (**!**)button, only blobs that begin with 'hello' appear.</span></span>

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> <span data-ttu-id="85b41-166">필터 필드는 대/소문자를 구분하며 와일드카드 문자 필터링을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-166">The filter field is case-sensitive and doesn’t support filtering with wildcard characters.</span></span> <span data-ttu-id="85b41-167">Blob은 접두사로만 필터링될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-167">Blobs can only be filtered by prefix.</span></span> <span data-ttu-id="85b41-168">구분 기호를 사용하여 가상 계층에 Blob을 구성하는 경우 접두사는 구분 기호를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-168">The prefix may include a delimiter if you are using a delimiter to organize blobs in a virtual hierarchy.</span></span> <span data-ttu-id="85b41-169">예를 들어, HelloFabric/ 접두사로 시작하는 필터링은 해당 문자열로 시작하는 모든 Blob을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-169">For example, filtering on the prefix HelloFabric/ returns all blobs beginning with that string.</span></span>
> 
> 

### <a name="to-download-blob-data"></a><span data-ttu-id="85b41-170">Blob 데이터를 다운로드하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-170">To download blob data</span></span>
* <span data-ttu-id="85b41-171">**클라우드 탐색기**에서 하나 이상의 Blob에 대한 바로 가기 메뉴를 열고 **열기**를 선택하거나, Blob 이름을 선택한 후 **열기** 단추를 선택하거나, Blob 이름을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-171">In **Cloud Explorer**, open the shortcut menu for one or more blobs and then choose **Open**, or choose the blob name and then choose the **Open** button, or double-click the blob name.</span></span>
  
    <span data-ttu-id="85b41-172">Blob 다운로드 진행률이 **Azure 활동 로그** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-172">The progress of a blob download appears in the **Azure Activity Log** window.</span></span>
  
    <span data-ttu-id="85b41-173">Blob는 해당 파일 형식에 대한 기본 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-173">The blob opens in the default editor for that file type.</span></span> <span data-ttu-id="85b41-174">운영 체제가 파일 형식을 인식하는 경우 파일은 로컬에 설치된 응용 프로그램에서 열립니다. 그렇지 않은 경우 Blob의 파일 형식에 대한 적절한 응용 프로그램을 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-174">If the operating system recognizes the file type, the file opens in a locally installed application; otherwise, you're prompted to choose an application that’s appropriate for the file type of the blob.</span></span> <span data-ttu-id="85b41-175">Blob을 다운로드할 때 생성되는 로컬 파일은 읽기 전용으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-175">The local file that’s created when you download a blob is marked as read-only.</span></span>
  
    <span data-ttu-id="85b41-176">Blob 데이터는 로컬로 캐시되고 Blob 서비스에서 Blob의 마지막 수정된 시간에 대해 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-176">Blob data is cached locally and checked against the blob's last modified time in the Blob service.</span></span> <span data-ttu-id="85b41-177">Blob이 마지막으로 다운로드된 후에 업데이트 된 경우 다시 다운로드됩니다. 그렇지 않은 경우 Blob은 로컬 디스크에서 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-177">If the blob has been updated since it was last downloaded, it will be downloaded again; otherwise, the blob will be loaded from the local disk.</span></span> <span data-ttu-id="85b41-178">기본적으로 Blob은 임시 디렉터리에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-178">By default, a blob is downloaded to a temporary directory.</span></span> <span data-ttu-id="85b41-179">특정 디렉터리에 Blob을 다운로드하려면 선택한 Blob 이름에 대한 바로 가기 메뉴를 열고 **다른 이름으로 저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-179">To download blobs to a specific directory, open the shortcut menu for the selected blob names and choose **Save As**.</span></span> <span data-ttu-id="85b41-180">이 방식으로 Blob을 저장하면 Blob 파일이 열리지 않으며, 로컬 파일이 읽기/쓰기 특성으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-180">When you save a blob in this manner, the blob file is not opened, and the local file is created with read-write attributes.</span></span>

### <a name="to-upload-blobs"></a><span data-ttu-id="85b41-181">Blob을 업로드하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-181">To upload blobs</span></span>
* <span data-ttu-id="85b41-182">Blob 컨테이너 보기에서 컨테이너가 열려 있을 때 **Blob 업로드** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-182">Choose the **Upload Blob** button when the container is open for viewing in the blob container view.</span></span>
  
    <span data-ttu-id="85b41-183">하나 이상의 파일을 선택해 업로드할 수 있으며 모든 형식의 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-183">You can choose one or more files to upload and you can upload files of any type.</span></span> <span data-ttu-id="85b41-184">**Azure 활동 로그** 에 업로드 진행률이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-184">The **Azure Activity Log** shows the progress of the upload.</span></span> <span data-ttu-id="85b41-185">Blob 데이터 작업 방법에 대한 자세한 내용은 [.NET에서 Azure Blob 저장소 서비스를 사용하는 방법](http://go.microsoft.com/fwlink/p/?LinkId=267911)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-185">For more information about how to work with blob data, see [How to use the Azure Blob Storage Service in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span></span>

### <a name="to-view-logs-transferred-to-blobs"></a><span data-ttu-id="85b41-186">Blob에 전송된 로그를 보려면</span><span class="sxs-lookup"><span data-stu-id="85b41-186">To view logs transferred to blobs</span></span>
* <span data-ttu-id="85b41-187">Azure 진단을 사용하여 Azure 응용 프로그램에서 데이터를 기록하고 저장소 계정에 로그를 전송하는 경우 이러한 로그에 대해 Azure에서 만들어진 컨테이너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-187">If you are using Azure Diagnostics to log data from your Azure application and you have transferred logs to your storage account, you’ll see containers that were created by Azure for these logs.</span></span> <span data-ttu-id="85b41-188">서버 탐색기에서 이러한 로그를 확인하는 것은 특히 Azure에 배포된 경우 응용 프로그램에 대한 문제를 식별하는 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-188">Viewing these logs in Server Explorer is an easy way to identify problems with your application, especially if it’s been deployed to Azure.</span></span> <span data-ttu-id="85b41-189">Azure 진단에 대한 자세한 내용은 [Azure 진단을 사용하여 로깅 데이터 수집](https://msdn.microsoft.com/library/azure/gg433048.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-189">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span></span>

### <a name="to-get-the-url-for-a-blob"></a><span data-ttu-id="85b41-190">Blob에 대한 URL을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="85b41-190">To get the URL for a blob</span></span>
* <span data-ttu-id="85b41-191">Blob의 바로 가기 메뉴를 열고 **URL 복사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-191">Open the blob’s shortcut menu and then choose **Copy URL**.</span></span>

### <a name="to-edit-a-blob"></a><span data-ttu-id="85b41-192">Blob을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-192">To edit a blob</span></span>
* <span data-ttu-id="85b41-193">Blob을 선택한 다음 **Blob 열기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-193">Select the blob and then choose the **Open Blob** button.</span></span>
  
    <span data-ttu-id="85b41-194">파일은 임시 위치로 다운로드되고 로컬 컴퓨터에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-194">The file is downloaded to a temporary location and opened on the local computer.</span></span> <span data-ttu-id="85b41-195">변경한 후 다시 Blob을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-195">You must upload the blob again after you make changes.</span></span>

## <a name="work-with-queue-resources"></a><span data-ttu-id="85b41-196">큐 리소스로 작업</span><span class="sxs-lookup"><span data-stu-id="85b41-196">Work with Queue Resources</span></span>
<span data-ttu-id="85b41-197">저장소 서비스 큐는 Azure 저장소 계정에서 호스팅되며 클라우드 서비스 역할이 메시지 전달 메커니즘에 의해 서로 및 다른 서비스와 통신할 수 있도록 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-197">Storage services queues are hosted in an Azure storage account and you can use them to allow your cloud service roles to communicate with each other and with other services by a message passing mechanism.</span></span> <span data-ttu-id="85b41-198">클라우드 서비스 및 외부 클라이언트에 대한 웹 서비스를 통해 프로그래밍 방식으로 큐에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-198">You can access the queue programmatically through a cloud service and over a web service for external clients.</span></span> <span data-ttu-id="85b41-199">또한 Visual Studio에서 서버 탐색기를 사용하여 직접 큐에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-199">You can also access the queue directly by using Server Explorer in Visual Studio.</span></span>

<span data-ttu-id="85b41-200">큐를 사용하는 클라우드 서비스를 개발할 때 Visual Studio를 사용하여 큐를 생성하여 코드를 개발 및 테스트하는 동안 대화형으로 작업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-200">When you develop a cloud service that uses queues, you might want to use Visual Studio to create queues and work with them interactively while you develop and test your code.</span></span>

<span data-ttu-id="85b41-201">서버 탐색기에서는 저장소 계정의 큐 보기, 큐 생성 및 삭제, 큐를 열어 메시지 보기, 큐에 메시지 추가하기가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-201">In Server Explorer, you can view the queues in a storage account, create and delete queues, open a queue to view its messages, and add messages to a queue.</span></span> <span data-ttu-id="85b41-202">큐를 확인하기 위해 열 때 개별 메시지를 볼 수 있으며 왼쪽 위의 단추를 사용하여 큐에서 다음의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-202">When you open a queue for viewing, you can view the individual messages, and you can perform the following actions on the queue by using the buttons in the top-left corner:</span></span>

* <span data-ttu-id="85b41-203">큐 보기 새로 고침</span><span class="sxs-lookup"><span data-stu-id="85b41-203">Refresh the view of the queue</span></span>
* <span data-ttu-id="85b41-204">큐에 메시지 추가</span><span class="sxs-lookup"><span data-stu-id="85b41-204">Add a message to the queue</span></span>
* <span data-ttu-id="85b41-205">최상위 메시지를 큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="85b41-205">Dequeue the topmost message</span></span>
* <span data-ttu-id="85b41-206">전체 큐 지우기</span><span class="sxs-lookup"><span data-stu-id="85b41-206">Clear the entire queue</span></span>

<span data-ttu-id="85b41-207">다음 그림에서는 두 개의 메시지를 포함하는 큐를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-207">The following image shows a queue that contains two messages.</span></span>

![큐 보기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

<span data-ttu-id="85b41-209">저장소 서비스 큐에 대한 자세한 내용은 [큐 저장소 서비스를 사용하는 방법](http://go.microsoft.com/fwlink/?LinkID=264702)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-209">For more information about storage services queues, see [How to: Use the Queue Storage Service](http://go.microsoft.com/fwlink/?LinkID=264702).</span></span> <span data-ttu-id="85b41-210">저장소 서비스 큐의 웹 서비스에 대한 자세한 내용은 [큐 서비스 개념](http://go.microsoft.com/fwlink/?LinkId=264788)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-210">For information about the web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span></span> <span data-ttu-id="85b41-211">Visual Studio를 사용하여 저장소 서비스 큐에 메시지를 보내는 방법에 대한 자세한 내용은 [저장소 서비스 큐에 메시지 보내기](https://msdn.microsoft.com/library/azure/jj649344.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-211">For information about how to send messages to a storage services queue by using Visual Studio, see [Sending Messages to a Storage Services Queue](https://msdn.microsoft.com/library/azure/jj649344.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="85b41-212">저장소 서비스 큐는 서비스 버스 큐와 구별됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-212">Storage services queues are distinct from service bus queues.</span></span> <span data-ttu-id="85b41-213">서비스 버스 큐에 대한 자세한 내용은 서비스 버스 큐, 항목 및 구독을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-213">For more information about service bus queues, see Service Bus Queues, Topics, and Subscriptions.</span></span>
> 
> 

## <a name="work-with-table-resources"></a><span data-ttu-id="85b41-214">테이블 리소스로 작업</span><span class="sxs-lookup"><span data-stu-id="85b41-214">Work with Table Resources</span></span>
<span data-ttu-id="85b41-215">Azure 테이블 저장소 서비스는 다량의 구조화된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-215">The Azure Table storage service stores large amounts of structured data.</span></span> <span data-ttu-id="85b41-216">이 서비스는 Azure 클라우드 내부 및 외부에서 인증된 호출을 수락하는 NoSQL 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-216">The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="85b41-217">Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-217">Azure tables are ideal for storing structured, non-relational data.</span></span>

### <a name="to-create-a-table"></a><span data-ttu-id="85b41-218">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="85b41-218">To create a table</span></span>
1. <span data-ttu-id="85b41-219">클라우드 탐색기에서 저장소 계정의 **테이블** 노드를 선택한 다음 **테이블 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-219">In Cloud Explorer, select the **Tables** node of the storage account, and then choose **Create Table**.</span></span>
2. <span data-ttu-id="85b41-220">**테이블 만들기** 대화 상자에서 테이블의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-220">In the **Create Table** dialog box, enter a name for the table.</span></span>

### <a name="to-view-table-data"></a><span data-ttu-id="85b41-221">테이블 데이터를 보려면</span><span class="sxs-lookup"><span data-stu-id="85b41-221">To view table data</span></span>
1. <span data-ttu-id="85b41-222">클라우드 탐색기에서 **Azure** 노드를 연 다음 **저장소** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-222">In Cloud Explorer, open the **Azure** node, and then open the **Storage** node.</span></span>
2. <span data-ttu-id="85b41-223">관심 있는 저장소 계정 노드를 연 다음 **테이블** 노드를 열어 저장소 계정에 대한 테이블 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-223">Open the storage account node that you are interested in, and then open the **Tables** node to see a list of tables for the storage account.</span></span>
3. <span data-ttu-id="85b41-224">테이블의 바로 가기 메뉴를 열고 **테이블 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-224">Open the shortcut menu for a table and then choose **View Table**.</span></span>
   
    ![솔루션 탐색기에 있는 Azure 테이블](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

<span data-ttu-id="85b41-226">테이블은 엔터티 (행에 표시) 및 속성 (열에 표시) 별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-226">The table is organized by entities (shown in rows) and properties (shown in columns).</span></span> <span data-ttu-id="85b41-227">예를 들어 다음 그림은 **테이블 디자이너**에 나열된 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-227">For example, the following illustration shows entities listed in the **Table Designer**:</span></span>

### <a name="to-edit-table-data"></a><span data-ttu-id="85b41-228">테이블 데이터를 편집하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-228">To edit table data</span></span>
1. <span data-ttu-id="85b41-229">**테이블 디자이너**에서 엔터티(단일 행) 또는 속성(단일 셀)에 대한 바로 가기 메뉴를 열고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-229">In the **Table Designer**, open the shortcut menu for an entity (a single row) or a property (a single cell) and then choose **Edit**.</span></span>
   
    ![테이블 엔터티 추가 또는 편집](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    <span data-ttu-id="85b41-231">단일 테이블의 엔터티는 속성 (열)과 동일한 집합을 가질 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-231">Entities in a single table aren’t required to have the same set of properties (columns).</span></span> <span data-ttu-id="85b41-232">테이블 데이터 보기 및 편집에 대한 다음의 제한 사항에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="85b41-232">Keep in mind the following restrictions on viewing and editing table data.</span></span>
   
   * <span data-ttu-id="85b41-233">이진 데이터(byte[] 형식)를 보거나 편집할 수 없지만 테이블에 저장할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-233">You can’t view or edit binary data (type byte[]), but you can store it in a table.</span></span>
   * <span data-ttu-id="85b41-234">Azure의 테이블 저장소는 **PartitionKey** 또는 **RowKey** 값의 편집을 지원하지 않으므로 해당 작업을 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-234">You can’t edit the **PartitionKey** or **RowKey** values, because table storage in Azure doesn't support that operation.</span></span>
   * <span data-ttu-id="85b41-235">Timestamp는 Azure 저장소 서비스가 사용하는 이름이므로 해당 이름의 속성을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-235">You can’t create a property called Timestamp, Azure Storage services use a property with that name.</span></span>
   * <span data-ttu-id="85b41-236">DateTime 값을 입력하는 경우 컴퓨터의 지역 및 언어 설정에 부합하는 형식을 따라야 합니다 (예: 미국 영어에 경우MM/DD/YYYY HH:MM:SS  [AM|PM]).</span><span class="sxs-lookup"><span data-stu-id="85b41-236">If you enter a DateTime value, you must follow a format that's appropriate to the region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for U.S. English).</span></span>

### <a name="to-add-entities"></a><span data-ttu-id="85b41-237">엔터티를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-237">To add entities</span></span>
1. <span data-ttu-id="85b41-238">**테이블 디자이너**에서 **엔터티 추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-238">In the **Table Designer**, choose the **Add Entity** button.</span></span>
   
    ![엔터티 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. <span data-ttu-id="85b41-240">**엔터티 추가** 대화 상자에서 **PartitionKey** 및 **RowKey** 속성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-240">In the **Add Entity** dialog box, enter the values of the **PartitionKey** and **RowKey** properties.</span></span>
   
    ![엔터티 대화 상자 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    <span data-ttu-id="85b41-242">엔터티를 삭제하고 다시 추가하지 않는 한 대화 상자를 닫은 후에는 값을 변경할 수 없으므로 신중하게 값을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-242">Enter the values carefully because you can't change them after you close the dialog box unless you delete the entity and add it again.</span></span>

### <a name="to-filter-entities"></a><span data-ttu-id="85b41-243">엔터티를 필터링하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-243">To filter entities</span></span>
<span data-ttu-id="85b41-244">쿼리 작성기를 사용하는 경우 테이블에 표시되는 엔터티 집합을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-244">You can customize the set of entities that appear in a table if you use the query builder.</span></span>

1. <span data-ttu-id="85b41-245">쿼리 작성기를 열려면 테이블을 열어 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-245">To open the query builder, open a table for viewing.</span></span>
2. <span data-ttu-id="85b41-246">테이블 보기의 도구 모음에서 쿼리 작성기 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-246">Choose the Query Builder button on the table view’s toolbar.</span></span>
   
    <span data-ttu-id="85b41-247">**쿼리 작성기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-247">The **Query Builder** dialog box appears.</span></span> <span data-ttu-id="85b41-248">다음 그림에서는 쿼리 작성기에서 작성되고 있는 쿼리를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-248">The following illustration shows a query that's being built in the query builder.</span></span>
   
    ![쿼리 작성기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. <span data-ttu-id="85b41-250">쿼리 작성을 마친 경우 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-250">When you’re done building the query, close the dialog box.</span></span> <span data-ttu-id="85b41-251">쿼리의 결과 텍스트 형식이 WCF 데이터 서비스 필터로 텍스트 상자에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-251">The resulting text form of the query appears in a text box as a WCF Data Services filter.</span></span>
4. <span data-ttu-id="85b41-252">쿼리를 실행하려면 녹색 삼각형 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-252">To run the query, choose the green triangle icon.</span></span>
   
    <span data-ttu-id="85b41-253">또한 필터 필드에 WCF 데이터 서비스 필터 문자열을 직접 입력한 경우 **테이블 디자이너** 에 나타나는 엔터티 데이터를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-253">You can also filter entity data that appears in the **Table Designer** if you enter a WCF Data Services filter string directly in the filter field.</span></span> <span data-ttu-id="85b41-254">이러한 종류의 문자열은 SQL WHERE 절과 유사하지만 HTTP 요청으로 서버에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-254">This kind of string is similar to a SQL WHERE clause but is sent to the server as an HTTP request.</span></span> <span data-ttu-id="85b41-255">필터 문자열을 생성하는 방법에 대한 자세한 내용은 [테이블 디자이너에 대한 필터 문자열 생성](https://msdn.microsoft.com/library/azure/ff683669.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-255">For information about how to construct filter strings, see [Constructing Filter Strings for the Table Designer](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>
   
    <span data-ttu-id="85b41-256">다음 그림에서는 유효한 필터 문자열의 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-256">The following illustration shows an example of a valid filter string:</span></span>
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a><span data-ttu-id="85b41-258">저장소 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="85b41-258">Refresh storage data</span></span>
<span data-ttu-id="85b41-259">서버 탐색기에 연결하거나 저장소 계정에서 데이터를 가져올 때 작업을 완료하기까지 최대 일 분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-259">When Server Explorer connects to or gets data from a storage account, it might take up to a minute for the operation to complete.</span></span> <span data-ttu-id="85b41-260">연결할 수 없는 경우 작업 시간이 초과될 수 있습니다. 데이터를 검색하는 동안에 Visual Studio의 다른 부분에서 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-260">If it can’t connect, the operation might time out. While data is retrieved, you can continue to work in other parts of Visual Studio.</span></span> <span data-ttu-id="85b41-261">작업이 너무 오래 걸려서 취소하려면, 서버 탐색기 도구 모음에서 **새로 고침 중지** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-261">To cancel the operation if it’s taking too long, choose the **Stop Refresh** button on the Server Explorer toolbar.</span></span>

#### <a name="to-refresh-blob-container-data"></a><span data-ttu-id="85b41-262">Blob 컨테이너 데이터를 새로 고치려면</span><span class="sxs-lookup"><span data-stu-id="85b41-262">To refresh blob container data</span></span>
* <span data-ttu-id="85b41-263">**저장소** 아래의 **Blob** 노드를 선택하고 서버 탐색기 도구 모음에서 **새로 고침** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-263">Select the **Blobs** node beneath **Storage** and choose the **Refresh** button on the Server Explorer toolbar.</span></span>
* <span data-ttu-id="85b41-264">표시된 Blob 목록을 새로 고치려면 **실행** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-264">To refresh the list of blobs that is displayed, choose the **Execute** button.</span></span>

#### <a name="to-refresh-table-data"></a><span data-ttu-id="85b41-265">테이블 데이터를 새로 고치려면</span><span class="sxs-lookup"><span data-stu-id="85b41-265">To refresh table data</span></span>
* <span data-ttu-id="85b41-266">**저장소** 아래의 **테이블** 노드를 선택하고 **새로 고침** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-266">Select the **Tables** node beneath **Storage** and choose the **Refresh** button.</span></span>
* <span data-ttu-id="85b41-267">**테이블 디자이너**에 표시된 엔터티 목록을 새로 고치려면 **테이블 디자이너**에서 **실행** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-267">To refresh the list of entities that is displayed in the **Table Designer**, choose the **Execute** button on the **Table Designer**.</span></span>

#### <a name="to-refresh-queue-data"></a><span data-ttu-id="85b41-268">큐 데이터를 새로 고치려면</span><span class="sxs-lookup"><span data-stu-id="85b41-268">To refresh queue data</span></span>
* <span data-ttu-id="85b41-269">**큐** 노드를 선택한 다음 **새로 고침** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-269">Select the **Queues** node, and then choose the **Refresh** button.</span></span>

#### <a name="to-refresh-all-items-in-a-storage-account"></a><span data-ttu-id="85b41-270">저장소 계정의 모든 항목을 새로 고치려면</span><span class="sxs-lookup"><span data-stu-id="85b41-270">To refresh all items in a storage account</span></span>
* <span data-ttu-id="85b41-271">계정 이름을 선택한 다음 서버 탐색기에 대한 도구 모음에서 **새로 고침** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-271">Choose the account name, and then choose the **Refresh** button on the toolbar for Server Explorer.</span></span>

### <a name="add-storage-accounts-by-using-server-explorer"></a><span data-ttu-id="85b41-272">서버 탐색기를 사용하여 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="85b41-272">Add storage accounts by using Server Explorer</span></span>
<span data-ttu-id="85b41-273">서버 탐색기를 사용하여 저장소 계정을 추가하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-273">There are two ways to add storage accounts by using Server Explorer.</span></span> <span data-ttu-id="85b41-274">Azure 구독에서 새 저장소 계정을 만들거나 기존 저장소 계정을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-274">You can create a new storage account in your Azure subscription, or you can attach an existing storage account.</span></span>

#### <a name="to-create-a-new-storage-account-by-using-server-explorer"></a><span data-ttu-id="85b41-275">서버 탐색기를 사용하여 새 저장소 계정을 만들려면</span><span class="sxs-lookup"><span data-stu-id="85b41-275">To create a new storage account by using Server Explorer</span></span>
1. <span data-ttu-id="85b41-276">서버 탐색기에서 저장소 노드에 대한 바로 가기 메뉴를 연 다음 저장소 계정 만들기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-276">In Server Explorer, open the shortcut menu for the Storage node, and then choose Create Storage Account.</span></span>
   
    ![새 Azure 저장소 계정 만들기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. <span data-ttu-id="85b41-278">**저장소 계정 만들기** 대화 상자에서 새 저장소 계정에 대한 다음의 정보를 선택 또는 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-278">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="85b41-279">저장소 계정을 추가할 Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-279">The Azure subscription to which you want to add the storage account.</span></span>
   * <span data-ttu-id="85b41-280">새 저장소 계정에 대해 사용하려는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-280">The name you want to use for the new storage account.</span></span>
   * <span data-ttu-id="85b41-281">지역 또는 선호도 그룹 (예: 미국 서부 또는 동아시아)입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-281">The region or affinity group (such as West US or East Asia).</span></span>
   * <span data-ttu-id="85b41-282">저장소 계정에 대해 사용하려는 복제의 유형입니다 – 예: 지역 중복.</span><span class="sxs-lookup"><span data-stu-id="85b41-282">The type of replication you want to use for the storage account, such as Geo-Redundant.</span></span>
3. <span data-ttu-id="85b41-283">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-283">Choose **Create**.</span></span>
   
    <span data-ttu-id="85b41-284">솔루션 탐색기의 **저장소** 목록에 새 저장소 계정이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-284">The new storage account appears in the **Storage** list in Solution Explorer.</span></span>

#### <a name="to-attach-an-existing-storage-account-by-using-server-explorer"></a><span data-ttu-id="85b41-285">서버 탐색기를 사용하여 기존 저장소 계정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-285">To attach an existing storage account by using Server Explorer</span></span>
1. <span data-ttu-id="85b41-286">서버 탐색기에서 Azure 저장소 노드에 대 한 바로 가기 메뉴를 연 다음 **외부 저장소 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-286">In Server Explorer, open the shortcut menu for the Azure storage node, and then choose **Attach External Storage**.</span></span>
   
    ![기존 저장소 계정 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. <span data-ttu-id="85b41-288">**저장소 계정 만들기** 대화 상자에서 새 저장소 계정에 대한 다음의 정보를 선택 또는 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-288">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="85b41-289">연결하려는 기존 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-289">The name of the existing storage account you want to attach.</span></span> <span data-ttu-id="85b41-290">이름을 입력하거나 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-290">You can enter a name or select it from the list.</span></span>
   * <span data-ttu-id="85b41-291">선택한 저장소 계정에 대한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-291">The key for the selected storage account.</span></span> <span data-ttu-id="85b41-292">저장소 계정을 선택할 때 일반적으로 이 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-292">This value is typically provided for you when you select a storage account.</span></span> <span data-ttu-id="85b41-293">Visual Studio가 저장소 계정 키를 기억하기를 원하는 경우 계정 키 상자 기억하기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-293">If you want Visual Studio to remember the storage account key, select the Remember account key box.</span></span>
   * <span data-ttu-id="85b41-294">저장소 계정에 연결하기 위해 사용하는 프로토콜입니다 - 예: HTTP, HTTPS, 또는 사용자 지정 끝점.</span><span class="sxs-lookup"><span data-stu-id="85b41-294">The protocol to use to connect to the storage account, such as HTTP, HTTPS, or a custom endpoint.</span></span> <span data-ttu-id="85b41-295">사용자 지정 끝점에 대한 자세한 내용은 [연결 문자열을 구성하는 방법](https://msdn.microsoft.com/library/azure/ee758697.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-295">See [How to Configure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx) for more information about custom endpoints.</span></span>

### <a name="to-view-the-secondary-endpoints"></a><span data-ttu-id="85b41-296">보조 끝점을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-296">To view the secondary endpoints</span></span>
* <span data-ttu-id="85b41-297">**읽기 액세스 지역 중복** 복제 옵션을 사용하여 저장소 계정을 만든 경우, 보조 끝점을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-297">If you created a storage account using the **Read-Access Geo Redundant** replication option, you can view its secondary endpoints.</span></span> <span data-ttu-id="85b41-298">계정 이름에 대한 바로 가기 메뉴를 연 다음 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-298">Open the shortcut menu for the account name, and then choose **Properties**.</span></span>
  
    ![저장소 보조 끝점](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="to-remove-a-storage-account-from-server-explorer"></a><span data-ttu-id="85b41-300">서버 탐색기에서 저장소 계정을 제거하려면</span><span class="sxs-lookup"><span data-stu-id="85b41-300">To remove a storage account from Server Explorer</span></span>
* <span data-ttu-id="85b41-301">서버 탐색기에서 계정 이름에 대한 바로 가기 메뉴를 연 다음 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-301">In Server Explorer, open the shortcut menu for the account name, and then choose **Delete**.</span></span> <span data-ttu-id="85b41-302">저장소 계정을 삭제하면 해당 계정에 저장된 키 정보도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-302">If you delete a storage account, any saved key information for that account is also removed.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="85b41-303">서버 탐색기에서 저장소 계정을 삭제하면 저장소 계정이나 그 안에 포함된 데이터에는 영향을 주지 않으며, 단순히 서버 탐색기의 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85b41-303">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains; it simply removes the reference from Server Explorer.</span></span> <span data-ttu-id="85b41-304">저장소 계정을 영구적으로 삭제하려면 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-304">To permanently delete a storage account, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
  > 
  > 

## <a name="next-steps"></a><span data-ttu-id="85b41-305">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85b41-305">Next steps</span></span>
<span data-ttu-id="85b41-306">Azure 저장소 서비스를 사용하는 방법에 대해 자세히 알아보려면 [Azure 저장소 서비스 액세스](https://msdn.microsoft.com/library/azure/ee405490.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85b41-306">To learn more about how use Azure storage services, see [Accessing the Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span></span>

