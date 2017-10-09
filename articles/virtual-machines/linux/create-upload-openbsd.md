---
title: "aaaCreate 및 업로드 OpenBSD VM 이미지 tooAzure | Microsoft Docs"
description: "어떻게 toocreate 및 업로드를 포함 하는 가상 하드 디스크 (VHD) hello OpenBSD 운영 체제 toocreate Azure CLI를 통해 Azure 가상 컴퓨터에 알아봅니다"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>만들기 및 업로드 OpenBSD 디스크 이미지 tooAzure
이 문서에서는 어떻게 toocreate 및 업로드를 포함 하는 가상 하드 디스크 (VHD) hello OpenBSD 운영 체제입니다. 를 업로드 한 후에 사용자 고유의 이미지 toocreate Azure CLI를 통해 Azure에서 가상 컴퓨터 (VM)으로 사용할 수 있습니다.


## <a name="prerequisites"></a>필수 조건
이 문서에서는 다음 항목 hello 있다고 가정 합니다.

* **Azure 구독** - 계정이 없는 경우 몇 분 만에 계정을 만들 수 있습니다. MSDN 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요. 그렇지 않은 경우 너무 방법을 알아보려면[무료 평가판 계정을 만들](https://azure.microsoft.com/pricing/free-trial/)합니다.  
* **Azure CLI 2.0** -있는지 hello 최신 [Azure CLI 2.0](/cli/azure/install-azure-cli) 설치 하 고 tooyour 된 Azure 계정 로그인 [az 로그인](/cli/azure/#login)합니다.
* **.Vhd 파일에 설치 된 OpenBSD 운영 체제** -지원 되는 OpenBSD 운영 체제 (버전 6.1) 설치 된 tooa 가상 하드 디스크 여야 합니다. 여러 도구 toocreate.vhd 파일을 포함 합니다. 예를 들어 Hyper-v toocreate hello.vhd 파일 등 가상화 솔루션을 사용 하 고 hello 운영 체제를 설치할 수 있습니다. Tooinstall 및 Hyper-v를 사용 하 여 참조 하는 방법에 대 한 지침은 [Hyper-v 설치 및 가상 컴퓨터 만들기](http://technet.microsoft.com/library/hh846766.aspx)합니다.


## <a name="prepare-openbsd-image-for-azure"></a>OpenBSD 이미지를 Azure에 사용하도록 준비
Hello hello OpenBSD 운영 체제 6.1, Hyper-v 지원 추가 설치한 VM hello 다음 절차를 완료 합니다.

1. DHCP를 설치 하는 동안 사용 하지 않는 hello 서비스를 다음과 같이 설정.

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. 다음과 같이 직렬 콘솔을 설치합니다.

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. 다음과 같이 패키지 설치를 구성합니다.

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. 기본적으로 hello `root` Azure의 가상 컴퓨터에서 사용자가 비활성화 되어 있습니다. 사용자가 hello를 사용 하 여 상승 된 권한으로 명령에 실행할 수 `doas` OpenBSD VM에서 명령을 합니다. Doas는 기본적으로 사용하도록 설정됩니다. 자세한 내용은 [doas.conf](http://man.openbsd.org/doas.conf.5)를 참조하세요. 

5. 설치 및 hello Azure 에이전트에 대 한 필수 구성 요소를 다음과 같이 구성 합니다.

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. 항상 hello hello Azure 에이전트의 최신 릴리스를 찾을 수 [Github](https://github.com/Azure/WALinuxAgent/releases)합니다. 다음과 같이 hello 에이전트를 설치 합니다.

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Azure 에이전트를 설치한 후 다음과 같이 실행 하는 것이 좋습니다 tooverify 됩니다.
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. 프로 비전 해제 하 고 확인 시스템 tooclean hello 다시 프로 비전에 대 한 적합 한 것입니다. hello 다음 명령은 삭제 hello 마지막 프로 비전 된 사용자 계정과 연결 된 hello 데이터:

    ```sh
    waagent -deprovision+user -force
    ```

이제 VM을 종료할 수 있습니다.


## <a name="prepare-hello-vhd"></a>Hello VHD를 준비 합니다.
hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다. Hyper-v 관리자를 사용 하 여 hello 디스크 toofixed VHD 형식으로 변환 하거나 Powershell hello 수 [convert vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet. 예제는 다음과 같습니다.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>저장소 리소스 만들기 및 업로드
먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload VHD를 사용 하는 저장소 계정 만들기 [az 저장소 계정에 create](/cli/azure/storage/account#create)합니다. 저장소 계정 이름은 고유해야 하므로 자신만의 이름을 제공하세요. hello 다음 예제에서는 저장소 계정인 *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol toohello 저장소 계정에 액세스를 사용 하 여 hello 저장소 키를 받아야 [az 저장소 계정 키 목록](/cli/azure/storage/account/keys#list) 다음과 같습니다.

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

toologically 별도 hello Vhd를 업로드 된 hello 저장소 계정 내에서 컨테이너를 만들 [az 저장소 컨테이너 만들기](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

마지막으로 다음과 같이 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 VHD를 업로드합니다.

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>VHD에서 VM 만들기
[샘플 스크립트](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md)를 사용하거나 직접 [az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들 수 있습니다. toospecify hello OpenBSD VHD 업로드를 사용 하 여 hello `--image` 다음과 같이 매개 변수:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Hello IP 주소를 사용 하 여 OpenBSD VM에 대 한 가져오기 [az vm 목록-ip-주소](/cli/azure/vm#list-ip-addresses) 다음과 같습니다.

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

이제 일반적인 방법으로 SSH tooyour OpenBSD VM에 수행할 수 있습니다.
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>다음 단계
Tooknow OpenBSD6.1에서 Hyper-v에 대 한 자세한 정보를 지원 하려면 읽기 [OpenBSD 6.1](https://www.openbsd.org/61.html) 및 [hyperv.4](http://man.openbsd.org/hyperv.4)합니다.

관리 되는 디스크에서 VM toocreate 읽을 [az 디스크](/cli/azure/disk)합니다. 
