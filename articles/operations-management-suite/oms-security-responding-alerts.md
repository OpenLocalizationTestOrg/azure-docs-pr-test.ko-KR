---
title: "aaaMonitoring 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고 | Microsoft Docs"
description: "이 문서 있습니다 toouse hello 위협 인텔리전스 옵션을 사용할 수 OMS 보안 및 감사 toomonitor 주며 toosecurity 경고에 응답 합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>모니터링 및 Operations Management Suite 보안 및 감사 솔루션에서 경고를 toosecurity 응답
이 문서를 사용 하 여 OMS 보안 및 감사 toomonitor에서 사용할 수 있는 hello 위협 인텔리전스 옵션을 사용 하 고 toosecurity 경고 응답할 수 있습니다.

## <a name="what-is-oms"></a>OMS란?
Microsoft Operations Management Suite(OMS)란 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. OMS에 대 한 자세한 내용은 hello 문서를 읽어 보세요. [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)합니다.

## <a name="threat-intelligence"></a>위협 인텔리전스
사용자가 광범위 한 액세스를 toohello 네트워크 하 고 다양 한 장치 tooconnect toocorporate 데이터를 사용 하 여 엔터프라이즈 환경에는 리소스를 적극적으로 모니터링 하 고 toosecurity 인시던트를 신속 하 게 응답할 수 있는 합니다. 특정 경고 위협 발생 시 키 지 않을 수 있습니다 일부 사이버 안보 때문에 hello 보안 수명 주기 측면에서 중요 한 또는 기존 보안 기술적 컨트롤으로 식별할 수 있는 의심 스러운 활동입니다. 

Hello를 사용 하 여 **위협 인텔리전스** 옵션 OMS 보안 및 감사에서 사용할 수 있는, IT 관리자 수 식별 hello 환경에 대 한 보안 위협 예를 들어, 특정 컴퓨터의 일부인 경우 식별 된 [ 봇 네트](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection)합니다. 공격자가 불법 비밀리이 컴퓨터 toohello 명령 및 제어를 연결 하는 맬웨어를 설치할 때 컴퓨터에서 봇 네트에서 노드를 될 수 있습니다. 또한 [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents)과 같은 지하 통신 채널에서 오는 잠재적 위협도 식별할 수 있습니다. 

순서 toobuild OMS 보안 및 감사가 위협 인텔리전스는 Microsoft에서 여러 원본에서 가져온 데이터를 사용 합니다. OMS 보안 및 감사 사용자 환경에 대 한이 데이터 tooidentify 잠재적인 위협 활용 됩니다.

hello 위협 인텔리전스 창의 세 가지 주요 옵션으로 구성 됩니다.

* 아웃바운드 악성 트래픽이 있는 서버
* 검색된 위협 유형
* 위협 인텔리전스 맵

> [!NOTE]
> 모든 옵션에 대한 개요는 [Operations Management Suite 보안 및 감사 솔루션 시작](oms-security-getting-started.md)을 참조하세요.
> 
> 

