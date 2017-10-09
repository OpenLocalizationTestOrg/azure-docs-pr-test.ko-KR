---
title: "aaaCreate 네트워크 보안 그룹-Azure 포털 | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate hello Azure 포털을 사용 하 여 네트워크 보안 그룹을 배포 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="ff645-103">네트워크 보안 그룹 hello Azure 포털을 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="ff645-103">Create network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ff645-104">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="ff645-105">수도 있습니다 [hello 클래식 배포 모델에서 Nsg를 만들](virtual-networks-create-nsg-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="ff645-106">위의 hello 시나리오를 기반으로 hello 예제 PowerShell 명령 아래에 이미 만든 단순한 환경 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="ff645-107">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 배포 하 여 [이 서식 파일](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), 클릭 **tooAzure 배포**, 대체 hello 기본 매개 변수 값 필요한 경우, 및의 지침에 따라 hello hello 포털 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ff645-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="ff645-108">hello 단계를 사용 하 여 아래 **RG NSG** hello 리소스 그룹 hello 템플릿의 이름을 hello에 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="ff645-109">Hello NSG 프런트 엔드 NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="ff645-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="ff645-110">toocreate hello **NSG 프런트 엔드** NSG 위의 hello 시나리오와 같이 hello 아래의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="ff645-111">브라우저에서 toohttp://portal.azure.com를 탐색 하 고, 필요한 경우 Azure 계정을 사용해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="ff645-112">**찾아보기>** > **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="ff645-114">Hello에 **네트워크 보안 그룹** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="ff645-116">Hello에 **네트워크 보안 그룹 만들기** 블레이드에서 라는 NSG 만들기 *NSG 프런트 엔드* hello에 *RG NSG* 리소스 그룹을 클릭 한 다음 **만들기**.</span><span class="sxs-lookup"><span data-stu-id="ff645-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="ff645-118">기존 NSG에서 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="ff645-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="ff645-119">hello Azure 포털에서에서 기존 NSG에서 규칙 toocreate 아래 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="ff645-120">**찾아보기 >** > **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="ff645-121">Nsg의 hello 목록에서 클릭 **NSG 프런트 엔드** > **인바운드 보안 규칙**</span><span class="sxs-lookup"><span data-stu-id="ff645-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure Portal - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="ff645-123">Hello 목록이 **인바운드 보안 규칙**, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure Portal - 규칙 추가](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="ff645-125">Hello에 **인바운드 보안 규칙 추가** 블레이드에서 라는 규칙을 만들 *웹 규칙* 의 우선 순위를 가진 *200* 를 통해 액세스할 수 있도록 *TCP* tooport *80* tooany VM에서 소스를 선택한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="ff645-126">이러한 설정 중 대부분은 이미 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure Portal - 규칙 설정](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="ff645-128">몇 초 후 hello hello NSG에에서 새 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Azure Portal - 새 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="ff645-130">단계를 반복 too6 toocreate 라는 인바운드 규칙 *rdp 규칙* 의 우선 순위를 가진 *250* 를 통해 액세스할 수 있도록 *TCP* tooport *3389* 모든 소스에서 VM tooany 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="ff645-131">Hello NSG toohello 프런트 엔드 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="ff645-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="ff645-132">**찾아보기 >** > **리소스 그룹** > **RG-NSG**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="ff645-133">Hello에 **RG NSG** 블레이드에서 클릭 **중...**   >  **TestVNet**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure Portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="ff645-135">Hello에 **설정** 블레이드에서 클릭 **서브넷** > **프런트 엔드** > **네트워크 보안 그룹**  >  **NSG 프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure Portal - 서브넷 설정](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="ff645-137">Hello에 **프런트 엔드** 블레이드에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure Portal - 서브넷 설정](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="ff645-139">Hello NSG 백 엔드 NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="ff645-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="ff645-140">toocreate hello **NSG 백 엔드** NSG 연결 toohello **백 엔드** 서브넷, 아래 hello 단계 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="ff645-141">단계를 반복 hello [만들기 hello NSG 프런트 엔드 NSG](#Create-the-NSG-FrontEnd-NSG) toocreate 라는 NSG *NSG 백 엔드*</span><span class="sxs-lookup"><span data-stu-id="ff645-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="ff645-142">단계를 반복 hello [기존 NSG에서 규칙을 만들](#Create-rules-in-an-existing-NSG) toocreate hello **인바운드** hello 테이블 아래에 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="ff645-143">인바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="ff645-143">Inbound rule</span></span> | <span data-ttu-id="ff645-144">아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="ff645-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure Portal - 인바운드 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure Portal - 아웃바운드 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="ff645-147">단계를 반복 hello [hello NSG toohello 프런트 엔드 서브넷 연결](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG 백 엔드** NSG toohello **백 엔드** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="ff645-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff645-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff645-148">Next Steps</span></span>
* <span data-ttu-id="ff645-149">너무 방법에 대해 알아봅니다[기존 Nsg를 관리 합니다.](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ff645-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="ff645-150">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="ff645-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

