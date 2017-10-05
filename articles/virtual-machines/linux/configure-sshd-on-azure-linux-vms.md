---
title: "Azure Linux Virtual Machines에서 SSHD 구성 | Microsoft Docs"
description: "보안 모범 사례에 대해 SSHD를 구성하여 Azure Linux Virtual Machines에 대한 SSH를 잠급니다."
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
ms.openlocfilehash: 0195c385b00ab92b2b92ce8ff00983a0d91bf3a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="5ab88-103">Azure Linux VM에서 SSHD 구성</span><span class="sxs-lookup"><span data-stu-id="5ab88-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="5ab88-104">이 문서에서는 암호 대신 SSH 키를 사용하여 Linux에서 SSH 서버를 잠그고 모범 사례 보안을 제공하며 SSH 로그인 프로세스를 가속화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="5ab88-105">추가로 SSHD를 잠그려면 루트 사용자를 로그인하는 작업에서 사용하지 않도록 설정하고 승인된 그룹 목록을 통해 로그인할 수 있는 사용자를 제한하게 되며 SSH 프로토콜 버전 1을 사용하지 않도록 설정하고 최소 키 비트를 설정하고 유휴 사용자의 자동 로그아웃을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="5ab88-106">이 문서에 대한 요구 사항은 Azure 계정([무료 평가판 가져오기](https://azure.microsoft.com/pricing/free-trial/)) 및 [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="5ab88-107">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="5ab88-107">Quick Commands</span></span>

<span data-ttu-id="5ab88-108">다음 설정을 사용하여 `/etc/ssh/sshd_config`을(를) 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-108">Configure `/etc/ssh/sshd_config` with the following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="5ab88-109">암호 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="5ab88-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a><span data-ttu-id="5ab88-110">루트 사용자가 로그인을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="5ab88-110">Disable login by the root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="5ab88-111">그룹 목록 허용</span><span class="sxs-lookup"><span data-stu-id="5ab88-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="5ab88-112">사용자 목록 허용</span><span class="sxs-lookup"><span data-stu-id="5ab88-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="5ab88-113">SSH 프로토콜 버전 1을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="5ab88-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="5ab88-114">최소 키 비트</span><span class="sxs-lookup"><span data-stu-id="5ab88-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="5ab88-115">유휴 사용자 연결 끊기</span><span class="sxs-lookup"><span data-stu-id="5ab88-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="5ab88-116">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="5ab88-116">Detailed Walkthrough</span></span>

<span data-ttu-id="5ab88-117">SSHD는 Linux VM에서 실행되는 SSH 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-117">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="5ab88-118">SSH는 MacBook의 셸, Linux 워크스테이션 또는 Windows의 Bash에서 실행되는 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="5ab88-119">또한 SSH는 워크스테이션과 Linux VM 간의 통신을 보호하고 암호화하는 데 사용되는 프로토콜이며 SSH를 VPN(사설 가상 네트워크)으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="5ab88-120">이 문서의 경우 전체 연습에 열려 있도록 Linux VM에 대한 로그인을 유지하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span></span>  <span data-ttu-id="5ab88-121">SSH 연결이 설정되면 창이 닫히지 않는 한 세션을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span></span>  <span data-ttu-id="5ab88-122">하나의 터미널에 로그인해 있다면 주요 변경 내용이 적용되는 경우 잠그지 않고 SSHD 서비스를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="5ab88-123">손상된 SSHD 구성을 사용하는 Linux VM이 잠긴 경우 Azure에서는 [Azure VM 액세스 확장](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 손상된 SSHD 구성을 다시 설정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5ab88-124">이러한 이유로 두 개의 터미널과 SSH을 양 쪽 모두에서 Linux VM에 대해 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="5ab88-125">첫 번째 터미널을 사용하여 SSHD 구성 파일을 변경하고 SSHD 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="5ab88-126">서비스가 다시 시작되면 두 번째 터미널을 사용하여 해당 변경 내용을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-126">We use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="5ab88-127">SSH 암호를 사용하지 않고 SSH 키에 엄격하게 의존하기 때문에 SSH가 올바르지 않고 VM에 대한 연결을 닫을 경우 VM은 영구적으로 잠기며 VM을 삭제하고 다시 요청하기 위해 아무도 로그인할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="5ab88-128">암호 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="5ab88-128">Disable password logins</span></span>

