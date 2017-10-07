---
title: "aaaAzure 미디어 서비스 동적 패키징 개요 | Microsoft Docs"
description: "동적 패키징 개요 및 hello 항목 제공 합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>동적 패키징
## <a name="overview"></a>개요
Microsoft Azure 미디어 서비스에 사용 되는 toodeliver 수 많은 미디어 소스 파일 형식, 미디어 스트리밍 형식 및 콘텐츠 보호 형식 tooa 다양 한 클라이언트 기술 (예를 들어 iOS, XBOX, Silverlight, Windows 8). 이러한 클라이언트는 여러 가지 프로토콜을 이해합니다. 예를 들어 iOS에는 HLS(HTTP 라이브 스트리밍) V4 형식이 필요하고 Silverlight와 Xbox에는 부드러운 스트리밍이 필요합니다. 적응 비트 전송률 (다중 비트 전송률) 집합이 있으면 MP4 (ISO 기본 미디어 14496-12) 파일 또는 MPEG DASH, HLS 또는 부드러운 스트리밍을 이해 하는 tooserve tooclients 원하는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 사용 해야 미디어의 서비스 동적 패키징입니다.

하기만 하면 동적 패키징하 toocreate 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합이 포함 된 자산입니다. 그런 다음 hello hello 매니페스트에 지정 된 형식에 따라 또는 요청 조각, 주문형 스트리밍 서버 hello 스트림이 선택한 hello 프로토콜에 수신 하는 방법을 사용 하면 hello 합니다. 결과적으로, toostore 하기만 하면 및 단일 저장소 형식 및 미디어 서비스 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서에서 요청에 따라 hello 적절 한 응답을 제공 합니다.

hello 다음 다이어그램에서는 기존의 인코딩 hello 및 정적 패키징 워크플로

![정적 인코딩](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

hello 다음 다이어그램에서는 hello 동적 패키징 워크플로

![동적 인코딩](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>일반적인 시나리오
1. 입력 파일(mezzanine 파일이라고 함)을 업로드합니다. 예를 들어 H.264, MP4 또는 WMV (지원 되는 형식의 hello 목록에 대 한 참조 [hello 미디어 인코더 표준에서 형식 지원](media-services-media-encoder-standard-formats.md)합니다.
2. 사용자 중 2 층 파일 tooH.264 MP4 적응 비트 전송률 집합을으로 인코딩하십시오.
3. Hello 적응 비트 전송률 MP4 세트 hello 주문형 로케이터를 만들어 포함 된 hello 자산을 게시 합니다.
4. 스트리밍 Url tooaccess hello 빌드하고 콘텐츠를 스트리밍해야 합니다.

## <a name="preparing-assets-for-dynamic-streaming"></a>동적 스트리밍을 위한 자산 준비
tooprepare 자산의 동적 스트리밍 있습니다에 대 한 두 가지 옵션이 있습니다.

1. [마스터 파일을 업로드합니다](media-services-dotnet-upload-files.md).
2. [Hello 미디어 인코더 표준 인코더 tooproduce H.264 MP4 적응 비트 전송률 세트를 사용 하 여](media-services-dotnet-encode-with-media-encoder-standard.md)합니다.
3. [콘텐츠를 스트림합니다](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>동적 패키징에서 지원하지 않는 형식
hello 다음 원본 파일 형식은 지원 되지 않습니다 동적 패키징에서.

* Dolby Digital mp4 파일
* Dolby Digital 부드러운 파일

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

