---
title: "Azure 보안 센터를 사용 하 여 개인 데이터 aaaProtect | Microsoft Docs"
description: "Azure Security Center를 사용하여 개인 데이터를 보호합니다."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>위반 및 공격으로부터 개인 데이터 보호: Azure Security Center

이 문서에서 toouse Azure 보안 센터 tooprotect 개인 데이터 침해 방법을 이해 하는 데 도움이 됩니다 하 고 공격입니다.

## <a name="scenario"></a>시나리오 

Hello 미국에서에서 본사는 큰 크루즈 회사 hello 영국 제도 뿐만 아니라 hello 지중해 발트어 바다에서 해당 작업 toooffer 일정 확장 합니다. 이러한 노력에 있어서 toohelp, 이탈리아, 독일, 덴마크, hello 영국에 따라 여러 개의 더 작은 크루즈 줄 획득

hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다. 여기에는 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다. 또한 다음과 같은 인적 자원 정보도 포함됩니다.

- 주소
- 전화 번호
- 납세자 번호
- 의료 보험 정보

hello 크루즈 줄에는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리합니다. 회사 직원 hello 네트워크 hello 회사의 원격 사무실 및 여행사에서 액세스 하는 hello world 주변에 있는 toosome 회사 리소스에 액세스 했습니다.
이러한 위치 및 hello Microsoft 데이터 센터 간에 개인 데이터 hello 네트워크를 통해 이동 됩니다.

## <a name="problem-statement"></a>문제 설명

hello 회사는 Azure 리소스에 대 한 공격 위협을 hello에 대 한 관심이 있습니다. 고객의 및 직원의 개인 데이터 toounauthorized 인원 tooprevent 노출을 원합니다. 방지 및 응답/업데이트 관리를 비롯해는 효과적인 방법은 toomonitor hello 대 한 지속적인 보안 클라우드 리소스에 대 한 지침을 원하는 것입니다.
오늘날의 정교하고 조직화된 공격자들에 대한 강력한 방어선이 필요합니다.

## <a name="company-goal"></a>회사 목표

Hello 회사의 목표 중 하나에 위협 으로부터 보호 하 여 고객의 및 직원의 개인 데이터의 tooensure hello 개인 정보입니다. Toosigns toomitigate 위반의 영향을 hello 즉시이 toorespond 팀의 목표 중 하나입니다. Tooassess hello 보안의 현재 상태는 방법, 취약 한 구성을 식별 되 고 재구성 합니다.

## <a name="solutions"></a>솔루션

Microsoft ASC(Azure Security Center)에서는 통합된 보안 모니터링 및 정책 관리 솔루션을 제공합니다. 사용하기 쉽고 효과적인 위협 방지, 검색 및 대응 기능을 제공합니다.

### <a name="prevention"></a>방지

ASC를 사용 하면 여 tooset 보안 정책 위반을 방지, 적시에 액세스를 제공 및 보안 권장 사항을 구현할 수 있습니다.

지정 된 hello 내의 리소스에 대 한 권장 되는 컨트롤의 hello 집합을 정의 하는 보안 정책을 구독 합니다. Just-in-time에서 액세스에 사용 되는 toolock 노출 tooattacks 감소 하 고 Azure Vm에서 인바운드 트래픽 tooyour 아래로 수 있습니다. Azure 리소스의 hello 보안 상태를 분석 한 후 asc 보안 권장 사항 생성 됩니다.

#### <a name="how-do-i-set-security-policies-in-asc"></a>ASC에서 보안 정책을 설정하려면 어떻게 할까요?

각 구독에 대한 보안 정책을 구성할 수 있습니다. 보안 정책 toomodify 소유자나 해당 구독에 대 한 참가자 여야 합니다. Hello Azure 포털에서에서 수행 hello를 수행 합니다.

1. 선택 **정책** hello ASC 대시보드에.

2. Tooenable hello 정책 원하는 hello 구독을 선택 합니다.

3. 선택 **방지 정책** 구독 당 tooconfigure 정책입니다. **가상 컴퓨터에서 데이터를 수집** 설정할지 너무**에 있습니다.**

4. Hello에 **방지 정책** 옵션을 선택 **에** hello 구독에 대 한 관련 된 tooenable hello 보안 권장 사항입니다.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

명령과 각 사용할 수 있는 hello 정책 권장 사항에 대 한 설명을 자세한 [Azure 보안 센터에 보안 정책을 설정할](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies)합니다.

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>JIT(Just-In-Time) 액세스를 구성하려면 어떻게 할까요?

JIT를 사용 하는 보안 센터 NSG 규칙을 만들어 Azure Vm 인바운드 트래픽 tooyour 아래로 잠급니다. Hello 포트 선택 hello VM toowhich에 인바운드 트래픽을 잠기는 합니다. JIT toouse 액세스, 다음 hello지 않습니다.

