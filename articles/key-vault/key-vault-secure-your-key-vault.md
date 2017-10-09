---
title: "키 자격 증명 모음 aaaSecure | Microsoft Docs"
description: "자격 증명 모음, 키 및 암호를 관리하기 위한 키 자격 증명 모음의 액세스 권한을 관리합니다. 키 자격 증명 모음과 어떻게 toosecure 키 자격 증명 모음에 대 한 인증 및 권한 부여 모델"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>키 자격 증명 모음 보안
Azure Key Vault는 클라우드 응용 프로그램에 대한 암호화 키와 암호(예: 인증서, 연결 문자열, 암호)를 보호하는 클라우드 서비스입니다. 이 데이터와 중요 한 비즈니스 있으므로 응용 프로그램 인증 된 있도록 toosecure 액세스 tooyour 키 자격 증명 모음을 원하는 되 고 사용자가 키 자격 증명 모음에 액세스할 수 있습니다. 이 문서에서는 주요 자격 증명 모음 액세스 모델에 대해 간략하게 설명 하 고, 인증 및 권한 부여에 설명, toosecure 액세스 tookey 첫 번째 예 클라우드 응용 프로그램에 대 한 자격 증명 모음에 방법을 설명 합니다.

## <a name="overview"></a>개요
두 개의 별도 인터페이스를 통해 제어 됩니다 액세스 tooa 키 자격 증명 모음: 평면 관리 및 데이터 평면입니다. 두 평면이 대 한 적절 한 인증 및 권한 부여 그래야를 (사용자 또는 응용 프로그램) 호출자 액세스 tookey 자격 증명 모음을 가져올 수 있습니다. 인증은 어떤 작업 hello 호출자가 tooperform 허용 권한 부여 결정 하는 동안 hello 호출자의 hello id를 설정 합니다.

인증을 위해 데이터 평면과 관리 평면 모두 Azure Active Directory를 사용합니다. 권한 부여를 위해서는 관리 평면에서 RBAC(역할 기반 액세스 제어)를 사용하는 반면 데이터 평면에서는 키 자격 증명 모음 액세스 정책을 사용합니다.

Hello 주제를 다룹니다의 간략 한 개요는 다음과 같습니다.

