---
title: "aaaMedia 스트리밍 hello Azure 콘텐츠 배달 네트워크를 통해 최적화"
description: "부드러운 배달을 위한 스트리밍 미디어 파일 최적화"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>미디어 스트리밍 hello Azure 콘텐츠 배달 네트워크를 통해 최적화 
 
Hd 비디오 사용 hello를 만드는 어려움 큰 파일의 배달에 대 한 인터넷에 계속 증가 하는 합니다. 고객의 비디오 부드러운 재생 필요에 따라 예상 또는 hello 세계 다양 한 네트워크와 클라이언트에서 비디오 자산을 라이브 합니다. 파일 스트리밍 미디어를 신속 하 고 효율적인 배달 메커니즘은 중요 한 tooensure 원활 하 고 즐거운 소비자 환경입니다.  

라이브 스트리밍 미디어는 hello 큰 크기 및 수가 동시 때문 비교적 쉽게 toodeliver입니다. 지연 시간이 길어서 사용자 tooleave를 발생 합니다. 라이브 스트림을 미리 캐시할 수 없습니다 및 하므로 큰 대기 시간이 허용 가능한 tooviewers 되지, 비디오 조각은 적절 한 시간 내에 배달 되어야 합니다. 

또한 스트리밍의 hello 요청 패턴 새로운 몇 가지 과제를 제공합니다. 인기 있는 라이브 스트림 또는 새 계열을 수천 주문형 비디오에 대 한 해제 될 때 뷰어 toomillions hello에 hello 스트림을 요청할 수 있습니다 동시 합니다. 이 경우 스마트 요청 통합이 중요 한 toonot 과도 한 부하가 걸리지 hello 원본 서버 hello 자산 아직 캐시 되지 않습니다.
 
이제 hello Azure 콘텐츠 배달 네트워크 Akamai에서 전달 하는 스트리밍 미디어 자산 효율적으로 toousers 배율로 hello 전세계 기능을 제공 합니다. hello 기능은 hello 원본 서버의 hello 로드가 감소 하므로 대기 시간을 줄여 줍니다. 이 기능은 hello Akamai 표준 가격 책정 계층을 사용할 수 있습니다. 

Azure 콘텐츠 배달 네트워크에서 Verizon hello hello 일반 웹 배달 최적화 형식에서 직접 스트리밍 미디어를 제공합니다.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>끝점 toooptimize에서에서 미디어 스트리밍을 hello Akamai에서 Azure 콘텐츠 배달 네트워크를 구성 합니다.
 
Hello Azure 포털을 통해 큰 파일에 대 한 콘텐츠 배달 네트워크 (CDN) 끝점 toooptimize 배송을 구성할 수 있습니다. 또한 REST Api를 사용할 수 있습니다 또는이 클라이언트 Sdk toodo 환영 중 하나입니다. hello 다음 단계 프로세스를 보여 hello hello Azure 포털을 통해:

1. hello에 새 끝점의 경우 tooadd **CDN 프로필** 페이지에서 **끝점**합니다.
  
    ![새 끝점](./media/cdn-media-streaming-optimization/01_Adding.png)

