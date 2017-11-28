---
title: "Azure에서 Linux 가상 컴퓨터 모니터링 | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터에 대한 부팅 진단과 성능 메트릭을 모니터링하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 3fe8390e88e609b57a462e066f972346f8e8730e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="05725-103">Azure에서 Linux 가상 컴퓨터를 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="05725-103">How to monitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="05725-104">Azure에서 VM(가상 컴퓨터)이 올바르게 실행되도록 부팅 진단과 성능 메트릭을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-104">To ensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="05725-105">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="05725-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05725-106">VM에서 부팅 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="05725-106">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="05725-107">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="05725-107">View boot diagnostics</span></span>
> * <span data-ttu-id="05725-108">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="05725-108">View host metrics</span></span>
> * <span data-ttu-id="05725-109">VM에서 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="05725-109">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="05725-110">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="05725-110">View VM metrics</span></span>
> * <span data-ttu-id="05725-111">진단 메트릭을 기반으로 하는 알림 만들기</span><span class="sxs-lookup"><span data-stu-id="05725-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="05725-112">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="05725-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="05725-113">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="05725-114">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="05725-115">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05725-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="05725-116">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="05725-116">Create VM</span></span>

<span data-ttu-id="05725-117">작동 중인 진단과 메트릭을 확인하려면 VM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-117">To see diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="05725-118">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05725-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="05725-119">다음 예제에서는 *eastus* 위치에 *myResourceGroupMonitor*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05725-119">The following example creates a resource group named *myResourceGroupMonitor* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="05725-120">이제 [az vm create](https://docs.microsoft.com/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05725-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="05725-121">다음 예제에서는 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05725-121">The following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="05725-122">부팅 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="05725-122">Enable boot diagnostics</span></span>

<span data-ttu-id="05725-123">Linux VM이 부팅할 때 부팅 진단 확장에서는 부팅 출력을 캡처하여 Azure 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-123">As Linux VMs boot, the boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="05725-124">이 데이터는 VM 부팅 문제를 해결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-124">This data can be used to troubleshoot VM boot issues.</span></span> <span data-ttu-id="05725-125">Azure CLI를 사용하여 Linux VM을 만들 때 부팅 진단을 사용하도록 자동으로 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-125">Boot diagnostics are not automatically enabled when you create a Linux VM using the Azure CLI.</span></span>

<span data-ttu-id="05725-126">부팅 진단을 사용하도록 설정하기 전에 먼저 부팅 로그를 저장할 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-126">Before enabling boot diagnostics, a storage account needs to be created for storing boot logs.</span></span> <span data-ttu-id="05725-127">저장소 계정은 전역적으로 고유한 이름을 가져야 하며, 3-24자 사이의 숫자와 소문자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="05725-128">[az storage account create](/cli/azure/storage/account#create)를 사용하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05725-128">Create a storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="05725-129">이 예제에서는 임의의 문자열을 사용하여 고유한 저장소 계정 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05725-129">In this example, a random string is used to create a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="05725-130">부팅 진단을 사용하도록 설정하는 경우 Blob 저장소 컨테이너에 대한 URI가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-130">When enabling boot diagnostics, the URI to the blob storage container is needed.</span></span> <span data-ttu-id="05725-131">다음 명령은 저장소 계정을 쿼리하여 이 URI를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-131">The following command queries the storage account to return this URI.</span></span> <span data-ttu-id="05725-132">URI 값은 *bloburi* 변수 이름에 저장되며 다음 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05725-132">The URI value is stored in a variable names *bloburi*, which is used in the next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="05725-133">이제 [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable)을 사용하여 부팅 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="05725-134">`--storage` 값은 이전 단계에서 수집된 Blob URI입니다.</span><span class="sxs-lookup"><span data-stu-id="05725-134">The `--storage` value is the blob URI collected in the previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="05725-135">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="05725-135">View boot diagnostics</span></span>

<span data-ttu-id="05725-136">부팅 진단을 사용하도록 설정되면, VM을 중지하고 시작할 때마다 부팅 프로세스에 대한 정보가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="05725-136">When boot diagnostics are enabled, each time you stop and start the VM, information about the boot process is written to a log file.</span></span> <span data-ttu-id="05725-137">이 예제에서는 먼저 다음과 같이 [az vm deallocate](/cli/azure/vm#deallocate) 명령을 사용하여 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-137">For this example, first deallocate the VM with the [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="05725-138">이제 다음과 같이 [az vm start]( /cli/azure/vm#stop) 명령을 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-138">Now start the VM with the [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="05725-139">다음과 같이 [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) 명령을 사용하여 *myVM*에 대한 부팅 진단 데이터를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-139">You can get the boot diagnostic data for *myVM* with the [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="05725-140">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="05725-140">View host metrics</span></span>

<span data-ttu-id="05725-141">Linux VM에는 Azure에서 상호 작용하는 전용 호스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="05725-142">이 호스트에 대한 메트릭이 자동으로 수집되며, 다음과 같이 Azure Portal에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-142">Metrics are automatically collected for the host and can be viewed in the Azure portal as follows:</span></span>

1. <span data-ttu-id="05725-143">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroupMonitor**를 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-143">In the Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="05725-144">호스트 VM의 성능을 보려면 VM 블레이드에서 **메트릭**을 클릭한 다음 **사용 가능한 메트릭**에서 *[호스트]* 메트릭 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-144">To see how the host VM is performing, click **Metrics** on the VM blade, then select any of the *[Host]* metrics under **Available metrics**.</span></span>

    ![호스트 메트릭 보기](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="05725-146">진단 확장 설치</span><span class="sxs-lookup"><span data-stu-id="05725-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05725-147">이 문서에서는 사용되지 않는 Linux 진단 확장 2.3 버전에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-147">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="05725-148">버전 2.3은 2018년 6월 30일까지 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="05725-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="05725-149">대신 Linux 진단 확장 3.0 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-149">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="05725-150">자세한 내용은 [설명서](./diagnostic-extension.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05725-150">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="05725-151">기본 호스트 메트릭을 사용할 수 있지만, 더 세분화된 VM 관련 메트릭을 보려면 VM에 Azure 진단 확장을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-151">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="05725-152">Azure 진단 확장을 사용하면 VM에서 추가 모니터링 및 진단 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-152">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="05725-153">이러한 성능 메트릭을 보고 VM 성능에 따라 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-153">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="05725-154">진단 확장은 다음과 같이 Azure Portal을 통해 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="05725-154">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="05725-155">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroup**을 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-155">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="05725-156">**진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="05725-157">목록에서는 *부트 진단*이 이전 섹션에서 이미 사용하도록 설정되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05725-157">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="05725-158">*기본 메트릭*에 대한 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-158">Click the check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="05725-159">*저장소 계정* 섹션에서 이전 섹션에서 만든 *mydiagdata[1234]* 계정을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-159">In the *Storage account* section, browse to and select the *mydiagdata[1234]* account created in the previous section.</span></span>
1. <span data-ttu-id="05725-160">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-160">Click the **Save** button.</span></span>

    ![진단 메트릭 보기](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="05725-162">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="05725-162">View VM metrics</span></span>

<span data-ttu-id="05725-163">호스트 VM 메트릭을 본 것과 동일한 방법으로 VM 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-163">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="05725-164">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroup**을 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-164">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="05725-165">VM의 성능을 보려면 VM 블레이드에서 **메트릭**을 클릭한 다음 **사용 가능한 메트릭**에서 진단 메트릭 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-165">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![VM 메트릭 보기](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="05725-167">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="05725-167">Create alerts</span></span>

<span data-ttu-id="05725-168">특정 성능 메트릭을 기반으로 하는 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="05725-169">예를 들어 평균 CPU 사용량이 특정 임계값을 초과하거나 사용 가능한 디스크 공간이 일정량 이하로 떨어지면 경고를 사용하여 사용자에게 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-169">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="05725-170">경고는 Azure Portal에 표시되거나 전자 메일을 통해 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-170">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="05725-171">또한 생성되는 경고에 대한 응답으로 Azure Automation Runbook 또는 Azure Logic Apps를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="05725-172">다음 예제에서는 평균 CPU 사용량에 대한 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05725-172">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="05725-173">Azure Portal에서 **리소스 그룹**을 클릭하고 **myResourceGroup**을 선택한 다음 리소스 목록에서 **myVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-173">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="05725-174">VM 블레이드에서 **경고 규칙**을 클릭한 다음, 경고 블레이드 위쪽에 있는 **메트릭 경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-174">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="05725-175">*myAlertRule*과 같이 경고에 대한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="05725-176">CPU 사용률이 5분 동안 1.0을 초과할 때 경고를 트리거하려면 다른 모든 기본값을 선택한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="05725-176">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="05725-177">필요한 경우 전자 메일 알림을 보내도록 *전자 메일 소유자, 참가자 및 읽기 권한자*의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-177">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="05725-178">기본 작업은 포털에서 알림을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="05725-178">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="05725-179">**확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-179">Click the **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="05725-180">고급 모니터링</span><span class="sxs-lookup"><span data-stu-id="05725-180">Advanced monitoring</span></span> 

<span data-ttu-id="05725-181">[Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)를 사용하여 VM에 대한 고급 모니터링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="05725-182">아직 사용해 보지 않았으면 Operations Management Suite의 [평가판](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="05725-183">OMS 포털에 액세스할 수 있으면 [설정] 블레이드에서 작업 영역 키와 작업 영역 식별자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-183">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="05725-184"><workspace-key> 및 <workspace-id>를 OMS 작업 영역의 값으로 바꾼 다음, **az vm extension set**을 사용하여 VM에 OMS 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-184">Replace <workspace-key> and <workspace-id> with the values for from your OMS workspace and then you can use **az vm extension set** to add the OMS extension to the VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="05725-185">OMS 포털의 [로그 검색] 블레이드에서 다음 그림과 같이 *myVM*이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05725-185">On the Log Search blade of the OMS portal, you should see *myVM* such as what is shown in the following picture:</span></span>

![OMS 블레이드](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="05725-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05725-187">Next steps</span></span>

<span data-ttu-id="05725-188">이 자습서에서는 Azure Security Center를 사용하여 VM을 구성하고 검토했습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="05725-189">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="05725-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05725-190">VM에서 부팅 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="05725-190">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="05725-191">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="05725-191">View boot diagnostics</span></span>
> * <span data-ttu-id="05725-192">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="05725-192">View host metrics</span></span>
> * <span data-ttu-id="05725-193">VM에서 진단 확장을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="05725-193">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="05725-194">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="05725-194">View VM metrics</span></span>
> * <span data-ttu-id="05725-195">진단 메트릭을 기반으로 하는 알림 만들기</span><span class="sxs-lookup"><span data-stu-id="05725-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="05725-196">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="05725-196">Set up advanced monitoring</span></span>

<span data-ttu-id="05725-197">Azure Security Center에 대해 알아보려면 다음 자습서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="05725-197">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="05725-198">VM 보안 관리</span><span class="sxs-lookup"><span data-stu-id="05725-198">Manage VM security</span></span>](./tutorial-azure-security.md)