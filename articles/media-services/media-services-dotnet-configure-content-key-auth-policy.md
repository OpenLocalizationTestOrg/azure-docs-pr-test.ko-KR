---
title: "미디어 서비스.NET SDK를 사용 하 여 aaaConfigure 콘텐츠 키 권한 부여 정책 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 미디어 서비스.NET SDK를 사용 하 여 콘텐츠 키에 대 한 권한 부여 정책."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="f49a7-103">동적 암호화: 콘텐츠 키 인증 정책 구성</span><span class="sxs-lookup"><span data-stu-id="f49a7-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="f49a7-104">개요</span><span class="sxs-lookup"><span data-stu-id="f49a7-104">Overview</span></span>
<span data-ttu-id="f49a7-105">Microsoft Azure 미디어 서비스 사용 하면 toodeliver MPEG DASH, 부드러운 스트리밍 및 HTTP 라이브 스트리밍 (HLS) 스트림에서 보호 된 암호화 표준 AES (고급) (128 비트 암호화 키 사용) 또는 [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="f49a7-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="f49a7-106">AMS 있습니다 toodeliver DASH 스트림을 Widevine DRM을 사용 하 여 암호화를 통해 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="f49a7-107">PlayReady 및 Widevine 모두 hello 일반 암호화 (ISO/IEC 23001-7 CENC) 사양 당 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="f49a7-108">또한 미디어 서비스 제공는 **키/라이선스 배달 서비스** 있는 클라이언트에서 AES 키를 가져올 수 또는 PlayReady/Widevine 라이선스 tooplay 암호화 된 콘텐츠를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="f49a7-109">에 대해 원하는 tooencrypt 미디어 서비스 자산, 해야 tooassociate 암호화 키 (**CommonEncryption** 또는 **EnvelopeEncryption**) hello 자산에 (설명 된 대로 [여기](media-services-dotnet-create-contentkey.md)) 고도 hello 키 (이 문서에서 설명)에 대 한 권한 부여 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="f49a7-110">미디어 서비스는 지정 된 hello 플레이어에서 스트림을 요청 되 면 키 toodynamically AES 또는 DRM 암호화를 사용 하 여 콘텐츠를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="f49a7-111">toodecrypt hello 스트림 hello 플레이어 hello 키 배달 서비스에서 hello 키를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="f49a7-112">hello 사용자가 아닌지 toodecide 권한이 tooget hello 키, hello 서비스 hello 키에 대해 지정한 hello 권한 부여 정책을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="f49a7-113">미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="f49a7-114">hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: **열고** 또는 **토큰** 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="f49a7-115">보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="f49a7-116">미디어 서비스는 hello에 토큰을 지원 **단순 웹 토큰** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 형식 및 **JSON 웹 토큰** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="f49a7-117">미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="f49a7-118">사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="f49a7-119">hello STS 구성된 toocreate hello 지정 된 키로 토큰에 서명 해야 하 고 (이 문서에서 설명)으로 hello 토큰 제한 구성에서 지정한 클레임을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="f49a7-120">hello 미디어 서비스 키 배달 서비스는 hello 암호화 키 toohello 클라이언트 반환 hello 토큰은 유효 하 고 hello hello 토큰의 클레임이 일치 hello 콘텐츠 키에 대해 구성 된 경우.</span><span class="sxs-lookup"><span data-stu-id="f49a7-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="f49a7-121">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f49a7-121">For more information, see</span></span>

[<span data-ttu-id="f49a7-122">JWT 토큰 인증</span><span class="sxs-lookup"><span data-stu-id="f49a7-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="f49a7-123">[Azure Active Directory와 Azure 미디어 서비스 OWIN MVC 기반 앱을 Azure Active Directory와 통합하고 JWT 클레임을 기반으로 하는 콘텐츠 키 배달을 제한합니다](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="f49a7-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="f49a7-124">[Azure ACS tooissue 토큰을 사용 하 여](http://mingfeiy.com/acs-with-key-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="f49a7-125">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-125">Some considerations apply:</span></span>
* <span data-ttu-id="f49a7-126">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="f49a7-127">동적 패키징 및 동적 암호화, 하려면 스트리밍 끝점, 콘텐츠 및 take 있다는 이점이 스트리밍 toostart hello에 대 한 toobe **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="f49a7-128">사용자의 자산은 적응 비트 전송률 MP4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="f49a7-129">자세한 내용은 [자산 인코딩](media-services-encode-asset.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f49a7-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="f49a7-130">**AssetCreationOptions.StorageEncrypted** 옵션을 사용하여 자산을 업로드하고 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="f49a7-131">동일 해야 하는 여러 콘텐츠 키 hello toohave 하려는 경우 정책 구성 하는 것이 권장 toocreate 단일 권한 부여 정책 및 여러 콘텐츠 키에 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="f49a7-132">키 배달 서비스 hello ContentKeyAuthorizationPolicy 및 관련된 개체 (정책 옵션 및 제한) 15 분 동안 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="f49a7-133">ContentKeyAuthorizationPolicy 만들기 및 toouse "토큰" 제한을 지정 합니다. 그런 다음 테스트 한 hello 정책을 업데이트 하는 경우 너무 "열" 제한, hello 정책 스위치 toohello "열기" 버전의 hello 정책 하기 전에 약 15 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="f49a7-134">자산 배달 정책을 추가하거나 업데이트하는 경우 기존 로케이터(있는 경우)를 삭제하고 새 로케이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="f49a7-135">현재 점진적 다운로드를 암호화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="f49a7-136">AES 128 동적 암호화.</span><span class="sxs-lookup"><span data-stu-id="f49a7-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="f49a7-137">열기 제한</span><span class="sxs-lookup"><span data-stu-id="f49a7-137">Open Restriction</span></span>
<span data-ttu-id="f49a7-138">개방형 제한 hello 시스템 키를 요청 하는 hello 키 tooanyone 제공 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="f49a7-139">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="f49a7-140">다음 예제는 hello open authorization 정책을 만들고 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="f49a7-141">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="f49a7-141">Token Restriction</span></span>
<span data-ttu-id="f49a7-142">이 섹션에서는 toocreate 콘텐츠 키 권한 부여 정책 및 hello 콘텐츠 키와 연결 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="f49a7-143">hello 권한 부여 정책은 설명 hello 사용자가 권한 있는 tooreceive hello 키 권한 부여 요구 사항이 충족된 toodetermine 이어야 합니다 (예를 들어 hello "확인 키" 목록 증명이 hello 키로 서명 된 hello 토큰).</span><span class="sxs-lookup"><span data-stu-id="f49a7-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="f49a7-144">XML toouse 해야 tooconfigure hello 토큰 제한 옵션을 toodescribe hello 토큰의 권한 부여 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="f49a7-145">hello 토큰 제한 구성 XML은 XML 스키마를 따르는 toohello를 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="f49a7-146"><a id="schema"></a>토큰 제한 스키마</span><span class="sxs-lookup"><span data-stu-id="f49a7-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="f49a7-147">Hello를 구성할 때 **토큰** 제한 정책을, hello 기본 * * 확인 키 * *를 지정 해야 **발급자** 및 **audience** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="f49a7-148">hello * * 기본 확인 키 * * 포함 토큰 hello hello 키 서명 된 **발급자** hello 보안 토큰 서비스에는 해당 문제 hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="f49a7-149">hello **audience** (라고도 **범위**) hello 의도 설명 hello 토큰 hello 토큰 또는 hello 리소스에 대 한 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="f49a7-150">hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="f49a7-151">사용 하는 경우 **Media Services SDK for.NET**, hello를 사용할 수 있습니다 **TokenRestrictionTemplate** 클래스 toogenerate hello 제한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="f49a7-152">다음 예제는 hello 토큰 제한 된 권한 부여 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="f49a7-153">이 예제에서는 hello 클라이언트는 toopresent 포함 하는 토큰: 서명 요구 된 클레임, 토큰 발급자 및 키 제시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
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

#### <span data-ttu-id="f49a7-154"><a id="test"></a>테스트 토큰</span><span class="sxs-lookup"><span data-stu-id="f49a7-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="f49a7-155">tooget hello 키 권한 부여 정책에 사용 된 hello 토큰 제한에 따라 테스트 토큰, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="f49a7-156">PlayReady 동적 암호화</span><span class="sxs-lookup"><span data-stu-id="f49a7-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="f49a7-157">미디어 서비스 tooconfigure hello 권한 및 제한 되도록 PlayReady DRM 런타임에서 tooenforce hello에 대 한 사용자가 하려고 할 때 tooplay 다시 보호 된 콘텐츠를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="f49a7-158">PlayReady로 콘텐츠를 보호 하는 경우 hello 중 하나가 필요한 권한 부여 정책에서 toospecify hello를 정의 하는 XML 문자열은 [PlayReady 라이선스 템플릿을](media-services-playready-license-template-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="f49a7-159">Media Services SDK for.NET에서에서 hello **PlayReadyLicenseResponseTemplate** 및 **PlayReadyLicenseTemplate** 클래스 hello PlayReady 라이선스 템플릿을 정의 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="f49a7-160">[이 항목](media-services-protect-with-drm.md) 표시 방법을 tooencrypt 사용 하 여 콘텐츠 **PlayReady** 및 **Widevine**합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="f49a7-161">열기 제한</span><span class="sxs-lookup"><span data-stu-id="f49a7-161">Open Restriction</span></span>
<span data-ttu-id="f49a7-162">개방형 제한 hello 시스템 키를 요청 하는 hello 키 tooanyone 제공 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="f49a7-163">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="f49a7-164">다음 예제는 hello open authorization 정책을 만들고 toohello 콘텐츠 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="f49a7-165">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="f49a7-165">Token Restriction</span></span>
<span data-ttu-id="f49a7-166">XML toouse 해야 tooconfigure hello 토큰 제한 옵션을 toodescribe hello 토큰의 권한 부여 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="f49a7-167">hello 토큰 제한 구성 XML에 표시 된 toohello XML 스키마를 준수 해야 [이](#schema) 섹션.</span><span class="sxs-lookup"><span data-stu-id="f49a7-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
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

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="f49a7-168">hello 키 권한 부여 정책 참조에 사용 된 hello 토큰 제한에 따라 테스트 토큰 tooget [이](#test) 섹션.</span><span class="sxs-lookup"><span data-stu-id="f49a7-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="f49a7-169"><a id="types"></a>ContentKeyAuthorizationPolicy를 정의할 때 사용되는 형식</span><span class="sxs-lookup"><span data-stu-id="f49a7-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="f49a7-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="f49a7-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="f49a7-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="f49a7-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="f49a7-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="f49a7-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="f49a7-173">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="f49a7-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f49a7-174">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f49a7-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="f49a7-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f49a7-175">Next step</span></span>
<span data-ttu-id="f49a7-176">콘텐츠 키 권한 부여 정책을 구성 했으므로 이동 toohello [어떻게 tooconfigure 자산 배달 정책](media-services-dotnet-configure-asset-delivery-policy.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a7-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

