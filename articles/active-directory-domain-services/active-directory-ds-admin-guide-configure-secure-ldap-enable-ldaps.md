---
title: "Azure AD 도메인 서비스에서 LDAP (LDAPS) Secure aaaConfigure | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성

## <a name="before-you-begin"></a>시작하기 전에
완료 했으면 확인 [작업 2-내보내기 hello 보안 LDAP 인증서 tooa 합니다. PFX 파일](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)합니다.

Toouse 미리 보기 포털 Azure 환경 hello Azure 클래식 포털 toocomplete이이 작업을 hello 하는지 여부를 선택 합니다.
> [!div class="op_single_selector"]
> * **Azure 포털 (미리 보기)**: [사용 hello Azure 포털을 사용 하 여 LDAP 보안](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Azure 클래식 포털**: [사용 hello 클래식 Azure 포털을 사용 하 여 LDAP 보안](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>작업 3-hello Azure 포털 (미리 보기)를 사용 하 여 hello 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정
tooenable 보안 LDAP에 hello 다음 구성 단계를 수행 합니다.

1. Toohello 이동  **[Azure 포털](https://portal.azure.com)**합니다.

2. '도메인 서비스' hello에 대 한 검색 **리소스 검색** 검색 상자입니다. 선택 **Azure AD 도메인 서비스** hello 검색 결과에서. hello **Azure AD 도메인 서비스** 블레이드에 관리 되는 도메인을 나열 합니다.

    ![프로비전되는 관리되는 도메인 찾기](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Hello 도메인에 대 한 자세한 내용은 hello 관리 되는 도메인 (예를 들어 ' contoso100.com') toosee의 hello 이름을 클릭 합니다.

    ![Domain Services - 프로비저닝 상태](./media/getting-started/domain-services-provisioning-state.png)

3. 클릭 **LDAP 보안** hello 탐색 창에서.

    ![Domain Services - 보안 LDAP 블레이드](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. 기본적으로 보안 LDAP 액세스 tooyour 관리 되는 도메인은 사용할 수 없습니다. 설정/해제 **LDAP 보안** 너무**사용**합니다.

    ![보안 LDAP를 사용하도록 설정](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. 기본적으로 보안 LDAP 액세스 tooyour 인터넷을 사용할 수 없습니다. hello를 통해 도메인을 관리 합니다. 설정/해제 **를 통해 보안 LDAP 액세스를 허용 hello 인터넷** 너무**사용**사용할 경우. 

6. Hello 폴더 아이콘 다음 클릭 **합니다. 보안 LDAP 인증서 인 PFX 파일이**합니다. 보안 LDAP 액세스 toohello 관리 되는 도메인에 대 한 hello 인증서로 hello toohello PFX 파일 경로 지정 합니다.

7. Hello 지정 **암호 toodecrypt 합니다. PFX 파일**합니다. Hello 제공 hello 인증서 toohello PFX 파일을 내보낼 때 사용한 동일한 암호입니다.

8. 완료 되 면 클릭 hello **저장** 단추입니다.

9. Hello 관리 되는 도메인에 대 한 보안 LDAP 구성 중인 알려 주는 알림이 표시 됩니다. 이 작업이 완료 될 때까지 hello 도메인에 대 한 다른 설정을 수정할 수 없습니다.

    ![Hello 관리 되는 도메인에 대 한 보안 LDAP를 구성합니다.](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> 관리 되는 도메인에 대 한 보안 LDAP tooenable 약 10 개 too15 분 걸립니다. Hello 제공 보안 LDAP 인증서가 일치 하지 않으면 hello 필수 조건, 보안 LDAP 디렉터리를 사용할 수 없습니다 및 오류가 표시 합니다. 예를 들어 hello 도메인 이름이 잘못 되었습니다, 그리고 hello 인증서가 이미 만료 되었거나 곧 만료 됩니다. 이 경우 유효한 인증서로 다시 시도해 보세요.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>작업 4-DNS tooaccess hello hello에서 관리 되는 도메인 구성 인터넷
> [!NOTE]
> **선택적 작업** -LDAPS를 사용 하 여 tooaccess hello 관리 되는 도메인 하지 않을 경우 넘는 인터넷 hello를이 구성 작업을 건너뜁니다.
>
>

이 작업을 시작 하기 전에 확인에 설명 된 hello 단계를 완료 한 [작업 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)합니다.

통해 보안 LDAP 액세스를 설정한 후 hello 인터넷 관리 되는 도메인에 필요한 tooupdate DNS 클라이언트 컴퓨터는 관리 되는이 도메인을 찾을 수 있도록 합니다. Hello에 표시 되는 외부 IP 주소 작업 3의 hello 끝 **속성** 블레이드 **외부 IP 주소에 대 한 LDAPS 액세스**합니다.

Hello의 hello DNS 이름을 도메인 (예를 들어 ' ldaps.contoso100.com') 포인트 toothis 외부 IP 주소를 관리 하므로 외부 DNS 공급자를 구성 합니다. 예에서 toocreate hello DNS 항목을 수행 해야 합니다.

    ldaps.contoso100.com  -> 52.165.38.113

이제 끝났습니다-현재 위치 관리 되는 준비 tooconnect toohello는를 통해 보안 LDAP를 사용 하 여 도메인에 인터넷 hello 합니다.

> [!WARNING]
> 클라이언트 컴퓨터가 hello LDAPS 인증서 toobe 수 tooconnect의 hello 발급자를 성공적으로 신뢰 해야 기억 toohello LDAPS를 사용 하 여 도메인을 관리 합니다. 공개적으로 신뢰할 수 있는 인증 기관을 사용 하는 경우 불필요 toodo 아무 것도 하므로 이러한 인증서 발급자를 신뢰 하는 클라이언트 컴퓨터입니다. 자체 서명 된 인증서를 사용 하는 경우 hello 자체 서명 된 인증서의 공개 부분이 hello hello 신뢰할 수 있는 인증서 저장소 hello 클라이언트 컴퓨터에 설치 합니다.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>작업 5-잠금 LDAPS 액세스 tooyour 관리 되는 도메인을 통해 인터넷 hello
> [!NOTE]
> **선택적 작업** -LDAPS를 설정 하지 않은 경우 액세스 toohello 관리 되는 도메인 넘는 인터넷 hello,이 구성 작업을 건너뜁니다.
>
>

이 작업을 시작 하기 전에 확인에 설명 된 hello 단계를 완료 한 [작업 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)합니다.

LDAPS 액세스를 위한 관리 되는 도메인 hello를 통해 노출 인터넷 보안 위협이 나타냅니다. hello 관리 되는 도메인은 hello에서 연결할 수 있는 보안 LDAP에 사용 되는 hello 포트에서 인터넷 (즉, 636 포트). 따라서 toorestrict 액세스 관리 toohello 도메인 toospecific 알려진 IP 주소를 선택할 수 있습니다. 보안 향상된을 위해 NSG ()를 네트워크 보안 그룹을 만들고 Azure AD 도메인 서비스를 설정한 hello 서브넷과 연결 합니다.

hello 다음 표에서 설명 샘플 NSG를 구성할 수 hello 통해 보안 LDAP 액세스 아래로 toolock 인터넷 합니다. hello NSG에는 TCP 포트를 통해 636 지정된 된 집합 에서만에서 IP 주소의 인바운드 LDAPS 액세스를 허용 하는 규칙 집합이 포함 되어 있습니다. hello 기본 'DenyAll' 규칙 적용 tooall 인바운드 트래픽을 다른 hello에서 인터넷 합니다. hello NSG 규칙 tooallow LDAPS 액세스 hello 통해 지정 된 IP 주소에서 인터넷에 hello DenyAll NSG 규칙 보다 우선 순위가 높습니다.

![샘플 NSG toosecure LDAPS 액세스를 통해 인터넷 hello](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**자세한 정보** - [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>관련 콘텐츠
* [Azure AD Domain Services - 시작 가이드](active-directory-ds-getting-started.md)
* [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
* [Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리](active-directory-ds-admin-guide-administer-group-policy.md)
* [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)
* [네트워크 보안 그룹 만들기](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
