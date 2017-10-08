---
title: "RemoteApp-몇 가지 일반적인 시나리오와 네트워크 대역폭 사용량 테스트 aaaAzure | Microsoft Docs"
description: "Azure RemoteApp에 필요한 네트워크 대역폭을 확인할 수 있도록 해주는 일반적인 사용량 시나리오에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp - 몇 가지 일반적 시나리오로 네트워크 대역폭 사용량 테스트
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

설명한 것 처럼 [예상 Azure RemoteApp 네트워크 대역폭 사용량](remoteapp-bandwidth.md), hello Azure RemoteApp tooyour 네트워크의 어떤 hello 영향을은 toorun 가장 좋은 방법은 toofigure 일부 사용 테스트 합니다. 집합 시간 기간 및 측정값 hello에 필요한 대역폭 각 시나리오에 대 한 이러한 테스트를 실행 합니다. Hello 기능이 있는 경우 hello 네트워크 패킷 손실 되 고 네트워크 지터 toounderstand hello 네트워크 패턴 특정 환경에 만들어질 수도 측정할 수 있습니다.

Hello 대역폭 사용량을 평가 하는, 여러 사용자가 회사 내에서 다르게 사용 해야 합니다. 예를 들어 일반적으로 텍스트를 읽거나 기록하는 사용자는 동영상으로 작업하는 사용자보다 적은 대역폭을 사용합니다. 최상의 결과 사용자 요구 사항 검토 하 고 회사의 hello 사용자를 가장 잘 나타내는 hello 다음 시나리오를 혼합 하 여 만듭니다. 너무 기억[대역폭 사용량 및 사용자 영향을 주는 검토 hello 요소 발생](remoteapp-bandwidthexperience.md) -을 도와 주는 hello 이상적인 테스트를 식별 합니다.

Hello 테스트에 대 한 첫 번째 읽기 여 조합을 선택 하 고 실행 합니다. Toohelp 추적 성능 아래 hello 표를 사용할 수 있습니다.

> [!NOTE]
> 직접 네트워크 테스트를 할 수 없습니다 않거나 없는 hello 시간 toodo 하므로, 체크 아웃 우리의 [기본 네트워크 대역폭 예상치/권장 사항을](remoteapp-bandwidthguidelines.md)합니다. 그러나 진행 정도가 다양할 수 있으므로 *가능하면* 자체 테스트를 실시합니다.
> 
> 

## <a name="hello-usage-tests"></a>hello 사용 테스트
이들 각각의 테스트는 실행 시간이 다르고 네트워크 대역폭을 사용하는 다양한 함수/기능을 테스트합니다. 각 회사 사용자에 게 가장 잘 맞는 테스트 toochoose hello 혼합을 기억 합니다.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>고급/복잡한 PowerPoint - 900-1000초 동안 실행
사용자는 전체 화면 모드로 Microsoft Office PowerPoint를 사용하여 45-50개 사이의 고품질 슬라이드를 표시합니다. 이미지, 전환 (애니메이션과) 및 회사에 대 한 일반 않은 색 그라데이션 사용 하 여 배경을 hello 슬라이드 포함 되어야 합니다. hello 사용자 각 슬라이드에 20 초 이상 걸리는 해야 합니다.

이 시나리오는 슬라이드 toohello 다음 프레젠테이션의 슬라이드에 hello 전환 될 때 돌발적 트래픽을 만듭니다.

