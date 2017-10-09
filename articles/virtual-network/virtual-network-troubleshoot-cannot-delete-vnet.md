---
title: "Azure에서 가상 네트워크를 삭제 하는 aaaCannot | Microsoft Docs"
description: "어떻게 tootroubleshoot hello Azure의 가상 네트워크를 삭제할 수는 없습니다 문제에 알아봅니다."
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
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="6074f-103">Azure의 가상 네트워크 toodelete 실패 문제 해결:</span><span class="sxs-lookup"><span data-stu-id="6074f-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="6074f-104">Microsoft Azure에서 가상 네트워크 toodelete 려 할 때 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="6074f-105">이 문서에서는 문제 해결 단계 toohelp이이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="6074f-106">문제 해결 지침</span><span class="sxs-lookup"><span data-stu-id="6074f-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="6074f-107">[가상 네트워크 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="6074f-108">[응용 프로그램 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.](#check-whether-an-application-gateway-is-running-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="6074f-109">[Azure Active Directory 도메인 서비스 hello 가상 네트워크에서 활성화 되어 있는지 여부를 확인](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="6074f-110">[Hello 가상 네트워크에 연결 된 tooother 리소스 인지 확인](#check-whether-the-virtual-network-is-connected-to-other-resource)합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="6074f-111">[Hello 가상 네트워크의 가상 컴퓨터가 여전히 실행 중인지 확인](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="6074f-112">[Hello 가상 네트워크 마이그레이션 걸려 있는지 여부를 확인](#check-whether-the-virtual-network-is-stuck-in-migration)합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="6074f-113">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="6074f-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="6074f-114">가상 네트워크 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6074f-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="6074f-115">tooremove hello 가상 네트워크를 hello 가상 네트워크 게이트웨이 먼저 제거 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="6074f-116">클래식 가상 네트워크에 대 한 이동 toohello **개요** hello Azure 포털의에서 hello 클래식 가상 네트워크의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="6074f-117">Hello에 **VPN 연결** 섹션에서 hello IP 표시는 hello 게이트웨이 hello 가상 네트워크에서 실행 중인 경우 hello 게이트웨이의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![게이트웨이가 실행 중인지 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="6074f-119">가상 네트워크에 대 한 이동 toohello **개요** hello 가상 네트워크의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="6074f-120">확인 **연결 된 장치** hello 가상 네트워크 게이트웨이에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Hello 연결 된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="6074f-122">Hello 게이트웨이 제거 하기 전에 먼저 제거 **연결** hello 게이트웨이의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="6074f-123">응용 프로그램 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6074f-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="6074f-124">Toohello 이동 **개요** hello 가상 네트워크의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="6074f-125">Hello 확인 **연결 된 장치** hello 응용 프로그램 게이트웨이에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Hello 연결 된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="6074f-127">응용 프로그램 게이트웨이 이면 hello 가상 네트워크를 삭제 하려면 먼저 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="6074f-128">Azure Active Directory 도메인 서비스 hello 가상 네트워크에서 설정 되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="6074f-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="6074f-129">Hello Active Directory 도메인 서비스는 활성화 되어 연결 된 toohello 가상 네트워크를이 가상 네트워크를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Hello 연결 된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="6074f-131">toodisable 서비스 hello, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="6074f-132">Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6074f-133">Hello 왼쪽된 창에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="6074f-134">Active Directory 도메인 서비스를 사용할 수 있는 hello Azure Active Directory (Azure AD) 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="6074f-135">선택 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="6074f-136">아래 **도메인 서비스**, hello 변경 **이 디렉터리에 대 한 도메인 서비스 사용** 옵션**아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="6074f-137">Hello 가상 네트워크에 연결 된 tooother 리소스 인지 확인</span><span class="sxs-lookup"><span data-stu-id="6074f-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="6074f-138">서킷 링크, 연결 및 가상 네트워크 피어링이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="6074f-139">이러한 가상 네트워크 삭제 toofail을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="6074f-140">hello 권장된 삭제 순서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="6074f-141">게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="6074f-141">Gateway connections</span></span>
2. <span data-ttu-id="6074f-142">게이트웨이</span><span class="sxs-lookup"><span data-stu-id="6074f-142">Gateways</span></span>
3. <span data-ttu-id="6074f-143">IP</span><span class="sxs-lookup"><span data-stu-id="6074f-143">IPs</span></span>
4. <span data-ttu-id="6074f-144">가상 네트워크 피어링</span><span class="sxs-lookup"><span data-stu-id="6074f-144">Virtual network peerings</span></span>
5. <span data-ttu-id="6074f-145">ASE(App Service Environment)</span><span class="sxs-lookup"><span data-stu-id="6074f-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="6074f-146">Hello 가상 네트워크의 가상 컴퓨터가 여전히 실행 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="6074f-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="6074f-147">어떤 가상 컴퓨터도 hello 가상 네트워크에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="6074f-148">Hello 가상 네트워크 마이그레이션 걸려 있는지 여부를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6074f-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="6074f-149">Hello 가상 네트워크 마이그레이션 상태에 걸려를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="6074f-150">Hello tooabort hello 마이그레이션 명령을 실행 하 고 hello 가상 네트워크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6074f-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="6074f-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6074f-151">Next steps</span></span>

- [<span data-ttu-id="6074f-152">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="6074f-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="6074f-153">Azure Virtual Network FAQ(질문과 대답)</span><span class="sxs-lookup"><span data-stu-id="6074f-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)