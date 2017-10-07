---
title: "VPN 게이트웨이 및 PowerShell을 사용 하 여 가상 네트워크 toomultiple 사이트 연결: 클래식 | Microsoft Docs"
description: "이 문서에서는 여러 로컬 온-프레미스 사이트 tooa 가상 네트워크 VPN 게이트웨이 사용 하 여 hello 클래식 배포 모델에 연결 하는 과정을 안내 합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="c1d58-103">사이트 간 연결 tooa VNet (클래식) 기존 VPN 게이트웨이 연결 된 추가</span><span class="sxs-lookup"><span data-stu-id="c1d58-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1d58-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c1d58-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c1d58-105">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="c1d58-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="c1d58-106">이 문서의 PowerShell tooadd 사이트 및 사이트 간 (S2S) 연결 tooa VPN 게이트웨이 기존 연결이 있는 사용 하 여 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="c1d58-107">이 연결의 형식은 종종 참조 tooas "멀티 사이트" 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="c1d58-108">hello이 문서의 단계 적용 toovirtual 네트워크 hello 클래식 배포 모델 (서비스 관리 라고 함)를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="c1d58-109">이러한 단계는 tooExpressRoute /-사이트 공존할 연결 구성 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="c1d58-110">배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="c1d58-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="c1d58-111">새 문서 및 추가 도구를 이 구성에 사용할 수 있게 되었으므로 다음 표를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="c1d58-112">문서를 사용할 수 있는이 테이블에서 tooit을 연결 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="c1d58-113">연결 정보</span><span class="sxs-lookup"><span data-stu-id="c1d58-113">About connecting</span></span>

<span data-ttu-id="c1d58-114">여러 온-프레미스 사이트 tooa 단일 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="c1d58-115">이 방식은 하이브리드 클라우드 솔루션을 구축하는 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="c1d58-116">다중 사이트 연결 tooyour Azure 가상 네트워크 게이트웨이 만들기는 비슷한 toocreating 다른 사이트 간 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="c1d58-117">실제로 hello 게이트웨이 동적으로 기존 Azure VPN 게이트웨이 사용할 수 있습니다 (경로 기반).</span><span class="sxs-lookup"><span data-stu-id="c1d58-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="c1d58-118">정적 게이트웨이에 연결 된 tooyour 가상 네트워크를 이미 있는 경우 순서 tooaccommodate 다중 사이트에 toorebuild hello 가상 네트워크 필요 없이 게이트웨이 유형 toodynamic hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="c1d58-119">Hello 라우팅 유형을 변경 하기 전에 온-프레미스 VPN 게이트웨이 경로 기반 VPN 구성을 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="c1d58-120">![다중 사이트 다이어그램](./media/vpn-gateway-multi-site/multisite.png "다중 사이트")</span><span class="sxs-lookup"><span data-stu-id="c1d58-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="c1d58-121">포인트 tooconsider</span><span class="sxs-lookup"><span data-stu-id="c1d58-121">Points tooconsider</span></span>

<span data-ttu-id="c1d58-122">**수 toouse hello 포털 toomake 변경 toothis 가상 네트워크 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="c1d58-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="c1d58-123">Hello 포털을 사용 하는 대신 toomake 변경 toohello 네트워크 구성 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="c1d58-124">Hello 포털에서 변경한 경우이 가상 네트워크에 대 한 다중 사이트 참조 설정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="c1d58-125">잘 알고 hello 시간별 hello 네트워크 구성 파일을 사용 하 여 hello 다중 사이트 절차를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="c1d58-126">그러나 네트워크 구성에 사용 하는 여러 사용자를 설정한 경우이 모두 알고 있어야이 대 한 toomake를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="c1d58-127">Hello 포털을 전혀 사용할 수 없다는 의미 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="c1d58-128">구성 변경 내용을 toothis 특정 가상 네트워크 만들기를 제외 하 고 다른 모든 항목에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c1d58-129">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c1d58-129">Before you begin</span></span>

