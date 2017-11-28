---
title: "Azure Linux 가상 컴퓨터에서 SSHD aaaConfigure | Microsoft Docs"
description: "보안 모범 사례 및 toolockdown SSH tooAzure Linux 가상 컴퓨터에 대 한 SSHD를 구성 합니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="828e4-103">Azure Linux VM에서 SSHD 구성</span><span class="sxs-lookup"><span data-stu-id="828e4-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="828e4-104">이 문서에서는 toolockdown 암호 대신 SSH 키를 사용 하 여 Linux, tooprovide 모범 사례 보안 및 hello SSH 로그인 프로세스를 toospeed SSH 서버를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="828e4-105">toofurther 잠금 수 toologin 없도록 toodisable hello 루트 사용자를 하겠습니다 SSHD 제한 hello 수 있는 사용자는 승인 된 그룹 목록을 통해 toologin SSH 프로토콜 버전 1을 사용 하지 않도록 설정 하 고, 최소 비트 키를 설정, 유휴 사용자의 자동 로그 아웃을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="828e4-106">이 문서에 대 한 hello 요구 사항은: Azure 계정 ([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/)) 및 [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="828e4-107">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="828e4-107">Quick Commands</span></span>

<span data-ttu-id="828e4-108">구성 `/etc/ssh/sshd_config` 설정 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="828e4-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="828e4-109">암호 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="828e4-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="828e4-110">Hello 루트 사용자가 로그인을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="828e4-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="828e4-111">그룹 목록 허용</span><span class="sxs-lookup"><span data-stu-id="828e4-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="828e4-112">사용자 목록 허용</span><span class="sxs-lookup"><span data-stu-id="828e4-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="828e4-113">SSH 프로토콜 버전 1을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="828e4-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="828e4-114">최소 키 비트</span><span class="sxs-lookup"><span data-stu-id="828e4-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="828e4-115">유휴 사용자 연결 끊기</span><span class="sxs-lookup"><span data-stu-id="828e4-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="828e4-116">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="828e4-116">Detailed Walkthrough</span></span>

<span data-ttu-id="828e4-117">SSHD는 hello hello Linux VM에서 실행 되는 SSH 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="828e4-118">SSH는 MacBook의 셸, Linux 워크스테이션 또는 Windows의 Bash에서 실행되는 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="828e4-119">SSH는 hello toosecure 사용 되는 프로토콜과 워크스테이션 및 hello SSH VPN (가상 사설망)도 수행 하는 Linux VM 간의 hello 통신을 암호화 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="828e4-120">이 문서는 매우 중요 한 tookeep 하나의 로그인 tooyour hello 전체 연습에 대 한 Linux VM 엽니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="828e4-121">SSH 연결 설정 되 면로 그대로 남아 세션이 열린으로 hello 창이 닫혀 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="828e4-122">로그인 한 터미널에 대해 있습니다 변경 내용을 toobe toohello SSHD 서비스를 없이 주요 변경 내용이 경우 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="828e4-123">끊어진된 SSHD 구성 사용 하 여 Linux VM 수행 잠기는, Azure 기능을 제공 hello 기능 tooreset hello로 손상된 된 SSHD 구성 [Azure VM 액세스 확장](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="828e4-124">이러한 이유로 म 열고 두 터미널 SSH toohello Linux VM에서 둘 모두.</span><span class="sxs-lookup"><span data-stu-id="828e4-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="828e4-125">Hello 첫 번째 터미널 toomake hello 변경 tooSSHDs 구성 파일을 사용 하 고 hello SSHD 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="828e4-126">이러한 변경 사항이 hello 서비스 다시 시작 되 면 터미널 tootest 두 번째 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="828e4-127">SSH 암호를 해제 하는 것 이므로 엄격 하 게 SSH 키, SSH 키에 잘못 된 하 고 hello 연결 toohello VM을 닫으면에 의존 hello VM 영구적으로 됩니다 잠기고 아무도 수 toologin tooit 삭제 하 고 다시 toobe 요구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="828e4-128">암호 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="828e4-128">Disable password logins</span></span>

<span data-ttu-id="828e4-129">가장 빠른 방법은 toosecure hello Linux VM는 toodisable 암호 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="828e4-130">암호 로그인을 사용할 수 없는 hello 암호 SSH를 사용 하 여 Linux VM에 대 한 강제로 봇 크롤링 hello 웹 toobrute 시도 즉시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="828e4-131">로그인 암호를 완전히 해제, 모든 암호 로그인 시도 hello SSH 서버 tooignore 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="828e4-132">Hello 루트 사용자가 로그인을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="828e4-132">Disable login by hello root user</span></span>

<span data-ttu-id="828e4-133">다음 Linux 모범 사례를 hello `root` 사용자 되지에 사용 하 여 또는 SSH를 통해 기록 되도록 `sudo su`합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="828e4-134">루트 수준의 권한이 필요한 모든 명령을 hello를 통해 항상 실행 해야 `sudo` 모든 작업을 나중에 감사를 기록 하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="828e4-135">사용 하지 않도록 설정 hello `root` SSH를 통한 로그인에서 사용자는 권한이 있는 사용자만 tooSSH 허용지 않습니다 보장 하는 보안 모범 사례 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="828e4-136">그룹 목록 허용</span><span class="sxs-lookup"><span data-stu-id="828e4-136">Allowed groups list</span></span>

<span data-ttu-id="828e4-137">SSH는 사용자 및 그룹에 SSH를 통한 로그인을 허용하거나 허용하지 않도록 제한하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="828e4-138">이 기능은 목록 tooapprove를 사용 하거나 특정 사용자 및 그룹에 로그인 하지 못하도록 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="828e4-139">Hello 휠 그룹 toohello 설정 `AllowGroups` 목록 hello 휠 그룹에 있는 SSH toojust 사용자 계정을 통해 승인 된 로그인을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="828e4-140">사용자 목록 허용</span><span class="sxs-lookup"><span data-stu-id="828e4-140">Allowed users list</span></span>

<span data-ttu-id="828e4-141">Tooaccomplish hello 같은 보다 구체적인 방식으로 작업 하는 SSH 로그인 toojust 사용자 제한 `AllowGroups` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="828e4-142">SSH 프로토콜 버전 1을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="828e4-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="828e4-143">SSH 프로토콜 버전 1은 안전하지 않고 비활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="828e4-144">SSH 프로토콜 버전 2는 안전 하 게 tooSSH tooyour 서버에서 제공 하는 hello 현재 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="828e4-145">SSH 버전 1 사용 하 여 hello SSH 서버와 tooestablish를 시도 하는 모든 SSH 클라이언트 연결을 거부 SSH 버전 1 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="828e4-146">SSH 버전 2 연결 toonegotiate 허용 되며 hello SSH 서버와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="828e4-147">최소 키 비트</span><span class="sxs-lookup"><span data-stu-id="828e4-147">Minimum key bits</span></span>

<span data-ttu-id="828e4-148">보안 모범 사례 암호 SSH 로그인을 사용할 수 없습니다 및 SSH 키만 toobe tooauthenticate hello SSH 서버에 사용 되는 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="828e4-149">비트 단위로 측정된 길이가 다른 키를 사용하여 이러한 SSH 키를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="828e4-150">모범 사례 키 길이가 2048 비트의 hello 최소 허용 가능한 키 길이 상태.</span><span class="sxs-lookup"><span data-stu-id="828e4-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="828e4-151">2048비트 미만의 키는 이론적으로 손상되었을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="828e4-152">설정 hello `ServerKeyBits` 너무`2048` 2048 비트 이상 키를 사용 하 여 모든 연결을 허용 하 고 보다 작은 2048 비트의 연결을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="828e4-153">유휴 사용자 연결 끊기</span><span class="sxs-lookup"><span data-stu-id="828e4-153">Disconnect idle users</span></span>

<span data-ttu-id="828e4-154">SSH에 대 한 유휴 시간 (초) 정해진된 기간 보다 그 이상 전문적 열린 연결이 있는 hello 기능 toodisconnect 사용자.</span><span class="sxs-lookup"><span data-stu-id="828e4-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="828e4-155">열려 있는 세션 tooonly hello Linux VM의 활성 제한 hello 노출을 인 사용자를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="828e4-156">SSHD 다시 시작</span><span class="sxs-lookup"><span data-stu-id="828e4-156">Restart SSHD</span></span>

<span data-ttu-id="828e4-157">tooenable hello 설정을 `/etc/ssh/sshd_config` hello SSH 서버를 다시 시작 하는 hello SSHD 프로세스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="828e4-158">hello open SSH 세션을 손실 하지 않고 toorestart hello SSH 서버를 사용 하는 hello 터미널 창을 열려 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="828e4-159">두 번째 터미널 창이 나 탭을 사용 하는 tootest hello 새 SSH 서버 설정 합니다.  별도 터미널 tootest hello SSH 연결을 사용 하 여 다시 toogo 하 고 있습니다 확인 추가 변경 toohello `/etc/ssh/sshd_config` SSHD 주요 변경 내용에 의해 잠기지 않고 hello 첫 번째 터미널에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="828e4-160">Redhat, Centos 및 Fedora에서</span><span class="sxs-lookup"><span data-stu-id="828e4-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="828e4-161">Debian 및 Ubuntu에서</span><span class="sxs-lookup"><span data-stu-id="828e4-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="828e4-162">Azure 재설정 액세스를 사용하여 SSHD 다시 설정</span><span class="sxs-lookup"><span data-stu-id="828e4-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="828e4-163">주요 변경 toohello SSHD 구성에서 잠긴 경우 hello Azure VM 액세스 확장 tooreset hello SSHD 구성 뒤로 toohello 원래 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="828e4-164">모든 예제 이름을 고유한 설정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="828e4-165">Fail2ban 설치</span><span class="sxs-lookup"><span data-stu-id="828e4-165">Install Fail2ban</span></span>

<span data-ttu-id="828e4-166">Tooinstall 및 설정 hello 오픈 소스 응용 프로그램 Fail2ban, 블록 무차별 암호 대입을 사용 하 여 SSH를 통해 시도 toologin tooyour Linux VM 반복 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="828e4-167">반복 Fail2ban 로그 시도 toologin SSH를 통해 실패 한 다음 방화벽 규칙을 tooblock hello IP 주소에서 비롯 되는지 hello 시도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="828e4-168">Fail2ban 홈페이지</span><span class="sxs-lookup"><span data-stu-id="828e4-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="828e4-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="828e4-169">Next Steps</span></span>

<span data-ttu-id="828e4-170">구성 하 고 hello SSH 서버 잠겨 있으며 Linux VM에서 추가 보안 모범 사례를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="828e4-171">사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에서 VMAccess 확장을 환영</span><span class="sxs-lookup"><span data-stu-id="828e4-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="828e4-172">Hello Azure CLI를 사용 하 여 Linux VM에서 디스크를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="828e4-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="828e4-173">Azure Resource Manager 템플릿의 액세스 및 보안</span><span class="sxs-lookup"><span data-stu-id="828e4-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
