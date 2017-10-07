---
title: "작업 공간에서 aaaUsing Windows 10 장치 | Microsoft Docs"
description: "사용자에 대 한 기능에 대 한 스냅숏을 제공 및 IT, 대비 hello 다른 방법으로 장치를 프로 비전 하 고 Windows 10과 기업에서 사용 될 수 있습니다."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>작업 공간에서 Windows 10 장치 사용
적용 대상: Windows 10 PC

Windows 10에서는 안전 하 고 편리한 방식으로 사용자가 tooaccess 작업 리소스를 사용 하는 조직에 대 한 세 가지 모델을 제공 합니다.

* **Azure Active Directory Join** (Azure AD Join) hello 클라우드에서 기본적으로 Office 365 등의 리소스에 액세스 하는 작업자에 대 한 합니다. Azure AD 조인은 Windows 10의 새로운 환경을 프로비전하는 셀프 서비스 작업입니다.
* **도메인 가입**: 온-프레미스 앱 및 리소스에 투자하는 조직용. 도메인 가입은 연결 된 경우 Windows 10에서 향상 된 환경을 제공 tooAzure AD 합니다.
* **새 BYOD 환경을 단순화**tooadd 작업 하려는 사용자 계정 또는 tooWindows 학교 및 개인 장치에서 리소스를 쉽게 액세스에 대 한 합니다.

hello 다음 표에 대 한 스냅숏을 제공 사용자와 hello 다른 방법으로 장치를 프로 비전 하 고 Windows 10과 기업에서 사용 될 수 대비 되는 IT 관리자에 대 한 기능:

|  | 도메인 가입 | Azure AD 조인 | 개인 장치 |
| --- | --- | --- | --- |
| 회사 또는 학교 계정을 위한 Windows 장치 로그인 |예 |예 |아니요 |
| 사용자 single sign-on (SSO) tooOffice 365 및 Azure AD 응용 프로그램. SSO는 한 번만 tooaccess 조직 리소스에 hello 기능 toosign 합니다. |예 |예 |예 |
| 사용자 SSO tooKerberos/NTLM 응용 프로그램입니다. |예 |제한 |예, VPN을 통해 |
| Microsoft Passport 및 Windows Hello를 사용하는 회사 또는 학교 계정에 대한 강력한 권한 부여 및 손쉬운 로그인 |예 |예 |예 |
| 회사 또는 학교 계정 (Microsoft 계정)으로 tooenterprise Windows 스토어에 액세스 합니다. |예 |예 |예 |
| 회사 또는 학교 계정을 사용하여 장치 간 사용자 설정을 로밍하는 엔터프라이즈 규정 준수 |예 |예 |예 |
| hello 기능 toorestrict 액세스 tooorganizational 앱 toodevices 조직 장치 정책을 준수 하는 합니다. |예 |예 |예 |
| "어디에서나 작업"에 대한 장치의 사용자 셀프 서비스 프로비전 |아니요 |예 |예 |
| 기능 toomanage 장치입니다. |예, GP/SCCM을 통해 |예 |예 |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Windows 10에서 Azure AD 조인 및 도메인 가입된 회사 소유의 장치 사용
Windows 10에는 작업 소유 장치 tooaccess 작업 리소스에 대 한 두 가지 방법을 제공 합니다.

* Azure AD 조인
* 도메인 가입
  
  모두 조직의 필요 및 요구 사항에 따라 유효한 옵션일 수 있습니다. 경우에 따라 조직이 배포하는 두 방법을 모두 설정하면 장점을 활용할 수 있습니다.

## <a name="when-toouse-azure-active-directory-join"></a>Azure Active Directory 가입 하는 toouse 경우
Azure AD 조인은 Windows 10의 환경을 프로비전하는 새로운 셀프 서비스 작업입니다.  Hello 클라우드에서 기본적으로 Office 365 등의 작업 리소스에 액세스 하는 작업자를 목표로 합니다. 간단한 방법을 tooconfigure 컴퓨터, 태블릿, 이며 hello 엔터프라이즈에 대 한 전화 합니다. 장치는 Windows 플랫폼 전반에 걸쳐 일관된 제어를 사용하여 모바일 장치 관리를 통해 관리됩니다.

