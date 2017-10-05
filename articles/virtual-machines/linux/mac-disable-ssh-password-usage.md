---
title: "SSHD를 구성하여 Linux VM에 SSH 암호 사용 안 함 | Microsoft Docs"
description: "SSH에 암호 로그인을 사용하지 않도록 설정하여 Azure에서 Linux VM을 보호합니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: dc45a1cdce29cef061acc5c7e5b15d9d89265cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="fbf58-103">SSHD를 구성하여 Linux VM에 SSH 암호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="fbf58-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="fbf58-104">이 문서는 Linux VM의 로그인 보안을 잠그는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-104">This article focuses on how to lock down the login security of your Linux VM.</span></span>  <span data-ttu-id="fbf58-105">SSH 포트 22가 World Bot에 열리는 즉시 암호를 추측하여 로그인하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-105">As soon as the SSH port 22 is opened to the world bots start trying to login by guessing passwords.</span></span>  <span data-ttu-id="fbf58-106">이 문서에서는 SSH를 통해 암호 로그인을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="fbf58-107">암호를 사용하는 기능을 완전히 제거하여 이러한 유형의 무차별 암호 대입 공격으로부터 Linux VM를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-107">By completely removing the ability to use passwords we protect the Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="fbf58-108">추가된 사항은 Linux SSHD를 구성하여 Linux에 로그인하는 가장 안전한 방법인 SSH 공용 및 개인 키를 통해 로그인을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-108">The added bonus is we will configure Linux SSHD to only allow logins via SSH public & private keys, by far the most secure way to login to Linux.</span></span>  <span data-ttu-id="fbf58-109">가능한 조합은 개인 키가 매우 크고 따라서 무차별 암호 대입 SSH 키를 사용해 보기 위해 신경 쓸 필요 없이 Bot을 권장하지 않는다고 추측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-109">The possible combinations of it would require to guess the private key is immense and therefore discourages bots from even bothering to try to brute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="fbf58-110">목표</span><span class="sxs-lookup"><span data-stu-id="fbf58-110">Goals</span></span>
* <span data-ttu-id="fbf58-111">허용되지 않는 SSHD 구성:</span><span class="sxs-lookup"><span data-stu-id="fbf58-111">Configure SSHD to disallow:</span></span>
  * <span data-ttu-id="fbf58-112">암호 로그인</span><span class="sxs-lookup"><span data-stu-id="fbf58-112">Password logins</span></span>
  * <span data-ttu-id="fbf58-113">루트 사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="fbf58-113">Root user login</span></span>
  * <span data-ttu-id="fbf58-114">시도-응답 인증</span><span class="sxs-lookup"><span data-stu-id="fbf58-114">Challenge-response authentication</span></span>
* <span data-ttu-id="fbf58-115">허용되는 SSHD 구성:</span><span class="sxs-lookup"><span data-stu-id="fbf58-115">Configure SSHD to allow:</span></span>
  * <span data-ttu-id="fbf58-116">SSH 키 로그인만 해당</span><span class="sxs-lookup"><span data-stu-id="fbf58-116">only SSH key logins</span></span>
