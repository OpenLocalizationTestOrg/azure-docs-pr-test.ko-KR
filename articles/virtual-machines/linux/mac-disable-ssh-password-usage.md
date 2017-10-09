---
title: "SSH 암호 SSHD를 구성 하 여 Linux VM에 aaaDisable | Microsoft Docs"
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
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="e04d9-103">SSHD를 구성하여 Linux VM에 SSH 암호 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="e04d9-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="e04d9-104">이 문서는 방법에 중점을 둡니다 toolock Linux VM의 로그인 보안을 hello 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="e04d9-105">SSH 포트 22 hello 열릴으로 toohello 세계 봇 toologin 암호를 추측 하 여 시도 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="e04d9-106">이 문서에서는 SSH를 통해 암호 로그인을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="e04d9-107">Hello 기능을 완전히 제거 하 여 toouse 암호 보호 hello Linux VM에서이 유형의 무차별 암호 대입 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="e04d9-108">hello 추가 보너스 tooonly 허용 Linux SSHD 구성가 SSH 공용 및 개인 키를 통해 로그인에는 지금까지 가장 안전한 방법은 toologin tooLinux hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="e04d9-109">가능한 조합을 hello tooguess hello 개인 키는 빚 이며 따라서 봇도 tootry toobrute force SSH 키를 신경에서 지원 되지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="e04d9-110">목표</span><span class="sxs-lookup"><span data-stu-id="e04d9-110">Goals</span></span>
* <span data-ttu-id="e04d9-111">SSHD toodisallow를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="e04d9-112">암호 로그인</span><span class="sxs-lookup"><span data-stu-id="e04d9-112">Password logins</span></span>
  * <span data-ttu-id="e04d9-113">루트 사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="e04d9-113">Root user login</span></span>
  * <span data-ttu-id="e04d9-114">시도-응답 인증</span><span class="sxs-lookup"><span data-stu-id="e04d9-114">Challenge-response authentication</span></span>
