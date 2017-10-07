---
title: "aaaImport Azure Redis Cache에서 데이터 내보내기 및 | Microsoft Docs"
description: "자세한 내용은 방법 premium Azure Redis Cache 인스턴스와 blob 저장소에서 데이터 tooand tooimport 및 내보내기"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="721f3-103">Azure Redis Cache에서 데이터 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="721f3-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="721f3-104">가져오기/내보내기는 수 있는 tooimport 데이터를 Azure Redis Cache 또는 Azure Redis 캐시의 데이터를 내보내는에서 가져오기 및 내보내기 Redis 캐시 데이터베이스 (RDB) 스냅숏은 Azure의 프리미엄 캐시 tooa blob으로 Azure Redis Cache 데이터 관리 작업을 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-104">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="721f3-105">**내보내기** -Azure Redis 캐시 RDB 스냅숏을 tooa 페이지 Blob을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-105">**Export** - you can export your Azure Redis Cache RDB snapshots tooa Page Blob.</span></span>
- <span data-ttu-id="721f3-106">**가져오기** - Redis Cache RDB 스냅숏을 페이지 Blob 또는 블록 Blob으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="721f3-107">가져오기/내보내기 toomigrate 서로 다른 Azure Redis Cache 인스턴스 간에 사용 하면 또는 hello 캐시 사용 하기 전에 데이터를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-107">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="721f3-108">이 문서는 가져오기 및 내보내기 Azure Redis Cache를 사용 하 여 데이터에 대 한 지침 제공 하 고 hello 대답을 제공 toocommonly 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides hello answers toocommonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="721f3-109">가져오기/내보내기는 미리 보기 상태이며, [프리미엄 계층](cache-premium-tier-intro.md) 캐시에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="721f3-110">가져오기</span><span class="sxs-lookup"><span data-stu-id="721f3-110">Import</span></span>
<span data-ttu-id="721f3-111">가져오기에는 클라우드 또는 Linux, Windows 또는 Amazon 웹 서비스 등과 같은 모든 클라우드 공급자에서 실행 되는 Redis를 포함 하 여 환경에서 실행 중인 모든 Redis 서버에서 사용 되는 toobring Redis 호환 RDB 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-111">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="721f3-112">데이터 가져오기는 쉽게 toocreate 미리 채워진된 데이터와 함께 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-112">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="721f3-113">Hello 가져오기 프로세스 동안 Azure Redis Cache hello RDB 파일을 Azure 저장소에서 메모리에 로드 한 다음 hello 캐시로 hello 키를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-113">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory and then inserts hello keys into hello cache.</span></span>

