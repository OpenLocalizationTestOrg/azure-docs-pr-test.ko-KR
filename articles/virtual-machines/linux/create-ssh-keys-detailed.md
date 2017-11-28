---
title: "Azure에서 Linux VM용 SSH 키 쌍을 만드는 자세한 단계 | Microsoft Docs"
description: "다양한 사용 사례에 대한 특정 인증서와 함께 Azure에서 Linux VM용 SSH 공개 및 개인 키 쌍을 만드는 추가 단계에 대해 알아봅니다."
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
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="e3e6f-103">Azure에서 Linux VM용 SSH 키 쌍 및 추가 인증서를 만드는 자세한 연습</span><span class="sxs-lookup"><span data-stu-id="e3e6f-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="e3e6f-104">SSH 키 쌍을 사용하면 인증을 위해 기본적으로 SSH 키를 사용하는 Virtual Machines를 Azure에서 만들 수 있으며 로그인하기 위해 암호가 필요하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="e3e6f-105">암호는 추측할 수 있으며 철저한 무차별 암호 대입 시도로 인해 VM을 오픈하여 암호를 추측합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="e3e6f-106">Azure CLI 또는 Resource Manager 템플릿을 사용하여 만든 VM은 배포의 일부로 SSH 공개 키를 포함할 수 있으며 SSH에 대한 암호 로그인을 사용하지 않도록 설정하는 게시 배포 구성 단계를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="e3e6f-107">이 문서에서는 Linux 가상 컴퓨터에서 사용 등을 위한 자세한 단계 및 인증서 생성에 대한 추가 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="e3e6f-108">SSH 키 쌍을 신속하게 만들고 사용하려면 [Azure에서 Linux VM용 SSH 공개 및 개인 키 쌍을 만드는 방법](mac-create-ssh-keys.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="e3e6f-109">SSH 키 이해</span><span class="sxs-lookup"><span data-stu-id="e3e6f-109">Understanding SSH keys</span></span>

