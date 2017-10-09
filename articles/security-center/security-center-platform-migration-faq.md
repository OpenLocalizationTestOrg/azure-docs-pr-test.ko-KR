---
title: "aaaSecurity Center 플랫폼 마이그레이션 관련 FAQ | Microsoft Docs"
description: "이 FAQ hello Azure 보안 센터 플랫폼 마이그레이션에 대 한 질문에 답변 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Security Center 마이그레이션 FAQ
초기 6 월 2017 Azure 보안 센터 hello Microsoft Monitoring Agent toocollect 및 저장소 데이터를 사용 하 여 시작 되었습니다. toolearn 더 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md)합니다. 이 FAQ hello 플랫폼 마이그레이션에 대 한 질문에 답변 합니다.

## <a name="data-collection-agents-and-workspaces"></a>데이터 수집, 에이전트 및 작업 영역

### <a name="how-is-data-collected"></a>데이터를 어떻게 수집해야 하나요?
보안 센터 Vm의 hello toocollect 보안 데이터를 Microsoft Monitoring Agent를 사용 합니다. hello 보안 데이터에는 사용 되는 tooidentify 취약점 보안 구성 및 사용 되는 toodetect 위협 요소인 보안 이벤트에 대 한 정보가 포함 됩니다. Hello 에이전트에 의해 수집 된 데이터는 기존 로그 분석 작업 영역 연결 toohello VM 또는 보안 센터에서 만든 새 작업 영역 중 하나에 저장 됩니다. 보안 센터 새 작업 영역을 만들 때의 hello hello geolocation VM 고려 됩니다.

> [!NOTE]
> hello Microsoft Monitoring Agent는 hello Operations Management Suite (OMS), 로그 분석 서비스 및 System Center Operations Manager (SCOM)에서 사용 되는 동일한 에이전트인 hello는입니다.
>
>

처음으로 또는 구독을 마이그레이션하는 경우 hello에 대 한 데이터 수집을 활성화 하는 경우 각 Vm에 Azure 확장으로 hello Microsoft Monitoring Agent가 이미 설치 되어 있는 경우 보안 센터 toosee를 확인 합니다. Hello Microsoft Monitoring Agent 설치 되지 않은 경우 다음 보안 센터를 수행 합니다.

- hello VM에 hello Microsoft Monitoring agent를 설치 합니다.
   - 에이전트는 작업 영역 연결된 toothis 보안 센터에서 이미 만든 작업 영역 동일한 지리적 위치의 hello VM을 같이 hello hello에 있는 경우
   - 작업 영역이 없는 경우 보안 센터 새 리소스 그룹 및 해당 지리적 위치에서 작업 영역을 기본 만들고 hello 에이전트 toothat 작업 영역을 연결 합니다. hello hello 작업 영역 및 리소스 그룹에 대 한 명명 규칙은:

       작업 영역: DefaultWorkspace-[subscription-ID]-[geo]

       리소스 그룹: DefaultResouceGroup-[geo]
- hello 작업 영역에서 보안 센터 솔루션을 설치 합니다.

hello 영역의 hello 위치 hello VM의 hello 위치를 기반으로 합니다. toolearn 더 참조 [데이터 보안](security-center-data-security.md)합니다.

> [!NOTE]
> 이전 tooplatform 마이그레이션 보안 센터는 hello Azure 모니터링 에이전트를 사용 하 여 Vm에서 보안 데이터를 수집 하 고 저장소 계정에 데이터를 저장 합니다. Hello 플랫폼 마이그레이션 후 보안 센터 hello Microsoft Monitoring Agent를 사용 하 여 및 작업 영역 toocollect 및 스토어 hello 같은 데이터입니다. hello 마이그레이션 후 hello 저장소 계정을 제거할 수 있습니다.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>로그 분석 또는 보안 센터에서 만든 hello 작업 영역에서 OMS에 대 한 요금이 청구 하나요?
아니요. Security Center에서 만든 작업 영역은 노드 요금 청구당 OMS에 구성되는 동안 OMS 요금이 청구되지 않습니다. 보안 센터 청구는 항상 사용자 보안 센터 보안 정책 및 hello 솔루션 작업 영역에 설치 된 기준:

- **무료 계층** – 보안 센터 hello 기본 작업 영역에 hello 'SecurityCenterFree' 솔루션을 설치 합니다. Hello 무료 계층에 대 한 요금이 청구 되지 않습니다.
- **표준 계층** – 보안 센터 'SecurityCenterFree' hello를 설치 하 고 솔루션에 'Security' hello 기본 작업 영역입니다.

