---
title: "미디어 서비스 개념 aaaAzure | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 서비스 개념에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Azure 미디어 서비스 개념
이 항목에서는 hello 가장 중요 한 미디어 서비스 개념의 개요를 제공 합니다.

## <a id="assets"></a>자산 및 저장소
### <a name="assets"></a>자산
[자산](https://docs.microsoft.com/rest/api/media/operations/asset) 디지털 파일 (비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 포함)를 포함 합니다. 이러한 파일에 대 한 메타 데이터를 hello 및 합니다. Hello 디지털 파일을 자산으로 업로드, 후 hello 미디어 서비스 인코딩 및 스트리밍 워크플로에 사용할 수 없습니다.

자산 hello Azure 저장소 계정에서 매핑된 tooa blob 컨테이너 이며 hello 파일 hello 자산에는 해당 컨테이너에 블록 blob으로 저장 됩니다. 페이지 blob은 Azure Media Services에서 지원되지 않습니다.

어떤 미디어 콘텐츠 tooupload 및는 자산에 대 한 저장소 고려 사항에 따라 hello 적용 결정:

* 자산에는 미디어 콘텐츠의 고유한 단일 인스턴스만 포함되어야 합니다. 예를 들어 TV 에피소드, 영화 또는 광고의 단일 편집이 포함됩니다.
* 자산에는 시청각 파일의 변환이나 편집이 여러 개 포함되어서는 안 됩니다. 부적절 한 자산 사용의 한 가지 예로 둘 이상의 TV 프로그램이, 광고 또는 여러 카메라 각도에서 자산에 대 한 단일 제작물 toostore 시도 합니다. 자산에 여러 변환 또는 자산은 시청각 파일의 편집 저장 인코딩 작업 전송, 스트리밍 및 안전한 hello 워크플로 뒷부분에 나오는 hello 자산의 hello 배달 하는 데 문제가 발생할 수 있습니다.  

### <a name="asset-file"></a>자산 파일
[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 은 Blob 컨테이너에 저장되는 실제 비디오 또는 오디오 파일을 나타냅니다. 자산 파일은 항상 자산과 연결되며 자산에는 하나 이상의 파일이 포함될 수 있습니다. hello 미디어 서비스 인코더 작업에는 자산 파일 개체가 blob 컨테이너의 디지털 파일과 연관 되지 않은 경우 실패 합니다.

hello **AssetFile** 인스턴스와 hello 실제 미디어 파일에는 별개의 두 개체 인스턴스가 있습니다. hello AssetFile 인스턴스 hello 미디어 파일 hello 실제 미디어 콘텐츠가 포함 되어 있지만 hello 미디어 파일에 대 한 메타 데이터를 포함 합니다.

미디어 서비스 Api를 사용 하지 않고 미디어 서비스에 의해 생성 된 blob 컨테이너의 toochange hello 내용을 하지 않아야 합니다.

### <a name="asset-encryption-options"></a>자산 암호화 옵션
Tooupload, 저장소 및 배달 하려는 콘텐츠 hello 유형에 따라, 미디어 서비스에서 선택할 수 있는 다양 한 암호화 옵션을 제공 합니다.

>[!NOTE]
>암호화가 사용되지 않습니다. Hello 기본값입니다. 이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.

Toodeliver MP4 점진적 다운로드를 사용 하 여 하려는 경우이 옵션 tooupload 콘텐츠를 사용 합니다.

**StorageEncrypted** –이 옵션 tooencrypt AES 256 비트 암호화를 사용 하 여 로컬로 되어 있지 않은 콘텐츠를 사용 하 고 암호화 된 상태로 저장 된 저장소 tooAzure 업로드 합니다. 자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다. 강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일 디스크에 놓으면 toosecure를 원하는 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다. 

순서 toodeliver 저장소 암호화 된 자산을 원하는 toodeliver 콘텐츠 미디어 서비스에서 알 수 있도록 hello 자산의 배달 정책을 구성 해야 합니다. 자산을 스트리밍하기 전에 스트리밍 서버 제거 hello 저장소 암호화 및 스트림을 hello를 사용 하 여 콘텐츠 hello 배달 정책 (예를 들어 AES, PlayReady 또는 암호화 안 함)를 지정 합니다. 

**CommonEncryptionProtected** -원하는 tooencrypt (또는 이미 암호화 업로드) 일반 암호화 또는 PlayReady DRM (예를 들어 부드러운 스트리밍 PlayReady DRM으로 보호 된)를 사용 하 여 콘텐츠 경우이 옵션을 사용 합니다.

**EnvelopeEncryptionProtected** – tooprotect (또는 이미 보호 업로드) 하려는 경우이 옵션을 사용 하 여 HTTP 라이브 스트리밍 (HLS) AES로 암호화 된 고급 암호화 표준 (). AES로 이미 암호화된 HLS를 업로드하려는 경우 Transform Manager로 암호화되어 있어야 합니다.

### <a name="access-policy"></a>액세스 정책
[AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) 권한 (예: 읽기, 쓰기 및 목록) 및 액세스 tooan 자산의 기간을 정의 합니다. 일반적으로 AccessPolicy 개체 tooa 로케이터는 자산에 포함 된 사용된 tooaccess hello 파일 수를 전달 합니다.

>[!NOTE]
>다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

### <a name="blob-container"></a>Blob 컨테이너
Blob 컨테이너는 Blob 집합의 그룹화를 제공합니다. Blob 컨테이너는 미디어 서비스에서 액세스 제어의 경계 지점 및 자산에 대한 SAS(공유 액세스 서명)으로 사용됩니다. 한 Azure 저장소 계정에 포함될 수 있는 Blob 컨테이너 수에는 제한이 없습니다. 한 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다.

>[!NOTE]
> 미디어 서비스 Api를 사용 하지 않고 미디어 서비스에 의해 생성 된 blob 컨테이너의 toochange hello 내용을 하지 않아야 합니다.
> 
> 

### <a id="locators"></a>로케이터
[로케이터](https://docs.microsoft.com/rest/api/media/operations/locator)의항목 지점 tooaccess hello 자산에 포함 된 파일을 제공 합니다. 액세스 정책은 사용 되는 toodefine hello 권한 및 자산을 지정 하는 액세스 tooa 클라이언트에 기간입니다. 동일한 사용 권한 및 기간 설정을; hello 서로 다른 여러 로케이터가 다른 시작 시간을 제공할 수 및 사용 하 여 모든 연결 형식을 toodifferent 클라이언트 동안 등을 로케이터 액세스 정책 사용 하 여 여러 tooone 관계를 가질 수 있습니다. 그러나 Azure 저장소 서비스에 의해 설정 된 공유 액세스 정책 제한으로 인해 6 개 이상의 고유한 로케이터는 한 번에 지정된 된 자산과 연관 수는 없습니다. 

미디어 서비스는 두 가지 로케이터 유형을 지원: OnDemandOrigin 로케이터 toostream 미디어 (예를 들어, MPEG DASH, HLS 또는 부드러운 스트리밍)를 사용 하거나 미디어 및 사용 되는 tooupload 또는 다운로드 미디어 파일 to\from Azure 저장소 SAS URL locator를 점진적으로 다운로드 합니다. 

>[!NOTE]
>hello 나열 권한 (AccessPermissions.List) OnDemandOrigin 로케이터를 만들 때 사용할 수 없습니다. 

### <a name="storage-account"></a>저장소 계정
모든 액세스 tooAzure 저장소는 저장소 계정을 통해 수행 됩니다. 미디어 서비스 계정은 하나 이상의 저장소 계정에 연결될 수 있습니다. 전체 크기가 저장소 계정당 500TB를 초과하지 않을 경우 한 계정에 포함될 수 있는 컨테이너 수에는 제한이 없습니다.  미디어 서비스 SDK 수준 tooallow 도구를 제공 하면 toomanage 여러 저장소 계정 및 부하 분산 메트릭 또는 무작위 분산을 기반으로 업로드 toothese 계정 하는 동안 해당 자산의 hello 배포 합니다. 자세한 내용은 [Azure 저장소](https://msdn.microsoft.com/library/azure/dn767951.aspx)작업을 참조하세요. 

## <a name="jobs-and-tasks"></a>작업 및 태스크
A [작업](https://https://docs.microsoft.com/rest/api/media/operations/job) 일반적으로 사용 되는 tooprocess 됩니다 (예를 들어, 인덱스 또는 인코딩할) 오디오/비디오 프레젠테이션을 합니다. 여러 비디오를 처리 하는 경우 인코딩할 각 비디오 toobe에 대 한 작업을 만듭니다.

작업을 수행 하는 hello 처리 toobe에 대 한 메타 데이터를 포함 합니다. 각 작업에는 원자성 처리 태스크, 해당 입력 자산, 출력 자산, 미디어 프로세서 및 관련 설정을 지정하는 하나 이상의 [태스크](https://docs.microsoft.com/rest/api/media/operations/task)가 포함됩니다. 작업 내의 태스크를 서로 연결 될 수 하, 자산 toohello 다음 작업을 입력 한 작업의 출력 자산 hello hello로 지정 된 위치입니다. 이러한 방식으로 하나의 작업이 미디어 프레젠테이션에 필요한 hello 처리의 모든 포함할 수 있습니다.

## <a id="encoding"></a>인코딩
Azure 미디어 서비스는 hello hello 클라우드에 있는 미디어의 인코딩에 대 한 여러 옵션을 제공 합니다.

미디어 서비스 시작, 경우에 중요 한 toounderstand hello 차이 코덱 및 파일 형식이 있습니다.
코덱은 파일 형식은 압축 hello 비디오를 보관 하는 컨테이너는 hello 압축/압축 풀기 알고리즘을 구현 하는 hello 소프트웨어입니다.

미디어 서비스는로 toore 패키지 필요 없이 적응 비트 전송률 MP4 또는 부드러운 스트리밍으로 인코딩 (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 지 원하는 형식 스트리밍을의 콘텐츠 toodeliver 수 있는 동적 패키징을 제공 합니다. 형식 스트리밍을 합니다.

tootake 활용 [동적 패키징](media-services-dynamic-packaging-overview.md), 표준 또는 프리미엄 스트리밍 끝점을 하나 이상 있고 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합으로 tooencode (원본)의 중 2 층 파일을 필요 합니다. 시작 상태입니다.

미디어 서비스 주문형으로 인코더는이 문서에 설명 된 다음 hello를 지원 합니다.

* [미디어 인코더 표준](media-services-encode-asset.md#media-encoder-standard)
* [미디어 인코더 Premium 워크플로](media-services-encode-asset.md#media-encoder-premium-workflow)

지원되는 인코더에 대한 자세한 내용은 [인코더](media-services-encode-asset.md)를 참조하세요

## <a name="live-streaming"></a>라이브 스트리밍
Azure 미디어 서비스에서 채널은 라이브 스트리밍 콘텐츠를 처리하기 위한 파이프라인을 나타냅니다. 채널은 다음 두 가지 방법 중 하나로 라이브 입력 스트림을 받습니다.

* 온-프레미스 라이브 인코더가 다중 비트 전송률 RTMP 또는 부드러운 스트리밍 (조각난 MP4) toohello 채널 보냅니다. Hello 다음 다중 비트 전송률 부드러운 스트리밍 출력 하는 라이브 인코더를 사용할 수 있습니다: MediaExcel, Ateme, 통신 한다고 가정, Envivio, Cisco 및 Elemental 합니다. hello 라이브 인코더 출력: Adobe Flash Live Encoder, Telestream Wirecast, Teradek, Haivision 및 Tricaster 인코더입니다. hello 수집 된 스트림은 채널을 통과 하지 않고 더 이상 코드 변환 및 인코딩. 요청 미디어 서비스는 hello 스트림 toocustomers를 제공 합니다.
* 단일 비트 전송률 스트림을 (hello 다음 형식 중 하나에서: RTP (MPEG-TS)), RTMP 또는 부드러운 스트리밍 (조각난 MP4)) toohello 채널을 미디어 서비스로 인코딩 라이브 tooperform 활성화 보내집니다. hello 채널 다음 라이브 인코딩합니다 hello 들어오는 단일 비트 전송률 스트림 tooa 다중 비트 전송률 (적응) 비디오 스트림으로 합니다. 요청 미디어 서비스는 hello 스트림 toocustomers를 제공 합니다.

### <a name="channel"></a>채널
미디어 서비스에서, [채널](https://docs.microsoft.com/rest/api/media/operations/channel)은 라이브 스트리밍 콘텐츠 처리를 담당합니다. Channel에서 제공 하는 입력된 끝점 (수집 URL) tooa 라이브 코드 변환기를 제공 합니다. hello 채널 hello 라이브 코드 변환기 로부터 라이브 입력된 스트림을 수신 하 고 하나 이상의 Streamingendpoint를 통해 스트리밍에 사용할 수 있게 합니다. 미리 보기 끝점 (미리 보기 URL) toopreview를 사용 하 고 추가 처리 및 배달 하기 전에 스트림을 유효성을 검사 하는 또한 채널을 제공 합니다.

Hello를 얻을 수 hello 채널을 만들 때 URL과 hello 미리 보기 URL을 수집 합니다. tooget 이러한 Url hello 채널이 없는 toobe hello 시작 상태입니다. 준비 toostart hello 채널에 라이브 코드 변환기에서 데이터 푸시의 경우에 hello 채널이 시작 되어야 합니다. 면 hello 라이브 코드 변환기 데이터 수집을 시작 하면 스트림을 미리볼 수 있습니다.

각 미디어 서비스 계정에는 여러 채널, 여러 프로그램 및 여러 StreamingEndpoints가 포함될 수 있습니다. Hello 대역폭 및 보안 요구에 따라 StreamingEndpoint 서비스 전용된 tooone 개 이상의 채널을 수 있습니다. 모든 StreamingEndpoint는 모든 채널에서 가져올 수 있습니다.

### <a name="program-event"></a>프로그램(이벤트)
A [프로그램 (이벤트)](https://docs.microsoft.com/rest/api/media/operations/program) toocontrol hello 게시 및 라이브 스트림의 세그먼트의 저장소를 사용 하면 됩니다. 채널은 프로그램(이벤트)을 관리합니다. hello 채널과 프로그램 관계는 비슷한 tootraditional 미디어 여기서는 채널에 일정 한 콘텐츠 스트림이 하 고 프로그램은 해당 채널의 이벤트 범위가 지정 된 toosome 시간이 초과 되었습니다.
시간을 기록 하는 hello 콘텐츠 tooretain hello 프로그램에 대 한 hello 설정 하 여 hello 수를 지정할 수 **ArchiveWindowLength** 속성입니다. 이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다.

또한 ArchiveWindowLength hello 최대 양을 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 지정 합니다. 프로그램 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다. 또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.

각 프로그램(이벤트)은 자산에 연결됩니다. toopublish hello 프로그램 hello에 대 한 로케이터를 만들어야 합니다 자산에 연결 합니다. 이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL 사용 됩니다.

최대 동시에 실행 중인 프로그램 hello 여러 보관 본을 만들 수 있도록 toothree 채널을 지원 합니다. 동일한 들어오는 스트림을 합니다. 이렇게 하면 필요에 따라 이벤트의 다른 부분 toopublish 및 보관 있습니다. 예를 들어 비즈니스 요구 사항 tooarchive 6 시간의 프로그램에서 나 toobroadcast만 마지막 10 분입니다. tooaccomplish이, 두 개의 동시 실행 프로그램을 toocreate 필요 합니다. 한 프로그램 tooarchive 6 시간의 이벤트 hello 설정 되어 있지만 hello 프로그램 게시 되지 않습니다. hello 다른 프로그램은 집합 tooarchive 10 분 동안 되며이 프로그램이 게시 됩니다.

자세한 내용은 다음을 참조하세요.

* [Live Enabled tooPerform 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)
* [온-프레미스 인코더에서 다중 비트 전송률 라이브 스트림을 받는 채널 작업](media-services-live-streaming-with-onprem-encoders.md)
* [할당량 및 제한 사항](media-services-quotas-and-limitations.md)

## <a name="protecting-content"></a>콘텐츠 보호
### <a name="dynamic-encryption"></a>동적 암호화
Azure 미디어 서비스 미디어를 저장, 처리 및 배달을 통해 컴퓨터를 벗어나 hello 시간 toosecure 있습니다를 사용 합니다. 미디어 서비스 콘텐츠 암호화 표준 AES (고급) (128 비트 암호화 키 사용) 및 PlayReady 및/또는 Widevine DRM을 사용 하 여 일반 암호화 (CENC)를 사용 하 여 동적으로 암호화 toodeliver가 있습니다. 또한 미디어 서비스 PlayReady 라이선스 tooauthorized 클라이언트와 AES 키 배달에 대 한 서비스를 제공 합니다.

현재 다음 스트리밍 형식 hello를 암호화할 수 있습니다: HLS, MPEG DASH, 부드러운 스트리밍 및 합니다. 점진적 다운로드를 암호화할 수 없습니다.

에 대해 원하는 tooencrypt 미디어 서비스 자산, 자산을 사용 하 여 암호화 키 (CommonEncryption 또는 EnvelopeEncryption) tooassociate 필요한 고 hello 키에 대 한 권한 부여 정책을 구성할 수도 있습니다.

순서 toospecify에 hello 자산의 배달 정책을 구성 해야 toostream 저장소 암호화 된 자산을 하려는 경우 원하는 toodeliver 자산입니다.

미디어 서비스는 지정 된 hello 플레이어에서 스트림을 요청 되 면 키 toodynamically (PlayReady Widevine)와 AES) (사용 하 여 봉투 (envelope) 암호화 또는 일반 암호화를 사용 하 여 콘텐츠를 암호화 합니다. toodecrypt hello 스트림 hello 플레이어 hello 키 배달 서비스에서 hello 키를 요청 합니다. hello 사용자가 아닌지 toodecide 권한이 tooget hello 키, hello 서비스 hello 키에 대해 지정한 hello 권한 부여 정책을 평가 합니다.

### <a name="token-restriction"></a>토큰 제한
hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: 열고, 제한, 또는 IP 제한이 토큰입니다. 보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다. 미디어 서비스는 hello 단순 웹 토큰 (SWT) 형식 및 JSON 웹 토큰 (JWT) 형식 토큰을 지원합니다. 미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다. 사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다. hello STS 구성된 toocreate 지정 hello로 토큰에 서명 해야 합니다. 키 클레임을 발급 hello 토큰 제한 구성에 지정 합니다. hello 미디어 서비스 키 배달 서비스는 hello 요청한 키 (또는 라이선스) toohello 클라이언트 hello 토큰이 유효한 경우 및 hello 반환 hello 토큰 일치 항목에 구성 된 hello 키 (또는 라이선스)에 대 한 클레임입니다.

토큰 제한 정책 hello를 구성할 때 hello 기본 확인 키, 발급자 및 대상 매개 변수를 지정 해야 합니다. hello hello 기본 확인 키가 포함 되어 hello 토큰이 서명, 발급자 hello 보안 토큰 서비스 hello 토큰을 발급 하는 키입니다. hello 리소스 hello 토큰에 대 한 액세스 권한을 부여 또는 hello audience (범위 라고도 함) hello 토큰의 hello 의도 설명 합니다. hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.

자세한 내용은 다음 문서는 hello 참조:

[콘텐츠 보호 개요](media-services-content-protection-overview.md)
[AES-128로 보호](media-services-protect-with-aes128.md)
[DRM으로 보호](media-services-protect-with-drm.md)

## <a name="delivering"></a>배달
### <a id="dynamic_packaging"></a>동적 패키징
미디어 서비스를 사용할 때는 설정 것이 좋습니다 중 2 층 파일을 적응 비트 전송률 MP4 집합 전환한 후 hello tooencode hello를 사용 하 여 toohello 원하는 형식 [동적 패키징](media-services-dynamic-packaging-overview.md)합니다.

### <a name="streaming-endpoint"></a>스트리밍 끝점
StreamingEndpoint 직접 tooa 클라이언트 플레이어 응용 프로그램 또는 tooa 네트워크 CDN (콘텐츠 배달) (Azure 미디어 서비스 이제 제공 hello Azure CDN 통합 합니다.) 향후 배포를 위해 콘텐츠를 배달할 수 있는 스트리밍 서비스를 나타내는 hello 스트리밍 끝점 서비스 아웃 바운드 스트림은 라이브 스트림 또는 미디어 서비스 계정에서 비디오 주문형으로 자산 수 있습니다. 미디어 서비스 고객 중 하나를 선택 합니다.는 **표준** 끝점 또는 하나 이상의 스트리밍 **프리미엄** 스트리밍 tootheir 요구에 따라 끝점입니다. 표준 스트리밍 끝점은 대부분의 스트리밍 워크로드에 적합합니다. 

표준 스트리밍 끝점은 대부분의 스트리밍 워크로드에 적합합니다. 표준 스트리밍 끝점 제공 hello 유연성 toodeliver 프로그램 콘텐츠 toovirtually HLS, MPEG DASH, 부드러운 스트리밍에 대 한 동적 패키징에 뿐만 아니라 Microsoft PlayReady, Google Widevine, 사과 Fairplay 동적 암호화를 통해 모든 장치 및 AES128 합니다.  Azure CDN 통합을 통해 동시 뷰어 수천 매우 작은 toovery 큰 대상 그룹에서 또한 확장 합니다. 스트리밍 끝점 처리량 목표 toostandard을 스트리밍 용량 요구 사항을 적용할 수 없는 또는 toocontrol hello 용량의 원하는 또는 고급를 사용 하는 작업이 있는 경우 hello StreamingEndpoint 서비스 toohandle 증가 대역폭 필요, 것이 좋습니다. tooallocate 배율 단위 (라고도 프리미엄 스트리밍 단위)입니다.

Toouse 동적 패키징 및/또는 동적 암호화 것이 좋습니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 

자세한 내용은 [이 항목](media-services-portal-manage-streaming-endpoints.md) 을 참조하세요.

기본적으로 미디어 서비스 계정에서 too2 스트리밍 끝점을 적용 하는 것이 있습니다. 더 높은 한도 toorequest 참조 [할당량 및 제한](media-services-quotas-and-limitations.md)합니다.

스트리밍 끝점이 실행 상태에 있을 때만 청구됩니다.

### <a name="asset-delivery-policy"></a>자산 배달 정책
미디어 서비스 콘텐츠 배달 워크플로 구성 하 고 hello 단계 hello 중 하나 [자산에 대 한 배달 정책을 ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)스트리밍 toobe 되도록 합니다. hello 자산 배달 정책 미디어 서비스 프로그램 자산 toobe 배달에 대해 원하는 방법을 알려 줍니다: 스트리밍 프로토콜에 자산 패키지 되어야 하며 동적으로 (예: MPEG DASH, HLS, 부드러운 스트리밍 또는 모두), 용 toodynamically 원하는 여부 자산 암호화 및 방법 (봉투 (envelope) 또는 일반 암호화) 합니다.

자산 스트리밍하기 전에 저장소 암호화 된 자산을 설정한 경우 hello 서버 제거 hello 저장소 암호화 및 스트림 hello를 사용 하 여 콘텐츠 스트리밍 배달 정책을 지정 합니다. 예를 들어 toodeliver 자산 암호화 표준 AES (고급) 암호화 키로 암호화 된 설정 hello 정책 형식 tooDynamicEnvelopeEncryption 합니다. tooremove 저장소 암호화 및 명확 hello에 스트림 hello 자산 hello 정책 형식 tooNoDynamicEncryption를 설정 합니다.

### <a name="progressive-download"></a>점진적 다운로드
점진적 다운로드 hello 전체 파일이 다운로드 되기 전에 미디어 재생 toostart가 있습니다. MP4 파일만 점진적으로 다운로드할 수 있습니다.

>[!NOTE]
>암호를 해독 해야 암호화 된 자산을 원할 경우 toobe 점진적 다운로드에 사용할 수 있습니다.

tooprovide 사용자를 점진적 다운로드 Url, 먼저 OnDemandOrigin 로케이터를 작성 해야 합니다. 기본 경로 toohello 자산 hello 제공 hello 로케이터를 만드는 중입니다. 그런 다음 MP4 파일의 tooappend hello 이름이 필요 합니다. 예:

http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>스트리밍 URL
프로그램 콘텐츠 tooclients 스트리밍. 스트리밍 Url이 포함 된 사용자가 tooprovide를 먼저 만들어야 OnDemandOrigin 로케이터 합니다. 원하는 toostream hello 콘텐츠를 포함 하는 기본 경로 toohello 자산 hello 제공 hello 로케이터를 만드는 중입니다. 그러나 toobe 수 toostream이 콘텐츠 toomodify 나중에이 경로 필요 합니다. 스트리밍 매니페스트 파일 전체 URL toohello, hello 로케이터 경로 연결 해야 tooconstruct 값과 hello 매니페스트 (filename.ism) 파일 이름입니다. 그런 다음 /Manifest와 적절 한 형식 (필요한 경우) toohello 로케이터 경로 추가 합니다.

SSL 연결을 통해 콘텐츠를 스트리밍할 수도 있습니다. toodo이를 HTTPS로 스트리밍 Url 시작 되었는지 확인 합니다. 현재 AMS는 사용자 지정 도메인을 사용하는 SSL을 지원하지 않습니다.  

>[!NOTE]
>스트리밍 끝점 콘텐츠를 배달 하는 hello 2014 년 9 월 10 일 이후에 만들어진 경우에 SSL을 통해 스트리밍할 수 있습니다. 스트리밍 Url hello 스트리밍 채널 9 월 10 일 이후에 작성을 기반으로 하는 경우 hello URL "streaming.mediaservices.windows.net" (새 형식 hello)를 포함 합니다. "Origin.mediaservices.windows.net" (이전 형식 hello)를 포함 하는 스트리밍 Url에서 SSL을 지원 하지 않습니다. URL이 이전 형식인 hello toobe 수 toostream SSL을 통해 원하는 경우 새 스트리밍 끝점을 만듭니다. 새 SSL을 통해 끝점 toostream 콘텐츠 스트리밍 hello를 기반으로 작성 된 Url을 사용 합니다.

다른 스트리밍 형식에 설명 하 고 예제를 제공 하는 목록 다음 hello:

* 부드러운 스트리밍

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

* MPEG DASH

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

* Apple HLS(HTTP 라이브 스트리밍) V4

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

* Apple HLS(HTTP 라이브 스트리밍) V3

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

