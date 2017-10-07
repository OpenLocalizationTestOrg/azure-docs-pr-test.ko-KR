---
title: "API 관리 FAQ aaaAzure | Microsoft Docs"
description: "Hello 답변 toocommon 질문, 패턴 및 Azure API 관리에서 모범 사례에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Azure API Management FAQ
Azure API 관리에 대 한 hello 답변 toocommon 질문, 패턴 및 모범 사례를 가져옵니다.

## <a name="contact-us"></a>문의처
* [어떻게 하나요 질문 hello Microsoft Azure API 관리 팀?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>질문과 대답
* [기능이 미리 보기 상태인 경우 어떤 의미입니까?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Hello API 관리 게이트웨이와 내 백 엔드 서비스 간의 hello 연결이 어떻게 보호 수 있습니까?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [내 API 관리 서비스 인스턴스 tooa 새 인스턴스를 복사 하려면 어떻게 해야 합니까?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [API 관리 인스턴스를 프로그래밍 방식으로 관리할 수 있습니까?](#can-i-manage-my-api-management-instance-programmatically)
* [사용자 toohello 관리자 그룹을 추가 하려면 어떻게 해야 합니까?](#how-do-i-add-a-user-to-the-administrators-group)
* [Hello 정책 추가 하고자 하는 tooadd hello 정책 편집기에서 사용할 수 없는 이유는 무엇입니까?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [API Management에서 API 버전 관리를 사용하려면 어떻게 해야 합니까?](#how-do-i-use-api-versioning-in-api-management)
* [단일 API에서 여러 환경을 설정하려면 어떻게 해야 합니까?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [API Management와 함께 SOAP를 사용할 수 있습니까?](#can-i-use-soap-with-api-management)
* [Hello API 관리 게이트웨이 IP 주소 상수 인지 확인 그것을 방화벽 규칙에 사용할 수 있습니까?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [AD FS 보안을 통해 OAuth 2.0 권한 부여 서버를 구성할 수 있습니까?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [API 관리에서 배포 toomultiple 지리적 위치에 어떤 라우팅 메서드를 사용 합니까?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Azure 리소스 관리자 템플릿 toocreate API 관리 서비스 인스턴스를 사용할 수 있습니까?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [백 엔드에 대해 자체 서명된 SSL 인증서를 사용할 수 있습니까?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [왜 인증이 실패 하는 GIT 리포지토리 tooclone 때?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [API Management는 Azure ExpressRoute와 함께 작동합니까?](#does-api-management-work-with-azure-expressroute)
* [API Management가 배포될 때 리소스 관리자 스타일 VNET에 전용 서브넷이 필요한 이유는 무엇인가요?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [VNET에 API 관리를 배포할 때 필요한 hello 최소 서브넷 크기 이란?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [하나의 구독 tooanother에서 API 관리 서비스를 이동할 수 있습니까?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [내 API를 가져오는 데 제한 사항 또는 알려진 문제가 있나요?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>어떻게 하나요 질문 hello Microsoft Azure API 관리 팀?
다음 옵션 중 하나를 사용하여 문의할 수 있습니다.

* [API Management MSDN 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt)에 질문을 게시합니다.
* 너무 전자 메일을 보내<mailto:apimgmt@microsoft.com>합니다.
* Hello에 기능 요청을 보내 [Azure 피드백 포럼](https://feedback.azure.com/forums/248703-api-management)합니다.

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>기능이 미리 보기 상태인 경우 어떤 의미입니까?
미리 보기 기능 이므로 의미 드립니다 hello 기능이 작동 방법에 대 한 피드백 적극적으로 검색 하는 것입니다. 미리 보기에서 기능은 기능적으로 완전 하지만 toocustomer 피드백 응답을 변경 하 여 중단을 만들면 가능 합니다. 프로덕션 환경에서 미리 보기에 있는 기능에 의존하지 않는 것이 좋습니다. 미리 보기 기능에 대 한 의견 있다면 알려주세요 hello에 연락처 옵션 중 하나를 통해 [방법을 문의할 수 있습니까 hello Microsoft Azure API 관리 팀 질문?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)합니다.

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Hello API 관리 게이트웨이와 내 백 엔드 서비스 간의 hello 연결이 어떻게 보호 수 있습니까?
API 관리 게이트웨이 hello 및 백 엔드 서비스 간의 몇 가지 옵션 toosecure hello 연결을 해야합니다. 다음을 수행할 수 있습니다.

* HTTP 기본 인증을 사용할 수 있습니다. 자세한 내용은 [API 설정 구성](api-management-howto-create-apis.md#configure-api-settings)을 참조하세요.
* 에 설명 된 대로 SSL 상호 인증을 사용 하 여 [Azure API 관리에서 클라이언트 인증서 인증을 사용 하 여 toosecure 백 엔드 서비스 하는 방법을](api-management-howto-mutual-certificates.md)합니다.
* 백 엔드 서비스에서 IP 허용 목록을 사용할 수 있습니다. 표준 또는 프리미엄 계층 API 관리 인스턴스를 설정한 경우 hello 게이트웨이의 IP 주소 hello 일정 하 게 유지 합니다. 이 IP 주소 허용 목록을 tooallow를 설정할 수 있습니다. Hello Azure 포털의에서 대시보드 hello에서 API 관리 인스턴스 hello IP 주소를 가져올 수 있습니다.
* API 관리 인스턴스 tooan Azure 가상 네트워크를 연결 합니다.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>내 API 관리 서비스 인스턴스 tooa 새 인스턴스를 복사 하려면 어떻게 해야 합니까?
Toocopy API 관리 인스턴스 tooa 새 인스턴스를 원하는 경우 몇 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

* Hello 백업을 사용 하 고 API 관리에서 함수를 복원 합니다. 자세한 내용은 참조 [tooimplement 재해 복구를 사용 하 여 백업 서비스 하 고 Azure API 관리에서 복원 하는 방법을](api-management-howto-disaster-recovery-backup-restore.md)합니다.
* 고유 백업을 만들고 hello를 사용 하 여 기능을 복원 [API 관리 REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)합니다. REST API toosave hello를 사용 하 고 원하는 hello 서비스 인스턴스에서 hello 엔터티를 복원 합니다.
* Git를 사용 하 여 hello 서비스 구성을 다운로드 한 후 새 인스턴스를 tooa 업로드 합니다. 자세한 내용은 참조 [어떻게 toosave 및 Git를 사용 하 여 API 관리 서비스 구성 구성](api-management-configuration-repository-git.md)합니다.

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>API 관리 인스턴스를 프로그래밍 방식으로 관리할 수 있습니까?
예, 다음을 사용하여 프로그래밍 방식으로 API Management를 관리할 수 있습니다.

* hello [API 관리 REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)합니다.
* hello [Microsoft Azure ApiManagement 서비스 관리 라이브러리 SDK](http://aka.ms/apimsdk)합니다.
* hello [서비스 배포](https://msdn.microsoft.com/library/mt619282.aspx) 및 [서비스 관리](https://msdn.microsoft.com/library/mt613507.aspx) PowerShell cmdlet.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>사용자 toohello 관리자 그룹을 추가 하려면 어떻게 해야 합니까?
Toohello 관리자 그룹 사용자를 추가 하는 방법을 다음과 같습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello API 관리 인스턴스 tooupdate 없는 toohello 리소스 그룹을 이동 합니다.
3. API 관리에서 할당 hello **Api 관리 참가자** toohello 사용자 역할입니다.

Hello 새로 추가 된 참가자 Azure PowerShell을 사용 하 여 이제 [cmdlet](https://msdn.microsoft.com/library/mt613507.aspx)합니다. 다음은 어떻게에서 관리자 권한으로 toosign:

1. 사용 하 여 hello `Login-AzureRmAccount` cmdlet toosign에 있습니다.
2. 사용 하 여 hello 서비스 하는 hello 컨텍스트 toohello 구독 설정 `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`합니다.
3. `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`을(를) 사용하여 Single Sign-On URL을 가져옵니다.
4. Hello URL tooaccess hello 관리자 포털을 사용 합니다.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Hello 정책 추가 하고자 하는 tooadd hello 정책 편집기에서 사용할 수 없는 이유는 무엇입니까?
Hello 정책 tooadd 나타납니다 흐리게 표시 hello 정책 편집기의 음영 처리 된 경우 hello hello 정책에 대 한 올바른 범위에 있는지 해야 합니다. 각 정책 설명에 특정 범위 및 정책 섹션 toouse 위해 설계 되었습니다. tooreview hello 정책 섹션 및 정책에 대 한 범위 참조 hello 정책 사용 현황 섹션 [API 관리 정책](https://msdn.microsoft.com/library/azure/dn894080.aspx)합니다.

### <a name="how-do-i-use-api-versioning-in-api-management"></a>API Management에서 API 버전 관리를 사용하려면 어떻게 해야 합니까?
API 관리에서 몇 가지 옵션 toouse API 버전 관리 있습니다.

* API 관리에서 Api toorepresent 서로 다른 버전을 구성할 수 있습니다. 예를 들어 두 개의 다른 API인 MyAPIv1 및 MyAPIv2가 있을 수 있습니다. 개발자는 개발자 hello hello 버전 toouse가 선택할 수 있습니다.
* 버전 세그먼트를 포함하지 않는 서비스 URL로(예: https://my.api) API를 구성할 수도 있습니다. 그런 다음 각 작업의 [URL 다시 쓰기](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) 템플릿에서 버전 세그먼트를 구성합니다. 예를 들어 /resource라는 [URL 템플릿](api-management-howto-add-operations.md#url-template) 및 /v1/Resource라는 [URL 다시 쓰기](api-management-howto-add-operations.md#rewrite-url-template) 템플릿이 포함된 작업을 가질 수 있습니다. 각 작업에 대해 별도로 hello 버전 세그먼트 값을 변경할 수 있습니다.
* 선택한 작업에 hello API의 서비스 URL에 "default" 버전 세그먼트 hello를 사용 하는 정책을 설정 tookeep 원하는 경우 [백 엔드 서비스 설정](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) 정책 toochange hello 백 엔드에서 요청 경로입니다.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>단일 API에서 여러 환경을 설정하려면 어떻게 해야 합니까?
tooset 다양 한 환경, 예: 테스트 환경 및 프로덕션 환경에서 단일 API 두 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

* 호스트에서 다른 Api hello 동일한 테 넌 트입니다.
* 호스트 hello 다른 테 넌 트에 동일한 Api입니다.

### <a name="can-i-use-soap-with-api-management"></a>API Management와 함께 SOAP를 사용할 수 있습니까?
이제 [SOAP 통과](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) 지원을 사용할 수 있습니다. 관리자는 hello 자신의 SOAP 서비스의 WSDL을 가져올 수 및 Azure API 관리에서는 SOAP 프런트 엔드를 만듭니다. 개발자 포털 설명서, 테스트 콘솔, 정책 및 분석을 SOAP 서비스에 모두 사용할 수 있습니다.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>Hello API 관리 게이트웨이 IP 주소 상수 인지 확인 그것을 방화벽 규칙에 사용할 수 있습니까?
Hello 공용 IP 주소 (VIP hello API 관리 테 넌 트의) hello 표준 및 프리미엄 계층에서 몇 가지 예외가 있는 hello 테 넌 트의 hello 수명에 대 한 정적가 됩니다. 이러한 상황에서는 hello IP 주소 변경:

* hello 서비스 삭제를 다시 생성 됩니다.
* hello 서비스 구독이 [일시 중단](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) 또는 [경고](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (예: 사용료) 다음 복원 하 고 있습니다.
* 추가 하거나 (hello Developer 및 Premium 계층에만 가상 네트워크 사용할 수 있음)는 Azure 가상 네트워크를 제거 합니다.

다중 지역 배포에 대 한 국가별 주소 변경 내용을 hello 영역이 비워진 되 고 다음 복원 하는 경우 hello (hello Premium 계층 에서만 다중 지역 배포 사용할 수 있음).

다중 지역 배포를 위해 구성된 프리미엄 계층 테넌트는 지역 당 하나의 공용 IP 주소에 할당됩니다.

Hello 테 넌 트 페이지 hello Azure 포털에서에서 IP 주소 (또는 다중 지역 배포에서 주소)을 얻을 수 있습니다.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>AD FS 보안을 통해 OAuth 2.0 권한 부여 서버를 구성할 수 있습니까?
tooconfigure Active Directory Federation Services (AD FS) 보안을 사용 하는 OAuth 2.0 권한 부여 서버를 확인 하려면 어떻게 toolearn [API 관리에서 사용 하 여 ADFS](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/)합니다.

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>API 관리에서 배포 toomultiple 지리적 위치에 어떤 라우팅 메서드를 사용 합니까?
API 관리에서는 hello [성능 트래픽 라우팅 방법](../traffic-manager/traffic-manager-routing-methods.md#priority) 배포 toomultiple 지리적 위치에 있습니다. 들어오는 트래픽을 라우트된 toohello 가장 가까운 API 게이트웨이입니다. 하나의 영역 오프 라인인 경우 들어오는 트래픽을 자동으로 라우팅된 toohello 다음 가장 가까운 게이트웨이입니다. [Traffic Manager 라우팅 방법](../traffic-manager/traffic-manager-routing-methods.md)에서 라우팅 방법에 대해 자세히 알아봅니다.

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>Azure 리소스 관리자 템플릿 toocreate API 관리 서비스 인스턴스를 사용할 수 있습니까?
예. Hello 참조 [Azure API 관리 서비스](http://aka.ms/apimtemplate) 퀵 스타트 템플릿.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>백 엔드에 대해 자체 서명된 SSL 인증서를 사용할 수 있습니까?
예. 어떻게 toouse는 자체 서명 된 SSL Secure Sockets Layer ()에 대해 인증서를 백 엔드 다음과 같습니다.

1. API Management를 사용하여 [백 엔드](https://msdn.microsoft.com/library/azure/dn935030.aspx) 엔터티를 만듭니다.
2. 집합 hello **skipCertificateChainValidation** 속성 너무**true**합니다.
3. Tooallow 자체 서명 된 인증서를 더 이상 사용 하지 않으려면 hello 백 엔드 엔터티를 삭제 하거나 hello 설정 **skipCertificateChainValidation** 속성 너무**false**합니다.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>왜 인증이 실패 하는 Git 리포지토리 tooclone 때?
Git 자격 증명 관리자를 사용 하는 경우 또는 Visual Studio를 사용 하 여 tooclone Git 리포지토리를 시도 하는 경우 hello Windows 자격 증명 대화 상자는 알려진된 문제가 발생할 수 있습니다. hello 대화 상자에 암호 길이 too127 문자 제한 하 고 hello Microsoft에서 생성 된 암호를 자릅니다. Hello 암호를 줄이는 작업 합니다. 지금은 사용 하십시오 Git Bash tooclone Git 리포지토리가 있습니다.

### <a name="does-api-management-work-with-azure-expressroute"></a>API Management는 Azure ExpressRoute와 함께 작동합니까?
예. API Management는 Azure ExpressRoute와 함께 작동합니다.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>API Management가 배포될 때 리소스 관리자 스타일 VNET에 전용 서브넷이 필요한 이유는 무엇인가요?
API 관리에 대 한 hello 전용된 서브넷 요구 사항 (PAAS V1 계층) 클래식 배포 모델을 기반으로 하는 hello 팩트에서 제공 됩니다. 에서는 리소스 관리자 VNET (V2 계층)에 배포할 수 있으며, 결과 toothat 가지 있습니다. hello Azure 클래식 배포 모델은 느슨한 hello 리소스 관리자 모델 등 V2 계층의 리소스를 만들 경우, hello V1 레이어 알지 못하기 및 toouse 이미 할당 된 IP를 시도 하는 API 관리와 같은 문제가 발생할 수 있습니다. tooa NIC (v 2에 작성 됨)입니다.
Azure 리소스 관리자 및 기본 모델의 차이 대 한 자세한 참조 너무 toolearn[배포 모델의 차이](../azure-resource-manager/resource-manager-deployment-model.md)합니다.

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>VNET에 API 관리를 배포할 때 필요한 hello 최소 서브넷 크기 이란?
hello 최소 서브넷 크기가 필요 toodeploy API 관리는 [/29](../virtual-network/virtual-networks-faq.md#configuration)를 지 원하는 Azure hello 최소 서브넷 크기를 변수인 합니다.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>하나의 구독 tooanother에서 API 관리 서비스를 이동할 수 있습니까?
예. toolearn를 확인 하려면 어떻게 해야 [리소스 tooa 새 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md)합니다.

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>내 API를 가져오는 데 제한 사항 또는 알려진 문제가 있나요?
Open API(Swagger), WSDL 및 WADL 형식에 대해 [알려진 문제 및 제한 사항](api-management-api-import-restrictions.md)입니다.