<span data-ttu-id="5ab88-129">Linux VM의 보안을 유지하는 가장 빠른 방법은 암호 로그인을 사용하지 않도록 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-129">The quickest way to secure you Linux VM is to disable password logins.</span></span>  <span data-ttu-id="5ab88-130">암호 로그인을 사용하는 경우 웹을 크롤링하는 보트는 즉시 SSH를 사용하여 Linux VM에 대한 암호를 무차별 암호 대입 추측하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span></span>  <span data-ttu-id="5ab88-131">암호 로그인을 완전히 사용하지 않도록 설정하면 SSH 서버가 모든 암호 로그인 시도를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a><span data-ttu-id="5ab88-132">루트 사용자가 로그인을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="5ab88-132">Disable login by the root user</span></span>

<span data-ttu-id="5ab88-133">Linux 모범 사례에 따르면 `root` 사용자는 SSH에 로그인되지 않고 `sudo su`를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="5ab88-134">루트 수준 사용 권한을 필요로 하는 모든 명령은 항상 `sudo` 명령을 통해 실행되어야 하며 여기서는 후속 감사에 대한 모든 작업을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="5ab88-135">`root` 사용자가 SSH를 통한 로그인을 사용하지 않도록 설정하는 작업은 권한이 있는 사용자만 SSH에 로그인하도록 허용하는 보안 모범 사례 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="5ab88-136">그룹 목록 허용</span><span class="sxs-lookup"><span data-stu-id="5ab88-136">Allowed groups list</span></span>

<span data-ttu-id="5ab88-137">SSH는 사용자 및 그룹에 SSH를 통한 로그인을 허용하거나 허용하지 않도록 제한하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="5ab88-138">이 기능은 목록을 사용하여 특정 사용자 및 그룹이 로그인하도록 승인하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-138">This feature uses lists to approve or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="5ab88-139">휠 그룹을 `AllowGroups` 목록으로 설정하면 SSH를 통해 승인된 휠 그룹에 있는 사용자 계정에 대한 로그인을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="5ab88-140">사용자 목록 허용</span><span class="sxs-lookup"><span data-stu-id="5ab88-140">Allowed users list</span></span>

<span data-ttu-id="5ab88-141">사용자에 대한 SSH 로그인을 제한하는 것은 `AllowGroups`인 동일한 태스크를 수행하는 보다 구체적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="5ab88-142">SSH 프로토콜 버전 1을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="5ab88-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="5ab88-143">SSH 프로토콜 버전 1은 안전하지 않고 비활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="5ab88-144">SSH 프로토콜 버전 2는 서버에 SSH하는 안전한 방법을 제공하는 현재 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span></span>  <span data-ttu-id="5ab88-145">SSH 버전 1을 사용하지 않도록 설정하면 SSH 버전 1을 사용하여 SSH 서버와의 연결을 설정하려고 시도하는 모든 SSH 클라이언트를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span></span>  <span data-ttu-id="5ab88-146">SSH 버전 2 연결을 통해서만 SSH 서버와의 연결이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="5ab88-147">최소 키 비트</span><span class="sxs-lookup"><span data-stu-id="5ab88-147">Minimum key bits</span></span>

<span data-ttu-id="5ab88-148">보안 모범 사례에 따라 암호 SSH 로그인을 사용하지 않도록 설정하고 SSH 서버에서 인증하는 데 SSH 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span></span>  <span data-ttu-id="5ab88-149">비트 단위로 측정된 길이가 다른 키를 사용하여 이러한 SSH 키를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="5ab88-150">모범 사례에 따르면 키 길이가 2048비트인 경우 허용 가능한 최소 키 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span></span>  <span data-ttu-id="5ab88-151">2048비트 미만의 키는 이론적으로 손상되었을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="5ab88-152">`ServerKeyBits`를 `2048`로 설정하면 2048비트 이상의 키를 사용하는 모든 연결을 허용하고 2048비트 미만의 연결을 거부하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="5ab88-153">유휴 사용자 연결 끊기</span><span class="sxs-lookup"><span data-stu-id="5ab88-153">Disconnect idle users</span></span>

