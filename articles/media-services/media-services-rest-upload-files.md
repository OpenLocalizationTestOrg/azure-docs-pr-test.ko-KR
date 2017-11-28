---
title: "REST를 사용 하 여 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "만들고 자산을 업로드 하 여 tooget 미디어를 미디어 서비스 콘텐츠 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="d7627-103">REST를 사용하여 Media Services 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d7627-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7627-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d7627-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="d7627-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="d7627-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="d7627-106">포털</span><span class="sxs-lookup"><span data-stu-id="d7627-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="d7627-107">미디어 서비스에서 자산에 디지털 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="d7627-108">hello [자산](https://docs.microsoft.com/rest/api/media/operations/asset) 엔터티 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터)를 포함할 수 있습니다  Hello 파일 hello 자산으로 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="d7627-109">hello 고려 사항에 따라 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="d7627-110">미디어 서비스 스트리밍 콘텐츠 (예를 들어 http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) hello에 대 한 Url 작성 시 hello IAssetFile.Name 속성의 hello 값을 사용 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="d7627-111">값의 hello hello **이름** 속성 hello 다음 중 하나를 사용할 수 없습니다 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="d7627-112">또한 하나만 있을 수 있습니다 하나 '.' hello 파일 이름 확장명에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="d7627-113">hello hello 이름 길이 260 자 보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="d7627-114">미디어 서비스에서 처리에 지원 되는 제한 toohello 최대 파일 크기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="d7627-115">참조 하십시오 [이](media-services-quotas-and-limitations.md) hello 파일 크기 제한에 대 한 세부 정보에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="d7627-116">자산을 업로드 하기 위한 기본 워크플로 hello hello 다음 섹션으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="d7627-117">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-117">Create an Asset</span></span>
* <span data-ttu-id="d7627-118">자산 암호화(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="d7627-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="d7627-119">업로드 파일 tooblob 저장소</span><span class="sxs-lookup"><span data-stu-id="d7627-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="d7627-120">AMS는 tooupload 자산을을 대량 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="d7627-121">자세한 내용은 [이](media-services-rest-upload-files.md#upload_in_bulk) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="d7627-122">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d7627-123">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="d7627-124">TooMedia 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="d7627-124">Connect tooMedia Services</span></span>

<span data-ttu-id="d7627-125">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d7627-126">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d7627-127">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="d7627-128">자산 업로드</span><span class="sxs-lookup"><span data-stu-id="d7627-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="d7627-129">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-129">Create an asset</span></span>

<span data-ttu-id="d7627-130">자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d7627-131">REST API를 자산 만들기 POST를 전송 해야 하는 hello에서 tooMedia 서비스를 요청 하 고 hello 요청 본문에 자산에 대 한 속성 정보를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="d7627-132">자산을 만드는 경우를 지정할 수 있는 hello 속성 중 하나 **옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="d7627-133">**옵션** 자산을 만들 수 있는 hello 암호화 옵션을 설명 하는 열거 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="d7627-134">유효한 값은 hello 아래 목록 값의 조합이 아니라 hello 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="d7627-135">**None** = **0**: 암호화가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="d7627-136">Hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-136">This is hello default value.</span></span> <span data-ttu-id="d7627-137">이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="d7627-138">Toodeliver MP4 점진적 다운로드를 사용 하 여 하려는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="d7627-139">**StorageEncrypted** = **1**: 업로드 및 저장에 대 한 AES 256 비트 암호화로 암호화 된 파일 toobe 프로그램에 대 한 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="d7627-140">자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="d7627-141">자세한 내용은 [자산 배달 정책 구성](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="d7627-142">**CommonEncryptionProtected** = **2**: 일반적인 암호화 방식(예: PlayReady)으로 보호된 파일을 업로드하는 경우 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="d7627-143">**EnvelopeEncryptionProtected** = **4**: AES로 암호화된 HLS 파일을 업로드하는 경우 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="d7627-144">참고 hello 파일을 인코딩된 있는지 및 Transform Manager를 통해 암호화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="d7627-145">자산 암호화를 사용 하는 경우 만들어야 합니다는 **ContentKey** hello 항목에 설명 된 대로 tooyour 자산에 연결:[어떻게 toocreate ContentKey](media-services-rest-create-contentkey.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="d7627-146">Hello 자산으로 hello 파일을 업로드 한 후 해야 hello에 tooupdate hello 암호화 속성 참고 **AssetFile** hello 하는 동안 가져온 hello 값이 있는 엔터티 **자산** 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="d7627-147">Hello를 사용 하 여 작업을 수행할 **병합** HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="d7627-148">hello 방법을 예제와 다음 toocreate 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="d7627-149">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="d7627-150">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-150">**HTTP Response**</span></span>

<span data-ttu-id="d7627-151">성공 하면 hello 다음 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="d7627-152">AssetFile 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-152">Create an AssetFile</span></span>
<span data-ttu-id="d7627-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 엔터티는 blob 컨테이너에 저장 하는 비디오 또는 오디오 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="d7627-154">자산 파일은 항상 자산에 연결되며 자산에는 하나 이상의 자산 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="d7627-155">hello 미디어 서비스 인코더 작업에는 자산 파일 개체가 blob 컨테이너의 디지털 파일과 연관 되지 않은 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="d7627-156">해당 hello 참고 **AssetFile** 인스턴스와 hello 실제 미디어 파일에는 별개의 두 개체 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="d7627-157">hello AssetFile 인스턴스 hello 미디어 파일 hello 실제 미디어 콘텐츠가 포함 되어 있지만 hello 미디어 파일에 대 한 메타 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="d7627-158">Hello를 사용 하는 blob 컨테이너에 디지털 미디어 파일을 업로드 한 후 **병합** HTTP 요청 tooupdate hello AssetFile (같이 hello 항목의 뒷부분에 나오는) 하 여 미디어 파일에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="d7627-159">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="d7627-160">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="d7627-161">쓰기 권한으로 hello AccessPolicy 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="d7627-162">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d7627-163">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="d7627-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d7627-164">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d7627-165">Blob 저장소에 파일을 업로드 하기 전에 hello 액세스 tooan asset을 작성 하기 위한 정책 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="d7627-166">HTTP 요청 toohello AccessPolicies 엔터티를 게시 하는 toodo 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="d7627-167">작성 시 DurationInMinutes 값을 정의하지 않으면 응답에서 500 내부 서버 오류 메시지가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="d7627-168">AccessPolicies에 대한 자세한 내용은 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="d7627-169">hello 방법을 예제와 다음 toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="d7627-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="d7627-170">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="d7627-171">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="d7627-172">Hello 업로드 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="d7627-172">Get hello Upload URL</span></span>
<span data-ttu-id="d7627-173">tooreceive 실제 업로드 URL hello, SAS 로케이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="d7627-174">로케이터는 tooaccess는 자산의 파일에에서는 클라이언트에 대 한 hello 시작 시간과 연결 끝점 유형을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="d7627-175">요청 및 요구 사항이 지정된 된 AccessPolicy-자산 쌍 toohandle 다른 클라이언트에 대 한 여러 개의 Locator 엔터티를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="d7627-176">이러한 각 로케이터 사용 하 여 hello StartTime 값과 DurationInMinutes 값 hello hello AccessPolicy toodetermine hello 기간 URL이 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="d7627-177">자세한 내용은 [로케이터](https://docs.microsoft.com/rest/api/media/operations/locator)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="d7627-178">SAS URL 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="d7627-179">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-179">Some considerations apply:</span></span>

* <span data-ttu-id="d7627-180">지정된 자산과 연관된 고유 로케이터는 한 번에 5개 이상 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="d7627-181">자세한 내용은 로케이터를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-181">For more information, see Locator.</span></span>
* <span data-ttu-id="d7627-182">필요한 경우 tooupload 파일 즉시, StartTime 값 toofive 분 hello 현재 시간 전에 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="d7627-183">클라이언트 컴퓨터와 미디어 서비스 사이에 시간차가 있을 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="d7627-184">또한 StartTime 값 날짜/시간 형식에 따라 hello에 이어야 합니다: YYYY-m M-DDTHH:mm:ssZ (예를 들어 "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="d7627-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="d7627-185">30 ~ 40 초 있을 수 있습니다 지연 로케이터를 만들면 toowhen 사용 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="d7627-186">이 문제는 tooboth SAS URL 및 Origin Locator를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="d7627-187">다음 예제는 hello toocreate 정의한 대로 SAS URL Locator를 (SAS 로케이터에 대 한 "1") 및 "2"에 대 한 주문형 origin locator hello 요청 본문의 Type 속성 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="d7627-188">hello **경로** 반환 된 속성을 사용 해야 tooupload 파일 hello URL이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="d7627-189">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="d7627-190">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-190">**HTTP Response**</span></span>

<span data-ttu-id="d7627-191">성공 하면 다음 응답 hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="d7627-192">Blob 저장소 컨테이너에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d7627-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="d7627-193">Hello AccessPolicy와 Locator 집합 있으면 hello 실제 파일이 hello Azure 저장소 REST Api를 사용 하 여 업로드 된 tooan Azure Blob 저장소 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="d7627-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="d7627-194">블록 blob으로 hello 파일을 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="d7627-195">페이지 blob은 Azure Media Services에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="d7627-196">Hello 파일 이름을 추가 해야 tooupload toohello 로케이터 hello 파일에 대 한 원하는 **경로** hello 이전 섹션에서 받은 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="d7627-197">예: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="d7627-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="d7627-198">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-198">.</span></span> <span data-ttu-id="d7627-199">.</span><span class="sxs-lookup"><span data-stu-id="d7627-199">.</span></span> <span data-ttu-id="d7627-200">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-200">.</span></span> 
> 
> 

<span data-ttu-id="d7627-201">Azure 저장소 Blob 작업에 대한 자세한 내용은 [Blob 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="d7627-202">Hello AssetFile 업데이트</span><span class="sxs-lookup"><span data-stu-id="d7627-202">Update hello AssetFile</span></span>
<span data-ttu-id="d7627-203">파일을 업로드 한 했으므로 hello FileAsset 크기 (및 다른) 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="d7627-204">예:</span><span class="sxs-lookup"><span data-stu-id="d7627-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="d7627-205">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-205">**HTTP Response**</span></span>

<span data-ttu-id="d7627-206">성공 hello 다음이 반환 됩니다: HTTP/1.1 204 콘텐츠 없음</span><span class="sxs-lookup"><span data-stu-id="d7627-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="d7627-207">Hello Locator와 AccessPolicy 삭제</span><span class="sxs-lookup"><span data-stu-id="d7627-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="d7627-208">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="d7627-209">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-209">**HTTP Response**</span></span>

<span data-ttu-id="d7627-210">성공 하면 hello 다음 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="d7627-211">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="d7627-212">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-212">**HTTP Response**</span></span>

<span data-ttu-id="d7627-213">성공 하면 hello 다음 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="d7627-214"><a id="upload_in_bulk"></a>대량으로 자산 업로드</span><span class="sxs-lookup"><span data-stu-id="d7627-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="d7627-215">Hello IngestManifest 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-215">Create hello IngestManifest</span></span>
<span data-ttu-id="d7627-216">hello IngestManifest는 자산, 자산 파일 및 수 있는 통계 정보 집합에 대 한 컨테이너 toodetermine hello 진행률 hello 집합에 대 한 대량 수집을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="d7627-217">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d7627-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="d7627-218">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-218">Create assets</span></span>
<span data-ttu-id="d7627-219">Hello IngestManifestAsset을 만들기 전에 toocreate hello 자산 대량 수집을 사용 하 여 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="d7627-220">자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d7627-221">Hello REST API, 자산 만들기 필요 Azure 미디어 서비스는 HTTP POST 요청 tooMicrosoft 보내고 hello 요청 본문에 자산에 대 한 속성 정보를 배치 합니다. 이 예제에서는 Asset hello hello 요청 본문에 포함 된 hello storageencrption (1) 옵션을 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="d7627-222">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="d7627-223">Hello IngestManifestAssets 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="d7627-224">IngestManifestAssets은 대량 수집에 사용되는 IngestManifest 내에서 자산을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="d7627-225">기본적으로 hello hello 자산 toohello 매니페스트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="d7627-226">Azure 미디어 서비스 ingestmanifestfile은 연결 된 컬렉션 toohello IngestManifestAsset에 따라 hello 파일 업로드를 위해 내부적으로 감시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="d7627-227">이러한 파일 업로드 되 면 hello 자산이 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="d7627-228">HTTP POST 요청으로 새로운 IngestManifestAsset을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="d7627-229">Hello 요청 본문에 hello IngestManifest Id 및 hello 자산 대량 수집을 위해 IngestManifestAsset이 함께 연결 해야 하는 hello Id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="d7627-230">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="d7627-231">각 자산에 대 한 hello Ingestmanifestfile 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="d7627-232">IngestManifestFile 자산에 대한 대량 수집의 일환으로 업로드될 실제 비디오 또는 오디오 blob 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="d7627-233">암호화 관련 hello 자산 암호화 옵션을 사용 하는 경우가 아니면 속성 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="d7627-234">이 섹션에 사용 하는 hello 예제 자산 이전에 만든 hello에 대 한 StorageEncryption을 사용 하는 IngestManifestFile 만들기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="d7627-235">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="d7627-236">Hello 파일 tooBlob 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="d7627-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="d7627-237">Hello 자산 파일 toohello blob 저장소 컨테이너 hello hello IngestManifest의 BlobStorageUriForUpload 속성에서 제공 하는 Uri를 업로드할 수 있는 고속 클라이언트 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="d7627-238">주목할 만한 고속 업로드 서비스 중 하나는 [Azure 응용 프로그램용 Aspera On Demand](http://go.microsoft.com/fwlink/?LinkId=272001)입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="d7627-239">대량 수집 진행률 모니터</span><span class="sxs-lookup"><span data-stu-id="d7627-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="d7627-240">대량 hello IngestManifest의 hello 통계 속성을 폴링하여 IngestManifest에 대 한 작업을 수집 hello 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="d7627-241">속성은 복합 형식인 [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics)입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="d7627-242">통계 속성 toopoll hello hello IngestManifest id입니다. 전달 HTTP GET 요청을 제출</span><span class="sxs-lookup"><span data-stu-id="d7627-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="d7627-243">암호화에 사용되는 ContentKey 만들기</span><span class="sxs-lookup"><span data-stu-id="d7627-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="d7627-244">자산 암호화를 사용 하는 경우 hello 자산 파일을 만들기 전에 암호화에 사용 되는 hello ContentKey toobe를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="d7627-245">저장소 암호화에 대 한 hello 다음과 같은 속성이 포함 되어야 합니다 hello 요청 본문에.</span><span class="sxs-lookup"><span data-stu-id="d7627-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="d7627-246">요청 본문 속성</span><span class="sxs-lookup"><span data-stu-id="d7627-246">Request body property</span></span> | <span data-ttu-id="d7627-247">설명</span><span class="sxs-lookup"><span data-stu-id="d7627-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7627-248">Id</span><span class="sxs-lookup"><span data-stu-id="d7627-248">Id</span></span> |<span data-ttu-id="d7627-249">hello 생성 하는 ContentKey Id를 수행 하는 hello를 사용 하 여 직접 형식으로 "nb:kid:UUID:<NEW GUID>"입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="d7627-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="d7627-250">ContentKeyType</span></span> |<span data-ttu-id="d7627-251">이 콘텐츠 키에 대 한 정수 hello 콘텐츠 키 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="d7627-252">저장소 암호화에 대 한 hello 값 1을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="d7627-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="d7627-253">EncryptedContentKey</span></span> |<span data-ttu-id="d7627-254">256비트(32바이트) 값인 새 콘텐츠 키 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="d7627-255">hello 키는 hello 저장소 암호화 X.509 인증서를 hello GetProtectionKeyId 및 GetProtectionKey 메서드에 대 한 HTTP GET 요청을 실행 하 여 Microsoft Azure 미디어 서비스에서 검색을 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="d7627-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="d7627-256">ProtectionKeyId</span></span> |<span data-ttu-id="d7627-257">콘텐츠 키를 사용 하는 tooencrypt hello 저장소 암호화 X.509 인증서에 대 한 보호 키 id hello는이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="d7627-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="d7627-258">ProtectionKeyType</span></span> |<span data-ttu-id="d7627-259">Hello 보호 키를 사용 하는 tooencrypt hello 콘텐츠 키에 대 한 hello 암호화 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="d7627-260">이 값은 예제에서 StorageEncryption(1)입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="d7627-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="d7627-261">Checksum</span></span> |<span data-ttu-id="d7627-262">hello MD5 hello 콘텐츠 키에 대 한 계산 된 체크섬입니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="d7627-263">Hello 콘텐츠 키를 가진 hello 콘텐츠 Id를 암호화 하 여 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="d7627-264">예제 코드에서는 hello toocalculate 체크섬 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="d7627-265">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="d7627-266">링크 hello ContentKey toohello 자산</span><span class="sxs-lookup"><span data-stu-id="d7627-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="d7627-267">hello ContentKey는 HTTP POST 요청을 전송 하 여 관련된 tooone 또는 자세한 자산은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="d7627-268">hello 다음 요청은 예제 toolink hello 예제 ContentKey toohello 예제 자산 id</span><span class="sxs-lookup"><span data-stu-id="d7627-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="d7627-269">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="d7627-270">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d7627-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="d7627-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7627-271">Next steps</span></span>

<span data-ttu-id="d7627-272">이제 업로드된 자산을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="d7627-273">자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="d7627-274">또한 Azure 함수 tootrigger hello 구성 컨테이너에 도착 하는 파일을 기반으로 하는 인코딩 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7627-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="d7627-275">자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7627-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d7627-276">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="d7627-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7627-277">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="d7627-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