**다음의 이유로 Azure AD 조인 사용**:

* Tooenable hello에 대 한 작업자에 대 한 장치 hello 프로비저닝 셀프 서비스 하는 것이 좋습니다.
* 사용자에게 태블릿 및 휴대폰과 같은 회사 소유의 모바일 장치를 제공합니다.
* 원하는 toomanage 사용자 집합에 Active Directory에 대신 Azure AD에서 계절별 직원, 하청 업체 또는 학생 등입니다.
* 제한 된 온-프레미스 인프라와 원거리 지사 사무실의 조인 기능 tooworkers를 tooprovide 사용 하는 것이 좋습니다.
* 온-프레미스 Active Directory가 없습니다.

일부 조직에서는 Azure AD Join을 사용 hello 기본적인 방법은 toodeploy 작업 소유 장치, 전체 또는 대부분의 리소스 toohello 클라우드를 마이그레이션할 때 특히. 하이브리드 조직 Active Directory와 Azure AD에 hello 사용자 또는 부서에 따라 toodeploy 한 가지 방법은 또는 다른 선택 되는 수 있습니다.

예를 들어, 학군 및 대학교는 직원은 Active Directory에서, 학생은 Azure AD에서 관리할 수 있습니다. 일부 회사는 Azure AD에서 toomanage 원격 사무실 또는 판매 부서 할 수도 있습니다. Azure AD 조인 및 도메인 가입 메서드는 모두 하이브리드 조직 내에서 사용할 수 있습니다. Azure AD 조인 작업 환경에서 장치를 배포 하기 위한 훌륭한 보수 toodomain 조인 될 수 있습니다.

**조직 수 하는 경우 추가 혜택을 이용할 수 hello 클라우드를 통해 hello 가장 일반적인 tooenterprise 리소스에 액세스할 경우**:

* 온-프레미스 ID 인프라에 대한 종속성을 제거할 수 있습니다.
* 이미징 솔루션에서 벗어나 셀프 서비스를 구성하여 장치 배포 모델을 간소화할 수 있습니다.
* 다른 플랫폼에서 모바일 장치 관리 toomanage 모든 장치를 사용할 수 있습니다.

Azure AD Join에 대 한 자세한 내용은 참조 [기능 tooWindows 10 장치의 Azure Active Directory Join을 통해 클라우드 확장](active-directory-azureadjoin-overview.md)합니다.

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Toouse 도메인 가입 하는 경우 (또는 계속 사용)
Hello에 대 한 마지막 15 년 대부분의 조직에서는 사용한 도메인 가입 tooconnect 작업 장치입니다. 사용자가 toosign 사용 하면 자신의 Active Directory를 사용 하 여 tootheir 장치에서 직장 이나 학교 계정을 합니다. 도메인 가입에서는 IT toocentrally 및 완벽 하 게 이러한 장치를 관리 합니다. 조직은 일반적으로 이미징 메서드 tooprovision 장치에 의존 하 고 종종 toomanage SCCM System Center Configuration Manager () 또는 그룹 정책 (GP)를 사용 하 여 해당 합니다.

**다음의 이유로 인해 엔터프라이즈에서 도메인 가입(또는 계속 사용)을 사용합니다**.

* NTLM/Kerberos를 사용 하는 Win32 앱 배포 toothese 장치 해야 합니다.
* GP 또는 SCCM/DCM toomanage 장치 필요합니다.
* 직원에 게 toocontinue toouse 이미징 솔루션 tooconfigure 장치 원하는합니다.

**또한 제공 도메인 가입 Windows 10에서 hello 다음을 활용 하는 경우 연결 tooAzure AD**:

* Microsoft Passport 및 Windows Hello를 사용하는 회사 또는 학교 계정에 대한 강력한 장치 바인딩된 인증 및 손쉬운 로그인
* 회사 또는 학교 계정 (Microsoft 계정이 필요) 사용 하는 장치에 대 한 toohello enterprise Windows 스토어에 액세스 합니다.
* 회사 또는 학교 계정을 사용하는 장치 간 사용자 설정의 엔터프라이즈 규격 로밍(Microsoft 계정 필요 없음)
* hello 기능 toorestrict 액세스 tooorganizational 앱 toodevices 조직 장치 정책을 준수 하는 합니다.

