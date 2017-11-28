---
title: "aaaUse Azure 미디어 서비스 toodeliver DRM 라이선스 또는 AES 키"
description: "이 문서에서는 Azure 미디어 서비스 (AMS) toodeliver PlayReady 및/또는 Widevine 라이선스 및 AES 키를 사용할 수 있지만 rest (인코딩, 암호화, 스트리밍) hello 수행 방법을 설명 온-프레미스 서버를 사용 하 여 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: a81da2973c79e5182ae58aeca7a0f14f3fc7c9ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-services-toodeliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="19a33-103">Azure 미디어 서비스 toodeliver DRM 라이선스 또는 AES 키를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="19a33-103">Use Azure Media Services toodeliver DRM licenses or AES keys</span></span>
<span data-ttu-id="19a33-104">Azure 미디어 서비스 AMS ()를 사용 하면 tooingest, 인코딩, 콘텐츠 보호를 추가 및 콘텐츠를 스트리밍하려면 (참조 [이](media-services-protect-with-drm.md) 내용은 문서의).</span><span class="sxs-lookup"><span data-stu-id="19a33-104">Azure Media Services (AMS) enables you tooingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="19a33-105">그러나만 toouse AMS toodeliver 라이선스 및/또는 키를 선택 하 고 수행 인코딩, 암호화 및 온-프레미스 서버를 사용 하 여 고객에 게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-105">However, there are customers who only want toouse AMS toodeliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="19a33-106">이 문서에서는 AMS toodeliver PlayReady 및/또는 Widevine 라이선스를 사용할 수 있지만 온-프레미스 서버와 함께 rest hello 수행 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-106">This article describes how you can use AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="19a33-107">개요</span><span class="sxs-lookup"><span data-stu-id="19a33-107">Overview</span></span>
<span data-ttu-id="19a33-108">Media Services는 PlayReady와 Widevine DRM 라이선스 및 AES-128 키를 제공하는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="19a33-109">미디어 서비스 hello 권한을 구성할 수 있는 Api도 제공 하 고 보호 된 콘텐츠 hello DRM hello DRM 런타임은 tooenforce 때 사용자에 대 한 원하는 제한을 다시 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-109">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello DRM runtime tooenforce when a user plays back hello DRM protected content.</span></span> <span data-ttu-id="19a33-110">사용자 요청 hello 보호 된 콘텐츠를 hello 플레이어 응용 프로그램 라이선스 hello AMS 라이선스 서비스에서 요청.</span><span class="sxs-lookup"><span data-stu-id="19a33-110">When a user requests hello protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="19a33-111">(이 권한이 부여 된) 경우 hello AMS 라이선스 서비스는 hello 라이선스 toohello 플레이어를 발행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-111">hello AMS license service will issue hello license toohello player (if it is authorized).</span></span> <span data-ttu-id="19a33-112">hello PlayReady 및 Widevine 라이선스 hello 클라이언트 플레이어 toodecrypt 및 스트림 hello 콘텐츠에서 사용할 수 있는 hello 암호 해독 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-112">hello PlayReady and Widevine licenses contain hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="19a33-113">미디어 서비스는 라이선스 또는 키를 요청하는 사용자에 권한을 부여하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="19a33-114">Hello 콘텐츠 키 권한 부여 정책 구성 및 hello 정책에는 하나 이상의 제한이 있을 수: 열거나 토큰 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-114">You configure hello content key's authorization policy and hello policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="19a33-115">보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="19a33-116">미디어 서비스는 hello 단순 웹 토큰 (SWT) 형식 및 JSON 웹 토큰 (JWT) 형식 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-116">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="19a33-117">hello 다음 보여 주는 다이어그램 주요 단계는 hello tootake toouse AMS toodeliver PlayReady 및/또는 Widevine 라이선스 필요 하지만 온-프레미스 서버와 함께 rest hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-117">hello following diagram shows hello main steps you need tootake toouse AMS toodeliver PlayReady and/or Widevine licenses but do hello rest with your on-premises servers.</span></span>

