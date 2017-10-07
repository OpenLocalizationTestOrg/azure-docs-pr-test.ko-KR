---
title: "Azure 미디어 서비스를 사용 하 여 DRM 하위 시스템의 aaaHybrid 디자인 | Microsoft Docs"
description: "이 항목에서는 Azure Media Services를 사용하는 DRM 하위 시스템의 하이브리드 디자인에 대해 설명합니다."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a>DRM 하위 시스템의 하이브리드 디자인

이 항목에서는 Azure Media Services를 사용하는 DRM 하위 시스템의 하이브리드 디자인에 대해 설명합니다.

## <a name="overview"></a>개요

Azure 미디어 서비스에는 다음 세 가지 DRM 시스템 hello에 대 한 지원을 제공 합니다.

* PlayReady
* Widevine(모듈)
* FairPlay

hello DRM 지원 브라우저 플레이어 SDK로 모든 3 DRMs를 지 원하는 Azure Media player DRM 암호화 (동적 암호화) 및 라이선스 배달에 포함 됩니다.

DRM/CENC 하위 시스템 디자인 및 구현 세부 처리로 라는 hello 문서를 참조 하십시오 [다중 DRM 및 액세스 제어 CENC](media-services-cenc-with-multidrm-access-control.md)합니다.

하지만 세 가지 DRM 시스템에 대 한 전체 지원 제공, 경우에 따라 고객 할 필요는 toouse 자신의 인프라/하위 시스템에 추가 tooAzure 미디어 서비스 toobuild 하이브리드 DRM 하위 시스템의 다양 한 부분입니다.

고객이 묻는 몇 가지 일반적인 질문은 다음과 같습니다.

* "나만의 DRM 라이선스 서버를 사용할 수 있습니까?" (이 경우 고객은 비즈니스 논리가 포함된 DRM 라이선스 서버 팜에 투자했습니다.)
* "AMS(Azure Media Services) 콘텐츠를 호스팅하지 않고 AMS에서 DRM 라이선스 배달만 사용할 수 있습니까?"

## <a name="modularity-of-hello-ams-drm-platform"></a>Hello AMS DRM 플랫폼의 모듈성

포괄적인 클라우드 비디오 플랫폼의 일부인 Azure Media Services DRM은 유연성과 모듈성을 고려하여 설계되었습니다. 다음 (hello 테이블에 사용 되는 hello 표기법에 대 한 설명을 따릅니다) hello 테이블에 설명 된 다양 한 조합을 hello를 사용 하 여 Azure 미디어 서비스를 사용할 수 있습니다. 

|**콘텐츠 호스팅 및 원본**|**콘텐츠 암호화**|**DRM 라이선스 배달**|
|---|---|---|
|AMS|AMS|AMS|
|AMS|AMS|타사|
|AMS|타사|AMS|
|AMS|타사|타사|
|타사|타사|AMS|

### <a name="content-hosting--origin"></a>콘텐츠 호스팅 및 원본

* AMS: AMS에서 비디오 자산을 호스팅하고, AMS 스트리밍 끝점을 통해 스트리밍합니다(반드시 동적 패키징일 필요는 없음).
* 타사: AMS 외부의 타사 스트리밍 플랫폼에서 비디오를 호스팅하고 배달합니다.

### <a name="content-encryption"></a>콘텐츠 암호화

* AMS: AMS 동적 암호화를 통해 동적으로/요청 시 콘텐츠 암호화를 수행합니다.
* 타사: AMS 외부에서 사전 처리 워크플로를 통해 콘텐츠 암호화를 수행합니다.

### <a name="drm-license-delivery"></a>DRM 라이선스 배달

* AMS: AMS 라이선스 배달 서비스를 통해 DRM 라이선스를 배달합니다.
* 타사: AMS 외부의 타사 DRM 라이선스 서버에서 DRM 라이선스를 배달합니다.

## <a name="configure-based-on-your-hybrid-scenario"></a>하이브리드 시나리오에 따른 구성

### <a name="content-key"></a>콘텐츠 키

콘텐츠 키의 구성을 통해 hello 다음 AMS 동적 암호화와 AMS 라이선스 배달 서비스의 특성을 제어할 수 있습니다.

