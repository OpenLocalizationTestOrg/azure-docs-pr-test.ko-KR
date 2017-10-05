---
title: "고객 Virtual Network에 배포되는 Azure RemoteApp용 허용 목록에 대한 포트 및 URL 목록 | Microsoft Docs"
description: "Azure RemoteApp을 통해 통신하기 위해 구성해야 하는 포트 및 URL을 알아봅니다."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="698ab-103">고객 가상 네트워크에 배포된 Azure RemoteApp에 대한 액세스를 허용하는 포트 및 URL 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="698ab-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="698ab-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="698ab-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="698ab-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="698ab-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="698ab-106">Azure RemoteApp 클라우드나 하이브리드 컬렉션을 VNET(Virtual Network)에 배포하는 경우 다음의 포트 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="698ab-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="698ab-107">Virtual Network에 대한 자세한 내용은 [Virtual Network 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="698ab-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="698ab-108">컬렉션에 트래픽을 Virtual Network 리소스로 제한하는 NSG(네트워크 보안 그룹)를 만든 경우 다음 포트에 액세스할 수 있는지와 Virtual Network의 보안 정책을 통해 허용되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="698ab-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="698ab-109">네트워크 보안 그룹에 대한 자세한 내용은 다음을 참조하세요. [네트워크 보안 그룹이란? (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="698ab-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="698ab-110">Azure RemoteApp 서브넷에 다음 끝점 및 URL에 대한 액세스 권한 필요:</span><span class="sxs-lookup"><span data-stu-id="698ab-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="698ab-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="698ab-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="698ab-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="698ab-112">*.servicebus.net</span></span>
* <span data-ttu-id="698ab-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="698ab-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="698ab-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="698ab-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="698ab-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="698ab-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="698ab-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="698ab-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="698ab-117">아웃바운드: TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="698ab-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="698ab-118">선택 사항 - UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="698ab-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="698ab-119">Azure RemoteApp 클라이언트에 다음 끝점 및 URL에 대한 액세스 권한 필요:</span><span class="sxs-lookup"><span data-stu-id="698ab-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="698ab-120">데스크톱, 장치 등의 클라이언트로 Azure RemoteApp 컬렉션에서 배포된 앱에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="698ab-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="698ab-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="698ab-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="698ab-122">https://*.remoteapp.windowsazure.com(선택적 UDP 포트는 이 주소를 위한 것임)</span><span class="sxs-lookup"><span data-stu-id="698ab-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="698ab-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="698ab-123">https://login.windows.net</span></span>  
* <span data-ttu-id="698ab-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="698ab-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="698ab-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="698ab-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="698ab-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="698ab-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="698ab-127">아웃바운드: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="698ab-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="698ab-128">선택 사항 - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="698ab-128">Optional - UDP: 3391</span></span> 

