---
title: "Azure VM을 확장 집합으로 변환 | Microsoft Docs"
description: "Azure CLI를 사용하여 Linux Azure 가상 컴퓨터 확장 집합을 만들고 배포합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: 8d3376d2791b1349298db618d475ce5573083702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-an-existing-azure-virtual-machine-to-a-scale-set"></a><span data-ttu-id="4f841-103">기존 Azure 가상 컴퓨터를 확장 집합으로 변환</span><span class="sxs-lookup"><span data-stu-id="4f841-103">Convert an existing Azure virtual machine to a scale set</span></span>

<span data-ttu-id="4f841-104">이 자습서는 Azure CLI 2.0을 사용하여 가상 컴퓨터를 가상 컴퓨터 확장 집합으로 변환하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-104">This tutorial shows you how to use Azure CLI 2.0 to convert a virtual machine to a virtual machine scale set.</span></span> <span data-ttu-id="4f841-105">확장 집합에서 가상 컴퓨터의 구성을 자동화하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-105">You also learn how to automate the configuration of the virtual machines in the scale set.</span></span> <span data-ttu-id="4f841-106">Azure CLI 2.0을 설치하는 방법에 대한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f841-106">For more information on how to install Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="4f841-107">규모 집합에 대한 자세한 내용은 [가상 컴퓨터 규모 집합](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f841-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-the-vm"></a><span data-ttu-id="4f841-108">1단계 - VM 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="4f841-108">Step 1 - Deprovision the VM</span></span>

<span data-ttu-id="4f841-109">SSH를 사용하여 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-109">Use SSH to connect to the VM.</span></span>

<span data-ttu-id="4f841-110">Azure VM 에이전트를 사용하여 VM 프로비전을 해제하여 파일과 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-110">Deprovision the VM using the Azure VM agent to delete files and data.</span></span> <span data-ttu-id="4f841-111">프로비전 해제에 대한 세부적인 개요는 [Linux 가상 컴퓨터 캡처](capture-image.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f841-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-the-vm"></a><span data-ttu-id="4f841-112">2단계 - VM 이미지 캡처</span><span class="sxs-lookup"><span data-stu-id="4f841-112">Step 2 - Capture an image of the VM</span></span>

