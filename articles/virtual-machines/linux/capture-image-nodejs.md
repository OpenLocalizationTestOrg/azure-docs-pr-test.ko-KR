---
title: "템플릿으로 Azure Linux VM toouse aaaCapture | Microsoft Docs"
description: "자세한 내용은 방법 toocapture Linux 기반 Azure 가상 컴퓨터 (VM) hello Azure 리소스 관리자 배포 모델을 사용 하 여 만든 이미지를 일반화 하 고 있습니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Azure에서 실행되는 Linux 가상 컴퓨터 캡처하기
이 문서 toogeneralize hello 단계를 수행 하 고 hello 리소스 관리자 배포 모델에서 Azure Linux 가상 컴퓨터 (VM)를 캡처하십시오. Hello VM을 일반화 하면 개인 계정 정보를 제거 하 고 hello VM toobe 이미지 형식으로 사용 되는 준비 합니다. 다음 일반화 된 가상 하드 디스크 (VHD) hello OS, 연결 된 데이터 디스크에 대 한 Vhd의 이미지 캡처 및 [리소스 관리자 템플릿](../../azure-resource-manager/resource-group-overview.md) 새 VM 배포에 대 한 합니다. 이 문서는 관리 되지 않는 디스크를 사용 하는 VM에 대 한 Azure CLI 1.0 hello로 이미지 toocapture VM 방법을 자세히 설명 합니다. 수도 있습니다 [Azure CLI 2.0 hello로 Azure 관리 되는 디스크를 사용 하는 VM 캡처](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 관리 되는 디스크 hello Azure 플랫폼에서 처리 되 고 모든 준비 단계 또는 위치 toostore 필요 하지 않은 하 합니다. 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요. 

toocreate hello 이미지를 사용 하 여 Vm 각 새 VM에 대 한 네트워크 리소스를 설정 하 고 hello 서식 파일 (JavaScript Object Notation 또는 JSON 파일) toodeploy VHD 이미지를 캡처한 hello에서 사용 합니다. 이러한 방식으로 현재 소프트웨어 구성 hello Azure Marketplace에서에서 이미지를 사용 하는 비슷한 toohello 방식으로 사용 하 여 VM을 복제할 수 있습니다.

> [!TIP]
> 백업 또는 디버깅에 대 한 toocreate 특수 상태 기존 Linux VM의 복사본을 원하는 경우 참조 [Azure에서 실행 중인 Linux 가상 컴퓨터의 복사본을 만들고](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 온-프레미스 VM에서 Linux VHD tooupload 참조 [업로드 하 고 사용자 지정 디스크 이미지에서 Linux VM을 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.  

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#before-you-begin) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

## <a name="before-you-begin"></a>시작하기 전에
Hello 다음 필수 구성 요소를 충족 하는지 확인 합니다.

* **Azure VM hello 리소스 관리자 배포 모델에서 만든** -Linux VM을 만들지 않은 경우에 hello을 사용할 수 있습니다 [포털](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), 또는 [리소스 관리자 서식 파일](create-ssh-secured-vm-from-template.md)합니다. 
  
    필요에 따라 VM hello를 구성 합니다. 예를 들어 [데이터 디스크를 추가하고](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), 업데이트를 적용하고, 응용 프로그램을 설치합니다. 
* **Azure CLI** -설치 hello [Azure CLI](../../cli-install-nodejs.md) 로컬 컴퓨터에 있습니다.

## <a name="step-1-remove-hello-azure-linux-agent"></a>1 단계: hello Azure Linux 에이전트 제거
먼저, 실행 하 여 hello **waagent** hello로 명령을 **프로 비전 해제** hello Linux VM에 대 한 매개 변수입니다. 이 명령은 파일 및 데이터 toomake hello VM 일반화 하는 것에 대 한 준비를 삭제합니다. 자세한 내용은 참조 hello [Azure Linux 에이전트 사용자 가이드](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

1. Tooyour SSH 클라이언트를 사용 하 여 Linux VM을 연결 합니다.
2. Hello SSH 창의 hello 다음 명령을 입력 합니다.
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > 만 toocapture 이미지 형식으로 하려는 VM에서이 명령을 실행 합니다. Hello 이미지가 중요 한 정보를 모두 선택 취소 되어 또는 재배포를 위해 적합 한 보장 하지 않습니다.
 
3. 형식 **y** toocontinue 합니다. Hello를 추가할 수 있습니다 **-강제로** 매개 변수 tooavoid이 확인 단계입니다.
4. Hello 명령이 완료 된 후 입력 **종료**합니다. 이 단계는 hello SSH 클라이언트를 닫습니다.

## <a name="step-2-capture-hello-vm"></a>2 단계: hello VM 캡처
Azure CLI toogeneralize hello를 사용 하 고 hello VM을 캡처하십시오. Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 **myResourceGroup**, **myVnet**, **myVM**이 포함됩니다.

1. 로컬 컴퓨터에서 열고 hello Azure CLI 및 [로그인 tooyour Azure 구독](../../xplat-cli-connect.md)합니다. 
2. Resource Manager 모드에 있는지 확인합니다.
   
    ```azurecli
    azure config mode arm
    ```
3. 다음 명령을 hello를 사용 하 여 이미 프로 비전 된 VM hello를 종료 합니다.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. 다음 명령을 hello로 hello VM 일반화 합니다.
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Hello µ ë ´ **azure vm 캡처** 캡처하 hello VM 명령입니다. 다음 예제는 hello, Vhd와 캡처됩니다 hello 이미지 이름을로 시작 **MyVHDNamePrefix**, 및 hello **-t** 경로 toohello 서식 파일을 지정 하는 옵션 **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > hello 이미지 VHD 파일에서 원본 VM hello 동일한 저장소 계정을 사용 하는 hello 기본적으로 작성 합니다. 사용 하 여 hello *동일한 저장소 계정* toostore hello hello 이미지에서 만드는 모든 새 Vm에 대 한 Vhd입니다. 

6. 캡처된 이미지에 대 한 텍스트 편집기에서 열고 hello JSON 서식 파일의 toofind hello 위치입니다. Hello에 **storageProfile**, hello **uri** 의 hello **이미지** hello에 **시스템** 컨테이너입니다. 예를 들어 hello hello OS 디스크 이미지의 URI는 비슷한 너무`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>3 단계: hello 캡처된 이미지에서 VM 만들기
이제 hello 이미지를 사용 하 여 템플릿 toocreate Linux VM을 사용 합니다. 이러한 단계는 toouse Azure CLI hello 하는 방법을 보여 줍니다 하 고 새 가상 네트워크에 대 한 VM toocreate hello 캡처한 JSON 파일 템플릿의 hello 합니다.

### <a name="create-network-resources"></a>네트워크 리소스 만들기
toouse hello 서식 파일을 먼저 가상 네트워크 및 NIC를 tooset 새 VM에 대 한 합니다. VM 이미지가 저장 되어 있는 hello 위치에 이러한 리소스에 대 한 리소스 그룹을 만드는 것이 좋습니다. 다음, 리소스 및 적절 한 Azure 위치 (이러한 명령에 "centralus")에 대 한 이름으로 대체 비슷한 toohello 명령을 실행 합니다.

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Hello hello NIC의 Id 가져오기
캡처 중에 저장 하는 JSON hello를 사용 하 여 hello 이미지에서 VM toodeploy 해야 hello hello NIC.의 Id Hello 다음 명령을 실행 하 여 가져올:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

hello **Id** hello에서 출력은 너무`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>VM 만들기
이제 실행된 hello 다음 명령은 toocreate hello에서 VM VM 이미지를 캡처합니다. 사용 하 여 hello **-f** 매개 변수 toospecify hello 경로 toohello 템플릿 JSON 파일 저장 합니다.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

Hello 명령 출력에 새 VM 이름, hello 관리자 사용자 이름 및 암호를 입력 정보 요청된 toosupply 하 고 hello hello 이전에 만든 NIC의 Id입니다.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

다음 예제는 hello 성공적인 배포에 대 한 표시를 보여 줍니다.

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Hello 배포 확인
이제 SSH toohello 가상 컴퓨터 tooverify hello 배포 및 시작에 사용 하 여 만든 새 VM hello 합니다. SSH 통해 tooconnect hello hello 다음 명령을 실행 하 여 만든 VM의 hello IP 주소를 찾기:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

hello 공용 IP 주소는 hello 명령 출력에 표시 됩니다. 기본적으로 포트 22에서 SSH 통해 Linux VM toohello를 연결합니다.

## <a name="create-additional-vms"></a>추가 VM 만들기
사용 하 여 hello 캡처된 이미지와 템플릿 toodeploy hello 단계를 사용 하 여 hello 섹션 앞에 추가 Vm입니다. 퀵 스타트 템플릿을 사용 하 여 또는 실행 hello hello 이미지에서 다른 옵션 toocreate Vm 포함 **azure vm 만들기** 명령입니다.

### <a name="use-hello-captured-template"></a>Hello 캡처된 템플릿을 사용 하 여
toouse hello 캡처된 이미지와 서식 파일 (hello 앞 섹션에서에서 자세히 설명) 다음이 단계를 수행 하십시오.

* VM 이미지 hello에 있는지 확인 VM의 VHD를 호스팅하는 동일한 저장소 계정입니다.
* Hello 템플릿 JSON 파일을 복사 하 고 hello 새 VM의 VHD (또는 Vhd) hello OS 디스크에 대 한 고유한 이름을 지정 합니다. 예를 들어 hello에에서 **storageProfile**아래에서 **vhd**에 **uri**, hello에 대 한 고유한 이름을 지정 **osDisk** 비슷한 VHD 너무`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* 같거나 다른 가상 네트워크를 어느 hello에서 NIC를 만듭니다.
* 수정 하는 hello 템플릿 JSON 파일을 사용 하는 hello 가상 네트워크를 설정 하는 hello 리소스 그룹에 배포를 만듭니다.

### <a name="use-a-quickstart-template"></a>빠른 시작 템플릿 사용
Hello 네트워크를 자동으로 만들 때 VM hello 이미지에서 설정 하려는 경우에 서식 파일에 이러한 리소스를 지정할 수 있습니다. 예를 들어 hello 참조 [사용자 이미지에서 vm 101 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) GitHub에서 합니다. 이 템플릿은 사용자 지정 이미지 및 hello 필요한 가상 네트워크, 공용 IP 주소 및 NIC 리소스에서 VM을 만듭니다. 참조에 대 한 hello Azure 포털에서에서 hello 템플릿을 사용 하는 연습은 [어떻게 toocreate 리소스 관리자 템플릿을 사용 하 여 사용자 지정 이미지에서 가상 컴퓨터](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/)합니다.

### <a name="use-hello-azure-vm-create-command"></a>사용 하 여 hello azure vm 만들기 명령
일반적으로 가장 쉬운 toouse 리소스 관리자 템플릿 toocreate hello 이미지에서 VM 됩니다. 그러나 hello VM을 만들 수 *명령적으로* hello를 사용 하 여 **azure vm 만들기** hello로 명령을 **-Q** (**-이미지 urn**) 매개 변수 . Hello이이 메서드를 사용 하는 경우 변수도 전달 **-d** (**-os 디스크 vhd**)에 대 한 OS hello.vhd 파일의 매개 변수 toospecify hello 위치에 새 VM hello 합니다. 이 파일의 hello 이미지 VHD 파일이 저장 된 hello 저장소 계정 hello vhd 컨테이너에 있어야 합니다. 복사본 hello에 대 한 VHD를 hello 명령 hello 새 VM 자동으로 toohello **vhd** 컨테이너입니다.

실행 하기 전에 **azure vm 만들기** hello 이미지 완료 단계를 수행 하는 hello:

1. 리소스 그룹을 만들거나 hello 배포에 대 한 기존 리소스 그룹을 식별 합니다.
2. 만들 공용 IP 주소 리소스와 NIC 리소스에 대 한 새 VM hello 합니다. 단계 toocreate 가상 네트워크, 공용 IP 주소 및 NIC hello CLI를 사용 하 여이 문서의 앞부분에서 참조 합니다. (**azure vm 만들기** NIC를 만들 수도 있지만 가상 네트워크 및 서브넷에 대 한 toopass 추가 매개 변수를 사용 해야 합니다.)

Tooboth hello 새 운영 체제 VHD 파일 및 이미지를 기존 hello Uri를 전달 하는 명령을 실행 합니다. 이 예제에서는 크기를 Standard_A1 VM 만들어집니다 hello 미국 동부 지역에 있습니다.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

추가적인 명령 옵션은 `azure help vm create`을 실행합니다.

## <a name="next-steps"></a>다음 단계
toomanage hello CLI가 있는 Vm의을 참조 hello [배포 및 Azure 리소스 관리자 템플릿을 사용 하 여 가상 컴퓨터를 관리 하 고 Azure CLI hello](create-ssh-secured-vm-from-template.md)합니다.