Azure AD Join에 대 한 자세한 내용은 참조 [기능 tooWindows 10 장치의 Azure Active Directory Join을 통해 클라우드 확장](active-directory-azureadjoin-overview.md)합니다.

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>회사 또는 학교용으로 개인 소유한 장치의 가입 사용
작업 또는 학교 계정 tootheir 컴퓨터, 태블릿 또는 휴대폰 hello enterprise, Windows 10에서에서 BYOD toosupport hello 사용자 hello 기능 tooadd를 제공합니다. Hello 후 사용자는 회사를 추가 하거나 hello 장치 학교 계정이 Azure AD에 등록 되 고 필요에 따라 hello 구성 하는 hello 모바일 장치 관리 시스템에 등록 합니다. hello 디렉터리 '등록 된' vs로 이러한 장치를 표시 됩니다. ‘Azure AD 조인된’으로 표시합니다. IT 관리자는 이 정보를 기반으로 다른 정책을 적용할 수 있으며 원하는 경우 회사 소유의 장치 보다 개인 소유의 장치에 맑은 터치를 제공합니다.

사용자는 작업을 추가 하거나 계정 tootheir 개인 장치를 매우 편리 하 게 학교 수 있습니다. 이 작업은 작업 응용 프로그램 hello에 대 한 처음으로 액세스 하는 경우 또는 hello 설정 메뉴를 통해 수동으로 할 수 있습니다. 이 계정은 SSO tooorganizational 리소스를 제공 합니다.

Azure AD Join에 대 한 자세한 내용은 참조 [발생 하는 Windows 10에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)합니다.

## <a name="enable-domain-join-or-azure-ad-join"></a>도메인 가입 또는 Azure AD 조인 사용
앞에서 설명한 모든 메서드에 (도메인 가입, Azure AD 조인 및 추가 회사 또는 학교 계정) 진입점 hello Windows 10 사용자 환경에 있어야 합니다. 그러나이 모든에 hello 인프라에는 IT 관리자 tooenable hello 기능 hello 경험을 사용 하려면 필요 합니다.

## <a name="requirements-for-deploying-azure-ad-join"></a>Azure AD 조인 배포를 위한 요구 사항
모든 사용자 집합에 대해 Azure AD Join toodeploy 다음 hello가 필요 합니다.