### <a name="simple-powerpoint---run-for-620-seconds"></a>간단한 PowerPoint - 620초 이하 동안 실행
사용자는 전체 화면 모드로 Microsoft Office PowerPoint를 사용하여 약 30개의 슬라이드로 이루어진 간단한 PowerPoint 파일을 표시합니다. hello 슬라이드 텍스트를 많이 보다 hello 임원/복잡 한 PowerPoint 시나리오에서는 하며 배경 및 이미지 (검정 다이어그램)를 더 간단 합니다. 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer - 250초 이하 동안 실행
사용자가 Internet Explorer를 사용 하 여 hello 웹을 탐색 합니다. hello 사용자가 선택한 텍스트, 자연 스러운 이미지 및 일부 계통도 다이어그램의 조합입니다. hello hello로 원격 데스크톱 세션 호스트 (RD 세션 호스트) 서버 hello의 로컬 디스크 드라이브에 저장 하는 웹 페이지는 합니다. MHT 파일입니다. Page Up, Page Down, 위쪽 및 아래쪽 키를 사용 하 여 각 키/유형의 스크롤에 대 한 다양 한 간격으로 스크롤 하는 hello 사용자:

    - Down - 250 keystrokes very 500 ms
    - Page Up - 36 keystrokes every 1000 ms
    - Down - 75 keystrokes every 100 ms
    - Page Down - 20 keystrokes every 500 ms
    - Up - 120 keystrokes every 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>PDF 문서 - 간단한 문서 - 610초 이하 동안 실행
사용자는 Adobe Acrobat Reader를 사용하여 다양한 방법으로 PDF 문서를 읽고 검색합니다. 테이블, 간단한 그래프 및 여러 텍스트 글꼴 hello 문서 구성 되어야 합니다. hello 문서는 35 40 페이지입니다. hello 사용자 스크롤 하는 두 개의 서로 다른 속도로 뒤와 4 개의 다른 확대/축소 크기로 전달 (toopage, 적합된 한 toowidth 맞게 100%와 선택한 다른). 확대/축소 hello 여러 크기로 hello 텍스트 (글꼴)가 렌더링 되는지 확인 합니다. 스크롤는 hello Page Up, Page Down, 위쪽 및 아래쪽 키를 사용 하 여 각 스크롤에 대 한 다양 한 간격으로 중단 되었습니다.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>PDF 문서 - 혼합 문서 - 320초 이하 동안 실행
사용자는 Adobe Acrobat Reader를 사용하여 다양한 방법으로 PDF 문서를 읽고 검색합니다. hello 문서 이미지 품질 (사진 포함), 테이블, 간단한 그래프 및 여러 텍스트 글꼴 구성 됩니다. hello 사용자 스크롤 하는 두 개의 서로 다른 속도로 뒤와 4 개의 다른 확대/축소 크기로 전달 (toopage, 적합된 한 toowidth 맞게 100%와 선택한 다른). 확대/축소 hello 여러 크기로 hello 텍스트 (글꼴)가 렌더링 되는지 확인 합니다. 스크롤는 hello Page Up, Page Down, 위쪽 및 아래쪽 키를 사용 하 여 각 스크롤에 대 한 다양 한 간격으로 중단 되었습니다.

### <a name="flash-video-playback---run-for-180-seconds"></a>플래시 비디오 재생 - 180초 이하 동안 실행
사용자는 웹 페이지에 포함된 Adobe Flash 인코드된 동영상을 봅니다. hello 웹 페이지는 hello hello RD 세션 호스트 서버의 로컬 하드 드라이브에 저장 됩니다. hello 비디오 플레이어가 포함된 플러그 인에서 Internet Explorer 내에 재생 됩니다.

이 시나리오는 멀티미디어를 포함하는 풍부한 콘텐츠 웹 페이지를 보는 사용자를 에뮬레이트합니다. 대부분의 hello 데이터 VOBR 통해 bo 해야 합니다.

### <a name="word-remote-typing---run-for-1800-seconds"></a>단어 원격 입력 - 1800초 이하 동안 실행
사용자가 RDP 세션을 통해 문서를 입력합니다. 키 입력 hello 원격 세션에서 실행 하는 hello RDP 세션 tooa Microsoft Word에서 문서를 통한 hello 클라이언트 쪽에서 전송 됩니다. hello 급여를 입력 한 문자 마다 250 밀리초 (총 7050 문자)입니다. 

지식 근로자에 대 한 hello 가장 일반적인 시나리오 중 하나입니다. 이 시나리오는 최신 작업 프로세서에를 입력 하는 사용자의 hello 응답성을 테스트 합니다. 이 시나리오는 대역폭 사용량에 중요 한 tooeven 약간 변경 합니다.

