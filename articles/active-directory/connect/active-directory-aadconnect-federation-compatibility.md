---
title: "AD aaaAzure 페더레이션 호환성 목록"
description: "이 페이지에는 Microsoft가 아닌 타사 tooimplement 사용된 될 수 있는 id 공급자 single sign on입니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a>Azure AD 페더레이션 호환성 목록
Azure Active Directory에서는 임의 타사 솔루션을 요구하지 않고 Office 365용 Single Sign-On과 강화된 응용 프로그램 액세스 보안 및 하이브리드와 클라우드 전용 구현에 대한 기타 Microsoft Online Services를 제공합니다. 대부분의 Microsoft Online Services와 마찬가지로 Office 365는 디렉터리 서비스, 인증 및 권한 부여에 대해 Azure Active Directory와 통합되어 있습니다. 온-프레미스 웹 응용 프로그램 및 azure Active Directory에는 또한 SaaS 응용 프로그램의 single sign on toothousands 제공 합니다. 지원 되는 SaaS 응용 프로그램에 대 한 hello Azure Active Directory 응용 프로그램 갤러리를 참조 하십시오.

Microsoft가 아닌 타사 페더레이션 솔루션에 투자 하는 조직에서는이 항목에서는 Microsoft가 아닌 타사 id 공급자를 사용 하 여 Microsoft Online 서비스를 사용 하 여 single sign on Windows Server Active Directory 사용자를 위한 구성에 대 한 지침 hello "Azure Active Directory 페더레이션 호환성 목록에" 아래 합니다. 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
[Oxford Computer Group](http://oxfordcomputergroup.com/)은 Microsoft를 대신하여 이러한 Single Sign-On 환경을 Azure Active Directory와 공통된 사용 사례 집합에 대해 타사 ID 공급자를 사용하여 테스트했습니다.

여기에 나열된 타사 ID 공급자를 가져오는 방법에 대한 내용은 Oxford Computer Group( [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com))에 문의하세요.

> [!IMPORTANT]
> Oxford 컴퓨터 그룹에는 이러한 single sign-on 시나리오의 hello 페더레이션 기능만을 테스트 했습니다. 컴퓨터 그룹 Oxford hello 동기화, 다단계 인증, 등 이러한 single sign-on 시나리오의 구성 요소 테스트를 수행 하지 못했습니다.
> 
> 로그인의 대체 ID tooUPN 사용이이 프로그램에서 테스트 되지 합니다.
> 
> 

* [Azure Active Directory](#azure-active-directory)
* [AuthAnvil Single Sign On 4.5](#authanvil-single-sign-on-45)
* [BIG-IP with Access Policy Manager BIG-IP 버전 11.3x – 11.6x](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [BitGlass](#bitglass)
* [CA Secure Cloud](#ca-secure-cloud) 
* [CA SiteMinder 12.52](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [Centrify](#centrify) 
* [Dell One Identity Cloud Access Manager v7.1](#dell-one-identity-cloud-access-manager-v71) 
* [DigitalPersona 복합 인증](#digitalpersona-composite-authentication)
* [IBM Tivoli Federated Identity Manager 6.2.2](#ibm-tivoli-federated-identity-manager-622) 
* [IceWall Federation 버전 3.0](#icewall-federation-version-30) 
* [Memority](#memority)
* [NetIQ Access Manager 4.x](#netiq-access-manager-4x) 
* [Okta](#okta) 
* [OneLogin](#onelogin) 
* [Optimal IDM Virtual Identity Server Federation Services](#optimal-idm-virtual-identity-server-federation-services) 
* [PingFederate 6.11, 7.2, 8.x](#pingfederate-611-72-8x)
* [RadiantOne CFS 3.0](#radiantone-cfs-30) 
* [Sailpoint IdentityNow](#sailpoint-identitynow)
* [SecureAuth IdP 7.2.0](#secureauth-idp-720) 
* [Sign&go 5.3](#signgo-53) 
* [SoftBank Technology Online Service Gate](#softbank)
* [VMware Workspace One](#vmware-workspace-one)



> [!IMPORTANT]
> 이러한 타사 제품 이므로 Microsoft는 hello 배포, 구성, 문제 해결, 모범 사례, 등 문제 및 이러한 id 공급자에 관한 질문에 대 한 지원을 제공 하지 않습니다. 지원 및 이러한 id 공급자에 관한 질문에 대 한 연락처 hello 제 3 자가 직접 지원 합니다.
> 
> 이러한 타사 ID 공급자는 Microsoft 클라우드 서비스와의 상호 운용성에 대해 WS-Federation 및 WS-Trust 프로토콜만 사용하여 테스트되었습니다. 테스트 hello SAML 프로토콜을 사용 하 여 포함 되지 않았습니다.
> 


## <a name="azure-active-directory"></a>Azure Active Directory

hello 다음은이 로그온 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |
| Office 2016과 같은 ADAL을 사용하는 최신 응용 프로그램 |지원됨 |없음 |

AD FS를 통해 Azure Active Directory를 사용하는 방법에 대한 자세한 내용은 [ADFS(Active Directory Federation Services)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)를 참조하세요.

암호 동기화를 통해 Azure Active Directory를 사용하는 방법에 대한 자세한 내용은 [Azure AD Connect](active-directory-aadconnect.md)를 참조하세요.

## <a name="authanvil-single-sign-on-45"></a>AuthAnvil Single Sign On 4.5

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

자세한 내용은 [AuthAnvil Single Sign-On](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-)을 참조하세요.


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a>BIG-IP with Access Policy Manager BIG-IP 버전 11.3x – 11.6x

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원되지 않음 |지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

BIG-IP Access Policy Manager에 대한 자세한 내용은 [BIG-IP Access Policy Manager](https://f5.com/products/modules/access-policy-manager) 

Pdf hello에 대 한 hello BIG-IP Access Policy Manager 지침은이 STS tooprovide hello single sign on 환경을 tooyour Active Directory 사용자를 다운로드 하는 tooconfigure 어떻게 [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf)합니다.

## <a name="bitglass"></a>BitGlass

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

BitGlass에 대한 자세한 내용은 [BitGlass](http://www.bitglass.com)를 참조하세요.

## <a name="ca-secure-cloud"></a>CA Secure Cloud

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

CA Secure Cloud에 대한 자세한 내용은 [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx)를 참조하세요.

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a>CA SiteMinder 12.52 SP1 누적 릴리스 4

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

CA SiteMinder에 대한 자세한 내용은 [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html)을 참조하세요. 

## <a name="centrify"></a>Centrify

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |클라이언트 액세스 제어는 지원되지 않습니다. |

Centrify에 대한 자세한 내용은 [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp)를 참조하세요.

## <a name="dell-one-identity-cloud-access-manager-v71"></a>Dell One Identity Cloud Access Manager v7.1

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

Dell One Identity Cloud Access Manager에 대한 자세한 내용은 [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager)를 참조하세요.

 Hello에 대 한 지침은 tooconfigure이 STS tooprovide hello single sign on 환경을 tooyour Office 365 사용자를 확인 하려면 어떻게 [Office 365 사용자 구성](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365)합니다. 

## <a name="digitalpersona-composite-authentication"></a>DigitalPersona 복합 인증  

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음|
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음|
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

자세한 내용은 [DigitalPersona 복합 인증](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf)을 참조하세요.


## <a name="ibm-tivoli-federated-identity-manager-622"></a>IBM Tivoli Federated Identity Manager 6.2.2

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

IBM Tivoli Federated Identity Manager에 대한 자세한 내용은 [Microsoft 응용 프로그램용 IBM Security Access Manager](http://www-01.ibm.com/support/docview.wss?uid=swg24029517)를 참조하세요.

## <a name="icewall-federation-version-30"></a>IceWall Federation 버전 3.0

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

IceWall Federation에 대한 자세한 내용은 [IceWall Federation 버전 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) 및 [Office 365를 사용하여 IceWall Federation](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html)을 참조하세요.

## <a name="memority"></a>Memority

hello 다음은이 로그온 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

Memority 사용에 대한 자세한 내용은 [Memority](http://www.memority.com)를 참조하세요.


## <a name="netiq-access-manager-4x"></a>NetIQ Access Manager 4.x

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음|
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음|
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

자세한 내용은 [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m)를 참조하세요.

## <a name="okta"></a>Okta

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증에는 추가 웹 서버 및 Okta 응용 프로그램 설치가 필요합니다. |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

Okta에 대한 자세한 내용은 [Okta](https://www.okta.com/)를 참조하세요.

## <a name="onelogin"></a>OneLogin

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

OneLogin에 대한 자세한 내용은 [OneLogin](https://www.onelogin.com/)을 참조하세요.

## <a name="optimal-idm-virtual-identity-server-federation-services"></a>Optimal IDM Virtual Identity Server Federation Services

hello 다음이 single sign-on 환경을 시나리오 지원 매트릭스 hello 됩니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |

클라이언트에 대 한 자세한 정보에 대 한 액세스 정책을 참조 [액세스 제한 tooOffice 365 서비스 hello hello 클라이언트의 위치에 따라](https://technet.microsoft.com/library/hh526961.aspx)합니다.





## <a name="pingfederate-611-72-8x"></a>PingFederate 6.11, 7.2, 8.x

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

Tooyour Active Directory 사용자에 대 한 hello PingFederate 지침은 어떻게 tooconfigure이 STS tooprovide hello single sign on 환경을 hello 다음 중 하나를 참조: 

- [PingFederate 6.11](http://go.microsoft.com/fwlink/?LinkID=266321)
- [PingFederate 7.2](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [PingFederate 8.x](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a>RadiantOne CFS 3.0

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

RadiantOne CFS에 대한 자세한 내용은 [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/)를 참조하세요.

## <a name="sailpoint-identitynow"></a>Sailpoint IdentityNow

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

자세한 내용은 [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/)를 참조하세요.

## <a name="secureauth-idp-720"></a>SecureAuth IdP 7.2.0

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다. 

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |없음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

SecureAuth에 대한 자세한 내용은 [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293)를 참조하세요.














## <a name="signgo-53"></a>Sign&go 5.3

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Kerberos 계약 지원됨 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |없음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

Sign&go 5.3은 Kerberos 계약 구성을 통해 Kerberos 인증을 지원합니다.  이 구성 사용 하 여 도움이 필요한 경우 Ilex 또는 보기 hello 설치 가이드를 문의 하십시오 [sign&go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)

## <a name="softbank-technology-online-service-gate"></a>SoftBank Technology Online Service Gate

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

SoftBank Technology Online Service Gate에 대한 자세한 내용은 [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)를 참조하세요.

## <a name="vmware-workspace-one"></a>VMware Workspace One

hello 다음은이 single sign-on 환경에 대 한 hello 시나리오 지원 매트릭스입니다.

| 클라이언트 | 지원 | 예외 |
| --- | --- | --- |
| Exchange Web Access 및 SharePoint Online과 같은 웹 기반 클라이언트 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Lync, Office Subscription, CRM과 같은 리치 클라이언트 응용 프로그램 |지원됨 |Windows 통합 인증은 지원되지 않음 |
| Outlook 및 ActiveSync와 같은 메일 리치 클라이언트 |지원됨 |없음 |

자세한 내용은 [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)을 참조하세요.

