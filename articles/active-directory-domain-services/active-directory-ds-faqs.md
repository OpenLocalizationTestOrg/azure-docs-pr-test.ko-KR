---
title: "aaaFAQs-Azure Active Directory 도메인 서비스 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스에 대해 자주 묻는 질문과 대답입니다."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: 자주 묻는 질문과 대답(FAQ)
이 페이지 hello Azure Active Directory 도메인 서비스에 대 한 질문과 대답을 제공 합니다. 업데이트를 계속 확인합니다.

### <a name="troubleshooting-guide"></a>문제 해결 가이드
Tooour 참조 [문제 해결 가이드](active-directory-ds-troubleshooting.md) 솔루션 toocommon 문제가 발생할 경우에 대 한 구성 또는 Azure AD 도메인 서비스를 관리 합니다.

### <a name="configuration"></a>구성
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>단일 Azure AD 디렉터리에 여러 도메인을 만들 수 있나요?
아니요. 단일 Azure AD 디렉터리에 대해 Azure AD 도메인 서비스에서 서비스되는 단일 도메인만 만들 수 있습니다.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Azure Resource Manager 가상 네트워크에서 Azure AD Domain Services를 사용할 수 있습니까?
아니요. 클래식 Azure 가상 네트워크에서는 Azure AD Domain Services만 사용할 수 있습니다. Hello 클래식 가상 네트워크 tooa 리소스 관리자 가상 네트워크 가상 네트워크 피어 링 toouse 리소스 관리자 가상 네트워크에서 관리 되는 도메인을 사용 하 여 연결할 수 있습니다.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>페더레이션된 Azure AD 디렉터리에서 Azure AD Domain Services를 사용할 수 있습니까? 액세스 tooOffice 365에 ADFS tooauthenticate 사용자를 사용 합니다. 이 디렉터리에 Azure AD Domain Services를 사용할 수 있습니까?
아니요. Azure AD 도메인 서비스 toohello 암호 해시는 사용자 계정, tooauthenticate가 NTLM 또는 Kerberos를 통해 액세스 해야 합니다. 페더레이션된 디렉터리에 암호 해시 hello Azure AD 디렉터리에 저장 되지 않습니다. 따라서 Azure AD Domain Services는 이러한 Azure AD 디렉터리와 함께 작동하지 않습니다.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Azure AD Domain Services를 내 구독 내의 여러 가상 네트워크에서 사용할 수 있나요?
hello 서비스 자체는이 시나리오를 직접 지원 하지 않습니다. Azure AD Domain Services는 한 번에 하나의 가상 네트워크에서만 사용할 수 있습니다. 그러나 여러 개의 가상 네트워크 tooexpose Azure AD 도메인 서비스 tooother 가상 네트워크 간의 연결을 구성할 수 있습니다. 이 문서에서는 [Azure에서 가상 네트워크를 연결](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)하는 방법을 설명합니다.

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>PowerShell을 사용하여 Azure AD 도메인 서비스를 사용할 수 있나요?
Azure AD 도메인 서비스의 PowerShell/자동화된 배포는 현재 사용할 수 없습니다.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Azure AD 도메인 서비스는 hello 새 Azure 포털에서 사용할 수 있습니까?
아니요. Azure AD 도메인 서비스는 hello에만 구성할 수 있습니다 [Azure 클래식 포털](https://manage.windowsazure.com)합니다. Hello에 대 한 tooextend 지원 될 것으로 예상 [Azure 포털](https://portal.azure.com) hello 앞에 있습니다.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>도메인 컨트롤러 tooan Azure AD 도메인 서비스 관리 되는 도메인을 추가할 수 있습니까?
아니요. hello Azure AD 도메인 서비스에서 제공 되는 관리 되는 도메인이입니다. Tooprovision 필요 하지 않습니다, 구성 하거나, 그렇지 않으면이 도메인-이러한 관리 작업은 Microsoft에서 서비스 제공에 대 한 도메인 컨트롤러를 관리 합니다. 따라서 hello 관리 되는 도메인에 대 한 추가 도메인 컨트롤러 (읽기 / 쓰기 또는 읽기 전용)를 추가할 수 없습니다.

### <a name="administration-and-operations"></a>관리 및 운영
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>원격 데스크톱을 사용 하 여 관리 되는 도메인에 대 한 toohello 도메인 컨트롤러에 연결할 수 있습니까?
아니요. 원격 데스크톱을 통해 관리 되는 도메인 hello에 대 한 사용 권한을 tooconnect toodomain 컨트롤러 않아도 됩니다. Hello ' AAD DC Administrators' 그룹의 구성원이 AD PowerShell 관리 센터 ADAC (Active Directory) hello 등 AD 관리 도구를 사용 하 여 hello 관리 되는 도메인을 관리할 수 있습니다. Hello ' 원격 서버 관리 도구 '를 사용 하 여 이러한 도구가 설치 되어 Windows 서버에서 기능 toohello 관리 되는 도메인에 가입 합니다.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Azure AD 도메인 서비스를 사용한 적이 있습니다. 사용자 계정을 컴퓨터 toothis 도메인에 가입 toodomain 사용 합니까?
' AAD DC Administrators' hello 관리 그룹의 구성원이 도메인 가입 컴퓨터 수입니다. 또한이 그룹의 구성원에는 도메인에 가입된 toohello 된 원격 데스크톱 액세스 toomachines를 부여 됩니다.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Azure AD 도메인 서비스에서 제공 하는 hello 관리 되는 도메인에 대 한 도메인 관리자 권한이 있습니까?
아니요. Hello 관리 되는 도메인에 대해 관리자 권한이 부여 되지 않습니다. ' 도메인 관리자 '와 ' 엔터프라이즈 관리자 ' 권한 toouse hello 도메인 내에서 사용할 수 없는 합니다. 기존 도메인 관리자 또는 Azure AD 디렉터리 내에서 엔터프라이즈 관리자 그룹도 부여 되지 않습니다 hello 도메인에 도메인/엔터프라이즈 관리자 권한이 있습니다.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>관리되는 도메인에서 LDAP 또는 다른 AD 관리 도구를 사용하여 그룹 멤버 자격을 수정할 수 있습니까?
아니요. Azure AD 도메인 서비스에서 서비스를 제공하는 도메인에 그룹 멤버 자격을 수정할 수 없습니다. hello 사용자 특성에 마찬가지입니다. 그러나 Azure AD 또는 온-프레미스 도메인에서 그룹 구성원 자격 또는 사용자 특성을 변경할 수도 있습니다. 이러한 변경이 자동으로 동기화 된 tooAzure AD 도메인 서비스에 설명 합니다.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>얼마나 오래 걸립니까 변경에 대 한 I toomy Azure AD 디렉터리 toobe 관리 되는 도메인 내에서 표시 하도록 설정?
Hello Azure AD UI 또는 PowerShell을 사용 하 여 Azure AD 디렉터리의 변경 내용은 tooyour 동기화 된 관리 되는 도메인 됩니다. 이 동기화 프로세스 hello 백그라운드에서 실행 됩니다. 디렉터리의 hello 일회성 초기 동기화 완료 되 면 일반적으로 Azure AD toobe에서 변경 될 때까지 20 분 정도 걸립니다 반영 관리 되는 도메인 내에서.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Azure AD 도메인 서비스에서 제공 하는 hello 관리 되는 도메인의 hello 스키마를 확장할 수 있습니까?
아니요. hello 스키마는 hello 관리 되는 도메인에 대 한 Microsoft에서 관리 됩니다. 스키마 확장은 Azure AD 도메인 서비스에서 지원되지 않습니다.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>관리되는 도메인에서 DNS 레코드를 수정하거나 추가할 수 있습니까?
예. Hello AAD ' DC Administrators' 그룹의 구성원 ' DNS 관리자 ' 권한을 부여 받은 toomodify DNS 기록 hello 관리 되는 도메인에 합니다. 컴퓨터가 실행 중인 Windows Server 조인된 toohello 관리 되는 도메인에 DNS toomanage hello DNS 관리자 콘솔을 사용할 수 있습니다. toouse hello DNS 관리자 콘솔 ' DNS 서버 도구 ' hello ' 원격 서버 관리 도구 ' hello 서버의 선택적 기능에 포함 되어 있는 설치 합니다. [DNS를 관리하고, 모니터링하고 문제를 해결하는 유틸리티](https://technet.microsoft.com/library/cc753579.aspx) 에 대한 자세한 정보는 TechNet를 참조하세요.

### <a name="billing-and-availability"></a>요금 청구 및 가용성
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Azure AD Domain Services는 유료 서비스인가요?
예. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/active-directory-ds/)합니다.

#### <a name="is-there-a-free-trial-for-hello-service"></a>Hello 서비스에 대 한 무료 평가판이 있나요?
이 서비스는 Azure 용 hello 무료 평가판에 포함 됩니다. [Azure의 1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>Enterprise Mobility Suite(EMS)의 일부로 Azure AD 도메인 서비스를 가져올 수 있습니까? Azure AD Premium toouse Azure AD 도메인 서비스를 필요 합니까?
아니요. Azure AD Domain Services는 종량제 Azure 서비스이며 EMS의 일부가 아닙니다. Azure AD Domain Services는 모든 에디션의 Azure AD(무료, 기본 및 프리미엄)에 사용할 수 있습니다. 사용 방식에 따라 시간 단위로 청구됩니다.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>어떤 Azure 지역은 hello 서비스에서 사용할 수 있습니까?
Toohello 참조 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/) 목록을 페이지 toosee hello Azure AD 도메인 서비스를 사용할 수 있는 Azure 지역입니다.
