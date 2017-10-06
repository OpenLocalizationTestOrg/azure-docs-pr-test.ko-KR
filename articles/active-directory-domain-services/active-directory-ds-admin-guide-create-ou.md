---
title: "Azure Active Directory Domain Services: 관리 가이드 | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 OU(조직 구성 단위) 만들기"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Azure AD 도메인 서비스 관리되는 도메인에 OU(조직 구성 단위) 만들기
Azure AD 도메인 서비스 관리되는 도메인에는 'AADDC 컴퓨터'와 'AADDC 사용자'라는 두 개의 기본 제공 컨테이너가 각각 있습니다. hello ' AADDC 컴퓨터가 ' 컨테이너에 있는 모든 컴퓨터에 대 한 컴퓨터 개체 가입 toohello 관리 되는 도메인입니다. hello ' AADDC Users' 컨테이너 hello Azure AD 테 넌 트에 사용자 및 그룹을 포함합니다. 경우에 따라 관리 되는 hello 도메인 toodeploy 워크 로드에 필요한 toocreate 서비스 계정 수 있습니다. 이 작업을 위해 hello 관리 되는 도메인에는 사용자 지정 조직 구성 단위 (OU)를 만들 있고 해당 OU 내에서 서비스 계정을 만듭니다. 이 문서에서는 관리 되는 도메인의 OU toocreate 합니다.

## <a name="before-you-begin"></a>시작하기 전에
이 문서에 나열 된 tooperform hello 작업 해야 합니다.

1. 유효한 **Azure 구독**.
2. **Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.
3. **Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다. 그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.
4. Hello Azure AD 도메인 서비스를 관리 하는 도메인에 가입 된 가상 컴퓨터는 도메인을 관리 합니다. 가상 컴퓨터에 없으면 hello 문서에 설명 된 모든 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.
5. hello 자격 증명이 필요는 **사용자 계정이 속하는 toohello ' AAD DC Administrators' 그룹** toocreate 관리 되는 도메인에서 사용자 지정 된 OU 디렉터리에 있습니다.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>도메인 가입된 가상 컴퓨터에 원격 관리를 위한 AD 관리 도구 설치
Azure AD 도메인 서비스 관리 되는 도메인 hello AD PowerShell 또는 관리 센터 ADAC (Active Directory)와 같은 친숙 한 Active Directory 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다. 테 넌 트 관리자에 원격 데스크톱을 통해 관리 되는 도메인 hello 권한 tooconnect toodomain 컨트롤러를 갖지 않습니다. tooadminister hello 관리 되는 도메인, 가상 컴퓨터에 가입된 toohello 관리 되는 도메인에 hello AD 관리 도구 기능을 설치 합니다. Toohello 문서 참조 [Azure AD 도메인 서비스는 관리 되는 도메인을 관리할](active-directory-ds-admin-guide-administer-domain.md) 지침에 대 한 합니다.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Hello 관리 되는 도메인에 조직 구성 단위 만들기
Hello AD 관리 도구가 설치 되어 했으므로 hello에 도메인에 가입 된 가상 컴퓨터, hello 관리 되는 도메인에서 이러한 도구 toocreate 조직 구성 단위를 사용할 수 있습니다. Hello 다음 단계를 수행 합니다.

> [!NOTE]
> Hello ' AAD DC Administrators' 그룹의 구성원만 사용자 지정 된 OU 필요한 권한이 toocreate hello 있어야 합니다. Hello toothis 그룹에 속한 사용자로 다음 단계를 수행 했는지 확인 합니다.
>
>

1. Hello 시작 화면에서 클릭 **관리 도구**합니다. Hello 가상 컴퓨터에 설치 하는 hello AD 관리 도구 표시 되어야 합니다.

    ![서버에 설치된 관리 도구](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. **Active Directory 관리 센터**를 클릭합니다.

    ![Active Directory 관리 센터](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooview hello 도메인 (예를 들어 ' contoso100.com') hello 왼쪽된 창에서 hello 도메인 이름을 클릭 합니다.

    ![ADAC - 도메인 보기](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Hello 오른쪽에 **작업** 창에서 클릭 **새로** hello 도메인 이름 노드 아래 합니다. 이 예제에서는 클릭 **새로** hello 오른쪽에 hello 'contoso100(local)' 노드 아래의 **작업** 창.

    ![ADAC - 새 OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Hello 옵션 toocreate 조직 구성 단위에 표시 됩니다. 클릭 **조직 구성 단위** toolaunch hello **조직 구성 단위 만들기** 대화 상자.
6. Hello에 **조직 구성 단위 만들기** 대화 상자에서 지정 된 **이름** 에 대 한 새 OU hello 합니다. Hello OU에 대 한 간략 한 설명을 제공 합니다. Hello를 설정할 수도 있습니다 **관리자** hello OU에 대 한 필드입니다. toocreate hello 사용자 지정 OU를 클릭 **확인**합니다.

    ![ADAC - OU 대화 상자 만들기](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. 이제 OU를 새로 만든 hello hello AD ADAC (관리 센터)에 나타납니다.

    ![ADAC - 만든 OU](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>새로 만든 OU에 대한 사용 권한/보안
사용자 지정 OU에 대해 관리자 권한 (모든 권한)을 부여는 hello 만든 hello 사용자 (hello AAD ' DC Administrators' 그룹의 구성원)는 기본적으로 OU hello 합니다. 그런 다음 hello 사용자 계속 진행 하 고 원하는 대로 toohello ' AAD DC Administrators' 그룹 또는 권한이 tooother 사용자 권한을 부여 수 있습니다. 다음 스크린 샷에서 hello와 같이 사용자 hello 'bob@domainservicespreview.onmicrosoft.com' 만든된 hello 새 'MyCustomOU' 조직 구성 단위 것에 대 한 모든 권한을 부여 받은 합니다.

 ![ADAC - 새 OU 보안](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>사용자 지정 OU 관리에 대한 참고 사항
이제 사용자 지정 OU를 만들었으므로 계속해서 이 OU에 사용자, 그룹, 컴퓨터 및 서비스 계정을 만들 수 있습니다. Hello ' AADDC Users' OU toocustom Ou에서에서 사용자 또는 그룹을 이동할 수 없습니다.

> [!WARNING]
> 사용자 지정 OU에서 만든 사용자 계정, 그룹, 서비스 계정 및 컴퓨터 개체는 Azure AD 테넌트에서 사용할 수 없습니다. 즉, 이러한 개체는 hello Azure AD Graph API를 사용 하 여 위나 hello Azure AD UI에서에서 표시 하지 않습니다. Azure AD Domain Services 관리되는 도메인에서만 이러한 개체를 사용할 수 있습니다.
>
>

## <a name="related-content"></a>관련 콘텐츠
* [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
* [관리되는 도메인에서 그룹 정책 구성](active-directory-ds-admin-guide-administer-group-policy.md)
* [Active Directory 관리 센터: 시작](https://technet.microsoft.com/library/dd560651.aspx)
* [서비스 계정 단계별 가이드](https://technet.microsoft.com/library/dd548356.aspx)