2. Hello에 **에 대 한 액세스에 최적화 된** 드롭 다운 목록 **요청 시 미디어 스트리밍 비디오** 주문형 비디오 자산에 대 한 합니다. 라이브 및 주문형 비디오 스트리밍을 조합하는 경우 **일반 미디어 스트리밍**을 선택합니다.

    ![스트리밍 선택됨](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Hello 끝점을 만든 후에 특정 기준에 일치 하는 모든 파일에 대 한 hello 최적화를 적용 됩니다. hello 다음 섹션에서는이 프로세스를 설명 합니다. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>미디어 스트리밍 hello Akamai에서 Azure 콘텐츠 배달 네트워크에 대 한 최적화
 
Akamai의 미디어 스트리밍 최적화는 배달에 개별 미디어 조각을 사용하는 라이브 또는 주문형 비디오 스트리밍 미디어에 효과적입니다. 이 프로세스는 점진적 다운로드 또는 바이트 범위 요청을 통해 전송되는 단일 대규모 자산과 다릅니다. 해당 스타일의 미디어 배달에 대한 자세한 내용은 [대용량 파일 최적화](cdn-large-file-optimization.md)를 참조하세요.


hello 일반 미디어 배달 또는 주문형 비디오 미디어 배달 최적화 종류 사용 CDN 백 엔드 최적화 toodeliver 미디어 자산 속도가 빨라집니다. 또한 시간이 지남에 따라 학습된 모범 사례에 따라 미디어 자산에 대한 구성을 사용합니다.

### <a name="caching"></a>구성

Hello Akamai에서 Azure 콘텐츠 배달 네트워크에서 해당 hello 자산 스트리밍 매니페스트 나 조각이를 감지 하면 일반 웹 배달 서로 다른 캐시 만료 시간을 사용 합니다. (다음 표는 hello hello 전체 목록 참조). 늘 그렇듯이 cache-control 또는 Expires 헤더 hello 원점에서 보낸 적용 됩니다. Hello 자산 미디어 자산을 없으면 일반 웹 배달에 대 한 hello 만료 시간을 사용 하 여 캐시 합니다.

hello 짧은 음수 캐싱 시간이 여러 사용자가 아직 존재 하지 않는 조각을 요청할 때 원래 오프 로드 유용 합니다. 예를 hello 패킷에 사용할 수 없습니다 hello 원점에서 해당 초 라이브 스트림을입니다. hello 더 이상 캐싱 간격은 또한 비디오 콘텐츠 일반적으로 수정 되지 않습니다 hello 원점에서 요청을 오프 로드할 수 있습니다.
 

|    | 일반<br> web<br>배달 | 일반<br> 미디어<br> 스트리밍 | 주문형 비디오 <br>미디어<br> 스트리밍  
--- | --- | --- | ---
캐싱: 긍정 <br> HTTP 200, 203, 300, <br> 301, 302 및 410 | 7 일 |365일 | 365일   
캐싱: 부정 <br> HTTP 204, 305, 404 <br> 및 405 | 없음 | 1초 | 1초
 
### <a name="deal-with-origin-failure"></a>원본 오류 처리  

일반 미디어 배달 및 주문형 비디오 미디어 배달에도 일반적인 요청 패턴에 대한 모범 사례에 기반한 원본 시간 제한 및 다시 시도 로그가 있습니다. 예를 들어 일반 미디어 전달에 대 한 실시간 이며 주문형 비디오 미디어 배달 사용 toohello 시간이 중요 한 특성으로 인해 더 짧은 연결 제한 시간 때문에 라이브 스트리밍.

연결 시간 초과 되 면 hello CDN에는 "-504 게이트웨이 시간 초과" 오류 toohello 클라이언트를 보내기 전에 횟수 만큼 다시 시도 합니다. 

파일 hello 파일 형식 및 크기 조건 목록과 일치 하는 경우 CDN hello 미디어 스트리밍에 대 한 hello 동작을 사용 합니다. 그렇지 않으면 일반 웹 배달을 사용합니다.
   
### <a name="conditions-for-media-streaming-optimization"></a>미디어 스트리밍 최적화에 대한 조건 

다음 표에서 hello hello 집합이 조건 toobe 미디어 스트리밍 최적화 만족된 보여 줍니다. 
 
지원되는 스트리밍 유형 | 파일 확장명  
--- | ---  
Apple HLS | m3u8, m3u, m3ub, key, ts, aac
Adobe HDS | f4m, f4x, drmmeta, bootstrap, f4f,<br>Seg-Frag URL 구조 <br> (일치하는 regex: ^(/.*)Seq(\d+)-Frag(\d+)
DASH | mpd, dash, divx, ismv, m4s, m4v, mp4, mp4v, <br> sidx, webm, mp4a, m4a, isma
부드러운 스트리밍 | /manifest/,/QualityLevels/Fragments/
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>미디어 스트리밍 hello Verizon에서 Azure 콘텐츠 배달 네트워크에 대 한 최적화

Azure 콘텐츠 배달 네트워크에서 Verizon hello hello 일반 웹 배달 최적화 유형을 사용 하 여 직접 스트리밍 미디어 자산을 배달 합니다. 기본적으로 미디어 자산을 배달에 몇 가지 기능 hello CDN에서 직접 지원 합니다.

### <a name="partial-cache-sharing"></a>부분 캐시 공유

부분 캐시 공유 hello CDN tooserve 부분적으로 캐시 된 콘텐츠 toonew 요청 수 있습니다. 예를 들어 hello 첫 번째 요청 toohello CDN 캐시 누락에 결과가 hello 요청이 toohello 원점을 전송 됩니다. 불완전 한이 콘텐츠가 hello CDN에 캐시에 로드 되지만 다른 요청 toohello CDN이이 데이터를 가져오는 시작할 수 있습니다. 

### <a name="cache-fill-wait-time"></a>캐시 채우기 대기 시간

 hello 캐시 채우기 대기 시간 기능에는 모든 후속 요청에 대 한 HTTP 응답 헤더 hello 원본 서버에서 도착할 때까지 동일한 리소스 hello hello edge 서버 toohold 강제로 수행 합니다. Hello 타이머가 만료 전에 도착할 때까지 hello 원점에서 HTTP 응답 헤더, 대기 중으로 저장 된 모든 요청은 캐시 증가 하 고 hello에서 제공 됩니다. Hello에 이와 hello 캐시가 hello 원본 데이터로 채워집니다. 기본적으로 hello 캐시 채우기 대기 시간 too3, 000 밀리초 설정 됩니다. 

