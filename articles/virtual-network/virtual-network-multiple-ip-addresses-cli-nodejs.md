---
title: "hello Azure CLI 1.0을 사용 하 여 여러 IP 주소와 aaaVM | Microsoft Docs"
description: "여러 IP 해결 하는 tooassign 방법을 알아보려면 Azure CLI 1.0 hello tooa 가상 컴퓨터를 사용 하 여 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Toovirtual 컴퓨터 Azure CLI 1.0을 사용 하 여 여러 IP 주소를 할당 합니다.

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

이 문서에서는 toocreate hello Azure 리소스 관리자 배포 모델을 사용 하 여 가상 컴퓨터 (VM) Azure CLI 1.0 hello 하는 방법을 설명 합니다. Hello 클래식 배포 모델을 통해 만든 tooresources 여러 IP 주소를 할당할 수 없습니다. Azure 배포 모델을 읽을 hello에 대 한 자세한 toolearn [배포 모델을 이해](../resource-manager-deployment-model.md) 문서.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기

Hello Azure CLI 1.0 (이 문서) 또는 hello를 사용 하 여이 작업을 완료할 수 있습니다 [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md)합니다. 수행 하는 hello 단계 hello 시나리오에 설명 된 대로 toocreate 예로 여러 IP 사용 하 여 VM 해결 하는 방법을 설명 합니다. 변수 이름과 IP 주소 유형을 구현에 필요한 대로 변경합니다.

1. 에서 설치 및 구성 단계를 다음 hello 하 여 Azure CLI 1.0 hello hello [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서 hello 사용 하 여 Azure 계정에 로그인 합니다 `azure-login` 명령입니다.

2. 리소스 그룹 만들기:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. 가상 네트워크 만들기:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Hello 가상 네트워크에 서브넷을 만듭니다.

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Hello VM에 대 한 저장소 계정을 만듭니다. Hello를 실행 하기 전에 다음 명령을, 대체 *mystorageaccount* 고유한 이름을 사용 합니다. hello 이름은 Azure 전체에서 고유 해야 합니다.

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Hello IP 구성, NIC를 만들고 hello IP 구성을 toohello NIC. 할당 추가, 제거 또는 필요에 따라 hello 구성을 변경할 수 있습니다. 구성을 따르고 hello hello 시나리오에 설명 되어 있습니다.

    **IPConfig-1**

    Toocreate 다음에 나오는 hello 명령을 입력 합니다.

    - 고정 공용 IP 주소가 있는 공용 IP 주소 리소스
    - NIC를 hello 공용 IP 주소 및 정적 개인 IP 주소 tooit 할당 합니다.
    
    대체 *mypublicdns* hello Azure 위치 내에서 고유한 이름을 사용 합니다.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > 공용 IP 주소에는 명목 요금이 부과됩니다. 가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.

    **IPConfig-2**

     새 공용 IP 주소 리소스와 고정 공용 IP 주소 및 정적 개인 IP 주소를 사용 하 여 새 IP 구성이 hello 명령을 toocreate 다음을 입력 합니다.
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig-3**

    Hello 명령을 toocreate IP 구성을 정적 개인 IP 주소와 공용 IP 주소가 없습니다. 다음을 입력 합니다.

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >이 문서에는 모든 IP 구성을 tooa 할당 있지만 단일 NIC를 지정할 수 있습니다 여러 IP 구성은 VM에서 NIC tooany 합니다. 여러 Nic 사용 하 여 VM 읽기 toocreate 방법 toolearn hello 여러 Nic 문서를 사용 하 여 VM 만들기.

7. Linux VM 만들기 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange hello VM 크기 tooStandard DS2 v2, 예를 들어 hello 다음 속성을 추가 하기만 하면 `--vm-size Standard_DS3_v2` toohello `azure vm create` 6 단계에서 명령을 합니다.

8. Hello 명령 tooview hello NIC를 다음을 입력 하 고 hello IP 구성 관련 된 키를 누릅니다.

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. 추가 hello 개인 IP 주소 수 toohello VM 운영 체제 hello에 운영 체제에 대 한 hello 단계를 완료 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션.

## <a name="add"></a>IP 주소 tooa VM 추가

추가 개인 및 공용 IP 주소 tooan NIC를 수행 하는 hello 단계를 완료 하 여 기존를 추가할 수 있습니다. hello를 바탕으로 hello 예제 [시나리오](#Scenario) 이 문서에서 설명 합니다.

1. Azure CLI 및이 섹션의 단계를 단일 CLI 세션 내에서 남은 전체 hello를 엽니다. 전체 hello hello의 단계를 이미 설치 및 구성 하는 Azure CLI 없다면 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서 Azure 계정에 로그인 합니다.

2. Hello 절, 요구 사항에 따라 다음 중 하나의 hello 단계를 완료 합니다.

    - **개인 IP 주소 추가**
    
        개인 IP 주소 tooa NIC tooadd 아래 hello 명령을 사용 하 여 IP 구성을 만들어야 합니다. hello 고정 주소 hello 서브넷에 대 한 사용 되지 않는 주소 여야 합니다.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        고유한 구성 이름과 개인 IP 주소를 사용하여 필요한 만큼 구성을 만듭니다(정적 IP 주소를 가진 구성의 경우).

    - **공용 IP 주소 추가**
    
        공용 IP 주소를 tooeither 연결 하 여 추가 되는 새 IP 구성 또는 기존 IP 구성 합니다. 필요한 만큼 따르려면 hello 섹션 중 하나에 hello 단계를 완료 합니다.

        > [!NOTE]
        > 공용 IP 주소에는 명목 요금이 부과됩니다. 가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.
        >

        **Hello 리소스 tooa 새 IP 구성에 연결**
    
        새 IP 구성의 공용 IP 주소를 추가할 때마다 모든 IP 구성 시 개인 IP 주소가 있어야 하기 때문에 개인 IP 주소도 추가해야 합니다. 기존 공용 IP 주소 리소스를 추가하거나 새로 만들 수 있습니다. toocreate 한 새 hello 다음 명령을 입력 합니다.

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        개인 고정 IP 주소와 연결 된 hello 새 IP 구성이 toocreate *myPublicIP3* 공용 IP 리소스에 주소를 hello 다음 명령을 입력 합니다.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Hello 리소스 tooan 기존 IP 구성에 연결**

        공용 IP 주소 리소스에 아직 연결 되어 관련된 tooan IP 구성만 가능 합니다. IP 구성 hello 다음 명령을 입력 하 여 연결 된 공용 IP 주소에 있는지 여부를 확인할 수 있습니다.

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        IPConfig-3에 대 한 출력을 반환 하는 hello에 나오는 줄 비슷한 toohello를 찾습니다.

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Hello 이후 **공용 IP** 열에 대 한 *IpConfig-3* 은 공백은, 공용 IP 주소 리소스가 현재 연결된 tooit입니다. 기존 공용 IP 주소 리소스 tooIpConfig-3, 더하거나 명령 toocreate 하나를 수행 하는 hello 입력:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        다음 명령을 tooassociate hello 공용 IP 주소 리소스 toohello 기존 IP 구성 라는 hello 입력 *IPConfig-3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. 보기 hello 개인 IP 주소 및 다음 명령을 입력 하 여 NIC hello 공용 IP 주소 할당 된 리소스 toohello hello:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      hello 출력은 유사한 toohello 다음 반환:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Hello에 대 한 hello 지침에 따라 toohello NIC toohello VM 운영 체제를 추가한 hello 개인 IP 주소 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
