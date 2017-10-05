---
title: "Azure Import/Export에 대한 내보내기 작업 만들기 | Microsoft Docs"
description: "Microsoft Azure Import/Export 서비스에 대해 내보내기 작업을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="9486a-103">Azure Import/Export 서비스에 대한 내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="9486a-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="9486a-104">REST API를 사용하여 Microsoft Azure Import/Export 서비스에 대해 내보내기 작업을 만드는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="9486a-105">내보낼 blob 선택</span><span class="sxs-lookup"><span data-stu-id="9486a-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="9486a-106">배송 위치 가져오기</span><span class="sxs-lookup"><span data-stu-id="9486a-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="9486a-107">내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="9486a-107">Creating the export job.</span></span>

-   <span data-ttu-id="9486a-108">지원되는 운송업체 서비스를 통해 Microsoft에 빈 드라이브 배송</span><span class="sxs-lookup"><span data-stu-id="9486a-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="9486a-109">패키지 정보를 사용하여 내보내기 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="9486a-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="9486a-110">Microsoft에서 드라이브 다시 받기</span><span class="sxs-lookup"><span data-stu-id="9486a-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="9486a-111">Import/Export 서비스에 대한 개요 및 [Azure Portal](https://portal.azure.com/)을 사용하여 가져오기 및 내보내기 작업을 만들고 관리하는 방법을 보여 주는 자습서는 [Microsoft Azure Import/Export 서비스를 사용하여 데이터를 Blob Storage로 전송](storage-import-export-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9486a-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="9486a-112">내보낼 blob 선택</span><span class="sxs-lookup"><span data-stu-id="9486a-112">Selecting blobs to export</span></span>
 <span data-ttu-id="9486a-113">내보내기 작업을 만들려면 저장소 계정에서 내보낼 blob 목록을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="9486a-114">다음과 같은 방법으로 내보낼 blob을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="9486a-115">상대 blob 경로를 사용하여 단일 blob 및 해당 스냅숏을 모두 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="9486a-116">상대 blob 경로를 사용하여 단일 blob을 선택하고 해당 스냅숏은 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="9486a-117">상대 blob 경로 및 스냅숏 시간을 사용하여 단일 스냅숏을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="9486a-118">blob 접두사를 사용하여 지정된 접두사를 갖는 모든 blob 및 스냅숏을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="9486a-119">저장소 계정의 모든 blob 및 스냅숏을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="9486a-120">내보낼 blob을 지정하는 방법에 대한 자세한 내용은 [작업 배치](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 연산을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9486a-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="9486a-121">배송 위치 가져오기</span><span class="sxs-lookup"><span data-stu-id="9486a-121">Obtaining your shipping location</span></span>
<span data-ttu-id="9486a-122">내보내기 작업을 만들기 전에 [위치 가져오기](https://portal.azure.com) 또는 [위치 나열](/rest/api/storageimportexport/listlocations) 연산을 호출하여 배송 위치 이름 및 주소를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="9486a-123">`List Locations`는 위치 목록과 해당 우편 발송 주소 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="9486a-124">반환된 목록에서 위치를 선택하고 해당 주소로 하드 드라이브 배송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="9486a-125">`Get Location` 연산을 사용하여 특정 위치에 대한 배송 주소를 직접 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="9486a-126">배송 위치를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="9486a-127">저장소 계정의 위치 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="9486a-128">이 값은 클래식 포털에서 저장소 계정의 **대시보드**에 있는 **위치** 필드에서 찾거나 Service Management API 연산 [저장소 계정 속성 가져오기](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties)를 사용하여 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="9486a-129">`Get Location` 연산을 호출하여 이 저장소 계정을 처리하는 데 사용할 수 있는 위치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="9486a-130">위치의 `AlternateLocations` 속성에 해당 위치 자체가 포함될 경우 이 위치를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="9486a-131">그렇지 않으면 대체 위치 중 하나를 사용하여 `Get Location` 연산을 다시 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="9486a-132">유지 관리를 위해 원래 위치가 일시적으로 닫혀 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="9486a-133">내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="9486a-133">Creating the export job</span></span>
 <span data-ttu-id="9486a-134">내보내기 작업을 만들려면 [작업 배치](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 연산을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="9486a-135">다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="9486a-136">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-136">A name for the job.</span></span>

-   <span data-ttu-id="9486a-137">저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-137">The storage account name.</span></span>

-   <span data-ttu-id="9486a-138">이전 단계에서 얻은 배송 위치 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="9486a-139">작업 유형(내보내기)입니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-139">A job type (Export).</span></span>

-   <span data-ttu-id="9486a-140">내보내기 작업이 완료된 후 드라이브를 보낼 반환 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="9486a-141">내보낼 blob(또는 blob 접두사) 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="9486a-142">드라이브 배송</span><span class="sxs-lookup"><span data-stu-id="9486a-142">Shipping your drives</span></span>
 <span data-ttu-id="9486a-143">다음으로 Azure Import/Export 도구를 사용하여 내보내려고 선택한 blob 및 드라이브 크기에 따라 전송하려는 드라이브 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="9486a-144">자세한 내용은 [Azure Import/Export 도구 참조](storage-import-export-tool-how-to-v1.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9486a-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="9486a-145">드라이브를 단일 패키지로 포장한 다음 이전 단계에서 얻은 주소로 배송합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="9486a-146">다음 단계를 위해 패키지의 추적 번호를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="9486a-147">패키지의 추적 번호를 제공하는 지원 운송업체 서비스를 통해 드라이브를 배송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="9486a-148">패키지 정보를 사용하여 내보내기 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="9486a-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="9486a-149">추적 번호가 있으면 [작업 속성 업데이트](/rest/api/storageimportexport/jobs#Jobs_Update) 연산을 호출하여 배송업체 이름과 작업의 추적 번호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="9486a-150">경우에 따라 드라이브 개수, 반송 주소 및 배송 날짜를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="9486a-151">패키지 받기</span><span class="sxs-lookup"><span data-stu-id="9486a-151">Receiving the package</span></span>
 <span data-ttu-id="9486a-152">내보내기 작업이 처리된 후 암호화된 데이터와 함께 드라이브가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="9486a-153">[작업 가져오기](/rest/api/storageimportexport/jobs#Jobs_Get) 연산을 호출하여 각 드라이브의 BitLocker 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="9486a-154">그런 다음 이 키를 사용하여 드라이브 잠금을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="9486a-155">각 드라이브에 있는 드라이브 매니페스트 파일에는 드라이브의 파일 목록과 각 파일의 원래 blob 주소도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9486a-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9486a-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9486a-156">Next steps</span></span>

* [<span data-ttu-id="9486a-157">Import/Export 서비스 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="9486a-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
