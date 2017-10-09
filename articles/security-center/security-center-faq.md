---
title: "aaaAzure 질문과 대답 (FAQ) 보안 센터 | Microsoft Docs"
description: "이 FAQ는 Azure 보안 센터에 대한 질문에 답변합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Azure 보안 센터 FAQ(질문과 대답)
이 FAQ Azure 보안 센터를 방지 하 고 검색에 대 한 향상 된 가시성 및 Microsoft Azure 리소스의 보안을 hello에 대 한 제어를 사용 하 여 toothreats 응답할 때 도움이 되는 서비스에 대 한 질문에 답변 합니다.

> [!NOTE]
> 보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다. toolearn 더 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md)합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>
>

## <a name="general-questions"></a>일반적인 질문
### <a name="what-is-azure-security-center"></a>Azure 보안 센터란?
Azure 보안 센터를 사용 하면 방지 하 고 검색에 대 한 향상 된 가시성 및 Azure 리소스의 보안을 hello에 대 한 제어를 사용 하 여 toothreats 응답할 수 있습니다. 이는 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

### <a name="how-do-i-get-azure-security-center"></a>Azure 보안 센터를 이용하려면 어떻게 해야 하나요?
Azure 보안 센터를 Microsoft Azure 구독에 사용 되 고 hello에서 액세스 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다. ([Toohello 포털에 로그인](https://portal.azure.com)선택, **찾아보기**, 너무 스크롤하여**보안 센터**).  

## <a name="billing"></a>결제
### <a name="how-does-billing-work-for-azure-security-center"></a>Azure 보안 센터에 대한 청구는 어떻게 작동합니까?
Security Center는 두 계층으로 제공됩니다.

hello **무료 계층** 파트너 로부터 보안 제품 및 서비스와 Azure 리소스, 기본 보안 정책, 보안 권장 사항 및 통합의 hello 보안 상태에 대 한 가시성을 제공 합니다.

hello **표준 계층** 고급 위협 감지 기능을 포함 하 여 위협 인텔리전스, 동작 분석, 변칙 검색, 보안 문제 및 위협 attribution 보고서를 추가 합니다. hello 표준 계층은 처음 60 일 hello에 대 한 무료입니다. 60 일 이후에도 toocontinue toouse hello 서비스를 선택한 경우 자동으로 시작 toocharge hello 서비스에 대 한 합니다.  tooupgrade, hello에서 가격 책정 계층을 선택 [보안 정책](security-center-policies.md#set-security-policies)합니다. toolearn 더 참조 [보안 센터 가격](security-center-pricing.md)합니다.

## <a name="permissions"></a>권한
Azure 보안 센터를 사용 하 여 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md)를 제공 하는 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md) toousers, 그룹 및 Azure 서비스에에서 할당할 수 있습니다.

보안 센터의 리소스 tooidentify 보안 문제 및 취약점 hello 구성을 평가합니다. 보안 센터에만 정보를 확인할 때 hello 구독 또는 리소스 그룹에 속한 리소스에 대 한 소유자, 참가자 또는 판독기의 hello 역할이 할당 된 경우 tooa 리소스와 관련 된 합니다.

참조 [Azure 보안 센터에서 사용 권한을](security-center-permissions.md) toolearn 역할 및 보안 센터에서 허용 되는 작업에 대 한 자세한 합니다.

## <a name="data-collection"></a>데이터 수집
보안 센터에서에서 데이터를 수집한 가상 컴퓨터 tooassess 자신의 보안 상태, 보안 권장 사항을 제공 하 고 있습니다 toothreats 경고 합니다. 보안 센터에 처음 액세스할 경우 구독의 모든 가상 컴퓨터에서 데이터 수집을 활성화합니다. 또한 hello 정책 보안 센터에서에서 데이터 수집을 활성화할 수 있습니다.

### <a name="how-do-i-disable-data-collection"></a>데이터 컬렉션을 사용하지 않도록 설정하려면 어떻게 해야 하나요?
Hello Azure 보안 센터 무료 계층을 사용 하는 경우에 언제 든 지 가상 컴퓨터에서 데이터 수집을 해제할 수 있습니다. 데이터 수집 hello 표준 계층에 구독이 필요 합니다. Hello 보안 정책에서에서 구독에 대 한 데이터 수집을 해제할 수 있습니다. ([Toohello Azure 포털에에서 로그인](https://portal.azure.com)선택, **찾아보기**선택, **보안 센터**, 선택 하 고 **정책**.)  구독을 선택 하는 경우는 새 블레이드가 열리고 옵션 tooturn hello **데이터 수집**합니다.

### <a name="how-do-i-enable-data-collection"></a>데이터 컬렉션을 사용하도록 설정하려면 어떻게 해야 하나요?
Hello 보안 정책에서에서 Azure 구독에 대 한 데이터 수집을 활성화할 수 있습니다. tooenable 데이터 컬렉션입니다. [Toohello Azure 포털에에서 로그인](https://portal.azure.com)선택, **찾아보기**선택, **보안 센터**, 선택 하 고 **정책**합니다. 설정 **데이터 수집** 너무**에**합니다.

### <a name="what-happens-when-data-collection-is-enabled"></a>데이터 수집을 사용하도록 설정하면 어떻게 될까요?
데이터 수집을 사용 하는 경우 Microsoft Monitoring Agent hello 자동으로 모든 기존에 프로 비전 하 고 새로 지원 되는 모든 가상 컴퓨터에 배포 된 hello 구독에 있습니다.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Monitoring Agent의 서버 hello 성능에 영향 hello 합니까?
hello 에이전트 명목 양의 시스템 리소스를 사용 하며 hello 성능에 거의 영향을 주지 해야 합니다. 성능에 미치는 영향 및 hello 에이전트 및 확장에 대 한 자세한 내용은 참조 hello [계획 및 운영 가이드](security-center-planning-and-operations-guide.md#data-collection-and-storage)합니다.

### <a name="where-is-my-data-stored"></a>내 데이터는 어디에 저장되나요?
이 에이전트에서 수집된 데이터는 구독 또는 새 작업 영역에 연결된 기존 Log Analytics 작업 영역 중 하나에 저장됩니다. 자세한 내용은 [데이터 보안](security-center-data-security.md)을 참조하세요.

## <a name="using-azure-security-center"></a>Azure 보안 센터 사용
### <a name="what-is-a-security-policy"></a>보안 정책이란?
지정 된 hello 내의 리소스에 대 한 권장 되는 컨트롤의 hello 집합을 정의 하는 보안 정책을 구독 합니다. Azure 보안 센터 tooyour 회사의 보안 요구 사항 및 응용 프로그램의 hello 유형 또는 hello 데이터 각 구독에서의 민감도 따라 Azure 구독에 대 한 정책을 정의 합니다.

hello 보안 정책을 Azure 보안 센터 드라이브에 대 한 보안 권장 사항 및 모니터링에서 사용 하도록 설정 합니다. 보안 정책에 대 한 자세한 정보는 toolearn 참조 [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)합니다.

### <a name="who-can-modify-a-security-policy"></a>보안 정책을 누가 수정할 수 있나요?
보안 정책 toomodify 보안 관리자 또는 소유자 또는 참가자의 해당 구독 이어야 합니다.

tooconfigure 보안 정책을 확인 하려면 어떻게 해야 toolearn [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)합니다.

### <a name="what-is-a-security-recommendation"></a>보안 권장 사항이란?
Azure 보안 센터 리소스를 Azure의 hello 보안 상태를 분석합니다. 잠재적인 보안 취약성이 식별되면 권장 사항이 생성됩니다. hello 권장 사항 가이드 hello 구성 hello 과정을 통해 제어 해야 합니다. 예:

* 맬웨어 방지 toohelp 프로 비전을 식별 하 고 악성 소프트웨어를 제거 합니다.
* 구성 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 와 toocontrol 트래픽 toovirtual 컴퓨터 규칙
* 웹 응용 프로그램을 대상으로 하는 공격을 방어할 웹 응용 프로그램 방화벽 toohelp의 프로 비전
* 누락된 시스템 업데이트 배포
* 초기 권장 hello와 일치 하지 않는 운영 체제 구성을 주소 지정

보안 정책에 사용하도록 설정된 권장 사항만 여기에 표시됩니다.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>내 Azure 리소스의 hello 현재 보안 상태를 확인 하려면 어떻게 해야 합니까?
hello **보안 센터 개요** 블레이드 환경 구분 하 여 계산, 네트워킹, 저장소 및 데이터 및 응용 프로그램의 전반적인 보안 상태를 hello 보여 줍니다. 각 리소스 종류에는 잠재적 보안 취약성이 식별되었는지 나타내는 표시기가 있습니다. 각 타일을 클릭 하면 hello 구독의 리소스에에서 대 한 인벤토리를 함께 보안 센터에서 식별 하는 보안 문제 목록이 표시 됩니다.

### <a name="what-triggers-a-security-alert"></a>보안 경고를 트리거하는 것은 무엇인가요?
Azure 보안 센터를 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크 및 맬웨어 방지 및 방화벽 같은 파트너 솔루션에서 로그 데이터를 결합 시킵니다. 위협이 감지되었을 때 보안 경고가 생성됩니다. 감지되는 사항의 예:

* 알려진 악성 IP 주소와 통신하는 손상된 가상 컴퓨터
* Windows 오류 보고를 사용 하여 감지된 고급 맬웨어
* 가상 컴퓨터에 대한 무작위 공격
* 맬웨어 방지 프로그램 또는 웹 응용 프로그램 방화벽 등과 같은 통합된 파트너 보안 솔루션에서의 보안 경고

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>위협 검색 되 고 Microsoft 보안 대응 센터 Azure 보안 센터를 비교 하 여 경고를 hello 차이 무엇입니까?
Microsoft 보안 대응 센터 (MSRC) hello 선택 보안 hello Azure 네트워크 및 인프라의 모니터링을 수행 하 고 제 3 자에서 위협 인텔리전스 및 남용 불만 받습니다. MSRC 불법 또는 무단 당사자가 고객 데이터에 액세스 또는 Azure의 hello 고객의 사용 준수 하지 않는 hello 용어 허용 가능한 사용에 대 한 인식 되 면 보안 사고 관리자 hello 고객을 알립니다. 알림 전자 메일 toohello 보안 보안 연락처를 지정 하지 않으면 Azure 보안 센터 또는 hello Azure 구독 소유자에 지정 된 연락처를 전송 하 여 일반적으로 발생 합니다.

보안 센터는 지속적으로 hello 고객의 Azure 환경을 모니터링 하 고 분석 tooautomatically 적용 하는 Azure 서비스 광범위 한 잠재적으로 악의적인 활동을 검색 합니다. 이러한 검색 hello 보안 센터 대시보드에 대 한 보안 경고로 표시 됩니다.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Azure Security Center에서는 어떤 Azure 리소스를 모니터링하나요?
Azure 보안 센터 hello 다음 Azure 리소스를 모니터링 합니다.

* 가상 컴퓨터(VM)( [Cloud Services](../cloud-services/cloud-services-choose-me.md)포함)
* Azure 가상 네트워크
* Azure SQL 서비스
* Azure 저장소 계정
* Azure Web Apps([App Service Environment](../app-service/app-service-app-service-environments-readme.md))
* VM 및 [App Service Environment](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>가상 컴퓨터
### <a name="what-types-of-virtual-machines-are-supported"></a>어떤 유형의 가상 컴퓨터가 지원되나요?
두 hello를 사용 하 여 만든 가상 컴퓨터 (Vm)에 사용할 수 있는 모니터링 및 권장 사항 [클래식 및 리소스 관리자 배포 모델](../azure-classic-rm.md)합니다.

지원되는 플랫폼 목록은 [Azure Security Center에서 지원되는 플랫폼](security-center-os-coverage.md)을 참조하세요.

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>Azure 보안 센터를 Azure VM에서 실행 중인 hello 맬웨어 방지 솔루션 인식 하지 못하는 이유는?
Azure Security Center는 Azure 확장을 통해 설치된 맬웨어 방지 프로그램을 확인할 수 있습니다. 예를 들어 보안 센터는 사용자가 제공한 이미지 또는 사용자 고유의 프로세스 (예: 구성 관리 시스템)를 사용 하 여 가상 컴퓨터에 맬웨어 방지를 설치 하는 경우 미리 설치 되어 있던 수 toodetect 맬웨어 방지 합니다.

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>왜 hello 메시지 "누락 된 검색 데이터" 내 VM에 대 한?
VM에 대한 검색 데이터가 없는 경우 이 메시지가 표시됩니다. Azure 보안 센터에서 데이터 수집을 활성화 한 후 검색 데이터 toopopulate (1 시간 미만) 다소 시간이 걸릴 수 있습니다. 검색 데이터의 초기 채우기 hello 후 검색 데이터가 전혀 없는 또는 최근 검색 데이터가 없기 때문에이 메시지가 나타날 수 있습니다. VM이 중지된 상태이면 검사를 수행해도 데이터가 입력되지 않습니다. 이 메시지는 검색 데이터가 최근에 (에 따라 보존 정책에는 30 일의 기본값이 hello Windows 에이전트에 대 한 hello) 채워지지가 경우에 나타날 수 있습니다.

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>이유 받기 hello 메시지 "VM 에이전트는 Missing?"
hello VM 에이전트가 Vm tooenable 데이터 컬렉션에 설치 해야 합니다. hello Azure Marketplace에서에서 배포 되는 Vm에 대 한 hello VM 에이전트는 기본적으로 설치 됩니다. Tooinstall 다른 Vm에서 VM 에이전트를 hello 하는 방법에 대 한 내용은 hello 블로그 게시물을 참조 [VM 에이전트 및 확장](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)합니다.