* <span data-ttu-id="fbf58-117">로그인 중에 SSHD 다시 시작</span><span class="sxs-lookup"><span data-stu-id="fbf58-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="fbf58-118">새 SSHD 구성 테스트</span><span class="sxs-lookup"><span data-stu-id="fbf58-118">Test the new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="fbf58-119">소개</span><span class="sxs-lookup"><span data-stu-id="fbf58-119">Introduction</span></span>
[<span data-ttu-id="fbf58-120">정의된 SSH</span><span class="sxs-lookup"><span data-stu-id="fbf58-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="fbf58-121">SSHD는 Linux VM에서 실행되는 SSH 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-121">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="fbf58-122">SSH는 MacBook 또는 Linux 워크스테이션의 셸에서 실행되는 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="fbf58-123">또한 SSH는 워크스테이션과 Linux VM 간의 통신을 보호하고 암호화하는 데 사용되는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-123">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM.</span></span>

<span data-ttu-id="fbf58-124">이 문서의 경우 전체 연습에 열려 있도록 Linux VM에 대한 로그인을 유지하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-124">For this article it is very important to keep one login to your Linux VM open for the entire walk through.</span></span>  <span data-ttu-id="fbf58-125">이러한 이유로 두 개의 터미널과 SSH을 양 쪽 모두에서 Linux VM에 대해 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-125">For this reason we will open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="fbf58-126">첫 번째 터미널을 사용하여 SSHD 구성 파일을 변경하고 SSHD 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-126">We will use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="fbf58-127">서비스가 다시 시작되면 두 번째 터미널을 사용하여 해당 변경 내용을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-127">We will use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="fbf58-128">SSH 암호를 사용하지 않고 SSH 키에 엄격하게 의존하기 때문에 SSH가 올바르지 않고 VM에 대한 연결을 닫을 경우 VM은 영구적으로 잠기며 VM을 삭제하고 다시 요청하기 위해 아무도 로그인할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbf58-129">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fbf58-129">Prerequisites</span></span>
* [<span data-ttu-id="fbf58-130">Azure의 Linux VM용 Linux 및 Mac에서 SSH 키 만들기</span><span class="sxs-lookup"><span data-stu-id="fbf58-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="fbf58-131">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="fbf58-131">Azure account</span></span>
  * [<span data-ttu-id="fbf58-132">무료 평가판 등록</span><span class="sxs-lookup"><span data-stu-id="fbf58-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="fbf58-133">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fbf58-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="fbf58-134">Azure에서 실행 중인 Linux VM</span><span class="sxs-lookup"><span data-stu-id="fbf58-134">Linux VM running on azure</span></span>
* <span data-ttu-id="fbf58-135">`~/.ssh/`에서 SSH 공용 및 개인 키 쌍</span><span class="sxs-lookup"><span data-stu-id="fbf58-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="fbf58-136">Linux VM의 `~/.ssh/authorized_keys`에서 SSH 공개 키</span><span class="sxs-lookup"><span data-stu-id="fbf58-136">SSH public key in `~/.ssh/authorized_keys` on the Linux VM</span></span>
* <span data-ttu-id="fbf58-137">VM의 Sudo 권한</span><span class="sxs-lookup"><span data-stu-id="fbf58-137">Sudo rights on the VM</span></span>
* <span data-ttu-id="fbf58-138">열린 포트 22</span><span class="sxs-lookup"><span data-stu-id="fbf58-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="fbf58-139">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="fbf58-139">Quick Commands</span></span>
<span data-ttu-id="fbf58-140">*TLDR 버전이 필요한 숙련된 Linux 관리자는 여기서부터 시작합니다.  자세한 설명과 연습이 필요한 다른 사용자는 이 섹션을 건너뜁니다.*</span><span class="sxs-lookup"><span data-stu-id="fbf58-140">*Seasoned Linux Admins who just want the TLDR version start here.  For everyone else that wants the detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="fbf58-141">다음과 같이 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-141">Edit the config file as follows:</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

<span data-ttu-id="fbf58-142">SSHD 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-142">Restart the SSHD service.</span></span> <span data-ttu-id="fbf58-143">Debian 기반 배포판에서:</span><span class="sxs-lookup"><span data-stu-id="fbf58-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="fbf58-144">Red Hat 기반 배포판에서:</span><span class="sxs-lookup"><span data-stu-id="fbf58-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="fbf58-145">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="fbf58-145">Detailed Walk Through</span></span>
<span data-ttu-id="fbf58-146">터미널 1(T1)에서 Linux VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-146">Login to the Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="fbf58-147">터미널 2(T2)에서 Linux VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-147">Login to the Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="fbf58-148">T2에서 SSHD 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-148">On T2 we are going to edit the SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="fbf58-149">여기에서부터 암호를 사용하지 않고 SSH 키 로그인을 사용하도록 설정을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-149">From here we will edit just the settings to disable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="fbf58-150">Linux 및 SSH을 필요한 만큼으로 안전하게 만들기 위해 조사하고 변경해야 하는 이 파일에는 많은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-150">There are many settings in this file that you should research and change to make Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="fbf58-151">암호 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="fbf58-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="fbf58-152">공개 키 인증 사용</span><span class="sxs-lookup"><span data-stu-id="fbf58-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="fbf58-153">루트 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="fbf58-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="fbf58-154">시도-응답 인증 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="fbf58-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="fbf58-155">SSHD 다시 시작</span><span class="sxs-lookup"><span data-stu-id="fbf58-155">Restart SSHD</span></span>
<span data-ttu-id="fbf58-156">T1 셸에서 계속 로그인되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-156">From the T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="fbf58-157">암호를 이제 사용하지 않기 때문에 SSH 키가 올바르지 않은 경우 VM을 잠그지 않는 것이 중요합니다. </span><span class="sxs-lookup"><span data-stu-id="fbf58-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="fbf58-158">Linux VM에서 설정이 올바르지 않은 경우 여전히 로그인한 상태이며 SSHD 서비스가 다시 시작하는 동안 SSH가 연결되어 있으므로 T1을 사용하여 sshd_config를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-158">If any setting are incorrect on your Linux VM you can use T1 to fix sshd_config as you will still be logged in and SSH will keep the connection alive during the SSHD service restart.</span></span>

<span data-ttu-id="fbf58-159">T2에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-159">From T2 run:</span></span>

##### <a name="on-the-debian-family"></a><span data-ttu-id="fbf58-160">Debian 제품군에서</span><span class="sxs-lookup"><span data-stu-id="fbf58-160">On the Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a><span data-ttu-id="fbf58-161">RedHat 제품군에서</span><span class="sxs-lookup"><span data-stu-id="fbf58-161">On the RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="fbf58-162">암호는 이제 무차별 암호 로그인 시도에서 VM을 보호하는 기능을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="fbf58-163">SSH로 키를 사용하면 훨씬 더 신속하고 안전하게 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbf58-163">With only SSH Keys allowed you will be able to login faster and much more secure.</span></span>

