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
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="5244b-103">Terraform을 사용하여 Azure에서 기본 인프라 만들기</span><span class="sxs-lookup"><span data-stu-id="5244b-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="5244b-104">이 문서에서는 tootake tooprovision 기본 인프라와 함께 가상 컴퓨터를 Azure에 해야 하는 hello 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="5244b-105">어떻게 toowrite Terraform 스크립트 및 toovisualize hello 하기 전에 어떻게 변경 되는지 있도록를 클라우드 인프라를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="5244b-106">또한 배웁니다 방법을 Terraform를 사용 하 여 Azure에서 toocreate 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="5244b-107">tooget 시작 (Visual Studio 코드/Sublime/Vim/등)가 원하는 텍스트 편집기에서 \terraform_azure101.tf 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="5244b-108">hello 파일의 정확한 이름을 hello의 hello 폴더 이름을 매개 변수로 허용 하는 Terraform 없으므로 들이 중요 하지 않습니다: hello 폴더에서 모든 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="5244b-109">Hello를 hello 새 파일에 코드 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="5244b-110">Hello에 `provider` hello 섹션 스크립트 hello 스크립트의 Terraform toouse Azure 공급자 tooprovision 리소스 알립니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="5244b-111">subscription_id, appId, 암호 및 tenant_id에 대 한 tooget 값 참조 hello [설치 및 Terraform 구성](terraform-install-configure.md) 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="5244b-112">이 블록의 hello 값에 대 한 환경 변수를 만든 경우 tooinclude 않아도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="5244b-113">hello `azurerm_resource_group` 리소스 Terraform toocreate 새 리소스 그룹에 게 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="5244b-114">이 문서의 뒷부분에 나오는 Terraform에서 사용할 수 있는 더 많은 리소스 유형을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="5244b-115">Hello 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="5244b-115">Execute hello script</span></span>
<span data-ttu-id="5244b-116">Hello 스크립트를 저장 한 후 toohello 콘솔/명령 줄을 종료 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="5244b-117">Azure에 대 한 tooinitialize Terraform 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="5244b-118">Hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="5244b-119">있다고 가정 `terraformscripts` 는 hello 스크립트 저장 된 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="5244b-120">Hello 사용 `plan` Terraform 명령을 hello 스크립트에 정의 된 hello 리소스를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="5244b-121">다음 출력 hello 계획된 실행 및 Terraform에서 저장 하는 상태 정보가 toohello 비교 하기 _없이_ Azure에서 리소스를 실제로 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="5244b-122">Hello 이전 명령을 실행 하면 다음 화면 hello 유사한 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform 계획](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="5244b-124">모두 제대로 표시 하는 경우 hello 다음을 실행 하 여 Azure에서이 새 리소스 그룹 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="5244b-125">Hello Azure 포털에서에서 라는 hello 새 빈 리소스 그룹을 확인 해야 `terraformtest`합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="5244b-126">Hello 섹션 뒤, 가상 컴퓨터 및 모든 해당 가상 컴퓨터 toohello 리소스 그룹에 대 한 지원 인프라 hello 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="5244b-127">Terraform으로 Ubuntu VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="5244b-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="5244b-128">보겠습니다 필요한 tooprovision 있는 hello 세부 정보를 사용 하 여 만든 म hello Terraform 스크립트 Ubuntu를 실행 하는 가상 컴퓨터 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="5244b-129">다음 섹션 hello를 프로 비전 하는 hello 리소스를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="5244b-130">단일 서브넷이 있는 네트워크</span><span class="sxs-lookup"><span data-stu-id="5244b-130">A network with a single subnet</span></span>
* <span data-ttu-id="5244b-131">네트워크 인터페이스 카드</span><span class="sxs-lookup"><span data-stu-id="5244b-131">A network interface card</span></span> 
* <span data-ttu-id="5244b-132">저장소 컨테이너가 있는 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="5244b-132">A storage account with a storage container</span></span>
* <span data-ttu-id="5244b-133">공용 IP</span><span class="sxs-lookup"><span data-stu-id="5244b-133">A public IP</span></span>
* <span data-ttu-id="5244b-134">모든 hello 이전 리소스를 활용 하는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="5244b-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="5244b-135">각 hello Azure Terraform 리소스에 대 한 철저 한 설명서 참조 hello [Terraform 설명서](https://www.terraform.io/docs/providers/azurerm/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="5244b-136">전체 버전의 hello hello [프로비저닝](#complete-terraform-script) 편의 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="5244b-137">Hello Terraform 스크립트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-137">Extend hello Terraform script</span></span>
<span data-ttu-id="5244b-138">다음과 같이 hello 다음 리소스를 사용 하 여 만든 hello 스크립트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-138">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="5244b-139">hello 이전 스크립트는 가상 네트워크와 가상 네트워크 내의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="5244b-140">Hello 참조 toohello 리소스 그룹 "${azurerm_resource_group.helloterraform.name}" hello 가상 네트워크와 hello 서브넷 정의 통해 이미 만든 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}
~~~~
<span data-ttu-id="5244b-141">hello 이전 스크립트 조각에서 만든 hello 공용 IP를 활용 하는 네트워크 인터페이스와 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="5244b-142">참고 hello toosubnet_id와 public_ip_address_id 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="5244b-143">Terraform에 기본 제공 intelligence toounderstand hello 해당 네트워크 인터페이스에 종속 되어 hello 리소스 hello 네트워크 인터페이스의 hello 생성 하기 전에 해당 필요 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
<span data-ttu-id="5244b-144">여기에서 저장소 계정을 만들고 해당 저장소 계정 내에서 저장소 컨테이너를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="5244b-145">이 저장소 계정은 toobe 생성에 대 한 hello 가상 컴퓨터에 대 한 가상 하드 디스크 (Vhd)를 저장 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
<span data-ttu-id="5244b-146">마지막으로, hello 이전 코드 조각에서 이미 프로 비전 하는 모든 hello 리소스를 활용 하는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="5244b-147">저장소 계정 및 VHD는 공용 IP 및 서브넷을 지정 하는 네트워크 인터페이스에 대 한 컨테이너 이며 hello 리소스 그룹이 이미 만든 경우.</span><span class="sxs-lookup"><span data-stu-id="5244b-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="5244b-148">Note hello vm_size 속성을 여기서 hello 스크립트 Azure A0 SKU를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="5244b-149">Hello 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="5244b-149">Execute hello script</span></span>
<span data-ttu-id="5244b-150">저장 hello 전체 스크립트를 사용 하면 toohello 콘솔/명령줄을 종료 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="5244b-151">일정 시간이 지난 후 hello 리소스를 가상 컴퓨터를 포함 하 여 hello에 표시 `terraformtest` hello Azure 포털에서에서 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="5244b-152">전체 Terraform 스크립트</span><span class="sxs-lookup"><span data-stu-id="5244b-152">Complete Terraform script</span></span>

<span data-ttu-id="5244b-153">사용자 편의 위해 다음은 전체 Terraform 스크립트 hello이이 문서에서 설명 하는 hello 인프라의 모든 해당 프로 비전입니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
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
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5244b-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5244b-154">Next steps</span></span>
<span data-ttu-id="5244b-155">Terraform을 사용하여 Azure에서 기본 인프라를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="5244b-156">부하 분산 장치 및 가상 컴퓨터 확장 집합을 사용하는 예제를 비롯한 보다 복잡한 시나리오는 여러 가지 [Azure에 대한 Terraform 예제](https://github.com/hashicorp/terraform/tree/master/examples)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5244b-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="5244b-157">지원 되는 Azure 공급자의 최신 목록, 참조 hello [Terraform 설명서](https://www.terraform.io/docs/providers/azurerm/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="5244b-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
