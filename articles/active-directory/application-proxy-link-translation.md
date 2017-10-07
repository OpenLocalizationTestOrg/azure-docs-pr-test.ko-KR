---
title: "aaaTranslate 링크와 Azure AD 응용 프로그램 프록시 Url | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대 한 hello 기본 사항에 설명합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Azure AD 응용 프로그램 프록시를 사용하여 게시된 앱에 대해 하드 코드된 링크 리디렉션

Azure AD 응용 프로그램 프록시는 원격 장애가 있거나가 자신의 장치에서 온-프레미스 앱 사용 가능한 toousers를 프로그램을 만듭니다. 그러나 일부 응용 프로그램 hello HTML에에서 포함 된 로컬 링크와 함께 개발 되었습니다. 이러한 링크는 hello 응용 프로그램을 원격으로 사용할 때 제대로 작동 하지 않습니다. 여러 온-프레미스 응용 프로그램 지점 tooeach 다른을 사용 하는 경우 사용자가 hello 링크 tookeep hello에 있지 않는 경우 작업을 예상 합니다. 

hello 가장 좋은 방법은 toomake 완료 되었는지 링크 작업 동일한 내부 hello 회사 네트워크 외부에 tooconfigure hello 앱 toobe의 외부 Url을 hello 내부 사이트의 Url로 동일 합니다. 사용 하 여 [사용자 지정 도메인](active-directory-application-proxy-custom-domains.md) tooconfigure hello 기본 응용 프로그램 프록시 도메인이 아닌 회사 도메인 이름을 지정 하 여 외부 Url toohave 합니다.

테 넌 트의 사용자 지정 도메인을 사용할 수 없다면, 응용 프로그램 프록시 링크 변환 기능은 hello 위해 사용자에 관계 없이 작업 링크를 유지 합니다. 직접 매핑할 수 있습니다 toointernal 종단점 또는 포트를 가리키는 응용 프로그램이 있는 경우 이러한 내부 Url toohello 외부 응용 프로그램 프록시 Url을 게시 합니다. 링크 변환을 사용하는 경우 응용 프로그램 프록시는 HTML, CSS를 통해 검색하고 게시되는 내부 링크에 대해 JavaScript 태그를 선택합니다. 그런 다음 응용 프로그램 프록시 서비스 hello 변환 사용자가 중단 없이 환경을 얻을 수 있도록 합니다.

