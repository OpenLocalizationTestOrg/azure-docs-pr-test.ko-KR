---
title: "aaaAzure 미디어 서비스 질문과 대답 | Microsoft Docs"
description: "FAQ(질문과 대답)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>질문과 대답

이 문서에서는 질문과 대답 hello Azure 미디어 서비스 (AMS) 사용자 커뮤니티에 의해 발생 합니다.

## <a name="general-ams-faqs"></a>일반 AMS FAQ
Q: 인덱싱을 확장하려면 어떻게 하나요?

A: hello 예약 단위는 인코딩 및 인덱싱 작업에 대 한 동일한 hello 됩니다. 지침에 따라 [어떻게 tooScale 인코딩 예약 단위](media-services-scale-media-processing-overview.md)합니다. **참고** : 인덱서 성능은 예약 단위 유형의 영향을 받지 않습니다.

Q: 업로드, 인코딩 및 동영상을 게시합니다. Hello 이유 hello 비디오 것은 toostream 때 재생 되지 않으면 해당?

A: hello 가장 일반적으로이 스트리밍 끝점에서 hello tooplayback 하려는 hello 없는 이유 중 하나 **실행** 상태입니다.  

Q: 라이브 스트림에서 합치기를 수행할 수 있나요?

A: 합성 라이브 스트림에는 현재 제공 되지 않습니다 Azure 미디어 서비스에서 toopre 해야 하므로-컴퓨터에 작성 합니다.

Q: 라이브 스트리밍으로 Azure CDN을 사용할 수 있나요?

A: 미디어 서비스와 Azure CDN 통합을 지원 (자세한 내용은 참조 [방법을 미디어 서비스 계정에서 tooManage 스트리밍 끝점](media-services-portal-manage-streaming-endpoints.md)).  CDN을 사용하여 라이브 스트리밍을 사용할 수 있습니다. Azure 미디어 서비스는 부드러운 스트리밍, HLS 및 MPEG-DASH 출력을 제공합니다. 이러한 형식에서는 HTTP를 데이터 전송에 사용하여 HTTP 캐싱의 이점을 얻을 수 있습니다. 라이브 스트리밍 비디오/오디오의 실제 데이터 분할된 toofragments 되며이 개별 조각을 CDN에 캐시 되는 것입니다. 새로 고친된 데이터 요구 toobe만는 hello 매니페스트 데이터입니다. CDN은 매니페스트 데이터를 주기적으로 새로 고칩니다.

Q: Azure 미디어 서비스는 저장된 이미지를 지원하나요?

A: toostore JPEG 또는 PNG 이미지 방금 찾으려는 경우 Azure Blob 저장소에 유지 해야 합니다. 비디오 또는 오디오 자산와 연결 된 해당 tookeep 사용 하려는 경우가 아니면 미디어 서비스에서 계정 없는 혜택 tooputting이 있습니다. 또는 경우 hello 비디오 인코더에 오버레이 필요 toouse hello 이미지를 할 수 있습니다. 미디어 인코더 표준 비디오, 위에 이미지 오버레이 지원 하며 JPEG 및 PNG 지원 나열 작업 하는 형식을 입력 합니다. 자세한 내용은 [오버레이 만들기](media-services-advanced-encoding-with-mes.md#overlay)를 참조하세요.

Q: 자산 하나 미디어 서비스 계정 tooanother에서 어떻게 복사할 수 있습니다.

A: toocopy 자산.NET을 사용 하 여 한 미디어 서비스 계정 tooanother에서 사용 하 여 [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) hello에서 사용할 수 있는 확장 메서드 [Azure 미디어 서비스.NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) 저장소입니다. 자세한 내용은 [이](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) 포럼 스레드를 참조하세요.

Q: hello 지원 되는 문자 AMS 작업할 때 파일 이름 지정

A: 미디어 서비스 스트리밍 콘텐츠 (예를 들어 http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) hello에 대 한 Url 작성 시 hello IAssetFile.Name 속성의 hello 값을 사용 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다. 값의 hello hello **이름** 속성 hello 다음 중 하나를 사용할 수 없습니다 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다. 또한 ‘.’ 하나만 사용할 수 있습니다. hello 파일 이름 확장명입니다.

Q: 어떻게를 놓으면 tooconnect를 사용 하 여?

A:에 대 한 내용은 tooconnect toohello AMS API를 확인 하려면 어떻게 해야 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다. 

Q: hello 인코딩 프로세스 동안 비디오를 어떻게 회전할 수 있습니다.

A: hello [미디어 인코더 표준](media-services-dotnet-encode-with-media-encoder-standard.md) 90/180/270의 회전 각도으로 지원 합니다. hello 기본 동작은 "자동", hello 들어오는 MP4/MOV 파일에 toodetect hello 회전 메타 데이터를 시도 하 고 그에 대 한 보정 합니다. Hello 다음이 포함 **소스** hello json 정의 사전 설정의 요소 tooone [여기](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
