---
title: "aaaConvert 하는 Azure VM tooa 범위로 설정 | Microsoft Docs"
description: "만들고 hello Azure CLI를 사용 하 여 설정 Linux Azure 가상 컴퓨터 크기를 배포 합니다."
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
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="143cf-103">기존 Azure 가상 컴퓨터 tooa 눈금 집합으로 변환</span><span class="sxs-lookup"><span data-stu-id="143cf-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="143cf-104">이 자습서는 가상 컴퓨터 tooa 가상 컴퓨터 크기 설정 하는 Azure CLI 2.0 toouse tooconvert 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="143cf-105">또한 hello 규모에 맞게 hello 가상 컴퓨터의 tooautomate hello 구성을 설정 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="143cf-106">Tooinstall Azure CLI 2.0을 확인 하려면 어떻게 해야 대 한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="143cf-107">규모 집합에 대한 자세한 내용은 [가상 컴퓨터 규모 집합](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="143cf-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="143cf-108">1 단계-Deprovision hello VM</span><span class="sxs-lookup"><span data-stu-id="143cf-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="143cf-109">SSH tooconnect toohello VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="143cf-110">프로 비전 해제 hello VM hello Azure VM 에이전트 toodelete 파일 및 데이터를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="143cf-111">프로비전 해제에 대한 세부적인 개요는 [Linux 가상 컴퓨터 캡처](capture-image.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="143cf-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="143cf-112">2 단계-hello VM의 이미지 캡처</span><span class="sxs-lookup"><span data-stu-id="143cf-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="143cf-113">캡처에 대한 세부적인 개요는 [Linux 가상 컴퓨터 캡처](capture-image.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="143cf-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="143cf-114">Deallocate의 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="143cf-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="143cf-115">일반화의 VM hello [az vm 일반화](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="143cf-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="143cf-116">사용 하 여 hello VM 리소스에서 이미지 만들기 [az 이미지 만들기](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="143cf-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="143cf-117">3 단계-hello 크기 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="143cf-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="143cf-118">Hello 가져오기 **id** hello 이미지의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="143cf-119">[az vm create](/cli/azure/vmss#create)를 사용하여 이미지 리소스에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="143cf-120">이 명령은 10GB 데이터 디스크도 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="143cf-121">Hello VM에 따라 선택한 크기는 (사용 **Standard_DS1_v2**), 허용 되는 데이터 디스크의 hello 번호가 다르면 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="143cf-122">자세한 내용을 보려면 검토 hello [가상 컴퓨터 크기](sizes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="143cf-123">Hello 배율 설정 완료 되 면 tooit을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="143cf-124">와 SSH에 대 한 hello 인스턴스 IP 주소의 목록을 가져올 [az vmss 목록-인스턴스-연결-정보](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="143cf-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="143cf-125">이제 toohello 가상 컴퓨터 인스턴스 tooinitialize hello 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="143cf-126">4 단계-hello 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="143cf-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="143cf-127">연결 된 toohello 가상 컴퓨터를 하는 동안와 hello 디스크 파티션 `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="143cf-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="143cf-128">Hello로 파일 시스템 toohello 파티션에 쓰기 `mkfs` 명령:</span><span class="sxs-lookup"><span data-stu-id="143cf-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="143cf-129">Hello 운영 체제에 액세스할 수 있도록 hello 새 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="143cf-130">hello 디스크 hello datadrive 탑재 지점,으로 확인할 수 있습니다를 통해 액세스 될 수 있습니다 `ls /datadrive/`합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="143cf-131">Hello SSH 세션을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="143cf-132">5단계 - 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="143cf-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="143cf-133">Hello 방화벽 toohello 웹 서버 hello 크기 집합에서 호스트를 통해 구멍을 펀치 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="143cf-134">Hello 크기 집합 만들었고, 부하 분산 장치도 생성을 사용 하는 경우 **SSH** toohello 개별 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="143cf-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="143cf-135">두 가지 정보를 얻을 수 해야 포트 tooopen Azure CLI를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="143cf-136">**프런트 엔드 IP 주소 풀**</span><span class="sxs-lookup"><span data-stu-id="143cf-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="143cf-137">**백 엔드 IP 주소 풀**</span><span class="sxs-lookup"><span data-stu-id="143cf-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="143cf-138">이러한 두 가지 이름을 사용하여 포트 **80**을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="143cf-139">6단계 – 구성 자동화</span><span class="sxs-lookup"><span data-stu-id="143cf-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="143cf-140">hello 데이터 디스크 toobe 각 가상 컴퓨터 인스턴스에서 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="143cf-141">Hello로 hello 가상 컴퓨터의 hello 구성을 자동화할 수 우리 **CustomScript** 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="143cf-142">먼저 만듭니다는 *.sh* hello 디스크 형식 명령을 포함 하는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="143cf-143">그런 다음 해당 스크립트 파일 toowhere hello 업로드 **CustomScript** 확장에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="143cf-144">복사본은 [여기](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="143cf-145">라는 로컬 파일을 만들어 **settings.json** put hello JSON 블록에 다음 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="143cf-146">hello `flieUris` 속성을 설정 해야 toowhere 스크립트 파일에 업로드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="143cf-147">이 명령은 tooyour 규모 hello를 사용 하 여 설정 배포 **CustomScript** hello 참조 확장 **settings.json** 방금 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="143cf-148">이 확장은 현재의 모든 인스턴스와 나중에 크기 조정에 의해 생성되는 모든 인스턴스에서 자동으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="143cf-149">7단계 - 자동 크기 조정 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="143cf-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="143cf-150">현재 자동 크기 조정 규칙은 Azure CLI에서 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="143cf-151">사용 하 여 hello [Azure 포털](https://portal.azure.com) tooconfigure 자동 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="143cf-152">8단계 - 관리 작업</span><span class="sxs-lookup"><span data-stu-id="143cf-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="143cf-153">Hello 크기 집합의 hello 수명 주기 동안 toorun 할 수 있습니다 하나 이상의 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="143cf-154">또한 다양 한 수명 주기 작업을 자동화 하는 toocreate 스크립트 할 수도 있습니다 하 고 hello Azure CLI 신속 하 게 toodo를 해당 작업 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="143cf-155">다음은 몇 가지 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="143cf-156">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="143cf-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="143cf-157">인스턴스 수 설정(수동 크기 조정)</span><span class="sxs-lookup"><span data-stu-id="143cf-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="143cf-158">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="143cf-158">Delete resource group</span></span>

<span data-ttu-id="143cf-159">리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="143cf-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="143cf-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="143cf-160">Next steps</span></span>
<span data-ttu-id="143cf-161">이 자습서에 도입 된 기능을 설정 hello 가상 컴퓨터 크기 중 일부에 대 한 자세한 toolearn hello 다음 정보를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="143cf-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="143cf-162">Azure Virtual Machine Scale Sets 개요</span><span class="sxs-lookup"><span data-stu-id="143cf-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="143cf-163">Azure Load Balancer개요</span><span class="sxs-lookup"><span data-stu-id="143cf-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="143cf-164">네트워크 보안 그룹을 사용하여 네트워크 트래픽 흐름 제어</span><span class="sxs-lookup"><span data-stu-id="143cf-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)