## <a name="tracking-hello-test-results"></a>Hello 테스트 결과 추적
Hello 다음 환경에서 테이블 tooevaluate hello 시나리오를 사용할 수 있습니다. 아래에 제공 된 hello 데이터는 설명을 돕기 위해 방금-관찰 하기를 따라 크게 달라질 수 있습니다. 

간단한 설명을 위해 hello 동일한 1920 x 1080 픽셀이 화면 해상도 사용 하 여 모든 시나리오는 테스트 및 hello 120 ms + 표시 약 1%에서 200 밀리초와 네트워크 미만의 대기 시간 (지연)를 사용 하 여 네트워크에서 TCP 전송 지터 가정 합니다.

에 대 한 hello 표:

* **평균 경험** hello 사용자 생산성 크게 영향을 받지 없지만 가끔 비디오 또는 오디오 결함 제외 되지 않은 경우 네트워크 대역폭을 포함 합니다. hello 시스템 수 toorecover hello 동적 논리를 활용 하 여 신속 하 게 됩니다. hello 네트워크 대역폭 예상치 시도 tooguarantee hello 품질 hello 사용자 환경의입니다.
  * **별다른 문제 (중단점)** hello 네트워크 대역폭 여기서 사용자 경험에 관한 주요 눈에 띄지 하 고 측정 가능한 기간에 대 한 해당 생산성은 영향을 포함 합니다. 이 시점에서 hello RDP 알고리즘 메시징 및 부족 하 여 네트워크 대역폭으로 인해 환경의 hello 사용자의 품질을 보장할 수 없습니다.
  * **권장** 좋은 또는 뛰어난 경험에 대 한 권장 hello 네트워크 대역폭을 포함 합니다. 일반적으로 한 단계 hello 해당 hello 값 보다 높은 **경험 평균** 열입니다.
  * **참고** 에는 관찰 내용 및 설명이 포함됩니다.

| 테스트 | 평균 환경 | 눈에 띄는 문제(중단점) | 권장 네트워크 대역폭 | 참고 |
| --- | --- | --- | --- | --- |
| 고급/복잡한 PPT |10MB/초 |1MB/초 |>10MB/s, 100MB/s 선호 |1MB/s에서 많은 애니메이션이 손실됨 |
| 간단한 PPT |5MB/초 |256KB/초 |10MB/초 |현저한 지연이 함께 로드 hello 슬라이드에서 256 k B/초 |
| Internet Explorer |10MB/초 |1MB/초 |>10MB/s, 100MB/s 선호 |1MB/s에서 웹 동영상이 흐리고 고르지 못함, 빠른 스크롤 시 문제 발생 |
| 간단한 PDF |1MB/초 |256KB/초 |5MB/초 |256 KB/s에서까지 약간의 시간이 tooload hello 페이지 |
| 혼합 PDF |1MB/초 |256KB/초 |5MB/초 |256 k B/초 hello 페이지는 상당한 양의 시간 tooload |
| 플래시 동영상 재생 |10MB/초 |1MB/초 |>10MB/s, 100MB/s 선호 |1 MB/s에서 비디오 hello 매끄럽지 이며 일부 프레임이 손실는 |
| 단어 원격 입력 |256KB/초 |128KB/초 |1MB/초 |사용자 256 k B/초에 키 입력 간의 hello 시간 표시 될 수도 |

사용자 당 tooevaluate hello 네트워크 대역폭 다양 한 시나리오 위에 hello와 hello 해당 비율 필요한 네트워크 대역폭을 만듭니다. 시나리오에 필요한 hello 가장 높은 번호를 선택 합니다. 사용자가 거의 단독 hello 시스템을 사용 하므로 일부 예약에 동시에 작동 하는 사용자가 동일한 네트워크 hello에 대 한 고려 합니다.

## <a name="learn-more"></a>자세한 정보
* [Azure RemoteApp 네트워크 대역폭 사용량 예측](remoteapp-bandwidth.md)
* [Azure RemoteApp - 네트워크 대역폭과 체감 품질을 함께 작동하는 방식은 무엇인가요?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp 네트워크 대역폭 - 일반적인 지침(자체 테스트를 수행할 수 없는 경우)](remoteapp-bandwidthguidelines.md)

