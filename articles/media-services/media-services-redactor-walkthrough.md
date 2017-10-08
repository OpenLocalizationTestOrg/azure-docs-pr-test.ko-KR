---
title: "Azure 미디어 분석 연습을 aaaRedact 면 | Microsoft Docs"
description: "이 항목에서는 방법에 단계별 지침을 보여 줍니다. toorun Azure 미디어 서비스 탐색기 (AMSE) 및 Azure 미디어 Redactor 시각화 도우미 (오픈 소스 도구)를 사용 하 여 전체 교정 워크플로 합니다."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Azure 미디어 분석으로 얼굴 편집 안내

## <a name="overview"></a>개요

**Azure 미디어 Redactor** 는 [Azure 미디어 분석](media-services-analytics-overview.md) hello 클라우드에서 확장 가능한 글꼴 교정에서 제공 하는 미디어 프로세서 (MP). Face 교정 있습니다 toomodify 선택한 개인의 순서 tooblur 면에서 비디오를 수 있습니다. 공용 안전과 뉴스 미디어 시나리오에서 toouse hello 얼굴 교정 서비스를 할 수 있습니다. 몇 분 정도 여러 글꼴로 포함 된 장면 시간 tooredact 수동으로 필요로 하지만이 서비스 hello 모양을 가진 교정 프로세스는 몇 가지 간단한 단계만 거치면 요구 됩니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-redactor/) 를 참조하세요.

에 대 한 세부 정보에 대 한 **Azure 미디어 Redactor**, hello 참조 [얼굴 교정 개요](media-services-face-redaction.md) 항목입니다.

이 항목에서는 방법에 단계별 지침을 보여 줍니다. toorun Azure 미디어 서비스 탐색기 (AMSE) 및 Azure 미디어 Redactor 시각화 도우미 (오픈 소스 도구)를 사용 하 여 전체 교정 워크플로 합니다.

hello **Azure 미디어 Redactor** MP는 현재 미리 보기로 합니다. 이 기능은 모든 공용 Azure 지역과 미국 정부 및 중국 데이터 센터에서 사용할 수 있습니다. 이 미리 보기는 현재 무료입니다. Hello 현재 릴리스에서 처리 된 비디오 길이 제한은 10 분은 없습니다.

자세한 내용은 [이 블로그](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) 를 참조하세요.

## <a name="azure-media-services-explorer-workflow"></a>Azure Media Services 탐색기 워크플로

hello 가장 쉬운 방법은 tooget 시작 Redactor는 github에서 toouse hello 오픈 소스 AMSE 도구입니다. 통해 간단한 워크플로 실행할 수 있습니다 **결합** toohello 주석 json 또는 hello 얼굴 jpg 이미지에 액세스할 필요 하지 않는 경우에 모드입니다.

### <a name="download-and-setup"></a>다운로드 및 설치