![PlayReady로 보호](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="19a33-119">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="19a33-119">Download sample</span></span>
<span data-ttu-id="19a33-120">이 문서에서 설명 하는 hello 샘플을 다운로드할 수 [여기](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-120">You can download hello sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="19a33-121">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="19a33-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="19a33-122">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-122">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="19a33-123">추가 요소를 너무 다음 hello**appSettings** app.config 파일에 정의 된:</span><span class="sxs-lookup"><span data-stu-id="19a33-123">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="19a33-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="19a33-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="19a33-125">.NET 코드 예제</span><span class="sxs-lookup"><span data-stu-id="19a33-125">.NET code example</span></span>

<span data-ttu-id="19a33-126">다음 코드 예제는 hello 방법을 보여 줍니다 toocreate 공통 콘텐츠 키 Widevine 또는 PlayReady 라이선스 취득 Url을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-126">hello following code example shows how toocreate a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="19a33-127">Tooget 필요한 AMS에서 정보를 다음 hello 하 고 온-프레미스 서버 구성: **콘텐츠 키**, **키 id**, **라이선스 취득 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-127">You need tooget hello following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="19a33-128">온-프레미스 서버를 구성하면 자체 스트리밍 서버에서 스트림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="19a33-129">Hello 암호화 스트림 포인트 tooAMS 라이선스 서버를 이후 플레이어 AMS에서 라이선스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-129">Since hello encrypted stream points tooAMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="19a33-130">토큰 인증을 선택 하면 hello AMS 라이선스 서버는 HTTPS를 통해 전송 된 hello 토큰 유효성을 검사 하 고 (유효한 경우) hello 라이선스 백 tooyour 플레이어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-130">If you choose token authentication, hello AMS license server will validate hello token you sent through HTTPS and (if valid) will deliver hello license back tooyour player.</span></span> <span data-ttu-id="19a33-131">(hello 코드 예제에서는 방법을 보여 줍니다 toocreate 공통 콘텐츠 키 Widevine 또는 PlayReady 라이선스 취득 Url을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19a33-131">(hello code example only shows how toocreate a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="19a33-132">Aes-128 toodelivery 키 원하는 toocreate 봉투 콘텐츠 키를 해야 키 취득 URL을 가져올 및 [이](media-services-protect-with-aes128.md) 방법을 보여 줍니다 문서 toodo 것).</span><span class="sxs-lookup"><span data-stu-id="19a33-132">If you want toodelivery AES-128 keys, you need toocreate an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how toodo it).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static readonly Uri _sampleIssuer =
                new Uri(ConfigurationManager.AppSettings["Issuer"]);
            private static readonly Uri _sampleAudience =
                new Uri(ConfigurationManager.AppSettings["Audience"]);

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out hello key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Open",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                            Requirements = null
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.Widevine,
                        restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Token Authorization Policy",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                            Requirements = tokenTemplateString,
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.Widevine,
                            restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with token restrictions").
                            Result;

                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

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

                //hello PlayReadyLicenseResponseTemplate class represents hello template 
                //for hello response sent back toohello end user. 
                //It contains a field for a custom data string between hello license server 
                //and hello application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // hello PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // toobe returned toohello end users. 
                // It contains hello data on hello content key in hello license 
                // and any rights or restrictions toobe 
                // enforced by hello PlayReady DRM runtime when using hello content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether hello license is persistent 
                // (saved in persistent storage on hello client) 
                // or non-persistent (only held in memory while hello player is using hello license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use hello license or not.  
                // If true, hello MinimumSecurityLevel property of hello license
                // is set too150.  If false (hello default), 
                // hello MinimumSecurityLevel property of hello license is set too2000.
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

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect hello consumer experience. 
                // If hello output protections are configured too restrictive, 
                // hello content might be unplayable on some clients. 
                // For more information, see hello PlayReady Compliance Rules document.

                // For example:
                //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }


            private static string ConfigureWidevineLicenseTemplate()
            {
                var template = new WidevineMessage
                {
                    allowed_track_types = AllowedTrackTypes.SD_HD,
                    content_key_specs = new[]
                    {
                            new ContentKeySpecs
                            {
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                                security_level = 1,
                                track_type = "SD"
                            }
                        },
                    policy_overrides = new
                    {
                        can_play = true,
                        can_persist = true,
                        can_renew = false
                    }
                };

                string configuration = JsonConvert.SerializeObject(template);
                return configuration;
            }


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="19a33-133">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="19a33-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="19a33-134">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="19a33-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="19a33-135">참고 항목</span><span class="sxs-lookup"><span data-stu-id="19a33-135">See also</span></span>
[<span data-ttu-id="19a33-136">PlayReady 및/또는 Widevine 동적 일반 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="19a33-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="19a33-137">AES-128 동적 암호화 및 키 전달 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="19a33-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="19a33-138">파트너 toodeliver Widevine 라이선스 tooAzure 미디어 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="19a33-138">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>](media-services-licenses-partner-integration.md)

