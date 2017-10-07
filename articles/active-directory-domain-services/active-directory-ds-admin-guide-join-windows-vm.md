---
title: "Azure Active Directory 도메인 서비스: Windows Server VM tooa 관리 되는 도메인에 가입 | Microsoft Docs"
description: "Windows Server 가상 컴퓨터를 가입 tooAzure AD 도메인 서비스"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Windows Server 가상 컴퓨터 tooa 관리 되는 도메인에 가입
> [!div class="op_single_selector"]
> * [Azure 클래식 포털 - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

이 문서는 가상 컴퓨터가 실행 중인 Windows Server 2012 R2 tooan Azure AD 도메인 서비스 toojoin hello Azure 클래식 포털을 사용 하 여 도메인을 관리 하는 방법을 보여 줍니다.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>1 단계: hello Windows Server 가상 컴퓨터 만들기
Hello에 설명 된 hello 지침에 따라 [hello Azure 클래식 포털에서에서 Windows를 실행 중인 가상 컴퓨터를 만드는](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 자습서입니다. 이 새로 만든된 가상 컴퓨터는 tooensure 가입 toohello 반드시 Azure AD 도메인 서비스를 사용할 수 있는 동일한 가상 네트워크입니다. 옵션 ' 빨리 만들기 ' hello toojoin hello 가상 컴퓨터 tooa 가상 네트워크를 사용 하지 않습니다. 따라서 toouse hello ' 갤러리에서 ' 옵션 toocreate hello 가상 컴퓨터.

수행 Windows 가상 컴퓨터에 가입된 toohello 가상 네트워크를 Azure AD 도메인 서비스를 활성화 한 다음 단계 toocreate hello 합니다.

1. Hello hello hello 창 맨 아래에 hello 명령 모음에서 Azure 클래식 포털에서에서 클릭 **새로**합니다.
2. **계산**에서 **가상 컴퓨터**를 클릭한 후 **갤러리에서**를 클릭합니다.
3. hello 첫 번째 화면을 사용 하면 **이미지 선택** 사용 가능한 이미지의 hello 목록에서 가상 컴퓨터에 대 한 합니다. Hello 적절 한 이미지를 선택 합니다.

    ![이미지 선택](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. 두 번째 화면 hello를 사용 하면 컴퓨터 이름, 크기 및 관리자 사용자 이름 및 암호를 선택할 수 있습니다. Hello 계층 및 필요한 크기 toorun 앱 또는 워크 로드를 사용 합니다. 여기에서 선택 하는 hello 사용자 이름은 hello 컴퓨터에서 로컬 관리자 사용자를입니다. 여기에 도메인 사용자 계정 자격 증명을 입력하지 마세요.

    ![가상 컴퓨터 구성](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. 세 번째 화면 hello 네트워킹, 저장소 및 가용성에 대 한 리소스를 구성할 수 있습니다. Hello에서 Azure AD 도메인 서비스를 사용할 수 있는 hello 가상 네트워크를 선택 **지역/선호도 그룹/가상 네트워크** 드롭다운입니다. 지정 된 **클라우드 서비스 DNS 이름** hello 가상 컴퓨터에 적합 합니다.

    ![가상 컴퓨터에 대한 가상 네트워크 선택](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > 가상 컴퓨터 toohello hello 참가 하는 확인 동일한 가상 네트워크를 Azure AD 도메인 서비스를 활성화 한 합니다. 결과적으로, hello 가상 컴퓨터 '' hello 도메인 보고 수 hello 도메인 가입 등의 작업을 수행 합니다. 다른 가상 네트워크에 toocreate hello 가상 컴퓨터를 선택 하면 Azure AD 도메인 서비스를 활성화 한 있는 해당 가상 네트워크 toohello 가상 네트워크를 연결 합니다.
   >
   >
6. hello 네 번째 화면을 사용 하면 hello VM 에이전트를 설치 하 고 구성 하는 hello 사용 가능한 확장의 일부를 수행할 수 있습니다.

    ![완료된](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. 클래식 포털 hello hello hello에서 새 가상 컴퓨터를 나열 hello 가상 컴퓨터를 만든 후 **가상 컴퓨터** 노드. Hello 가상 컴퓨터 및 클라우드 서비스를 모두 자동으로 시작 하 고 해당 상태로 나열 되어 **실행**합니다.

    ![가상 컴퓨터가 시작되어 실행 중](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>2 단계: hello 로컬 관리자 계정을 사용 하 여 toohello Windows Server 가상 컴퓨터에 연결
이제 toohello 새로 만든 Windows Server 가상 컴퓨터, toojoin 연결한 것 toohello 도메인입니다. Tooconnect tooit hello 가상 컴퓨터를 만들 때 지정한 hello 로컬 관리자 자격 증명을 사용 합니다.

Hello 단계 tooconnect toohello 가상 컴퓨터를 다음을 수행 합니다.

1. 너무 이동**가상 컴퓨터** hello 클래식 포털에서 노드. 1 단계에서에서 만든 hello 가상 컴퓨터를 선택 하 고 클릭 **연결** hello hello 창 맨 아래에 hello 명령 모음에서 합니다.

    ![TooWindows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. hello 클래식 포털 묻는 tooopen 또는 변수인 사용 되는 tooconnect toohello 가상 컴퓨터 '.rdp' 확장명을 가진 파일을 저장 합니다. 다운로드를 마쳤을 때 tooopen hello 파일을 클릭 합니다.
3. Hello 로그인 프롬프트에서 다음을 입력 하면 **로컬 관리자 자격 증명**, hello 가상 컴퓨터를 만드는 동안 지정 합니다. 예를 들어 이 예에서 'localhost\mahesh'를 사용했습니다.

이 시점에서 사용자로 로그인 toohello 새로 만든 로컬 관리자 자격 증명을 사용 하 여 Windows 가상 컴퓨터. 다음 단계 hello toojoin hello 가상 컴퓨터 toohello 도메인입니다.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>3 단계: hello Windows Server 가상 컴퓨터 toohello AAD DS 관리 되는 도메인에 가입
Hello 단계 toojoin hello Windows Server 가상 컴퓨터 toohello AAD DS 관리 되는 도메인에 다음을 수행 합니다.

1. 2 단계에서에서와 같이 toohello Windows Server를 연결 합니다. Hello 시작 화면에서 엽니다 **서버 관리자**합니다.
2. 클릭 **로컬 서버** hello 왼쪽된 창의 hello 서버 관리자 창에서.

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. 클릭 **작업 그룹** hello에서 **속성** 섹션. Hello에 **시스템 속성** 속성 페이지를 클릭 하 여 **변경** toojoin hello 도메인입니다.

    ![시스템 속성 페이지](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Hello에 Azure AD 도메인 서비스 관리 되는 도메인의 도메인 이름을 hello 지정 **도메인** 텍스트 상자를 클릭 하 고 **확인**합니다.

    ![Hello 도메인 toobe 조인 지정](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. 하면 자격 증명 toojoin hello 도메인 증명된 tooenter 됩니다. 확인을 **hello 사용자 속하는 toohello AAD DC 관리자 자격 증명을 지정** 그룹입니다. 이 그룹의 구성원만 권한을 toojoin 컴퓨터 toohello 관리 되는 도메인을 가집니다.

    ![도메인 가입에 자격 증명 지정](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Hello 같은 방법으로 다음 중 하나에 자격 증명을 지정할 수 있습니다.

   * UPN 형식: Azure AD에 구성 된 대로 hello 사용자 계정에 대 한 hello UPN 접미사를 지정 합니다. 이 예에서 'bob' hello 사용자의 hello UPN 접미사는 'bob@domainservicespreview.onmicrosoft.com'.
   * SAMAccountName 형식: hello SAMAccountName 형식에서 hello 계정 이름을 지정할 수 있습니다. 이 예제에서는 'bob' hello 사용자 tooenter 'CONTOSO100\bob' 해야 합니다.

     > [!NOTE]
     > **Hello UPN 형식 toospecify 자격 증명을 사용 하는 것이 좋습니다.** SAMAccountName hello 사용자의 UPN 접두사는 시간 (예: 'joereallylongnameuser')에 과도 하 게 하는 경우 자동으로 생성 될 수 있습니다. 여러 사용자가 Azure AD 테 넌 트의 SAMAccountName 형식 같은 UPN 접두사 (예를 들어 ' bob') 생성 될 수 있습니다 자동-hello 서비스는 hello 경우. 이러한 경우 hello UPN 형식을 사용할 수 안정적으로 toolog toohello 도메인에 있습니다.
     >
     >
7. 도메인 가입 되 면 hello toohello 도메인 환영 메시지의 뒤에 표시 됩니다. 도메인 가입 작업 toocomplete hello에 대 한 hello 가상 컴퓨터를 다시 시작 합니다.

    ![시작 toohello 도메인](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>도메인 가입 문제 해결
### <a name="connectivity-issues"></a>연결 문제
Hello 가상 컴퓨터가 없습니다 toofind hello 도메인 경우 toohello 문제 해결 단계를 참조 하십시오.

* 연결 된 toohello hello 가상 컴퓨터가 해당 확인 것과 동일한 가상 네트워크에 도메인 서비스를 활성화 한 합니다. 그렇지 않으면 hello 가상 컴퓨터가 없습니다 tooconnect toohello 도메인 이며 따라서 없습니다 toojoin hello 도메인.
* Hello 가상 컴퓨터가 가상 네트워크에 연결 된 tooanother 경우이 가상 네트워크는 도메인 서비스를 활성화 한 가상 네트워크를 연결 된 toohello 인지 확인 합니다.
* Hello 관리 되는 도메인 (예를 들어 ' ping contoso100.com')의 도메인 이름을 hello를 사용 하 여 tooping hello 도메인을 봅니다. 인 경우 toodo 수 없습니다 따라서 시도 hello 도메인 hello 페이지에 표시를 사용 하도록 설정한 Azure AD 도메인 서비스에 대 한 tooping hello IP 주소 (예를 들어 ' ping 10.0.0.4'). 사용자 수 tooping hello IP 주소가 있지만 hello 도메인이 아닌 경우 DNS 있습니다 수 잘못 구성 되었습니다. 사용자가 하지 구성한 hello 도메인의 hello IP 주소 hello 가상 네트워크에 대 한 DNS 서버와 합니다.
* Hello hello 가상 컴퓨터 ('ipconfig /flushdns')에서 DNS 확인 프로그램 캐시를 플러시 하십시오.

Toohello 묻는 대화 상자를 toojoin hello 도메인 자격 증명에 대 한 발생 하는 경우 연결 문제가 없는 합니다.

### <a name="credentials-related-issues"></a>자격 증명 관련 문제
Toohello 없습니다 toojoin hello 도메인을 자격 증명으로 문제가 있는 경우 다음 단계를 참조 하십시오.

* Hello UPN 형식 toospecify 자격 증명을 사용 하십시오. 사용자 계정에 대 한 hello SAMAccountName 생성 될 수 있습니다 자동-여러 사용자가 같은 UPN 테 넌 트의 접두사 또는 UPN 접두사는 과도 하 게 하는 경우 긴 hello로 합니다. 따라서 사용자 계정에 대 한 hello SAMAccountName 형식 기능 활성화 되거나 온-프레미스 도메인의 사용에서 다를 수 있습니다.
* Toouse hello toohello AAD ' DC Administrators' 그룹 toojoin 컴퓨터 toohello 관리 되는 도메인에 속해 있는 사용자 계정 자격 증명을 시도 합니다.
* 갖추어야 할 [암호 동기화를 사용 하도록 설정](active-directory-ds-getting-started-password-sync.md) hello 시작 가이드에 설명 된 hello 단계에 따라 합니다.
* Azure AD에 구성 된 대로 hello 사용자의 UPN hello를 사용 해야 합니다 (예를 들어 'bob@domainservicespreview.onmicrosoft.com')에서 toosign 합니다.
* 충분 한 시간 동안 암호 동기화 toocomplete hello 시작 가이드에 지정 된 대로 간격인 있는지 확인 합니다.

## <a name="related-content"></a>관련 콘텐츠
* [Azure AD Domain Services - 시작 가이드](active-directory-ds-getting-started.md)
* [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
