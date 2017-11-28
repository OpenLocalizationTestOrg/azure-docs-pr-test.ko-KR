---
title: "Azure에서 Linux용 가상 컴퓨터 확장 집합 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="67393-103">가상 컴퓨터 확장 집합 만들기 및 Linux에 항상 사용 가능한 앱 배포</span><span class="sxs-lookup"><span data-stu-id="67393-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="67393-104">가상 컴퓨터 확장 집합을 사용하면 동일한 자동 크기 조정 가상 컴퓨터 집합을 배포하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="67393-105">확장 집합의 VM 수를 수동으로 조정하거나 CPU 사용률, 메모리 요구량 또는 네트워크 트래픽을 기반으로 자동으로 크기를 조정하는 규칙을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="67393-106">이 자습서에서는 Azure에서 가상 컴퓨터 확장 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="67393-107">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67393-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="67393-108">cloud-init를 사용하여 크기를 조정하는 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="67393-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="67393-109">가상 컴퓨터 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="67393-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="67393-110">확장 집합의 인스턴스 수 증가 또는 감소</span><span class="sxs-lookup"><span data-stu-id="67393-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="67393-111">확장 집합 인스턴스에 대한 연결 정보 보기</span><span class="sxs-lookup"><span data-stu-id="67393-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="67393-112">확장 집합에 데이터 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="67393-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="67393-113">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="67393-114">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="67393-115">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67393-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="67393-116">확장 집합 개요</span><span class="sxs-lookup"><span data-stu-id="67393-116">Scale Set overview</span></span>
<span data-ttu-id="67393-117">가상 컴퓨터 확장 집합을 사용하면 동일한 자동 크기 조정 가상 컴퓨터 집합을 배포하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="67393-118">확장 집합은 이전의 [고가용성 VM 만들기](tutorial-availability-sets.md) 자습서에서 알아본 것과 동일한 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="67393-119">확장 집합의 VM은 가용성 집합에 만들어지고 논리 장애 도메인 및 업데이트 도메인에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="67393-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="67393-120">VM은 필요에 따라 확장 집합에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="67393-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="67393-121">사용자는 확장 집합에서 VM이 추가되거나 제거되는 방법 및 시기를 제어하는 자동 크기 조정 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="67393-122">이러한 규칙은 메트릭(예: CPU 부하, 메모리 사용량 또는 네트워크 트래픽)을 기반으로 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="67393-123">확장 집합은 Azure 플랫폼 이미지를 사용하는 경우 최대 1,000개의 VM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="67393-124">프로덕션 워크로드의 경우 [사용자 지정 VM 이미지 만들기](tutorial-custom-images.md) 작업이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="67393-125">사용자 지정 이미지를 사용하는 경우 확장 집합에 최대 100개의 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="67393-126">크기를 조정하는 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="67393-126">Create an app to scale</span></span>
<span data-ttu-id="67393-127">프로덕션 사용을 위해 설치되고 구성된 응용 프로그램을 포함하는 [사용자 지정 VM 이미지 만들기](tutorial-custom-images.md) 작업이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="67393-128">이 자습서에서는 처음 부팅 시 VM을 사용자 지정하여 확장 집합의 실제 동작을 신속하게 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="67393-129">이전 자습서에서 cloud-init를 사용하여 [처음 부팅 시 Linux 가상 컴퓨터를 사용자 지정하는 방법](tutorial-automate-vm-deployment.md)을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="67393-130">동일한 cloud-init 구성 파일을 사용하여 NGINX를 설치하고 간단한 'Hello World' Node.js 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="67393-131">현재 셸에서 *cloud-init.txt*라는 파일을 만들고 다음 구성을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="67393-132">예를 들어 로컬 컴퓨터에 없는 Cloud Shell에서 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67393-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="67393-133">`sensible-editor cloud-init.txt`를 입력하여 파일을 만들고 사용할 수 있는 편집기의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="67393-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="67393-134">전체 cloud-init 파일, 특히 첫 줄이 올바르게 복사되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="67393-135">확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="67393-135">Create a scale set</span></span>
<span data-ttu-id="67393-136">확장 집합을 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67393-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="67393-137">다음 예제에서는 *eastus* 위치에 *myResourceGroupScaleSet*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67393-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="67393-138">이제 [az vmss create](/cli/azure/vmss#create)를 사용하여 가상 컴퓨터 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67393-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="67393-139">다음 예제에서는 *myScaleSet*이라는 확장 집합을 만들고, cloud-init 파일을 사용하여 VM을 사용자 지정하고, SSH 키가 없는 경우 SSH 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="67393-140">확장 집합 리소스와 VM을 모두 만들고 구성하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="67393-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="67393-141">Azure CLI에서 프롬프트로 반환한 후 실행을 계속하는 백그라운드 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="67393-142">앱에 액세스하려면 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="67393-143">웹 트래픽 허용</span><span class="sxs-lookup"><span data-stu-id="67393-143">Allow web traffic</span></span>
<span data-ttu-id="67393-144">부하 분산 장치는 가상 컴퓨터 확장 집합의 일부로 자동으로 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="67393-145">부하 분산 장치는 부하 분산 장치 규칙을 사용하여 정의된 VM 집합 전역에 트래픽을 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="67393-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="67393-146">다음 자습서 [Azure에서 Virtual Machines의 부하를 분산하는 방법](tutorial-load-balancer.md)에서 부하 분산 장치 개념 및 구성에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="67393-147">트래픽이 Web App에 도달하도록 허용하려면 [az network lb rule create](/cli/azure/network/lb/rule#create)를 사용하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67393-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="67393-148">다음 예제는 *myLoadBalancerRuleWeb*이라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67393-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="67393-149">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="67393-149">Test your app</span></span>
<span data-ttu-id="67393-150">웹에서 Node.js 앱을 보려면 [az network public-ip show](/cli/azure/network/public-ip#show)를 사용하여 부하 분산 장치의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="67393-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="67393-151">다음 예제에서는 확장 집합의 일부로 만든 *myScaleSetLBPublicIP*의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="67393-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="67393-152">웹 브라우저에 공용 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="67393-153">앱이 표시되고 부하 분산 장치가 트래픽을 분산한 VM의 호스트 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67393-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Node.js 앱 실행](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="67393-155">확장 집합의 실제 동작을 확인하려면 웹 브라우저에서 새로 고침을 실행하여 부하 분산 장치가 앱이 실행되는 모든 VM으로 트래픽을 분산시키는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="67393-156">관리 작업</span><span class="sxs-lookup"><span data-stu-id="67393-156">Management tasks</span></span>
<span data-ttu-id="67393-157">확장 집합의 수명 주기 내내 하나 이상의 관리 작업을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="67393-158">또한 다양한 수명 주기 작업을 자동화하는 스크립트를 만들어야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="67393-159">Azure CLI 2.0은 이러한 작업을 수행할 수 있는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="67393-160">다음은 몇 가지 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="67393-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="67393-161">확장 집합의 VM 보기</span><span class="sxs-lookup"><span data-stu-id="67393-161">View VMs in a scale set</span></span>
<span data-ttu-id="67393-162">확장 집합에서 실행 중인 VM 목록을 보려면 다음과 같이 [az vmss list-instances](/cli/azure/vmss#list-instances)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="67393-163">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="67393-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="67393-164">VM 인스턴스 증가 또는 감소</span><span class="sxs-lookup"><span data-stu-id="67393-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="67393-165">현재 확장 집합의 인스턴스 수를 보려면 [az vmss show](/cli/azure/vmss#show)를 사용하여 *sku.capacity*를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="67393-166">그런 다음[az vmss scale](/cli/azure/vmss#scale)을 사용하여 확장 집합의 Virtual Machines 수를 수동으로 증가 또는 감소시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="67393-167">다음 예제는 확장 집합의 VM 수를 *5*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="67393-168">자동 크기 조정 규칙을 사용하면 네트워크 트래픽 또는 CPU 사용량과 같은 수요에 대응하여 확장 집합의 VM 수를 확대하거나 축소하는 방법을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="67393-169">현재 이 규칙은 Azure CLI 2.0에서 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="67393-170">자동 크기 조정을 구성하려면 [Azure Portal](https://portal.azure.com)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="67393-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="67393-171">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="67393-171">Get connection info</span></span>
<span data-ttu-id="67393-172">확장 집합의 VM에 대한 연결 정보를 가져오려면 [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="67393-173">이 명령은 SSH와 연결할 수 있도록 각 VM의 공용 IP 주소 및 포트를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="67393-174">확장 집합으로 데이터 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="67393-174">Use data disks with scale sets</span></span>
<span data-ttu-id="67393-175">확장 집합으로 데이터 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="67393-176">OS 디스크 대신 데이터 디스크에 앱을 빌드하는 모범 사례 및 성능 향상에 대해 설명하는 이전 자습서에서는 [Azure 디스크를 관리하는 방법](tutorial-manage-disks.md)을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="67393-177">데이터 디스크로 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="67393-177">Create scale set with data disks</span></span>
<span data-ttu-id="67393-178">확장 집합을 만들고 데이터 디스크를 연결하려면 [az vmss create](/cli/azure/vmss#create) 명령에 `--data-disk-sizes-gb` 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="67393-179">다음 예제에서는 각 인스턴스에 *50*Gb 데이터 디스크가 연결된 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67393-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

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

<span data-ttu-id="67393-180">확장 집합에서 인스턴스가 제거되면 연결된 데이터 디스크도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="67393-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="67393-181">데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="67393-181">Add data disks</span></span>
<span data-ttu-id="67393-182">확장 집합의 인스턴스에 데이터 디스크를 추가하려면 [az vmss disk attach](/cli/azure/vmss/disk#attach) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="67393-183">다음 예제는 각 인스턴스에 *50*Gb 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="67393-184">데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="67393-184">Detach data disks</span></span>
<span data-ttu-id="67393-185">확장 집합의 인스턴스에서 데이터 디스크를 제거하려면 [az vmss disk detach](/cli/azure/vmss/disk#detach) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="67393-186">다음 예제는 각 인스턴스의 LUN *2*에서 데이터 디스크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="67393-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67393-187">Next steps</span></span>
<span data-ttu-id="67393-188">이 자습서에서는 가상 컴퓨터 확장 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="67393-189">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="67393-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="67393-190">cloud-init를 사용하여 크기를 조정하는 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="67393-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="67393-191">가상 컴퓨터 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="67393-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="67393-192">확장 집합의 인스턴스 수 증가 또는 감소</span><span class="sxs-lookup"><span data-stu-id="67393-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="67393-193">확장 집합 인스턴스에 대한 연결 정보 보기</span><span class="sxs-lookup"><span data-stu-id="67393-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="67393-194">확장 집합에 데이터 디스크 사용</span><span class="sxs-lookup"><span data-stu-id="67393-194">Use data disks in a scale set</span></span>

<span data-ttu-id="67393-195">Virtual Machines의 부하 분산 개념에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="67393-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="67393-196">Virtual Machines 부하 분산</span><span class="sxs-lookup"><span data-stu-id="67393-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)