---
title: "Azure Active Directory Domain Services: 관리되는 도메인에서 DNS 관리 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 DNS 관리"
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
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Azure AD 도메인 서비스 관리되는 도메인에서 DNS 관리
Azure Active Directory 도메인 서비스는 hello 관리 되는 도메인에 대 한 DNS 확인을 제공 하는 DNS (도메인 이름 확인) 서버를 포함 합니다. 경우에 따라서는 tooconfigure hello 관리 되는 도메인에 DNS를 할 수 있습니다. 조인 된 toohello 도메인에 있지 않은 컴퓨터를 부하 분산 장치에 대 한 가상 IP 주소 구성 또는 외부 DNS 전달자를 설치에 대 한 toocreate DNS 레코드를 할 수 있습니다. 이러한 이유로 toohello ' AAD DC Administrators' 그룹에 속한 사용자는 hello 관리 되는 도메인에 대 한 DNS 관리 권한은 부여 됩니다.

## <a name="before-you-begin"></a>시작하기 전에
이 문서에 나열 된 tooperform hello 작업 해야 합니다.

1. 유효한 **Azure 구독**.
2. **Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.
3. **Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다. 그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.
4. A **가상 컴퓨터를 도메인에 가입 된** hello Azure AD 도메인 서비스 관리 되는 도메인에서 관리 하는입니다. 가상 컴퓨터에 없으면 hello 문서에 설명 된 모든 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.
5. hello 자격 증명이 필요는 **사용자 계정이 속하는 toohello ' AAD DC Administrators' 그룹** tooadminister DNS 관리 되는 도메인에 대 한 디렉터리에 있습니다.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>작업 1-프로 비전 한 가상 컴퓨터를 도메인에 가입 된 tooremotely hello 관리 되는 도메인의 DNS 관리
Azure AD 도메인 서비스 관리 되는 도메인 hello AD PowerShell 또는 관리 센터 ADAC (Active Directory)와 같은 친숙 한 Active Directory 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다. 마찬가지로, hello 관리 되는 도메인에 대 한 DNS hello DNS 서버 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다.

Azure AD 디렉터리의 관리자가 원격 데스크톱을 통해 관리 되는 도메인 hello에 권한이 tooconnect toodomain 컨트롤러를 갖지 않습니다. Hello ' AAD DC Administrators' 그룹의 구성원은 관리 되는 도메인에 가입된 toohello 하는 Windows 서버/클라이언트 컴퓨터에서 DNS 서버 도구를 사용 하 여 원격으로 관리 되는 도메인에 대 한 DNS를 관리할 수 있습니다. Windows 서버에서 원격 서버 관리 도구 (RSAT) 선택적 기능 hello의 일부로 DNS 서버 도구를 설치할 수 있습니다 및 클라이언트 컴퓨터에 관리 되는 toohello 도메인에 가입 합니다.

hello 첫 번째 작업은 관리 되는 도메인에 가입된 toohello 되는 Windows Server 가상 컴퓨터 tooprovision입니다. 자세한 내용은 toohello 문서를 참조 [Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>작업 2-hello 가상 컴퓨터에서 DNS 서버 설치 도구
Hello 단계 tooinstall hello DNS 관리 도구 hello 도메인에 가입 된 가상 컴퓨터에서 다음을 수행 합니다. [원격 서버 관리 도구 설치 및 사용](https://technet.microsoft.com/library/hh831501.aspx)에 대한 자세한 내용은 TechNet을 참조하세요.

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
9. Hello에 **기능** 페이지에서 tooexpand hello **원격 서버 관리 도구** 노드 tooexpand hello를 클릭 한 다음 **역할 관리 도구** 노드. 선택 **DNS 서버 도구** hello 역할 관리 도구 목록에서 기능입니다.

    ![기능 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. Hello에 **확인** 페이지 **설치** tooinstall hello DNS 서버 도구 hello 가상 컴퓨터 기능입니다. 기능 설치가 완료 되 면 클릭 **닫기** tooexit hello **역할 및 기능 추가** 마법사.

    ![확인 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>작업 3-실행 hello DNS 관리 콘솔 tooadminister DNS
Hello DNS 서버 도구에 기능이 설치 되어 가상 컴퓨터를 도메인에 가입 된 hello, 했으므로 hello 관리 되는 도메인에 hello DNS 도구 tooadminister DNS를 사용할 수 있습니다.

> [!NOTE]
> Toobe tooadminister hello 관리 되는 도메인에 있는 DNS hello AAD ' DC Administrators' 그룹의 구성원을 해야합니다.
>
>

1. Hello 시작 화면에서 클릭 **관리 도구**합니다. Hello 표시 되어야 **DNS** 콘솔 hello 가상 컴퓨터에 설치 합니다.

    ![관리 도구 - DNS 콘솔](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. 클릭 **DNS** toolaunch hello DNS 관리 콘솔.
3. Hello에 **tooDNS 서버 연결** 대화 상자에서 이라는 hello 옵션을 클릭 **컴퓨터 다음 hello**, hello 관리 되는 도메인 (예를 들어 ' contoso100.com')의 hello DNS 도메인 이름을 입력 합니다.

    ![DNS 콘솔-toodomain 연결](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. DNS 콘솔 hello toohello 관리 되는 도메인을 연결합니다.

    ![DNS 콘솔 - 도메인 관리](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. 이제는 AAD 도메인 서비스를 활성화 한 hello 가상 네트워크 내의 컴퓨터에 대 한 hello DNS 콘솔 tooadd DNS 항목을 사용할 수 있습니다.

> [!WARNING]
> DNS 관리 도구를 사용 하 여 도메인 관리 되는 hello에 대 한 DNS를 관리 하는 경우 주의 해야 합니다. 확인을 **hello 도메인에 도메인 서비스에서 사용 되는 hello 기본 제공 하는 DNS 레코드를 수정 하거나 삭제 하지 마십시오**합니다. 기본 제공 DNS 레코드는 도메인 DNS 레코드, 이름 서버 레코드 및 DC 위치에 사용되는 기타 레코드를 포함합니다. 이러한 레코드를 수정 하는 경우 도메인 서비스는 hello 가상 네트워크에서 트랜잭션이 중단 됩니다.
>
>

Hello 참조 [DNS 도구 Technet에서 문서](https://technet.microsoft.com/library/cc753579.aspx) DNS 관리 하는 방법에 대 한 자세한 내용은 합니다.

## <a name="related-content"></a>관련 콘텐츠
* [Azure AD Domain Services - 시작 가이드](active-directory-ds-getting-started.md)
* [Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)
* [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
* [DNS 관리 도구](https://technet.microsoft.com/library/cc753579.aspx)
