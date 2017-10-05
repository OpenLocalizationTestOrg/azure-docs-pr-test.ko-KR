---
title: "Axinom을 사용하여 Azure Media Services에 Widevine 라이선스 배달 | Microsoft 문서"
description: "이 문서에서는 Azure 미디어 서비스(AMS)를 사용하여 PlayReady와 Widevine DRM이 모두 있는 AMS에서 동적으로 암호화된 스트림을 전달하는 방법을 설명합니다. PlayReady 라이선스는 미디어 서비스 PlayReady 라이선스 서버에서 제공되며 Widevine 라이선스는 Axinom 라이선스 서버에서 제공됩니다."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 64e8d4a88ea78e0de065e5a2c12dba4885e08bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-axinom-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="c8326-104">Axinom을 사용하여 Azure 미디어 서비스에 Widevine 라이선스 제공</span><span class="sxs-lookup"><span data-stu-id="c8326-104">Using Axinom to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8326-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="c8326-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="c8326-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="c8326-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c8326-107">개요</span><span class="sxs-lookup"><span data-stu-id="c8326-107">Overview</span></span>
<span data-ttu-id="c8326-108">Azure 미디어 서비스(AMS)에 Google Widevine 동적 보호가 추가되었습니다(자세한 내용은 [Mingfei의 블로그](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) 참조).</span><span class="sxs-lookup"><span data-stu-id="c8326-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="c8326-109">또한 Azure 미디어 플레이어(AMP)에도 Widevine 지원이 추가되었습니다(자세한 내용은 [AMP 문서](http://amp.azure.net/libs/amp/latest/docs/) 참조).</span><span class="sxs-lookup"><span data-stu-id="c8326-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="c8326-110">이는 MSE 및 EME가 포함된 현대식 브라우저에 대한 다중 원시 DRM(PlayReady 및 Widevine)를 가진 CENC로 보호되는 DASH 콘텐츠 합리화의 주요 성과입니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="c8326-111">미디어 서비스 .NET SDK 버전 3.5.2부터는 미디어 서비스를 사용하여 Widevine 라이선스 템플릿을 구성하고 Widevine 라이선스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-111">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="c8326-112">또한 다음 AMS 파트너를 사용하여 Widevine 라이선스를 배달할 수 있습니다. [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="c8326-112">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="c8326-113">이 문서에서는 Axinom에서 관리하는 Widevine 라이선스 서버를 통합하고 테스트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-113">This article describes how to integrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="c8326-114">구체적으로 다음 사항을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="c8326-115">해당 라이선스 취득 URL이 포함된 다중-DRM(PlayReady 및 Widevine)을 사용하여 동적 일반 암호화 구성;</span><span class="sxs-lookup"><span data-stu-id="c8326-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="c8326-116">라이선스 서버 요구 사항을 충족하기 위해 JWT 토큰 생성;</span><span class="sxs-lookup"><span data-stu-id="c8326-116">Generating a JWT token in order to meet the license server requirements;</span></span>
* <span data-ttu-id="c8326-117">JWT 토큰 인증으로 라이선스 취득을 처리하는 Azure 미디어 플레이어 앱 개발;</span><span class="sxs-lookup"><span data-stu-id="c8326-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="c8326-118">전체 시스템 및 콘텐츠 키, 키 ID, 키 시드, JTW 토큰 및 해당 클레임의 흐름을 다음 다이어그램에 의해 가장 잘 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-118">The complete system and the flow of content key, key ID, key seed, JTW token and its claims can be best described by the following diagram.</span></span>

