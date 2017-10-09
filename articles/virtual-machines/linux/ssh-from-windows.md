---
title: "Linux vm의 Windows를 통해 키로 SSH aaaUse | Microsoft Docs"
description: "Toogenerate와 SSH 사용 하 여 Azure에서 Windows 컴퓨터 tooconnect tooa Linux 가상 컴퓨터에 키 하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Azure에서 Windows를 통해 tooUse SSH 키 하는 방법
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

TooLinux Azure의 가상 컴퓨터 (Vm)에 연결할 때 사용 해야 [공개 키 암호화](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide tooyour Linux VM의에서 보다 안전한 방식으로 toolog 합니다. 이 프로세스를 사용 하 여 hello 보안 셸 (SSH) 명령 tooauthenticate 직접 사용자 이름 및 암호 대신 공용 및 개인 키 교환 포함 됩니다. 암호는 웹 서버 등과 같이 인터넷 연결 Vm에서 특히 취약 toobrute 대입 공격입니다. 이 문서에서는 SSH 키 및 toogenerate Windows 컴퓨터에 적절 한 키를 hello 하는 방법에 대 한 개요를 제공 합니다.

## <a name="overview-of-ssh-and-keys"></a>SSH 및 키에 대한 개요
공개 및 개인 키를 사용 하 여 tooyour Linux VM을 안전 하 게 로그인 할 수 있습니다.

* hello **공개 키** Linux VM을 또는 원하는 toouse 공개 키 암호화와 기타 서비스에 배치 됩니다.
* hello **개인 키** tooverify에 로그인 할 때가 있는 tooyour Linux VM 하는 사용자의 id입니다. 이 개인 키는 보호해야 하는 한편, 공유하면 안됩니다.

이러한 공용 및 개인 키는 여러 VM 및 서비스에서 사용할 수 있습니다. 각 VM 또는 tooaccess 서비스에 대 한 키 쌍이 필요가 없습니다. 자세한 개요에 대해서는 [public-key 암호화](https://wikipedia.org/wiki/Public-key_cryptography)를 참조하세요.

SSH는 안전하지 않은 연결에서 안전하게 로그인할 수 있도록 하는 암호화된 연결 프로토콜입니다. Azure에서 호스팅되는 Linux Vm에 대 한 hello 기본 연결 프로토콜입니다. SSH 자체 암호화 된 연결을 제공 하지만 암호를 사용 하 여 SSH 연결을 사용 하더라도 hello VM 취약 toobrute 대입 공격 및 암호 추측. 연결 tooa는 더 안전 하 고 기본 방법은 이러한 공용 및 개인 키, 라고도 SSH 키를 사용 하 여 SSH를 사용 하 여 VM입니다.

SSH 키 toouse 지 tooyour 암호를 사용 하 여 Linux Vm에에서 로깅할 수 있습니다. VM 인터넷 노출된 toohello 없는 경우에 암호를 사용 하 여 충분 한 수 있습니다. 그러나 여전히 toomanage 암호 각 Linux VM에 대 한 및 해야 정상 암호 정책 및 사례를 정기적으로 업데이트 하 고 최소 암호 길이 유지 관리 합니다. SSH 키의 hello 사용 여러 Vm 간에 개별 자격 증명 관리 hello 복잡성을 줄입니다.

## <a name="windows-packages-and-ssh-clients"></a>Windows 패키지 및 SSH 클라이언트
Tooand 연결에서 사용 하 여 Azure Linux Vm을 관리 한 **SSH 클라이언트**합니다. 일반적으로 Windows 컴퓨터에는 SSH 클라이언트를 설치하지 않습니다. Windows 10 Anniversary 업데이트 hello를 이용한 적 for Windows를 추가 하 고 hello 최신 Windows 10 작성자 업데이트는 제공 추가 업데이트. Linux에 대 한이 Windows 하위 Bash 셸의 내에서 고유 하 게 SSH 클라이언트 등의 toorun 및 액세스 유틸리티도가 있습니다. 그런 다음 하나를 수행 hello Linux 문서와 같은 [Linux 용 toogenerate SSH 키 쌍은 어떻게](mac-create-ssh-keys.md)합니다. Windows용 Bash는 아직 개발 중이며 베타 릴리스 버전으로 간주됩니다. Windows용 Bash에 대한 자세한 내용은 [Ubuntu on Windows의 Bash](https://msdn.microsoft.com/commandline/wsl/about)를 참조하세요.

원할 경우 toouse 무언가 이용한 적에 대 한 Windows 이외의 일반적인 Windows SSH 클라이언트를 설치할 수 있습니다는 hello 다음 패키지에에서 포함 됩니다.

* [Windows 용 Git](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>키 파일 toocreate 필요 한가요?
Azure는 최소한 2048비트, **ssh-rsa** 형식 공개 및 개인 키 서식이 필요합니다. Hello 클래식 배포 모델을 사용 하 여 Azure 리소스를 관리 하는 경우 또한 해야 toogenerate PEM (`.pem` 파일).

다음은 hello 배포 시나리오와 각 사용 파일 hello 형식입니다.

1. **ssh rsa** hello를 사용 하 여 모든 배포에 키가 필요 [Azure 포털](https://portal.azure.com), 및 hello를 사용 하 여 리소스 관리자 배포 [Azure CLI](../../cli-install-nodejs.md)합니다.
   * 대개 이러한 키는 대부분의 모든 사용자에게 필요한 것입니다.
2. A `.pem` 파일은 hello 클래식 배포를 사용 하 여 필요한 toocreate Vm입니다. Hello를 사용 하는 경우 클래식 배포에서는 이러한 키가 지원 [Azure 포털](https://portal.azure.com) 또는 [Azure CLI](../../cli-install-nodejs.md)합니다.
   * 필요할 때만 toocreate 이러한 추가 키와 인증서 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 관리 하는 경우.

## <a name="install-git-for-windows"></a>Windows용 Git 설치
hello 이전 섹션에 나열 hello를 포함 하는 여러 패키지 `openssl` Windows 용 도구입니다. 이 도구는 필요한 toocreate 공개 및 개인 키입니다. 예제 세부 정보를 어떻게 다음 hello tooinstall 사용 하 여 **Windows 용 Git**경우에 원하는 어떤 패키지를 선택할 수 있습니다. **Windows 용 Git** toosome 추가 하는 오픈 소스 소프트웨어를 액세스할 수 있습니다 ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) 도구 및 유틸리티를 사용할 때는 Linux Vm의 경우에 유용할 수 있습니다.

1. 다운로드 및 설치 **Windows 용 Git** hello 수정할 수 있는 위치에서에서: [https://git-for-windows.github.io/](https://git-for-windows.github.io/)합니다.
2. Toochange 특별히 필요한 경우가 아니면 hello 시 hello 기본 옵션 설치 프로세스에 동의 하 합니다.
3. 실행 **Git Bash** hello에서 **시작 메뉴** > **Git** > **Git Bash**합니다. hello 콘솔에는 다음 예제와 비슷한 toohello 표시 됩니다.

    ![Windows용 Git의 Bash 셸](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>개인 키 만들기
1. 사용자 **Git Bash** 창을 사용 하 여 `openssl.exe` toocreate 개인 키입니다. hello 다음 예제에서는 라는 키 `myPrivateKey` 및 명명 된 인증서 `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    hello 출력은 다음 예제와 비슷한 toohello 합니다.

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Bash가 오류를 보고하는 경우 상승된 권한으로 새 **Git Bash** 창을 엽니다. 그런 다음 hello를 다시 실행 `openssl` 명령입니다.

2. 국가 이름, 위치, 조직 이름 등에 대 한 응답 hello 메시지 표시합니다.
3. 새 개인 키와 인증서가 현재 작업 중인 디렉터리에 만들어집니다. 보안 조치로,만 액세스할 수 있도록 사용자의 개인 키 hello 사용 권한을 설정 해야 합니다.

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. hello [절로](#create-a-private-key-for-putty) PuTTYgen tooboth를 사용 하 여 세부 정보 보기 및 hello 공개 키를 사용 하 여 PuTTY tooSSH tooLinux Vm을 사용 하 여에 대 한 특정 개인 키를 만듭니다. hello 다음 명령은 생성 라는 공개 키 파일 `myPublicKey.key` 바로 사용할 수 있는:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Toomanage 클래식 리소스를 필요할 경우 변환 hello `myCert.pem` 너무`myCert.cer` (DER로 인코딩된 X509 인증서). Toospecifically 해야 하는 경우에이 선택적 단계를 수행 합니다. 이전 클래식 리소스를 관리 합니다.

    다음 명령을 hello를 사용 하 여 hello 인증서를 변환 합니다.

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>PuTTY용 개인 키 만들기
PuTTY는 Windows용 공용 SSH 클라이언트입니다. 사용자는 무료 toouse SSH 클라이언트를 합니다. PuTTY toouse toocreate 특별 한 종류의 키-는 PuTTY 개인 키 (PPK) 필요합니다. Toouse PuTTY를 원하지 않는 경우이 섹션을 건너뛰십시오.

hello 다음 예제에서는이 키를 만들며 추가 개인 PuTTY toouse 용으로 특별히:

1. 사용 하 여 **Git Bash** tooconvert PuTTYgen 이해할 수 RSA 개인 키로 개인 키입니다. hello 다음 예제에서는 라는 키 `myPrivateKey_rsa` 라는 hello 기존 키에서 `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    보안 조치로,만 액세스할 수 있도록 사용자의 개인 키 hello 사용 권한을 설정 해야 합니다.

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. 에서 다운로드 및 실행 PuTTYgen hello 수정할 수 있는 위치: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Hello 메뉴: **파일** > **부하 개인 키**
4. 사용자의 개인 키를 찾습니다 (`myPrivateKey_rsa` hello 이전 예제에서). 시작할 때 hello 기본 디렉터리 **Git Bash** 은 `C:\Users\%username%`합니다. Hello 파일 필터 tooshow 변경 **모든 파일 (\*.\*)** :

    ![PuTTYgen hello 기존 개인 키 로드](./media/ssh-from-windows/load-private-key.png)
5. **열기**를 클릭합니다. 메시지가 해당 hello 키가 성공적으로 가져왔습니다 나타냅니다.

    ![성공적으로 가져온된 키 tooPuTTYgen](./media/ssh-from-windows/successfully-imported-key.png)
6. 클릭 **확인** tooclose hello 프롬프트입니다.
7. hello 공개 키가 hello hello 위쪽에 표시 됩니다. **PuTTYgen** 창. 복사한 Linux VM을 만들 때 hello Azure 포털 또는 Azure 리소스 관리자 템플릿에이 공개 키를 붙여 넣습니다. 클릭할 수도 있습니다 **저장 공개 키** toosave 복사본 tooyour 컴퓨터:

    ![PuTTY 공개 키 파일 저장](./media/ssh-from-windows/save-public-key.png)

    hello 다음 예제를 복사 하는 방법을 Linux VM을 만들 때 hello Azure 포털에이 공개 키를 붙여 넣습니다. hello 공개 키는 일반적으로에 저장 한 다음 `~/.ssh/authorized_keys` 새 VM에 있습니다.

    ![Hello Azure 포털에서에서 VM을 만들 때 공개 키를 사용 하 여](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. 다음과 같이 다시 **PuTTYgen**에서 **개인 키 저장**을 클릭합니다.

    ![PuTTY 개인 키 파일 저장](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > 메시지가 트 키에 대 한 암호를 입력 하지 않고 toocontinue 원하는 나타납니다. 암호는 암호 tooyour 연결 된 개인 키와 비슷합니다. Tooobtain 사용자 인 경우에 사용자의 개인 키를 여전히 됩니다 수 tooauthenticate hello 키만 사용 합니다. Hello 암호를 해야 합니다. 암호 없이 사용자의 개인 키를 가져오면 누군가가 tooany VM에에서 로그인 하거나 수 해당 키를 사용 하 여 서비스입니다. 따라서 전달 구를 만드는 것이 좋습니다. 그러나 hello 암호를 잊은 경우는 방식으로 toorecover 없습니다 것입니다.
   >
   >

    Tooenter 암호를 클릭 하 여 **아니요**, hello 주 PuTTYgen 창에는 암호를 입력 하 고 클릭 **개인 키 저장** 다시 합니다. 그렇지 않으면 클릭 **예** toocontinue hello 선택적으로 암호를 제공 하지 않고 있습니다.
9. 이름 및 위치 toosave PPK 파일을 입력 합니다.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Putty tooSSH tooa Linux 컴퓨터를 사용 하 여
다시금 말하지만 PuTTY는 Windows용 공용 SSH 클라이언트입니다. 사용자는 무료 toouse SSH 클라이언트를 합니다. 다음 단계 세부 정보를 어떻게 hello toouse와 SSH를 사용 하 여 Azure VM에 개인 키 tooauthenticate 합니다. hello 단계는 다른 SSH 키 클라이언트 tooload SSH 연결에 개인 키 tooauthenticate hello 필요 측면에서 유사 합니다.

1. 다운로드 및 실행된 putty에서 위치 다음 hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Hello 호스트 이름 또는 hello Azure 포털에서에서 VM의 IP 주소를 입력 합니다.

    ![새 PuTTY 연결 열기](./media/ssh-from-windows/putty-new-connection.png)
3. **열기**를 선택하기 전에 **연결** > **SSH** > **인증** 탭을 클릭합니다. 찾아보기 tooand 사용자의 개인 키를 선택 합니다.

    ![인증용 PuTTY 개인 키 선택](./media/ssh-from-windows/putty-auth-dialog.png)
4. 클릭 **열려** tooconnect tooyour 가상 컴퓨터

## <a name="next-steps"></a>다음 단계
Hello 공개 및 개인 키를 생성할 수도 있습니다 [Osx 및 Linux를 사용 하 여](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

이용한 적 for Windows 및 Windows 컴퓨터에서 쉽게 사용할 수 있는 OSS 도구의 hello 이점에 대 한 자세한 내용은 참조 [Windows에서 Ubuntu를 이용한 적](https://msdn.microsoft.com/commandline/wsl/about)합니다.

SSH tooconnect tooyour Linux Vm을 사용 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