> [!NOTE]
> <span data-ttu-id="721f3-114">Hello 가져오기 작업을 시작 하기 전에 확인 Redis 데이터베이스 (RDB) 파일 또는 파일을 페이지도 업로드 하거나 동일 hello에서 Azure 저장소에 블록 blob과 Azure Redis 캐시 인스턴스의 지역 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-114">Before beginning hello import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in hello same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="721f3-115">자세한 내용은 [Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="721f3-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="721f3-116">Hello를 사용 하 여 RDB 파일을 내보낸 경우 [Azure Redis 캐시 내보내기](#export) RDB 파일 페이지 blob에 이미 저장 되어 기능과 가져올 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-116">If you exported your RDB file using hello [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="721f3-117">하나 이상의 tooimport 캐시 blob를 내보낸 [tooyour 캐시 찾아보기](cache-configure.md#configure-redis-cache-settings) 에 Azure 포털 hello 및 클릭 **데이터를 가져올** hello에서 **리소스 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-117">tooimport one or more exported cache blobs, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Import data** from hello **Resource menu**.</span></span>

    ![데이터 가져오기][cache-import-data]
2. <span data-ttu-id="721f3-119">클릭 **선택 Blob(s)** hello 데이터 tooimport 포함 된 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-119">Click **Choose Blob(s)** and select hello storage account that contains hello data tooimport.</span></span>

    ![저장소 계정 선택][cache-import-choose-storage-account]
3. <span data-ttu-id="721f3-121">Hello 데이터 tooimport를 포함 하는 hello 컨테이너를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-121">Click hello container that contains hello data tooimport.</span></span>

    ![컨테이너 선택][cache-import-choose-container]
4. <span data-ttu-id="721f3-123">하나 이상의 blob tooimport hello blob 이름의 hello 영역 toohello 왼쪽을 클릭 하 여 선택한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-123">Select one or more blobs tooimport by clicking hello area toohello left of hello blob name, and then click **Select**.</span></span>

    ![Blob 선택][cache-import-choose-blobs]
5. <span data-ttu-id="721f3-125">클릭 **가져올** toobegin hello 가져오기 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-125">Click **Import** toobegin hello import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="721f3-126">hello 가져오기 프로세스 동안 hello 캐시는 캐시 클라이언트에서 액세스할 수 없습니다 및 hello 캐시에 기존 데이터가 모두 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-126">hello cache is not accessible by cache clients during hello import process, and any existing data in hello cache is deleted.</span></span>
   >
   >

    ![가져오기][cache-import-blobs]

    <span data-ttu-id="721f3-128">Hello Azure 포털에서에서 다음과 같은 hello 알림이 하거나 hello에 hello 이벤트를 확인 하 여 hello 가져오기 작업의 hello 진행률을 모니터링할 수 있습니다 [감사 로그](../azure-resource-manager/resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-128">You can monitor hello progress of hello import operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![가져오기 진행][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="721f3-130">내보내기</span><span class="sxs-lookup"><span data-stu-id="721f3-130">Export</span></span>
<span data-ttu-id="721f3-131">내보내기는 Azure Redis Cache tooRedis 호환 RDB 파일에 저장 된 tooexport hello 데이터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-131">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB file(s).</span></span> <span data-ttu-id="721f3-132">Azure Redis Cache 인스턴스 tooanother 또는 tooanother Redis 서버 하나에서이 기능 toomove 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-132">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="721f3-133">Hello 내보내기 과정에서 임시 파일 VM 호스트 hello Azure Redis Cache 서버 인스턴스 및 hello 파일은 저장소 계정을 지정 하는 업로드 된 toohello hello에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-133">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="721f3-134">실패 또는 성공 상태가 hello 내보내기 작업이 완료 되 면 hello 임시 파일이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-134">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

1. <span data-ttu-id="721f3-135">tooexport hello hello 캐시 toostorage의 현재 내용을 [tooyour 캐시 찾아보기](cache-configure.md#configure-redis-cache-settings) Azure 포털 hello와 클릭 **데이터 내보내기** hello에서 **리소스 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-135">tooexport hello current contents of hello cache toostorage, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Export data** from hello **Resource menu**.</span></span>

    ![저장소 컨테이너 선택][cache-export-data-choose-storage-container]
2. <span data-ttu-id="721f3-137">클릭 **저장소 컨테이너 선택** hello 원하는 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-137">Click **Choose Storage Container** and select hello desired storage account.</span></span> <span data-ttu-id="721f3-138">저장소 계정 hello hello에 있어야 합니다. 동일한 구독 및 지역이 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-138">hello storage account must be in hello same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="721f3-139">내보내기는 페이지 Blob을 사용하고, 클래식 및 Resource Manager 저장소 계정 양쪽 모두에서 지원되지만, [Blob Storage 계정](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)에서는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![저장소 계정][cache-export-data-choose-account]
3. <span data-ttu-id="721f3-141">Hello 필요한 blob 컨테이너 및 클릭 선택 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-141">Choose hello desired blob container and click **Select**.</span></span> <span data-ttu-id="721f3-142">새 컨테이너 toouse 클릭 **컨테이너 추가** tooadd 선택 되어 있고 첫 번째 hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-142">toouse new a container, click **Add Container** tooadd it first and then select it from hello list.</span></span>

    ![저장소 컨테이너 선택][cache-export-data-container]
4. <span data-ttu-id="721f3-144">입력 **Blob 이름 접두사** 클릭 **내보내기** toostart hello 내보내기 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-144">Type a **Blob name prefix** and click **Export** toostart hello export process.</span></span> <span data-ttu-id="721f3-145">hello blob 이름 접두사는이 내보내기 작업에 의해 생성 된 파일의 사용 되는 tooprefix hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-145">hello blob name prefix is used tooprefix hello names of files generated by this export operation.</span></span>

    ![내보내기][cache-export-data]

    <span data-ttu-id="721f3-147">Hello Azure 포털에서에서 다음과 같은 hello 알림이 하거나 hello에 hello 이벤트를 확인 하 여 hello 내보내기 작업의 hello 진행률을 모니터링할 수 있습니다 [감사 로그](../azure-resource-manager/resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-147">You can monitor hello progress of hello export operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![데이터 내보내기 완료][cache-export-data-export-complete]

    <span data-ttu-id="721f3-149">캐시는 hello 내보내기 프로세스 중에 사용 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-149">Caches remain available for use during hello export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="721f3-150">가져오기/내보내기 FAQ</span><span class="sxs-lookup"><span data-stu-id="721f3-150">Import/Export FAQ</span></span>
<span data-ttu-id="721f3-151">이 섹션에서는 hello 가져오기/내보내기 기능에 대 한 질문과 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-151">This section contains frequently asked questions about hello Import/Export feature.</span></span>

* [<span data-ttu-id="721f3-152">어떤 가격 책정 계층에서 가져오기/내보내기를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="721f3-153">Redis 서버에서 데이터를 가져올 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="721f3-154">가져올 수 있는 RDB 버전은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="721f3-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="721f3-155">Import/Export 작업을 진행하는 동안 내 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="721f3-156">Redis 클러스터에 가져오기/내보내기를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="721f3-157">가져오기/내보내기는 사용자 지정 데이터베이스 설정에서 어떻게 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="721f3-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="721f3-158">가져오기/내보내기가 Redis 지속성과 어떻게 다른가요?</span><span class="sxs-lookup"><span data-stu-id="721f3-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="721f3-159">PowerShell, CLI, 또는 다른 관리 클라이언트를 사용하여 가져오기/내보내기를 자동화할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="721f3-160">가져오기/내보내기 작업을 진행하는 동안 시간 초과 오류가 발생했습니다. 무엇을 의미하나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="721f3-161">내 데이터 tooAzure Blob 저장소를 내보낼 때 오류가 나타났습니다. 어떻게 된 건가요?</span><span class="sxs-lookup"><span data-stu-id="721f3-161">I got an error when exporting my data tooAzure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="721f3-162">어떤 가격 책정 계층에서 가져오기/내보내기를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="721f3-163">가져오기/내보내기는 hello 프리미엄 가격 책정 계층 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-163">Import/Export is available only in hello premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="721f3-164">Redis 서버에서 데이터를 가져올 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="721f3-165">예, 또한 Azure Redis Cache 인스턴스에서 내보낸 tooimporting 데이터를 가져올 수 있습니다 RDB 파일에서 모든 클라우드 또는 Linux, Windows 또는 Amazon 웹 서비스와 같은 클라우드 공급자와 같은 환경에서 실행 중인 모든 Redis 서버.</span><span class="sxs-lookup"><span data-stu-id="721f3-165">Yes, in addition tooimporting data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="721f3-166">toodo이 업로드 hello RDB 파일 원하는 hello Redis 서버에서 Azure 저장소 계정 및 내보낸 후에 페이지 또는 블록 blob에 것으로 premium Azure Redis 캐시 인스턴스의입니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-166">toodo this, upload hello RDB file from hello desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="721f3-167">예를 들어 프로덕션 캐시에서 tooexport hello 데이터를 원하는 및 테스트 또는 마이그레이션에 대 한 스테이징 환경의 일부로 사용 되는 캐시에 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-167">For example, you may want tooexport hello data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="721f3-168">toosuccessfully는 페이지 blob을 hello 페이지 blob 크기를 사용 하 여 512 바이트 경계에 정렬 해야 하는 경우 Azure Redis Cache가 아닌 Redis 서버에서 내보낸 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-168">toosuccessfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, hello page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="721f3-169">샘플 코드 tooperform에 대 한 모든 필수 바이트 안쪽 여백, 참조 [샘플 페이지 블로그 업로드](https://github.com/JimRoberts-MS/SamplePageBlobUpload)합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-169">For sample code tooperform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="721f3-170">가져올 수 있는 RDB 버전은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="721f3-170">What RDB versions can I import?</span></span>

<span data-ttu-id="721f3-171">Azure Redis Cache는 RDB 버전 7을 통해 RDB 가져오기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="721f3-172">Import/Export 작업을 진행하는 동안 내 캐시를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="721f3-173">**내보내기** -캐시를 사용할 수 있는 상태로 유지 하 고 내보내기 작업 중 toouse 캐시를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-173">**Export** - Caches remain available and you can continue toouse your cache during an export operation.</span></span>
* <span data-ttu-id="721f3-174">**가져올** -캐시 가져오기 작업이 시작 될 때 사용할 수 없게 되 고 hello 가져오기 작업이 완료 될 때 사용 하기 위해 사용할 수 있는 수입니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when hello import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="721f3-175">Redis 클러스터에 가져오기/내보내기를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="721f3-176">예, 클러스터형 캐시와 비클러스터형 캐시 사이에서 가져오기/내보내기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="721f3-177">Redis 클러스터는 [0 데이터베이스만 지원](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)하기 때문에, 0 이외의 데이터베이스에 저장된 데이터를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="721f3-178">클러스터 된 캐시 데이터를 가져올 때 hello 키 hello 클러스터의 hello 분할 영역 보다 짧은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-178">When clustered cache data is imported, hello keys are redistributed among hello shards of hello cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="721f3-179">가져오기/내보내기는 사용자 지정 데이터베이스 설정에서 어떻게 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="721f3-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="721f3-180">일부 가격 책정 계층에는 다른 [제한 데이터베이스](cache-configure.md#databases)hello에 대 한 사용자 지정 값을 구성한 경우 가져올 때 몇 가지 고려 사항은 `databases` 캐시 만들기 중에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="721f3-181">가격 책정 계층 낮은 tooa 가져올 때 `databases` 내보낸 hello 계층 보다 제한:</span><span class="sxs-lookup"><span data-stu-id="721f3-181">When importing tooa pricing tier with a lower `databases` limit than hello tier from which you exported:</span></span>
  * <span data-ttu-id="721f3-182">Hello 기본 개수를 사용 하는 경우 `databases`을 만드는데 모든 가격 책정 계층에 대해 16 개, 어떤 데이터도 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-182">If you are using hello default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="721f3-183">사용자 지정 된 수를 사용 하는 경우 `databases` hello에 대 한 hello 제한 내에서 위치 합니다. 계층 가져오는 toowhich 하 어떤 데이터도 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-183">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are importing, no data is lost.</span></span>
  * <span data-ttu-id="721f3-184">Hello 새 계층의 hello 한계를 초과 하는 데이터베이스에 데이터를 포함 하는 내보낸된 데이터를 hello 데이터 해당 상위 데이터베이스를 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-184">If your exported data contained data in a database that exceeds hello limits of hello new tier, hello data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="721f3-185">가져오기/내보내기가 Redis 지속성과 어떻게 다른가요?</span><span class="sxs-lookup"><span data-stu-id="721f3-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="721f3-186">Azure Redis Cache 지 속성 Redis tooAzure 저장소에에서 저장 된 toopersist 데이터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-186">Azure Redis Cache persistence allows you toopersist data stored in Redis tooAzure Storage.</span></span> <span data-ttu-id="721f3-187">지 속성 구성 된 경우 Azure Redis Cache에서 구성 가능한 백업 빈도에 따라 Redis 이진 형식 toodisk hello Redis cache의 스냅숏을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-187">When persistence is configured, Azure Redis Cache persists a snapshot of hello Redis cache in a Redis binary format toodisk based on a configurable backup frequency.</span></span> <span data-ttu-id="721f3-188">재해 기본 hello와 복제본 캐시 모두 비활성화 하는 경우 자동으로 가장 최근의 스냅숏으로 hello를 사용 하 여 데이터를 캐시 하는 hello 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-188">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache data is restored automatically using hello most recent snapshot.</span></span> <span data-ttu-id="721f3-189">자세한 내용은 참조 [어떻게 Premium Azure Redis Cache에 대 한 데이터 보존 tooconfigure](cache-how-to-premium-persistence.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-189">For more information, see [How tooconfigure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="721f3-190">가져오기 / 내보내기 있습니다 toobring 데이터를 또는 Azure Redis Cache에서 내보내기를 합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-190">Import/ Export allows you toobring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="721f3-191">Redis 지속성을 사용하여 백업 및 복원을 구성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="721f3-192">PowerShell, CLI, 또는 다른 관리 클라이언트를 사용하여 가져오기/내보내기를 자동화할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="721f3-193">예, PowerShell 명령 참조 [tooimport Redis 캐시](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) 및 [tooexport Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache)합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-193">Yes, for PowerShell instructions see [tooimport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [tooexport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="721f3-194">가져오기/내보내기 작업을 진행하는 동안 시간 초과 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="721f3-195">무엇을 의미하나요?</span><span class="sxs-lookup"><span data-stu-id="721f3-195">What does it mean?</span></span>
<span data-ttu-id="721f3-196">Hello에 계속 남아 있는 경우 **데이터를 가져올** 또는 **데이터 내보내기** 블레이드에서 hello 작업을 시작 하기 전에 15 분 이상에 대 한 오류가 발생 된 다음 예에서는 오류 메시지와 비슷한 toohello:</span><span class="sxs-lookup"><span data-stu-id="721f3-196">If you remain on hello **Import data** or **Export data** blade for longer than 15 minutes before initiating hello operation, you receive an error with an error message similar toohello following example:</span></span>

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

<span data-ttu-id="721f3-197">tooresolve 시작 hello 가져오기 또는 내보내기 작업을이 15 분이 경과 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="721f3-197">tooresolve this, initiate hello import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a><span data-ttu-id="721f3-198">내 데이터 tooAzure Blob 저장소를 내보낼 때 오류가 나타났습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-198">I got an error when exporting my data tooAzure Blob Storage.</span></span> <span data-ttu-id="721f3-199">어떻게 된 건가요?</span><span class="sxs-lookup"><span data-stu-id="721f3-199">What happened?</span></span>
<span data-ttu-id="721f3-200">내보내기는 페이지 Blob으로 저장된 RDB 파일에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="721f3-201">현재 핫 및 쿨 계층의 Blob Storage 계정을 비롯한 다른 Blob 형식이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="721f3-202">자세한 내용은 [Blob Storage 계정](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="721f3-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="721f3-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="721f3-203">Next steps</span></span>
<span data-ttu-id="721f3-204">Toouse 더 프리미엄 기능을 캐시 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="721f3-204">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="721f3-205">Toohello Azure Redis Cache 프리미엄 계층 소개</span><span class="sxs-lookup"><span data-stu-id="721f3-205">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