![대시 및 CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="c8326-120">콘텐츠 보호</span><span class="sxs-lookup"><span data-stu-id="c8326-120">Content Protection</span></span>
<span data-ttu-id="c8326-121">동적 보호 및 키 배달 정책을 구성하려면 Mingfei의 블로그: [Azure 미디어 서비스로 Widevine 패키징을 구성하는 방법](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8326-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How to configure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="c8326-122">다음 두 가지가 모두 있는 DASH 스트리밍용 다중 DRM으로 동적 CENC 보호를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of the following:</span></span>

1. <span data-ttu-id="c8326-123">토큰 인증 제한이 포함될 수 있는 MS Edge 및 IE11에 대한 PlayReady 보호.</span><span class="sxs-lookup"><span data-stu-id="c8326-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="c8326-124">토큰 제한 정책은 Azure Active Directory 등과 같은 보안 토큰 서비스(STS)에 의해 발급된 토큰이 수반되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-124">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="c8326-125">Chrome에 대한 Widevine 보호의 경우 다른 STS가 발급한 토큰을 이용한 토큰 인증이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="c8326-126">Azure Active Directory를 Axinom의 Widevine 라이선스 서버에 대한 STS로 사용할 수 없는 이유는 [JWT 토큰 생성](media-services-axinom-integration.md#jwt-token-generation) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8326-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="c8326-127">고려 사항</span><span class="sxs-lookup"><span data-stu-id="c8326-127">Considerations</span></span>
1. <span data-ttu-id="c8326-128">Axinom 지정 키 시드(8888000000000000000000000000000000000000) 및 사용자가 생성하거나 선택한 키 ID를 사용하여 키 배달 서비스를 구성하기 위한 콘텐츠 키를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-128">You must use the Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID to generate the content key for configuring key delivery service.</span></span> <span data-ttu-id="c8326-129">Axinom 라이선스 서버는 테스트와 생산에 모두 유효한 동일한 키 시드를 기반으로 콘텐츠 키를 포함하고 있는 모든 라이선스를 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-129">Axinom license server will issue all licenses containing content keys based on the same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="c8326-130">테스트를 위한 Widevine 라이선스 취득 URL: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="c8326-130">The Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="c8326-131">HTTP 및 HTTS 모두 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="c8326-132">Azure 미디어 플레이어 준비</span><span class="sxs-lookup"><span data-stu-id="c8326-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="c8326-133">AMP v1.4.0은 PlayReady와 Widevine DRM 둘 다를 사용하여 동적으로 패키징된 AMS 콘텐츠의 재생을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="c8326-134">Widevine 라이선스 서브에 토큰 인증이 필요하지 않은 경우 Widevine에서 보호하는 DASH 콘텐츠를 테스트하기 위해 추가로 수행해야 하는 일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-134">If Widevine license server does not require token authentication, there is nothing additional you need to do to test a DASH content protected by Widevine.</span></span> <span data-ttu-id="c8326-135">예를 들어 AMP 팀에는 PlayReady를 지원하는 Edge 및 IE11과 Widevine을 지원하는 Chrome에서 작동 모습을 볼 수 있는 간단한 [샘플](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-135">For an example, the AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="c8326-136">Axinom 제공한 Widevine 라이선스 서버에는 JWT 토큰 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-136">The Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="c8326-137">HTTP 헤더 “X-AxDRM-Message”를 통해 라이선스 요청과 함께 JWT 토큰을 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-137">The JWT token needs to be submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="c8326-138">이 목적을 위해 원본을 설정하기 전에 웹 페이지 호스팅 AMP에서 다음과 같은 javascript를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-138">For this purpose, you need to add the following javascript in the web page hosting AMP before setting the source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="c8326-139">AMP 코드의 나머지 부분은 AMP 문서 [여기](http://amp.azure.net/libs/amp/latest/docs/)에서와 같이 표준 AMP API입니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-139">The rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="c8326-140">참고로 사용자 지정 인증 헤더를 설정하기 위한 위의 javascript는 AMP의 공식적인 장기적 방식이 출시되기 전의 단기적인 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-140">Note that the above javascript for setting custom authorization header is still a short term approach before the official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="c8326-141">JWT 토큰 생성</span><span class="sxs-lookup"><span data-stu-id="c8326-141">JWT Token Generation</span></span>
<span data-ttu-id="c8326-142">테스트용 Axinom Widevine 라이선스 서버에는 JWT 토큰 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="c8326-143">또한 JWT 토큰의 클레임 중 하나는 기본 데이터 형식이 아닌 복잡한 개체 유형으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-143">In addition, one of the claims in the JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="c8326-144">아쉽게도 Azure AD는 기본 형식의 JWT 토큰만 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="c8326-145">마찬가지로,.NET Framework API(System.IdentityModel.Tokens.SecurityTokenHandler 및 JwtPayload)를 사용하면 복잡한 개체 유형을 클레임으로 입력하는 것만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you to input complex object type as claims.</span></span> <span data-ttu-id="c8326-146">그러나 클레임은 여전히 문자열로 직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-146">However, the claims are still serialized as string.</span></span> <span data-ttu-id="c8326-147">그러므로 Widevine 라이선스 요청에 대한 JWT 토큰을 생성하는 경우 둘 중 하나를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-147">Therefore we cannot use any of the two for generating the JWT token for Widevine license request.</span></span>

<span data-ttu-id="c8326-148">John Sheehan의 [JWT Nuget 패키지](https://www.nuget.org/packages/JWT) 는 요구 사항에 부합하므로 이 Nuget 패키지를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets the needs so we are going to use this Nuget package.</span></span>

<span data-ttu-id="c8326-149">다음은 테스트를 위해 Axinom Widevine 라이선스 서버에서 요구한 대로 필요한 클레임을 사용하여 JWT 토큰을 생성하기 위한 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-149">Below is the code for generating JWT token with the needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string to byte[] Note: Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string to byte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "The binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="c8326-150">Axinom Widevine 라이선스 서버</span><span class="sxs-lookup"><span data-stu-id="c8326-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="c8326-151">고려 사항</span><span class="sxs-lookup"><span data-stu-id="c8326-151">Considerations</span></span>
1. <span data-ttu-id="c8326-152">AMS PlayReady 라이선스 배달 서비스의 경우 인증 토큰 앞에 “Bearer=”가 필요하지만, Axinom Widevine 라이선스 서버는 이를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="c8326-153">Axinom 통신 키는 서명 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-153">The Axinom communication key is used as signing key.</span></span> <span data-ttu-id="c8326-154">참고로 키는 16진 문자열이지만 인코딩할 때에는 문자열이 아닌 일련의 바이트로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-154">Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="c8326-155">ConvertHexStringToByteArray 메서드를 사용하면 이 목적이 달성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-155">This is achieved by the method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="c8326-156">키 ID 검색</span><span class="sxs-lookup"><span data-stu-id="c8326-156">Retrieving Key ID</span></span>
<span data-ttu-id="c8326-157">JWT 토큰을 생성하기 위한 코드에서 키 ID가 필요하다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-157">You may have noticed that in the code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="c8326-158">JWT 토큰은 AMP 플레이어를 로드하기 전에 준비되어 있어야 하므로 JWT 토큰을 생성하려면 키 ID를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-158">Since the JWT token needs to be ready before loading AMP player, key ID needs to be retrieved in order to generate JWT token.</span></span>

<span data-ttu-id="c8326-159">물론 키 ID를 유지하는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-159">Of course there are multiple ways to get hold of key ID.</span></span> <span data-ttu-id="c8326-160">예를 들어 키 ID를 콘텐츠 메타데이터와 함께 데이터베이스에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="c8326-161">또는 DASH MPD(미디어 프레젠테이션 설명) 파일에서 키 ID를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="c8326-162">아래 코드는 후자의 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-162">The code below is for the latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="c8326-163">요약</span><span class="sxs-lookup"><span data-stu-id="c8326-163">Summary</span></span>
<span data-ttu-id="c8326-164">최근 Azure 미디어 서비스 콘텐츠 보호 및 Azure 미디어 플레이어에 모두 Widevine 지원이 추가됨에 따라, AMS의 PlayReady 라이선스 서비스 및 다음과 같은 현대적인 브라우저에 대한 Axinom의 Widevine 라이선스 서버를 사용하여 DASH + 다중 원시 DRM(PlayReady + Widevine)의 스트리밍을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able to implement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for the following modern browsers:</span></span>

* <span data-ttu-id="c8326-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="c8326-165">Chrome</span></span>
* <span data-ttu-id="c8326-166">Windows 10용 Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="c8326-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="c8326-167">Windows 8.1 및 Windows 10용 IE 11</span><span class="sxs-lookup"><span data-stu-id="c8326-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="c8326-168">Mac(iOS 제외)용 Firefox(데스크톱) 및 Safari도 Silverlight 및 Azure 미디어 플레이어와 같은 URL을 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and the same URL with Azure Media Player</span></span>

<span data-ttu-id="c8326-169">Axinom Widevine 라이선스 서버를 활용하는 미니 솔루션에는 다음과 같은 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-169">The following parameters are required in the mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="c8326-170">키 ID를 제외하고 매개 변수의 나머지 부분은 Widevine 서버 설정에 따라 Axinom에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-170">Except for key ID, the rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="c8326-171">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c8326-171">Parameter</span></span> | <span data-ttu-id="c8326-172">사용 방법</span><span class="sxs-lookup"><span data-stu-id="c8326-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="c8326-173">통신 키 ID</span><span class="sxs-lookup"><span data-stu-id="c8326-173">Communication key ID</span></span> |<span data-ttu-id="c8326-174">JWT 토큰의 클레임 "com_key_id"의 값으로 포함되어야 합니다([이](media-services-axinom-integration.md#jwt-token-generation) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="c8326-174">Must be included as value of the claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c8326-175">통신 키</span><span class="sxs-lookup"><span data-stu-id="c8326-175">Communication key</span></span> |<span data-ttu-id="c8326-176">JWT 토큰의 서명 키로 사용해야 합니다( [이](media-services-axinom-integration.md#jwt-token-generation) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="c8326-176">Must be used as the signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c8326-177">키 시드</span><span class="sxs-lookup"><span data-stu-id="c8326-177">Key seed</span></span> |<span data-ttu-id="c8326-178">지정된 콘텐츠 키 ID로 콘텐츠 키를 생성하는 데 사용해야 합니다([이](media-services-axinom-integration.md#content-protection) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="c8326-178">Must be used to generate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="c8326-179">Widevine 라이선스 획득 URL</span><span class="sxs-lookup"><span data-stu-id="c8326-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="c8326-180">DASH 스트리밍에 대한 자산 배달 정책 구성에 사용해야 합니다([이](media-services-axinom-integration.md#content-protection) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="c8326-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="c8326-181">콘텐츠 키 ID</span><span class="sxs-lookup"><span data-stu-id="c8326-181">Content Key ID</span></span> |<span data-ttu-id="c8326-182">JWT 토큰의 자격 부여 메시지 클레임 값의 일부로 포함되어야 합니다( [이](media-services-axinom-integration.md#jwt-token-generation) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="c8326-182">Must be included as part of the value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="c8326-183">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="c8326-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8326-184">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="c8326-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="c8326-185">승인</span><span class="sxs-lookup"><span data-stu-id="c8326-185">Acknowledgments</span></span>
<span data-ttu-id="c8326-186">이 문서를 만들 때 기여한 Axinom의 Kristjan Jõgi, Mingfei Yan 그리고 Amit Rajput에게 감사를 드립니다.</span><span class="sxs-lookup"><span data-stu-id="c8326-186">We would like to acknowledge the following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

