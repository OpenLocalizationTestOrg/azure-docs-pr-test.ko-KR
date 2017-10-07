---
title: "Azure Active Directory Domain Services: 관리되는 도메인에서 그룹 정책 관리 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 그룹 정책 관리"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리
Azure Active Directory 도메인 서비스는 hello ' AADDC 사용자 ' 및 ' AADDC 컴퓨터 ' 컨테이너에 대 한 기본 제공 그룹 정책 개체 (Gpo)를 포함합니다. 이러한 기본 제공 Gpo tooconfigure hello 관리 되는 도메인의 그룹 정책은 사용자 지정할 수 있습니다. 또한 hello ' AAD DC Administrators' 그룹의 구성원 hello 관리 되는 도메인에 자체 사용자 지정 Ou를 만들 수 있습니다. 사용자 지정 Gpo를 만들 수 있고 toothese 사용자 지정 연결은 Ou입니다. Toohello ' AAD DC Administrators' 그룹에 속한 사용자는 hello 관리 되는 도메인에 대 한 그룹 정책 관리 권한은 부여 됩니다.

## <a name="before-you-begin"></a>시작하기 전에
이 문서에 나열 된 tooperform hello 작업 해야 합니다.

1. 유효한 **Azure 구독**.
2. **Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.
3. **Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다. 그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.
4. A **가상 컴퓨터를 도메인에 가입 된** hello Azure AD 도메인 서비스 관리 되는 도메인에서 관리 하는입니다. 가상 컴퓨터에 없으면 hello 문서에 설명 된 모든 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.
5. hello 자격 증명이 필요는 **사용자 계정이 속하는 toohello ' AAD DC Administrators' 그룹** tooadminister 그룹 정책 관리 되는 도메인에 대 한 디렉터리에 있습니다.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>작업 1-프로 비전 한 가상 컴퓨터를 도메인에 가입 된 tooremotely hello 관리 되는 도메인에 대 한 그룹 정책 관리
Azure AD 도메인 서비스 관리 되는 도메인 hello AD PowerShell 또는 관리 센터 ADAC (Active Directory)와 같은 친숙 한 Active Directory 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다. 마찬가지로, hello 관리 되는 도메인에 대 한 그룹 정책은 hello 그룹 정책 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다.

Azure AD 디렉터리의 관리자가 원격 데스크톱을 통해 관리 되는 도메인 hello에 권한이 tooconnect toodomain 컨트롤러를 갖지 않습니다. Hello ' AAD DC Administrators' 그룹의 멤버는 관리 되는 도메인에 대 한 원격으로 그룹 정책을 관리할 수 있습니다. Windows 서버/클라이언트 컴퓨터에 가입된 toohello 관리 되는 도메인에서 그룹 정책 도구를 사용할 수 있습니다. Hello Windows 서버 및 클라이언트 컴퓨터에 선택적 기능 그룹 정책 관리의 일부 toohello 관리 되는 도메인에 가입 그룹 정책 도구를 설치할 수 있습니다.

