---
title: "Linux VM의 이미지 캡처 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 만든, Linux 기반 Azure VM(가상 컴퓨터)의 이미지를 캡처하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: ecde5dd3211bfbb290e6910d7d55136d079c6cf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-capture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="98e7b-103">클래식 Linux 가상 컴퓨터를 이미지로 캡처하는 방법</span><span class="sxs-lookup"><span data-stu-id="98e7b-103">How to capture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="98e7b-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="98e7b-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="98e7b-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="98e7b-107">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="98e7b-108">이 문서에서는 Linux를 실행하는 클래식 Azure VM(Virtual Machine)을 캡처하여 다른 Virtual Machines를 만들 때 이미지로 사용하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span></span> <span data-ttu-id="98e7b-109">이 이미지에는 OS 디스크를 비롯해 VM에 연결된 데이터 디스크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-109">This image includes the OS disk and data disks attached to the VM.</span></span> <span data-ttu-id="98e7b-110">여기에 네트워킹 구성은 포함되지 않으므로 이미지에서 다른 VM을 만들 때 네트워킹을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span></span>

<span data-ttu-id="98e7b-111">Azure는 사용자가 업로드한 이미지와 함께 해당 이미지를 **Images**아래에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-111">Azure stores the image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="98e7b-112">이미지에 대한 자세한 내용은 [Azure의 가상 컴퓨터 이미지 정보][About Virtual Machine Images in Azure]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98e7b-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="98e7b-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="98e7b-113">Before you begin</span></span>
<span data-ttu-id="98e7b-114">이러한 단계는 이미 클래식 배포 모델을 사용하여 Azure VM을 만들었으며 데이터 디스크 연결을 비롯해 운영 체제 구성을 완료했다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="98e7b-115">VM을 만들어야 할 경우 [Linux 가상 컴퓨터를 만드는 방법][How to Create a Linux Virtual Machine]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98e7b-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="98e7b-116">가상 컴퓨터 캡처</span><span class="sxs-lookup"><span data-stu-id="98e7b-116">Capture the virtual machine</span></span>
1. <span data-ttu-id="98e7b-117">선택한 SSH 클라이언트를 사용하여 [VM에 연결](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="98e7b-118">SSH 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-118">In the SSH window, type the following command.</span></span> <span data-ttu-id="98e7b-119">`waagent` 의 출력은 이 유틸리티의 버전에 따라 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-119">The output from `waagent` may vary slightly depending on the version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="98e7b-120">이전 명령은 시스템을 정리하여 다시 프로비전하기에 적합하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="98e7b-121">이 작업은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-121">This operation performs the following tasks:</span></span>

   * <span data-ttu-id="98e7b-122">SSH 호스트 키를 제거합니다(구성 파일에서 Provisioning.RegenerateSshHostKeyPair가 'y'인 경우).</span><span class="sxs-lookup"><span data-stu-id="98e7b-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="98e7b-123">/etc/resolv.conf의 Nameserver 구성을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="98e7b-124">/etc/shadow에서 `root` 사용자 암호를 제거합니다(구성 파일에서 Provisioning.DeleteRootPassword가 'y'인 경우).</span><span class="sxs-lookup"><span data-stu-id="98e7b-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="98e7b-125">캐시된 DHCP 클라이언트 임대 제거</span><span class="sxs-lookup"><span data-stu-id="98e7b-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="98e7b-126">호스트 이름을 localhost.localdomain으로 다시 설정</span><span class="sxs-lookup"><span data-stu-id="98e7b-126">Resets host name to localhost.localdomain</span></span>
   * <span data-ttu-id="98e7b-127">마지막으로 프로비전된 사용자 계정 (/var/lib/waagent에서 얻은) **및 관련 데이터**를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="98e7b-128">프로비전을 해제하면 파일 및 데이터가 삭제되어 이미지가 "일반화"됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-128">Deprovisioning deletes files and data to "generalize" the image.</span></span> <span data-ttu-id="98e7b-129">새 이미지 템플릿 파일로 캡처할 VM에서만 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-129">Only run this command on a VM that you intend to capture as a new image template.</span></span> <span data-ttu-id="98e7b-130">하지만 이미지에서 중요한 정보가 모두 지워지고 이미지가 제3자에게 다시 배포하기에 적합하다고 보증할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span></span>

3. <span data-ttu-id="98e7b-131">계속하려면 **y** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-131">Type **y** to continue.</span></span> <span data-ttu-id="98e7b-132">`-force` 매개 변수를 추가하여 이 확인 단계를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-132">You can add the `-force` parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="98e7b-133">**Exit** 를 입력하여 SSH 클라이언트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-133">Type **Exit** to close the SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="98e7b-134">나머지 단계에서는 클라이언트 컴퓨터에 이미 [Azure CLI를 설치](../../../cli-install-nodejs.md) 했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="98e7b-135">다음 모든 단계는 [Azure Portal](http://portal.azure.com)에서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-135">All the following steps can also be done in the [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="98e7b-136">클라이언트 컴퓨터에서 Azure CLI를 열고 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-136">From your client computer, open Azure CLI and login to your Azure subscription.</span></span> <span data-ttu-id="98e7b-137">자세한 내용은 [Azure CLI에서 Azure 구독에 연결](../../../xplat-cli-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98e7b-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="98e7b-138">Azure Portal에서 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-138">In the Azure portal, log in to the portal.</span></span>

6. <span data-ttu-id="98e7b-139">서비스 관리 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="98e7b-140">이미 프로비전 해제된 VM을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-140">Shut down the VM that is already deprovisioned.</span></span> <span data-ttu-id="98e7b-141">다음 예에서는 `myVM`이라는 VM을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-141">The following example shuts down the VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="98e7b-142">필요한 경우 `azure vm list`를 사용하여 구독에서 만든 모든 VM 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-142">If needed, you can view a list all the VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="98e7b-143">Azure Portal을 사용하는 경우 VM을 선택하고 **중지**를 클릭하여 VM을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-143">If you're using the Azure portal, select the VM and click **Stop** to shut down the VM.</span></span>

8. <span data-ttu-id="98e7b-144">VM이 중지되면 이미지를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-144">When the VM is stopped, capture the image.</span></span> <span data-ttu-id="98e7b-145">다음 예에서는 `myVM`이라는 VM을 캡처하고 `myNewVM`이라는 범용 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-145">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="98e7b-146">`-t` 하위 명령은 원래 가상 컴퓨터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-146">The `-t` subcommand deletes the original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="98e7b-147">Azure Portal의 허브 메뉴에서 **이미지**를 선택하여 이미지를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-147">In the Azure portal, you can capture an image by selecting **Image** from the hub menu.</span></span> <span data-ttu-id="98e7b-148">이미지에 대한 다음 정보를 제공해야 합니다. 이름, 리소스 그룹, 위치, 운영 체제 유형 및 저장소 Blob 경로</span><span class="sxs-lookup"><span data-stu-id="98e7b-148">You need to supply the following information for the image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="98e7b-149">이제 새 VM을 구성하는 데 사용할 수 있는 이미지 목록에서 새 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-149">The new image is now available in the list of images that can be used to configure any new VM.</span></span> <span data-ttu-id="98e7b-150">다음 명령을 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-150">You can view it with the command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="98e7b-151">[Azure Portal](http://portal.azure.com)에서 새 이미지는 **계산** 서비스에 속하는 **VM 이미지(클래식)**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-151">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span></span> <span data-ttu-id="98e7b-152">Azure 서비스 목록의 맨 아래에서 _추가 서비스_를 클릭하고 **계산** 서비스를 살펴보아 **VM 이미지(클래식)**에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-152">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span></span>   

   ![이미지 캡처 성공](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="98e7b-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98e7b-154">Next steps</span></span>
<span data-ttu-id="98e7b-155">이제 이미지를 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-155">The image is ready to be used to create VMs.</span></span> <span data-ttu-id="98e7b-156">Azure CLI 명령 `azure vm create` 을 사용하고 만든 이미지 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-156">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span></span> <span data-ttu-id="98e7b-157">자세한 내용은 [클래식 배포 모델에서 Azure CLI 사용](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98e7b-157">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="98e7b-158">또는 [Azure Portal](http://portal.azure.com)에서 **이미지** 방법을 사용하고 만든 이미지를 선택하여 사용자 지정 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98e7b-158">Alternatively, use the [Azure portal](http://portal.azure.com) to create a custom VM by using the **Image** method and selecting the image you created.</span></span> <span data-ttu-id="98e7b-159">자세한 내용은 [사용자 지정 VM을 만드는 방법][How to Create a Custom Virtual Machine]을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="98e7b-159">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span></span>

<span data-ttu-id="98e7b-160">**참고 항목:** [Azure Linux 에이전트 사용자 가이드](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="98e7b-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How to Create a Custom Virtual Machine]:create-custom.md
[How to Attach a Data Disk to a Virtual Machine]:attach-disk.md
[How to Create a Linux Virtual Machine]:create-custom.md
