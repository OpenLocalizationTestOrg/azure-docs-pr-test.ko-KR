---
title: "Active Directory의 플레이 북 블록 개념 증명 aaaAzure | Microsoft Docs"
description: "ID 및 액세스 관리 시나리오를 탐색하고 신속하게 구현"
services: active-directory
keywords: "Azure Active Directory, 플레이 북, 개념 증명, PoC"
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Azure Active Directory 개념 증명 플레이 북: 문서 블록

## <a name="catalog-of-roles"></a>역할 카탈로그

| 역할 | 설명 | 개념 증명(PoC) 책임 |
| --- | --- | --- |
| **ID 아키텍처/개발 팀** | 이 팀은 일반적으로 hello 솔루션을 디자인을 구현 하는 프로토타입, 승인, 드라이브 toooperations에 마지막으로 전달한 하나 hello | Hello 환경을 제공 하며 hello 관리 효율성 측면에서 hello 구성 제공 하는 hello 평가 다른 시나리오는 |
| **온-프레미스 ID 작업 팀** | Hello 다른 id 소스 온-프레미스 관리: Active Directory 포리스트, LDAP 디렉터리, HR 시스템 및 페더레이션 Id 공급자입니다. | PoC 시나리오 hello에 필요한 tooon 온-프레미스 리소스에 액세스를 제공 합니다.<br/>가능한 한 적게 포함되어야 합니다.|
| **응용 프로그램 기술 소유자** | Azure AD와 통합 하는 hello 다른 클라우드 앱과 서비스의 기술 소유자 | SaaS 응용 프로그램(잠재적으로 테스트할 인스턴스)에 대한 세부 정보를 제공합니다. |
| **Azure AD 전역 관리자** | Azure AD hello 구성 관리 | Tooconfigure hello 동기화 서비스 자격 증명을 제공 합니다. 일반적으로 Id 아키텍처와 같은 팀 PoC 중 hello 있지만 hello 작업 단계 동안 별도|
| **데이터베이스 팀** | Hello 데이터베이스 인프라의 소유자 | 특정 시나리오의 준비 작업에 대 한 액세스 tooSQL 환경 (ad FS 또는 Azure AD Connect)를 제공 합니다.<br/>가능한 한 적게 포함되어야 합니다. |
| **네트워크 팀** | Hello 네트워크 인프라의 소유자 | 서버 tooproperly hello 데이터 원본 액세스 hello 동기화에 대 한 hello 네트워크 수준에서 필요한 액세스를 제공 하 고 클라우드 서비스 (방화벽 규칙, 열린 포트, IPSec 규칙 등) |
| **보안 팀** | Hello 보안 전략을 정의 하 고, 다양 한 소스에서 보안 보고서를 분석 하 고를 통해 다음 결과에. | 대상 보안 평가 시나리오를 제공합니다. |

## <a name="common-prerequisites-for-all-building-blocks"></a>모든 문서 블록에 대한 일반적인 필수 구성 요소

