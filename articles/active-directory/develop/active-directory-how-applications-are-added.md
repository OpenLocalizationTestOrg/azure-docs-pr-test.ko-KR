---
title: "응용 프로그램 aaaHow tooAzure Active Directory에 추가 됩니다."
description: "이 문서에서는 응용 프로그램을 Azure Active Directory의 tooan 인스턴스를 추가 하는 방법을 설명 합니다."
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>응용 프로그램을 AD tooAzure 추가 방법과 이유
처음 하느라 작업의 Azure Active Directory 인스턴스에 응용 프로그램 목록을 볼 때 hello 중 하나는 hello 응용 프로그램에서 제공 하는 위치 및 있습니다는 이유 파악 합니다.  이 문서에서는 응용 프로그램이 hello 디렉터리에 표시 하 고 응용 프로그램 디렉터리에 toobe를 제공 하는 방법을 이해 하는 데 도움이 되는 컨텍스트를 제공 하는 방식의 높은 수준의 개요를 제공 합니다.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>어떤 서비스 Azure AD에서 제공 하는 tooapplications
응용 프로그램을 제공 하는 hello 서비스의 하나 이상의 AD tooAzure tooleverage는 추가 합니다.  서비스 포함 사항:

* 인증 및 권한 부여
* 사용자 인증 및 권한 부여
* 페더레이션 또는 암호를 사용한 SSO(Single Sign-On)
* 사용자 프로비전 및 동기화
* 역할 기반 액세스 제어. 사용 하 여 hello 디렉터리 toodefine 응용 프로그램 역할 tooperform 역할 기반 응용 프로그램에서 권한 부여 확인 합니다.
* oAuth 권한 부여 서비스 (Office 365 및 기타 Microsoft 앱 tooauthorize tooAPIs/리소스에 액세스 하 여 사용 됩니다.)
* 응용 프로그램 게시 및 프록시가 잘못 되었습니다. 개인 네트워크 toohello에서 응용 프로그램을 게시 인터넷

## <a name="how-are-applications-represented-in-hello-directory"></a>Hello 디렉터리에 응용 프로그램을 표현 하는 방법
응용 프로그램 hello 2 개체를 사용 하 여 Azure AD에에서 표시 됩니다: 응용 프로그램 개체 및 서비스 사용자 개체입니다.  "홈"에 등록 한 응용 프로그램 개체는 / 디렉터리를 "소유자" 또는 "게시" 및 하나 이상의 서비스를 사용 하는 모든 디렉터리에서 hello 응용 프로그램을 나타내는 보안 주체 개체입니다.  

hello application 개체 hello 앱 tooAzure AD (hello 다중 테 넌 트 서비스)에 대해 설명 하 고 hello 다음 중 하나일 수 있습니다: (*참고*: 완전 한 목록을 아닙니다.)

* 이름, 로고, 게시자
* 비밀 (대칭 및/또는 비대칭 키 tooauthenticate hello 앱을 사용 하는 데 사용)
* API 종속성(oAuth)
* 게시된 API/리소스/범위(oAuth)
* 응용 프로그램 역할(RBAC)
* SSO 메타데이터 및 구성(SSO)
* 사용자 프로비전 메타데이터 및 구성
* 프록시 메타데이터 및 구성

hello 서비스 사용자는 hello 응용 프로그램 hello 응용 프로그램의 홈 디렉터리를 포함 하는 역할 모든 디렉터리에 대 한 기록 합니다.  hello 서비스 사용자의 경우:

* 다시 hello 응용 프로그램 id 속성을 통해 tooan application 개체 참조
* 로컬 사용자 및 그룹 응용 프로그램 역할 할당 기록
* 레코드 로컬 사용자 및 관리자 권한 부여 toohello 응용 프로그램
  * 예를 들어: hello 앱 tooaccess 특정 사용자가 전자 메일에 대 한 사용 권한
* 조건부 액세스 정책을 포함하여 로컬 정책 기록
* 앱의 대체 로컬 설정 기록
  * 클레임 변환 규칙
  * 특성 매핑(사용자 프로비전)
  * (Hello 앱 지 원하는 경우 사용자 정의 역할) 테 넌 트 특정 응용 프로그램 역할
  * 이름/로고

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>응용 프로그램 개체 및 서비스 주체 액세스 디렉터리 다이어그램
![응용 프로그램 개체와 서비스 주체가 Azure AD 인스턴스와 같이 존재하는 방법을 보여 주는 다이어그램입니다.][apps_service_principals_directory]

