---
title: "고정 공용 IP가 있는 VM 만들기 - Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스) 2.0을 사용하여 고정 공용 IP 주소가 있는 VM을 만드는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c32694949880037f01bb2b6b9779d2cbb9809c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-cli-20"></a><span data-ttu-id="1ebcb-103">Azure CLI 2.0을 사용하여 고정 공용 IP 주소가 있는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1ebcb-103">Create a VM with a static public IP address using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ebcb-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1ebcb-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="1ebcb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ebcb-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="1ebcb-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1ebcb-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="1ebcb-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1ebcb-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="1ebcb-108">템플릿</span><span class="sxs-lookup"><span data-stu-id="1ebcb-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="1ebcb-109">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="1ebcb-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="1ebcb-110">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="1ebcb-111">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 클래식 배포 모델 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-111">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="1ebcb-112"><a name = "create"></a>VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1ebcb-112"><a name = "create"></a>Create the VM</span></span>

<span data-ttu-id="1ebcb-113">Azure CLI 2.0(이 문서) 또는 [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)을 사용하여 이 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-113">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="1ebcb-114">다음 단계에서 변수에 대한 ""의 값은 시나리오의 설정을 사용하여 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-114">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="1ebcb-115">사용자 환경에 적절한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-115">Change the values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="1ebcb-116">[Azure CLI 2.0](/cli/azure/install-az-cli2)을 아직 설치하지 않은 경우 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-116">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="1ebcb-117">[Linux VM에 SSH 공용 및 개인 키 쌍 만들기](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)의 단계를 완료하여 Linux VM에 SSH 공용 및 개인 키 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-117">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="1ebcb-118">명령 셸에서 `az login` 명령을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-118">From a command shell, login with the command `az login`.</span></span>
4. <span data-ttu-id="1ebcb-119">Linux 또는 Mac 컴퓨터에서 다음에 나오는 스크립트를 실행하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-119">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="1ebcb-120">Azure 공용 IP 주소, 가상 네트워크, 네트워크 인터페이스 및 VM 리소스는 모두 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-120">The Azure public IP address, virtual network, network interface, and VM resources must all exist in the same location.</span></span> <span data-ttu-id="1ebcb-121">리소스가 모두 동일한 리소스 그룹에 위치할 필요는 없습니다. 하지만 다음 스크립트에서는 모두 동일한 리소스 그룹에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-121">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using the --allocation-method Static option.
# If you do not specify this option, the address is allocated dynamically. The address is assigned to the
# resource from a pool of IP adresses unique to each Azure region. The DnsName must be unique within the
# Azure location it's created in. Download and view the file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists the ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected to the VNet with a static private IP address and associate the public IP address
# resource to the NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with the NIC

VmName="WEB1"

# Replace the value for the VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace the value for the OsImage variable with a value for *urn* from the output returned by entering
# the `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace the following value with the path to your public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove the previous line and you'll be prompted for the password you want to configure for the VM.
```

<span data-ttu-id="1ebcb-122">스크립트는 VM 외에도 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-122">In addition to creating a VM, the script creates:</span></span>
- <span data-ttu-id="1ebcb-123">기본적으로 단일 프리미엄이 디스크를 관리했지만 만들 수 있는 디스크 유형에 대한 다른 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-123">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="1ebcb-124">자세한 내용은 [Azure CLI 2.0을 사용하여 Linux VM 만들기](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-124">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="1ebcb-125">가상 네트워크, 서브넷, NIC 및 공용 IP 주소 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="1ebcb-126">또는 *기존* 가상 네트워크, 서브넷, NIC 또는 공용 IP 주소 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="1ebcb-127">추가 리소스를 만드는 것이 아니라 기존 네트워크 리소스를 사용하는 방법을 알아보려면 `az vm create -h`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-127">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="1ebcb-128"><a name = "validate"></a>VM 생성 및 공용 IP 주소의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1ebcb-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="1ebcb-129">`az resource list --resouce-group IaaSStory --output table` 명령을 입력하여 스크립트로 만든 리소스의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-129">Enter the command `az resource list --resouce-group IaaSStory --output table` to see a list of the resources created by the script.</span></span> <span data-ttu-id="1ebcb-130">반환된 출력에 네트워크 인터페이스, 디스크, 공용 IP 주소, 가상 네트워크 및 가상 컴퓨터와 같은 5개의 리소스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-130">There should be five resources in the returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="1ebcb-131">`az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-131">Enter the command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="1ebcb-132">반환된 출력에서 **IpAddress** 값을 확인하고 **PublicIpAllocationMethod** 값이 *고정*인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-132">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="1ebcb-133">다음 명령을 실행하기 전에 <>를 제거하고 *사용자 이름*을 스크립트의 **사용자 이름** 변수에 사용된 이름으로 바꾸고 *ipAddress*를 이전 단계의 **ipAddress**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-133">Before executing the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span></span> <span data-ttu-id="1ebcb-134">`ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>` 명령을 실행하여 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-134">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="1ebcb-135"><a name= "clean-up"></a>VM 및 관련된 리소스 제거</span><span class="sxs-lookup"><span data-stu-id="1ebcb-135"><a name= "clean-up"></a>Remove the VM and associated resources</span></span>

<span data-ttu-id="1ebcb-136">프로덕션에서 VM을 사용하지 않는 경우 이 연습에서 만든 리소스를 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-136">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="1ebcb-137">VM, 공용 IP 주소 및 디스크 리소스를 프로비전하는 경우 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="1ebcb-138">이 연습에서 만든 리소스를 제거하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-138">To remove the resources created during this exercise, complete the following steps:</span></span>

1. <span data-ttu-id="1ebcb-139">리소스 그룹의 리소스를 보려면 `az resource list --resource-group IaaSStory` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-139">To view the resources in the resource group, run the `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="1ebcb-140">리소스 그룹에 이 문서의 스크립트에서 만든 리소스 외에 다른 리소스가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-140">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span></span> 
3. <span data-ttu-id="1ebcb-141">이 연습에서 만든 모든 리소스를 삭제하려면 `az group delete -n IaaSStory` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-141">To delete all resources created in this exercise, run the `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="1ebcb-142">이 명령은 리소스 그룹과 그 속에 포함된 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-142">The command deletes the resource group and all the resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ebcb-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ebcb-143">Next steps</span></span>

<span data-ttu-id="1ebcb-144">이 문서에서 만든 VM 간에 네트워크 트래픽을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-144">Any network traffic can flow to and from the VM created in this article.</span></span> <span data-ttu-id="1ebcb-145">네트워크 인터페이스, 서브넷 또는 둘 간에 전달할 수 있는 트래픽을 제한하는 NSG 내에서 인바운드 및 아웃바운드 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-145">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from the network interface, the subnet, or both.</span></span> <span data-ttu-id="1ebcb-146">NSG에 대해 자세히 알아보려면 [NSG 개요](virtual-networks-nsg.md) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="1ebcb-146">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span></span>