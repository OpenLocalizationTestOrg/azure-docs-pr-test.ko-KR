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
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>RedHat Linux VM tooan Azure Active Directory 도메인 서비스에 가입

이 문서에서는 toojoin Red Hat Enterprise Linux (RHEL) 7 가상 컴퓨터 tooan Azure Active Directory 도메인 서비스 (AADDS) 도메인을 관리 하는 방법을 보여 줍니다.  hello 요구 사항은 같습니다.

- [Azure 계정](https://azure.microsoft.com/pricing/free-trial/)

- [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md)

- [Azure Active Directory Domain Services DC](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>빠른 명령

_모든 예제를 고유한 설정으로 바꿉니다._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Hello azure cli tooclassic 배포 모드를 전환 합니다.

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>RHEL 버전 및 이미지 검색

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Redhat Linux VM 만들기

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

### <a name="ssh-toohello-vm"></a>SSH toohello VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>YUM 패키지 업데이트

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>필요한 패키지 설치

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

이제 필요한 hello 패키지 hello Linux 가상 컴퓨터에 설치 되 면 다음 태스크에서는 hello입니다 toojoin hello 가상 컴퓨터 toohello 관리 되는 도메인.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Hello AAD 도메인 서비스에 대 한 관리 되는 도메인 검색

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>kerberos 초기화

Toohello AAD ' DC Administrators' 그룹에 속한 사용자가을 지정 했는지 확인 합니다. 이러한 사용자만 컴퓨터 toohello 관리 되는 도메인에 가입할 수 있습니다.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Hello 컴퓨터 toohello 도메인에 가입

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>도메인에 가입된 toohello hello 컴퓨터 확인

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>다음 단계

* [Azure에서 주문형 Red Hat Enterprise Linux VM에 대한 RHUI(Red Hat Update Infrastructure)](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Resource Manager에서 가상 컴퓨터에 대한 Key Vault 설정](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [배포 하 고 hello Azure CLI 및 Azure 리소스 관리자 템플릿을 사용 하 여 가상 컴퓨터를 관리 합니다.](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