<span data-ttu-id="e3e6f-110">SSH 공개 키와 개인 키를 사용하는 것이 Linux 서버에 로그인하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="e3e6f-111">[공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography) 는 암호보다 더 안전하게 Azure의 Linux 또는 BSD VM에 로그인하는 방법을 제공하며 무차별 암호 대입을 훨씬 더 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="e3e6f-112">다른 사람과 공개 키를 공유할 수 있지만 사용자(또는 로컬 보안 인프라)만이 개인 키를 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="e3e6f-113">SSH 개인 키에는 해당 키를 보호할 [매우 안전한 암호](https://www.xkcd.com/936/)(출처: [xkcd.com](https://xkcd.com))가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="e3e6f-114">이 암호는 개인 SSH 키 파일에 액세스하기 위한 것으로 사용자 계정 암호가 **아닙니다**.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="e3e6f-115">SSH 키에 암호를 추가하면 128비트 AES를 사용하여 개인 키를 암호화하므로 암호가 없는 개인 키는 해독하는 데 쓸모가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="e3e6f-116">공격자가 개인 키를 훔치고 해당 키에 암호가 없는 경우 해당 개인 키를 사용하여 해당하는 공개 키가 있는 서버에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="e3e6f-117">개인 키가 암호로 보호된 경우 공격자가 사용할 수 없어 Azure에서 인프라에 대해 보안 계층을 추가로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="e3e6f-118">이 문서에서는 SSH 프로토콜 버전 2 RSA 공개 및 개인 키 파일 쌍("ssh-rsa" 키라고도 함)을 생성하며 이 쌍은 Azure Resource Manager로 배포하는 데 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="e3e6f-119">클래식 및 Resource Manager 배포를 위해 *ssh-rsa* 키가 [포털](https://portal.azure.com)에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="e3e6f-120">SSH 키 용도 및 이점</span><span class="sxs-lookup"><span data-stu-id="e3e6f-120">SSH keys use and benefits</span></span>

<span data-ttu-id="e3e6f-121">Azure에는 최소 2048비트, SSH 프로토콜 버전 2 RSA 형식 공개 및 개인 키가 필요하며 공개 키 파일은 `.pub` 컨테이너 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="e3e6f-122">키를 만들려면 일련의 사항을 질문한 다음 개인 키와 일치하는 공개 키를 작성하는 `ssh-keygen`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="e3e6f-123">Azure VM을 만드는 경우 Azure에서는 공개 키를 VM의 `~/.ssh/authorized_keys` 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="e3e6f-124">`~/.ssh/authorized_keys` 에서 SSH 키는 SSH 로그인 연결에 대한 해당 개인 키를 일치하도록 클라이언트의 문제를 해결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="e3e6f-125">인증을 위해 SSH 키를 사용하도록 Azure Linux VM이 만들어지면 Azure는 SSH 키만 허용하고 암호 로그인은 허용하지 않도록 SSHD 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="e3e6f-126">따라서 SSH 키를 사용하여 Azure Linux VM을 만들면 VM 배포 보안을 유지하고 **sshd_config** 파일에서 암호를 사용하지 않도록 설정하는 일반 사후 배포 구성 단계를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="e3e6f-127">ssh-keygen 사용</span><span class="sxs-lookup"><span data-stu-id="e3e6f-127">Using ssh-keygen</span></span>

<span data-ttu-id="e3e6f-128">이 명령은 2048비트 RSA를 사용하여 암호 보안된(암호화된) SSH 키 쌍을 만들고 쉽게 식별할 수 있도록 주석 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="e3e6f-129">SSH 키는 기본적으로 `~/.ssh` 디렉터리에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="e3e6f-130">`~/.ssh` 디렉터리가 없는 경우 적절한 권한이 있는 사용자가 `ssh-keygen` 명령으로 해당 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="e3e6f-131">*설명된 명령*</span><span class="sxs-lookup"><span data-stu-id="e3e6f-131">*Command explained*</span></span>

<span data-ttu-id="e3e6f-132">`ssh-keygen` = 키를 만드는 데 사용한 프로그램</span><span class="sxs-lookup"><span data-stu-id="e3e6f-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="e3e6f-133">`-t rsa` = RSA 형식을 만드는 키 유형[wikipedia][끝에 괄호](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = 키의 비트</span><span class="sxs-lookup"><span data-stu-id="e3e6f-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="e3e6f-134">`-C "azureuser@myserver"` = 쉽게 식별할 수 있도록 공개 키 파일의 끝에 추가된 주석</span><span class="sxs-lookup"><span data-stu-id="e3e6f-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="e3e6f-135">일반적으로 전자 메일은 주석으로 사용되지만 인프라에 가장 적합한 것을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="e3e6f-136">`asm`을 사용하여 클래식 배포</span><span class="sxs-lookup"><span data-stu-id="e3e6f-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="e3e6f-137">클래식 배포 모델(CLI에서 `asm` 모드)을 사용하는 경우 pem 컨테이너에서 SSH-RSA 공개 키 또는 RFC4716 형식 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="e3e6f-138">SSH-RSA 공개 키는 이 문서의 앞부분에서 `ssh-keygen`을 사용하여 작성한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="e3e6f-139">기존 SSH 공개 키에서 RFC4716 형식 키를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="e3e6f-140">ssh-keygen 예제</span><span class="sxs-lookup"><span data-stu-id="e3e6f-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
The keys randomart image is:
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

<span data-ttu-id="e3e6f-141">저장된 키 파일:</span><span class="sxs-lookup"><span data-stu-id="e3e6f-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="e3e6f-142">이 문서에 대한 키 쌍 이름.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-142">The key pair name for this article.</span></span>  <span data-ttu-id="e3e6f-143">**id_rsa**라는 키 쌍을 기본값으로 가지고 일부 도구는 **id_rsa** 개인 키 파일 이름을 예상하므로 하나 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="e3e6f-144">디렉터리 `~/.ssh/` 은 SSH 키 쌍 및 SSH 구성 파일에 대한 기본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="e3e6f-145">전체 경로를 지정하지 않으면 `ssh-keygen`에서 `~/.ssh` 기본 디렉터리가 아니라 현재 작업 디렉터리에 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="e3e6f-146">`~/.ssh` 디렉터리의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="e3e6f-147">키 암호:</span><span class="sxs-lookup"><span data-stu-id="e3e6f-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="e3e6f-148">`ssh-keygen`은 개인 키 파일에 대한 암호를 "암호(passphrase)"로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="e3e6f-149">개인 키에 암호를 추가하는 것이 *가장* 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="e3e6f-150">키 파일을 보호하는 암호가 없는 경우, 누구나 해당 공개 키가 있는 서버에 로그인하는 데 키 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="e3e6f-151">암호(password 및 passphrase)를 추가하면 보호 기능을 제공합니다. 이 경우에 개인 키 파일에 대한 액세스 권한을 얻을 수 있으며 인증하는 데 사용한 키를 변경할 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="e3e6f-152">ssh 에이전트를 사용하여 개인 키 암호 저장</span><span class="sxs-lookup"><span data-stu-id="e3e6f-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="e3e6f-153">모든 SSH 로그인으로 개인 키 파일 암호를 입력하지 않으려면 `ssh-agent` 을 사용하여 개인 키 파일 암호를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="e3e6f-154">Mac을 사용하는 경우 `ssh-agent`를 호출할 때 OSX 키 집합은 개인 키 암호를 안전하게 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="e3e6f-155">ssh-agent와 ssh-add를 확인하고 사용하여 전달 구를 대화형으로 사용할 필요가 없도록 SSH 시스템에 키 파일을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="e3e6f-156">이제 `ssh-add` 명령을 사용하여 개인 키를 `ssh-agent`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="e3e6f-157">개인 키 암호는 이제 `ssh-agent`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="e3e6f-158">키를 기존 VM에 복사하는 데 `ssh-copy-id` 사용</span><span class="sxs-lookup"><span data-stu-id="e3e6f-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="e3e6f-159">VM을 이미 만든 경우 다음을 사용하여 Linux VM에 새 SSH 공개 키를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="e3e6f-160">SSH 구성 파일 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="e3e6f-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="e3e6f-161">SSH 클라이언트 동작을 최적화하기 위해 `~/.ssh/config` 파일을 만들고 구성하여 로그인 속도를 높이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="e3e6f-162">다음 예제에서는 표준 구성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="e3e6f-163">파일 만들기</span><span class="sxs-lookup"><span data-stu-id="e3e6f-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="e3e6f-164">파일을 편집하여 새 SSH 구성 추가</span><span class="sxs-lookup"><span data-stu-id="e3e6f-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="e3e6f-165">예제 `~/.ssh/config` 파일:</span><span class="sxs-lookup"><span data-stu-id="e3e6f-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="e3e6f-166">이 SSH 구성은 각 서버에 대한 섹션을 제공하여 자체 전용 키 쌍을 각각 보유하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="e3e6f-167">상위 구성 파일에서 특정 호스트와 일치하지 않는 호스트에 대한 기본 설정(`Host *`)입니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="e3e6f-168">설명된 구성 파일</span><span class="sxs-lookup"><span data-stu-id="e3e6f-168">Config file explained</span></span>

<span data-ttu-id="e3e6f-169">`Host` = 터미널에서 호출되는 호스트의 이름.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="e3e6f-170">`ssh fedora22`는 레이블이 `Host fedora22`로 지정된 설정 블록에서 값을 사용하도록 `SSH`에 지시합니다. 참고: 호스트는 사용하기 위한 논리적인 레이블일 수 있고 어떤 서버의 실제 호스트 이름을 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="e3e6f-171">`Hostname 102.160.203.241` = 액세스된 서버에 대한 IP 주소 또는 DNS 이름.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="e3e6f-172">`User ahmet` = 서버에 로그인할 때 사용할 원격 사용자 계정.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="e3e6f-173">`PubKeyAuthentication yes` = SSH가 로그인에 SSH 키를 사용하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="e3e6f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = 인증을 위해 사용할 SSH 개인 키와 해당 공개 키.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="e3e6f-175">암호 없이 Linux에 SSH</span><span class="sxs-lookup"><span data-stu-id="e3e6f-175">SSH into Linux without a password</span></span>

<span data-ttu-id="e3e6f-176">SSH 키 쌍 및 구성된 SSH 구성 파일이 있으므로 빠르고 안전하게 Linux VM에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="e3e6f-177">처음으로 SSH 키를 사용하는 서버에 로그인하면 명령은 해당 키 파일을 입력하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="e3e6f-178">설명된 명령</span><span class="sxs-lookup"><span data-stu-id="e3e6f-178">Command explained</span></span>

<span data-ttu-id="e3e6f-179">`ssh fedora22`이 SSH를 실행하는 경우 `Host fedora22` 블록에서 설정을 배치하고 로드한 다음 마지막 블록 `Host *`의 나머지 모든 설정을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3e6f-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3e6f-180">Next Steps</span></span>

<span data-ttu-id="e3e6f-181">다음으로 새 SSH 공개 키를 사용하여 Azure Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="e3e6f-182">기본 로그인 메서드 암호를 사용하여 만든 VM보다 SSH 공개 키를 로그인으로 사용하여 만든 Azure VM의 보안이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="e3e6f-183">SSH 키를 사용하여 만든 Azure VM은 기본적으로 비활성화된 암호를 사용하여 구성되고 강제 무차별 암호 추측 시도를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="e3e6f-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="e3e6f-184">Azure 템플릿을 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e3e6f-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e3e6f-185">Azure Portal을 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e3e6f-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e3e6f-186">Azure CLI를 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e3e6f-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
