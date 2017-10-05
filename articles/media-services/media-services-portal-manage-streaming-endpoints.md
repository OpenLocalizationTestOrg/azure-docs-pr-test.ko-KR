---
title: "Azure Portal을 통해 스트리밍 끝점 관리 | Microsoft 문서"
description: "이 항목에서는 Azure 포털을 사용하여 스트리밍 끝점을 관리하는 방법을 설명합니다."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 797dced6c3e2525730afa29987259cb9b435ba66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="0c527-103">Azure 포털을 통해 스트리밍 끝점 관리</span><span class="sxs-lookup"><span data-stu-id="0c527-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="0c527-104">이 항목은 Azure Portal을 사용하여 스트리밍 끝점을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-104">This topic shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="0c527-105">[개요](media-services-streaming-endpoints-overview.md) 항목을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="0c527-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="0c527-106">스트리밍 끝점의 크기를 조정하는 방법에 대한 자세한 내용은 [이 항목](media-services-portal-scale-streaming-endpoints.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c527-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="0c527-107">스트리밍 끝점 관리 시작</span><span class="sxs-lookup"><span data-stu-id="0c527-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="0c527-108">계정의 스트리밍 끝점 관리를 시작하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="0c527-109">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="0c527-110">**설정** 블레이드에서 **스트리밍 끝점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="0c527-112">스트리밍 끝점이 실행 중인 상태일 때만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="0c527-113">스트리밍 끝점 추가/삭제</span><span class="sxs-lookup"><span data-stu-id="0c527-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="0c527-114">기본 스트리밍 끝점은 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="0c527-115">Azure 포털을 사용하여 스트리밍 끝점을 추가/삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="0c527-116">스트리밍 끝점을 추가하려면 페이지 위쪽의 **+ 끝점** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="0c527-117">다른 CDN 및 직접 액세스를 사용하려는 경우 여러 스트리밍 끝점을 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="0c527-118">스트리밍 끝점을 삭제하려면 **삭제** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="0c527-119">스트리밍 끝점을 시작하려면 **시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="0c527-121"><a id="configure_streaming_endpoints"></a>스트리밍 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="0c527-121"><a id="configure_streaming_endpoints"></a>Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="0c527-122">스트리밍 끝점을 사용하면 다음 속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="0c527-123">액세스 제어</span><span class="sxs-lookup"><span data-stu-id="0c527-123">Access control</span></span>
* <span data-ttu-id="0c527-124">캐시 제어</span><span class="sxs-lookup"><span data-stu-id="0c527-124">Cache control</span></span>
* <span data-ttu-id="0c527-125">교차 사이트 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="0c527-125">Cross site access policies</span></span>

<span data-ttu-id="0c527-126">이러한 속성에 대한 자세한 정보는 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c527-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="0c527-127">다음을 수행하여 스트리밍 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-127">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="0c527-128">구성하려는 스트리밍 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-128">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="0c527-129">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-129">Click **Settings**.</span></span>

<span data-ttu-id="0c527-130">필드에 대한 간략한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-130">A brief description of the fields follows.</span></span>

