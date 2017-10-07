---
title: "-Azure 남은 부분과 aaaConfigure 콘텐츠 키 권한 부여 정책 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 미디어 서비스 REST API를 사용 하 여 콘텐츠 키에 대 한 권한 부여 정책."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c058b7682bcbfb736faba18ec7fce33f2f2acb49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="05beb-103">동적 암호화: 콘텐츠 키 인증 정책 구성</span><span class="sxs-lookup"><span data-stu-id="05beb-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="05beb-104">개요</span><span class="sxs-lookup"><span data-stu-id="05beb-104">Overview</span></span>
<span data-ttu-id="05beb-105">Microsoft Azure 미디어 서비스 있습니다 toodeliver 암호화 표준 AES (고급) (128 비트 암호화 키 사용) 및 PlayReady 또는 Widevine DRM을 사용 하 여 (동적)를 암호화 하 여 콘텐츠를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-105">Microsoft Azure Media Services enables you toodeliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="05beb-106">미디어 서비스는 또한 tooauthorized 클라이언트 키 및 PlayReady/Widevine 라이선스 배달용 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses tooauthorized clients.</span></span>

<span data-ttu-id="05beb-107">에 대해 원하는 tooencrypt 미디어 서비스 자산, 해야 tooassociate 암호화 키 (**CommonEncryption** 또는 **EnvelopeEncryption**) hello 자산에 (설명 된 대로 [여기](media-services-rest-create-contentkey.md)) 고도 hello 키 (이 문서에서 설명)에 대 한 권한 부여 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-107">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="05beb-108">미디어 서비스는 지정 된 hello 플레이어에서 스트림을 요청 되 면 키 toodynamically AES 또는 PlayReady 암호화를 사용 하 여 콘텐츠를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-108">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="05beb-109">toodecrypt hello 스트림 hello 플레이어 hello 키 배달 서비스에서 hello 키를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-109">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="05beb-110">hello 사용자가 아닌지 toodecide 권한이 tooget hello 키, hello 서비스 hello 키에 대해 지정한 hello 권한 부여 정책을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-110">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="05beb-111">미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="05beb-112">hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: **열고** 또는 **토큰** 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-112">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="05beb-113">보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-113">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="05beb-114">미디어 서비스는 hello에 토큰을 지원 **단순 웹 토큰** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 형식 및 * * **(JWT) JSON 웹 토큰 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-114">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="05beb-115">미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="05beb-116">사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-116">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="05beb-117">hello STS 구성된 toocreate hello 지정 된 키로 토큰에 서명 해야 하 고 (이 문서에서 설명)으로 hello 토큰 제한 구성에서 지정한 클레임을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-117">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="05beb-118">hello 미디어 서비스 키 배달 서비스는 hello 암호화 키 toohello 클라이언트 반환 hello 토큰은 유효 하 고 hello hello 토큰의 클레임이 일치 hello 콘텐츠 키에 대해 구성 된 경우.</span><span class="sxs-lookup"><span data-stu-id="05beb-118">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="05beb-119">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05beb-119">For more information, see</span></span>

