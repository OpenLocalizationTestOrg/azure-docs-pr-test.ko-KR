---
title: "aaaAnalyze Azure 포털 hello 사용 하 여 미디어 | Microsoft Docs"
description: "이 항목에서는 방법을 tooprocess 미디어 분석 미디어 프로세서 (Mp)를 사용 하 여 미디어 hello Azure 포털입니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 미디어를 분석 합니다.
> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
> 
> 

## <a name="overview"></a>개요
Azure 미디어 서비스 분석은 음성 및 비전에서 구성 요소 (엔터프라이즈 규모, 규정 준수, 보안 및 글로벌 서비스)을 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서의 컬렉션입니다. Azure Media Services Analytics에 대한 자세한 개요는 [이](media-services-analytics-overview.md) 항목을 참조하세요. 

이 항목에서는 방법을 tooprocess 미디어 분석 미디어 프로세서 (Mp)를 사용 하 여 미디어 hello Azure 포털입니다. 미디어 분석 MP는 MP4 파일 또는 JSON 파일을 생성합니다. 미디어 프로세서 MP4 파일을 생성 하는 경우에 hello 파일을 점진적으로 다운로드할 수 있습니다. 미디어 프로세서는 JSON 파일을 생성 하는 경우에 hello Azure blob 저장소에서에서 hello 파일을 다운로드할 수 있습니다. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>자산 선택 tooanalyze 원하는
1. Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.
2. Hello에 **설정** 창에서 **자산**합니다.  
   에서도 확인할 수 있습니다.
    ![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. 원하는 선택 hello 자산 tooanalyze 및 키를 눌러 hello **분석** 단추입니다.
   
    ![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. Hello에 **미디어 분석 인 미디어 자산 프로세스** 창, 선택 hello 프로세서. 
   
    hello 문서의 hello 나머지 부분에서는 근거, 방법에 대해 설명 toouse 각 프로세서. 
5. 키를 눌러 **만들기** toohello 작업을 시작 합니다.

## <a name="azure-media-indexer"></a>Azure 미디어 인덱서
hello **Azure Media Indexer** 미디어 프로세서를 사용 하면 toomake 미디어 파일 및 콘텐츠를 검색할 수, 닫힌된 캡션 트랙을 생성 합니다. 이 섹션에서는 이 MP에 대해 지정할 수 있는 옵션에 대한 자세한 내용을 제공합니다.

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>언어
hello 자연어 toobe hello 멀티미디어 파일에서 인식 합니다. 예를 들어 영어 또는 스페인어입니다. 

### <a name="captions"></a>자막
콘텐츠에서 생성할 자막 형식을 선택할 수 있습니다. 한 인덱싱 작업 hello 형식 뒤에 닫힌된 캡션 파일을 생성할 수 있습니다.  

* **SAMI**
* **TTML**
* **WebVTT**

비디오 파일 청각 장애가 있는 toopeople를 액세스할 수 있으며 이러한 형식의 닫힌된 캡션 (CC) 파일 사용된 toomake 오디오를 수 있습니다.

### <a name="aib-file"></a>AIB 파일
사용자는 사용 하기 위해 toogenerate hello 오디오 인덱스 Blob 파일 같은 hello 사용자 지정 SQL Server IFilter이이 옵션을 선택 합니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) 를 참조하세요.

### <a name="keywords"></a>키워드
Toogenerate 키워드 XML 파일을 원하는 경우이 옵션을 선택 합니다. 이 파일에는 빈도 및 오프셋된 정보와 함께 hello 음성 콘텐츠에서 추출 된 키워드가 포함 되어 있습니다.

### <a name="job-name"></a>작업 이름
Hello 작업을 식별할 수 있는 이름입니다. [이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다. 

### <a name="output-file"></a>출력 파일
Hello 출력 콘텐츠를 식별할 수 있는 이름입니다. 

## <a name="azure-media-hyperlapse"></a>Azure 미디어 Hyperlapse
Azure Media Hyperlapse는 1인칭 또는 액션 카메라 콘텐츠에서 부드러운 시간 경과 비디오를 만드는 MP입니다.  자세한 내용은 [이 항목](media-services-hyperlapse-content.md)을 참조하세요. 이 섹션에서는 이 MP에 대해 지정할 수 있는 옵션에 대한 자세한 내용을 제공합니다.

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>속도
Hello 입력된 비디오를 어떤 toospeed와 hello 속도 지정 합니다. hello 출력은 hello 입력된 비디오의 안정화 및 된 경과 된 시간 변환을입니다.

### <a name="job-name"></a>작업 이름
Hello 작업을 식별할 수 있는 이름입니다. [이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다. 

### <a name="output-file"></a>출력 파일
Hello 출력 콘텐츠를 식별할 수 있는 이름입니다. 

## <a name="azure-media-face-detector"></a>Azure 미디어 얼굴 탐지기
hello **Azure 미디어 얼굴 탐지기** 미디어 프로세서 MP ()를 사용 하면 toocount, 트랙 이동을 계기 청중 참여도 있고 얼굴 식을 통해 반응 합니다. 이 서비스는 두 가지 기능을 포함합니다. 

* **얼굴 검색**
  
    얼굴 검색은 동영상 내의 얼굴을 찾아 추적합니다. 여러 글꼴로 검색 하 hello 시간 및 위치 메타 데이터와 JSON 파일에서 반환 된, 이동 하는 동안 이후에 추적할 수 있습니다. 추적 하는 동안 toogive hello 사용자가 이동 화면의 hello 프레임을 간단 하 게 유지 되거나 방해 하는 경우에 하는 동안에 맞서게 동일한 일관 된 ID toohello 시도 합니다.
  
  > [!NOTE]
  > 이 서비스는 안면 인식을 수행하지 않습니다. Hello 프레임을 벗어나거나에 대 한 방해 되는 사람이 너무 오래 하 게 할 새 ID를 반환 합니다.
  > 
  > 
* **감정 검색**
  
    Emotion 검색은 hello hello 얼굴 감지 만족도, 슬픔, 걱정, 분노를 등의 여러 있지만 특성을 분석을 반환 하는 얼굴 감지 미디어 프로세서의 선택적 구성 요소는 있습니다. 

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>감지 모드
Hello 프로세서에 의해 hello 다음 모드 중 하나를 사용할 수 있습니다.

* 얼굴 감지
* 얼굴별 감정 감지
* 감정 집계 감지

### <a name="job-name"></a>작업 이름
Hello 작업을 식별할 수 있는 이름입니다. [이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다. 

### <a name="output-file"></a>출력 파일
Hello 출력 콘텐츠를 식별할 수 있는 이름입니다. 

## <a name="azure-media-motion-detector"></a>Azure 미디어 동작 탐지기
hello **Azure 미디어 동작 탐지기** 미디어 프로세서 (MP) 사용 하도록 설정 하면 tooefficiently 그렇지 않으면 길고 정상적인 비디오 내에서 필요한 섹션을 식별 합니다. 동작 감지 동작 발생 hello 비디오의 정적 카메라 장면 tooidentify 섹션에서 사용할 수 있습니다. 타임 스탬프 및 hello hello 이벤트가 발생 하는 영역 경계와 메타 데이터를 포함 하는 JSON 파일을 생성 합니다.

이 기술은 보안 비디오 피드를 겨냥 수 toocategorize 동작 관련 이벤트 및 거짓 긍정 그림자 조명 변경 등으로입니다. 이렇게 하면 있습니다 카메라 피드에서 toogenerate 보안 경고 수 tooextract 시간이 매우 긴 거리 내 감시 비디오에서 관심 있는 하면서 무한 관련이 없는 이벤트로 스팸 메일 되지 않고.

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure 미디어 비디오 미리 보기
이 프로세서를 사용 하면 hello 원본 비디오에서 흥미로운 조각을 자동으로 선택 하 여 긴 비디오의 요약을 만들 수 있습니다. Tooprovide 비디오에서 어떤 tooexpect의 간략 한 개요를 원하는 경우에 유용 합니다. 자세한 내용 및 예제에 대 한 참조 [Azure 미디어 비디오 축소판 그림 사용 tooCreate 비디오 요약](media-services-video-summarization.md)

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>작업 이름
Hello 작업을 식별할 수 있는 이름입니다. [이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다. 

### <a name="output-file"></a>출력 파일
Hello 출력 콘텐츠를 식별할 수 있는 이름입니다. 

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로 보기.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

