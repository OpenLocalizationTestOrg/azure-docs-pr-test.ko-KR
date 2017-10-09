---
title: "hello Azure 콘텐츠 배달 네트워크를 통해 aaaLarge 파일 다운로드 최적화"
description: "대용량 파일 다운로드 최적화에 대해 자세히 설명합니다."
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
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Hello Azure 콘텐츠 배달 네트워크를 통해 큰 파일 다운로드 최적화

파일 크기 hello 인터넷을 통해 제공 되는 콘텐츠의 toogrow 기한 tooenhanced 기능, 향상 된 그래픽 및 리치 미디어 콘텐츠를 계속 합니다. 이러한 확장은 광대역 보급, 더 크고 저렴한 저장 장치, 고화질 비디오 확산, 인터넷 연결 장치(IoT) 등 여러 가지 요인으로 추진되고 있습니다. 큰 파일에 대 한 빠르고 효율적인 전달 메커니즘에는 중요 한 tooensure 원활 하 고 즐거운 소비자 환경입니다.

대용량 파일을 배달하는 데 있어 몇 가지 과제가 있습니다. 첫째, 응용 프로그램 데이터를 모두 순차적으로 다운로드할 수 있습니다. 때문에 hello 평균 시간 toodownload 큰 파일 중요할 수 있습니다. 경우에 따라 응용 프로그램 hello hello 첫 번째 부분 대기 시키기 전에 파일의 마지막 부분을 다운로드할 수 있습니다. 를 소량의 파일을 요청 하거나 다운로드를 놓을 때 hello 다운로드 실패할 수 있습니다. 또한 hello 다운로드는 hello 후 (CDN) 콘텐츠 배달 네트워크에서 원본 서버 hello hello 전체 파일을 검색 될 때까지으로 지연 될 수 있습니다. 

둘째, 사용자의 컴퓨터 및 hello 파일 간의 hello 대기 시간 결정 hello 속도는 콘텐츠를 볼 수 있습니다. 또한 네트워크 정체 및 용량 문제도 처리량에 영향을 줍니다. 사용자와 서버 간의 거리 패킷 손실 toooccur 품질 감소에 대 한 추가 기회를 창출 합니다. 품질의 hello 감소 처리량을 제한 하 여 발생 하 여 증가 된 패킷 손실이 파일 다운로드 toofinish에 대 한 hello 대기 시간이 늘어날 수 있습니다. 

셋째, 많은 대용량 파일이 전체적으로 배달되지 않습니다. 사용자는 중간 부분 다운로드를 취소할 수 있습니다 또는 hello 몇 분이 지나면 긴 MP4 비디오를 시청 합니다. 따라서 소프트웨어와 미디어 배달 회사 요청 되는 파일의 유일한 hello 부분을 toodeliver 합니다. Hello 효율적으로 배포할 요청 부분 hello 원본 서버에서 hello 들어오고 나가는 트래픽이 감소 했습니다. 효율적인 배포 hello 메모리와 I/O 압력 hello 원본 서버에서 줄어듭니다. 

이제 hello Azure 콘텐츠 배달 네트워크 Akamai에서 전달 하는 큰 파일 효율적으로 toousers 배율로 hello 전세계 기능을 제공 합니다. hello 기능은 hello 원본 서버의 hello 로드가 감소 하므로 대기 시간을 줄여 줍니다. 이 기능은 hello Akamai 표준 가격 책정 계층을 사용할 수 있습니다.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>큰 파일의 CDN 끝점 toooptimize 배달을 구성합니다

CDN 끝점 toooptimize 배송 hello Azure 포털을 통해 큰 파일을 구성할 수 있습니다. 또한 REST Api를 사용할 수 있습니다 또는이 클라이언트 Sdk toodo 환영 중 하나입니다. hello 다음 단계 프로세스를 보여 hello hello Azure 포털을 통해.

