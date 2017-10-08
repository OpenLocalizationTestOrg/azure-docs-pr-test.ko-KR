---
title: "미디어 인코더 표준 Azure 포털 hello로 사용 하 여 자산 aaaEncode | Microsoft Docs"
description: "이 자습서는 Azure 포털 hello로 미디어 인코더 표준를 사용 하 여 자산 인코딩 hello 단계를 안내 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>미디어 인코더 표준 Azure 포털 hello로 사용 하 여 자산을 인코딩하
> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
> 
> 

적응 비트 전송률 스트리밍 tooyour 클라이언트 제공 하는 hello 가장 일반적인 시나리오 중 하나는 Azure 미디어 서비스를 사용 합니다. 미디어 서비스는 hello 적응 비트 전송률 스트리밍 기술에 따라 지원: HLS HTTP 라이브 스트리밍 (), 부드러운 스트리밍, MPEG DASH 합니다. tooprepare 비디오 적응 비트 전송률 스트리밍에 대 한 필요한 tooencode 원본 비디오를 다중 비트 전송률 파일로 합니다. Hello를 사용 해야 **미디어 인코더 표준** 인코더 tooencode 비디오입니다.  

또한 미디어 서비스 제공 toodeliver 수 있는 동적 패키징 hello 스트리밍 형식 뒤에 여 다중 비트 전송률 mp4: MPEG DASH, HLS, 부드러운 스트리밍 형식 스트리밍을로 toore 패키지 필요 없이 합니다. 동적 패키징을 사용 하면 toostore 및 단일 저장소 형식 및 미디어 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서에서 요청에 따라 hello 적절 한 응답을 제공 합니다.

tootake 이점은 동적 패키징을 tooencode 소스 파일에 필요한 (hello 인코딩 단계는이 섹션의 나중에 설명 된) 다중 비트 전송률 MP4 파일 집합이 있습니다.

처리 tooscale 미디어 참조 [이](media-services-portal-scale-media-processing.md) 항목입니다.

## <a name="encode-with-hello-azure-portal"></a>Azure 포털 hello로 인코딩
이 섹션에서는 프록시 hello tooencode 미디어 인코더 표준 사용 하 여 콘텐츠를 사용할 수 있습니다.

1. Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.
2. Hello에 **설정** 창에서 **자산**합니다.  
3. Hello에 **자산** 창, 싶다는 의사를 tooencode 선택 hello 자산입니다.
4. 키를 눌러 hello **인코딩** 단추입니다.
5. Hello에 **자산을 인코딩하** 창, "미디어 인코더 표준" 선택 hello 프로세서 및 사전 설정입니다. 기본 설정에 대한 자세한 내용은 [비트 전송률 래더 자동 생성](media-services-autogen-bitrate-ladder-with-mes.md) 및 [MES에 대한 작업 기본 설정](media-services-mes-presets-overview.md)을 참조하세요. Toocontrol 어떤 인코딩 사전 설정을 사용 하려는 경우이 점을 명심: tooselect hello 입력된 비디오에 가장 적합 하는 미리 설정 된 것입니다. 예를 들어 입력된 비디오 1920 x 1080 픽셀이 고 해상도 알고 있는 경우 다음 사용할 수 있습니다 hello "H264 다중 비트 전송률 1080p" 사전 설정입니다. 낮은 해상도(640x360) 비디오가 있는 경우 기본 “H264 다중 비트 전송률 1080p” 기본 설정을 사용하지 말아야 합니다.
   
   관리를 간소화 하기 hello 출력 자산 편집 hello 이름 및 hello 작업의 hello 이름은 선택할을 수 있습니다.
   
   ![자산 인코딩](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. **만들기**를 누릅니다.

## <a name="next-step"></a>다음 단계
에 설명 된 대로 hello Azure 포털을 사용 하 여 인코딩 작업 진행률을 모니터링할 수 있습니다 [이](media-services-portal-check-job-progress.md) 문서.  

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

