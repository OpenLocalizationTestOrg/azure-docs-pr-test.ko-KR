---
title: "내보내기 작업에 대 한 Azure 가져오기/내보내기 aaaCreate | Microsoft Docs"
description: "내보내기 toocreate hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 작업 하는 방법에 대해 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="6d935-103">Hello Azure 가져오기/내보내기 서비스에 대 한 내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="6d935-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="6d935-104">Hello REST API를 사용 하 여 hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 내보내기 작업 만들기 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="6d935-105">Tooexport를 blob hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="6d935-106">배송 위치 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d935-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="6d935-107">Hello 내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="6d935-107">Creating hello export job.</span></span>

-   <span data-ttu-id="6d935-108">지원 되는 운송 업체 서비스를 통해에 빈 드라이브 tooMicrosoft으로 배송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="6d935-109">Hello 패키지 정보로 hello 내보내기 작업을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="6d935-110">Microsoft에서 다시 수신 hello 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="6d935-111">참조 [hello Windows Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](storage-import-export-service.md) hello 가져오기/내보내기 서비스 및 설명 하는 자습서에 대 한 개요 방법을 toouse hello [Azure 포털](https://portal.azure.com/) toocreate 가져오기 및 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="6d935-112">Blob tooexport 선택</span><span class="sxs-lookup"><span data-stu-id="6d935-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="6d935-113">내보내기 작업 toocreate tooprovide blob 저장소 계정에서 tooexport 되도록 목록이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="6d935-114">몇 가지 tooselect toobe 내보낼 blob:</span><span class="sxs-lookup"><span data-stu-id="6d935-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="6d935-115">상대 blob 경로 tooselect 단일 blob 및 해당 스냅숏을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="6d935-116">상대 blob 경로 tooselect 해당 스냅숏을 제외한 단일 blob를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="6d935-117">상대 blob 경로 스냅숏 시간 tooselect 단일 스냅숏 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="6d935-118">접두사를 지정 하는 hello로 blob 접두사 tooselect 모든 blob 및 스냅숏을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="6d935-119">모든 blob 및 스냅숏을 hello 저장소 계정에서 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="6d935-120">지정 하는 방법에 대 한 자세한 내용은 tooexport blob에 대 한 참조 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="6d935-121">배송 위치 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d935-121">Obtaining your shipping location</span></span>
<span data-ttu-id="6d935-122">내보내기 작업을 만들기 전에 tooobtain 배송 위치 이름 및 주소에서 필요한 호출 hello [가져오기 위치](https://portal.azure.com) 또는 [위치 나열](/rest/api/storageimportexport/listlocations) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="6d935-123">`List Locations`는 위치 목록과 해당 우편 발송 주소 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="6d935-124">Hello 반환 된 목록에서에서 위치를 선택 하 고 인 하드 드라이브 toothat 주소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="6d935-125">Hello를 사용할 수도 있습니다 `Get Location` 작업 tooobtain hello 특정 위치에 대 한 주소를 직접 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="6d935-126">Tooobtain hello 배송 위치 아래에 있는 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="6d935-127">저장소 계정의 hello 위치의 hello 이름을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="6d935-128">Hello이이 값을 확인할 수 있습니다 **위치** 필드 hello 저장소 계정에 **대시보드** hello 기본 포털 이나 hello 서비스 관리 API 작업을 사용 하 여에 대 한 쿼리 [가져오기 저장소 계정 속성](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="6d935-129">Hello를 호출 하 여이 저장소 계정을 사용할 수 있는 tooprocess 있는 hello 위치를 검색할 `Get Location` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="6d935-130">경우 hello `AlternateLocations` 자체 hello 위치를 포함 하는 hello 위치의 속성을 덮어쓰려면 toouse이이 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="6d935-131">그렇지 않으면 hello 호출 `Get Location` hello 대체 위치 중 하나를 사용 하 여 다시 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="6d935-132">유지 관리에 대 한 hello 원래 위치를 일시적으로 닫혔을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="6d935-133">Hello 내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="6d935-133">Creating hello export job</span></span>
 <span data-ttu-id="6d935-134">toocreate hello 내보내기 작업을 호출 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="6d935-135">다음 정보는 tooprovide hello이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="6d935-136">Hello 작업에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-136">A name for hello job.</span></span>

-   <span data-ttu-id="6d935-137">hello 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-137">hello storage account name.</span></span>

-   <span data-ttu-id="6d935-138">hello hello 이전 단계에서 얻은 위치 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="6d935-139">작업 유형(내보내기)입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-139">A job type (Export).</span></span>

-   <span data-ttu-id="6d935-140">hello 반송 주소는 hello 내보내기 작업이 완료 된 후 hello 드라이브를 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="6d935-141">hello는 blob (또는 blob 접두사) 목록을 toobe가 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="6d935-142">드라이브 배송</span><span class="sxs-lookup"><span data-stu-id="6d935-142">Shipping your drives</span></span>
 <span data-ttu-id="6d935-143">다음으로, 내보낸 toobe 선택한 hello blob 기반 toosend 필요한 드라이브 hello Azure 가져오기/내보내기 도구 toodetermine hello 번호를 사용 하 고 hello 드라이브 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="6d935-144">Hello 참조 [Azure 가져오기/내보내기 도구 참조](storage-import-export-tool-how-to-v1.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="6d935-145">단일에서 패키지 hello 드라이브 패키지 및 toohello 보내줄 hello에서 가져온 주소로 앞 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="6d935-146">Note hello hello 다음 단계에 대 한 패키지 수를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="6d935-147">패키지의 추적 번호를 제공하는 지원 운송업체 서비스를 통해 드라이브를 배송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="6d935-148">패키지 정보를 사용 hello 내보내기 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="6d935-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="6d935-149">추적 번호를 사용 하는 다음 호출 hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 작업 tooupdated hello 배송 업체 이름과 추적 번호 hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="6d935-150">Hello 드라이브 수, hello 반환 주소 및 hello 배송 날짜도 선택적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="6d935-151">Hello 패키지 받기</span><span class="sxs-lookup"><span data-stu-id="6d935-151">Receiving hello package</span></span>
 <span data-ttu-id="6d935-152">내보내기 작업을 처리 한 후 암호화 된 데이터와 함께 tooyou 드라이브가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="6d935-153">각 호출 hello로 hello 드라이브에 대 한 hello BitLocker 키를 검색할 수 있습니다 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="6d935-154">Hello 키를 사용 하 여 hello 드라이브 잠금을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="6d935-155">각 드라이브에 hello 드라이브 매니페스트 파일에는 각 파일에 대 한 원래 blob 주소도 hello: hello 드라이브에 파일의 hello 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6d935-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d935-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d935-156">Next steps</span></span>

* [<span data-ttu-id="6d935-157">Hello 가져오기/내보내기 서비스 REST API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6d935-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
