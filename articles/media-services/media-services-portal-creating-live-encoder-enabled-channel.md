---
title: "aaaHow tooperform 라이브 스트리밍을 toocreate 다중 비트 전송률 스트림을 Azure 미디어 서비스를 사용 하 여 Azure 포털 hello로 | Microsoft Docs"
description: "이 자습서에서는 단일 비트 전송률 라이브 스트림을 수신 하는 채널을 만드는 단계 hello 하 고 hello Azure 포털을 사용 하 여 toomulti 비트 전송률 스트림으로 인코딩합니다."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Azure 포털 hello로 어떻게 스트리밍하 tooperform 라이브 스트리밍을 Azure 미디어 서비스 toocreate 다중 비트 전송률을 사용 하 여
> [!div class="op_single_selector"]
> * [포털](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [REST API](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

이 자습서에서는 hello 만드는 단계는 **채널** 단일 비트 전송률 라이브 스트림을 수신 하 고 toomulti 비트 전송률 스트림으로 인코딩합니다.

> [!NOTE]
> 자세한 개념 정보에 대 한 라이브 인코딩이 관련된 tooChannels 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.
> 
> 

## <a name="common-live-streaming-scenario"></a>일반적인 라이브 스트리밍 시나리오
hello 다음은 일반적인 라이브 스트리밍 응용 프로그램 만들기와 관련 된 일반적인 단계입니다.

> [!NOTE]
> 현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다. 오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오.
> 
> 

1. 비디오 카메라 tooa 컴퓨터에 연결 합니다. 시작 하 고 hello 다음 프로토콜 중 하나에 단일 비트 전송률 스트림을 출력 하는 온-프레미스 라이브 인코더 구성: RTMP, 부드러운 스트리밍 또는 RTP (MPEG-TS). 자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.
   
    이 단계는 채널을 만든 후에도 수행할 수 있습니다.
2. 채널을 만들고 시작합니다. 
3. 검색 hello 채널 수집 URL입니다. 
   
    hello 수집 URL hello 라이브 인코더 toosend hello 스트림 toohello 채널에서 사용 됩니다.
4. Hello 채널 미리 보기 URL을 검색 합니다. 
   
    이 URL tooverify 채널이 라이브 스트림을 hello을 수신 하 고 제대로 사용 합니다.
5. 이벤트/프로그램을 만듭니다(자산도 만들어짐). 
6. (를 hello 연결 된 자산에 대 한 OnDemand 로케이터 만들기) hello 이벤트를 게시 합니다.    
7. 스트리밍 및 보관 준비 toostart 있을 때는 hello 이벤트를 시작 합니다.
8. 필요에 따라 hello 라이브 인코더에 신호를 받은 toostart 광고 수 있습니다. hello 광고 hello 출력 스트림에 삽입 됩니다.
9. Hello 이벤트 toostop 스트리밍 및 hello 이벤트를 보관 하려는 경우 중지 합니다.
10. Hello 이벤트 삭제 (및 필요에 따라 hello 자산을 삭제) 합니다.   

## <a name="in-this-tutorial"></a>자습서 내용
이 자습서에서는 hello Azure 포털은 작업을 수행 하는 사용 되는 tooaccomplish hello: 

1. 채널을 만드는 즉 사용된 tooperform 라이브 인코딩을 합니다.
2. Get 순서 toosupply의 수집 URL hello 것 toolive 인코더입니다. hello 라이브 인코더는이 URL tooingest hello 스트림을 hello 채널에 사용 합니다.
3. 이벤트/프로그램(및 자산)을 만듭니다.
4. Hello 자산을 게시 하 고 스트리밍 Url을 가져옵니다.  
5. 콘텐츠를 재생합니다.
6. 정리합니다.

## <a name="prerequisites"></a>필수 조건
필요한 toocomplete hello 자습서는 hello 다음과가 같습니다.

* toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 
  자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* Media Services 계정. 미디어 서비스 계정 toocreate 참조 [계정 만들기](media-services-portal-create-account.md)합니다.
* 단일 비트 전송률 라이브 스트림을 보낼 수 있는 웹캠 및 인코더.

## <a name="create-a-channel"></a>채널 만들기
1. Hello에 [Azure 포털](https://portal.azure.com/), 미디어 서비스를 선택 하 고 미디어 서비스 계정 이름을 클릭 합니다.
2. **라이브 스트리밍**을 선택합니다.
3. **사용자 지정 만들기**를 선택합니다. 이 옵션을 통해 Live Encoding에 사용할 수 있는 채널을 만들 수 있습니다.
   
    ![채널 만들기](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. **설정**을 클릭합니다.
   
   1. Hello 선택 **라이브 인코딩을** 채널 형식입니다. 이 형식은 라이브 인코딩에 사용 하도록 설정 된 채널 toocreate 되도록 지정 합니다. 의미 hello 들어오는 단일 비트 전송률을 스트림 toohello 채널을 전달 하 고 라이브 인코더를 지정 된 설정을 사용 하 여 다중 비트 전송률 스트림으로 인코딩될 합니다. 자세한 내용은 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다. 확인을 클릭합니다.
   2. 채널의 이름을 지정합니다.
   3. Hello hello 화면 맨 아래에 확인을 클릭 합니다.
5. 선택 hello **수집** 탭 합니다.
   
   1. 이 페이지에서는 스트리밍 프로토콜을 선택할 수 있습니다. Hello에 대 한 **라이브 인코딩을** 채널 형식을 유효한 프로토콜 옵션은:
      
      * 단일 비트 전송률 조각화된 MP4(부드러운 스트리밍)
      * 단일 비트 전송률 RTMP
      * RTP(MPEG-TS): RTP를 통한 MPEG-2 전송 스트림
        
        각 프로토콜에 대 한 자세한 내용은 참조 하십시오. [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.
        
        연결 된 이벤트/프로그램을 실행 하는 또는 hello 채널 하는 동안 hello 프로토콜 옵션을 변경할 수 없습니다. 다른 프로토콜을 요청하는 경우 각각의 스트리밍 프로토콜에 대한 개별 채널을 만들어야 합니다.  
   2. IP 제한이 hello에 적용할 수 수집 합니다. 
      
       Hello IP를 정의할 수 있는 주소 tooingest 비디오 toothis 채널을 허용 합니다. 허용된 IP 주소는 단일 IP 주소(예: '10.0.0.1'), IP 주소와 CIDR 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1/22'), 또는 IP 주소와 점으로 구분된 10진수 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1(255.255.252.0)').
      
       IP 주소가 지정되지 않고 정의된 규칙이 없는 경우 IP 주소가 허용되지 않습니다. tooallow 모든 IP 주소 규칙을 만들고 0.0.0.0/0을 설정 합니다.
6. Hello에 **미리 보기** 탭, hello 미리 보기에서 IP 제한을 적용 합니다.
7. Hello에 **인코딩** 탭 hello 인코딩 사전 설정을 지정 합니다. 
   
    현재 시스템만 hello 사전 설정을 선택할 수는 **720p 기본**합니다. toospecify 사용자 지정 사전 설정, Microsoft 지원 티켓을 엽니다. 다음의 hello hello 이름을 입력으로 생성 하는 사전 설정입니다. 

> [!NOTE]
> 현재 채널 시작 hello too30 분 정도 걸릴 수 있습니다. 채널 재설정 too5 분 정도 걸릴 수 있습니다.
> 
> 

Hello 채널에서을 클릭 하 고 선택할 수 hello 채널을 만든 후 **설정을** 채널 구성을 볼 수 있습니다. 

자세한 내용은 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.

## <a name="get-ingest-urls"></a>수집 URL 가져오기
가져올 수 있습니다 hello 채널을 만든 후 수집 toohello 라이브 인코더 제공할 Url입니다. hello 인코더에서 이러한 Url tooinput 라이브 스트림을 사용 합니다.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>이벤트 만들기 및 관리
### <a name="overview"></a>개요
채널은 toocontrol hello 게시 및 저장 라이브 스트림의 세그먼트의 수 있는 이벤트/프로그램와 관련이 있습니다. 채널은 이벤트/프로그램을 관리합니다. hello 채널과 프로그램 관계는 매우 유사한 tootraditional 미디어 여기서는 채널에 일정 한 콘텐츠 스트림이 하 고 프로그램은 해당 채널의 이벤트 범위가 지정 된 toosome 시간이 초과 되었습니다.

시간을 기록 하는 hello 콘텐츠 tooretain hello 이벤트에 대 한 hello 설정 하 여 hello 수를 지정할 수 **보관 창** 길이입니다. 이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다. 보관 창 길이는 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 최대한 hello 따라 결정 됩니다. 이벤트 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다. 또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.

각 이벤트는 자산에 연결됩니다. toopublish hello 이벤트 hello에 대 한 OnDemand 로케이터를 만들어야 합니다 자산에 연결 합니다. 이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL 사용 됩니다.

채널에서는 toothree hello 여러 보관 본을 만들 수 있도록 이벤트 동시에 실행 가능한 최대 지원 같은 들어오는 스트림을 합니다. 이렇게 하면 필요에 따라 이벤트의 다른 부분 toopublish 및 보관 있습니다. 예를 들어 비즈니스 요구 사항 tooarchive 6 시간의 이벤트를 있지만 toobroadcast만 마지막 10 분입니다. tooaccomplish이를 동시에 실행 가능한 두 개의 toocreate 필요한 이벤트입니다. 하나의 이벤트 tooarchive 6 시간의 이벤트 hello 설정 되어 있지만 hello 프로그램 게시 되지 않습니다. hello 다른 이벤트 집합 tooarchive 10 분 동안 이며이 프로그램이 게시 됩니다.

새 이벤트에 기존 프로그램을 다시 사용할 수 없습니다. 대신, 각 이벤트에 대해 새 프로그램을 만들고 시작합니다.

스트리밍 및 보관 준비 toostart 있을 때는 행사/프로그램을 시작 합니다. Hello 이벤트 toostop 스트리밍 및 hello 이벤트를 보관 하려는 경우 중지 합니다. 

toodelete 보관 된 콘텐츠 중지 되어 hello 이벤트를 삭제 하 고 hello 관련된 자산을 삭제 합니다. Hello 이벤트;에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다. 

중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오.

수행 tooretain hello 보관 된 콘텐츠, 하지만 스트리밍에 사용할 수 없는, hello 스트리밍 로케이터를 삭제 합니다.

### <a name="createstartstop-events"></a>이벤트 만들기/시작/중지
Hello 스트림 있으면 들어오는 hello 채널 시작할 수 있습니다는 자산, 프로그램 및 스트리밍 로케이터를 만들어 이벤트 스트리밍 hello. Hello 스트림 보관 되 고 사용할 수 있는 tooviewers hello 스트리밍 끝점을 통해 확인 합니다. 

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 

두 가지 방법으로 toostart 이벤트 가지가 있습니다. 

1. Hello에서 **채널** 페이지에서 키를 눌러 **라이브 이벤트** tooadd 새 이벤트입니다.
   
    이벤트 이름, 자산 이름, 보관 창 및 암호화 옵션을 지정합니다.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    두 었으 면 **이 라이브 이벤트를 지금 게시** 옵션을 선택 hello 이벤트 hello 게시 Url 작성 됩니다.
   
    누르면 **시작**준비 toostream hello 이벤트 때마다, 합니다.
   
    Hello 이벤트를 시작 하면 누르면 **조사식** toostart hello 콘텐츠를 재생 합니다.
2. 또는 바로 가기 및 키를 눌러를 사용할 수 있습니다 **Go Live** hello 단추 **채널** 페이지. 그러면 기본 자산, 프로그램 및 스트리밍 로케이터가 만들어집니다.
   
    hello 이벤트 이름은 **기본** hello 보관 창은 설정 되어 too8 시간입니다.

Hello hello에서 게시 된 이벤트를 볼 수 있습니다 **라이브 이벤트** 페이지. 

**가동 안 함**을 클릭하면 라이브 이벤트를 모두 중지합니다. 

## <a name="watch-hello-event"></a>조사식 hello 이벤트
toowatch hello 이벤트 클릭 **조사식** 스트리밍 URL Azure 포털 또는 복사 hello hello와 원하는 플레이어를 사용 합니다. 

![생성일](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

라이브 이벤트는 자동으로 중지 될 때 이벤트 tooon 주문형 콘텐츠를 변환 합니다.

## <a name="clean-up"></a>정리
이벤트 스트리밍 작업을 마쳤으면 tooclean 이전에 프로 비전 하는 hello 리소스를 원하는 절차를 수행 하는 hello를 수행 하세요.

* Hello 스트림 hello 인코더에서 밀어넣기를 중지 합니다.
* Hello 채널을 중지 합니다. Hello 채널 중지 되 고 나면 비용이 발생 하지는 않습니다. Toostart 필요한 경우 다시 것은 hello 동일 수집 URL tooreconfigure 인코더 필요 하지 않습니다.
* 주문형 스트림으로 라이브 이벤트 toocontinue tooprovide hello 보관 하려는 경우가 아니면 스트리밍 끝점을 중지할 수 있습니다. Hello 채널이 중지 상태인 경우 비용이 발생 하지 않습니다.

## <a name="view-archived-content"></a>보관된 콘텐츠 보기
중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오. 이벤트에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다. 

toomanage 자산, 선택 **설정** 클릭 **자산**합니다.

![자산](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>고려 사항
* 현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다. 오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오.
* 끝점을 toostream 하려는 콘텐츠 스트리밍 hello hello에 있는지 확인 **실행** 상태입니다.

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

