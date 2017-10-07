---
title: "aaaMedia 서비스 릴리스 정보 | Microsoft Docs"
description: "미디어 서비스 릴리스 정보"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Azure 미디어 서비스 릴리스 정보
이 릴리스 정보에는 이전 릴리스 이후의 변경 내용과 알려진 문제가 요약되어 있습니다.

> [!NOTE]
> 갈수록 고객 으로부터 toohear 원하는 하 고 영향을 주는 문제 해결에 집중 합니다. tooreport 문제 또는 질문 하 고 hello에 게시 해 주세요 [Azure 미디어 서비스 MSDN 포럼]합니다.
> 
> 

## <a id="issues"></a>현재 알려진 문제
### <a id="general_issues"></a>미디어 서비스 관련 일반 문제
| 문제 | 설명 |
| --- | --- |
| Hello REST API에에서는 몇 가지 일반적인 HTTP 헤더가 제공 되지 않습니다. |Hello REST API를 사용 하 여 미디어 서비스 응용 프로그램을 개발 하는 경우 표시 하는 몇 가지 일반적인 HTTP 헤더 필드 (클라이언트 요청 ID를 포함 하 여 요청 ID 및 클라이언트 요청 ID 반환)는 지원 되지 않습니다. hello 헤더는 향후 업데이트에서 추가 됩니다. |
| 퍼센트 인코딩은 허용되지 않습니다. |미디어 서비스 스트리밍 콘텐츠 (예를 들어 http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) hello에 대 한 Url 작성 시 hello IAssetFile.Name 속성의 hello 값을 사용 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다. 값의 hello hello **이름** 속성 hello 다음 중 하나를 사용할 수 없습니다 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다. 또한 ‘.’ 하나만 사용할 수 있습니다. hello 파일 이름 확장명입니다. |
| 일부인 ListBlobs 메서드 hello hello Azure 저장소 SDK 버전 3.x에 실패 합니다. |Media Services hello를 기반으로 하는 SAS Url 생성 [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) 버전입니다. Hello를 사용 하 여 blob 컨테이너에 toouse Azure 저장소 SDK toolist blob을 하려는 경우 [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) Azure 저장소 SDK 버전의 일부인 메서드 2.x 합니다. 일부인 ListBlobs 메서드 hello hello Azure 저장소 SDK 버전 3.x이 실패 합니다. |
| 미디어 서비스 제한 메커니즘 toohello 서비스 과도 하 게 요청 하는 응용 프로그램에 대 한 hello 리소스 사용량을 제한 합니다. hello 서비스는 hello 서비스 사용할 수 없음 (503) HTTP 상태 코드를 반환할 수 있습니다. |자세한 내용은 hello에 hello 503 HTTP 상태 코드에 대 한 hello 설명을 보려면 [Azure 미디어 서비스 오류 코드](media-services-encoding-error-codes.md) 항목입니다. |
| 엔터티를 쿼리할 때 공용 REST v2 쿼리 결과 too1000 결과 제한 하기 때문에 한 번에 반환 된 1000 엔터티 제한이 있습니다. |Toouse 해야 **Skip** 및 **걸릴** (.NET) / **top** (REST)에 설명 된 대로 [.NET 예제](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) 및 [이 REST API 예제](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)합니다. |
| 일부 클라이언트 hello 부드러운 스트리밍 매니페스트의의 반복 태그 문제를 통해 가져올 수 있습니다. |자세한 내용은 [이](media-services-deliver-content-overview.md#known-issues) 섹션을 참조하세요. |
| Azure 미디어 서비스 .NET SDK 개체는 직렬화할 수 없으며 따라서 Azure 캐싱에서 작동하지 않습니다. |Tooserialize hello SDK AssetCollection 개체 tooadd 시도 하면 해당 tooAzure 캐싱, 예외가 throw 됩니다. |
| 메시지 문자열 "Stage: DownloadFile. Code: System.NullReferenceException"을 나타내며 인코딩 작업이 실패합니다. |hello 일반적인 인코딩 워크플로 되었거나 tooupload 입력된 비디오 파일 tooan 입력 자산, 및 제출 하나 더 많은 인코딩 작업에 대 한 입력 자산, 입력 자산 추가로 수정 하지 않고 있습니다. 그러나 수정 하는 경우 hello 입력 (예: 추가/삭제/파일 이름 바꾸기 hello 자산 내), 여는 자산 다음 다운로드 오류와 후속 작업이 실패할 수 있습니다. hello 해결 하는 방법은 toodelete hello 입력 자산, 및 파일 tooa 입력 다시 업로드 새 자산입니다. |

## <a id="rest_version_history"></a>REST API 버전 기록
미디어 서비스 REST API 버전 기록 hello에 대 한 정보를 참조 하십시오. [Azure 미디어 서비스 REST API 참조]합니다.

## <a name="june-2017-release"></a>2017년 6월 릴리스

이제 Media Services는 [Azure AD(Azure Active Directory) 기반 인증](media-services-use-aad-auth-to-access-ams-api.md)을 지원합니다.

> [!IMPORTANT]
> 현재 미디어 서비스는 hello Azure 액세스 제어 서비스 인증 모델을 지원 합니다. 그러나 Access Control 권한 부여는 2018년 6월 1일부로 더 이상 사용되지 않을 예정입니다. Toohello Azure AD 인증 모델을 최대한 빨리 마이그레이션하는 것이 좋습니다.

## <a name="march-2017-release"></a>2017년 3월 릴리스

이제 사용할 수 있습니다 Azure 미디어 표준 너무[자동 생성 비트 전송률 사다리](media-services-autogen-bitrate-ladder-with-mes.md) hello "적응 스트리밍" 사전 설정 문자열 인코딩 작업을 만들 때 지정 하 여 합니다. "적응 스트리밍" 사전 설정이 권장된 하는 hello 이면 tooencode 비디오 스트리밍 미디어 서비스에 대 한 원하는. 특정 시나리오에 대 한 인코딩 사전 설정을 toocustomize 해야 할 경우부터 시작할 수 있습니다 [이러한](media-services-mes-presets-overview.md) 사전 설정입니다.

이제 사용할 수 있습니다 Azure 미디어 표준 또는 미디어 인코더 프리미엄 워크플로 너무[fMP4 청크를 생성 하는 인코딩 작업을 만들어](media-services-generate-fmp4-chunks.md)합니다. 


## <a name="febuary-2017-release"></a>2017년 2월 릴리스

2017 년 4 월 1부터 90 일 보다 오래 된 계정에서 모든 작업 기록은 자동으로 함께 삭제 됩니다, 관련된 작업 레코드를 레코드의 총 수 hello hello 최대 할당량 미만인 경우에 합니다. 내용을 tooarchive hello 작업/태스크를 설명 하는 hello 코드를 사용할 수 있습니다 [여기](media-services-dotnet-manage-entities.md)합니다.

## <a name="january-2017-release"></a>2017년 1월 릴리스

Microsoft Azure 미디어 서비스 AMS ()는 **스트리밍 끝점** 직접 tooa 클라이언트 플레이어 응용 프로그램 또는 향후 배포를 위해 네트워크 CDN (콘텐츠 배달) tooa 콘텐츠를 배달할 수 있는 스트리밍 서비스를 나타냅니다. 미디어 서비스는 매끄러운 Azure CDN 통합도 제공합니다. StreamingEndpoint 서비스 hello 아웃 바운드 스트림은 라이브 스트림, 수요 또는 미디어 서비스 계정에 자산 점진적 다운로드 관련 한 비디오 수 있습니다. 각 Azure Media Services 계정에는 기본 StreamingEndpoint 포함됩니다. Hello 계정에서 추가 Streamingendpoint은 만들 수 있습니다. StreamingEndpoints 1.0 및 2.0이라는 두 가지 버전이 있습니다. 2017년 1월 10일부터 새로 만든 AMS 계정은 **기본** StreamingEndpoint 버전 2.0을 포함합니다. 스트리밍 끝점 toothis 계정을 추가 하는 추가 됩니다 버전 2.0. 이 변경은 기존 계정 hello; 영향을 미치지 않습니다. 기존 Streamingendpoint 버전 1.0 및 2.0 업그레이드 tooversion 될 수 있습니다. 이 변경 사항으로 인해 동작, 청구 및 기능이 변경됩니다(자세한 내용은 [이](media-services-streaming-endpoints-overview.md) 항목 참조).

Hello 2.15 버전부터 Azure 미디어 서비스 추가 toohello 스트리밍 끝점 엔터티 속성을 다음 hello: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**합니다. 이러한 속성의 자세한 개요는 [여기](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)를 참조하세요. 

## <a name="december-2016-release"></a>2016년 12월 릴리스

이제 azure 미디어 서비스는 해당 서비스에 대 한 원격 분석/메트릭 데이터 tooaccess 사용 합니다. hello AMS의 현재 버전을 사용 하 여 StreamingEndpoint, 라이브 채널용 원격 분석 데이터를 수집 하 고 라이브 보관 엔터티 수 있습니다. 자세한 내용은 [이 항목](media-services-telemetry-overview.md) 을 참조하세요.

## <a id="july_changes16"></a>2016년 7월 릴리스
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>업데이트 toomanifest 파일 (*. 인코딩 작업에 의해 생성 된 ISM)
인코딩 작업 제출 된 tooMedia 인코더 표준 또는 Azure 미디어 인코더 인 경우 hello 인코딩 작업 생성는 [스트리밍 매니페스트 파일](media-services-deliver-content-overview.md) (*.ism) 파일 hello에 자산을 출력 합니다. 최신 서비스 릴리스 hello 사용이 스트리밍 매니페스트 파일의 hello 구문을 업데이트 되었습니다.

> [!NOTE]
> hello 스트리밍 매니페스트 (.ism) 파일의 hello 구문은 내부 용도로 예약 되어 이며 이후 릴리스에서 주체 toochange 합니다. 하십시오 수정 하거나 안이 파일의 내용을 hello를 조작 합니다.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>새 클라이언트 매니페스트 (*. Hello에 ISMC) 파일이 생성 되는 인코딩 작업 하나 이상의 MP4 파일을 출력 하는 경우 자산을 출력
자산 스트리밍 클라이언트 매니페스트 (*.ismc) 파일에도 포함 됩니다 hello 출력 hello 하나 더 많은 MP4 파일을 생성 하는 인코딩 작업 완료 된 후 최신 서비스 릴리스 hello로 시작 합니다. hello.ismc 파일 동적 스트리밍의 hello 성능을 향상 시킬 수 있습니다. 

> [!NOTE]
> hello 클라이언트 매니페스트 (.ismc) 파일의 hello 구문 내부 용도로 예약 되어 이며 이후 릴리스에서 주체 toochange 합니다. 하십시오 수정 하거나 안이 파일의 내용을 hello를 조작 합니다.
> 
> 

자세한 내용은 [이 블로그](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) 를 참조하세요.

### <a name="known-issues"></a>알려진 문제
일부 클라이언트 hello 부드러운 스트리밍 매니페스트의의 반복 태그 문제를 통해 가져올 수 있습니다. 자세한 내용은 [이](media-services-deliver-content-overview.md#known-issues) 섹션을 참조하세요.

## <a id="apr_changes16"></a>2016년 4월 릴리스
### <a name="azure-media-analytics"></a>Azure 미디어 분석
Azure 미디어 서비스는 강력한 비디오 인텔리전스를 위한 Azure 미디어 분석을 출시했습니다. 자세한 내용은 [Azure 미디어 서비스 분석 개요](media-services-analytics-overview.md)를 참조하세요.

### <a name="apple-fairplay-preview"></a>Apple FairPlay(미리 보기)
Azure 미디어 이제 있습니다 toodynamically HTTP 라이브 스트리밍 (HLS) 암호화할 수 있도록 Apple FairPlay로 콘텐츠를 서비스 합니다. AMS 라이선스 배달 서비스 toodeliver FairPlay 라이선스 tooclients를 사용할 수 있습니다. 자세한 내용은 참조 [Apple FairPlay로 HLS 콘텐츠 보호를 사용 하 여 Azure 미디어 서비스 tooStream ](media-services-protect-hls-with-fairplay.md)합니다.

## <a id="feb_changes16"></a>2016년 2월 릴리스
Azure Media Services SDK for.NET (3.5.3)의 최신 버전 hello Widevine 관련된 버그 수정을 포함합니다. hello 문제가 발견 된: AssetDeliveryPolicy Widevine를 사용 하 여 암호화 하는 여러 자산에 대 한 다시 사용할 수 없습니다. 이 버그 수정이 반영 hello의 일환으로 속성을 다음 추가한 toohello SDK: **WidevineBaseLicenseAcquisitionUrl**합니다.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>2016년 1월 릴리스
인코딩 예약 단위 tooreduce 혼동을 인코더 이름으로 바뀝니다.

hello Basic, Standard 및 Premium 인코딩 예약된 단위는 이름이 바뀐된 tooS1, S2, S3 예약 단위를 각각 및 합니다.  오늘 기본 인코딩 Ru를 사용 하는 고객 표준 하는 동안 Azure 포털에서 (및 hello bill) hello 레이블로 s 1에 표시 되 고 Premium hello 레이블을 S2, S3를 각각 표시 됩니다. 

## <a id="dec_changes_15"></a>2015년 12월 릴리스

### <a name="azure-media-encoder-deprecation-announcement"></a>Azure Media Encoder 사용 중단 알림

미디어 인코더 표준의 hello 릴리스에서 12 개월에 약부터 azure 미디어 인코더 지원 되지 것입니다.

### <a name="azure-sdk-for-php"></a>PHP용 Azure SDK
hello Azure SDK 팀 게시 hello의 새로운 릴리스가 [PHP 용 Azure SDK](http://github.com/Azure/azure-sdk-for-php) 패키지를 Microsoft Azure 미디어 서비스에 대 한 업데이트와 새로운 기능을 포함 합니다. 특히, 이제 지원 hello 최신 Azure Media Services SDK for PHP hello [콘텐츠 보호](media-services-content-protection-overview.md) 기능:와 토큰 제한 없는 (PlayReady 및 Widevine) DRM 및 AES 동적 암호화. 또한 [인코딩 단위](media-services-dotnet-encoding-units.md)크기 조정을 지원합니다.

자세한 내용은 다음을 참조하세요.

* hello [Microsoft Azure Media Services SDK for PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) 블로그.
* hello 다음 [코드 샘플](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp 드리겠습니다 신속 하 게 합니다.
  * **vodworkflow_aes.php**: 이것은 보여 주는 PHP 파일 방법을 toouse aes-128 동적 암호화 및 키 배달 서비스. 설명 하는 hello.NET 샘플에 기반 하는 [이](media-services-protect-with-aes128.md) 문서.
  * **vodworkflow_aes.php**: 이것은 보여 주는 PHP 파일 방법을 toouse PlayReady 동적 암호화 및 라이선스 배달 서비스. 설명 하는 hello.NET 샘플에 기반 하는 [이](media-services-protect-with-drm.md) 문서.
  * **scale_encoding_units.php**: tooscale 인코딩 단위를 예약 하는 방법을 보여 주는 PHP 파일입니다.

## <a id="nov_changes_15"></a>2015년 11월 릴리스
Azure 미디어 서비스는 이제 hello 클라우드에서 Google Widevine 라이선스 배달 서비스를 제공합니다. 자세한 내용은 참조 너무[알림 블로그](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/)합니다. 또한 [이 자습서](media-services-protect-with-drm.md) 및 [GitHub 리포지토리](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm)도 참조하세요. 

Azure 미디어 서비스에서 제공하는 Widevine 라이선스 배달 서비스는 미리 보기로 제공됩니다. 자세한 내용은 [이 게시물](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/)을 참조하세요.

## <a id="oct_changes_15"></a>2015년 10월 릴리스
Azure 미디어 서비스 AMS ()는 데이터 센터를 수행 하는 hello 동시에 이제: 브라질 남쪽, 인도 서 부, 남부 인도 및 중앙 인도 있습니다. 이제 사용할 수 있습니다 hello Azure 포털 너무[미디어 서비스 계정을 만드는](media-services-portal-create-account.md) 설명 하는 다양 한 작업을 수행 하 고 [여기](https://azure.microsoft.com/documentation/services/media-services/)합니다. 그러나 라이브 인코딩은 이러한 데이터 센터에서 활성화되지 않습니다. 또한 모든 유형의 인코딩 예약 단위를 이러한 데이터 센터에서 사용할 수 없습니다.

* 브라질 남부:                                          표준 및 기본 인코딩 예약 단위만 사용 가능합니다.
* 인도 서부, 인도 남부 및 인도 중부:             기본 인코딩 예약 단위만 사용 가능

## <a id="september_changes_15"></a>2015년 9월 릴리스
* 제안 기능은 tooprotect hello 이제 AMS 주문형 비디오 VOD () 및 라이브 스트림을 Widevine 모듈식 DRM 기술로 모두 합니다. Widevine 라이선스를 제공 하는 배달 서비스 파트너 toohelp 다음 hello를 사용할 수 있습니다: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/)합니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)를 참조하세요.
  
    사용할 수 있습니다 [AMS.NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (3.5.1 hello 버전부터 시작) 또는 REST API tooconfigure 프로그램 AssetDeliveryConfiguration toouse Widevine 합니다.  
* AMS에서 Apple ProRes 동영상 지원을 추가했습니다. 이제 Apple ProRes 또는 기타 코덱을 사용하는 QuickTime 원본 동영상 파일을 업로드할 수 있습니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/)를 참조하세요.
* 미디어 인코더 표준 toodo 하위 클리핑 및 라이브 보관 추출 이제 사용할 수 있습니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/)를 참조하세요.
* 다음 업데이트를 필터링 하는 hello 만들 수 있습니다. 
  
  * 이제 오디오 전용 필터로 Apple HTTP 라이브 스트리밍(HLS) 포맷을 사용할 수 있습니다. 이 업데이트 하면 tooremove 오디오 전용 추적을 지정 하 여 (오디오 전용 = false) hello url에서입니다.
  * 자산에 대 한 필터를 정의할 때 (위쪽 too3) 여러 필터는 단일 URL에는 기능 toocombine를 해야 합니다.
    
    자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 를 참조하세요.
* AMS는 이제 HLS v4에 I-프레임을 지원합니다. I-프레임 지원은 빨리 감기와 되감기 작업을 최적화합니다. 기본적으로 모든 HLS v4 출력은 I-프레임 재생 목록(EXT-X-I-FRAME-STREAM-INF)를 포함합니다.
  
    자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 를 참조하세요.

## <a id="august_changes_15"></a>2015년 8월 릴리스
* Azure Media Services SDK for Java V0.8.0 릴리스 및 새로운 샘플이 제공됩니다. 자세한 내용은 다음을 참조하세요.
  
  * [블로그 게시물](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Java 샘플 리포지토리](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* 다중 오디오 스트림을 지원하는 Azure 미디어 플레이어 업데이트. 자세한 내용은 다음을 참조하세요.
  * [블로그 게시물](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>2015년 7월 릴리스
* 미디어 인코더 표준의 일반 공급 hello를 발표합니다. 자세한 내용은 [이 블로그 게시물](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)에 게시해 주세요.
  
    미디어 인코더 표준은 [이](http://go.microsoft.com/fwlink/?LinkId=618336) 섹션에 설명된 기본 설정을 사용합니다. 4k 인코딩합니다에 대 한를 사전 설정을 사용할 때는 hello 발생 해야 참고 **프리미엄** 예약 단위 형식입니다. 자세한 내용은 참조 [어떻게 tooScale 인코딩](media-services-scale-media-processing-overview.md)합니다.
* Azure 미디어 서비스 및 플레이어의 라이브 실시간 캡션. 자세한 내용은 [이 블로그 게시물](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)을 참조하세요.

### <a name="media-services-net-sdk-updates"></a>미디어 서비스 .NET SDK 업데이트
Azure 미디어 서비스 .NET SDK의 현재 버전은 3.4.0.0입니다. 이 릴리스에서 hello 다음 기능이 추가 되었습니다.  

* 라이브 아카이브에 대한 지원 구현 라이브 아카이브를 포함한 자산은 다운로드할 수 없습니다.
* 동적 필터에 대한 지원 구현
* 자산을 삭제 하는 동안 사용자가 tookeep 저장소 컨테이너를 허용 하는 구현 된 기능입니다.
* 버그 수정 관련 채널 tooretry 정책을 합니다.
* **미디어 인코더 프리미엄 워크플로**사용

## <a id="june_changes_15"></a>2015년 6월 릴리스
### <a name="media-services-net-sdk-updates"></a>미디어 서비스 .NET SDK 업데이트
Azure 미디어 서비스 .NET SDK의 현재 버전은 3.3.0.0입니다. 이 릴리스에서 hello 다음 기능이 추가 되었습니다.  

* OpenId Connect Discovery 사양 지원
* ID 공급자 측의 키 롤오버 처리 지원 

OpenID Connect 검색 문서를 노출 하는 id 공급자를 사용 하는 경우 (hello 다음 공급자 않으며: Azure Active Directory, Google, Salesforce), 서명 키에서 JWT 토큰의 유효성 검사를 위해 Azure 미디어 서비스 tooobtain 지시할 수 있습니다 OpenID 검색 사양을 연결 합니다. 

자세한 내용은 참조 [를 사용 하 여 Json 웹 키 검색 사양 toowork OpenID Connect에서 JWT로 Azure 미디어 서비스에서 인증 토큰](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/)합니다.

## <a id="may_changes_15"></a>2015년 5월 릴리스
Hello 같은 새로운 기능 발표 합니다.

* [미디어 서비스로 라이브 인코딩 미리 보기](media-services-manage-live-encoder-enabled-channels.md)
* [동적 매니페스트](media-services-dynamic-manifest-overview.md)
* [Azure 미디어 Hyperlapse 미디어 프로세서 미리 보기](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>2015년 4월 릴리스
### <a name="general-media-services-updates"></a>일반 미디어 서비스 업데이트
* [Azure 미디어 플레이어가 도입](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)되었습니다.
* 기본으로 만들어진 채널은 RTMP 프로토콜을 구성 된 tooingest 미디어 서비스 REST 2.10로 시작 하 고 보조 수집 Url입니다. 자세한 내용은 [채널 수집 구성](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Azure 미디어 인덱서 업데이트
* 스페인어 지원
* 새로운 구성 xml 형식

자세한 내용은 [이 게시물](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/)을 참조하세요.

### <a name="media-services-net-sdk-updates"></a>미디어 서비스 .NET SDK 업데이트
Azure 미디어 서비스 .NET SDK의 현재 버전은 3.2.0.0입니다.

hello 고객 업데이트 관련 hello 다음과가 같습니다.

* **주요 변경 내용**: 변경 **TokenRestrictionTemplate.Issuer** 및 **TokenRestrictionTemplate.Audience** toobe string 형식입니다.
* 업데이트를 관련 된 toocreating 사용자 지정 다시 시도 정책입니다.
* 버그 수정 관련 파일 toouploading/다운로드 합니다.
* hello **MediaServicesCredentials** 클래스에는 이제에 대 한 기본 및 보조 액세스 제어 끝점 tooauthenticate 적용 합니다.

## <a id="march_changes_15"></a>2015년 3월 릴리스
### <a name="general-media-services-updates"></a>일반 미디어 서비스 업데이트
* 미디어 서비스는 이제 Azure CDN 통합을 제공합니다. toosupport hello 통합, hello **CdnEnabled** 속성 너무 추가한**StreamingEndpoint**합니다.  **CdnEnabled** 는 버전 2.9부터 REST API와 함께 사용할 수 있습니다(자세한 내용은 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)참조).  **CdnEnabled**는 버전 3.1.0.2부터 .NET SDK와 함께 사용할 수 있습니다(자세한 내용은 [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx) 참조).
* **미디어 인코더 Premium 워크플로**알림. 자세한 내용은 [Azure 미디어 서비스의 프리미엄 인코딩 소개](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)를 참조하세요.

## <a id="february_changes_15"></a>2015년 2월 릴리스
### <a name="general-media-services-updates"></a>일반 미디어 서비스 업데이트
이제 미디어 서비스 REST API의 버전이 2.9입니다. 이 버전 부터는 hello Azure CDN 통합 된 스트리밍 끝점을 사용할 수 있습니다. 자세한 내용은 [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx)를 참조하세요.

## <a id="january_changes_15"></a>2015년 1월 릴리스
### <a name="general-media-services-updates"></a>일반 미디어 서비스 업데이트
동적 암호화를 통해 GA(General Availability)의 콘텐츠 보호 알림. 자세한 내용은 [Azure 미디어 서비스에서 DRM 기술의 일반적인 가용성으로 스트리밍 보안 강화](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/)를 참조하세요.

### <a name="media-services-net-sdk-updates"></a>미디어 서비스 .NET SDK 업데이트
이제 Azure 미디어 서비스 .NET SDK의 버전은 3.1.0.1입니다.

이 릴리스에서 hello 기본 Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate 생성자 사용 되지 않는 것으로 표시 합니다. 새로운 생성자 hello TokenType을 인수로 사용 합니다.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>2014년 12월 릴리스
### <a name="general-media-services-updates"></a>일반 미디어 서비스 업데이트
* 일부 업데이트와 새로운 기능 toohello Azure 인덱서 미디어 프로세서를 추가 되었습니다. 자세한 내용은 [Azure 미디어 인덱서 버전 1.1.6.7 릴리스 정보](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/)를 참조하세요.
* Tooupdate 인코딩 예약된 단위 수 있도록 새 REST API가 추가: [rest EncodingReservedUnitType](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)합니다.
* 키 배달 서비스를 위한 CORS 지원이 추가되었습니다.
* 권한 부여 정책 옵션을 쿼리하는 성능이 향상되었습니다.
* 중국 데이터 센터에서 hello [키 배달 URL](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) 고객당 되었습니다 (다른 데이터 센터에서 처럼).
* HLS 자동 대상 기간이 추가되었습니다. 라이브 스트리밍을 수행할 때 HLS는 항상 동적으로 패키지됩니다. 기본적으로 미디어 서비스는 HLS 세그먼트 패키징 비율 (FragmentsPerSegment) hello 키 프레임 간격 (KeyFrameInterval) 라고도 tooas Group of Pictures hello 라이브 인코더에서 받은 GOP에 따라 자동으로 계산 합니다. 자세한 내용은 [Azure Media Services 라이브 스트리밍 사용]을 참조하세요.

### <a name="media-services-net-sdk-updates"></a>미디어 서비스 .NET SDK 업데이트
* [Azure 미디어 서비스 .NET SDK](http://www.nuget.org/packages/windowsazure.mediaservices/) 의 현재 버전은 3.1.0.0입니다.
* 업그레이드 hello.Net SDK 종속성 too.NET 4.5 프레임 워크입니다.
* Tooupdate 인코딩 예약된 단위 수 있는 새로운 API를 추가 합니다. 자세한 내용은 [.NET을 사용하여 예약 단위 유형 업데이트 및 증가 인코딩 RU 증가](media-services-dotnet-encoding-units.md)를 참조하세요.
* 노큰 인증을 위한 JWT(JSON 웹 토큰) 지원이 추가되었습니다. 자세한 내용은 [Azure 미디어 서비스 및 동적 암호화의 JWT 토큰 인증](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)을 참조하세요.
* 추가 된 용 상대 오프셋이 BeginDate 및 ExpirationDate hello PlayReady 라이선스 템플릿에 있습니다.

## <a id="november_changes_14"></a>2014년 11월 릴리스
* 미디어 서비스 이제 하면는 라이브 부드러운 스트리밍 (FMP4) 콘텐츠 tooingest SSL 연결을 통해. SSL 통해 tooingest 수집 URL tooHTTPS 있는지 tooupdate hello를 확인 합니다.  현재 AMS는 사용자 지정 도메인을 사용하는 SSL을 지원하지 않습니다.  라이브 스트리밍에 대한 자세한 내용은 [Azure Media Services 라이브 스트리밍 사용]을 참조하세요.
* 현재 SSL 연결을 통해 RTMP 라이브 스트림을 수집할 수 없습니다.
* 스트리밍 끝점 콘텐츠를 배달 하는 hello 2014 년 9 월 10 일 이후에 만들어진 경우에 SSL을 통해 스트리밍할 수 있습니다. 스트리밍 Url hello 스트리밍 채널 9 월 10 일 이후에 작성을 기반으로 하는 경우 hello URL "streaming.mediaservices.windows.net" (새 형식 hello)를 포함 합니다. "Origin.mediaservices.windows.net" (이전 형식 hello)를 포함 하는 스트리밍 Url에서 SSL을 지원 하지 않습니다. Hello 이전 형식으로 프로그램 URL이 고 SSL을 통해 toobe 수 toostream를 원하는 경우 [새 스트리밍 끝점 만들기](media-services-portal-manage-streaming-endpoints.md)합니다. 새 SSL을 통해 끝점 toostream 콘텐츠 스트리밍 hello를 기반으로 작성 된 Url을 사용 합니다.

## <a id="october_changes_14"></a>2014년 10월 릴리스
### <a id="new_encoder_release"></a>미디어 서비스 인코더 릴리스
미디어 서비스 Azure 미디어 인코더의 hello 새 릴리스를 발표합니다. Hello로만 대 한 요금이 청구 최신 Azure 미디어 인코더 출력 Gb에 하지만 그 외에 새 인코더 hello hello 이전 인코더와 호환 되는 기능입니다. 자세한 내용은 [미디어 서비스 가격 정보]를 참조하세요.

### <a id="oct_sdk"></a>미디어 서비스 .NET SDK
이제 .NET용 미디어 서비스 SDK 확장의 버전이 2.0.0.3입니다.

이제 .NET용 미디어 서비스 SDK의 버전이 3.0.0.8입니다.

변경 내용을 따라 hello 만들 수 있습니다.

* 재시도 정책 클래스에서 리팩터링합니다.
* 사용자 에이전트 문자열 toohttp 요청 헤더를 추가 합니다.
* Nuget 복원 빌드 단계를 추가합니다.
* 리포지토리에서 시나리오 테스트 toouse x509 인증서를 수정 합니다.
* 채널 및 스트리밍 끝점을 업데이트할 때 설정의 유효성을 감사합니다.

### <a name="new-github-repository-toohost-media-services-samples"></a>새 GitHub 리포지토리 toohost 미디어 서비스 샘플
샘플은 [Azure 미디어 서비스 샘플 GitHub 리포지토리](https://github.com/Azure/Azure-Media-Services-Samples)에 있습니다.

## <a id="september_changes_14"></a>2014년 9월 릴리스
이제 미디어 서비스 REST 메타데이터의 버전이 2.7입니다. Hello 최신 REST 업데이트에 대 한 자세한 내용은 참조 [Azure 미디어 서비스 REST API 참조]합니다.

이제 .NET용 미디어 서비스 SDK의 버전이 3.0.0.7입니다.

### <a id="sept_14_breaking_changes"></a>주요 변경 내용
* **Origin** 너무 이름이 바뀐[StreamingEndpoint]합니다.
* Hello를 사용 하는 경우 hello 기본 동작이 변경 **Azure 포털** tooencode MP4 파일을 게시 합니다.

이전에 Azure 클래식 포털 toopublish hello를 사용 하는 경우 단일 파일 MP4 비디오 자산 SAS URL 생성 되기 (SAS Url을 허용 하면 toodownload hello blob 저장소에서 비디오). 현재, Azure 클래식 포털 tooencode hello를 사용 하 고 다음 단일 파일 MP4 비디오 자산을 게시 하는 경우 hello URL 포인트 tooan Azure 미디어 서비스 스트리밍 끝점을 생성 합니다.  이 변경 직접 업로드 tooMedia 서비스 되 고 Azure 미디어 서비스에서 인코딩하지 않고 게시는 MP4 비디오에 영향을 주지 않습니다.

현재 다음 두 가지 옵션 toosolve hello 문제 hello를 해야 합니다.

* 스트리밍 단위를 사용 하도록 설정 하 고 부드러운 스트리밍 프레젠테이션으로 동적 패키징 toostream hello.mp4 자산을 사용 합니다.
* SAS url toodownload (만들거나 점진적으로 재생) hello.mp4 합니다. 방법에 대 한 자세한 내용은 toocreate SAS 로케이터 참조 [콘텐츠 배달]합니다.

### <a id="sept_14_GA_changes"></a>GA 릴리스에 포함된 새 기능/시나리오
* **인덱서 미디어 프로세서**. 자세한 내용은 [Azure 미디어 인덱서를 사용하여 미디어 파일 인덱싱]을 참조하세요.
* hello [StreamingEndpoint] 엔터티 이제 하면 tooadd (호스트) 사용자 지정 도메인 이름입니다.
  
    Hello 미디어 서비스 스트리밍 끝점 이름으로 사용 되는 사용자 지정 도메인 이름 toobe tooadd 사용자 지정 호스트 이름을 tooyour 스트리밍 끝점 필요 합니다. Hello 미디어 서비스 REST Api 또는.NET SDK tooadd 사용자 지정 호스트 이름을 사용 합니다.
  
    hello 고려 사항에 따라 적용 됩니다.
  
  * Hello 사용자 지정 도메인 이름의 소유권 hello 있어야 합니다.
  * Azure 미디어 서비스 hello 도메인 이름의 hello 소유권을 확인 해야 합니다. toovalidate hello 도메인을 매핑하는 CName을 만들어야 <MediaServicesAccountId>합니다.<parent domain> tooverifydns입니다. < mediaservices dns 영역 >. 
  * Hello 사용자 지정 호스트 이름 (예를 들어 sports.contoso.com) tooyour 미디어 서비스 StreamingEndpont의 호스트 이름 (예를 들어 amstest.streaming.mediaservices.windows.net) 매핑되는 다른 CName을 만들어야 합니다.

    자세한 내용은 참조 hello **CustomHostNames** hello에 대 한 속성 [StreamingEndpoint] 항목입니다.

### <a id="sept_14_preview_changes"></a>Hello 공개 미리 보기 릴리스의 일부인 새 기능/시나리오
* 라이브 스트리밍 미리 보기. 자세한 내용은 [Azure Media Services 라이브 스트리밍 사용]을 참조하세요.
* 키 전달 서비스. 자세한 내용은 [AES-128 동적 암호화 및 키 전달 서비스 사용]을 참조하세요.
* AES 동적 암호화. 자세한 내용은 [AES-128 동적 암호화 및 키 전달 서비스 사용]을 참조하세요.
* PlayReady License Delivery 서비스. 자세한 내용은 [PlayReady 동적 암호화 및 License Delivery 서비스 사용]을 참조하세요.
* PlayReady 동적 암호화. 자세한 내용은 [PlayReady 동적 암호화 및 License Delivery 서비스 사용]을 참조하세요.
* 미디어 서비스 PlayReady 라이선스 템플릿. 자세한 정보는 [미디어 서비스 PlayReady 라이선스 템플릿 개요]를 참조하세요.
* 저장소에서 암호화된 자산 스트리밍. 자세한 내용은 [저장소에서 암호화된 콘텐츠 스트리밍]를 참조하세요.

## <a id="august_changes_14"></a>2014년 8월 릴리스
자산을 인코딩하는 경우 hello 인코딩 작업 완료 시 출력 자산이 생성 됩니다. 이번 릴리스까지 Azure 미디어 서비스 인코더는 출력 자산에 대한 메타데이터를 생성했습니다. 이 릴리스 hello 인코더 부터는 입력된 자산에 대 한 메타 데이터도 생성 합니다. 자세한 내용은 참조 hello [입력 메타 데이터] 및 [출력 메타 데이터] 항목입니다.

## <a id="july_changes_14"></a>2014년 7월 릴리스
버그 수정 다음 hello hello에 대 한 Azure 미디어 서비스 패키지 작성 도구 및 암호기:

* 라이브 보관 자산 tooHTTP 트랜스 먹 싱 라이브 스트리밍 –이 문제는 수정 된 하 고, 이제 오디오와 비디오가 재생 되 때 오디오만 재생 됨.
* 자산 tooHTTP 라이브 스트리밍 및 AES 128 비트 봉투 암호화를 패키지할 때 hello 패키지 스트림이 재생 되지 않는 Android 장치에서 –이 버그는 수정 하 고 Android 장치를 지 원하는 HTTP 라이브 스트리밍에 hello 패키지 스트림이 재생 합니다.

## <a id="may_changes_14"></a>2014년 5월 릴리스
### <a id="may_14_changes"></a>일반 미디어 서비스 업데이트
이제 사용할 수 있습니다 [동적 패키징] toostream HTTP 라이브 스트리밍 (HLS) v3 합니다. toostream HLS v3 hello 형식 toohello 원래 로케이터 경로 따라 추가: *.ism/manifest(format=m3u8-aapl-v3) 합니다. 자세한 내용은 [Nick Drouin의 블로그]를 참조하세요.

이제 동적 패키징에서는 PlayReady를 통해 정적으로 암호화된 부드러운 스트리밍을 기반으로 하여 PlayReady로 암호화된 HLS(v3 및 v4)도 배달할 수 있습니다. 방법에 대 한 PlayReady로 부드러운 스트리밍을 tooencrypt 참조 [PlayReady로 부드러운 스트림을 보호]합니다.

### <a name="may_14_donnet_changes"></a>미디어 서비스 .NET SDK 업데이트
향상 된 기능을 수행 하는 hello 미디어 서비스.NET SDK 3.0.0.5 릴리스에서 hello에 포함 됩니다.

* 미디어 자산을 업로드하거나 다운로드할 경우 속도와 복원력이 향상되었습니다.
* 다시 시도 논리와 일시적 예외 처리 시 다음이 향상되었습니다. 
  
  * 쿼리, 변경 내용 저장, 파일 업로드 또는 다운로드로 인해 발생한 예외의 경우 일시적인 오류 감지 및 다시 시도 논리가 향상되었습니다. 
  * 웹 예외(예: ACS 토큰 요청 중)가 발생할 경우 치명적인 오류가 급속도로 사라집니다.

자세한 내용은 참조 [hello Media Services SDK for.NET에에서 다시 시도 논리]합니다.

## <a id="april_changes_14"></a>2014년 4월 인코더 릴리스
### <a name="april_14_enocer_changes"></a>미디어 서비스 인코더 업데이트
* Grass Valley HQ/HQX 코덱을 사용 하 여 압축 하는 비디오 hello lightly는 hello Grass Valley EDIUS 비선형 편집기를 사용 하 여 제작 된 AVI 파일 수집 하는 방법에 대 한 지원이 추가 되었습니다. 자세한 내용은 참조 [Grass Valley 알림 EDIUS 7 스트리밍 통해 hello 클라우드]합니다.
* Hello hello 미디어 인코더에서 생성 된 hello 파일에 대 한 명명 규칙을 지정 하기 위한 지원이 추가 되었습니다. 자세한 내용은 [미디어 서비스 인코더 출력 파일 이름 제어]를 참조하세요.
* 비디오 및/또는 오디오 오버레이에 대한 지원이 추가되었습니다. 자세한 내용은 [오버레이 만들기]를 참조하세요.
* 여러 비디오 세그먼트를 함께 연결하는 데 대한 지원이 추가되었습니다. 자세한 내용은 [비디오 세그먼트 연결]을 참조하세요.
* 관련 버그가 수정 tootranscoding mpeg-1 Audio layer 3 (오디오가 MP3)으로 인코딩된 hello 오디오를 mp4입니다.

## <a id="jan_feb_changes_14"></a>2014년 1월/2월 릴리스
### <a name="jan_fab_14_donnet_changes"></a>Azure 미디어 서비스 .NET SDK 3.0.0.1, 3.0.0.2 및 3.0.0.3
3.0.0.1 및 3.0.0.2의 hello 변경은 다음과 같습니다.

* 고정된 문제 관련 toousage OrderBy 문 통한 LINQ 쿼리 됩니다.
* [GitHub] 의 테스트 솔루션이 단위 기반 테스트와 시나리오 기반 테스트로 분할되었습니다.

Hello 변경에 대 한 자세한 내용은 참조 하세요.: [Azure 미디어 서비스.NET SDK 3.0.0.1 및 3.0.0.2 릴리스]합니다.

변경 내용을 따라 hello 3.0.0.3에서 만들 수 있습니다.

* Azure 저장소 종속성 toouse 버전 3.0.3.0을 업그레이드 합니다. 
* 3에 게시해 주세요.0에 게시해 주세요.*에 게시해 주세요.* 릴리스에 대한 이전 버전과의 호환성 문제가 해결되었습니다. 

## <a id="december_changes_13"></a>2013년 12월 릴리스
### <a name="dec_13_donnet_changes"></a>Azure 미디어 서비스 .NET SDK 3.0.0.0
> [!NOTE]
> 3.0.x.x 릴리스는 이전 버전인 2.4.x.x 릴리스와 호환되지 않습니다.
> 
> 

hello 최신 hello Media Services SDK 버전 3.0.0.0 되었습니다. Nuget에서 hello 최신 패키지를 다운로드 하거나 hello 비트를 가져올 수 있습니다 [GitHub]합니다.

Hello 미디어 서비스 SDK 버전 3.0.0.0 부터는 다시 사용할 수 있습니다 hello [Azure Active Directory 액세스 제어 서비스 (ACS)] 토큰입니다. 자세한 내용은 hello "재사용 액세스 제어 서비스 토큰"을 참조 하십시오. hello 섹션인 [.NET 용 미디어 서비스 SDK hello로 tooMedia 서비스를 연결] 항목입니다.

### <a name="dec_13_donnet_ext_changes"></a>Azure 미디어 서비스 .NET SDK 확장 2.0.0.0
hello Azure 미디어 서비스.NET SDK Extensions는 일련의 확장 메서드와 도우미 함수 코드를 단순화 하 고 Azure 미디어 서비스와 함께 보다 쉽게 toodevelop를 확인 합니다. Hello에서 최신 파일을 가져올 수 있습니다 [Azure 미디어 서비스.NET SDK Extensions]합니다.

## <a id="november_changes_13"></a>2013년 11월 릴리스
### <a name="nov_13_donnet_changes"></a>Azure 미디어 서비스 .NET SDK 변경 내용
이 버전 부터는 hello Media Services SDK for.NET 호출 toohello 미디어 서비스 REST API 계층을 만들 때 발생할 수 있는 일시적인 오류를 처리 합니다.

## <a id="august_changes_13"></a>2013년 8월 릴리스
### <a name="aug_13_powershell_changes"></a>Azure SDK 도구에 포함된 미디어 서비스 PowerShell cmdlet
이제 미디어 서비스 PowerShell cmdlet을 다음 hello에 포함 되므로 [azure sdk-도구]합니다.

* Get-AzureMediaServices 
  
    예: `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    예: `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    예: `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    예: `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>2013년 6월 릴리스
### <a name="june_13_general_changes"></a>Azure 미디어 서비스 변경 내용
이 섹션에 설명 된 hello 변경 내용은 2013 년 6 월 미디어 서비스를 해제 하는 hello에 포함 된 업데이트입니다.

* 기능 toolink 여러 저장소 계정을 tooa 미디어 서비스 계정. 
  
    StorageAccount
  
    Asset.StorageAccountName 및 Asset.StorageAccount
* 기능 tooupdate Job.Priority 합니다. 
* 알림 관련 엔터티 및 속성: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    작업
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Azure 미디어 서비스 .NET SDK 변경 내용
hello 다음과 같은 변경 내용이 포함 되어 2013 년 6 월 미디어 서비스 SDK를 해제 합니다. hello 최신 미디어 서비스 SDK는 GitHub에서 사용할 수 있습니다.

* Hello 버전 2.3.0.0 Media Services SDK 지원 여러 저장소 계정을 tooa 미디어 서비스 계정에 연결 하는 hello로 시작 합니다. hello 다음 Api이이 기능을 지원 합니다.
  
    hello IStorageAccount 유형입니다.
  
    hello Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts 속성입니다.
  
    hello StorageAccount 속성입니다.
  
    hello StorageAccountName 속성입니다.
  
    자세한 내용은 [여러 저장소 계정에서 미디어 서비스 자산 관리]를 참조하세요.
* 알림 관련 API. Hello 버전 2.2.0.0 hello 기능 toolisten tooAzure 큐 저장소 알림이 있는로 시작 합니다. 자세한 내용은 [미디어 서비스 작업 알림 처리]를 참조하세요.
  
    hello Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions 속성입니다.
  
    hello Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint 유형입니다.
  
    hello Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription 유형입니다.
  
    hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection 유형입니다.
  
    hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType 유형입니다.
  
    hello Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState 유형입니다.
* Azure 저장소 클라이언트 SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll) hello에 종속성이 있습니다.
* OData 5.5(Microsoft.Data.OData.dll)에 대한 종속성

## <a id="december_changes_12"></a>2012년 12월 릴리스
### <a name="dec_12_dotnet_changes"></a>Azure 미디어 서비스 .NET SDK 변경 내용
* Intellisense: 다양한 유형의 누락된 Intellisense 설명서가 추가되었습니다.
* Microsoft.Practices.TransientFaultHandling.Core: hello SDK 여전히에이 어셈블리의 종속성 tooan 이전 버전 문제를 해결 합니다. SDK 이제 참조 5.1.1209.1이이 어셈블리의 버전 번호입니다.

2012 년 11 월 SDK hello에서 발견 된 문제를 해결 합니다.

* IAsset.Locators.Count: 이제 모든 로케이터가 삭제된 후 이 수가 새로운 IAsset 인터페이스에서 올바르게 보고됩니다.
* IAssetFile.ContentFileSize: 이제 IAssetFile.Upload(filepath)로 업로드한 후 이 값이 올바르게 설정됩니다.
* IAssetFile.ContentFileSize: 이제 자산 파일을 만들 때 이 속성을 설정할 수 있습니다. 이전에는 이 속성이 읽기 전용이었습니다.
* Iassetfile.upload (filepath):이 동기식 업로드 메서드가 여러 파일 toohello 자산을 업로드 하는 경우 다음 오류가 hello를 발생 된 문제를 해결 합니다. hello 오류는 "서버 tooauthenticate hello 요청을 실패 했습니다. 있는지 확인 올바르게 hello 서명을 포함 하 여 권한 부여 헤더의 hello 값 형성 됩니다. "
* IAssetFile.UploadAsync: 5개가 넘는 파일을 동시에 업로드할 수 없는 문제를 해결합니다.
* IAssetFile.UploadProgressChanged:이 이벤트는 이제 hello SDK 통해 제공 됩니다.
* IAssetFile.DownloadAsync(string, BlobTransferClient, ILocator, CancellationToken): 이제 이 메서드 오버로드가 제공됩니다.
* IAssetFile.DownloadAsync: 5개가 넘는 파일을 동시에 다운로드할 수 없는 문제를 해결합니다.
* Iassetfile.delete (): 여기서 delete를 호출 하면 예외가 throw IAssetFile hello에 대 한 업로드 된 파일이 없는 경우 문제를 해결 합니다.
* 작업: 문제가 해결 여기서 "MP4 tooSmooth 스트림 작업"는 "PlayReady Protection 작업" 작업 서식 파일을 사용 하 여 체인을 만들지 않습니다 작업 전혀.
* Encryptionutils.getcertificatefromstore ():이 방법을 더 이상 인증서 구성 문제를 기반으로 하는 hello 인증서를 찾지 못하여 tooa 발생 인해 null 참조 예외를 throw 합니다.

## <a id="november_changes_12"></a>2012년 11월 릴리스
hello이 섹션에 언급 된 변경 내용에에서 포함 된 업데이트 hello 2012 년 11 월 (버전 2.0.0.0) SDK입니다. 이러한 변경에는 hello 2012 년 6 월 미리 보기 SDK 릴리스 toobe 수정 하거나 다시 작성에서 작성 된 코드를 할 수 있습니다.

* 자산
  
    Iasset.create (assetname) hello 유일한 자산 작성 함수입니다. IAsset.Create는 더 이상 hello 메서드 호출의 일부로 파일을 업로드합니다. IAssetFile을 사용하여 업로드합니다.
  
    hello 서비스 SDK에서에서 IAsset.Publish 메서드와 AssetState.Publish 열거 값이 hello hello 제거 되었습니다. 이 값을 기반으로 하는 모든 코드를 다시 작성해야 합니다.
* FileInfo
  
    이 클래스는 제거되었으며 IAssetFile로 바뀌었습니다.
  
    IAssetFiles
  
    IAssetFile은 FileInfo를 대체하며 동작이 다릅니다. toouse, hello IAssetFiles 개체를 인스턴스화할 미디어 서비스 SDK 또는 Azure 저장소 SDK hello hello를 사용 하 여 뒤에 여 파일을 업로드 합니다. IAssetFile.Upload 오버 로드를 수행 하는 hello는 사용할 수 있습니다.
  
  * Iassetfile.upload (filepath): 하는 동기 메서드 hello 스레드를 차단 하며 단일 파일을 업로드 하는 경우에 권장 됩니다.
  * IAssetFile.UploadAsync(filePath, blobTransferClient, locator, cancellationToken): 비동기 메서드로, 기본 설정 hello 업로드 메커니즘입니다. 
    
    알려진된 버그: hello cancellationToken을 사용 하 여 hello 업로드; 실제로 취소 됩니다 그러나 hello 작업의 취소 상태가 hello 여러 상태 중 하나일 수 있습니다. 예외를 올바르게 파악하여 처리해야 합니다.
* 로케이터
  
    hello 원본 관련 버전이 제거 되었습니다. SAS 관련 hello 컨텍스트입니다. 사용 되지 않는, 나 여 ga에 있습니다. 제거 Locators.CreateSasLocator (asset, accessPolicy) 표시 됩니다. Hello 로케이터를 참조 하십시오. 업데이트 된 동작에 대 한 새 기능 아래의 섹션.

## <a id="june_changes_12"></a>2012년 6월 미리 보기 릴리스
기능을 수행 하는 hello hello SDK의 hello 년 11 월 릴리스의 새로운 했습니다.

* 엔터티 삭제
  
    IAsset, IAssetFile, ILocator, IAccessPolicy, IContentKey 개체가 삭제 되었습니다 컬렉션 hello에 나 가지 않고도 IObject.Delete() 즉, hello 개체 수준 이제 삭제 됩니다.
* 로케이터
  
    로케이터는 이제 hello CreateLocator 메서드를 사용 하 여 만들고 hello 하며 LocatorType.SAS 또는 LocatorType.OnDemandOrigin 열거 값을 사용 하 여 특정 유형의 로케이터를 hello에 대 한 인수로 서 toocreate 경우가 있습니다.
  
    새 속성 tooLocators toomake 추가 된 것 보다 쉽게 tooobtain 콘텐츠에 사용할 수 있는 Uri입니다. 이 로케이터를 새롭게이 디자인 된 tooprovide 더 많은 유연성이 다음 버전의 공급 업체 확장에 대 한 하며 모든 미디어 클라이언트 응용 프로그램에 대 한 사용 편의성을 향상 합니다.
* 비동기 메서드 지원
  
    Tooall 메서드에 비동기 지원이 추가 되었습니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Azure 미디어 서비스 MSDN 포럼]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[Azure 미디어 서비스 REST API 참조]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[미디어 서비스 가격 정보]: http://azure.microsoft.com/pricing/details/media-services/
[입력 메타 데이터]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[출력 메타 데이터]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[콘텐츠 배달]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[Azure 미디어 인덱서를 사용하여 미디어 파일 인덱싱]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[Azure Media Services 라이브 스트리밍 사용]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[AES-128 동적 암호화 및 키 전달 서비스 사용]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[PlayReady 동적 암호화 및 License Delivery 서비스 사용]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[미디어 서비스 PlayReady 라이선스 템플릿 개요]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[저장소에서 암호화된 콘텐츠 스트리밍]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[동적 패키징]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[Nick Drouin의 블로그]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[PlayReady로 부드러운 스트림을 보호]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[hello Media Services SDK for.NET에에서 다시 시도 논리]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[Grass Valley 알림 EDIUS 7 스트리밍 통해 hello 클라우드]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[미디어 서비스 인코더 출력 파일 이름 제어]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[오버레이 만들기]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[비디오 세그먼트 연결]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[Azure 미디어 서비스.NET SDK 3.0.0.1 및 3.0.0.2 릴리스]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory 액세스 제어 서비스 (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[.NET 용 미디어 서비스 SDK hello로 tooMedia 서비스를 연결]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[Azure 미디어 서비스.NET SDK Extensions]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure sdk-도구]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[여러 저장소 계정에서 미디어 서비스 자산 관리]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[미디어 서비스 작업 알림 처리]: http://msdn.microsoft.com/library/azure/dn261241.aspx

