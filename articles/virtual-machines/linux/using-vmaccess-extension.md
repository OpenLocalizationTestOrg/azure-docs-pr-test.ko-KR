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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Linux Vm에 Azure CLI 2.0 hello로 VMAccess 확장을 환영
Linux VM의 디스크 hello이 오류가 표시 됩니다. 어떻게 하 든 Linux VM에 대 한 hello 루트 암호를 재설정 하거나 실수로 SSH 개인 키를 삭제 합니다. Hello 데이터 센터의 hello 일 후에 다시이 경우 toodrive 발생 해야 하는 다음 hello KVM tooget hello 서버 콘솔을 엽니다. Hello Azure VMAccess 확장 콘솔 tooreset 액세스 tooLinux hello 하면 tooaccess 하거나 디스크 수준 유지 관리를 수행할 수 있도록 KVM 스위치 라고 생각 됩니다.

이 문서에서는 어떻게 toouse Azure VMAccess 확장 toocheck hello 또는 디스크 복구, 사용자 액세스를 다시 설정, 사용자 계정 관리 또는 Linux에서 hello SSH 구성을 다시 설정 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.


## <a name="ways-toouse-hello-vmaccess-extension"></a>같은 방법으로 toouse hello VMAccess 확장
두 가지 방법으로 Linux Vm에서 VMAccess 확장 hello를 사용할 수 있습니다.

* Hello Azure CLI 2.0 및 필요한 hello 매개 변수를 사용 합니다.
* [원시 JSON을 사용 하 여 해당 hello VMAccess 확장 프로세스 파일](#use-json-files-and-the-vmaccess-extension) 한 후에 작업을 수행 합니다.

다음 예제에서 사용 hello [az vm 사용자](/cli/azure/vm/user) 명령입니다. 이 단계는 tooperform, 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.

## <a name="reset-ssh-key"></a>SSH 키 다시 설정
hello 다음 예제에서는 재설정 hello 사용자에 대 한 SSH 키 hello `azureuser` hello 라는 VM에서 `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>암호 재설정
hello 다음 예제에서는 암호를 다시 설정 hello hello 사용자에 대 한 `azureuser` hello 라는 VM에서 `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>SSH 다시 시작
hello 다음 예제에서는 다시 시작 hello SSH 디먼이 및 재설정 hello 라는 VM에서 SSH 구성 toodefault 값 `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>사용자 만들기
hello 다음 예제에서는 라는 사용자 `myNewUser` hello 라는 VM에서 인증을 위해 SSH 키를 사용 하 여 `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>사용자 삭제
hello 다음 예에서는 삭제 라는 사용자 `myNewUser` hello 라는 VM에서 `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>JSON 파일을 사용 하 고 hello VMAccess 확장
다음 예제는 hello 원시 JSON 파일을 사용 합니다. 사용 하 여 [az vm 확장 집합](/cli/azure/vm/extension#set) toothen JSON 파일을 호출 합니다. 이러한 JSON 파일은 Azure 템플릿에서도 호출할 수 있습니다. 

### <a name="reset-user-access"></a>사용자 액세스 다시 설정
Linux VM에 대 한 액세스 tooroot를 잃어버린 경우에 사용자의 SSH 키 또는 암호 VMAccess 스크립트 tooreset를 시작할 수 있습니다.

사용자, tooreset hello SSH 공개 키 파일을 만듭니다 `reset_ssh_key.json` 및 형식에 따라 hello에 설정을 추가 합니다. Hello에 대 한 고유한 값으로 대체 `username` 및 `ssh_key` 매개 변수:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

사용자 암호를 tooreset 라는 파일을 만들어 `reset_user_password.json` 및 형식에 따라 hello에 설정을 추가 합니다. Hello에 대 한 고유한 값으로 대체 `username` 및 `password` 매개 변수:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>SSH 다시 시작
SSH 디먼이 hello 및 hello SSH 구성 toodefault 값 다시 설정, 라는 파일을 만들어 toorestart `reset_sshd.json`합니다. Hello 다음 콘텐츠를 추가 합니다.

```json
{
  "reset_ssh": true
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>사용자 관리

인증을 위해 SSH 키를 사용 하는 사용자 toocreate 라는 파일을 만들어 `create_new_user.json` 형식에 따라 hello에 설정을 추가 하 고 있습니다. Hello에 대 한 고유한 값으로 대체 `username` 및 `ssh_key` 매개 변수:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

사용자를 toodelete 라는 파일을 만들어 `delete_user.json` hello 다음 콘텐츠를 추가 합니다. Hello에 대 한 고유한 값을 대체 `remove_user` 매개 변수:

```json
{
  "remove_user":"myNewUser"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>확인 또는 복구 hello 디스크
VMAccess를 사용 하 여 확인 및 복구 toohello Linux VM을 추가 하면 디스크 수도 있습니다.

toocheck 및 복구 hello 디스크 라는 파일을 만들어 `disk_check_repair.json` 및 형식에 따라 hello에 설정을 추가 합니다. Hello 이름에 대 한 고유한 값을 대체 `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>다음 단계
Linux를 업데이트 하면 실행 중인 Linux VM에 하나의 메서드 toomake 변경은 hello Azure VMAccess 확장을 사용 하 여. 작업을 부팅 시 Linux VM 클라우드 init 및 Azure 리소스 관리자 템플릿 toomodify와 같은 도구도 사용할 수도 있습니다.

[Linux용 가상 컴퓨터 확장 및 기능](extensions-features.md)

[Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[클라우드 init toocustomize Linux VM을 만드는 동안 사용 하 여](using-cloud-init.md)

