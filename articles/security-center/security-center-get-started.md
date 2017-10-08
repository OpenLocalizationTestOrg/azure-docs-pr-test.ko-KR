---
title: "aaaAzure 보안 센터 빠른 시작 가이드 | Microsoft Docs"
description: "이 문서에서는 hello 보안 모니터링 및 정책 관리 구성 요소를 안내 하 고 toonext 단계를 연결 하 여 Azure 보안 센터를 신속 하 게 시작할 수 있습니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Azure Security Center 빠른 시작 가이드
이 문서에서는 빠르게 시작 Azure 보안 센터 hello 모니터링 및 정책 관리의 보안 구성 요소 보안 센터를 안내 하 여 합니다.

> [!NOTE]
> 보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다. 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>
>

## <a name="prerequisites"></a>필수 조건
보안 센터와 시작 tooget, 구독 tooMicrosoft Azure 있어야 합니다. 구독이 없는 경우 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)으로 등록할 수 있습니다.

보안 센터의 hello 무료 계층 구독에 자동으로 활성화 하 고 Azure 리소스의 hello 보안 상태에 대 한 가시성을 제공 합니다. Azure 파트너의 보안 제품과 서비스를 통해 기본 보안 정책 관리, 보안 권장 사항 및 통합이 제공됩니다.

