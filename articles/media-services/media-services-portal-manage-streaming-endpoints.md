---
title: "hello Azure 포털을 사용 하 여 끝점을 스트리밍 aaaManage | Microsoft Docs"
description: "이 항목에서는 toomanage 스트리밍 끝점이 Azure 포털 hello 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="5f54d-103">Azure 포털 hello로 스트리밍 끝점을 관리</span><span class="sxs-lookup"><span data-stu-id="5f54d-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="5f54d-104">이 항목에서는 toouse Azure 포털 toomanage 스트리밍 끝점을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="5f54d-105">있는지 tooreview hello 확인 [개요](media-services-streaming-endpoints-overview.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="5f54d-106">어떻게 tooscale hello 스트리밍 끝점에 대 한 정보를 참조 하십시오. [이](media-services-portal-scale-streaming-endpoints.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="5f54d-107">스트리밍 끝점 관리 시작</span><span class="sxs-lookup"><span data-stu-id="5f54d-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="5f54d-108">회원님의 계정에 대 한 스트리밍 끝점을 관리 하는 toostart 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="5f54d-109">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5f54d-110">Hello에 **설정** 블레이드를 **스트리밍 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="5f54d-112">스트리밍 끝점이 실행 중인 상태일 때만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="5f54d-113">스트리밍 끝점 추가/삭제</span><span class="sxs-lookup"><span data-stu-id="5f54d-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="5f54d-114">hello 기본 스트리밍 끝점을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="5f54d-115">tooadd/삭제 스트리밍 끝점에 사용 하 여 Azure 포털 hello, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="5f54d-116">스트리밍 끝점 tooadd 클릭 hello **+ 끝점** hello hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="5f54d-117">Toohave 하려는 경우에 여러 개의 스트리밍 끝점을 할 수 있습니다 다른 Cdn 또는 CDN 및 직접 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="5f54d-118">스트리밍 끝점 toodelete 키를 눌러 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="5f54d-119">Hello 클릭 **시작** 단추 toostart hello 스트리밍 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="5f54d-121"><a id="configure_streaming_endpoints"></a>Hello 스트리밍 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="5f54d-122">스트리밍 끝점 tooconfigure hello를 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="5f54d-123">Access Control</span><span class="sxs-lookup"><span data-stu-id="5f54d-123">Access control</span></span>
* <span data-ttu-id="5f54d-124">캐시 제어</span><span class="sxs-lookup"><span data-stu-id="5f54d-124">Cache control</span></span>
* <span data-ttu-id="5f54d-125">교차 사이트 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="5f54d-125">Cross site access policies</span></span>

<span data-ttu-id="5f54d-126">이러한 속성에 대한 자세한 정보는 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f54d-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="5f54d-127">Hello 다음을 수행 하 여 스트리밍 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="5f54d-128">스트리밍 끝점 tooconfigure 원하는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="5f54d-129">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-129">Click **Settings**.</span></span>

<span data-ttu-id="5f54d-130">Hello 필드에 대 한 간단한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-130">A brief description of hello fields follows.</span></span>

![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="5f54d-132">최대 캐시 정책: tooconfigure 사용 되는 자산의 캐시 수명을이 스트리밍 끝점을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="5f54d-133">설정 된 hello 기본값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="5f54d-134">Azure 저장소에 직접 hello 기본값을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="5f54d-135">Azure CDN hello 스트리밍 끝점을 사용 하도록 구성 되어 600 초 보다 hello 캐시 정책 값 tooless를 설정 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="5f54d-136">허용 된 IP 주소: toospecify IP 주소는 허용 tooconnect toohello 스트리밍 끝점을 게시 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="5f54d-137">IP 주소가 지정 된 없는 경우 모든 IP 주소 수 tooconnect입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="5f54d-138">IP 주소는 단일 IP 주소(예: '10.0.0.1'), IP 주소 및 CIDR 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1/22') 또는 IP 주소와 점으로 구분된 십진수 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1(255.255.255.0)')로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="5f54d-139">Akamai 서명 헤더 인증에 대 한 구성을: toospecify Akamai 서버의 서명 헤더 인증 요청 구성 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="5f54d-140">만료 시간은 UTC 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="5f54d-141">프리미엄 스트리밍 끝점 규모 조정</span><span class="sxs-lookup"><span data-stu-id="5f54d-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="5f54d-142">자세한 내용은 [이 항목](media-services-portal-scale-streaming-endpoints.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f54d-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="5f54d-143"><a id="enable_cdn"></a>Azure CDN 통합 사용</span><span class="sxs-lookup"><span data-stu-id="5f54d-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="5f54d-144">새 계정을 만들면 기본 스트리밍 끝점 Azure CDN 통합이 기본적으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="5f54d-145">나중에 CDN 사용 toodisable/hello, 원하는 경우 스트리밍 끝점 hello에 있어야 **중지** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="5f54d-146">CDN을 팝 하는 모든 hello에서 hello Azure CDN 통합 tooget 사용 하도록 설정 하 고 hello 변경 toobe 활성 too2 시간이 걸릴 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="5f54d-147">그러나 수 있습니다 hello 스트리밍 끝점에서에서 스트리밍 끝점과 중단 없이 스트림 시작 하 고 hello 통합 완료 되 면 hello 스트림 hello CDN에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="5f54d-148">Hello 기간을 프로 비전 하는 동안 하려면 스트리밍 끝점에 포함 됩니다 **시작** 상태 및 있습니다 degredad 성능을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="5f54d-149">CDN 통합은 모든 Azure 데이터 센터 execpt 중국 hello 및 연방 Goverment 영역에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="5f54d-150">활성화 되 면 hello **액세스 제어**, **사용자 지정 호스트 이름** 및 **Akamai 서명 인증** 구성을 사용할 수 없게 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="5f54d-151">Azure Media Services와 Azure CDN의 통합은 **Verizon의 Azure CDN**에서 표준 스트리밍 끝점에 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="5f54d-152">프리미엄 스트리밍 끝점은 모든 **Azure CDN 가격 책정 및 공급자**를 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="5f54d-153">Azure CDN 기능에 대 한 자세한 내용은 참조 hello [CDN 개요](../cdn/cdn-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="5f54d-154">추가 고려 사항</span><span class="sxs-lookup"><span data-stu-id="5f54d-154">Additional considerations</span></span>

* <span data-ttu-id="5f54d-155">스트리밍 끝점에 CDN을 사용할 때 클라이언트 hello 원본에서 직접 콘텐츠를 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="5f54d-156">CDN 유무 콘텐츠 hello 기능 tootest 해야 할 경우 CDN을 사용 하도록 설정 되지 않은 다른 스트리밍 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="5f54d-157">스트리밍 끝점 호스트 이름은 유지 CDN을 사용 하도록 설정한 후 같은 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="5f54d-158">CDN을 사용 하도록 설정한 후 모든 변경 내용을 tooyour 미디어 서비스 워크플로 toomake 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="5f54d-159">예를 들어 프로그램 스트리밍 끝점 호스트 이름 CDN을 사용 하도록 설정한 후 strasbourg.streaming.mediaservices.windows.net, 경우 hello 정확히 동일한 호스트 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="5f54d-160">새 스트리밍 끝점에 대 한; 새로운 끝점을 만들고 하기만 CDN을 사용할 수 있습니다. 기존 스트리밍 끝점 toofirst 중지 hello 끝점과 설정/해제 hello CDN이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="5f54d-161">표준 스트리밍 끝점은 Azure 관리 포털에서 **Verizon 표준 CDN 공급자**를 통해서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="5f54d-162">그러나 REST API를 사용하여 다른 Azure CDN 공급자를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="5f54d-163">CDN 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="5f54d-163">Configure CDN profile</span></span>

<span data-ttu-id="5f54d-164">Hello를 선택 하 여 hello CDN 프로필을 구성할 수 있습니다 **CDN 관리** hello 위에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="5f54d-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f54d-166">Next steps</span></span>
<span data-ttu-id="5f54d-167">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5f54d-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5f54d-168">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5f54d-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

