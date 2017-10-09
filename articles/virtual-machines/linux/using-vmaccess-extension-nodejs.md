---
title: "aaaReset 액세스를 사용 하 여 Azure Linux Vm에서 VMAccess 확장을 hello | Microsoft Docs"
description: "Hello VMAccess 확장을 사용 하 여 Azure Linux Vm에 대 한 액세스를 다시 설정 합니다."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="3d7bf-103">사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에 Azure CLI 1.0 hello로 VMAccess 확장을 환영</span><span class="sxs-lookup"><span data-stu-id="3d7bf-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="3d7bf-104">이 문서에서는 어떻게 toouse Azure VMAcesss 확장 toocheck hello 또는 디스크 복구, 사용자 액세스를 다시 설정, 사용자 계정 관리 또는 Linux에서 hello SSHD 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="3d7bf-105">hello 문서에는 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-105">hello article requires:</span></span>

* <span data-ttu-id="3d7bf-106">Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="3d7bf-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="3d7bf-107">hello [Azure CLI](../../cli-install-nodejs.md) 로그인 한 `azure login`합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="3d7bf-108">hello Azure CLI *에 있어야* Azure Resource Manager 모드 `azure config mode arm`합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3d7bf-109">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="3d7bf-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="3d7bf-110">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3d7bf-111">[Azure CLI 1.0](#quick-commands)– 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="3d7bf-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3d7bf-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="3d7bf-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="3d7bf-113">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="3d7bf-113">Quick commands</span></span>
<span data-ttu-id="3d7bf-114">두 가지 방법으로 toouse Linux Vm에서 VMAccess 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="3d7bf-115">Hello Azure CLI 1.0 및 hello를 사용 하 여 매개 변수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="3d7bf-116">VMAccess에서 처리한 후 관련 작업을 수행하는 원시 JSON 파일 사용</span><span class="sxs-lookup"><span data-stu-id="3d7bf-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="3d7bf-117">Hello 빠른 명령 섹션에 대 한 하겠습니다 toouse hello Azure CLI 1.0 `azure vm reset-access` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="3d7bf-118">Hello 다음 명령 예에서는 "예" hello 값을 가진 사용자가 자신의 환경에서 포함 하는 hello 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="3d7bf-119">리소스 그룹 및 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3d7bf-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="3d7bf-120">Debian VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3d7bf-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="3d7bf-121">루트 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="3d7bf-121">Reset root password</span></span>
<span data-ttu-id="3d7bf-122">tooreset hello 루트 암호:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="3d7bf-123">SSH 키 다시 설정</span><span class="sxs-lookup"><span data-stu-id="3d7bf-123">SSH key reset</span></span>
<span data-ttu-id="3d7bf-124">루트가 아닌 사용자의 tooreset hello SSH 키:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="3d7bf-125">사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3d7bf-125">Create a user</span></span>
<span data-ttu-id="3d7bf-126">toocreate 사용자:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="3d7bf-127">사용자 제거</span><span class="sxs-lookup"><span data-stu-id="3d7bf-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="3d7bf-128">SSHD 재설정</span><span class="sxs-lookup"><span data-stu-id="3d7bf-128">Reset SSHD</span></span>
<span data-ttu-id="3d7bf-129">tooreset hello SSHD 구성:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="3d7bf-130">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="3d7bf-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="3d7bf-131">VMAccess 정의:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-131">VMAccess defined:</span></span>
<span data-ttu-id="3d7bf-132">Linux VM의 디스크 hello이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="3d7bf-133">어떻게 하 든 Linux VM에 대 한 hello 루트 암호를 재설정 하거나 실수로 SSH 개인 키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="3d7bf-134">Hello 데이터 센터의 hello 일 후에 다시이 경우 toodrive 발생 해야 하는 다음 hello KVM tooget hello 서버 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="3d7bf-135">Hello Azure VMAccess 확장 콘솔 tooreset 액세스 tooLinux hello 하면 tooaccess 하거나 디스크 수준 유지 관리를 수행할 수 있도록 KVM 스위치 라고 생각 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="3d7bf-136">Hello에 대 한 자세한 연습에서는 toouse hello 긴 형식의 원시 JSON 파일을 사용 하 여 VMAccess 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="3d7bf-137">이러한 VMAccess JSON 파일은 Azure 템플릿에서도 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="3d7bf-138">Linux VM의 VMAccess toocheck 또는 복구 hello 디스크를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3d7bf-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="3d7bf-139">VMAccess를 사용 하 여 할 수 있는 한 fsck Linux VM에서 hello 디스크에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="3d7bf-140">VMAccess를 사용하여 디스크 검사와 디스크 복구를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="3d7bf-141">toocheck, 및 복구 hello 디스크가 VMAccess 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="3d7bf-142">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="3d7bf-143">VMAccess tooreset 사용자 액세스 tooLinux를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3d7bf-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="3d7bf-144">Linux VM에 대 한 액세스 tooroot를 잃어버린 경우 VMAccess 스크립트 tooreset hello 루트 암호를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="3d7bf-145">tooreset hello 루트 암호를이 VMAccess 스크립트 사용:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="3d7bf-146">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="3d7bf-147">루트가 아닌 사용자의 tooreset hello SSH 키에는이 VMAccess 스크립트 사용:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="3d7bf-148">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="3d7bf-149">Linux에서 VMAccess toomanage 사용자 계정을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3d7bf-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="3d7bf-150">VMAccess 없이 로그인 하 고 sudo 또는 hello 루트 계정을 사용 하 여 Linux VM에 사용 되는 toomanage 사용자 일 수 있는 Python 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="3d7bf-151">toocreate 사용자를이 VMAccess 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="3d7bf-152">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="3d7bf-153">toodelete 사용자를이 VMAccess 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="3d7bf-154">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="3d7bf-155">VMAccess tooreset hello SSHD 구성을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3d7bf-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="3d7bf-156">변경 내용 toohello Linux Vm SSHD 구성과 hello 변경 내용 확인 되기 전에 닫기 hello SSH 연결을 만들면 연결할 수 없을 수도 SSH'ing에서 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="3d7bf-157">VMAccess 사용된 tooreset hello SSHD 구성 뒤로 tooa로 성공한 구성 SSH를 통해 로그인 하지 않고 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="3d7bf-158">이 VMAccess 스크립트를 사용 하는 tooreset hello SSHD 구성:</span><span class="sxs-lookup"><span data-stu-id="3d7bf-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="3d7bf-159">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="3d7bf-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d7bf-160">Next steps</span></span>
<span data-ttu-id="3d7bf-161">Linux 업데이트 되어 실행 중인 Linux VM에 하나의 메서드 toomake 변경 내용을 Azure VMAccess 확장을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="3d7bf-162">작업을 부팅 시 Linux VM 클라우드 init 및 Azure 템플릿 toomodify와 같은 도구도 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d7bf-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="3d7bf-163">가상 컴퓨터 확장 및 기능 정보</span><span class="sxs-lookup"><span data-stu-id="3d7bf-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="3d7bf-164">Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="3d7bf-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="3d7bf-165">클라우드 init toocustomize Linux VM을 만드는 동안 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3d7bf-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

