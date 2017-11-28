---
title: "Azure Linux VM을 캡처하여 템플릿으로 사용 | Microsoft Docs"
description: "Azure Resource Manager 배포 모델을 사용하여 만든, Linux 기반 Azure VM(가상 컴퓨터)의 이미지를 캡처하고 일반화하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="1325e-103">Azure에서 실행되는 Linux 가상 컴퓨터 캡처하기</span><span class="sxs-lookup"><span data-stu-id="1325e-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="1325e-104">Resource Manager 배포 모델에서 Azure Linux 가상 컴퓨터(VM)을 일반화하고 캡처하려면 이 문서의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="1325e-105">VM을 일반화하는 경우 개인 계정 정보를 제거하고 VM이 이미지로 사용되도록 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="1325e-106">그런 다음 OS용 일반화된 VHD(가상 하드 디스크) 이미지, 연결된 데이터 디스크용 VHD, 새 VM 배포용 [Resource Manager 템플릿](../../azure-resource-manager/resource-group-overview.md)을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="1325e-107">이 문서에서는 VM에 대해 Azure CLI 1.0으로 관리되지 않는 디스크를 사용하여 VM 이미지를 캡처하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="1325e-108">[Azure CLI 2.0으로 Azure Managed Disks를 사용하여 VM을 캡처](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1325e-109">관리되는 디스크는 Azure 플랫폼을 통해 처리되며 디스크를 저장할 위치나 준비가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="1325e-110">자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1325e-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="1325e-111">이미지를 사용하여 VM을 만들려면, 각각의 새 VM에 대해 네트워크 리소스를 설정하고, 템플릿(JSON(JavaScript Object Notation) 파일)을 사용하여 캡처한 VHD 이미지로부터 VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="1325e-112">이러한 방식으로 Azure Marketplace에서 이미지를 사용하는 것과 유사한 방식으로 현재 소프트웨어 구성으로 VM을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="1325e-113">백업 또는 디버깅용의 특수화된 상태로 기존 Linux VM의 복사본을 만들려면 [Azure에서 실행되는 Linux 가상 컴퓨터의 복사본 만들기](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1325e-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1325e-114">온-프레미스 VM으로부터 Linux VHD를 업로드하려면 [사용자 지정 디스크 이미지에서 Linux VM 업로드 및 만들기](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1325e-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1325e-115">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="1325e-115">CLI versions to complete the task</span></span>
<span data-ttu-id="1325e-116">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="1325e-117">[Azure CLI 1.0](#before-you-begin) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="1325e-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1325e-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="1325e-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1325e-119">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1325e-119">Before you begin</span></span>
<span data-ttu-id="1325e-120">다음 필수 조건을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="1325e-121">**Azure VM이 Resource Manager 배포 모델에 생성됨** - Linux VM을 만들지 않은 경우, [포털](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [Resource Manager 템플릿](create-ssh-secured-vm-from-template.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="1325e-122">필요에 따라 VM을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-122">Configure the VM as needed.</span></span> <span data-ttu-id="1325e-123">예를 들어 [데이터 디스크를 추가하고](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), 업데이트를 적용하고, 응용 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="1325e-124">**Azure CLI** - 로컬 컴퓨터에 [Azure CLI](../../cli-install-nodejs.md)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="1325e-125">1단계: Azure Linux 에이전트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="1325e-126">우선 Linux VM에서 **deprovision** 매개 변수와 함께 **waagent** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="1325e-127">이 명령은 VM이 가상화 준비가 되도록 파일과 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="1325e-128">자세한 내용은 [Azure Linux 에이전트 사용자 가이드](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1325e-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="1325e-129">SSH 클라이언트를 사용하여 Linux VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="1325e-130">SSH 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="1325e-131">이미지로 캡처하려는 VM에서만 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="1325e-132">이 과정이 이미지에서 중요한 정보가 모두 지워졌다거나 재배포에 적합하다는 것을 보장하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="1325e-133">계속하려면 **y** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-133">Type **y** to continue.</span></span> <span data-ttu-id="1325e-134">이 확인 단계를 피하려면 **-force** 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="1325e-135">명령이 완료된 후 **exit**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="1325e-136">이 단계는 SSH 클라이언트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="1325e-137">2단계: VM 캡처</span><span class="sxs-lookup"><span data-stu-id="1325e-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="1325e-138">Azure CLI를 사용하여 VM을 일반화하고 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="1325e-139">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1325e-140">예제 매개 변수 이름에는 **myResourceGroup**, **myVnet**, **myVM**이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="1325e-141">로컬 컴퓨터에서 Azure CLI를 열고 [Azure 구독에 로그인](../../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="1325e-142">Resource Manager 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="1325e-143">다음 명령을 사용하여 프로비전을 해제한 VM을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="1325e-144">다음 명령을 사용하여 VM을 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="1325e-145">이제 VM을 캡처하는 **azure vm capture** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="1325e-146">다음 예의 경우 이름이 **MyVHDNamePrefix**로 시작되는 이미지 VHD가 캡처되며 **-t** 옵션은 **MyTemplate.json** 템플릿에 대한 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="1325e-147">이미지 VHD 파일이 원본 VM이 사용된 동일한 저장소 계정에서 기본적으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="1325e-148">이미지를 통해 만든 새 VM에 대한 VHD를 저장하려면 *동일한 저장소 계정*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="1325e-149">캡처한 이미지의 위치를 찾으려면 텍스트 편집기에서 JSON 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="1325e-150">**storageProfile**에서 **시스템** 컨테이너에 있는 **이미지**의 **uri**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="1325e-151">예를 들어, OS 디스크 이미지의 URI는 `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="1325e-152">3단계: 캡처한 이미지로부터 새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1325e-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="1325e-153">템플릿과 이미지를 사용하여 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="1325e-154">이 단계는 Azure CLI 및 캡처한 JSON 파일 템플릿을 사용하여 새 가상 네트워크에 VM을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="1325e-155">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="1325e-155">Create network resources</span></span>
<span data-ttu-id="1325e-156">템플릿을 사용하려면 우선 새 VM에 대한 NIC와 가상 네트워크를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="1325e-157">VM 이미지가 저장된 위치에 있는 이러한 리소스에 대해 리소스 그룹을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="1325e-158">다음과 유사한 명령을, 리소스 이름과 Azure 위치(이 명령의 경우 “centralus”)를 적절하게 대체한 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="1325e-159">NIC의 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="1325e-159">Get the Id of the NIC</span></span>
<span data-ttu-id="1325e-160">캡처를 하는 동안 저장한 JSON을 사용하여 이미지의 VM을 배포하려면 NIC의 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="1325e-161">다음 명령을 실행하여 ID를 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="1325e-162">출력되는 **Id**는 `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="1325e-163">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1325e-163">Create a VM</span></span>
<span data-ttu-id="1325e-164">이제 다음 명령을 실행하여 캡처한 VM 이미지로부터 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="1325e-165">**-f** 매개 변수를 사용하여 저장해 놓은 템플릿 JSON 파일에 대한 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="1325e-166">명령 출력에 새 VM 이름, 관리자 사용자 이름 및 암호, 이전에 만든 NIC의 ID를 제공하라는 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="1325e-167">다음 샘플은 배포 완료 시 표시되는 내용을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-the-deployment"></a><span data-ttu-id="1325e-168">배포 확인</span><span class="sxs-lookup"><span data-stu-id="1325e-168">Verify the deployment</span></span>
<span data-ttu-id="1325e-169">생성한 가상 컴퓨터에 SSH를 실행하여 배포를 확인하고 새 VM 사용을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="1325e-170">SSH를 통해 연결하려면 다음 명령을 실행하여 생성한 VM의 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="1325e-171">명령 출력에 공용 IP 주소가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="1325e-172">기본적으로 SSH 포트 22를 사용하여 Linux VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="1325e-173">추가 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1325e-173">Create additional VMs</span></span>
<span data-ttu-id="1325e-174">이전 섹션의 단계를 사용하여 캡처한 이미지와 템플릿을 사용하여 추가 VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="1325e-175">이미지를 통해 VM을 만드는 다른 옵션에는 빠른 시작 템플릿을 사용하거나 **azure vm create** 명령을 실행하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="1325e-176">캡처한 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="1325e-176">Use the captured template</span></span>
<span data-ttu-id="1325e-177">캡처한 이미지와 템플릿을 사용하려면 다음 단계를 수행합니다(앞의 섹션에 자세히 설명됨).</span><span class="sxs-lookup"><span data-stu-id="1325e-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="1325e-178">VM 이미지가 VM의 VHD를 호스팅하는 계정과 동일한 저장소 계정에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="1325e-179">템플릿 JSON 파일을 복사하고 새 VM VHD의 OS 디스크에 대해 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="1325e-180">예를 들어, **storageProfile**의 **vhd** 아래 **uri**에 **osDisk** VHD에 대한 고유한 이름을 `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`와 유사하게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="1325e-181">NIC를 동일한 가상 네트워크 또는 다른 가상 네트워크에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="1325e-182">수정된 템플릿 JSON 파일을 사용하여, 가상 네트워크를 설정한 리소스 그룹에 배포를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="1325e-183">빠른 시작 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="1325e-183">Use a quickstart template</span></span>
<span data-ttu-id="1325e-184">이미지로부터 VM을 만들 때 네트워크에서 자동으로 설정되도록 하려면 템플릿에 해당 리소스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="1325e-185">예를 들어 GitHub의 [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1325e-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="1325e-186">이 템플릿은 사용자 지정 이미지에서 VM을 만들고 필요한 가상 네트워크, 공용 IP 주소, NIC 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="1325e-187">Azure 포털에서 템플릿 사용에 대한 안내는 [Resource Manager 템플릿을 사용하여 사용자 지정 이미지에서 가상 컴퓨터 만드는 방법](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1325e-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="1325e-188">azure vm create 명령 사용</span><span class="sxs-lookup"><span data-stu-id="1325e-188">Use the azure vm create command</span></span>
<span data-ttu-id="1325e-189">Resource Manager 템플릿을 사용하여 이미지에서 VM을 만드는 것이 일반적으로 가장 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="1325e-190">하지만 **-Q**(**--image-urn**) 매개 변수와 함께 **azure vm create** 명령을 사용하면 *명령적으로* VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="1325e-191">이 방법을 사용하는 경우 새 VM에 대한 OS .vhd 파일 위치를 지정하는 **-d**(**--os-disk-vhd**) 매개 변수도 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="1325e-192">이 파일은 이미지 VHD 파일이 저장된 저장소 계정의 VHD 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="1325e-193">이 명령은 새 VM에 대한 VHD를 자동으로 **vhds** 컨테이너에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="1325e-194">이미지에 **azure vm create** 을 실행하기 전에 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="1325e-195">리소스 그룹을 만들거나 배포를 위한 기존 리소스 그룹을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="1325e-196">새 VM에 대한 NIC 리소스와 공용 IP 주소 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="1325e-197">CLI를 사용하여 가상 네트워크, 공용 IP 주소, NIC를 만드는 단계는 이 문서의 앞부분을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1325e-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="1325e-198">(**azure vm create** 역시 NIC를 만들 수 있지만 가상 네트워크 및 서브넷에 대해 추가적인 매개 변수를 전달해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1325e-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="1325e-199">그런 다음 새 OS VHD 파일 및 기존 이미지 양쪽 모두에 URI를 전달하는 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="1325e-200">이 예의 경우 크기가 Standard_A1인 VM이 미국 동부 지역에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="1325e-201">추가적인 명령 옵션은 `azure help vm create`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1325e-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1325e-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1325e-202">Next steps</span></span>
<span data-ttu-id="1325e-203">CLI를 사용하여 VM을 관리하려면 [Azure 리소스 관리자 템플릿 및 Azure CLI를 사용하여 가상 컴퓨터 배포 및 관리](create-ssh-secured-vm-from-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1325e-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

