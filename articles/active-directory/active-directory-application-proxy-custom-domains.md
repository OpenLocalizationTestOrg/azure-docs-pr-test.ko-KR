---
title: "Azure AD 응용 프로그램 프록시의 사용자 지정 도메인 | Microsoft Docs"
description: "앱의 URL이 사용자가 액세스하는 위치에 관계 없이 동일하도록 Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인을 관리합니다."
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
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업

Azure Active Directory 응용 프로그램 프록시를 통해 응용 프로그램을 게시할 때 사용자가 원격으로 작업 중일 때 이동하도록 외부 URL을 만듭니다. 이 URL은 기본 도메인 *yourtenant.msappproxy.net*을 가져옵니다. 예를 들어 Expenses라는 앱을 게시한 경우 테넌트는 Contoso로 이름이 지정된 다음 외부 URL은 https://expenses-contoso.msappproxy.net이 됩니다. 자신의 도메인 이름을 사용하려는 경우 응용 프로그램에 대한 사용자 지정 도메인을 구성합니다. 

언제나 가능한 응용 프로그램에 대한 사용자 지정 도메인을 설정하는 것이 좋습니다. 사용자 지정 도메인의 이점 중 일부는 다음과 같습니다.

- 사용자가 네트워크 내부 또는 외부에서 근무하든지 동일한 URL을 사용하여 응용 프로그램에 접근할 수 있습니다.
- 모든 응용 프로그램이 동일한 내부 및 외부 URL을 갖는 경우 다른 응용 프로그램을 가리키는 하나의 응용 프로그램의 링크는 회사 네트워크 외부에서도 계속해서 작동합니다. 
- 브랜딩을 제어하고 원하는 URL을 만듭니다. 


## <a name="configure-a-custom-domain"></a>사용자 지정 도메인 구성

### <a name="prerequisites"></a>필수 조건

사용자 지정 도메인을 구성하기 전에 다음 요구 사항이 준비되어 있는지 확인합니다. 
- [Azure Active Directory에 추가된 확인된 도메인](active-directory-domains-add-azure-portal.md).
- PFX 파일 형태의 도메인에 대한 사용자 지정 인증서. 
- [응용 프로그램 프록시를 통해 게시된](application-proxy-publish-azure-portal.md) 온-프레미스 앱.

### <a name="configure-your-custom-domain"></a>사용자 지정 도메인 구성

이러한 세 가지 요구 사항을 준비한 경우 다음 단계를 따라 사용자 지정 도메인을 설정합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.
2. **Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램**으로 이동하고 관리하려는 앱을 선택합니다.
3. **응용 프로그램 프록시**를 선택합니다. 
4. 외부 URL 필드에서 드롭다운 목록을 사용하여 사용자 지정 도메인을 선택합니다. 목록에서 도메인이 보이지 않는 경우 아직 확인되지 않은 것입니다. 
5. **저장**을 선택합니다.
5. 비활성화되었던 **인증서** 필드가 활성화됩니다. 이 필드를 선택합니다. 

   ![인증서를 업로드하려면 클릭](./media/active-directory-application-proxy-custom-domains/certificate.png)

   이 도메인에 대한 인증서를 이미 업로드한 경우 인증서 필드에는 인증서 정보가 표시됩니다. 

6. PFX 인증서를 업로드하고 인증서의 암호를 입력합니다. 
7. **저장**을 선택하여 변경 내용을 저장합니다. 
8. msappproxy.net 도메인에 새 외부 URL을 리디렉션하는 [DNS 레코드](../dns/dns-operations-recordsets-portal.md)를 추가합니다. 

>[!TIP] 
>사용자 지정 도메인당 하나의 인증서를 업로드하기만 하면 됩니다. 인증서를 업로드한 후 새 앱을 게시하고 DNS 레코드를 제외하고 추가 구성을 수행할 필요가 없는 경우 사용자 지정 도메인을 선택할 수 있습니다. 

## <a name="manage-certificates"></a>인증서 관리

### <a name="certificate-format"></a>인증서 형식
인증서 서명 메서드에 대한 제한은 없습니다. ECC(타원 곡선암호화), SAN(주체 대체 이름 ) 및 다른 일반적인 인증서 형식은 모두 지원됩니다. 

와일드카드가 원하는 외부 URL과 일치하는 한 와일드카드 인증서를 사용할 수 있습니다. 

자체 서명된 인증서도 사용할 수 있습니다. 개인 인증 기관을 사용하는 경우 인증서에 대한 CDP(인증서 해지 지점 배포 지점)는 공용이어야 합니다.

### <a name="changing-the-domain"></a>도메인 변경
모든 확인된 도메인은 응용 프로그램에 대한 외부 URL 드롭다운 목록에 나타납니다. 도메인을 변경하려면 응용 프로그램에 대한 해당 필드를 업데이트합니다. 원하는 도메인이 목록에 없는 경우 [확인된 도메인으로 추가](active-directory-domains-add-azure-portal.md)합니다. 연결된 인증서가 없는 도메인을 선택하는 경우 5-7단계를 수행하여 인증서를 추가합니다. 그런 다음 새 외부 URL에서 리디렉션할 DNS 레코드를 업데이트해야 합니다. 

### <a name="certificate-management"></a>인증서 관리
응용 프로그램이 외부 호스트를 공유하지 않는 한 여러 응용 프로그램에 대해 동일한 인증서를 사용할 수 있습니다. 

인증서가 만료되면 포털을 통해 다른 인증서를 업로드하라는 경고를 받습니다. 인증서가 해지되면 응용 프로그램에 액세스할 때 보안 경고를 볼 수 있습니다. 인증서에 대한 해지 검사를 수행하지 않습니다.  지정된 응용 프로그램에 대한 인증서를 업데이트하려면 응용 프로그램으로 이동하고 게시된 응용 프로그램에 사용자 지정 도메인 구성에 대한 5-7단계를 수행하여 새 인증서를 업로드합니다. 이전 인증서가 다른 응용 프로그램에서 사용되고 있지 않으면 자동으로 삭제됩니다. 

현재 모든 인증서 관리는 개별 응용 프로그램 페이지를 통하므로 관련 응용 프로그램의 컨텍스트에서 인증서를 관리해야 합니다. 

## <a name="next-steps"></a>다음 단계
* Azure AD 인증을 사용하여 게시된 앱에 대해 [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
* 게시된 앱에 대해 [조건부 액세스 사용](active-directory-application-proxy-conditional-access.md)
* [Azure AD에 사용자 지정 도메인 이름 추가](active-directory-domains-add-azure-portal.md)


