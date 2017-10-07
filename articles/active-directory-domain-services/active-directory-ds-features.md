---
title: "Azure Active Directory Domain Services: 기능 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스의 기능"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="features"></a>기능
관리 되는 Azure AD 도메인 서비스 도메인에서 hello 같은 기능을 사용할 수 있는 합니다.

* **간단한 배포 환경:** 몇 번의 클릭만으로 Azure AD 테넌트에 Azure AD 도메인 서비스를 사용하도록 설정할 수 있습니다. Azure AD 테넌트가 클라우드 테넌트이든 온-프레미스 디렉터리와 동기화되든 간에 관리되는 도메인을 신속하게 프로비전할 수 있습니다.
* **도메인 가입에 대 한 지원:** 쉽게 hello 관리 되는 도메인 이름은에서 사용할 수 있는 Azure 가상 네트워크의에서 도메인 가입 컴퓨터 수 있습니다. Windows 클라이언트와 Azure AD 도메인 서비스에서 처리 하는 도메인에 대해 원활 하 게 서버 운영 체제 works에서 hello 도메인 가입 경험 합니다. 이러한 도메인을 대상으로 자동화된 도메인 가입 도구도 사용할 수 있습니다.
* **Azure AD 디렉터리당 하나의 도메인 인스턴스:** Azure AD 디렉터리마다 단일 Active Directory 도메인을 만들 수 있습니다.
* **사용자 지정 이름으로 도메인 만들기:** Azure AD Domain Services를 사용하여 사용자 지정 이름(예: 'contoso100.com')으로 도메인을 만들 수 있습니다. 확인된 또는 확인되지 않은 도메인 이름 중 하나를 사용할 수 있습니다. 필요에 따라 만들 수도 있습니다 도메인 hello 기본 제공 도메인 접미사가 있는 (즉, ' *. onmicrosoft.com') Azure AD 디렉터리에서 제공 합니다.
* **Azure AD와 통합:** tooconfigure 필요 하거나 복제를 관리 하지 않는 tooAzure AD 도메인 서비스. Azure AD 디렉터리의 사용자 계정, 그룹 멤버 자격 및 사용자 자격 증명(암호)을 Azure AD Domain Services에서 자동으로 사용할 수 있습니다. 새 사용자, 그룹 또는 Azure AD 테 넌 트 또는 온-프레미스 디렉터리에서 변경 내용 tooattributes는 자동으로 동기화 된 tooAzure AD 도메인 서비스입니다.
* **NTLM 및 Kerberos 인증:** NTLM 및 Kerberos 인증 지원 기능을 사용하여 Windows 통합 인증을 사용하는 응용 프로그램을 배포할 수 있습니다.
* **회사 자격 증명/암호 사용:** Azure AD 테넌트의 사용자 암호가 Azure AD Domain Services에서 작동합니다. 사용자가 회사 자격 증명 toodomain 조인 컴퓨터를 사용 하 여 수, 대화형으로 또는 원격 데스크톱을 통해 로그인 및 hello 관리 되는 도메인에 대해 인증 합니다.
* **LDAP 바인딩 및 LDAP 읽기 지원:** tooauthenticate 사용자가 Azure AD 도메인 서비스에서 서비스 도메인에서 LDAP 바인딩을 사용 하는 응용 프로그램을 사용할 수 있습니다. 또한 LDAP를 사용 하는 응용 프로그램 읽기 tooquery 사용자/컴퓨터 특성 hello 디렉터리에서 Azure AD 도메인 서비스에 대해 처리할 수는 작업입니다.
* **보안 LDAP (LDAPS):** 보안 LDAP (LDAPS)를 통해 toohello 디렉터리에 액세스를 활성화할 수 있습니다. 보안 LDAP 액세스는 기본적으로 hello 가상 네트워크 내에서 사용할 수 있습니다. 그러나 Hello를 통해 보안 LDAP 액세스도 선택적으로 사용할 수 인터넷 합니다.
* **그룹 정책:** 단일 기본 제공 GPO를 각를 사용 하 여 hello 사용자 및 컴퓨터에 대 한 사용자 계정 및 도메인에 가입 된 컴퓨터에 대 한 필수 보안 정책 사용 하 여 컨테이너 tooenforce 준수 합니다. 사용자 고유의 사용자 지정 하는 Gpo를 만들 수 있고 배정할 toocustom 조직 구성 단위 너무 있습니다[그룹 정책 관리](active-directory-ds-admin-guide-administer-group-policy.md)합니다.
* **DNS 관리:** hello ' AAD DC Administrators' 그룹의 구성원 친숙 한 DNS 관리를 사용 하 여 관리 되는 도메인의 DNS 관리 MMC 스냅인 hello와 같은 도구에 대 한 DNS를 관리할 수 있습니다.
* **사용자 지정 조직 구성 단위 (Ou)를 만들:** hello ' AAD DC Administrators' 그룹의 구성원 hello 관리 되는 도메인에서 사용자 지정 Ou를 만들 수 있습니다. 이러한 사용자에게 사용자 지정 OU를 통해 모든 관리 권한이 부여되므로, 이러한 사용자 지정 OU 내에서 서비스 계정, 컴퓨터, 그룹 등을 추가/제거할 수 있습니다.
* **여러 Azure 지역에서 사용할 수 있는:** 참조 hello [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/) 페이지 tooknow hello Azure AD 도메인 서비스를 사용할 수 있는 Azure 지역입니다.
* **고가용성:** Azure AD Domain Services는 도메인에 고가용성을 제공합니다. 이 기능은 더 높은 서비스 작동 시간 및 탄력성 toofailures hello 보장을 제공합니다. 기본 제공 상태 새 인스턴스가 실패 tooreplace 인스턴스 및 tooprovide 구성 함으로써 제공 오류 로부터 자동된 치료 모니터링 도메인에 대 한 서비스를 계속 합니다.
* **친숙 한 관리 도구를 사용 하 여:** hello Active Directory 관리 센터 또는 Active Directory PowerShell 관리 tooadminister 도메인 등 친숙 한 Windows Server Active Directory 관리 도구를 사용할 수 있습니다.
