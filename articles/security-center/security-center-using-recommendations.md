---
title: "Azure 보안 센터 권장 사항 tooenhance 보안 aaaUse | Microsoft Docs"
description: " Toouse 보안 정책 및 Azure 보안 센터 toohelp에서 권장 하는 보안 공격을 줄일 방법을 알아봅니다. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Azure 보안 센터를 사용 하 여 권장 사항 tooenhance 보안
보안 정책을 구성 하 고 다음 Azure 보안 센터에서 제공 하는 hello 권장 사항을 구현 하 여 중요 한 보안 이벤트의 hello 가능성을 줄일 수 있습니다. 이 문서에서는 toouse 보안 정책 및 보안 센터 toohelp에서 권장 하는 보안 공격을 줄일 방법을 보여 줍니다.

> [!NOTE]
> Hello 역할 및 보안 센터 hello에 도입 된 개념을 기반으로이 문서 [계획 및 운영 가이드](security-center-planning-and-operations-guide.md)합니다. 계속 하기 전에 좋습니다 tooreview hello 계획 가이드를이 있습니다.
>
>

## <a name="managing-security-recommendations"></a>보안 권장 사항 관리
보안 정책 hello hello 지정된 구독 또는 리소스 그룹 내의 리소스에 대 한 권장 되는 컨트롤 집합을 정의 합니다. 보안 센터 tooyour 회사의 보안 요구 사항에 따라 정책을 정의 합니다. toolearn 더 참조 [보안 센터에 보안 정책을 설정할](security-center-policies.md)합니다.

리소스 그룹에 대 한 보안 정책은 hello 구독 수준에서 상속 됩니다.

![보안 정책 상속][1]

특정 리소스 그룹에 사용자 지정 정책을 해야 할 경우에 hello 리소스 그룹에서 상속을 해제할 수 있습니다. toodisable, 상속 tooUnique hello 보안 정책 블레이드의 설정 및 보안 센터에 대 한 권장 사항을 표시 하는 hello 컨트롤을 사용자 지정 합니다.

예를 들어 hello SQL 데이터베이스 투명 한 데이터 암호화 (TDE) 정책 필요 하지 않은 워크 로드를 사용 하도록 설정한 경우 hello 구독 수준에서 hello 정책을 해제 하 고 SQL TDE가 필요한 곳 hello 리소스 그룹에만 사용 하도록 설정 합니다.

> [!NOTE]
> 구독 수준 정책 및 리소스 그룹 수준의 정책 간에 충돌이 발생 하는 경우 hello 리소스 그룹 수준 정책이 우선 합니다.
>
>

보안 센터 리소스를 Azure의 hello 보안 상태를 분석합니다. 보안 센터 잠재적인 보안 문제를 식별 하는 경우 hello 컨트롤 hello 보안 정책 설정에 따라 권장 구성을 만듭니다. hello 권장 사항을 hello hello 필요한 보안 제어를 구성 과정을 안내 합니다.

현재 Security Center의 정책 권장 사항은 시스템 업데이트, OS 구성, 네트워크 서브넷 및 VM(가상 컴퓨터)의 네트워크 보안 그룹, SQL Database 감사, SQL Database TDE 및 웹 응용 프로그램 방화벽에 집중되어 있습니다. 보안 센터 권장 구성의 가장 최신 적용 범위 hello에 대 한 참조 [보안 권장 사항 보안 센터에서 관리](security-center-recommendations.md)합니다.