1. 선택 hello **시간 VM 액세스 타일에 Just** hello ASC 블레이드에서 합니다.

2. 선택 hello **권장** 탭 합니다.

3. 아래 **Vm**, 원하는 tooenable hello Vm을 선택 합니다. 확인 표시 다음 tooa VM을 추가합니다. 
4. VM에서 **JIT 사용**을 선택합니다.
5. **저장**을 선택합니다.

그런 다음 ASC 권장 JIT를 사용 하도록 설정 하는 hello 기본 포트를 확인할 수 있습니다. 추가할 수 있으며 시간 솔루션에만 있는 tooenable hello 원하는 새 포트를 구성할 수도 있습니다. hello **VM 액세스 시간에에서만** hello 보안 센터에서에서 타일 hello JIT 액세스용으로 구성 하는 Vm 수를 표시 합니다. 또한 hello 지난주 hello에 대 한 액세스 승인 된 요청 수를 보여 줍니다.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

방법에 대 한 지침은 toodo이를 마법사에 대 한 추가 정보에 대 한 런타임 액세스를 참조 하 고 [just-in-time에서를 사용 하 여 가상 컴퓨터 액세스 관리 합니다.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>ASC 보안 권장 사항을 구현하려면 어떻게 할까요?

보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다. hello 권장 사항이 필요한 hello 컨트롤 구성의 hello 프로세스를 안내 합니다. 
1. 선택 hello **권장 사항을** hello ASC 대시보드에서 타일을 합니다.

2. 여기서 각 줄은 한 가지 권장 하는 테이블 형식에 표시 된 대로 hello 권장 사항을 봅니다.

3. toofilter 권장 사항을 선택 **필터** toosee 원하는 hello 심각도 및 상태 값을 선택 합니다.

4. 적용할 수 있는 권장 사항 toodismiss 마우스 오른쪽 단추로 클릭 하 고 선택할 수 **해제 합니다.**

5. 먼저 어떤 권고 사항을 적용해야 하는지 평가합니다.

6. Hello 권장 사항 우선 순위에 따라에서 적용 됩니다.

가능한 권장 사항 및 방법에 대 한 연습 목록은 tooapply 각각 참조 [보안 권장 사항 Azure 보안 센터에서 관리 합니다.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>검색 및 대응

검색 및 응답 함께 이동 하려는 방법 그대로 toorespond 최대한 빨리 위협이 검색 된 후 합니다.
ASC 위협 요소 탐지 자동으로 Azure 리소스, hello 네트워크와 연결 된 파트너 솔루션의 보안 정보를 수집 하 여 작동 합니다. 공격자가 새롭고 점차 정교해지는 악용을 풀어 놓음에 따라 ASC에서는 검색 알고리즘을 빠르게 업데이트할 수 있습니다. ASC 위협 검색 기능이 작동하는 방법에 대한 자세한 내용은 [Azure Security Center 검색 기능](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)을 참조하세요.

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>관리 및 toosecurity 경고 응답 어떻게 해야 합니까?

Hello와 함께 보안 센터에서 우선 순위가 지정 된 보안 경고의 목록이 표시 됩니다 tooquickly 필요한 정보 hello 문제를 조사 합니다. 보안 센터에도 방법에 대 한 권장 사항을 tooremediate 공격입니다. toomanage 보안 경고 hello 다음을 수행 합니다.

1. 선택 hello **보안 경고** hello ASC 대시보드 타일입니다. 그러면 각 경고에 대한 세부 정보가 표시됩니다.

2. 날짜, 상태 및 심각도 기준으로 toofilter 알림을 선택 **필터** 한 다음 원하는 toosee hello 값을 선택 합니다.

3. toorespond tooan 경고를 선택 하 고 및 hello 정보를 검토 하, 공격 된 hello 리소스를 선택 합니다.

4. Hello에 **설명** 필드 권장된 업데이트 관리를 포함 한 정보를 표시 됩니다.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

응답 toosecurity 경고에 대 한 지침 보다 자세한 참조 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity 합니다.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

보안 경고를 조사 하려는 자세한 도움말 hello 회사와 통합할 수 ASC 경고는 자체 SIEM 솔루션을 사용 하 여 [Azure 로그 통합](https://aka.ms/AzLog)합니다.

#### <a name="how-do-i-manage-security-incidents"></a>보안 인시던트를 관리하려면 어떻게 할까요?

ASC에서 보안 인시던트는 킬 체인(kill chain) 패턴과 일치하는 리소스에 대한 모든 경고의 집계입니다. 인시던트 각 항목에 대 한 자세한 내용은 tooobtain 있습니다 수 있도록 하는 hello 목록이 관련된 경고를 표시 합니다. 인시던트 보안 경고 타일 hello 및 블레이드에 표시 됩니다.

tooreview 및 보안 문제를 관리 다음 hello지 않습니다.

1. 선택 hello **보안 경고** 바둑판식으로 배열입니다. 보안 문제가 감지 되 면 hello 보안 경고 그래프 아래 나타납니다. 다른 경고와 다른 아이콘이 표시됩니다.

2. 이 보안 사고에 대 한 자세한 내용은 hello 인시던트 toosee를 선택 합니다. 추가 세부 정보는 해당 전체 설명, 심각도, 현재 상태, 공격 hello 리소스, hello 인시던트에 대 한 업데이트 관리 단계가 hello 및 hello이 서비스에 포함 된 경고입니다.

Toosee 필터링 할 수 있습니다 **인시던트만**, **만 경고**, 또는 **둘 다**합니다.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>Hello 위협 인텔리전스 보고서를 액세스 하려면 어떻게 해야 합니까?

ASC는 여러 소스 tooidentify 위협 요소 로부터 정보를 분석 합니다. tooassist 사고 대응 팀 조사 및 재구성 위협, 보안 센터 발견 된 hello 위협에 대 한 정보를 포함 하는 위협 인텔리전스 보고서에 포함 되어 있습니다.

Security Center에는 공격에 따라 달라질 수 있는 세 가지 유형의 위협 보고서가 있습니다.
사용할 수 있는 hello 보고서에는

- 활동 그룹 보고서: 공격자 및 이들의 목표와 전술에 대해 자세히 설명합니다.

- 캠페인 보고서: 특정 공격 캠페인의 세부 정보에 중점을 둡니다.

- 보고서를 요약 하는 위협: hello 이전 두 보고서에 있는 모든 항목을 다룹니다.

Hello 사고 대응 프로세스 동안 이러한 종류의 정보는 매우 유용, 공격자의 동기 및 어떤 toodo toomitigate 앞으로이 문제는 진행 중인 조사 toounderstand hello 소스 hello 공격의 있는 hello 합니다.

1. tooaccess hello 위협 인텔리전스 보고서, 다음 hello지 않습니다.

2. 선택 hello **보안 경고** hello ASC 대시보드에서 타일을 합니다.

3. 자세한 내용은 tooobtain 원하는 hello 보안 경고를 선택 합니다.

4. Hello에 **보고서** 필드 hello 링크 toohello 위협 인텔리전스 보고서를 클릭 합니다.

5. Hello PDF 파일을 다운로드할 수 있는 열립니다.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Hello ASC 위협 인텔리전스 보고서에 대 한 자세한 내용은 참조 하십시오. [Azure 보안 센터 위협 인텔리전스 보고서입니다.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>평가

테스트, 평가 및의 보안 상태 평가 toohelp, ASC 제공 Qualys와 통합 된 취약성 평가 대 한 클라우드 에이전트는 가상 컴퓨터 권장 구성의 일부분으로 합니다.

hello Qualys 에이전트 취약점 데이터 toohello Qualys 관리 플랫폼으로, 다음 백업 tooASC 취약점와 상태 모니터링 데이터를 전송 하는 보고 합니다. 취약성 평가 솔루션 hello에 표시 되는 권장 사항 tooadd hello **권장 사항을** hello ASC 대시보드에서 블레이드입니다.

Hello 취약점 평가 솔루션 hello 대상 VM에 설치 된 후에 보안 센터 검색 VM toodetect hello 및 시스템 및 응용 프로그램 보안 문제를 식별 합니다. 문제는 hello 아래에 표시 된 검색 **가상 컴퓨터의 권장 사항을** 옵션입니다.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>취약성 평가 솔루션을 구현하려면 어떻게 할까요? 

통합된 취약성 평가 솔루션이 Virtual Machine에 아직 배포되지 않았으면 Security Center에 설치하는 것이 좋습니다.

1. Hello ASC 대시보드 hello에서에서 **권장 사항을** 블레이드를 **취약점 평가 솔루션을 추가 합니다.**

2. Hello Vm tooinstall hello 취약점 평가 솔루션을 원하는 위치를 선택 합니다.

3. **[수]개 VM에 설치**를 클릭합니다.

4. Hello Azure 마켓플레이스 또는 파트너 솔루션 선택 **기존 솔루션을 사용 하 여** 선택 **Qualys 합니다.**

5. Hello hello 자동 업데이트 설정 또는 해제를 해제할 수 **파트너 솔루션** 블레이드입니다.

자세한 방법에 대 한 tooimplement 취약점 평가 솔루션 참조 [Azure 보안 센터에 대 한 취약점 평가 합니다.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>다음 단계

- [Azure Security Center 빠른 시작 가이드](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [소개 tooAzure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Azure 로그 통합에 Azure Security Center 경고 통합](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [통합된 취약성 평가를 통한 Azure Security Center 강화(영문)](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
