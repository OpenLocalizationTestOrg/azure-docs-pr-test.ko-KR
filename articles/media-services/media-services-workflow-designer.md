---
title: "aaaCreate 고급 인코딩 워크플로는 워크플로 디자이너 | Microsoft Docs"
description: "Toocreate 워크플로 디자이너로 인코딩 워크플로 고급 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>워크플로 디자이너와 고급 인코딩 워크플로 만들기
## <a name="overview"></a>개요
hello **워크플로 디자이너** 은 Windows 데스크톱 도구를 사용 하는 toodesign 및 빌드 사용자 지정에 대 한 워크플로 인코딩을 **미디어 인코더 프리미엄 워크플로**합니다.
Hello 활용 hello 워크플로 디자이너 도구를 사용 하 여 디자인 하 고에서 실행 되는 복잡 한 워크플로 만드는 **미디어 인코더 프리미엄**합니다.  

워크플로 고객 의사 결정 논리를 포함할 수 있습니다 및 hello 입력된 소스 파일의 속성을 기반으로 분기 합니다. 재정의 가능한 속성과 동적 값 toomake 짝수 hello 가장 복잡 한 인코딩 작업 쉽게 toorepeat 사용 하 여 워크플로 만들고 hello 클라우드에서 사용자 지정할 수 있습니다.

만들 수 있는 예제 워크플로는 다음과 같습니다.

* 의사 결정 확인용 hello 원본 콘텐츠를 검사 하 고만 원하는 hello 출력 트랙을 인코딩하는 워크플로 기반으로 합니다.  Hello 원본 콘텐츠 실수로 upscaling 하 여 발생 하는 hello 불필요 하 게 트랙을 제거 하 여 helfpul입니다.
* 여러 입력된 파일이 사용 되는 toosupport 캡션과 오버레이 연결 함께 콘텐츠 수 있습니다. 

이 도구도 사용 되는 toomodify 중 하나일 수 있습니다이 [워크플로 게시](media-services-workflow-designer.md#existing_workflows)합니다. 

> [!NOTE]
> tooget hello 워크플로 디자이너 도구의 사본을 문의 mepd@microsoft.com합니다.
> 
> 

워크플로 파일을 만든 후 이를 자산으로 업로드한 다음 미디어 파일을 인코딩하는 데 사용할 수 있습니다. 방법에 대 한 내용은와 tooencode **미디어 인코더 프리미엄 워크플로** 를 사용 하 여 **.NET**, 참조 [미디어 인코더 프리미엄 워크플로 인코딩을 고급](media-services-encode-with-premium-workflow.md)합니다.

## <a id="existing_workflows"></a>기존 워크플로 수정
기본 hello [워크플로 게시](media-services-workflow-designer.md#existing_workflows) hello 디자이너 도구를 사용 하 여 수정할 수 있습니다. Hello 기본 워크플로 파일을 가져올 수 [여기](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)합니다. hello 폴더에는 이러한 파일에 대 한 hello 설명을 포함 되어 있습니다.

다음 비디오 hello toouse 디자이너 hello 하는 방법을 보여 줍니다.

### <a name="day-1--getting-started"></a>1일차 – 시작하기
1일차 비디오에서 다루는 내용은 다음과 같습니다.

* 디자이너 개요
* 기본 워크플로 – "Hello World"
* Azure 미디어 서비스 스트리밍에서 사용할 여러 출력 MP4 파일 만들기

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>2일차
2일차 비디오에서 다루는 내용은 다음과 같습니다.

* 다양한 소스 파일 시나리오 – 오디오 처리
* 고급 논리를 사용한 워크플로
* 그래프 단계

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>3일차
3일차 비디오에서 다루는 내용은 다음과 같습니다.

* 워크플로/청사진 내부 스크립팅
* 제한 된 hello 현재 인코더
* Q&A

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

지원 하거나 hello 워크플로 디자이너 도구에서 사용자 지정 워크플로 만들기에 대 한 질문이 필요한 경우 전자 메일을 보내 주십시오 toomepd@microsoft.com합니다.

## <a name="see-also"></a>참고 항목
[Azure Premium 인코더 워크플로 디자이너 교육 비디오](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

