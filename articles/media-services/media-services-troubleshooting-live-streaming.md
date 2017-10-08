---
title: "라이브 스트리밍을 위한 aaaTroubleshooting 가이드 | Microsoft Docs"
description: "이 항목에서는 어떻게 tootroubleshoot 라이브 스트리밍 문제에서 제안 사항을 제공 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>라이브 스트리밍 문제 해결 가이드
이 항목에서는 방법에 제안을 제공 tootroubleshoot 일부 라이브 스트리밍 문제입니다.

## <a name="issues-related-tooon-premises-encoders"></a>관련 된 문제 tooon 온-프레미스 인코더
이 섹션에서는 제안 된 tootroubleshoot 문제 관련된 tooon 온-프레미스 인코더 toosend를 구성 하는 방법에 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널을 제공 합니다.

### <a name="problem-would-like-toosee-logs"></a>문제: toosee 로그 려 합니다.
* **잠재적인 문제**: 문제를 디버그할 때 도움이 될 만한 인코더 로그를 찾을 수 없습니다.
  
  * **Telestream Wirecast**: 보통 C:\Users\{username}\AppData\Roaming\Wirecast\에서 로그를 찾을 수 있습니다. 
  * **실세계 Live**: 링크 toologs hello 관리 포털에 찾을 수 있습니다. **통계**, **로그**를 차례로 클릭합니다. Hello에 **로그 파일** 페이지 LiveEvent 항목 hello; 현재 세션을 일치 하는 hello 선택 모두에 대 한 로그의 목록이 표시 됩니다. 
  * **Media 라이브 인코더 플래시**: hello를 찾을 수 있습니다 **로그 디렉터리 중...**  toohello 이동 하 여 **인코딩 로그** 탭 합니다.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>문제: 점진적 스트림을 출력하기 위한 옵션이 없습니다.
* **잠재적인 문제**: hello 인코더를 사용 하 고 자동으로 디인터레이스 하지 않습니다. 
  
    **문제 해결 단계**: hello 인코더 인터페이스에서 인터레이스 취소 옵션을 찾습니다. 디인터레이스를 사용하도록 설정한 후 다시 점진적 출력 설정을 확인합니다. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>문제: 몇 가지 인코더 출력 설정 및 아직도 없습니다 tooconnect 하려고 했습니다.
* **잠재적인 문제**: Azure 인코딩 채널이 올바르게 다시 설정되지 않았습니다. 
  
    **문제 해결 단계**: 확인 되었는지 hello 인코더 tooAMS 푸시합니다 더 이상, 중지 및 hello 채널을 다시 설정 합니다. 다시 실행 되 면 hello 새 설정을 사용 하 여 인코더를 연결 하십시오. 이 아직 해결 되지 않으면 hello 문제를 완전히 새 채널을 만들어 보세요, 경우에 따라 채널 손상 될 수 있습니다 여러 번의 실패 후 합니다.  
* **잠재적인 문제**: hello GOP 크기 또는 키 프레임 설정은 최적이 아닙니다. 
  
    **문제 해결 단계**: 권장 GOP 크기 또는 키프레임 간격은 2초입니다. 일부 인코더는 이 설정을 프레임 단위로 계산하는 반면, 다른 인코더는 초를 사용합니다. 예를 들어: 30fps를 출력할 때 hello GOP 크기 것 60 프레임은 해당 too2 초입니다.  
* **잠재적인 문제**: 닫힌된 포트 hello 스트림을 차단 합니다. 
  
    **문제 해결 단계**: RTMP 통해 스트리밍할 때 방화벽 및/또는 프록시 설정 tooconfirm 1935 및 1936 아웃 바운드 포트가 열려 있는지 확인 합니다. RTP 스트리밍을 사용하는 경우 아웃바운드 포트 2010이 열려 있는지 확인합니다. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>문제: hello 인코더 toostream hello RTP 프로토콜을 구성할 때 위치가 없으므로 tooenter 호스트 이름입니다.
* **잠재적인 문제**: 많은 RTP 인코더 호스트 이름에 허용 되지 않는 및 IP 주소 toobe 획득 해야 합니다.  
  
    **문제 해결 단계**: toofind hello IP 주소, 모든 컴퓨터에서 명령 프롬프트를 엽니다. windows에서이 열 toodo 실행 시작 관리자 (WIN + R) hello 및 tooopen "cmd"를 입력 합니다.  
  
    Hello 명령 프롬프트를 연 후에 "Ping [AMS 호스트 이름]"를 입력 합니다. 
  
    hello 호스트 이름으로 다음 예제는 hello 강조 표시 된 hello Azure 수집 URL에서에서 포트 번호 hello를 생략 하 여 파생 될 수 있습니다. 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> 있습니다 수 없는 성공적으로 이전 처럼 스트리밍할 hello 문제 해결 단계를 따른 후 경우 hello Azure 포털을 사용 하 여 지원 티켓을 제출 합니다.
> 
> 

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