![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="0c527-132">최대 캐시 정책: 이 스트리밍 끝점을 통해 제공되는 자산의 캐시 수명 주기를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-132">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="0c527-133">값을 설정하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-133">If no value is set, the default is used.</span></span> <span data-ttu-id="0c527-134">Azure Storage에서 기본값을 직접 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-134">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="0c527-135">스트리밍 끝점에 대해 Azure CDN을 사용하도록 설정한 경우에는 캐시 정책 값을 600초보다 작게 설정하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-135">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="0c527-136">허용된 IP 주소: 게시된 스트리밍 끝점에 연결할 수 있는 IP 주소를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-136">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="0c527-137">IP 주소를 지정하지 않은 경우 모든 IP 주소에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-137">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="0c527-138">IP 주소는 단일 IP 주소(예: '10.0.0.1'), IP 주소 및 CIDR 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1/22') 또는 IP 주소와 점으로 구분된 십진수 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1(255.255.255.0)')로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="0c527-139">Akamai 서명 헤더 인증에 대한 구성: Akamai 서버의 서명 헤더 인증 요청을 구성하는 방법을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-139">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="0c527-140">만료 시간은 UTC 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="0c527-141">프리미엄 스트리밍 끝점 규모 조정</span><span class="sxs-lookup"><span data-stu-id="0c527-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="0c527-142">자세한 내용은 [이 항목](media-services-portal-scale-streaming-endpoints.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c527-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="0c527-143"><a id="enable_cdn"></a>Azure CDN 통합 사용</span><span class="sxs-lookup"><span data-stu-id="0c527-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="0c527-144">새 계정을 만들면 기본 스트리밍 끝점 Azure CDN 통합이 기본적으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="0c527-145">나중에 CDN을 사용/사용 안 함으로 설정하려면 스트리밍 끝점이 **중지됨** 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-145">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="0c527-146">Azure CDN 통합이 사용하도록 설정되고 변경 내용이 모든 CDN POP에 활성화되려면 최대 2시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-146">It could take up to 2 hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="0c527-147">그러나 스트리밍 끝점을 시작하고 스트리밍 끝점에서 중단 없이 스트리밍할 수 있으며 통합이 완료되면 CDN에서 스트림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-147">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream will be delivered from the CDN.</span></span> <span data-ttu-id="0c527-148">프로비전 기간 동안에는 스트리밍 끝점이 **시작** 상태가 되고 성능 저하를 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-148">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="0c527-149">CDN 통합은 중국 및 연방 정부 지역을 제외한 모든 Azure 데이터 센터에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-149">CDN integration is enabled in all the Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="0c527-150">CDN 통합이 설정되면 **액세스 제어**, **사용자 지정 호스트 이름** 및 **Akamai 서명 인증** 구성이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-150">Once it is enabled, the **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="0c527-151">Azure Media Services와 Azure CDN의 통합은 **Verizon의 Azure CDN**에서 표준 스트리밍 끝점에 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="0c527-152">프리미엄 스트리밍 끝점은 모든 **Azure CDN 가격 책정 및 공급자**를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="0c527-153">Azure CDN 기능에 대한 자세한 내용은 [CDN 개요](../cdn/cdn-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c527-153">For more information about Azure CDN features, see the [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="0c527-154">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0c527-154">Additional considerations</span></span>

* <span data-ttu-id="0c527-155">스트리밍 끝점에 CDN이 사용되면 클라이언트에서는 원점으로부터 직접 콘텐츠를 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="0c527-156">CDN을 사용하거나 사용하지 않고 콘텐츠를 테스트하는 기능이 필요하면 CDN이 사용하도록 설정되지 않은 또 다른 스트리밍 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-156">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="0c527-157">스트리밍 끝점 호스트 이름은 CDN을 사용하도록 설정한 후에도 동일하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-157">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="0c527-158">CDN을 사용하도록 설정한 후 미디어 서비스 워크플로에 변경 내용을 적용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-158">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="0c527-159">예를 들어 스트리밍 끝점 호스트 이름이 strasbourg.streaming.mediaservices.windows.net이면 CDN을 사용하도록 설정한 후에 똑같은 호스트 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="0c527-160">새 스트리밍 끝점의 경우 새 끝점을 만들어서 CDN을 사용하도록 설정할 수 있습니다. 기본 스트리밍 끝점의 경우 먼저 끝점을 중지하고 CDN을 사용/사용 안 함으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="0c527-161">표준 스트리밍 끝점은 Azure 관리 포털에서 **Verizon 표준 CDN 공급자**를 통해서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="0c527-162">그러나 REST API를 사용하여 다른 Azure CDN 공급자를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="0c527-163">CDN 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="0c527-163">Configure CDN profile</span></span>

<span data-ttu-id="0c527-164">위쪽에서 **CDN 관리** 단추를 선택하여 CDN 프로필을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-164">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="0c527-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c527-166">Next steps</span></span>
<span data-ttu-id="0c527-167">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="0c527-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0c527-168">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="0c527-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

