---
title: "Azure Active Directory Domain Services: 배포 시나리오 | Microsoft Docs"
description: "Azure AD 도메인 서비스용 배포 시나리오"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>배포 시나리오 및 사용 사례
이 섹션에서는 Azure AD(Active Directory) 도메인 서비스에서 이익이 되는 몇 가지 시나리오 및 사용 사례를 살펴보겠습니다.

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Azure 가상 컴퓨터의 안전하고 손쉬운 관리
Azure Active Directory 도메인 서비스 toomanage Azure 가상 컴퓨터는 간소화 된 방식으로 사용할 수 있습니다. Azure 가상 컴퓨터에는 조인 된 toohello 관리 되는 도메인에 따라서 toouse 회사 AD toolog에 자격 증명 사용 될 수 있습니다. 이 방법은 각 Azure 가상 컴퓨터에서 로컬 관리자 계정 유지 관리와 같은 복잡한 자격 증명 관리 과정을 방지하도록 돕습니다.

관리 되는 도메인 조인된 toohello 있는 서버 가상 컴퓨터도으로 관리 하 고 그룹 정책을 사용 하 여 보호 합니다. 필요한 보안 기준을 tooyour Azure 가상를 적용할 수 있습니다를 설치 하 고 회사 보안 지침에 따라 그 고정 합니다. 예를 들어 이러한 가상 컴퓨터에 그룹 정책 관리 기능 toorestrict hello 유형의 시작 될 수 있는 응용 프로그램을 사용할 수 있습니다.