<span data-ttu-id="4f841-113">캡처에 대한 세부적인 개요는 [Linux 가상 컴퓨터 캡처](capture-image.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f841-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="4f841-114">[az vm deallocate](/cli/azure/vm#deallocate)로 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-114">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4f841-115">[az vm generalize](/cli/azure/vm#generalize)로 VM을 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-115">Generalize the VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4f841-116">[az image create](/cli/azure/image#create)로 VM 리소스에서 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-116">Create an image from the VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-the-scale-set"></a><span data-ttu-id="4f841-117">3단계 - 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="4f841-117">Step 3 - Create the scale set</span></span>

<span data-ttu-id="4f841-118">이미지의 **id**를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-118">Get the **id** of the image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="4f841-119">[az vm create](/cli/azure/vmss#create)를 사용하여 이미지 리소스에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="4f841-120">이 명령은 10GB 데이터 디스크도 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="4f841-121">선택한 VM 크기(**Standard_DS1_v2**가 사용됨)에 따라 허용되는 데이터 디스크 수가 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-121">Keep in mind that depending on the VM size chosen (we used **Standard_DS1_v2**), the number of data disks allowed is different.</span></span> <span data-ttu-id="4f841-122">자세한 내용은 [가상 컴퓨터 크기](sizes.md)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="4f841-122">For more information, review the [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="4f841-123">확장 집합이 완료되면 확장 집합에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-123">Once the scale set finishes, connect to it.</span></span> <span data-ttu-id="4f841-124">[az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info)를 사용하여 SSH를 위한 인스턴스의 IP 주소 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-124">Get a list of IP addresses for the instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="4f841-125">이제 가상 컴퓨터 인스턴스에 연결하여 데이터 디스크를 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-125">Now you can connect to the virtual machine instance to initialize the data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-the-data-disk"></a><span data-ttu-id="4f841-126">4단계 - 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="4f841-126">Step 4 - Initialize the data disk</span></span>

<span data-ttu-id="4f841-127">가상 컴퓨터에 연결되어 있는 동안 `fdisk`를 사용하여 디스크를 파티션합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-127">While connected to the virtual machine, partition the disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="4f841-128">`mkfs` 명령을 사용하여 파티션에 파일 시스템을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-128">Write a file system to the partition with the `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="4f841-129">운영 체제에서 액세스할 수 있도록 새 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-129">Mount the new disk so that it is accessible in the operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="4f841-130">이제 데이터 드라이브 탑재 지점을 통해 디스크에 액세스할 수 있으며 `ls /datadrive/`를 사용하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-130">The disk can now be accesses through the datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="4f841-131">SSH 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-131">End the SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="4f841-132">5단계 - 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="4f841-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="4f841-133">방화벽을 통해 확장 집합이 호스트하는 웹 서버에 구멍을 냅니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-133">Punch a hole through the firewall to the webserver hosted by the scale set.</span></span> <span data-ttu-id="4f841-134">확장 집합이 생성될 때 부하 분산 장치도 만들어지며 개별적인 가상 컴퓨터에 **SSH**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-134">When the scale set was created, a load balancer was also created, and you used it **SSH** to the individual virtual machines.</span></span> <span data-ttu-id="4f841-135">포트를 열려면 두 가지 정보가 필요하며 Azure CLI를 사용하여 해당 정보를 구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-135">To open a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="4f841-136">**프런트 엔드 IP 주소 풀**</span><span class="sxs-lookup"><span data-stu-id="4f841-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="4f841-137">**백 엔드 IP 주소 풀**</span><span class="sxs-lookup"><span data-stu-id="4f841-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="4f841-138">이러한 두 가지 이름을 사용하여 포트 **80**을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="4f841-139">6단계 – 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="4f841-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="4f841-140">데이터 디스크는 각각의 가상 컴퓨터 인스턴스에서 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-140">The data disk needs to be configured on each virtual machine instance.</span></span> <span data-ttu-id="4f841-141">**CustomScript** 확장을 사용하여 가상 컴퓨터 구성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-141">We can automate the configuration of the virtual machine with the **CustomScript** extension.</span></span>

<span data-ttu-id="4f841-142">먼저 디스크 포맷 명령을 포함하는 *.sh* 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-142">First, create a *.sh* script that includes the disk format commands.</span></span>

```sh
#!/bin/bash

# Setup the data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="4f841-143">다음으로 이 스크립트 파일을 **CustomScript** 확장이 액세스할 수 있는 위치에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-143">Next, upload that script file to where the **CustomScript** extension can access it.</span></span> <span data-ttu-id="4f841-144">복사본은 [여기](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="4f841-145">**settings.json**이라는 이름의 로컬 파일을 만들고 다음 JSON 블록을 파일에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-145">Create a local file named **settings.json** and put the following JSON block in it.</span></span> <span data-ttu-id="4f841-146">`flieUris` 속성은 스크립트 파일을 업로드한 위치로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-146">The `flieUris` property should be set to where your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="4f841-147">방금 만든 **settings.json** 파일을 참조하는 **CustomScript** 확장을 사용하여 확장 집합에 이 명령을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-147">Deploy this command to your scale set with the **CustomScript** extension, referencing the **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="4f841-148">이 확장은 현재의 모든 인스턴스와 나중에 크기 조정에 의해 생성되는 모든 인스턴스에서 자동으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="4f841-149">7단계 - 자동 크기 조정 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="4f841-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="4f841-150">현재 자동 크기 조정 규칙은 Azure CLI에서 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="4f841-151">자동 크기 조정을 구성하려면 [Azure Portal](https://portal.azure.com)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="4f841-151">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="4f841-152">8단계 - 관리 작업</span><span class="sxs-lookup"><span data-stu-id="4f841-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="4f841-153">확장 집합의 수명 주기 내내 하나 이상의 관리 작업을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-153">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="4f841-154">또한 다양한 수명 주기 작업을 자동화하는 스크립트를 만들어야 하는 경우도 있습니다. Azure CLI는 이러한 작업을 수행할 수 있는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-154">Additionally, you may want to create scripts that automate various lifecycle-tasks, and the Azure CLI provides a quick way to do those tasks.</span></span> <span data-ttu-id="4f841-155">다음은 몇 가지 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="4f841-156">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f841-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="4f841-157">인스턴스 수 설정(수동 크기 조정)</span><span class="sxs-lookup"><span data-stu-id="4f841-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="4f841-158">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="4f841-158">Delete resource group</span></span>

<span data-ttu-id="4f841-159">리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f841-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4f841-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f841-160">Next steps</span></span>
<span data-ttu-id="4f841-161">이 자습서에 소개된 일부 가상 컴퓨터 확장 집합 기능에 대한 자세한 내용은 다음 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f841-161">To learn more about some of the virtual machine scale set features introduced in this tutorial, see the following information:</span></span>

- [<span data-ttu-id="4f841-162">Azure Virtual Machine Scale Sets 개요</span><span class="sxs-lookup"><span data-stu-id="4f841-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="4f841-163">Azure Load Balancer개요</span><span class="sxs-lookup"><span data-stu-id="4f841-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="4f841-164">네트워크 보안 그룹을 사용하여 네트워크 트래픽 흐름 제어</span><span class="sxs-lookup"><span data-stu-id="4f841-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)