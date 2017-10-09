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
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a><span data-ttu-id="2c2a3-103">Azure에서 Windows를 통해 tooUse SSH 키 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2c2a3-103">How tooUse SSH keys with Windows on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c2a3-104">Windows</span><span class="sxs-lookup"><span data-stu-id="2c2a3-104">Windows</span></span>](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [<span data-ttu-id="2c2a3-105">Linux/Mac</span><span class="sxs-lookup"><span data-stu-id="2c2a3-105">Linux/Mac</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

<span data-ttu-id="2c2a3-106">TooLinux Azure의 가상 컴퓨터 (Vm)에 연결할 때 사용 해야 [공개 키 암호화](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide tooyour Linux VM의에서 보다 안전한 방식으로 toolog 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-106">When you connect tooLinux virtual machines (VMs) in Azure, you should use [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide a more secure way toolog in tooyour Linux VM.</span></span> <span data-ttu-id="2c2a3-107">이 프로세스를 사용 하 여 hello 보안 셸 (SSH) 명령 tooauthenticate 직접 사용자 이름 및 암호 대신 공용 및 개인 키 교환 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-107">This process involves a public and private key exchange using hello secure shell (SSH) command tooauthenticate yourself rather than a username and password.</span></span> <span data-ttu-id="2c2a3-108">암호는 웹 서버 등과 같이 인터넷 연결 Vm에서 특히 취약 toobrute 대입 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-108">Passwords are vulnerable toobrute-force attacks, especially on Internet-facing VMs such as web servers.</span></span> <span data-ttu-id="2c2a3-109">이 문서에서는 SSH 키 및 toogenerate Windows 컴퓨터에 적절 한 키를 hello 하는 방법에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-109">This article provides an overview of SSH keys and how toogenerate hello appropriate keys on a Windows computer.</span></span>

## <a name="overview-of-ssh-and-keys"></a><span data-ttu-id="2c2a3-110">SSH 및 키에 대한 개요</span><span class="sxs-lookup"><span data-stu-id="2c2a3-110">Overview of SSH and keys</span></span>
<span data-ttu-id="2c2a3-111">공개 및 개인 키를 사용 하 여 tooyour Linux VM을 안전 하 게 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-111">You can securely log in tooyour Linux VM by using public and private keys:</span></span>

* <span data-ttu-id="2c2a3-112">hello **공개 키** Linux VM을 또는 원하는 toouse 공개 키 암호화와 기타 서비스에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-112">hello **public key** is placed on your Linux VM, or any other service that you wish toouse with public-key cryptography.</span></span>
* <span data-ttu-id="2c2a3-113">hello **개인 키** tooverify에 로그인 할 때가 있는 tooyour Linux VM 하는 사용자의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-113">hello **private key** is what you present tooyour Linux VM when you log in, tooverify your identity.</span></span> <span data-ttu-id="2c2a3-114">이 개인 키는 보호해야 하는 한편,</span><span class="sxs-lookup"><span data-stu-id="2c2a3-114">Protect this private key.</span></span> <span data-ttu-id="2c2a3-115">공유하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-115">Do not share it.</span></span>

<span data-ttu-id="2c2a3-116">이러한 공용 및 개인 키는 여러 VM 및 서비스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-116">These public and private keys can be used on multiple VMs and services.</span></span> <span data-ttu-id="2c2a3-117">각 VM 또는 tooaccess 서비스에 대 한 키 쌍이 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-117">You do not need a pair of keys for each VM or service you wish tooaccess.</span></span> <span data-ttu-id="2c2a3-118">자세한 개요에 대해서는 [public-key 암호화](https://wikipedia.org/wiki/Public-key_cryptography)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-118">For a more detailed overview, see [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="2c2a3-119">SSH는 안전하지 않은 연결에서 안전하게 로그인할 수 있도록 하는 암호화된 연결 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-119">SSH is an encrypted connection protocol that allows secure logins over unsecured connections.</span></span> <span data-ttu-id="2c2a3-120">Azure에서 호스팅되는 Linux Vm에 대 한 hello 기본 연결 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-120">It is hello default connection protocol for Linux VMs hosted in Azure.</span></span> <span data-ttu-id="2c2a3-121">SSH 자체 암호화 된 연결을 제공 하지만 암호를 사용 하 여 SSH 연결을 사용 하더라도 hello VM 취약 toobrute 대입 공격 및 암호 추측.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-121">Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves hello VM vulnerable toobrute-force attacks or guessing of passwords.</span></span> <span data-ttu-id="2c2a3-122">연결 tooa는 더 안전 하 고 기본 방법은 이러한 공용 및 개인 키, 라고도 SSH 키를 사용 하 여 SSH를 사용 하 여 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-122">A more secure and preferred method of connecting tooa VM using SSH is by using these public and private keys, also known as SSH keys.</span></span>

<span data-ttu-id="2c2a3-123">SSH 키 toouse 지 tooyour 암호를 사용 하 여 Linux Vm에에서 로깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-123">If you do not wish toouse SSH keys, you can still log in tooyour Linux VMs using a password.</span></span> <span data-ttu-id="2c2a3-124">VM 인터넷 노출된 toohello 없는 경우에 암호를 사용 하 여 충분 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-124">If your VM is not exposed toohello Internet, using passwords may be sufficient.</span></span> <span data-ttu-id="2c2a3-125">그러나 여전히 toomanage 암호 각 Linux VM에 대 한 및 해야 정상 암호 정책 및 사례를 정기적으로 업데이트 하 고 최소 암호 길이 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-125">However, you still need toomanage your passwords for each Linux VM and maintain healthy password policies and practices, such as minimum password length and regularly updating them.</span></span> <span data-ttu-id="2c2a3-126">SSH 키의 hello 사용 여러 Vm 간에 개별 자격 증명 관리 hello 복잡성을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-126">hello use of SSH keys reduces hello complexity of managing individual credentials across multiple VMs.</span></span>

## <a name="windows-packages-and-ssh-clients"></a><span data-ttu-id="2c2a3-127">Windows 패키지 및 SSH 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2c2a3-127">Windows packages and SSH clients</span></span>
<span data-ttu-id="2c2a3-128">Tooand 연결에서 사용 하 여 Azure Linux Vm을 관리 한 **SSH 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-128">You connect tooand manage Linux VMs in Azure using an **SSH client**.</span></span> <span data-ttu-id="2c2a3-129">일반적으로 Windows 컴퓨터에는 SSH 클라이언트를 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-129">Windows computers do not typically have an SSH client installed.</span></span> <span data-ttu-id="2c2a3-130">Windows 10 Anniversary 업데이트 hello를 이용한 적 for Windows를 추가 하 고 hello 최신 Windows 10 작성자 업데이트는 제공 추가 업데이트.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-130">hello Windows 10 Anniversary Update added Bash for Windows, and hello latest Windows 10 Creators Update provides additional updates.</span></span> <span data-ttu-id="2c2a3-131">Linux에 대 한이 Windows 하위 Bash 셸의 내에서 고유 하 게 SSH 클라이언트 등의 toorun 및 액세스 유틸리티도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-131">This Windows Subsystem for Linux allows you toorun and access utilities such as an SSH client natively within a Bash shell.</span></span> <span data-ttu-id="2c2a3-132">그런 다음 하나를 수행 hello Linux 문서와 같은 [Linux 용 toogenerate SSH 키 쌍은 어떻게](mac-create-ssh-keys.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-132">You can then follow any of hello Linux docs, such as [How toogenerate SSH key pairs for Linux](mac-create-ssh-keys.md).</span></span> <span data-ttu-id="2c2a3-133">Windows용 Bash는 아직 개발 중이며 베타 릴리스 버전으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-133">Bash for Windows is still under development, and is considered a beta release.</span></span> <span data-ttu-id="2c2a3-134">Windows용 Bash에 대한 자세한 내용은 [Ubuntu on Windows의 Bash](https://msdn.microsoft.com/commandline/wsl/about)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-134">For more information about Bash for Windows, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="2c2a3-135">원할 경우 toouse 무언가 이용한 적에 대 한 Windows 이외의 일반적인 Windows SSH 클라이언트를 설치할 수 있습니다는 hello 다음 패키지에에서 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-135">If you wish toouse something other than Bash for Windows, common Windows SSH clients you can install are included in hello following packages:</span></span>

* [<span data-ttu-id="2c2a3-136">Windows 용 Git</span><span class="sxs-lookup"><span data-stu-id="2c2a3-136">Git For Windows</span></span>](https://git-for-windows.github.io/)
* [<span data-ttu-id="2c2a3-137">puTTY</span><span class="sxs-lookup"><span data-stu-id="2c2a3-137">puTTY</span></span>](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [<span data-ttu-id="2c2a3-138">MobaXterm</span><span class="sxs-lookup"><span data-stu-id="2c2a3-138">MobaXterm</span></span>](http://mobaxterm.mobatek.net/)
* [<span data-ttu-id="2c2a3-139">Cygwin</span><span class="sxs-lookup"><span data-stu-id="2c2a3-139">Cygwin</span></span>](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a><span data-ttu-id="2c2a3-140">키 파일 toocreate 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="2c2a3-140">Which key files do you need toocreate?</span></span>
<span data-ttu-id="2c2a3-141">Azure는 최소한 2048비트, **ssh-rsa** 형식 공개 및 개인 키 서식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-141">Azure requires at least 2048-bit, **ssh-rsa** formatted public and private keys.</span></span> <span data-ttu-id="2c2a3-142">Hello 클래식 배포 모델을 사용 하 여 Azure 리소스를 관리 하는 경우 또한 해야 toogenerate PEM (`.pem` 파일).</span><span class="sxs-lookup"><span data-stu-id="2c2a3-142">If you are managing Azure resources using hello Classic deployment model, you also need toogenerate a PEM (`.pem` file).</span></span>

<span data-ttu-id="2c2a3-143">다음은 hello 배포 시나리오와 각 사용 파일 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-143">Here are hello deployment scenarios, and hello types of files you use in each:</span></span>

1. <span data-ttu-id="2c2a3-144">**ssh rsa** hello를 사용 하 여 모든 배포에 키가 필요 [Azure 포털](https://portal.azure.com), 및 hello를 사용 하 여 리소스 관리자 배포 [Azure CLI](../../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-144">**ssh-rsa** keys are required for any deployment using hello [Azure portal](https://portal.azure.com), and Resource Manager deployments using hello [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="2c2a3-145">대개 이러한 키는 대부분의 모든 사용자에게 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-145">These keys are usually all most people need.</span></span>
2. <span data-ttu-id="2c2a3-146">A `.pem` 파일은 hello 클래식 배포를 사용 하 여 필요한 toocreate Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-146">A `.pem` file is required toocreate VMs using hello Classic deployment.</span></span> <span data-ttu-id="2c2a3-147">Hello를 사용 하는 경우 클래식 배포에서는 이러한 키가 지원 [Azure 포털](https://portal.azure.com) 또는 [Azure CLI](../../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-147">These keys are supported in Classic deployments when using hello [Azure portal](https://portal.azure.com) or [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="2c2a3-148">필요할 때만 toocreate 이러한 추가 키와 인증서 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 관리 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-148">You only need toocreate these additional keys and certificates if you are managing resources created using hello Classic deployment model.</span></span>

## <a name="install-git-for-windows"></a><span data-ttu-id="2c2a3-149">Windows용 Git 설치</span><span class="sxs-lookup"><span data-stu-id="2c2a3-149">Install Git for Windows</span></span>
<span data-ttu-id="2c2a3-150">hello 이전 섹션에 나열 hello를 포함 하는 여러 패키지 `openssl` Windows 용 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-150">hello preceding section listed several packages that include hello `openssl` tool for Windows.</span></span> <span data-ttu-id="2c2a3-151">이 도구는 필요한 toocreate 공개 및 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-151">This tool is needed toocreate public and private keys.</span></span> <span data-ttu-id="2c2a3-152">예제 세부 정보를 어떻게 다음 hello tooinstall 사용 하 여 **Windows 용 Git**경우에 원하는 어떤 패키지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-152">hello following examples detail how tooinstall and use **Git for Windows**, though you can choose whichever package you prefer.</span></span> <span data-ttu-id="2c2a3-153">**Windows 용 Git** toosome 추가 하는 오픈 소스 소프트웨어를 액세스할 수 있습니다 ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) 도구 및 유틸리티를 사용할 때는 Linux Vm의 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-153">**Git for Windows** gives you access toosome additional open-source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) tools and utilities that may be useful as you work with Linux VMs.</span></span>

1. <span data-ttu-id="2c2a3-154">다운로드 및 설치 **Windows 용 Git** hello 수정할 수 있는 위치에서에서: [https://git-for-windows.github.io/](https://git-for-windows.github.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-154">Download and install **Git for Windows** from hello following location: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span></span>
2. <span data-ttu-id="2c2a3-155">Toochange 특별히 필요한 경우가 아니면 hello 시 hello 기본 옵션 설치 프로세스에 동의 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-155">Accept hello default options during hello install process unless you specifically need toochange them.</span></span>
3. <span data-ttu-id="2c2a3-156">실행 **Git Bash** hello에서 **시작 메뉴** > **Git** > **Git Bash**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-156">Run **Git Bash** from hello **Start Menu** > **Git** > **Git Bash**.</span></span> <span data-ttu-id="2c2a3-157">hello 콘솔에는 다음 예제와 비슷한 toohello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-157">hello console looks similar toohello following example:</span></span>

    ![Windows용 Git의 Bash 셸](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a><span data-ttu-id="2c2a3-159">개인 키 만들기</span><span class="sxs-lookup"><span data-stu-id="2c2a3-159">Create a private key</span></span>
1. <span data-ttu-id="2c2a3-160">사용자 **Git Bash** 창을 사용 하 여 `openssl.exe` toocreate 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-160">In your **Git Bash** window, use `openssl.exe` toocreate a private key.</span></span> <span data-ttu-id="2c2a3-161">hello 다음 예제에서는 라는 키 `myPrivateKey` 및 명명 된 인증서 `myCert.pem`:</span><span class="sxs-lookup"><span data-stu-id="2c2a3-161">hello following example creates a key named `myPrivateKey` and certificate named `myCert.pem`:</span></span>

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    <span data-ttu-id="2c2a3-162">hello 출력은 다음 예제와 비슷한 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-162">hello output looks similar toohello following example:</span></span>

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

   <span data-ttu-id="2c2a3-163">Bash가 오류를 보고하는 경우 상승된 권한으로 새 **Git Bash** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-163">If bash reports an error, try opening a new **Git Bash** window with elevated privileges.</span></span> <span data-ttu-id="2c2a3-164">그런 다음 hello를 다시 실행 `openssl` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-164">Then, rerun hello `openssl` command.</span></span>

2. <span data-ttu-id="2c2a3-165">국가 이름, 위치, 조직 이름 등에 대 한 응답 hello 메시지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-165">Answer hello prompts for country name, location, organization name, etc.</span></span>
3. <span data-ttu-id="2c2a3-166">새 개인 키와 인증서가 현재 작업 중인 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-166">Your new private key and certificate are created in your current working directory.</span></span> <span data-ttu-id="2c2a3-167">보안 조치로,만 액세스할 수 있도록 사용자의 개인 키 hello 사용 권한을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-167">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. <span data-ttu-id="2c2a3-168">hello [절로](#create-a-private-key-for-putty) PuTTYgen tooboth를 사용 하 여 세부 정보 보기 및 hello 공개 키를 사용 하 여 PuTTY tooSSH tooLinux Vm을 사용 하 여에 대 한 특정 개인 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-168">hello [next section](#create-a-private-key-for-putty) details using PuTTYgen tooboth view and use hello public key, and create a private key specific for using PuTTY tooSSH tooLinux VMs.</span></span> <span data-ttu-id="2c2a3-169">hello 다음 명령은 생성 라는 공개 키 파일 `myPublicKey.key` 바로 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="2c2a3-169">hello following command generates a public key file named `myPublicKey.key` that you can use right away:</span></span>

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. <span data-ttu-id="2c2a3-170">Toomanage 클래식 리소스를 필요할 경우 변환 hello `myCert.pem` 너무`myCert.cer` (DER로 인코딩된 X509 인증서).</span><span class="sxs-lookup"><span data-stu-id="2c2a3-170">If you also need toomanage Classic resources, convert hello `myCert.pem` too`myCert.cer` (DER encoded X509 certificate).</span></span> <span data-ttu-id="2c2a3-171">Toospecifically 해야 하는 경우에이 선택적 단계를 수행 합니다. 이전 클래식 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-171">Perform this optional step only if you need toospecifically manage older Classic resources.</span></span>

    <span data-ttu-id="2c2a3-172">다음 명령을 hello를 사용 하 여 hello 인증서를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-172">Convert hello certificate using hello following command:</span></span>

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a><span data-ttu-id="2c2a3-173">PuTTY용 개인 키 만들기</span><span class="sxs-lookup"><span data-stu-id="2c2a3-173">Create a private key for PuTTY</span></span>
<span data-ttu-id="2c2a3-174">PuTTY는 Windows용 공용 SSH 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-174">PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="2c2a3-175">사용자는 무료 toouse SSH 클라이언트를 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-175">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="2c2a3-176">PuTTY toouse toocreate 특별 한 종류의 키-는 PuTTY 개인 키 (PPK) 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-176">toouse PuTTY, you need toocreate an additional type of key - a PuTTY Private Key (PPK).</span></span> <span data-ttu-id="2c2a3-177">Toouse PuTTY를 원하지 않는 경우이 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-177">If you do not wish toouse PuTTY, skip this section.</span></span>

<span data-ttu-id="2c2a3-178">hello 다음 예제에서는이 키를 만들며 추가 개인 PuTTY toouse 용으로 특별히:</span><span class="sxs-lookup"><span data-stu-id="2c2a3-178">hello following example creates this additional private key specifically for PuTTY toouse:</span></span>

1. <span data-ttu-id="2c2a3-179">사용 하 여 **Git Bash** tooconvert PuTTYgen 이해할 수 RSA 개인 키로 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-179">Use **Git Bash** tooconvert your private key into an RSA private key that PuTTYgen can understand.</span></span> <span data-ttu-id="2c2a3-180">hello 다음 예제에서는 라는 키 `myPrivateKey_rsa` 라는 hello 기존 키에서 `myPrivateKey`:</span><span class="sxs-lookup"><span data-stu-id="2c2a3-180">hello following example creates a key named `myPrivateKey_rsa` from hello existing key named `myPrivateKey`:</span></span>

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    <span data-ttu-id="2c2a3-181">보안 조치로,만 액세스할 수 있도록 사용자의 개인 키 hello 사용 권한을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-181">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. <span data-ttu-id="2c2a3-182">에서 다운로드 및 실행 PuTTYgen hello 수정할 수 있는 위치: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="2c2a3-182">Download and run PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
3. <span data-ttu-id="2c2a3-183">Hello 메뉴: **파일** > **부하 개인 키**</span><span class="sxs-lookup"><span data-stu-id="2c2a3-183">Click hello menu: **File** > **Load Private Key**</span></span>
4. <span data-ttu-id="2c2a3-184">사용자의 개인 키를 찾습니다 (`myPrivateKey_rsa` hello 이전 예제에서).</span><span class="sxs-lookup"><span data-stu-id="2c2a3-184">Locate your private key (`myPrivateKey_rsa` in hello previous example).</span></span> <span data-ttu-id="2c2a3-185">시작할 때 hello 기본 디렉터리 **Git Bash** 은 `C:\Users\%username%`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-185">hello default directory when you start **Git Bash** is `C:\Users\%username%`.</span></span> <span data-ttu-id="2c2a3-186">Hello 파일 필터 tooshow 변경 **모든 파일 (\*.\*)** :</span><span class="sxs-lookup"><span data-stu-id="2c2a3-186">Change hello file filter tooshow **All Files (\*.\*)**:</span></span>

    ![PuTTYgen hello 기존 개인 키 로드](./media/ssh-from-windows/load-private-key.png)
5. <span data-ttu-id="2c2a3-188">**열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-188">Click **Open**.</span></span> <span data-ttu-id="2c2a3-189">메시지가 해당 hello 키가 성공적으로 가져왔습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-189">A prompt indicates that hello key has been successfully imported:</span></span>

    ![성공적으로 가져온된 키 tooPuTTYgen](./media/ssh-from-windows/successfully-imported-key.png)
6. <span data-ttu-id="2c2a3-191">클릭 **확인** tooclose hello 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-191">Click **OK** tooclose hello prompt.</span></span>
7. <span data-ttu-id="2c2a3-192">hello 공개 키가 hello hello 위쪽에 표시 됩니다. **PuTTYgen** 창.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-192">hello public key is displayed at hello top of hello **PuTTYgen** window.</span></span> <span data-ttu-id="2c2a3-193">복사한 Linux VM을 만들 때 hello Azure 포털 또는 Azure 리소스 관리자 템플릿에이 공개 키를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-193">You copy and paste this public key into hello Azure portal or Azure Resource Manager template when you create a Linux VM.</span></span> <span data-ttu-id="2c2a3-194">클릭할 수도 있습니다 **저장 공개 키** toosave 복사본 tooyour 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="2c2a3-194">You can also click **Save public key** toosave a copy tooyour computer:</span></span>

    ![PuTTY 공개 키 파일 저장](./media/ssh-from-windows/save-public-key.png)

    <span data-ttu-id="2c2a3-196">hello 다음 예제를 복사 하는 방법을 Linux VM을 만들 때 hello Azure 포털에이 공개 키를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-196">hello following example shows how you would copy and paste this public key into hello Azure portal when you create a Linux VM.</span></span> <span data-ttu-id="2c2a3-197">hello 공개 키는 일반적으로에 저장 한 다음 `~/.ssh/authorized_keys` 새 VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-197">hello public key is typically then stored in `~/.ssh/authorized_keys` on your new VM.</span></span>

    ![Hello Azure 포털에서에서 VM을 만들 때 공개 키를 사용 하 여](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. <span data-ttu-id="2c2a3-199">다음과 같이 다시 **PuTTYgen**에서 **개인 키 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-199">Back in **PuTTYgen**, Click **Save private Key**:</span></span>

    ![PuTTY 개인 키 파일 저장](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > <span data-ttu-id="2c2a3-201">메시지가 트 키에 대 한 암호를 입력 하지 않고 toocontinue 원하는 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-201">A prompt asks if you wish toocontinue without entering a passphrase for your key.</span></span> <span data-ttu-id="2c2a3-202">암호는 암호 tooyour 연결 된 개인 키와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-202">A passphrase is like a password attached tooyour private key.</span></span> <span data-ttu-id="2c2a3-203">Tooobtain 사용자 인 경우에 사용자의 개인 키를 여전히 됩니다 수 tooauthenticate hello 키만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-203">Even if someone were tooobtain your private key, they still would not be able tooauthenticate using just hello key.</span></span> <span data-ttu-id="2c2a3-204">Hello 암호를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-204">They would also need hello passphrase.</span></span> <span data-ttu-id="2c2a3-205">암호 없이 사용자의 개인 키를 가져오면 누군가가 tooany VM에에서 로그인 하거나 수 해당 키를 사용 하 여 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-205">Without a passphrase, if someone obtains your private key, they can log in tooany VM or service that uses that key.</span></span> <span data-ttu-id="2c2a3-206">따라서 전달 구를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-206">We recommend you create a passphrase.</span></span> <span data-ttu-id="2c2a3-207">그러나 hello 암호를 잊은 경우는 방식으로 toorecover 없습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-207">However, if you forget hello passphrase, there is no way toorecover it.</span></span>
   >
   >

    <span data-ttu-id="2c2a3-208">Tooenter 암호를 클릭 하 여 **아니요**, hello 주 PuTTYgen 창에는 암호를 입력 하 고 클릭 **개인 키 저장** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-208">If you wish tooenter a passphrase, click **No**, enter a passphrase in hello main PuTTYgen window, and then click **Save private key** again.</span></span> <span data-ttu-id="2c2a3-209">그렇지 않으면 클릭 **예** toocontinue hello 선택적으로 암호를 제공 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-209">Otherwise, click **Yes** toocontinue without providing hello optional passphrase.</span></span>
9. <span data-ttu-id="2c2a3-210">이름 및 위치 toosave PPK 파일을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-210">Enter a name and location toosave your PPK file.</span></span>

## <a name="use-putty-toossh-tooa-linux-machine"></a><span data-ttu-id="2c2a3-211">Putty tooSSH tooa Linux 컴퓨터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2c2a3-211">Use Putty tooSSH tooa Linux Machine</span></span>
<span data-ttu-id="2c2a3-212">다시금 말하지만 PuTTY는 Windows용 공용 SSH 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-212">Again, PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="2c2a3-213">사용자는 무료 toouse SSH 클라이언트를 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-213">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="2c2a3-214">다음 단계 세부 정보를 어떻게 hello toouse와 SSH를 사용 하 여 Azure VM에 개인 키 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-214">hello following steps detail how toouse your private key tooauthenticate with your Azure VM using SSH.</span></span> <span data-ttu-id="2c2a3-215">hello 단계는 다른 SSH 키 클라이언트 tooload SSH 연결에 개인 키 tooauthenticate hello 필요 측면에서 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-215">hello steps are similar in other SSH key clients in terms of needing tooload your private key tooauthenticate hello SSH connection.</span></span>

1. <span data-ttu-id="2c2a3-216">다운로드 및 실행된 putty에서 위치 다음 hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="2c2a3-216">Download and run putty from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="2c2a3-217">Hello 호스트 이름 또는 hello Azure 포털에서에서 VM의 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-217">Fill in hello host name or IP address of your VM from hello Azure portal:</span></span>

    ![새 PuTTY 연결 열기](./media/ssh-from-windows/putty-new-connection.png)
3. <span data-ttu-id="2c2a3-219">**열기**를 선택하기 전에 **연결** > **SSH** > **인증** 탭을 클릭합니다. 찾아보기 tooand 사용자의 개인 키를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-219">Before selecting **Open**, click **Connection** > **SSH** > **Auth** tab. Browse tooand select your private key:</span></span>

    ![인증용 PuTTY 개인 키 선택](./media/ssh-from-windows/putty-auth-dialog.png)
4. <span data-ttu-id="2c2a3-221">클릭 **열려** tooconnect tooyour 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="2c2a3-221">Click **Open** tooconnect tooyour virtual machine</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c2a3-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c2a3-222">Next steps</span></span>
<span data-ttu-id="2c2a3-223">Hello 공개 및 개인 키를 생성할 수도 있습니다 [Osx 및 Linux를 사용 하 여](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-223">You can also generate hello public and private keys [using OS X and Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2c2a3-224">이용한 적 for Windows 및 Windows 컴퓨터에서 쉽게 사용할 수 있는 OSS 도구의 hello 이점에 대 한 자세한 내용은 참조 [Windows에서 Ubuntu를 이용한 적](https://msdn.microsoft.com/commandline/wsl/about)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-224">For more information about Bash for Windows and hello benefits of having OSS tools readily available on your Windows computer, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="2c2a3-225">SSH tooconnect tooyour Linux Vm을 사용 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c2a3-225">If you have trouble using SSH tooconnect tooyour Linux VMs, see [Troubleshoot SSH connections tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
