---
title: "hello Azure 포털을 사용 하 여 온-프레미스 인코더를 사용 하 여 aaaLive 스트림을 | Microsoft Docs"
description: "이 자습서에서는 hello 통과 배달에 대해 구성 하는 채널을 만드는 과정을 안내 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>어떻게를 통해 라이브 스트리밍 tooperform 온-프레미스 인코더 hello Azure 포털을 사용 하 여
> [!div class="op_single_selector"]
> * [포털](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

이 자습서에서는 Azure 포털 toocreate hello를 사용 하 여 hello 단계는 **채널** 하도록 구성 되어 있는 통과 배달 합니다. 

## <a name="prerequisites"></a>필수 조건
hello 다음은 필요한 toocomplete hello 자습서입니다.

* Azure 계정. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
* Media Services 계정. 미디어 서비스 계정 toocreate 참조 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.
* 웹캠. 예를 들어, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm)

다음 문서 tooreview hello이 가장 좋습니다.

* [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Azure 미디어 서비스를 사용하는 라이브 스트리밍 개요](media-services-manage-channels-overview.md)
* [다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>일반적인 라이브 스트리밍 시나리오
hello 다음 단계에서는 일반적인 라이브 스트리밍 응용 프로그램을 만드는 통과 배달에 대해 구성 된 채널을 사용 하는 것과 관련 된 작업. 이 자습서에서는 어떻게 toocreate 통과 채널 및 라이브 이벤트 및 관리 합니다.

>[!NOTE]
>스트리밍 끝점 toostream 콘텐츠 원하는 hello hello에 있는지 확인 **실행** 상태입니다. 
    
1. 비디오 카메라 tooa 컴퓨터에 연결 합니다. 다중 비트 전송률 RTMP 또는 조각화된 MP4 스트림을 출력하는 온-프레미스 라이브 인코더를 실행 및 구성합니다. 자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.
   
    이 단계는 채널을 만든 후에도 수행할 수 있습니다.
2. 통과 채널을 만들고 시작합니다.
3. 검색 hello 채널 수집 URL입니다. 
   
    hello 수집 URL hello 라이브 인코더 toosend hello 스트림 toohello 채널에서 사용 됩니다.
4. Hello 채널 미리 보기 URL을 검색 합니다. 
   
    이 URL tooverify 채널이 라이브 스트림을 hello을 수신 하 고 제대로 사용 합니다.
5. 라이브 이벤트/프로그램을 만듭니다. 
   
    Azure 포털을 hello를 사용 하 여, 하는 경우 라이브 이벤트를 만들면 자산도 만들어집니다. 

6. 스트리밍 및 보관 준비 toostart 있을 때는 hello 이벤트/프로그램을 시작 합니다.
7. 필요에 따라 hello 라이브 인코더에 신호를 받은 toostart 광고 수 있습니다. hello 광고 hello 출력 스트림에 삽입 됩니다.
8. Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 이벤트/프로그램을 중지 합니다.
9. Hello 이벤트/프로그램을 삭제 합니다 (및 필요에 따라 hello 자산을 삭제) 합니다.     

> [!IMPORTANT]
> 검토 하십시오 [다중 비트 전송률 스트림을 만들 수 있는 온-프레미스 인코더를 통해 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md) toolearn 개념 및 고려 사항에 대 한 온-프레미스 인코더 및 통과 채널 toolive 스트리밍 관련 됩니다.
> 
> 

## <a name="tooview-notifications-and-errors"></a>tooview 알림 및 오류
Tooview 알림을 발생 한 오류로 인해 hello 하 여 Azure 포털을 hello 알림 아이콘을 클릭 합니다.

![알림](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>통과 채널 및 이벤트 만들기 및 시작
채널은 toocontrol hello 게시 및 저장 라이브 스트림의 세그먼트의 수 있는 이벤트/프로그램와 관련이 있습니다. 채널은 이벤트를 관리합니다. 

시간을 기록 하는 hello 콘텐츠 tooretain hello 프로그램에 대 한 hello 설정 하 여 hello 수를 지정할 수 **보관 창** 길이입니다. 이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다. 보관 창 길이는 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 최대한 hello 따라 결정 됩니다. 이벤트 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다. 또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.

각 이벤트는 자산에 연결됩니다. toopublish hello 이벤트 hello 연결 된 자산에 대 한 OnDemand 로케이터를 만들어야 합니다. 이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL을 사용 하도록 설정 합니다.

채널에서는 toothree hello 여러 보관 본을 만들 수 있도록 이벤트 동시에 실행 가능한 최대 지원 같은 들어오는 스트림을 합니다. 이렇게 하면 필요에 따라 이벤트의 다른 부분 toopublish 및 보관 있습니다. 예를 들어 비즈니스 요구 사항 tooarchive 6 시간의 프로그램에서 나 toobroadcast만 마지막 10 분입니다. tooaccomplish이, 두 개의 동시 실행 프로그램을 toocreate 필요 합니다. 한 프로그램 tooarchive 6 시간의 이벤트 hello 설정 되어 있지만 hello 프로그램 게시 되지 않습니다. hello 다른 프로그램은 집합 tooarchive 10 분 동안 되며이 프로그램이 게시 됩니다.

기존 라이브 이벤트를 다시 사용해서는 안 됩니다. 대신, 각 이벤트에 대해 새 이벤트를 만들고 시작합니다.

스트리밍 및 보관 준비 toostart 있을 때는 hello 이벤트를 시작 합니다. Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 프로그램을 중지 합니다. 

toodelete 보관 된 콘텐츠 중지 되어 hello 이벤트를 삭제 하 고 hello 관련된 자산을 삭제 합니다. 이벤트에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다. 

중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오.

수행 tooretain hello 보관 된 콘텐츠, 하지만 스트리밍에 사용할 수 없는, hello 스트리밍 로케이터를 삭제 합니다.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse hello 포털 toocreate 채널
이 섹션에서는 어떻게 toouse hello **빠른 생성** 옵션 toocreate 채널을 통과 합니다.

통과 채널에 대한 자세한 내용은 [다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.

1. Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.
2. Hello에 **설정** 창 클릭 **라이브 스트리밍**합니다. 
   
    ![시작](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    hello **라이브 스트리밍을** 창이 나타납니다.
3. 클릭 **빠른 생성** toocreate RTMP hello로 통과 채널 수집 프로토콜입니다.
   
    hello **새 채널 만들기** 창이 나타납니다.
4. 이름을 hello 새 채널을 지정 하 고 클릭 **만들기**합니다. 
   
    그러면 생성 통과 채널 hello RTMP 수집 프로토콜입니다.

## <a name="create-events"></a>이벤트 생성
1. 원하는 tooadd 이벤트 채널 toowhich를 선택 합니다.
2. **라이브 이벤트** 단추를 누릅니다.

![행사](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>수집 URL 가져오기
가져올 수 있습니다 hello 채널을 만든 후 수집 toohello 라이브 인코더 제공할 Url입니다. hello 인코더에서 이러한 Url tooinput 라이브 스트림을 사용 합니다.

![생성일](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>조사식 hello 이벤트
toowatch hello 이벤트 클릭 **조사식** 스트리밍 URL Azure 포털 또는 복사 hello hello와 원하는 플레이어를 사용 합니다. 

![생성일](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

라이브 이벤트는 자동으로 중지 될 때 변환 된 tooon 주문형 콘텐츠를 가져옵니다.

## <a name="clean-up"></a>정리
통과 채널에 대한 자세한 내용은 [다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.

* 모든 이벤트/hello 채널에서 프로그램을 중지 하는 경우에 채널을 중지할 수 있습니다.  Hello 채널 중지 되 고 나면 비용이 발생 하지는 않습니다. Toostart 필요한 경우 다시 것은 hello 동일 수집 URL tooreconfigure 인코더 필요 하지 않습니다.
* Hello 채널에서 모든 라이브 이벤트를 삭제 하는 경우에 채널을 삭제할 수 있습니다.

## <a name="view-archived-content"></a>보관된 콘텐츠 보기
중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오. 이벤트에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다. 

toomanage 자산, 선택 **설정** 클릭 **자산**합니다.

![자산](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

