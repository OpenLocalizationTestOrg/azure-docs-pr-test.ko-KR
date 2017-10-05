---
title: "Media Services .NET SDK를 사용하여 콘텐츠 키 권한 부여 정책 구성 | Microsoft 문서"
description: "미디어 서비스 .NET SDK를 사용하여 콘텐츠 키에 대한 인증 정책을 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 75dd9107dca215a0b31db3d44bada69210fe9ac6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="cd98c-103">동적 암호화: 콘텐츠 키 인증 정책 구성</span><span class="sxs-lookup"><span data-stu-id="cd98c-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="cd98c-104">개요</span><span class="sxs-lookup"><span data-stu-id="cd98c-104">Overview</span></span>
<span data-ttu-id="cd98c-105">Microsoft Azure 미디어 서비스를 사용하면 AES(Advanced Encryption Standard)(128비트 암호화 키 사용) 또는 [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/)으로 보호되는 MPEG-DASH, 부드러운 스트리밍 및 HTTP-Live-Streaming(HLS) 스트림을 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="cd98c-106">또한 AMS를 사용하면 Widevine DRM으로 암호화된 DASH 스트림을 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="cd98c-107">PlayReady와 Widevine 모두 일반적인 암호화(ISO/IEC 23001-7 CENC) 사양에 따라 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="cd98c-108">또한 미디어 서비스는 **키/라이선스 배달 서비스** 를 제공하여 클라이언트가 암호화된 콘텐츠를 재생할 수 있는 AES 키 또는 PlayReady/Widevine 라이선스를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="cd98c-109">Media Services에서 자산을 암호화하려는 경우 [여기](media-services-dotnet-create-contentkey.md)서 설명한 대로 암호화 키(**CommonEncryption** 또는 **EnvelopeEncryption**)와 자산을 연결하고, 이 문서에서 설명한 대로 키 인증 정책도 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-109">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="cd98c-110">플레이어가 스트림을 요청하면 미디어 서비스는 지정된 키를 사용하고 AES 또는 DRM 암호화를 사용하여 동적으로 사용자의 콘텐츠를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="cd98c-111">스트림을 해독하기 위해 플레이어는 키 배달 서비스에서 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-111">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="cd98c-112">사용자에게 키를 얻을 수 있는 권한이 있는지 여부를 결정하기 위해 서비스는 키에 지정된 권한 부여 정책을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-112">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="cd98c-113">미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="cd98c-114">콘텐츠 키 권한 부여 정책에는 **열기** 또는 **토큰** 제한과 같은 하나 이상의 권한 부여 제한이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-114">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="cd98c-115">토큰 제한 정책은 보안 토큰 서비스(STS)에 의해 발급된 토큰이 수반되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="cd98c-116">Media Services에서는 **단순 웹 토큰**([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 형식 및 **JSON Web Token**([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) 형식의 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-116">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="cd98c-117">미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="cd98c-118">사용자 지정 STS를 만들거나 Microsoft Azure ACS를 활용하여 토큰을 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-118">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="cd98c-119">지정된 키로 서명된 토큰을 만들고 토큰 제한 구성에서 지정한 클레임을 발급하려면 반드시 STS를 구성해야 합니다(이 문서에서 설명).</span><span class="sxs-lookup"><span data-stu-id="cd98c-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="cd98c-120">토큰이 유효하고 해당 토큰의 클레임이 콘텐츠 키에 대해 구성된 클레임과 일치하는 경우 미디어 서비스 키 배달 서비스는 암호화 키를 클라이언트에게 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-120">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="cd98c-121">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd98c-121">For more information, see</span></span>

[<span data-ttu-id="cd98c-122">JWT 토큰 인증</span><span class="sxs-lookup"><span data-stu-id="cd98c-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="cd98c-123">[Azure Active Directory와 Azure 미디어 서비스 OWIN MVC 기반 앱을 Azure Active Directory와 통합하고 JWT 클레임을 기반으로 하는 콘텐츠 키 배달을 제한합니다](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="cd98c-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="cd98c-124">[Azure ACS를 사용하여 토큰을 발급합니다](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="cd98c-124">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="cd98c-125">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-125">Some considerations apply:</span></span>
* <span data-ttu-id="cd98c-126">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-126">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="cd98c-127">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 스트리밍 끝점이 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-127">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="cd98c-128">사용자의 자산은 적응 비트 전송률 MP4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="cd98c-129">자세한 내용은 [자산 인코딩](media-services-encode-asset.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd98c-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="cd98c-130">**AssetCreationOptions.StorageEncrypted** 옵션을 사용하여 자산을 업로드하고 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="cd98c-131">동일한 정책 구성이 필요한 여러 콘텐츠 키를 사용하려는 경우 단일 인증 정책을 만들고 여러 콘텐츠 키와 함께 다시 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-131">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="cd98c-132">키 배달 서비스는 ContentKeyAuthorizationPolicy 및 관련 개체(정책 옵션 및 제한 사항)를 15분 동안 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-132">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="cd98c-133">ContentKeyAuthorizationPolicy를 만들고 "Token" 제한을 사용하도록 지정 및 테스트하고 정책의 제한을 "개방"으로 업데이트 하는 경우, 해당 정책이 "개방" 버전으로 전환하는 데 약 15분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-133">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="cd98c-134">자산 배달 정책을 추가하거나 업데이트하는 경우 기존 로케이터(있는 경우)를 삭제하고 새 로케이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="cd98c-135">현재 점진적 다운로드를 암호화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="cd98c-136">AES 128 동적 암호화.</span><span class="sxs-lookup"><span data-stu-id="cd98c-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="cd98c-137">열기 제한</span><span class="sxs-lookup"><span data-stu-id="cd98c-137">Open Restriction</span></span>
<span data-ttu-id="cd98c-138">열기 제한은 시스템이 키를 요청하는 사람에게 키를 제공하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-138">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="cd98c-139">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="cd98c-140">다음 예제에서는 열기 권한 부여 정책을 만들고 콘텐츠 키에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-140">The following example creates an open authorization policy and adds it to the content key.</span></span>

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


### <a name="token-restriction"></a><span data-ttu-id="cd98c-141">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="cd98c-141">Token Restriction</span></span>
<span data-ttu-id="cd98c-142">이 섹션에서는 콘텐츠 키 인증 정책을 만들고 콘텐츠 키와 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-142">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="cd98c-143">인증 정책은 사용자가 키를 받도록 인증받는지 여부를 결정하기 위해 어떤 인증 요구 사항이 충족돼야 하는지 설명합니다(예: “확인 키”목록은 토큰 서명에 사용된 키를 포함).</span><span class="sxs-lookup"><span data-stu-id="cd98c-143">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="cd98c-144">토큰 제한 옵션을 구성하려면 XML을 사용하여 토큰의 권한 부여 요구 사항을 설명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-144">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="cd98c-145">토큰 제한 구성 XML은 다음 XML 스키마를 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-145">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="cd98c-146"><a id="schema"></a>토큰 제한 스키마</span><span class="sxs-lookup"><span data-stu-id="cd98c-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="cd98c-147">**토큰** 제한 정책을 구성할 때는 기본** 확인 키**, **issuer** 및 **audience** 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-147">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="cd98c-148">**기본 확인 키**는 토큰 서명 시 사용된 키를 포함하며, **issuer**는 토큰을 발급한 보안 토큰 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-148">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="cd98c-149">**대상**(때로는 **범위**라고도 함)은 토큰의 의도 또는 토큰에서 접근을 인증하는 대상 리소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-149">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="cd98c-150">미디어 서비스 키 배달 서비스는 이러한 토큰의 값이 템플릿 파일에 있는 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="cd98c-151">**.NET용 Media Services SDK**를 사용할 때 **TokenRestrictionTemplate** 클래스를 사용하여 제한 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-151">When using **Media Services SDK for .NET**, you can use the **TokenRestrictionTemplate** class to generate the restriction token.</span></span>
<span data-ttu-id="cd98c-152">다음 예제에서는 토큰 제한으로 인증 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-152">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="cd98c-153">이 예제에서는 서명 키(VerificationKey), 토큰 발급자 및 필요한 클레임을 포함하는 토큰을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-153">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

#### <span data-ttu-id="cd98c-154"><a id="test"></a>테스트 토큰</span><span class="sxs-lookup"><span data-stu-id="cd98c-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="cd98c-155">키 권한 부여 정책에 사용된 토큰 제한에 따라 테스트 토큰을 가져오려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd98c-155">To get a test token based on the token restriction that was used for the key authorization policy, do the following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="cd98c-156">PlayReady 동적 암호화</span><span class="sxs-lookup"><span data-stu-id="cd98c-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="cd98c-157">Media Services를 사용하면 사용자가 보호된 콘텐츠를 재생하려고 할 때 PlayReady DRM 런타임이 적용하도록 하려는 권한 및 제한을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-157">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="cd98c-158">PlayReady로 콘텐츠를 보호하려는 경우 권한 부여 정책에서 지정해야 하는 항목 중 하나는 [PlayReady 라이선스 템플릿](media-services-playready-license-template-overview.md)을 정의하는 XML 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-158">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="cd98c-159">.NET용 Media Services SDK에서 **PlayReadyLicenseResponseTemplate** 및 **PlayReadyLicenseTemplate** 클래스는 PlayReady 라이선스 템플릿을 정의하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-159">In Media Services SDK for .NET, the **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define the PlayReady License Template.</span></span>

<span data-ttu-id="cd98c-160">[이 항목](media-services-protect-with-drm.md)에서는 **PlayReady** 및 **Widevine**으로 콘텐츠를 암호화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-160">[This topic](media-services-protect-with-drm.md) shows how to encrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="cd98c-161">열기 제한</span><span class="sxs-lookup"><span data-stu-id="cd98c-161">Open Restriction</span></span>
<span data-ttu-id="cd98c-162">열기 제한은 시스템이 키를 요청하는 사람에게 키를 제공하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-162">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="cd98c-163">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="cd98c-164">다음 예제에서는 열기 권한 부여 정책을 만들고 콘텐츠 키에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-164">The following example creates an open authorization policy and adds it to the content key.</span></span>

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

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="cd98c-165">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="cd98c-165">Token Restriction</span></span>
<span data-ttu-id="cd98c-166">토큰 제한 옵션을 구성하려면 XML을 사용하여 토큰의 권한 부여 요구 사항을 설명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-166">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="cd98c-167">토큰 제한 구성 XML은 [이](#schema) 섹션에 표시된 XML 스키마를 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-167">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

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

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key
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
        // The following code configures PlayReady License Template using .NET classes
        // and returns the XML string.

        //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user. 
        //It contains a field for a custom data string between the license server and the application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // to be returned to the end users. 
        //It contains the data on the content key in the license and any rights or restrictions to be 
        //enforced by the PlayReady DRM runtime when using the content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether the license is persistent (saved in persistent storage on the client) 
        //or non-persistent (only held in memory while the player is using the license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use the license or not.  
        // If true, the MinimumSecurityLevel property of the license
        // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
        // It grants the user the ability to playback the content subject to the zero or more restrictions 
        // configured in the license and on the PlayRight itself (for playback specific policy). 
        // Much of the policy on the PlayRight has to do with output restrictions 
        // which control the types of outputs that the content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
        //then the DRM runtime will only allow the video to be displayed over digital outputs 
        //(analog video outputs won’t be allowed to pass the content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience. 
        // If the output protections are configured too restrictive, 
        // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="cd98c-168">키 권한 부여 정책에 사용된 토큰 제한에 따라 테스트 토큰을 가져오려면 [이](#test) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd98c-168">To get a test token based on the token restriction that was used for the key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="cd98c-169"><a id="types"></a>ContentKeyAuthorizationPolicy를 정의할 때 사용되는 형식</span><span class="sxs-lookup"><span data-stu-id="cd98c-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="cd98c-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="cd98c-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="cd98c-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="cd98c-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="cd98c-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="cd98c-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="cd98c-173">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="cd98c-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cd98c-174">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="cd98c-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="cd98c-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd98c-175">Next step</span></span>
<span data-ttu-id="cd98c-176">콘텐츠 키의 권한 부여 정책을 구성했으므로 [자산 배포 정책 구성 방법](media-services-dotnet-configure-asset-delivery-policy.md) 항목으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cd98c-176">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

