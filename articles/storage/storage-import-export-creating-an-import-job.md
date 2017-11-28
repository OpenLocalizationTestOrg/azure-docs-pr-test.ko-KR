---
title: "가져오기 작업에 대 한 Azure 가져오기/내보내기 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 가져오기."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="2a291-103">Hello Azure 가져오기/내보내기 서비스에 대 한 가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="2a291-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="2a291-104">Hello REST API를 사용 하 여 hello Microsoft Azure 가져오기/내보내기 서비스에 대 한 가져오기 작업 만들기 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="2a291-105">Azure 가져오기/내보내기 도구 hello로 드라이브를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="2a291-106">Hello 위치 toowhich tooship hello 드라이브를 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="2a291-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="2a291-107">Hello 가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="2a291-107">Creating hello import job.</span></span>

-   <span data-ttu-id="2a291-108">지원 되는 운송 업체 서비스를 통해 tooMicrosoft 드라이브 hello를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="2a291-109">세부 정보를 전달 하는 hello로 hello 가져오기 작업을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="2a291-110">참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](storage-import-export-service.md) hello 가져오기/내보내기 서비스 및 설명 하는 자습서에 대 한 개요 방법을 toouse hello [Azure 포털](https://portal.azure.com/) toocreate 가져오기 및 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="2a291-111">Azure 가져오기/내보내기 도구 hello가 있는 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="2a291-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="2a291-112">가져오기 작업에 대 한 hello 단계 tooprepare 드라이브는 동일한 jobvia hello 포털 hello 또는 hello REST API를 통해 만드는 지 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="2a291-113">다음은 드라이브 준비에 대한 간단한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="2a291-114">Toohello 참조 [Azure 가져오기 ExportTool 참조](storage-import-export-tool-how-to-v1.md) 자세한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="2a291-115">Hello Azure 가져오기/내보내기 도구를 다운로드할 수 있습니다 [여기](http://go.microsoft.com/fwlink/?LinkID=301900)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="2a291-116">드라이브를 준비하는 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="2a291-117">가져온 hello 데이터 toobe를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="2a291-118">Windows Azure 저장소에 hello 대상 blob을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="2a291-119">Azure 가져오기/내보내기 도구 toocopy hello를 사용 하 여 데이터 tooone 또는 더 많은 하드 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="2a291-120">준비가 된 것 처럼 각 hello 드라이브 hello Azure 가져오기/내보내기 도구를 사용 하면 매니페스트 파일 또한 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="2a291-121">매니페스트 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-121">A manifest file contains:</span></span>

-   <span data-ttu-id="2a291-122">모든 hello 파일 업로드 및 이러한 파일 tooblobs hello 매핑을 위한의 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="2a291-123">각 파일의 hello 세그먼트의 체크섬입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="2a291-124">각 blob과 함께 메타 데이터 및 속성 tooassociate hello에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="2a291-125">Hello 컨테이너에 있는 기존 blob 이름을 업로드 될 blob hello에는 목록 hello 동작 tootake 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="2a291-126">가능한 옵션은: a) hello blob 버전으로 덮어쓰기 hello 파일, b) hello 기존 blob 및 hello 파일 업로드 건너뛰기 유지, c) 다른 파일과 충돌 하지 않는 접미사 toohello 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="2a291-127">배송 위치 가져오기</span><span class="sxs-lookup"><span data-stu-id="2a291-127">Obtaining your shipping location</span></span>

<span data-ttu-id="2a291-128">가져오기 작업을 만들기 전에 tooobtain 배송 위치 이름 및 주소에서 필요한 호출 hello [위치 나열](/rest/api/storageimportexport/listlocations) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="2a291-129">`List Locations`는 위치 목록과 해당 우편 발송 주소 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="2a291-130">Hello 반환 된 목록에서에서 위치를 선택 하 고 인 하드 드라이브 toothat 주소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="2a291-131">Hello를 사용할 수도 있습니다 `Get Location` 작업 tooobtain hello 특정 위치에 대 한 주소를 직접 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="2a291-132">Tooobtain hello 배송 위치 아래에 있는 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="2a291-133">저장소 계정의 hello 위치의 hello 이름을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="2a291-134">Hello이이 값을 확인할 수 있습니다 **위치** 필드 hello 저장소 계정에 **대시보드** hello Azure 포털 또는 hello 서비스 관리 API 작업을 사용 하 여 쿼리할에 [저장소 가져오기 계정 속성](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="2a291-135">Hello를 호출 하 여 hello 위치를 사용할 수 있는 tooprocess이 저장소 계정을 검색 `Get Location` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="2a291-136">경우 hello `AlternateLocations` 자체 hello 위치를 포함 하는 hello 위치의 속성을 덮어쓰려면 toouse이이 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="2a291-137">그렇지 않으면 hello 호출 `Get Location` hello 대체 위치 중 하나를 사용 하 여 다시 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="2a291-138">유지 관리에 대 한 hello 원래 위치를 일시적으로 닫혔을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="2a291-139">Hello 가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="2a291-139">Creating hello import job</span></span>
<span data-ttu-id="2a291-140">toocreate hello 가져오기 작업을 호출 hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="2a291-141">다음 정보는 tooprovide hello이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="2a291-142">Hello 작업에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-142">A name for hello job.</span></span>

-   <span data-ttu-id="2a291-143">hello 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-143">hello storage account name.</span></span>

-   <span data-ttu-id="2a291-144">배송 위치 이름, hello 이전 단계에서 가져온 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="2a291-145">작업 유형(가져오기)입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-145">A job type (Import).</span></span>

-   <span data-ttu-id="2a291-146">hello 반송 주소는 hello 가져오기 작업이 완료 된 후 hello 드라이브를 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="2a291-147">hello hello 작업의 드라이브 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-147">hello list of drives in hello job.</span></span> <span data-ttu-id="2a291-148">각 드라이브에 대 한 hello 다음 hello 드라이브 준비 단계에서 가져온 정보를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="2a291-149">hello 드라이브 Id</span><span class="sxs-lookup"><span data-stu-id="2a291-149">hello drive Id</span></span>

    -   <span data-ttu-id="2a291-150">hello BitLocker 키</span><span class="sxs-lookup"><span data-stu-id="2a291-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="2a291-151">hello hello 하드 드라이브에 매니페스트 파일 상대 경로</span><span class="sxs-lookup"><span data-stu-id="2a291-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="2a291-152">hello Base16 인코딩된 매니페스트 파일 MD5 해시</span><span class="sxs-lookup"><span data-stu-id="2a291-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="2a291-153">드라이브 배송</span><span class="sxs-lookup"><span data-stu-id="2a291-153">Shipping your drives</span></span>
<span data-ttu-id="2a291-154">Hello 이전 단계에서 가져온 사용자 드라이브 toohello 주소를 배송 해야 하 고 hello 패키지 수를 추적 하는 hello로 hello 가져오기/내보내기 서비스를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="2a291-155">패키지의 추적 번호를 제공하는 지원 운송업체 서비스를 통해 드라이브를 배송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="2a291-156">배송 정보 사용 hello 가져오기 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="2a291-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="2a291-157">추적 번호를 사용 하는 다음 호출 hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) 작업 tooupdate hello 통신 회사 이름, hello 작업에 대 한 추적 번호 hello 및 반환 전달용 hello 운송 업체 계정 번호를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="2a291-158">필요에 따라 hello 드라이브 수 및 배송 날짜도 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a291-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a291-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a291-159">Next steps</span></span>

* [<span data-ttu-id="2a291-160">Hello 가져오기/내보내기 서비스 REST API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2a291-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
