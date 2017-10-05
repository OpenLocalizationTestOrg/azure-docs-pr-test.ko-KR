---
title: "REST를 사용한 주문형 콘텐츠 제공 시작 | Microsoft Docs"
description: "이 자습서에서는 REST API를 사용한 Azure 미디어 서비스로 주문형 콘텐츠 배달 응용 프로그램을 구현하는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="57809-103">REST를 사용한 주문형 콘텐츠 제공 시작</span><span class="sxs-lookup"><span data-stu-id="57809-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="57809-104">이 자습서에서는 AMS(Azure 미디어 서비스) REST API를 사용하여 주문형 비디오(VoD) 콘텐츠 제공 응용 프로그램을 구현하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="57809-105">기본적인 미디어 서비스 워크플로와 미디어 서비스 개발에 필요한 가장 일반적인 프로그래밍 개체 및 작업을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="57809-106">자습서를 마치면 업로드하고 인코딩하고 다운로드한 샘플 미디어 파일을 스트리밍하거나 점진적으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="57809-107">다음 이미지에서는 Media Services OData 모델에 대해 VoD 응용 프로그램을 개발할 때 가장 일반적으로 사용되는 개체 중 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="57809-108">전체 크기로 보려면 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="57809-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="57809-109">Prerequisites</span></span>
<span data-ttu-id="57809-110">미디어 서비스 REST API를 사용하여 개발을 시작하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="57809-111">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="57809-111">An Azure account.</span></span> <span data-ttu-id="57809-112">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="57809-113">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="57809-113">A Media Services account.</span></span> <span data-ttu-id="57809-114">Media Services 계정을 만들려면 [Media Services 계정을 만드는 방법](media-services-portal-create-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="57809-115">미디어 서비스 REST API를 사용하여 개발하는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="57809-116">자세한 내용은 [Media Services REST API 개요](media-services-rest-how-to-use.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="57809-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="57809-117">HTTP 요청 및 응답을 보낼 수 있도록 선택한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="57809-118">이 자습서에서는 [Fiddler](http://www.telerik.com/download/fiddler)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="57809-119">다음 작업은 본 퀵 스타트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="57809-120">스트리밍 끝점을 시작합니다(Azure Portal 사용).</span><span class="sxs-lookup"><span data-stu-id="57809-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="57809-121">REST API를 통해 미디어 서비스 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="57809-122">REST API를 통해 새 자산을 만들고 비디오를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="57809-123">REST API를 통해 원본 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="57809-124">REST API를 통해 자산을 게시하고 스트리밍 기능 및 URL 점진적 다운로드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="57809-125">콘텐츠를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="57809-126">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="57809-127">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="57809-128">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="57809-129">이 항목에 사용된 AMS REST 엔터티에 대한 자세한 내용은 [Azure Media Services REST API 참조](/rest/api/media/services/azure-media-services-rest-api-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="57809-130">참고 항목: [Azure Media Services 개념](media-services-concepts.md)</span><span class="sxs-lookup"><span data-stu-id="57809-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="57809-131">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="57809-132">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="57809-133">Azure Portal을 사용하여 스트리밍 끝점 시작</span><span class="sxs-lookup"><span data-stu-id="57809-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="57809-134">Azure Media Services 작업 시 가장 일반적인 시나리오 중 하나는 적응 비트 전송률 스트리밍을 통해 비디오를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="57809-135">Media Services는 적응 비트 전송률 MP4 인코딩 콘텐츠를 Media Services에서 적시에 지원되는 각 스트리밍 형식(MPEG DASH, HLS, 부드러운 스트리밍)의 사전 패키징된 버전을 저장하지 않고도 이런 스트리밍 형식으로 배달할 수 있게 하는 동적 패키징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="57809-136">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="57809-137">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="57809-138">스트리밍 끝점을 시작하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="57809-139">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="57809-140">설정 창에서 스트리밍 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="57809-141">기본 스트리밍 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="57809-142">기본 스트리밍 끝점 세부 정보 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="57809-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="57809-143">시작 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-143">Click the Start icon.</span></span>
5. <span data-ttu-id="57809-144">저장 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="57809-145"><a id="connect"></a>REST API를 통해 미디어 서비스 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="57809-146">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="57809-147">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="57809-148">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="57809-149">예를 들어 연결을 시도한 후 다음 항목을 받은 경우.</span><span class="sxs-lookup"><span data-stu-id="57809-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="57809-150">https://wamsbayclus001rest-hs.cloudapp.net/api/에 후속 API 호출을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="57809-151"><a id="upload"></a>REST API를 통해 새 자산을 만들고 비디오를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="57809-152">미디어 서비스에서 자산에 디지털 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="57809-153">**자산** 엔터티에는 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택 자막 파일(및 이러한 파일에 대한 메타데이터)이 포함될 수 있습니다.  자산에 파일이 업로드되면 이후 처리 및 스트리밍을 위해 콘텐츠가 클라우드에 안전하게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="57809-154">자산을 만들 때 제공해야 하는 값 중 하나는 자산 생성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="57809-155">**옵션** 속성은 자산으로 만들 수 있는 암호화 옵션을 설명하는 열거 값입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="57809-156">유효한 값은 이 목록의 값의 조합이 아니라 아래 목록에 있는 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="57809-157">**없음** = **0** - 암호화가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="57809-158">이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="57809-159">MP4를 배달하려는 경우 이 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="57809-160">**StorageEncrypted** = **1** - 암호화 되어 있지 않은 콘텐츠를 AES-256 비트 암호화를 사용하여 로컬에서 암호화한 다음 암호화되어 저장되는 Azure Storage에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="57809-161">저장소 암호화로 보호된 자산은 자동으로 암호 해제되어 인코딩되기 전에 암호화된 파일 시스템에 배치됩니다. 그리고 필요에 따라 새 출력 자산으로 다시 업로드되기 전에 다시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="57809-162">저장소 암호화를 사용하는 기본적인 사례는 디스크에 저장된 상태일 때 강력한 암호화로 고품질의 입력 미디어 파일을 보호하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="57809-163">**CommonEncryptionProtected** = **2** - 이미 암호화되어 일반적인 암호화 또는 PlayReady DRM(예: PlayReady DRM으로 보호되는 부드러운 스트리밍)으로 보호된 콘텐츠를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="57809-164">**EnvelopeEncryptionProtected** = **4** - AES로 암호화된 HLS를 업로드하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="57809-165">파일을 Transform Manager로 인코딩 및 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="57809-166">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-166">Create an asset</span></span>
<span data-ttu-id="57809-167">자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="57809-168">REST API에서 자산을 만들려면 미디어 서비스에 POST 요청을 보내고 자산에 대한 속성 정보를 요청 본문에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="57809-169">다음 예제에서는 자산을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="57809-170">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="57809-171">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-171">**HTTP Response**</span></span>

<span data-ttu-id="57809-172">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-172">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="57809-173">AssetFile 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-173">Create an AssetFile</span></span>
<span data-ttu-id="57809-174">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 엔터티는 blob 컨테이너에 저장된 비디오 또는 오디오 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="57809-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="57809-175">자산 파일은 항상 자산에 연결되며 자산에는 하나 이상의 AssetFile이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="57809-176">자산 파일 개체가 blob 컨테이너의 디지털 파일과 연결되지 않은 경우 미디어 서비스 인코더 작업을 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="57809-177">Blob 컨테이너에 디지털 미디어 파일을 업로드 한 후 **MERGE** HTTP 요청을 사용하여 미디어 파일에 대한 정보로 AssetFile을 업데이트합니다(이 항목의 뒷부분 참조).</span><span class="sxs-lookup"><span data-stu-id="57809-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="57809-178">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="57809-179">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="57809-180">쓰기 권한으로 AccessPolicy 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="57809-181">blob 저장소에 모든 파일을 업로드하기 전에 자산에 쓰기 위한 액세스 정책 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="57809-182">이렇게 하려면 AccessPolicies 엔터티 집합에 HTTP 요청을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="57809-183">작성 시 DurationInMinutes 값을 정의하지 않으면 응답에서 500 내부 서버 오류 메시지가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="57809-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="57809-184">AccessPolicies에 대한 자세한 내용은 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="57809-185">다음 예제에서는 AccessPolicy를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="57809-186">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="57809-187">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-187">**HTTP Response**</span></span>

<span data-ttu-id="57809-188">성공하면 다음 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-188">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-the-upload-url"></a><span data-ttu-id="57809-189">업로드 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="57809-189">Get the Upload URL</span></span>

<span data-ttu-id="57809-190">실제 업로드 URL을 받으려면 SAS 로케이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57809-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="57809-191">로케이터는 자산에 있는 파일에 액세스하려는 클라이언트에 대한 시작 시간과 연결 끝점의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="57809-192">다양한 클라이언트 요청 및 요구 사항을 처리하기 위해 지정된 AccessPolicy 및 자산 쌍에 대해 여러 로케이터 엔터티를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="57809-193">이러한 각 로케이터는 AccessPolicy의 StartTime 값과 DurationInMinutes 값을 사용하여 URL이 사용될 수는 시간의 길이를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="57809-194">자세한 내용은 [로케이터](https://docs.microsoft.com/rest/api/media/operations/locator)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="57809-195">SAS URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="57809-196">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-196">Some considerations apply:</span></span>

* <span data-ttu-id="57809-197">지정된 자산과 연관된 고유 로케이터는 한 번에 5개 이상 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="57809-198">자세한 내용은 로케이터를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-198">For more information, see Locator.</span></span>
* <span data-ttu-id="57809-199">파일을 즉시 업로드해야 하는 경우 StartTime 값을 현재 시간에서 5분 전으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="57809-200">클라이언트 컴퓨터와 미디어 서비스 사이에 시간차가 있을 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="57809-201">또한 StartTime 값은 다음 DateTime 형식이어야 합니다. YYYY-MM-DDTHH:mm:ssZ(예: "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="57809-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="57809-202">로케이터를 만든 후 사용할 수 있을 때까지 30-40초의 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="57809-203">이 문제는 SAS URL 및 원본 로케이터 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="57809-204">SAS 로케이터에 대한 자세한 내용은 [이 블로그](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="57809-205">다음 예제에서는 요청 본문의 형식 속성에서 정의한 대로(SAS 로케이터의 경우 "1" 그리고 주문형 원본 로케이터의 경우 "2") SAS URL 로케이터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="57809-206">반환된 **경로** 속성은 파일 업로드 시 반드시 사용해야 하는 URL을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="57809-207">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="57809-208">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-208">**HTTP Response**</span></span>

<span data-ttu-id="57809-209">성공하면 다음 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-209">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="57809-210">Blob 저장소 컨테이너에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="57809-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="57809-211">AccessPolicy와 로케이터를 설정했으면 실제 파일은 Azure Storage REST API를 사용하여 Azure Blob Storage 컨테이너에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="57809-212">블록 blob으로 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="57809-213">페이지 blob은 Azure Media Services에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="57809-214">이전 섹션에서 받은 로케이터 **경로** 값에 업로드하려는 파일에 대한 파일 이름을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="57809-215">예: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="57809-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="57809-216">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-216">.</span></span> <span data-ttu-id="57809-217">.</span><span class="sxs-lookup"><span data-stu-id="57809-217">.</span></span> <span data-ttu-id="57809-218">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-218">.</span></span>
>
>

<span data-ttu-id="57809-219">Azure 저장소 Blob 작업에 대한 자세한 내용은 [Blob 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="57809-220">AssetFile 업데이트</span><span class="sxs-lookup"><span data-stu-id="57809-220">Update the AssetFile</span></span>
<span data-ttu-id="57809-221">이제 파일을 업로드했으므로 FileAsset 크기(및 기타) 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="57809-222">예:</span><span class="sxs-lookup"><span data-stu-id="57809-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="57809-223">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-223">**HTTP Response**</span></span>

<span data-ttu-id="57809-224">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="57809-225">로케이터와 AccessPolicy 삭제</span><span class="sxs-lookup"><span data-stu-id="57809-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="57809-226">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="57809-227">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-227">**HTTP Response**</span></span>

<span data-ttu-id="57809-228">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="57809-229">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="57809-230">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-230">**HTTP Response**</span></span>

<span data-ttu-id="57809-231">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="57809-232"><a id="encode"></a>원본 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩</span><span class="sxs-lookup"><span data-stu-id="57809-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="57809-233">미디어 서비스에 자산을 삽입하고 나면 미디어를 클라이언트에 배달하기 전에 인코딩, 트랜스믹싱, 워터마크 지정 등을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="57809-234">이러한 활동은 높은 성능과 가용성을 보장하기 위해 여러 백그라운드 역할 인스턴스에 대해 예약 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="57809-235">이러한 활동을 작업이라고 하며 각 작업은 자산 파일에서 실제 작업을 수행하는 원자성 작업으로 구성됩니다(자세한 내용은 [작업](/rest/api/media/services/job), [태스크](/rest/api/media/services/task) 설명 참조).</span><span class="sxs-lookup"><span data-stu-id="57809-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="57809-236">앞에서 언급한 대로, Azure 미디어 서비스 작업 시 가장 일반적인 시나리오 중 하나는 적응 비트 전송률 스트리밍을 클라이언트에 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="57809-237">Media Services는 적응 비트 전송률 MP4 파일을 HLS(HTTP 라이브 스트리밍), 부드러운 스트리밍, MPEG DASH 형식 중 하나로 동적 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="57809-238">다음 섹션에서는 하나의 인코딩 작업을 포함하는 작업을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="57809-239">이 작업은 **미디어 인코더 표준**을 사용하여 메자닌 파일을 적응 비트 전송률 MP4 집합으로 트랜스코딩하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="57809-240">이 섹션에서는 작업 진행 상황을 모니터링하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="57809-241">작업이 완료되면 자산에 대한 액세스하는 데 필요한 로케이터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="57809-242">미디어 프로세서 가져오기</span><span class="sxs-lookup"><span data-stu-id="57809-242">Get a media processor</span></span>
<span data-ttu-id="57809-243">미디어 서비스에서 미디어 프로세서는 인코딩, 형식 변환, 콘텐츠, 암호화 또는 암호 해독 미디어와 같은 특정 처리 작업을 처리 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="57809-244">이 자습서에 표시된 인코딩 작업에서는 미디어 인코더 표준을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="57809-245">다음 코드는 인코더의 id를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="57809-246">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="57809-247">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="57809-248">작업 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-248">Create a job</span></span>
<span data-ttu-id="57809-249">각 작업을 수행하려는 처리 유형에 따라 하나 이상의 작업을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="57809-250">REST API를 통해 두 방법 중 하나로 작업 및 관련된 작업을 만들 수 있습니다. 작업은 작업 엔터티에 대한 작업 탐색 속성 또는 OData 배치를 통해 인라인으로 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="57809-251">Media Services SDK는 일괄 처리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="57809-252">하지만 이 항목에 있는 코드 예제 가독성의 경우 작업은 인라인으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="57809-253">일괄 처리에 대한 정보는 [Open Data Protocol(OData) 일괄 처리](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="57809-254">다음 예제에서는 특정 해상도와 품질로 비디오를 인코딩하기 위해 하나의 작업 집합으로 작업을 만들어 게시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="57809-255">다음 설명서 섹션은 미디어 인코더 표준 프로세서에서 지원하는 모든 [작업 사전 설정](http://msdn.microsoft.com/library/mt269960) 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="57809-256">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="57809-257">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-257">**HTTP Response**</span></span>

<span data-ttu-id="57809-258">성공하면 다음 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-258">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="57809-259">모든 작업 요청에는 몇 가지 중요한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="57809-260">TaskBody 속성은 리터럴 XML을 사용하여 작업에서 사용되는 입력이나 출력 수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="57809-261">작업 항목은 해당 XML에 대한 XML 스키마 정의를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="57809-262">TaskBody 정의에서 <inputAsset> 및 <outputAsset>에 대한 각각의 내부 값은 JobInputAsset(value) 또는 JobOutputAsset(value)으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="57809-263">작업 출력 자산은 여러 개일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-263">A task can have multiple output assets.</span></span> <span data-ttu-id="57809-264">작업에서 하나의 JobOutputAsset(x)을 작업 출력으로 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="57809-265">JobInputAsset 또는 JobOutputAsset을 작업의 입력 자산으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="57809-266">작업은 주기를 형성해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="57809-267">JobInputAsset 또는 JobOutputAsset에 전달하는 값 매개변수는 자산에 대한 인덱스 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="57809-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="57809-268">실제 자산은 작업 엔터티 정의에 있는 InputMediaAssets 및 OutputMediaAssets 탐색 속성에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="57809-269">미디어 서비스는 OData v 3를 기반으로 하기 때문에 InputMediaAssets 및 OutputMediaAssets 탐색 속성 컬렉션에 있는 개별 자산은 "__metadata : uri" 이름 값 쌍으로 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="57809-270">InputMediaAsset은 미디어 서비스에서 만든 하나 이상의 자산에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="57809-271">OutputMediaAsset은 시스템에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="57809-272">기존 자산을 참조하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="57809-273">OutputMediaAsset은 assetName 특성을 사용하여 명명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="57809-274">이 특성이 없을 경우 OutputMediaAsset의 이름은 <outputAsset> 요소의 내부 텍스트 값이 작업 이름 값 또는 작업 Id 값(이름 속성이 정의되어 있지 않은 경우)의 접미사를 갖는 어떤 것이든 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="57809-275">예를 들어, assetName에 대한 값을 "Sample"로 설정하는 경우 OutputMediaAsset 이름 속성은 "Sample"로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="57809-276">하지만 assetName에 대한 값은 설정하지 않았지만 작업 이름을 "NewJob"으로 설정한 경우 OutputMediaAsset 이름은 "JobOutputAsset(값)_NewJob"이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="57809-277">다음 예제에서는 assetName 특성을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="57809-278">작업 체인을 사용하려면,</span><span class="sxs-lookup"><span data-stu-id="57809-278">To enable task chaining:</span></span>

  * <span data-ttu-id="57809-279">작업에 작업이 2개 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="57809-280">작업에서 입력이 다른 작업의 출력인 작업이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="57809-281">자세한 내용은 [미디어 서비스 REST API를 사용하여 인코딩 작업 만들기](media-services-rest-encode-asset.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="57809-282">처리 진행 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="57809-282">Monitor Processing Progress</span></span>
<span data-ttu-id="57809-283">다음 예제와 같이 State 속성을 사용하여 작업 상태를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="57809-284">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="57809-285">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-285">**HTTP Response**</span></span>

<span data-ttu-id="57809-286">성공하면 다음 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-286">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="57809-287">작업 취소</span><span class="sxs-lookup"><span data-stu-id="57809-287">Cancel a job</span></span>
<span data-ttu-id="57809-288">미디어 서비스를 사용하면 CancelJob 함수를 통해 실행 중인 작업을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="57809-289">이 호출은 작업 상태가 취소됨, 취소 중, 오류 또는 완료일 때 작업을 취소하려고 하면 400 오류 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="57809-290">다음 예제에서는 CancelJob을 호출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="57809-291">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="57809-292">성공하는 경우 메시지 본문 없이 204 응답 코드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="57809-293">작업 id(일반적으로 nb:jid:UUID: somevalue)가 CancelJob에 매개변수로 전달되는 경우 작업 id를 URL 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="57809-294">출력 자산 가져오기</span><span class="sxs-lookup"><span data-stu-id="57809-294">Get the output asset</span></span>
<span data-ttu-id="57809-295">다음 코드에서는 출력 자산 id를 요청하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="57809-296">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="57809-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="57809-297">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="57809-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="57809-298"><a id="publish_get_urls"></a>REST API를 통해 자산을 게시하고 스트리밍 기능 및 URL 점진적 다운로드를 사용</span><span class="sxs-lookup"><span data-stu-id="57809-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="57809-299">자산을 스트리밍하거나 다운로드하려면 먼저 로케이터를 만들어 자산을 "게시"해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="57809-300">로케이터는 자산에 포함된 파일에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="57809-301">미디어 서비스는 두 가지 유형의 로케이터를 지원합니다.하나는 OnDemandOrigin 로케이터로서 미디어를 스트리밍하는 데 사용되고(예: MPEG DASH, HLS 또는 부드러운 스트리밍) 다른 하나는 SAS(공유 액세스 서명) 로케이터로서 미디어 파일을 다운로드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="57809-302">SAS 로케이터에 대한 자세한 내용은 [이 블로그](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="57809-303">로케이터를 만든 후에 파일을 스트리밍하거나 다운로드하는 데 사용되는 URL을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="57809-304">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="57809-305">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="57809-306">부드러운 스트리밍에 대한 스트리밍 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="57809-307">HLS에 대한 스트리밍 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="57809-308">MPEG DASH에 대한 스트리밍 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="57809-309">파일을 다운로드하는 데 사용되는 SAS URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="57809-310">이 섹션에서는 자산을 "게시"하기 위해 다음 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="57809-311">읽기 권한이 포함된 AccessPolicy 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="57809-312">콘텐츠를 다운로드할 SAS URL 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="57809-313">콘텐츠 스트리밍을 위한 원본 URL 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="57809-314">읽기 권한이 포함된 AccessPolicy 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="57809-315">미디어 콘텐츠를 다운로드하거나 스트리밍하기 전에 먼저 읽기 권한이 포함된 AccessPolicy를 정의하고 클라이언트에 대해 사용하도록 설정하려는 배달 메커니즘 유형을 지정하는 적절한 로케이터 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57809-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="57809-316">사용할 수 있는 속성에 대한 자세한 내용은 [AccessPolicy 엔터티 속성](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="57809-317">다음 예제에서는 지정된 자산에 대한 읽기 권한의 AccessPolicy를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="57809-318">성공하면 사용자가 만든 AccessPolicy 엔터티를 설명하는 201 성공 코드가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="57809-319">이제 AccessPolicy Id를 로케이터 엔터티를 만들기 위해 배달하려는 파일이 포함된 자산(예: 출력 자산)의 자산 ID와 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="57809-320">이 기본 워크플로는 자산을 통합할 때 파일을 업로드하는 것과 같습니다(이 항목의 앞부분에서 설명함).</span><span class="sxs-lookup"><span data-stu-id="57809-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="57809-321">또한 파일을 업로드하는 것과 마찬가지로 사용자(또는 클라이언트)가 파일에 즉시 액세스해야 하는 경우 StartTime 값을 현재 시간에서 5분 전으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="57809-322">이 동작은 클라이언트와 미디어 서비스 사이에 시간차가 있을 수 있기 때문에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="57809-323">StartTime 값은 YYYY-MM-DDTHH:mm:ssZ(예: 2014-05-23T17:53:50Z) 형식의 DateTime이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="57809-324">콘텐츠를 다운로드할 SAS URL 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="57809-325">다음 코드는 이전에 만들어서 업로드한 미디어 파일을 다운로드하는 데 사용할 수 있는 URL을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="57809-326">AccessPolicy는 읽기 권한을 설정하고 로케이터 경로는 SAS 다운로드 URL을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="57809-327">성공하면 다음 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-327">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="57809-328">반환된 **경로** 속성은 SAS URL을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="57809-329">저장소가 암호화된 콘텐츠를 다운로드하는 경우 렌더링하기 전에 수동으로 암호를 해독하거나 처리 작업에서 저장소 암호 해독 미디어 프로세서를 사용하여 암호화되지 않은 상태로 처리된 파일을 OutputAsset으로 출력한 다음 해당 자산에서 다운로드해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="57809-330">처리에 대한 자세한 내용은 미디어 서비스 REST API를 사용하여 인코딩 작업 만들기를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="57809-331">또한 SAS URL 로케이터를 만들고 나면 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="57809-332">예를 들어, 업데이트된 StartTime 값으로 동일한 로케이터를 다시 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="57809-333">SAS URL을 만드는 방식 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="57809-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="57809-334">로케이터가 만료된 후 다운로드할 자산에 액세스하려면 새 StartTime으로 새 로케이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="57809-335">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="57809-335">Download files</span></span>
<span data-ttu-id="57809-336">AccessPolicy와 로케이터를 설정했으면 Azure 저장소 REST API를 사용하여 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="57809-337">다운로드하려는 파일의 파일 이름을 이전 섹션에서 받은 로케이터 **경로** 값에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="57809-338">예: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="57809-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="57809-339">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-339">.</span></span> <span data-ttu-id="57809-340">.</span><span class="sxs-lookup"><span data-stu-id="57809-340">.</span></span> <span data-ttu-id="57809-341">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-341">.</span></span>
>
>

<span data-ttu-id="57809-342">Azure 저장소 Blob 작업에 대한 자세한 내용은 [Blob 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57809-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="57809-343">이전에 수행한 인코딩 작업(적응 MP4 집합으로 인코딩)의 결과로 점진적으로 다운로드할 수 있는 여러 MP4 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="57809-344">예:</span><span class="sxs-lookup"><span data-stu-id="57809-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="57809-345">콘텐츠 스트리밍을 위한 스트리밍 URL 만들기</span><span class="sxs-lookup"><span data-stu-id="57809-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="57809-346">다음 코드에서는 스트리밍 URL 로케이터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57809-346">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="57809-347">성공하면 다음 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="57809-347">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="57809-348">스트리밍 미디어 플레이어에서 부드러운 스트리밍 원본 URL을 스트리밍하려면 "/매니페스트" 다음에 부드러운 스트리밍 매니페스트 파일의 이름이 포함된 경로 속성을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="57809-349">HLS를 스트리밍하려면 "/매니페스트" 뒤에 추가(format=m3u8-aapl)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="57809-350">MPEG DASH를 스트리밍하려면 "/매니페스트" 뒤에 추가(format=mpd-time-csf)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="57809-351"><a id="play"></a>콘텐츠 재생</span><span class="sxs-lookup"><span data-stu-id="57809-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="57809-352">비디오를 스트리밍하려면 [Azure 미디어 서비스 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57809-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="57809-353">점진적 다운로드를 테스트하려면 IE, Chrome, Safari 등의 브라우저에 URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="57809-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="57809-354">다음 단계: 미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="57809-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="57809-355">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="57809-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
