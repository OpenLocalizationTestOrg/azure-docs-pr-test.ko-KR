---
title: "Azure에서 Linux VM용 SSH 키 쌍 만들기 및 사용 | Microsoft Docs"
description: "Azure에서 인증 프로세스의 보안을 개선하기 위해 Linux VM용 SSH 공용 및 개인 키를 만들고 사용하는 방법입니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 0fb71d2ffe533afba6e1e527b727a7b085e7da14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="e797f-103">Azure에서 Linux VM용 SSH 공개 및 개인 키 쌍을 만들고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="e797f-103">How to create and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="e797f-104">SSH(보안 셸) 키 쌍을 사용하면 인증을 위해 SSH 키를 사용하는 VM(가상 컴퓨터)을 Azure에서 만들 수 있으며 로그인하기 위해 암호가 필요하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="e797f-105">이 문서에서는 Linux VM용 SSH 프로토콜 버전 2 RSA 공개 및 개인 키 파일 쌍을 신속하게 생성하고 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-105">This article shows you how to quickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="e797f-106">자세한 단계 및 추가 예제는 [SSH 키 쌍 및 인증서를 만드는 자세한 단계](create-ssh-keys-detailed.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e797f-106">For more detailed steps and additional examples, see [detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="e797f-107">SSH 키 쌍 만들기</span><span class="sxs-lookup"><span data-stu-id="e797f-107">Create an SSH key pair</span></span>
<span data-ttu-id="e797f-108">`ssh-keygen` 명령을 사용하여 기본적으로 `~/.ssh` 디렉터리에 생성되는 SSH 공개 및 개인 키 파일을 만들지만 메시지가 표시되면 다른 위치 및 추가 암호(개인 키 파일에 액세스하는 암호)를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-108">Use the `ssh-keygen` command to create SSH public and private key files that are by default created in the `~/.ssh` directory, but you can specify a different location and additional passphrase (a password to access the private key file) when prompted.</span></span> <span data-ttu-id="e797f-109">Bash 셸에서 다음 명령을 실행하여 사용자 고유의 정보로 프롬프트에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-109">Run the following command from a Bash shell, answering the prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-the-ssh-key-pair"></a><span data-ttu-id="e797f-110">SSH 키 쌍 사용</span><span class="sxs-lookup"><span data-stu-id="e797f-110">Use the SSH key pair</span></span>
<span data-ttu-id="e797f-111">Azure에서 Linux VM에 배치하는 공개 키는 만들 때 위치를 변경하지 않는다면, 기본적으로 `~/.ssh/id_rsa.pub`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-111">The public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed the location when you created them.</span></span> <span data-ttu-id="e797f-112">[Azure CLI 2.0](/cli/azure)을 사용하여 사용자의 VM을 만드는 경우 [az vm create](/cli/azure/vm#create)와 `--ssh-key-path` 옵션을 사용할 때 이 공개 키의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-112">If you use the [Azure CLI 2.0](/cli/azure) to create your VM, specify the location of this public key when you use the [az vm create](/cli/azure/vm#create) with the `--ssh-key-path` option.</span></span> <span data-ttu-id="e797f-113">Azure Portal 또는 Resource Manager 템플릿에서 사용할 공개 키 파일의 내용을 복사하여 붙여넣으려는 경우 추가 공백은 복사하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-113">If you copy and paste the contents of the public key file to use in the Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="e797f-114">예를 들어, OS X을 사용하는 경우 공개 키 파일(기본적으로 **~/.ssh/id_rsa.pub**)을 **pbcopy**로 파이프하여 내용을 복사할 수 있습니다(`xclip`처럼 동일한 작업을 수행하는 다른 Linux 프로그램이 있음).</span><span class="sxs-lookup"><span data-stu-id="e797f-114">For example, if you use OS X, you can pipe the public key file (by default, **~/.ssh/id_rsa.pub**) to **pbcopy** to copy the contents (there are other Linux programs that do the same thing, such as `xclip`).</span></span>

<span data-ttu-id="e797f-115">SSH 공개 키를 잘 모르는 경우 다음과 같이 `cat`을 실행하여 공개 키를 확인할 수 있습니다. 이때 `~/.ssh/id_rsa.pub`를 사용자 고유의 공개 키 파일 위치로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="e797f-116">Azure VM에서 공개 키를 통해 VM의 IP 주소 및 DNS 이름을 사용하여 VM에 SSH를 사용합니다(아래 `azureuser` 및 `myvm.westus.cloudapp.azure.com`을 관리자 사용자 이름 및 정규화된 도메인 이름 또는 IP 주소로 대체해야 함).</span><span class="sxs-lookup"><span data-stu-id="e797f-116">With the public key on your Azure VM, SSH to your VM using the IP address or DNS name of your VM (remember to replace `azureuser` and `myvm.westus.cloudapp.azure.com` below with the admin username and the fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="e797f-117">키 쌍을 만들 때 암호를 제공한 경우 로그인 프로세스 중에 메시지가 표시되면 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-117">If you provided a passphrase when you created your key pair, enter the passphrase when prompted during the login process.</span></span> <span data-ttu-id="e797f-118">(서버가 `~/.ssh/known_hosts` 폴더에 추가되고 Azure VM에서 공개 키가 변경되거나 서버 이름이 `~/.ssh/known_hosts`에서 제거될 까지 다시 연결할지 묻는 메시지가 표시되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="e797f-118">(The server is added to your `~/.ssh/known_hosts` folder, and you won't be asked to connect again until the public key on your Azure VM changes or the server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e797f-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e797f-119">Next steps</span></span>

<span data-ttu-id="e797f-120">SSH 키를 사용하여 만든 VM은 기본적으로 비활성화된 암호를 사용하여 구성되고 강제 무차별 암호 추측 시도를 더욱 비용이 많이 들고 결과적으로 어렵게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-120">VMs created using SSH keys are by default configured with passwords disabled, to make brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="e797f-121">이 항목에서는 빠른 사용을 위해 간단한 SSH 키 쌍을 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="e797f-122">SSH 키 쌍 만들기에 도움이 필요하거나 추가 인증서가 필요한 경우 [SSH 키 쌍 및 인증서를 만드는 자세한 단계](create-ssh-keys-detailed.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e797f-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="e797f-123">Azure Portal, CLI 및 템플릿을 사용하여 SSH 키 쌍을 사용하는 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e797f-123">You can create VMs that use your SSH key pair using the Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="e797f-124">Azure Portal을 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e797f-124">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e797f-125">Azure CLI 2.0를 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e797f-125">Create a secure Linux VM using the Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e797f-126">Azure 템플릿을 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e797f-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
