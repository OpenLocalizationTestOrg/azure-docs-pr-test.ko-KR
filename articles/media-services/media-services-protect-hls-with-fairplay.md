---
title: "Apple FairPlay-Azure 또는 Microsoft PlayReady로 HLS 콘텐츠를 aaaProtect | Microsoft Docs"
description: "이 항목 한 개요를 제공 하 고 Azure 미디어 서비스 toodynamically toouse Apple FairPlay 사용 하 여 HTTP 라이브 스트리밍 (HLS) 콘텐츠를 암호화 하는 방법을 보여 줍니다. 또한 toouse hello 미디어 서비스 배달 서비스 toodeliver FairPlay 라이선스 tooclients를 라이선스 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Microsoft PlayReady 또는 Apple FairPlay로 HLS 콘텐츠 보호
Azure 미디어 서비스 사용 하면 toodynamically hello 다음 형식을 사용 하 여 HTTP 라이브 스트리밍 (HLS) 콘텐츠를 암호화 합니다.  

* **AES-128 비트 봉투 암호화되지 않은 키**

    hello 전체 청크 암호화 되어 hello를 사용 하 여 **S-128 CBC** 모드입니다. hello 스트림의 hello 암호 해독 되는 iOS 및 OS X 플레이어 고유 하 게 지원 됩니다. 자세한 내용은 [AES-128 동적 암호화 및 키 배달 서비스 사용](media-services-protect-with-aes128.md)을 참조하세요.
* **Apple FairPlay**

    hello 개별 비디오 및 오디오 샘플 hello를 사용 하 여 암호화 된 **S-128 CBC** 모드입니다. **FairPlay 스트리밍** (FPS)는 iOS와 Apple TV 네이티브 지원과 hello 장치 운영 체제에 통합 합니다. OS X에서 safari hello 암호화 미디어 확장 (EME) 인터페이스 지원을 사용 하 여 FPS를 수 있습니다.
* **Microsoft PlayReady**

hello 다음 그림에 나와 hello **HLS + FairPlay 또는 PlayReady 동적 암호화** 워크플로 합니다.

