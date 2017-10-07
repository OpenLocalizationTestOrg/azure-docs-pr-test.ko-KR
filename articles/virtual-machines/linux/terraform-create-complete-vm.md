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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="7b4af-103">Terraform을 사용하여 Azure에서 기본 인프라 만들기</span><span class="sxs-lookup"><span data-stu-id="7b4af-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="7b4af-104">이 문서에서는 tootake tooprovision 기본 인프라와 함께 가상 컴퓨터를 Azure에 해야 하는 hello 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="7b4af-105">어떻게 toowrite Terraform 스크립트 및 toovisualize hello 하기 전에 어떻게 변경 되는지 있도록를 클라우드 인프라를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="7b4af-106">또한 배웁니다 방법을 Terraform를 사용 하 여 Azure에서 toocreate 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="7b4af-107">tooget 시작 (Visual Studio 코드/Sublime/Vim/등)가 원하는 텍스트 편집기에서 \terraform_azure101.tf 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="7b4af-108">hello 파일의 정확한 이름을 hello의 hello 폴더 이름을 매개 변수로 허용 하는 Terraform 없으므로 들이 중요 하지 않습니다: hello 폴더에서 모든 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="7b4af-109">Hello를 hello 새 파일에 코드 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-109">Paste hello following code in hello new file:</span></span>

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
<span data-ttu-id="7b4af-110">Hello에 `provider` hello 섹션 스크립트 hello 스크립트의 Terraform toouse Azure 공급자 tooprovision 리소스 알립니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="7b4af-111">subscription_id, appId, 암호 및 tenant_id에 대 한 tooget 값 참조 hello [설치 및 Terraform 구성](terraform-install-configure.md) 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="7b4af-112">이 블록의 hello 값에 대 한 환경 변수를 만든 경우 tooinclude 않아도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="7b4af-113">hello `azurerm_resource_group` 리소스 Terraform toocreate 새 리소스 그룹에 게 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="7b4af-114">이 문서의 뒷부분에 나오는 Terraform에서 사용할 수 있는 더 많은 리소스 유형을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="7b4af-115">Hello 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="7b4af-115">Execute hello script</span></span>
<span data-ttu-id="7b4af-116">Hello 스크립트를 저장 한 후 toohello 콘솔/명령 줄을 종료 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="7b4af-117">Azure에 대 한 tooinitialize hello Terraform 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="7b4af-118">그런 다음 hello 디렉터리를 너무 변경**terraformscripts**, 다음 명령을 문제 hello 및:</span><span class="sxs-lookup"><span data-stu-id="7b4af-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="7b4af-119">Hello 사용 `plan` Terraform 명령을 hello 스크립트에 정의 된 hello 리소스를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="7b4af-120">다음 출력 hello 계획된 실행 및 Terraform에서 저장 하는 상태 정보가 toohello 비교 하기 _없이_ Azure에서 리소스를 실제로 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="7b4af-121">Hello 이전 명령을 실행 하면 다음 화면 hello 유사한 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform 계획](./media/terraform/tf_plan2.png)

