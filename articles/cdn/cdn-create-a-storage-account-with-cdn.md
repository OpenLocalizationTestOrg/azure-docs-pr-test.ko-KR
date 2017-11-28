---
title: "Azure CDN과 Azure Storage 계정 통합 | Microsoft Docs"
description: "Azure Storage에서 Blob을 캐시하여 고대역폭 콘텐츠를 배달하기 위해 Azure CDN(콘텐츠 배달 네트워크)을 사용하는 방법을 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="e8d66-103">Azure CDN과 Azure Storage 계정 통합</span><span class="sxs-lookup"><span data-stu-id="e8d66-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="e8d66-104">CDN을 사용하도록 설정하여 Azure 저장소의 콘텐츠를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="e8d66-105">CDN은 미국, 유럽, 아시아, 오스트레일리아 및 남아메리카의 물리적 노드에서 계산 인스턴스의 Blob 및 정적 콘텐츠를 캐시하여 고대역폭 콘텐츠를 제공하기 위한 글로벌 솔루션을 개발자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="e8d66-106">1 단계: 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e8d66-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="e8d66-107">다음 절차에 따라 Azure 구독에 대한 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="e8d66-108">저장소 계정을 통해 Azure 저장소 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="e8d66-109">저장소 계정은 Blob 서비스, 큐 서비스, 테이블 서비스 등 각 Azure 저장소 서비스 구성 요소에 액세스하는 데 필요한 가장 높은 수준의 네임스페이스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="e8d66-110">자세한 내용은 [Microsoft Azure 저장소 소개](../storage/common/storage-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8d66-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="e8d66-111">저장소 계정을 만들려면 관련 구독에 대한 서비스 관리자 또는 공동 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e8d66-112">Azure 포털 및 Powershell을 포함하여 저장소 계정을 만드는 데 사용할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="e8d66-113">이 자습서에서는 Azure 포털을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="e8d66-114">**Azure 구독에 대한 저장소 계정을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="e8d66-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="e8d66-115">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e8d66-116">왼쪽 위에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="e8d66-117">**새로 만들기** 대화 상자에서 **데이터 + 저장소**를 선택한 다음 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="e8d66-118">**저장소 계정 만들기** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-118">The **Create storage account** blade appears.</span></span>   

    ![저장소 계정 만들기][create-new-storage-account]  

3. <span data-ttu-id="e8d66-120">**이름** 필드에 하위 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="e8d66-121">이 입력에는 3-24자의 소문자와 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="e8d66-122">이 값은 구독에 대한 Blob, 큐 또는 테이블 리소스의 주소를 지정하는 데 사용되는 URI 내의 호스트 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="e8d66-123">Blob 서비스에 있는 컨테이너 리소스의 주소를 지정하려면 다음 형식의 URI를 사용하며, 여기서 *&lt;StorageAccountLabel&gt;*은 **URL 입력**에 입력한 값을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="e8d66-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="e8d66-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="e8d66-125">**중요:** URL 레이블은 저장소 계정 URI의 하위 도메인을 구성하며, Azure에서 호스팅된 모든 서비스에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="e8d66-126">이 값은 프로그래밍 방식으로 이 계정에 액세스할 때 또는 포털에서 이 저장소 계정의 이름으로도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="e8d66-127">**배포 모델**, **계정 종류**, **성능** 및 **복제**에 대한 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="e8d66-128">저장소 계정을 사용할 **구독** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="e8d66-129">**리소스 그룹**을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="e8d66-130">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8d66-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="e8d66-131">저장소 계정의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="e8d66-132">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-132">Click **Create**.</span></span> <span data-ttu-id="e8d66-133">저장소 계정을 만드는 프로세스를 완료하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="e8d66-134">2단계: 저장소 계정에 대해 CDN 사용</span><span class="sxs-lookup"><span data-stu-id="e8d66-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="e8d66-135">이제 최신 통합을 사용하여 저장소 포털 확장을 종료하지 않고도 저장소 계정에 대한 CDN을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="e8d66-136">저장소 계정을 선택하고, "CDN"을 검색하거나 왼쪽 탐색 메뉴에서 아래로 스크롤한 다음 "Azure CDN"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="e8d66-137">**Azure CDN** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-137">The **Azure CDN** blade appears.</span></span>

    ![cdn 사용 탐색][cdn-enable-navigation]
    
2. <span data-ttu-id="e8d66-139">필요한 정보를 입력하여 새 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="e8d66-140">**CDN 프로필**: 새 프로필을 만들거나 기존 프로필을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="e8d66-141">**가격 책정 계층**: 새 CDN 프로필을 만드는 경우 가격 책정 계층만 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="e8d66-142">**CDN 끝점 이름**: 원하는 끝점 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="e8d66-143">만든 CDN 끝점은 기본적으로 저장소 계정의 호스트 이름을 토대로 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="e8d66-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="e8d66-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="e8d66-145">만들어진 새 끝점은 위의 끝점 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![CDN 저장소 새 끝점][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="e8d66-147">Azure CDN 확장으로 이동하여 CDN을 사용하도록 설정할 수도 있습니다. [자습서](#Tutorial-cdn-create-profile)</span><span class="sxs-lookup"><span data-stu-id="e8d66-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="e8d66-148">3단계: 추가 CDN 기능 사용</span><span class="sxs-lookup"><span data-stu-id="e8d66-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="e8d66-149">저장소 계정의 "Azure CDN" 블레이드에서 목록에 있는 CDN 끝점을 클릭하여 CDN 구성 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="e8d66-150">전송에 대해 압축, 쿼리 문자열, 지역 필터링 등과 같은 추가 CDN 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="e8d66-151">CDN 끝점에 사용자 지정 도메인 매핑을 추가하고 사용자 지정 도메인 HTTPS를 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN 저장소 CDN 구성][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="e8d66-153">4단계: CDN 콘텐츠 액세스</span><span class="sxs-lookup"><span data-stu-id="e8d66-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="e8d66-154">CDN에 캐시된 콘텐츠에 액세스하려면 포털에 제공된 CDN URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="e8d66-155">캐시된 Blob의 주소는 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="e8d66-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="e8d66-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="e8d66-157">저장소 계정에 대한 CDN 액세스를 사용하도록 설정하면 공개적으로 사용 가능한 모든 개체가 CDN 에지 캐싱에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="e8d66-158">현재 CDN에 캐시된 개체를 수정하는 경우 캐시된 콘텐츠 TTL(Time-to-Live) 기간이 만료될 때 CDN에서 해당 콘텐츠를 새로 고쳐야 CDN을 통해 새 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="e8d66-159">5단계: CDN에서 콘텐츠 제거</span><span class="sxs-lookup"><span data-stu-id="e8d66-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="e8d66-160">더 이상 Azure CDN(콘텐츠 배달 네트워크)에 개체를 캐시하지 않으려면 다음 단계 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="e8d66-161">컨테이너를 공용 대신 전용으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-161">You can make the container private instead of public.</span></span> <span data-ttu-id="e8d66-162">자세한 내용은 [컨테이너 및 Blob에 대한 익명읽기 권한 관리](../storage/blobs/storage-manage-access-to-resources.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8d66-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="e8d66-163">관리 포털을 사용하여 CDN 끝점을 사용하지 않도록 설정하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="e8d66-164">더 이상 개체 요청에 응답하지 않도록 호스티드 서비스를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="e8d66-165">CDN에 이미 캐시된 개체는 개체의 TTL(Time-to-Live) 기간이 만료되거나 끝점이 삭제될 때까지 캐시된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="e8d66-166">TTL(Time-to-Live)이 만료되면 CDN에서 CDN 끝점이 여전히 유효하며 개체에 익명으로 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="e8d66-167">그렇지 않으면 개체가 더 이상 캐시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8d66-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8d66-168">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e8d66-168">Additional resources</span></span>
* [<span data-ttu-id="e8d66-169">CDN 콘텐츠를 사용자 지정 도메인에 매핑하는 방법</span><span class="sxs-lookup"><span data-stu-id="e8d66-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="e8d66-170">사용자 지정 도메인에 대해 HTTPS 사용</span><span class="sxs-lookup"><span data-stu-id="e8d66-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
