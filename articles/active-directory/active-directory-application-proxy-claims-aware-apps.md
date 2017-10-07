---
title: "aaaClaims 인식 앱-Azure AD 응용 프로그램 프록시 | Microsoft Docs"
description: "어떻게 toopublish 온-프레미스 ASP.NET 응용 프로그램에 대 한 보안 원격 액세스 사용자가 ADFS 클레임을 수락 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>응용 프로그램 프록시에서 클레임 인식 앱으로 작업
[클레임 인식 응용 프로그램](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) 리디렉션 toohello 보안 토큰 서비스 (STS)를 수행 합니다. hello STS 토큰의 교환으로 hello 사용자 로부터 자격 증명을 요청 하 고 hello 사용자 toohello 응용 프로그램을 리디렉션합니다. 몇 가지 방법으로 tooenable 응용 프로그램 프록시 이러한 리디렉션은 toowork 가지가 있습니다. 클레임 인식 응용 프로그램에 대 한이 문서 tooconfigure 배포를 사용 합니다. 

## <a name="prerequisites"></a>필수 조건
클레임 인식 응용 프로그램 hello 해당 hello STS 리디렉션합니다 toois 온-프레미스 네트워크 외부에서 사용할 수 있는지 확인 합니다. 있습니다 수 hello STS 또는 사용할 수 있도록 프록시를 통해 노출 하 여 외부 연결을 허용 하 여 합니다. 

## <a name="publish-your-application"></a>응용 프로그램 게시

1. 에 설명 된 toohello 지침에 따라 응용 프로그램을 게시 [응용 프로그램 프록시는 응용 프로그램 게시](application-proxy-publish-azure-portal.md)합니다.
2. Hello 선택 하 고 포털의 응용 프로그램 페이지 toohello 이동 **Single sign on**합니다.
3. **Azure Active Directory**를 **사전 인증 방법**으로 선택했다면 **Azure AD Single Sign-On 비활성화**를 **내부 인증 방법**으로 선택합니다. 선택한 경우 **통과** 으로 프로그램 **사전 인증 방법**, toochange 어느 것에 필요 하지 않습니다.

## <a name="configure-adfs"></a>ADFS 구성

두 가지 방법 중 하나에서 클레임 인식 앱에 대한 ADFS를 구성할 수 있습니다. 사용자 지정 도메인을 사용 하 여 hello 먼저가 있습니다. Ws-federation과 hello 둘째 됩니다. 

### <a name="option-1-custom-domains"></a>옵션 1: 사용자 지정 도메인

응용 프로그램은 정규화 된 내부 Url hello 모든 경우 도메인 이름 (Fqdn) 다음을 구성할 수 있습니다 [사용자 지정 도메인](active-directory-application-proxy-custom-domains.md) 응용 프로그램에 대 한 합니다. 사용 하 여 hello 사용자 지정 도메인 toocreate 있는 외부 Url 내부 Url hello와 동일 하 게 hello 됩니다. 외부 Url 내부 Url이 일치 하는 경우 사용자가 온-프레미스 또는 원격 인지 관계 없이 hello STS 리디렉션이 작동 합니다. 

### <a name="option-2-ws-federation"></a>옵션 2: WS-Federation

1. ADFS 관리를 엽니다.
2. 너무 이동**신뢰 당사자 트러스트**응용 프로그램 프록시 게시 하는 hello 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.  

   ![신뢰 당사자 트러스트 앱 이름을 마우스 오른쪽 단추로 클릭 - 스크린샷](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. Hello에 **끝점** 탭의 **끝점 유형이**선택, **WS-페더레이션**합니다.
4. **신뢰할 수 있는 URL**에서 응용 프로그램 프록시 hello에 입력 하는 hello URL 입력 **외부 URL** 클릭 **확인**합니다.  

   ![끝점 추가 - 신뢰할 수 있는 URL 값 설정 - 스크린샷](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>다음 단계
* 클레임 인식이 아닌 응용 프로그램에 대한 [Single Sign-On 사용](application-proxy-sso-overview.md)
* [네이티브 클라이언트 앱 toointeract 프록시 응용 프로그램을 사용 하도록 설정](active-directory-application-proxy-native-client.md)


