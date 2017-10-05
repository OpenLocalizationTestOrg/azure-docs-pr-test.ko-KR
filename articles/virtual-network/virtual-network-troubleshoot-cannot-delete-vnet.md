---
title: "Azure에서 가상 네트워크를 삭제할 수 없음 | Microsoft Docs"
description: "Azure에서 가상 네트워크를 삭제할 수 없는 문제를 해결하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="f7dfa-103">문제 해결: Azure에서 가상 네트워크를 삭제하지 못함</span><span class="sxs-lookup"><span data-stu-id="f7dfa-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="f7dfa-104">Microsoft Azure에서 가상 네트워크를 삭제하려고 할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="f7dfa-105">이 문서에서는 이 문제를 해결하는 데 도움이 되는 문제 해결 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="f7dfa-106">문제 해결 지침</span><span class="sxs-lookup"><span data-stu-id="f7dfa-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="f7dfa-107">[가상 네트워크에서 가상 네트워크 게이트웨이가 실행 중인지 확인](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="f7dfa-108">[가상 네트워크에서 응용 프로그램 게이트웨이가 실행 중인지 확인](#check-whether-an-application-gateway-is-running-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="f7dfa-109">[가상 네트워크에서 Azure Active Directory Domain Service가 사용하도록 설정되어 있는지 확인](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="f7dfa-110">[가상 네트워크가 다른 리소스에 연결되어 있는지 확인](#check-whether-the-virtual-network-is-connected-to-other-resource)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="f7dfa-111">[가상 네트워크에서 가상 컴퓨터가 여전히 실행 중인지 확인](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="f7dfa-112">[가상 네트워크가 마이그레이션 도중에 걸려 있는지 확인](#check-whether-the-virtual-network-is-stuck-in-migration)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="f7dfa-113">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="f7dfa-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="f7dfa-114">가상 네트워크에서 가상 네트워크 게이트웨이가 실행 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="f7dfa-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="f7dfa-115">가상 네트워크를 제거하려면 먼저 가상 네트워크 게이트웨이를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="f7dfa-116">클래식 가상 네트워크의 경우 Azure Portal에서 클래식 가상 네트워크에 대한 **개요** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="f7dfa-117">가상 네트워크에서 게이트웨이가 실행 중인 경우에는 **VPN 연결** 섹션에 게이트웨이의 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![게이트웨이가 실행 중인지 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="f7dfa-119">가상 네트워크의 경우 가상 네트워크에 대한 **개요** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="f7dfa-120">가상 네트워크 게이트웨이에 대한 **연결된 장치**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-120">Check **Connected devices** for the virtual network gateway.</span></span>

![연결된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="f7dfa-122">게이트웨이를 제거하려면 먼저 게이트웨이에서 **연결** 개체를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="f7dfa-123">가상 네트워크에서 응용 프로그램 게이트웨이가 실행 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="f7dfa-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="f7dfa-124">가상 네트워크에 대한 **개요** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="f7dfa-125">응용 프로그램 게이트웨이에 대한 **연결된 장치**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-125">Check the **Connected devices** for the application gateway.</span></span>

![연결된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="f7dfa-127">응용 프로그램 게이트웨이가 있는 경우 이를 제거해야 가상 네트워크를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="f7dfa-128">가상 네트워크에서 Azure Active Directory Domain Service가 사용하도록 설정되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="f7dfa-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="f7dfa-129">Active Directory Domain Service가 사용하도록 설정되어 있고 가상 네트워크에 연결되어 있다면 이 가상 네트워크를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![연결된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="f7dfa-131">서비스를 사용하지 않도록 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="f7dfa-132">[Azure 클래식 포털](https://manage.windowsazure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f7dfa-133">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="f7dfa-134">Active Directory Domain Service가 사용 설정되어 있는 Azure AD(Azure Active Directory) 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="f7dfa-135">**구성** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="f7dfa-136">**도메인 서비스**에서 **이 디렉터리에 대해 도메인 서비스 사용** 옵션을 **아니요**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="f7dfa-137">가상 네트워크가 다른 리소스에 연결되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="f7dfa-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="f7dfa-138">서킷 링크, 연결 및 가상 네트워크 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="f7dfa-139">이러한 요소가 가상 네트워크를 삭제하지 못하는 원인일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="f7dfa-140">권장되는 삭제 순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="f7dfa-141">게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="f7dfa-141">Gateway connections</span></span>
2. <span data-ttu-id="f7dfa-142">게이트웨이</span><span class="sxs-lookup"><span data-stu-id="f7dfa-142">Gateways</span></span>
3. <span data-ttu-id="f7dfa-143">IP</span><span class="sxs-lookup"><span data-stu-id="f7dfa-143">IPs</span></span>
4. <span data-ttu-id="f7dfa-144">가상 네트워크 피어링</span><span class="sxs-lookup"><span data-stu-id="f7dfa-144">Virtual network peerings</span></span>
5. <span data-ttu-id="f7dfa-145">ASE(App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="f7dfa-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="f7dfa-146">가상 네트워크에서 가상 컴퓨터가 여전히 실행 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="f7dfa-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="f7dfa-147">가상 네트워크에서 실행 중인 가상 컴퓨터가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="f7dfa-148">가상 네트워크가 마이그레이션 도중에 걸려 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="f7dfa-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="f7dfa-149">마이그레이션 상태에 걸려 있는 경우 가상 네트워크를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="f7dfa-150">다음 명령을 실행하여 마이그레이션 중단한 다음 가상 네트워크를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="f7dfa-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7dfa-151">Next steps</span></span>

- [<span data-ttu-id="f7dfa-152">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="f7dfa-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="f7dfa-153">Azure Virtual Network FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="f7dfa-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)