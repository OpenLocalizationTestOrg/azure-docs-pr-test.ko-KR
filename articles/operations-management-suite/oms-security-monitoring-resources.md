---
title: "Operations Management Suite 보안 및 감사 솔루션의 리소스 aaaMonitoring | Microsoft Docs"
description: "이 문서 toouse OMS 보안 및 감사 기능 toomonitor를 사용 하면 리소스 및 보안 문제를 식별 합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링
이 문서를 사용 하 여 OMS 보안 및 감사 기능 toomonitor 리소스를 사용 하 고 보안 문제를 식별할 수 있습니다.

## <a name="what-is-oms"></a>OMS란?
Microsoft Operations Management Suite(OMS)란 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다. OMS에 대 한 자세한 내용은 hello 문서를 읽어 보세요. [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)합니다.

## <a name="monitoring-resources"></a>리소스 모니터링
때마다 가능 tooprevent 보안 사고 hello 첫 번째 위치에서 발생에서 해야 합니다. 그러나 것이 불가능 한 tooprevent 모두 보안 사고 합니다. 보안 문제가 발생할 경우 tooensure 미치는 영향을 최소화 해야 합니다.  사용 되는 toominimize 일 수 있는 세 가지 중요 한 권장 사항 숫자 hello 및 보안 사고의 영향 hello:

* 사용자 환경의 취약성을 정기적으로 평가합니다.
* 모든 컴퓨터 시스템 및 설치 된 최신 패치 hello 모든 네트워크 장치 tooensure 정기적으로 확인 합니다.
* 운영 시스템 이벤트 로그, 응용 프로그램별 로그, 침입 검색 시스템 로그를 포함한 모든 로그와 로깅 메커니즘을 정기적으로 검사합니다.

보안 문제의 hello 영향을 최소화 하는 데 사용할 수 있는 모든 리소스를 모니터링 하는 IT tooactively OMS 보안 및 감사 솔루션 수 있습니다. OMS 보안 및 감사에는 리소스 모니터링에 사용할 수 있는 보안 도메인이 있습니다. hello 보안 도메인 빠르게 액세스할 tooa 옵션, 보안 모니터링 hello에 대 한 다음 도메인 자세히 설명 합니다.

* 맬웨어 평가
* 업데이트 평가
* ID 및 액세스

> [!NOTE]
> 모든 옵션에 대한 개요는 [Operations Management Suite 보안 및 감사 솔루션 시작](oms-security-getting-started.md)을 참조하세요.
> 
> 

### <a name="monitoring-system-protection"></a>시스템 보호 모니터링
철저 한 방어 방법은, 모든 계층의 보호는 hello에 대 한 중요 한 자산의 전반적인 보안 상태입니다. 사용 하는 컴퓨터 위협 및 보호가 부족 한 컴퓨터에에서 표시 됩니다 hello 맬웨어 평가 타일 보안 도메인에서 검색 했습니다. 맬웨어 평가 hello에서 hello 정보를 통해 필요로 하는 계획 tooapply 보호 toohello 서버를 식별할 수 있습니다. 아래 단계를이 옵션에 따라 hello tooaccess:

1. Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **보안 및 감사** 바둑판식으로 배열입니다.
   
    ![보안 및 감사](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Hello에 **보안 및 감사** 대시보드를 클릭 하 여 **맬웨어 방지 평가** 아래 **보안 도메인**합니다. hello **맬웨어 방지 평가** 아래 표시 된 대로 대시보드가 표시 됩니다.

![맬웨어 평가](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

Hello를 사용할 수 있습니다 **맬웨어 평가** 다음 보안 문제는 대시보드 tooidentify hello:

* **활성 위협이**:가 손상 되 고 활성 위협이 hello 시스템에 있는 컴퓨터입니다.
* **위협 재구성**: hello 위협 하지만 손상 된 컴퓨터 재구성 합니다.
* **날짜가 지난 서명**: 맬웨어 보호를 사용할 수 있지만 hello 서명을 포함 하는 컴퓨터 최신이 아닙니다.
* **실시간 보호하지 않음**: 맬웨어 방지 프로그램이 설치되지 않은 컴퓨터

### <a name="monitoring-updates"></a>업데이트 모니터링
Hello 최신 보안 업데이트를 적용 하는 것은 최상의 보안 방법 및 업데이트 관리 전략에 포함 되어야 합니다. Microsoft Monitoring Agent 서비스 (HealthService.exe) 모니터링 되는 컴퓨터에서 업데이트 정보를 읽고 한 다음 처리를 위해 클라우드의 hello에이 업데이트 된 정보 toohello OMS 서비스를 보냅니다. Microsoft Monitoring Agent 서비스 hello로 자동 서비스가 구성 된 하 고 hello 대상 컴퓨터에서 항상 실행 해야 합니다.

![업데이트 모니터링](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

논리는 데이터를 업데이트 하는 적용 된 toohello 및 hello 클라우드 서비스는 hello 데이터를 기록 합니다. 누락 된 업데이트가 발견 되 면 hello에 표시 됩니다 **업데이트** 대시보드 합니다. Hello를 사용할 수 있습니다 **업데이트** 대시보드 toowork 누락 된 업데이트 하 고 계획 tooapply을 개발 하 고 필요로 하는 toohello 서버입니다. Tooaccess hello 아래 hello 단계에 따라 **업데이트** 대시보드:

1. Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **보안 및 감사** 바둑판식으로 배열입니다.
2. Hello에 **보안 및 감사** 대시보드를 클릭 하 여 **업데이트 평가** 아래 **보안 도메인**합니다. hello 업데이트 대시보드가 다음과 같이 나타납니다.

![업데이트 평가](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

이 대시보드는 업데이트 평가 toounderstand hello의 현재 상태 컴퓨터와 가장 중요 한 위협을 해결 hello 수행할 수 있습니다. Hello를 사용 하 여 **중요 또는 보안 업데이트가** 타일, IT 관리자가 될 수 tooaccess 자세한 아래와 같이 누락 된 hello 업데이트에 대 한 정보:

![검색 결과](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

이 보고서에 포함 될 수 있는 중요 한 정보 tooidentify hello 위협의 경우이 시스템은에, 취약 한 hello 보안 업데이트 및 MS 공지 hello에 대 한 자세한 세부 정보를 포함 하는 hello와 관련 된 hello Microsoft KB 문서를 포함 하는 데 사용 보안 문제가 있습니다.

### <a name="monitoring-identity-and-access"></a>ID 및 액세스 모니터링
사용자들이 어디에서나 다양한 장치를 사용하여 많은 클라우드 및 온-프레미스 앱에 액세스함에 따라 자격 증명을 보호하는 것이 매우 중요해졌습니다. 자격 증명 도난 공격에 노출 되는를 처음 공격자는 권한 tooa 일반 사용자 자격 증명 tooaccess hello 네트워크 내에서 시스템입니다. 여러 번이 처음 공격이 방식으로 tooget 액세스 toohello 네트워크만, hello 궁극적인 목표는 toodiscover 권한 계정입니다. 

공격자는 무료로 사용할 수 있는 다른 로그온 계정 hello 세션에서 자격 증명 tooextract 도구를 사용 하 여 hello 네트워크에 유지 됩니다. Hello 시스템 구성에 따라 해시, 티켓 또는도 일반 텍스트 암호의 hello 형태로 이러한 자격 증명을 추출할 수 있습니다.  

> [!NOTE]
> 직접 않는 노출 toohello 인터넷 모든 종류의 잘 알려진 사용자 이름 (예: 관리자)를 사용 하 여 해당 try toologin 시도 실패 많은 표시 됩니다. 대부분의 경우에서 되 확인 hello 잘 알려진 사용자 이름을 사용 하지 않는 경우 들어 hello 암호가 강력 합니다.
> 
> 

해당 권한 계정을 손상 되기 전에 가능한 tooidentify 이러한 침입자가 있습니다. 활용할 수 있는 **OMS 보안 및 감사 솔루션** toomonitor id 및 액세스 합니다. Tooaccess hello 아래 hello 단계에 따라 **Id 및 액세스** 대시보드:

1. Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 보안 및 감사 타일입니다.
2. Hello에 **보안 및 감사** 대시보드를 클릭 하 여 **Id 및 액세스** 아래 **보안 도메인**합니다. hello **Id 및 액세스** 아래 표시 된 대로 대시보드가 표시 됩니다.

![ID 및 액세스](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

일반 모니터링 전략에 반드시 ID 모니터링을 포함해야 합니다. IT 관리자는 유효한 특정 사용자 이름에 여러 번의 시도가 있었는지 살펴보아야 합니다. Hello 실제 사용자 이름을 획득 하거나 공격자를 나타내고 toobrute 대입 또는 만료 하드 코드 된 암호를 사용 하는 자동 도구 시도 될 수 있습니다이 합니다.

이 대시보드 사용 IT tooquickly 잠재적 위협 관련된 tooidentity 및 액세스 toocompany의 리소스를 식별 합니다. 특정은 중요 한 tooalso 잠재적인 추세를 파악 합니다. 예를 들어 hello 로그온 시간에 따른 타일에서 확인할 수 있습니다 기간 동안 실패 한 로그온 시도가 수행 된 횟수입니다. 이 경우 컴퓨터를 hello **FileServer** 35 로그온 시도 수신 합니다. 이 컴퓨터를 클릭하여 자세한 정보를 확인할 수 있습니다. 

![자세한 내용](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

이 컴퓨터에 대해 생성 된 hello 보고서는이 패턴에 대 한 중요 한 세부 정보를 제공 합니다. 해당 hello 발견 **계정** 열은 사용 되는 tootry tooaccess 사용자 계정과 hello hello 시스템 hello **TIMEGENERATED** 는 hello 시도가 수행 된 시간 간격을 hello 열 제공 하 고 hello **LOGONTYPENAME** 이 시도가 수행 된 위치를 hello 열 제공 합니다. 이러한 시도 프로그램에 의해 hello 시스템에서 로컬로 수행 된, 경우 hello **프로세스** 열에서 hello 프로세스 이름을 보여 주는 것입니다. 시나리오 hello 로그온 시도 프로그램에서 제공 되는 위치에서 이미 hello 프로세스 이름을 사용할 수 있으며 이제 수행할 수 있습니다 추가로 조사 hello 대상 시스템에 있습니다.

## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 toouse OMS 보안 및 감사 솔루션 toomonitor 리소스입니다. OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:

* [OMS(Operations Management Suite) 개요](operations-management-suite-overview.md)
* [Operations Management Suite 보안 및 감사 솔루션 시작](oms-security-getting-started.md)
* [모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고](oms-security-responding-alerts.md)

