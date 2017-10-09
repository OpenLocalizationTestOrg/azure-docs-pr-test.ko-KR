---
title: "Azure 사이트 간 연결의 강제 터널링 구성: 클래식 | Microsoft Docs"
description: "어떻게 tooredirect 또는 'force' 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 위치 합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="9edb7-103">강제 터널링을 사용 하 여 구성 hello 클래식 배포 모델</span><span class="sxs-lookup"><span data-stu-id="9edb7-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="9edb7-104">강제 터널링 리디렉션 또는 "강제" 검사 및 감사용 사이트 간 VPN 터널을 통해 모든 인터넷 바인딩된 트래픽이 백 tooyour 온-프레미스 위치로 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="9edb7-105">대부분의 엔터프라이즈 IT 정책에 있어서 중요한 보안 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="9edb7-106">강제 터널링 기능이 없으면 Azure 내 Vm의에서 인터넷 바인딩된 트래픽이 항상 트래버스할 hello 옵션 tooallow 없이 toohello 인터넷 아웃 직접 Azure 네트워크 인프라에서 있습니다 tooinspect 또는 감사 hello 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="9edb7-107">인터넷에 대 한 무단된 액세스 tooinformation 노출 또는 기타 유형의 보안 위반을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="9edb7-108">이 문서에서는 구성 강제 hello 클래식 배포 모델을 사용 하 여 만든 가상 네트워크에 대 한 터널링 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="9edb7-109">강제 터널링 되지 hello 포털을 통해 PowerShell을 사용 하 여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="9edb7-110">Tooconfigure 강제 터널링 hello 리소스 관리자 배포 모델에 대 한 클래식 문서 hello 다음 드롭다운 목록에서에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9edb7-111">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="9edb7-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="9edb7-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9edb7-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="9edb7-113">요구 사항 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="9edb7-113">Requirements and considerations</span></span>
<span data-ttu-id="9edb7-114">Azure에서 강제 터널링은 가상 네트워크 UDR(사용자 정의 경로)을 통해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="9edb7-115">트래픽 tooan 리디렉션 온-프레미스 사이트는 기본 경로 toohello Azure VPN 게이트웨이로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="9edb7-116">hello 다음 섹션에는 Azure 가상 네트워크에 대 한 경로 및 hello 라우팅 테이블의 한 hello 현재 제한:</span><span class="sxs-lookup"><span data-stu-id="9edb7-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="9edb7-117">각 가상 네트워크 서브넷에는 기본 제공 시스템 라우팅 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="9edb7-118">hello 시스템에 대 한 라우팅 테이블에는 3 개의 그룹의 경로 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="9edb7-119">**지역 VNet 경로:** 직접 toohello의에서 대상 Vm hello 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="9edb7-120">**온-프레미스 경로:** toohello Azure VPN 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="9edb7-121">**기본 경로:** toohello 인터넷 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="9edb7-122">패킷을 toohello 개인 IP 주소 hello 이전 두 경로에서 포함 하지 않는 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="9edb7-123">사용자 정의 경로의 hello 릴리스로 라우팅 테이블 tooadd 기본 경로 만들 수 있으며 hello 라우팅 테이블 tooyour VNet 서브넷 tooenable 강제 터널링 이러한 서브넷에 연결 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="9edb7-124">Hello 크로스-프레미스 로컬 사이트 toohello 연결 된 가상 네트워크 간에 tooset "기본 사이트" 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="9edb7-125">강제 터널링은 동적 라우팅 VPN Gateway(정적 게이트웨이 아님)가 있는 VNet에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="9edb7-126">Express 경로 강제 터널링이 메커니즘을 통해 구성 되지 않은 하지만 대신 hello ExpressRoute BGP를 통해 기본 경로으로 활성화 되어 피어 링 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="9edb7-127">Hello를 참조 하십시오 [express 경로 설명서](https://azure.microsoft.com/documentation/services/expressroute/) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="9edb7-128">구성 개요</span><span class="sxs-lookup"><span data-stu-id="9edb7-128">Configuration overview</span></span>
<span data-ttu-id="9edb7-129">다음 예제는 hello, 프런트 엔드 서브넷은 강제 되지 hello 터널링 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="9edb7-130">hello 프런트 엔드 서브넷에 hello 작업 tooaccept 계속 한 hello 인터넷에서에서 직접 toocustomer 요청에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="9edb7-131">hello 중간 계층 및 백 엔드 서브넷은 강제 터널링 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="9edb7-132">이러한 두 서브넷 toohello 인터넷의에서 모든 아웃 바운드 연결에는 hello S2S VPN 터널 중 하나를 통해 강제 또는 다시 리디렉션된 tooan 온-프레미스 사이트가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="9edb7-133">이 toorestrict 있습니다 및 가상 컴퓨터에서 인터넷 액세스를 검사 또는 tooenable 필요한 다중 계층 서비스 아키텍처를 계속 하면서 클라우드 azure에서 서비스.</span><span class="sxs-lookup"><span data-stu-id="9edb7-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="9edb7-134">또한 가상 네트워크에 인터넷 연결 작업이 없는 경우 강제 터널링 toohello 전체 가상 네트워크를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![강제 터널링](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="9edb7-136">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9edb7-136">Before you begin</span></span>
<span data-ttu-id="9edb7-137">다음 항목 구성 시작 하기 전에 hello 수 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9edb7-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="9edb7-138">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="9edb7-138">An Azure subscription.</span></span> <span data-ttu-id="9edb7-139">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9edb7-140">구성된 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-140">A configured virtual network.</span></span> 
* <span data-ttu-id="9edb7-141">hello hello Azure PowerShell cmdlet의 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9edb7-142">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="9edb7-143">강제 터널링 구성</span><span class="sxs-lookup"><span data-stu-id="9edb7-143">Configure forced tunneling</span></span>
<span data-ttu-id="9edb7-144">절차를 수행 하는 hello를 사용 하는 가상 네트워크에 대해 강제 터널링을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="9edb7-145">toohello VNet 네트워크 구성 파일을 해당 하는 hello 구성 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="9edb7-146">이 예제에서는 ' Multitier-vnet ' hello 가상 네트워크에 서브넷이 3 개의: 4 개의 크로스 프레미스 연결과 '프런트 엔드', 'Midtier' 및 '백 엔드' 서브넷: 'DefaultSiteHQ' 및 3 개 분기 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="9edb7-147">hello 단계 'DefaultSiteHQ' hello 강제 터널링 용 hello 기본 사이트 연결으로 설정 하 고 hello Midtier 및 Backend 서브넷 toouse 강제 터널링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="9edb7-148">라우팅 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-148">Create a routing table.</span></span> <span data-ttu-id="9edb7-149">다음 cmdlet toocreate hello 경로 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="9edb7-150">기본 경로 toohello 라우팅 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="9edb7-151">hello 다음 예제에서는 추가 기본 경로 toohello 라우팅 테이블 1 단계에서에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="9edb7-152">지원 되는 경로 hello 참고는 "0.0.0.0/0" toohello "VPNGateway" 다음 홉의 hello 대상 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="9edb7-153">Hello 라우팅 테이블 toohello 서브넷을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="9edb7-154">라우팅 테이블을 만들고는 경로 추가, 후에 다음 예제에서는 tooadd hello를 사용 하거나 hello 경로 테이블 tooa VNet 서브넷 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="9edb7-155">hello 경로 테이블 "MyRouteTable" toohello Midtier 및 Backend 서브넷의 multitier-vnet VNet을 추가 하는 hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="9edb7-156">강제 터널링에 대한 기본 사이트를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="9edb7-157">앞 단계 hello, hello 샘플 cmdlet 스크립트 라우팅 테이블 hello 만들고 hello 경로 테이블 tootwo hello VNet 서브넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="9edb7-158">hello 나머지 단계는 tooselect hello 기본 사이트 또는 터널와 hello 가상 네트워크의 hello 다중 사이트 연결에서 로컬 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9edb7-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="9edb7-159">추가 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="9edb7-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="9edb7-160">경로 테이블 toodelete</span><span class="sxs-lookup"><span data-stu-id="9edb7-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="9edb7-161">경로 테이블 toolist</span><span class="sxs-lookup"><span data-stu-id="9edb7-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="9edb7-162">경로 테이블에서 경로 toodelete</span><span class="sxs-lookup"><span data-stu-id="9edb7-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="9edb7-163">tooremove 서브넷에서 경로</span><span class="sxs-lookup"><span data-stu-id="9edb7-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="9edb7-164">서브넷과 연결 된 toolist hello 경로 테이블</span><span class="sxs-lookup"><span data-stu-id="9edb7-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="9edb7-165">tooremove VNet VPN 게이트웨이에서 기본 사이트</span><span class="sxs-lookup"><span data-stu-id="9edb7-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```