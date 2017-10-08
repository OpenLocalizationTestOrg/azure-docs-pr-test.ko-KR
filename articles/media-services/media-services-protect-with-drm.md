---
title: "aaaUsing PlayReady 및/또는 Widevine 동적 일반 암호화 | Microsoft Docs"
description: "Microsoft Azure 미디어 서비스에서는 있습니다 toodeliver MPEG DASH, 부드러운 스트리밍 및 Http 라이브 스트리밍 (HLS) 스트림을 Microsoft PlayReady DRM으로 보호 합니다. 또한, toodelivery를 Widevine DRM을 사용 하 여 암호화 된 DASH를 있습니다. 이 항목에서는 toodynamically Widevine DRM 및 PlayReady로 암호화 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>PlayReady 및/또는 Widevine 동적 일반 암호화 사용

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Microsoft Azure 미디어 서비스 사용 하면 toodeliver MPEG DASH, 부드러운 스트리밍 및 HTTP 라이브 스트리밍 (HLS) 스트림에서 보호 된 [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/)합니다. 또한, DRM Widevine 라이선스를 갖고 있는 toodeliver 암호화 된 DASH 스트림을 있습니다. PlayReady 및 Widevine 모두 hello 일반 암호화 (ISO/IEC 23001-7 CENC) 사양 당 암호화 됩니다. 사용할 수 있습니다 [AMS.NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (3.5.1 hello 버전부터 시작) 또는 REST API tooconfigure 프로그램 AssetDeliveryConfiguration toouse Widevine 합니다.

미디어 서비스는 PlayReady와 Widevine DRM 라이선스를 제공하는 서비스를 제공합니다. 미디어 서비스 hello 권한을 구성할 수 있는 Api도 제공 하 고 hello PlayReady 또는 Widevine DRM 런타임은 tooenforce 때 사용자에 대 한 원하는 제한을 보호 된 콘텐츠를 재생 합니다. 사용자 DRM으로 보호 된 콘텐츠를 요청 하는 경우 hello 플레이어 응용 프로그램 hello AMS 라이선스 서비스에서 라이선스를 요청 합니다. hello AMS 라이선스 서비스에서 권한 부여 라이선스 toohello 플레이어를 발생 합니다. PlayReady 또는 Widevine 라이선스 hello 클라이언트 플레이어 toodecrypt 및 스트림 hello 콘텐츠 사용할 수 있는 hello 암호 해독 키를 포함 합니다.

Widevine 라이선스를 배달 AMS 파트너 toohelp 다음 hello을 사용할 수 있습니다: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/)합니다. 자세한 내용은 [Axinom](media-services-axinom-integration.md) 및 [castLabs](media-services-castlabs-integration.md)를 이용한 통합을 참조하세요.

미디어 서비스는 키를 요청 하는 사용자에 권한을 부여하는 여러 방법을 지원합니다. hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: 열거나 토큰 제한 합니다. 보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다. 미디어 서비스는 hello에 토큰을 지원 [단순 웹 토큰](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) 형식 및 [JSON 웹 토큰](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) 형식입니다. 자세한 내용은 구성 hello 콘텐츠 키 권한 부여 정책을 참조 하십시오.

tootake 이점은 다중 비트 전송률 MP4 파일 또는 다중 비트 전송률 부드러운 스트리밍 원본 파일 집합이 포함 된 자산 toohave 동적 암호화 해야 합니다. 또한 해야 tooconfigure hello 배달 정책 (이 항목의 뒷부분에 설명) hello 자산에 대 한 합니다. 그런 다음 형식에 따라 hello hello 스트리밍 URL에에서 지정 된, 주문형 스트리밍 서버 hello 됩니다 되도록 해당 hello 스트림의 선택한 hello 프로토콜에서 제공 됩니다. 결과적으로, toostore 하기만 하면 및 단일 저장소 형식 및 미디어 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서 각 요청에 따라 hello 적절 한 HTTP 응답을 제공 합니다.

이 항목에는 유용한 toodevelopers PlayReady Widevine 등 여러 DRMs로 보호 된 미디어를 전달 하는 응용 프로그램에서 작동 하는 것입니다. hello 항목에서는 권한 있는 클라이언트만 PlayReady 또는 Widevine 라이선스를 받을 수 있도록 권한 부여 정책 사용 하 여 PlayReady 라이선스 배달 서비스 tooconfigure hello 하는 방법을 보여 줍니다. 또한 표시 방법을 PlayReady 또는 대시를 통해 Widevine DRM을 사용 하 여 toouse 동적 암호화 암호화 합니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 