![동적 암호화 워크플로 다이어그램](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

이 항목에서는 미디어 서비스 toodynamically toouse Apple FairPlay로 HLS 콘텐츠를 암호화 하는 방법을 보여 줍니다. 또한 toouse hello 미디어 서비스 배달 서비스 toodeliver FairPlay 라이선스 tooclients를 라이선스 하는 방법을 보여 줍니다.

> [!NOTE]
> 또한 원하는 tooencrypt HLS PlayReady로 콘텐츠 toocreate 공통 콘텐츠 키를 해야 자산에 연결 합니다. 에 설명 된 대로 tooconfigure hello 콘텐츠 키 권한 부여 정책 등을 또한 해야 [PlayReady를 사용 하 여 동적 일반 암호화](media-services-protect-with-drm.md)합니다.
>
>

## <a name="requirements-and-considerations"></a>요구 사항 및 고려 사항

암호화 된 HLS 미디어 서비스 toodeliver FairPlay, 및 toodeliver FairPlay 라이선스와 함께 사용 하는 경우 hello 다음 필수입니다.

  * Azure 계정. 자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조하세요.
  * Media Services 계정. 하나의 toocreate 참조 [hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정 만들기](media-services-portal-create-account.md)합니다.
  * [Apple Development Program](https://developer.apple.com/)에 등록합니다.
  * Apple에서는 hello 콘텐츠 소유자 tooobtain hello 요구 [배포 패키지](https://developer.apple.com/contact/fps/)합니다. 미디어 서비스 키 보안 모듈 (KSM)를 이미 구현 하기 hello 최종 FPS 패키지를 요청 하 고 상태입니다. 최종 FPS toogenerate 인증 패키징하고 가져올 hello의 지침을 응용 프로그램 암호 키 (ASK) hello는 합니다. FairPlay ASK tooconfigure를 사용 합니다.
  * Azure 미디어 서비스 .NET SDK 버전 **3.6.0** 이상.

미디어 서비스 키 배달 측 작업을 수행 하는 hello는 설정 해야 합니다.

  * **응용 프로그램 인증서 (AC)**: hello 개인 키가 포함 된.pfx 파일입니다. 이 파일을 만들고 암호로 암호화합니다.

       키 배달 정책을 구성 하면 Base64 형식으로 해당 암호 및 hello.pfx 파일을 제공 해야 합니다.

      단계를 수행 하는 hello FairPlay에 대 한 toogenerate.pfx 인증서 파일 하는 방법을 설명 합니다.

    1. https://slproweb.com/products/Win32OpenSSL.html에서 OpenSSL을 설치합니다.

        Hello FairPlay 인증서와 다른 파일을 Apple에 의해 전달 있는 toohello 폴더를 이동 합니다.
    2. Hello hello 명령줄에서 다음 명령을 실행 합니다. 이 hello.cer 파일 tooa.pem 파일을 변환합니다.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem
    3. Hello hello 명령줄에서 다음 명령을 실행 합니다. 이 hello 개인 키가 있는 hello.pem 파일 tooa.pfx 파일을 변환합니다. 그런 다음 hello.pfx 파일에 대 한 hello 암호 OpenSSL에 요청 했습니다.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt
  * **응용 프로그램 인증서 암호가**: hello.pfx 파일을 만들기 위한 hello 암호입니다.
  * **응용 프로그램 인증서 암호 ID**: hello 암호를 다른 미디어 서비스 키를 업로드 하는 비슷한 toohow 업로드 해야 합니다. 사용 하 여 hello **ContentKeyType.FairPlayPfxPassword** enum 값 tooget hello 미디어 서비스 id입니다. 이것은 필요한 toouse 내 hello 키 배달 정책 옵션입니다.
  * **iv**: 16바이트의 임의 값입니다. 일치 해야 hello 자산 배달 정책에 iv hello 합니다. 생성할 hello iv를 두 위치에 저장 합니다: hello 자산 배달 정책 및 hello 키 배달 정책 옵션입니다.
  * **요청**: hello Apple 개발자 포털을 사용 하 여 hello 인증을 생성 하면이 키를 받습니다. 각 개발 팀에 고유한 ASK가 제공됩니다. Hello ASK의 복사본을 저장 하 고 안전한 장소에 저장 합니다. FairPlayAsk tooMedia 서비스로 tooconfigure ASK 나중에 필요 합니다.
  * **ASK ID**: 이 ID는 Media Services에 ASK를 업로드할 때 얻습니다. ASK hello를 사용 하 여 업로드 해야 **ContentKeyType.FairPlayAsk** 열거형 값입니다. Hello 결과로 hello 미디어 서비스 ID가 반환 하 고 hello 키 배달 정책 옵션을 설정할 때 용도입니다.

hello 다음과 같은 상황이 발생 하는 설정 해야 hello FPS 클라이언트 측:

  * **응용 프로그램 인증서 (AC)**: 일부 페이로드는 hello 운영 체제 tooencrypt 사용 하 여 hello 공개 키를 포함 하는.cer/.der 파일입니다. 미디어 서비스는 hello 플레이어에 필요 하기 때문에 항목에 대 한 tooknow가 필요 합니다. hello 키 배달 서비스 hello 해당 개인 키를 사용 하 여 해독 합니다.

tooplay는 FairPlay 암호화 스트림을 다시, 실제 ASK 첫 번째를 가져오고 실제 인증서를 생성 합니다. 이 프로세스에서는 다음 세 가지 요소를 모두 만듭니다.

  * .der 파일
  * .pfx 파일
  * hello.pfx에 대 한 암호

hello 다음 클라이언트는 지원로 HLS **S-128 CBC** 암호화: OS X, Apple TV iOS Safari 합니다.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>FairPlay 동적 암호화 및 라이선스 배달 서비스 구성
hello 다음은 hello 미디어 서비스 라이선스 배달 서비스를 사용 하 여 및 동적 암호화를 사용 하 여 FairPlay로 자산을 보호 하기 위한 일반적인 단계입니다.

1. 자산을 만들고 hello 자산에 파일을 업로드 합니다.
2. Hello 파일 toohello 적응 비트 전송률 MP4 세트를 포함 하는 hello 자산을으로 인코딩하십시오.
3. 콘텐츠 키를 만들고 hello 인코딩된 자산에 연결 합니다.  
4. Hello 콘텐츠 키 권한 부여 정책을 구성 합니다. Hello 다음을 지정 합니다.

   * hello에 (이 경우 FairPlay) 배달 방법.
   * FairPlay 정책 옵션 구성 - 방법에 대 한 자세한 내용은 tooconfigure FairPlay, 참조 hello **ConfigureFairPlayPolicyOptions()** hello 샘플 아래 메서드.

     > [!NOTE]
     > 일반적으로 원할 tooconfigure FairPlay 정책 옵션을 한 번만 인증은 ASK 서로 집합 하나만 있으므로 합니다.
     >
     >
   * 제한(열기 또는 토큰).
   * Hello 키 toohello 클라이언트 배달 방법을 정의 하는 정보 특정 toohello 키 배달 유형입니다.
5. Hello 자산 배달 정책을 구성 합니다. hello 배달 정책 구성에 포함 됩니다.

   * hello 배달 프로토콜 (HLS)입니다.
   * 동적 암호화 (일반 CBC 암호화)의 hello 형식입니다.
   * hello 라이선스 취득 URL입니다.

     > [!NOTE]
     > FairPlay와 다른 디지털 Rights Management (DRM) 시스템을 사용 하 여 암호화 하는 스트림을 toodeliver 원하는 tooconfigure 별도 배달 정책을 사용할 수 있습니다.
     >
     > * HTTP (대시)와 CENC (Common Encryption) (PlayReady + Widevine) 및 PlayReady로 부드러운 스트리밍 적응 스트리밍 동적 하나 IAssetDeliveryPolicy tooconfigure
     > * 다른 IAssetDeliveryPolicy tooconfigure FairPlay HLS에 대 한
     >
     >
6. OnDemand 로케이터 tooget 스트리밍 URL을 만듭니다.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>플레이어 앱별 FairPlay 키 배달 사용
Hello iOS SDK를 사용 하 여 플레이어 응용 프로그램을 개발할 수 있습니다. toobe 수 tooplay FairPlay 콘텐츠 tooimplement hello 라이선스 교환 프로토콜을 해야합니다. Apple에서는 이 프로토콜을 지정하지 않습니다. 가 tooeach 앱 toosend 키 배달 요청 하는 방식입니다. hello 미디어 서비스 FairPlay 키 배달 서비스는 hello SPC toocome hello 다음 양식에서에서 www-form-url 인코딩된 post 메시지로 필요 합니다.

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player hello 초기 FairPlay 재생을 지원 하지 않습니다. MAC OS X에서 tooget FairPlay 재생 hello Apple 개발자 계정에서에서 hello 샘플 플레이어를 가져옵니다.
>
>

## <a name="streaming-urls"></a>스트리밍 URL
Hello 스트리밍 URL에에서는 암호화 태그를 사용 해야 둘 이상의 DRM으로 자산 암호화 된 경우: (형식 ='m3u8-aapl' 암호화 'xxx' =) 합니다.

hello 고려 사항에 따라 적용 됩니다.

* 1개 이하의 암호화 형식만 지정할 수 있습니다.
* hello 암호화 유형 toobe 한 암호화가 적용 된 toohello 자산만 hello URL에 지정 되어 있지 않습니다.
* hello 암호화 유형은 대/소문자 구분입니다.
* hello 다음 암호화 종류를 지정할 수 있습니다.  
  * **cenc**: 일반 암호화(PlayReady 또는 Widevine)
  * **cbcs-aapl**: FairPlay
  * **cbc**: AES 봉투 암호화

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

1. 개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 
2. 추가 요소를 너무 다음 hello**appSettings** app.config 파일에 정의 된:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>예제

다음 예제는 hello hello 기능 toouse 미디어 서비스 toodeliver FairPlay로 암호화 된 콘텐츠를 보여 줍니다. 이 기능은 for.NET 버전 3.6.0 hello Azure Media Services SDK에서에서 도입 되었습니다. 

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
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a>다음 단계: 미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