자세한 내용은 [Security Center 가격 책정](https://azure.microsoft.com/pricing/details/security-center/)을 참조하세요. 가격 페이지 주소 hello toosecurity 데이터 저장 및 2017 년 6 월에에서 할부 청구 시작을 변경 합니다.

> [!NOTE]
> 보안 센터에서 만든 작업 영역의 hello OMS 가격 책정 계층에 보안 센터 청구 영향을 주지 않습니다.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>보안 센터에서 만든 hello 기본 작업 영역을 삭제할 수 있습니까?
**Hello 기본 작업 영역 삭제 권장 되지 않습니다.** 보안 센터 내 vm에서 hello 기본 작업 영역 toostore 보안 데이터를 사용합니다.  보안 센터 작업 영역을 삭제 하는 경우는 없습니다 toocollect이이 데이터 및 몇 가지 보안 권장 사항 및 경고를 사용할 수 없는 경우

toorecover, 제거 hello hello Vm 삭제 하는 연결 된 toohello 작업 영역에서 Microsoft Monitoring Agent입니다. 보안 센터 hello 에이전트를 다시 설치 하 고 새 기본 작업 영역을 만듭니다.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>경우에 어떻게 hello Microsoft Monitoring Agent hello VM에 대 한 확장으로 이미 설치 된?
보안 센터에서 기존 연결 toouser 작업 영역을 재정의 하지 않습니다. 보안 센터 hello hello 작업 영역에서 VM에서에서 보안 데이터를 저장 이미 연결 되었습니다.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>경우에 어떻게 확장 아니라 hello 컴퓨터에 설치 된 Microsoft Monitoring Agent 해야 했던?
Hello Microsoft Monitoring Agent가 직접 설치 된 경우 hello에 VM (이 아니라 Azure 확장), 보안 센터를 설치 하지 않습니다 hello Microsoft Monitoring Agent 및 보안 모니터링 제한 됩니다.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>이러한 확장을 제거할 경우의 hello 영향 이란?
Hello Microsoft 모니터링 확장을 제거 하는 경우 보안 센터 hello VM 수 toocollect 보안 데이터는 하지 않으며 일부 보안 권장 사항 및 경고 사용할 수 없습니다. 보안 센터에는 24 시간 이내 hello VM hello 확장 없습니다 및 파일이 손실 hello 확장 결정 합니다.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Hello 자동 에이전트 설치 및 작업 영역 만들기를 중지 하는 방법
Hello 보안 정책에서 구독에 대 한 데이터 수집을 해제할 수 있지만 권장 되지는 않습니다. 데이터 컬렉션을 해제하면 Security Center 권장 사항 및 경고를 제한합니다. 데이터 수집 hello 표준 가격 책정 계층에 구독이 필요 합니다. toodisable 데이터 수집:

1. 구독 hello 표준 계층으로 구성 된 경우 해당 구독에 대 한 보안 정책을 hello 열고 hello 선택 **무료** 계층입니다.

   ![가격 책정 계층 ][1]

2. 다음으로, 선택 하 여 데이터 수집을 해제할 **오프** hello에 **보안 정책-데이터 수집** 블레이드입니다.

   ![데이터 수집][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Security Center에서 설치한 OMS 확장을 제거하려면 어떻게 할까요?
Microsoft Monitoring Agent hello를 수동으로 제거할 수 있습니다. Security Center 권장 사항 및 경고를 제한하기 때문에 권장되지는 않습니다.

> [!NOTE]
> 데이터 수집을 사용 하는 경우 보안 센터를 다시 설치 하려고 hello 에이전트 제거 하 고 나면 합니다.  Hello 에이전트를 수동으로 제거 하기 전에 toodisable 데이터 수집을 해야 합니다. 참조 [hello 자동 에이전트 설치 및 작업 영역 만들기 중지 어떻게?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) 에 대 한 데이터 수집을 사용 하지 않도록 설정 합니다.
>
>

toomanually는 hello 에이전트를 제거 합니다.

1.  Hello 포털을 열고 **로그 분석**합니다.
2.  Hello 로그 분석 블레이드에서 작업 영역을 선택 합니다.
3.  원하는 toomonitor 및 선택 하지 않는 각 VM 선택 **연결 끊기**합니다.

   ![Hello 에이전트 제거][3]

> [!NOTE]
> Linux VM에 이미 비 확장 OMS 에이전트 hello 에이전트도 제거 hello 확장 제거 되 고 hello 고객에 게 tooreinstall 것입니다.
>
>

## <a name="existing-oms-customers"></a>기존 OMS 고객

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Security Center에서 VM과 작업 영역 간의 모든 기존 연결을 재정의하나요?
VM에 Azure 확장으로 설치 된 Microsoft Monitoring Agent hello 이미 있으면 보안 센터 hello 기존 작업 영역 연결을 재정의 하지 않습니다. 대신, 보안 센터 hello 기존 작업 영역을 사용합니다.

보안 센터 솔루션은 hello 작업 영역에 없는 경우 설치를 이미 사용 하며 hello 솔루션은 적용 된 유일한 toohello 관련 Vm입니다. 솔루션에 추가 하면 기본 tooall Windows 및 Linux 에이전트 연결된 tooyour 로그 분석 작업 영역에 의해 자동으로 배포 됩니다. [솔루션 Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), tooapply 범위를 허용 하는 OMS 기능, tooyour 솔루션입니다.

Hello Microsoft Monitoring Agent가 직접 설치 된 경우 hello에 VM (이 아니라 Azure 확장), 보안 센터를 설치 하지 않습니다 hello Microsoft Monitoring Agent 및 보안 모니터링 제한 됩니다.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>hello 데이터 플랫폼 마이그레이션 hello 연결 내 Vm 및 내 작업 영역 중 하나를 위반 하는 것으로 의심 되는 경우 어떻게 해야 하나요?
이런 상황은 일어나지 않습니다. 있다면 않습니다 [Azure 지원 요청 만들기](../azure-supportability/how-to-create-azure-support-request.md) hello 다음 세부 정보를 포함 합니다.

- VM을 영향을 받음 hello의 hello Azure 리소스 ID
- hello 연결이 끊겼습니다 전에 hello 확장에 구성 된 hello 영역의 hello Azure 리소스 ID
- hello 에이전트와 이전에 설치 된 버전

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>Security Center에서 기존 OMS 작업 영역에 솔루션을 설치하나요? Hello 요금이 청구 될 무엇입니까?
Tooyour 가격 책정 계층에 따라이 작업 영역에서 솔루션을 사용 하면 VM은 이미 연결 된 tooa 작업 영역을 만든 보안 센터 보안 센터를 식별 하는 경우. 솔루션 hello를 통해 적용 된 유일한 toohello 관련 Azure Vm은 [솔루션을 대상으로](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)이므로 hello 청구 남아 hello 동일 합니다.

- **무료 계층** – 보안 센터 hello 작업 영역에 hello 'SecurityCenterFree' 솔루션을 설치 합니다. Hello 무료 계층에 대 한 요금이 청구 되지 않습니다.
- **표준 계층** – 보안 센터 'SecurityCenterFree' hello를 설치 하 고 솔루션에 'Security' hello 작업 영역입니다.

   ![기본 작업 영역의 솔루션][4]

> [!NOTE]
> hello 로그 분석에서 'Security' 솔루션은 hello 보안 및 감사 솔루션을 OMS에입니다.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>내 환경에서 이미 작업 영역, 사용 합니까 toocollect 보안 데이터?
VM에 Azure 확장으로 설치 된 Microsoft Monitoring Agent hello 이미 있으면 보안 센터 hello 기존 연결 된 작업 영역을 사용 합니다. 보안 센터 솔루션은 hello 작업 영역에 없는 경우 설치를 이미 사용 하며 hello 솔루션은 적용 된 유일한 toohello 통해 관련 Vm [솔루션을 대상으로](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)합니다.

보안 센터 Vm에서 hello Microsoft Monitoring Agent는 설치 될 때 보안 센터에서 만든 hello 기본 중 사용 합니다. 곧 고객은 어떤 중 사용 되는 수 tooconfigure 됩니다.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>내 작업 영역에 보안 솔루션이 이미 있습니다. Hello 요금이 청구 될 무엇입니까?
hello 보안 및 감사 솔루션은 Azure Vm에 대 한 보안 센터 표준 계층 기능을 사용 하는 tooenable입니다. Hello 보안 및 감사 솔루션 작업 영역에 이미 설치 되어 있는 경우 보안 센터 hello 기존 솔루션을 사용 합니다. 요금 청구는 변하지 않습니다.

## <a name="next-steps"></a>다음 단계
hello 보안 센터 플랫폼 마이그레이션에 대해 자세히 toolearn 참조

- [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)
- [Azure Security Center 문제 해결 가이드](security-center-troubleshooting-guide.md).

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
