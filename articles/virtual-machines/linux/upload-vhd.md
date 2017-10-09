---
title: "aaaUpload 또는 Azure CLI 2.0을 사용 하 여 사용자 지정 Linux VM 복사 | Microsoft Docs"
description: "업로드 하거나 복사할 hello 리소스 관리자 배포 모델 및 hello Azure CLI 2.0을 사용 하 여 사용자 지정된 가상 컴퓨터"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Azure CLI 2.0 hello로 사용자 지정 디스크에서 Linux VM 만들기

<!-- rename toocreate-vm-specialized -->

이 문서에서는 어떻게 tooupload 사용자 지정 된 가상 하드 디스크 (VHD) 또는 복사는 Azure에서 기존 VHD hello 사용자 지정 디스크에서 새 Linux 가상 컴퓨터 (Vm)를 만듭니다. 설치 하 고 Linux 배포판 tooyour 요구 사항을 구성 하 고 다음 해당 VHD를 사용 하 여 수 tooquickly 새 Azure 가상 컴퓨터를 만듭니다.

원할 경우 toocreate 여러 Vm 사용자 지정 된 디스크에서 VM 또는 VHD에서 이미지를 만들어야 합니다. 자세한 내용은 참조 [hello CLI를 사용 하 여 Azure VM의 사용자 지정 이미지를 만드는](tutorial-custom-images.md)합니다.