<span data-ttu-id="c1d58-130">구성을 시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="c1d58-131">각 온-프레미스 위치에서 호환되는 VPN 하드웨어.</span><span class="sxs-lookup"><span data-stu-id="c1d58-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="c1d58-132">확인 [VPN 장치에 대 한 가상 네트워크 연결을 위한](vpn-gateway-about-vpn-devices.md) toobe 호환 알려진 tooverify toouse hello 장치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="c1d58-133">각 VPN 장치에 대한 외부 연결 공용 IPv4 IP 주소.</span><span class="sxs-lookup"><span data-stu-id="c1d58-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="c1d58-134">NAT 뒤 hello IP 주소를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="c1d58-135">이는 필수 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-135">This is requirement.</span></span>
* <span data-ttu-id="c1d58-136">Tooinstall hello 최신 버전의 hello Azure PowerShell cmdlet 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c1d58-137">또한 toohello 리소스 관리자 버전에 hello 서비스 관리 (SM) 버전을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="c1d58-138">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="c1d58-139">VPN 하드웨어 구성에 능숙한 사용자.</span><span class="sxs-lookup"><span data-stu-id="c1d58-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="c1d58-140">Toohave 방법 완전히 이해 해야 tooconfigure VPN 장치 또는 아는 사람과 함께 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="c1d58-141">hello IP 주소 범위 (아직 만들지 않은 하나) 하는 경우 가상 네트워크에 대 한 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="c1d58-142">각 hello 로컬 네트워크 사이트에 연결 하는 hello IP 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="c1d58-143">각 tooconnect toodo 겹치지 원하는 hello 로컬 네트워크 사이트에 hello IP 주소 범위는 있는지 toomake가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="c1d58-144">그렇지 않으면 hello 포털 또는 REST API hello hello 구성 되 고 업로드를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="c1d58-145">예를 들어 hello IP 주소 범위 10.2.3.0/24 모두 포함 하 고 대상 주소가 10.2.3.3 인 패키지에 있는 두 개의 로컬 네트워크 사이트가 있는 경우 Azure를 알 수 없습니다 toosend hello 패키지 toobecause hello 주소 범위는 원하는 어떤 사이트 겹칩니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="c1d58-146">tooprevent 라우팅 문제 Azure 허용 하지 않습니다 tooupload 범위가 겹치는 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="c1d58-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="c1d58-147">1. 사이트 간 VPN 만들기</span><span class="sxs-lookup"><span data-stu-id="c1d58-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="c1d58-148">동적 라우팅 게이트웨이를 사용한 사이트 간 VPN이 이미 있으면 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="c1d58-149">너무 진행할 수[hello 가상 네트워크 구성 설정 내보내기](#export)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="c1d58-150">그렇지 않은 경우 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="c1d58-151">사이트 간 가상 네트워크가 이미 있지만 정적(정책 기반) 라우팅 게이트웨이가 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="c1d58-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="c1d58-152">게이트웨이 유형 toodynamic 라우팅 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="c1d58-153">다중 사이트 VPN에는 동적(경로 기반이라고도 함) 라우팅 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="c1d58-154">toochange 게이트웨이 입력, 필요한 toofirst delete hello 기존 게이트웨이 만든 후 새로 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="c1d58-155">자세한 내용은 [어떻게 toochange hello VPN 게이트웨이 라우팅 유형을](vpn-gateway-configure-vpn-gateway-mp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="c1d58-156">새 게이트웨이를 구성하고 VPN 터널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="c1d58-157">자세한 내용은 [hello Azure 클래식 포털에서에서 VPN 게이트웨이 구성](vpn-gateway-configure-vpn-gateway-mp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="c1d58-158">먼저, 게이트웨이 유형 toodynamic 라우팅 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="c1d58-159">사이트 간 가상 네트워크 사이트가 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="c1d58-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="c1d58-160">이러한 지침을 사용 하 여 사이트 간 가상 네트워크를 만든: [hello Azure 클래식 포털에서에서 사이트 간 VPN 연결을 가진 가상 네트워크 만들기](vpn-gateway-site-to-site-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="c1d58-161">[VPN 게이트웨이 구성](vpn-gateway-configure-vpn-gateway-mp.md)을 참조하여 동적 라우팅 게이트웨이를 구성하십시오.</span><span class="sxs-lookup"><span data-stu-id="c1d58-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="c1d58-162">수 있는지 tooselect **동적 라우팅** 게이트웨이 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="c1d58-163"><a name="export"></a>2. 내보내기 hello 네트워크 구성 파일</span><span class="sxs-lookup"><span data-stu-id="c1d58-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="c1d58-164">Hello 다음 명령을 실행 하 여 Azure 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="c1d58-165">Hello 위치의 hello tooexport tooa 다른 필요한 경우 파일 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="c1d58-166">3. 열기 hello 네트워크 구성 파일</span><span class="sxs-lookup"><span data-stu-id="c1d58-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="c1d58-167">Hello 마지막 단계에서 다운로드 한 hello 네트워크 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="c1d58-168">원하는 xml 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-168">Use any xml editor that you like.</span></span> <span data-ttu-id="c1d58-169">hello 파일에는 비슷한 toohello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="c1d58-170">4. 여러 사이트 참조 추가</span><span class="sxs-lookup"><span data-stu-id="c1d58-170">4. Add multiple site references</span></span>
<span data-ttu-id="c1d58-171">구성 변경 내용을 추가 하거나 제거 하면 사이트 참조 정보를 지정 toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="c1d58-172">새 로컬 사이트 참조를 추가할 새 터널을 Azure toocreate 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="c1d58-173">Hello 아래의 예제에서는 hello 네트워크 구성은 단일 사이트 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="c1d58-174">프로그램의 변경을 완료 되 면 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="c1d58-175">(멀티 사이트 구성 만들기) tooadd 추가 사이트 참조를 아래 hello 예에 나와 있는 것 처럼 추가 "LocalNetworkSiteRef" 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="c1d58-176">5. Hello 네트워크 구성 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="c1d58-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="c1d58-177">Hello 네트워크 구성 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-177">Import hello network configuration file.</span></span> <span data-ttu-id="c1d58-178">Hello 변경 내용으로이 파일을 가져올 때 hello 새 터널이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="c1d58-179">hello 터널 hello 앞에서 만든 동적 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="c1d58-180">Hello 클래식 포털 또는 PowerShell tooimport hello 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="c1d58-181">6. 키 다운로드</span><span class="sxs-lookup"><span data-stu-id="c1d58-181">6. Download keys</span></span>
<span data-ttu-id="c1d58-182">새 터널을 추가한 후 각 터널용에 대 한 hello PowerShell cmdlet ' Get AzureVNetGatewayKey' tooget hello IPsec/IKE 사전 공유 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="c1d58-183">예:</span><span class="sxs-lookup"><span data-stu-id="c1d58-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="c1d58-184">원하는 경우 사용할 수도 있습니다 hello *가상 네트워크 게이트웨이 공유 키 가져오기* REST API tooget hello 사전 공유 키.</span><span class="sxs-lookup"><span data-stu-id="c1d58-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="c1d58-185">7. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="c1d58-185">7. Verify your connections</span></span>
<span data-ttu-id="c1d58-186">Hello 다중 사이트 터널 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="c1d58-187">Hello 각 터널용 키를 다운로드 한 후 tooverify 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="c1d58-188">아래 hello 예에 나와 있는 것 처럼 ' Get AzureVnetConnection' tooget 가상 네트워크의 목록이 터널링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="c1d58-189">VNet1에는 VNet hello hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="c1d58-190">예제는 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="c1d58-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1d58-191">Next steps</span></span>

<span data-ttu-id="c1d58-192">VPN 게이트웨이에 대 한 자세한 정보는 toolearn 참조 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1d58-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
