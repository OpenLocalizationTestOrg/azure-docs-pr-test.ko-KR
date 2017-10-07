---
title: "Azure AD 응용 프로그램 프록시에 aaaCustom 도메인 | Microsoft Docs"
description: "Hello 앱에 대 한 해당 hello URL은 동일한 사용자가 액세스 하는 것에 관계 없이 hello Azure AD 응용 프로그램 프록시에 사용자 지정 도메인을 관리 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업

Azure Active Directory 응용 프로그램 프록시를 통해 응용 프로그램을 게시 하면 원격으로 작업 하는 사용자가 toogo toowhen 프로그램에 대 한 외부 URL을 만듭니다. 이 URL 가져옵니다 hello 기본 도메인 *yourtenant.msappproxy.net*합니다. 예를 들어 게시 한 경우 응용 프로그램 이라는 비용 및 테 넌 트, Contoso 라는 있으면 hello 외부 URL 합니다 https://expenses-contoso.msappproxy.net 합니다. 자신의 도메인 이름을 toouse을 원하는 경우 응용 프로그램에 대 한 사용자 지정 도메인을 구성 합니다. 

언제나 가능한 응용 프로그램에 대한 사용자 지정 도메인을 설정하는 것이 좋습니다. 사용자 지정 도메인의 hello 이점 중 일부는 다음과 같습니다.

- 사용자가 toohello 응용 프로그램을 가져올 수 내부 또는 외부 네트워크에서 근무 하는 동일한 URL을 hello 합니다.
- 동일한 내부 및 외부 Url hello는의 모든 응용 프로그램, tooanother 가리키는 한 응용 프로그램에서 링크 hello 회사 네트워크 외부 에서도 toowork를 계속 합니다. 
- 브랜딩, 제어 및 원하는 hello Url을 만듭니다. 


## <a name="configure-a-custom-domain"></a>사용자 지정 도메인 구성

### <a name="prerequisites"></a>필수 조건

사용자 지정 도메인을 구성 하기 전에 hello 준비 하는 요구 사항을 준수 했는지 확인 합니다. 
- A [확인 된 도메인이 추가 Active Directory tooAzure](active-directory-domains-add-azure-portal.md)합니다.
- PFX 파일의 hello 형태로 hello 도메인에 대 한 사용자 지정 인증서입니다. 
- [응용 프로그램 프록시를 통해 게시된](application-proxy-publish-azure-portal.md) 온-프레미스 앱.

### <a name="configure-your-custom-domain"></a>사용자 지정 도메인 구성

이러한 세 가지 요구 사항을 준비 해야 하는 경우 이러한 단계 tooset을 사용자 지정 도메인을 따르십시오.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 너무 이동**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** hello 응용 프로그램을 선택 하 고 원하는 toomanage 합니다.
3. **응용 프로그램 프록시**를 선택합니다. 
4. Hello 외부 URL 필드에 hello 드롭다운 목록 tooselect 사용자 지정 도메인을 사용 합니다. Hello 목록에서 도메인을 보이지 않으면 다음 그 아직 확인 되지 않은 합니다. 
5. **저장**을 선택합니다.
5. hello **인증서** 사용할 수 없는 필드에 사용할 수 있게 됩니다. 이 필드를 선택합니다. 

   ![Tooupload 인증서를 클릭 합니다.](./media/active-directory-application-proxy-custom-domains/certificate.png)

   아직이 도메인에 대 한 인증서를 업로드 하는 경우 hello 인증서 필드 hello 인증서 정보를 표시 합니다. 

6. Hello PFX 인증서를 업로드 하 고 hello 인증서에 대 한 hello 암호를 입력 합니다. 
7. 선택 **저장** toosave 변경 내용을 합니다. 
8. 추가 [DNS 레코드](../dns/dns-operations-recordsets-portal.md) 리디렉션을 새 외부 URL toohello msappproxy.net 도메인 hello 하 합니다. 

>[!TIP] 
>사용자 지정 도메인당 하나의 인증서 tooupload 하기만 하면 됩니다. 인증서를 업로드 한 후 새 응용 프로그램을 게시 하 고 hello DNS 레코드를 제외 하 고 추가 구성이 toodo hello 사용자 지정 도메인을 선택할 수 있습니다. 

## <a name="manage-certificates"></a>인증서 관리

### <a name="certificate-format"></a>인증서 형식
Hello 인증서 서명 방법에 대 한 제한은 없습니다. ECC(타원 곡선암호화), SAN(주체 대체 이름 ) 및 다른 일반적인 인증서 형식은 모두 지원됩니다. 

Hello 와일드 카드 원하는 hello 외부 URL과 일치으로 와일드 카드 인증서를 사용할 수 있습니다. 

자체 서명된 인증서도 사용할 수 있습니다. 개인 인증 기관을 사용 하는 hello CDP (인증서 해지 지점 배포 지점) hello 인증서에 대 한 공용 이어야 합니다.

### <a name="changing-hello-domain"></a>Hello 도메인 변경
모든 확인 된 도메인 응용 프로그램에 대 한 hello 외부 URL 드롭다운 목록에 나타납니다. toochange hello 도메인, hello 응용 프로그램에 대 한 필드를 업데이트 합니다. Hello 도메인 hello 목록에 없으면 [확인 된 도메인으로 추가](active-directory-domains-add-azure-portal.md)합니다. 에 연결 된 인증서가 아직 없는 도메인을 선택 하는 경우 tooadd hello 인증서를 5-7 단계를 따릅니다. 그런 다음 hello 새 외부 URL에서 DNS 레코드 tooredirect hello를 업데이트 해야 합니다. 

### <a name="certificate-management"></a>인증서 관리
Hello hello 응용 프로그램 외부 호스트를 공유 하지 않는 한 여러 응용 프로그램에 대 한 동일한 인증서를 사용할 수 있습니다. 

경고가 나타나면 인증서가 만료 되 면 tooupload 알리는 hello 포털을 통해 다른 인증서입니다. Hello 인증서가 해지 되는 경우 hello 응용 프로그램에 액세스할 때 보안 경고를 볼 수 있습니다. 인증서에 대한 해지 검사를 수행하지 않습니다.  지정된 된 응용 프로그램에 대 한 tooupdate hello 인증서 toohello 응용 프로그램을 탐색 하 고 게시 된 응용 프로그램 tooupload 새 인증서에 사용자 지정 도메인 구성에 대 한 5-7 단계를 수행 합니다. Hello 이전 인증서는 다른 응용 프로그램에서 사용 되 고 하지 않으면, 자동으로 삭제 됩니다. 

현재 모든 인증서 관리 이므로 개별 응용 프로그램 페이지를 통해 hello 관련 응용 프로그램의 hello 컨텍스트에서 toomanage 인증서가 필요 합니다. 

## <a name="next-steps"></a>다음 단계
* [Single sign-on 사용](active-directory-application-proxy-sso-using-kcd.md) tooyour Azure AD 인증을 사용 하 여 앱을 게시 합니다.
* [조건부 액세스를 사용](active-directory-application-proxy-conditional-access.md) tooyour 게시 된 앱입니다.
* [사용자 지정 도메인 이름을 tooAzure AD 추가](active-directory-domains-add-azure-portal.md)


