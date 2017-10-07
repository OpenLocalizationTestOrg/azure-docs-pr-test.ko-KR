---
title: "Terraform를 사용 하 여 Azure에서 aaaCreate 기본 인프라 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure Terraform를 사용 하 여 리소스"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Terraform을 사용하여 Azure에서 기본 인프라 만들기
이 문서에서는 tootake tooprovision 기본 인프라와 함께 가상 컴퓨터를 Azure에 해야 하는 hello 단계를 설명 합니다. 어떻게 toowrite Terraform 스크립트 및 toovisualize hello 하기 전에 어떻게 변경 되는지 있도록를 클라우드 인프라를 설명 합니다. 또한 배웁니다 방법을 Terraform를 사용 하 여 Azure에서 toocreate 인프라입니다.

tooget 시작 (Visual Studio 코드/Sublime/Vim/등)가 원하는 텍스트 편집기에서 \terraform_azure101.tf 라는 파일을 만듭니다. hello 파일의 정확한 이름을 hello의 hello 폴더 이름을 매개 변수로 허용 하는 Terraform 없으므로 들이 중요 하지 않습니다: hello 폴더에서 모든 스크립트를 실행 합니다. Hello를 hello 새 파일에 코드 다음에 붙여 넣습니다.

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
Hello에 `provider` hello 섹션 스크립트 hello 스크립트의 Terraform toouse Azure 공급자 tooprovision 리소스 알립니다. subscription_id, appId, 암호 및 tenant_id에 대 한 tooget 값 참조 hello [설치 및 Terraform 구성](terraform-install-configure.md) 가이드입니다. 이 블록의 hello 값에 대 한 환경 변수를 만든 경우 tooinclude 않아도 것입니다. 

hello `azurerm_resource_group` 리소스 Terraform toocreate 새 리소스 그룹에 게 지시 합니다. 이 문서의 뒷부분에 나오는 Terraform에서 사용할 수 있는 더 많은 리소스 유형을 확인할 수 있습니다.

## <a name="execute-hello-script"></a>Hello 스크립트 실행
Hello 스크립트를 저장 한 후 toohello 콘솔/명령 줄을 종료 하 고 hello 다음을 입력 합니다.
```
terraform init
```
 Azure에 대 한 tooinitialize hello Terraform 공급자입니다. 그런 다음 hello 디렉터리를 너무 변경**terraformscripts**, 다음 명령을 문제 hello 및:
```
terraform plan
```
Hello 사용 `plan` Terraform 명령을 hello 스크립트에 정의 된 hello 리소스를 살펴봅니다. 다음 출력 hello 계획된 실행 및 Terraform에서 저장 하는 상태 정보가 toohello 비교 하기 _없이_ Azure에서 리소스를 실제로 만드는 합니다. 

Hello 이전 명령을 실행 하면 다음 화면 hello 유사한 출력이 표시 됩니다.

![Terraform 계획](./media/terraform/tf_plan2.png)

모두 제대로 표시 하는 경우 hello 다음을 실행 하 여 Azure에서이 새 리소스 그룹 프로 비전 합니다. 
```
terraform apply
```
Hello Azure 포털에서에서 라는 hello 새 빈 리소스 그룹을 확인 해야 `terraformtest`합니다. Hello 섹션 뒤, 가상 컴퓨터 및 모든 해당 가상 컴퓨터 toohello 리소스 그룹에 대 한 지원 인프라 hello 추가 합니다.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Terraform으로 Ubuntu VM 프로비전
보겠습니다 필요한 tooprovision 있는 hello 세부 정보를 사용 하 여 만든 म hello Terraform 스크립트 Ubuntu를 실행 하는 가상 컴퓨터 확장 합니다. 다음 섹션 hello를 프로 비전 하는 hello 리소스를 있습니다.

* 단일 서브넷이 있는 네트워크
* 네트워크 인터페이스 카드 
* 가상 컴퓨터 진단 hello에 대 한 저장소 계정
* 공용 IP
* 모든 hello 이전 리소스를 활용 하는 가상 컴퓨터 

각 hello Azure Terraform 리소스에 대 한 철저 한 설명서 참조 hello [Terraform 설명서](https://www.terraform.io/docs/providers/azurerm/index.html)합니다.

전체 버전의 hello hello [프로비저닝](#complete-terraform-script) 편의 위해 제공 됩니다.

### <a name="extend-hello-terraform-script"></a>Hello Terraform 스크립트를 확장 합니다.
다음과 같이 hello 다음 리소스를 사용 하 여 만든 hello 스크립트를 확장 합니다. 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
hello 이전 스크립트는 가상 네트워크와 가상 네트워크 내의 서브넷을 만듭니다. Hello 참조 toohello 리소스 그룹 "${azurerm_resource_group.helloterraform.name}" hello 가상 네트워크와 hello 서브넷 정의 통해 이미 만든 note 합니다.

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
hello 이전 스크립트 조각에서 만든 hello 공용 IP를 활용 하는 네트워크 인터페이스와 공용 IP를 만듭니다. 참고 hello toosubnet_id와 public_ip_address_id 참조합니다. Terraform에 기본 제공 intelligence toounderstand hello 해당 네트워크 인터페이스에 종속 되어 hello 리소스 hello 네트워크 인터페이스의 hello 생성 하기 전에 해당 필요 toobe 합니다.

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
여기에서 저장소 계정을 만들었습니다. 이 저장소 계정은 hello 가상 컴퓨터 진단 세부 정보를 저장 합니다.

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
마지막으로, hello 이전 코드 조각에서 이미 프로 비전 하는 모든 hello 리소스를 활용 하는 가상 컴퓨터를 만듭니다. 가상 컴퓨터 진단 hello, 공용 IP 및 서브넷을 지정 된 네트워크 인터페이스에 대 한 저장소 계정을 이며 hello 리소스 그룹이 이미 만든 경우. Note hello vm_size 속성을 여기서 hello 스크립트 Azure 표준 DS1v2 SKU를 지정 합니다.

필요한 toosupply SSH 공개 키가 됩니다. Hello 섹션으로 hello 공개 키 값을 배치 **... INSERT OPENSSH PUBLIC KEY HERE ...**에 배치합니다. 기존 ssh에서는 키 쌍 또는 hello에 따라 [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) 또는 [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) 설명서 toogenerate hello에 대 한 키 쌍.

### <a name="execute-hello-script"></a>Hello 스크립트 실행
저장 hello 전체 스크립트를 사용 하면 toohello 콘솔/명령줄을 종료 하 고 hello 다음을 입력 합니다.
```
terraform apply
```
일정 시간이 지난 후 hello 리소스를 가상 컴퓨터를 포함 하 여 hello에 표시 `terraformtest` hello Azure 포털에서에서 리소스 그룹입니다.

## <a name="complete-terraform-script"></a>전체 Terraform 스크립트

사용자 편의 위해 다음은 전체 Terraform 스크립트 hello이이 문서에서 설명 하는 hello 인프라의 모든 해당 프로 비전입니다.

```
# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a>다음 단계
Terraform을 사용하여 Azure에서 기본 인프라를 만들었습니다. 부하 분산 장치 및 가상 컴퓨터 확장 집합을 사용하는 예제를 비롯한 보다 복잡한 시나리오는 여러 가지 [Azure에 대한 Terraform 예제](https://github.com/hashicorp/terraform/tree/master/examples)를 참조하세요. 지원 되는 Azure 공급자의 최신 목록, 참조 hello [Terraform 설명서](https://www.terraform.io/docs/providers/azurerm/index.html)합니다.
