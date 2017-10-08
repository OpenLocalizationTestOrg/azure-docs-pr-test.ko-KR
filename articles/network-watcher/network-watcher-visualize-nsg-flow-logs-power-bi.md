---
title: "Power BI를 사용 하 여 Azure 네트워크 보안 그룹 흐름 aaaVisualizing 기록 | Microsoft Docs"
description: "이 페이지는 Power BI를 사용 하 여 toovisualize NSG 흐름을 기록 하는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Power BI를 사용하여 네트워크 보안 그룹 흐름 로그 시각화

네트워크 보안 그룹 흐름 로그 IP 트래픽이 ingress 및 egress에 대 한 네트워크 보안 그룹에 tooview 정보를 사용 합니다. 이러한 흐름 로그 아웃 바운드 나타나며 당 규칙 별로 인바운드 흐름 hello NIC hello 흐름 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜) 및 hello 트래픽을 허용 또는 거부 된 경우에 대 한 5-튜플 정보에 적용 됩니다.

수동으로 hello 로그 파일을 검색 하 여 로깅 데이터 흐름에 대 한 어려운 toogain 정보 수 있습니다. 이 문서에서는 가장 최근의 흐름 로그 및 네트워크의 트래픽에 대 한 자세한 내용은 솔루션 toovisualize를 제공 합니다.

## <a name="scenario"></a>시나리오

시나리오를 따르는 hello에서 NSG 흐름 로깅 데이터에 대 한 hello 싱크로 구성 했습니다 Power BI 데스크톱 toohello 저장소 계정을 연결 했습니다. Tooour 저장소 계정, 연결 후 Power BI는 다운로드 하 고 hello 로그 tooprovide을 시각적으로 네트워크 보안 그룹에 의해 기록 된 hello 트래픽 구문 분석 합니다.

Hello 서식 파일을 검사할 수 있습니다에 제공 된 hello 시각적 개체를 사용 하 여:

* 상위 토커
* 방향 및 규칙 결정에 따른 시계열 흐름 데이터
* 네트워크 인터페이스 MAC 주소에 따른 흐름
* NSG 및 규칙에 따른 흐름
* 대상 포트에 따른 흐름

제공 된 hello 템플릿을 편집할 수 있으므로 tooadd 새 데이터를 시각적 개체를 수정 하거나 쿼리 toosuit 요구에 맞게 편집할 수 있습니다.

## <a name="setup"></a>설정

시작하기 전에 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다. 네트워크 보안을 사용 하도록 설정에 대 한 지침은 로그 흐름 toohello 다음 문서를 참조 하십시오: [네트워크 보안 그룹에 대 한 소개 tooflow 로깅을](network-watcher-nsg-flow-logging-overview.md)합니다.

또한 hello Power BI Desktop 클라이언트와 충분 한 컴퓨터에 설치 되어 컴퓨터 toodownload 및 부하 hello 로그 데이터의 저장소 계정에서 사용 가능한 공간 있어야 합니다.

![Visio 다이어그램][1]

### <a name="steps"></a>단계

