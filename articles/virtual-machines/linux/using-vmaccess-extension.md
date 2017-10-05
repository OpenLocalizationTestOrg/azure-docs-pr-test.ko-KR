---
title: "Azure Linux VM에 대한 액세스 다시 설정 | Microsoft Docs"
description: "VMAccess 확장 및 Azure CLI 2.0을 사용하여 사용자를 관리하고 Linux VM에 대한 액세스를 다시 설정하는 방법"
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
ms.openlocfilehash: 587c73278a9a92776276a811c5c4c8d3db773de3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-20"></a><span data-ttu-id="4680d-103">Azure CLI 2.0에서 VMAccess 확장을 사용하여 사용자, SSH 관리 및 Linux VM의 디스크 검사 또는 복구</span><span class="sxs-lookup"><span data-stu-id="4680d-103">Manage users, SSH, and check or repair disks on Linux VMs using the VMAccess Extension with the Azure CLI 2.0</span></span>
<span data-ttu-id="4680d-104">Linux VM의 디스크에 오류가 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-104">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="4680d-105">사용자가 Linux VM의 루트 암호를 재설정했거나 SSH 개인 키를 실수로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-105">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="4680d-106">데이터 센터를 사용할 때는 이러한 경우 데이터 센터로 직접 가서 KVM을 열어 서버 콘솔에 액세스해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-106">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="4680d-107">Azure VMAccess 확장을 콘솔에 액세스하여 Linux에 대한 액세스 권한을 재설정하거나 디스크 수준 유지 관리를 수행할 수 있는 이 KVM 스위치로 생각하세요.</span><span class="sxs-lookup"><span data-stu-id="4680d-107">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="4680d-108">이 문서는 VMAccess VM 확장을 사용하여 디스크를 검사 또는 복구하거나, 사용자 액세스를 다시 설정하거나, 사용자 계정을 관리하거나, Linux의 SSH 구성을 다시 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-108">This article shows you how to use the Azure VMAccess Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSH configuration on Linux.</span></span> <span data-ttu-id="4680d-109">[Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-109">You can also perform these steps with the [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-to-use-the-vmaccess-extension"></a><span data-ttu-id="4680d-110">VMAccess 확장을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4680d-110">Ways to use the VMAccess Extension</span></span>
<span data-ttu-id="4680d-111">Linux VM에서 두 가지 방법으로 VMAccess 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-111">There are two ways that you can use the VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="4680d-112">Azure CLI 2.0 및 필수 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-112">Use the Azure CLI 2.0 and the required parameters.</span></span>
* <span data-ttu-id="4680d-113">[VMAccess 확장을 처리하고 관련 작업을 수행하는 원시 JSON 파일을 사용](#use-json-files-and-the-vmaccess-extension)합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-113">[Use raw JSON files that the VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="4680d-114">다음 예에서는 [az vm user](/cli/azure/vm/user) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-114">The following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="4680d-115">이러한 단계를 수행하려면 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-115">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="4680d-116">SSH 키 다시 설정</span><span class="sxs-lookup"><span data-stu-id="4680d-116">Reset SSH key</span></span>
<span data-ttu-id="4680d-117">다음 예제에서는 VM `myVM`에서 사용자 `azureuser`에 대한 SSH 키를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-117">The following example resets the SSH key for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="4680d-118">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="4680d-118">Reset password</span></span>
<span data-ttu-id="4680d-119">다음 예제에서는 VM `myVM`에서 사용자 `azureuser`에 대한 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-119">The following example resets the password for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="4680d-120">SSH 다시 시작</span><span class="sxs-lookup"><span data-stu-id="4680d-120">Restart SSH</span></span>
<span data-ttu-id="4680d-121">다음 예제에서는 SSH 디먼을 다시 시작하고 SSH 구성을 `myVM`이라는 VM에서 기본값으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-121">The following example restarts the SSH daemon and resets the SSH configuration to default values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="4680d-122">사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4680d-122">Create a user</span></span>
<span data-ttu-id="4680d-123">다음 예제에서는 VM `myVM`에서 인증을 위해 SSH 키를 사용하여 사용자 `myNewUser`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-123">The following example creates a user named `myNewUser` using an SSH key for authentication on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="4680d-124">사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="4680d-124">Delete a user</span></span>
<span data-ttu-id="4680d-125">다음 예제에서는 VM `myVM`에서 사용자 `myNewUser`을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-125">The following example deletes a user named `myNewUser` on the VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-the-vmaccess-extension"></a><span data-ttu-id="4680d-126">JSON 파일 및 VMAccess 확장 사용</span><span class="sxs-lookup"><span data-stu-id="4680d-126">Use JSON files and the VMAccess Extension</span></span>
<span data-ttu-id="4680d-127">다음 예제에서는 원시 JSON 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-127">The following examples use raw JSON files.</span></span> <span data-ttu-id="4680d-128">[az vm extension set](/cli/azure/vm/extension#set)을 사용하여 JSON 파일을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-128">Use [az vm extension set](/cli/azure/vm/extension#set) to then call your JSON files.</span></span> <span data-ttu-id="4680d-129">이러한 JSON 파일은 Azure 템플릿에서도 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="4680d-130">사용자 액세스 다시 설정</span><span class="sxs-lookup"><span data-stu-id="4680d-130">Reset user access</span></span>
<span data-ttu-id="4680d-131">Linux VM의 루트에 액세스할 수 없게 된 경우 VMAccess 스크립트를 시작하여 사용자의 SSH 키 또는 암호를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-131">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset a user's SSH key or password.</span></span>

<span data-ttu-id="4680d-132">사용자의 SSH 공개 키를 다시 설정하려면 파일 `reset_ssh_key.json`을 만들고 다음 형식으로 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-132">To reset the SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in the following format.</span></span> <span data-ttu-id="4680d-133">`username` 및 `ssh_key` 매개 변수에 대해 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-133">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="4680d-134">다음을 사용하여 VMAccess 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-134">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="4680d-135">사용자 암호를 다시 설정하려면 파일 `reset_user_password.json`을 만들고 다음 형식으로 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-135">To reset a user password, create a file named `reset_user_password.json` and add settings in the following format.</span></span> <span data-ttu-id="4680d-136">`username` 및 `password` 매개 변수에 대해 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-136">Substitute your own values for the `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="4680d-137">다음을 사용하여 VMAccess 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-137">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="4680d-138">SSH 다시 시작</span><span class="sxs-lookup"><span data-stu-id="4680d-138">Restart SSH</span></span>
<span data-ttu-id="4680d-139">SSH 디먼을 다시 시작하고 SSH 구성을 기본값으로 다시 설정하려면 파일 `reset_sshd.json`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-139">To restart the SSH daemon and reset the SSH configuration to default values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="4680d-140">다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-140">Add the following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="4680d-141">다음을 사용하여 VMAccess 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-141">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="4680d-142">사용자 관리</span><span class="sxs-lookup"><span data-stu-id="4680d-142">Manage users</span></span>

<span data-ttu-id="4680d-143">인증을 위해 SSH 키를 사용하는 사용자를 만들려면 파일 `create_new_user.json`을 만들고 다음 형식으로 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-143">To create a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in the following format.</span></span> <span data-ttu-id="4680d-144">`username` 및 `ssh_key` 매개 변수에 대해 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-144">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="4680d-145">다음을 사용하여 VMAccess 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-145">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="4680d-146">사용자를 삭제하려면 파일 `delete_user.json`을 만들고 다음 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-146">To delete a user, create a file named `delete_user.json` and add the following content.</span></span> <span data-ttu-id="4680d-147">`remove_user` 매개 변수에 대해 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-147">Substitute your own value for the `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="4680d-148">다음을 사용하여 VMAccess 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-148">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-the-disk"></a><span data-ttu-id="4680d-149">디스크 확인 또는 복구</span><span class="sxs-lookup"><span data-stu-id="4680d-149">Check or repair the disk</span></span>
<span data-ttu-id="4680d-150">VMAccess를 사용하여 Linux VM에 추가한 디스크를 확인하고 복구할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-150">Using VMAccess you can also check and repair a disk that you added to the Linux VM.</span></span>

<span data-ttu-id="4680d-151">디스크를 확인한 다음 복구하려면 파일 `disk_check_repair.json`을 만들고 다음 형식으로 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-151">To check and then repair the disk, create a file named `disk_check_repair.json` and add settings in the following format.</span></span> <span data-ttu-id="4680d-152">`repair_disk`의 이름에 대해 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-152">Substitute your own value for the name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="4680d-153">다음을 사용하여 VMAccess 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-153">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="4680d-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4680d-154">Next steps</span></span>
<span data-ttu-id="4680d-155">실행 중인 Linux VM에서 변경을 수행하는 한 가지 방법은 Azure VMAccess 확장을 사용하여 Linux를 업데이트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-155">Updating Linux using the Azure VMAccess Extension is one method to make changes on a running Linux VM.</span></span> <span data-ttu-id="4680d-156">cloud-init 및 Azure Resource Manager 템플릿 등의 도구를 사용하여 부팅 시 Linux VM을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4680d-156">You can also use tools like cloud-init and Azure Resource Manager templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="4680d-157">Linux용 가상 컴퓨터 확장 및 기능</span><span class="sxs-lookup"><span data-stu-id="4680d-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="4680d-158">Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="4680d-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="4680d-159">cloud-init를 사용하여 생성 중인 Linux VM 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4680d-159">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md)