1. hello에 새 끝점의 경우 tooadd **CDN 프로필** 페이지에서 **끝점**합니다.

    ![새 끝점](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. Hello에 **에 대 한 액세스에 최적화 된** 드롭 다운 목록 **큰 파일을 다운로드**합니다.

    ![대용량 파일 최적화 선택](./media/cdn-large-file-optimization/02_Creating.png)


Hello CDN 끝점을 만든 후에 특정 기준에 일치 하는 모든 파일에 대 한 hello 큰 파일을 최적화 적용 됩니다. hello 다음 섹션에서는이 프로세스를 설명 합니다.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Akamai hello Azure 콘텐츠 배달 네트워크를 사용 하 여 큰 파일의 배달을 위해 최적화

hello 큰 파일을 최적화 형식 기능 빠르고 반응성 네트워크 최적화 및 구성 toodeliver 큰 파일을 설정합니다. Akamai와 일반 웹 배달 1.8 g B 아래에 파일을 캐시 및 터널 (캐시) 수를 too150 GB 파일입니다. 큰 파일을 최적화 too150 GB 파일을 캐시 합니다.

대용량 파일 최적화는 특정 조건이 충족될 때 효과적입니다. 조건에는 원본 서버 hello 작동 하는 방법 및 hello 크기와 요청 된 hello 파일 형식을 포함 됩니다. 이 주제에 대 한 세부 정보에 들어가기 전에 hello 최적화의 작동 원리를 이해 해야 합니다. 

### <a name="object-chunking"></a>개체 청크 

Akamai에서 Azure 콘텐츠 배달 네트워크 hello 개체 청크 이라는 기술을 사용 합니다. 큰 파일 요청 되 면 hello CDN hello 원점에서 hello 파일의 더 작은 부분을 검색 합니다. Hello CDN POP 지/서버는 full 또는 바이트 범위 파일 요청을 받은 후이 최적화에 대 한 hello 파일 형식이 지원 되는지 여부를 확인 합니다. 또한 hello 파일 형식을 hello 파일 크기 요구 사항을 충족 하는지 확인 합니다. Hello 파일 크기가 10 MB 보다 큰 경우 hello CDN에 지 서버 hello 파일 hello 출처 2MB의 청크에서를 요청 합니다. 

Hello 청크 hello CDN 가장자리에 도착 하면 캐시 된이 있으며 즉시 toohello 사용자를 제공 합니다. CDN hello 다음 병렬로 hello 다음 청크 사전 인출 합니다. 이 사전 인출 된 hello 콘텐츠 대기 시간이 단축 하는 hello 사용자 미리 하나의 청크를 유지 하는 것을 보장 합니다. 이 프로세스 전체 hello 될 때까지 계속 됩니다 (요청 된 경우) 파일을 다운로드할 바이트 범위를 모든 요청할 경우에 사용할 수 있는, 또는 hello 클라이언트 hello 연결을 종료 합니다. 

Hello 바이트 범위 요청에 대 한 자세한 내용은 참조 하십시오. [RFC 7233](https://tools.ietf.org/html/rfc7233)합니다.

CDN hello 받을 때 처럼 모든 청크를 캐시 합니다. 전체 파일 hello toobe hello CDN에 캐시에 캐시 되어 있지 않습니다. Hello 파일 또는 바이트 범위에 대 한 후속 요청은 hello CDN 캐시에서에서 제공 됩니다. 일부 hello 청크 hello CDN에 캐시 되는 경우 프리페치는 hello 원점에서 사용 되는 toorequest 청크 합니다. 이 최적화는 hello 증명 hello 원본 서버 toosupport 바이트 범위 요청을 사용합니다. _원본 서버 hello 바이트 범위 요청을 지원 하지 않으면이 최적화 효과적이 지 않습니다._ 

### <a name="caching"></a>구성
대용량 파일 최적화는 일반 웹 배달과 다른 기본 caching-expiration(캐싱 만료) 시간을 사용합니다. HTTP 응답 코드에 따라 양수 캐싱과 음수 캐싱을 구분합니다. 원본 서버 hello 캐시 제어를 통해 만료 시간을 지정 하거나 hello에 대 한 응답 헤더를 만료, hello CDN 해당 값을 준수 합니다. Hello 원본 지정 하지 않으면 hello 파일에는 이와 같은 최적화에 대 한 hello 유형 및 크기 조건과 일치 하는 경우 CDN hello 큰 파일을 최적화에 대 한 hello 기본값을 사용 합니다. 그렇지 않으면 hello CDN는 일반 웹 배달에 대 한 기본값을 사용 합니다.


|    | 일반 웹 | 대용량 파일 최적화 
--- | --- | --- 
캐싱: 긍정 <br> HTTP 200, 203, 300, <br> 301, 302 및 410 | 7 일 |1일  
캐싱: 부정 <br> HTTP 204, 305, 404 <br> 및 405 | 없음 | 1초 

### <a name="deal-with-origin-failure"></a>원본 오류 처리

hello 원본 읽기 제한 길이 hello 큰 파일을 최적화 형식에 대 한 일반 웹 배달 tootwo 분 동안 2 초에서 증가합니다. 이 처럼 증가 hello 더 큰 파일 크기 tooavoid 시기 상 조일 시간 초과 연결을 차지합니다.

연결 시간 초과 되 면 hello CDN에는 "-504 게이트웨이 시간 초과" 오류 toohello 클라이언트를 보내기 전에 횟수 만큼 다시 시도 합니다. 

### <a name="conditions-for-large-file-optimization"></a>대용량 파일 최적화에 대한 조건

다음 표에서 hello hello 집합이 조건 toobe 큰 파일을 최적화를 위해 만족된 보여 줍니다.

조건 | 값 
--- | --- 
지원되는 파일 형식 | 3g2, 3gp, asf, avi, bz2, dmg, exe, f4v, flv, <br> gz, hdp, iso, jxr, m4v, mkv, mov, mp4, <br> mpeg, mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
최소 파일 크기 | 10MB 
최대 파일 크기 | 150GB 
원본 서버 특성 | 바이트 범위 요청을 지원해야 함 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Verizon hello Azure 콘텐츠 배달 네트워크를 사용 하 여 큰 파일의 배달을 위해 최적화

hello Verizon에서 Azure 콘텐츠 배달 네트워크 파일 크기에 대 한 한도가 하지 않고 큰 파일을 제공합니다. 추가 기능으로 켜져 있습니다 큰 파일의 기본 toomake 배달 속도가 빨라집니다.

### <a name="complete-cache-fill"></a>전체 캐시 채우기

hello 기본 전체 캐시 채우기 기능 hello 캐시로 hello CDN toopull 파일을 통해 초기 요청은 중단 되거나 손실 되는 경우. 

전체 캐시 채우기는 대규모 자산에 가장 유용합니다. 일반적으로 사용자가 시작 toofinish에서 다운로드 하지 않습니다. 점진적 다운로드를 사용합니다. hello 기본 동작 hello edge 서버 tooinitiate hello 원본 서버에서의 hello 자산의 배경 페치를 강제로 수행합니다. 나중에 hello 자산 hello 지 서버 로컬 캐시에서 이합니다. Hello 전체 개체에 hello 캐시 되 면 hello에 지 서버 hello 캐시 된 개체에 대 한 바이트 범위 요청 toohello CDN을 충족 합니다.

hello Verizon Premium 계층에에서 hello 규칙 엔진을 통해 hello 기본 동작을 비활성화할 수 있습니다.

### <a name="peer-cache-fill-hot-filing"></a>피어 캐시 채우기 핫파일링(hot-filing)

hello 기본 피어 캐시 채우기 핫 정리 기능은 정교한 소유 알고리즘을 사용합니다. 캐시 서버 대역폭에 따라 추가 가장자리를 사용 하 여 및 집계는 매우 인기, 큰 개체에 대 한 메트릭을 toofulfill 클라이언트 요청을 요청 합니다. 이 기능은 추가 상당히 많은 수의 tooa 사용자의 원본 서버 전송 되는 상황을 방지 합니다. 

### <a name="conditions-for-large-file-optimization"></a>대용량 파일 최적화에 대한 조건

Verizon에 대 한 hello 최적화 기능은 기본적으로 켜 집니다. 최대 파일 크기에는 제한이 없습니다. 

## <a name="additional-considerations"></a>추가 고려 사항

Hello를 이와 같은 최적화에 대 한 추가 측면을 따르는 것이 좋습니다.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Akamai의 Content Delivery Network

- 프로세스를 청크 hello toohello 원본 서버에 추가 요청을 생성 합니다. 그러나 hello 전반적인 hello 원본에서 제공 하는 데이터 양이 훨씬 작습니다. 청크 결과 hello CDN에서 캐싱 특성 정보가 개선 되었습니다.

- Hello 파일의 더 작은 부분 배달 하기 때문에 메모리 및 I/O 압력 hello 원점에 감소 됩니다.

- Hello CDN에 캐시 된 청크로 구성에 대 한 추가 요청이 없는 toohello 원점 hello 콘텐츠 만료 되거나 hello 캐시에서 제거 될 때까지 합니다.

- 사용자가 범위를 만들 수 toohello CDN에서 요청 하 고 일반 파일 처럼 처리 하는 합니다. 최적화는 올바른 파일 형식 이므로 hello 바이트 범위는 10MB-150GB 경우에 적용 됩니다. 요청 된 hello 평균 파일 크기 10 MB 보다 작은 경우 toouse 일반 웹 배달 대신 할 수 있습니다.

### <a name="azure-content-delivery-network-from-verizon"></a>Verizon의 Azure Content Delivery Network

hello 일반 웹 배달 최적화 종류는 큰 파일을 제공할 수 있습니다.
