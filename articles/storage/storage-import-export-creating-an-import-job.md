---
title: "Azure Import/Export에 대한 내보내기 작업 만들기 | Microsoft Docs"
description: "Microsoft Azure Import/Export 서비스에 대해 가져오기 작업을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="2b735-103">Azure Import/Export 서비스에 대한 가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="2b735-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="2b735-104">REST API를 사용하여 Microsoft Azure Import/Export 서비스에 대해 가져오기 작업을 만드는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="2b735-105">Azure Import/Export 도구로 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="2b735-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="2b735-106">드라이브를 배송할 위치 가져오기</span><span class="sxs-lookup"><span data-stu-id="2b735-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="2b735-107">가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="2b735-107">Creating the import job.</span></span>

-   <span data-ttu-id="2b735-108">지원되는 운송업체 서비스를 통해 Microsoft에 드라이브 배송</span><span class="sxs-lookup"><span data-stu-id="2b735-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="2b735-109">배송 정보로 가져오기 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="2b735-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="2b735-110">Import/Export 서비스에 대한 개요 및 [Azure Portal](https://portal.azure.com/)을 사용하여 가져오기 및 내보내기 작업을 만들고 관리하는 방법을 보여 주는 자습서는 [Microsoft Azure Import/Export 서비스를 사용하여 데이터를 Blob Storage로 전송](storage-import-export-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b735-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="2b735-111">Azure Import/Export 도구로 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="2b735-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="2b735-112">가져오기 작업을 위해 드라이브를 준비하는 단계는 포털을 통해 작업을 만들거나 REST API를 통해 작업을 만들 경우 둘 다 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="2b735-113">다음은 드라이브 준비에 대한 간단한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="2b735-114">자세한 지침은 [Azure Import-Export 도구 참조](storage-import-export-tool-how-to-v1.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b735-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="2b735-115">[여기](http://go.microsoft.com/fwlink/?LinkID=301900)에서 Azure Import/Export 도구를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="2b735-116">드라이브를 준비하는 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="2b735-117">가져올 데이터 식별</span><span class="sxs-lookup"><span data-stu-id="2b735-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="2b735-118">Microsoft Azure Storage에서 대상 blob 식별</span><span class="sxs-lookup"><span data-stu-id="2b735-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="2b735-119">Azure Import/Export 도구를 사용하여 하나 이상의 하드 드라이브로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="2b735-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="2b735-120">또한 Azure Import/Export 도구는 드라이브가 준비되면 각 드라이브에 대해 매니페스트 파일도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="2b735-121">매니페스트 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-121">A manifest file contains:</span></span>

-   <span data-ttu-id="2b735-122">업로드한 모든 파일의 열거형과 이러한 파일에서 blob으로의 매핑</span><span class="sxs-lookup"><span data-stu-id="2b735-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="2b735-123">각 파일의 세그먼트 체크섬</span><span class="sxs-lookup"><span data-stu-id="2b735-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="2b735-124">각 blob에 연결될 속성 및 메타데이터에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="2b735-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="2b735-125">업로드될 blob이 컨테이너의 기존 blob과 이름이 같은 경우 수행할 작업 목록</span><span class="sxs-lookup"><span data-stu-id="2b735-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="2b735-126">가능한 옵션: a) blob을 파일로 덮어쓰기 b) 기존 blob을 유지하고 파일 업로드 건너뛰기 c) 다른 파일과 충돌하지 않게 이름에 접미사 추가</span><span class="sxs-lookup"><span data-stu-id="2b735-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="2b735-127">배송 위치 가져오기</span><span class="sxs-lookup"><span data-stu-id="2b735-127">Obtaining your shipping location</span></span>

<span data-ttu-id="2b735-128">가져오기 작업을 만들기 전에 [위치 나열](/rest/api/storageimportexport/listlocations) 연산을 호출하여 배송 위치 이름 및 주소를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="2b735-129">`List Locations`는 위치 목록과 해당 우편 발송 주소 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="2b735-130">반환된 목록에서 위치를 선택하고 해당 주소로 하드 드라이브 배송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="2b735-131">`Get Location` 연산을 사용하여 특정 위치에 대한 배송 주소를 직접 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="2b735-132">배송 위치를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="2b735-133">저장소 계정의 위치 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="2b735-134">이 값은 Azure Portal에서 저장소 계정의 **대시보드**에 있는 **위치** 필드에서 찾거나 Service Management API 연산 [저장소 계정 속성 가져오기](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)를 사용하여 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="2b735-135">`Get Location` 연산을 호출하여 이 저장소 계정을 처리하는 데 사용할 수 있는 위치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="2b735-136">위치의 `AlternateLocations` 속성에 해당 위치 자체가 포함될 경우 이 위치를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="2b735-137">그렇지 않으면 대체 위치 중 하나를 사용하여 `Get Location` 연산을 다시 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="2b735-138">유지 관리를 위해 원래 위치가 일시적으로 닫혀 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="2b735-139">가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="2b735-139">Creating the import job</span></span>
<span data-ttu-id="2b735-140">가져오기 작업을 만들려면 [작업 배치](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 연산을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="2b735-141">다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="2b735-142">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-142">A name for the job.</span></span>

-   <span data-ttu-id="2b735-143">저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-143">The storage account name.</span></span>

-   <span data-ttu-id="2b735-144">이전 단계에서 얻은 배송 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="2b735-145">작업 유형(가져오기)입니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-145">A job type (Import).</span></span>

-   <span data-ttu-id="2b735-146">가져오기 작업이 완료된 후 드라이브를 보낼 반환 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="2b735-147">작업의 드라이브 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-147">The list of drives in the job.</span></span> <span data-ttu-id="2b735-148">각 드라이브에 대해 드라이브 준비 단계 중에 획득한 다음 정보를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="2b735-149">드라이브 ID</span><span class="sxs-lookup"><span data-stu-id="2b735-149">The drive Id</span></span>

    -   <span data-ttu-id="2b735-150">BitLocker 키</span><span class="sxs-lookup"><span data-stu-id="2b735-150">The BitLocker key</span></span>

    -   <span data-ttu-id="2b735-151">하드 드라이브의 매니페스트 파일 상대 경로</span><span class="sxs-lookup"><span data-stu-id="2b735-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="2b735-152">Base16 인코딩 매니페스트 파일 MD5 해시</span><span class="sxs-lookup"><span data-stu-id="2b735-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="2b735-153">드라이브 배송</span><span class="sxs-lookup"><span data-stu-id="2b735-153">Shipping your drives</span></span>
<span data-ttu-id="2b735-154">이전 단계에서 획득한 주소로 드라이브를 배송해야 하고, Import/Export 서비스에 패키지의 추적 번호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="2b735-155">패키지의 추적 번호를 제공하는 지원 운송업체 서비스를 통해 드라이브를 배송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="2b735-156">배송 정보로 가져오기 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="2b735-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="2b735-157">추적 번호가 있으면 [작업 속성 업데이트](/api/storageimportexport/jobs#Jobs_Update) 연산을 호출하여 배송업체 이름, 작업의 추적 번호 및 반송을 위한 배송업체 계정 번호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="2b735-158">경우에 따라 드라이브 개수 및 배송 날짜를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b735-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b735-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b735-159">Next steps</span></span>

* [<span data-ttu-id="2b735-160">Import/Export 서비스 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="2b735-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
