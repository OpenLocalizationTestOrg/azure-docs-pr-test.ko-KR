---
title: "사용자 지정 Linux 이미지를 Azure CLI 1.0과 함께 aaaUpload | Microsoft Docs"
description: "페이지를 만들고 가상 하드 디스크 (VHD) tooAzure hello 리소스 관리자 배포 모델 및 hello Azure CLI 1.0을 사용 하 여 사용자 지정 Linux 이미지를 사용 하 여 업로드 합니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>업로드 하 고 hello Azure CLI 1.0을 사용 하 여 사용자 지정 디스크 이미지에서 Linux VM을 만듭니다
이 문서에는 사용 하 여 가상 하드 디스크 (VHD) tooAzure tooupload hello 리소스 관리자 배포 모델 및 Linux Vm의 경우이 사용자 지정 이미지를 만드는 방법을 보여줍니다. 이 기능은 tooinstall 사용 하면 구성 Linux 배포판 tooyour 요구 하 고 다음 해당 VHD를 사용 하 여 tooquickly Azure 가상 컴퓨터 (Vm)를 만듭니다.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한


## <a name="quick-commands"></a>빠른 명령
Tooquickly 해야 할 경우 hello 작업을 수행, 다음 섹션의 세부 정보 hello hello 기본 명령을 tooupload VM tooAzure 합니다. 각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#requirements)합니다.

확인 했는지 [Azure CLI 1.0 hello](../../cli-install-nodejs.md) 에 로그인 하 고 리소스 관리자 모드를 사용 하 여:

```azurecli
azure config mode arm
```

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myimages`가 포함됩니다.

먼저 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `WestUs` 위치:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

저장소 계정 toohold 가상 디스크를 만듭니다. hello 다음 예제에서는 라는 저장소 계정을 `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

저장소 계정에 대 한 hello 선택 키를 나열 합니다. `key1`을 기록해 둡니다.

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

가져온 hello 저장소 키를 사용 하 여 저장소 계정 내에서 컨테이너를 만듭니다. hello 다음 예에서는 라는 컨테이너를 만듭니다 `myimages` hello 저장소 키 값을 사용 하 여 `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

마지막으로 만든 VHD toohello 컨테이너를 업로드 합니다. Hello 로컬 경로 tooyour VHD 지정 아래 `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

이제 [Resource Manager 템플릿을 사용하여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)업로드된 가상 디스크에서 VM을 만들 수 있습니다. Hello URI tooyour 디스크를 지정 하 여 hello CLI를 사용할 수도 있습니다 (`--image-urn`). hello 다음 예제에서는 V `myVM` 이전에 업로드 하는 hello 가상 디스크를 사용 하 여:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

hello 대상 저장소 계정에 가상 디스크를 업로드 하는 위치와 같은 hello toobe 있습니다. 모든 hello hello에 필요한 추가 매개 변수, 또한 toospecify, 필요에 대 한 프롬프트에 응답 또는 `azure vm create` 가상 네트워크, 공용 IP 주소, 사용자 이름 및 SSH 키와 같은 명령입니다. 자세한 내용은 hello에 대 한 [CLI 리소스 관리자 매개 변수를 사용할 수 있는](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)합니다.

## <a name="requirements"></a>요구 사항
toocomplete hello 필요한 다음 단계를:

