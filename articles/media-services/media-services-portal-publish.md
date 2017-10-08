---
title: "aaa\"hello Azure 포털으로 콘텐츠를 게시 | \"Microsoft Docs"
description: "이 자습서의 hello Azure 포털을 사용 하 여 콘텐츠를 게시 hello 단계를 안내 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Azure 포털 hello로 콘텐츠를 게시 합니다.
> [!div class="op_single_selector"]
> * [포털](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST (영문)](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>개요
> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
> 
> 

tooprovide는 url을 사용 하는 toostream 하거나 콘텐츠를 다운로드할 수 있는 사용자를 처음 필요 너무 "게시할" 자산 로케이터를 만들어 합니다. 로케이터는 hello 자산에 포함 된 액세스 toofiles를 제공 합니다. Media Services는 두 가지 유형의 로케이터를 지원합니다. 

* 스트리밍 로케이터 (OnDemandOrigin), (예를 들어 toostream MPEG DASH, HLS 또는 부드러운 스트리밍) 적응 스트리밍에 사용 합니다. 스트리밍 로케이터 toocreate 자산인.ism 파일을 포함 해야 합니다. 
* 점진적(SAS) 로케이터로, 점진적 다운로드를 통해 비디오를 배달하는 데 사용합니다.

스트리밍 URL 형식에 따라 hello 개이고 tooplay 부드러운 스트리밍 자산을 사용할 수 있습니다.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS 스트리밍 URL을 한 toobuild 추가 (형식 = m3u8 aapl) toohello URL입니다.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

스트리밍 URL, MPEG DASH는 toobuild 추가 (형식 = mpd-시간-csf) toohello URL입니다.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

SAS URL 형식에 따라 hello에 있습니다.

    {blob container name}/{asset name}/{file name}/{SAS signature}

자세한 내용은 [콘텐츠 제공 개요](media-services-deliver-content-overview.md)를 참조하세요.

> [!NOTE]
> 2015 년 3 월 이전에 hello 포털 toocreate 로케이터를 사용 하는 경우 로케이터는 2 년 유효 기간으로 만들어집니다.  
> 
> 

만료 날짜를 사용 하 여 로케이터는 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 또는 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) Api입니다. SAS 로케이터의 hello 만료 날짜를 업데이트 하면 hello URL 변경 되는지 note 합니다.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello 포털 toopublish 자산
toouse hello 포털 toopublish 자산, 다음 hello지 않습니다.

1. Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.
2. 계정 배포 진행 상태를 보려면 **설정** > **자산**을 참조하세요.
3. 원하는 toopublish hello 자산을 선택 합니다.
4. Hello 클릭 **게시** 단추입니다.
5. Hello 로케이터 유형을 선택 합니다.
6. **추가**를 누릅니다.
   
    ![게시](./media/media-services-portal-vod-get-started/media-services-publish1.png)

hello URL toohello 목록이 추가 될 **게시 Url**합니다.

## <a name="play-content-from-hello-portal"></a>Hello 포털에서 콘텐츠 재생
hello Azure 포털에서 제공 콘텐츠 플레이어를 사용할 수 있는 tootest 비디오.

원하는 hello 비디오를 클릭 하 고 hello 클릭 **재생** 단추입니다.

![게시](./media/media-services-portal-vod-get-started/media-services-play.png)

다음과 같은 몇 가지 고려 사항이 적용됩니다.

* 게시 된 비디오 hello 있는지 확인 합니다.
* 이 **미디어 플레이어** hello 기본 스트리밍 끝점에서에서 재생 합니다. 기본이 아닌에서 tooplay 스트리밍 끝점을 toocopy hello URL을 클릭 하 고 다른 플레이어를 사용 합니다. 예를 들어 [Azure Media Services 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.
* 스트리밍 끝점을 스트리밍하는 hello 실행 되어야 합니다.  

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

