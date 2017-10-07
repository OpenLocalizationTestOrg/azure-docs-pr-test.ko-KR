---
title: "aaaCreate는 내부 부하 분산 장치-Azure CLI | Microsoft Docs"
description: "Toocreate는 내부 부하 분산 장치를 사용 하 여 리소스 관리자의 Azure CLI hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="a7658-103">내부 부하 분산 장치는 hello Azure CLI를 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="a7658-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7658-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="a7658-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="a7658-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7658-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="a7658-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a7658-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="a7658-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="a7658-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a7658-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a7658-109">사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](load-balancer-get-started-ilb-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="a7658-110">Hello Azure CLI를 사용 하 여 hello 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="a7658-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="a7658-111">단계를 수행 하는 hello 어떻게 toocreate 인터넷 연결 부하 분산 장치 CLI와 Azure 리소스 관리자를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="a7658-112">Azure 리소스 관리자와 각 리소스 만들어집니다 및 개별적으로 구성 된 한 다음 함께 toocreate 리소스.</span><span class="sxs-lookup"><span data-stu-id="a7658-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="a7658-113">Toocreate 필요 하 고이 정보를 개체 toodeploy 부하 분산 장치 뒤 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="a7658-114">**프런트 엔드 IP 구성**: 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="a7658-115">**백 엔드 주소 풀**: hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽을 허용 하는 네트워크 인터페이스 (Nic)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="a7658-116">**부하 분산 규칙**: hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트를 매핑하는 규칙이 포함</span><span class="sxs-lookup"><span data-stu-id="a7658-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="a7658-117">**인바운드 NAT 규칙**: hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트를 매핑하는 규칙이 포함</span><span class="sxs-lookup"><span data-stu-id="a7658-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="a7658-118">**프로브**: hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 되는 toocheck hello 가용성은 상태 프로브를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="a7658-119">자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7658-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="a7658-120">CLI toouse 리소스 관리자 설정</span><span class="sxs-lookup"><span data-stu-id="a7658-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="a7658-121">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="a7658-122">Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a7658-123">Hello 실행 **azure 구성 모드** tooswitch tooResource 관리자 모드를 다음과 같이 명령:</span><span class="sxs-lookup"><span data-stu-id="a7658-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="a7658-124">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="a7658-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="a7658-125">내부 부하 분산 장치를 단계별로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="a7658-126">TooAzure에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="a7658-127">메시지가 표시되면 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="a7658-128">Hello 명령 도구 tooAzure 리소스 관리자 모드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="a7658-129">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a7658-129">Create a resource group</span></span>

<span data-ttu-id="a7658-130">Azure Resource Manager의 모든 리소스는 리소스 그룹과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="a7658-131">리소스 그룹을 아직 만들지 않았으면 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="a7658-132">내부 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="a7658-133">내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="a7658-133">Create an internal load balancer</span></span>

    <span data-ttu-id="a7658-134">시나리오를 따르는 hello, nrprg 라는 리소스 그룹은 미국 동부 지역에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="a7658-135">동일한 리소스 그룹 hello 및 동일한 hello 같은 가상 네트워크 및 가상 네트워크 서브넷은 내부 부하 분산 장치에 대 한 모든 리소스에 있어야 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="a7658-136">Hello 내부 부하 분산 장치에 대 한 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="a7658-137">가상 네트워크의 hello 서브넷 범위에 사용 하는 hello IP 주소 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="a7658-138">Hello 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="a7658-139">프런트 엔드 IP 주소 및 백 엔드 주소 풀을 정의한 후에 부하 분산 장치 규칙, 인바운드 NAT 규칙을 만들고 상태 프로브를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="a7658-140">Hello 내부 부하 분산 장치에 대 한 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="a7658-141">Hello 이전 단계를 수행 하는 경우 hello 명령은 설정 수신 tooport 1433에 대 한 부하 분산 장치 규칙 hello 프런트 엔드 풀 및 보내는 네트워크 부하 분산 된 트래픽 toohello 백 엔드 주소 풀에도 포트 1433을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="a7658-142">인바운드 NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="a7658-143">인바운드 NAT 규칙은 tooa 특정 가상 컴퓨터 인스턴스를 이동 하는 부하 분산 장치에 사용 되는 toocreate 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="a7658-144">hello 이전 단계에는 원격 데스크톱에 대 한 NAT 규칙을 두 개 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="a7658-145">Hello 부하 분산 장치에 대 한 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="a7658-146">상태 검색에는 모든 가상 컴퓨터 인스턴스 toomake 네트워크 트래픽을 보낼 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="a7658-147">실패 한 프로브 검사를 사용 하 여 hello 가상 컴퓨터 인스턴스는 다시 온라인 상태로 전환 되 고 프로브 확인 정상 임을 확인 될 때까지 hello 부하 분산 장치에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="a7658-148">hello Microsoft Azure 플랫폼에는 다양 한 관리 시나리오에 대 한 정적, 공개적으로 라우팅 가능한 IPv4 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="a7658-149">hello IP 주소 168.63.129.16입니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="a7658-150">이 IP 주소를 방화벽으로 차단하면 안 됩니다. 예기치 않은 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="a7658-151">존중 tooAzure 내부 부하 분산 가상 컴퓨터 부하 분산 집합에 대해 프로브 hello 부하 분산 장치 toodetermine hello 성능 상태를 모니터링 하 여이 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="a7658-152">네트워크 보안 그룹 사용 되는 toorestrict 내부적으로 부하 분산 된 집합에 트래픽을 tooAzure 가상 컴퓨터는 되거나 적용 된 tooa 가상 네트워크 서브넷에 경우에 네트워크 보안 규칙 tooallow 트래픽을 168.63.129.16에서 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="a7658-153">NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="a7658-153">Create NICs</span></span>

<span data-ttu-id="a7658-154">Toocreate nic가 필요 (또는 기존 템플릿을 수정할)와 tooNAT 규칙, 부하 분산 장치 규칙 및 프로브에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="a7658-155">명명 된 NIC를 만들 *lb nic1 수*, hello와 연결할 및 *rdp1* NAT 규칙 및 hello *beilb* 백 엔드 주소 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="a7658-156">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="a7658-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="a7658-157">명명 된 NIC를 만들 *lb nic2 수*, hello와 연결할 및 *rdp2* NAT 규칙 및 hello *beilb* 백 엔드 주소 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="a7658-158">라는 가상 컴퓨터 만들기 *DB1*, hello 라는 NIC와 연결할 및 *lb nic1 수*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="a7658-159">저장소 계정 이라는 *web1nrp* hello 다음 명령을 실행 하기 전에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="a7658-160">Vm에서 부하 분산 장치 필요 toobe에 hello 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="a7658-161">사용 하 여 `azure availset create` toocreate 한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="a7658-162">라는 가상 컴퓨터 (VM) 만들기 *DB2*, hello 라는 NIC와 연결할 및 *lb nic2 수*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="a7658-163">저장소 계정 이라는 *web1nrp* hello 다음 명령을 실행 하기 전에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="a7658-164">부하 분산 장치 삭제</span><span class="sxs-lookup"><span data-stu-id="a7658-164">Delete a load balancer</span></span>

<span data-ttu-id="a7658-165">부하 분산 장치를 tooremove hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7658-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="a7658-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7658-166">Next steps</span></span>

[<span data-ttu-id="a7658-167">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="a7658-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a7658-168">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a7658-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

