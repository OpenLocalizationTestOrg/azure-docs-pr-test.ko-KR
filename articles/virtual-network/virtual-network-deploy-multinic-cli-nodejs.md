---
title: "여러 Nic-Azure CLI 1.0을 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "사용 하 여 여러 Nic 사용 하 여 VM toocreate Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0을 사용 하 여 여러 Nic를 포함 한 VM 만들기

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](virtual-network-deploy-multinic-classic-cli.md)합니다.
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

hello 다음 단계 사용 하 여 명명 된 리소스 그룹 *IaaSStory* hello 웹 서버 및 리소스 그룹에 대 한 명명 된 *IaaSStory 백 엔드* hello DB 서버에 대 한 합니다. Hello Azure CLI 1.0 (이 문서) 또는 hello를 사용 하 여이 작업을 완료할 수 있습니다 [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)합니다. hello에 값 "" 다음에 나오는 hello 단계의 hello 변수 hello 시나리오의 설정으로 리소스를 만듭니다. 사용자 환경에 적절 하 게 hello 값을 변경 합니다.

## <a name="prerequisites"></a>필수 조건
Hello DB 서버를 만들려면 먼저 toocreate hello *IaaSStory* 이 시나리오에 대 한 모든 hello 필요한 리소스의 리소스 그룹입니다. 이러한 리소스를 완료 하는 toocreate hello 다음 단계:

1. 너무 이동[hello 템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)합니다.
2. Hello 템플릿 페이지의 오른쪽 toohello **부모 리소스 그룹**, 클릭 **tooAzure 배포**합니다.
3. 필요한 경우 hello 매개 변수 값을를 변경한 다음 hello Azure preview 포털 toodeploy hello 리소스 그룹의 hello 단계를 수행 합니다.

> [!IMPORTANT]
> 저장소 계정 이름이 고유한지 확인합니다. Azure에서 중복된 저장소 계정 이름을 사용할 수 없습니다.
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Hello 백 엔드 Vm 만들기
hello 백 엔드 Vm hello 생성의 다음 리소스는 hello에 따라 달라 집니다.

* **데이터 디스크용 저장소 계정**. 성능 향상을 위해 hello 데이터베이스 서버에 데이터 디스크 hello 프리미엄 저장소 계정을 사용 해야 하는 반도체 드라이브 (SSD) 기술을 사용 합니다. 있는지 hello toosupport 프리미엄 저장소를 배포 하는 Azure 위치를 확인 합니다.
* **NIC**. 각 VM에 데이터베이스 액세스용으로 하나, 그리고 관리용으로 하나씩, 두 개의 NIC가 사용됩니다.
* **가용성 집합**. 모든 데이터베이스 서버를 추가할 tooa 단일 가용성 집합, tooensure hello Vm 중 하나 이상이 실행 되 고 유지 관리 합니다.

### <a name="step-1---start-your-script"></a>1단계 - 스크립트 시작
사용 되는 hello 전체 bash 스크립트를 다운로드할 수 있습니다 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh)합니다. 사용자 환경에서 toochange hello 스크립트 toowork 아래 hello 단계를 수행 합니다.

1. Hello에 위의 배포 된 기존 리소스 그룹에 따라 hello 변수 값 변경 [필수 구성 요소](#Prerequisites)합니다.

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. Hello 값을 변경 hello 값을 기반으로 hello 변수 원하는 toouse 백 엔드 배포에 대 한 합니다.

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. Hello에 대 한 hello ID 검색 `BackEnd` 서브넷 hello Vm 만들어집니다. 필요한 toodo이 hello Nic 연결 toobe toothis 서브넷 다른 리소스 그룹에 있으므로 합니다.

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > 첫 번째 명령을 사용 하 여 위에 hello [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) 및 [문자열 조작](http://tldp.org/LDP/abs/html/string-manipulation.html) (구체적으로, 부분 문자열 제거).
   >

4. Hello에 대 한 hello ID 검색 `NSG-RemoteAccess` NSG 합니다. 필요한 toodo이 hello Nic toobe toothis NSG는 다른 리소스 그룹에 연결 된 이후입니다.

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>2단계 - VM에 필요한 리소스 만들기

1. 모든 백 엔드 리소스를 위한 새 리소스 그룹을 만듭니다. 공지 hello 사용 hello `$backendRGName` hello 리소스 그룹 이름에 대 한 변수 및 `$location` hello Azure 지역에 대 한 합니다.

    ```azurecli
    azure group create $backendRGName $location
    ```

2. OS hello에 대 한 프리미엄 저장소 계정 및 사용자 Vm에서 사용 하는 데이터 디스크 toobe를 만듭니다.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. 가용성 집합 hello Vm 만듭니다.

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a>3 단계-hello Nic와 백 엔드 Vm 만들기

1. 루프 toocreate hello에 따라 여러 Vm을 시작 `numberOfVMs` 변수입니다.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. 각 VM에 대해 데이터베이스 액세스를 위한 NIC를 만듭니다.

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. 각 VM에 대해 원격 액세스를 위한 NIC를 만듭니다. 공지 hello `--network-security-group` 매개 변수를 사용 하는 tooassociate hello NIC tooan NSG 합니다.

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. Hello VM을 만듭니다.

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. 각 VM에 대 한 두 개의 데이터 디스크 및 만들기 종료 hello 루프 hello `done` 명령입니다.

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-hello-script"></a>4 단계-실행 hello 스크립트
다운로드 하 고 hello 스크립트 toocreate hello를 다시 실행 요구 사항에 따라 hello 스크립트를 변경 했으므로 여러 nic가 있는 데이터베이스 Vm을 종료 합니다.

1. 스크립트를 저장하고 **Bash** 터미널에서 실행합니다. 아래와 같이 hello 초기 출력에 나타납니다.
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. 몇 분 후 hello 실행이 종료 하 고 hello 나머지 hello 출력 아래와 같이 표시 됩니다.
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

