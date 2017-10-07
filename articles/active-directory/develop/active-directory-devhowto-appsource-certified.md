---
title: "Azure Active Directory에 대 한 인증 AppSource aaaHow tooget | Microsoft Docs"
description: "어떻게 tooget AppSource 응용 프로그램에 대해 인증 된 Azure Active Directory에 대 한 세부 정보입니다."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>Azure Active Directory에 대 한 tooget AppSource 인증 하는 방법
[Microsoft AppSource](https://appsource.microsoft.com/) 대상이 되는 비즈니스 사용자가 toodiscover를 실행 하 고 관리 업무의 SaaS 응용 프로그램 (독립 실행형 추가 기능 및 SaaS tooexisting SaaS 제품).

독립 실행형 AppSource에서 SaaS 응용 프로그램 toolist single sign on에서 모든 회사 또는 조직 Azure Active Directory에서 작업 계정에서 응용 프로그램 동의 해야 합니다. hello 로그인 프로세스는 hello를 사용 해야 [OpenID Connect](./active-directory-protocols-openid-connect-code.md) 또는 [OAuth 2.0](./active-directory-protocols-oauth-code.md) 프로토콜입니다. SAML 통합은 AppSource 인증에 허용되지 않습니다.

## <a name="guides-and-code-samples"></a>지침 및 코드 샘플
가이드에 따라 및 코드 hello에 대 한 샘플 Openid를 사용 하 여 Azure Active Directory와 응용 프로그램 연결 하는 toointegrate 방법에 대 한 toolearn 하려는 경우 [Azure Active Directory 개발자 가이드](./active-directory-developers-guide.md#get-started "시작 개발자를 위한 azure AD")합니다.

## <a name="multi-tenant-applications"></a>다중 테넌트 응용 프로그램

별도 인스턴스, 구성 또는 배포를 요구하지 않고 Azure Active Directory가 있는 모든 회사 또는 조직에서 사용자의 로그인을 허용하는 응용 프로그램은 *다중 테넌트 응용 프로그램*이라고 합니다. AppSource 응용 프로그램은 다중 테 넌 트 tooenable hello 구현 하는 것이 좋습니다. *단일 클릭* 평가판 체험을 해제 합니다.

순서 tooenable 다중 테 넌 트 응용 프로그램에서:
- 설정 `Multi-Tenanted` 속성 너무`Yes` hello의 응용 프로그램 등록의 정보에 [Azure 포털](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (기본적으로 hello Azure 포털에서에서 만든 응용 프로그램으로 구성 된 *단일-테넌트*)
- 프로그램 코드 toosend 요청 toohello 업데이트 '`common`' 끝점 (hello 끝점에서 업데이트 *https://login.microsoftonline.com/ {yourtenant}* 너무*https://login.microsoftonline.com/common*)
- ASP.NET과 같은 일부 플랫폼에 대 한 필요한도 tooupdate 코드 tooaccept 여러 발급자

다중 테 넌 트에 대 한 자세한 내용은 참조: [방법을 사용 하 여 모든 Azure AD (Active Directory) 사용자의 toosign hello 다중 테 넌 트 응용 프로그램 패턴](./active-directory-devhowto-multi-tenant-overview.md)합니다.

### <a name="single-tenant-applications"></a>단일 테넌트 응용 프로그램
정의된 Azure Active Directory 인스턴스의 사용자의 로그인만 허용하는 응용 프로그램은 *단일 테넌트 응용 프로그램*이라고 합니다. 외부 사용자 (다른 조직에서 회사 또는 학교 계정 또는 개인 계정 포함)으로 각 사용자를 추가한 후 tooa 단일 테 넌 트 응용 프로그램에 로그인 할 수 *게스트 계정* toohello Azure Active Directory 인스턴스를 hello 응용 프로그램 등록 됩니다. Hello 통해 게스트 계정 tooan Azure Active Directory로 사용자를 추가할 수 있습니다 [ *Azure AD B2B 공동 작업* ](../active-directory-b2b-what-is-azure-ad-b2b.md) -수행 될 수 있습니다 [프로그래밍](../active-directory-b2b-code-samples.md)합니다. 게스트 계정 tooan Azure Active Directory로 사용자를 추가 하면 hello hello 초대 메일 링크를 클릭 하 여 tooaccept hello 초대를 가진 toohello 사용자 초대 메일 전송 됩니다. Hello 파트너 조식의 멤버 이기도 초대 조직의 tooan 추가 사용자 보낸 초대에는 초대 toosign를 tooaccept 필요 하지 않습니다는 합니다.

단일 테 넌 트 응용 프로그램에는 hello 사용 하도록 설정할 수 *연락처 Me* 을 발생 하지만 tooenable hello 단일 클릭 / 무료 평가판 체험 AppSource 권장 하는 경우 사용 하도록 설정 응용 프로그램에 다중 테 넌 트 대신 합니다.


## <a name="appsource-trial-experiences"></a>AppSource 평가판 체험

### <a name="free-trial-customer-led-trial-experience"></a>평가판(고객 주도 평가판 체험) 
hello *고객 이끄는 평가판* AppSource 권장 단일 클릭 액세스 tooyour 응용 프로그램이 제공 하는 hello 환경 진행 됩니다. 아래는 이 체험이 표시되는 방식의 그림입니다.<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>사용자는 AppSource 웹 사이트에서 응용 프로그램을 찾습니다.</li><li>‘평가판’ 옵션을 선택합니다.</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource 리디렉션하여 사용자 tooa URL은 웹 사이트에서</li><li>웹 사이트가 시작 hello <i>단일 로그온</i> 에서 자동으로 (페이지 로드) 프로세스</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>사용자가 리디렉션된 tooMicrosoft 로그인 페이지</li><li>사용자의 자격 증명 toosign를 제공합니다.</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>사용자는 응용 프로그램에 대한 동의를 제공합니다.</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>로그인을 완료 하 고 사용자가 리디렉션된 백 tooyour 웹 사이트</li><li>사용자가 hello 무료 평가판 시작</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>연락처(파트너 주도 평가판 체험)
hello *평가판 체험 파트너* 수동 또는 장기 작업 toohappen tooprovision hello 사용자 필요로 하는 경우 사용할 수 있습니다 / 회사: 예를 들어 응용 프로그램에 필요한 tooprovision 가상 컴퓨터, 데이터베이스 인스턴스 또는 많은 시간 toocomplete를 사용 하는 작업입니다. 이 경우 사용자가 선택 되어 hello 후 *요청 평가판* 단추를 사용자의 연락처 정보를 hello 보냅니다 AppSource는 양식을 작성 합니다. 이 정보를 받으면 다음 프로 비전 hello 환경 및 있습니다 어떻게 tooaccess hello 평가판 체험에 hello 지침 toohello 사용자 보내기:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>사용자는 AppSource 웹 사이트에서 응용 프로그램을 찾습니다.</li><li>'연락처' 옵션을 선택합니다.</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>연락처 정보로 양식을 작성합니다.</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>사용자 정보를 수신합니다.</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>환경을 설정합니다.</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>평가판 정보로 사용자에게 연락합니다.</td>
        </tr>
        </table><br/><br/>
        <ul><li>사용자의 정보를 받고 평가판 인스턴스를 설정합니다.</li><li>Hello 하이퍼링크 tooaccess 응용 프로그램 toohello 사용자 보내기</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>사용자가 응용 프로그램 및 전체 hello 단일 로그온 프로세스를 액세스</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>사용자는 응용 프로그램에 대한 동의를 제공합니다.</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>로그인을 완료 하 고 사용자가 리디렉션된 백 tooyour 웹 사이트</li><li>사용자가 hello 무료 평가판 시작</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>자세한 정보
Hello AppSource 평가판 체험 방법에 대 한 자세한 내용은 참조 [이 비디오](https://aka.ms/trialexperienceforwebapps)합니다. 
 
## <a name="next-steps"></a>다음 단계

- Azure Active Directory 로그인을 지원하는 응용 프로그램 구축에 대한 자세한 내용은 [Azure AD에 대한 인증 시나리오](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)를 참조하세요. 

- 방법 toolist AppSource에서 SaaS 응용 프로그램으로 참조에 대 한 내용은 [AppSource 파트너 정보](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>지원 받기
Azure Active Directory 통합을 위해 사용 하 여 [스택 오버플로](http://stackoverflow.com/questions/tagged/azure-active-directory) hello 커뮤니티 tooprovide 지원 합니다. 

스택 오버플로에 질문을 먼저 확인 하 고 질문 하기 전에 요청에 다른 사람이 되 면 기존 문제 toosee 찾아보기 것이 좋습니다. 질문이나 의견이 `[azure-active-directory]`로 태그가 지정되어 있는지 확인합니다.

다음 설명 섹션 tooprovide 피드백 hello를 사용 하 여 및 구체화 하 고 콘텐츠를 셰이핑 하는 데 도움이 됩니다.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->