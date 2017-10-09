---
title: "CLI hello에서 tooAzure에 aaaLog | Microsoft Docs"
description: "Mac, Linux 및 Windows 용 Azure 명령줄 인터페이스 (Azure CLI) hello에서 tooyour Azure 구독 연결"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>TooAzure hello Azure CLI에서 로그인
hello Azure CLI는 Azure 리소스 작업에 대 한 오픈 소스, 크로스 플랫폼 명령 집합. 이 문서에서는 다양 한 방법 tooprovide hello Azure 계정 자격 증명 tooconnect hello Azure CLI tooyour를 Azure 구독을 설명합니다.

* Hello 실행 `azure login` Azure Active Directory를 통해 CLI 명령 tooauthenticate 합니다. 이 메서드에 액세스할 수 있도록 모두 tooCLI 명령을 [모드 명령](#cli-command-modes)합니다. 추가 옵션 없이 hello 명령을 실행할 때 `azure login` 묻는 toocontinue 웹 포털을 통해 대화형으로 로그인 합니다. 에 대 한 추가 `azure login` 명령 옵션,이 문서에서는 또는 입력 hello 시나리오 참조 `azure login --help`합니다.
* 하기만 toouse Azure 서비스 관리 모드 CLI 명령 (대부분의 새로운 배포에 대 한 권장 하지 않음) 하는 경우 다운로드 하 고 게시 설정 파일을 컴퓨터에를 설치할 수 있습니다.

Hello CLI를 아직 설치 하지 않은 경우 참조 [설치 hello Azure CLI](cli-install-nodejs.md)합니다. Azure 구독이 없는 경우 몇 분 만에 [무료 계정](http://azure.microsoft.com/free/) 을 만들 수 있습니다.

다른 계정 ID 및 Azure 구독에 대한 배경 정보는 [Azure 구독과 Azure Active Directory의 연관 관계](active-directory/active-directory-how-subscriptions-associated-directory.md)를 참조하세요.

## <a name="scenario-1-azure-login-with-interactive-login"></a>시나리오 1: 대화형 로그인을 사용한 Azure 로그인
특정 계정으로 hello CLI 해야 toorun `azure login` 후 웹 포털 이라는 프로세스를 통해 웹 브라우저를 사용 하 여 hello 로그인 프로세스를 계속 *대화형 로그인*합니다. 일반적인 이유는 회사 또는 학교 계정이 있는 경우 (라고도 *조직 계정*) toorequire 다단계 인증 설정 된 합니다. 또한 toouse 리소스 관리자 모드 명령 하려는 경우 य ा Microsoft ख 대화형 로그인을 사용 합니다.

대화형 로그인 쉽습니다: 형식 `azure login` -옵션-없이 hello 다음 예제와 같이:

```
azure login
```                                                                                             

hello 출력 hello 다음과 같은 내용이 나타납니다.

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Tooyou hello 명령 출력에 제공 하는 hello 코드를 복사 하 고 지정 된 경우 브라우저 toohttp://aka.ms/devicelogin 또는 다른 페이지를 엽니다. (Hello에서 브라우저를 열 수 동일한 컴퓨터 또는 다른 컴퓨터 또는 장치입니다.) Hello 코드를 입력 및 입력 정보 요청된 tooenter hello 사용자 이름 및 암호는 다음 원하는 toouse hello id에 대 한 합니다. 해당 프로세스가 완료 되 면 hello 명령 셸 hello 로그인을 완료 합니다. 다음과 같이 표시될 수 있습니다.

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> 대화형 로그인을 사용할 경우 인증 및 권한 부여는 Azure Active Directory를 사용하여 수행합니다. Microsoft 계정 id를 사용 하는 경우 Azure Active Directory 기본 도메인 hello 로그인 프로세스에 액세스 합니다. 무료 Azure 계정에 등록한 경우 Azure Active Directory에서 계정에 대한 기본 도메인이 자동으로 생성됩니다.
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>시나리오 2: 사용자 이름 및 암호를 사용한 Azure 로그인
사용 하 여 hello `azure login` hello 사용자 이름을 가진 명령 (`-u`) 매개 변수 tooauthenticate toouse 회사 또는 학교 계정을 하는 경우 다단계 인증에 필요 하지 않습니다. Hello 암호에 대 한 hello 명령줄에서 메시지가 표시 됩니다 (hello의 추가 매개 변수로 hello 암호를 선택적으로 전달할 수 또는 `azure login` 명령). hello 다음 예제에서는 전달 조직 계정의 hello 사용자 이름:

    azure login -u myUserName@contoso.onmicrosoft.com

다음은 메시지가 tooenter 암호:

    info:    Executing command login
    Password: *********

hello 로그인 프로세스 다음 완료 됩니다.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

이러한 자격 증명을 사용 하 여 프로그램 처음 로그온 이면 tooverify 묻는 한다고 toocache 인증 토큰입니다. Hello 이전에 사용한 경우에이 메시지가 발생 `azure logout` 명령 (hello 문서의 뒷부분에 나오는 설명 참조). toobypass 자동화 시나리오에 대 한이 프롬프트 실행 `azure login` hello로 `-q` 매개 변수입니다.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>시나리오 3: 서비스 사용자와 함께 Azure 로그인 사용
Active Directory 응용 프로그램에 대 한 서비스 사용자를 만들고 hello 서비스 사용자에 대 한 권한이 구독을 하는 경우에 hello을 사용할 수 있습니다 `azure login` 명령 tooauthenticate hello 서비스 사용자입니다. 시나리오에 따라 hello의 명시적 매개 변수로 hello 서비스 사용자의 hello 자격 증명을 제공할 수 있습니다 `azure login` 명령입니다. 예를 들어 hello 다음 명령을 전달 hello 서비스 사용자 이름 및 Active Directory 테 넌 트 ID:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

입력 정보 요청된 tooprovide hello 암호 않은 합니다. CLI 스크립트 또는 응용 프로그램 코드를 통해 hello 자격 증명을 제공 하거나 자동화 시나리오에 대 한 비 대화형 인증서 tooauthenticate hello 서비스 사용자를 사용할 수 있습니다. 자세한 내용 및 예제는 [Azure Resource Manager를 사용하여 서비스 사용자 인증](resource-group-authenticate-service-principal-cli.md)을 참조하세요.

## <a name="scenario-4-use-a-publish-settings-file"></a>시나리오 4: 게시 설정 파일 사용
Toouse hello Azure 서비스 관리 모드 CLI 명령 자체입니다 (예: hello 클래식 배포 모델에서 Azure Vm toodeploy) 하기만 하는 경우 게시 설정 파일을 사용 하 여 연결할 수 있습니다. 이 메서드는 hello 구독 및 hello 인증서는 유효한 상태로 tooperform 관리 작업에 대 한 수 있는 로컬 컴퓨터에 인증서를 설치 합니다.

* **게시 설정 파일을 toodownload hello** 회원님의 계정에 대 한 확인 CLI를 입력 하 여 서비스 관리 모드에는 해당 hello `azure config mode asm`합니다. Hello 다음 명령을 실행 합니다.

        azure account download

기본 브라우저가 열리고 toohello에 toosign 묻는 [Azure 클래식 포털](https://manage.windowsazure.com)합니다. 로그인하면 `.publishsettings` 파일이 다운로드됩니다. 이 파일이 저장된 위치를 기록해 둡니다.

> [!NOTE]
> 계정이 여러 Azure Active Directory 테 넌 트와 연결 된 경우에 Active Directory 게시 설정을 toodownload을 원하는 파일에 대 한 증명된 tooselect 수도 있습니다.
>
>

Hello Azure 클래식 포털을 방문 하 여 또는 hello 다운로드 페이지를 사용 하 여 선택 하 고 나면 hello 선택한 Active Directory은 hello 기본 hello 클래식 포털 및 다운로드 페이지에서 사용 됩니다. Hello 텍스트를 참조 하는 기본 설정 된 후 '**여기 tooreturn toohello 선택 페이지를 클릭**' hello hello 다운로드 페이지 위쪽에 있습니다. 링크 tooreturn toohello 선택 페이지를 제공 하는 hello를 사용 합니다.

* **게시 설정 파일을 tooimport hello**실행 hello 다음 명령을:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> 가져온 후에 게시 설정, hello를 삭제 해야 `.publishsettings` 파일입니다. Hello Azure CLI에 더 이상 필요한 하 고 사용된 toogain 액세스 tooyour 구독 지 보안 위험이 없습니다.
>
>

## <a name="cli-command-modes"></a>CLI 명령 모드
hello Azure CLI 다른 명령 집합을 사용 하 여 Azure 리소스를 사용 하기 위한 두 가지 명령 모드를 제공 합니다.

* **리소스 관리자 모드** -hello 리소스 관리자 배포 모델에서 Azure 리소스를 사용 합니다. tooset 실행이 모드에서는 `azure config mode arm`합니다.
* **서비스 관리 모드** -hello 클래식 배포 모델에서 Azure 리소스를 사용 합니다. tooset 실행이 모드에서는 `azure config mode asm`합니다.

를 처음 설치할 때 현재 릴리스의 리소스 관리자 모드에서 CLI는 hello hello 합니다.

> [!NOTE]
> hello Resource Manager 모드와 서비스 관리 모드는 함께 사용할 수 없습니다. Hello에서 하나의 모드로 생성 된 리소스를 관리할 수 없습니다, 즉 다른 모드입니다.
>
>

## <a name="multiple-subscriptions"></a>여러 구독
여러 Azure 구독이 있는 경우 액세스 tooall 구독에 연결 된 자격 증명 부여 tooAzure 연결 합니다. 구독을 하나 hello 기본적으로 선택 된 이며 hello Azure CLI 작업을 수행할 때 사용 됩니다. 현재 기본 구독 hello를 포함 하 여, hello를 사용 하 여 hello 구독을 볼 수 있습니다 `azure account list` 명령입니다. 이 명령은 비슷한 toohello 다음을 정보를 반환합니다.

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

Hello 목록 앞에에서 hello **현재** 열을 Azure 하위 1 hello 현재 기본 구독을 나타냅니다. toochange hello 기본 구독을 사용 하 여 hello `azure account set` 명령을 실행 하 고 원하는 toobe hello 기본 hello 구독을 지정 합니다. 예:

    azure account set Azure-sub-2

이렇게 하면 hello 기본 구독 tooAzure-하위-2를 변경 합니다.

> [!NOTE]
> Hello 기본 구독 변경 즉시 적용 되며 전역 변경; 새 Azure CLI 명령에서 실행 하는지 여부 hello 동일한 명령줄 인스턴스 또는 다른 인스턴스나 hello 새 기본 구독을 사용 합니다.
>
>

Hello toouse hello Azure CLI로 기본이 아닌 구독을 선택 해도 toochange hello에 대 한 현재 기본 하지 않을 경우 사용할 수 있습니다 `--subscription` hello 명령에 대 한 옵션 및 hello 이름을 제공 원하는 toouse hello 작업에 대 한 hello 구독 합니다.

연결 된 Azure 구독 tooyour 했으면 Azure CLI 명령을 toowork hello를 사용 하 여 Azure 리소스에 시작할 수 있습니다.

## <a name="storage-of-cli-settings"></a>CLI 설정 저장소
Hello를 사용 하 여 기록할 것인지 여부를 `azure login` 명령 또는 가져오기에 대 한 게시 설정, CLI 프로필 및 로그에 저장 됩니다는 `.azure` 디렉터리에 있는 프로그램 `user` 디렉터리입니다. `user` 디렉터리는 운영 체제에 의해 보호됩니다. 그러나 좋습니다 tooencrypt 추가 단계를 수행 하는 프로그램 `user` 디렉터리입니다. 다음 방법으로 hello에 그렇게 할 수 있습니다.

* Windows에서는 hello 디렉터리 속성을 수정 하거나 BitLocker를 사용 합니다.
* Mac을 설정 FileVault hello 디렉터리에 대 한 합니다.
* Ubuntu, hello 암호화 홈 디렉터리 기능을 사용 합니다. 기타 Linux 배포에서도 유사한 기능을 제공합니다.

## <a name="logging-out"></a>로그아웃
다음 명령을 사용 하 여 hello 아웃 toolog:

    azure logout -u <username>

와 연결 된 hello 구독 hello 계정 로그 아웃 hello 로컬 프로필의 삭제 hello 구독 정보를 Active Directory와만 인증 됩니다. 그러나 또한 hello 구독에 대 한 게시 설정 파일을 가져온 경우, 로그 아웃 삭제 Active Directory에서에서 관련 정보 hello 로컬 프로필에만 합니다.

## <a name="next-steps"></a>다음 단계
* toouse Azure CLI 명령을 참조 [리소스 관리자 모드에서 Azure CLI 명령을](virtual-machines/azure-cli-arm-commands.md) 및 [서비스 관리 모드에서 Azure CLI 명령을](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.
* hello Azure CLI에 대해 자세히 toolearn 소스 코드를 다운로드, 문제를 보고 또는 toohello 프로젝트 참가, hello 방문 [Azure CLI hello에 대 한 GitHub 리포지토리](https://github.com/azure/azure-xplat-cli)합니다.
* Hello Azure CLI 또는 Azure를 사용 하 여 문제를 발생 하는 경우 방문 hello [의 Azure 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)합니다.
