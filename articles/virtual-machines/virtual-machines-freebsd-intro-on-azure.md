---
title: "Azure의 FreeBSD 소개 | Microsoft Docs"
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
ms.openlocfilehash: d0fc5de34f7d9e5a607495eb97d9e35dc9eb21f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="56a15-103">Azure의 FreeBSD 소개</span><span class="sxs-lookup"><span data-stu-id="56a15-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="56a15-104">이 항목에서는 Azure에서 FreeBSD 가상 컴퓨터를 실행하는 방법의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="56a15-105">개요</span><span class="sxs-lookup"><span data-stu-id="56a15-105">Overview</span></span>
<span data-ttu-id="56a15-106">Microsoft Azure용 FreeBSD는 최신 서버, 데스크톱 및 포함된 플랫폼을 작동하는 데 사용되는 고급 컴퓨터 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="56a15-107">Microsoft Corporation은 Azure에서 사용 가능한 [Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/)가 미리 구성된 FreeBSD 이미지를 만들고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="56a15-108">현재 다음 FreeBSD 버전이 Microsoft에서 이미지로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="56a15-109">FreeBSD 10.3 릴리스</span><span class="sxs-lookup"><span data-stu-id="56a15-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="56a15-110">FreeBSD 11.0 릴리스</span><span class="sxs-lookup"><span data-stu-id="56a15-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="56a15-111">이 에이전트는 처음 사용 시 VM을 프로비전(사용자 이름, 암호 또는 SSH 키, 호스트 이름 등)하고 선택적 VM 확장 기능을 사용하도록 설정하는 것과 같은 작업을 위해 FreeBSD VM과 Azure 패브릭 간의 통신을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="56a15-112">FreeBSD 후속 버전에서는 제품을 최신 상태로 유지하고, FreeBSD 릴리스 엔지니어링 팀에서 게시한 후에 바로 해당 최신 릴리스를 사용할 수 있도록 하는 전략을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="56a15-113">FreeBSD 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="56a15-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="56a15-114">FreeBSD 가상 컴퓨터 배포 작업은 Azure Portal에서 Azure Marketplace의 이미지를 사용하는 간단한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="56a15-115">Azure Marketplace의 FreeBSD 10.3</span><span class="sxs-lookup"><span data-stu-id="56a15-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="56a15-116">Azure Marketplace의 FreeBSD 11.0</span><span class="sxs-lookup"><span data-stu-id="56a15-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="56a15-117">FreeBSD에서 Azure CLI 2.0을 통해 FreeBSD VM 만들기</span><span class="sxs-lookup"><span data-stu-id="56a15-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="56a15-118">먼저 FreeBSD 컴퓨터에서 다음 명령을 사용하여 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="56a15-119">bash가 FreeBSD 컴퓨터에 설치되지 않은 경우 설치 전에 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="56a15-120">python이 FreeBSD 컴퓨터에 설치되지 않은 경우 설치 전에 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="56a15-121">설치하는 동안 `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="56a15-122">`y`로 답변하고 `a path to an rc file to update`로 `/etc/rc.conf`를 입력하면 문제 `ERROR: [Errno 13] Permission denied`가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="56a15-123">이 문제를 해결하려면 현재 사용자에게 `etc/rc.conf` 파일에 대한 쓰기 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="56a15-124">이제 Azure에 로그인한 후 FreeBSD VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="56a15-125">다음은 FreeBSD 11.0 VM을 만드는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="56a15-126">새로 만든 공용 IP의 정규화된 DNS 이름을 사용하여 `--public-ip-address-dns-name` 매개 변수를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="56a15-127">그런 후 위 배포의 출력에 표시된 IP 주소를 통해 FreeBSD VM에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="56a15-128">FreeBSD에 대한 VM 확장</span><span class="sxs-lookup"><span data-stu-id="56a15-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="56a15-129">FreeBSD에서 지원되는 VM 확장은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="56a15-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="56a15-130">VMAccess</span></span>
<span data-ttu-id="56a15-131">[VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) 확장으로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="56a15-132">원래 sudo 사용자의 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="56a15-133">지정된 암호를 사용하여 새 sudo 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="56a15-134">지정된 키로 공개 호스트 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="56a15-135">호스트 키가 제공되지 않은 경우 VM 프로비전 중에 제공된 공개 호스트 키를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="56a15-136">SSH 포트(22)를 열고, reset_ssh가 true로 설정된 경우 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="56a15-137">기존 사용자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-137">Remove the existing user.</span></span>
* <span data-ttu-id="56a15-138">디스크를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-138">Check disks.</span></span>
* <span data-ttu-id="56a15-139">추가된 디스크를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="56a15-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="56a15-140">CustomScript</span></span>
<span data-ttu-id="56a15-141">[CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) 확장으로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="56a15-142">제공될 경우 Azure Storage 또는 외부 공용 저장소(예: GitHub)에서 사용자 지정된 스크립트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="56a15-143">진입점 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-143">Run the entry point script.</span></span>
* <span data-ttu-id="56a15-144">인라인 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-144">Support inline commands.</span></span>
* <span data-ttu-id="56a15-145">셸 및 Python 스크립트에서 Windows 스타일 줄 바꿈 문자를 자동으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="56a15-146">셸 및 Python 스크립트의 BOM을 자동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="56a15-147">CommandToExecute의 중요 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="56a15-148">FreeBSD VM은 현재 CustomScript 버전 1.x만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="56a15-149">인증: 사용자 이름, 암호 및 SSH 키</span><span class="sxs-lookup"><span data-stu-id="56a15-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="56a15-150">Azure 포털을 사용하여 FreeBSD 가상 컴퓨터를 만들 때 사용자 이름, 암호 또는 SSH 공개 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="56a15-151">Azure에서 FreeBSD 가상 컴퓨터를 배포하기 위한 사용자 이름은 가상 컴퓨터에 이미 있는 시스템 계정 이름(UID <100)(예: "root")과 일치해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="56a15-152">현재는 RSA SSH 키만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="56a15-153">여러 줄 SSH 키는 `---- BEGIN SSH2 PUBLIC KEY ----`로 시작하고 `---- END SSH2 PUBLIC KEY ----`로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="56a15-154">Superuser 권한 얻기</span><span class="sxs-lookup"><span data-stu-id="56a15-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="56a15-155">Azure에서 가상 컴퓨터 인스턴스를 배포하는 동안 지정한 사용자 계정이 권한 있는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="56a15-156">sudo의 패키지는 게시된 FreeBSD 이미지에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="56a15-157">이 사용자 계정을 통해 로그인하면 명령 구문을 사용하여 루트 권한으로 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="56a15-158">선택적으로 `sudo -s`를 사용하여 루트 셸을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="56a15-159">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="56a15-159">Known issues</span></span>
<span data-ttu-id="56a15-160">[Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 버전 2.2.2에는 Azure의 FreeBSD VM에 프로비전 오류를 유발하는 [알려진 문제](https://github.com/Azure/WALinuxAgent/pull/517)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="56a15-161">[Azure VM 게스트 에이전트](https://github.com/Azure/WALinuxAgent/) 버전 2.2.3 및 이후 릴리스에서는 해결책이 확보될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="56a15-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56a15-162">Next steps</span></span>
* <span data-ttu-id="56a15-163">[Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) 로 가서 FreeBSD VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56a15-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="56a15-164">자체 FreeBSD를 Azure로 가져오려면 [FreeBSD VHD 만들기 및 Azure로 업로드](linux/classic/freebsd-create-upload-vhd.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56a15-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
