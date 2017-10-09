---
title: "Azure에서 linux 가상 컴퓨터 크기 집합 aaaCreate | Microsoft Docs"
description: "가상 컴퓨터 확장 집합을 사용하여 Linux VM에 항상 사용 가능한 응용 프로그램을 만들고 배포합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="a9aa1-103">가상 컴퓨터 확장 집합 만들기 및 Linux에 항상 사용 가능한 앱 배포</span><span class="sxs-lookup"><span data-stu-id="a9aa1-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="a9aa1-104">가상 컴퓨터 크기 집합 toodeploy 있으며, 자동 크기 조정 동일한 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="a9aa1-105">수동으로 hello hello 크기 집합의 Vm 수의 크기를 조정 하거나 기반으로 CPU 사용량, 메모리 수요가 또는 네트워크 트래픽 규칙 tooautoscale 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="a9aa1-106">이 자습서에서는 Azure에서 가상 컴퓨터 확장 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="a9aa1-107">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9aa1-108">클라우드 init toocreate 앱 tooscale 사용</span><span class="sxs-lookup"><span data-stu-id="a9aa1-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="a9aa1-109">가상 컴퓨터 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="a9aa1-110">Hello 크기 집합의 인스턴스 수를 늘리거나</span><span class="sxs-lookup"><span data-stu-id="a9aa1-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="a9aa1-111">확장 집합 인스턴스에 대한 연결 정보 보기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="a9aa1-112">확장 집합에 데이터 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="a9aa1-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9aa1-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a9aa1-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a9aa1-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="a9aa1-116">확장 집합 개요</span><span class="sxs-lookup"><span data-stu-id="a9aa1-116">Scale Set overview</span></span>
<span data-ttu-id="a9aa1-117">가상 컴퓨터 크기 집합 toodeploy 있으며, 자동 크기 조정 동일한 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="a9aa1-118">크기 조정 설정 사용 하 여 hello 동일한 구성 요소 hello 이전 자습서에서 너무 배운[항상 사용 가능한 Vm을 만들](tutorial-availability-sets.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="a9aa1-119">확장 집합의 VM은 가용성 집합에 만들어지고 논리 장애 도메인 및 업데이트 도메인에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="a9aa1-120">VM은 필요에 따라 확장 집합에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="a9aa1-121">자동 크기 조정 규칙 toocontrol 정의 방법 및 시기 Vm 더하거나 hello 크기 집합에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="a9aa1-122">이러한 규칙은 메트릭(예: CPU 부하, 메모리 사용량 또는 네트워크 트래픽)을 기반으로 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="a9aa1-123">크기 조정 설정 too1, 000 Vm Azure 플랫폼 이미지 사용을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="a9aa1-124">프로덕션 작업에 대해 지정할 수 있습니다 너무[사용자 지정 VM 이미지를 만들](tutorial-custom-images.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="a9aa1-125">Too100 vm 크기 집합 사용자 지정 이미지를 사용 하는 경우에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="a9aa1-126">응용 프로그램 tooscale 만들기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-126">Create an app tooscale</span></span>
<span data-ttu-id="a9aa1-127">프로덕션 용도로 수도 있습니다 너무[사용자 지정 VM 이미지를 만들](tutorial-custom-images.md) 응용 프로그램 설치 및 구성 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="a9aa1-128">이 자습서에 대 한 첫 번째 부팅 tooquickly에 있는 Vm 크기 집합 작업에서 참조 하는 hello를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="a9aa1-129">이전 자습서에서 배운 [어떻게 toocustomize Linux 가상 컴퓨터를 처음 부팅할](tutorial-automate-vm-deployment.md) 클라우드 init로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="a9aa1-130">에서는 동일한 클라우드 init 구성 파일 tooinstall NGINX hello 및 간단한 ' Hello World' Node.js 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="a9aa1-131">현재 셸에서 라는 파일을 만들어 *클라우드 init.txt* 붙여넣기 hello 구성에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="a9aa1-132">예를 들어 로컬 컴퓨터에 없는 클라우드 셸 hello에 hello 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="a9aa1-133">입력 `sensible-editor cloud-init.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="a9aa1-134">해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="a9aa1-135">확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-135">Create a scale set</span></span>
<span data-ttu-id="a9aa1-136">확장 집합을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a9aa1-137">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupScaleSet* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="a9aa1-138">이제 [az vmss create](/cli/azure/vmss#create)를 사용하여 가상 컴퓨터 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="a9aa1-139">hello 다음 예제에서는 크기 명명 된 집합 *myScaleSet*hello 클라우드 init 파일 toocustomize hello VM을 사용 하 고 존재 하지 않는 경우 SSH 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="a9aa1-140">몇 분 toocreate 걸리고 모든 hello 눈금 집합 리소스와 Vm을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="a9aa1-141">Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="a9aa1-142">다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="a9aa1-143">웹 트래픽 허용</span><span class="sxs-lookup"><span data-stu-id="a9aa1-143">Allow web traffic</span></span>
<span data-ttu-id="a9aa1-144">부하 분산 장치는 hello 가상 컴퓨터 크기 집합의 일부로 자동으로 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="a9aa1-145">hello 부하 분산 장치 부하 분산 장치 규칙을 사용 하 여 정의 된 Vm의 조합에 대해 트래픽을 분산 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="a9aa1-146">부하 분산 장치 개념과 hello 다음 자습서에서는 구성에 대 한 자세히 알아볼 수 있습니다 [tooload Azure의 가상 컴퓨터를 분산 하는 방법을](tutorial-load-balancer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="a9aa1-147">tooallow 트래픽 tooreach hello 웹 앱을 사용 하는 규칙을 만들 [az 네트워크 lb 규칙 만들기](/cli/azure/network/lb/rule#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="a9aa1-148">hello 다음 규칙을 만드는 예제는 명명 된 *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="a9aa1-149">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="a9aa1-149">Test your app</span></span>
<span data-ttu-id="a9aa1-150">toosee hello 웹에서 Node.js 응용 프로그램으로 부하 분산 장치의 hello 공용 IP 주소를 가져올 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip#show)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="a9aa1-151">hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myScaleSetLBPublicIP* hello 크기 집합의 일부로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="a9aa1-152">Tooa 웹 브라우저에서 hello 공용 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="a9aa1-153">hello 앱 hello 해당 VM을 분산 장치 배포 트래픽의 부하를 hello의 hello 호스트 이름을 포함 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Node.js 앱 실행](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="a9aa1-155">작업에서 설정 toosee hello 눈금 있습니다 수 강제 새로 고침 웹 브라우저 toosee hello 부하 분산 장치 앱을 실행 하는 모든 hello Vm 트래픽을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="a9aa1-156">관리 작업</span><span class="sxs-lookup"><span data-stu-id="a9aa1-156">Management tasks</span></span>
<span data-ttu-id="a9aa1-157">Hello 크기 집합의 hello 수명 주기 동안 toorun 할 수 있습니다 하나 이상의 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="a9aa1-158">또한 다양 한 수명 주기 작업을 자동화 하는 toocreate 스크립트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="a9aa1-159">hello Azure CLI 2.0 신속 하 게 toodo 이러한 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="a9aa1-160">다음은 몇 가지 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="a9aa1-161">확장 집합의 VM 보기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-161">View VMs in a scale set</span></span>
<span data-ttu-id="a9aa1-162">tooview 눈금에서 실행 중인 Vm의 목록 설정, 사용 하 여 [az vmss 목록 인스턴스](/cli/azure/vmss#list-instances) 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="a9aa1-163">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="a9aa1-164">VM 인스턴스 증가 또는 감소</span><span class="sxs-lookup"><span data-stu-id="a9aa1-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="a9aa1-165">인스턴스의 toosee hello 수 현재는 규모에 맞게 설정, 사용 하 여 [az vmss 표시](/cli/azure/vmss#show) 에서 쿼리 및 *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="a9aa1-166">있습니다 다음 수동으로 거 나 낮출 수로 설정 하는 hello 규모에 맞게 가상 컴퓨터의 hello 수 [az vmss 확장](/cli/azure/vmss#scale)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="a9aa1-167">hello 다음 예제에서는 설정 hello Vm 수 너무 설정 하 여 규모에 맞게*5*:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="a9aa1-168">자동 크기 조정 규칙 tooscale hello 눈금에서 Vm 수의 위아래로 예: 네트워크 트래픽 또는 CPU 사용량 응답 toodemand에서 설정 하는 방법을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="a9aa1-169">현재 이 규칙은 Azure CLI 2.0에서 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="a9aa1-170">사용 하 여 hello [Azure 포털](https://portal.azure.com) tooconfigure 자동 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="a9aa1-171">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-171">Get connection info</span></span>
<span data-ttu-id="a9aa1-172">tooobtain 연결 정보에 대 한 Vm 크기 집합의 hello, 사용 하 여 [az vmss 목록-인스턴스-연결-정보](/cli/azure/vmss#list-instance-connection-info)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="a9aa1-173">이 명령은 tooconnect SSH 사용 하면 각 VM에 대 한 hello 공용 IP 주소와 포트를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="a9aa1-174">확장 집합으로 데이터 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="a9aa1-174">Use data disks with scale sets</span></span>
<span data-ttu-id="a9aa1-175">확장 집합으로 데이터 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="a9aa1-176">이전 자습서에서 배운 너무 어떻게[관리 Azure 디스크](tutorial-manage-disks.md) 윤곽선 hello 모범 사례 및 hello 운영 체제 디스크 대신 데이터 디스크에 앱을 빌드하기 위한 성능 향상을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="a9aa1-177">데이터 디스크로 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-177">Create scale set with data disks</span></span>
<span data-ttu-id="a9aa1-178">소수 자릿수를 설정 하 고 데이터 디스크 연결 toocreate hello 추가 `--data-disk-sizes-gb` 매개 변수 toohello [az vmss 만들기](/cli/azure/vmss#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="a9aa1-179">hello 다음 예제에서는 사용 하 여 설정 하는 눈금 *50*Gb 데이터 디스크가 연결 tooeach 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="a9aa1-180">확장 집합에서 인스턴스가 제거되면 연결된 데이터 디스크도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="a9aa1-181">데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="a9aa1-181">Add data disks</span></span>
<span data-ttu-id="a9aa1-182">사용 하 여 tooadd 눈금에 데이터 디스크 tooinstances 설정 [az vmss 디스크 연결](/cli/azure/vmss/disk#attach)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="a9aa1-183">hello 다음 예제에서는 추가 *50*Gb 디스크 tooeach 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="a9aa1-184">데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="a9aa1-184">Detach data disks</span></span>
<span data-ttu-id="a9aa1-185">사용 하 여 tooremove 눈금에 데이터 디스크 tooinstances 설정 [az vmss 디스크 분리](/cli/azure/vmss/disk#detach)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="a9aa1-186">hello 다음 예제에서는 제거 hello 데이터 디스크 LUN에 *2* 각 인스턴스에서:</span><span class="sxs-lookup"><span data-stu-id="a9aa1-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="a9aa1-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9aa1-187">Next steps</span></span>
<span data-ttu-id="a9aa1-188">이 자습서에서는 가상 컴퓨터 확장 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="a9aa1-189">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9aa1-190">클라우드 init toocreate 앱 tooscale 사용</span><span class="sxs-lookup"><span data-stu-id="a9aa1-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="a9aa1-191">가상 컴퓨터 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="a9aa1-192">Hello 크기 집합의 인스턴스 수를 늘리거나</span><span class="sxs-lookup"><span data-stu-id="a9aa1-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="a9aa1-193">확장 집합 인스턴스에 대한 연결 정보 보기</span><span class="sxs-lookup"><span data-stu-id="a9aa1-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="a9aa1-194">확장 집합에 데이터 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="a9aa1-194">Use data disks in a scale set</span></span>

<span data-ttu-id="a9aa1-195">부하 분산 가상 컴퓨터에 대 한 개념에 대 한 자세한 toohello 다음 자습서 toolearn를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9aa1-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9aa1-196">Virtual Machines 부하 분산</span><span class="sxs-lookup"><span data-stu-id="a9aa1-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)