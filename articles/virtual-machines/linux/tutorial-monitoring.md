---
title: "Azure에서 Linux 가상 컴퓨터 aaaMonitor | Microsoft Docs"
description: "Toomonitor Azure에서 Linux 가상 컴퓨터에서 진단 및 성능 메트릭을 확인을 부팅 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="95986-103">어떻게 toomonitor Azure에서 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="95986-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="95986-104">Azure에서 가상 컴퓨터 (Vm)는 올바르게 실행 되는 tooensure, 부트 진단 및 성능 메트릭을 확인을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="95986-105">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="95986-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95986-106">Hello VM에 대 한 부트 진단 유틸리티를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="95986-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="95986-107">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="95986-107">View boot diagnostics</span></span>
> * <span data-ttu-id="95986-108">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="95986-108">View host metrics</span></span>
> * <span data-ttu-id="95986-109">Hello VM에 진단 확장을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="95986-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="95986-110">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="95986-110">View VM metrics</span></span>
> * <span data-ttu-id="95986-111">진단 메트릭을 기반으로 하는 알림 만들기</span><span class="sxs-lookup"><span data-stu-id="95986-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="95986-112">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="95986-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="95986-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="95986-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="95986-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="95986-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="95986-116">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="95986-116">Create VM</span></span>

<span data-ttu-id="95986-117">toosee 진단 및 작업에 따라 메트릭을 VM 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="95986-118">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95986-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="95986-119">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupMonitor* hello에 *eastus* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="95986-120">이제 [az vm create](https://docs.microsoft.com/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95986-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="95986-121">hello 다음 예제에서는 V *myVM*:</span><span class="sxs-lookup"><span data-stu-id="95986-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="95986-122">부팅 진단을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="95986-122">Enable boot diagnostics</span></span>

<span data-ttu-id="95986-123">Linux Vm의 경우 부팅 하는 대로 hello 부트 진단 확장 부팅 출력을 캡처하여이 Azure 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="95986-124">이 데이터에 사용 되는 tootroubleshoot VM 부팅 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="95986-125">부트 진단이 hello Azure CLI를 사용 하 여 Linux VM을 만들 때 자동으로 활성화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="95986-126">부트 진단이를 활성화 하기 전에 저장소 계정에는 부팅 로그를 저장 하기 위해 만든 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="95986-127">저장소 계정은 전역적으로 고유한 이름을 가져야 하며, 3-24자 사이의 숫자와 소문자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="95986-128">Hello로 저장소 계정을 만드는 [az 저장소 계정에 create](/cli/azure/storage/account#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="95986-129">이 예제에서는 임의 문자열은 사용 되는 toocreate 고유한 저장소 계정 이름</span><span class="sxs-lookup"><span data-stu-id="95986-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="95986-130">부트 진단이를 설정할 경우 hello URI toohello blob 저장소 컨테이너 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="95986-131">hello 명령 쿼리인 hello 저장소 계정 tooreturn이이 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="95986-132">hello URI 값 변수 이름에 저장 됩니다 *bloburi*, hello 다음 단계에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95986-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="95986-133">이제 [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable)을 사용하여 부팅 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="95986-134">hello `--storage` hello 이전 단계에 값이 hello blob URI를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="95986-135">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="95986-135">View boot diagnostics</span></span>

<span data-ttu-id="95986-136">부트 진단이 설정 되 면 중지 하 고 hello VM을 시작할 때마다 hello 부팅 프로세스에 대 한 정보는 기록 tooa 로그 파일.</span><span class="sxs-lookup"><span data-stu-id="95986-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="95986-137">이 예에서는 먼저 할당을 취소 hello로 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate) 다음과 같이 명령:</span><span class="sxs-lookup"><span data-stu-id="95986-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="95986-138">이제 VM hello hello로 시작 [az vm 시작]( /cli/azure/vm#stop) 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="95986-139">Hello에 대 한 부트 진단 데이터를 가져올 수 있습니다 *myVM* hello로 [az vm 부팅 진단 get-부팅-로그](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="95986-140">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="95986-140">View host metrics</span></span>

<span data-ttu-id="95986-141">Linux VM에는 Azure에서 상호 작용하는 전용 호스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="95986-142">메트릭은 hello 호스트에 대 한 자동으로 수집 되며 다음과 같이 hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="95986-143">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroupMonitor**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="95986-144">toosee hello 호스트 VM을 수행 하는 방법을 클릭 **메트릭** hello VM 블레이드에서 다음 중 하나를 선택 hello *[호스트]* 에서 메트릭 **사용 가능한 메트릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![호스트 메트릭 보기](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="95986-146">진단 확장 설치</span><span class="sxs-lookup"><span data-stu-id="95986-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95986-147">이 문서에서는 버전 2.3의 hello Linux 진단 확장을 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="95986-148">버전 2.3은 2018년 6월 30일까지 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="95986-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="95986-149">Hello Linux 진단 확장의 버전 3.0을 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="95986-150">자세한 내용은 참조 [설명서 hello](./diagnostic-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="95986-151">hello 기본 호스트 메트릭을 사용할 수 있는 보다 세부적인 toosee 있고 VM 관련 메트릭, 있습니다 tooneed tooinstall hello Azure 진단 확장을 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="95986-152">hello Azure 진단 확장 추가 모니터링 및 진단 데이터 toobe hello VM에서에서 검색을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="95986-153">이러한 성능 메트릭을 보고 하 고 hello VM 수행 하는 방법을 기반으로 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="95986-154">hello 진단 확장 다음과 같이 hello Azure 포털을 통해 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95986-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="95986-155">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="95986-156">**진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="95986-157">hello 목록에 표시 하는 *진단 부팅* hello 이전 단원에서 이미 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="95986-158">Hello에 대 한 확인란을 클릭 *기본 메트릭*합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="95986-159">Hello에 *저장소 계정* 섹션에서 tooand 선택 hello 찾아보기 *mydiagdata [1234]* hello 이전 섹션에서 만든 계정.</span><span class="sxs-lookup"><span data-stu-id="95986-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="95986-160">Hello 클릭 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-160">Click hello **Save** button.</span></span>

    ![진단 메트릭 보기](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="95986-162">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="95986-162">View VM metrics</span></span>

<span data-ttu-id="95986-163">Hello hello VM 메트릭을 볼 수 있습니다 동일한 방식으로 hello 호스트 VM 메트릭을 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="95986-164">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="95986-165">toosee hello VM을 수행 하는 방법을 클릭 **메트릭** VM 블레이드 hello 되 고 아래 hello 진단 메트릭 중 하나를 선택 **사용 가능한 메트릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![VM 메트릭 보기](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="95986-167">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="95986-167">Create alerts</span></span>

<span data-ttu-id="95986-168">특정 성능 메트릭을 기반으로 하는 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="95986-169">경고에는 예를 들어 사용된 toonotify 평균 CPU 사용률이 특정 임계값 또는 사용 가능한 디스크 공간을 초과 하는 일정량 아래로 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="95986-170">경고나 hello Azure 포털에에서 표시 되는 전자 메일을 통해 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="95986-171">또한 Azure 자동화 runbook 또는 Azure 논리 앱에서 생성 되 고 응답 tooalerts 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="95986-172">hello 다음 예제에서는 평균 CPU 사용량에 대 한 경고</span><span class="sxs-lookup"><span data-stu-id="95986-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="95986-173">Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="95986-174">클릭 **규칙 경고** hello VM 블레이드에서 클릭 **추가 메트릭 경고** hello 경고 블레이드의 hello 위쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="95986-175">*myAlertRule*과 같이 경고에 대한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="95986-176">tootrigger CPU 백분율을 5 분 동안 1.0을 초과할 때 경고 모든 hello 선택한 다른 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="95986-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="95986-177">필요에 따라 확인란 hello에 대 한 *소유자, 참가자 및 독자를 전자 메일로 보내기* toosend 전자 메일 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="95986-178">hello 기본 동작은 toopresent hello 포털의 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="95986-179">Hello 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="95986-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="95986-180">고급 모니터링</span><span class="sxs-lookup"><span data-stu-id="95986-180">Advanced monitoring</span></span> 

<span data-ttu-id="95986-181">[Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)를 사용하여 VM에 대한 고급 모니터링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="95986-182">아직 사용해 보지 않았으면 Operations Management Suite의 [평가판](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="95986-183">액세스 toohello OMS 포털을 사용 하는 경우에 hello 설정 블레이드에서 hello 작업 영역 키 및 작업 영역 id를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="95986-184">Replace < 작업 영역 키 > 및 < 작업 영역 id > OMS에 대 한 hello 값으로 작업 영역 및 다음 צ ְ ײ **az vm 확장 집합** tooadd hello OMS 확장 toohello VM:</span><span class="sxs-lookup"><span data-stu-id="95986-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

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

<span data-ttu-id="95986-185">Hello OMS 포털의 로그 검색 블레이드에서 hello 나타납니다 *myVM* 같은 hello 다음 그림에에서 표시 되는 내용:</span><span class="sxs-lookup"><span data-stu-id="95986-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![OMS 블레이드](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="95986-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95986-187">Next steps</span></span>

<span data-ttu-id="95986-188">이 자습서에서는 Azure Security Center를 사용하여 VM을 구성하고 검토했습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="95986-189">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="95986-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95986-190">Hello VM에 대 한 부트 진단 유틸리티를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="95986-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="95986-191">부트 진단 보기</span><span class="sxs-lookup"><span data-stu-id="95986-191">View boot diagnostics</span></span>
> * <span data-ttu-id="95986-192">호스트 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="95986-192">View host metrics</span></span>
> * <span data-ttu-id="95986-193">Hello VM에 진단 확장을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="95986-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="95986-194">VM 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="95986-194">View VM metrics</span></span>
> * <span data-ttu-id="95986-195">진단 메트릭을 기반으로 하는 알림 만들기</span><span class="sxs-lookup"><span data-stu-id="95986-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="95986-196">고급 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="95986-196">Set up advanced monitoring</span></span>

<span data-ttu-id="95986-197">Azure 보안 센터에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95986-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95986-198">VM 보안 관리</span><span class="sxs-lookup"><span data-stu-id="95986-198">Manage VM security</span></span>](./tutorial-azure-security.md)