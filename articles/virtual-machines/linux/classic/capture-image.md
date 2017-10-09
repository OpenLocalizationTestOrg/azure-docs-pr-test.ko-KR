---
title: "Linux VM의 이미지 aaaCapture | Microsoft Docs"
description: "Toocapture Linux 기반 Azure 가상 컴퓨터 (VM)의 이미지 만드는 방법을 hello 클래식 배포 모델에 알아봅니다."
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
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="a1cf6-103">어떻게 toocapture 이미지 형식으로 클래식 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="a1cf6-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a1cf6-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a1cf6-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a1cf6-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a1cf6-107">너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a1cf6-108">이 문서에서는 어떻게 toocapture는 클래식 Azure 가상 컴퓨터 (VM) 다른 가상 컴퓨터 이미지 toocreate로 Linux를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="a1cf6-109">이 이미지에 hello OS 디스크는 및 연결 된 toohello VM 데이터 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="a1cf6-110">네트워킹 구성 tooconfigure 있으므로 포함 되지 않습니다는 만들 때 hello 다른 VM hello 이미지에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="a1cf6-111">Azure 저장소에서 이미지 hello **이미지**, 업로드 한 모든 이미지와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="a1cf6-112">이미지에 대한 자세한 내용은 [Azure의 가상 컴퓨터 이미지 정보][About Virtual Machine Images in Azure]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1cf6-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a1cf6-113">Before you begin</span></span>
<span data-ttu-id="a1cf6-114">이 단계에서는 Azure VM hello 클래식 배포 모델 및 데이터 디스크를 연결까지 포함 하는 구성 된 hello 운영 체제를 사용 하 여 이미 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="a1cf6-115">VM toocreate 해야 할 경우 읽기 [어떻게 tooCreate Linux 가상 컴퓨터를][How tooCreate a Linux Virtual Machine]합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="a1cf6-116">Hello 가상 컴퓨터 캡처</span><span class="sxs-lookup"><span data-stu-id="a1cf6-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="a1cf6-117">[Toohello VM 연결](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 원하는 SSH 클라이언트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="a1cf6-118">Hello SSH 창의 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="a1cf6-119">hello에서 출력 `waagent` hello이이 유틸리티의 버전에 따라 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="a1cf6-120">hello 이전 명령이 tooclean hello 시스템 고 다시 프로 비전에 맞게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="a1cf6-121">이 작업 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="a1cf6-122">(Provisioning.RegenerateSshHostKeyPair 'y' hello 구성 파일의 경우) SSH 호스트 키를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="a1cf6-123">/etc/resolv.conf의 Nameserver 구성을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="a1cf6-124">제거 hello  `root` /등/그림자 (Provisioning.DeleteRootPassword hello 구성 파일에서 'y'는) 하는 경우 사용자 암호</span><span class="sxs-lookup"><span data-stu-id="a1cf6-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="a1cf6-125">캐시된 DHCP 클라이언트 임대 제거</span><span class="sxs-lookup"><span data-stu-id="a1cf6-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="a1cf6-126">다시 설정 합니다. 호스트 이름 toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="a1cf6-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="a1cf6-127">Hello (/var/lib/waagent에서 가져온)는 마지막 프로 비전 된 사용자 계정을 삭제 **와 관련 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="a1cf6-128">데이터 너무 "일반화" hello 이미지 및 파일 삭제 프로 비전 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="a1cf6-129">만 VM에서 새 이미지 템플릿으로 toocapture를 만들려는 경우이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="a1cf6-130">Hello 이미지가 중요 한 정보를 모두 선택 취소 되어 또는 재배포 toothird 파티에 대 한 적합 한 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="a1cf6-131">형식 **y** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-131">Type **y** toocontinue.</span></span> <span data-ttu-id="a1cf6-132">Hello를 추가할 수 있습니다 `-force` 매개 변수 tooavoid이 확인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="a1cf6-133">형식 **종료** tooclose hello SSH 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a1cf6-134">hello 나머지 단계 있다고 가정 이미 [hello Azure CLI 설치](../../../cli-install-nodejs.md) 클라이언트 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="a1cf6-135">단계를 수행 하는 모든 hello hello에서 수행할 수 있습니다 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="a1cf6-136">클라이언트 컴퓨터에서 Azure CLI 및 로그인 tooyour Azure 구독을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="a1cf6-137">자세한 내용은 읽기 [hello Azure CLI에서에서 tooan Azure 구독 연결](../../../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="a1cf6-138">Hello Azure 포털에서에서 toohello 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="a1cf6-139">서비스 관리 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="a1cf6-140">Hello 이미 프로 비전 해제 하는 VM 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="a1cf6-141">hello 다음 예에서는 종료 hello 라는 VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="a1cf6-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="a1cf6-142">필요한 경우 모든 hello Vm이 구독에서 사용 하 여 만든 목록을 볼 수 있습니다.`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="a1cf6-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="a1cf6-143">Hello Azure 포털을 사용 하는 경우 hello VM을 선택 하 고 클릭 **중지** hello VM 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="a1cf6-144">Hello VM이 중지 되 면 hello 이미지를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="a1cf6-145">다음 예에서는 캡처 hello hello 라는 VM `myVM` 라는 일반화 된 이미지를 만들고 `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="a1cf6-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="a1cf6-146">hello `-t` 삭제 hello 원래 가상 컴퓨터 하위 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1cf6-147">Hello Azure 포털에서에서 선택 하 여 이미지를 캡처할 수 **이미지** hello 허브 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="a1cf6-148">다음 hello 이미지에 대 한 정보는 toosupply hello 필요: 이름, 리소스 그룹, 위치, 운영 체제 유형 및 저장소 blob 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="a1cf6-149">hello 새 이미지 될 수 있는 이미지의 hello 목록에서 사용할 수 있는 사용 된 tooconfigure 모든 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="a1cf6-150">Hello 명령을 사용 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="a1cf6-151">Hello에 [Azure 포털](http://portal.azure.com), hello에 hello 새 이미지가 나타납니다 **VM 이미지 (클래식)** toohello 속하는 **계산** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="a1cf6-152">에 액세스할 수 있습니다 **VM 이미지 (클래식)** 클릭 하 여 _더 많은 서비스_ hello Azure의 hello 맨 아래에 서비스 목록 및 hello를 검색 한 다음 **계산** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![이미지 캡처 성공](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="a1cf6-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1cf6-154">Next steps</span></span>
<span data-ttu-id="a1cf6-155">hello 이미지는 사용 되는 준비 toobe toocreate Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="a1cf6-156">Hello Azure CLI 명령을 사용 하 여 `azure vm create` 및 만든 공급 hello 이미지 이름.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="a1cf6-157">자세한 내용은 참조 [클래식 배포 모델에 사용 하 여 hello Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="a1cf6-158">또는 hello를 사용 하 여 [Azure 포털](http://portal.azure.com) toocreate hello를 사용 하 여 사용자 지정 VM **이미지** 메서드 및 hello를 선택 하는 사용자가 만든 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="a1cf6-159">자세한 내용은 참조 [방법을 사용자 지정 VM tooCreate][How tooCreate a Custom Virtual Machine]합니다.</span><span class="sxs-lookup"><span data-stu-id="a1cf6-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="a1cf6-160">**참고 항목:** [Azure Linux 에이전트 사용자 가이드](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a1cf6-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
