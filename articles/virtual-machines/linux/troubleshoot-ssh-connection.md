---
title: "aaaTroubleshoot SSH 연결 문제 tooan Azure VM | Microsoft Docs"
description: "어떻게 tootroubleshoot 발급 'SSH 연결을 실패 했습니다.' 또는 'SSH 연결을 거부 했습니다.'와 같은 Azure VM에 대 한 Linux를 실행 합니다."
keywords: "ssh 연결 거부, ssh 오류, azure ssh, SSH 연결 실패"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>SSH 연결 tooan Azure Linux VM에 실패 하면 out, 오류 또는 거부 되었습니다. 문제 해결
SSH 연결 실패, SSH (보안 셸) 오류가 발생 하면 또는 SSH 거부 되었습니다. tooconnect tooa Linux 가상 컴퓨터 (VM)를 할 때 다양 한 이유가 있습니다. 이 문서에서는 찾기 및 올바른 hello 문제입니다. Linux tootroubleshoot에 hello Azure 포털, Azure CLI 또는 VM 액세스 확장을 사용할 수 있으며 연결 문제를 해결할 수 있습니다.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure 및 스택 오버플로 포럼 hello](http://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](http://azure.microsoft.com/support/options/) 선택 **지원을 받는**합니다. Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](http://azure.microsoft.com/support/faq/)합니다.

## <a name="quick-troubleshooting-steps"></a>빠른 문제 해결 단계
각 문제 해결 단계를 수행한 후 toohello VM을 다시 연결을 시도 합니다.

1. Hello SSH 구성을 다시 설정 합니다.
2. Hello hello 사용자 자격 증명 다시 설정 합니다.
3. Hello 확인 [네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md) 규칙 SSH 트래픽을 허용 합니다.
   * 네트워크 보안 그룹 규칙 (기본적으로 TCP 포트 22) toopermit SSH 트래픽 있는지 확인 하십시오.
   * Azure Load Balancer를 사용하지 않고 포트 리디렉션/매핑을 사용할 수 없습니다.
4. Hello 확인 [VM 리소스 상태](../../resource-health/resource-health-overview.md)합니다. 
   * 해당 hello VM 확인 정상인로 보고서 사용.
   * 부트 진단이 사용 하도록 설정 하는 경우 VM hello hello 로그에 있는 부팅 오류를 보고 하지 않는 확인 합니다.
5. Hello VM을 다시 시작 합니다.
6. Hello VM을 다시 배포 합니다.

자세한 문제 해결 단계와 설명이 필요한 경우 계속 읽어보세요.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>사용할 수 있는 방법 tootroubleshoot SSH 연결 문제
자격 증명 또는 hello 메서드를 다음 중 하나를 사용 하 여 SSH 구성을 다시 설정할 수 있습니다.

* [Azure 포털](#use-the-azure-portal) -tooquickly 해야 할 경우 좋은 hello SSH 구성을 또는 SSH 키를 다시 설정 하 고 설치 된 Azure 도구를 hello 하지 않습니다.
* [Azure CLI 2.0](#use-the-azure-cli-20) -이미 실행 중인 hello 명령줄에 신속 하 게 hello SSH 구성을 다시 설정 또는 자격 증명 하는 경우. Hello를 사용할 수도 있습니다 [Azure CLI 1.0](#use-the-azure-cli-10)
* [Azure 작업에서는 VMAccessForLinux 확장](#use-the-vmaccess-extension) -만들고 json 정의 파일 tooreset hello SSH 구성 또는 사용자 자격 증명을 다시 사용 합니다.

각 문제 해결 단계 후 tooyour VM을 다시 연결 하십시오. 여전히 연결할 수 없는 경우 hello 다음 단계를 시도 합니다.

## <a name="use-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여
hello Azure 포털 로컬 컴퓨터에 다양 한 도구를 설치 하지 않고 신속 하 게 tooreset hello는 SSH 구성 이나 사용자 자격 증명을 제공 합니다.

Hello Azure 포털에서에서 VM을 선택 합니다. Toohello 아래로 스크롤하여 **지원 + 문제 해결** 선택한 섹션 **암호 재설정** hello 다음 예제와 같이:

![Hello Azure 포털에서에서 자격 증명 또는 SSH 구성을 다시 설정](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Hello SSH 구성을 다시 설정
첫 번째 단계로, 선택 `Reset configuration only` hello에서 **모드** 드롭 다운 메뉴 hello 스크린 샷, 이전에 클릭 hello **재설정** 단추입니다. 이 작업 완료 되 면 tooaccess VM 다시 시도 합니다.

### <a name="reset-ssh-credentials-for-a-user"></a>사용자에 대한 SSH 자격 증명 다시 설정
기존 사용자의 tooreset hello 자격 증명 중 하나를 선택 합니다. `Reset SSH public key` 또는 `Reset password` hello에서 **모드** hello 스크린 샷 앞에서 같이 드롭 다운 메뉴. Hello 사용자 이름 및 SSH 키 또는 새 암호를 지정 하 고 hello 클릭 **재설정** 단추입니다.

또한이 메뉴에서 VM hello에서 sudo 권한이 있는 사용자를 만들 수 있습니다. 새 사용자 이름 및 연결 된 암호 또는 SSH 키를 입력 하 고 클릭 hello **재설정** 단추입니다.

## <a name="use-hello-azure-cli-20"></a>Hello Azure CLI 2.0을 사용 하 여
아직 하지 않는 경우 hello를 최신 버전 설치 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.

만든 사용자 지정 Linux 디스크 이미지를 업로드 하는 경우 확인 되었는지 hello [Microsoft Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 2.0.5 버전 이상이 설치 되어 있습니다. 갤러리 이미지를 사용하여 만든 VM의 경우 이 액세스 확장이 이미 설치되어 자동으로 구성됩니다.

### <a name="reset-ssh-configuration"></a>SSH 구성 다시 설정
처음 시도 재설정 하는 중 hello SSH 구성 toodefault 값과 재부팅 중 이어서 hello SSH 서버 hello VM에서 할 수 있습니다. 이 변경 한다는 것 hello 사용자 계정 이름, 암호 또는 SSH 키 note 합니다.
hello 다음 예제에서는 [az vm 사용자 재설정-ssh](/cli/azure/vm/user#reset-ssh) hello 라는 VM에서 tooreset hello SSH 구성을 `myVM` 에서 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>사용자에 대한 SSH 자격 증명 다시 설정
hello 다음 예제에서는 [az vm 사용자 업데이트](/cli/azure/vm/user#update) tooreset hello에 대 한 자격 증명 `myUsername` toohello 값에 지정 된 `myPassword`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

SSH 키 인증을 사용 하는 경우 지정된 된 사용자에 대 한 hello SSH 키를 다시 설정할 수 있습니다. hello 다음 예제에서는 **az vm 집합-linux 사용자 액세스** tooupdate hello SSH 키에 저장 된 `~/.ssh/id_rsa.pub` 라는 hello 사용자에 대 한 `myUsername`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Hello VMAccess 확장을 사용 하 여
Linux 용 VM 액세스 확장 hello 아웃 toocarry 동작을 정의 하는 json 파일에서 읽습니다. 이러한 작업에는 SSHD 다시 설정, SSH 키를 다시 설정 또는 사용자 추가가 포함됩니다. Hello Azure CLI toocall hello VMAccess 확장을 계속 사용할 하지만 원하는 경우 여러 Vm 간에 hello json 파일을 재사용할 수입니다. 이 방법을 사용 하면 toocreate 주어진 시나리오에 대 한 다음 호출 수 있는 json 파일의 리포지토리입니다.

### <a name="reset-sshd"></a>SSHD 재설정
라는 파일을 만들어 `settings.json` 콘텐츠를 다음 hello로:

```json
{  
    "reset_ssh":"True"
}
```

Hello Azure CLI를 사용 하 여 다음 호출 hello `VMAccessForLinux` 확장 tooreset json 파일을 지정 하 여 SSHD 연결 합니다. hello 다음 예제에서는 [az vm 확장 집합](/cli/azure/vm/extension#set) hello 라는 VM에서 tooreset SSHD `myVM` 에서 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>사용자에 대한 SSH 자격 증명 다시 설정
SSHD toofunction 올바르게 나타나면 giver 사용자에 대 한 hello 자격 증명을 재설정할 수 있습니다. 사용자가 tooreset hello 암호 라는 파일을 만들어 `settings.json`합니다. hello 다음 예제에서는 다시 설정에 대 한 자격 증명 hello `myUsername` toohello 값에 지정 된 `myPassword`합니다. Hello 줄에 다음을 입력 하면 `settings.json` 고유한 값을 사용 하 여 파일:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

또는 사용자에 대 한 SSH 키 hello, 먼저 라는 파일을 만들어 tooreset `settings.json`합니다. hello 다음 예제에서는 다시 설정에 대 한 자격 증명 hello `myUsername` toohello 값에 지정 된 `myPassword`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다. Hello 줄에 다음을 입력 하면 `settings.json` 고유한 값을 사용 하 여 파일:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Json 파일을 만든 후 hello Azure CLI toocall hello를 사용 하 여 `VMAccessForLinux` 확장 tooreset json 파일을 지정 하 여 SSH 사용자 자격 증명입니다. hello 다음 예제에서는 재설정 hello 라는 VM에서 자격 증명 `myVM` 에서 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Hello Azure CLI 1.0을 사용 하 여
아직 없는 경우, [hello Azure CLI 1.0을 설치 하 고 tooyour Azure 구독 연결](../../cli-install-nodejs.md)합니다. 다음과 같이 Resource Manager 모드를 사용하는지 확인합니다.

```azurecli
azure config mode arm
```

만든 사용자 지정 Linux 디스크 이미지를 업로드 하는 경우 확인 되었는지 hello [Microsoft Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 2.0.5 버전 이상이 설치 되어 있습니다. 갤러리 이미지를 사용하여 만든 VM의 경우 이 액세스 확장이 이미 설치되어 자동으로 구성됩니다.

### <a name="reset-ssh-configuration"></a>SSH 구성 다시 설정
hello SSHD 구성 자체 잘못 구성 되었을 수 있습니다 또는 hello 서비스 오류가 발생 했습니다. SSHD toomake 자체 hello SSH 구성이 유효한 지 다시 설정할 수 있습니다. SSHD 재설정 hello 첫 번째 문제 해결 단계를 수행한 이어야 합니다.

hello 다음 예제에서는 재설정 라는 VM에서 SSHD `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다. 다음과 같이 고유한 VM 및 리소스 그룹 이름을 사용합니다.

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>사용자에 대한 SSH 자격 증명 다시 설정
SSHD toofunction 올바르게 나타나면 hello giver 사용자의 암호를 재설정할 수 있습니다. hello 다음 예제에서는 다시 설정에 대 한 자격 증명 hello `myUsername` toohello 값에 지정 된 `myPassword`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

SSH 키 인증을 사용 하는 경우 지정된 된 사용자에 대 한 hello SSH 키를 다시 설정할 수 있습니다. 다음 예에서는 업데이트 hello SSH 키에 저장 된 hello `~/.ssh/id_rsa.pub` 라는 hello 사용자에 대 한 `myUsername`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>VM 다시 시작
Hello SSH 구성 및 사용자 자격 증명 다시 설정, 또는 작업에 오류가 발생 하는 경우에 hello VM tooaddress 되었던 계산 문제를 다시 시작을 시도할 수 있습니다.

### <a name="azure-portal"></a>Azure portal
사용 하 여 VM toorestart hello Azure 포털에서 선택 하 고 VM hello **다시 시작** hello 다음 예제와 같이 단추:

![Hello Azure 포털에서에서 VM을 다시 시작](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
다음 예제에서는 다시 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
hello 다음 예제에서는 [az vm 다시 시작](/cli/azure/vm#restart) toorestart hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>VM 재배포
모든 기본 네트워킹 문제를 해결할 수도 있습니다는 Azure 내에서 VM tooanother 노드를 다시 배포할 수 있습니다. VM을 다시 배포 하는 방법에 대 한 정보를 참조 하십시오. [가상 컴퓨터 toonew Azure 노드를 다시 배포](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

> [!NOTE]
> 이 작업이 완료 되 면 임시 디스크 데이터 손실 되 고 hello 가상 컴퓨터와 연결 된 동적 IP 주소 업데이트 됩니다.
> 
> 

### <a name="azure-portal"></a>Azure portal
VM 및 toohello 아래로 스크롤하여 사용 하 여 VM tooredeploy hello Azure 포털에서 선택 **지원 + 문제 해결** 섹션. Hello 클릭 **재배포** hello 다음 예제와 같이 단추:

![Hello Azure 포털에서에서 VM을 다시 배포](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
다음 예에서는 재배포 시 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
다음 예에서는 사용 하 여 hello [az vm 재배포](/cli/azure/vm#redeploy) tooredeploy hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다. 다음과 같이 사용자 고유의 값을 사용합니다.

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Hello 클래식 배포 모델을 사용 하 여 만든 Vm
Hello 클래식 배포 모델을 사용 하 여 만든 Vm에 대해 이러한 단계 tooresolve hello 가장 일반적인 SSH 연결 실패를 시도 하십시오. 각 단계를 수행한 후 toohello VM을 다시 연결을 시도 합니다.

* Hello에서 원격 액세스를 다시 설정 [Azure 포털](https://portal.azure.com)합니다. 에 Azure 포털 hello VM을 선택 하 고 hello 클릭 **원격 다시 설정...**  단추입니다.
* Hello VM을 다시 시작 합니다. Hello에 [Azure 포털](https://portal.azure.com), VM을 선택 하 고 hello 클릭 **다시 시작** 단추입니다.
    
* Hello VM tooa 새 Azure 노드를 다시 배포 합니다. 방법에 대 한 정보에 대 한 VM을 tooredeploy 참조 [가상 컴퓨터 toonew Azure 노드를 다시 배포](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
  
    이 작업이 완료 되 면 임시 디스크 데이터 손실 되 고 hello 가상 컴퓨터와 연결 된 동적 IP 주소 업데이트 됩니다.
* Hello 지침에 따라 [어떻게 tooreset 암호 또는 Linux 기반 가상 컴퓨터에 대 한 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 에:
  
  * Hello 암호 또는 SSH 키를 다시 설정 합니다.
  * 새 *sudo* 사용자 계정을 만듭니다.
  * Hello SSH 구성을 다시 설정 합니다.
* 플랫폼 문제가 있는지에 대 한 hello VM의 리소스 상태를 확인 합니다.<br>
     VM을 선택하고 **설정** > **상태 확인**까지 아래로 스크롤합니다.

## <a name="additional-resources"></a>추가 리소스
* 인 경우 아직 못했습니다 tooSSH tooyour VM 후 다음 단계 이후 hello 참조 [자세한 문제 해결 단계](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview 추가 단계 tooresolve 문제입니다.
* 응용 프로그램 액세스 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [문제 해결 액세스 tooan 응용 프로그램이 Azure 가상 컴퓨터에서 실행 중인](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooreset 암호 또는 Linux 기반 가상 컴퓨터에 대 한 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

