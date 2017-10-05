---
title: "Azure에서 Linux VM에 사용자 추가 | Microsoft Docs"
description: "Azure에서 Linux VM에 사용자를 추가합니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: a95157f57c0cbd1f2a9ed68a0fe83140d7c9ec40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-user-to-an-azure-vm"></a><span data-ttu-id="0fca3-103">Azure VM에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="0fca3-103">Add a user to an Azure VM</span></span>
<span data-ttu-id="0fca3-104">새 Linux VM의 첫 번째 작업 중 하나가 새 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-104">One of the first tasks on any new Linux VM is to create a new user.</span></span>  <span data-ttu-id="0fca3-105">이 문서에서는 sudo 사용자 계정을 만들고, 암호를 설정하고, SSH 공개 키를 추가하고, `visudo` 를 사용하여 암호 없이 sudo를 허용하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-105">In this article, we walk through creating a sudo user account, setting the password, adding SSH Public Keys, and finally use `visudo` to allow sudo without a password.</span></span>

<span data-ttu-id="0fca3-106">필수 구성 요소는 [Azure 계정](https://azure.microsoft.com/pricing/free-trial/), [SSH 공개 및 개인 키](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Azure 리소스 그룹, 설치되고 `azure config mode arm`을 사용하여 Azure Resource Manager 모드로 전환된 Azure CLI입니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and the Azure CLI installed and switched to Azure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0fca3-107">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="0fca3-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy the SSH Public Key to the new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers to allow no password
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify the SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0fca3-108">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="0fca3-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="0fca3-109">소개</span><span class="sxs-lookup"><span data-stu-id="0fca3-109">Introduction</span></span>
<span data-ttu-id="0fca3-110">새 서버에서 수행되는 첫 번째 작업이자 가장 일반적인 작업 중 하나는 사용자 계정을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-110">One of the first and most common task with a new server is to add a user account.</span></span>  <span data-ttu-id="0fca3-111">루트 로그인은 비활성화되어야 하며, 루트 계정 자체도 사용해서는 안 됩니다. Linux 서버에서는 sudo만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-111">Root logins should be disabled and the root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="0fca3-112">sudo를 사용하여 사용자에게 루트 에스컬레이션 권한을 제공하는 것이 Linux를 관리하고 사용하는 적절한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-112">Giving a user root escalation privileges using sudo it the proper way to administer and use Linux.</span></span>

<span data-ttu-id="0fca3-113">명령 `useradd` 를 사용하여 Linux VM에 사용자 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-113">Using the command `useradd` we are adding user accounts to the Linux VM.</span></span>  <span data-ttu-id="0fca3-114">`useradd`를 실행하면 `/etc/passwd`, `/etc/shadow`, `/etc/group` 및 `/etc/gshadow`가 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="0fca3-115">명령줄 플래그를 `useradd` 명령에 추가하고 새 사용자를 Linux의 적절한 sudo 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-115">We are adding a command-line flag to the `useradd` command to also add the new user to the proper sudo group on Linux.</span></span>  <span data-ttu-id="0fca3-116">`useradd`는 `/etc/passwd`에 항목을 만들지만 새 사용자 계정에 암호를 제공하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give the new user account a password.</span></span>  <span data-ttu-id="0fca3-117">간단한 `passwd` 명령을 사용하여 새 사용자의 초기 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-117">We are creating an initial password for the new user using the simple `passwd` command.</span></span>  <span data-ttu-id="0fca3-118">마지막 단계에서는 사용자가 모든 명령에 암호를 입력할 필요 없이 sudo 권한으로 명령을 실행할 수 있도록 sudo 규칙을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-118">The last step is to modify the sudo rules to allow that user to execute commands with sudo privileges without having to enter a password for every command.</span></span>  <span data-ttu-id="0fca3-119">개인 키 쌍을 사용하여 로그인한 경우에는 사용자 계정이 부정 행위자로부터 안전한 것으로 가정하여 암호 없는 sudo 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-119">Logging in using the Private key we are assuming that user account is safe from bad actors and are going to allow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-to-an-azure-vm"></a><span data-ttu-id="0fca3-120">Azure VM에 단일 sudo 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="0fca3-120">Adding a single sudo user to an Azure VM</span></span>
<span data-ttu-id="0fca3-121">SSH 키를 사용하여 Azure VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-121">Log in to the Azure VM using SSH keys.</span></span>  <span data-ttu-id="0fca3-122">SSH 공개 키 액세스를 설정하지 않은 경우 먼저 [Azure에서 공개 키 인증 사용](http://link.to/article)문서를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="0fca3-123">`useradd` 명령은 다음 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-123">The `useradd` command completes the following tasks:</span></span>

* <span data-ttu-id="0fca3-124">새 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="0fca3-124">create a new user account</span></span>
* <span data-ttu-id="0fca3-125">이름이 같은 새 사용자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="0fca3-125">create a new user group with the same name</span></span>
* <span data-ttu-id="0fca3-126">`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="0fca3-126">add a blank entry to `/etc/passwd`</span></span>
* <span data-ttu-id="0fca3-127">`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="0fca3-127">add a blank entry to `/etc/gpasswd`</span></span>

<span data-ttu-id="0fca3-128">`-G` 명령줄 플래그는 적절한 Linux 그룹에 새 사용자 계정을 추가하여 새 사용자 계정에 루트 에스컬레이션 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-128">The `-G` command-line flag adds the new user account to the proper Linux group giving the new user account root escalation privileges.</span></span>

#### <a name="add-the-user"></a><span data-ttu-id="0fca3-129">사용자 추가</span><span class="sxs-lookup"><span data-stu-id="0fca3-129">Add the user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="0fca3-130">암호 설정</span><span class="sxs-lookup"><span data-stu-id="0fca3-130">Set a password</span></span>
<span data-ttu-id="0fca3-131">`useradd` 명령은 사용자를 만들고 `/etc/passwd` 및 `/etc/gpasswd`에 항목을 추가하지만 실제로 암호를 설정하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-131">The `useradd` command creates the user and adds an entry to both `/etc/passwd` and `/etc/gpasswd` but does not actually set the password.</span></span>  <span data-ttu-id="0fca3-132">이 암호는 `passwd` 명령을 사용하여 항목에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-132">The password is added to the entry using the `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="0fca3-133">서버에 sudo 권한이 있는 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-133">We now have a user with sudo privileges on the server.</span></span>

### <a name="add-your-ssh-public-key-to-the-new-user-account"></a><span data-ttu-id="0fca3-134">새 사용자 계정에 SSH 공개 키 추가</span><span class="sxs-lookup"><span data-stu-id="0fca3-134">Add your SSH Public Key to the new user account</span></span>
<span data-ttu-id="0fca3-135">컴퓨터에서 새 암호와 함께 `ssh-copy-id` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-135">From your machine, use the `ssh-copy-id` command with the new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-to-allow-sudo-usage-without-a-password"></a><span data-ttu-id="0fca3-136">visudo를 사용하여 암호 없이 sudo를 사용하도록 허용</span><span class="sxs-lookup"><span data-stu-id="0fca3-136">Using visudo to allow sudo usage without a password</span></span>
<span data-ttu-id="0fca3-137">`visudo`를 사용하여 `/etc/sudoers` 파일을 편집하면 중요한 이 파일이 잘못 수정되는 것을 방지하는 몇 개의 보호 계층이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-137">Using `visudo` to edit the `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="0fca3-138">`visudo`를 실행할 때 `/etc/sudoers` 파일은 편집 중에 다른 사용자가 변경할 수 없도록 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-138">Upon executing `visudo`, the `/etc/sudoers` file is locked to ensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="0fca3-139">또한 저장하거나 종료하려고 할 때 `visudo`에서 `/etc/sudoers` 파일에 대한 실수를 확인하므로 손상된 sudoers 파일을 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-139">The `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt to save or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="0fca3-140">이미 sudo 액세스를 위한 올바른 기본 그룹에 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-140">We already have users in the correct default group for sudo access.</span></span>  <span data-ttu-id="0fca3-141">이제 암호 없이 sudo를 사용할 수 있도록 이러한 그룹을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0fca3-141">Now we are going to enable those groups to use sudo with no password.</span></span>

```bash
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-the-user-ssh-keys-and-sudo"></a><span data-ttu-id="0fca3-142">사용자, ssh 키 및 sudo 확인</span><span class="sxs-lookup"><span data-stu-id="0fca3-142">Verify the user, ssh keys, and sudo</span></span>
```bash
# Verify the SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