## <a name="scenario"></a>시나리오
이 시나리오에 보안 센터 권장 사항을 모니터링 하 고 작업을 수행 하 여 toouse 보안 센터 toohelp hello 가능성 문제가 발생 한 중요 한 보안을 줄이는 방법을 보여줍니다. hello 시나리오 사용 하 여 hello 가상 회사인 Contoso, 및 역할에 제공 된 보안 센터 hello [계획 및 운영 가이드](security-center-planning-and-operations-guide.md#security-roles-and-access-controls)합니다. hello 역할 개인과 보안 센터 tooperform 다른 보안 관련 작업을 사용할 수 있는 팀을 나타냅니다. hello 역할이 있습니다.

![시나리오 역할][2]

최근에 Contoso 자신의 온-프레미스 리소스 tooAzure 중 일부를 마이그레이션. Contoso가 tooimplement와 hello 클라우드의 해당 리소스의 취약점 tooa 보안 공격을 축소 하는 보호를 유지 합니다.

## <a name="recommended-solution"></a>권장된 솔루션
솔루션은 toouse 보안 센터 tooprevent 및 보안 취약점을 탐지 합니다. Contoso는 해당 Azure 구독을 통해 tooSecurity 센터를 있습니다. hello [무료 계층](security-center-pricing.md) 의 보안 센터 자동으로 모든 Azure 구독에서 사용 하 고 자신의 구독에 있는 모든 Vm에서 데이터 수집을 활성화 합니다.

Contoso의 IT 보안에서 David는 Security Center를 사용하여 **보안 정책**을 구성합니다. 보안 센터 Contoso의 Azure 리소스의 hello 보안 상태를 분석합니다. 보안 센터 잠재적인 보안 문제를 식별 하는 경우 생성 **권장 사항을** hello 보안 정책으로에서 설정 하는 hello 컨트롤 기반으로 합니다.

클라우드 워크로드 소유자인 Jeff는 Contoso의 보안 정책에 따라 보호 방법을 구현하고 유지 관리하는 업무를 담당합니다. Jeff는 보안 센터 tooapply 보호 기능에서 만든 hello 권장 사항을 모니터링할 수 있습니다. hello 권장 사항을 Jeff hello 필요한 보안 제어를 구성 hello 과정 안내 됩니다.

Jeff tooimplement 순서 및 보호를 유지 하 고, 보안 취약점을 그 요구를 제거 합니다.

- Security Center에서 제공한 보안 권장 사항 모니터링
- 보안 권장 사항을 평가하고 적용하거나 해제해야 할지를 결정합니다.
- 보안 권장 사항 적용

제프의 단계 toosee 보겠습니다 수행 방법을 사용 하 여 보안 센터 권장 사항을 tooguide 그 컨트롤 tooeliminate 보안 취약점 구성 hello 과정을 통해.

## <a name="how-tooimplement-this-solution"></a>어떻게 tooimplement이이 솔루션
제프가 너무 로그인[Azure 포털](https://azure.microsoft.com/features/azure-portal/) 열립니다 hello 보안 센터 콘솔 및 합니다. 활동을 모니터링 하는 그의 매일의 일환으로, hello 다음 단계를 수행 하 여 보안 권장 사항이 경우 toosee 체크:

1. 제프 선택 hello **권장 사항을** 타일 tooopen hello **권장 사항을** 블레이드입니다.
   ![타일 선택 hello 권장 사항][3]
2. Jeff는 hello 권장 사항 목록을 검토합니다. 느껴질 보안 센터 권장 사항 우선 순위에 따라 우선 순위가 가장 높은 우선 순위 toolowest에서 hello 목록을 제공 했습니다. 그 tooaddress hello 목록에는 우선 순위가 높은 권장 구성을 결정합니다. 그런 다음 선택 **Endpoint Protection 설치** hello에 **권장 사항을** 블레이드입니다.
3. hello **Endpoint Protection 설치** 블레이드 열리고 사용 하도록 설정 하는 맬웨어 방지 프로그램 없이 Vm 목록을 표시 합니다. 제프 Vm hello 목록을 검토 하 모든 Vm을 선택 하 고 다음 선택 **3 개의 Vm에 설치**합니다.
   ![Endpoint Protection 설치][4]
4. hello **Endpoint Protection 선택** 블레이드 두 가지 맬웨어 방지 솔루션 제공 Jeff 열립니다. 제프 선택 hello **Microsoft 맬웨어 방지** 솔루션입니다.
5. Hello 맬웨어 방지 솔루션에 대 한 추가 정보가 표시 됩니다. Jeff는 **만들기**를 선택합니다.
   ![Microsoft 맬웨어 방지][5]
6. 제프 hello에서 필요한 hello 구성 설정에 진입 **설치** 블레이드에 대 한 선택 **확인**합니다.

[Microsoft 맬웨어 방지](../security/azure-security-antimalware.md) 이제 hello 사용 중인 Vm을 선택 합니다.

제프 구현에서 결정 hello 높은 우선 순위 및 중간 우선 권장 사항을 통해 toomove를 계속 합니다. 제프 참조 hello [보안 권장 사항 관리](security-center-recommendations.md) toounderstand hello 권장 사항 및 각 동작이 수행 그가 적용 하는 경우 문서.

Jeff는 학습 [Microsoft 보안 대응 센터 (MSRC)](../security/azure-security-response-center.md) 선택 보안 hello Azure 네트워크 및 인프라의 모니터링을 수행 하 고 제 3 자에서 위협 인텔리전스 및 남용 불만 사항을 받습니다. Jeff는 Contoso의 Azure 구독에 대 한 보안 연락처 세부 정보를 제공, 하는 경우 Microsoft 연락처 hello MSRC 해당 Contoso의 고객 데이터가 검색 된 경우 Contoso 불법 또는 무단 사용자가 액세스 되었습니다. Hello를 적용 하는 그 Jeff에 따라 보겠습니다 **보안 연락처 세부 정보를 제공** 권장 사항 (권장 사항 심각도 중간 위 권장 사항 hello 목록).

1. 제프 선택 **보안 연락처 세부 정보를 제공** hello에 **권장 사항을** hello 열리는 블레이드 **보안 연락처 세부 정보를 제공** 블레이드입니다.
2. 제프에 hello Azure 구독 tooprovide 연락처 정보를 선택합니다. 두 번째 **보안 연락처 세부 정보 제공** 블레이드가 열립니다.
   ![보안 연락처 세부 정보][6]
3. Hello에 두 번째 **보안 연락처 세부 정보를 제공** 블레이드에서 제프가 입력:

  - (없기 그 입력할 수 있는 전자 메일 주소 수는 제한 toohello) 쉼표로 구분 하 여 hello 보안 연락처 전자 메일 주소
  - 보안 연락처 전화 번호

4. 제프 hello 옵션으로 설정 하기도 **경고에 대 한 전자 메일을 내게 보내기** 심각도 높은 경고에 대 한 tooreceive 전자 메일입니다.
5. 제프 선택 **확인** tooapply hello 보안 정보 tooContoso 구독에 게 문의 하십시오.

제프 hello 낮은 우선 순위 추천을 검토 하는 마지막으로, **재구성 OS 취약점** 결정이 권장 사항은 적용할 수 없습니다. Toodismiss hello 권장 구성을 얻으려고 합니다. 제프 toohello 오른쪽을 다음 선택 나타나는 hello 세 점을 선택 **Dismiss**합니다.
   ![권장 사항 해제][7]

## <a name="conclusion"></a>결론
Security Center에서 권장 사항을 모니터링하면 공격이 발생하기 전에 보안 취약점을 제거할 수 있습니다. Security Center에서 보안 정책을 사용하여 보호를 구현하고 유지 관리하여 보안 인시던트를 방지할 수 있습니다.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
