---
title: "지점 및 사이트 간 연결과 인증서 인증을 사용하여 가상 네트워크에 컴퓨터 연결: Azure Portal 클래식 | Microsoft Docs"
description: "Azure Portal을 사용하여 지점 및 사이트 간 VPN Gateway 연결을 만들어 클래식 Azure Virtual Network에 안전하게 연결합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 5ac679279bb977fb7d38b5046164d1b5f6a80e0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-classic-azure-portal"></a><span data-ttu-id="d4a6d-103">인증서 인증(클래식)을 사용하여 VNet에 지점 및 사이트 간 연결 구성: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d4a6d-103">Configure a Point-to-Site connection to a VNet using certificate authentication (classic): Azure portal</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

<span data-ttu-id="d4a6d-104">이 문서에서는 클래식 배포 모델에서 Azure Portal을 사용하여 지점 및 사이트 간 연결로 VNet을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-104">This article shows you how to create a VNet with a Point-to-Site connection in the classic deployment model using the Azure portal.</span></span> <span data-ttu-id="d4a6d-105">이 구성은 인증서를 사용하여 연결 중인 클라이언트를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-105">This configuration uses certificates to authenticate the connecting client.</span></span> <span data-ttu-id="d4a6d-106">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-106">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4a6d-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d4a6d-107">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="d4a6d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4a6d-108">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="d4a6d-109">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="d4a6d-109">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

<span data-ttu-id="d4a6d-110">지점 및 사이트 간(P2S) VPN Gateway를 통해 개별 클라이언트 컴퓨터에서 가상 네트워크에 안전한 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-110">A Point-to-Site (P2S) VPN gateway lets you create a secure connection to your virtual network from an individual client computer.</span></span> <span data-ttu-id="d4a6d-111">지점 및 사이트 간 VPN 연결은 집 또는 회의에서 원격 통신하는 경우와 같이 원격 위치에서 VNet에 연결하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-111">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="d4a6d-112">VNet에 연결해야 하는 몇 가지 클라이언트만 있는 경우에 사이트 간 VPN 대신 P2S VPN을 사용하는 것도 유용한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-112">A P2S VPN is also a useful solution to use instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span> 

<span data-ttu-id="d4a6d-113">P2S는 SSL 기반 VPN 프로토콜인 SSTP(Secure Socket Tunneling Protocol)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-113">P2S uses the Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="d4a6d-114">클라이언트 컴퓨터에서 시작하여 P2S VPN 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-114">A P2S VPN connection is established by starting it from the client computer.</span></span>