[<span data-ttu-id="05beb-120">JWT 토큰 인증</span><span class="sxs-lookup"><span data-stu-id="05beb-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="05beb-121">[Azure Active Directory와 Azure 미디어 서비스 OWIN MVC 기반 앱을 Azure Active Directory와 통합하고 JWT 클레임을 기반으로 하는 콘텐츠 키 배달을 제한합니다](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="05beb-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="05beb-122">[Azure ACS tooissue 토큰을 사용 하 여](http://mingfeiy.com/acs-with-key-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-122">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="05beb-123">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-123">Some considerations apply:</span></span>
* <span data-ttu-id="05beb-124">toobe 수 toouse 동적 패키징 및 동적 암호화 toostream 원하는 끝점 콘텐츠 스트리밍 hello hello에 있는지 확인 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-124">toobe able toouse dynamic packaging and dynamic encryption, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>
* <span data-ttu-id="05beb-125">사용자의 자산은 적응 비트 전송률 MP4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="05beb-126">자세한 내용은 [자산 인코딩](media-services-encode-asset.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05beb-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="05beb-127">**AssetCreationOptions.StorageEncrypted** 옵션을 사용하여 자산을 업로드하고 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="05beb-128">동일 해야 하는 여러 콘텐츠 키 hello toohave 하려는 경우 정책 구성 하는 것이 권장 toocreate 단일 권한 부여 정책 및 여러 콘텐츠 키에 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-128">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="05beb-129">키 배달 서비스 hello ContentKeyAuthorizationPolicy 및 관련된 개체 (정책 옵션 및 제한) 15 분 동안 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-129">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="05beb-130">ContentKeyAuthorizationPolicy 만들기 및 toouse "토큰" 제한을 지정 합니다. 그런 다음 테스트 한 hello 정책을 업데이트 하는 경우 너무 "열" 제한, hello 정책 스위치 toohello "열기" 버전의 hello 정책 하기 전에 약 15 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-130">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="05beb-131">자산 배달 정책을 추가하거나 업데이트하는 경우 기존 로케이터(있는 경우)를 삭제하고 새 로케이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="05beb-132">현재 점진적 다운로드를 암호화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="05beb-133">AES 128 동적 암호화.</span><span class="sxs-lookup"><span data-stu-id="05beb-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="05beb-134">Hello hello 미디어 서비스 REST API를 사용 하는 경우 다음 고려 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-134">When working with hello Media Services REST API, hello following considerations apply:</span></span>
> 
> <span data-ttu-id="05beb-135">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="05beb-136">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05beb-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="05beb-137">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-137">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="05beb-138">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-138">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="05beb-139">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-139">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="05beb-140">열기 제한</span><span class="sxs-lookup"><span data-stu-id="05beb-140">Open Restriction</span></span>
<span data-ttu-id="05beb-141">개방형 제한 hello 시스템 키를 요청 하는 hello 키 tooanyone 제공 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-141">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="05beb-142">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="05beb-143">다음 예제는 hello open authorization 정책을 만들고 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-143">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="05beb-144"><a id="ContentKeyAuthorizationPolicies"></a>ContentKeyAuthorizationPolicies 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="05beb-145">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="05beb-146">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="05beb-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>ContentKeyAuthorizationPolicyOptions 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="05beb-148">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="05beb-149">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="05beb-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>ContentKeyAuthorizationPolicies를 옵션과 연결</span><span class="sxs-lookup"><span data-stu-id="05beb-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="05beb-151">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="05beb-152">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="05beb-153"><a id="AddAuthorizationPolicyToKey"></a>권한 부여 정책 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy toohello content key</span></span>
<span data-ttu-id="05beb-154">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="05beb-155">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="05beb-156">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="05beb-156">Token Restriction</span></span>
<span data-ttu-id="05beb-157">이 섹션에서는 toocreate 콘텐츠 키 권한 부여 정책 및 hello 콘텐츠 키와 연결 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-157">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="05beb-158">hello 권한 부여 정책은 설명 hello 사용자가 권한 있는 tooreceive hello 키 권한 부여 요구 사항이 충족된 toodetermine 이어야 합니다 (예를 들어 hello "확인 키" 목록 증명이 hello 키로 서명 된 hello 토큰).</span><span class="sxs-lookup"><span data-stu-id="05beb-158">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="05beb-159">XML toouse 해야 tooconfigure hello 토큰 제한 옵션을 toodescribe hello 토큰의 권한 부여 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-159">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="05beb-160">hello 토큰 제한 구성 XML은 XML 스키마를 따르는 toohello를 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-160">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="05beb-161"><a id="schema"></a>토큰 제한 스키마</span><span class="sxs-lookup"><span data-stu-id="05beb-161"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="05beb-162">Hello를 구성할 때 **토큰** 제한 정책을, hello 기본 * * 확인 키 * *를 지정 해야 **발급자** 및 **audience** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-162">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="05beb-163">hello * * 기본 확인 키 * * 포함 토큰 hello hello 키 서명 된 **발급자** hello 보안 토큰 서비스에는 해당 문제 hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-163">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="05beb-164">hello **audience** (라고도 **범위**) hello 의도 설명 hello 토큰 hello 토큰 또는 hello 리소스에 대 한 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-164">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="05beb-165">hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-165">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="05beb-166">다음 예제는 hello 토큰 제한 된 권한 부여 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-166">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="05beb-167">이 예제에서는 hello 클라이언트는 toopresent 포함 하는 토큰: 서명 요구 된 클레임, 토큰 발급자 및 키 제시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-167">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="05beb-168">ContentKeyAuthorizationPolicies 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="05beb-169">표시 된 것 처럼 "토큰 제한 정책" hello 만들기 [여기](#ContentKeyAuthorizationPolicies)합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-169">Create hello "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="05beb-170">ContentKeyAuthorizationPolicyOptions 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="05beb-171">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="05beb-172">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="05beb-173">ContentKeyAuthorizationPolicies를 옵션과 연결</span><span class="sxs-lookup"><span data-stu-id="05beb-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="05beb-174">[여기](#ContentKeyAuthorizationPolicies)에 표시된 대로 ContentKeyAuthorizationPolicies을 옵션과 연결</span><span class="sxs-lookup"><span data-stu-id="05beb-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="05beb-175">권한 부여 정책 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-175">Add authorization policy toohello content key</span></span>
<span data-ttu-id="05beb-176">표시 된 것 처럼 AuthorizationPolicy toohello ContentKey 추가 [여기](#AddAuthorizationPolicyToKey)합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-176">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="05beb-177">PlayReady 동적 암호화</span><span class="sxs-lookup"><span data-stu-id="05beb-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="05beb-178">미디어 서비스 tooconfigure hello 권한 및 제한 되도록 PlayReady DRM 런타임에서 tooenforce hello에 대 한 사용자가 하려고 할 때 tooplay 다시 보호 된 콘텐츠를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-178">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="05beb-179">PlayReady로 콘텐츠를 보호 하는 경우 hello 중 하나가 필요한 권한 부여 정책에서 toospecify hello를 정의 하는 XML 문자열은 [PlayReady 라이선스 템플릿을](media-services-playready-license-template-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-179">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="05beb-180">열기 제한</span><span class="sxs-lookup"><span data-stu-id="05beb-180">Open Restriction</span></span>
<span data-ttu-id="05beb-181">개방형 제한 hello 시스템 키를 요청 하는 hello 키 tooanyone 제공 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-181">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="05beb-182">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="05beb-183">다음 예제는 hello open authorization 정책을 만들고 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-183">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="05beb-184"><a id="ContentKeyAuthorizationPolicies2"></a>ContentKeyAuthorizationPolicies 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="05beb-185">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="05beb-186">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="05beb-187">ContentKeyAuthorizationPolicyOptions 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="05beb-188">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="05beb-189">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="05beb-190">ContentKeyAuthorizationPolicies를 옵션과 연결</span><span class="sxs-lookup"><span data-stu-id="05beb-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="05beb-191">[여기](#ContentKeyAuthorizationPolicies)에 표시된 대로 ContentKeyAuthorizationPolicies을 옵션과 연결</span><span class="sxs-lookup"><span data-stu-id="05beb-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="05beb-192">권한 부여 정책 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-192">Add authorization policy toohello content key</span></span>
<span data-ttu-id="05beb-193">표시 된 것 처럼 AuthorizationPolicy toohello ContentKey 추가 [여기](#AddAuthorizationPolicyToKey)합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-193">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="05beb-194">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="05beb-194">Token Restriction</span></span>
<span data-ttu-id="05beb-195">XML toouse 해야 tooconfigure hello 토큰 제한 옵션을 toodescribe hello 토큰의 권한 부여 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-195">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="05beb-196">hello 토큰 제한 구성 XML에 표시 된 toohello XML 스키마를 준수 해야 [이](#schema) 섹션.</span><span class="sxs-lookup"><span data-stu-id="05beb-196">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="05beb-197">ContentKeyAuthorizationPolicies 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="05beb-198">[여기](#ContentKeyAuthorizationPolicies2)에 표시된 대로 ContentKeyAuthorizationPolicies 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="05beb-199">ContentKeyAuthorizationPolicyOptions 만들기</span><span class="sxs-lookup"><span data-stu-id="05beb-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="05beb-200">요청:</span><span class="sxs-lookup"><span data-stu-id="05beb-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="05beb-201">응답:</span><span class="sxs-lookup"><span data-stu-id="05beb-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="05beb-202">ContentKeyAuthorizationPolicies를 옵션과 연결</span><span class="sxs-lookup"><span data-stu-id="05beb-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="05beb-203">[여기](#ContentKeyAuthorizationPolicies)에 표시된 대로 ContentKeyAuthorizationPolicies을 옵션과 연결</span><span class="sxs-lookup"><span data-stu-id="05beb-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="05beb-204">권한 부여 정책 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-204">Add authorization policy toohello content key</span></span>
<span data-ttu-id="05beb-205">표시 된 것 처럼 AuthorizationPolicy toohello ContentKey 추가 [여기](#AddAuthorizationPolicyToKey)합니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-205">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="05beb-206"><a id="types"></a>ContentKeyAuthorizationPolicy를 정의할 때 사용되는 형식</span><span class="sxs-lookup"><span data-stu-id="05beb-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="05beb-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="05beb-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="05beb-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="05beb-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="05beb-209">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="05beb-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="05beb-210">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="05beb-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="05beb-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05beb-211">Next Steps</span></span>
<span data-ttu-id="05beb-212">콘텐츠 키 권한 부여 정책을 구성 했으므로 이동 toohello [어떻게 tooconfigure 자산 배달 정책](media-services-rest-configure-asset-delivery-policy.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="05beb-212">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

