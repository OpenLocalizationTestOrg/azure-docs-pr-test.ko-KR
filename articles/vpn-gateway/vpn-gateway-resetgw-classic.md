---
title: "IPsec 터널는 Azure VPN 게이트웨이 tooreestablish 재설정 | Microsoft Docs"
description: "이 문서에서는 다시 설정 하 여 Azure VPN 게이트웨이 tooreestablish IPsec 터널을 통해 안내 합니다. hello 문서 tooVPN 게이트웨이 hello 리소스 관리자 배포 모델 및 클래식, hello에 적용 됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="818b5-104">VPN Gateway 다시 설정</span><span class="sxs-lookup"><span data-stu-id="818b5-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="818b5-105">Azure VPN Gateway 재설정은 하나 이상의 사이트 간 VPN 터널에서 크로스-프레미스 VPN 연결이 손실되는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="818b5-106">이 경우 온-프레미스 VPN 장치는 모든 정상적으로 작동 하지만 수 없습니다. tooestablish IPsec 터널 hello Azure VPN 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="818b5-107">이 문서는 VPN Gateway를 다시 설정하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="818b5-108">다시 설정하는 동안 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="818b5-108">What happens during a reset?</span></span>

<span data-ttu-id="818b5-109">VPN Gateway는 활성-대기 구성에서 실행 중인 두 VM 인스턴스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="818b5-110">Hello 게이트웨이 다시 설정 하면 hello 게이트웨이 다시 부팅 하 고 다시 적용 hello 크로스-프레미스 구성 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="818b5-111">hello 게이트웨이 이미 hello 공용 IP 주소를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="818b5-112">즉, Azure VPN 게이트웨이에 대 한 새 공용 IP 주소와 tooupdate hello VPN 라우터 구성 필요 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="818b5-113">Hello 명령 tooreset hello 게이트웨이 실행 하면 hello hello Azure VPN 게이트웨이의 현재 활성 인스턴스가 즉시 다시 부팅 된 경우</span><span class="sxs-lookup"><span data-stu-id="818b5-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="818b5-114">Hello 활성 인스턴스 (다시 부팅), toohello 대기 인스턴스 간에서 hello 장애 조치 중에 대 한 간략 한 간격이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="818b5-115">hello 시간 간격은 1 분 미만 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="818b5-116">문제 hello 동일 hello 연결 hello 첫 번째 다시 부팅 한 후 복원 되지 않으면, 명령을 다시 tooreboot hello 두 번째 VM 인스턴스 (hello 새 활성 게이트웨이).</span><span class="sxs-lookup"><span data-stu-id="818b5-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="818b5-117">Hello 2 회의 재부팅이 인 요청 된 뒤로 tooback 됩니다 약간 오랜 기간 동안 두 VM 인스턴스 (활성 및 대기) 되 고 다시 부팅 되는.</span><span class="sxs-lookup"><span data-stu-id="818b5-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="818b5-118">Vm toocomplete hello 재부팅 시 too2 too4 분을 hello VPN 연결에 더 긴 간격을 그러면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="818b5-119">두 번 다시 부팅 후 크로스-프레미스 연결에 문제가 여전히 발생 하는 경우 요청을 개시 하세요 지원 hello Azure 포털에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="818b5-120"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="818b5-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="818b5-121">게이트웨이 다시 설정 하기 전에 각 IPsec 사이트 및 사이트 간 (S2S) VPN 터널에 대 한 아래 나열 된 hello 주요 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="818b5-122">S2S VPN 터널의 hello 연결 끊기 hello 항목 일치 하지 않는 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="818b5-123">확인 하 고 온-프레미스 및 Azure VPN 게이트웨이에 대 한 hello 구성을 수정 하면 불필요 한 재부팅에서와 저장에 대 한 작업 중단 hello hello 게이트웨이의 다른 작업 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="818b5-124">Hello 게이트웨이 다시 설정 하기 전에 다음 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="818b5-125">hello 인터넷 IP (Vip) 모두 hello Azure VPN 게이트웨이 및 주소가 hello 온-프레미스 VPN 게이트웨이 모두 hello Azure와 hello 온-프레미스 VPN 정책이에 올바르게 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="818b5-126">hello 미리 공유한 키는 Azure 및 온-프레미스 VPN 게이트웨이에서 동일한 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="818b5-127">암호화, 해시 알고리즘 및 PFS (Perfect Forward 보안과) Azure hello 모두 있고 온-프레미스 VPN 게이트웨이 hello 확인와 같은 특정 IPsec/IKE 구성을 적용 하는 경우 동일한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="818b5-128"><a name="portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="818b5-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="818b5-129">Hello Azure 포털을 사용 하 여 리소스 관리자 VPN 게이트웨이 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="818b5-130">클래식 게이트웨이 tooreset hello를 참조 하십시오 [PowerShell](#resetclassic) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="818b5-131">리소스 관리자 배포 모델</span><span class="sxs-lookup"><span data-stu-id="818b5-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="818b5-132">열기 hello [Azure 포털](https://portal.azure.com) tooreset 원하는 toohello 리소스 관리자 가상 네트워크 게이트웨이 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="818b5-133">Hello 가상 네트워크 게이트웨이에 대 한 hello 블레이드를 원래 대로를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![VPN Gateway 블레이드 다시 설정](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="818b5-135">Hello에 블레이드를 다시 설정, hello **재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="818b5-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="818b5-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="818b5-137">리소스 관리자 배포 모델</span><span class="sxs-lookup"><span data-stu-id="818b5-137">Resource Manager deployment model</span></span>

<span data-ttu-id="818b5-138">게이트웨이 다시 설정에 대 한 cmdlet hello **재설정 AzureRmVirtualNetworkGateway**합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="818b5-139">리셋을 수행 하기 전에 최신 버전의 hello hello 있는지 확인 [리소스 관리자 PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="818b5-140">hello 다음 예제에서는 재설정 VNet1GW hello TestRG1 리소스 그룹에 이름이 지정 된 가상 네트워크 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="818b5-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="818b5-141">결과:</span><span class="sxs-lookup"><span data-stu-id="818b5-141">Result:</span></span>

<span data-ttu-id="818b5-142">반환 결과 받으면 hello 게이트웨이 재설정 했습니다 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="818b5-143">그러나에 없는 경우 아무 것도 해당 hello 재설정 성공적으로 명시적으로 나타내는 hello 반환 결과</span><span class="sxs-lookup"><span data-stu-id="818b5-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="818b5-144">Toolook hello 기록 toosee에 밀접 하 게 하려는 경우 hello 게이트웨이 재설정할 때 정확 하 게 발생 한 hello에서 해당 정보를 볼 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="818b5-145">Hello 포털에서 이동 너무**'GatewayName'-> 리소스 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="818b5-146"><a name="resetclassic"></a>클래식 배포 모델</span><span class="sxs-lookup"><span data-stu-id="818b5-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="818b5-147">게이트웨이 다시 설정에 대 한 cmdlet hello **재설정 AzureVNetGateway**합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="818b5-148">리셋을 수행 하기 전에 최신 버전의 hello hello 있는지 확인 [서비스 관리 (SM) PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="818b5-149">hello 다음 예제에서는 초기화 "ContosoVNet" 이라는 가상 네트워크에 대 한 hello 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="818b5-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="818b5-150">결과:</span><span class="sxs-lookup"><span data-stu-id="818b5-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="818b5-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="818b5-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="818b5-152">tooreset hello 게이트웨이 사용 하 여 hello [az 네트워크 vnet 게이트웨이 다시 설정](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="818b5-153">hello 다음 예제에서는 재설정 VNet5GW hello TestRG5 리소스 그룹에 이름이 지정 된 가상 네트워크 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="818b5-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="818b5-154">결과:</span><span class="sxs-lookup"><span data-stu-id="818b5-154">Result:</span></span>

<span data-ttu-id="818b5-155">반환 결과 받으면 hello 게이트웨이 재설정 했습니다 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="818b5-156">그러나에 없는 경우 아무 것도 해당 hello 재설정 성공적으로 명시적으로 나타내는 hello 반환 결과</span><span class="sxs-lookup"><span data-stu-id="818b5-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="818b5-157">Toolook hello 기록 toosee에 밀접 하 게 하려는 경우 hello 게이트웨이 재설정할 때 정확 하 게 발생 한 hello에서 해당 정보를 볼 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="818b5-158">Hello 포털에서 이동 너무**'GatewayName'-> 리소스 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="818b5-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