>[!NOTE]
>hello 링크 변환 기능을 테 넌 트에 사용자 지정 도메인을 사용할 수 없습니다 어떤 이유 때문에 대 한 toohave hello가 앱에 대 한 동일한 내부 및 외부 Url입니다. 이 기능을 사용하도록 설정하기 전에 [Azure AD 응용 프로그램 프록시의 사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)이 작동하는지 확인하세요.
>
>SharePoint tooconfigure 링크 변환 사용 해야 하는 hello 응용 프로그램을 사용 하는 경우 참조 또는 [SharePoint 2013에 대 한 대체 액세스 매핑 구성](https://technet.microsoft.com/library/cc263208.aspx) 또 다른 방법은 toomapping 링크에 대 한 합니다.

## <a name="how-link-translation-works"></a>링크 변환의 작동 방식

인증을 받은 후 프록시 서버 hello 전달 hello 응용 프로그램 데이터 toohello 사용자 응용 프로그램 프록시 하드 코드 된 링크에 대 한 hello 응용 프로그램 검색과 해당으로 바꿉니다 외부 Url을 게시.

응용 프로그램 프록시는 응용 프로그램이 UTF-8에서 인코딩되는 것으로 가정합니다. 않은 hello 경우, hello 인코딩 유형을 지정 http 응답 헤더에 같은 `Content-Type:text/html;charset=utf-8`합니다.

### <a name="which-links-are-affected"></a>영향을 받는 링크

hello 링크 변환 기능은 응용 프로그램의 hello 본문에 코드 태그에 있는 링크에 대해서만 찾습니다. 응용 프로그램 프록시에는 헤더에서 쿠키 또는 URL을 변환하는 별도의 기능이 있습니다. 

온-프레미스 응용 프로그램에는 두 가지 일반적인 유형의 내부 링크가 있습니다.

- **내부 링크 상대** 해당 지점 tooa 공유 리소스와 같은 로컬 파일 구조에서 `/claims/claims.html`합니다. 이러한 링크는 자동으로 응용 프로그램 프록시를 통해 게시 하 고 toowork 또는 링크 변환 하지 않고 계속 하는 앱에서 작동 합니다. 
- **하드 코드 된 내부 링크** tooother 온-프레미스와 같은 앱 `http://expenses` 게시 된 같은 파일 또는 `http://expenses/logo.jpg`합니다. hello 링크 변환 기능은 하드 코드 된 내부 링크를 작동 하 고 원격 사용자가 통해 toogo 필요한 toopoint toohello 외부 Url을 변경 합니다.

### <a name="how-do-apps-link-tooeach-other"></a>앱 tooeach 다른 연결 방법

링크 변환 hello 앱 별 수준에서 게 hello 사용자 환경 제어할 수 있도록 각 응용 프로그램에 대 한 활성화 됩니다. Hello 링크 하려는 경우에 응용 프로그램에 대 한 링크 변환 설정 *에서* 해당 앱 toobe 번역 링크 하지 *를* 앱. 

예를 들어, 모든 다른 tooeach에 연결 하는 응용 프로그램 프록시를 통해 게시 된 세 개의 응용 프로그램을 해야: 이점과 비용을 이동 합니다. 그리고 응용 프로그램 프록시를 통해 게시되지 않은 네 번째 Feedback 앱이 있습니다.

Hello 이점 앱에 대 한 링크 변환을 사용 하도록 설정 하면 hello 링크 tooExpenses 및 여행 해당 앱에 대 한 외부 Url 리디렉션된 toohello 하지만 외부 URL이 없습니다 있기 때문에 hello 링크 tooFeedback 리디렉션되지 않습니다. 비용 및 여행 백 tooBenefits 그러한 두 응용 프로그램에 대 한 링크 변환이 설정 되어 있으므로 작동 하지 않는에서 링크를 제공 합니다.

![앱에서 링크 변환을 사용 하는 이점 tooother 앱의 링크](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>변환되지 않는 링크

일부 링크 없습니다 tooimprove 성능 및 보안을 변환 합니다.

- 코드 태그 내부에 있지 않은 링크. 
- HTML, CSS 또는 JavaScript에 있지 않은 링크. 
- 다른 프로그램에서 연 내부 링크. 메일이나 인스턴트 메시지를 통해 전송되거나 다른 문서에 포함된 링크는 변환되지 않습니다. hello 사용자 tooknow toogo toohello 외부 URL이 필요 합니다.

이러한 두 시나리오 중 하나가 toosupport 해야 할 경우 사용 하 여 동일한 hello 링크 변환 하는 대신 내부 및 외부 Url입니다.  

## <a name="enable-link-translation"></a>링크 변환을 사용하도록 설정

링크 변환 시작은 단추를 클릭하는 것만큼 간단합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.
2. 너무 이동**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** > toomanage 선택 hello 앱 > **응용 프로그램 프록시**합니다.
3. 설정 **응용 프로그램 본문에 Url 변환** 너무**예**합니다.

   ![응용 프로그램이 본문의 예 tootranslate Url 선택](./media/application-proxy-link-translation/select_yes.png)에서도 확인할 수 있습니다.
4. 선택 **저장** tooapply 변경 내용을 합니다.

이제 사용자가이 응용 프로그램에 액세스 하는 경우 hello 프록시 테 넌 트에 응용 프로그램 프록시를 통해 게시 된 내부 Url에 대 한 자동으로 검사 합니다.

## <a name="send-feedback"></a>피드백 보내기

원하는 도움말 toomake이 기능은 작업 모든 앱에 대 한 합니다. HTML 및 CSS를 30 개 이상의 태그를 검색 하 고는 JavaScript의 경우 toosupport 고려 하 고 있습니다. 번역 되지 되지 않은 생성 된 링크의 예를 사용 하는 경우 코드 조각에 너무 보낼[응용 프로그램 프록시 피드백](mailto:aadapfeedback@microsoft.com)합니다. 

## <a name="next-steps"></a>다음 단계
[사용자 지정 도메인을 사용 하 여 Azure AD 응용 프로그램 프록시](active-directory-application-proxy-custom-domains.md) toohave hello 동일한 내부 및 외부 URL

[SharePoint 2013에 대한 대체 액세스 매핑 구성](https://technet.microsoft.com/library/cc263208.aspx)