<span data-ttu-id="7b4af-123">모두 제대로 표시 하는 경우 hello 다음을 실행 하 여 Azure에서이 새 리소스 그룹 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="7b4af-124">Hello Azure 포털에서에서 라는 hello 새 빈 리소스 그룹을 확인 해야 `terraformtest`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="7b4af-125">Hello 섹션 뒤, 가상 컴퓨터 및 모든 해당 가상 컴퓨터 toohello 리소스 그룹에 대 한 지원 인프라 hello 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="7b4af-126">Terraform으로 Ubuntu VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="7b4af-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="7b4af-127">보겠습니다 필요한 tooprovision 있는 hello 세부 정보를 사용 하 여 만든 म hello Terraform 스크립트 Ubuntu를 실행 하는 가상 컴퓨터 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="7b4af-128">다음 섹션 hello를 프로 비전 하는 hello 리소스를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="7b4af-129">단일 서브넷이 있는 네트워크</span><span class="sxs-lookup"><span data-stu-id="7b4af-129">A network with a single subnet</span></span>
* <span data-ttu-id="7b4af-130">네트워크 인터페이스 카드</span><span class="sxs-lookup"><span data-stu-id="7b4af-130">A network interface card</span></span> 
* <span data-ttu-id="7b4af-131">가상 컴퓨터 진단 hello에 대 한 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="7b4af-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="7b4af-132">공용 IP</span><span class="sxs-lookup"><span data-stu-id="7b4af-132">A public IP</span></span>
* <span data-ttu-id="7b4af-133">모든 hello 이전 리소스를 활용 하는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="7b4af-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="7b4af-134">각 hello Azure Terraform 리소스에 대 한 철저 한 설명서 참조 hello [Terraform 설명서](https://www.terraform.io/docs/providers/azurerm/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="7b4af-135">전체 버전의 hello hello [프로비저닝](#complete-terraform-script) 편의 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="7b4af-136">Hello Terraform 스크립트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-136">Extend hello Terraform script</span></span>
<span data-ttu-id="7b4af-137">다음과 같이 hello 다음 리소스를 사용 하 여 만든 hello 스크립트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-137">Extend hello script that was created with hello following resources:</span></span> 
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
<span data-ttu-id="7b4af-138">hello 이전 스크립트는 가상 네트워크와 가상 네트워크 내의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="7b4af-139">Hello 참조 toohello 리소스 그룹 "${azurerm_resource_group.helloterraform.name}" hello 가상 네트워크와 hello 서브넷 정의 통해 이미 만든 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

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
<span data-ttu-id="7b4af-140">hello 이전 스크립트 조각에서 만든 hello 공용 IP를 활용 하는 네트워크 인터페이스와 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="7b4af-141">참고 hello toosubnet_id와 public_ip_address_id 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="7b4af-142">Terraform에 기본 제공 intelligence toounderstand hello 해당 네트워크 인터페이스에 종속 되어 hello 리소스 hello 네트워크 인터페이스의 hello 생성 하기 전에 해당 필요 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

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
<span data-ttu-id="7b4af-143">여기에서 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-143">Here, you created a storage account.</span></span> <span data-ttu-id="7b4af-144">이 저장소 계정은 hello 가상 컴퓨터 진단 세부 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

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
<span data-ttu-id="7b4af-145">마지막으로, hello 이전 코드 조각에서 이미 프로 비전 하는 모든 hello 리소스를 활용 하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="7b4af-146">가상 컴퓨터 진단 hello, 공용 IP 및 서브넷을 지정 된 네트워크 인터페이스에 대 한 저장소 계정을 이며 hello 리소스 그룹이 이미 만든 경우.</span><span class="sxs-lookup"><span data-stu-id="7b4af-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="7b4af-147">Note hello vm_size 속성을 여기서 hello 스크립트 Azure 표준 DS1v2 SKU를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="7b4af-148">필요한 toosupply SSH 공개 키가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="7b4af-149">Hello 섹션으로 hello 공개 키 값을 배치 **... INSERT OPENSSH PUBLIC KEY HERE ...**에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="7b4af-150">기존 ssh에서는 키 쌍 또는 hello에 따라 [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) 또는 [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) 설명서 toogenerate hello에 대 한 키 쌍.</span><span class="sxs-lookup"><span data-stu-id="7b4af-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="7b4af-151">Hello 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="7b4af-151">Execute hello script</span></span>
<span data-ttu-id="7b4af-152">저장 hello 전체 스크립트를 사용 하면 toohello 콘솔/명령줄을 종료 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="7b4af-153">일정 시간이 지난 후 hello 리소스를 가상 컴퓨터를 포함 하 여 hello에 표시 `terraformtest` hello Azure 포털에서에서 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="7b4af-154">전체 Terraform 스크립트</span><span class="sxs-lookup"><span data-stu-id="7b4af-154">Complete Terraform script</span></span>

<span data-ttu-id="7b4af-155">사용자 편의 위해 다음은 전체 Terraform 스크립트 hello이이 문서에서 설명 하는 hello 인프라의 모든 해당 프로 비전입니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7b4af-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b4af-156">Next steps</span></span>
<span data-ttu-id="7b4af-157">Terraform을 사용하여 Azure에서 기본 인프라를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="7b4af-158">부하 분산 장치 및 가상 컴퓨터 확장 집합을 사용하는 예제를 비롯한 보다 복잡한 시나리오는 여러 가지 [Azure에 대한 Terraform 예제](https://github.com/hashicorp/terraform/tree/master/examples)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b4af-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="7b4af-159">지원 되는 Azure 공급자의 최신 목록, 참조 hello [Terraform 설명서](https://www.terraform.io/docs/providers/azurerm/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b4af-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