hello 첫 번째 작업은 관리 되는 도메인에 가입된 toohello 되는 Windows Server 가상 컴퓨터 tooprovision입니다. 자세한 내용은 toohello 문서를 참조 [Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>작업 2-hello 가상 컴퓨터에 설치 그룹 정책 도구
Hello 단계 tooinstall hello 그룹 정책 관리 도구 hello 도메인에 가입 된 가상 컴퓨터에서 다음을 수행 합니다.

1. 너무 이동**가상 컴퓨터** hello Azure 클래식 포털에서에서 노드. 작업 1에서 만든 hello 가상 컴퓨터를 선택 하 고 클릭 **연결** hello hello 창 맨 아래에 hello 명령 모음에서 합니다.

    ![TooWindows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. hello 클래식 포털 묻는 tooopen 또는 변수인 사용 되는 tooconnect toohello 가상 컴퓨터 '.rdp' 확장명을 가진 파일을 저장 합니다. 다운로드를 마쳤을 때 hello 파일을 클릭 합니다.
3. Hello 로그인 프롬프트 toohello ' AAD DC Administrators' 그룹에 속한 사용자의 hello 자격 증명을 사용 합니다. 사용 예를 들어 'bob@domainservicespreview.onmicrosoft.com' 여기서에서 합니다.
4. Hello 시작 화면에서 엽니다 **서버 관리자**합니다. 클릭 **역할 및 기능 추가** hello 중앙 창의 hello 서버 관리자 창에서.

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Hello에 **시작 하기 전에** hello 페이지 **추가 역할 및 기능 마법사**, 클릭 **다음**합니다.

    ![시작하기 전에 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Hello에 **설치 유형을** 페이지에서 hello **역할 기반 또는 기능 기반 설치** 옵션을 선택 하 고 클릭 **다음**합니다.

    ![설치 유형 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Hello에 **서버 선택** 페이지 hello 서버 풀의 hello 현재 가상 컴퓨터를 선택 하 고 클릭 **다음**합니다.

    ![서버 선택 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Hello에 **서버 역할** 페이지 **다음**합니다. 에서는 이후 hello 서버에 있는 모든 역할 설치 하지 않는 것이 페이지를 건너뜁니다.
9. Hello에 **기능** 페이지, 선택 hello **그룹 정책 관리** 기능입니다.

    ![기능 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. Hello에 **확인** 페이지 **설치** hello 가상 컴퓨터에 tooinstall hello 그룹 정책 관리 기능. 기능 설치가 완료 되 면 클릭 **닫기** tooexit hello **역할 및 기능 추가** 마법사.

    ![확인 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>작업 3-실행 hello 그룹 정책 관리 콘솔 tooadminister 그룹 정책
가상 컴퓨터를 도메인에 가입 된 tooadminister hello hello 관리 되는 도메인에서 그룹 정책에 hello 그룹 정책 관리 콘솔을 사용할 수 있습니다.

> [!NOTE]
> Toobe tooadminister hello 관리 되는 도메인의 그룹 정책은 hello AAD ' DC Administrators' 그룹의 멤버가 필요합니다.
>
>

1. Hello 시작 화면에서 클릭 **관리 도구**합니다. Hello 표시 되어야 **그룹 정책 관리** 콘솔 hello 가상 컴퓨터에 설치 합니다.

    ![그룹 정책 관리 시작](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. 클릭 **그룹 정책 관리** toolaunch hello 그룹 정책 관리 콘솔.

    ![그룹 정책 콘솔](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>작업 4 - 기본 제공 그룹 정책 개체 사용자 지정
두 개의 기본 제공 그룹 정책 개체 (Gpo)-관리 되는 도메인의 hello ' AADDC 컴퓨터 ' 및 ' AADDC Users' 컨테이너에 대해 각각 하나씩 있습니다. 이러한 Gpo tooconfigure 그룹 정책 hello 관리 되는 도메인을 사용자 지정할 수 있습니다.

1. Hello에 **그룹 정책 관리** 콘솔에서 tooexpand hello **포리스트: contoso100.com** 및 **도메인** 노드 toosee hello 그룹 정책 관리 되는 도메인에 대 한 합니다.

    ![기본 제공 GPO](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. 관리 되는 도메인에서 이러한 기본 제공의 Gpo tooconfigure 그룹 정책을 사용자 지정할 수 있습니다. Hello GPO를 마우스 오른쪽 단추로 클릭 하 고 클릭 **편집...**  toocustomize hello에 대 한 기본 제공 GPO 합니다. 그룹 정책 구성 편집기 도구 hello toocustomize hello GPO 수 있습니다.

    ![기본 제공 GPO 편집](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. 이제 hello를 사용할 수 있습니다 **그룹 정책 관리 편집기** tooedit hello에 대 한 기본 제공 GPO 콘솔. 예를 들어, 다음 스크린 샷 hello toocustomize 기본 제공 ' AADDC 컴퓨터 ' GPO hello 하는 방법을 보여 줍니다.

    ![GPO 사용자 지정](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>작업 5 - 사용자 지정 GPO(그룹 정책 개체) 만들기
사용자 지정 그룹 정책 개체를 만들거나 가져올 수 있습니다. 사용자 지정 Gpo tooa 사용자 지정을 연결할 수도 있습니다. 관리 되는 도메인 내에서 만든 OU입니다. 사용자 지정 조직 구성 단위를 만드는 방법에 대한 자세한 내용은 [관리되는 도메인에서 사용자 지정 OU 만들기](active-directory-ds-admin-guide-create-ou.md)를 참조하세요.

> [!NOTE]
> Toobe tooadminister hello 관리 되는 도메인의 그룹 정책은 hello AAD ' DC Administrators' 그룹의 멤버가 필요합니다.
>
>

1. Hello에 **그룹 정책 관리** 콘솔 tooselect 사용자 지정 조직 구성 단위 (OU)를 클릭 합니다. Hello OU를 마우스 오른쪽 단추로 클릭 하 고 클릭 **이 도메인에서 GPO를 만들고 여기에 연결...** .

    ![사용자 지정 GPO 만들기](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Hello 새 GPO의 이름을 지정 하 고 클릭 **확인**합니다.

    ![GPO의 이름 지정](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. 새 GPO 만들어져 tooyour 사용자 지정 연결 OU입니다. Hello GPO를 마우스 오른쪽 단추로 클릭 하 고 클릭 **편집...**  hello 메뉴에서 합니다.

    ![새로 만든 GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. Hello를 사용 하 여 hello 새로 만든 GPO를 사용자 지정할 수 있습니다 **그룹 정책 관리 편집기**합니다.

    ![새 GPO 사용자 지정](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


[그룹 정책 관리 콘솔](https://technet.microsoft.com/library/cc753298.aspx) 사용에 대한 자세한 내용은 Technet에서 확인할 수 있습니다.

## <a name="related-content"></a>관련 콘텐츠
* [Azure AD Domain Services - 시작 가이드](active-directory-ds-getting-started.md)
* [Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)
* [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
* [그룹 정책 관리 콘솔](https://technet.microsoft.com/library/cc753298.aspx)
