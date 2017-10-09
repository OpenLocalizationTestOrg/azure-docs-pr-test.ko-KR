---
title: "Azure CDN 사용 되는 Azure 저장소 계정과 aaaIntegrate | Microsoft Docs"
description: "Toouse hello Azure 콘텐츠 배달 네트워크 (CDN) toodeliver 고대역폭 콘텐츠를 캐시 하 여 Azure 저장소에서 blob 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="d79aa-103">Azure CDN과 Azure Storage 계정 통합</span><span class="sxs-lookup"><span data-stu-id="d79aa-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="d79aa-104">CDN 사용된 toocache Azure 저장소에서 콘텐츠를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="d79aa-105">Blob 및 hello 미국, 유럽, 아시아, 오스트레일리아 및 남아메리카에 있는 물리적 노드에서 계산 인스턴스의 정적 콘텐츠를 캐시 하 여 고대역폭 콘텐츠를 배달 하기 위한 글로벌 솔루션 개발자에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="d79aa-106">1 단계: 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d79aa-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="d79aa-107">다음 프로시저 toocreate Azure 구독에 대 한 새 저장소 계정을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="d79aa-108">저장소 계정을 통해 Azure 저장소 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="d79aa-109">hello 저장소 계정은 hello 최고 수준의 각 hello Azure 저장소 서비스 구성 요소에 액세스 하기 위한 hello 네임 스페이스를 나타냅니다: Blob 서비스, 큐 서비스 및 테이블 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="d79aa-110">자세한 내용은 참조 toohello [Azure 저장소 소개 tooMicrosoft](../storage/common/storage-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="d79aa-111">서비스 관리자에 게 또는 연결 된 hello에 대 한 공동 관리자 여야 합니다 toocreate 저장소 계정, 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d79aa-112">몇 가지가 toocreate hello Azure 포털 및 Powershell을 포함 하 여 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="d79aa-113">이 자습서에서는 Azure 포털 hello를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="d79aa-114">**Azure 구독에 대 한 저장소 계정 toocreate**</span><span class="sxs-lookup"><span data-stu-id="d79aa-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="d79aa-115">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d79aa-116">Hello 왼쪽된 위 모서리에서 선택 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="d79aa-117">Hello에 **새로** 대화 상자에서 **데이터 + 저장소**, 클릭 **저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="d79aa-118">hello **저장소 계정 만들기** 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-118">hello **Create storage account** blade appears.</span></span>   

    ![저장소 계정 만들기][create-new-storage-account]  

3. <span data-ttu-id="d79aa-120">Hello에 **이름** 필드 하위 도메인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="d79aa-121">이 입력에는 3-24자의 소문자와 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="d79aa-122">이 값은 hello hello 구독에 대 한 Blob, 큐 또는 테이블 리소스를 처리 하는 데 사용 되는 URI 내에서 hello 호스트 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="d79aa-123">하려면 hello Blob 서비스에서에서 컨테이너 리소스에 주소를 사용 하는 URI, 형식에 따라 hello에 여기서  *&lt;StorageAccountLabel&gt;*  toohello 값에 입력 한 참조 **URL입력**:</span><span class="sxs-lookup"><span data-stu-id="d79aa-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="d79aa-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="d79aa-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="d79aa-125">**중요:** URL 레이블 forms hello 하위 도메인의 hello 저장소 계정 URI hello 및 Azure에서 모든 호스팅된 서비스에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="d79aa-126">이 값은 프로그래밍 방식으로이 계정에 액세스할 때 hello 또는 hello 포털에서이 저장소 계정 이름으로도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="d79aa-127">에 대 한 hello 기본값 그대로 두고 **배포 모델**, **kind 계정**, **성능**, 및 **복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="d79aa-128">선택 hello **구독** 된와 hello 저장소 계정은 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="d79aa-129">**리소스 그룹**을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="d79aa-130">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d79aa-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="d79aa-131">저장소 계정의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="d79aa-132">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-132">Click **Create**.</span></span> <span data-ttu-id="d79aa-133">hello hello 저장소 계정을 만드는 과정은 몇 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="d79aa-134">Hello 저장소 계정에 대해 CDN을 사용 하는 2 단계:</span><span class="sxs-lookup"><span data-stu-id="d79aa-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="d79aa-135">Hello 최신 통합 저장소 포털 확장을 종료 하지 않고 저장소 계정에 대해 CDN을 지금 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="d79aa-136">Hello 저장소 계정을 선택를 다음 검색 "CDN" 또는 스크롤 등에 hello 왼쪽된 탐색 메뉴에서 "Azure CDN"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="d79aa-137">hello **Azure CDN** 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-137">hello **Azure CDN** blade appears.</span></span>

    ![cdn 사용 탐색][cdn-enable-navigation]
    
2. <span data-ttu-id="d79aa-139">Hello 필요한 정보를 입력 하 여 새 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="d79aa-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="d79aa-140">**CDN 프로필**: 새 프로필을 만들거나 기존 프로필을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="d79aa-141">**가격 책정 계층**: tooselect 새 CDN 프로필을 만드는 경우는 가격 책정 계층에 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="d79aa-142">**CDN 끝점 이름**: 원하는 끝점 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="d79aa-143">만든 hello CDN 끝점이 기본적으로 원점으로 저장소 계정의 hello 호스트 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="d79aa-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="d79aa-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="d79aa-145">를 만든 후 hello 새 끝점에에서 표시 됩니다 위의 hello 끝점 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![CDN 저장소 새 끝점][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="d79aa-147">또한 tooAzure CDN 확장 tooenable CDN을 이동할 수 있습니다. [자습서](#Tutorial-cdn-create-profile)합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="d79aa-148">3단계: 추가 CDN 기능 사용</span><span class="sxs-lookup"><span data-stu-id="d79aa-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="d79aa-149">저장소 계정 "Azure CDN" 블레이드에서 hello 목록 tooopen CDN 구성 블레이드에서 hello CDN 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="d79aa-150">전송에 대해 압축, 쿼리 문자열, 지역 필터링 등과 같은 추가 CDN 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="d79aa-151">사용자 지정 도메인 매핑에 tooyour CDN 끝점을 추가 하 고 사용자 지정 도메인 HTTPS를 사용 하도록 설정 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN 저장소 CDN 구성][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="d79aa-153">4단계: CDN 콘텐츠 액세스</span><span class="sxs-lookup"><span data-stu-id="d79aa-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="d79aa-154">hello 포털에서 사용 하 여 hello CDN URL 제공 tooaccess hello CDN에서 콘텐츠를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="d79aa-155">캐시 된 blob에 대 한 hello 주소 비슷한 toohello 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="d79aa-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="d79aa-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="d79aa-157">CDN 액세스 tooa 저장소 계정을 사용 하도록 설정 하면 공개적으로 사용 가능한 모든 개체가 CDN에 지 캐싱 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="d79aa-158">현재 hello CDN에에서 캐시 된 개체를 수정 하면 hello CDN 캐시 hello 콘텐츠 활성 시간 기간이 만료 된 경우 콘텐츠를 새로 고칠 때까지 hello 새 콘텐츠는 hello CDN 통해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="d79aa-159">5 단계: hello CDN에서에서 콘텐츠를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="d79aa-160">더 이상 원할 경우 toocache 개체 hello Azure 콘텐츠 배달 네트워크 (CDN)의 단계를 수행 하는 hello 중 하나를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="d79aa-161">Hello 공용이 아닌 전용 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="d79aa-162">참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../storage/blobs/storage-manage-access-to-resources.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="d79aa-163">사용 하지 않도록 설정 하거나 관리 포털 hello를 사용 하 여 hello CDN 끝점을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="d79aa-164">에 호스팅된 서비스 toono 긴 응답 toorequests hello 개체에 대 한를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="d79aa-165">이미 hello CDN에에서 캐시 된 개체는 hello 끝점은 제거 하거나 hello 개체에 대 한 hello 활성 시간 기간이 만료 될 때까지 캐싱된 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="d79aa-166">Hello 활성 시간 기간이 만료 되 면 hello CDN 끝점이 여전히 유효한 지 여부 및 익명 액세스할 수 hello 개체 hello CDN toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="d79aa-167">그렇지 않은 경우에 hello 개체가 더 이상 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d79aa-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d79aa-168">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d79aa-168">Additional resources</span></span>
* [<span data-ttu-id="d79aa-169">어떻게 tooMap CDN 콘텐츠 tooa 사용자 지정 도메인</span><span class="sxs-lookup"><span data-stu-id="d79aa-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="d79aa-170">사용자 지정 도메인에 대해 HTTPS 사용</span><span class="sxs-lookup"><span data-stu-id="d79aa-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