위의 hello 다이어그램에서 볼 수 있습니다.  Microsoft는 두 디렉터리를 관리 내부적으로 (hello 왼쪽에) 사용 하 여 toopublish 응용 프로그램입니다.

* Microsoft 응용 프로그램용 디렉터리(Microsoft 서비스 디렉터리)
* 사전 통합된 타사 응용 프로그램용 디렉터리(응용 프로그램 갤러리 디렉터리)

응용 프로그램 게시자/공급 업체 Azure AD와 통합은 필요한 toohave 게시 디렉터리입니다.  (일부 SAAS 디렉터리)

직접 추가하는 응용 프로그램은 다음과 같습니다.

* 직접 개발한 응용 프로그램(AAD와 통합됨)
* Single-Sign-On용으로 연결된 응용 프로그램
* 사용 하 여 게시 된 응용 프로그램 hello Azure AD 응용 프로그램 프록시입니다.

### <a name="a-couple-of-notes-and-exceptions"></a>일부 참고 및 예외 사항
* 일부 서비스 주체 백 tooapplication 개체를 가리킵니다.  그렇죠? Azure AD 원래 작성 했을 때 hello 서비스 제공 tooapplications 훨씬 더 제한 된 hello 서비스 사용자는 응용 프로그램 id를 설정 하는 데만 있어도 충분 했습니다.  hello 원래 서비스 사용자가 셰이프 toohello Windows Server Active Directory 서비스 계정에에서 더 가깝기 때문입니다.  사용 하 여 서비스 사용자는 여전히 가능한 toocreate는 이러한 이유로 먼저 응용 프로그램 개체를 만들지 않고 Azure AD PowerShell hello 합니다.  Graph API hello 사용자는 서비스를 만들기 전에 응용 프로그램 개체를 필요 합니다.
* 위에서 설명한 hello 정보 중 일부만 프로그래밍 방식으로 노출 현재 됩니다.  hello 다음 UI hello 사용할 수만 있습니다.
  * 클레임 변환 규칙
  * 특성 매핑(사용자 프로비전)