![지점 및 사이트 간 다이어그램](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


<span data-ttu-id="d4a6d-116">지점 및 사이트 간 인증서 인증 연결을 사용하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-116">Point-to-Site certificate authentication connections require the following:</span></span>

* <span data-ttu-id="d4a6d-117">동적 VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="d4a6d-117">A Dynamic VPN gateway.</span></span>
* <span data-ttu-id="d4a6d-118">Azure에 업로드된 루트 인증서에 대한 공개 키(.cer 파일)입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-118">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span></span> <span data-ttu-id="d4a6d-119">신뢰할 수 있는 인증서로 간주되며 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-119">This is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="d4a6d-120">루트 인증서에서 생성되고 연결할 각 클라이언트 컴퓨터에 설치된 클라이언트 인증서 -</span><span class="sxs-lookup"><span data-stu-id="d4a6d-120">A client certificate generated from the root certificate, and installed on each client computer that will connect.</span></span> <span data-ttu-id="d4a6d-121">클라이언트 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-121">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="d4a6d-122">연결하는 모든 클라이언트 컴퓨터에 VPN 클라이언트 구성 패키지를 생성하여 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-122">A VPN client configuration package must be generated and installed on every client computer that connects.</span></span> <span data-ttu-id="d4a6d-123">클라이언트 구성 패키지는 VNet에 연결하는 데 필요한 정보와 함께 운영 체제에 이미 있는 기본 VPN 클라이언트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-123">The client configuration package configures the native VPN client that is already on the operating system with the necessary information to connect to the VNet.</span></span>

<span data-ttu-id="d4a6d-124">지점 및 사이트 간 연결에는 VPN 장치 또는 온-프레미스 공용 IP 주소가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-124">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="d4a6d-125">VPN 연결은 SSTP(Secure Socket Tunneling Protocol)를 통해 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-125">The VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="d4a6d-126">서버 쪽에서 SSTP 버전 1.0, 1.1 및 1.2를 지원하며,</span><span class="sxs-lookup"><span data-stu-id="d4a6d-126">On the server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="d4a6d-127">클라이언트에서 사용할 버전을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-127">The client decides which version to use.</span></span> <span data-ttu-id="d4a6d-128">Windows 8.1 이상에서는 기본적으로 SSTP 버전 1.2를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-128">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="d4a6d-129">지점 및 사이트 간 연결에 대한 자세한 내용은 이 문서의 끝에 있는 [지점 및 사이트 간 FAQ](#faq)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-129">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span></span>

### <a name="example-settings"></a><span data-ttu-id="d4a6d-130">예제 설정</span><span class="sxs-lookup"><span data-stu-id="d4a6d-130">Example settings</span></span>

<span data-ttu-id="d4a6d-131">다음 값을 사용하여 테스트 환경을 만들거나 이 값을 참조하여 이 문서의 예제를 보다 정확하게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-131">You can use the following values to create a test environment, or refer to these values to better understand the examples in this article:</span></span>

* <span data-ttu-id="d4a6d-132">**이름: VNet1**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-132">**Name: VNet1**</span></span>
* <span data-ttu-id="d4a6d-133">**주소 공간: 192.168.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-133">**Address space: 192.168.0.0/16**</span></span><br><span data-ttu-id="d4a6d-134">이 예제에서는 하나의 주소 공간만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-134">For this example, we use only one address space.</span></span> <span data-ttu-id="d4a6d-135">VNet에는 둘 이상의 주소 공간을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-135">You can have more than one address space for your VNet.</span></span>
* <span data-ttu-id="d4a6d-136">**서브넷 이름: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-136">**Subnet name: FrontEnd**</span></span>
* <span data-ttu-id="d4a6d-137">**서브넷 주소 범위: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-137">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="d4a6d-138">**구독:** 구독이 2개 이상 있는 경우 올바른 구독을 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-138">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="d4a6d-139">**리소스 그룹: TestRG**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-139">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="d4a6d-140">**위치: 미국 동부**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-140">**Location: East US**</span></span>
* <span data-ttu-id="d4a6d-141">**연결 형식: 지점 및 사이트 간**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-141">**Connection type: Point-to-site**</span></span>
* <span data-ttu-id="d4a6d-142">**클라이언트 주소 공간: 172.16.201.0/24**.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-142">**Client Address Space: 172.16.201.0/24**.</span></span> <span data-ttu-id="d4a6d-143">이 지점 및 사이트 간 연결을 사용하여 VNet에 연결되는 VPN 클라이언트는 지정된 풀에서 IP 주소를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-143">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the specified pool.</span></span>
* <span data-ttu-id="d4a6d-144">**GatewaySubnet: 192.168.200.0/24**.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-144">**GatewaySubnet: 192.168.200.0/24**.</span></span> <span data-ttu-id="d4a6d-145">게이트웨이 서브넷의 이름으로 "GatewaySubnet"을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-145">The Gateway subnet must use the name 'GatewaySubnet'.</span></span>
* <span data-ttu-id="d4a6d-146">**크기:** 사용할 게이트웨이 SKU를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-146">**Size:** Select the gateway SKU that you want to use.</span></span>
* <span data-ttu-id="d4a6d-147">**라우팅 유형: 동적**</span><span class="sxs-lookup"><span data-stu-id="d4a6d-147">**Routing Type: Dynamic**</span></span>

## <span data-ttu-id="d4a6d-148"><a name="vnetvpn"></a>1. 가상 네트워크 및 VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="d4a6d-148"><a name="vnetvpn"></a>1. Create a virtual network and a VPN gateway</span></span>

<span data-ttu-id="d4a6d-149">시작하기 전에 Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-149">Before beginning, verify that you have an Azure subscription.</span></span> <span data-ttu-id="d4a6d-150">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-150">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>

### <span data-ttu-id="d4a6d-151"><a name="createvnet"></a>1부: 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="d4a6d-151"><a name="createvnet"></a>Part 1: Create a virtual network</span></span>

<span data-ttu-id="d4a6d-152">가상 네트워크가 아직 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-152">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="d4a6d-153">스크린샷은 예제로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-153">Screenshots are provided as examples.</span></span> <span data-ttu-id="d4a6d-154">사용자 고유의 값으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-154">Be sure to replace the values with your own.</span></span> <span data-ttu-id="d4a6d-155">Azure 포털을 사용하여 VNet을 만들려면 다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-155">To create a VNet by using the Azure portal, use the following steps:</span></span>

1. <span data-ttu-id="d4a6d-156">브라우저에서 [Azure 포털](http://portal.azure.com) 로 이동하고 필요한 경우 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-156">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="d4a6d-157">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-157">Click **New**.</span></span> <span data-ttu-id="d4a6d-158">**마켓플레이스 검색** 필드에 ‘Virtual Network’를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-158">In the **Search the marketplace** field, type 'Virtual Network'.</span></span> <span data-ttu-id="d4a6d-159">반환된 목록에서 **Virtual Network**를 찾아서 클릭하여 **Virtual Network** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-159">Locate **Virtual Network** from the returned list and click to open the **Virtual Network** page.</span></span>

  ![가상 네트워크 검색 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. <span data-ttu-id="d4a6d-161">Virtual Network 페이지 아래쪽 근처의 **배포 모델 선택** 목록에서 **클래식**을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-161">Near the bottom of the Virtual Network page, from the **Select a deployment model** list, select **Classic**, and then click **Create**.</span></span>

  ![배포 모델 선택](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. <span data-ttu-id="d4a6d-163">**가상 네트워크 만들기** 페이지에서 VNet 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-163">On the **Create virtual network** page, configure the VNet settings.</span></span> <span data-ttu-id="d4a6d-164">이 페이지에서 첫 번째 주소 공간과 단일 서브넷 주소 범위를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-164">On this page, you add your first address space and a single subnet address range.</span></span> <span data-ttu-id="d4a6d-165">VNet 만들기를 완료한 후에 다시 돌아와서 추가 서브넷 및 주소 공간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-165">After you finish creating the VNet, you can go back and add additional subnets and address spaces.</span></span>

  ![가상 네트워크 만들기 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. <span data-ttu-id="d4a6d-167">**구독**이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-167">Verify that the **Subscription** is the correct one.</span></span> <span data-ttu-id="d4a6d-168">드롭다운을 사용하여 구독을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-168">You can change subscriptions by using the drop-down.</span></span>
6. <span data-ttu-id="d4a6d-169">**리소스 그룹**을 클릭하고 기존 리소스 그룹을 선택하거나 새 리소스 그룹에 대한 이름을 입력하여 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-169">Click **Resource group** and either select an existing resource group, or create a new one by typing a name for your new resource group.</span></span> <span data-ttu-id="d4a6d-170">새 리소스 그룹을 만드는 경우 계획된 구성 값에 따라 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-170">If you are creating a new resource group, name the resource group according to your planned configuration values.</span></span> <span data-ttu-id="d4a6d-171">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-171">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="d4a6d-172">다음으로 VNet에 대한 **위치** 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-172">Next, select the **Location** settings for your VNet.</span></span> <span data-ttu-id="d4a6d-173">이 위치는 VNet에 배포하는 리소스가 상주할 곳을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-173">The location determines where the resources that you deploy to this VNet will reside.</span></span>
8. <span data-ttu-id="d4a6d-174">대시보드에서 VNet을 쉽게 찾을 수 있으려면 **대시보드에 고정**을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-174">Select **Pin to dashboard** if you want to be able to find your VNet easily on the dashboard, and then click **Create**.</span></span>

  ![대시보드에 고정](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. <span data-ttu-id="d4a6d-176">[만들기]를 클릭하면 VNet의 진행 상황을 반영하는 타일이 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-176">After clicking Create, a tile appears on your dashboard that will reflect the progress of your VNet.</span></span> <span data-ttu-id="d4a6d-177">타일은 VNet이 생성되면서 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-177">The tile changes as the VNet is being created.</span></span>

  ![가상 네트워크 만들기 타일](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. <span data-ttu-id="d4a6d-179">가상 네트워크를 만들면 Azure 클래식 포털의 네트워크 페이지에 있는 **상태** 아래에 **만들어짐**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-179">Once your virtual network has been created, you see **Created** listed under **Status** on the networks page in the Azure classic portal.</span></span>
11. <span data-ttu-id="d4a6d-180">DNS 서버를 추가합니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="d4a6d-180">Add a DNS server (optional).</span></span> <span data-ttu-id="d4a6d-181">가상 네트워크를 만든 후에 이름 확인을 위해 DNS 서버의 IP 주소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-181">After you create your virtual network, you can add the IP address of a DNS server for name resolution.</span></span> <span data-ttu-id="d4a6d-182">지정한 DNS 서버 IP 주소는 VNet에서 리소스의 이름을 확인할 수 있는 DNS 서버의 주소여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-182">The DNS server IP address that you specify should be the address of a DNS server that can resolve the names for the resources in your VNet.</span></span><br><span data-ttu-id="d4a6d-183">DNS 서버를 추가하려면 가상 네트워크에 대한 설정을 열고 DNS 서버를 클릭하고 사용하려는 DNS 서버의 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-183">To add a DNS server, open the settings for your virtual network, click DNS servers, and add the IP address of the DNS server that you want to use.</span></span>

### <span data-ttu-id="d4a6d-184"><a name="gateway"></a>2부: 게이트웨이 서브넷 및 동적 라우팅 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="d4a6d-184"><a name="gateway"></a>Part 2: Create gateway subnet and a dynamic routing gateway</span></span>

<span data-ttu-id="d4a6d-185">이 단계에서는 게이트웨이 서브넷 및 동적 라우팅 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-185">In this step, you create a gateway subnet and a Dynamic routing gateway.</span></span> <span data-ttu-id="d4a6d-186">클래식 배포 모델을 위한 Azure Portal에서 게이트웨이 서브넷 및 게이트웨이 만들기는 동일한 구성 페이지를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-186">In the Azure portal for the classic deployment model, creating the gateway subnet and the gateway can be done through the same configuration pages.</span></span>

1. <span data-ttu-id="d4a6d-187">포털에서 게이트웨이를 만들려는 가상 네트워크로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-187">In the portal, navigate to the virtual network for which you want to create a gateway.</span></span>
2. <span data-ttu-id="d4a6d-188">가상 네트워크에 대한 페이지에 대해, **개요** 페이지의 VPN 연결 섹션에서 **게이트웨이**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-188">On the page for your virtual network, on the **Overview** page, in the VPN connections section, click **Gateway**.</span></span>

  ![클릭하여 게이트웨이 서브넷 만들기](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. <span data-ttu-id="d4a6d-190">**새 VPN 연결** 페이지에서 **지점 및 사이트 간**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-190">On the **New VPN Connection** page, select **Point-to-site**.</span></span>

  ![지점 및 사이트 간 연결 형식](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. <span data-ttu-id="d4a6d-192">**클라이언트 주소 공간**에 대해 IP 주소 범위를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-192">For **Client Address Space**, add the IP address range.</span></span> <span data-ttu-id="d4a6d-193">연결할 때 VPN 클라이언트에서 IP 주소를 받는 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-193">This is the range from which the VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="d4a6d-194">연결 원본이 되는 온-프레미스 위치 또는 연결 대상이 되는 VNet과 겹치지 않는 개인 IP 주소 범위를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-194">Use a private IP address range that does not overlap with the on-premises location that you will connect from, or with the VNet that you want to connect to.</span></span> <span data-ttu-id="d4a6d-195">자동으로 채워진 범위를 삭제한 다음 사용하려는 개인 IP 주소 범위를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-195">You can delete the auto-filled range, then add the private IP address range that you want to use.</span></span>

  ![클라이언트 주소 공간](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. <span data-ttu-id="d4a6d-197">**게이트웨이 즉시 만들기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-197">Select the **Create gateway immediately** checkbox.</span></span>

  ![게이트웨이 즉시 만들기](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. <span data-ttu-id="d4a6d-199">**선택적 게이트웨이 구성**을 클릭하여 **게이트웨이 구성** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-199">Click **Optional gateway configuration** to open the **Gateway configuration** page.</span></span>

  ![선택적 게이트웨이 구성 클릭](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. <span data-ttu-id="d4a6d-201">**서브넷 필수 설정 구성**을 클릭하여 **게이트웨이 서브넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-201">Click **Subnet Configure required settings** to add the **gateway subnet**.</span></span> <span data-ttu-id="d4a6d-202">게이트웨이 서브넷을 /29만큼 작게 만들 수 있지만 적어도 /28 또는 /27을 선택하여 더 많은 주소를 포함하는 큰 서브넷을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-202">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="d4a6d-203">이렇게 하면 나중에 필요할 수도 있는 추가 구성에 맞게 충분히 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-203">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span> <span data-ttu-id="d4a6d-204">게이트웨이 서브넷에서 작업할 때는 게이트웨이 서브넷에 NSG(네트워크 보안 그룹)를 연결하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-204">When working with gateway subnets, avoid associating a network security group (NSG) to the gateway subnet.</span></span> <span data-ttu-id="d4a6d-205">이 서브넷에 네트워크 보안 그룹을 연결하면 VPN Gateway가 정상적으로 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-205">Associating a network security group to this subnet may cause your VPN gateway to stop functioning as expected.</span></span>

  ![GatewaySubnet 추가](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. <span data-ttu-id="d4a6d-207">게이트웨이 **크기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-207">Select the gateway **Size**.</span></span> <span data-ttu-id="d4a6d-208">크기는 가상 네트워크 게이트웨이에 대한 게이트웨이 SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-208">The size is the gateway SKU for your virtual network gateway.</span></span> <span data-ttu-id="d4a6d-209">포털에서 SKU 기본값은 **기본**입니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-209">In the portal, the Default SKU is **Basic**.</span></span> <span data-ttu-id="d4a6d-210">게이트웨이 SKU에 대한 자세한 내용은 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-210">For more information about gateway SKUs, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

  ![게이트웨이 크기](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. <span data-ttu-id="d4a6d-212">게이트웨이에 대한 **라우팅 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-212">Select the **Routing Type** for your gateway.</span></span> <span data-ttu-id="d4a6d-213">P2S 구성에는 **동적** 라우팅 유형이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-213">P2S configurations require a **Dynamic** routing type.</span></span> <span data-ttu-id="d4a6d-214">이 페이지 구성을 완료했으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-214">Click **OK** when you have finished configuring this page.</span></span>

  ![라우팅 유형 구성](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. <span data-ttu-id="d4a6d-216">**새 VPN 연결** 페이지 하단에 **확인**을 클릭하여 가상 네트워크 게이트웨이 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-216">On the **New VPN Connection** page, click **OK** at the bottom of the page to begin creating your virtual network gateway.</span></span> <span data-ttu-id="d4a6d-217">VPN 게이트웨이는 선택한 게이트웨이 SKU에 따라 완료하는 데 최대 45분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-217">A VPN gateway can take up to 45 minutes to complete, depending on the gateway sku that you select.</span></span>

## <span data-ttu-id="d4a6d-218"><a name="generatecerts"></a>2. 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="d4a6d-218"><a name="generatecerts"></a>2. Create certificates</span></span>

<span data-ttu-id="d4a6d-219">인증서는 지점 및 사이트 간 VPN에 대한 VPN 클라이언트를 인증하기 위해 Azure에 의해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-219">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="d4a6d-220">Azure에 루트 인증서의 공개 키 정보를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-220">You upload the public key information of the root certificate to Azure.</span></span> <span data-ttu-id="d4a6d-221">그러면 해당 공개 키가 '신뢰할 수 있는 키'로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-221">The public key is then considered 'trusted'.</span></span> <span data-ttu-id="d4a6d-222">클라이언트 인증서는 신뢰할 수 있는 루트 인증서에서 생성한 다음 각 클라이언트 컴퓨터의 [인증서 - 현재 사용자/개인] 인증서 저장소에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-222">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="d4a6d-223">인증서는 VNet에 대한 연결을 시작할 때 해당 클라이언트를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-223">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span></span> 

<span data-ttu-id="d4a6d-224">자체 서명된 인증서를 사용하는 경우 특정 매개 변수를 사용하여 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-224">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="d4a6d-225">[PowerShell 및 Windows 10](vpn-gateway-certificates-point-to-site.md) 또는 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)에 대한 지침을 사용하여 자체 서명된 인증서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-225">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="d4a6d-226">자체 서명된 루트 인증서로 작동하고 자체 서명된 루트 인증서에서 클라이언트 인증서를 생성할 때 이들 지침에 있는 단계를 따르는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-226">It's important that you follow the steps in these instructions when working with self-signed root certificates and generating client certificates from the self-signed root certificate.</span></span> <span data-ttu-id="d4a6d-227">그렇지 않으면 만든 인증서는 P2S 연결과 호환되지 않으며 연결 오류가 발생하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-227">Otherwise, the certificates you create will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="d4a6d-228"><a name="cer"></a>1부: 루트 인증서용 공개 키(.cer) 가져오기</span><span class="sxs-lookup"><span data-stu-id="d4a6d-228"><a name="cer"></a>Part 1: Obtain the public key (.cer) for the root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <span data-ttu-id="d4a6d-229"><a name="genclientcert"></a>2부: 클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="d4a6d-229"><a name="genclientcert"></a>Part 2: Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="d4a6d-230"><a name="upload"></a>3. 루트 인증서 .cer 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d4a6d-230"><a name="upload"></a>3. Upload the root certificate .cer file</span></span>

<span data-ttu-id="d4a6d-231">게이트웨이를 만든 후에 신뢰할 수 있는 루트 인증서의 .cer 파일(공개 키 정보 포함)을 Azure로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-231">After the gateway has been created, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span></span> <span data-ttu-id="d4a6d-232">루트 인증서에 대한 개인 키를 Azure에 업로드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-232">You do not upload the private key for the root certificate to Azure.</span></span> <span data-ttu-id="d4a6d-233">a.cer 파일이 업로드되면 Azure는 이.cer 파일을 사용하여 신뢰할 수 있는 루트 인증서에서 생성된 클라이언트 인증서를 설치한 클라이언트를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-233">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span></span> <span data-ttu-id="d4a6d-234">필요한 경우 나중에 신뢰할 수 있는 루트 인증서 파일을 최대 20개까지 추가로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-234">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span></span>  

1. <span data-ttu-id="d4a6d-235">VNet에 대한 페이지의 **VPN 연결** 섹션에서 **클라이언트** 그래픽을 클릭하여 **지점 및 사이트 간 VPN 연결** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-235">On the **VPN connections** section of the page for your VNet, click the **clients** graphic to open the **Point-to-site VPN connection** page.</span></span>

  ![클라이언트](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. <span data-ttu-id="d4a6d-237">**지점 및 사이트 간 연결** 페이지에서 **인증서 관리**를 클릭하여 **인증서** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-237">On the **Point-to-site connection** page, click **Manage certificates** to open the **Certificates** page.</span></span><br>

  ![인증서 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. <span data-ttu-id="d4a6d-239">**인증서** 페이지에서 **업로드**를 클릭하여 **인증서 업로드** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-239">On the **Certificates** page, click **Upload** to open the **Upload certificate** page.</span></span><br>

    ![인증서 업로드 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. <span data-ttu-id="d4a6d-241">폴더 그래픽을 클릭하여 .cer 파일을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-241">Click the folder graphic to browse for the .cer file.</span></span> <span data-ttu-id="d4a6d-242">파일을 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-242">Select the file, then click **OK**.</span></span> <span data-ttu-id="d4a6d-243">페이지를 새로 고쳐 **인증서** 페이지에서 업로드된 인증서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-243">Refresh the page to see the uploaded certificate on the **Certificates** page.</span></span>

  ![인증서 업로드](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <span data-ttu-id="d4a6d-245"><a name="vpnclientconfig"></a>4. 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="d4a6d-245"><a name="vpnclientconfig"></a>4. Configure the client</span></span>

<span data-ttu-id="d4a6d-246">지점 및 사이트 간 VPN을 사용하여 VNet에 연결하려면 각 클라이언트에서 기본 Windows VPN 클라이언트를 구성하는 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-246">To connect to a VNet using a Point-to-Site VPN, each client must install a package to configure the native Windows VPN client.</span></span> <span data-ttu-id="d4a6d-247">구성 패키지는 가상 네트워크에 연결하는 데 필요한 설정을 사용하여 네이티브 Windows VPN 클라이언트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-247">The configuration package configures the native Windows VPN client with the settings necessary to connect to the virtual network.</span></span>

<span data-ttu-id="d4a6d-248">버전이 클라이언트의 아키텍처와 일치하는 한 각 클라이언트 컴퓨터에서 동일한 VPN 클라이언트 구성 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-248">You can use the same VPN client configuration package on each client computer, as long as the version matches the architecture for the client.</span></span> <span data-ttu-id="d4a6d-249">지원되는 클라이언트 운영 체제의 목록은 이 문서 끝의 [지점 및 사이트 간 연결 FAQ](#faq)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-249">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span></span>

### <span data-ttu-id="d4a6d-250"><a name="generateconfigpackage"></a>1부: VPN 클라이언트 구성 패키지 생성 및 설치</span><span class="sxs-lookup"><span data-stu-id="d4a6d-250"><a name="generateconfigpackage"></a>Part 1: Generate and install the VPN client configuration package</span></span>

1. <span data-ttu-id="d4a6d-251">Azure Portal에서 VNet에 대한 **개요** 페이지의 **VPN 연결**에서 클라이언트 그래픽을 클릭하여 **지점 및 사이트 간 VPN 연결** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-251">In the Azure portal, in the **Overview** page for your VNet, in **VPN connections**, click the client graphic to open the **Point-to-site VPN connection** page.</span></span>
2. <span data-ttu-id="d4a6d-252">**지점 및 사이트 간 VPN 연결** 페이지 맨 위에서 설치할 클라이언트 운영 체제에 해당하는 다운로드 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-252">At the top of the **Point-to-site VPN connection** page, click the download package that corresponds to the client operating system on which it will be installed:</span></span>

  * <span data-ttu-id="d4a6d-253">64비트 클라이언트인 경우 **VPN 클라이언트(64비트)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-253">For 64-bit clients, select **VPN Client (64-bit)**.</span></span>
  * <span data-ttu-id="d4a6d-254">32비트 클라이언트인 경우 **VPN 클라이언트(32비트)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-254">For 32-bit clients, select **VPN Client (32-bit)**.</span></span>

  ![VPN 클라이언트 구성 패키지 다운로드](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. <span data-ttu-id="d4a6d-256">패키지가 생성되면 다운로드하여 클라이언트 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-256">Once the packaged generates, download and install it on your client computer.</span></span> <span data-ttu-id="d4a6d-257">SmartScreen 팝업이 표시되면 **자세한 정보**, **실행**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-257">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="d4a6d-258">다른 클라이언트 컴퓨터에 설치하기 위해 패키지를 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-258">You can also save the package to install on other client computers.</span></span>

### <span data-ttu-id="d4a6d-259"><a name="installclientcert"></a>2부: 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="d4a6d-259"><a name="installclientcert"></a>Part 2: Install the client certificate</span></span>

<span data-ttu-id="d4a6d-260">클라이언트 인증서를 생성하는 데 사용한 것 외의 클라이언트 컴퓨터에서 P2S 연결을 만들려는 경우 클라이언트 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-260">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="d4a6d-261">클라이언트 인증서를 설치하는 경우 클라이언트 인증서를 내보낼 때 만든 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-261">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span> <span data-ttu-id="d4a6d-262">일반적으로 이 인증서를 두 번 클릭하고 설치하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-262">Typically, this is just a matter of double-clicking the certificate and installing it.</span></span> <span data-ttu-id="d4a6d-263">자세한 내용은 [내보낸 클라이언트 인증서 설치](vpn-gateway-certificates-point-to-site.md#install)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-263">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span>

## <span data-ttu-id="d4a6d-264"><a name="connect"></a>5. Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="d4a6d-264"><a name="connect"></a>5. Connect to Azure</span></span>

### <a name="connect-to-your-vnet"></a><span data-ttu-id="d4a6d-265">VNet에 연결</span><span class="sxs-lookup"><span data-stu-id="d4a6d-265">Connect to your VNet</span></span>

1. <span data-ttu-id="d4a6d-266">VNet에 연결하려면 클라이언트 컴퓨터에서 VPN 연결로 이동하고 만든 VPN 연결을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-266">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="d4a6d-267">가상 네트워크와 같은 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-267">It is named the same name as your virtual network.</span></span> <span data-ttu-id="d4a6d-268">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-268">Click **Connect**.</span></span> <span data-ttu-id="d4a6d-269">인증서 사용을 안내하는 팝업 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-269">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="d4a6d-270">이 경우 **계속** 을 클릭하여 상승된 권한을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-270">If this happens, click **Continue** to use elevated privileges.</span></span>
2. <span data-ttu-id="d4a6d-271">**연결** 상태 페이지에서 **연결**을 클릭하여 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-271">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="d4a6d-272">**인증서 선택** 화면에서 표시되는 클라이언트 인증서가 연결하는 데 사용할 인증서인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-272">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="d4a6d-273">그렇지 않은 경우 드롭다운 화살표를 사용하여 올바른 인증서를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-273">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>

  ![VPN 클라이언트 연결](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. <span data-ttu-id="d4a6d-275">연결이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-275">Your connection is established.</span></span>

  ![설정된 연결](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="d4a6d-277">P2S 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d4a6d-277">Troubleshooting P2S connections</span></span>

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <span data-ttu-id="d4a6d-278"><a name="verifyvpnconnect"></a>VPN 연결 확인</span><span class="sxs-lookup"><span data-stu-id="d4a6d-278"><a name="verifyvpnconnect"></a>Verify the VPN connection</span></span>

1. <span data-ttu-id="d4a6d-279">VPN 연결이 활성인지를 확인하려면, 관리자 권한 명령 프롬프트를 열고 *ipconfig/all*을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-279">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="d4a6d-280">결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-280">View the results.</span></span> <span data-ttu-id="d4a6d-281">받은 IP 주소가 VNet을 만들 때 지정한 지점 및 사이트 간 연결 주소 범위 내의 주소 중 하나인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-281">Notice that the IP address you received is one of the addresses within the Point-to-Site connectivity address range that you specified when you created your VNet.</span></span> <span data-ttu-id="d4a6d-282">결과는 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-282">The results should be similar to this example:</span></span>

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="d4a6d-283"><a name="connectVM"></a>가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="d4a6d-283"><a name="connectVM"></a>Connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <span data-ttu-id="d4a6d-284"><a name="add"></a>신뢰할 수 있는 루트 인증서 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="d4a6d-284"><a name="add"></a>Add or remove trusted root certificates</span></span>

<span data-ttu-id="d4a6d-285">Azure에서 신뢰할 수 있는 루트 인증서를 추가 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-285">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="d4a6d-286">루트 인증서를 제거하면 해당 루트에서 생성된 인증서가 있는 클라이언트를 인증하지 못하게 됩니다. 따라서 연결할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-286">When you remove a root certificate, clients that have a certificate generated from that root won't be able to authenticate, and thus will not be able to connect.</span></span> <span data-ttu-id="d4a6d-287">클라이언트를 인증하고 연결하려는 경우 Azure에 (업로드된)신뢰할 수 있는 루트 인증서에서 생성된 새 클라이언트 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-287">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span></span>

### <span data-ttu-id="d4a6d-288"><a name="addtrustedroot"></a>신뢰할 수 있는 루트 인증서를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="d4a6d-288"><a name="addtrustedroot"></a>To add a trusted root certificate</span></span>

<span data-ttu-id="d4a6d-289">Azure에 최대 20개의 신뢰할 수 있는 루트 인증서 .cer 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-289">You can add up to 20 trusted root certificate .cer files to Azure.</span></span> <span data-ttu-id="d4a6d-290">지침은 [섹션 3 - 루트 인증서 .cer 파일 업로드](#upload)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-290">For instructions, see [Section 3 - Upload the root certificate .cer file](#upload).</span></span>

### <span data-ttu-id="d4a6d-291"><a name="removetrustedroot"></a>신뢰할 수 있는 루트 인증서를 제거하려면</span><span class="sxs-lookup"><span data-stu-id="d4a6d-291"><a name="removetrustedroot"></a>To remove a trusted root certificate</span></span>

1. <span data-ttu-id="d4a6d-292">VNet에 대한 페이지의 **VPN 연결** 섹션에서 **클라이언트** 그래픽을 클릭하여 **지점 및 사이트 간 VPN 연결** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-292">On the **VPN connections** section of the page for your VNet, click the **clients** graphic to open the **Point-to-site VPN connection** page.</span></span>

  ![클라이언트](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. <span data-ttu-id="d4a6d-294">**지점 및 사이트 간 연결** 페이지에서 **인증서 관리**를 클릭하여 **인증서** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-294">On the **Point-to-site connection** page, click **Manage certificates** to open the **Certificates** page.</span></span><br>

  ![인증서 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. <span data-ttu-id="d4a6d-296">**인증서** 페이지에서 제거할 인증서 옆에 있는 줄임표를 클릭한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-296">On the **Certificates** page, click the ellipsis next to the certificate that you want to remove, then click **Delete**.</span></span>

  ![루트 인증서 삭제](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <span data-ttu-id="d4a6d-298"><a name="revokeclient"></a>클라이언트 인증서 해지</span><span class="sxs-lookup"><span data-stu-id="d4a6d-298"><a name="revokeclient"></a>Revoke a client certificate</span></span>

<span data-ttu-id="d4a6d-299">클라이언트 인증서를 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-299">You can revoke client certificates.</span></span> <span data-ttu-id="d4a6d-300">인증서 해지 목록에서 개별 클라이언트 인증서를 기반으로 하는 지점 및 사이트 간 연결을 선택적으로 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-300">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="d4a6d-301">이것은 신뢰할 수 있는 루트 인증서를 제거하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-301">This differs from removing a trusted root certificate.</span></span> <span data-ttu-id="d4a6d-302">Azure에서 신뢰할 수 있는 루트 인증서 .cer를 제거하면, 해지된 루트 인증서로 생성/서명된 모든 클라이언트 인증서에 대한 액세스 권한도 해지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-302">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="d4a6d-303">루트 인증서가 아닌 클라이언트 인증서를 해지해야 루트 인증서로부터 생성된 다른 인증서를 지점 및 사이트 간 연결을 위한 인증에 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-303">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication for the Point-to-Site connection.</span></span>

<span data-ttu-id="d4a6d-304">해지된 클라이언트 인증서를 사용하는 동안 개별 사용자의 세분화된 액세스 제어를 위해 일반적으로 루트 인증서를 사용하여 팀 또는 조직 수준에서 액세스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-304">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="d4a6d-305"><a name="revokeclientcert"></a>클라이언트 인증서를 해지하려면</span><span class="sxs-lookup"><span data-stu-id="d4a6d-305"><a name="revokeclientcert"></a>To revoke a client certificate</span></span>

<span data-ttu-id="d4a6d-306">해지 목록에 지문을 추가하여 클라이언트 인증서를 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-306">You can revoke a client certificate by adding the thumbprint to the revocation list.</span></span>

1. <span data-ttu-id="d4a6d-307">클라이언트 인증서 지문을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-307">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="d4a6d-308">자세한 내용은 [방법: 인증서의 지문 검색](https://msdn.microsoft.com/library/ms734695.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-308">For more information, see [How to: Retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="d4a6d-309">텍스트 편집기에 정보를 복사하고 연속 문자열이 되도록 공백을 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-309">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span>
3. <span data-ttu-id="d4a6d-310">**[클래식 가상 네트워크 이름] > [지점 및 사이트 간 VPN 연결] > [인증서]** 페이지로 이동한 다음 **해지 목록**을 클릭하여 해지 목록 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-310">Navigate to the **'classic virtual network name' > Point-to-site VPN connection > Certificates** page and then click **Revocation list** to open the Revocation list page.</span></span> 
4. <span data-ttu-id="d4a6d-311">**해지 목록** 페이지에서 **+인증서 추가**를 클릭하여 **해지 목록에 인증서 추가** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-311">On the **Revocation list** page, click **+Add certificate** to open the **Add certificate to revocation list** page.</span></span>
5. <span data-ttu-id="d4a6d-312">**해지 목록에 인증서 추가** 페이지에서 인증서 지문을 공백 없이 연속적인 텍스트 줄로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-312">On the **Add certificate to revocation list** page, paste the certificate thumbprint as one continuous line of text, with no spaces.</span></span> <span data-ttu-id="d4a6d-313">페이지 아래쪽에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-313">Click **OK** at the bottom of the page.</span></span>
6. <span data-ttu-id="d4a6d-314">업데이트가 완료된 후에는 인증서를 더 이상 연결에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-314">After updating has completed, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="d4a6d-315">이 인증서를 사용하여 연결하려는 클라이언트에서 인증서가 더 이상 유효하지 않다고 하는 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-315">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

## <span data-ttu-id="d4a6d-316"><a name="faq"></a>지점 및 사이트 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="d4a6d-316"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d4a6d-317">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4a6d-317">Next steps</span></span>
<span data-ttu-id="d4a6d-318">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-318">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="d4a6d-319">자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-319">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="d4a6d-320">네트워킹 및 가상 컴퓨터에 대한 자세한 내용은 [Azure 및 Linux VM 네트워크 개요](../virtual-machines/linux/azure-vm-network-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4a6d-320">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>