---
title: "Azure에서 Linux Vm에 대 한 aaaCreate는 SSH 키 쌍 | Microsoft Docs"
description: "Azure Linux VM을 위한 SSH 공개 및 개인 키 쌍을 안전하게 만듭니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="1883f-103">Linux VM에 대한 SSH 공용 및 개인 키 쌍 만들기</span><span class="sxs-lookup"><span data-stu-id="1883f-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="1883f-104">이 문서 toogenerate SSH 프로토콜 버전 2 RSA 공개 및 개인 키 쌍 toouse Linux Vm이 포함 된 파일 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="1883f-105">SSH 키 쌍에서 암호 toolog hello 필요성을 제거 기본 인증을 위해 SSH 키 toousing Azure에서 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="1883f-106">암호 해독할 수 있으며 toorelentless 무단 시도 tooguess Vm에 암호를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="1883f-107">Azure 템플릿 또는 hello를 사용 하 여 만든 Vm `azure-cli` SSH에 대 한 로그인 암호를 사용 하지 않도록 설정의 게시물 배포 구성 단계를 제거 하는 hello 배포의 일부로 SSH 공개 키를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1883f-108">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="1883f-108">Quick Commands</span></span>

<span data-ttu-id="1883f-109">명령에서 Bash 셸의 다음, 사용자 고유의 선택 하 여 hello 예제 대체 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="1883f-110">SSH 공개 키 파일은 기본적으로 `~/.ssh/id_rsa.pub`에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="1883f-111">대화 상자가 나타나면 다음 명령을 hello를 사용 하 여 만들어야 "암호" toosecure 개인 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="1883f-112">(hello 암호는 암호 tooencrypt 사용자의 개인 키를 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1883f-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="1883f-113">새로 만든 hello 키 너무 추가`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="1883f-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="1883f-114">거의 모든 배포판의 Linux 운영 체제 명령 작업 위에 hello 하지만 반드시 작동 하는 컨테이너에서 hello 환경 근본적으로 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="1883f-115">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="1883f-115">Detailed Walkthrough</span></span>

<span data-ttu-id="1883f-116">SSH 공개 및 개인 키를 사용 하 여 hello tooyour Linux 서버에 가장 쉬운 방법은 toolog입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="1883f-117">[공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography) 무차별 암호 강제 훨씬 더 쉽게 수 있는 암호 보다는 훨씬 더 안전한 방식으로 toolog tooyour Linux에서에서 또는 Azure에서 VM BSD를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1883f-118">다른 사람과 공개 키를 공유할 수 있지만 사용자(또는 로컬 보안 인프라)만이 개인 키를 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="1883f-119">hello SSH 개인 키가 있어야 합니다는 [매우 안전한 방법이 암호](https://www.xkcd.com/936/) (소스:[xkcd.com](https://xkcd.com)) toosafeguard 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="1883f-120">이 암호는 정당한 tooaccess hello 개인 SSH 키 및 **않습니다** hello 사용자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="1883f-121">Hello 개인 키가 hello 암호 toodecrypt 무용지물이 있도록 128 비트 AES를 사용 하 여 hello 개인 키 암호화 암호 tooyour SSH 키를 추가 하면 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="1883f-122">공격자가 개인 키로 훔쳐 경우 및 키 암호 없는, 즉 개인 수 toouse 예상 되는 toolog hello 해당 공개 키를 가진 tooany 서버에서 키입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="1883f-123">개인 키가 암호로 보호된 경우 공격자가 사용할 수 없어 Azure에서 인프라에 대해 보안 계층을 추가로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="1883f-124">이 문서 SSH 프로토콜 버전 2 RSA 공용 및 개인 키 파일을 만든 hello 리소스 관리자에서 배포에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="1883f-125">*ssh rsa* hello에 키가 필요 [포털](https://portal.azure.com) 기본 및 리소스 관리자 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="1883f-126">SSH 키를 사용하여 SSH 암호 비활성화</span><span class="sxs-lookup"><span data-stu-id="1883f-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="1883f-127">Azure는 최소한 2048비트, ssh rsa 형식 공개 및 개인 키 서식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="1883f-128">toocreate hello 키를 사용 하 여 `ssh-keygen`, 일련의 질문을 요청 하 고 다음 개인 키와 일치 하는 공개 키를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="1883f-129">Hello 공개 키 너무 복사 하 고 Azure VM이 만들어지면`~/.ssh/authorized_keys`합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="1883f-130">SSH 키에 `~/.ssh/authorized_keys` 사용 되는 toochallenge hello 클라이언트 toomatch hello 해당 개인 키에 대 한 SSH 로그인 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="1883f-131">Azure Linux VM이 만들어지면 인증을 위해 SSH 키를 사용 하 여 Azure hello SSHD 구성 서버 toonot 로그인 암호, SSH 키만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="1883f-132">따라서 Azure Linux Vm의 경우 SSH 키를 만들면 보안 hello VM 배포에 도움이 되 고 직접 hello sshd_config config 파일에서 암호를 사용 하지 않도록 설정의 hello 일반적인 배포 후 구성 단계를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="1883f-133">ssh-keygen 사용</span><span class="sxs-lookup"><span data-stu-id="1883f-133">Using ssh-keygen</span></span>

<span data-ttu-id="1883f-134">이 명령은 SSH 키 쌍 (암호화 된) 2048 비트 RSA를 사용 하 여 보안 암호를 만들고이 주석 처리 tooeasily 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="1883f-135">SSH 키가 hello에 보관 하는 기본적으로 `~/.ssh` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="1883f-136">하지 않은 경우는 `~/.ssh` 디렉터리, hello `ssh-keygen` 명령 그 사용자를 위해 만드는 hello로 올바른 사용 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="1883f-137">*설명된 명령*</span><span class="sxs-lookup"><span data-stu-id="1883f-137">*Command explained*</span></span>

<span data-ttu-id="1883f-138">`ssh-keygen`= hello 사용 프로그램 toocreate hello 키</span><span class="sxs-lookup"><span data-stu-id="1883f-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="1883f-139">`-t rsa`hello RSA 형식인 키 toocreate 유형의 = [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="1883f-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="1883f-140">`-b 2048`hello 키의 비트</span><span class="sxs-lookup"><span data-stu-id="1883f-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="1883f-141">클래식 포털 및 X.509 인증서</span><span class="sxs-lookup"><span data-stu-id="1883f-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="1883f-142">사용 중인 경우 Azure hello [클래식 포털](https://manage.windowsazure.com/), hello SSH 키에 대 한 X.509 인증서를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="1883f-143">다른 형식의 SSH 공개 키는 허용되지 않으며 *X.509 인증서여야 합니다*.</span><span class="sxs-lookup"><span data-stu-id="1883f-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="1883f-144">toocreate 기존 SSH RSA 개인 키에서 된 X.509 인증서:</span><span class="sxs-lookup"><span data-stu-id="1883f-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="1883f-145">`asm`을 사용하여 클래식 배포</span><span class="sxs-lookup"><span data-stu-id="1883f-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="1883f-146">Hello 클래식을 사용 하는 경우 모델을 배포 (Azure 서비스 관리 CLI `asm`), SSH RSA 공개 키를 사용할 수 있습니다 또는 RFC4716 서식이 지정 된 키에 **.pem** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="1883f-147">hello SSH RSA 공개 키가 사용 하 여이 문서 앞부분에서 만들어진 `ssh-keygen`합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="1883f-148">RFC4716 toocreate 기존 SSH 공개 키에서 키 서식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="1883f-149">ssh-keygen 예제</span><span class="sxs-lookup"><span data-stu-id="1883f-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="1883f-150">저장된 키 파일:</span><span class="sxs-lookup"><span data-stu-id="1883f-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="1883f-151">이 문서에 대 한 hello 키 쌍 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-151">hello key pair name for this article.</span></span>  <span data-ttu-id="1883f-152">명명 된 키 쌍을 필요 **id_rsa** hello 기본 템플릿이 고 일부 도구는 hello 예상 **id_rsa** 개인 키 파일 이름을 있으므로 하나 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="1883f-153">hello 디렉터리 `~/.ssh/` hello SSH 키 쌍과 hello SSH 구성 파일 기본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="1883f-154">전체 경로 지정 되지 않은 경우 `ssh-keygen` hello 현재 작업 디렉터리의 hello 키 만들 되 면 기본 하지 hello `~/.ssh`합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="1883f-155">Hello 목록이 `~/.ssh` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="1883f-156">키 암호:</span><span class="sxs-lookup"><span data-stu-id="1883f-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="1883f-157">`ssh-keygen`"암호입니다."로 tooa 사용 되는 암호 tooencrypt hello 개인 키를 참조</span><span class="sxs-lookup"><span data-stu-id="1883f-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="1883f-158">*강력한* tooadd 암호 tooyour 키 쌍을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="1883f-159">암호 보호 hello 개인 키 없이 hello 키 파일에 있는 모든 사용자에서 사용할 수 toolog hello 해당 공개 키를 가진 tooany 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="1883f-160">Tooauthenticate를 사용 되는 시간 toochange hello 키 제공에 수 toogain 액세스 tooyour 개인 키 파일을 사용자가 경우에 더 나은 보호를 제공 암호를 추가 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="1883f-161">Ssh-에이전트 toostore 개인 키 암호를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1883f-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="1883f-162">사용자의 개인 키를 입력 하는 tooavoid 파일 암호 모든 SSH 로그인 사용 하면 `ssh-agent` toocache 개인 키 파일 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="1883f-163">Hello OSX 키 집합 호출할 때 안전 하 게 hello 개인 키 암호를 저장 하는 Mac을 사용 하는 경우 `ssh-agent`합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="1883f-164">확인 하 고 사용 하 여 `ssh-agent` 및 `ssh-add` tooinform hello hello 키 파일에 대 한 SSH 시스템을 hello 암호 toobe 대화형으로 사용 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="1883f-165">이제 너무 hello 개인 키를 추가할`ssh-agent` hello 명령을 사용 하 여 `ssh-add`합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="1883f-166">hello 개인 키 암호에 따라 저장 `ssh-agent`합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="1883f-167">사용 하 여 `ssh-copy-id` tooinstall hello에 대 한 새 키</span><span class="sxs-lookup"><span data-stu-id="1883f-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="1883f-168">VM을 이미 만든 경우 다음 명령을, hello VM 사용자 이름 및 hello 서버 주소를 원하는 값으로 교체 hello로 hello 새 SSH 공개 키 tooyour Linux VM을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="1883f-169">SSH 구성 파일 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="1883f-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="1883f-170">모범 사례 toocreate 이며 구성는 `~/.ssh/config` 로그인 할 경우 구성 파일 toospeed 및 SSH 클라이언트 동작을 최적화 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="1883f-171">다음 예제는 hello 표준 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="1883f-172">Hello 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="1883f-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="1883f-173">Hello 파일 tooadd hello 새 SSH 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="1883f-174">예제 `~/.ssh/config` 파일:</span><span class="sxs-lookup"><span data-stu-id="1883f-174">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="1883f-175">SSH 구성 하면 있습니다 섹션에 대 한 각 서버 tooenable 각 toohave 자체 전용된 키 쌍이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="1883f-176">기본 설정 hello (`Host *`) hello 특정 호스트에서 위쪽 hello 구성 파일에서 일치 하지 않는 모든 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="1883f-177">설명된 구성 파일</span><span class="sxs-lookup"><span data-stu-id="1883f-177">Config file explained</span></span>

<span data-ttu-id="1883f-178">`Host`= 터미널 hello에 호출 되는 hello 호스트의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="1883f-179">`ssh fedora22`지시 `SSH` 레이블이 지정 된 hello settings 블록에 toouse hello 값 `Host fedora22` 참고: 호스트 사용량에 대 한 논리는 모든 서버 hello 실제 호스트를 나타내지 않는 레이블과 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="1883f-180">`Hostname 102.160.203.241`= hello IP 주소 또는 액세스 하 고 hello 서버에 대 한 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="1883f-181">`User ahmet`toohello 서버에 로그인 할 때 hello 원격 사용자 계정 toouse를 = 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="1883f-182">`PubKeyAuthentication yes`= toouse SSH 키 toolog에서 원하는 SSH에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="1883f-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`hello SSH 개인 키와 인증을 위해 해당 공개 키 toouse =입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="1883f-184">암호 없이 Linux에 SSH</span><span class="sxs-lookup"><span data-stu-id="1883f-184">SSH into Linux without a password</span></span>

<span data-ttu-id="1883f-185">SSH 키 쌍과 구성 된 SSH config 파일을가지고 빠르고 안전 하 게 tooyour Linux VM의에서 수 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="1883f-186">처음에 로그인 할 때 SSH 키 hello 명령 프롬프트를 사용 하 여 tooa 서버 하면 해당 키 파일에 대 한 hello 암호에 대 한 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="1883f-187">설명된 명령</span><span class="sxs-lookup"><span data-stu-id="1883f-187">Command explained</span></span>

<span data-ttu-id="1883f-188">때 `ssh fedora22` 실행 SSH 먼저 찾아서 hello에서 모든 설정을 로드 `Host fedora22` 블록 및 모든 hello 남은 hello 마지막 블록에서에서 설정을 로드 `Host *`합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1883f-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1883f-189">Next Steps</span></span>

<span data-ttu-id="1883f-190">다음을 toocreate Azure Linux Vm의 경우 사용 하는 hello 새 SSH 공개 키.</span><span class="sxs-lookup"><span data-stu-id="1883f-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="1883f-191">Hello 로그인으로 SSH 공개 키를 사용 하 여 만든 azure Vm은 보안 hello 기본 로그인 방법, 암호를 사용 하 여 만든 Vm 보다 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="1883f-192">SSH 키를 사용하여 만든 Azure VM은 기본적으로 비활성화된 암호를 사용하여 구성되고 강제 무차별 암호 추측 시도를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="1883f-193">SSH 키 쌍 만들기에 도움이 필요 하거나 추가 인증서가 필요한 경우 다음을 참조 하세요 hello 클래식 포털에 사용할 구조의 등 [단계 toocreate SSH 키 쌍과 인증서 세부](create-ssh-keys-detailed.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1883f-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="1883f-194">Azure 템플릿을 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1883f-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1883f-195">Hello Azure 포털을 사용 하 여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1883f-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1883f-196">Hello Azure CLI를 사용 하 여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1883f-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
