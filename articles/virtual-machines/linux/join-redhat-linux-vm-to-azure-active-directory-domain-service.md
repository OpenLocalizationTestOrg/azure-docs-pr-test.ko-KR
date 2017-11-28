---
title: RedHat Linux VM tooan Azure Active Directory DS aaaJoin | Microsoft Docs
description: "어떻게 toojoin 기존 RedHat Enterprise Linux 7 VM tooan Azure Active Directory 도메인 서비스."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="e47f2-103">RedHat Linux VM tooan Azure Active Directory 도메인 서비스에 가입</span><span class="sxs-lookup"><span data-stu-id="e47f2-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="e47f2-104">이 문서에서는 toojoin Red Hat Enterprise Linux (RHEL) 7 가상 컴퓨터 tooan Azure Active Directory 도메인 서비스 (AADDS) 도메인을 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e47f2-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="e47f2-105">hello 요구 사항은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e47f2-105">hello requirements are:</span></span>

- [<span data-ttu-id="e47f2-106">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="e47f2-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="e47f2-107">SSH 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="e47f2-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="e47f2-108">Azure Active Directory Domain Services DC</span><span class="sxs-lookup"><span data-stu-id="e47f2-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="e47f2-109">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="e47f2-109">Quick Commands</span></span>

<span data-ttu-id="e47f2-110">_모든 예제를 고유한 설정으로 바꿉니다._</span><span class="sxs-lookup"><span data-stu-id="e47f2-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="e47f2-111">Hello azure cli tooclassic 배포 모드를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e47f2-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="e47f2-112">RHEL 버전 및 이미지 검색</span><span class="sxs-lookup"><span data-stu-id="e47f2-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="e47f2-113">Redhat Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e47f2-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a><span data-ttu-id="e47f2-114">SSH toohello VM</span><span class="sxs-lookup"><span data-stu-id="e47f2-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="e47f2-115">YUM 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="e47f2-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="e47f2-116">필요한 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="e47f2-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="e47f2-117">이제 필요한 hello 패키지 hello Linux 가상 컴퓨터에 설치 되 면 다음 태스크에서는 hello입니다 toojoin hello 가상 컴퓨터 toohello 관리 되는 도메인.</span><span class="sxs-lookup"><span data-stu-id="e47f2-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="e47f2-118">Hello AAD 도메인 서비스에 대 한 관리 되는 도메인 검색</span><span class="sxs-lookup"><span data-stu-id="e47f2-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="e47f2-119">kerberos 초기화</span><span class="sxs-lookup"><span data-stu-id="e47f2-119">Initialize kerberos</span></span>

<span data-ttu-id="e47f2-120">Toohello AAD ' DC Administrators' 그룹에 속한 사용자가을 지정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e47f2-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="e47f2-121">이러한 사용자만 컴퓨터 toohello 관리 되는 도메인에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e47f2-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="e47f2-122">Hello 컴퓨터 toohello 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="e47f2-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="e47f2-123">도메인에 가입된 toohello hello 컴퓨터 확인</span><span class="sxs-lookup"><span data-stu-id="e47f2-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="e47f2-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e47f2-124">Next Steps</span></span>

* [<span data-ttu-id="e47f2-125">Azure에서 주문형 Red Hat Enterprise Linux VM에 대한 RHUI(Red Hat Update Infrastructure)</span><span class="sxs-lookup"><span data-stu-id="e47f2-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e47f2-126">Azure Resource Manager에서 가상 컴퓨터에 대한 Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="e47f2-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e47f2-127">배포 하 고 hello Azure CLI 및 Azure 리소스 관리자 템플릿을 사용 하 여 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e47f2-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
