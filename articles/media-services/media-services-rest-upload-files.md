---
title: "REST를 사용하여 Media Services 계정에 파일 업로드 | Microsoft Docs"
description: "자산을 만들고 업로드하여 미디어 서비스에 미디어 콘텐츠를 가져오는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="d033b-103">REST를 사용하여 Media Services 계정에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d033b-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d033b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d033b-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="d033b-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="d033b-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="d033b-106">포털</span><span class="sxs-lookup"><span data-stu-id="d033b-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="d033b-107">미디어 서비스에서 자산에 디지털 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="d033b-108">[자산](https://docs.microsoft.com/rest/api/media/operations/asset) 엔터티에는 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택 자막 파일(및 이러한 파일에 대한 메타데이터)이 포함될 수 있습니다.  자산에 파일이 업로드되면 이후 처리 및 스트리밍을 위해 콘텐츠가 클라우드에 안전하게 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="d033b-109">고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="d033b-110">Media Services는 스트리밍 콘텐츠(예: http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.)를 위해 URL을 작성할 때 IAssetFile.Name 속성 값을 사용합니다. 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="d033b-111">**Name** 속성 값에는 !*'();:@&=+$,/?%#[]"와 같은 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="d033b-112">또한 파일 이름 확장명에는 ‘.’ 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="d033b-113">이름 길이는 260자보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="d033b-114">Media Services에서 처리를 위해 지원되는 최대 파일 크기에 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="d033b-115">파일 크기 제한에 대한 세부 정보는 [이](media-services-quotas-and-limitations.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="d033b-116">자산 업로드를 위한 기본 워크플로는 다음 섹션으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="d033b-117">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-117">Create an Asset</span></span>
* <span data-ttu-id="d033b-118">자산 암호화(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="d033b-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="d033b-119">Blob 저장소에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d033b-119">Upload a file to blob storage</span></span>

<span data-ttu-id="d033b-120">또한 AMS을 사용하면 대량으로 자산을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="d033b-121">자세한 내용은 [이](media-services-rest-upload-files.md#upload_in_bulk) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="d033b-122">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d033b-123">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="d033b-124">미디어 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="d033b-124">Connect to Media Services</span></span>

<span data-ttu-id="d033b-125">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d033b-126">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d033b-127">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="d033b-128">자산 업로드</span><span class="sxs-lookup"><span data-stu-id="d033b-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="d033b-129">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-129">Create an asset</span></span>

<span data-ttu-id="d033b-130">자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d033b-131">REST API에서 자산을 만들려면 미디어 서비스에 POST 요청을 보내고 자산에 대한 속성 정보를 요청 본문에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="d033b-132">자산을 만들 때 지정할 수 있는 속성 중 하나는 **옵션**입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="d033b-133">**옵션** 은 자산으로 만들 수 있는 암호화 옵션을 설명하는 열거 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="d033b-134">유효한 값은 값의 조합이 아니라 아래 목록에 있는 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="d033b-135">**None** = **0**: 암호화가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="d033b-136">기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-136">This is the default value.</span></span> <span data-ttu-id="d033b-137">이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="d033b-138">MP4를 배달하려는 경우 이 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="d033b-139">**StorageEncrypted** = **1**: 파일 업로드 및 저장 시 AES-256비트 암호화로 암호화할 것인지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="d033b-140">자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="d033b-141">자세한 내용은 [자산 배달 정책 구성](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="d033b-142">**CommonEncryptionProtected** = **2**: 일반적인 암호화 방식(예: PlayReady)으로 보호된 파일을 업로드하는 경우 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="d033b-143">**EnvelopeEncryptionProtected** = **4**: AES로 암호화된 HLS 파일을 업로드하는 경우 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="d033b-144">파일을 Transform Manager로 인코딩 및 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="d033b-145">자산에서 암호화를 사용하는 경우 **ContentKey** 를 만들어 이를[ContentKey를 만드는 방법](media-services-rest-create-contentkey.md)항목에서 설명한 대로 자산에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="d033b-146">자산에 파일을 업로드한 후에는 **자산**을 암호화하는 동안 얻은 값으로 **AssetFile** 엔터티의 암호화 속성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="d033b-147">**MERGE** HTTP 요청을 사용하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="d033b-148">다음 예제에서는 자산을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="d033b-149">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-149">**HTTP Request**</span></span>

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

<span data-ttu-id="d033b-150">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-150">**HTTP Response**</span></span>

<span data-ttu-id="d033b-151">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-151">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="d033b-152">AssetFile 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-152">Create an AssetFile</span></span>
<span data-ttu-id="d033b-153">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 엔터티는 blob 컨테이너에 저장된 비디오 또는 오디오 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="d033b-154">자산 파일은 항상 자산에 연결되며 자산에는 하나 이상의 자산 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="d033b-155">자산 파일 개체가 blob 컨테이너의 디지털 파일과 연결되지 않은 경우 미디어 서비스 인코더 작업을 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="d033b-156">**AssetFile** 인스턴스와 실제 미디어 파일은 뚜렷이 다른 두 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="d033b-157">AssetFile 인스턴스는 미디어 파일에 대한 메타데이터를 포함하는 반면 미디어 파일은 실제 미디어 콘텐츠를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="d033b-158">Blob 컨테이너에 디지털 미디어 파일을 업로드 한 후 **MERGE** HTTP 요청을 사용하여 미디어 파일에 대한 정보로 AssetFile을 업데이트하게 됩니다(이 항목의 뒷부분 참조).</span><span class="sxs-lookup"><span data-stu-id="d033b-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="d033b-159">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-159">**HTTP Request**</span></span>

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

<span data-ttu-id="d033b-160">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="d033b-161">쓰기 권한으로 AccessPolicy를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="d033b-162">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d033b-163">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d033b-164">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d033b-165">blob 저장소에 모든 파일을 업로드하기 전에 자산에 쓰기 위한 액세스 정책 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="d033b-166">이렇게 하려면 AccessPolicies 엔터티 집합에 HTTP 요청을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="d033b-167">작성 시 DurationInMinutes 값을 정의하지 않으면 응답에서 500 내부 서버 오류 메시지가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="d033b-168">AccessPolicies에 대한 자세한 내용은 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="d033b-169">다음 예제에서는 AccessPolicy를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="d033b-170">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-170">**HTTP Request**</span></span>

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

<span data-ttu-id="d033b-171">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="d033b-172">업로드 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="d033b-172">Get the Upload URL</span></span>
<span data-ttu-id="d033b-173">실제 업로드 URL을 받으려면 SAS 로케이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="d033b-174">로케이터는 자산에 있는 파일에 액세스하려는 클라이언트에 대한 시작 시간과 연결 끝점의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="d033b-175">다양한 클라이언트 요청 및 요구 사항을 처리하기 위해 지정된 AccessPolicy 및 자산 쌍에 대해 여러 로케이터 엔터티를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="d033b-176">이러한 각 로케이터는 AccessPolicy의 StartTime 값과 DurationInMinutes 값을 사용하여 URL이 사용될 수는 시간의 길이를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="d033b-177">자세한 내용은 [로케이터](https://docs.microsoft.com/rest/api/media/operations/locator)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="d033b-178">SAS URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="d033b-179">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-179">Some considerations apply:</span></span>

* <span data-ttu-id="d033b-180">지정된 자산과 연관된 고유 로케이터는 한 번에 5개 이상 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="d033b-181">자세한 내용은 로케이터를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-181">For more information, see Locator.</span></span>
* <span data-ttu-id="d033b-182">파일을 즉시 업로드해야 하는 경우 StartTime 값을 현재 시간에서 5분 전으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="d033b-183">클라이언트 컴퓨터와 미디어 서비스 사이에 시간차가 있을 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="d033b-184">또한 StartTime 값은 다음 DateTime 형식이어야 합니다. YYYY-MM-DDTHH:mm:ssZ(예: "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="d033b-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="d033b-185">로케이터를 만든 후 사용할 수 있을 때까지 30-40초의 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="d033b-186">이 문제는 SAS URL 및 원본 로케이터 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="d033b-187">다음 예제에서는 요청 본문의 형식 속성에서 정의한 대로(SAS 로케이터의 경우 "1" 그리고 주문형 원본 로케이터의 경우 "2") SAS URL 로케이터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="d033b-188">반환된 **경로** 속성은 파일 업로드 시 반드시 사용해야 하는 URL을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="d033b-189">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-189">**HTTP Request**</span></span>

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

<span data-ttu-id="d033b-190">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-190">**HTTP Response**</span></span>

<span data-ttu-id="d033b-191">성공하면 다음 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="d033b-192">Blob 저장소 컨테이너에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d033b-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="d033b-193">AccessPolicy와 로케이터를 설정했으면 실제 파일은 Azure 저장소 REST API를 사용하여 Azure Blob 저장소 컨테이너에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="d033b-194">블록 blob으로 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="d033b-195">페이지 blob은 Azure Media Services에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="d033b-196">이전 섹션에서 받은 로케이터 **경로** 값에 업로드하려는 파일에 대한 파일 이름을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="d033b-197">예: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="d033b-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="d033b-198">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-198">.</span></span> <span data-ttu-id="d033b-199">.</span><span class="sxs-lookup"><span data-stu-id="d033b-199">.</span></span> <span data-ttu-id="d033b-200">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-200">.</span></span> 
> 
> 

<span data-ttu-id="d033b-201">Azure 저장소 Blob 작업에 대한 자세한 내용은 [Blob 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="d033b-202">AssetFile 업데이트</span><span class="sxs-lookup"><span data-stu-id="d033b-202">Update the AssetFile</span></span>
<span data-ttu-id="d033b-203">이제 파일을 업로드했으므로 FileAsset 크기(및 기타) 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="d033b-204">예:</span><span class="sxs-lookup"><span data-stu-id="d033b-204">For example:</span></span>

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


<span data-ttu-id="d033b-205">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-205">**HTTP Response**</span></span>

<span data-ttu-id="d033b-206">성공하면 HTTP/1.1 204 내용 없음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="d033b-207">로케이터와 AccessPolicy 삭제</span><span class="sxs-lookup"><span data-stu-id="d033b-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="d033b-208">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="d033b-209">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-209">**HTTP Response**</span></span>

<span data-ttu-id="d033b-210">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="d033b-211">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="d033b-212">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-212">**HTTP Response**</span></span>

<span data-ttu-id="d033b-213">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="d033b-214"><a id="upload_in_bulk"></a>대량으로 자산 업로드</span><span class="sxs-lookup"><span data-stu-id="d033b-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="d033b-215">IngestManifest 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-215">Create the IngestManifest</span></span>
<span data-ttu-id="d033b-216">IngestManifest는 집합에 대해 대량 수집의 진행률을 확인하는 데 사용할 수 있는 자산, 자산 파일 및 통계 정보의 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="d033b-217">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="d033b-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="d033b-218">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-218">Create assets</span></span>
<span data-ttu-id="d033b-219">IngestManifestAsset을 만들기 전에 대량 수집을 사용하여 완료할 수 있는 자산을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="d033b-220">자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d033b-221">REST API에서 자산 생성은 Microsoft Azure 미디어 서비스에 HTTP POST 요청을 보내고 요청 본문에 자산에 대한 속성 정보를 배치해야 합니다. 이 예제에서는 요청 본문에 포함된 StorageEncrption(1) 옵션을 사용하여 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="d033b-222">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-222">**HTTP Response**</span></span>

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

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="d033b-223">IngestManifestAssets 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="d033b-224">IngestManifestAssets은 대량 수집에 사용되는 IngestManifest 내에서 자산을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="d033b-225">기본적으로 자산을 매니페스트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="d033b-226">Azure 미디어 서비스는 IngestManifestAsset에 연관된 IngestManifestFiles 컬렉션에 기반하여 파일 업로드를 내부적으로 감시합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="d033b-227">이러한 파일을 업로드하면 자산이 완성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="d033b-228">HTTP POST 요청으로 새로운 IngestManifestAsset을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="d033b-229">IngestManifestAsset이 대량 수집을 위해 함께 연결해야 하는 IngestManifest ID 및 자산 ID를 요청 본문에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="d033b-230">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-230">**HTTP Response**</span></span>

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


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="d033b-231">각 자산에 대한 IngestManifestFiles 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="d033b-232">IngestManifestFile 자산에 대한 대량 수집의 일환으로 업로드될 실제 비디오 또는 오디오 blob 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="d033b-233">자산이 암호화 옵션을 사용하지 않으면 암호화 관련 속성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="d033b-234">이 섹션에 사용된 예제는 이전에 만든 자산에 StorageEncryption를 사용하는 IngestManifestFile를 만드는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="d033b-235">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-235">**HTTP Response**</span></span>

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

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="d033b-236">Blob 저장소에 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d033b-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="d033b-237">IngestManifest의  BlobStorageUriForUpload 속성이 제공하는 blob 저장소 컨테이너 URI에 자산 파일을 업로드할 수 있는 고속 클라이언트 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="d033b-238">주목할 만한 고속 업로드 서비스 중 하나는 [Azure 응용 프로그램용 Aspera On Demand](http://go.microsoft.com/fwlink/?LinkId=272001)입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="d033b-239">대량 수집 진행률 모니터</span><span class="sxs-lookup"><span data-stu-id="d033b-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="d033b-240">IngestManifest의 통계 속성을 폴링하여 IngestManifest에 대한 대량 수집 과정을 
모니터할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="d033b-241">속성은 복합 형식인 [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics)입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="d033b-242">통계 속성을 폴링하여 IngestManifest ID를 전달하는 HTTP GET 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="d033b-243">암호화에 사용되는 ContentKey 만들기</span><span class="sxs-lookup"><span data-stu-id="d033b-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="d033b-244">자산에 암호화를 사용하면 자산 파일을 만들기 전에 암호화에 사용할 ContentKey를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="d033b-245">저장소 암호화를 위해 다음 속성을 요청 본문에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="d033b-246">요청 본문 속성</span><span class="sxs-lookup"><span data-stu-id="d033b-246">Request body property</span></span> | <span data-ttu-id="d033b-247">설명</span><span class="sxs-lookup"><span data-stu-id="d033b-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d033b-248">Id</span><span class="sxs-lookup"><span data-stu-id="d033b-248">Id</span></span> |<span data-ttu-id="d033b-249">“nb:kid:UUID:<NEW GUID>” 형식을 사용하여 직접 생성하는 ContentKey Id입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="d033b-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="d033b-250">ContentKeyType</span></span> |<span data-ttu-id="d033b-251">이 콘텐츠 키에 대한 정수인 콘텐츠 키 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="d033b-252">저장소 암호화에 1값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="d033b-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="d033b-253">EncryptedContentKey</span></span> |<span data-ttu-id="d033b-254">256비트(32바이트) 값인 새 콘텐츠 키 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="d033b-255">GetProtectionKeyId 및 GetProtectionKey 메서드에 대한 HTTP GET 요청을 실행하여 Microsoft Azure 미디어 서비스에서 검색하는 저장소 암호화 X.509 인증서를 사용하여 키를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="d033b-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="d033b-256">ProtectionKeyId</span></span> |<span data-ttu-id="d033b-257">콘텐츠 키를 암호화하는 데 사용한 저장소 암호화 X.509 인증서에 대한 보호 키 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="d033b-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="d033b-258">ProtectionKeyType</span></span> |<span data-ttu-id="d033b-259">콘텐츠 키를 암호화하는 데 사용한 보호 키에 대한 암호화 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="d033b-260">이 값은 예제에서 StorageEncryption(1)입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="d033b-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="d033b-261">Checksum</span></span> |<span data-ttu-id="d033b-262">콘텐츠 키에 대한 MD5 계산 된 체크섬입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="d033b-263">콘텐츠 키로 콘텐츠 ID를 암호화하여 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="d033b-264">예제 코드는 체크섬을 계산하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="d033b-265">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-265">**HTTP Response**</span></span>

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

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="d033b-266">ContentKey를 자산에 연결</span><span class="sxs-lookup"><span data-stu-id="d033b-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="d033b-267">ContentKey는 HTTP POST 요청을 전송하여 하나 이상의 자산에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="d033b-268">다음 요청은 예제 ContentKey를 예제 자산 ID에 연결하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="d033b-269">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-269">**HTTP Response**</span></span>

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

<span data-ttu-id="d033b-270">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="d033b-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="d033b-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d033b-271">Next steps</span></span>

<span data-ttu-id="d033b-272">이제 업로드된 자산을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="d033b-273">자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="d033b-274">또한 Azure Functions를 사용하여 구성된 컨테이너에 도착하는 파일에 따라 인코딩 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d033b-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="d033b-275">자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d033b-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d033b-276">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="d033b-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d033b-277">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="d033b-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

