---
title: "Azure Active Directory B2B 공동 작업에 대 한 등록 포털 aaaSelf 서비스 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 비즈니스 파트너 tooselectively 액세스 회사 응용 프로그램을 사용 하 여 회사 간 관계 지원"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Azure AD B2B 공동 작업 등록을 위한 셀프 서비스 포털

고객 많은 hello 우리의 IT 관리자를 통해 노출 되는 기본 제공 기능으로 작업을 수행할 수 [Azure 포털](https://portal.azure.com) 및 [응용 프로그램 액세스 패널로](https://myapps.microsoft.com) 최종 사용자에 대 한 합니다. 하지만 된 기업 할 toocustomize hello 온 보 딩 워크플로 B2B 사용자 toofit에 대 한 조직의 요구 됩니다. 이러한 작업은 [API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)를 통해 수행할 수 있습니다.

고객들과 이러한 점을 논의하면서 일반적인 요구가 있다는 것을 알게 되었습니다. 조직 초대 hello 모를 수 hello가 미리 개별 외부 공동 작업자 tootheir 리소스에 액세스 해야 하는 합니다. 파트너 회사에서 사용자가 너무 자체에 등록 정책 집합이 조직 컨트롤 초대 해당 hello에 대 한 방식으로 원했습니다. 이 시나리오는 API를 통해 구현될 수 있습니다. 따라서 이러한 작업을 수행하는 [샘플 Github 프로젝트](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web)를 GItHub에 게시했습니다.

Github 프로젝트 진행는 방법을 보여 주는 조직 수 Api를 사용 하 여 액세스할 수 있는 hello 응용 프로그램을 결정 하는 규칙으로 신뢰할 수 있는 해당 파트너에 대 한 정책 기반, 셀프 서비스 등록 기능을 제공 합니다. 필요할 때, 안전 하 게 hello 초대 조직 toomanually 등록할 필요 없이 파트너 사용자 액세스 tooresources를 얻을 수 있습니다 이러한. 선택한 Azure 구독에 hello 프로젝트를 쉽게 배포할 수 있습니다.

## <a name="as-is-code"></a>원본 코드

이 코드 샘플 toodemonstrate hello Azure Active Directory B2B 초대 API의 사용으로 사용할 수 있는지를 기억 합니다. 따라서 개발 팀 또는 파트너가 코드를 사용자 지정해야 하고 프로덕션 시나리오에서 배포하기 전에 검토해야 합니다.

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:
* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-admin-add-users.md)
* [정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-iw-add-users.md)
* [hello B2B 공동 작업 초대 메일의 hello 요소](active-directory-b2b-invitation-email.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 공동 작업 라이선스](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)](active-directory-b2b-faq.md)
* [B2B 공동 작업 사용자에 대한 다단계 인증](active-directory-b2b-mfa-instructions.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)