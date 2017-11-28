---
title: "고객 가상 네트워크에 Azure RemoteApp 배포에 대 한 Url과 포트 toowhitelist aaaList | Microsoft Docs"
description: "포트 및 tooconfigure Azure RemoteApp을 통한 통신에 필요한 Url에 알아봅니다."
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
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="cb756-103">고객 가상 네트워크에에서 Azure RemoteApp 배포에 대 한 Url과 포트 toopermit 액세스 목록</span><span class="sxs-lookup"><span data-stu-id="cb756-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cb756-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb756-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cb756-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb756-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cb756-106">가상 네트워크 (VNET)는 Azure RemoteApp 클라우드 또는 하이브리드 컬렉션을 배포 하는 경우 hello 다음 포트 정보를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb756-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="cb756-107">Virtual Network에 대한 자세한 내용은 [Virtual Network 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb756-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="cb756-108">트래픽 toohello 가상 네트워크 리소스 컬렉션에 대 한 제한 된 네트워크 보안 그룹 NSG ()를 만든 경우 다음 포트 hello 액세스 가능 하 고 hello 가상 네트워크에 hello 보안 정책을 통해 허용 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb756-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="cb756-109">네트워크 보안 그룹에 대한 자세한 내용은 다음을 참조하세요. [네트워크 보안 그룹이란? (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="cb756-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="cb756-110">Azure RemoteApp 서브넷 액세스 toothese 끝점 및 Url이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb756-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="cb756-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="cb756-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="cb756-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="cb756-112">*.servicebus.net</span></span>
* <span data-ttu-id="cb756-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="cb756-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="cb756-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="cb756-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="cb756-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="cb756-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="cb756-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="cb756-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="cb756-117">아웃바운드: TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="cb756-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="cb756-118">선택 사항 - UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="cb756-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="cb756-119">Azure RemoteApp 클라이언트 toothese 끝점 및 Url에 액세스할 필요:</span><span class="sxs-lookup"><span data-stu-id="cb756-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="cb756-120">다시 말해 주는 _ 개발자 데스크톱 장치 등 hello 클라이언트에서 사용 하 여 tooconnect toohello 앱 배포 hello에 Azure RemoteApp 컬렉션.</span><span class="sxs-lookup"><span data-stu-id="cb756-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="cb756-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="cb756-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="cb756-122">https://*.remoteapp.windowsazure.com (이 주소는 hello 선택적 UDP 포트)</span><span class="sxs-lookup"><span data-stu-id="cb756-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="cb756-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="cb756-123">https://login.windows.net</span></span>  
* <span data-ttu-id="cb756-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="cb756-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="cb756-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="cb756-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="cb756-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="cb756-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="cb756-127">아웃바운드: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="cb756-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="cb756-128">선택 사항 - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="cb756-128">Optional - UDP: 3391</span></span> 