다음 두 가지 옵션을 사용할 수 있습니다.
* [VHD 업로드](#option-1-upload-a-specialized-vhd)
* [기존 Azure VM 복사](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>빠른 명령

사용 하 여 새 VM을 만들 때 [az vm 만들기](/cli/azure/vm#create) 사용자 지정 또는 특수 한 디스크에서 있습니다 **연결** hello 디스크 (--os-디스크 연결)는 사용자 지정 또는 마켓플레이스 이미지를 지정 하는 대신 (-이미지). hello 다음 예제에서는 V *myVM* hello를 사용 하 여 관리 하는 명명 된 디스크 *myManagedDisk* 사용자 지정 된 VHD에서 만든:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>요구 사항
toocomplete hello 필요한 다음 단계를:

* Azure에서 사용하기 위해 준비된 Linux 가상 컴퓨터 hello [준비 hello VM](#prepare-the-vm) 이 문서의 단원에 어떻게 toofind distro 설치에 대 한 정보 hello 필요 하면 toobe 수 tooconnect 및 Azure에서 제대로 VM toowork hello에 대 한 Azure Linux 에이전트 (waagent) SSH를 사용 하 여 tooit 합니다.
* 기존 VHD 파일 hello [Linux Azure 보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (참조 또는 [비 보증 배포판에 대 한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD 형식의 가상 디스크입니다. VM 및 VHD toocreate 존재 하는 여러 도구:
  * 설치 및 구성 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD 이미지 형식으로 처리 합니다. 필요한 경우 **qemu-img convert**를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.
  * 또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.

> [!NOTE]
> Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다. VM을 만들 때 hello 형식으로 VHD를 지정 합니다. 필요한 경우 사용 하 여 VHDX 디스크 tooVHD 변환할 수 있습니다 [qemu img 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 hello [CONVERT-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet. 또한 Azure에서는 tooconvert 필요 하므로 동적 Vhd를 업로드 이러한 디스크 toostatic Vhd 업로드 하기 전에. 와 같은 도구를 사용할 수 있습니다 [GO에 대 한 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure 업로드 프로세스 중 tooconvert 동적 디스크.
> 
> 


* Hello 최신 있는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *mydisks*가 포함됩니다.

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>Hello VM 준비

Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조). 다음 문서는 hello 어떻게 tooprepare hello Azure에서 지원 되는 다양 한 Linux 배포를 안내 합니다.

* [CentOS 기반 배포](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES 및 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [기타 - 보증되지 않는 배포](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

또한 hello를 참조 하십시오. [Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 보다 일반적인 방법에 대 한 azure Linux 이미지를 준비 합니다.

> [!NOTE]
> hello [Azure 플랫폼 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) tooVMs Linux를 실행 하 여 지원 버전에서 지정 된 대로 hello 구성 세부 정보를 사용 하는 분포를 지지 하는 hello 중 하나에 적용 됩니다. [Azure 보증에 Linux 분포](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
> 
> 

## <a name="option-1-upload-a-vhd"></a>옵션 1: VHD 업로드

로컬 컴퓨터에서 실행 중이거나 다른 클라우드에서 내보낸 사용자 지정된 VHD를 업로드할 수 있습니다. tooupload hello VHD tooa 저장소가 필요한 toouse hello VHD toocreate 새 Azure VM 계정 및 hello VHD에서에서 관리 되는 디스크를 만듭니다. 

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

사용자 지정 디스크를 업로드 하 고 Vm을 만들 하기 전에 먼저 toocreate 인 리소스 그룹과 [az 그룹 만들기](/cli/azure/group#create)합니다.

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치: [Azure 관리 되는 디스크 개요](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>저장소 계정 만들기

[az storage account create](/cli/azure/storage/account#create)를 사용하여 사용자 지정 디스크 및 VM에 대한 저장소 계정을 만듭니다. 

hello 다음 예제에서는 저장소 계정인 *mystorageaccount* 이전에 만든 hello 리소스 그룹에서:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>저장소 계정 키 나열
Azure는 각 저장소 계정에 대해 두 개의 512 비트 선택키를 생성합니다. 이러한 액세스 키에는 쓰기 작업을 수행 하는 같은 toohello 저장소 계정에 인증할 때 사용 됩니다. 에 대해 자세히 알아보세요 [toostorage 여기에 액세스 관리](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다. Hello 액세스 키를 보면 [az 저장소 계정 키 목록](/cli/azure/storage/account/keys#list)합니다.

만든 hello 저장소 계정에 대 한 hello 액세스 키 보기:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

hello 출력은 유사 합니다.

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
메모 **key1** 됩니다 사용할 toointeract hello 다음 단계에서 저장소 계정과 합니다.

### <a name="create-a-storage-container"></a>저장소 컨테이너 만들기
동일한 방식으로 다른 디렉터리 toologically 만드는 hello에 로컬 파일 시스템을 구성 하 고, 디스크 저장소 계정 tooorganize 내 컨테이너를 만들 합니다. 저장소 계정에 포함할 수 있는 컨테이너의 수에는 제한이 없습니다. [az storage container create](/cli/azure/storage/container#create)를 사용하여 컨테이너를 만듭니다.

hello 다음 예에서는 라는 컨테이너를 만듭니다 *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Hello VHD 업로드
이제 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 사용자 지정 디스크 이미지를 업로드합니다. 업로드하고 사용자 지정 디스크를 페이지 Blob으로 저장합니다.

다음 경로 toohello 로컬 컴퓨터에 사용자 지정 디스크 hello 및 액세스 키, hello 이전 단계에서 만든 hello 컨테이너를 지정 합니다.

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
VHD 업로드 hello 시간이 걸릴 수 있습니다.

### <a name="create-a-managed-disk"></a>관리 디스크 만들기


Hello VHD를 사용 하 여에서 관리 되는 디스크를 만들 [az 디스크 만들기](/cli/azure/disk#create)합니다. hello 다음 예제에서는 관리 되는 디스크 이름은 *myManagedDisk* 라는 저장소 계정 및 컨테이너 tooyour 업로드 한 VHD hello에서:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>옵션 2: 기존 VM 복사

만들 수도 있습니다 hello 사용자 지정 된 VM에 Azure와 hello OS 디스크를 복사 하 고 새 VM toocreate tooa 연결 다른 복사본입니다. 테스트에 문제가 있지만 여러 새 Vm에 대 한 기존 Azure VM toouse hello 모델로 하려는 경우 실제로 만들어야는 **이미지** 대신 합니다. 기존 Azure VM에서 이미지 만들기에 대 한 자세한 내용은 참조 [hello CLI를 사용 하 여 Azure VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>스냅숏 만들기

이 예에서는 *myResourceGroup*이라는 리소스 그룹에 *myVM*이라는 VM의 스냅숏을 만들고 *osDiskSnapshot*이라는 스냅숏을 만듭니다.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Hello 관리 되는 디스크 만들기

Hello 스냅숏에서 새 관리 되는 디스크를 만듭니다.

Hello 스냅숏의 hello ID를 가져옵니다. 이 예제에서는 hello 스냅숏 이름은 *osDiskSnapshot* hello에 속해 *myResourceGroup* 리소스 그룹입니다.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Hello 관리 되는 디스크를 만듭니다. 이 예제에서는 스냅숏에서 *myManagedDisk*라는 관리 디스크를 만들고 이는 표준 저장소에서 128GB 크기입니다.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Hello VM 만들기

이제를 사용 하 여 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 및 연결 (--os-디스크 연결) hello hello 운영 체제 디스크와 디스크를 관리 합니다. hello 다음 예제에서는 V *myNewVM* hello 관리를 사용 하 여 업로드 된 VHD에서 만든 디스크:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Hello VM에 수 tooSSH 있어야 hello 자격 증명을 사용 하 여 hello 소스 VM에서에서 합니다. 

## <a name="next-steps"></a>다음 단계
사용자 지정 가상 디스크를 준비하고 업로드한 후 [Resource Manager 및 템플릿 사용하기](../../azure-resource-manager/resource-group-overview.md)에 관해 자세히 알아볼 수 있습니다. 너무 필요가 있습니다[데이터 디스크 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour 새 Vm입니다. Tooaccess 해야 하는 Vm에서 실행 하는 응용 프로그램의 경우 반드시 너무[포트와 끝점을 열어야](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