* **.Vhd 파일에 설치 된 Linux 운영 체제** -설치 프로그램 [Linux Azure 보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (참조 또는 [비 보증 배포판에 대 한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD에서에서 가상 디스크 형식입니다. VM 및 VHD toocreate 존재 하는 여러 도구:
  * 설치 및 구성 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD 이미지 형식으로 처리 합니다. 필요한 경우 `qemu-img convert`를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.
  * 또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.

> [!NOTE]
> Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다. VM을 만들 때 hello 형식으로 VHD를 지정 합니다. 필요한 경우 사용 하 여 VHDX 디스크 tooVHD 변환할 수 있습니다 [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet. 또한 Azure에서는 tooconvert 필요 하므로 동적 Vhd를 업로드 이러한 디스크 toostatic Vhd 업로드 하기 전에. 와 같은 도구를 사용할 수 있습니다 [GO에 대 한 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure 업로드 프로세스 중 tooconvert 동적 디스크.
> 
> 

* 사용자 지정 이미지에서 만들어진 Vm에에서 상주해 야 hello 동일 hello 이미지 자체와 저장소 계정
  * 사용자 지정 이미지와 Vm을 만든된 저장소 계정 및 컨테이너 toohold 만들기
  * 모든 VM을 만든 후 이미지를 안전하게 삭제할 수 있습니다.

확인 했는지 [Azure CLI 1.0 hello](../../cli-install-nodejs.md) 에 로그인 하 고 리소스 관리자 모드를 사용 하 여:

```azurecli
azure config mode arm
```

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myimages`가 포함됩니다.

<a id="prepimage"> </a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Hello 이미지 toobe 업로드 준비
Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조). 다음 문서는 hello 어떻게 tooprepare hello Azure에서 지원 되는 다양 한 Linux 배포를 안내 합니다.

* **[CentOS 기반 배포](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES 및 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[기타 - 보증되지 않는 배포](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

또한 hello를 참조 하십시오.  **[Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes)**  보다 일반적인 방법에 대 한 azure Linux 이미지를 준비 합니다.

> [!NOTE]
> hello [Azure 플랫폼 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) tooVMs Linux를 실행 하 여 지원 버전에서 지정 된 대로 hello 구성 세부 정보를 사용 하는 분포를 지지 하는 hello 중 하나에 적용 됩니다. [Azure 보증에 Linux 분포](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.


## <a name="create-a-resource-group"></a>리소스 그룹 만들기
리소스 그룹 논리적으로 결합 하도록 모든 hello Azure 리소스 toosupport hello 가상 네트워킹 및 저장소와 같은 가상 컴퓨터. [여기서 Azure 리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아 봅니다. 사용자 지정 디스크 이미지를 업로드 하 고 Vm을 만들 하기 전에 먼저 toocreate 리소스 그룹을 해야 합니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `WestUS` 위치:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>저장소 계정 만들기
VM은 저장소 계정 내에서 페이지 blob으로 저장됩니다. [여기서 Azure Blob 저장소](../../storage/common/storage-introduction.md#blob-storage)에 대해 자세히 알아 봅니다. 사용자 지정 디스크 이미지 및 VM에 대한 저장소 계정을 만듭니다. 에 사용자 지정 디스크 이미지 필요 toobe에서 만드는 모든 Vm 이미지와 동일한 저장소 계정을 hello 합니다.

hello 다음 예제에서는 라는 저장소 계정을 `mystorageaccount` 이전에 만든 hello 리소스 그룹에:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>저장소 계정 키 나열
Azure는 각 저장소 계정에 대해 두 개의 512 비트 선택키를 생성합니다. 이러한 액세스 키에는 쓰기 작업 toocarry 같은 toohello 저장소 계정에 인증할 때 사용 됩니다. 에 대해 자세히 알아보세요 [toostorage 여기에 액세스 관리](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다. Hello로 선택 키를 볼 수 있습니다 `azure storage account keys list` 명령입니다.

만든 hello 저장소 계정에 대 한 hello 액세스 키 보기:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
메모 `key1` 됩니다 사용할 toointeract hello 다음 단계에서 저장소 계정과 합니다.

## <a name="create-a-storage-container"></a>저장소 컨테이너 만들기
동일한 방식으로 다른 디렉터리 toologically 만드는 hello에 로컬 파일 시스템 구성, 가상 디스크 및 이미지 저장소 계정 tooorganize 내 컨테이너를 만들 합니다. 저장소 계정에 포함할 수 있는 컨테이너의 수에는 제한이 없습니다. 

hello 다음 예에서는 라는 컨테이너를 만듭니다 `myimages`, hello 이전 단계에서 얻은 hello 선택 키 지정 (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>VHD를 업로드 합니다.
이제 사용자 지정 디스크 이미지를 실제로 업로드할 수 있습니다. VM이 사용하는 모든 가상 디스크를 통해 사용자 지정 디스크 이미지를 페이지 Blob으로 업로드하고 저장합니다.

다음 로컬 컴퓨터의 경로 toohello 사용자 지정 디스크 이미지를 hello 및 액세스 키, hello 이전 단계에서 만든 hello 컨테이너를 지정 합니다.

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>사용자 지정 이미지에서 VM 만들기
사용자 지정 디스크 이미지에서 Vm을 만들 때 hello URI toohello 디스크 이미지를 지정 합니다. 사용자 지정 디스크 이미지가 저장 되어 있는 대상 저장소 계정 일치 해당 hello를 확인 합니다. Hello Azure CLI 또는 리소스 관리자 JSON 템플릿을 사용 하 여 VM을 만들 수 있습니다.

### <a name="create-a-vm-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 VM 만들기
Hello 지정 `--image-urn` hello로 매개 변수 `azure vm create` 명령 toopoint tooyour 사용자 지정 디스크 이미지입니다. 되도록 `--storage-account-name` 일치 hello 사용자 지정 디스크 이미지가 저장 되는 저장소 계정입니다. Hello 동일한 컨테이너 사용자 지정 디스크 이미지 toostore hello 대로 Vm toouse를 않아도 됩니다. 있는지 toocreate는 다른 컨테이너에서 hello 확인 같은 방식으로 이전 단계에서 사용자 지정 디스크 이미지를 업로드 하기 전에 hello 합니다.

hello 다음 예제에서는 V `myVM` 사용자 지정 디스크 이미지에서:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

모든 hello hello에 필요한 추가 매개 변수, 여전히 toospecify, 필요에 대 한 프롬프트에 응답 또는 `azure vm create` 가상 네트워크, 공용 IP 주소, 사용자 이름 및 SSH 키와 같은 명령입니다. Hello에 대 한 자세한 [CLI 리소스 관리자 매개 변수를 사용할 수 있는](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)합니다.

### <a name="create-a-vm-using-a-json-template"></a>JSON 템플릿을 사용하여 VM 만들기
Azure 리소스 관리자 템플릿은 toobuild 원하는 hello 환경을 정의 하는 개체 JSON (JavaScript Notation) 파일입니다. hello 템플릿 계산, 네트워크 등 toodifferent 리소스 공급자에서 분할 됩니다. 기존 템플릿을 사용하거나 직접 템플릿을 작성할 수 있습니다. [Resource Manager 및 템플릿 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아봅니다.

Hello 내 `Microsoft.Compute/virtualMachines` 있는 서식 파일의 공급자는 `storageProfile` 노드 VM에 대 한 hello 구성 세부 정보를 포함 하는 합니다. hello 두 주요 매개 변수 tooedit는 hello `image` 및 `vhd` tooyour 사용자 지정 디스크 이미지와 새 VM의 가상 디스크를 가리키는 Uri입니다. hello 다음 사용자 지정 디스크 이미지를 사용 하기 위한 hello JSON의 예를 보여 줍니다.

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

사용할 수 있습니다 [사용자 지정 이미지에서 VM이 기존 템플릿 toocreate](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) 에 대 한 읽기 또는 [사용자 지정 Azure 리소스 관리자 템플릿을 만들어](../../azure-resource-manager/resource-group-authoring-templates.md)합니다. 

Hello를 사용 하 여 Vm에 구성 된 템플릿을 있으면 만들면 `azure group deployment create` 명령입니다. Hello를 사용 하 여 hello JSON 서식 파일의 URI를 지정 `--template-uri` 매개 변수:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

컴퓨터에 로컬로 저장 된 JSON 파일이 있는 경우에 hello을 사용할 수 있습니다 `--template-file` 매개 변수 대신:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>다음 단계
사용자 지정 가상 디스크를 준비하고 업로드한 후 [Resource Manager 및 템플릿 사용하기](../../azure-resource-manager/resource-group-overview.md)에 관해 자세히 알아볼 수 있습니다. 너무 필요가 있습니다[데이터 디스크 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour 새 Vm입니다. Tooaccess 해야 하는 Vm에서 실행 하는 응용 프로그램의 경우 반드시 너무[포트와 끝점을 열어야](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

