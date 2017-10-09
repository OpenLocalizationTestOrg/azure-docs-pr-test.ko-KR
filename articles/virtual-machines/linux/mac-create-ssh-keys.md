---
title: "Azure에서 Linux Vm에 대 한 aaaCreate 및 사용 된 SSH 키 쌍 | Microsoft Docs"
description: "어떻게 toocreate 및 tooimprove Azure Linux Vm에 대 한 SSH 공용 및 개인 키 쌍 사용 hello hello 인증 프로세스의 보안 합니다."
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
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="b1b1f-103">Azure에서 Linux Vm에 대 한 toocreate 및 SSH 공개 및 개인 키를 사용 하 여 쌍 연결 하는 방법</span><span class="sxs-lookup"><span data-stu-id="b1b1f-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="b1b1f-104">보안 셸 SSH 키 쌍에서 암호 toolog hello 필요성을 제거 인증을 위해 SSH 키를 사용 하 여 Azure에서 가상 컴퓨터 (Vm)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="b1b1f-105">이 문서 tooquickly 생성 하 고 Linux Vm에 대 한 SSH 프로토콜 버전 2 RSA 공개 및 개인 키 파일 쌍을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="b1b1f-106">자세한 단계 및 추가 예제를 참조 하세요. [단계 toocreate SSH 키 쌍과 인증서 세부](create-ssh-keys-detailed.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="b1b1f-107">SSH 키 쌍 만들기</span><span class="sxs-lookup"><span data-stu-id="b1b1f-107">Create an SSH key pair</span></span>
<span data-ttu-id="b1b1f-108">사용 하 여 hello `ssh-keygen` 명령 toocreate SSH 공용 및 개인 키 파일 hello에서 만든 기본적으로 되어 있는 `~/.ssh` 디렉터리 이지만 지정할 수도 있습니다를 다른 위치 및 공유 암호 (암호 tooaccess hello 개인 키 파일을)를 추가 하면 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="b1b1f-109">사용자의 정보로 메시지 표시 hello 응답 hello Bash 셸의에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="b1b1f-110">Hello SSH 키 쌍을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b1b1f-110">Use hello SSH key pair</span></span>
<span data-ttu-id="b1b1f-111">Azure에서 Linux VM에 배치 하는 hello 공개 키가 기본적으로에 저장 `~/.ssh/id_rsa.pub`을 만들 때 hello 위치를 변경 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="b1b1f-112">Hello를 사용 하는 경우 [Azure CLI 2.0](/cli/azure) toocreate VM을 hello를 사용 하는 경우이 공개 키의 hello 위치를 지정 [az vm 만들기](/cli/azure/vm#create) hello로 `--ssh-key-path` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="b1b1f-113">복사한 hello Azure 포털 또는 리소스 관리자 템플릿을 hello hello 공개 키 파일 toouse 내용의 압축을 붙여 넣는 경우 모든 추가 공백 복사 하지 않으면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="b1b1f-114">예를 들어, OS X를 사용 하는 경우 공개 키 파일 hello 파이프할 수 (기본적으로 **~/.ssh/id_rsa.pub**) 너무**pbcopy** (에 없는 같은동일한작업을hello수행하는다른Linux프로그램toocopyhello내용`xclip`).</span><span class="sxs-lookup"><span data-stu-id="b1b1f-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="b1b1f-115">SSH 공개 키를 잘 모르는 경우 다음과 같이 `cat`을 실행하여 공개 키를 확인할 수 있습니다. 이때 `~/.ssh/id_rsa.pub`를 사용자 고유의 공개 키 파일 위치로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="b1b1f-116">IP 주소 또는 VM의 DNS 이름을 hello 사용 하 여 SSH tooyour VM hello Azure VM에서 공개 키를 (tooreplace 기억 `azureuser` 및 `myvm.westus.cloudapp.azure.com` 아래 주소에 hello 관리자 사용자 이름 및 hello 정규화 된 도메인 이름-or IP):</span><span class="sxs-lookup"><span data-stu-id="b1b1f-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="b1b1f-117">사용자 키 쌍을 만들 때 암호를 제공한 경우 hello 로그인 프로세스 동안 메시지가 표시 되 면 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="b1b1f-118">(hello 서버가 tooyour 추가 `~/.ssh/known_hosts` 을 묻는 메시지가 나타나지 않습니다 tooconnect hello 공개 키까지 다시 변경 내용을 Azure VM에서 또는 hello 서버 이름에서 제거 되 `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="b1b1f-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b1f-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1b1f-119">Next steps</span></span>

<span data-ttu-id="b1b1f-120">SSH 키를 사용 하 여 만든 Vm은 사용 하지 않도록 설정 하는 암호를 사용 하 여 구성 하는 기본적으로, 따라서 어렵고 훨씬 더 비쌉니다 시도 toomake 추측 무차별 암호 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="b1b1f-121">이 항목에서는 빠른 사용을 위해 간단한 SSH 키 쌍을 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="b1b1f-122">SSH 키 쌍 만들기에 도움이 필요 하거나 추가 인증서가 필요한 경우 참조 [단계 toocreate SSH 키 쌍과 인증서 세부](create-ssh-keys-detailed.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="b1b1f-123">Hello Azure 포털, CLI 및 서식 파일을 사용 하 여 SSH 키 쌍을 사용 하는 Vm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1b1f-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="b1b1f-124">Hello Azure 포털을 사용 하 여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b1b1f-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b1b1f-125">Hello Azure CLI 2.0을 사용 하 여 보안 Linux VM 만들기)</span><span class="sxs-lookup"><span data-stu-id="b1b1f-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b1b1f-126">Azure 템플릿을 사용하여 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b1b1f-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
