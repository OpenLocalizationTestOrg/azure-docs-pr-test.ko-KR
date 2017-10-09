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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에 Azure CLI 1.0 hello로 VMAccess 확장을 환영
이 문서에서는 어떻게 toouse Azure VMAcesss 확장 toocheck hello 또는 디스크 복구, 사용자 액세스를 다시 설정, 사용자 계정 관리 또는 Linux에서 hello SSHD 구성을 다시 설정 합니다. hello 문서에는 다음 사항이 필요합니다.

* Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))
* hello [Azure CLI](../../cli-install-nodejs.md) 로그인 한 `azure login`합니다.
* hello Azure CLI *에 있어야* Azure Resource Manager 모드 `azure config mode arm`합니다.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-commands)– 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="quick-commands"></a>빠른 명령
두 가지 방법으로 toouse Linux Vm에서 VMAccess 가지가 있습니다.

* Hello Azure CLI 1.0 및 hello를 사용 하 여 매개 변수가 필요 합니다.
* VMAccess에서 처리한 후 관련 작업을 수행하는 원시 JSON 파일 사용

Hello 빠른 명령 섹션에 대 한 하겠습니다 toouse hello Azure CLI 1.0 `azure vm reset-access` 메서드. Hello 다음 명령 예에서는 "예" hello 값을 가진 사용자가 자신의 환경에서 포함 하는 hello 값을 대체 합니다.

## <a name="create-a-resource-group-and-linux-vm"></a>리소스 그룹 및 Linux VM 만들기
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Debian VM 만들기
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

## <a name="reset-root-password"></a>루트 암호 다시 설정
tooreset hello 루트 암호:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>SSH 키 다시 설정
루트가 아닌 사용자의 tooreset hello SSH 키:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>사용자 만들기
toocreate 사용자:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>사용자 제거
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>SSHD 재설정
tooreset hello SSHD 구성:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>자세한 연습
### <a name="vmaccess-defined"></a>VMAccess 정의:
Linux VM의 디스크 hello이 오류가 표시 됩니다. 어떻게 하 든 Linux VM에 대 한 hello 루트 암호를 재설정 하거나 실수로 SSH 개인 키를 삭제 합니다. Hello 데이터 센터의 hello 일 후에 다시이 경우 toodrive 발생 해야 하는 다음 hello KVM tooget hello 서버 콘솔을 엽니다. Hello Azure VMAccess 확장 콘솔 tooreset 액세스 tooLinux hello 하면 tooaccess 하거나 디스크 수준 유지 관리를 수행할 수 있도록 KVM 스위치 라고 생각 됩니다.

Hello에 대 한 자세한 연습에서는 toouse hello 긴 형식의 원시 JSON 파일을 사용 하 여 VMAccess 하겠습니다.  이러한 VMAccess JSON 파일은 Azure 템플릿에서도 호출할 수 있습니다.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Linux VM의 VMAccess toocheck 또는 복구 hello 디스크를 사용 하 여
VMAccess를 사용 하 여 할 수 있는 한 fsck Linux VM에서 hello 디스크에서 실행 합니다.  VMAccess를 사용하여 디스크 검사와 디스크 복구를 수행할 수도 있습니다.

toocheck, 및 복구 hello 디스크가 VMAccess 스크립트를 사용합니다.

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>VMAccess tooreset 사용자 액세스 tooLinux를 사용 하 여
Linux VM에 대 한 액세스 tooroot를 잃어버린 경우 VMAccess 스크립트 tooreset hello 루트 암호를 시작할 수 있습니다.

tooreset hello 루트 암호를이 VMAccess 스크립트 사용:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

루트가 아닌 사용자의 tooreset hello SSH 키에는이 VMAccess 스크립트 사용:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Linux에서 VMAccess toomanage 사용자 계정을 사용 하 여
VMAccess 없이 로그인 하 고 sudo 또는 hello 루트 계정을 사용 하 여 Linux VM에 사용 되는 toomanage 사용자 일 수 있는 Python 스크립트입니다.

toocreate 사용자를이 VMAccess 스크립트를 사용 합니다.

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete 사용자를이 VMAccess 스크립트를 사용 합니다.

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>VMAccess tooreset hello SSHD 구성을 사용 하 여
변경 내용 toohello Linux Vm SSHD 구성과 hello 변경 내용 확인 되기 전에 닫기 hello SSH 연결을 만들면 연결할 수 없을 수도 SSH'ing에서 다시 합니다.  VMAccess 사용된 tooreset hello SSHD 구성 뒤로 tooa로 성공한 구성 SSH를 통해 로그인 하지 않고 될 수 있습니다.

이 VMAccess 스크립트를 사용 하는 tooreset hello SSHD 구성:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Hello VMAccess 스크립트를 실행 합니다.

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>다음 단계
Linux 업데이트 되어 실행 중인 Linux VM에 하나의 메서드 toomake 변경 내용을 Azure VMAccess 확장을 사용 하 여 합니다.  작업을 부팅 시 Linux VM 클라우드 init 및 Azure 템플릿 toomodify와 같은 도구도 사용할 수도 있습니다.

[가상 컴퓨터 확장 및 기능 정보](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Linux VM 확장을 사용하여 Azure Resource Manager 템플릿 작성](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[클라우드 init toocustomize Linux VM을 만드는 동안 사용 하 여](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

