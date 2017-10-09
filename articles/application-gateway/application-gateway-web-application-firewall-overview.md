---
title: "Azure 응용 프로그램 게이트웨이 aaaIntroduction tooweb 응용 프로그램 방화벽 (WAF) | Microsoft Docs"
description: "이 페이지에서는 Application Gateway용 WAF(웹 응용 프로그램 방화벽)의 개요를 제공합니다."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>WAF(웹 응용 프로그램 방화벽)

WAF(웹 응용 프로그램 방화벽)는 일반적인 악용 및 취약점으로부터 웹 응용 프로그램에 대해 중앙 집중화된 보호를 제공하는 Application Gateway의 기능입니다. 

웹 응용 프로그램 방화벽 hello에서 규칙을 기반 [OWASP 코어 규칙 집합](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 또는 2.2.9 퀵 합니다. 웹 응용 프로그램의 널리 알려진 취약점을 악용하는 악의적인 공격이 점점 많아지고 있습니다. 이러한 익스플로잇 간에 공통적으로 적용은 SQL 삽입 공격, tooname 몇 가지 공격 교차 사이트 스크립팅 합니다. 응용 프로그램 코드에서 이러한 공격 방지 하기가 어려울 수 있습니다 및 엄격한 유지 관리, 패치 및 hello 응용 프로그램 토폴로지의 여러 계층에서 모니터링 해야 할 수 있습니다. 중앙 집중식된 웹 응용 프로그램 방화벽은 보안 관리를 훨씬 더 간단 하 게 하면 하 고 더 나은 보증 위협 또는 침입 tooapplication 관리자를 제공 합니다. WAF 솔루션와 각각의 개별 웹 응용 프로그램 보안을 중앙 위치에서 알려진된 취약점의 패치를 적용 하 여 tooa 보안 위협이 더 빠르게 반응 수 있습니다. 기존 응용 프로그램 게이트웨이 변환 된 tooa 웹 응용 프로그램 방화벽을 사용 응용 프로그램 게이트웨이 쉽게 될 수 있습니다.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

응용 프로그램 게이트웨이 여러 웹 사이트 및 보안 향상 된 기능은 응용 프로그램 배달 컨트롤러 및 제안 SSL 종료, 쿠키 기반 세션 선호도, 라운드 로빈 부하 분산, 콘텐츠 기반 라우팅, 기능 toohost로 작동합니다. 응용 프로그램 게이트웨이에서 제공 하는 향상 된 보안 SSL 정책 관리, SSL 지원 끝 tooend 포함 됩니다. 응용 프로그램 보안은 이제 WAF (웹 응용 프로그램 방화벽) hello ADC 서비스에 직접 통합 하 여 강화 됩니다. 쉽게 tooconfigure 중앙 위치 toomanage를 제공할 수 있으며 일반적인 웹 취약점 으로부터 웹 응용 프로그램을 보호 합니다.

## <a name="benefits"></a>이점

hello 다음은 응용 프로그램 게이트웨이 및 웹 응용 프로그램 방화벽 제공 하는 hello 핵심적인 이점입니다.

### <a name="protection"></a>보호

* 웹 응용 프로그램 웹 취약점 및 toobackend 코드를 수정 하지 않고 공격 으로부터 보호 합니다.

* 보호 여러 웹 응용 프로그램 게이트웨이 뒤 시간이 hello에서 응용 프로그램입니다. 응용 프로그램 게이트웨이 호스팅 WAF와 웹 공격 으로부터 보호 되어야 수 있는 단일 게이트웨이 뒤 too20 웹 사이트를 지원 합니다.

### <a name="monitoring"></a>모니터링

* 실시간 WAF 로그를 사용하여 공격으로부터 웹 응용 프로그램을 모니터링합니다. 이 로그와 통합 되어 [Azure 모니터](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAF 경고 기록 및 쉽게 추세를 모니터링 합니다.

* WAF는 곧 Azure Security Center와 통합됩니다. Azure 보안 센터 모든 Azure 리소스의 hello 보안 상태를 전반적으로 살펴볼 수 있습니다.

### <a name="customization"></a>사용자 지정

* hello 기능 toocustomize WAF 규칙 및 규칙에는 응용 프로그램 요구 사항 toosuit를 그룹화 하 고 거짓 긍정 제거.

## <a name="features"></a>기능

웹 응용 프로그램 방화벽 기본적으로 미리 구성 된 CRS 3.0 제공 되는지, 아니면 toouse 2.2.9 퀵을 선택할 수 있습니다. CRS 3.0 제품은 2.2.9를 통해 거짓 긍정을 줄입니다. 기능을 너무 hello[규칙 toosuit 요구에 맞게 사용자 지정](application-gateway-customize-waf-rules-portal.md) 제공 됩니다. Hello 일반적인 웹 취약점 으로부터 보호 하는 웹 응용 프로그램 방화벽 중 일부에 다음이 포함 됩니다.

* SQL 삽입 공격 보호
* 교차 사이트 스크립팅 공격 보호
* 명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할, 원격 파일 포함 공격 등의 일반 웹 공격 보호
* HTTP 프로토콜 위반 보호
* 누락된 호스트 사용자-에이전트 및 수락 헤더 같은 HTTP 프로토콜 이상 보호
* 보트, 크롤러 및 스캐너 방지
* 일반적인 응용 프로그램 구성 오류(예: Apache, IIS 등) 검색

해당 보호 및 더 자세한 규칙 목록이 참조 hello 다음 [규칙 집합 핵심](#core-rule-sets)합니다.

### <a name="core-rule-sets"></a>핵심 규칙 집합

Application Gateway는 CRS 3.0 및 CRS 2.2.9라는 두 개의 규칙 집합을 지원합니다. 이러한 핵심 규칙 집합은 악의적인 활동으로부터 웹 응용 프로그램을 보호하는 규칙의 컬렉션입니다.

#### <a name="owasp30"></a>OWASP_3.0

다음 표에 hello와 같이 제공 된 hello 3.0 코어 규칙 집합에 13 규칙 그룹이 있습니다. 이러한 규칙 그룹은 각각 비활성화할 수 있는 여러 개의 규칙을 포함합니다.

|RuleGroup|설명|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|알려진된 스팸 또는 악의적인 활동에 대해 규칙 tooprotect 포함 되어 있습니다.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|포함 규칙 toolock 다운 메서드에서 (PUT, PATCH <..)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| 서비스 거부 (DoS) 공격에 대 한 규칙 tooprotect 포함 되어 있습니다.|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| 포트 및 환경 스캐너에 대 한 규칙 tooprotect 포함 되어 있습니다.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|프로토콜 및 인코딩 문제에 대 한 규칙 tooprotect 포함 되어 있습니다.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|헤더 주입, smuggling, 요청 및 응답 분할에 대 한 규칙 tooprotect 포함|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|파일 및 경로 공격에 대 한 규칙 tooprotect 포함 되어 있습니다.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|포함 규칙 tooprotect에 대해 포함 RFI (Remote File)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|포함 규칙 tooprotect 다시 한 원격 코드 실행 합니다.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|규칙 tooprotect PHP 삽입 공격을 포함합니다.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|사이트 간 스크립팅으로부터 보호하기 위한 규칙을 포함합니다.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|SQL 주입 공격으로부터 보호하기 위한 규칙을 포함합니다.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|세션 고정 공격에 대 한 규칙 tooprotect 포함 되어 있습니다.|

#### <a name="owasp229"></a>OWASP_2.2.9

제공 된 hello 2.2.9 퀵 코어 규칙 집합 hello 다음 표에서 같이 10 규칙 그룹에 있습니다. 이러한 규칙 그룹은 각각 비활성화할 수 있는 여러 개의 규칙을 포함합니다.

|RuleGroup|설명|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|프로토콜 위반 (잘못 된 문자를 요청 본문 등과 함께 GET.)에 대 한 규칙 tooprotect 포함|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|잘못 된 헤더 정보에 대 한 규칙 tooprotect 포함 되어 있습니다.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|형식 정의 나 한계를 초과 하는 파일에 대 한 규칙 tooprotect 포함 되어 있습니다.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|제한 된 메서드, 헤더 및 파일 형식에 대해 규칙 tooprotect 포함 되어 있습니다. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|웹 크롤러 및 스캐너에 대 한 규칙 tooprotect 포함 되어 있습니다.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|제네릭 공격 (고정 세션, 원격 파일 포함, PHP 주입 등)에 대 한 규칙 tooprotect 포함|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|SQL 삽입 공격 으로부터 규칙 tooprotect 포함|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|교차 사이트 스크립팅 으로부터 규칙 tooprotect 포함 되어 있습니다.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|경로 탐색 공격에 대 한 규칙 tooprotect 포함|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|백도어 트로이 목마에 대 한 규칙 tooprotect 포함 되어 있습니다.|

### <a name="waf-modes"></a>WAF 모드

응용 프로그램 게이트웨이 WAF hello 다음 두 가지 모드에서에서 구성 된 toorun 될 수 있습니다.

* **검색 모드** – 응용 프로그램 게이트웨이 WAF 검색 모드로 구성 된 toorun를 모니터링 하 고 모든 위협 경고 tooa 로그 파일에 기록 하는 경우. 응용 프로그램 게이트웨이에 대 한 진단 내용을 로깅하를 설정 해야 hello를 사용 하 여 **진단** 섹션. 또한 WAF hello tooensure 해야 로그를 선택 하 고 설정 합니다. 웹 응용 프로그램 방화벽을 감지 모드로 실행하면 들어오는 요청을 차단하지 않습니다.
* **방지 모드** – 응용 프로그램 게이트웨이 방지 모드로 구성 된 toorun 침입 및 해당 규칙에서 검색 하는 공격을 적극적으로 차단 하는 경우. hello 공격자가 403 무단된 액세스 예외가 받아 hello 연결이 종료 됩니다. 방지 모드 hello WAF 로그의 toolog 이러한 공격을 계속합니다.

### <a name="application-gateway-waf-reports"></a>WAF 모니터링

응용 프로그램 게이트웨이의 hello 상태를 모니터링 하는 것이 중요 합니다. 웹 응용 프로그램의 응용 프로그램 방화벽 및 hello를 보호 하는 hello 상태 모니터링 로깅 및 Azure 모니터, Azure 보안 센터 (출시 예정), 및 로그 분석 통합을 통해 제공 됩니다.

![진단](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure Monitor

각 Application Gateway 로그는 [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md)와 통합됩니다.  이렇게 하면 WAF 경고 및 로그를 포함 하 여 tootrack 진단 정보가 있습니다.  이 기능은 hello hello 포털 hello에서 응용 프로그램 게이트웨이 리소스 내 **진단** 탭 또는 hello Azure 모니터를 통해 직접를 서비스 합니다. 응용 프로그램 게이트웨이에 대 한 진단 로그를 사용 하도록 설정 하는 방법에 대 한 내용은 방문 toolearn [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Azure 보안 센터

[Azure 보안 센터](../security-center/security-center-intro.md) 사용 방지를 감지 하 고 및 toothreats 파악할을 사용 하 여 응답을 제어할 수 hello Azure 리소스의 보안 합니다. 이제 Application Gateway는 [Azure Security Center로 통합](application-gateway-integration-security-center.md)합니다. Azure 보안 센터 환경 toodetect 보호 되지 않은 상태로 웹 응용 프로그램을 검색합니다. 이제 응용 프로그램 게이트웨이 WAF tooprotect 취약 한 리소스인 권장할 수 있습니다 것입니다. Hello Azure 보안 센터에서에서 응용 프로그램 게이트웨이 WAF를 직접 만들 수 있습니다.  이러한 WAF 인스턴스 Azure 보안 센터와 통합 되어 있으며 경고 및 상태 정보 보고에 대 한 보안 센터 tooAzure 다시 보내집니다.

![그림 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>로깅

Application Gateway WAF는 감지된 각 위협에 대한 상세 보고를 제공합니다. 로깅은 Azure 진단 로그에 통합되고 경고는 json 형식으로 기록됩니다. 이러한 로그는 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)와 통합될 수 있습니다.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Application Gateway WAF SKU 가격 책정

새 WAF SKU 아래에서 웹 응용 프로그램 방화벽을 사용할 수 있습니다. 이 SKU가 hello 클래식 배포 모델에 포함 되지 않은 Azure 리소스 관리자 프로 비전 모델에만 사용할 수 있습니다. 또한 WAF SKU는 중간 규모 및 대규모 Application Gateway 인스턴스 크기로만 제공됩니다. 응용 프로그램 게이트웨이에 대 한 모든 hello 제한도 toohello WAF SKU를 적용 합니다. 가격 책정은 시간 당 게이트웨이 인스턴스 요금 및 데이터 처리 충전을 기반으로 합니다. WAF SKU 시간 당 게이트웨이 가격 책정은 표준 SKU 요금과 다르며 [Application Gateway 가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/application-gateway/)에서 찾을 수 있습니다. 데이터 처리 요금이 계속 hello 동일 합니다. 규칙 또는 규칙 그룹 당 요금은 없습니다. 여러 웹 응용 프로그램을 보호할 수 있는 여러 응용 프로그램을 지원 하기 위한 추가 요금이 청구 되지 및 동일한 웹 응용 프로그램 방화벽 뒤에 hello 합니다. 

결제 WAF에 대 한 시작 후 hello WAF SKU 게이트웨이 계속 toobe 표준 요율로 요금이 부과 될 때까지 효과적으로 5/5/2017 년 1.

## <a name="next-steps"></a>다음 단계

WAF의 hello 기능에 대해 학습 한 후 방문 [어떻게 tooconfigure 웹 응용 프로그램 방화벽에서 응용 프로그램 게이트웨이](application-gateway-web-application-firewall-portal.md)합니다.