## <a name="download-sample"></a>샘플 다운로드
이 문서에서 설명 하는 hello 샘플을 다운로드할 수 [여기](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm)합니다.

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>동적 일반 암호화 및 DRM 라이선스 전달 서비스 구성

hello 다음은 hello 미디어 서비스 라이선스 배달 서비스를 사용 하 고 또한 동적 암호화를 사용 하 여 PlayReady로 자산을 보호 하는 경우 tooperform 해야 하는 일반적인 단계입니다.

1. 자산 만들기 hello 자산 파일 업로드 합니다.
2. Hello 자산 포함 hello 파일 toohello 적응 비트 전송률을 MP4 집합으로 인코딩하십시오.
3. 콘텐츠 키를 만들고 hello 인코딩된 자산에 연결 합니다. 미디어 서비스 콘텐츠 키 hello hello 자산의 암호화 키를 포함합니다.
4. Hello 콘텐츠 키 권한 부여 정책을 구성 합니다. hello 콘텐츠 키 인증 정책은 구성 하 고 hello 클라이언트에서 콘텐츠 키 toobe 배달된 toohello 클라이언트 hello 하려면 충족 해야 합니다.

    Toospecify hello 다음 hello 콘텐츠 키 권한 부여 정책을 만들 때 필요한: 배달 메서드 (PlayReady 또는 Widevine) 제한 사항 (열기 또는 토큰) 및 정보 hello 키 배달 방법을 정의 하는 특정 toohello 키 배달 유형 toohello 클라이언트 ([PlayReady](media-services-playready-license-template-overview.md) 또는 [Widevine](media-services-widevine-license-template-overview.md) 라이선스 템플릿을).

5. 자산에 대 한 hello 배달 정책을 구성 합니다. hello 배달 정책 구성에: 배달 프로토콜 (예를 들어, MPEG DASH, HLS, 부드러운 스트리밍 또는 모두), hello 동적 암호화 (예를 들어 일반 암호화), PlayReady 또는 Widevine 라이선스 취득 URL 형식입니다.

    Hello에 서로 다른 정책 tooeach 프로토콜을 적용할 수 동일한 자산입니다. 예를 들어 PlayReady 암호화 tooSmooth/DASH 및 AES 봉투 (envelope) tooHLS 적용할 수 있습니다. 배달 정책에 정의 되어 있지 않은 모든 프로토콜 (예를 들어 추가한만 hello 프로토콜로 HLS를 지정 하는 단일 정책을) 스트리밍에서 차단 됩니다. hello 예외 toothis는 없는 자산 배달 정책을 정의 해야 합니다. 그런 다음 모든 프로토콜이 일반 hello에 허용 됩니다.

6. 순서 tooget 스트리밍 URL에서에서 OnDemand 로케이터를 만듭니다.

Hello 항목의 hello 끝에는 전체.NET 예제를 찾을 수 있습니다.

다음 이미지는 hello 위에서 설명한 hello 워크플로를 보여 줍니다. 여기서 hello 토큰 인증을 위해 사용 됩니다.