<span data-ttu-id="5ab88-154">SSH에는 열린 연결이 설정 시간(초) 이상 유휴 상태로 유지되는 사용자 연결을 끊을 수 있는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="5ab88-155">활성화된 해당 사용자에게 열려 있는 세션을 유지하면 Linux VM의 노출을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="5ab88-156">SSHD 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5ab88-156">Restart SSHD</span></span>

<span data-ttu-id="5ab88-157">`/etc/ssh/sshd_config`에서 설정을 사용하려면 SSH 서버를 다시 시작하는 SSHD 프로세스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span></span>  <span data-ttu-id="5ab88-158">SSH 서버를 다시 시작하는 데 사용하는 터미널 창은 열린 SSH 세션을 손실하지 않고 열려 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span></span>  <span data-ttu-id="5ab88-159">새 SSH 서버 설정을 테스트하려면 두 번째 터미널 창 또는 탭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-159">To test the new SSH server settings use a second terminal window or tab.</span></span>  <span data-ttu-id="5ab88-160">SSH 연결을 테스트하기 위해 별도 터미널을 사용하면 SSHD 주요 변경 내용으로 잠그지 않고 뒤로 돌아가서 첫 번째 터미널에 있는 `/etc/ssh/sshd_config`을 추가로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-160">Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="5ab88-161">Redhat, Centos 및 Fedora에서</span><span class="sxs-lookup"><span data-stu-id="5ab88-161">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="5ab88-162">Debian 및 Ubuntu에서</span><span class="sxs-lookup"><span data-stu-id="5ab88-162">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="5ab88-163">Azure 재설정 액세스를 사용하여 SSHD 다시 설정</span><span class="sxs-lookup"><span data-stu-id="5ab88-163">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="5ab88-164">SSHD 구성에 주요 변경 내용이 잠겨진 경우 Azure VM 액세스 확장을 사용하여 SSHD 구성을 원래 구성으로 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-164">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span></span>

<span data-ttu-id="5ab88-165">모든 예제 이름을 고유한 설정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-165">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="5ab88-166">Fail2ban 설치</span><span class="sxs-lookup"><span data-stu-id="5ab88-166">Install Fail2ban</span></span>

<span data-ttu-id="5ab88-167">오픈 소스 앱 Fail2ban을 설치하고 설정하는 것이 가장 좋습니다. 그러면 무차별 암호 대입을 사용하여 SSH를 통해 Linux VM에 로그인하려는 반복적인 시도를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-167">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="5ab88-168">Fail2ban에서는 반복된 실패 시도를 기록하여 SSH를 통해 로그인한 다음 방화벽 규칙을 만들어서 시도가 시작된 IP 주소를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-168">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span></span>

* [<span data-ttu-id="5ab88-169">Fail2ban 홈페이지</span><span class="sxs-lookup"><span data-stu-id="5ab88-169">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="5ab88-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ab88-170">Next Steps</span></span>

<span data-ttu-id="5ab88-171">이제 Linux VM에서 SSH 서버를 구성하고 잠갔으므로 추가 보안 모범 사례를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ab88-171">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="5ab88-172">VMAccess 확장을 사용하여 사용자, SSH 관리 및 Azure Linux VM의 디스크 검사 또는 복구</span><span class="sxs-lookup"><span data-stu-id="5ab88-172">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="5ab88-173">Azure CLI를 사용하여 Linux VM에서 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="5ab88-173">Encrypt disks on a Linux VM using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="5ab88-174">Azure Resource Manager 템플릿의 액세스 및 보안</span><span class="sxs-lookup"><span data-stu-id="5ab88-174">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
