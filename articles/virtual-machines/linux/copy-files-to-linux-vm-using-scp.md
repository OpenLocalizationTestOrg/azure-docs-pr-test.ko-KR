---
title: "SCP를 사용하여 Azure Linux VM 간에 파일 이동 | Microsoft Docs"
description: "SCP 및 SSH 키 쌍을 사용하여 Azure에서 Linux VM 간에 안전하게 파일을 이동합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 736f7c11ec3de04f1ad52ee29d0a4c952c9b0545
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="move-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="0669e-103">SCP를 사용하여 Linux VM 간에 파일 이동</span><span class="sxs-lookup"><span data-stu-id="0669e-103">Move files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="0669e-104">이 문서에서는 보안 복사본(SCP)를 사용하여 워크스테이션에서 Azure Linux VM으로 또는 Azure Linux VM에서 워크스테이션으로 파일을 이동하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="0669e-105">워크스테이션과 Linux VM 간에 신속하고 안전하게 파일을 이동하는 것은 Azure 인프라 관리의 중요한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="0669e-106">이 문서의 경우 [SSH 공개 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 Azure에 Linux VM이 배포되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0669e-107">또한 로컬 컴퓨터에 SCP 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="0669e-108">SSH 위에 구축되었고 대부분의 Linux 및 Mac 컴퓨터 기본 Bash 셸과 일부 Windows 셸에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-108">It is built on top of SSH and included in the default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0669e-109">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="0669e-109">Quick commands</span></span>

<span data-ttu-id="0669e-110">Linux VM으로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="0669e-110">Copy a file up to the Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="0669e-111">Linux VM에서 파일 복사</span><span class="sxs-lookup"><span data-stu-id="0669e-111">Copy a file down from the Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0669e-112">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="0669e-112">Detailed walkthrough</span></span>

<span data-ttu-id="0669e-113">예를 들어 Linux VM까지 Azure 구성 파일을 이동하고 로그 파일 디렉터리를 끌어오는 경우 모두 SCP 및 SSH 키를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-113">As examples, we move an Azure configuration file up to a Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="0669e-114">SSH 키 쌍 인증</span><span class="sxs-lookup"><span data-stu-id="0669e-114">SSH key pair authentication</span></span>

<span data-ttu-id="0669e-115">SCP는 전송 계층에 대해 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-115">SCP uses SSH for the transport layer.</span></span> <span data-ttu-id="0669e-116">SSH는 대상 호스트에서 인증을 처리하고 SSH와 함께 기본적으로 제공되는 암호화된 터널에서 파일을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-116">SSH handles the authentication on the destination host, and it moves the file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="0669e-117">SSH 인증에는 사용자 이름 및 암호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="0669e-118">그러나 SSH 공개 및 개인 키 인증이 보안 모범 사례로 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="0669e-119">SSH에서 연결을 인증하면 SCP는 파일 복사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-119">Once SSH has authenticated the connection, SCP then begins copying the file.</span></span> <span data-ttu-id="0669e-120">적절히 구성된 `~/.ssh/config`와 SSH 공개 및 개인 키를 사용하면 서버 이름(또는 IP 주소)만 사용해서 SCP 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="0669e-121">SSH 키가 하나만 있는 경우 SCP는 `~/.ssh/` 디렉터리에서 이 키를 찾은 후 VM에 로그인하는 데 기본적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-121">If you only have one SSH key, SCP looks for it in the `~/.ssh/` directory, and uses it by default to log in to the VM.</span></span>

<span data-ttu-id="0669e-122">`~/.ssh/config`와 SSH 공개 및 개인 키 구성에 대한 자세한 내용은 [SSH 키 만들기](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0669e-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="0669e-123">파일을 Linux VM으로 SCP</span><span class="sxs-lookup"><span data-stu-id="0669e-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="0669e-124">첫 번째 예제에서는 Azure 구성 파일을 Automation 배포에 사용되는 Linux VM까지 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-124">For the first example, we copy an Azure configuration file up to a Linux VM that is used to deploy automation.</span></span> <span data-ttu-id="0669e-125">이 파일에는 비밀이 포함된 Azure API 자격 증명이 있으므로 보안이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="0669e-126">SSH에서 제공하는 암호화된 터널은 파일의 콘텐츠를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-126">The encrypted tunnel provided by SSH protects the contents of the file.</span></span>

<span data-ttu-id="0669e-127">다음 명령에서는 로컬 *.azure/config* 파일을 FQDN *myserver.eastus.cloudapp.azure.com*을 사용하여 Azure VM에 복사합니다. Azure VM의 관리자 사용자 이름은 *azureuser*입니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-127">The following command copies the local *.azure/config* file to an Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. The admin user name on the Azure VM is *azureuser*.</span></span> <span data-ttu-id="0669e-128">파일은 */home/azureuser/* 디렉터리로 대상이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-128">The file is targeted to the */home/azureuser/* directory.</span></span> <span data-ttu-id="0669e-129">이 명령에서 고유한 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="0669e-130">디렉터리를 Linux VM에서 SCP</span><span class="sxs-lookup"><span data-stu-id="0669e-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="0669e-131">이 예제에서는 Linux VM에서 워크스테이션으로 로그 파일 디렉터리를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-131">For this example, we copy a directory of log files from the Linux VM down to your workstation.</span></span> <span data-ttu-id="0669e-132">로그 파일에는 중요한 데이터 및 비밀 데이터가 있을 수도 있고 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="0669e-133">그러나 SCP를 사용하면 로그 파일의 콘텐츠가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-133">However, using SCP ensures the contents of the log files are encrypted.</span></span> <span data-ttu-id="0669e-134">SCP를 사용하여 파일을 전송하는 것이 로그 디렉터리 및 파일을 안전하게 워크스테이션으로 가져오는 가장 쉬우면서도 안전한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-134">Using SCP to transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

<span data-ttu-id="0669e-135">다음 명령에서는 Azure VM에서 */home/azureuser/logs/* 디렉터리의 파일을 local/tmp 디렉터리로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-135">The following command copies files in the */home/azureuser/logs/* directory on the Azure VM to the local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="0669e-136">`-r` cli 플래그는 명령에 나열된 디렉터리의 시점부터 파일 및 디렉터리를 재귀적으로 복사하도록 SCP에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-136">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="0669e-137">또한 명령줄 구문은 `cp` 복사 명령과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0669e-137">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0669e-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0669e-138">Next steps</span></span>

* [<span data-ttu-id="0669e-139">VMAccess 확장을 사용하여 사용자, SSH 관리 및 Azure Linux VM의 디스크 검사 또는 복구</span><span class="sxs-lookup"><span data-stu-id="0669e-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)