![PlayReady로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

이 항목의 나머지 부분 hello에 대 한 세부 정보, 코드 예제 및 tooachieve 위에서 설명한 작업 hello 하는 방법을 보여 주는 링크 tootopics 제공 합니다.

## <a name="current-limitations"></a>현재 제한 사항
를 추가 하거나 자산 배달 정책을 업데이트 하는 경우 (있는 경우) 연결 된 hello 로케이터를 삭제 하 고 새 로케이터를 만듭니다 해야 합니다.

Azure 미디어 서비스를 사용하여 Widevine를 암호화할 때 제한 사항은 현재 여러 콘텐츠 키가 지원되지 않는다는 점입니다.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>자산 만들기 및 hello 자산에 파일 업로드
순서 toomanage 인코딩 및 스트리밍 비디오, Microsoft Azure 미디어 서비스에 콘텐츠를 먼저 업로드 해야 합니다. 를 업로드 한 후 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.

자세한 내용은 [미디어 서비스 계정에 파일 업로드](media-services-dotnet-upload-files.md)를 참조하세요.

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Hello 자산 포함 hello 파일 toohello 적응 비트 전송률 MP4 세트로 인코딩
동적 암호화 toocreate 다중 비트 전송률 MP4 파일 또는 다중 비트 전송률 부드러운 스트리밍 원본 파일 집합이 포함 된 자산은 하기만 하면 됩니다. 그런 다음 hello hello 매니페스트에 지정 된 형식에 따라 및 요청 조각, 주문형 스트리밍 서버 hello 스트림이 선택한 hello 프로토콜에 수신 하는 방법을 사용 하면 hello 합니다. 결과적으로, toostore 하기만 하면 및 단일 저장소 형식 및 미디어 서비스 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서에서 요청에 따라 hello 적절 한 응답을 제공 합니다. 자세한 내용은 참조 hello [동적 패키징 개요](media-services-dynamic-packaging-overview.md) 항목입니다.

방법에 대 한 지침은 tooencode, 참조 [어떻게 tooencode 미디어 인코더 표준를 사용 하 여 자산](media-services-dotnet-encode-with-media-encoder-standard.md)합니다.

## <a id="create_contentkey"></a>콘텐츠 키를 만들고 hello 인코딩된 자산에 연결
Hello 콘텐츠 키 미디어 서비스 자산 tooencrypt hello 키에 포함 되어 있는 합니다.

자세한 내용은 [콘텐츠 키 만들기](media-services-dotnet-create-contentkey.md)를 참조하세요.

## <a id="configure_key_auth_policy"></a>Hello 콘텐츠 키 권한 부여 정책 구성
미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다. hello 콘텐츠 키 인증 정책은 구성 하 고 hello 키 toobe toohello 클라이언트에 배달 하려면에서 hello 클라이언트 (플레이어)에서 충족 해야 합니다. hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: 열거나 토큰 제한 합니다.

자세한 내용은 [콘텐츠 키 권한 부여 정책 구성](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption)을 참조하세요.

## <a id="configure_asset_delivery_policy"></a>자산 배달 정책 구성
자산에 대 한 hello 배달 정책을 구성 합니다. 자산 배달 정책 구성 hello 있는 일부의 원인에는 다음이 포함 됩니다.

* hello DRM 라이선스 취득 URL입니다.
* hello 자산 배달 프로토콜 (예를 들어, MPEG DASH, HLS, 부드러운 스트리밍 또는 모두)입니다.
* 동적 암호화 (이 경우 일반 암호화)에 hello 형식입니다.

자세한 내용은 [자산 배달 정책 구성 ](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.

## <a id="create_locator"></a>주문형 스트리밍 로케이터 순서 tooget 스트리밍 URL 만들기
스트리밍 URL을 부드러운 스트리밍, DASH 또는 HLS hello로 사용자 tooprovide를 해야 합니다.

> [!NOTE]
> 자산 배달 정책을 추가하거나 업데이트하는 경우 기존 로케이터(있는 경우)를 삭제하고 새 로케이터를 만들어야 합니다.
>
>

Toopublish 자산 및 빌드 스트리밍 URL 참조 하는 방법에 대 한 지침은 [스트리밍 URL을 작성할](media-services-deliver-streaming-content.md)합니다.

## <a name="get-a-test-token"></a>테스트 토큰 가져오기
테스트 토큰 가져오기 hello 키 권한 부여 정책에 사용 된 hello 토큰 제한을 기반 합니다.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


Hello를 사용할 수 있습니다 [AMS 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest 스트림을 합니다.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

1. 개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 
2. 추가 요소를 너무 다음 hello**appSettings** app.config 파일에 정의 된:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>예제

hello 다음 예제에서는.Net 용 Azure 미디어 서비스 SDK에 도입 된 기능-버전 3.5.2 (특히 hello 기능 toodefine는 Widevine 라이선스 템플릿 및 Azure 미디어 서비스에서 Widevine 라이선스를 요청)입니다.

이 섹션에 표시 된 hello 코드도 Program.cs 파일의 hello 코드를 덮어씁니다.

>[!NOTE]
>다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

확인 되었는지 tooupdate 변수 toopoint toofolders 입력된 파일이 있는 위치 합니다.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
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

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
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

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
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


## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[다중 DRM 및 액세스 제어가 포함된 CENC](media-services-cenc-with-multidrm-access-control.md)

[AMS로 Widevine 패키징 구성](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Azure 미디어 서비스에서 Google Widevine 라이선스 전달 서비스 발표](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