* <span data-ttu-id="e04d9-115">SSHD tooallow를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="e04d9-116">SSH 키 로그인만 해당</span><span class="sxs-lookup"><span data-stu-id="e04d9-116">only SSH key logins</span></span>
* <span data-ttu-id="e04d9-117">로그인 중에 SSHD 다시 시작</span><span class="sxs-lookup"><span data-stu-id="e04d9-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="e04d9-118">테스트 hello 새 SSHD 구성</span><span class="sxs-lookup"><span data-stu-id="e04d9-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="e04d9-119">소개</span><span class="sxs-lookup"><span data-stu-id="e04d9-119">Introduction</span></span>
[<span data-ttu-id="e04d9-120">정의된 SSH</span><span class="sxs-lookup"><span data-stu-id="e04d9-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="e04d9-121">SSHD는 hello hello Linux VM에서 실행 되는 SSH 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="e04d9-122">SSH는 MacBook 또는 Linux 워크스테이션의 셸에서 실행되는 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="e04d9-123">SSH는 hello toosecure 사용 되는 프로토콜과 워크스테이션 및 hello Linux VM 간의 hello 통신을 암호화 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="e04d9-124">이 문서 것이 매우 중요 한 tookeep 하나의 로그인 tooyour 전체 hello에 대 한 열기 Linux VM을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="e04d9-125">이러한 이유로 열립니다 두 터미널 및 SSH toohello Linux VM에서 둘 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="e04d9-126">Hello 첫 번째 터미널 toomake hello 변경 tooSSHDs 구성 파일을 사용 하 고 hello SSHD 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="e04d9-127">Hello 두 번째 터미널 tootest hello 서비스 다시 시작 되 면 변경 하는 것을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="e04d9-128">SSH 암호를 해제 하는 것 이므로 엄격 하 게 SSH 키, SSH 키에 잘못 된 하 고 hello 연결 toohello VM을 닫으면에 의존 hello VM 영구적으로 됩니다 잠기고 아무도 수 toologin tooit 삭제 하 고 다시 toobe 요구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e04d9-129">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e04d9-129">Prerequisites</span></span>
* [<span data-ttu-id="e04d9-130">Azure의 Linux VM용 Linux 및 Mac에서 SSH 키 만들기</span><span class="sxs-lookup"><span data-stu-id="e04d9-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="e04d9-131">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="e04d9-131">Azure account</span></span>
  * [<span data-ttu-id="e04d9-132">무료 평가판 등록</span><span class="sxs-lookup"><span data-stu-id="e04d9-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="e04d9-133">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="e04d9-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="e04d9-134">Azure에서 실행 중인 Linux VM</span><span class="sxs-lookup"><span data-stu-id="e04d9-134">Linux VM running on azure</span></span>
* <span data-ttu-id="e04d9-135">`~/.ssh/`에서 SSH 공용 및 개인 키 쌍</span><span class="sxs-lookup"><span data-stu-id="e04d9-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="e04d9-136">SSH 공개 키를 `~/.ssh/authorized_keys` hello Linux VM에</span><span class="sxs-lookup"><span data-stu-id="e04d9-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="e04d9-137">Hello VM에 대 한 Sudo 권한</span><span class="sxs-lookup"><span data-stu-id="e04d9-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="e04d9-138">열린 포트 22</span><span class="sxs-lookup"><span data-stu-id="e04d9-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="e04d9-139">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="e04d9-139">Quick Commands</span></span>
<span data-ttu-id="e04d9-140">*숙련 된 Linux 관리자에 게 hello TLDR 버전 원하는 여기에서 시작 합니다.  Hello를가 하는 다른 모든 사용자에 대 한 자세한 설명과 워크를 통해이 섹션을 건너뛰십시오.*</span><span class="sxs-lookup"><span data-stu-id="e04d9-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="e04d9-141">다음과 같이 hello 구성 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="e04d9-142">Hello SSHD 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-142">Restart hello SSHD service.</span></span> <span data-ttu-id="e04d9-143">Debian 기반 배포판에서:</span><span class="sxs-lookup"><span data-stu-id="e04d9-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="e04d9-144">Red Hat 기반 배포판에서:</span><span class="sxs-lookup"><span data-stu-id="e04d9-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="e04d9-145">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="e04d9-145">Detailed Walk Through</span></span>
<span data-ttu-id="e04d9-146">로그인 toohello Linux VM에 터미널 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="e04d9-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="e04d9-147">로그인 toohello Linux VM에 터미널 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="e04d9-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="e04d9-148">T 2에서 tooedit hello SSHD 구성 파일을 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="e04d9-149">여기에서 방금 hello 설정을 toodisable 암호를 편집 하 고 SSH 키 로그인을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="e04d9-150">연구 및 toomake Linux 및 필요에 따라 보안 SSH를 변경 해야이 파일의 여러 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="e04d9-151">암호 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="e04d9-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="e04d9-152">공개 키 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e04d9-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="e04d9-153">루트 로그인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="e04d9-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="e04d9-154">시도-응답 인증 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="e04d9-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="e04d9-155">SSHD 다시 시작</span><span class="sxs-lookup"><span data-stu-id="e04d9-155">Restart SSHD</span></span>
<span data-ttu-id="e04d9-156">Hello T1 셸에서 있는지 계속 로그인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="e04d9-157">암호를 이제 사용하지 않기 때문에 SSH 키가 올바르지 않은 경우 VM을 잠그지 않는 것이 중요합니다. </span><span class="sxs-lookup"><span data-stu-id="e04d9-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="e04d9-158">모든 설정을 사용할 수 있습니다 T1 toofix sshd_config 있습니다 여전히 기록 되 고 SSH 상태로 유지 합니다 hello 연결 hello SSHD 서비스 중 Linux VM에 올바르지 않은 경우 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="e04d9-159">T2에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="e04d9-160">Hello Debian 제품군에서</span><span class="sxs-lookup"><span data-stu-id="e04d9-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="e04d9-161">Hello RedHat 제품군에서</span><span class="sxs-lookup"><span data-stu-id="e04d9-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="e04d9-162">암호는 이제 무차별 암호 로그인 시도에서 VM을 보호하는 기능을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="e04d9-163">SSH 키만 허용 수 toologin 빠르고 훨씬 더 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e04d9-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