1. Hello AMSE 도구를 다운로드할 [여기](https://github.com/Azure/Azure-Media-Services-Explorer)합니다.
1. Tooyour 서비스 키를 사용 하 여 미디어 서비스 계정에에서 로그인 합니다.

    계정 이름 및 키 정보, 이동 toohello tooobtain hello [Azure 포털](https://portal.azure.com/) AMS 계정을 선택 합니다. 그런 후 설정 > 키를 선택합니다. hello 관리 키 windows hello 계정 이름을 표시 하 고 hello 기본 및 보조 키 표시 됩니다. Hello 계정 이름 및 hello 기본 키의 값을 복사 합니다.

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>1 패스 – 분석 모드

1. 자산 –> 업로드를 통해 또는 끌어서 놓기를 통해 미디어 파일을 업로드합니다. 
1. 마우스 오른쪽 단추를 클릭하고 Media Analytics –> Azure Media Redactor –> 분석 모드를 사용하여 미디어 파일을 처리합니다. 


![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

hello 출력은 검색 된 각 면의 jpg 뿐만 아니라 얼굴 위치 데이터를 사용 하는 주석 json 파일이 포함 됩니다. 

![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>2 패스 – 교정 모드

1. Hello 첫 번째 패스에서 출력 하 고 기본 자산으로 설정 하 여 원래 비디오 자산 toohello를 업로드 합니다. 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (선택 사항) 줄 바꿈 구분 된 목록이 hello tooredact 원하는 Id 포함 하는 'Dance_idlist.txt' 파일을 업로드 합니다. 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (선택 사항) 모든 편집 내용이 toohello annotations.json 파일을 늘리는 등 hello 경계 상자 경계를 확인 합니다. 
4. Hello 첫 번째 패스에서 hello 출력 자산을 마우스 오른쪽 단추로 클릭 하 고 hello Redactor, 선택 hello를 사용 하 여 실행 **Redact** 모드입니다. 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. 다운로드 하거나 hello 최종 교정된 출력 자산을 공유 합니다. 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Azure Media Redactor Visualizer 오픈 소스 도구

오픈 소스 [시각화 도우미 도구](https://github.com/Microsoft/azure-media-redactor-visualizer) 디자인 된 toohelp 개발자가 구문 분석 한 hello 출력을 사용 하 여 hello 주석 형식으로 시작 됩니다.

Toodownload FFMPEG 할 순서 toorun hello 프로젝트에서 hello 리포지토리를 복제 한 후에서 자신의 [공식 사이트](https://ffmpeg.org/download.html)합니다.

샘플 코드 예제에 대 한 JSON 주석 데이터 tooparse hello 시도 개발자 인 경우 Models.MetaData 내부 확인 합니다.

### <a name="set-up-hello-tool"></a>Hello 도구 설정

1.  다운로드 하 고 hello 전체 솔루션을 빌드하십시오. 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  [여기](https://ffmpeg.org/download.html)에서 FFMPEG를 다운로드합니다. 이 프로젝트는 정적 링크가 있는 be1d324(2016-10-04)를 사용하여 개발되었습니다. 
3.  Ffmpeg.exe 및 ffprobe.exe toohello 복사 AzureMediaRedactor.exe 동일한 출력 폴더입니다. 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. AzureMediaRedactor.exe를 실행합니다. 

### <a name="use-hello-tool"></a>Hello 도구 사용

1. 분석 모드 hello Redactor MP로 Azure 미디어 서비스 계정에서 비디오를 처리 합니다. 
2. 원본 비디오 파일 hello와 hello 교정의 hello 출력을 다운로드 하-작업을 분석 합니다. 
3. Hello 시각화 도우미 응용 프로그램을 실행 하 고 위의 hello 파일을 선택 합니다. 

    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. 파일을 미리 봅니다. 선택 하면 향하도록 것인지 hello에 hello 사이드바 통해 tooblur 오른쪽 합니다. 
    
    ![얼굴 편집](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  hello 아래쪽 텍스트 필드는 hello 글꼴 Id로 업데이트 됩니다. 줄 바꿈으로 구분된 이러한 ID 목록으로 "idlist.txt"라는 파일을 만듭니다. 

    >[!NOTE]
    > hello idlist.txt은 ANSI에 저장 됩니다. Ansi에서 메모장 toosave를 사용할 수 있습니다.
    
6.  1 단계에서이 파일 toohello 출력 자산을 업로드 합니다. Hello 원래 비디오 toothis 자산으로 업로드 하 고 기본 자산으로 설정 합니다. 
7.  이 자산 "Redact" 모드 tooget hello 최종 교정 비디오 교정 작업을 실행 합니다. 

## <a name="next-steps"></a>다음 단계 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>관련 링크
[Azure Media Services 분석 개요](media-services-analytics-overview.md)

[Azure 미디어 분석 데모](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Azure Media Analytics의 얼굴 편집 발표](https://azure.microsoft.com/blog/azure-media-redactor/)