* 더 자세한 hello 서비스 사용자에 대 한 정보 및 응용 프로그램 개체 toohello Azure AD 그래프 REST API 참조 설명서를 참조 하십시오.  *힌트*: hello Azure AD 그래프 API 설명서가 현재 사용할 수 있는 Azure AD에 대 한 hello 가장 가까운 것 tooa 스키마 참조 합니다.  
  * [응용 프로그램](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [서비스 주체](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>앱은 toomy Azure AD 인스턴스를 추가 하는 방법
여러 가지 방법으로 앱 tooAzure 광고를 추가할 수 있습니다.

* Hello에서 앱을 추가 [Azure Active Directory 응용 프로그램 갤러리](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Azure Active Directory와 통합된 타사 응용 프로그램에 등록/로그인(예: [Smartsheet](https://app.smartsheet.com/b/home) 또는 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))
  * 등록/사용자가 로그인 하는 동안 자주 묻는 toogive 권한 toohello 앱 tooaccess은 자신의 프로필 및 다른 권한입니다.  첫 번째 사람 toogive hello 원인을 hello 앱 toobe 추가 toohello 디렉터리를 나타내는 서비스 사용자를 동의 합니다.
* [Office 365](http://products.office.com/)
  * TooOffice 365를 구독 하거나 평가판 하나를 시작 하거나 더 많은 서비스 사용자는 다양 한 서비스를 Office 365와 관련 된 hello 기능을 모두 사용 되는 toodeliver hello 나타내는 hello 디렉터리에 만들어집니다.
  * SharePoint와 같은 일부 Office 365 서비스는 워크플로 포함 하 여 구성 요소 간에 지속적으로 tooallow 보안 통신에 서비스 사용자를 만듭니다.
* Azure 관리 포털에서 참조 하는 hello에서 개발 하는 앱 추가: https://msdn.microsoft.com/library/azure/dn132599.aspx
* Visual Studio를 사용하여 개발 중인 응용 프로그램 추가. 참조:
  * [ASP.Net 인증 방법](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [연결된 서비스](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* 응용 프로그램 toouse toouse hello 추가 [Azure AD 응용 프로그램 프록시](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* SAML 또는 암호 SSO를 사용하여 Single-Sign-On용 응용 프로그램 연결
* Azure의 다양한 개발자 환경 및 개발자 센터의 API 탐색기 환경을 포함한 기타 여러 가지 방법

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>사용 권한 tooadd 응용 프로그램 toomy Azure AD 인스턴스 사람은 누구 입니까?
다음 작업은 전역 관리자만 수행할 수 있습니다.

* Hello Azure AD 앱 갤러리 (사전 통합 된 타사 앱)에서 앱을 추가 합니다.
* Hello Azure AD 응용 프로그램 프록시를 사용 하 여 앱 게시

디렉터리의 모든 사용자는 개발 중인 권한 tooadd 응용 프로그램 및 응용 프로그램을 통해 이러한 공유/제공 tootheir 조직 데이터에 액세스를 신중 하 게 갖습니다.  *위쪽/tooan 응용 프로그램에서 사용자 로그인 하십시오. 서비스 생성 되 고 사용자 권한을 부여 한다고 해 발생할 수 있습니다.*

이 처음 사운드에 관한 수 있지만 유지 hello 염두에서 다음:

* 앱은 hello 디렉터리에 등록 된/기록 hello 응용 프로그램 toobe 필요 없이 몇 년에 대 한 사용자 인증에 대 한 Windows Server Active Directory tooleverage 수 되었습니다.  Hello 조직 가시성 tooexactly 되었지만 이제 응용 프로그램과 hello 디렉터리 및 이유를 사용 하 합니다.
* 관리자 중심 응용 프로그램 게시/등록 프로세스가 필요하지 않습니다.  Active Directory Federation services는 관리자가 tooadd 응용 프로그램 개발자를 대신 하 여 신뢰 당사자로 가능성이 있었습니다.  이제 개발자가 직접 할 수 있습니다.
* 사용자 로그인/tooapps 자신의 조직 계정을 사용 하 여 업무 목적을 좋은 소식입니다.  이후에 hello 조직을 떠나면 액세스 tootheir 계정을 사용 하 던 hello 응용 프로그램에서 손실 됩니다.
* 어떤 데이터를 어떤 응용 프로그램과 공유했는지 기록하는 것이 좋습니다.  데이터는 더욱 전송하기 쉬워졌으며 어떤 데이터를 어떤 응용 프로그램으로 누구와 공유했는지 기록해놓는 것이 유용합니다.
* OAuth 용 Azure AD를 사용 하는 응용 프로그램 사용자가 수 toogrant tooapplications 및 사용 권한이 필요로 하는 관리자 tooagree 권한을 정확 하 게 결정 합니다.  보다 중요 한 권한과 toolarger 범위 관리자만 동의할 수 독립 이동 해야 합니다.
* 추가 하 고 해당 데이터는 앱 tooaccess 감사 된 이벤트 hello Azure 관리 포털 toodetermine 내 hello 감사 보고서를 볼 수 있도록 허용 하는 사용자가 앱 추가 하는 방법과 toohello 디렉터리입니다.

**참고:** *개월 수에 대 한 hello 기본 구성을 사용 하 여 자체 Microsoft 작동 합니다.*

모두 것이 가능한 tooprevent 사용자가 응용 프로그램을 추가 하 고 hello Azure 관리 포털에서 디렉터리 구성을 수정 하 여 응용 프로그램과 공유 하는 정보에 대해 신중 하 게 못하도록 디렉터리에 있다고 합니다.  hello 다음과 같은 구성이 액세스할 수 있습니다 디렉터리의 "구성" 탭에서 hello Azure 관리 포털 내에서.

![통합된 응용 프로그램 설정을 구성 하기 위한 UI hello의 스크린 샷][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
에 대 한 자세한 방법에 대 한 tooadd 응용 프로그램 tooAzure AD 및 tooconfigure 앱에 대 한 서비스 하는 방법입니다.

* 개발자: [학습 방법을 toointegrate AAD에 응용 프로그램](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* 개발자: [GitHub에서 Azure Active Directory와 통합된 앱의 샘플 코드 검토하기](https://github.com/AzureADSamples)
* 개발자와 IT 전문가: [hello Azure Active Directory Graph API에 대 한 hello REST API 설명서를 검토 합니다.](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* IT 전문가: [toouse Azure Active Directory hello 응용 프로그램 갤러리에서에서 응용 프로그램 미리 통합 하는 방법에 대해 알아봅니다](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* IT 전문가: [사전 통합된 특정 응용 프로그램 구성에 대한 자습서 찾기](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* IT 전문가: [방법을 사용 하 여 앱 toopublish hello Azure Active Directory 응용 프로그램 프록시에 알아봅니다](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>참고 항목
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
