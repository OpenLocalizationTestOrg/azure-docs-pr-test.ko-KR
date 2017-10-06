---
title: "Azure 보안 센터를 사용 하는 aaaRespond toosecurity 인시던트 | Microsoft Docs"
description: "이 문서는 어떻게 toouse Azure 보안 센터가 사고 대응 시나리오를 설명 합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>사고 대응에 Azure Security Center 사용
대부분의 조직에 알아봅니다 방법만 공격을 받은 후 toorespond toosecurity 사고 합니다. tooreduce 비용 및 손상 사고 대응 계획이 공격이 발생 하기 전에 중요 한 toohave 됩니다. Azure Security Center는 사고에 대응하는 여러 단계에서 사용할 수 있습니다.

## <a name="incident-response-planning"></a>사고 대응 계획 수립
세 가지 핵심 기능에 따라 달라 집니다 하는 효과적인 계획: 수 tooprotect 되 고을 감지 하 고 toothreats 응답 합니다. 문제를 방지에 대 한 보호는, 및 위협을 조기에 확인 하는 방법에 대 한 검색은 hello 공격자를 제거 하는 방식 및 위반의 시스템 toomitigate hello 영향을 복원 하는 방법에 대 한 응답은 합니다.

이 문서는 hello에서 hello 보안 사고 대응 단계를 사용 하 여 [hello 클라우드에서에서 Microsoft Azure 보안 응답](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) hello 다음 다이어그램에에서 나와 있는 것 처럼 문서:

![사고 대응 수명 주기](./media/security-center-incident-response/security-center-incident-response-fig1.png)

보안 센터 hello 검색, 평가, 및 진단 단계 동안 사용할 수 있습니다. 보안 센터 수 있는 방법을 유용 hello 세 초기 사고 대응 단계 중의 예는 다음과 같습니다.

* **검색**: hello 이벤트 확인의 첫 번째 표시를 검토 합니다.
  * 예: 검토 hello 초기 확인 하면 우선 순위가 높은 보안 경고가 hello 보안 센터 대시보드에서 발생 했습니다.
* **평가**: hello 초기 평가 tooobtain hello 의심 스러운 활동에 대 한 자세한 정보를 수행 합니다.
  * 예: hello 보안 경고에 대 한 자세한 정보를 가져옵니다.
* **진단**: 기술 조사를 수행하고 포함, 완화 및 해결 방법 전략을 식별합니다.
  * 예: 해당 특정 보안 경고의 보안 센터에서 설명 하는 hello 수정 단계를 수행 합니다.

뒤에 오는 hello 시나리오 중 tooleverage 보안 센터 보안 문제의 검색, 평가, 및 진단/응답 단계 hello 하는 방법을 보여 줍니다. Security Center에서 [보안 사고](security-center-incident.md)는 리소스에 대해 [킬 체인(kill chain)](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) 패턴과 일치하는 모든 경고의 집계입니다. Hello에 인시던트 표시 [보안 경고](security-center-managing-and-responding-alerts.md) 타일 및 블레이드입니다. 인시던트에서 각 항목에 대 한 자세한 내용은 tooobtain 있습니다 수 있도록 하는 hello 목록이 관련된 경고를 보여 줍니다. 보안 센터는 또한 독립 실행형 아래로 의심 스러운 활동을 사용 하는 tootrack 또한 수 있는 보안 알림을 제공 합니다.

## <a name="scenario"></a>시나리오
최근에 Contoso 일부 업무의 작업 가상 컴퓨터 기반 및 SQL 데이터베이스를 포함 하 여 자신의 온-프레미스 리소스 tooAzure 중 일부를 마이그레이션. 현재 Contoso의 CSIRT(주요 컴퓨터 보안 사고 대응 팀)에는 현재의 사고 대응 도구와 통합되지 않는 보안 인텔리전스로 인해 보안 문제를 조사하는 데 문제가 있습니다. 이 제대로 통합 되지이 않으므로 hello 평가 및 진단 단계 중은 물론 hello 검색 단계 (너무 많은 가양성) 하는 동안 문제를 소개합니다. 이들은 했는데 tooopt이 마이그레이션의 일부로 보안 센터 toohelp에 대 한 이러한 문제를 해결 합니다.

등록 된 후이 마이그레이션을 완료 하는 첫 번째 단계를 hello 리소스를 모두 한 모든 보안 센터에서 hello 보안 권장 사항 해결 합니다. Contoso CSIRT는 컴퓨터 보안 문제를 처리 하기 위한 hello 중점이 됩니다. hello 팀의 보안 문제 해결에 대 한 책임이 있는 사용자 그룹으로 구성 됩니다. hello 팀 멤버는 처리 되지 않는 응답의 어떤 영역 남아 있는 의무 tooensure를 정의 명확 하 게 했습니다.

이 시나리오의 hello 용도로 여기 toofocus hello 다음 Contoso CSIRT의 일부인 가상 사용자의 역할 모두 hello에:

