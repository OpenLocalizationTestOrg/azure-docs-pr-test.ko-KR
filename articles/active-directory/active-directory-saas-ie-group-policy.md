---
title: "ie GPO를 사용 하 여 Azure 액세스 패널 확장이 aaaDeploy | Microsoft Docs"
description: "어떻게 toouse 정책 toodeploy hello Internet Explorer 추가 기능 hello My Apps 포털에 대 한 그룹입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>그룹 정책을 사용 하 여 Internet Explorer에 대 한 tooDeploy 액세스 패널 확장이 hello 하는 방법
이 자습서에서는 어떻게 toouse 그룹 정책 tooremotely hello 액세스 패널에 확장을 설치 Internet Explorer에 대 한 사용자의 컴퓨터. 이 확장은 toosign를 사용 하 여 구성 된 앱에 필요한 Internet Explorer 사용자에 대 한 필요한 [암호 기반 single sign on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)합니다.

Admins이이 확장의 hello 배포를 자동화 하는 것이 좋습니다. 그렇지 않으면 사용자 toodownload가 확장 및 설치 hello 자체 발생 하기 쉬운 toouser 오류가 발생 하 고 관리자 권한이 필요 합니다. 이 자습서에서는 그룹 정책을 사용하여 소프트웨어 배포를 자동화하는 한 가지 방법을 설명합니다. [그룹 정책에 대해 알아봅니다.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

액세스 패널 확장 hello는 가능 [크롬](https://go.microsoft.com/fwLink/?LinkID=311859) 및 [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), 둘 중 필요한 관리자 권한을 tooinstall 합니다.

## <a name="prerequisites"></a>필수 조건
* 설정한 후 [Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), 사용자의 컴퓨터 tooyour 도메인에 가입한 하 고 있습니다.
* Hello "설정 편집" 권한이 tooedit hello 그룹 정책 개체 (GPO) 있어야 합니다. 기본적으로 hello 다음 보안 그룹의 멤버는이 권한이 있는: Domain Administrators, 엔터프라이즈 관리자 및 Group Policy Creator Owners 합니다. [자세한 정보](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>1 단계: hello 배포 지점 만들기
첫째, hello 설치 관리자 패키지 tooremotely 설치 hello 확장에 가져오려는 hello 컴퓨터에서 액세스할 수 있는 네트워크 위치에 배치 해야 합니다. toodo이를 다음이 단계를 수행 합니다.

1. 관리자 권한으로 toohello 서버에 로그온 합니다.
2. Hello에 **서버 관리자** 창 너무 이동**파일 및 저장소 서비스**합니다.
   
    ![파일 및 저장소 서비스 열기](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Toohello 이동 **공유** 탭 합니다. 그런 다음 **태스크** > **새 공유...**를 클릭합니다.
   
    ![파일 및 저장소 서비스 열기](./media/active-directory-saas-ie-group-policy/shares.png)
4. 전체 hello **새 공유 마법사** 및 설정 권한 tooensure 사용자의 컴퓨터에서 액세스할 수 있습니다. [공유에 대해 알아봅니다.](https://technet.microsoft.com/library/cc753175.aspx)
5. Microsoft Windows Installer 패키지 (.msi 파일)를 수행 하는 hello 다운로드: [액세스 패널 Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Hello hello 공유에서 설치 관리자 패키지 tooa 원하는 위치에 복사 합니다.
   
    ![Hello.msi 파일 toohello 공유에 복사 합니다.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. 클라이언트 컴퓨터 수 tooaccess hello 공유에서 설치 관리자 패키지를 hello 있는지 확인 합니다. 

## <a name="step-2-create-hello-group-policy-object"></a>2 단계: hello 그룹 정책 개체 만들기
1. Active Directory 도메인 서비스 (AD DS) 설치를 호스팅하는 toohello 서버에 로그온 합니다.
2. Hello 서버 관리자에서에서 이동 너무**도구** > **그룹 정책 관리**합니다.
   
    ![TooTools 이동 > 그룹 정책 관리](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. Hello hello의 왼쪽된 창에서 **그룹 정책 관리** 창 조직 구성 단위 (OU) 계층 구조를 확인 하 고는 범위에서 원하는 tooapply hello 그룹 정책을 확인 합니다. 예를 들어, 테스트를 위해 작은 OU toodeploy tooa toopick 몇몇 사용자가 결정할 수 있습니다 또는 최상위 OU toodeploy tooyour 전체 조직을 선택할 수 있습니다.
   
   > [!NOTE]
   > Toocreate 같은 조직 단위 (Ou)를 편집 하거나, 백 toohello 서버 관리자를 전환 하 고 이동 너무**도구** > **Active Directory 사용자 및 컴퓨터**합니다.
   > 
   > 
4. OU를 선택한 후에 마우스 오른쪽 단추로 클릭하고 **이 도메인에서 GPO를 만들고 여기에 연결...**을 선택합니다.
   
    ![새 GPO 만들기](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. Hello에 **새 GPO** , 프롬프트에 대 한 이름 입력 hello 새 그룹 정책 개체입니다.
   
    ![Hello 새 GPO 이름](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. 마우스 오른쪽 단추로 클릭 하 고 사용자가 만든 선택 그룹 정책 개체 hello **편집**합니다.
   
    ![Hello 새 GPO를 편집 합니다.](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>3 단계: 할당 hello 설치 패키지
1. 에 따라 toodeploy hello 확장 하는지 여부를 결정 **컴퓨터 구성** 또는 **사용자 구성**합니다. 사용 하는 경우 [컴퓨터 구성](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello 확장 프로그램에 관계 없이 사용자가 로그온 tooit hello 컴퓨터에 설치 합니다. 와 [사용자 구성](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), 사용자가 로그온 하는 컴퓨터에 관계 없이 설치 하는 hello 확장 합니다.
2. Hello hello의 왼쪽된 창에서 **그룹 정책 관리 편집기** hello 폴더 경로, 선택한 구성의 유형에 따라 다음의 이동 tooeither 창:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. **소프트웨어 설치**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기** > **패키지...**를 선택합니다.
   
    ![새 소프트웨어 설치 패키지 만들기](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Hello 설치 관리자 패키지를 포함 하는 공유 폴더를 이동 toohello [1 단계: hello 배포 지점 만들기](#step-1-create-the-distribution-point)hello.msi 파일을 선택 하 고 클릭 **열려**합니다.
   
   > [!IMPORTANT]
   > Hello 공유를 동일한 서버에 있는 경우 hello.msi를 액세스 하는 hello 로컬 파일 경로 대신 hello 네트워크 파일 경로 통해 있는지 확인 합니다.
   > 
   > 
   
    ![Hello 공유 폴더에서 hello 설치 패키지를 선택 합니다.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. Hello에 **소프트웨어 배포** 프롬프트를 선택 **Assigned** 배포 방법에 대 한 합니다. 그런 후 **OK**를 클릭합니다.
   
    ![할당됨을 선택하고 확인을 클릭합니다.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

배포 된 toohello 선택한 OU hello 확장이 되었습니다. [그룹 정책 소프트웨어 설치에 대해 알아봅니다.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>4 단계: 자동 사용 hello Internet Explorer에 대 한 확장
또한 Internet Explorer에 대 한 모든 확장 toorunning hello 설치 관리자 사용 하려면 먼저 명시적으로 활성화 되어야 합니다. Tooenable 아래 hello 단계 수행 hello 그룹 정책을 사용 하 여 액세스 패널 확장:

1. Hello에 **그룹 정책 관리 편집기** 창에서 선택한 구성의 유형에 따라 경로 따라 hello의 이동 tooeither [3 단계: 할당 hello 설치 패키지](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. **추가 기능 목록**을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.
    ![추가 기능 목록을 편집합니다.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. Hello에 **추가 기능 목록** 창에서 **Enabled**합니다. 그런 다음 hello **옵션** 섹션에서 클릭 **표시...** .
   
    ![사용을 클릭한 다음 표시...를 클릭합니다.](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. Hello에 **내용 표시** 창의 hello 다음 단계를 수행 합니다.
   
   1. Hello 첫 번째 열에 대 한 (hello **값 이름** 필드), 복사 및 붙여넣기 hello 다음 클래스 ID:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Hello 두 번째 열에 대 한 (hello **값** 필드), hello 다음 값 입력:`1`
   3. 클릭 **확인** tooclose hello **내용 표시** 창.
      
      ![Hello 값 위에 지정 된 대로 입력 합니다.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. 클릭 **확인** tooapply은 변경 내용 및 닫기 hello **추가 기능 목록** 창.

hello 확장 이제 설정할지 hello 컴퓨터 선택 hello에 대 한 OU입니다. [그룹 정책 tooenable 사용에 대 한 자세한 내용을 보거나 Internet Explorer 추가 기능을 사용 하지 않도록 설정 합니다.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>5단계(선택 사항): “암호 저장" 프롬프트 비활성화
사용자가 로그인 toowebsites hello 액세스 패널 확장을 사용 하 여, Internet Explorer 수 표시 hello 다음 묻는 "보 시겠습니까 toostore 암호?" 라는

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

사용자가이 프롬프트를 보지 못하도록 tooprevent을 원할 경우 이사 암호에서 자동 완성 tooprevent 아래 hello 단계를 수행:

1. Hello에 **그룹 정책 관리 편집기** 창, 이동 toohello 경로 아래에 나열 된 합니다. 이 구성 설정은 **사용자 구성**에서만 사용할 수 있습니다.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. 명명 된 hello 설정의 찾을 **hello forms에 사용자 이름 및 암호에 대 한 자동 완성 기능을 켤**합니다.
   
   > [!NOTE]
   > 이전 버전의 Active Directory hello 이름으로이 설정을 나열할 수 있습니다 **자동 완성 toosave 암호를 허용 하지 않는**합니다. 해당 설정에 대 한 hello 구성 hello 설정을이 자습서에서 다릅니다.
   > 
   > 
   
    ![사용자 설정에서이 대 한 toolook를 기억 합니다.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Hello 설정 위에 마우스 오른쪽 단추로 클릭 하 고 선택 **편집**합니다.
4. 이라는 hello 창에서 **hello forms에 사용자 이름 및 암호에 대 한 자동 완성 기능을 설정**선택, **비활성화 된**합니다.
   
    ![사용 안함 선택](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. 클릭 **확인** tooapply 이러한 변경 내용 및 닫기 hello 창.

사용자는 더 이상 수 toostore 자격 증명 수 또는 자동 완성 tooaccess 이전에 저장 된 자격 증명을 사용 합니다. 그러나이 정책에서 허용 사용자 toocontinue toouse 검색 필드 등의 양식 필드의 다른 형식에 대 한 자동 완성 합니다.

> [!WARNING]
> 이 정책은 하는 사용자가 선택한 toostore 일부 자격 증명 후이 정책을 사용 하는 경우 *하지* 이미 저장 되어 있는 hello 자격 증명의 선택을 취소 합니다.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>6 단계: 테스트 배포 문자열
Hello 확장 배포에 성공 하면 tooverify 아래 hello 단계를 수행 합니다.

1. 사용 하 여 배포한 경우 **컴퓨터 구성**, toohello에서 선택한 OU에 속하는 클라이언트 컴퓨터에 로그인 [2 단계: hello 그룹 정책 개체 만들기](#step-2-create-the-group-policy-object)합니다. 사용 하 여 배포한 경우 **사용자 구성**에 있는지 toosign toothat OU에 속한 사용자로 확인 합니다.
2. 몇 가지 기호 걸릴 수 있습니다이 컴퓨터 toofully 업데이트 hello 그룹 정책에 대 한 기능을 변경 합니다. 열기 tooforce hello 업데이트는 **명령 프롬프트** 창과 다음 명령이 실행된 hello:`gpupdate /force`
3. Hello 설치 tootake 위 hello 컴퓨터를 다시 시작 해야 합니다. 부팅 시 hello 확장 하는 동안 일반적인 설치 보다 훨씬 더 많은 시간이 걸릴 수 있습니다.
4. 다시 시작한 후 **Internet Explorer**를 엽니다. Hello hello 창의 오른쪽 위 모서리를 클릭 **도구** (hello 기어 아이콘)을 선택한 후 **추가 기능을 관리**합니다.
   
    ![TooTools 이동 > 추가 기능 관리](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. Hello에 **추가 기능 관리** 창 해당 hello 확인 **액세스 패널 확장** 가 설치 되어 있는지 해당 **상태** 너무 설정 된**사용**.
   
    ![액세스 패널 확장이 설치 및 활성화 되어 해당 hello를 확인 합니다.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)
* [Internet Explorer에 대 한 hello 액세스 패널 확장 문제 해결](active-directory-saas-ie-troubleshooting.md)

