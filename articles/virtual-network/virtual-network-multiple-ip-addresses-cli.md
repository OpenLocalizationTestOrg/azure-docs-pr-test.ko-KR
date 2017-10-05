---
title: "Azure CLI 2.0을 사용하여 여러 IP 주소가 있는 VM | Microsoft Docs"
description: "Azure CLI 2.0 | Resource Manager를 사용하여 가상 컴퓨터에 여러 IP 주소를 할당하는 방법을 알아봅니다."
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
ms.openlocfilehash: 0e9b2ef89ca39a7988a7b2573496a605dfc604b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-cli-20"></a><span data-ttu-id="cf7d0-103">Azure CLI 2.0을 사용하여 가상 컴퓨터에 여러 IP 주소 할당</span><span class="sxs-lookup"><span data-stu-id="cf7d0-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="cf7d0-104">이 문서는 Azure CLI 2.0을 사용하여 Azure Resource Manager 배포 모델을 통해 VM(가상 컴퓨터)을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span></span> <span data-ttu-id="cf7d0-105">클래식 배포 모델을 통해 생성된 리소스에 여러 IP 주소를 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="cf7d0-106">Azure 배포 모델에 대해 자세히 알아보려면 [배포 모델 이해](../resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="cf7d0-107"><a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="cf7d0-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="cf7d0-108">Azure CLI 2.0(이 문서) 또는 [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md)을 사용하여 이 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="cf7d0-109">사용자 환경에 적절한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-109">Change the values, as appropriate, for your environment.</span></span> <span data-ttu-id="cf7d0-110">다음 단계는 시나리오에 설명된 대로 여러 IP 주소를 가진 예시 VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="cf7d0-111">""의 변수 값과 IP 주소 유형을 구현에 필요한 대로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="cf7d0-112">[Azure CLI 2.0](/cli/azure/install-az-cli2)을 아직 설치하지 않은 경우 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="cf7d0-113">[Linux VM에 SSH 공용 및 개인 키 쌍 만들기](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json)의 단계를 완료하여 Linux VM에 SSH 공용 및 개인 키 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="cf7d0-114">명령 셸에서 `az login` 명령을 사용하고 사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-114">From a command shell, login with the command `az login` and select the subscription you're using.</span></span>
4. <span data-ttu-id="cf7d0-115">Linux 또는 Mac 컴퓨터에서 다음에 나오는 스크립트를 실행하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="cf7d0-116">스크립트는 리소스 그룹, 하나의 VNet(가상 네트워크), 세 개의 IP 구성이 있는 하나의 NIC 및 연결된 두 개의 NIC가 있는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="cf7d0-117">NIC, 공용 IP 주소, 가상 네트워크 및 VM 리소스는 모두 동일한 위치 및 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="cf7d0-118">리소스가 모두 동일한 리소스 그룹에 위치할 필요는 없습니다. 하지만 다음 스크립트에서는 모두 동일한 리소스 그룹에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using the `--allocation-method Static` option. If you
# do not specify this option, the address is allocated dynamically. The address is assigned to the resource from a pool
# of IP adresses unique to each Azure region. Download and view the file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists the ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected to the subnet and associate the public IP address to it. Azure will create the
# first IP configuration with a static private IP address and will associate the public IP address resource to it.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it to the NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it to the NIC. This configuration has  static private IP address and   # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations
# to any NIC in a VM. To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach the NIC.

VmName="myVm"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. The script fails if the VM size
# is not supported in the location you select. Run the `azure vm sizes --location estcentralus` command to get a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace the value for the OsImage variable value with a value for *urn* from the utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file. If you're creating a Windows VM, remove the following
# line and you'll be prompted for the password you want to configure for the VM.

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
```

<span data-ttu-id="cf7d0-119">스크립트는 세 가지 IP 구성의 NIC로 VM을 만드는 것 외에 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span></span>

- <span data-ttu-id="cf7d0-120">기본적으로 단일 프리미엄이 디스크를 관리했지만 만들 수 있는 디스크 유형에 대한 다른 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="cf7d0-121">자세한 내용은 [Azure CLI 2.0을 사용하여 Linux VM 만들기](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="cf7d0-122">하나의 서브넷 및 두 개의 공용 IP 주소를 가진 가상 네트워크.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="cf7d0-123">또는 *기존* 가상 네트워크, 서브넷, NIC 또는 공용 IP 주소 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="cf7d0-124">추가 리소스를 만드는 것이 아니라 기존 네트워크 리소스를 사용하는 방법을 알아보려면 `az vm create -h`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="cf7d0-125">공용 IP 주소에는 명목 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cf7d0-126">IP 주소 가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cf7d0-127">구독 내에서 사용할 수 있는 공용 IP 주소의 수는 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cf7d0-128">이러한 한에 대한 자세한 내용은 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="cf7d0-129">VM을 만든 후에 `az network nic show --name MyNic1 --resource-group myResourceGroup` 명령을 입력하여 NIC 구성을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span></span> <span data-ttu-id="cf7d0-130">`az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table`을 입력하여 NIC에 연결된 IP 구성의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span></span>

<span data-ttu-id="cf7d0-131">이 문서의 [VM 운영 체제에 IP 주소 추가](#os-config) 섹션에 나오는 사용자 운영 체제별 단계를 완료하여 개인 IP 주소를 VM 운영 체제에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="cf7d0-132"><a name="add"></a>VM에 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="cf7d0-132"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="cf7d0-133">다음 단계를 완료하여 개인 및 공용 IP 주소를 기존 NIC에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="cf7d0-134">예제는 이 문서에서 설명된 [시나리오](#Scenario)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-134">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="cf7d0-135">명령 셸을 열고 단일 세션 내에서 이 섹션의 나머지 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-135">Open a command shell and complete the remaining steps in this section within a single session.</span></span> <span data-ttu-id="cf7d0-136">아직 Azure CLI를 설치 및 구성하지 않은 경우 [Azure CLI 2.0 설치](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서에 나오는 단계를 완료하고 `az-login` 명령을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span></span>

2. <span data-ttu-id="cf7d0-137">요구 사항에 따라 다음 섹션 중 하나의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-137">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="cf7d0-138">**개인 IP 주소 추가**</span><span class="sxs-lookup"><span data-stu-id="cf7d0-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="cf7d0-139">NIC에 개인 IP 주소를 추가하려면 다음 명령을 사용하여 IP 구성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span></span> <span data-ttu-id="cf7d0-140">고정 IP 주소는 서브넷에 사용되지 않는 주소여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-140">The static IP address must be an unused address for the subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="cf7d0-141">고유한 구성 이름과 개인 IP 주소를 사용하여 필요한 만큼 구성을 만듭니다(정적 IP 주소를 가진 구성의 경우).</span><span class="sxs-lookup"><span data-stu-id="cf7d0-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="cf7d0-142">**공용 IP 주소 추가**</span><span class="sxs-lookup"><span data-stu-id="cf7d0-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="cf7d0-143">공용 IP 주소는 새 IP 구성 또는 기존 IP 구성에 연결하면 해당 주소가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="cf7d0-144">필요에 따라 이후 섹션 중 하나에 나와 있는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-144">Complete the steps in one of the sections that follow, as you require.</span></span>

    <span data-ttu-id="cf7d0-145">공용 IP 주소에는 명목 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cf7d0-146">IP 주소 가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cf7d0-147">구독 내에서 사용할 수 있는 공용 IP 주소의 수는 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cf7d0-148">이러한 한에 대한 자세한 내용은 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="cf7d0-149">**새 IP 구성에 리소스 연결**</span><span class="sxs-lookup"><span data-stu-id="cf7d0-149">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="cf7d0-150">새 IP 구성의 공용 IP 주소를 추가할 때마다 모든 IP 구성 시 개인 IP 주소가 있어야 하기 때문에 개인 IP 주소도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="cf7d0-151">기존 공용 IP 주소 리소스를 추가하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="cf7d0-152">새 파일을 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-152">To create a new one, enter the following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="cf7d0-153">고정 개인 IP 주소 및 여기에 연결된 *myPublicP3* 공용 IP 주소 리소스가 있는 새 IP 구성을 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="cf7d0-154">**기존 IP 구성에 리소스 연결** 공용 IP 주소 리소스에 아직 연결 되어 있는 IP 구성에 연결할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="cf7d0-155">다음 명령을 입력하면 IP 구성에 연결된 공용 IP 주소가 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="cf7d0-156">반환되는 출력:</span><span class="sxs-lookup"><span data-stu-id="cf7d0-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="cf7d0-157">*IpConfig-3*에 대한 **PublicIpAddressId** 열이 출력에서 비어 있기 때문에 현재 공용 IP 주소 리소스가 여기에 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="cf7d0-158">IpConfig-3에 기존 공용 IP 주소 리소스를 추가하거나 다음 명령을 입력하여 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="cf7d0-159">*IPConfig 3*이라는 기존 IP 구성에 공용 IP 주소 리소스를 연결하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="cf7d0-160">NIC에 할당된 개인 IP 주소 및 공용 IP 주소 리소스 ID를 보려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="cf7d0-161">반환되는 출력:</span><span class="sxs-lookup"><span data-stu-id="cf7d0-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="cf7d0-162">이 문서의 [VM 운영 체제에 IP 주소 추가](#os-config) 섹션에 나오는 지침에 따라 NIC에 추가한 개인 IP 주소를 VM 운영 체제에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="cf7d0-163">운영 체제에 공용 IP 주소를 추가하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="cf7d0-163">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