[Azure Active Directory를 사용 하 여 인증](#authentication-using-azure-active-directory) -이 섹션에서는 호출자가 인증 하는 방법을 Azure Active Directory tooaccess 평면 관리 및 데이터 평면을 통해 주요 자격 증명 모음에 설명 합니다. 

[관리 평면 및 데이터 평면](#management-plane-and-data-plane) - 관리 평면과 데이터 평면은 키 자격 증명 모음에 액세스하는 데 사용되는 두 액세스 평면입니다. 각 액세스 평면마다 특정 작업을 지원합니다. 이 섹션에서는 hello 액세스 끝점을 설명, 지원 및 액세스 제어 방법 각 평면에서 사용 하는 작업을 합니다. 

[평면 액세스 제어 관리](#management-plane-access-control) -역할 기반 액세스 제어를 사용 하 여 toomanagement 평면 작업 액세스를 허용 하는에서 살펴보게이 섹션에 있습니다.

[데이터 평면 액세스 제어](#data-plane-access-control) -이 섹션에서는 toouse 주요 자격 증명 모음 액세스 정책 toocontrol 데이터 액세스를 평면 하는 방법을 설명 합니다.

[예제](#example) -이 예제에서는 toosetup 주요 자격 증명 모음 tooallow 3 다른 팀 (보안 팀, 개발자/연산자 및 감사자)에 대 한 제어를 액세스 하는 방법을 설명 tooperform 특정 작업 toodevelop 관리 하 고 Azure에서 응용 프로그램 모니터링 .

## <a name="authentication-using-azure-active-directory"></a>Azure Active Directory를 통한 인증
Azure 구독에서 주요 자격 증명 모음을 만들 때 자동으로 hello 구독의 Azure Active Directory 테 넌 트와 연결 됩니다. 모든 호출자가 (사용자 및 응용 프로그램) 해야이 주요 자격 증명 모음을이 테 넌 트 tooaccess에 등록 합니다. 응용 프로그램 또는 사용자는 Azure Active Directory tooaccess 키 자격 증명 모음에 인증 해야 합니다. 이 적용 됩니다 tooboth 관리 평면 및 데이터 평면 액세스 합니다. 두 경우 모두 응용 프로그램에서 다음과 같은 두 가지 방법으로 키 자격 증명 모음에 액세스할 수 있습니다.

* **사용자 + 앱 액세스** - 대개 로그인한 사용자를 대신하여 키 자격 증명 모음에 액세스하는 응용 프로그램에서 사용하는 방법입니다. Azure PowerShell과 Azure Portal은 이러한 액세스 유형의 예입니다. 두 가지 toogrant 액세스 toousers:는 한 가지 방법은 toogrant 액세스 toousers 주요 자격 증명 모음 모든 응용 프로그램에서 액세스할 수 있도록 이며 hello 다른 방법으로 사용자 액세스 tookey 자격 증명 모음 toogrant 특정 응용 프로그램 (참조 tooas 복합 id)를 사용 하는 경우에 합니다. 
* **응용 프로그램 전용 액세스** -응용 프로그램이 있는지 daemon 서비스를 실행 등 hello 응용 프로그램의 id에 부여 하는 백그라운드 작업 액세스 toohello 자격 증명 모음 키입니다.

두 종류의 응용 프로그램에서 hello를 사용 하 여 Azure Active Directory와 hello 응용 프로그램 인증 [지원 되는 인증 방법](../active-directory/active-directory-authentication-scenarios.md) 하며 토큰을 가져옵니다. 사용 된 인증 방법 hello 응용 프로그램 종류에 따라 달라 집니다. 그런 다음 hello 응용 프로그램이이 토큰을 사용 하 고 REST API 요청 tookey 자격 증명 모음을 보냅니다. 관리 평면 액세스 hello 발생 한 경우 요청은 Azure 리소스 관리자 끝점을 통해 라우팅됩니다. 평면 데이터에 액세스할 때는 직접 tooa 주요 자격 증명 모음 끝점 hello 응용 프로그램 설명 합니다. Hello에 자세한 내용을 보려면 [전체 인증 흐름](../active-directory/active-directory-protocols-oauth-code.md)합니다. 

hello 리소스 이름을 hello 응용 프로그램 토큰을 요청 하는 관리 평면 또는 데이터 평면 hello 응용 프로그램에 액세스 하는지 여부에 따라 다릅니다. 따라서 hello 리소스 이름이 hello Azure 환경에 따라 이후 섹션에서 hello 표에 설명 된 두 관리 평면 또는 데이터 평면 끝점입니다.

인증 tooboth에 대 한 단일 메커니즘 중 하나에 있는 관리 및 데이터 평면 자체 이점은 다음과 같습니다.

* 조직은 액세스 tooall 키 자격 증명 모음은 조직의 중앙에서 제어 수 있습니다.
* 사용자가 이러한 즉시 액세스 권한이 손실 hello 조직에서 tooall에 키 자격 증명 모음.
* 조직에 인증 hello 옵션 Azure Active Directory (예를 들어 권한 부여에 대해 multi-factor authentication 추가 보안)을 통해 사용자 지정할 수 있습니다.

## <a name="management-plane-and-data-plane"></a>관리 평면 및 데이터 평면
Azure Key Vault는 Azure Resource Manager 배포 모델을 통해 사용할 수 있는 Azure 서비스입니다. 키 자격 증명 모음을 만들면 키, 암호 및 인증서와 같은 다른 개체를 만들 수 있는 가상 컨테이너가 생깁니다. 그런 다음 관리 평면 및 데이터 평면 tooperform 특정 작업을 사용 하 여 주요 자격 증명 모음에 액세스할 수 있습니다. 관리 평면 인터페이스는 키 자격 증명 모음에 만들기, 삭제, 주요 자격 증명 모음 특성을 업데이트 및 데이터 평면에 대 한 액세스 정책을 설정 같은 자체 사용된 toomanage입니다. 데이터 평면 인터페이스는 사용 되는 tooadd, 삭제, 수정 및 hello 키, 암호, 및 주요 자격 증명 모음에 저장 된 인증서를 사용 합니다.

hello 관리 평면 및 데이터 평면 인터페이스 (표 참조) 다른 끝점을 통해 액세스 됩니다. hello hello 테이블의 두 번째 열에 서로 다른 Azure 환경에서 이러한 끝점에 대 한 hello DNS 이름을 설명합니다. hello 세 번째 열에는 각 액세스 평면에서 수행할 수 있습니다 하는 hello 작업 설명 합니다. 또한 각 액세스 평면에는 자체 액세스 제어 메커니즘이 있습니다. 즉 관리 평면 액세스 제어는 Azure Resource Manager RBAC(역할 기반 액세스 제어)를 통해 설정되고, 데이터 평면 액세스 제어는 키 자격 증명 모음 액세스 정책을 통해 설정됩니다.

| 액세스 평면 | 액세스 끝점 | 작업 | 액세스 제어 메커니즘 |
| --- | --- | --- | --- |
| 관리 평면 |**전역:**<br> management.azure.com:443<br><br> **Azure 중국:**<br> management.chinacloudapi.cn:443<br><br> **Azure 미국 정부:**<br> management.usgovcloudapi.net:443<br><br> **Azure 독일:**<br> management.microsoftazure.de:443 |키 자격 증명 모음 만들기/읽기/업데이트/삭제 <br> 키 자격 증명 모음에 대한 액세스 정책 설정<br>키 자격 증명 모음에 대한 태그 설정 |Azure Resource Manager RBAC |
| 데이터 평면 |**전역:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure 중국:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure 미국 정부:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure 독일:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |키: 암호 해독, 암호화, UnwrapKey, WrapKey, 확인, 로그인, 권한 가져오기, 목록 표시, 업데이트, 만들기, 가져오기, 삭제, 백업, 복원<br><br> 암호: 권한 가져오기, 목록 표시, 설정, 삭제 |키 자격 증명 모음 액세스 정책 |

hello 관리 평면 및 데이터 평면 액세스 제어 독립적으로 작동합니다. 예를 들어 키 자격 증명 모음에 응용 프로그램 액세스 toouse 키 toogrant 원하는 toogrant 데이터 평면 액세스 권한을 주요 자격 증명 모음 액세스 정책을 사용 하면 및이 응용 프로그램에 필요한 관리 평면 액세스할 수 없습니다. 및 반대로 사용자 toobe 수 하려면 tooread 자격 증명 모음에 속성 및 태그 하는데 모든 액세스 tookeys, 비밀 정보 또는 인증서가 없는,이 사용자 권한을 부여할 수 있습니다, '읽기' 없는 액세스 toodata 평면을 RBAC를 사용 하 여 액세스가 필요 합니다.

## <a name="management-plane-access-control"></a>관리 평면 액세스 제어
hello 관리 평면 hello 주요 자격 증명 모음 자체에 영향을 주는 작업으로 구성 됩니다. 예를 들어 키 자격 증명 모음을 만들거나 삭제할 수 있습니다. 구독에서 자격 증명 모음 목록을 가져올 수 있습니다. 주요 자격 증명 모음 속성 (예: SKU, 태그)를 검색 하 고 hello 사용자 및 키와 암호 hello 키 자격 증명 모음에 액세스할 수 있는 응용 프로그램을 제어 하는 액세스 정책을 주요 자격 증명 모음을 설정할 수 있습니다. 관리 평면 액세스 제어는 RBAC를 사용합니다. 이전 섹션에서 hello 표에 평면 관리를 통해 수행할 수 있는 주요 자격 증명 모음 작업의 전체 목록은 hello를 참조 하십시오. 

### <a name="role-based-access-control-rbac"></a>RBAC(역할 기반 액세스 제어)
각 Azure 구독에는 Azure Active Directory가 있습니다. 사용자, 그룹 및이 디렉터리에서 응용 프로그램 hello Azure 리소스 관리자 배포 모델을 사용 하는 hello Azure 구독에에서 대 한 액세스 toomanage 리소스를 부여할 수 있습니다. 이 액세스 제어 유형은 참조 tooas 역할 기반 액세스 제어 (RBAC)입니다. toomanage 액세스이 hello를 사용할 수 있습니다 [Azure 포털](https://portal.azure.com/), hello [Azure CLI 도구](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), 또는 hello [Azure리소스관리자RESTApi](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Hello Azure 리소스 관리자 모델에서는 Azure Active Directory를 사용 하 여 리소스 그룹 및 컨트롤 액세스 toohello 관리 평면에서이 주요 자격 증명 모음의 주요 자격 증명 모음을 만듭니다. 예를 들어, 사용자 또는 그룹 기능 toomanage 키 자격 증명 모음 특정 리소스 그룹에 부여할 수 있습니다.

적절 한 RBAC 역할을 할당 하 여 액세스 toousers, 그룹 및 특정 범위의 응용 프로그램에 부여할 수 있습니다. 예를 들어 toogrant 액세스할 tooa 사용자 toomanage 키 자격 증명 모음 toothis 사용자 특정 범위에는 미리 정의 된 역할 '주요 자격 증명 모음 참가자'를 지정할 수 있습니다. 구독, 리소스 그룹 또는 특정 키 자격 hello 범위 수는 경우. 구독 수준에서 할당 된 역할은 tooall 리소스 그룹 및 해당 구독 내의 리소스에 적용 됩니다. 리소스 그룹 수준에서 할당 된 역할은 해당 리소스 그룹에서 tooall 리소스에 적용 됩니다. 특정 리소스에 대 한 할당 된 역할에는 toothat 리소스만을 적용 됩니다. 몇 가지 미리 정의 된 역할 (참조 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)), 미리 정의 된 역할 hello 경우 및 역할을 직접 정의할 수도 있습니다 필요에 맞게 하지 않습니다.

> [!IMPORTANT]
> 사용자에 게 참가자 권한을 (RBAC) tooa 주요 자격 증명 모음 관리 평면 경우 그녀 부여할 수 있는 자신 액세스 toodata 평면 toodata 평면 액세스를 제어 하는 주요 자격 증명 모음 액세스 정책을 설정 하 여 note 합니다. 따라서이 '참가자' 액세스 tooyour 키 자격 증명 모음 tooensure만 권한이 있는 사용자를 액세스 하 고 키 자격 증명 모음, 키, 암호, 및 인증서를 관리할 수 있는 사람을 tootightly 제어를 좋습니다.
> 
> 

## <a name="data-plane-access-control"></a>데이터 평면 액세스 제어
hello 주요 자격 증명 모음 데이터 평면 키 자격 증명 모음, 키, 암호, 인증서 등의 hello 개체에 영향을 주는 작업으로 구성 됩니다.  여기에는 키 작업(키 만들기, 가져오기, 업데이트, 목록 표시, 백업 및 복원), 암호화 작업(로그인, 확인, 암호화, 암호 해독, 래핑 및 래핑 해제), 키의 태그 및 기타 속성 설정이 포함됩니다. 마찬가지로 암호에 대해서는 권한 가져오기, 설정, 목록 표시 및 삭제가 포함됩니다.

데이터 평면 액세스 권한은 키 자격 증명 모음에 대한 액세스 정책을 설정함으로써 부여됩니다. 사용자, 그룹 또는 응용 프로그램에 해당 키 자격 증명 모음에 대 한 주요 자격 증명 모음 toobe 수 tooset 액세스 정책에 대 한 관리 평면에 대 한 (RBAC) 참가자 권한이 있어야 합니다. 사용자, 그룹 또는 응용 프로그램 액세스 키 또는 키 자격 증명 모음의 암호에 대 한 특정 작업 tooperform 부여할 수 있습니다. 주요 자격 증명 모음 키 자격 증명 모음에 대 한 too16 액세스 정책 항목을를 지원 합니다. Azure Active Directory 보안 그룹을 만들고 사용자 toothat 그룹 toogrant 데이터 평면 액세스 tooseveral 사용자 tooa 주요 자격 증명 모음을 추가 합니다.

### <a name="key-vault-access-policies"></a>키 자격 증명 모음 액세스 정책
주요 자격 증명 모음 액세스 정책 사용 권한 tookeys, 암호 및 인증서를 개별적으로 부여합니다. 예를 들어 사용자 액세스 tooonly 키 하지만 비밀 정보에 대 한 사용 권한 없음를 제공할 수 있습니다. 그러나 권한 tooaccess 키 또는 암호 또는 인증서 hello 자격 증명 모음 수준에서 됩니다. 즉 키 자격 증명 모음 액세스 정책에서는 개체 수준 권한을 지원하지 않습니다. 사용할 수 있습니다 [Azure 포털](https://portal.azure.com/), hello [Azure CLI 도구](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), 또는 hello [주요 자격 증명 모음 관리 REST Api](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset 액세스 정책 에 대 한 주요 자격 증명 모음입니다.

> [!IMPORTANT]
> 주요 자격 증명 모음 액세스 정책 hello 자격 증명 모음 수준에서 적용 되는 note 합니다. 예를 들어 사용자 toocreate 및 delete 키를 권한이 부여 되는 키 자격 증명 모음에 모든 키에 해당 작업을 수행할 수 그녀.
> 
> 

## <a name="example"></a>예제
SSL에는 인증서를, 데이터 저장에는 Azure 저장소를, 로그인 작업에는 RSA 2048비트 키를 사용하는 응용 프로그램을 개발하고, VM(또는 VM 확장 집합)에서 이 응용 프로그램을 실행한다고 가정해 보겠습니다. 응용 프로그램 암호 및 키 자격 증명 모음 toostore hello 부트스트랩 인증서 사용에서 Azure Active Directory와 응용 프로그램 tooauthenticate hello 사용 되는 hello 모든 주요 자격 증명 모음 toostore를 사용할 수 있습니다.

따라서 여기에 키 자격 증명 모음에 저장 된 모든 hello 키와 암호 toobe 간략하게 합니다.

* **SSL 인증서** - SSL에 사용
* **저장소 키** -tooget 액세스 tooStorage 계정 사용
* **RSA 2048비트 키** - 로그인 작업에 사용
* **부트스트랩 인증서** -서명에 tooauthenticate tooAzure Active Directory, tooget 액세스 tookey 자격 증명 모음 toofetch hello 저장소 키 및 사용 하 여 hello RSA 키 사용 합니다.

이제 회의가 hello 사용자에 게 관리, 배포 및이 응용 프로그램을 감사 합니다. 이 예제에서는 세 가지 역할을 사용합니다.

* **보안 팀** -hello '사무실의 hello CSO (Chief 보안 책임자)'에서 IT 담당자는 일반적으로 또는 해당 하는, 담당 환영 보안의 적합 한 안전 하 게 보관와 같은 SSL 인증서를 서명에 대 한 연결 문자열 사용 되는 RSA 키 데이터베이스, 저장소 계정 키입니다.
* **개발자/연산자** -이이 응용 프로그램을 개발 하 고 다음 Azure에서 배포 hello 직원입니다. 일반적으로,은 hello 보안 팀의 일부가 아닌 및 따라서 권한이 없어야 액세스 tooany 중요 한 데이터를 SSL 인증서의 RSA 키 하지만 배포할 hello 응용 프로그램 액세스 toothose 있어야 합니다.
* **감사자** -이 일반적으로 다양 한 사람, 일반 IT 담당자와 hello 개발자에서 격리 합니다. 책임은 tooreview 적절 한 사용 및 인증서, 키 등의 유지 관리 이며 데이터 보안 표준 준수를 확인 합니다. 

더 많은 하나의 역할이이 응용 프로그램, 하지만 언급 했 듯이 여기서 toobe 관련의 외부 hello 범위 이며 되는 hello 구독 (또는 리소스 그룹) 관리자입니다. 구독 관리자 hello 보안 팀에 대 한 초기 액세스 권한을 설정합니다. 여기에서는 해당 hello 구독 관리자는이 응용 프로그램 reside에 필요한 리소스 hello 모든 액세스 toohello 보안 팀 tooa 리소스 그룹에 부여 가정 합니다.

이제이 응용 프로그램의 hello 컨텍스트에서 각 역할을 수행 하는 동작을 살펴보겠습니다.

* **보안 팀**
  * 키 자격 증명 모음 만들기
  * 키 자격 증명 모음 로깅 사용 설정
  * 키/암호 추가
  * 재해 복구를 위한 키 백업 만들기
  * 주요 자격 증명 모음 액세스 정책 toogrant 권한 toousers 및 응용 프로그램 tooperform 특정 작업 설정
  * 주기적 키/암호 롤백
* **개발자/운영자**
  * 참조 toobootstrap 및 SSL 인증서 (지문) 저장소 키 (비밀 URI) 및 서명 키 (키 URI) 보안 팀에서 가져오기
  * 프로그래밍 방식으로 키와 암호에 액세스하는 응용 프로그램 개발 및 배포
* **감사자**
  * 사용 현황 로그 tooconfirm 적절 한 키/암호 사용 및 데이터 보안 표준 준수를 검토 합니다.

이제 어떤 액세스 권한을 tookey 자격 증명 모음 각 역할 (및 hello 응용 프로그램)에 필요한를 확인해 보겠습니다 tooperform 배정된 된 작업입니다. 

| 사용자 역할 | 관리 평면 사용 권한 | 데이터 평면 사용 권한 |
| --- | --- | --- |
| 보안 팀 |키 자격 증명 모음 참가자 |키: 백업, 만들기, 삭제, 권한 가져오기, 가져오기, 목록 표시, 복원 <br> 암호: 모두 |
| 개발자/운영자 |주요 자격 증명 모음 배포할 hello Vm hello 키 자격 증명 모음에서 암호를 인출할 수 있도록 권한 배포 |없음 |
| 감사자 |없음 |키: 목록 표시<br>암호: 목록 표시 |
| 응용 프로그램 |없음 |키: 로그인<br>암호: 권한 가져오기 |

> [!NOTE]
> 키와 하지 태그와 같은 hello 로그에서 발생 하는 암호에 대 한 특성을 검사할 수 있도록 감사자에 게 필요한 목록 권한이 키 및 암호에 대 한 정품 인증 및 만료 날짜입니다.
> 
> 

사용 권한 tookey 자격 증명 모음 외에도 세 역할이 모두 리소스에도 필요 액세스할 tooother 합니다. 예를 들어 toobe 수 toodeploy Vm (또는 웹 응용 프로그램 등.) 개발자/연산자 '참가자' 액세스 toothose 리소스 종류를 해야합니다. 감사자 필요 읽기 액세스 toohello 저장소 계정 hello 주요 자격 증명 모음 로그 저장 됩니다.

이 문서의 hello 핵심 액세스 tooyour 자격 증명 모음 키를 보호 하 고, 이후 것만 toothis 주제와 관련 된 hello 관련 부분 및 인증서를 배포, 키 및 암호를 프로그래밍 방식으로 등 액세스에 대 한 내용을 건너뛸입니다. 이러한 내용은 이미 다른 곳에서 다루고 있습니다. 에 대해서는 tooVMs 주요 자격 증명 모음에에서 저장 된 인증서를 배포는 [블로그 게시물](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/), 있으면 [샘플 코드](https://www.microsoft.com/download/details.aspx?id=45343) 사용할 수 있는 방법을 보여 주는 toouse 부트스트랩 tooauthenticate tooAzure AD tooget 인증서 하는 방법 액세스 tookey 자격 증명 모음입니다.

Azure 포털을 사용 하 여 대부분의 hello 액세스 권한 부여할 수 있지만 결과 원하는 toogrant 세부적인 권한을 toouse Azure PowerShell (또는 Azure CLI) tooachieve hello를 할 수 있습니다. 

다음 PowerShell 코드 조각을 hello 가정 합니다.

* Azure Active Directory 관리자에 게 역할 hello 3 Contoso 응용 프로그램 감사자 즉 Contoso 응용 프로그램 Devops Contoso 보안 팀을 나타내는 보안 그룹을 만들었습니다. 관리자에 게는 자신이 속한 사용자 toohello 그룹도 추가 했습니다.
* **ContosoAppRG** hello 리소스를 모두 있는 hello 리소스 그룹입니다. **contosologstorage** hello 로그 저장 됩니다. 
* 주요 자격 증명 모음 **ContosoKeyVault** 및 주요 자격 증명 모음 로그에 사용 되는 저장소 계정 **contosologstorage** hello에 있어야 동일한 Azure 위치

첫 번째 관리자에 게 구독 '참가자 자격 증명 모음 키' 및 ' 사용자 액세스 관리자 ' 역할 toohello 보안 팀에 할당합니다. 이 hello 보안 팀 toomanage tooother 리소스에 액세스를 허용 하 고 ContosoAppRG hello 리소스 그룹에서 주요 자격 증명 모음을 관리 합니다.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

hello 다음 스크립트에서는 hello 보안 팀 수 키 자격 증명 모음 만들기, 로깅, 설치 및 다른 역할과 hello 응용 프로그램에 대 한 액세스 권한을 설정 하는 방법을 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

hello 사용자 지정 역할 정의 할당할 수 있는 toohello 구독만 hello ContosoAppRG 리소스 그룹이 생성 됩니다. Hello 동일한 사용자 정의 역할에 사용할 다른 구독에서 다른 프로젝트를 하는 경우의 범위 추가 구독을 더 있을 수 있습니다.

hello 개발자/hello "배포/작업" 권한에 대 한 연산자에 대 한 hello 사용자 지정 역할 할당은 범위가 지정 된 toohello 리소스 그룹입니다. 이러한 방식으로 hello Vm만 'ContosoAppRG' hello 암호 (SSL 인증서 및 부트스트랩 cert) 받아볼 hello 리소스 그룹에 만들어집니다. 개발/자동화할 팀의 멤버가 다른 리소스 그룹에 만들어지는 모든 Vm 됩니다 수 tooget 이러한 암호 hello 비밀 Uri 임을 알고 있는 경우에 합니다.

이 예제에서는 간단한 시나리오를 보여 줍니다. 실제 시나리오는 더 복잡 해질 수 있습니다 및 tooadjust 권한을 tooyour 키 자격 증명 모음 요구 사항에 따라 할 수 있습니다. 예를 들어 예제에서는 해당 보안 팀에서는 hello 키와 비밀 참조 (Uri 및 지문이) 응용 프로그램에 해당 개발자/연산자 팀 필요 tooreference 가정 했습니다. 따라서 않아도 toogrant 개발자/연산자는 모든 데이터 평면 액세스 합니다. 또한 이 예제에서는 키 자격 증명 모음 보호에 중점을 둡니다. 비슷한 고려해 야 toosecure [Vm](https://azure.microsoft.com/services/virtual-machines/security/), [저장소 계정은](../storage/common/storage-security-guide.md) 및 다른 Azure 리소스 너무 합니다.

> [!NOTE]
> 참고: 이 예제에서는 프로덕션 환경에서 키 자격 증명 모음 액세스를 잠글 수도 있습니다. hello 개발자 있어야 자신의 구독 또는 리소스 그룹에 있는 모든 권한을 toomanage 자신의 자격 증명 모음, Vm 및 저장소 계정을 hello 응용 프로그램을 개발 하 합니다.
> 
> 

## <a name="resources"></a>리소스
* [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)
  
  이 문서에서는 hello 설명 Azure Active Directory 역할 기반 액세스 제어 및 청구 방식입니다.
* [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)
  
  이 문서 세부 정보를 모든 hello RBAC에 사용할 수 있는 기본 제공 역할입니다.
* [리소스 관리자 배포 및 클래식 배포 이해](../azure-resource-manager/resource-manager-deployment-model.md)
  
  이 문서는 hello 리소스 관리자 배포 및 클래식 배포 모델에 설명 하 고 hello 리소스 관리자 및 리소스 그룹을 사용 하 여 hello 이점을 설명합니다
* [Azure PowerShell을 사용하여 역할 기반 액세스 제어 관리](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  이 문서에서는 Azure PowerShell을 사용한 제어 toomanage 역할 기반 액세스 하는 방법을 설명합니다
* [Hello REST API로 역할 기반 액세스 제어 관리](../active-directory/role-based-access-control-manage-access-rest.md)
  
  이 문서에서는 toouse REST API toomanage RBAC hello 하는 방법을 보여 줍니다.
* [Ignite를 사용한 Microsoft Azure에 대한 역할 기반 액세스 제어](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  이 hello 2015 MS Ignite 컨퍼런스에서 Channel 9 비디오 링크 tooa는입니다. 이 세션에 대 한 이야기 관리 및 Azure의 보고 기능에 액세스 하 고 Azure Active Directory를 사용 하 여 tooAzure 구독 액세스 보안에 대 한 모범 사례를 탐색 합니다.
* [OAuth 2.0 및 Azure Active Directory를 사용 하 여 tooweb 응용 프로그램 액세스 권한 부여](../active-directory/active-directory-protocols-oauth-code.md)
  
  이 문서에서는 Azure Active Directory로 인증하기 위한 OAuth 2.0 흐름 전체에 대해 설명합니다.
* [키 자격 증명 모음 관리 REST API](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  이 문서는 키 자격 증명 모음에 프로그래밍 방식으로 키 자격 증명 모음 액세스 정책 설정을 비롯 한 hello REST Api toomanage에 대 한 hello 참조입니다.
* [ 키 자격 증명 모음 REST API](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  링크 tookey 자격 증명 모음 REST API 참조 설명서입니다.
* [키 액세스 제어](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  링크 tooSecret 액세스 제어 참조 설명서입니다.
* [암호 액세스 제어](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  링크 tooKey 액세스 제어 참조 설명서입니다.
* PowerShell을 사용하여 키 자격 증명 모음 액세스 정책 [설정](https://msdn.microsoft.com/library/mt603625.aspx) 및 [제거](https://msdn.microsoft.com/library/mt619427.aspx)
  
  PowerShell cmdlet toomanage 주요 자격 증명 모음 액세스 정책에 대 한 링크 tooreference 설명서입니다.

## <a name="next-steps"></a>다음 단계
관리자를 위한 시작 자습서에 대해서는 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md)을 참조하십시오.

키 자격 증명 모음의 사용 현황 로깅에 대한 자세한 내용은 [Azure 키 자격 증명 모음 로깅](key-vault-logging.md)을 참조하십시오.

Azure 키 자격 증명 모음에서 키 및 암호를 사용하는 방법에 대한 자세한 내용은 [키 및 암호 정보](https://msdn.microsoft.com/library/azure/dn903623.aspx)를 참조하십시오.

주요 자격 증명 모음에 대 한 질문이 있으면 방문 hello [Azure 키 자격 증명 모음 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

