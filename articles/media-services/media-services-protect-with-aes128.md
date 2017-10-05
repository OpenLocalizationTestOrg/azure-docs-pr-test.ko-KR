---
title: "AES-128 동적 암호화 및 키 전달 서비스 사용 | Microsoft 문서"
description: "Microsoft Azure 미디어 서비스를 사용하면 AES 128비트 암호화 키로 암호화된 콘텐츠를 배달할 수 있습니다. 미디어 서비스는 권한 있는 사용자에게 암호화 키를 제공하는 키 배달 서비스도 제공합니다. 이 항목에서는 AES-128로 동적으로 암호화하는 방법과 키 배달 서비스를 사용하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: ae1b36c26e688e74eb8fcc1a4cdbd3be0c014c08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="2d7b5-105">AES-128 동적 암호화 및 키 전달 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="2d7b5-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d7b5-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2d7b5-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="2d7b5-107">Java</span><span class="sxs-lookup"><span data-stu-id="2d7b5-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="2d7b5-108">PHP</span><span class="sxs-lookup"><span data-stu-id="2d7b5-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="2d7b5-109">개요</span><span class="sxs-lookup"><span data-stu-id="2d7b5-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="2d7b5-110">AES 암호화를 사용하여 미디어 콘텐츠를 보호하는 방법에 대한 개요는 [이 비디오](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how to protect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="2d7b5-111">Microsoft Azure 미디어 서비스를 사용하면 128 비트 암호화 키를 사용하는 AES(Advanced Encryption Standard)로 암호화된 Http-Live-Streaming(HLS) 및 부드러운 스트림을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-111">Microsoft Azure Media Services enables you to deliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="2d7b5-112">미디어 서비스는 권한 있는 사용자에게 암호화 키를 제공하는 키 배달 서비스도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-112">Media Services also provides the Key Delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="2d7b5-113">미디어 서비스에서 자산을 암호화하려는 경우 암호화 키를 자산에 연결하고 해당 키에 대해 권한 부여 정책도 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-113">If you want for Media Services to encrypt an asset, you need to associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="2d7b5-114">플레이어가 스트림을 요청하면 미디어 서비스는 지정된 키를 사용하고 AES 암호화를 사용하여 동적으로 사용자의 콘텐츠를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-114">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="2d7b5-115">스트림을 해독하기 위해 플레이어는 키 배달 서비스에서 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-115">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="2d7b5-116">사용자에게 키를 얻을 수 있는 권한이 있는지 여부를 결정하기 위해 서비스는 키에 지정된 권한 부여 정책을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-116">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="2d7b5-117">미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="2d7b5-118">콘텐츠 키 권한 부여 정책에는 열기 또는 토큰 제한과 같은 하나 이상의 권한 부여 제한이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-118">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="2d7b5-119">토큰 제한 정책은 보안 토큰 서비스(STS)에 의해 발급된 토큰이 수반되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-119">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="2d7b5-120">Media Services 지원 토큰에는 [단순 웹 토큰](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)(SWT) 형식 및 [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)(JWT) 형식의 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-120">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="2d7b5-121">자세한 내용은 [콘텐츠 키의 권한 부여 정책 구성](media-services-protect-with-aes128.md#configure_key_auth_policy)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-121">For more information, see [Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="2d7b5-122">동적 암호화를 이용하려면 다중 비트 전송률 MP4 파일 또는 다중 비트 전송률 부드러운 스트리밍 원본 파일의 집합이 포함된 자산을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-122">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="2d7b5-123">또한 자산의 배달 정책을 구성해야 합니다(이 항목의 뒷부분에서 설명).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-123">You also need to configure the delivery policy for the asset (described later in this topic).</span></span> <span data-ttu-id="2d7b5-124">이렇게 하면 스트리밍 URL에 지정된 형식에 따라 주문형 스트리밍 서버는 사용자가 선택한 프로토콜로 스트림이 배달되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-124">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="2d7b5-125">따라서 사용자는 단일 저장소 형식으로 파일을 저장하고 해당 파일에 대한 요금을 지불하기만 하면 되며, 미디어 서비스에서 클라이언트의 요청에 따라 적절한 응답을 작성하고 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-125">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="2d7b5-126">이 항목은 보호된 미디어를 배달하는 응용 프로그램에 대한 작업을 수행하는 개발자에게 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-126">This topic would be useful to developers that work on applications that deliver protected media.</span></span> <span data-ttu-id="2d7b5-127">이 항목에서는 권한 부여 정책으로 키 배달 서비스를 구성하여 권한이 있는 클라이언트만 암호화 키를 받을 수 있도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-127">The topic shows you how to configure the key delivery service with authorization policies so that only authorized clients could receive the encryption keys.</span></span> <span data-ttu-id="2d7b5-128">또한 동적 암호화를 사용하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-128">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="2d7b5-129">AES-128 동적 암호화 및 키 배달 서비스 워크플로</span><span class="sxs-lookup"><span data-stu-id="2d7b5-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="2d7b5-130">다음은 AES로 자산을 암호화하고 미디어 서비스 키 배달 서비스를 사용하며 동적 암호화를 사용할 때 수행해야 하는 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-130">The following are general steps that you would need to perform when encrypting your assets with AES, using the Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="2d7b5-131">[자산을 만들고 파일을 자산에 업로드합니다](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-131">[Create an asset and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="2d7b5-132">[파일이 들어 있는 자산을 적응 비트 전송률 MP4 집합으로 인코딩합니다](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-132">[Encode the asset containing the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="2d7b5-133">[콘텐츠 키를 만들어 인코딩된 자산에 연결합니다](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-133">[Create a content key and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="2d7b5-134">미디어 서비스에서 콘텐츠 키에는 자산의 암호화 키가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-134">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="2d7b5-135">[콘텐츠 키의 권한 부여 정책을 구성합니다](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-135">[Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="2d7b5-136">콘텐츠 키 권한 부여 정책은 사용자가 구성해야 하며 콘텐츠 키를 클라이언트에 배달하기 위해서는 해당 클라이언트를 충족시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-136">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>
5. <span data-ttu-id="2d7b5-137">[자산에 대한 배달 정책을 구성합니다](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-137">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="2d7b5-138">배달 정책 구성에는 키 획득 URL 및 IV(Initialization Vector)(AES 128에는 암호화 및 해독 시 동일한 IV를 제공해야 함), 배달 프로토콜(예: MPEG DASH, HLS, 부드러운 스트리밍 또는 모두), 동적 암호화 유형(예: 봉투(envelope) 또는 동적이지 않은 암호화)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-138">The delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires the same IV to be supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="2d7b5-139">동일한 자산의 각 프로토콜에 다른 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-139">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="2d7b5-140">예를 들어, Smooth/DASH에 PlayReady 암호화를, HLS에 AES 봉투(envelope)를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-140">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="2d7b5-141">배달 정책에 정의되지 않은 모든 프로토콜(예: HLS만 프로토콜로 지정하는 단일 정책)은 스트리밍에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="2d7b5-142">정의한 자산 배달 정책이 없는 경우는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-142">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="2d7b5-143">이렇게 하면 모든 프로토콜이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-143">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="2d7b5-144">[주문형 로케이터를 만듭니다](media-services-protect-with-aes128.md#create_locator) .</span><span class="sxs-lookup"><span data-stu-id="2d7b5-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order to get a streaming URL.</span></span>

<span data-ttu-id="2d7b5-145">또한 이 항목에서는 [클라이언트 응용 프로그램이 키 배달 서비스로부터 키를 요청하는 방법](media-services-protect-with-aes128.md#client_request)도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-145">The topic also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="2d7b5-146">이 항목의 끝부분에서 전체 .NET [예제](media-services-protect-with-aes128.md#example) 가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at the end of the topic.</span></span>

<span data-ttu-id="2d7b5-147">다음 이미지는 위에서 설명한 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-147">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="2d7b5-148">여기서는 인증에 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-148">Here the token is used for authentication.</span></span>

![AES-128로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="2d7b5-150">이 항목의 나머지 부분에서는 자세한 설명, 코드 예제 및 위에서 설명한 작업을 수행하는 방법을 보여주는 항목에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-150">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="2d7b5-151">현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="2d7b5-151">Current limitations</span></span>
<span data-ttu-id="2d7b5-152">자산 배달 정책을 추가하거나 업데이트하는 경우 기존 로케이터(있는 경우)를 삭제하고 새 로케이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="2d7b5-153"><a id="create_asset"></a>자산 만들기 및 파일을 자산에 업로드</span><span class="sxs-lookup"><span data-stu-id="2d7b5-153"><a id="create_asset"></a>Create an asset and upload files into the asset</span></span>
<span data-ttu-id="2d7b5-154">관리, 인코딩 및 비디오 스트림을 수행하려면 먼저 콘텐츠를 Microsoft Azure 미디어 서비스에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-154">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="2d7b5-155">업로드되면 이후 처리 및 스트리밍을 위해 콘텐츠가 클라우드에 안전하게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-155">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="2d7b5-156">자세한 내용은 [미디어 서비스 계정에 파일 업로드](media-services-dotnet-upload-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="2d7b5-157"><a id="encode_asset"></a>파일이 들어 있는 자산을 적응 비트 전송률 MP4 집합으로 인코딩</span><span class="sxs-lookup"><span data-stu-id="2d7b5-157"><a id="encode_asset"></a>Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="2d7b5-158">동적 암호화를 사용하는 경우 다중 비트 전송률 MP4 파일 또는 다중 비트 전송률 부드러운 스트리밍 원본 파일의 집합이 포함된 자산을 만들기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-158">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="2d7b5-159">이렇게 하면 매니페스트 또는 조각 요청의 지정된 형식에 따라 주문형 스트리밍 서버는 사용자가 선택한 프로토콜로 스트림을 받을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-159">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="2d7b5-160">따라서 사용자는 단일 저장소 형식으로 파일을 저장하고 해당 파일에 대한 요금을 지불하기만 하면 되며, 미디어 서비스에서 클라이언트의 요청에 따라 적절한 응답을 작성하고 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-160">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="2d7b5-161">자세한 내용은 [동적 패키징 개요](media-services-dynamic-packaging-overview.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-161">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="2d7b5-162">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-162">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="2d7b5-163">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-163">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="2d7b5-164">또한 동적 패키징 및 동적 암호화를 사용하려면 자산이 적응 비트 전송률 MP4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-164">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="2d7b5-165">인코딩하는 방법에 관한 지침은 [미디어 인코더 표준을 사용하여 자산을 인코딩하는 방법](media-services-dotnet-encode-with-media-encoder-standard.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-165">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="2d7b5-166"><a id="create_contentkey"></a>콘텐츠 키를 만들어 인코딩된 자산에 연결</span><span class="sxs-lookup"><span data-stu-id="2d7b5-166"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="2d7b5-167">미디어 서비스에서 콘텐츠 키에는 자산을 암호화할 키가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-167">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="2d7b5-168">자세한 내용은 [콘텐츠 키 만들기](media-services-dotnet-create-contentkey.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="2d7b5-169"><a id="configure_key_auth_policy"></a>콘텐츠 키의 인증 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-169"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="2d7b5-170">미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="2d7b5-171">콘텐츠 키 권한 부여 정책은 사용자가 구성해야 하며 이 키를 클라이언트에 배달하기 위해서는 해당 클라이언트(플레이어)를 충족시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-171">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="2d7b5-172">콘텐츠 키 권한 부여 정책에는 열기, 토큰 제한 또는 IP 제한과 같은 하나 이상의 권한 부여 제한이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-172">The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="2d7b5-173">자세한 내용은 [콘텐츠 키 권한 부여 정책 구성](media-services-dotnet-configure-content-key-auth-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="2d7b5-174"><a id="configure_asset_delivery_policy"></a>자산 배달 정책 구성</span><span class="sxs-lookup"><span data-stu-id="2d7b5-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="2d7b5-175">자산에 대한 배달 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-175">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="2d7b5-176">자산 배달 정책 구성에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-176">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="2d7b5-177">키 획득 URL.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-177">The Key acquisition URL.</span></span> 
* <span data-ttu-id="2d7b5-178">봉투(envelope) 암호화에 사용할 IV(Initialization Vector).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-178">The Initialization Vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="2d7b5-179">AES 128에는 암호화 및 해독 시 동일한 IV를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-179">AES 128 requires the same IV to be supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="2d7b5-180">자산 배달 프로토콜(예: MPEG DASH, HLS, 부드러운 스트리밍 또는 모두).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-180">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="2d7b5-181">동적 암호화 유형(예: AES 봉투) 또는 동적이지 않은 암호화.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-181">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="2d7b5-182">자세한 내용은 [자산 배달 정책 구성 ](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="2d7b5-183"><a id="create_locator"></a>스트리밍 URL을 얻기 위해 주문형 스트리밍 로케이터 만들기</span><span class="sxs-lookup"><span data-stu-id="2d7b5-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="2d7b5-184">사용자에게 Smooth, DASH 또는 HLS에 대한 스트리밍 URL을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-184">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="2d7b5-185">자산 배달 정책을 추가하거나 업데이트하는 경우 기존 로케이터(있는 경우)를 삭제하고 새 로케이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="2d7b5-186">자산을 게시하고 스트리밍 URL을 작성하는 방법은 [스트리밍 URL 작성](media-services-deliver-streaming-content.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-186">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="2d7b5-187">테스트 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="2d7b5-187">Get a test token</span></span>
<span data-ttu-id="2d7b5-188">키 권한 부여 정책에 사용된 토큰 제한에 따라 테스트 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-188">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="2d7b5-189">[AMS 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html) 를 사용하여 스트림을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-189">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <span data-ttu-id="2d7b5-190"><a id="client_request"></a>클라이언트가 키 배달 서비스로부터 키를 요청하는 방법</span><span class="sxs-lookup"><span data-stu-id="2d7b5-190"><a id="client_request"></a>How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="2d7b5-191">이전 단계에서는 매니페스트 파일을 가리키는 URL을 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-191">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="2d7b5-192">클라이언트는 키 배달 서비스에 요청을 수행하기 위해 스트리밍 매니페스트 파일에서 필요한 정보를 추출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-192">Your client needs to extract the necessary information from the streaming manifest files in order to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="2d7b5-193">매니페스트 파일</span><span class="sxs-lookup"><span data-stu-id="2d7b5-193">Manifest files</span></span>
<span data-ttu-id="2d7b5-194">클라이언트는 매니페스트 파일에서 URL(콘텐츠 키 Id도 포함(kid)) 값을 추출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-194">The client needs to extract the URL (that also contains content key Id (kid)) value from the manifest file.</span></span> <span data-ttu-id="2d7b5-195">그런 다음 키 배달 서비스로부터 암호화 키 가져오기를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-195">The client will then try to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="2d7b5-196">또한 IV 값을 추출하고 이 값을 사용하여 스트림을 해독합니다. 다음 코드 조각은 부드러운 스트리밍 매니페스트의 <Protection> 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-196">The client also needs to extract the IV value and use it do decrypt the stream.The following snippet shows the <Protection> element of the Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="2d7b5-197">HLS의 경우 루트 매니페스트는 세그먼트 파일로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-197">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="2d7b5-198">예를 들어 루트 매니페이스는 http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl)이고 세그먼트 파일 이름 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-198">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="2d7b5-199">세그먼트 파일 중 하나를 텍스트 편집기에서 열면(예: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl)), #EXT-X-KEY가 포함되어 있어야 하며 이는 파일이 암호화되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-199">If you open one of the segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that the file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="2d7b5-200">Safari에서 AES 암호화 HLS를 재생하려는 경우 [이 블로그](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-200">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="2d7b5-201">키 배달 서비스로부터 키 요청</span><span class="sxs-lookup"><span data-stu-id="2d7b5-201">Request the key from the key delivery service</span></span>

<span data-ttu-id="2d7b5-202">다음 코드에서는 키 배달 Uri(매니페스트에서 추출됨) 및 토큰을 사용하여 미디어 서비스 키 배달 서비스로 요청을 보내는 방법을 보여 줍니다(이 항목에서는 보안 토큰 서비스에서 간단한 웹 토큰을 가져오는 방법에 대해서는 다루지 않음).</span><span class="sxs-lookup"><span data-stu-id="2d7b5-202">The following code shows how to send a request to the Media Services key delivery service using a key delivery Uri (that was extracted from the manifest) and a token (this topic does not talk about how to get Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="2d7b5-203">.NET을 사용하여 AES-128로 콘텐츠 보호</span><span class="sxs-lookup"><span data-stu-id="2d7b5-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2d7b5-204">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="2d7b5-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="2d7b5-205">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-205">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="2d7b5-206">다음 요소를 app.config 파일에 정의된 **appSettings**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-206">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="2d7b5-207"><a id="example"></a>예제</span><span class="sxs-lookup"><span data-stu-id="2d7b5-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="2d7b5-208">Program.cs 파일에 있는 코드를 이 섹션에 나와 있는 코드로 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-208">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="2d7b5-209">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="2d7b5-210">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-210">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="2d7b5-211">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="2d7b5-212">입력 파일이 있는 폴더를 가리키도록 변수를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d7b5-212">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing the issuer of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // The Audience or Scope of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //The GenerateTestToken method returns the token without the word “Bearer” in front
            //so you have to add it in front of the token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the bit.ly/aesplayer Flash player to test the URL 
            // (with open authorization policy). 
            // Paste the URL and click the Update button to play the video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose to associate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in the key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  the URL does not contains a key ID

            // The following policy configuration specifies: 
            // key url that will have KID=<Guid> appended to the envelope and
            // the Initialization Vector (IV) to use for the envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin. 
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file. 
            return originLocator.Path + assetFile.Name;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="2d7b5-213">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="2d7b5-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2d7b5-214">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="2d7b5-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

