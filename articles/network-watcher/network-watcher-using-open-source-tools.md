---
title: "Azure 네트워크 감시자 오픈 소스 도구와 aaaVisualize 네트워크 트래픽 패턴 | Microsoft Docs"
description: "이 페이지에서는 toouse 네트워크 감시자 패킷 캡처 Capanalysis toovisualize 트래픽 패턴 tooand 내 vm에서을 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>오픈 소스 도구를 사용 하 여 Vm에서 네트워크 트래픽 패턴 tooand 시각화

패킷 캡처 tooperform 네트워크 법정 데이터와 심층 패킷 검사 수 있는 네트워크 데이터를 포함 합니다. Tooanalyze 패킷 캡처 toogain insights를 사용 하 여 네트워크에 대 한 소스 도구는 많은 열립니다. 이러한 도구 중 하나는 오픈 소스 패킷 캡처 시각화 도구인 CapAnalysis입니다. 패킷 캡처 데이터를 시각화는 tooquickly 패턴 및 네트워크 내에서 잘못 된 부분에 대 한 통찰력을 파생 하는 귀중 한 방법입니다. 또한 시각화는 이러한 정보를 손쉽게 공유할 수 있는 수단을 제공합니다.

Azure의 네트워크 감시자를 네트워크에 기능 toocapture tooperform 패킷을 허용 하 여이 중요 한 데이터를 캡처합니다 hello 제공 합니다. 이 문서에서는 패킷에서 toovisualize 및 게인 insights 캡처합니다 CapAnalysis 네트워크 감시자를 사용 하 여 하는 방법을 보여 주는 연습을 제공 합니다.

## <a name="scenario"></a>시나리오

배포 하는 간단한 웹 응용 프로그램이 Azure 원하는 toouse 오픈 소스 도구 toovisualize에서 VM에 해당 네트워크 트래픽을 tooquickly 가능한 오류를 확인 및 흐름 패턴을 식별 합니다. Network Watcher를 사용하면 네트워크 환경의 패킷 캡처를 획득하여 저장소 계정에 바로 저장할 수 있습니다. 그런 다음 CapAnalysis hello 패킷 캡처 직접 hello 저장소 blob에서 수집 하 고 해당 콘텐츠를 시각화할 수 있습니다.

![시나리오][1]

## <a name="steps"></a>단계

### <a name="install-capanalysis"></a>CapAnalysis 설치

tooinstall CapAnalysis 가상 컴퓨터에서 toohello 공식 지침을 참조할 수 있습니다 여기 https://www.capanalysis.net/ca/how-to-install-capanalysis 합니다.
순서 CapAnalysis를 원격으로 액세스, 새 인바운드 보안 규칙을 추가 하 여 VM에 tooopen 포트 9877 필요 합니다. 네트워크 보안 그룹의 규칙을 만드는 방법에 대 한 자세한 참조 너무[기존 NSG에서 규칙을 만들](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg)합니다. 수 tooaccess CapAnalysis 있어야 hello 규칙 성공적으로 추가 되 면에서`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Azure 네트워크 감시자 toostart 패킷을 캡처 세션을 사용 하 여

네트워크 감시자는 가상 컴퓨터를 내부 및 외부로 toocapture 패킷을 tootrack 트래픽을 허용합니다. Toohello 지침을 참조할 수 있습니다 [관리 패킷 캡처 네트워크 감시자를](network-watcher-packet-capture-manage-portal.md) toostart 패킷 캡처 세션입니다. 이 패킷 캡처 CapAnalysis에서 액세스 하는 저장소 blob toobe에 저장할 수 있습니다.

### <a name="upload-a-packet-capture-toocapanalysis"></a>패킷 캡처 tooCapAnalysis 업로드
Hello 패킷 캡처를 저장 되어 있는 네트워크 감시자 hello "가져오기에서 URL" 탭을 사용 하 고 링크 toohello 저장소 blob를 제공 하 여 수행 되는 패킷 캡처를 직접 업로드할 수 있습니다.

링크 tooCapAnalysis를 제공 하는 SAS 토큰 toohello 저장소 blob URL tooappend 있는지 확인 합니다.  toodo hello 저장소 계정에서 액세스 서명 tooShared 탐색이, 사용 권한을 허용 하는 hello를 지정 하 고 hello SAS 생성 단추 toocreate 토큰 키를 누릅니다. 그런 다음이 SAS 토큰 toohello 패킷 캡처 저장소 blob URL을 추가할 수 있습니다.

hello 결과 URL은 다음과 같은: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>패킷 캡처 분석

CapAnalysis 다양 한 옵션 toovisualize 패킷 캡처를 다른 관점에서 각 제공 분석을 제공합니다. 이러한 시각적 요약 정보를 통해 네트워크 트래픽 추세를 이해하고 신속하게 비정상적인 활동을 발견할 수 있습니다. 이러한 기능 중 몇 가지 hello 목록 다음에 나와 있습니다.

1. 흐름 테이블

    이 테이블을 제공 hello 패킷 데이터의 흐름 목록이 hello, hello 흐름와 연결 된 타임 스탬프 hello hello hello 흐름 뿐만 아니라 원본 및 대상 IP와 관련 된 다양 한 프로토콜.

    ![capanalysis 흐름 페이지][5]

1. 프로토콜 개요

    이 창을 사용 하면 다양 한 프로토콜 및 지리적 tooquickly hello를 통해 네트워크 트래픽 분산 hello를 참조 합니다.

    ![capanalysis 프로토콜 개요][6]

1. 통계

    이 창에는 경우 tooview 네트워크 트래픽 통계 바이트를 소스 및 대상 Ip, hello 소스 및 대상 Ip, 각각에 대해 흐름에서 받은 프로토콜에 사용 되는 다양 한 흐름의 흐름 hello 기간 수 있습니다.

    ![capanalysis 통계][7]

1. 지역 지도

    이 창을 사용 하면 네트워크 트래픽의 지도 보기 각 국가의 트래픽의 toohello 볼륨 크기 조정 하는 색으로 있습니다. 해당 국가에서 Ip에서 보내고 받는 데이터의 hello 비율 등의 강조 표시 된 국가 tooview 추가 흐름 통계를 선택할 수 있습니다.

    ![지역 지도][8]

1. 필터

    CapAnalysis는 특정 패킷을 신속하게 분석할 수 있는 필터 집합을 제공합니다. 예를 들어 프로토콜 toogain 특정 insights 트래픽의 해당 하위 집합에 의해 toofilter hello 데이터를 선택할 수 있습니다.

    ![filters][11]

    방문 [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn 모든 CapAnalysis 기능에 대 한 자세한 합니다.

## <a name="conclusion"></a>결론

네트워크 감시자 패킷 캡처 기능에는 네트워크 트래픽을 더 잘 이해 및 toocapture hello 필요한 tooperform 네트워크 법정 있습니다. 이 시나리오에서는 Network Watcher의 패킷 캡처를 오픈 소스 시각화 도구와 간단하게 통합하는 방법을 살펴보았습니다. CapAnalysis toovisualize 패킷 캡처와 같은 오픈 소스 도구 사용 하면 심층 패킷 검사를 수행할 수 있으며 네트워크 트래픽을 내에서 추세를 빠르게 식별할 수 있습니다.

## <a name="next-steps"></a>다음 단계

NSG 흐름 로그에 대해 자세히 toolearn 방문 [NSG 흐름 기록](network-watcher-nsg-flow-logging-overview.md)

Toovisualize NSG 흐름 기록 하는 방법을 Power BI를 방문 하 여 자세한 [NSG 시각화할 Power BI를 사용 하 여 로그 전달](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
