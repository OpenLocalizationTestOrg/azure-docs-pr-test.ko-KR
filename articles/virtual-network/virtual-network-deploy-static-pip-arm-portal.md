---
title: "고정 공용 IP 주소-Azure 포털을 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "고정 공용 IP 주소를 사용 하 여 사용 하 여 VM toocreate Azure 포털 hello 하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="1a263-103">고정 공용 IP 주소로 hello Azure 포털을 사용 하 여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1a263-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a263-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1a263-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="1a263-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a263-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="1a263-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1a263-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="1a263-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="1a263-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="1a263-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="1a263-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="1a263-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1a263-110">이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="1a263-111">고정 공용 IP를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1a263-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="1a263-112">단계를 수행 하는 전체 hello hello Azure 포털의에서 주소는 고정 공용 IP 사용 하 여 VM이 toocreate:</span><span class="sxs-lookup"><span data-stu-id="1a263-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="1a263-113">브라우저에서 탐색 toohello [Azure 포털](https://portal.azure.com) 및 필요에 따라 Azure 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="1a263-114">Hello 포털의 왼쪽 위 모서리 hello 클릭 **새로**>>**계산**>**Windows Server 2012 R2 Datacenter**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="1a263-115">Hello에 **배포 모델 선택** 목록에서 선택 **리소스 관리자** 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="1a263-116">Hello에 **기본 사항** 블레이드에서 아래와 같이 hello VM 정보를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure 포털 - 기본 사항](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="1a263-118">Hello에 **크기를 선택** 블레이드에서 클릭 **표준 A1** 아래와 같이 다음를 클릭 하 고 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure 포털 - 크기 선택](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="1a263-120">Hello에 **설정** 블레이드에서 클릭 **공용 IP 주소**, hello에 다음 **공용 IP 주소 만들기** 블레이드 아래 **할당**, 클릭 **정적** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="1a263-121">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-121">And then click **OK**.</span></span>
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="1a263-123">Hello에 **설정** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="1a263-124">검토 hello **요약** 블레이드에서 아래와 같이 하 고 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="1a263-126">Hello 대시보드에서 새 타일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a263-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="1a263-128">Hello VM을 만든 후 hello **설정을** 블레이드는 아래와 같이 표시 됩니다</span><span class="sxs-lookup"><span data-stu-id="1a263-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure 포털 - 공용 IP 주소 만들기](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

