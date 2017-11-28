---
title: "Azure Linux VM aaaReset 액세스 tooan | Microsoft Docs"
description: "Toomanage 사용자 및 재설정 액세스를 사용 하 여 Linux Vm에서 VMAccess 확장을 hello 방법과 Azure CLI 2.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="e78de-103">사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Linux Vm에 Azure CLI 2.0 hello로 VMAccess 확장을 환영</span><span class="sxs-lookup"><span data-stu-id="e78de-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="e78de-104">Linux VM의 디스크 hello이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="e78de-105">어떻게 하 든 Linux VM에 대 한 hello 루트 암호를 재설정 하거나 실수로 SSH 개인 키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="e78de-106">Hello 데이터 센터의 hello 일 후에 다시이 경우 toodrive 발생 해야 하는 다음 hello KVM tooget hello 서버 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="e78de-107">Hello Azure VMAccess 확장 콘솔 tooreset 액세스 tooLinux hello 하면 tooaccess 하거나 디스크 수준 유지 관리를 수행할 수 있도록 KVM 스위치 라고 생각 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="e78de-108">이 문서에서는 어떻게 toouse Azure VMAccess 확장 toocheck hello 또는 디스크 복구, 사용자 액세스를 다시 설정, 사용자 계정 관리 또는 Linux에서 hello SSH 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="e78de-109">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="e78de-110">같은 방법으로 toouse hello VMAccess 확장</span><span class="sxs-lookup"><span data-stu-id="e78de-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="e78de-111">두 가지 방법으로 Linux Vm에서 VMAccess 확장 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="e78de-112">Hello Azure CLI 2.0 및 필요한 hello 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="e78de-113">[원시 JSON을 사용 하 여 해당 hello VMAccess 확장 프로세스 파일](#use-json-files-and-the-vmaccess-extension) 한 후에 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="e78de-114">다음 예제에서 사용 hello [az vm 사용자](/cli/azure/vm/user) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="e78de-115">이 단계는 tooperform, 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="e78de-116">SSH 키 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e78de-116">Reset SSH key</span></span>
<span data-ttu-id="e78de-117">hello 다음 예제에서는 재설정 hello 사용자에 대 한 SSH 키 hello `azureuser` hello 라는 VM에서 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e78de-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="e78de-118">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="e78de-118">Reset password</span></span>
<span data-ttu-id="e78de-119">hello 다음 예제에서는 암호를 다시 설정 hello hello 사용자에 대 한 `azureuser` hello 라는 VM에서 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e78de-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="e78de-120">SSH 다시 시작</span><span class="sxs-lookup"><span data-stu-id="e78de-120">Restart SSH</span></span>
<span data-ttu-id="e78de-121">hello 다음 예제에서는 다시 시작 hello SSH 디먼이 및 재설정 hello 라는 VM에서 SSH 구성 toodefault 값 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e78de-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="e78de-122">사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e78de-122">Create a user</span></span>
<span data-ttu-id="e78de-123">hello 다음 예제에서는 라는 사용자 `myNewUser` hello 라는 VM에서 인증을 위해 SSH 키를 사용 하 여 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e78de-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="e78de-124">사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="e78de-124">Delete a user</span></span>
<span data-ttu-id="e78de-125">hello 다음 예에서는 삭제 라는 사용자 `myNewUser` hello 라는 VM에서 `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e78de-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="e78de-126">JSON 파일을 사용 하 고 hello VMAccess 확장</span><span class="sxs-lookup"><span data-stu-id="e78de-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="e78de-127">다음 예제는 hello 원시 JSON 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="e78de-128">사용 하 여 [az vm 확장 집합](/cli/azure/vm/extension#set) toothen JSON 파일을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="e78de-129">이러한 JSON 파일은 Azure 템플릿에서도 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="e78de-130">사용자 액세스 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e78de-130">Reset user access</span></span>
<span data-ttu-id="e78de-131">Linux VM에 대 한 액세스 tooroot를 잃어버린 경우에 사용자의 SSH 키 또는 암호 VMAccess 스크립트 tooreset를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="e78de-132">사용자, tooreset hello SSH 공개 키 파일을 만듭니다 `reset_ssh_key.json` 및 형식에 따라 hello에 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="e78de-133">Hello에 대 한 고유한 값으로 대체 `username` 및 `ssh_key` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="e78de-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="e78de-134">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="e78de-135">사용자 암호를 tooreset 라는 파일을 만들어 `reset_user_password.json` 및 형식에 따라 hello에 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="e78de-136">Hello에 대 한 고유한 값으로 대체 `username` 및 `password` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="e78de-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="e78de-137">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="e78de-138">SSH 다시 시작</span><span class="sxs-lookup"><span data-stu-id="e78de-138">Restart SSH</span></span>
<span data-ttu-id="e78de-139">SSH 디먼이 hello 및 hello SSH 구성 toodefault 값 다시 설정, 라는 파일을 만들어 toorestart `reset_sshd.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="e78de-140">Hello 다음 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="e78de-141">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="e78de-142">사용자 관리</span><span class="sxs-lookup"><span data-stu-id="e78de-142">Manage users</span></span>

<span data-ttu-id="e78de-143">인증을 위해 SSH 키를 사용 하는 사용자 toocreate 라는 파일을 만들어 `create_new_user.json` 형식에 따라 hello에 설정을 추가 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="e78de-144">Hello에 대 한 고유한 값으로 대체 `username` 및 `ssh_key` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="e78de-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="e78de-145">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="e78de-146">사용자를 toodelete 라는 파일을 만들어 `delete_user.json` hello 다음 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="e78de-147">Hello에 대 한 고유한 값을 대체 `remove_user` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="e78de-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="e78de-148">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="e78de-149">확인 또는 복구 hello 디스크</span><span class="sxs-lookup"><span data-stu-id="e78de-149">Check or repair hello disk</span></span>
<span data-ttu-id="e78de-150">VMAccess를 사용 하 여 확인 및 복구 toohello Linux VM을 추가 하면 디스크 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="e78de-151">toocheck 및 복구 hello 디스크 라는 파일을 만들어 `disk_check_repair.json` 및 형식에 따라 hello에 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="e78de-152">Hello 이름에 대 한 고유한 값을 대체 `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="e78de-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="e78de-153">Hello VMAccess 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="e78de-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e78de-154">Next steps</span></span>
<span data-ttu-id="e78de-155">Linux를 업데이트 하면 실행 중인 Linux VM에 하나의 메서드 toomake 변경은 hello Azure VMAccess 확장을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="e78de-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="e78de-156">작업을 부팅 시 Linux VM 클라우드 init 및 Azure 리소스 관리자 템플릿 toomodify와 같은 도구도 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e78de-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="e78de-157">Linux용 가상 컴퓨터 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="e78de-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="e78de-158">Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="e78de-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="e78de-159">클라우드 init toocustomize Linux VM을 만드는 동안 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e78de-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