Azure AD Premium에서 POC에 필요한 일부 필수 구성 요소는 다음과 같습니다.

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 유효한 Azure 구독을 통해 정의된 Azure AD 테넌트 | [Tooget Azure Active Directory 테 넌 트](active-directory-howto-tenant.md)<br/>**참고:** toohttps://aka.ms/accessaad 이동 하 여 cap 구독을 Azure AD Premium 라이선스를 갖고 있는 환경이 이미 있는 경우 가져올 수 있습니다 <br/>참고 항목: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ 및 https://technet.microsoft.com/library/dn832618.aspx |
| 정의 및 확인된 도메인 | [사용자 지정 도메인 이름을 tooAzure Active Directory를 추가 합니다.](active-directory-domains-add-azure-portal.md)<br/>**참고:** 일부 워크 로드는 azure AD 테 넌 트 hello에서 Power BI 프로 비전 수와 같은 다룹니다. toocheck 지정된 된 도메인은 테 넌 트 관련된 tooa 이동 toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration 합니다. 성공적인 응답을 hello 도메인 tooa 테 넌 트에 이미 할당 되어 다음로 인계 필요할 수 있습니다. 이 경우 Microsoft에 추가 지침을 문의하세요. Hello에 감염 옵션에 대 한 자세한 정보: [Azure 셀프서비스 란?](active-directory-self-service-signup.md) |
| Azure AD Premium 또는 EMS 평가판 사용 | [한 달 동안 Azure Active Directory Premium 체험](https://azure.microsoft.com/trial/get-started-active-directory/) |
| TooPoC 사용자가 Azure AD Premium 또는 EMS 라이선스를 할당 했는지 | [Azure Active Directory에서 사용자 본인 및 사용자의 사용자 라이선스](active-directory-licensing-get-started-azure-portal.md) |
| Azure AD 전역 관리자 자격 증명 | [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md) |
| 선택 사항이지만 강력하게 권장됨: 대체로서 병렬 랩 환경 | [Azure AD Connect에 대한 필수 구성 요소](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>디렉터리 동기화 - PHS(암호 해시 동기화) - 새 설치

시간 tooComplete 대략적인: 1, 000 보다 작은 PoC 사용자에 대 한 1 시간

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 서버 tooRun Azure AD Connect | [Azure AD Connect에 대한 필수 구성 요소](./connect/active-directory-aadconnect-prerequisites.md) |
| Hello에 POC 사용자를 대상 동일한 도메인 및 보안 그룹과 OU의 일부 | [Azure AD Connect의 사용자 지정 설치](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD 연결에 필요한 기능 hello POC 식별 | [Active Directory와 Azure Active Directory 연결 - 동기화 기능 구성](./connect/active-directory-aadconnect.md#configure-sync-features) |
| 온-프레미스 및 클라우드 환경에 대한 자격 증명이 필요함  | [Azure AD Connect: 계정 및 사용 권한](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Hello 최신 버전의 Azure AD Connect 다운로드 | [Download Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594)(Microsoft Azure Active Directory Connect 다운로드) |
| Hello 간단한 경로와 Azure AD Connect 설치: Express <br/>1. 필터 toohello 대상 OU toominimize hello 동기화 주기 시간<br/>2. Hello 온-프레미스 그룹에 사용자의 대상 집합을 선택 합니다.<br/>3. 다른 POC 테마 hello 필요한 hello 기능 배포 | [Azure AD Connect: 사용자 지정 설치: 도메인 및 OU 필터링](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: 사용자 지정 설치: 그룹 기반 필터링](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Azure Active Directory와 온-프레미스 ID 통합: 동기화 기능 구성](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Hello Azure AD Connect UI 열고 실행 하는 hello 프로필은 완료 된 (가져오기, 동기화 및 내보내기)를 참조 하십시오. | [Azure AD Connect 동기화: 스케줄러](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| 열기 hello [Azure AD 관리 포털](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/)toohello "모든 사용자" 블레이드로 이동, "Windows Server AD"에서 오는 것으로 올바르게 표시 된 "인증 원본" 열과 hello 사용자 나타나는 참조 추가 | [Azure AD management portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)(Azure AD 관리 포털) |

### <a name="considerations"></a>고려 사항

1. 암호 해시 동기화의 보안 고려 사항 hello 살펴보고 [여기](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)합니다.  파일럿 프로덕션 사용자에 대 한 암호 해시 동기화 옵션 명확 하지 경우 hello 대체를 수행 하 여 다음:
   * Hello 프로덕션 도메인에서 테스트 사용자를 만듭니다. 다른 계정을 동기화하지 않는지 확인합니다.
   * 이동 tooan 사용자 수용 테스트 환경
2.  이 좋은지를 toopursue 페더레이션 하려는 경우 측정값 hello에 대해 제공 되는 것을 찾고와 toounderstand hello 비용 hello POC 초과 온-프레미스 Id 공급자와 페더레이션된 솔루션을 연결 합니다.
    * Hello 요주의 경로에 고가용성을 위해 toodesign 이므로
    * Toocapacity 계획 해야 하는 온-프레미스 서비스
    * toomonitor/유지 관리/patch 필요한 온-프레미스 서비스

참고 항목: [Office 365 ID 및 Azure Active Directory 이해 - 페더레이션 ID](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>브랜딩

시간 tooComplete 대략적인: 15 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 자산 (이미지, 로고, 등). 가장 적합 한 시각화에 대 한 크기를 추천 hello가 있는지 hello 자산을 확인 합니다. | [회사 hello Azure Active Directory에서에서 tooyour 로그인 페이지 브랜딩 추가](active-directory-branding-custom-signon-azure-portal.md) |
| 선택 사항: hello 환경 ADFS 서버 있으면 액세스 toohello 서버 toocustomize 웹 테마 | [AD FS user sign-in customization](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization)(AD FS 사용자 로그인 사용자 지정) |
| 클라이언트 컴퓨터 tooperform 최종 사용자 로그인 환경 |  |
| 선택 사항: 모바일 장치 toovalidate 경험 |  |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 이동 tooAzure AD 관리 포털 | [Azure AD Management Portal - Company Branding](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding)(Azure AD 관리 포털 - 회사 브랜딩) |
| Hello 로그인 페이지 (hero 로고, 작은 로고, 레이블 등)에 대 한 hello 자산을 업로드 합니다. AD FS를 사용 하는 경우 필요에 따라 정렬 hello ADFS 로그인 페이지를 사용 하 여 동일한 자산 | [회사 브랜딩 tooyour 로그인 및 액세스 패널 페이지 추가: 사용자 지정 가능 요소](active-directory-add-company-branding.md) |
| 몇 분 내 hello 변경 toofully 영향에 대 한 대기 |  |
| POC 사용자 자격 증명 toohttps://myapps.microsoft.com hello로에 로그인 |  |
| 브라우저에서 hello 모양 및 느낌을 확인 합니다. | [회사 브랜딩 tooyour 로그인 및 액세스 패널 페이지 추가](active-directory-add-company-branding.md) |
| 필요에 따라 다른 장치에서 hello 모양 및 느낌을 확인 |  |

### <a name="considerations"></a>고려 사항

Hello 이전 모양과 느낌 hello 사용자 지정 후 유지 되는 경우 다음 hello 브라우저 클라이언트 캐시를 플러시하고 hello 작업을 다시 시도 합니다.

## <a name="group-based-licensing"></a>그룹 기반 라이선싱

시간 tooComplete 대략적인: 10 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 모든 POC 사용자가 보안 그룹에 속함(클라우드 또는 온-프레미스) | [Azure Active Directory에서 그룹 만들기 및 구성원 추가](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Azure AD 관리 포털에서 toolicenses 블레이드로 이동 | [Azure AD Management Portal: Licensing](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products)(Azure AD 관리 포털: 라이선싱) |
| POC 사용자와 hello 라이선스 toohello 보안 그룹을 할당 합니다. | [Azure Active Directory에서 사용자의 라이선스 tooa 그룹 할당](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>고려 사항

모든 문제 발생 시 이동 너무[시나리오, 제한 사항 및 Azure Active Directory에서 그룹 toomanage 라이선스를 사용 하 여 알려진된 문제](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>SaaS 페더레이션 SSO 구성

시간 tooComplete 대략적인: 60 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| SaaS 응용 프로그램을 사용할 수 있는 hello의 환경을 테스트 합니다. 이 가이드에서는 ServiceNow를 예제로 사용합니다.<br/>권장 toouse 테스트 인스턴스 toominimize 마찰 기존 데이터 품질 및 매핑을 탐색 합니다. | Toohttps://developer.servicenow.com/app.do# 이동! / 테스트 인스턴스를 가져오는 toostart hello 과정 홈 |
| 관리자 액세스 toohello ServiceNow 관리 콘솔 | [자습서: ServiceNow와 Azure Active Directory 통합](active-directory-saas-servicenow-tutorial.md) |
| 대상은 사용자 tooassign hello 응용 프로그램의 집합입니다. Hello PoC 사용자가 포함 된 보안 그룹을 사용 하는 것이 좋습니다. <br/>Hello 그룹을 만드는 적절 하지 않은 경우 사용자를 지정할 hello PoC hello에 대 한 toodirectly toohello 응용 프로그램 | [Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Microsoft 설명서에서 hello 자습서 tooall 작업자를 공유 합니다.  | [자습서: ServiceNow와 Azure Active Directory 통합](active-directory-saas-servicenow-tutorial.md) |
| 작업 회의 설정 하 고 각 행위자를 사용 하 여 hello 자습서 단계를 따릅니다. | [자습서: ServiceNow와 Azure Active Directory 통합](active-directory-saas-servicenow-tutorial.md) |
| Hello 필수 구성 요소에서에서 식별 된 hello app toohello 그룹을 할당 합니다. 나중에 다시 확인 하 고 MFA를 추가할 수 hello POC hello 범위에 대 한 조건부 액세스 있으면 및와 유사 합니다. <br/>Hello (구성 된 경우)의 프로 비전 프로세스는 조정이 시작이 note |  [Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Azure Active Directory에서 그룹 만들기 및 구성원 추가](active-directory-groups-create-azure-portal.md) |
| Azure AD 관리 포털 tooadd ServiceNow 응용 프로그램을 사용 하 여 갤러리에서| [Azure AD management Portal: Enterprise Applications](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview)(Azure AD 관리 포털: 엔터프라이즈 응용 프로그램) <br/>[Azure Active Directory의 새로운 엔터프라이즈 응용 프로그램 관리 기능](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| ServiceNow 앱의 "Single Sign-On" 블레이드에서 "SAML 기반 로그인"을 사용하도록 설정합니다. |  |
| ServiceNow URL을 통해 “로그온 URL” 및 “식별자” 필드를 입력합니다.<br/>Hello 확인란 너무 "만들기" 새 인증서 active<br/>설정을 저장합니다. |  |
| 사용자 지정 지침 tooconfigure ServiceNow hello 패널 tooview의 hello 아래쪽에 "구성 ServiceNow" 블레이드 열기 |  |
| 지침 tooconfigure ServiceNow를 수행 합니다. |  |
| ServiceNow 앱의 “프로비전” 블레이드에서 “자동” 프로비전을 사용하도록 설정합니다. | [Hello 새 Azure 포털에서 엔터프라이즈 앱에 대 한 프로 비전 하는 사용자 계정 관리](active-directory-enterprise-apps-manage-provisioning.md) |
| 프로비전이 완료되는 동안 몇 분 정도 기다립니다.  Hello에 그 동안를 확인할 수 hello 보고서를 프로 비전 |  |
| Toohttps://myapps.microsoft.com/ 액세스할 수 있는 테스트 사용자로 로그인 | [액세스 패널 hello 이란?](active-directory-saas-access-panel-introduction.md) |
| 방금 만든 hello 응용 프로그램에 대 한 hello 타일을 클릭 합니다. 액세스 권한을 확인합니다. |  |
| 필요에 따라 hello 응용 프로그램 사용 현황 보고서를 확인할 수 있습니다. 여기에 메모 약간의 대기 시간 이므로 toowait hello 보고서에 상당한 시간 toosee hello 트래픽이 필요 합니다. | [Hello Azure Active Directory 포털의 로그인 활동 보고서: 관리 되는 응용 프로그램의 사용](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory 보고서 보존 정책](active-directory-reporting-retention.md) |

### <a name="considerations"></a>고려 사항

1. 위의 [자습서](active-directory-saas-servicenow-tutorial.md) tooold Azure AD 관리 환경을 참조 합니다. 하지만 PoC는 [빠른 시작](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away) 환경에 기반을 둡니다.
2. 대상 응용 프로그램 hello hello 갤러리에 요소가 없는 경우 가져오기 위해 자신의 앱"사용할 수 있습니다. 참고 항목: [Azure Active Directory의 새로운 엔터프라이즈 응용 프로그램 관리 기능: 한 곳에서 사용자 지정 응용 프로그램 추가](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>SaaS 암호 SSO 구성

시간 tooComplete 대략적인: 15 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| SaaS 응용 프로그램에 대한 테스트 환경. 암호 SSO의 예로는 HipChat 및 Twitter가 있습니다. 다른 응용 프로그램 html 로그인 폼과 hello 페이지의 hello 정확한 URL이 필요합니다. | [Microsoft Azure Marketplace의 Twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Microsoft Azure Marketplace의 HipChat](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| 테스트 hello 응용 프로그램에 대 한 계정이 있습니다. | [Sign up for Twitter](https://twitter.com/signup?lang=en)(Twitter 가입)<br/>[Sign Up for Free: HipChat](https://www.hipchat.com/sign_up)(무료 가입: HipChat) |
| 대상은 사용자 tooassign hello 응용 프로그램의 집합입니다. 보안 그룹에 포함 된 hello 사용자가 사용 하는 것이 좋습니다. | [Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당](active-directory-coreapps-assign-user-azure-portal.md) |
| 로컬 관리자 액세스 tooa 컴퓨터 toodeploy hello Internet Explorer, Chrome 또는 Firefox에 대 한 액세스 패널 확장 | [Access Panel Extension for IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)(IE용 액세스 패널 확장)<br/>[Access Panel Extension for Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)(Chrome용 액세스 패널 확장)<br/>[Access Panel Extension for Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409)(Firefox용 액세스 패널 확장) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Hello 브라우저 확장을 설치 | [Access Panel Extension for IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)(IE용 액세스 패널 확장)<br/>[Access Panel Extension for Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)(Chrome용 액세스 패널 확장)<br/>[Access Panel Extension for Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409)(Firefox용 액세스 패널 확장) |
| 갤러리에서 응용 프로그램을 구성합니다. | [Azure Active Directory에서 엔터프라이즈 응용 프로그램 관리의 새로운 기능: hello 새롭고 향상 된 응용 프로그램 갤러리](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| 암호 SSO를 구성합니다. | [Single sign on hello 새 Azure 포털에서 엔터프라이즈 앱에 대 한 관리: 암호 기반 로그온](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Hello 필수 구성 요소에서에서 식별 된 hello app toohello 그룹 할당 | [Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당](active-directory-coreapps-assign-user-azure-portal.md) |
| Toohttps://myapps.microsoft.com/ 액세스할 수 있는 테스트 사용자로 로그인 |  |
| 방금 만든 hello 응용 프로그램에 대 한 hello 타일을 클릭 합니다. | [액세스 패널 hello 이란?: id 프로비저닝 기능이 없는 암호 기반 SSO](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Hello 응용 프로그램 자격 증명을 제공 합니다. | [액세스 패널 hello 이란?: id 프로비저닝 기능이 없는 암호 기반 SSO](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| 반복 hello 로그인 및 hello 브라우저를 닫습니다. 이번 hello 사용자에 대 한 원활한 액세스 toohello 응용 프로그램이 표시 됩니다. |  |
| 필요에 따라 hello 응용 프로그램 사용 현황 보고서를 확인할 수 있습니다. 여기에 메모 약간의 대기 시간 이므로 toowait hello 보고서에 상당한 시간 toosee hello 트래픽이 필요 합니다. | [Hello Azure Active Directory 포털의 로그인 활동 보고서: 관리 되는 응용 프로그램의 사용](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory 보고서 보존 정책](active-directory-reporting-retention.md) |

### <a name="considerations"></a>고려 사항

대상 응용 프로그램 hello hello 갤러리에 요소가 없는 경우 가져오기 위해 자신의 앱"사용할 수 있습니다. 참고 항목: [Azure Active Directory의 새로운 엔터프라이즈 응용 프로그램 관리 기능: 한 곳에서 사용자 지정 응용 프로그램 추가](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 유의 hello 요구 사항에 주의 하십시오.
   * 응용 프로그램에 알려진 로그인 URL이 있어야 합니다.
   * hello 로그인 페이지 hello 브라우저 확장 채울 수 있는 자동-하나 이상의 텍스트 필드를 사용 하 여 HTML 폼을 포함 해야 합니다. 최소 hello에서 사용자 이름 및 암호 포함 되어야 합니다.

## <a name="saas-shared-accounts-configuration"></a>SaaS 고유 계정 구성

시간 tooComplete 대략적인: 30 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 대상 응용 프로그램 목록을 hello 및 hello 미리 정확한 로그인 URL입니다. 예를 들어 Twitter를 사용할 수 있습니다. | [Microsoft Azure Marketplace의 Twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Sign up for Twitter](https://twitter.com/signup?lang=en)(Twitter 가입) |
| 이 SaaS 응용 프로그램에 대한 공유 자격 증명. | [Azure AD를 사용한 계정 공유](active-directory-sharing-accounts.md)<br/>[이제 미리 보기에서 Facebook, Twitter 및 LinkedIn에 대해 Azure AD 자동화된 암호 롤오버! - 엔터프라이즈 모바일 및 보안 블로그(영문)] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/ ) |
| 액세스 하는 두 개 이상의 팀 멤버에 대 한 자격 증명 hello 동일한 계정입니다. 이 팀원은 보안 그룹에 속해야 합니다. | [Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당](active-directory-coreapps-assign-user-azure-portal.md) |
| 로컬 관리자 액세스 tooa 컴퓨터 toodeploy hello Internet Explorer, Chrome 또는 Firefox에 대 한 액세스 패널 확장 | [Access Panel Extension for IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)(IE용 액세스 패널 확장)<br/>[Access Panel Extension for Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)(Chrome용 액세스 패널 확장)<br/>[Access Panel Extension for Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409)(Firefox용 액세스 패널 확장) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Hello 브라우저 확장을 설치 | [Access Panel Extension for IE](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)(IE용 액세스 패널 확장)<br/>[Access Panel Extension for Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)(Chrome용 액세스 패널 확장)<br/>[Access Panel Extension for Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409)(Firefox용 액세스 패널 확장) |
| 갤러리에서 응용 프로그램을 구성합니다. | [Azure Active Directory에서 엔터프라이즈 응용 프로그램 관리의 새로운 기능: hello 새롭고 향상 된 응용 프로그램 갤러리](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| 암호 SSO를 구성합니다. | [Single sign on hello 새 Azure 포털에서 엔터프라이즈 앱에 대 한 관리: 암호 기반 로그온](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| 자격 증명을 할당 하는 동안 hello 필수 구성 요소에서에서 식별 된 hello app toohello 그룹 할당 | [Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당](active-directory-coreapps-assign-user-azure-portal.md) |
| 다른 사용자로 hello로 액세스 앱 로그인 **동일한 계정을 공유 합니다.**  |  |
| 필요에 따라 hello 응용 프로그램 사용 현황 보고서를 확인할 수 있습니다. 여기에 메모 약간의 대기 시간 이므로 toowait hello 보고서에 상당한 시간 toosee hello 트래픽이 필요 합니다. | [Hello Azure Active Directory 포털의 로그인 활동 보고서: 관리 되는 응용 프로그램의 사용](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory 보고서 보존 정책](active-directory-reporting-retention.md) |


### <a name="considerations"></a>고려 사항

대상 응용 프로그램 hello hello 갤러리에 요소가 없는 경우 가져오기 위해 자신의 앱"사용할 수 있습니다. 참고 항목: [Azure Active Directory의 새로운 엔터프라이즈 응용 프로그램 관리 기능: 한 곳에서 사용자 지정 응용 프로그램 추가](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 유의 hello 요구 사항에 주의 하십시오.
   * 응용 프로그램에 알려진 로그인 URL이 있어야 합니다.
   * hello 로그인 페이지 hello 브라우저 확장 채울 수 있는 자동-하나 이상의 텍스트 필드를 사용 하 여 HTML 폼을 포함 해야 합니다. 최소 hello에서 사용자 이름 및 암호 포함 되어야 합니다.

## <a name="app-proxy-configuration"></a>앱 프록시 구성

시간 tooComplete 대략적인: 20 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 사용자가 전역 관리자인 Microsoft Azure AD 기본 또는 프리미엄 구독 및 Azure AD 디렉터리 | [Azure Active Directory 버전](active-directory-editions.md) |
| 웹 응용 프로그램 호스트 온-프레미스 싶다는 의사를 원격 액세스를 위한 tooconfigure |  |
| Hello 응용 프로그램 프록시 커넥터를 설치할 수 있는 Windows Server 2012 R2 또는 Windows 8.1 이상을 실행 중인 서버 | [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md) |
| Hello 경로에 방화벽이 있는 경우 것는 열려 있으므로 toohello 응용 프로그램 프록시를 요청 하는 해당 hello 커넥터는 HTTPS (TCP)을 만들 수 있는지 확인 | [Hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정: 응용 프로그램 프록시 사전 요구 사항](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| 조직에서 프록시를 사용 하는 경우 서버 tooconnect toohello 인터넷에 대 한 기존 온-프레미스 프록시 서버와 작업을 게시 하는 hello 블로그를 확인 하는 내용이 방법에 자세히 설명 tooconfigure에 | [기존 온-프레미스 프록시 서버 작업](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Hello 서버에 커넥터를 설치 합니다. | [Hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정: hello 커넥터 등록 및 설치](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Azure ad 응용 프로그램 프록시 응용 프로그램으로 hello 온-프레미스 응용 프로그램 게시 | [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](application-proxy-publish-azure-portal.md) |
| 테스트 사용자를 할당합니다. | [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시: 테스트 사용자 추가](application-proxy-publish-azure-portal.md#add-a-test-user) |
| 필요한 경우 사용자에 대한 Single Sign-On 환경을 구성합니다. | [Azure AD 응용 프로그램 프록시를 사용하여 Single Sign-On 제공](application-proxy-sso-azure-portal.md) |
| 할당 된 사용자로 tooMyApps 포털에 로그인 하면 응용 프로그램 테스트 | https://myapps.microsoft.com |

### <a name="considerations"></a>고려 사항

1. Hello 커넥터 회사 네트워크에 배치 하는 것이 좋습니다, 하는 동안 다음과 같은 경우 더 나은 성능을 hello 클라우드에 배치 하는 것이 표시 됩니다. 참고 항목: [Azure Active Directory 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항](application-proxy-network-topology-considerations.md)
2. 보안에 대한 자세한 내용과 아웃바운드 연결만 유지 관리하는 방식으로 특별히 안전한 원격 액세스 솔루션을 제공하는 방법은 [Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항](application-proxy-security-considerations.md)을 참조하세요.

## <a name="generic-ldap-connector-configuration"></a>일반 LDAP 커넥터 구성

시간 tooComplete 대략적인: 60 분

> [!IMPORTANT]
> 이 작업은 FIM/MIM 사용 경험이 요구되는 고급 구성입니다. 프로덕션에 사용되는 경우 이 구성에 대한 질문이 있으면 [프리미어 지원](https://support.microsoft.com/premier)을 참고하는 것이 좋습니다.

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 설치 및 구성된 Azure AD Connect | 문서 블록: [디렉터리 동기화 - 암호 해시 동기화](#directory-synchronization--password-hash-sync-phs--new-installation) |
| ADLDS 인스턴스 모임 요구 사항 | [일반 LDAP 커넥터 기술 참조: hello 일반 LDAP 커넥터 개요](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| 사용자가 사용 중인 작업 목록 및 이러한 작업과 연결된 특성 | [Azure AD Connect 동기화: tooAzure Active Directory 동기화 되는 특성](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 일반 LDAP 커넥터를 추가합니다. | [일반 LDAP 커넥터 기술 참조: 새 커넥터 만들기](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| 생성된 커넥터에 대한 실행 프로필을 만듭니다(전체 가져오기, 델타 가져오기, 전체 동기화, 델타 동기화, 내보내기) | [Create a Management Agent Run Profile](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)(관리 에이전트 실행 프로필 만들기)<br/> [커넥터를 사용 하 여 Azure AD Connect 동기화 서비스 관리자 hello로](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| 전체 가져오기 프로필을 실행하고 커넥터 공간에 개체가 있는지 확인합니다. | [Search for a Connector Space Object](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)(커넥터 공간 개체 검색)<br/>[커넥터를 사용 하 여 Azure AD Connect 동기화 서비스 관리자 hello로: 커넥터 공간 검색](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Metaverse의 개체에 작업에 필요한 특성이 포함되도록 동기화 규칙을 만듭니다. | [Azure AD Connect 동기화: hello 기본 구성 변경에 대 한 유용한: tooSynchronization 규칙 변경](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Azure AD Connect 동기화: 선언적 프로비전 이해](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect Sync: 선언적 프로비전 식 이해](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| 전체 동기화 주기를 시작합니다. | [Azure AD Connect 동기화: 스케줄러: hello 스케줄러를 시작 합니다.](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| 문제 발생 시 문제 해결을 수행합니다. | [TooAzure AD를 동기화 하는 개체 문제 해결](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| 확인, LDAP 사용자 수에 로그인 한 hello 응용 프로그램에 액세스 | https://myapps.microsoft.com |

### <a name="considerations"></a>고려 사항

> [!IMPORTANT]
> 이 작업은 FIM/MIM 사용 경험이 요구되는 고급 구성입니다. 프로덕션에 사용되는 경우 이 구성에 대한 질문이 있으면 [프리미어 지원](https://support.microsoft.com/premier)을 참고하는 것이 좋습니다.

## <a name="groups---delegated-ownership"></a>그룹 - 위임된 소유권

시간 tooComplete 대략적인: 10 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| SaaS 응용 프로그램(페더레이션 SSO 또는 암호 SSO)이 이미 구성됨 | 문서 블록: [SaaS 페더레이션 SSO 구성](#saas-federated-sso-configuration) |
| 액세스 toohello 응용 프로그램이 # 1에 할당 된 클라우드 그룹 식별 | 문서 블록: [SaaS 페더레이션 SSO 구성](#saas-federated-sso-configuration) <br/>[Azure Active Directory에서 그룹 만들기 및 구성원 추가](active-directory-groups-create-azure-portal.md) |
| Hello 그룹 소유자에 대 한 자격 증명을 사용할 수 있습니다 | [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md) |
| Hello 정보 작업자 앱에 액세스 hello에 대 한 자격 증명 확인 되었습니다. | [액세스 패널 hello 이란?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Toohello 응용 프로그램 액세스 권한이 있는 hello 그룹을 식별 하 고 지정 된 hello 소유자 구성 그룹| [Azure Active Directory에서 그룹에 대 한 hello 설정을 관리 합니다.](active-directory-groups-settings-azure-portal.md) |
| 그룹 소유자 hello로 로그인 액세스 패널의 그룹 탭에서 hello 그룹 구성원을 참조 하십시오 | [Azure Active Directory Groups Management page](https://account.activedirectory.windowsazure.com/r/#/groups)(Azure Active Directory 그룹 관리 페이지) |
| 원하는 tootest hello 정보 근로자를 추가 합니다. |  |
| Hello 정보 근로자, 즉 hello 타일의 사용 가능한 지 확인 | [액세스 패널 hello 이란?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>고려 사항

Hello 응용 프로그램에 사용 하도록 설정 하는 프로 비전 하는 경우에 필요할 수 toowait 몇 분 정도 hello toocomplete hello 정보 근로자 hello 응용 프로그램에 액세스 하기 전에 프로 비전 합니다.

## <a name="saas-and-identity-lifecycle"></a>SaaS 및 ID 수명 주기

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| SaaS 응용 프로그램(페더레이션 SSO 또는 암호 SSO)이 이미 구성됨 | 문서 블록: [SaaS 페더레이션 SSO 구성](#saas-federated-sso-configuration) |
| 액세스 toohello 응용 프로그램이 # 1에 할당 된 클라우드 그룹 식별 | 문서 블록: [SaaS 페더레이션 SSO 구성](#saas-federated-sso-configuration) <br/>[Azure Active Directory에서 그룹 만들기 및 구성원 추가](active-directory-groups-create-azure-portal.md) |
| Hello 정보 작업자 앱에 액세스 hello에 대 한 자격 증명 확인 되었습니다. | [액세스 패널 hello 이란?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 제거 hello 그룹 hello 앱에서 hello 사용자가 너무 할당| [Azure Active Directory 테넌트의 사용자에 대한 그룹 멤버 자격 관리](active-directory-groups-members-azure-portal.md) |
| 프로비전이 해제되는 동안 몇 분 정도 기다립니다. | [Azure AD에서 SaaS 앱 사용자를 자동으로 프로비전: 자동 프로비전은 어떻게 수행되나요?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| 별도 브라우저 세션에서 hello 정보 작업자 toomy 앱 포털에 로그인 하 고 누락 된 해당 타일 확인 | http://myapps.microsoft.com |


### <a name="considerations"></a>고려 사항

Hello PoC 시나리오 tooleavers 및/또는 병가 시나리오를 추정 합니다. Hello 사용자 가져옵니다 사용할 수 없는 경우 온-프레미스 AD 제거는 더 이상 방식으로 toolog toohello SaaS 응용 프로그램에서에서 또는 합니다.

## <a name="self-service-access-tooapplication-management"></a>셀프 서비스 액세스 tooApplication 관리

시간 tooComplete 대략적인: 10 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| Hello 보안 그룹의 일부로 액세스 toohello 응용 프로그램을 요청 하는 POC 사용자 식별 | 문서 블록: [SaaS 페더레이션 SSO 구성](#saas-federated-sso-configuration) |
| 배포된 대상 응용 프로그램 | 문서 블록: [SaaS 페더레이션 SSO 구성](#saas-federated-sso-configuration) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Azure AD 관리 포털에서 tooEnterprise 응용 프로그램 블레이드로 이동 | [Azure AD Management Portal: Enterprise Applications](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/)(Azure AD 관리 포털: 엔터프라이즈 응용 프로그램) |
| 셀프 서비스를 사용하여 필수 구성 요소에서 응용 프로그램 구성 | [Azure Active Directory의 새로운 엔터프라이즈 응용 프로그램 관리 기능: 셀프 서비스 응용 프로그램 액세스 구성](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Hello 정보 작업자 toomy 앱 포털에 로그인 | http://myapps.microsoft.com |
| 확인 "+ 앱 추가" hello 페이지의 op 단추입니다. Tooget 액세스 toohello 앱 사용 |  |

### <a name="considerations"></a>고려 사항

hello 응용 프로그램 선택 toohello 응용 프로그램을 즉시 이동 몇 가지 오류가 발생할 수 있으므로 요구 사항, 프로 비전 있을 수 있습니다. Azure ad와 프로비저닝을 지원 하 여 hello 응용 프로그램을 선택 하 고 구성 되어 있는 경우는 영업 기회 tooshow hello 전체 흐름 끝 tooend 작업으로이 사용할 수 있습니다. Hello 문서 블록에 대 한 참조 [SaaS 페더레이션 SSO 구성](#saas-federated-sso-configuration) 추가 권장 사항은

## <a name="self-service-password-reset"></a>셀프 서비스 암호 재설정

시간 tooComplete 대략적인: 15 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 테넌트에서 셀프 서비스 암호 관리 사용. | [IT 관리자에 대한 Azure Active Directory 암호 재설정](active-directory-passwords.md) |
| 온-프레미스에서 암호 쓰기 저장 toomanage 암호를 사용 합니다. 이 작업에는 특정 Azure AD Connect 버전이 필요합니다. | [암호 쓰기 저장 필수 구성 요소](active-directory-passwords-writeback.md) |
| 이 기능을 사용 하 고 보안 그룹의 구성원 인지 확인는 여부를 지정 하는 hello PoC 사용자를 식별 합니다. hello 사용자가 관리자가 아닌 사용자 toofully 쇼케이스 hello 기능 여야 합니다. | [Azure AD 암호 관리 사용자 지정:: toopassword 재설정 액세스 제한](active-directory-passwords-writeback.md) |


### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 탐색 tooAzure AD 관리 포털: 암호 재설정 | [Azure AD Management Portal: Password Reset](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)(Azure AD 관리 포털: 암호 재설정) |
| Hello 암호 재설정 정책을 결정 합니다. POC 목적으로 사용할 수 있습니다 전화 통화 및 질문과 대답 Tooenable 등록 toobe tooaccess 패널에는 로그에 필요한 것이 좋습니다. |  |
| 로그아웃하고 정보 근로자로 로그인합니다. |  |
| 2 단계 당 구성 된 대로 hello 셀프 서비스 암호 재설정 데이터를 제공 합니다. | http://aka.ms/ssprsetup |
| 닫기 hello 브라우저 |  |
| 4 단계에서 사용한 hello 정보 근로자 hello 로그인 프로세스를 다시 시작 |  |
| Hello 암호 재설정 | [고유 암호 업데이트: 내 암호 재설정](active-directory-passwords-update-your-own-password.md) |
| Tooon 온-프레미스 리소스 뿐만 아니라 새 암호 tooAzure AD에 로그인을 하십시오. |  |

### <a name="considerations"></a>고려 사항

1. 되는 경우 Azure AD Connect 업그레이드 hello toocause 마찰, 그런 다음 클라우드 계정에 대해 사용 하는 것이 좋습니다 하거나 별도 환경에 대 한 데모 확인
2. hello 관리자는 다른 정책을 사용 하 여 고 admin 님 안녕하세요 계정 tooreset hello 암호 될 수 있습니다 hello PoC 테 혼동 합니다. 일반 사용자 계정 tootest hello 재설정 작업을 사용 하면


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>전화로 Azure Multi-Factor Authentication

시간 tooComplete 대략적인: 10 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| MFA를 사용할 POC 사용자 식별  |  |
| MFA 챌린지를 위한 수신 상태가 좋은 전화  | [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 너무 이동 Azure AD 관리 포털에서 "사용자 및 그룹" 블레이드 | [Azure AD Management Portal: Users and groups](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/)(Azure AD 관리 포털: 관리 포털) |
| “모든 사용자” 블레이드를 선택합니다. |  |
| Hello 상단의 표시줄 단추 선택 "Multi-factor Authentication"에서 | Azure MFA 포털의 직접 URL: https://aka.ms/mfaportal |
| Hello "User" 설정에 hello PoC 사용자를 선택 하 고 MFA에 대해 사용 하도록 설정 | [Azure Multi-Factor Authentication의 사용자 상태](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Hello 증명 프로세스를 안내 하 고 hello PoC 사용자로 로그인  |  |

### <a name="considerations"></a>고려 사항

1. 사용자에 대 한 모든 로그인에 MFA를 명시적으로 설정 하는이 문서 블록의 hello PoC 단계. 더 많은 대상 시나리오에서 MFA를 적용하는 ID 보호 및 조건부 액세스와 같은 다른 도구가 있습니다. 값이 됩니다 tooconsider POC tooproduction에서 이동할 때.
2. 이 문서 블록의 hello PoC 단계 전화 통화를 사용 하 여 hello expedience MFA 방법으로 명시적으로 됩니다. POC tooproduction에서으로 전환 하는 대로 hello와 같은 응용 프로그램을 사용 하는 것이 좋습니다 [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) 가능 하면 두 번째 요소로 합니다.
참고 항목: [DRAFT NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)(DRAFT NIST 특별 간행물 800-63B)

## <a name="mfa-conditional-access-for-saas-applications"></a>SaaS 응용 프로그램에 대한 MFA 조건부 액세스

시간 tooComplete 대략적인: 10 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| PoC 사용자 tootarget hello 정책을 식별 합니다. 이러한 사용자 보안 그룹 tooscope hello 조건부 액세스 정책에 있어야 합니다. | [SaaS 페더레이션된 SSO 구성](#saas-federated-sso-configuration) |
| SaaS 응용 프로그램이 이미 구성됨 |  |
| PoC 사용자가 이미 toohello 응용 프로그램 할당 |  |
| 사용할 수 있는 자격 증명 toohello POC 사용자 |  |
| POC 사용자가 MFA에 등록됨. 수신 상태가 좋은 전화 사용 | http://aka.ms/ssprsetup |
| Hello 내부 네트워크의 장치입니다. Hello 내부 주소 범위에 구성 된 IP 주소 | IP 주소 찾기: https://www.bing.com/search?q=what%27s+my+ip |
| Hello (hello 통신 회사의 모바일 네트워크를 사용 하 여 전화 수 있음)는 외부 네트워크의 장치 |  |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 이동 tooAzure AD 관리 포털: 조건부 액세스 블레이드 | [Azure AD Management Portal: Conditional Access](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)(Azure AD 관리 포털: 조건부 액세스) |
| 조건부 액세스 정책을 만듭니다.<br/>- “사용자 및 그룹”에서 PoC 사용자를 대상으로 지정합니다.<br/>- “클라우드 앱”에서 PoC 응용 프로그램을 대상으로 지정합니다.<br/>- “조건” -> “위치”에서 신뢰할 수 있는 위치를 제외한 모든 위치를 대상으로 지정합니다. **참고:** 신뢰할 수 있는 IP는 [MFA Portal](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)(MFA 포털)에서 구성됩니다.<br/>- “권한 부여”에서 다단계 인증이 필요합니다. | [Azure Active Directory에서 조건부 액세스 시작: 정책 구성 단계](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| 회사 네트워크 내부에서 응용 프로그램에 액세스합니다. | [Azure Active Directory의 조건부 액세스 시작: 테스트 hello 정책](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| 공용 네트워크에서 응용 프로그램에 액세스합니다. | [Azure Active Directory의 조건부 액세스 시작: 테스트 hello 정책](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>고려 사항

페더레이션을 사용 하는 경우 클레임 상태 회사 네트워크 내/외부 hello 온-프레미스 Id 공급자 (IdP) toocommunicate hello를 사용할 수 있습니다. 복잡 한 tooassess 수 및 대규모 조직에서 관리할 수 있는 IP 주소의 toomanage hello 목록이 필요 없이이 기법을 사용할 수 있습니다. 설정 된 환경에서 hello "network 로밍" 시나리오 (예: 커피숍 위치 하는 동안 로그인된 스위치 및 hello 내부 네트워크에 로그온 하는 사용자)에 대 한 계정 및 hello 의미를 이해 해야 합니다. 참고 항목: [Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안 유지: 페더레이션 사용자를 위한 신뢰할 수 있는 IP](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>PIM(Privileged Identity Management)

시간 tooComplete 대략적인: 15 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| PIM에 대 한 POC hello의 일부가 될 글로벌 admin 님 안녕하세요 식별 | [Azure AD Privileged Identity Management 시작](active-directory-privileged-identity-management-getting-started.md) |
| Hello 보안 관리자 역할을 할 글로벌 admin 님 안녕하세요 식별 | [Azure AD Privileged Identity Management 시작](active-directory-privileged-identity-management-getting-started.md)<br/> [Azure Active Directory PIM의 다른 관리자 역할](active-directory-privileged-identity-management-roles.md) |
| 선택 사항: hello 전역 관리자 전자 메일을 가질 경우 확인 PIM에서 전자 메일 알림을 tooexercise 액세스 | [Azure AD Privileged Identity Management 란?: hello 역할 활성화 설정을 구성 합니다.](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 전역 관리자 (GA) 및 부트스트랩 hello PIM 블레이드로 toohttps://portal.azure.com 로그인 합니다. 이 단계를 수행 하는 전역 관리자 hello hello 보안 관리자 권한으로 마련 됩니다.  이 행위자 GA1을 호출해 보겠습니다. | [Hello 보안 마법사를 사용 하 여 Azure AD Privileged Identity Management에](active-directory-privileged-identity-management-security-wizard.md) |
| 전역 admin 님 안녕하세요 식별 영구 tooeligible에서 이동 합니다. 이 이해 하기 쉽도록 1 단계에서 사용 되는 hello에서 별도 관리자 여야 합니다. 이 행위자 GA2를 호출해 보겠습니다. | [Azure AD Privileged Identity Management: 어떻게 tooadd 또는 사용자 역할 제거](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[Azure AD Privileged Identity Management 란?: hello 역할 활성화 설정을 구성 합니다.](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| 이제 GA2 toohttps://portal.azure.com으로 로그인 하 고 "사용자 설정"을 변경 하세요. 일부 옵션이 회색으로 표시되는 것을 알 수 있습니다. | |
| Hello 및 새 탭에서 동일한 세션 3, 실행 함에 따라 이제 toohttps://portal.azure.com 이동한 hello PIM 블레이드 toohello 대시보드를 추가 합니다. | [어떻게 tooactivate 또는 역할에 Azure AD Privileged Identity Management 비활성화 하려면: hello Privileged Identity Management 응용 프로그램 추가](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| 요청이 활성화 toohello 전역 관리자 역할 | [어떻게 tooactivate 또는 역할에 Azure AD Privileged Identity Management 비활성화 하려면: 역할 활성화](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| GA2가 MFA에 등록한 적이 없는 경우에는 Azure MFA에 대한 등록이 필요합니다. |  |
| 3 단계에서 원래 탭 toohello 돌아가서 hello hello 브라우저 새로 고침 단추를 클릭 하십시오. 이제이 있는 액세스 toochange "사용자 설정" note | |
| 필요에 따라 하거나 전역 관리자가 사용 하도록 설정 하는 전자 메일 수 GA1 및 GA2의 받은 편지함을 확인 hello 알림이 활성화 되 고 hello 역할의 표시 |  |
| 8은 hello 감사 내역을 확인 하 고 GA2 hello 보고서 tooconfirm hello 상승 표시 된 것을 관찰 합니다. | [Azure AD Privileged Identity Management란?: 역할 활동 검토](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>고려 사항

이 기능은 Azure AD Premium P2 및/또는 EMS E5에 포함됩니다.

## <a name="discovering-risk-events"></a>위험 이벤트 검색

시간 tooComplete 대략적인: 20 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| Tor 브라우저가 다운로드 및 설치된 장치 | [Download Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads)(Tor 브라우저 다운로드) |
| 액세스 tooPOC 사용자 toodo hello 로그인 | [Azure Active Directory ID 보호 플레이 북](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| Tor 브라우저를 엽니다. | [Download Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads)(Tor 브라우저 다운로드) |
| Toohttps://myapps.microsoft.com hello POC 사용자 계정으로 로그인 | [Azure Active Directory ID 보호 플레이 북: 위험 이벤트 시뮬레이트](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| 5~7분 정도 기다립니다. |  |
| 전역 관리자 toohttps://portal.azure.com으로 로그인 하 고 hello Identity Protection 블레이드를 열고 | https://aka.ms/aadipgetstarted |
| 위험 이벤트 블레이드 열기 hello 합니다. “익명 IP 주소에서 로그인” 아래에 있는 항목을 확인해야 합니다.  | [Azure Active Directory ID 보호 플레이 북: 위험 이벤트 시뮬레이트](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>고려 사항

이 기능은 Azure AD Premium P2 및/또는 EMS E5에 포함됩니다.

## <a name="deploying-sign-in-risk-policies"></a>로그인 위험 정책 배포

시간 tooComplete 대략적인: 10 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| Tor 브라우저가 다운로드 및 설치된 장치 | [Download Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads)(Tor 브라우저 다운로드) |
| 테스트를 POC 사용자 toodo hello 로그 액세스 |  |
| POC 사용자가 MFA에 등록됨. 있는지 toouse आ स ा 좋은 설치 된 휴대폰 확인 | 문서 블록: [전화로 Azure Multi-Factor Authentication](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| 전역 관리자 toohttps://portal.azure.com으로 로그인 하 고 hello Identity Protection 블레이드를 여세요 | https://aka.ms/aadipgetstarted |
| 다음과 같이 로그인 위험 정책을 사용하도록 설정합니다.<br/>- 할당 대상: POC 사용자<br/>- 조건: 로그인 위험 중간 이상(익명 위치에서 로그인을 중간 위험 수준으로 간주함)<br/>- 컨트롤: MFA 필요 | [Azure Active Directory ID 보호 플레이 북: 로그인 위험](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Tor 브라우저를 엽니다. | [Download Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads)(Tor 브라우저 다운로드) |
| Toohttps://myapps.microsoft.com hello PoC 사용자 계정으로 로그인 |  |
| 공지 hello MFA 챌린지 | [Azure AD ID 보호를 사용하는 로그인 환경: 위험한 로그인 복구](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>고려 사항

이 기능은 Azure AD Premium P2 및/또는 EMS E5에 포함됩니다. 위험 이벤트에 대 한 자세한 방문 toolearn: [Azure Active Directory 위험 이벤트](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>인증 기반 인증서 구성

시간 toocomplete 대략적인: 20 분

### <a name="pre-requisites"></a>필수 조건

| 필수 구성 요소 | 리소스 |
| --- | --- |
| 엔터프라이즈 PKI에서 사용자 인증서가 프로비전된 장치(Windows, iOS 또는 Android) | [사용자 인증서 배포](https://msdn.microsoft.com/library/cc770857.aspx) |
| ADFS를 통해 페더레이션된 Azure AD 도메인 | [Azure AD Connect 및 페더레이션](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Active Directory 인증서 서비스 개요](https://technet.microsoft.com/library/hh831740.aspx)|
| iOS 장치의 경우 Microsoft Authenticator 앱이 설치됨 | [Hello Microsoft Authenticator 앱 시작](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>단계

| 단계 | 리소스 |
| --- | --- |
| ADFS에서 “인증서 인증”을 사용하도록 설정합니다. | [인증 정책 구성: tooconfigure 기본 인증 Windows Server 2012 r 2에서 전체적으로](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| 선택 사항: Azure AD에서 Exchange Active Sync 클라이언트에 대해 인증서 인증을 사용하도록 설정합니다. | [Azure Active Directory에서 인증서 기반 인증 시작](active-directory-certificate-based-authentication-get-started.md) |
| TooAccess 패널을 이동 하 고 사용자 인증서를 사용 하 여 인증 | https://myapps.microsoft.com |

### <a name="considerations"></a>고려 사항

이 배포의 제한 사항에 대 한 자세한 방문 toolearn: [ADFS: Azure AD와 인증서 인증 & Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> 사용자 인증서 소유는 보호되어야 합니다. 장치를 관리하거나 스마트 카드의 경우 PIN을 사용합니다.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
