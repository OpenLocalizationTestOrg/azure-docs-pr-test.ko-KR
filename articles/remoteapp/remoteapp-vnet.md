---
title: "Azure RemoteApp과 함께 사용하기 위해 Azure VNET의 유효성 검사 | Microsoft Docs"
description: "Azure VNET이 Azure RemoteApp과 함께 사용할 준비가 되었는지 확인하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a><span data-ttu-id="3adfb-103">Azure RemoteApp과 함께 사용하기 위해 Azure VNET의 유효성을 검사</span><span class="sxs-lookup"><span data-stu-id="3adfb-103">Validate the Azure VNET to use with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3adfb-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3adfb-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3adfb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3adfb-106">Azure RemoteApp과 함께 Azure VNET을 사용하기 전에 VNET의 유효성을 검사하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span></span> <span data-ttu-id="3adfb-107">이렇게 하면 연결 문제를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="3adfb-108">Azure VNET의 유효성을 검사하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-108">To validate your Azure VNET, do the following:</span></span>

1. <span data-ttu-id="3adfb-109">Azure RemoteApp과 함께 사용하려는 Azure VNET의 서브넷 내에 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span></span>
2. <span data-ttu-id="3adfb-110">관리 포털의 **연결** 옵션을 사용하여 이 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-110">Connect to that VM by using the **Connect** option in the management portal.</span></span>
3. <span data-ttu-id="3adfb-111">가상 컴퓨터를 Azure RemoteApp과 함께 사용하려는 동일 도메인에 가입시켜 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span></span> <span data-ttu-id="3adfb-112">온-프레미스 네트워크에 연결하는 하이브리드 연결을 만드는 경우 가상 컴퓨터를 사용자의 로컬 도메인에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span></span>

<span data-ttu-id="3adfb-113">성공할 경우 Azure VNET은 RemoteApp과 함께 사용할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3adfb-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span></span>

<span data-ttu-id="3adfb-114">종단간 하이브리드 컬렉션 워크플로에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3adfb-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span></span>

* [<span data-ttu-id="3adfb-115">Azure RemoteApp에 대한 가상 네트워크를 계획하는 방법</span><span class="sxs-lookup"><span data-stu-id="3adfb-115">How to plan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="3adfb-116">하이브리드 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="3adfb-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="3adfb-117">Azure RemoteApp 컬렉션을 Azure 가상 네트워크에 배포(ExpressRoute 지원 포함)</span><span class="sxs-lookup"><span data-stu-id="3adfb-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