* Azure AD 구독
* 더 많은 기능이 필요한 경우 모바일 장치 관리 자동 등록과 같은 Azure AD Premium 구독
* 모바일 장치 관리-예: Microsoft Intune 구독, Office 365 용 모바일 장치 관리 또는 Azure AD와 통합 하는 hello 파트너 모바일 장치 관리 공급 합니다. (참조 hello [FAQ 섹션](#frequently-asked-questions) hello에 대 한 자세한 내용은이 문서의 끝에).

시설 하이브리드 인 Azure AD Connect tooextend hello 온-프레미스 디렉터리 tooAzure AD를 배포 하는 것이 좋습니다.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Azure AD에 도메인 가입을 사용하기 위한 요구 사항
도메인 가입을 항상가지고 toowork를 계속 합니다. 그러나 tooget hello Azure AD 이점이 필요 합니다를 수행 하는 hello.

* Azure AD 구독
* Azure AD Connect tooextend hello 온-프레미스 디렉터리 tooAzure 광고의 배포 서비스가 있습니다.
* 도메인에 가입 된 장치 toohave 조건부 액세스 tooAzure AD 허용 하는 정책입니다.
* 일부 장치에 대 한 toobe 수 toorestrict 액세스 하려는 경우 장치 너무 "도메인에 가입 된" 액세스를 허용 하는 정책입니다.
* System Center Configuration Manager 버전 1509 기술 미리 보기에서는 tooenable 규칙에 대 한 규격 장치를 요구 합니다. (TechNet 설명서 hello 및 블로그 게시물 참조).

도메인 가입 Windows 10에 대 한 자세한 내용은 참조 하세요. [발생 하는 Windows 10에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>BYOD 및 "회사 또는 학교 계정 추가" 사용을 위한 요구 사항
tooenable "bring your own device" (BYOD) hello 다음 회사 또는 학교 계정을 사용 해야 합니다.

* Azure AD 구독
* 더 많은 기능이 필요한 경우 모바일 장치 관리 자동 등록과 같은 Azure AD Premium 구독

## <a name="requirements-for-using-microsoft-passport"></a>Microsoft Passport 사용을 위한 요구 사항
Microsoft Passport tooenable hello 다음이 필요 합니다.

* Microsoft Passport를 사용하는 인증서 기반 인증 지원을 위한 PKI(공개 키 인프라)
* Azure AD 조인 및 회사 또는 학교 계정에 Microsoft Passport를 사용하는 인증서 기반 인증 지원을 위한 Intune 구독
* System Center Configuration Manager Technical Preview 버전 1509 (TechNet 설명서 hello 및 블로그 게시물 참조) Microsoft Passport를 사용 하 여 도메인 가입에 대 한 인증서 기반 인증 지원에 대 한 합니다.
* Hello 조직에서 Microsoft Passport를 사용 하기 위한 정책입니다.

대체 toousing PKI로 hello 다음을 수행 하 여 Microsoft Passport 키 기반를 설정할 수 있습니다.

* Windows Server 2016 "프로덕션 미리 보기 1" DC를 배포합니다(도메인 또는 포리스트 기능 수준이 필요하지 않습니다. 각 Active Directory 사이트를 제공하는 중복성에 대한 여러 DC).
* Hello 조직의 정책 tooenable Microsoft Passport를 설정 합니다.

Windows 10에서 Microsoft Passport 및 Windows Hello에 대한 자세한 내용은 <link-to-MS-Passport-and-Windows-Hello-document>을(를) 참조하세요.

## <a name="frequently-asked-questions"></a>질문과 대답
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Azure AD와 통합되는 파트너 모바일 장치 관리 제품은 무엇인가요?
hello 다음 공급 업체 제품 Azure AD와 통합 통합된 등록 및 Windows 10에서 조건부 액세스:

* AirWatch by VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* SOTI 온-프레미스 모바일 장치 관리
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Windows 10에서 작업 공간 가입은 어떠나요?
작업 공간 연결에 Windows 8.1 tooenable BYOD에에서 사용 되었습니다. Windows 10에서 BYOD는 이 문서의 앞부분에서 설명한 대로 "회사 또는 학교 계정 추가"를 통해 활성화됩니다. Azure AD와의 모바일 장치 관리를 통합 하지 않는 조직에 대 한 사용자가 장치를 등록 하려면 hello를 통해 수동으로 관리 **설정** > **계정**  >  **회사 액세스**합니다.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>사용자가 Windows 10에서 자신의 Microsoft 계정 tootheir 도메인 계정에 연결할 수 있습니까?
10 Windows에서는 안됩니다. Windows 8.1 사용자의 도메인에 가입 된 장치 수 "연결" 자신의 Microsoft 계정 (예: Hotmail, Live, Outlook, Xbox, 등) tootheir 도메인 계정 tooenable SSO tooLive 서비스, hello Windows 스토어의 사용 및의 로밍와 같은 특정 환경을 장치에서 사용자 설정입니다. Windows 10에서 Microsoft 계정을 "연결" 기능 hello는 만료 되었습니다. hello 사용자 서비스로 추가 계정 tooenable SSO tooconsumer hello Windows 스토어와 같은 Microsoft 계정을 하나 이상 추가할 수 있습니다. **설정** > **계정** > **계정**에서 수행됩니다.

Windows 8.1 도메인 가입 장치에서 업그레이드 하는 사용자 및 사용자가 Microsoft 계정을 연결 된 사용자, 됩니다 자동으로 연결 된 Microsoft 계정으로 추가한 toohello 목록이 추가 계정 사용 합니다.

## <a name="additional-information"></a>추가 정보
* [Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

