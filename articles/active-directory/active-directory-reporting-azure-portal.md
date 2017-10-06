---
title: Active Directory reporting aaaAzure | Microsoft Docs
description: "Azure Active Directory 보고에 대한 일반적 개요를 제공합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Azure Active Directory 보고

Azure Active Directory 보고 기능을 사용하면 환경이 작동하는 방법에 대한 정보를 얻을 수 있습니다.  
제공 된 hello 데이터를 수행할 수 있습니다.

- 사용자가 앱과 서비스를 활용하는 방식을 결정합니다.
- 사용자 환경의 hello 상태에 영향을 미치는 잠재적인 위험을 검색
- 사용자가 자신의 작업을 완료하지 못하게 하는 문제를 해결합니다.  

hello 보고 아키텍처는 두 가지 주요 사항에 의존합니다.

- 보안 보고서
- 작업 보고서

![보고](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>보안 보고서

Azure Active Directory에서 hello 보안 보고서는 조직의 identities tooprotect 있습니다를 유용합니다.  
Azure Active Directory에는 두 가지 유형의 보안 보고서가 있습니다.

- **위험에 대 한 플래그가 지정 된 사용자가** -hello에서 [위험 보안 보고서에 대 한 플래그가 지정 된 사용자](active-directory-reporting-security-user-at-risk.md), 손상 되었을 수 있는 사용자 계정의 개요를 얻게 됩니다.

- **위험한 로그인** -hello로 [위험한 로그인 보안 보고서](active-directory-reporting-security-risky-sign-ins.md), 장애가 있는 사용자에 의해 수행 된 로그인 시도 사용자 계정의 올바른 소유자를 하지 hello에 대 한 표시기를 가져옵니다. 

**어떤 Azure AD 라이선스가 tooaccess 보안 보고서 필요 한가요?**  
모든 Azure Active Directory 버전에서 위험 플래그가 지정된 사용자 보고서 및 위험한 로그인 보고서를 제공합니다.  
그러나 보고서 세분성 수준의 hello hello 버전 간에 달라 집니다. 

- Hello에 **Azure Active Directory Free 및 Basic edition**, 위험 및 위험한 로그인에 대 한 플래그가 지정 된 사용자 목록이 이미 얻게 됩니다. 

- hello **Azure Active Directory 프리미엄 1** edition 확장이 모델도 tooexamine를 사용 하 여 각 보고서에 대해 검색 된 위험 이벤트 원본으로 사용 하는 hello의 일부입니다. 

- hello **Azure Active Directory 프리미엄 2** 버전은 hello로 가장 자세한 위험 이벤트 원본으로 사용 하는 hello에 대 한 정보 및이 통해 있습니다 tooconfigured 자동으로 응답 하는 tooconfigure 보안 정책 제공 위험 수준입니다.


## <a name="activity-reports"></a>작업 보고서

Azure Active Directory에는 두 가지 유형의 활동 보고서가 있습니다.

- **감사 로그** -hello [감사 로그를 작업 보고서](active-directory-reporting-activity-audit-logs.md) 테 넌 트에 수행 된 모든 태스크의 toohello 기록을 액세스를 제공 합니다.

- **로그인** -hello로 [로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)를 확인할 수 있습니다, hello 감사 로그 보고서에서 보고 하는 hello 작업을 수행한 사용자입니다.



hello **감사 로그 보고서** 규정 준수 위한 레코드 시스템 작업을 제공 합니다.
다른 사용자에 게 적절 한 hello 데이터 사용 하면 tooaddress 일반적인 시나리오와 같은 제공.

- 다른 사용자가 내 테 넌 트에 액세스 tooan 관리 그룹을 가져왔습니다. 이들에게 액세스 권한을 부여한 사람을 알고 싶습니다. 

- 특정 앱에 로그인 하는 사용자의 tooknow hello 목록을 원하는 I 이후 최근에 등록 된 응용 프로그램 hello 및 tooknow 잘 수행 하는 경우

- 내 테 넌 트에 tooknow 개수 암호 재설정 발생 하 고 원합니다


**어떤 Azure AD 라이선스가 tooaccess hello 감사 로그 보고서 필요 한가요?**  
라이선스를 보유 하는 기능에 대 한 감사 로그 보고서 hello ´ ù. 특정 기능에 대 한 라이선스가 있는 경우 액세스 toohello 감사에 대 한 로그 정보를 갖게 됩니다.

자세한 내용은 참조 하십시오. **hello Free, Basic 및 Premium 버전의 일반적으로 사용할 수 있는 기능을 비교** 에 [Azure Active Directory 기능 및 특성](https://www.microsoft.com/cloud-platform/azure-active-directory-features)합니다.   



hello **로그인 활동 보고서** 활성화 tootoofind tooquestions에 같은 응답:

- 사용자의 hello 로그인 패턴 이란?
- 한 주 동안 얼마나 많은 사용자가 로그인했나요?
- 이러한 로그인의 hello 상태는 무엇입니까?


**하는 어떤 Azure AD 라이선스가 필요 tooaccess 로그인 활동 보고서 hello?**  
tooaccess hello 로그인 활동 보고서, 테 넌 트에 연결 된 Azure AD Premium 라이선스가 있어야 합니다.


## <a name="programmatic-access"></a>프로그래밍 방식 액세스

또한 toohello 사용자 인터페이스에서 Azure Active Directory reporting 또한 제공 된 [프로그래밍 방식 액세스](active-directory-reporting-api-getting-started-azure-portal.md) toohello 데이터를 보고 합니다. 이러한 보고서의 hello 데이터 SIEM 시스템, 감사, 비즈니스 인텔리전스 도구 등 매우 유용한 tooyour 응용 프로그램을 수 있습니다. hello Azure AD reporting Api는 REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다. 다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다. 


## <a name="next-steps"></a>다음 단계

Azure Active Directory의 다양 한 보고서 유형의 tooknow hello에 대 한 자세한 하려는 경우 참조:

- [위험 플래그가 지정된 사용자 보고서](active-directory-reporting-security-user-at-risk.md)
- [위험한 로그인 보고서](active-directory-reporting-security-risky-sign-ins.md)
- [감사 로그 보고서](active-directory-reporting-activity-audit-logs.md)
- [로그인 로그 보고서](active-directory-reporting-activity-sign-ins.md)

Hello 보고 API를 사용 하 여 데이터를 보고 하는 hello hello에 액세스 하는 방법에 대 한 자세한 tooknow, 참조: 

- [Azure Active Directory 보고 API hello 시작](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png