![사고 대응 수명 주기](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Judy는 보안 운영 업무를 담당하고 있습니다. 그녀의 책임은 다음과 같습니다.

* 모니터링 및 hello 클록 주위 toosecurity 위협 응답 합니다.
* Toohello 클라우드 작업 소유자 또는 필요에 따라 보안 분석가 에스컬레이션 합니다.

Sam은 보안 분석가이며 다음과 같은 업무를 담당합니다.

* 공격 조사
* 경고 수정
* 작업 소유자 toodetermine 작업 및 완화를 적용 합니다.

볼 수 있듯이 Judy 및 Sam 서로 다른 책임 있고 tooshare 보안 센터 정보 함께 작동 해야 합니다.

## <a name="recommended-solution"></a>권장된 솔루션
서로 다른 역할에 한 Judy 및 Sam 있습니다 사용할 예정 tooobtain 관련 정보 보안 센터의 다른 영역 일상적인 작업에 대 한입니다. Judy는 매일 모니터링 작업의 일부로 **보안 경고**를 사용합니다.

![보안 경고](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Judy는 hello 검색 및 평가 단계 중 보안 경고를 사용 합니다. Judy hello 초기 평가 완료 한 후 추가 확인이 필요한 경우 hello 문제 tooSam 제기 될 수 있습니다 그녀 합니다. 이 시점에서 Sam hello 제공한 정보는 보안 센터에서 경우에 따라 다른 데이터 원본과 함께에서 toomove toohello 진단 단계를 사용 합니다.

## <a name="how-tooimplement-this-solution"></a>어떻게 tooimplement이이 솔루션
toosee hello 검색 및 평가 단계에서 Judy의 단계를 수행 알아보고 다음 Sam의 용도 확인 하겠습니다 방법 사고 대응 시나리오에서 Azure 보안 센터를 사용 하는 toodiagnose hello 문제입니다.

### <a name="detect-and-assess-incident-response-stages"></a>감지 및 평가 사고 대응 단계
Judy는 toohello Azure 포털 로그인 하 고 hello 보안 센터 콘솔에서 작동 합니다. 그녀의 일별 활동 모니터링의 일환으로, 다음 단계를 수행 하 여 경고 hello 우선 순위가 높은 보안 검토 그녀 시작:

1. Hello 클릭 **보안 경고** 타일 및 액세스 hello **보안 경고** 블레이드입니다.
    ![보안 경고 블레이드](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > 이 시나리오의 hello 목적으로 Judy hello 앞 그림에에서 표시 되 고 tooperform hello 악의적인 SQL 활동 경고에 대 한 평가입니다.
   >
   >
2. Hello 클릭 **악의적인 SQL 활동** hello에 대 한 공격 hello 리소스를 검토 하 고 경고 **악의적인 SQL 활동** 블레이드: ![인시던트 정보](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    이 블레이드에 Judy 메모할 수 공격 hello 자원에 대 한 방법을 발견 된 경우 및이 공격에 여러 번 발생 합니다.
3. Hello 클릭 **리소스 공격** tooobtain이이 공격에 대 한 자세한 정보.

Hello 설명을 읽은 후에 거짓 긍정 및이 case tooSam를 제기 해야 그녀 Judy 따라가도록 유도 됩니다.

### <a name="diagnose-incident-response-stage"></a>진단 사고 대응 단계
Sam은 Judy에서 hello 대/소문자를 수신 하 고 보안 센터 제안 hello 수정 단계를 검토를 시작 합니다.

![사고 대응 수명 주기](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>추가 리소스
hello 사고 대응 팀도 활용할 수 hello [보안 센터 Power BI](security-center-powerbi.md) 기능 toosee 여러 종류의 보고서입니다. 이러한 보고서 추가 조사 toovisualize 하는 동안 사용자를 도울 수, 분석 및 권장 사항 및 보안 경고를 필터링 합니다. 회사의 보안 정보 및 이벤트 (SIEM) 관리 솔루션을 사용 하 여 hello 조사 프로세스 중에 대 한 수도 [보안 센터 솔루션과 통합](security-center-integrating-alerts-with-log-integration.md)합니다. Hello를 사용 하 여 Azure 감사 로그 및 가상 컴퓨터 (VM) 보안 이벤트 통합할 수도 [Azure 로그 통합 도구](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/)합니다. tooinvestigate 공격, 보안 센터를 제공 하는 hello 정보와 함께에서이 정보를 사용할 수 있습니다.

## <a name="conclusion"></a>결론
매우 중요 한 tooyour 조직 이며 긍정적인 영향을 미치는 문제를 처리 하는 방법을 인시던트가 발생 하기 전에 팀을 구성 합니다. Hello 적절 한 도구 toomonitor 리소스가 하지 않은 경우이 팀 tootake 정확한 단계 tooremediate 보안 문제가 발생 하는 데 도움이 됩니다. 보안 센터 [검색 기능이](security-center-detection-capabilities.md) IT tooquickly 응답 toosecurity 사고를 지원 하 고 보안 문제를 해결할 수 있습니다.
