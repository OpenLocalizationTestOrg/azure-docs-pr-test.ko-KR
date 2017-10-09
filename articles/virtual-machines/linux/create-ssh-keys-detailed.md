---
title: "Azure에서 Linux Vm에 대 한 aaaDetailed 단계 toocreate는 SSH 키 쌍 | Microsoft Docs"
description: "Azure에서 Linux Vm에 대 한 다른 사용 사례에 대 한 특정 인증서와 함께 추가 단계 toocreate SSH 공용 및 개인 키 쌍에 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="b940f-103">SSH 키 쌍 toocreate 및 Azure에서 Linux VM에 대 한 추가 인증서를 통해 자세한 워크</span><span class="sxs-lookup"><span data-stu-id="b940f-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="b940f-104">SSH 키 쌍에서 암호 toolog hello 필요성을 제거 기본 인증을 위해 SSH 키 toousing Azure에서 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="b940f-105">암호 해독할 수 있으며 toorelentless 무단 시도 tooguess Vm에 암호를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="b940f-106">Hello Azure CLI 또는 리소스 관리자 템플릿을 사용 하 여 만든 Vm SSH에 대 한 로그인 암호를 사용 하지 않도록 설정의 게시물 배포 구성 단계를 제거 하는 hello 배포의 일부로 SSH 공개 키를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="b940f-107">이 문서에서는 Linux 가상 컴퓨터에서 사용 등을 위한 자세한 단계 및 인증서 생성에 대한 추가 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="b940f-108">Tooquickly 하려는 경우 만들기 및 SSH 키 쌍을 사용 하 여, 참조 [toocreate SSH 공용 및 개인 키 쌍 Azure에서 Linux Vm에 대 한 연결 하는 방법을](mac-create-ssh-keys.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="b940f-109">SSH 키 이해</span><span class="sxs-lookup"><span data-stu-id="b940f-109">Understanding SSH keys</span></span>

<span data-ttu-id="b940f-110">SSH 공개 및 개인 키를 사용 하 여 hello tooyour Linux 서버에 가장 쉬운 방법은 toolog입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="b940f-111">[공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography) 무차별 암호 강제 훨씬 더 쉽게 수 있는 암호 보다는 훨씬 더 안전한 방식으로 toolog tooyour Linux에서에서 또는 Azure에서 VM BSD를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="b940f-112">다른 사람과 공개 키를 공유할 수 있지만 사용자(또는 로컬 보안 인프라)만이 개인 키를 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="b940f-113">hello SSH 개인 키가 있어야 합니다는 [매우 안전한 방법이 암호](https://www.xkcd.com/936/) (소스:[xkcd.com](https://xkcd.com)) toosafeguard 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="b940f-114">이 암호는 정당한 tooaccess hello 개인 SSH 키 파일 및 **않습니다** hello 사용자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="b940f-115">Hello 개인 키가 hello 암호 toodecrypt 무용지물이 있도록 128 비트 AES를 사용 하 여 hello 개인 키 암호화 암호 tooyour SSH 키를 추가 하면 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="b940f-116">공격자가 개인 키로 훔쳐 경우 및 키 암호 없는, 즉 개인 수 toouse 예상 되는 toolog hello 해당 공개 키를 가진 tooany 서버에서 키입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="b940f-117">개인 키가 암호로 보호된 경우 공격자가 사용할 수 없어 Azure에서 인프라에 대해 보안 계층을 추가로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="b940f-118">이 문서는 SSH 프로토콜 버전을 2 RSA 공개 및 개인 키 쌍 (또한 참조 tooas "ssh rsa" 키), Azure 리소스 관리자와 배포용으로 권장 되는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="b940f-119">*ssh rsa* hello에 키가 필요 [포털](https://portal.azure.com) 기본 및 리소스 관리자 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="b940f-120">SSH 키 용도 및 이점</span><span class="sxs-lookup"><span data-stu-id="b940f-120">SSH keys use and benefits</span></span>

<span data-ttu-id="b940f-121">Azure는 적어도 2048 비트를 필요한 SSH 프로토콜 버전 2 RSA 형식 공개 및 개인 키입니다. hello 공개 키 파일에 hello `.pub` 컨테이너 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="b940f-122">toocreate hello 키를 사용 하 여 `ssh-keygen`, 일련의 질문을 요청 하 고 다음 개인 키와 일치 하는 공개 키를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="b940f-123">Azure 복사본 공개 키 toohello hello Azure VM이 만들어지면 `~/.ssh/authorized_keys` hello VM의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="b940f-124">SSH 키에 `~/.ssh/authorized_keys` 사용 되는 toochallenge hello 클라이언트 toomatch hello 해당 개인 키에 대 한 SSH 로그인 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="b940f-125">Azure Linux VM이 만들어지면 인증을 위해 SSH 키를 사용 하 여 Azure hello SSHD 구성 서버 toonot 로그인 암호, SSH 키만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="b940f-126">따라서 Azure Linux Vm의 경우 SSH 키를 만들 수 있습니다 hello VM 배포를 보호 하 고 직접 hello에서 암호를 사용 하지 않도록 설정의 hello 일반적인 배포 후 구성 단계를 저장할 **sshd_config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="b940f-127">ssh-keygen 사용</span><span class="sxs-lookup"><span data-stu-id="b940f-127">Using ssh-keygen</span></span>

<span data-ttu-id="b940f-128">이 명령은 SSH 키 쌍 (암호화 된) 2048 비트 RSA를 사용 하 여 보안 암호를 만들고이 주석 처리 tooeasily 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="b940f-129">SSH 키가 hello에 보관 하는 기본적으로 `~/.ssh` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="b940f-130">하지 않은 경우는 `~/.ssh` 디렉터리, hello `ssh-keygen` 명령 그 사용자를 위해 만드는 hello로 올바른 사용 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="b940f-131">*설명된 명령*</span><span class="sxs-lookup"><span data-stu-id="b940f-131">*Command explained*</span></span>

<span data-ttu-id="b940f-132">`ssh-keygen`= hello 사용 프로그램 toocreate hello 키</span><span class="sxs-lookup"><span data-stu-id="b940f-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="b940f-133">`-t rsa`hello RSA 형식인 [wikipedia] 키 toocreate 유형의 =[끝에 괄호를](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` hello 키의 비트</span><span class="sxs-lookup"><span data-stu-id="b940f-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="b940f-134">`-C "azureuser@myserver"`= 식별 하는 추가 된 toohello hello 공개 키 파일 tooeasily 끝을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="b940f-135">일반적으로 전자 메일 hello 주석으로 사용 되지만 인프라에 대 한 가장 잘 작동 무엇이 든 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="b940f-136">`asm`을 사용하여 클래식 배포</span><span class="sxs-lookup"><span data-stu-id="b940f-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="b940f-137">Hello 클래식 배포 모델을 사용 하는 경우 (`asm` hello CLI에에서는 모드), SSH RSA 공개 키를 사용할 수 있습니다 또는 RFC4716 서식이 지정 된 pem 컨테이너의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="b940f-138">hello SSH RSA 공개 키가 사용 하 여이 문서 앞부분에서 만들어진 `ssh-keygen`합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="b940f-139">RFC4716 toocreate 기존 SSH 공개 키에서 키 서식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="b940f-140">ssh-keygen 예제</span><span class="sxs-lookup"><span data-stu-id="b940f-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
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

<span data-ttu-id="b940f-141">저장된 키 파일:</span><span class="sxs-lookup"><span data-stu-id="b940f-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="b940f-142">이 문서에 대 한 hello 키 쌍 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-142">hello key pair name for this article.</span></span>  <span data-ttu-id="b940f-143">명명 된 키 쌍을 필요 **id_rsa** hello 기본 템플릿이 고 일부 도구는 hello 예상 **id_rsa** 개인 키 파일 이름을 있으므로 하나 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="b940f-144">hello 디렉터리 `~/.ssh/` hello SSH 키 쌍과 hello SSH 구성 파일 기본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="b940f-145">전체 경로 지정 되지 않은 경우 `ssh-keygen` hello 현재 작업 디렉터리 hello 기본값이 아닌 hello 키를 만들고 `~/.ssh`합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="b940f-146">Hello 목록이 `~/.ssh` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="b940f-147">키 암호:</span><span class="sxs-lookup"><span data-stu-id="b940f-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="b940f-148">`ssh-keygen`"암호입니다."로 tooa 암호 hello 개인 키 파일에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="b940f-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="b940f-149">*강력한* tooadd 암호 tooyour 개인 키를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="b940f-150">암호 보호 hello 키 파일 없이 hello 파일에 있는 모든 사용자를 사용할 수 toolog hello 해당 공개 키를 가진 tooany 서버.</span><span class="sxs-lookup"><span data-stu-id="b940f-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="b940f-151">암호 (암호)를 추가 더 나은 보호 수 toogain 액세스 tooyour 개인 키 파일은 다른 사용자는 경우를 대비 하 고, 부여 받은 시간 toochange hello 키 사용 tooauthenticate 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="b940f-152">Ssh-에이전트 toostore 개인 키 암호를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b940f-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="b940f-153">tooavoid 모든 SSH 로그인 사용 하 여 개인 키 파일 암호를 입력 하는 데 `ssh-agent` toocache 개인 키 파일 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="b940f-154">Hello OSX 키 집합 호출할 때 안전 하 게 hello 개인 키 암호를 저장 하는 Mac을 사용 하는 경우 `ssh-agent`합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="b940f-155">확인 및 ssh-에이전트를 사용 하 고 ssh-추가 hello 키 파일에 대 한 tooinform hello SSH 시스템 되도록 hello 암호 toobe 대화형으로 사용 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="b940f-156">이제 너무 hello 개인 키를 추가할`ssh-agent` hello 명령을 사용 하 여 `ssh-add`합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="b940f-157">hello 개인 키 암호에 따라 저장 `ssh-agent`합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="b940f-158">사용 하 여 `ssh-copy-id` toocopy hello 키 tooan 기존 VM</span><span class="sxs-lookup"><span data-stu-id="b940f-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="b940f-159">VM을 이미 만든 경우에 hello 새 SSH 공개 키 tooyour Linux VM을 설치할 수 있습니다 사용:</span><span class="sxs-lookup"><span data-stu-id="b940f-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="b940f-160">SSH 구성 파일 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="b940f-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="b940f-161">권장된 모범 사례 toocreate 이며 구성는 `~/.ssh/config` 로그인 할 경우 구성 파일 toospeed 및 SSH 클라이언트 동작을 최적화 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="b940f-162">다음 예제는 hello 표준 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="b940f-163">Hello 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="b940f-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="b940f-164">Hello 파일 tooadd hello 새 SSH 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="b940f-165">예제 `~/.ssh/config` 파일:</span><span class="sxs-lookup"><span data-stu-id="b940f-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="b940f-166">SSH 구성 하면 있습니다 섹션에 대 한 각 서버 tooenable 각 toohave 자체 전용된 키 쌍이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="b940f-167">기본 설정 hello (`Host *`) hello 특정 호스트에서 위쪽 hello 구성 파일에서 일치 하지 않는 모든 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="b940f-168">설명된 구성 파일</span><span class="sxs-lookup"><span data-stu-id="b940f-168">Config file explained</span></span>

<span data-ttu-id="b940f-169">`Host`= 터미널 hello에 호출 되는 hello 호스트의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="b940f-170">`ssh fedora22`지시 `SSH` 레이블이 지정 된 hello settings 블록에 toouse hello 값 `Host fedora22` 참고: 호스트 사용량에 대 한 논리는 모든 서버 hello 실제 호스트를 나타내지 않는 레이블과 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="b940f-171">`Hostname 102.160.203.241`= hello IP 주소 또는 액세스 하 고 hello 서버에 대 한 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="b940f-172">`User ahmet`toohello 서버에 로그인 할 때 hello 원격 사용자 계정 toouse를 = 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="b940f-173">`PubKeyAuthentication yes`= toouse SSH 키 toolog에서 원하는 SSH에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="b940f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`hello SSH 개인 키와 인증을 위해 해당 공개 키 toouse =입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="b940f-175">암호 없이 Linux에 SSH</span><span class="sxs-lookup"><span data-stu-id="b940f-175">SSH into Linux without a password</span></span>

<span data-ttu-id="b940f-176">SSH 키 쌍과 구성 된 SSH config 파일을가지고 빠르고 안전 하 게 tooyour Linux VM의에서 수 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="b940f-177">처음에 로그인 할 때 SSH 키 hello 명령 프롬프트를 사용 하 여 tooa 서버 하면 해당 키 파일에 대 한 hello 암호에 대 한 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="b940f-178">설명된 명령</span><span class="sxs-lookup"><span data-stu-id="b940f-178">Command explained</span></span>

<span data-ttu-id="b940f-179">때 `ssh fedora22` 실행 SSH 먼저 찾아서 hello에서 모든 설정을 로드 `Host fedora22` 블록 및 모든 hello 남은 hello 마지막 블록에서에서 설정을 로드 `Host *`합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b940f-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b940f-180">Next Steps</span></span>

<span data-ttu-id="b940f-181">다음을 toocreate Azure Linux Vm의 경우 사용 하는 hello 새 SSH 공개 키.</span><span class="sxs-lookup"><span data-stu-id="b940f-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="b940f-182">Hello 로그인으로 SSH 공개 키를 사용 하 여 만든 azure Vm은 보안 hello 기본 로그인 방법, 암호를 사용 하 여 만든 Vm 보다 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="b940f-183">SSH 키를 사용하여 만든 Azure VM은 기본적으로 비활성화된 암호를 사용하여 구성되고 강제 무차별 암호 추측 시도를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b940f-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="b940f-184">Azure 템플릿을 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b940f-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b940f-185">Hello Azure 포털을 사용 하 여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b940f-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b940f-186">Hello Azure CLI를 사용 하 여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b940f-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
