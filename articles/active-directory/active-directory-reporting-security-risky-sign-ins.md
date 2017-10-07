---
title: "hello Azure Active Directory 포털에서 aaaRisky 로그인 보고서 | Microsoft Docs"
description: "Hello Azure Active Directory 포털에서 hello 위험한 로그인 보고서에 알아보기"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory 포털에서 위험한 로그인 보고서

Azure Active Directory (Azure AD)에 hello 보안 보고서와 함께 환경에서 손상 된 사용자 계정의 hello 확률에 대 한 정보를 얻을 수 있습니다. 

Azure AD 사용자 계정이 관련된 tooyour 의심 스러운 동작을 검색 합니다. 작업이 감지된 경우 *위험 이벤트*라는 레코드가 만들어집니다. 자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요. 

hello 위험 이벤트는 사용 되는 toocalculate 감지 함:

- **위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다. 자세한 내용은 [위험한 로그인](active-directory-identityprotection.md#risky-sign-ins)을 참조하세요. 

- **위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다. 자세한 내용은 [위험 플래그가 지정된 사용자](active-directory-identityprotection.md#users-flagged-for-risk)를 참조하세요.  

[Azure 포털 hello](https://portal.azure.com), hello 보안 hello에 보고서를 찾을 수 있습니다 **Azure Active Directory** hello 블레이드 **보안** 섹션. 

![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>어떤 Azure AD 라이선스가 tooaccess 보안 보고서 필요 한가요?  

모든 Azure Active Directory 버전에서 위험한 로그인 보고서를 제공합니다.  
그러나 보고서 세분성 수준의 hello hello 버전 간에 달라 집니다. 

- Hello에 **Azure Active Directory Free 및 Basic edition**, 이미 위험한 로그인 목록을 가져옵니다. 

- hello **Azure Active Directory 프리미엄 1** edition 확장이 모델도 tooexamine를 사용 하 여 각 보고서에 대해 검색 된 위험 이벤트 원본으로 사용 하는 hello의 일부입니다. 

- hello **Azure Active Directory 프리미엄 2** 버전은 hello로 가장 자세한 정보에 대 한 모든 기본 위험 이벤트 및이 통해 있습니다 tooconfigured 자동으로 응답 하는 tooconfigure 보안 정책 제공 위험 수준입니다.



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory 무료 및 기본 버전

hello Azure Active Directory free 및 basic edition 제공 위험한 로그인 검색 된 목록이 사용자에 대 한 합니다. 이 보고서는 다음을 표시합니다.

- **사용자** -hello hello 로그인 작업 중 사용 된 hello 사용자의 이름
- **IP** -hello hello 장치를 사용 하는 tooconnect tooAzure Active Directory의 IP 주소
- **위치** -tooconnect tooAzure Active Directory를 사용 하는 hello 위치
- **로그인 시간** -때 hello 로그인 수행한 hello 시간
- **상태** -hello hello에 대 한 로그인의 상태


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Hello 위험한 로그인 조사에 따르면 피드백 tooAzure Active Directory에서 작업을 수행 하는 hello의 형태로 제공할 수 있습니다.

- 해결
- 가양성으로 표시
- 무시
- 다시 활성화

![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/21.png)

자세한 내용은 [수동으로 위험 이벤트 닫기](active-directory-identityprotection.md#closing-risk-events-manually)를 참조하세요.

이 보고서는 다음과 같은 옵션을 제공합니다.

- 리소스 검색
- Hello 보고서 데이터를 다운로드 합니다.


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory Premium Edition

hello Azure Active Directory premium edition에서 hello 위험한 로그인 보고서를 제공 하는 합니다.

- Hello에 대 한 정보를 집계 [이벤트 유형을 위험](active-directory-identity-protection-risk-events.md) 검색

- 옵션 toodownload hello 보고서


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/456.png)


위험 이벤트를 선택하면 위험 이벤트에 대한 자세한 보고서 보기가 제공되고 다음과 같은 작업이 가능합니다.

- 옵션 tooconfigure는 [사용자 위험 관리 정책](active-directory-identityprotection.md#user-risk-security-policy)  

- Hello 위험 이벤트에 대 한 hello 검색 시간 표시 막대 검토  

- 이 이벤트가 감지된 사용자 목록 검토

- [위험 이벤트를 수동으로 닫거나](active-directory-identityprotection.md#closing-risk-events-manually) 수동으로 닫은 위험 이벤트를 다시 활성화 


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/457.png)

사용자를 선택하면 사용자에 대한 자세한 보고서 보기가 제공되고 다음과 같은 작업이 가능합니다.

- 열기 hello 로그인 기능을 모두 보려면

- Hello 사용자의 암호를 다시 설정

- 모든 이벤트 해제

- Hello 사용자에 대 한 보고 된 위험 이벤트를 조사 합니다. 


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/324.png)


위험 이벤트 tooinvestigate hello 목록에서 선택 합니다.  
Hello 열립니다 **세부 정보** 블레이드가 위험 이벤트에 대 한 합니다. Hello에 **세부 정보** 블레이드에서 hello 옵션 tooeither 있는 [위험 상황을 수동으로 닫고](active-directory-identityprotection.md#closing-risk-events-manually) 또는 수동으로 닫힌된 위험 이벤트를 다시 활성화 합니다. 


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>다음 단계

- Azure Active Directory ID 보호에 대한 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.