1. 다운로드 및 hello Power BI Desktop 응용 프로그램에서에서 Power BI 템플릿을 다음 열기 hello [네트워크 감시자 PowerBI 흐름 기록 서식 파일](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Hello 필요한 쿼리 매개 변수를 입력 합니다.
    1. **StorageAccountName** – toohello 이름을 포함 하는 hello NSG 흐름 로그 hello 저장소 계정의 지정 tooload 선택한 시각화 합니다.
    1. **NumberOfLogFiles** – hello toodownload 같은 및 Power BI의 시각화는 로그 파일 수를 지정 합니다. 예를 들어 50을 지정 하는 경우 hello 50 최신 로그 파일입니다. 설정 하 고 toosend NSG 흐름 로그 toothis 계정을 구성 하는 ff 2 Nsg는 다음 hello 25 지난 시간의 로그를 볼 수 있습니다.

    ![power BI 메인][2]

1. Hello 저장소 계정에 대 한 액세스 키를 입력 합니다. Hello Azure 선택 하 고 포털에서 저장소 계정을 tooyour를 탐색 하 여 유효한 액세스 키를 찾을 수 **선택 키** hello 설정 메뉴에서 합니다. 그런 다음 **연결**을 클릭하여 변경 내용을 적용합니다.

    ![액세스 키][3]

    ![액세스 키 2][4]

4.  로그를 다운로드 되 고 구문 분석 하 고 이제 hello 미리 작성된 된 시각적 개체를 사용할 수 있습니다.

## <a name="understanding-hello-visuals"></a>Hello 시각적 표시 이해

Hello 서식 파일은 제공 된 데 도움이 되는 시각적 개체 집합이 hello NSG 흐름 로그 데이터의 의미를 확인 합니다. hello 다음 이미지가 표시 hello 대시보드 데이터로 채울 때 처럼 보이는의 샘플입니다. 아래에서는 각 시각 효과를 좀 더 자세히 살펴보겠습니다. 

![powerbi][5]
 
hello Top 송신기 시각적 표시 hello Ip를 시작 했습니다. 지정 된 기간 hello를 통해 대부분의 연결을 hello 합니다. hello 상자 hello 크기 toohello 상대 연결 수가 해당합니다. 

![toptalkers][6]

hello 다음 시간 시계열 그래프 표시 hello 기간 동안 흐름 hello 수 있습니다. hello 위쪽 그래프 hello 흐름 방향으로 분리 된 및 hello 결정 (허용 또는 거부) 하 여 hello 낮은 조각화 됩니다. 이 시각 효과를 사용하면 시간에 따른 트래픽 추세를 검사하고, 트래픽 또는 트래픽 세그먼트의 비정상적인 급증 현상 또는 급감 현상을 찾아낼 수 있습니다.

![flowsoverperiod][7]

hello 다음 그래프에 표시 hello 흐름 hello 위쪽 방향으로 분리 및 hello 낮은 내린 결정 기호로 분리 된 네트워크 인터페이스당. 이 정보를 전달 하 여 Vm 중 어떤 hello 대부분 상대 tooothers 및 트래픽 tooa 특정 VM 되는 경우에 대 한 정보를 얻을 수 있습니다 허용 또는 거부 합니다.

![flowspernic][8]

hello 도넛 휠 차트 다음 분석 대상 포트 여 흐름을 보여 줍니다. 이 정보를 지정 하는 hello 내에서 사용 되는 가장 일반적으로 사용 하는 hello 대상 포트를 볼 수 있습니다 기간입니다.

![donut][9]

hello 다음 가로 막대형 차트에서는 hello NSG 및 규칙 흐름 이 정보를 볼 수 있습니다 hello Nsg hello에 대 한 책임 대부분 트래픽과 트래픽의 hello 분석 NSG에서 규칙에 의해.

![barchart][10]
 
hello hello Nsg에 대 한 정보 제공 용 이므로 차트 표시 정보를 다음 hello 로그에 있는, hello 흐름 hello 기간 및 hello 날짜 캡처된 hello 가장 빠른 로그를 캡처할 수 있습니다. 이 정보를 사용 하면 어떤 Nsg는 기록 되 고 및 흐름의 날짜 범위를 hello 수 있습니다.

![infochart1][11]

![infochart2][12]

이 템플릿에 안녕하세요 슬라이서 tooallow 다음 tooview 유일한 hello 데이터에 가장 관심이 있습니다. 사용자는 리소스 그룹, NSG 및 규칙을 필터링할 수 있습니다. 5 튜플 정보, 의사 결정, 및 hello 로그 기록 된 hello 시간에 필터링 할 수 있습니다.

![slicers][13]

## <a name="conclusion"></a>결론

했죠이 시나리오에서는 네트워크 감시자 및 Power BI에서 제공 하는 네트워크 보안 그룹 흐름 로그를 사용 하 여 우리 수 toovisualize를 hello 트래픽을 이해 합니다. 제공 된 hello 템플릿을 사용 하 여, Power BI hello 로그 저장소에서 직접 다운로드 합니다. 하 고 로컬로 처리 합니다. 다운로드 한 파일의 전체 크기 및 타임 라인 tooload hello 템플릿을 hello 요청한 파일 수에 따라 달라 집니다.

무료 toocustomize 요구에 따라이 서식 파일을 느낍니다. Power BI를 네트워크 보안 그룹 흐름 로그와 함께 사용할 수 있는 매우 다양한 방법이 있습니다. 

## <a name="notes"></a>참고 사항

* 로그는 기본적으로 `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`에 저장됩니다.

    * 다른 디렉터리에 다른 데이터가 있는 경우 쿼리 toopull를 hello 및 프로세스 hello 데이터를 수정 해야 합니다.

* 1GB 이상의 로그와 함께 사용할 hello 제공 템플릿의 권장 되지 않습니다.

* 로그 용량이 큰 경우 Data Lake 또는 SQL Server 같은 다른 데이터 저장소를 사용하는 솔루션을 알아보는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

Toovisualize NSG 흐름 기록 하는 방법을 Elastick 스택 hello로 방문 하 여 자세한 [오픈 소스 도구를 사용 하 여 Vm에서 네트워크 트래픽 패턴 tooand 시각화](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
