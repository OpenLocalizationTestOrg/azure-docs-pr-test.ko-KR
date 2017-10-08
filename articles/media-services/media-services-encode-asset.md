---
title: "aaaOverview와 비교에는 azure 미디어 인코더 요청 | Microsoft Docs"
description: "이 항목에서는 Azure 주문형 미디어 인코더를 대략적으로 설명하고 비교한 데이터를 제공합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Azure 주문형 미디어 인코더 개요 및 비교
## <a name="encoding-overview"></a>인코딩 개요
Azure 미디어 서비스는 hello hello 클라우드에 있는 미디어의 인코딩에 대 한 여러 옵션을 제공 합니다.

미디어 서비스 시작, 경우에 중요 한 toounderstand hello 차이 코덱 및 파일 형식이 있습니다.
코덱은 파일 형식은 압축 hello 비디오를 보관 하는 컨테이너는 hello 압축/압축 풀기 알고리즘을 구현 하는 hello 소프트웨어입니다.

미디어 서비스는로 toore 패키지 필요 없이 적응 비트 전송률 MP4 또는 부드러운 스트리밍으로 인코딩 (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 지 원하는 형식 스트리밍을의 콘텐츠 toodeliver 수 있는 동적 패키징을 제공 합니다. 형식 스트리밍을 합니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. tootake 활용 [동적 패키징](media-services-dynamic-packaging-overview.md), toodo hello 다음 해야 합니다.
>
>또한, 일련의 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 (hello 인코딩 단계는이 자습서의 뒷부분에서 설명)로 소스 파일을 암호화 합니다.

미디어 서비스는이 문서에서 설명 하는 요청 시 인코더에 hello 다음을 지원 합니다.

* [미디어 인코더 표준](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium 워크플로](media-services-encode-asset.md#media-encoder-premium-workflow)

이 문서에 간략하게 설명 필요에 따라 미디어 인코더를 제공 하 고 보다 자세한 정보를 제공 하는 링크 tooarticles를 제공 합니다. 또한 hello 항목 hello 인코더의 비교를 제공합니다.

>[!NOTE]
>기본적으로 각 미디어 서비스 계정은 한번에 하나의 인코딩 작업을 활성화할 수 있습니다. 구입한 각 인코딩 예약된 단위에 대 한 동시에 실행할 여러 인코딩 작업 toohave를 허용 하는 인코딩 단위를 예약할 수 있습니다. 자세한 내용은 [인코딩 단위 크기 조정](media-services-scale-media-processing-overview.md)을 참조하세요.

## <a name="media-encoder-standard"></a>미디어 인코더 표준
### <a name="how-toouse"></a>어떻게 toouse
[방식으로 미디어 인코더 표준 tooencode](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>형식
[형식 및 코덱](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>기본 설정
미디어 인코더 표준 구성 된 설명 hello 인코더 사전 설정 중 하나를 사용 하 여 [여기](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)합니다.

### <a name="input-and-output-metadata"></a>입력 및 출력 메타데이터
hello 인코더 입력된 메타 데이터 설명 [여기](media-services-input-metadata-schema.md)합니다.

hello 인코더 출력 메타 데이터 설명 [여기](media-services-output-metadata-schema.md)합니다.

### <a name="generate-thumbnails"></a>미리 보기 생성
정보를 참조 하십시오. [방법을 사용 하 여 미디어 인코더 표준 toogenerate 축소판 그림](media-services-advanced-encoding-with-mes.md#thumbnails)합니다.

### <a name="trim-videos-clipping"></a>비디오 자르기(클리핑)
정보를 참조 하십시오. [방법을 사용 하 여 미디어 인코더 표준 tootrim 비디오](media-services-advanced-encoding-with-mes.md#trim_video)합니다.

### <a name="create-overlays"></a>오버레이 만들기
정보를 참조 하십시오. [방법을 사용 하 여 미디어 인코더 표준 toocreate 오버레이](media-services-advanced-encoding-with-mes.md#overlay)합니다.

### <a name="see-also"></a>참고 항목
[hello 미디어 서비스 블로그](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>미디어 인코더 Premium 워크플로
### <a name="overview"></a>개요
[Azure 미디어 서비스의 프리미엄 인코딩 소개](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>어떻게 toouse
미디어 인코더 Premium 워크플로는 복잡한 워크플로를 사용하여 구성됩니다. 워크플로 파일을 만들 수 및 hello를 사용 하 여 업데이트할 [워크플로 디자이너](media-services-workflow-designer.md) 도구입니다.

[어떻게 tooUse Azure 미디어 서비스에서 프리미엄 인코딩](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>알려진 문제
입력된 비디오 닫힌 캡션를 포함 하지 않으면 hello 출력 자산 빈 TTML 파일에 계속 나타납니다.


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>관련 문서
* [미디어 인코더 표준 사전 설정을 사용자 지정하여 고급 인코딩 작업 수행](media-services-custom-mes-presets-with-dotnet.md)
* [할당량 및 제한 사항](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