보안 센터 hello에서 액세스 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)합니다. toolearn hello Azure 포털에 대 한 자세한 참조 hello [포털 설명서](https://azure.microsoft.com/documentation/services/azure-portal/)합니다.

## <a name="permissions"></a>권한
보안 센터에만 표시와 관련 된 정보가 tooan hello 구독 또는 리소스 그룹에 속한 리소스에 대 한 소유자, 참가자 또는 판독기의 hello 역할 할당 될 때 Azure 리소스입니다. 참조 [Azure 보안 센터에서 사용 권한을](security-center-permissions.md) toolearn 역할 및 보안 센터에서 허용 되는 작업에 대 한 자세한 합니다.

## <a name="data-collection"></a>데이터 수집
보안 센터에서에서 데이터를 수집한 가상 컴퓨터 (Vm) tooassess 자신의 보안 상태, 보안 권장 사항을 제공 하 고 있습니다 toothreats 경고 합니다. Security Center에 처음 액세스하는 경우 구독의 모든 VM에서 데이터 수집을 활성화합니다. 보안 센터에 모든 기존 프로 비전 hello Microsoft Monitoring Agent는 Azure Vm 및 만들어진 새로 지원. 참조 [데이터 컬렉션 활성화](security-center-enable-data-collection.md) toolearn 데이터 수집 작동 방식에 대 한 자세한 합니다.

데이터 수집을 사용하는 것이 좋습니다. 보안 센터의 무료 계층 hello를 사용 하는 경우에 hello 보안 정책에서 데이터 수집을 해제 하 여 Vm에서 데이터 수집을 해제할 수 있습니다. 데이터 컬렉션 보안 센터의 hello 표준 계층에 구독이 필요 합니다. 참조 [보안 센터 가격](security-center-pricing.md) 무료 및 표준 가격 책정 계층에 더 알아봅니다 toolearn hello 합니다.

단계를 수행 하는 hello 방법을 사용 하 여 tooaccess hello 보안 센터의 구성 요소에 설명 합니다. 이 단계에서는 보여줍니다 어떻게 tooturn 아웃 tooopt를 선택 하는 경우 데이터 수집 해제 합니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다. 단계별 가이드는 아닙니다.
>
>

## <a name="access-security-center"></a>Security Center 액세스
Hello 포털에서 이러한 단계 tooaccess 보안 센터를 따릅니다.

1. Hello에 **Microsoft Azure** 메뉴 선택 **보안 센터**합니다.

   ![Azure 메뉴][1]
2. 액세스 하려는 경우 보안 센터 hello에 대 한 처음으로, hello **시작** 블레이드를 엽니다. 선택 **시작 보안 센터** tooopen hello **보안 센터** 블레이드 및 tooenable 데이터 수집 합니다.
   ![시작 화면][10]
3. Hello 시작 블레이드에서 보안 센터를 시작 하거나에서 hello Microsoft Azure 보안 센터를 선택 하면 hello **보안 센터** 블레이드를 엽니다. 쉽게 액세스할 수 있도록 toohello에 대 한 **보안 센터** hello 이후, 선택 hello 블레이드 **Pin 블레이드 toodashboard** 옵션 (오른쪽 위).
   ![Pin 블레이드 toodashboard 옵션][2]

## <a name="use-security-center"></a>Security Center 사용
Azure 구독 및 리소스 그룹에 대한 보안 정책을 구성할 수 있습니다. 다음과 같이 구독에 대한 보안 정책을 구성하세요.

1. Hello에 **보안 센터** 블레이드, 선택 hello **정책** 바둑판식으로 배열입니다.
2. Hello에 **보안 정책-구독 당 정책을 정의** 블레이드, 구독을 선택 합니다.
3. Hello에 **보안 정책** 블레이드에서 **데이터 수집** 활성화 tooautomatically 수집 로그 됩니다. 모니터링 확장 hello hello 구독에서 모든 현재와 새 vm 프로 비전 됩니다. (보안 센터의 hello 무료 계층에서 있습니다 수 옵트아웃 데이터 수집을 설정 하 여 **데이터 수집** 너무**오프**합니다. 설정 **데이터 수집** 너무**오프** 보안 센터 보안 경고 및 권장 사항을 제공 하는 것을 금지 합니다.)
4. Hello에 **보안 정책** 블레이드를 **방지 정책**합니다. Hello 열립니다 **방지 정책** 블레이드입니다.
5. Hello에 **방지 정책** 블레이드에서 hello 권장 보안 정책의 일부로 toosee 되도록 설정 합니다. 예제:

   * 설정 **시스템 업데이트** 너무**에** 검사가 모든 누락 된 운영 체제 업데이트에 대 한 Vm을 지원 합니다.
   * 설정 **OS 취약점** 너무**에** 검색이 지원 되는 모든 Vm tooidentify 하도록 할 수 있는 모든 OS 구성을 hello VM tooattack 으로부터 더 취약 합니다.

### <a name="view-recommendations"></a>권장 사항 보기
1. Toohello 반환 **보안 센터** 블레이드에 대 한 선택 hello **권장 사항을** 바둑판식으로 배열입니다. 보안 센터 리소스를 Azure의 hello 보안 상태를 정기적으로 분석합니다. 보안 센터에는 잠재적인 보안 취약점 식별, hello에 권장 사항을 표시 **권장 사항을** 블레이드입니다.
   ![Azure Security Center의 권장 사항][5]
2. Hello에 대 한 권장 구성을 선택 **권장 사항을** 블레이드 tooview 자세한 정보 및/또는 tootake 작업 tooresolve hello 발급 합니다.

### <a name="view-hello-security-state-of-your-resources"></a>리소스 보기 hello 보안 상태
1. Toohello 반환 **보안 센터** 블레이드입니다. hello **방지** hello 대시보드의 Vm, 네트워킹, 데이터 및 응용 프로그램에 대 한 hello 보안 상태 표시기를 포함 합니다.
2. 선택 **계산** tooview 자세한 정보. hello **계산** 블레이드 보여 주는 세 개의 탭을 엽니다.

  - **개요** - 모니터링 및 VM 권장 사항이 포함되어 있습니다.
  - **가상 컴퓨터** - 모든 VM과 현재 보안 상태를 나열합니다.
  - **클라우드 서비스**: Security Center에서 모니터링하는 웹 및 작업자 역할을 나열합니다.

    ![Azure 보안 센터에서 hello 리소스 상태 타일][6]

3. Hello에 **개요** 탭 아래에서 권장 구성을 선택 합니다 **가상 컴퓨터의 권장 사항을** tooview 정보 및/또는 take 작업 tooconfigure 필요한 컨트롤을 더 합니다.
4. Hello에 **가상 컴퓨터** 탭 VM tooview 추가 세부 정보를 선택 합니다.

### <a name="view-security-alerts"></a>보안 경고 보기
1. Toohello 반환 **보안 센터** 블레이드에 대 한 선택 hello **보안 경고** 바둑판식으로 배열입니다. hello **보안 경고** 블레이드가 열리고 경고의 목록이 표시 됩니다. 이러한 경고를 생성 하는 hello 네트워크 작업 및 보안 로그의 보안 센터 분석 합니다. 통합된 파트너 솔루션에서 보내는 경고도 있습니다.
   ![Azure Security Center의 보안 경고][7]

   > [!NOTE]
   > 보안 경고는 보안 센터의 hello 표준 계층에서 사용 되는 경우에 사용할 수만 있습니다. Hello 표준 계층의 60 일 무료 평가판 ´ ù. 참조 [다음 단계](#next-steps) tooget 표준 hello 하는 방법에 대 한 내용은 계층입니다.
   >
   >
2. 경고 tooview 추가 정보를 선택 합니다. 이 예에서는 **수정된 시스템 이진 파일 검색**을 선택합니다. Hello 경고에 대 한 추가 세부 정보를 제공 하는 블레이드가 열립니다.
   ![Azure Security Center의 보안 경고 세부 정보][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>파트너 솔루션의 hello 상태 보기
1. Toohello 반환 **보안 센터** 블레이드입니다. hello **파트너 솔루션** 타일 모니터링할 수 있습니다를 한 눈에 hello Azure 구독과 통합 하 여 파트너 솔루션의 상태입니다.
2. 선택 hello **파트너 솔루션** 바둑판식으로 배열입니다. 블레이드 열리고 파트너 솔루션의 목록 표시 tooSecurity 센터 연결.
   ![파트너 솔루션][9]
3. 파트너 솔루션을 선택합니다. 이 예에서는 hello를 선택 하겠습니다 **QualysVa1** 솔루션입니다.  블레이드가 열리고 hello 업체 솔루션 및 hello 솔루션의 hello 상태 관련 리소스를 보여 줍니다. 선택 **솔루션 콘솔** 이 솔루션에 tooopen hello 파트너 관리 환경을 제공 합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 toohello 모니터링 및 정책 관리의 보안 구성 요소를 보안 센터 도입 되었습니다. 보안 센터에 익숙하다면 했으므로 hello 다음 단계를 시도해 보십시오.

* Azure 구독의 보안 정책을 구성합니다. toolearn 더 참조 [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)합니다.
* Hello 권장 사항을 사용 하 여 보안 센터 toohelp에서 Azure 리소스를 보호 합니다. toolearn 더 참조 [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md)합니다.
* 현재 보안 경고를 검토하고 관리합니다. toolearn 더 참조 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)합니다.
- [Azure Security Center 데이터 보안](security-center-data-security.md) - Security Center에서 데이터를 관리하고 보호하는 방법을 알아봅니다.
* Hello에 대 한 자세한 [고급 위협 검색 기능](security-center-detection-capabilities.md) hello 함께 제공 되 [표준 계층](security-center-pricing.md) 보안 센터의 합니다. hello 표준 계층은 무료로 제공 되지만 hello에 대 한 첫 번째 60 일입니다.
* 보안 센터를 사용 하는 방법에 대 한 질문이 있으면 참조 hello [Azure 보안 센터 FAQ](security-center-faq.md)합니다.

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
