---
title: "aaaUsing aes-128 동적 암호화 및 키 배달 서비스 | Microsoft Docs"
description: "Microsoft Azure 미디어 서비스 AES 128 비트 암호화 키로 암호화 된 콘텐츠를 toodeliver 수 있습니다. 또한 미디어 서비스 암호화 키 tooauthorized 사용자가 전달 하는 hello 키 배달 서비스를 제공 합니다. 이 항목에서는 toodynamically S-128로 암호화 하 고 hello 키 배달 서비스를 사용 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a>AES-128 동적 암호화 및 키 전달 서비스 사용
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>개요
> [!NOTE]
> 참조 [이](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) 어떻게 tooprotect 미디어는 AES 암호화를 사용한을 내용에 대 한 개요 비디오.
> 
> 

Microsoft Azure 미디어 서비스에서는 toodeliver Http 라이브 스트리밍 (HLS) 및 부드러운 스트리밍을 AES로 암호화 된 고급 암호화 표준 () (128 비트 암호화 키를 사용 하 여) 있습니다. 또한 미디어 서비스 암호화 키 tooauthorized 사용자가 전달 하는 hello 키 배달 서비스를 제공 합니다. 원하는 tooencrypt 미디어 서비스에 대 한 자산 tooassociate hello 자산에는 암호화 키를 필요한 고 hello 키에 대 한 권한 부여 정책을 구성할 수도 있습니다. 미디어 서비스는 지정 된 hello 플레이어에서 스트림을 요청 되 면 키 toodynamically AES 암호화를 사용 하 여 콘텐츠를 암호화 합니다. toodecrypt hello 스트림 hello 플레이어 hello 키 배달 서비스에서 hello 키를 요청 합니다. hello 사용자가 아닌지 toodecide 권한이 tooget hello 키, hello 서비스 hello 키에 대해 지정한 hello 권한 부여 정책을 평가 합니다.