### <a name="responding-toosecurity-alerts"></a>Toosecurity 경고 응답
hello 단계 중 하나는 [보안 사고 대응](https://technet.microsoft.com/library/cc512623.aspx) 프로세스는 hello 손상 시스템 tooidentify hello 심각도입니다. 이 단계에서는 작업을 수행 하는 hello를 수행 해야 합니다.

* Hello 공격의 hello 특성을 확인
* Hello 공격의 시작 위치를 결정 합니다.
* Hello 공격 hello 의도 확인 합니다. Hello 공격이에서 하기 조직 tooacquire 구체적인 정보 않거나 임의 않아서?
* Hello 시스템을 노출 되었습니다. 식별
* 액세스 한 되며 해당 파일의 hello 중요도 확인 하는 hello 파일 식별

활용할 수 있는 **위협 인텔리전스** OMS 보안 및 감사 솔루션 toohelp 이러한 작업에 대 한 정보입니다. 이 tooaccess 아래 hello 단계에 따라 **위협 인텔리전스** 옵션:

1. Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **보안 및 감사** 바둑판식으로 배열입니다.
   
    ![보안 및 감사](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Hello에 **보안 및 감사** 대시보드를 hello 나타납니다 **위협 인텔리전스** 아래와 같이 hello 오른쪽에 옵션:
   
    ![위협 인텔리전스](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

이러한 세 가지 타일 hello 현재 위협에 대 한 개요를 제공 합니다. Hello에 **아웃 바운드 악성 트래픽이 있는 서버** (내부 또는 외부 네트워크에서)를 모니터링 하는 모든 컴퓨터에 없는 경우 수 tooidentify 됩니다 즉 보내는 악의적인 트래픽 toohello 인터넷 합니다. 

hello **위협 유형을 검색** 타일 hello 와일드 카드"에서" 최신인 hello 위협 요약 정보를 표시,이 타일을 클릭 하면이 대 한 자세한 내용은 아래 표시 된 대로 나타납니다.

![검색된 위협 유형](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

각 위협을 클릭하여 자세한 내용을 확인할 수 있습니다. hello 감시할 봇 네트 대 한 자세한 정보를 보여 줍니다.

![위협에 대한 자세한 내용](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

이 섹션의 hello 시작 부분에서 설명한 대로이 정보가 매우 유용할 수 있습니다 사고 대응 사례 중입니다. 것도 중요할 수 있습니다 법정 조사 하는 동안 시스템 보안이 손상 되 고 타임 라인 hello hello 공격의 toofind hello 소스 해야 합니다. 이 보고서에 쉽게 식별할 수 hello 공격에 대 한 몇 가지 핵심 세부 정보 등의: hello 공격의 소스 hello, 보안이 손상 된 로컬 IP hello 및 hello hello 연결의 현재 세션 상태입니다. 

hello **위협 인텔리전스 맵** tooidentify hello 현재 위치 hello 전 세계에 악의적인 트래픽을 도움이 됩니다. 주황색 (보내는) 있으며 빨간색 (보내는) 화살표가 맵에서 이러한 화살표 중 하나를 클릭 하는 경우 hello 트래픽 방향과 식별 하는 hello 유형의 위협 요소 및 hello 트래픽 방향과 아래와 같이 표시 됩니다.

![위협 인텔리전스 맵](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> 에 toouse 사고 대응 하는 동안이 기능은 처리 하는 방법을 hello 프레젠테이션을 시청 하 여 데모를 보려면 수 [여 안내 조사 Operations Management Suite를 사용 하 여 데이터 센터 보안 위협을 줄이는](https://myignite.microsoft.com/videos/5000) Microsoft Ignite에 배달 합니다.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>응답 toodistinct 악성 IP 액세스
일부 시나리오에서는 모니터링되는 한 컴퓨터에서 잠재적인 악성 IP에 액세스한 것을 확인할 수 있습니다.

![위협 인텔리전스 맵](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

이 경고 및 기타 내 동일한 범주 hello, 활용 하 여 OMS 보안을 통해 생성 된 [Microsoft 위협 인텔리전스](https://youtu.be/O4WtxgUrDc8)합니다. hello 위협 인텔리전스 데이터는 Microsoft에서 수집한으로 업계 선두 위협 인텔리전스 공급 업체에서 구입 합니다. 이 데이터 자주 업데이트 되 고 위협 toofast 이동를 채택 합니다. Tooits 특성 인해 것 ठ ा 하는 동안 보안 정보의 다른 소스와 [조사](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) 보안 경고가 있습니다. 

## <a name="customize-alerts-received-via-e-mail"></a>전자 메일을 통해 수신한 경고를 사용자 지정

OMS 보안을 통해 보안 경고가 트리거되면 조직의 어떤 사용자에게 통보할지 사용자 지정할 수 있습니다. 이 옵션은 개요에서 사용할 수 있는 설정에는 OMS 대시보드가 hello /:

![Email](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 toouse hello **위협 인텔리전스** OMS 보안 및 감사 솔루션 toorespond toosecurity 경고에 대 한 옵션입니다. OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:

* [OMS(Operations Management Suite) 개요](operations-management-suite-overview.md)
* [Operations Management Suite 보안 및 감사 솔루션 시작](oms-security-getting-started.md)
* [Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링](oms-security-monitoring-resources.md)

