---
title: "Azure Active Directory Join을 통해 aaaExtending 클라우드 기능 10 tooWindows 장치 | Microsoft Docs"
description: "Windows 10 장치의 Azure Active Directory에 등록 된 Azure AD Join tooget 사용 방법을 한 세부적인된 개요를 제공 합니다."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.
## <a name="what-is-azure-active-directory-join"></a>Azure Active Directory 조인이란?
Azure Active Directory Join (Azure AD 조인)은 hello 장치의 Azure Active Directory tooenable 중앙 관리에서 회사 소유 장치를 등록 하는 hello 기능입니다. 사용 하면 사용자가 Azure Active Directory를 통해 직원 및 학생 tooconnect toohello 엔터프라이즈 클라우드 등입니다. 이 통해 간단한 Windows 배포 및 액세스 tooorganizational 앱 및 모든 Windows 장치에서 리소스를 둘 다 회사 소유 및 개인 소유 (BYOD).

Azure AD 조인은 클라우드 우선/클라우드 전용인 기업(일반적으로 온-프레미스 Windows Server Active Directory 인프라가 없는 중소 규모 기업)을 위한 것입니다. 기존 도메인 가입 (모바일 장치, 예:),이 따른 또는 사용자에 게 주로 tooaccess Office 365 또는 Azure AD와 통합 하는 다른 SaaS 앱에 대 한 지원 되지 않는 장치에서 큰 조직에서 언급, Azure AD 조인 수 및이 사용 합니다.

Hello 기존의 도메인 가입 hello를 계속 제공 하지만 최상의 온-프레미스 발생할 수 있는 도메인에 가입 된 장치에서 Azure AD 조인이 없는 도메인 가입 장치에 적합 합니다. Azure AD 조인 hello 클라우드에 있는 사용자를 관리 하기 위한 적절 한 이기도 합니다. 그룹 정책 및 SCCM(System Center Configuration Manager)과 같은 기존의 도메인 관리 도구를 사용하는 대신 모바일 장치 관리 기능을 사용하여 수행합니다.