미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다. hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: 열거나 토큰 제한 합니다. 보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다. 미디어 서비스는 hello에 토큰을 지원 [단순 웹 토큰](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) 형식 및 [JSON 웹 토큰](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) 형식입니다. 자세한 내용은 참조 [hello 콘텐츠 키 권한 부여 정책 구성](media-services-protect-with-aes128.md#configure_key_auth_policy)합니다.

tootake 이점은 다중 비트 전송률 MP4 파일 또는 다중 비트 전송률 부드러운 스트리밍 원본 파일 집합이 포함 된 자산 toohave 동적 암호화 해야 합니다. 또한 해야 tooconfigure hello 배달 정책 (이 항목의 뒷부분에 설명) hello 자산에 대 한 합니다. 그런 다음 형식에 따라 hello hello 스트리밍 URL에에서 지정 된, 주문형 스트리밍 서버 hello 됩니다 되도록 해당 hello 스트림의 선택한 hello 프로토콜에서 제공 됩니다. 결과적으로, toostore 하기만 하면 및 단일 저장소 형식 및 미디어 서비스 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서에서 요청에 따라 hello 적절 한 응답을 제공 합니다.

이 항목에는 보호 된 미디어를 전달 하는 응용 프로그램에서 작동 하는 유용한 toodevelopers 것입니다. hello 항목에서는 권한 있는 클라이언트만 hello 암호화 키를 받을 수 있도록 권한 부여 정책 사용 하 여 키 배달 서비스 tooconfigure hello 하는 방법을 보여 줍니다. 또한 표시 방법을 toouse 동적 암호화.


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a>AES-128 동적 암호화 및 키 배달 서비스 워크플로

hello 다음은 AES, hello 미디어 서비스 키 배달 서비스를 사용 하 고 또한 동적 암호화를 사용 하 여로 자산을 암호화할 때 tooperform 해야 하는 일반적인 단계입니다.

1. [자산을 만들고 파일 hello 자산으로 업로드](media-services-protect-with-aes128.md#create_asset)합니다.
2. [Hello 파일 toohello 적응 비트 전송률 MP4 세트를 포함 하는 hello 자산 인코딩](media-services-protect-with-aes128.md#encode_asset)합니다.
3. [콘텐츠 키를 만들고 hello 인코딩된 자산에 연결할](media-services-protect-with-aes128.md#create_contentkey)합니다. 미디어 서비스 콘텐츠 키 hello hello 자산의 암호화 키를 포함합니다.
4. [Hello 콘텐츠 키 권한 부여 정책 구성](media-services-protect-with-aes128.md#configure_key_auth_policy)합니다. hello 콘텐츠 키 인증 정책은 구성 하 고 hello 클라이언트에서 콘텐츠 키 toobe 배달된 toohello 클라이언트 hello 하려면 충족 해야 합니다.
5. [자산의 배달 정책을 hello 구성](media-services-protect-with-aes128.md#configure_asset_delivery_policy)합니다. hello 배달 정책 구성에: 키 취득 URL 및 IV (Initialization Vector) (AES 128을 암호화할 때 동일한 IV toobe 제공 하는 hello 및 암호 해독 필요), 배달 프로토콜 (예를 들어, MPEG DASH, HLS, 부드러운 스트리밍 또는 모두), hello 형식 동적 암호화 (예: 봉투 또는 동적 암호화 없음).

    Hello에 서로 다른 정책 tooeach 프로토콜을 적용할 수 동일한 자산입니다. 예를 들어 PlayReady 암호화 tooSmooth/DASH 및 AES 봉투 (envelope) tooHLS 적용할 수 있습니다. 배달 정책에 정의 되어 있지 않은 모든 프로토콜 (예를 들어 추가한만 hello 프로토콜로 HLS를 지정 하는 단일 정책을) 스트리밍에서 차단 됩니다. hello 예외 toothis는 없는 자산 배달 정책을 정의 해야 합니다. 그런 다음 모든 프로토콜이 일반 hello에 허용 됩니다.

6. [OnDemand 로케이터 만들기](media-services-protect-with-aes128.md#create_locator) 의 순서로 tooget 스트리밍 URL입니다.

hello 항목 표시 [로 인해 클라이언트 응용 프로그램 hello 키 배달 서비스에서 키를 요청할 수는 어떻게](media-services-protect-with-aes128.md#client_request)합니다.

전체.NET 있습니다 [예제](media-services-protect-with-aes128.md#example) hello 항목의 hello 끝에 있습니다.

다음 이미지는 hello 위에서 설명한 hello 워크플로를 보여 줍니다. 여기서 hello 토큰 인증을 위해 사용 됩니다.

![AES-128로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

이 항목의 나머지 부분 hello에 대 한 세부 정보, 코드 예제 및 tooachieve 위에서 설명한 작업 hello 하는 방법을 보여 주는 링크 tootopics 제공 합니다.

## <a name="current-limitations"></a>현재 제한 사항
자산 배달 정책을 추가하거나 업데이트하는 경우 기존 로케이터(있는 경우)를 삭제하고 새 로케이터를 만들어야 합니다.

## <a id="create_asset"></a>자산 만들기 및 hello 자산에 파일 업로드
순서 toomanage 인코딩 및 스트리밍 비디오, Microsoft Azure 미디어 서비스에 콘텐츠를 먼저 업로드 해야 합니다. 를 업로드 한 후 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다. 

자세한 내용은 [미디어 서비스 계정에 파일 업로드](media-services-dotnet-upload-files.md)를 참조하세요.

## <a id="encode_asset"></a>Hello 자산 포함 hello 파일 toohello 적응 비트 전송률 MP4 세트로 인코딩
동적 암호화 toocreate 다중 비트 전송률 MP4 파일 또는 다중 비트 전송률 부드러운 스트리밍 원본 파일 집합이 포함 된 자산은 하기만 하면 됩니다. 그런 다음 hello hello 매니페스트에 지정 된 형식에 따라 또는 요청 조각, 주문형 스트리밍 서버 hello 스트림이 선택한 hello 프로토콜에 수신 하는 방법을 사용 하면 hello 합니다. 결과적으로, toostore 하기만 하면 및 단일 저장소 형식 및 미디어 서비스 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서에서 요청에 따라 hello 적절 한 응답을 제공 합니다. 자세한 내용은 참조 hello [동적 패키징 개요](media-services-dynamic-packaging-overview.md) 항목입니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 
>
>또한 toobe 수 toouse 동적 패키징 및 동적 암호화 자산인 있어야 적응 비트 전송률 mp4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합입니다.

방법에 대 한 지침은 tooencode, 참조 [어떻게 tooencode 미디어 인코더 표준를 사용 하 여 자산](media-services-dotnet-encode-with-media-encoder-standard.md)합니다.

## <a id="create_contentkey"></a>콘텐츠 키를 만들고 hello 인코딩된 자산에 연결
Hello 콘텐츠 키 미디어 서비스 자산 tooencrypt hello 키에 포함 되어 있는 합니다.

자세한 내용은 [콘텐츠 키 만들기](media-services-dotnet-create-contentkey.md)를 참조하세요.

## <a id="configure_key_auth_policy"></a>Hello 콘텐츠 키 권한 부여 정책 구성
미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다. hello 콘텐츠 키 인증 정책은 구성 하 고 hello 키 toobe toohello 클라이언트에 배달 하려면에서 hello 클라이언트 (플레이어)에서 충족 해야 합니다. hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: 열고, 제한, 또는 IP 제한이 토큰입니다.

자세한 내용은 [콘텐츠 키 권한 부여 정책 구성](media-services-dotnet-configure-content-key-auth-policy.md)을 참조하세요.

## <a id="configure_asset_delivery_policy"></a>자산 배달 정책 구성
자산에 대 한 hello 배달 정책을 구성 합니다. 자산 배달 정책 구성 hello 있는 일부의 원인에는 다음이 포함 됩니다.

* hello 키 취득 URL 
* hello hello 봉투 암호화에 대 한 초기화 벡터 (IV) toouse 합니다. AES 128 hello 암호화 및 암호 해독 하는 경우 동일한 IV toobe 제공 해야 합니다. 
* hello 자산 배달 프로토콜 (예를 들어, MPEG DASH, HLS, 부드러운 스트리밍 또는 모두)입니다.
* hello 유형의 동적 암호화 (예: AES 봉투) 또는 동적 암호화 없음. 

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

## <a id="client_request"></a>클라이언트 프로그램은 어떻게 hello 키 배달 서비스에서 키를 요청할 수 있습니까?
Hello 이전 단계에서 tooa 매니페스트 파일을 가리키는 hello URL을 생성 합니다. 클라이언트는 hello tooextract hello 스트리밍 매니페스트 파일 순서 toomake 요청 toohello 키 배달 서비스에서에서 필요한 정보를 필요 합니다.

### <a name="manifest-files"></a>매니페스트 파일
hello 클라이언트 해야 (즉 콘텐츠 kid (키 Id)도 포함) tooextract hello URL hello 매니페스트 파일의 값입니다. 클라이언트 hello은 tooget hello 암호화 키 hello 키 배달 서비스를 먼저 시도 합니다. hello 클라이언트도 tooextract hello IV 값이 필요 하 고 다음 코드 조각 hello stream.hello 암호 해독을 사용 하 여 hello를 보여 줍니다. <Protection> hello 부드러운 스트리밍 매니페스트의 요소입니다.

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

HLS의 경우 hello hello 루트 매니페스트 세그먼트 파일로 구분 됩니다. 

예를 들어 hello 루트 매니페스트는: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) 이므로 세그먼트 파일 이름의 목록을 포함 합니다.

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

텍스트 편집기 (예를 들어 http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should에서에서 hello 세그먼트 파일 중 하나를 열면 #EXT-X 키를 나타내는 해당 hello 파일은 암호화를 포함 합니다.

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>AES 암호화 safari에서는 HLS tooplay 계획인 경우, 참조 [이 블로그](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)합니다.

### <a name="request-hello-key-from-hello-key-delivery-service"></a>Hello 키 배달 서비스에서 hello 키 요청

hello 다음 코드를 보여 줍니다 방법을 toosend 요청 toohello 미디어 서비스 키 배달 서비스는 키 배달 Uri (즉 hello 매니페스트에서 추출 된)를 사용 하 여 (이 항목 어떻게 tooget 단순 웹 토큰을 보안 토큰 서비스에서에 대 한와 통신 하지 않습니다) 토큰입니다.

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a>.NET을 사용하여 AES-128로 콘텐츠 보호

### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

1. 개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 
2. 추가 요소를 너무 다음 hello**appSettings** app.config 파일에 정의 된:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <a id="example"></a>예제

이 섹션에 표시 된 hello 코드도 Program.cs 파일의 hello 코드를 덮어씁니다.
 
>[!NOTE]
>다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

확인 되었는지 tooupdate 변수 toopoint toofolders 입력된 파일이 있는 위치 합니다.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

