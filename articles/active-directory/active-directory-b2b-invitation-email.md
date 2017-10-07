---
title: "hello Azure Active Directory B2B 공동 작업에 대 한 초대 전자 메일의 aaaThe 요소 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 초대 전자 메일 템플릿"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>hello B2B 공동 작업 초대 메일의 hello 요소

초대 메일 Azure ad에서 B2B 공동 작업 사용자도를 중요 한 구성 요소 toobring 파트너를 됩니다. 사용할 수 있습니다 tooincrease hello 받는 사람의 신뢰 합니다. 타당성이 및 소셜 증명 toohello 전자 메일을 추가할 수 있습니다, toomake 있는지 hello 받는 사람 선택 hello 익숙하지 느낌 **시작** tooaccept hello 초대 단추입니다. 이 트러스트 이므로 키 tooreduce 마찰을 공유 합니다. 고도 toomake hello 전자 메일 보기 좋은!

![Azure AD B2b 초대 전자 메일](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Hello 전자 메일 설명
살펴보겠습니다 hello 전자 메일의 몇 가지 요소는 최선의 방법 toouse의 기능을 확인할 수 있도록 합니다.

### <a name="subject"></a>제목
hello hello 전자 메일의 제목을 뒤에 오는 패턴 hello: 초대 toohello &lt;tenantname&gt; 조직

### <a name="from-address"></a>보낸 사람 주소
주소에서 hello에 대 한 LinkedIn 같은 패턴을 사용합니다.  하면 명확 해야 hello 초대자 이며 회사, 및도 명확히 hello 메일 Microsoft 전자 메일 주소에서 제공 되 게 합니다. hello 형식은: &lt;초대자의 표시 이름을&gt; 에서 &lt;tenantname&gt; (Microsoft)를 통해 <invites@microsoft.com&gt;

### <a name="reply-to"></a>회신
hello 회신 tooemail toohello 전자 메일에 전자 메일 백 toohello 초대자 보냅니다 회신할 수 있도록 사용 가능한 경우 toohello 초대자 전자 메일을 설정 됩니다.

### <a name="branding"></a>브랜딩
테 넌 트 로부터 전자 메일 브랜딩 하는 hello 회사를 사용 하는 hello 초대 수 설정한 테 넌 트에 대 한 합니다. 이 기능을 tootake 사용 하려는 경우 [여기](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) 방법에 대 한 hello 내용이 tooconfigure 것입니다. hello 배너 로고가 hello 전자 메일에 나타납니다. Hello 이미지 크기에 따라 및 품질 지침 [여기](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) 좋습니다. 또한 hello 회사 이름에에서도 표시 hello 호출 tooaction 합니다.

### <a name="call-tooaction"></a>Tooaction 호출
tooaction 두 부분으로 구성 하는 호출 hello: 이유 hello 받는 hello 메일을 어떤 hello 받는 항목에 대 한 toodo 요청 하는 설명 합니다.
- hello hello 패턴을 사용 하 여 "이유" 섹션을 해결할 수 있습니다: hello에 초대 된 tooaccess 응용 프로그램 확인 한 후 &lt;tenantname&gt; 조직

- "어떻게 되 고 묻는 toodo" 섹션의 hello hello 중일 경우에 표시 됩니다는 hello 및 **시작** 단추입니다. Hello 받는 사람 초대 hello 필요 없이 추가 된 경우이 단추 표시 되지 않습니다.

### <a name="inviters-information"></a>초대자에 대한 정보
hello 초대자 표시 이름 hello 전자 메일에 포함 됩니다. 등과 또한 프로필 사진을 Azure AD 계정에 대해 설정한 경우 전자 메일 초대 hello 됩니다도 해당 그림. 두 의도 한 tooincrease hello 전자 메일에 대 한 받는 사람의 신뢰성 됩니다.

프로필 사진 아직 설정 하지 않은, hello 그림 대신 hello 초대자 이니셜 있는 아이콘이 표시 됩니다.

  ![hello 초대자 이니셜을 표시합니다.](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>body
hello 메시지를 포함 하는 hello 본문 해당 hello 초대자 작성 또는 hello 초대 API 통해 전달 됩니다. 이것은 텍스트 영역에 불과하며, 보안상의 이유로 HTML 태그를 처리하지 않습니다.

### <a name="footer-section"></a>바닥글 섹션
hello 바닥글 hello Microsoft 회사 브랜드 있어서 hello 받는 발신에서 hello 전자 메일을 보냈습니다. 하는지 여부를 알 수 있습니다. 특수 사례:

- hello 초대자 테 넌 트를 초대 hello에 전자 메일 주소 없습니다

  ![그림 초대자 테 넌 트를 초대 hello에 ई म े 하지 않습니다.](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- hello 받는 tooredeem hello 초대 필요 하지 않습니다.

  ![받는 사람 tooredeem 초대 필요 하지 않은 경우](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법은 무엇입니까?](active-directory-b2b-admin-add-users.md)
* [정보 작업자가 B2B 공동 작업 사용자를 추가하는 방법은 무엇입니까?](active-directory-b2b-iw-add-users.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 공동 작업 라이선스](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 공동 작업 API 및 사용자 지정](active-directory-b2b-api.md)
* [B2B 공동 작업 사용자에 대한 다단계 인증](active-directory-b2b-mfa-instructions.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
