---
title: "Azure 네트워크 감시자 IP 흐름 확인-Azure CLI aaaVerify 트래픽 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocheck 가상 컴퓨터에서 트래픽 tooor 허용 또는 Azure CLI를 사용 하 여 거부 된 경우"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="82335-103">트래픽은 허용 되거나 Azure 네트워크 감시자의 구성 요소는 VM과 IP 확인 흐름에서 tooor을 거부 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="82335-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="82335-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="82335-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82335-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="82335-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="82335-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="82335-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="82335-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="82335-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="82335-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="82335-109">IP 흐름은 tooor 가상 컴퓨터에서 트래픽을 허용 하는 경우 tooverify 수 있는 네트워크 감시자의 기능 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="82335-110">이 시나리오는 유용한 tooget tooan 외부 리소스 또는 백 엔드 가상 컴퓨터를 서로 연결할 수 있는지 여부의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="82335-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="82335-111">IP 흐름 보안 그룹 NSG (네트워크) 규칙에 올바르게 구성 되어 NSG 규칙에 의해 차단 되는 흐름 문제를 해결 하는 경우 사용 되는 tooverify 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="82335-112">IP를 사용 하는 또 다른 이유 흐름 tooensure 트래픽이 차단 되도록 제대로 hello NSG 차단 하 고이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="82335-113">이 문서에서는 Windows, Mac 및 Linux에 대 한 사용 하지 않는 hello 리소스 관리 배포 모델, Azure CLI 2.0에 대 한 우리의 차세대 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="82335-114">이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="82335-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="82335-115">Before you begin</span></span>

<span data-ttu-id="82335-116">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 네트워크 감시자의 기존 인스턴스가 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="82335-117">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-117">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="82335-118">시나리오</span><span class="sxs-lookup"><span data-stu-id="82335-118">Scenario</span></span>

<span data-ttu-id="82335-119">이 시나리오는 가상 컴퓨터 수와 통신 tooa 알려진 경우 IP 확인 흐름 tooverify 사용 하 여 Bing IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="82335-119">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="82335-120">Hello 트래픽이 거부 되 면 해당 트래픽을 거부 하는 hello 보안 규칙을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="82335-121">IP 확인 흐름에 대 한 자세한 toolearn 방문 [IP 흐름 확인 개요](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="82335-121">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="82335-122">VM 확인</span><span class="sxs-lookup"><span data-stu-id="82335-122">Get a VM</span></span>

<span data-ttu-id="82335-123">IP 흐름에서의 원격 대상에서 가상 컴퓨터 tooor IP 주소를 트래픽 tooor 테스트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-123">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="82335-124">가상 컴퓨터의 Id가 hello cmdlet에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-124">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="82335-125">가상 컴퓨터 toouse hello의 hello ID를 알고 있는 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82335-125">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a><span data-ttu-id="82335-126">Hello NIC 가져오기</span><span class="sxs-lookup"><span data-stu-id="82335-126">Get hello NICS</span></span>

<span data-ttu-id="82335-127">hello 가상 컴퓨터에서 NIC의 IP 주소가 hello hello Nic는 가상 컴퓨터에서 검색 하는이 예에서 필요할 때.</span><span class="sxs-lookup"><span data-stu-id="82335-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="82335-128">원하는 tootest hello IP 주소를 알고 있으면 hello 가상 컴퓨터에서이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82335-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="82335-129">IP 흐름 확인 실행</span><span class="sxs-lookup"><span data-stu-id="82335-129">Run IP flow verify</span></span>

<span data-ttu-id="82335-130">Hello 았 hello 정보 toorun hello 필요한 cmdlet을 실행할 `az network watcher test-ip-flow` cmdlet tootest hello 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="82335-130">Now that we have hello information needed toorun hello cmdlet, we run hello `az network watcher test-ip-flow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="82335-131">이 예제에서 사용 하 여 첫 번째 IP 주소가 hello hello 첫 번째 NIC에서</span><span class="sxs-lookup"><span data-stu-id="82335-131">In this example, we are using hello first IP address on hello first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="82335-132">IP 흐름 hello VM 리소스 toorun가 할당 되는 필요한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-132">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="82335-133">결과 검토</span><span class="sxs-lookup"><span data-stu-id="82335-133">Review Results</span></span>

<span data-ttu-id="82335-134">실행 된 후 `az network watcher test-ip-flow` hello 다음 예제는 hello 앞 단계에서에서 반환 된 hello 결과, hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82335-134">After running `az network watcher test-ip-flow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="82335-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82335-135">Next steps</span></span>

<span data-ttu-id="82335-136">트래픽을 차단 하지 않아야 하는 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello 네트워크 보안 그룹 및 보안 정의 된 규칙을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="82335-137">방문 하 여 tooaudit NSG 설정을 알아봅니다 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82335-137">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