![온-프레미스 Active Directory 및 Azure AD와 개인 장치 및 회사 장치 개요](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>기업에서 Azure AD 조인을 채택해야 하는 이유는 무엇인가요?
* **기업에 주로 않은 hello 클라우드**: 이동 하거나 온-프레미스 공간 저하 되 고 지정 하 고 원하는 toooperate hello 클라우드에서 자세한 tooa 모델을 이동 하는 경우 Azure AD Join 이용할 수 있습니다. Azure AD 계정을 수동으로 또는 온-프레미스 Active Directory 동기화를 통해 만들었을 수 있습니다. 어떤 방법을 사용 하 여 계정이 Azure ad에서 및 tooWindows 10에서에서 toosign 사용할 수 있습니다. 사용자가 자신의 컴퓨터 tooAzure AD (OOBE) 중 하나가 hello 기본적으로 환경을 통해 또는 hello 설정 메뉴를 통해 연결할 수 있습니다. 을 조인한 후 사용자가 single sign on (SSO) toocloud 리소스에 액세스 Office 365와 같은 Office 응용 프로그램 또는 브라우저에서 이용할 수는 있습니다.
* **교육 기관**: 자주에 대 한 받고 hello 시나리오 중 하나는 교육 기관 두 사용자가 있는: 교직원 및 학생 들 합니다. 교직원 온-프레미스 계정을 만들어 바람직한 이므로 hello 조직의 장기적인 구성원이 간주 됩니다. 하지만 학생 hello 조직의 shorter-term 구성원이 고 따라서 Azure AD에서 관리할 수 있습니다. 이 디렉터리 눈금 저장된 온-프레미스 대신 toohello 클라우드를 처리할 수 있는 것을 의미 합니다. 또한 학생 tooWindows 자신의 Azure AD 계정에 로그인 하 고 Office 응용 프로그램 또는 브라우저에 대 한 액세스 tooOffice 365 리소스를 가져올 수 의미 합니다.
* **소매 업체**: म 들었습니다에 대 한 고객의 또 다른 시나리오는 해당 desire toomanage 계절별 작업자 보다 쉽게 합니다.  역시, 장기적인 정규직 직원을 위한 계정은 보통 도메인에 연결된 컴퓨터에 온-프레미스 계정으로 만들어집니다. 하지만 계절별 작업자 shorter-term의 멤버인 hello org 바람직한 toomanage 되기 때문에 있는 사용자 라이선스를 더 쉽게 이동할 수 있습니다. Office 365 라이선스를 갖고 있는 hello 클라우드에 이러한 사용자 계정을 만드는 hello tooWindows와 Azure AD 계정으로 Office 응용 프로그램에 대 한 로그인의 사용자가 tooget hello 이점 수 있습니다. 한편, 사용자가 조직을 떠난 후에 해당 라이선스에 더 많은 유연성을 유지할 수 있습니다.
* **기타 기업**: 온-프레미스 Active Directory에서 사용자를 유지 관리하더라도 사용자가 Azure-AD에 가입되는 장점을 계속 활용할 수 있습니다. Azure AD가 간소화된 가입 환경, 효율적인 장치 관리, 자동 모바일 장치 관리 등록 및 Azure AD/온-프레미스 리소스에 대한 Single Sign-On 기능을 제공하기 때문입니다.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Azure AD 조인에서 제공하는 기능은 무엇인가요?
Azure AD Join와 hello 다음을 발생할 수 있습니다.

* **회사 소유 장치 자체 프로 비전**: Windows 10 사용자가 구성할 수 있습니다는 완전히 새로운 축소 래핑된 장치 IT 담당자의 도움 없이 hello 기본적으로 경험 합니다.
* **최신 폼 팩터에 모두에 대 한 지원**: Azure AD 조인 hello 전통적인 도메인 가입 기능을 갖지 않는 장치에서 작동 합니다.  
* **기존 조직 계정에 대 한 지원**: 사용자가 더 이상 toocreate 필요 하 고 유지 관리는 Windows 8과 마찬가지로 개인 Microsoft 계정 tooget hello 회사에서 발급 한 장치에 대 한 최상의 경험 합니다. 대신 Azure AD에서 기존 회사 계정을 그대로 사용할 수 있습니다. 많은 조직에서는 기본적으로 즉, 사용자가을 설정 하 고 hello로 tooWindows에 동일한 로그인 수 tooaccess Office 365를 사용 하는 자격 증명입니다.
* **자동 모바일 장치 관리 등록**: 연결 된 경우 모바일 장치 관리에 장치를 자동으로 등록 하려면 tooAzure AD 합니다. 이 프로세스는 Microsoft Intune 및 파트너 모바일 장치 관리 솔루션으로 작동합니다. Intune로 장치 관리 완료 되 면 IT 관리자 모니터/관리할 수 hello SCCM 관리 콘솔에서 도메인에 가입 된 장치와 함께 Azure AD에 가입 된 장치.
* **Single sign on toocompany 리소스**: single sign on Windows 데스크톱 tooapps hello 및 Office 365 및 통해인증을위해AzureAD를사용하는비즈니스응용프로그램같은hello클라우드에서리소스에서사용자가이용하세요[Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md)합니다. 조인 된 tooAzure AD는 회사 소유 장치는 또한 SSO tooon 온-프레미스 리소스를 활용 hello 장치가 있으면 회사 네트워크와 모든 위치에서 이러한 리소스는 hello를 통해 노출 되 면 [Azure AD 응용 프로그램 프록시](https://msdn.microsoft.com/library/azure/Dn768219.aspx)합니다.
* **OS 상태 로밍**: 내게 필요한 옵션 설정, 웹 사이트, Wi-Fi 암호 및 기타 설정은 개인 Microsoft 계정 없이도 회사 소유의 장치 간에 동기화됩니다.
* **엔터프라이즈용 Windows 스토어**: hello Windows 스토어 응용 프로그램 취득 및 Azure AD 계정에 라이선스를 지원 합니다. 조직에 볼륨 라이선스 앱 수 하 고 조직에서 사용할 수 있는 toohello 사용자를 확인 합니다.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>다양한 장치가 Azure AD 조인에서 어떻게 작동하나요?
| 회사 장치 (조인 된 tooon 온-프레미스 도메인) | 회사 장치 (조인 된 toohello 클라우드) | 개인 장치 |
| --- | --- | --- |
| 사용자는 회사 자격 증명을 사용하여 Windows에 로그인할 수 있습니다(현재 방식). |사용자가 Azure AD에서 관리 되는 작업 자격 증명으로 tooWindows 로그인 수 있습니다. 이 방식은 다음 세 가지 경우의 회사 장치와 관련됩니다. <ol><li>hello 조직 (예를 들어 소규모 기업) 온-프레미스에 Active Directory 되어 있지 않습니다.</li><li>hello 조직 Active Directory에서 모든 사용자 계정을 만들고 하지 않습니다 (예를 들어, 학생, 컨설턴트 또는 계절별 작업자에 대 한 계정을 만들어집니다 Active Directory에).</li><li>hello 조직 휴대폰 또는 태블릿 모바일 SKU (예를 들어 보조 장치 라인 tooa 공장/소매 층) 실행와 같은 조인된 tooan (온-프레미스) 도메인을 사용할 수 없는 회사 장치에 있습니다.</li></ol> Azure AD 조인은 관리 및 페더레이션 조직 모두를 위한 회사 장치의 가입을 지원합니다. |사용자가 자신의 개인 Microsoft 계정 자격 증명 (변화 없음)와 tooWindows에 로그인합니다. |
| 사용자가 액세스 tooroaming 설정 hello enterprise Windows 스토어 있습니다. 이러한 서비스는 회사 계정으로 작업하고 개인 Microsoft 계정이 필요하지 않습니다. AD가 온-프레미스 Active Directory tooAzure 조직 tooconnect 필요합니다. |사용자는 셀프 서비스 설정을 수행할 수 있습니다. 것 (FRX) hello 첫 실행 경험을 통해 회사 계정을 통해는 대체 toohaving IT으로 hello 장치를 프로 비전 하 고, 두 방법 모두 지원 되지만 합니다. |사용자가 Active Directory 또는 Azure AD에서 관리되는 회사 계정을 쉽게 추가할 수 있습니다. |
| 사용자는 hello toowork 데스크톱 앱, 웹 사이트 및 리소스--온-프레미스 리소스와 인증을 위해 Azure AD를 사용 하는 클라우드 앱을 포함 하 여 SSO 기능이 있습니다. |장치는 hello 엔터프라이즈 디렉터리 (Azure AD)에 자동으로 등록 되 고 자동으로 모바일 장치 관리에 등록 합니다. (Azure AD Premium 기능) |사용자는 앱 및 회사 계정에이 사용 하 여 toowebsites/리소스에서 SSO 기능이 있습니다. |
| 사용자가 추가할 수 자신의 개인 Microsoft 계정 tooaccess 자신의 개인 사진 및 파일 엔터프라이즈 데이터에 영향을 주지 않고 합니다. (로밍 설정 계속 toowork가 회사 계정 사용 합니다.) Microsoft 계정 hello SSO 있으며 특정 hello 로밍 설정의 더 이상 드라이브 합니다. |사용자는 winlogon에서 셀프 서비스 암호 재설정(SSPR)을 수행할 수 있으므로 잊어버린 암호를 재설정할 수 있습니다. (Azure AD Premium 기능) |사용자는 액세스 toohello enterprise Windows 스토어가 설정 하 고 자신의 개인 장치에서 기간 업무 앱을 사용할 수 있도록 합니다. |

## <a name="additional-information"></a>추가 정보
* [Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport를 통해 암호 없이 ID 인증](active-directory-azureadjoin-passport.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