* 동적 DRM 암호화에 사용 되는 hello 콘텐츠 키입니다.
* DRM 라이선스 콘텐츠 toobe 라이선스 배달 서비스에서 전달한: 권한, 콘텐츠 키 및 제한 합니다.
* **콘텐츠 키 인증 정책 제한** 유형: 공개, IP 또는 토큰 제한
* 경우 **토큰** 유형의 **콘텐츠 키 권한 부여 정책 제한은 사용**, hello **콘텐츠 키 권한 부여 정책 제한** 라이선스를 발급 하기 전에 충족 해야 합니다.

### <a name="asset-delivery-policy"></a>자산 배달 정책

자산 배달 정책 구성을 통해 사용 되는 특성 AMS 동적 packager는 AMS 스트리밍 끝점의 동적 암호화를 수행 하는 hello를 제어할 수 있습니다.

* CENC(PlayReady 및 Widevine)에서 DASH, PlayReady에서 부드러운 스트리밍, Widevine 또는 PlayReady에서 HLS와 같은 스트리밍 프로토콜 및 DRM 암호화의 조합
* 각 hello에 대 한 라이선스 배달 Url 기본/포함 hello DRMs에 관련 되었습니다.
* DASH MPD 또는 HLS 재생 목록의 라이선스 획득 URL(LA_URL)에서 Widevine 및 FairPlay 각각에 대한 키 ID(KID) 쿼리 문자열을 포함하는지 여부

## <a name="scenarios-and-samples"></a>시나리오 및 샘플

Hello 이전 단원의 hello 설명에 따라, hello 다음 5 개의 하이브리드 시나리오 사용 하 여 해당 **콘텐츠 키**-**자산 배달 정책** 구성 조합은 (hello hello 마지막 열에 언급 된 샘플 다음과 hello 테이블).

|**콘텐츠 호스팅 및 원본**|**DRM 암호화**|**DRM 라이선스 배달**|**콘텐츠 키 구성**|**자산 배달 정책 구성**|**샘플**|
|---|---|---|---|---|---|
|AMS|AMS|AMS|예|예|샘플 1|
|AMS|AMS|타사|예|예|샘플 2|
|AMS|타사|AMS|예|아니요|샘플 3|
|AMS|타사|외부|아니요|아니요|샘플 4|
|타사|타사|AMS|예|아니요|    

Hello 샘플에서 PlayReady 보호 대시 및 부드러운 스트리밍에 대 한 작동 합니다. 아래 hello 비디오 Url은 부드러운 스트리밍 Url입니다. tooget hello 해당 DASH Url, 추가 "(형식 = mpd-시간-csf)"입니다. Hello를 사용할 수 있습니다 [azure 미디어 플레이어 테스트](http://aka.ms/amtest) 브라우저에서 tootest 합니다. Tooconfigure 수 있는 기술에서 프로토콜 toouse 스트리밍입니다. Windows 10의 IE11 및 MS Edge는 EME를 통해 PlayReady를 지원합니다. 자세한 내용은 참조 [hello에 대 한 세부 정보 도구를 테스트할](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/)합니다.

### <a name="sample-1"></a>샘플 1

* 원본(기본) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest 
* PlayReady LA_URL(DASH 및 부드러운 스트리밍): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 
* Widevine LA_URL(DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4 
* FairPlay LA_URL(HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8 

### <a name="sample-2"></a>샘플 2

* 원본(기본) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest 
* PlayReady LA_URL(DASH 및 부드러운 스트리밍): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx 

### <a name="sample-3"></a>샘플 3

* 원본 URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest 
* PlayReady LA_URL(DASH 및 부드러운 스트리밍): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 

### <a name="sample-4"></a>샘플 4

* 원본 URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest 
* PlayReady LA_URL(DASH 및 부드러운 스트리밍): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx 

## <a name="summary"></a>요약

요약하면 Azure Media Services DRM 구성 요소는 유연합니다. 이 항목에서 설명한 대로 콘텐츠 키와 자산 배달 정책을 올바르게 구성하여 하이브리드 시나리오에서 이러한 구성 요소를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로 보기.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