![Azure 가상 컴퓨터의 간소화된 관리](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

서버 및 기타 인프라가 수명 끝에 도달 하는 대로 Contoso 현재 프레미스 toohello 클라우드에서 호스트 하는 많은 응용 프로그램으로 이동 합니다. 현재 해당 IT 표준은 기업 응용 프로그램을 호스팅하는 서버가 그룹 정책을 사용하여 도메인에 가입하고 관리되어야 한다고 규정합니다. Contoso의 IT 관리자가 Azure에서 쉽게 toomake 관리에 배포 된 toodomain 조인 가상 컴퓨터를 선호 합니다. 결과적으로, 관리자 및 사용자는 회사 자격 증명을 사용하여 로그인할 수 있습니다. Hello에서 같은 시간 컴퓨터 그룹 정책을 사용 하 여 필요한 보안 기준과 함께 구성 된 toocomply 될 수 있습니다. Contoso 하지 toohave toodeploy 방법을 모니터링 하 고 Azure toosecure에서 도메인 컨트롤러를 관리할 Azure 가상 컴퓨터. 따라서 Azure AD 도메인 서비스는 이 사용 사례에 대한 최적의 선택입니다.

**배포 참고 사항**

이 배포 시나리오에 대 한 중요 한 사항에 따라 hello를 고려 합니다.

* Azure AD 도메인 서비스에서 제공하는 관리되는 도메인은 단일 플랫 OU(조직 구성 단위) 구조를 기본으로 제공합니다. 모든 도메인에 가입된 컴퓨터는 단일 플랫 OU에 상주합니다. 그러나 사용자 지정 Ou toocreate를 선택할 수 있습니다.
* Azure AD 도메인 서비스의 기본 제공 GPO 각 hello 사용자 및 컴퓨터에 대 한 hello 형태로 단순 그룹 정책 지원 컨테이너입니다. 사용자 지정 Gpo를 만들 수 있으며 toocustom Ou에 대상으로 지정.
* Azure AD 도메인 서비스는 hello 기본 AD 컴퓨터 개체 스키마를 지원합니다. Hello 컴퓨터 개체의 스키마를 확장할 수 없습니다.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>리프트 및-시프트 LDAP 바인딩 인증 tooAzure 인프라 서비스를 사용 하는 온-프레미스 응용 프로그램
![LDAP 바인딩](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Contoso에는 ISV에서 몇 년 전에 구입한 온-프레미스 응용 프로그램이 있습니다. hello 응용 프로그램 현재 hello ISV 여 유지 관리 모드 이므로 요청 변경 toohello 응용 프로그램은 Contoso에 대 한 많은 비용이 들 합니다. 이 응용 프로그램에 web form을 사용 하 여 사용자 자격 증명을 수집 하 고 다음 LDAP 바인딩 toohello 수행 하 여 사용자를 인증 하는 웹 기반 프런트 엔드 회사 Active Directory 합니다. Contoso toomigrate 있을 것이 응용 프로그램 tooAzure 인프라 서비스입니다. Hello 응용 프로그램을 변경할 필요 없이 대로 작동 하는지 좋을 것입니다. 또한 사용자가 기존 회사 자격 증명을 사용 하 여 수 tooauthenticate 수와 다르게 tooretrain 사용자 toodo 작업이 필요 없이 해야 합니다. 즉, 최종 사용자에 게 hello 응용 프로그램이 실행 중인의 인식 하지 못하고 고 hello 마이그레이션 투명 toothem 이어야 합니다.

**배포 참고 사항**

이 배포 시나리오에 대 한 중요 한 사항에 따라 hello를 고려 합니다.

* Hello 응용 프로그램 toomodify/쓰기 toohello 디렉터리가 필요 하지 않습니다 확인 합니다. Azure AD 도메인 서비스에서 제공 하는 LDAP 쓰기 액세스 toomanaged 도메인 지원 되지 않습니다.
* Hello 관리 되는 도메인에 대해 직접 암호를 변경할 수 없습니다. 최종 사용자가 암호를 하거나 변경할 수 Azure AD의 셀프 서비스 암호 변경 메커니즘을 사용 하 여 hello 온-프레미스 디렉터리에 대해 또는 합니다. 이러한 변경 내용은 자동으로 동기화 하 고 사용할 수 있는 hello 관리 되는 도메인에서 됩니다.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>리프트 시프트 읽기 tooaccess hello 디렉터리 tooAzure 인프라 서비스 LDAP를 사용 하는 온-프레미스 응용 프로그램
Contoso에는 거의 10년 전에 개발된 온-프레미스 LOB(기간 업무) 응용 프로그램이 있습니다. 이 응용 프로그램 인식 디렉터리가 고 Windows Server AD와 함께 설계 된 toowork 되었습니다. hello 응용 LDAP (Lightweight Directory Access Protocol) tooread 정보/특성에 대 한 Active Directory에서 사용자를 사용합니다. hello 응용 프로그램 특성을 수정 하거나 그렇지 않으면 toohello 디렉터리 쓰기 하지 않습니다. Contoso toomigrate 있을 것이 응용 프로그램 tooAzure 인프라 서비스 및이 응용 프로그램을 호스팅 중인 hello 에이징 온-프레미스 하드웨어 사용 중지 합니다. hello 응용 프로그램에는 Azure AD Graph API REST 기반 hello와 같은 다시 쓴된 toouse 최신 디렉터리 Api 수 없습니다. 따라서 hello 응용 프로그램 코드를 수정 하거나 hello 응용 프로그램을 다시 작성 하지 않고 hello 클라우드에서 마이그레이션된 toorun 수는 그 리프트 shift 옵션 방법이 필요 합니다.

**배포 참고 사항**

이 배포 시나리오에 대 한 중요 한 사항에 따라 hello를 고려 합니다.

* Hello 응용 프로그램 toomodify/쓰기 toohello 디렉터리가 필요 하지 않습니다 확인 합니다. Azure AD 도메인 서비스에서 제공 하는 LDAP 쓰기 액세스 toomanaged 도메인 지원 되지 않습니다.
* Hello 응용 프로그램에 사용자 지정/확장 된 Active Directory 스키마가 필요 하지 않습니다 확인 합니다. 스키마 확장은 Azure AD 도메인 서비스에서 지원되지 않습니다.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>온-프레미스 서비스 또는 데몬 응용 프로그램 tooAzure 인프라 서비스 마이그레이션
일부 응용 프로그램에서 데이터베이스 계층 등 tooperform 인증 된 호출 tooa 백 엔드 계층 필요한 hello 계층 중 하나는 여러 계층에 구성 됩니다. Active Directory 서비스 계정은 이러한 사용 사례에 대해 자주 사용됩니다. 리프트 시프트 하면 이러한 응용 프로그램 tooAzure 인프라 서비스 및 이러한 응용 프로그램의 hello identity 요구 사항에 대 한 Azure AD 도메인 서비스를 사용 합니다. 선택할 수 있습니다 toouse hello 온-프레미스 디렉터리 tooAzure AD에서에서 동기화 되는 동일한 서비스 계정입니다. 또는 사용자 지정 된 OU를 만들려면 먼저 하 고 toodeploy 해당 OU에 별도 서비스 계정의 이러한 응용 프로그램 만들 수 있습니다.

![WIA를 사용하는 서비스 계정](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Contoso에는 웹 프런트 엔드, SQL server 및 백 엔드 FTP 서버를 포함하는 사용자 지정 소프트웨어 자격 증명 모음 응용 프로그램이 있습니다. 서비스 계정의 Windows 통합 인증에는 사용 되는 tooauthenticate hello 웹 프런트 엔드 toohello FTP 서버입니다. hello 웹 프런트 엔드 서비스 계정으로 toorun 설정 되어 있습니다. hello 백 엔드 서버가 hello 웹 프런트 엔드에 대 한 hello 서비스 계정에서 tooauthorize 액세스 합니다. Contoso는이 응용 프로그램 tooAzure 인프라 서비스 하지 toohave toodeploy hello 클라우드 toomove는 도메인 컨트롤러 가상 컴퓨터를 선호합니다. Contoso의 IT 관리자는 hello 웹 프런트 엔드, SQL server 및 hello FTP 서버 tooAzure 가상 컴퓨터를 호스트 하는 hello 서버를 배포할 수 있습니다. 이러한 컴퓨터는 더 조인된 tooan Azure AD 도메인 서비스 도메인을 관리 합니다. 그런 다음, 사용할 수 hello 응용 프로그램의 인증을 위해가 온-프레미스 디렉터리에서 동일한 서비스 계정을 hello 합니다. 이 서비스 계정은 동기화 된 toohello Azure AD 도메인 서비스에 대 한 관리 되는 도메인 이며 용도로 사용할 수 있습니다.

**배포 참고 사항**

이 배포 시나리오에 대 한 중요 한 사항에 따라 hello를 고려 합니다.

* Hello 응용 프로그램 인증에 대 한 사용자 이름/암호를 사용 해야 합니다. Azure AD 도메인 서비스에서 인증서/스마트 카드 기반 인증을 지원하지 않습니다.
* Hello 관리 되는 도메인에 대해 직접 암호를 변경할 수 없습니다. 최종 사용자가 암호를 하거나 변경할 수 Azure AD의 셀프 서비스 암호 변경 메커니즘을 사용 하 여 hello 온-프레미스 디렉터리에 대해 또는 합니다. 이러한 변경 내용은 자동으로 동기화 하 고 사용할 수 있는 hello 관리 되는 도메인에서 됩니다.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Azure에서 Windows Server 원격 데스크톱 서비스 배포
Tooprovide AD 관리 되는 Azure AD 도메인 서비스를 사용 하려면 도메인 tooyour 원격 데스크톱 서버 Azure에 배포 된 서비스입니다.

이 배포 시나리오에 대 한 자세한 내용은 참조 방법을 너무[RDS 배포와 Azure AD 도메인 서비스 통합](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds)합니다.
