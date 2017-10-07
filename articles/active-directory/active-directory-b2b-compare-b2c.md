---
title: "aaaCompare B2B 공동 작업 및 Azure Active directory에서 B2C | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 및 Azure AD B2C hello 차이 무엇입니까?"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Azure Active Directory에서 B2B 공동 작업과 B2C 비교

Azure Active Directory (Azure AD) B2B 공동 작업 및 Azure AD B2C 모두 사용 하면 toowork 외부 사용자와 Azure AD에 있습니다. 하지만 어떻게 비교할 수 있나요?


B2B 공동 작업 기능 |     Azure AD B2C 독립 실행형 제품
-------- | --------
위한: toobe 수 tooauthenticate 사용자가 id 공급자에 관계 없이 파트너 조직에서 하려는 조직은 합니다. | 대상: 개인이든, 기관이든, 조직이든 상관없이 모바일 및 웹앱 고객을 Azure AD에 초대하려는 사용자
지원되는 ID: 회사 또는 학교 계정이 있는 직원, 회사 또는 학교 계정이 있는 파트너 또는 모든 전자 메일 주소입니다. 곧 toosupport 직접 페더레이션 합니다.  | 지원되는 ID: 로컬 응용 프로그램 계정(모든 전자 메일 주소 또는 사용자 이름)이 있는 소비자 사용자 또는 직접 페더레이션이 포함된 지원되는 소셜 ID입니다.
Hello 파트너 사용자 디렉터리에 있는: hello 외부 조직의 사용자에서 관리 되는 파트너 hello 주석이 추가 된 하지만 직원와 동일한 디렉터리 특별 하 게 합니다. 자격 증명은 관리 hello 동일한 직원으로 방식으로 추가 된 toohello 동일한 그룹 및 수 등  | 에 디렉터리 hello 고객 사용자 엔터티는 어떤: hello 응용 프로그램 디렉터리에 있습니다. Hello 조직의 직원 및 파트너 디렉터리 (해당 되는 경우에서 별도로 관리.
Single sign-on (SSO) tooall Azure AD에 연결 된 앱은 지원 됩니다. 예를 들어 액세스 tooOffice 365 또는 온-프레미스 앱 및 Salesforce 또는 Workday 같은 tooother SaaS 앱을 제공할 수 있습니다.  |  SSO toocustomer hello Azure AD B2C 테 넌 트 내에서 앱은 지원 되는 소유 합니다. SSO tooOffice 365 tooother Microsoft 및 타사 SaaS 응용 프로그램 지원 되지 않습니다.
파트너 수명 주기: hello 호스트/초대 조직에서 관리 합니다.  | 고객 수명 주기: 셀프 서비스 또는 hello 응용 프로그램에 의해 관리 되는 합니다.
보안 정책 및 규정 준수: hello 호스트/초대 조직에서 관리 합니다.  | 보안 정책 및 규정 준수: hello 응용 프로그램으로 관리 합니다.
브랜딩: 호스트/초대한 조직의 브랜드가 사용됩니다.  |    브랜딩: 응용 프로그램에 의해 관리됩니다. 일반적으로 제품이 나 hello 배경으로 hello 조직 페이드 toobe 제품을 경향이 있습니다.
추가 정보: [블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [설명서](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | 추가 정보: [제품 페이지](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [설명서](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업용 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
* [B2B 공동 작업에 대한 지원 받기](active-directory-b2b-support.md)
