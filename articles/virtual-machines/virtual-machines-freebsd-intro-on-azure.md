---
title: "Azure에서 aaaIntroduction tooFreeBSD | Microsoft Docs"
description: "Azure에서 FreeBSD 가상 컴퓨터를 사용하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="26d17-103">Azure에서 tooFreeBSD 소개</span><span class="sxs-lookup"><span data-stu-id="26d17-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="26d17-104">이 항목에서는 Azure에서 FreeBSD 가상 컴퓨터를 실행하는 방법의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="26d17-105">개요</span><span class="sxs-lookup"><span data-stu-id="26d17-105">Overview</span></span>
<span data-ttu-id="26d17-106">Microsoft Azure에 대 한 FreeBSD toopower 최신 서버, 데스크톱 및 포함 된 플랫폼을 사용 하는 고급 컴퓨터 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="26d17-107">Microsoft Corporation은 FreeBSD의 이미지에서 사용할 수 있도록 Azure hello로 [Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="26d17-108">현재 hello 다음 FreeBSD 버전에서 제공 하는 이미지와 Microsoft:</span><span class="sxs-lookup"><span data-stu-id="26d17-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="26d17-109">FreeBSD 10.3 릴리스</span><span class="sxs-lookup"><span data-stu-id="26d17-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="26d17-110">FreeBSD 11.0 릴리스</span><span class="sxs-lookup"><span data-stu-id="26d17-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="26d17-111">hello 에이전트가 hello FreeBSD VM 간의 통신을 담당 하 고 프로 비전 하는 등의 작업에 대 한 Azure 패브릭이 hello 처음 사용할 (사용자 이름, 암호 또는 SSH 키, 호스트 이름, 등) 및 선택적 VM 확장에 사용할 수 있도록 기능에 대해 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="26d17-112">FreeBSD의 이후 버전의 경우와 hello 전략은 현재 toostay 고 hello 최신 릴리스에 사용할 수 있도록 hello FreeBSD 릴리스 엔지니어링 팀에서 게시 한 후에 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="26d17-113">FreeBSD 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="26d17-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="26d17-114">FreeBSD 가상 컴퓨터를 배포할은 hello Azure 포털에서에서 Azure 마켓플레이스 hello에서 이미지를 사용 하 여 간단한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="26d17-115">Azure 마켓플레이스 hello에 FreeBSD 10.3</span><span class="sxs-lookup"><span data-stu-id="26d17-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="26d17-116">Azure 마켓플레이스 hello에 FreeBSD 11.0</span><span class="sxs-lookup"><span data-stu-id="26d17-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="26d17-117">FreeBSD에서 Azure CLI 2.0을 통해 FreeBSD VM 만들기</span><span class="sxs-lookup"><span data-stu-id="26d17-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="26d17-118">Tooinstall 먼저 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) FreeBSD 컴퓨터에서 다음 명령을 있지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="26d17-119">Bash FreeBSD 컴퓨터에 설치 되지 않은 경우 다음 hello 설치 하기 전에 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="26d17-120">Python FreeBSD 컴퓨터에 설치 되지 않은 경우 다음 hello 설치 하기 전에 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="26d17-121">Hello 설치 하는 동안 요청 `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="26d17-122">업그레이드 하도록 `y` 입력 `/etc/rc.conf` 으로 `a path tooan rc file tooupdate`, hello 문제를 충족할 수 `ERROR: [Errno 13] Permission denied`합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="26d17-123">tooresolve이이 문제를 hello 쓰기 오른쪽 toocurrent 사용자 hello 파일에 대해 부여 하면 `etc/rc.conf`합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="26d17-124">이제 Azure에 로그인한 후 FreeBSD VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="26d17-125">다음 예에서는 toocreate FreeBSD 11.0 VM은입니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="26d17-126">Hello 매개 변수를 추가할 수도 있습니다 `--public-ip-address-dns-name` 새로 생성된 된 공용 IP에 대 한 전역적으로 고유 DNS 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="26d17-127">그런 다음 배포 위의 hello 출력으로 인쇄 하는 hello ip 주소를 통해 tooyour FreeBSD VM에에서 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="26d17-128">FreeBSD에 대한 VM 확장</span><span class="sxs-lookup"><span data-stu-id="26d17-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="26d17-129">FreeBSD에서 지원되는 VM 확장은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="26d17-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="26d17-130">VMAccess</span></span>
<span data-ttu-id="26d17-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) 확장 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="26d17-132">Hello 원래 sudo 사용자의 hello 암호 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="26d17-133">새 사용자를 sudo hello 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="26d17-134">지정 된 hello 키로 hello 공개 호스트 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="26d17-135">VM hello 호스트 키를 제공 하지 않으면 프로 비전 중에 제공 된 hello 공개 호스트 키를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="26d17-136">Hello SSH 포트 (22)를 열고 reset_ssh tootrue 설정 된 경우 hello sshd_config를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="26d17-137">Hello 기존 사용자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-137">Remove hello existing user.</span></span>
* <span data-ttu-id="26d17-138">디스크를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-138">Check disks.</span></span>
* <span data-ttu-id="26d17-139">추가된 디스크를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="26d17-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="26d17-140">CustomScript</span></span>
<span data-ttu-id="26d17-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) 확장 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="26d17-142">제공 된 경우 Azure 저장소 서비스 또는 외부 공용 저장소 (예를 들어 GitHub)에서 사용자 지정 하는 hello 스크립트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="26d17-143">Hello 항목 지점 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-143">Run hello entry point script.</span></span>
* <span data-ttu-id="26d17-144">인라인 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-144">Support inline commands.</span></span>
* <span data-ttu-id="26d17-145">셸 및 Python 스크립트에서 Windows 스타일 줄 바꿈 문자를 자동으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="26d17-146">셸 및 Python 스크립트의 BOM을 자동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="26d17-147">CommandToExecute의 중요 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="26d17-148">FreeBSD VM은 현재 CustomScript 버전 1.x만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="26d17-149">인증: 사용자 이름, 암호 및 SSH 키</span><span class="sxs-lookup"><span data-stu-id="26d17-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="26d17-150">Hello Azure 포털을 사용 하 여 FreeBSD 가상 컴퓨터를 만들 때 사용자 이름, 암호 또는 SSH 공개 키를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="26d17-151">Azure에서 FreeBSD 가상 컴퓨터를 배포 하기 위한 사용자 이름 해야 시스템 계정 이름과 일치 하지 (UID < 100) hello 가상 컴퓨터 (예: "root")에 이미 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="26d17-152">현재 hello RSA SSH 키만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="26d17-153">여러 줄 SSH 키는 `---- BEGIN SSH2 PUBLIC KEY ----`로 시작하고 `---- END SSH2 PUBLIC KEY ----`로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="26d17-154">Superuser 권한 얻기</span><span class="sxs-lookup"><span data-stu-id="26d17-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="26d17-155">Azure에서 가상 컴퓨터 인스턴스에 배포 하는 동안 지정 된 hello 사용자 계정은 권한 있는 계정이입니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="26d17-156">hello sudo의 패키지에 설치 되어 hello FreeBSD 이미지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="26d17-157">이 사용자 계정을 통해 로그인 한 후에 hello 명령 구문을 사용 하 여 루트로 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="26d17-158">선택적으로 `sudo -s`를 사용하여 루트 셸을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="26d17-159">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="26d17-159">Known issues</span></span>
<span data-ttu-id="26d17-160">hello [Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 버전 2.2.2에 [알려진된 문제가 있습니다.] (https://github.com/Azure/WALinuxAgent/pull/517) 되도록 hello 프로 비전 실패 Azure에 FreeBSD VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="26d17-161">hello 수정 하 여 캡처 되었습니다 [Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 2.2.3 버전 또는 이후 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="26d17-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26d17-162">Next steps</span></span>
* <span data-ttu-id="26d17-163">너무 이동[Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD VM입니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="26d17-164">사용자 고유의 FreeBSD tooAzure toobring을 원하는 경우 너무 참조[만들기 및 업로드 FreeBSD VHD tooAzure](linux/classic/freebsd-create-upload-vhd.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26d17-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
