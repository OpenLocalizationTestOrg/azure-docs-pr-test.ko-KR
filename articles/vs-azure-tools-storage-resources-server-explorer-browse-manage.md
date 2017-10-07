---
title: "aaaBrowsing 서버 탐색기로 저장소 리소스 및 관리 | Microsoft Docs"
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
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a><span data-ttu-id="5b783-103">서버 탐색기로 저장소 리소스 찾아보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="5b783-103">Browsing and Managing Storage Resources with Server Explorer</span></span>
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a><span data-ttu-id="5b783-104">개요</span><span class="sxs-lookup"><span data-stu-id="5b783-104">Overview</span></span>
<span data-ttu-id="5b783-105">Hello Azure Tools for Microsoft Visual Studio를 설치한 경우 볼 수 있습니다 blob, 큐 및 테이블 데이터 저장소 계정에서 Azure에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-105">If you've installed hello Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span></span> <span data-ttu-id="5b783-106">서버 탐색기에서 Azure 저장소 노드 hello 로컬 저장소 에뮬레이터 계정 및 다른 Azure 저장소 계정에 있는 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-106">hello Azure Storage node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span></span>

<span data-ttu-id="5b783-107">hello 메뉴 모음에서 Visual Studio 서버 탐색기 tooview 선택 **보기**, **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-107">tooview Server Explorer in Visual Studio, on hello menu bar, choose **View**, **Server Explorer**.</span></span> <span data-ttu-id="5b783-108">hello 저장소 노드 모두에서 각 Azure 구독/인증서에 연결 되어 있는 hello 저장소 계정을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-108">hello storage node shows all of hello storage accounts that exist under each Azure subscription/certificate you're connected to.</span></span> <span data-ttu-id="5b783-109">저장소 계정이 표시 되지 않으면 hello 지침에 따라 추가할 수 있습니다 [이 항목의 뒷부분에 나오는](#add-storage-accounts-by-using-server-explorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-109">If your storage account doesn't appear, you can add it by following hello instructions [later in this topic](#add-storage-accounts-by-using-server-explorer).</span></span>

<span data-ttu-id="5b783-110">Azure SDK 2.7부터 새로운 클라우드 탐색기 tooview hello를 사용 하 여 고 Azure 리소스를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-110">Starting in Azure SDK 2.7, you can also use hello new Cloud Explorer tooview and manage your Azure resources.</span></span> <span data-ttu-id="5b783-111">자세한 내용은 [클라우드 탐색기를 사용하여 Azure 리소스 관리](vs-azure-tools-resources-managing-with-cloud-explorer.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b783-111">See [Managing Azure Resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) for more information.</span></span>

## <a name="view-and-manage-storage-resources-in-visual-studio"></a><span data-ttu-id="5b783-112">Visual Studio에서 저장소 리소스를 확인 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-112">View and manage storage resources in Visual Studio</span></span>
<span data-ttu-id="5b783-113">서버 탐색기는 저장소 에뮬레이터 계정에 있는 Blob, 큐, 테이블 목록을 자동으로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span></span> <span data-ttu-id="5b783-114">hello 저장소 에뮬레이터 계정 hello hello 저장소 노드 아래에서 서버 탐색기에 나열 됩니다 **개발** 노드.</span><span class="sxs-lookup"><span data-stu-id="5b783-114">hello storage emulator account is listed in Server Explorer under hello Storage node as hello **Development** node.</span></span>

<span data-ttu-id="5b783-115">toosee hello 저장소 에뮬레이터 계정의 리소스 확장 hello **개발** 노드.</span><span class="sxs-lookup"><span data-stu-id="5b783-115">toosee hello storage emulator account’s resources, expand hello **Development** node.</span></span> <span data-ttu-id="5b783-116">Hello를 확장 하면 hello 저장소 에뮬레이터 시작 되지 않은 상태 경우 **개발** 노드를 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-116">If hello storage emulator hasn’t been started when you expand hello **Development** node, it will automatically start.</span></span> <span data-ttu-id="5b783-117">이 작업은 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-117">This can take several seconds.</span></span> <span data-ttu-id="5b783-118">Hello 저장소 에뮬레이터를 시작 하는 동안 Visual Studio의 다른 영역에서 toowork를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-118">You can continue toowork in other areas of Visual Studio while hello storage emulator starts.</span></span>

<span data-ttu-id="5b783-119">저장소 계정에 tooview 리소스 서버 탐색기에서 hello 저장소 계정의 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-119">tooview resources in a storage account, expand hello storage account’s node in Server Explorer.</span></span> <span data-ttu-id="5b783-120">하위 노드를 다음 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-120">hello following sub-nodes appear:</span></span>

* <span data-ttu-id="5b783-121">Blob</span><span class="sxs-lookup"><span data-stu-id="5b783-121">Blobs</span></span>
* <span data-ttu-id="5b783-122">큐</span><span class="sxs-lookup"><span data-stu-id="5b783-122">Queues</span></span>
* <span data-ttu-id="5b783-123">테이블</span><span class="sxs-lookup"><span data-stu-id="5b783-123">Tables</span></span>

## <a name="work-with-blob-resources"></a><span data-ttu-id="5b783-124">Blob 리소스로 작업</span><span class="sxs-lookup"><span data-stu-id="5b783-124">Work with Blob Resources</span></span>
<span data-ttu-id="5b783-125">hello Blob 노드에 hello 선택한 저장소 계정에 대 한 컨테이너 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-125">hello Blobs node displays a list of containers for hello selected storage account.</span></span> <span data-ttu-id="5b783-126">Blob 컨테이너는 Blob 파일을 포함하고 있으며 이러한 Blob을 폴더와 하위 폴더로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-126">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span></span> <span data-ttu-id="5b783-127">참조 [어떻게 toouse.NET에서 Blob 저장소](storage/blobs/storage-dotnet-how-to-use-blobs.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-127">See [How toouse Blob Storage from .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information.</span></span>

### <a name="toocreate-a-blob-container"></a><span data-ttu-id="5b783-128">toocreate blob 컨테이너</span><span class="sxs-lookup"><span data-stu-id="5b783-128">toocreate a blob container</span></span>
1. <span data-ttu-id="5b783-129">Hello에 대 한 바로 가기 메뉴를 열고 hello **Blob** 노드를 선택한 후 **Create Blob Container**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-129">Open hello shortcut menu for hello **Blobs** node, and then choose **Create Blob Container**.</span></span>
2. <span data-ttu-id="5b783-130">Hello에 **Create Blob Container** 대화 상자 hello 새 컨테이너의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-130">In hello **Create Blob Container** dialog box, enter hello name of hello new container.</span></span>  
3. <span data-ttu-id="5b783-131">키를 눌러 **ENTER** 키보드 또는 있습니다 수 또는 클릭 하 여 hello 이름 필드 toosave hello blob 컨테이너의 외부 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-131">Press **ENTER** on your keyboard or you can click or tap outside of hello name field toosave hello blob container.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5b783-132">hello blob 컨테이너 이름은 숫자 (0-9) 또는 소문자 (a ~ z)로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-132">hello blob container name must begin with a number (0-9) or lowercase letter (a-z).</span></span>
   > 
   > 

### <a name="toodelete-a-blob-container"></a><span data-ttu-id="5b783-133">toodelete blob 컨테이너</span><span class="sxs-lookup"><span data-stu-id="5b783-133">toodelete a blob container</span></span>
* <span data-ttu-id="5b783-134">Tooremove을 눌러 hello blob 컨테이너에 대 한 바로 가기 메뉴를 열고 hello **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-134">Open hello shortcut menu for hello blob container you want tooremove and then choose **Delete**.</span></span>

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a><span data-ttu-id="5b783-135">blob 컨테이너에 toodisplay hello 항목 목록이 포함 된</span><span class="sxs-lookup"><span data-stu-id="5b783-135">toodisplay a list of hello items contained in a blob container</span></span>
* <span data-ttu-id="5b783-136">Hello 목록에서 blob 컨테이너 이름에 대 한 hello 바로 가기 메뉴를 열고 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-136">Open hello shortcut menu for a blob container name in hello list and then choose **Open**.</span></span>
  
    <span data-ttu-id="5b783-137">Blob 컨테이너의 hello 콘텐츠를 볼 때 hello blob 컨테이너 보기로 알려진 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-137">When you view hello contents of a blob container, it appears in a tab known as hello blob container view.</span></span>
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    <span data-ttu-id="5b783-139">Hello blob 컨테이너 뷰의 hello 오른쪽 위 모서리에 hello 단추를 사용 하 여 blob에 대 한 작업을 수행 하는 hello를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-139">You can perform hello following operations on blobs by using hello buttons in hello top-right corner of hello blob container view:</span></span>
  
  * <span data-ttu-id="5b783-140">필터 값을 입력 및 적용하기</span><span class="sxs-lookup"><span data-stu-id="5b783-140">Enter a filter value and apply it</span></span>
  * <span data-ttu-id="5b783-141">Hello hello 컨테이너의 blob 목록 새로 고침</span><span class="sxs-lookup"><span data-stu-id="5b783-141">Refresh hello list of blobs in hello container</span></span>
  * <span data-ttu-id="5b783-142">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="5b783-142">Upload a file</span></span>
  * <span data-ttu-id="5b783-143">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="5b783-143">Delete a blob</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5b783-144">Blob 컨테이너에서 파일을 삭제 하면 파일을 원본으로 사용 하는 hello; 삭제 되지 않습니다. 에서만 제거 hello blob 컨테이너에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-144">Deleting a file from a blob container doesn’t delete hello underlying file; it only removes it from hello blob container.</span></span>
    > 
    > 
  * <span data-ttu-id="5b783-145">Blob 열기</span><span class="sxs-lookup"><span data-stu-id="5b783-145">Open a blob</span></span>
  * <span data-ttu-id="5b783-146">Blob toohello 로컬 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-146">Save a blob toohello local computer</span></span>

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a><span data-ttu-id="5b783-147">toocreate 폴더 또는 blob 컨테이너에 대 한 하위 폴더</span><span class="sxs-lookup"><span data-stu-id="5b783-147">toocreate a folder or subfolder in a blob container</span></span>
1. <span data-ttu-id="5b783-148">클라우드 탐색기에서 hello blob 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-148">Choose hello blob container in Cloud Explorer.</span></span> <span data-ttu-id="5b783-149">Hello 컨테이너 창의 hello 선택 **Blob 업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-149">In hello container window, choose hello **Upload Blob** button.</span></span>
   
    ![Blob 폴더에 파일 업로드하기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. <span data-ttu-id="5b783-151">Hello에 **새 파일 업로드** 대화 상자에서 선택 하는 hello **찾아보기** 단추 toospecify hello 원하는 파일 tooupload를 선택한 다음 hello에 폴더 이름을 입력 **폴더 (옵션)** 상자 .</span><span class="sxs-lookup"><span data-stu-id="5b783-151">In hello **Upload New File** dialog box, choose hello **Browse** button toospecify hello file you want tooupload, and then enter a folder name in hello **Folder (optional)** box.</span></span>
   
    <span data-ttu-id="5b783-152">하위 폴더에 따라 컨테이너 폴더에 동일한 hello를 추가할 수 있습니다 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-152">You can add subfolders in container folders by following hello same procedure.</span></span> <span data-ttu-id="5b783-153">Hello 파일이 됩니다 폴더 이름을 지정 하지 않으면, hello blob 컨테이너의 최상위 수준 toohello 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-153">If you don’t specify a folder name, hello file will be uploaded toohello top level of hello blob container.</span></span> <span data-ttu-id="5b783-154">hello 파일이 hello 컨테이너에서 hello 지정한 폴더에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-154">hello file appears in hello specified folder in hello container.</span></span>
   
    ![폴더는 tooa blob 컨테이너를 추가합니다.](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. <span data-ttu-id="5b783-156">Hello 폴더를 두 번 클릭 하거나 hello 폴더 내용의 toosee hello ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-156">Double-click hello folder or press ENTER toosee hello contents of hello folder.</span></span> <span data-ttu-id="5b783-157">Hello를 선택 하 여 hello 컨테이너의 뒤로 toohello 루트를 탐색할 수 hello 컨테이너 폴더에 있는 경우 **부모 디렉터리 열기** (위쪽 화살표) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-157">When you’re in hello container’s folder, you can navigate back toohello root of hello container by choosing hello **Open Parent Directory** (up arrow) button.</span></span>

### <a name="toodelete-a-container-folder"></a><span data-ttu-id="5b783-158">toodelete 컨테이너 폴더</span><span class="sxs-lookup"><span data-stu-id="5b783-158">toodelete a container folder</span></span>
* <span data-ttu-id="5b783-159">Hello 폴더에 hello 파일 모두 삭제</span><span class="sxs-lookup"><span data-stu-id="5b783-159">Delete all of hello files in hello folder</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5b783-160">Blob 컨테이너의 폴더 가상 폴더 이므로, 빈 폴더를 만들 수 없습니다도 삭제할 수 폴더 toodelete 파일 내용을.</span><span class="sxs-lookup"><span data-stu-id="5b783-160">Because folders in blob containers are virtual folders, you can’t create an empty folder, nor can you delete a folder toodelete its file contents.</span></span> <span data-ttu-id="5b783-161">Toodelete hello 폴더 toodelete hello 폴더의 전체 내용을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-161">You have toodelete hello entire contents of a folder toodelete hello folder.</span></span>
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a><span data-ttu-id="5b783-162">컨테이너의 blob toofilter</span><span class="sxs-lookup"><span data-stu-id="5b783-162">toofilter blobs in a container</span></span>
<span data-ttu-id="5b783-163">공통 접두사를 지정 하 여 표시 되는 hello blob를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-163">You can filter hello blobs that are displayed by specifying a common prefix.</span></span>

<span data-ttu-id="5b783-164">예를 들어, hello 접두사를 입력 하면 `hello` 에 hello 필터 텍스트 상자를 선택한 후 hello **Execute** (**!**) 단추를 'hello'로 시작 하는 blob만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-164">For example, if you enter hello prefix `hello` in hello filter text box and then choose hello **Execute** (**!**)button, only blobs that begin with 'hello' appear.</span></span>

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> <span data-ttu-id="5b783-166">hello 필터 필드는 대/소문자 구분 하 고 와일드 카드 문자를 사용 하 여 필터링을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-166">hello filter field is case-sensitive and doesn’t support filtering with wildcard characters.</span></span> <span data-ttu-id="5b783-167">Blob은 접두사로만 필터링될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-167">Blobs can only be filtered by prefix.</span></span> <span data-ttu-id="5b783-168">hello 접두사는 가상 계층 구조에서 구분 기호 tooorganize blob을 사용 하는 경우 구분 기호를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-168">hello prefix may include a delimiter if you are using a delimiter tooorganize blobs in a virtual hierarchy.</span></span> <span data-ttu-id="5b783-169">예를 들어에서 필터링 접두사 HelloFabric hello/해당 문자열로 시작 하는 모든 blob를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-169">For example, filtering on hello prefix HelloFabric/ returns all blobs beginning with that string.</span></span>
> 
> 

### <a name="toodownload-blob-data"></a><span data-ttu-id="5b783-170">toodownload blob 데이터</span><span class="sxs-lookup"><span data-stu-id="5b783-170">toodownload blob data</span></span>
* <span data-ttu-id="5b783-171">**클라우드 탐색기**를 하나 이상의 blob에 대 한 hello 바로 가기 메뉴를 열고 다음을 선택 **열고**, 또는 hello blob 이름을 선택 하 고 hello 선택 **열** 단추를 두 번 클릭 하거나 hello blob 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-171">In **Cloud Explorer**, open hello shortcut menu for one or more blobs and then choose **Open**, or choose hello blob name and then choose hello **Open** button, or double-click hello blob name.</span></span>
  
    <span data-ttu-id="5b783-172">hello에 blob 다운로드 hello 진행률이 나타납니다 **Azure 활동 로그** 창.</span><span class="sxs-lookup"><span data-stu-id="5b783-172">hello progress of a blob download appears in hello **Azure Activity Log** window.</span></span>
  
    <span data-ttu-id="5b783-173">hello blob 해당 파일 형식에 대 한 hello 기본 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-173">hello blob opens in hello default editor for that file type.</span></span> <span data-ttu-id="5b783-174">로컬에 설치 된 응용 프로그램의 hello 파일이 열립니다 hello 운영 체제 hello 파일 형식을 인식 하는 경우 그렇지 않으면 묻는 toochoose hello hello blob 파일 형식에 적합 한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-174">If hello operating system recognizes hello file type, hello file opens in a locally installed application; otherwise, you're prompted toochoose an application that’s appropriate for hello file type of hello blob.</span></span> <span data-ttu-id="5b783-175">blob을 다운로드할 때 만들어진 hello 로컬 파일 읽기 전용으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-175">hello local file that’s created when you download a blob is marked as read-only.</span></span>
  
    <span data-ttu-id="5b783-176">Blob 데이터를 로컬로 캐시 되 고 hello hello Blob 서비스에서에서 blob의 마지막 수정된 시간이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-176">Blob data is cached locally and checked against hello blob's last modified time in hello Blob service.</span></span> <span data-ttu-id="5b783-177">마지막으로 다운로드 이후 hello blob 업데이트 된 경우는 다시 다운로드 해; 그렇지 않으면 hello blob hello 로컬 디스크에서 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-177">If hello blob has been updated since it was last downloaded, it will be downloaded again; otherwise, hello blob will be loaded from hello local disk.</span></span> <span data-ttu-id="5b783-178">기본적으로 blob는 다운로드 한 tooa 임시 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-178">By default, a blob is downloaded tooa temporary directory.</span></span> <span data-ttu-id="5b783-179">toodownload blob tooa 특정 디렉터리를 선택 하는 hello에 대 한 바로 가기 메뉴를 열고 hello blob 이름을 선택한 **다른 이름으로 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-179">toodownload blobs tooa specific directory, open hello shortcut menu for hello selected blob names and choose **Save As**.</span></span> <span data-ttu-id="5b783-180">이런이 방식으로 blob을 저장할 때 hello blob 파일이 열려 있지 않으면 및 hello 로컬 파일 읽기 / 쓰기 특성을 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-180">When you save a blob in this manner, hello blob file is not opened, and hello local file is created with read-write attributes.</span></span>

### <a name="tooupload-blobs"></a><span data-ttu-id="5b783-181">tooupload blob</span><span class="sxs-lookup"><span data-stu-id="5b783-181">tooupload blobs</span></span>
* <span data-ttu-id="5b783-182">Hello 선택 **Blob 업로드** hello 컨테이너 보기 hello blob 컨테이너 보기에 대해 열려 있을 때 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-182">Choose hello **Upload Blob** button when hello container is open for viewing in hello blob container view.</span></span>
  
    <span data-ttu-id="5b783-183">하나를 선택할 수 또는 더 많은 파일 tooupload 및 모든 형식의 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-183">You can choose one or more files tooupload and you can upload files of any type.</span></span> <span data-ttu-id="5b783-184">hello **Azure 활동 로그** 표시 hello hello 업로드의 진행률입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-184">hello **Azure Activity Log** shows hello progress of hello upload.</span></span> <span data-ttu-id="5b783-185">방법에 대 한 자세한 내용은 blob 데이터로 toowork 참조 [어떻게 toouse hello.NET에서 Azure Blob 저장소 서비스로](http://go.microsoft.com/fwlink/p/?LinkId=267911)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-185">For more information about how toowork with blob data, see [How toouse hello Azure Blob Storage Service in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span></span>

### <a name="tooview-logs-transferred-tooblobs"></a><span data-ttu-id="5b783-186">tooview 로그 전송 tooblobs</span><span class="sxs-lookup"><span data-stu-id="5b783-186">tooview logs transferred tooblobs</span></span>
* <span data-ttu-id="5b783-187">Azure 응용 프로그램에서 Azure 진단을 toolog 데이터를 사용 하는 로그 tooyour 저장소 계정에 전송한 경우 이러한 로그에 대 한 Azure에서 만들어진 컨테이너가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-187">If you are using Azure Diagnostics toolog data from your Azure application and you have transferred logs tooyour storage account, you’ll see containers that were created by Azure for these logs.</span></span> <span data-ttu-id="5b783-188">서버 탐색기에서 이러한 로그 보기 응용 프로그램에 쉽게 tooidentify 문제는 특히 경과 했는데도 문제가 있다면 배포 tooAzure 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5b783-188">Viewing these logs in Server Explorer is an easy way tooidentify problems with your application, especially if it’s been deployed tooAzure.</span></span> <span data-ttu-id="5b783-189">Azure 진단에 대한 자세한 내용은 [Azure 진단을 사용하여 로깅 데이터 수집](https://msdn.microsoft.com/library/azure/gg433048.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b783-189">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span></span>

### <a name="tooget-hello-url-for-a-blob"></a><span data-ttu-id="5b783-190">blob에 대 한 tooget hello URL</span><span class="sxs-lookup"><span data-stu-id="5b783-190">tooget hello URL for a blob</span></span>
* <span data-ttu-id="5b783-191">Hello blob의 바로 가기 메뉴를 열고 **URL 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-191">Open hello blob’s shortcut menu and then choose **Copy URL**.</span></span>

### <a name="tooedit-a-blob"></a><span data-ttu-id="5b783-192">tooedit blob</span><span class="sxs-lookup"><span data-stu-id="5b783-192">tooedit a blob</span></span>
* <span data-ttu-id="5b783-193">Hello blob을 선택 하 고 hello를 눌러 **Blob 열기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-193">Select hello blob and then choose hello **Open Blob** button.</span></span>
  
    <span data-ttu-id="5b783-194">hello 파일은 임시 위치로 다운로드 한 tooa 고 hello 로컬 컴퓨터에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-194">hello file is downloaded tooa temporary location and opened on hello local computer.</span></span> <span data-ttu-id="5b783-195">변경한 후 다시 hello blob을 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-195">You must upload hello blob again after you make changes.</span></span>

## <a name="work-with-queue-resources"></a><span data-ttu-id="5b783-196">큐 리소스로 작업</span><span class="sxs-lookup"><span data-stu-id="5b783-196">Work with Queue Resources</span></span>
<span data-ttu-id="5b783-197">저장소 서비스 큐는 Azure 저장소 계정에서 호스팅되며 tooallow 사용할 수 있습니다 프로그램 클라우드 서비스 역할 toocommunicate 서로 다른 서비스와 메시지 전달 메커니즘을 통해.</span><span class="sxs-lookup"><span data-stu-id="5b783-197">Storage services queues are hosted in an Azure storage account and you can use them tooallow your cloud service roles toocommunicate with each other and with other services by a message passing mechanism.</span></span> <span data-ttu-id="5b783-198">외부 클라이언트에 대 한 웹 서비스 및 클라우드 서비스를 통해 hello 큐를 프로그래밍 방식으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-198">You can access hello queue programmatically through a cloud service and over a web service for external clients.</span></span> <span data-ttu-id="5b783-199">또한 Visual Studio에서 서버 탐색기를 사용 하 여 직접 hello 큐를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-199">You can also access hello queue directly by using Server Explorer in Visual Studio.</span></span>

<span data-ttu-id="5b783-200">큐를 사용 하는 클라우드 서비스를 개발 하는 경우 Visual Studio toocreate 큐 toouse 수도 있으며 작업할 대화식으로 개발 하 고 코드를 테스트 하는 동안 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-200">When you develop a cloud service that uses queues, you might want toouse Visual Studio toocreate queues and work with them interactively while you develop and test your code.</span></span>

<span data-ttu-id="5b783-201">서버 탐색기에서 있습니다 수 hello 큐는 저장소 계정에 볼, 및 큐를 삭제, 큐 tooview 메시지를 만들고 열고 tooa 큐 메시지 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-201">In Server Explorer, you can view hello queues in a storage account, create and delete queues, open a queue tooview its messages, and add messages tooa queue.</span></span> <span data-ttu-id="5b783-202">보기에 대 한 큐를 열 때 hello 개별 메시지를 볼 수 있습니다 및 hello hello 왼쪽 위 모서리에 hello 단추를 사용 하 여 hello 큐에 작업을 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-202">When you open a queue for viewing, you can view hello individual messages, and you can perform hello following actions on hello queue by using hello buttons in hello top-left corner:</span></span>

* <span data-ttu-id="5b783-203">Hello hello 큐 보기 새로 고침</span><span class="sxs-lookup"><span data-stu-id="5b783-203">Refresh hello view of hello queue</span></span>
* <span data-ttu-id="5b783-204">메시지 toohello 큐 추가</span><span class="sxs-lookup"><span data-stu-id="5b783-204">Add a message toohello queue</span></span>
* <span data-ttu-id="5b783-205">Hello 최상위 메시지를 큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="5b783-205">Dequeue hello topmost message</span></span>
* <span data-ttu-id="5b783-206">전체 큐 지우기 hello</span><span class="sxs-lookup"><span data-stu-id="5b783-206">Clear hello entire queue</span></span>

<span data-ttu-id="5b783-207">다음 이미지는 hello에서는 두 개의 메시지를 포함 하는 큐를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-207">hello following image shows a queue that contains two messages.</span></span>

![큐 보기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

<span data-ttu-id="5b783-209">저장소에 대 한 자세한 내용은 서비스 큐에 대 한 참조 [하는 방법: 큐 저장소 서비스 사용 하 여 hello](http://go.microsoft.com/fwlink/?LinkID=264702)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-209">For more information about storage services queues, see [How to: Use hello Queue Storage Service](http://go.microsoft.com/fwlink/?LinkID=264702).</span></span> <span data-ttu-id="5b783-210">Hello 웹 서비스에 대 한 정보에 대 한 저장소 서비스 큐에 대 한 참조 [큐 서비스 개념](http://go.microsoft.com/fwlink/?LinkId=264788)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-210">For information about hello web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span></span> <span data-ttu-id="5b783-211">Toosend 메시지 tooa 저장소 Visual Studio를 사용 하 여 큐를 서비스 하는 방법에 대 한 정보를 참조 하십시오. [저장소 서비스 큐의 메시지를 보내는 tooa](https://msdn.microsoft.com/library/azure/jj649344.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-211">For information about how toosend messages tooa storage services queue by using Visual Studio, see [Sending Messages tooa Storage Services Queue](https://msdn.microsoft.com/library/azure/jj649344.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5b783-212">저장소 서비스 큐는 서비스 버스 큐와 구별됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-212">Storage services queues are distinct from service bus queues.</span></span> <span data-ttu-id="5b783-213">서비스 버스 큐에 대한 자세한 내용은 서비스 버스 큐, 항목 및 구독을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b783-213">For more information about service bus queues, see Service Bus Queues, Topics, and Subscriptions.</span></span>
> 
> 

## <a name="work-with-table-resources"></a><span data-ttu-id="5b783-214">테이블 리소스로 작업</span><span class="sxs-lookup"><span data-stu-id="5b783-214">Work with Table Resources</span></span>
<span data-ttu-id="5b783-215">hello Azure 테이블 저장소 서비스는 다량의 구조화 된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-215">hello Azure Table storage service stores large amounts of structured data.</span></span> <span data-ttu-id="5b783-216">hello 서비스는 허용 하는 NoSQL 데이터 저장소 인증 내부와 Azure 클라우드 hello 외부에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-216">hello service is a NoSQL datastore which accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="5b783-217">Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-217">Azure tables are ideal for storing structured, non-relational data.</span></span>

### <a name="toocreate-a-table"></a><span data-ttu-id="5b783-218">toocreate 테이블</span><span class="sxs-lookup"><span data-stu-id="5b783-218">toocreate a table</span></span>
1. <span data-ttu-id="5b783-219">클라우드 탐색기에서 선택 hello **테이블** 노드 hello 저장소 계정을 선택한 후 **Create Table**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-219">In Cloud Explorer, select hello **Tables** node of hello storage account, and then choose **Create Table**.</span></span>
2. <span data-ttu-id="5b783-220">Hello에 **Create Table** 대화 상자 hello 테이블에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-220">In hello **Create Table** dialog box, enter a name for hello table.</span></span>

### <a name="tooview-table-data"></a><span data-ttu-id="5b783-221">tooview 테이블 데이터</span><span class="sxs-lookup"><span data-stu-id="5b783-221">tooview table data</span></span>
1. <span data-ttu-id="5b783-222">클라우드 탐색기에서 열어 hello **Azure** 노드를 차례로 연 다음 hello **저장소** 노드.</span><span class="sxs-lookup"><span data-stu-id="5b783-222">In Cloud Explorer, open hello **Azure** node, and then open hello **Storage** node.</span></span>
2. <span data-ttu-id="5b783-223">관심 있는 하 고 hello를 열면 다음 열기 hello 저장소 계정 노드 **테이블** 노드 toosee hello 저장소 계정의 테이블 목록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-223">Open hello storage account node that you are interested in, and then open hello **Tables** node toosee a list of tables for hello storage account.</span></span>
3. <span data-ttu-id="5b783-224">테이블에 대 한 hello 바로 가기 메뉴를 열고 **뷰 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-224">Open hello shortcut menu for a table and then choose **View Table**.</span></span>
   
    ![솔루션 탐색기에 있는 Azure 테이블](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

<span data-ttu-id="5b783-226">hello 테이블은 엔터티 (행에 표시) 및 속성 (열에 표시)로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-226">hello table is organized by entities (shown in rows) and properties (shown in columns).</span></span> <span data-ttu-id="5b783-227">다음 그림 hello hello에 나열 된 엔터티를 표시 하는 예를 들어 **테이블 디자이너**:</span><span class="sxs-lookup"><span data-stu-id="5b783-227">For example, hello following illustration shows entities listed in hello **Table Designer**:</span></span>

### <a name="tooedit-table-data"></a><span data-ttu-id="5b783-228">tooedit 테이블 데이터</span><span class="sxs-lookup"><span data-stu-id="5b783-228">tooedit table data</span></span>
1. <span data-ttu-id="5b783-229">Hello에 **테이블 디자이너**를 엔터티 (단일 행) 또는 속성 (단일 셀)에 대 한 hello 바로 가기 메뉴를 열고 다음 선택 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-229">In hello **Table Designer**, open hello shortcut menu for an entity (a single row) or a property (a single cell) and then choose **Edit**.</span></span>
   
    ![테이블 엔터티 추가 또는 편집](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    <span data-ttu-id="5b783-231">단일 테이블의 엔터티에 필요한 toohave hello 동일 속성 (열)의 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-231">Entities in a single table aren’t required toohave hello same set of properties (columns).</span></span> <span data-ttu-id="5b783-232">제한 사항에 나오는 테이블 데이터 보기 및 편집에 유의 hello에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-232">Keep in mind hello following restrictions on viewing and editing table data.</span></span>
   
   * <span data-ttu-id="5b783-233">이진 데이터(byte[] 형식)를 보거나 편집할 수 없지만 테이블에 저장할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-233">You can’t view or edit binary data (type byte[]), but you can store it in a table.</span></span>
   * <span data-ttu-id="5b783-234">Hello를 편집할 수 없습니다 **PartitionKey** 또는 **RowKey** azure에서 테이블 저장소는 해당 작업을 지원 하지 않는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-234">You can’t edit hello **PartitionKey** or **RowKey** values, because table storage in Azure doesn't support that operation.</span></span>
   * <span data-ttu-id="5b783-235">Timestamp는 Azure 저장소 서비스가 사용하는 이름이므로 해당 이름의 속성을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-235">You can’t create a property called Timestamp, Azure Storage services use a property with that name.</span></span>
   * <span data-ttu-id="5b783-236">날짜/시간 값을 입력 하면 컴퓨터의 적절 한 toohello 국가 및 언어 설정 되는 형식을 따라야 (hh: MM/DD/YYYY mm: 예를 들어 [AM | PM] 미국 [AM|PM]).</span><span class="sxs-lookup"><span data-stu-id="5b783-236">If you enter a DateTime value, you must follow a format that's appropriate toohello region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for U.S. English).</span></span>

### <a name="tooadd-entities"></a><span data-ttu-id="5b783-237">tooadd 엔터티</span><span class="sxs-lookup"><span data-stu-id="5b783-237">tooadd entities</span></span>
1. <span data-ttu-id="5b783-238">Hello에 **테이블 디자이너**, hello 선택 **엔터티 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-238">In hello **Table Designer**, choose hello **Add Entity** button.</span></span>
   
    ![엔터티 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. <span data-ttu-id="5b783-240">Hello에 **엔터티 추가** 대화 상자 hello의 hello 값을 입력 **PartitionKey** 및 **RowKey** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-240">In hello **Add Entity** dialog box, enter hello values of hello **PartitionKey** and **RowKey** properties.</span></span>
   
    ![엔터티 대화 상자 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    <span data-ttu-id="5b783-242">Hello 엔터티를 삭제 하 고 다시 추가 하지 않으면 hello 대화 상자를 닫은 후 변경할 수 없으므로 신중 하 게 hello 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-242">Enter hello values carefully because you can't change them after you close hello dialog box unless you delete hello entity and add it again.</span></span>

### <a name="toofilter-entities"></a><span data-ttu-id="5b783-243">toofilter 엔터티</span><span class="sxs-lookup"><span data-stu-id="5b783-243">toofilter entities</span></span>
<span data-ttu-id="5b783-244">Hello hello 쿼리 작성기를 사용 하는 경우 테이블에 표시 되는 엔터티 집합을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-244">You can customize hello set of entities that appear in a table if you use hello query builder.</span></span>

1. <span data-ttu-id="5b783-245">tooopen hello 쿼리 작성기 보기에 대 한 테이블을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-245">tooopen hello query builder, open a table for viewing.</span></span>
2. <span data-ttu-id="5b783-246">Hello 테이블 보기의 도구 모음에서 hello 쿼리 작성기 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-246">Choose hello Query Builder button on hello table view’s toolbar.</span></span>
   
    <span data-ttu-id="5b783-247">hello **쿼리 작성기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-247">hello **Query Builder** dialog box appears.</span></span> <span data-ttu-id="5b783-248">hello 다음 그림에서는 쿼리를 작성 중인 hello 쿼리 작성기.</span><span class="sxs-lookup"><span data-stu-id="5b783-248">hello following illustration shows a query that's being built in hello query builder.</span></span>
   
    ![쿼리 작성기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. <span data-ttu-id="5b783-250">완료 하면 hello 대화 상자를 닫고 hello 쿼리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-250">When you’re done building hello query, close hello dialog box.</span></span> <span data-ttu-id="5b783-251">hello hello 쿼리의 결과 텍스트 형식이 WCF Data Services 필터로 텍스트 상자에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-251">hello resulting text form of hello query appears in a text box as a WCF Data Services filter.</span></span>
4. <span data-ttu-id="5b783-252">toorun hello 쿼리, hello 녹색 삼각형 아이콘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-252">toorun hello query, choose hello green triangle icon.</span></span>
   
    <span data-ttu-id="5b783-253">Hello에 표시 되는 엔터티 데이터를 필터링 할 수 있습니다 **테이블 디자이너** hello 필터 필드에 직접 WCF Data Services 필터 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-253">You can also filter entity data that appears in hello **Table Designer** if you enter a WCF Data Services filter string directly in hello filter field.</span></span> <span data-ttu-id="5b783-254">이 종류의 문자열 비슷한 tooa SQL WHERE 절이 있지만 toohello 서버에 HTTP 요청으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-254">This kind of string is similar tooa SQL WHERE clause but is sent toohello server as an HTTP request.</span></span> <span data-ttu-id="5b783-255">Tooconstruct 문자열을 필터링 하는 방법에 대 한 정보를 참조 하십시오. [hello 테이블 디자이너에 대 한 필터 문자열 생성](https://msdn.microsoft.com/library/azure/ff683669.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-255">For information about how tooconstruct filter strings, see [Constructing Filter Strings for hello Table Designer](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>
   
    <span data-ttu-id="5b783-256">hello 다음 그림과 유효한 필터 문자열의 예:</span><span class="sxs-lookup"><span data-stu-id="5b783-256">hello following illustration shows an example of a valid filter string:</span></span>
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a><span data-ttu-id="5b783-258">저장소 데이터 새로 고침</span><span class="sxs-lookup"><span data-stu-id="5b783-258">Refresh storage data</span></span>
<span data-ttu-id="5b783-259">서버 탐색기에 저장소 계정에서 데이터를 가져오면 tooor 연결 되 면 hello 작업 toocomplete tooa 분이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-259">When Server Explorer connects tooor gets data from a storage account, it might take up tooa minute for hello operation toocomplete.</span></span> <span data-ttu-id="5b783-260">연결할 수 없는 경우 hello 작업이 시간 초과 될 수 있습니다. 데이터를 검색 하는 동안 Visual Studio의 다른 부분에서 toowork를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-260">If it can’t connect, hello operation might time out. While data is retrieved, you can continue toowork in other parts of Visual Studio.</span></span> <span data-ttu-id="5b783-261">너무 오래 걸리는 경우 toocancel hello 작업이 선택 hello **새로 고침 중지** hello 서버 탐색기 도구 모음 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-261">toocancel hello operation if it’s taking too long, choose hello **Stop Refresh** button on hello Server Explorer toolbar.</span></span>

#### <a name="toorefresh-blob-container-data"></a><span data-ttu-id="5b783-262">toorefresh blob 컨테이너 데이터</span><span class="sxs-lookup"><span data-stu-id="5b783-262">toorefresh blob container data</span></span>
* <span data-ttu-id="5b783-263">선택 hello **Blob** 아래에 있는 노드 **저장소** hello 선택 **새로 고침** hello 서버 탐색기 도구 모음 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-263">Select hello **Blobs** node beneath **Storage** and choose hello **Refresh** button on hello Server Explorer toolbar.</span></span>
* <span data-ttu-id="5b783-264">표시 되는 blob의 toorefresh hello 목록 선택 hello **Execute** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-264">toorefresh hello list of blobs that is displayed, choose hello **Execute** button.</span></span>

#### <a name="toorefresh-table-data"></a><span data-ttu-id="5b783-265">toorefresh 테이블 데이터</span><span class="sxs-lookup"><span data-stu-id="5b783-265">toorefresh table data</span></span>
* <span data-ttu-id="5b783-266">선택 hello **테이블** 아래에 있는 노드 **저장소** hello 선택 **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-266">Select hello **Tables** node beneath **Storage** and choose hello **Refresh** button.</span></span>
* <span data-ttu-id="5b783-267">hello에 표시 되는 엔터티의 toorefresh hello 목록을 **테이블 디자이너**, hello 선택 **Execute** hello 단추 **테이블 디자이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-267">toorefresh hello list of entities that is displayed in hello **Table Designer**, choose hello **Execute** button on hello **Table Designer**.</span></span>

#### <a name="toorefresh-queue-data"></a><span data-ttu-id="5b783-268">toorefresh 큐 데이터</span><span class="sxs-lookup"><span data-stu-id="5b783-268">toorefresh queue data</span></span>
* <span data-ttu-id="5b783-269">선택 hello **큐** 노드를 선택한 후 hello **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-269">Select hello **Queues** node, and then choose hello **Refresh** button.</span></span>

#### <a name="toorefresh-all-items-in-a-storage-account"></a><span data-ttu-id="5b783-270">저장소 계정에 있는 모든 항목 toorefresh</span><span class="sxs-lookup"><span data-stu-id="5b783-270">toorefresh all items in a storage account</span></span>
* <span data-ttu-id="5b783-271">Hello 계정 이름을 선택 하 고 hello 선택 **새로 고침** 서버 탐색기에 대 한 hello 도구 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-271">Choose hello account name, and then choose hello **Refresh** button on hello toolbar for Server Explorer.</span></span>

### <a name="add-storage-accounts-by-using-server-explorer"></a><span data-ttu-id="5b783-272">서버 탐색기를 사용하여 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="5b783-272">Add storage accounts by using Server Explorer</span></span>
<span data-ttu-id="5b783-273">두 가지가 tooadd 저장소 계정을 서버 탐색기를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-273">There are two ways tooadd storage accounts by using Server Explorer.</span></span> <span data-ttu-id="5b783-274">Azure 구독에서 새 저장소 계정을 만들거나 기존 저장소 계정을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-274">You can create a new storage account in your Azure subscription, or you can attach an existing storage account.</span></span>

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a><span data-ttu-id="5b783-275">서버 탐색기를 사용 하 여 새 저장소 계정 toocreate</span><span class="sxs-lookup"><span data-stu-id="5b783-275">toocreate a new storage account by using Server Explorer</span></span>
1. <span data-ttu-id="5b783-276">서버 탐색기에서 hello 저장소 노드에 대 한 hello 바로 가기 메뉴를 열고 하 고 저장소 계정 만들기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-276">In Server Explorer, open hello shortcut menu for hello Storage node, and then choose Create Storage Account.</span></span>
   
    ![새 Azure 저장소 계정 만들기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. <span data-ttu-id="5b783-278">선택 또는 입력 hello hello에 새 저장소 계정에 대 한 정보를 다음 hello **저장소 계정 만들기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5b783-278">Select or enter hello following information for hello new storage account in hello **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="5b783-279">hello Azure 구독 toowhich tooadd hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-279">hello Azure subscription toowhich you want tooadd hello storage account.</span></span>
   * <span data-ttu-id="5b783-280">hello 이름 toouse hello 새 저장소 계정에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-280">hello name you want toouse for hello new storage account.</span></span>
   * <span data-ttu-id="5b783-281">hello 지역 또는 선호도 그룹 (예: 미국 서 부 또는 아시아의 경우).</span><span class="sxs-lookup"><span data-stu-id="5b783-281">hello region or affinity group (such as West US or East Asia).</span></span>
   * <span data-ttu-id="5b783-282">형식 hello 복제 원하는 toouse 지리적 중복 같은 hello 저장소 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-282">hello type of replication you want toouse for hello storage account, such as Geo-Redundant.</span></span>
3. <span data-ttu-id="5b783-283">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-283">Choose **Create**.</span></span>
   
    <span data-ttu-id="5b783-284">hello에 hello 새 저장소 계정을 표시 **저장소** 솔루션 탐색기의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-284">hello new storage account appears in hello **Storage** list in Solution Explorer.</span></span>

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a><span data-ttu-id="5b783-285">서버 탐색기를 사용 하 여 기존 저장소 계정 tooattach</span><span class="sxs-lookup"><span data-stu-id="5b783-285">tooattach an existing storage account by using Server Explorer</span></span>
1. <span data-ttu-id="5b783-286">서버 탐색기에서 hello Azure 저장소 노드에 대 한 hello 바로 가기 메뉴를 열고 한 다음 **외부 저장소 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-286">In Server Explorer, open hello shortcut menu for hello Azure storage node, and then choose **Attach External Storage**.</span></span>
   
    ![기존 저장소 계정 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. <span data-ttu-id="5b783-288">선택 또는 입력 hello hello에 새 저장소 계정에 대 한 정보를 다음 hello **저장소 계정 만들기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5b783-288">Select or enter hello following information for hello new storage account in hello **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="5b783-289">hello 이름 tooattach 원하는 hello 기존 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-289">hello name of hello existing storage account you want tooattach.</span></span> <span data-ttu-id="5b783-290">이름을 입력 하거나 hello 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-290">You can enter a name or select it from hello list.</span></span>
   * <span data-ttu-id="5b783-291">hello에 대 한 hello 키 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-291">hello key for hello selected storage account.</span></span> <span data-ttu-id="5b783-292">저장소 계정을 선택할 때 일반적으로 이 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-292">This value is typically provided for you when you select a storage account.</span></span> <span data-ttu-id="5b783-293">Visual Studio tooremember hello 저장소 계정 키 hello 사용자 이름 및 암호 계정 키 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-293">If you want Visual Studio tooremember hello storage account key, select hello Remember account key box.</span></span>
   * <span data-ttu-id="5b783-294">hello 프로토콜 toouse tooconnect toohello 저장소 계정, HTTP, HTTPS 또는 사용자 지정 끝점 등입니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-294">hello protocol toouse tooconnect toohello storage account, such as HTTP, HTTPS, or a custom endpoint.</span></span> <span data-ttu-id="5b783-295">참조 [연결 문자열의 tooConfigure 방법](https://msdn.microsoft.com/library/azure/ee758697.aspx) 사용자 지정 끝점에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-295">See [How tooConfigure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx) for more information about custom endpoints.</span></span>

### <a name="tooview-hello-secondary-endpoints"></a><span data-ttu-id="5b783-296">tooview hello 보조 끝점</span><span class="sxs-lookup"><span data-stu-id="5b783-296">tooview hello secondary endpoints</span></span>
* <span data-ttu-id="5b783-297">Hello를 사용 하 여 저장소 계정을 만든 경우 **읽기 액세스 지역 중복** 복제 옵션을 보조 끝점을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-297">If you created a storage account using hello **Read-Access Geo Redundant** replication option, you can view its secondary endpoints.</span></span> <span data-ttu-id="5b783-298">Hello 계정 이름에 대 한 hello 바로 가기 메뉴를 열고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-298">Open hello shortcut menu for hello account name, and then choose **Properties**.</span></span>
  
    ![저장소 보조 끝점](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a><span data-ttu-id="5b783-300">서버 탐색기에서 저장소 계정 tooremove</span><span class="sxs-lookup"><span data-stu-id="5b783-300">tooremove a storage account from Server Explorer</span></span>
* <span data-ttu-id="5b783-301">서버 탐색기에서 hello 계정 이름에 대 한 hello 바로 가기 메뉴를 열고 한 다음 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-301">In Server Explorer, open hello shortcut menu for hello account name, and then choose **Delete**.</span></span> <span data-ttu-id="5b783-302">저장소 계정을 삭제하면 해당 계정에 저장된 키 정보도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-302">If you delete a storage account, any saved key information for that account is also removed.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5b783-303">서버 탐색기에서 저장소 계정을 삭제 하면 저장소 계정 또는; 포함 된 모든 데이터가 적용 되지 않습니다. 단순히 서버 탐색기에서 hello 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-303">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains; it simply removes hello reference from Server Explorer.</span></span> <span data-ttu-id="5b783-304">toopermanently 저장소 계정을 삭제, hello를 사용 하 여 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-304">toopermanently delete a storage account, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
  > 
  > 

## <a name="next-steps"></a><span data-ttu-id="5b783-305">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b783-305">Next steps</span></span>
<span data-ttu-id="5b783-306">toolearn 방법에 대 한 Azure 저장소 서비스를 사용 하 여, 참조 [hello Azure 저장소 서비스에 액세스](https://msdn.microsoft.com/library/azure/ee405490.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b783-306">toolearn more about how use Azure storage services, see [Accessing hello Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span></span>

