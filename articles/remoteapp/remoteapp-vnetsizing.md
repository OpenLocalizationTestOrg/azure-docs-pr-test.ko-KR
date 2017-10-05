---
title: "Azure RemoteApp의 VNET에 대한 크기 정보 | Microsoft Docs"
description: "VNET에서 실행 중인 Azure RemoteApp의 IP 주소 요구 사항에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="60193-103">Azure RemoteApp의 VNET에 대한 크기 정보</span><span class="sxs-lookup"><span data-stu-id="60193-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="60193-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="60193-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="60193-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="60193-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="60193-106">VNET(가상 네트워크)에서 Azure RemoteApp을 사용할 경우 RemoteApp에서는 서브넷 내의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60193-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="60193-107">RemoteApp 서비스의 크기에 따라 서브넷에 RemoteApp 가상 컴퓨터에 사용할 수 있는 IP 주소가 충분한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60193-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="60193-108">이 크기 조정 지침은 컬렉션 내에서 RemoteApp이 가상 컴퓨터를 위 또는 아래로 동적으로 회전하는 방법을 완벽하게 나타내지는 않지만, 서브넷 범위를 예측하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60193-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="60193-109">이는 RemoteApp 서비스가 VNET 내에 배치된 경우 RemoteApp을 제거하지 않고는 서브넷 크기를 늘릴 수 없으므로 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="60193-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="60193-110">최대 용량으로 실행하려는 각 RemoteApp 컬렉션에 대해 100개의 IP 주소를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60193-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="60193-111">예를 들어 표준 요금제에 RemoteApp 컬렉션이 하나 있고 최대 500명의 사용자를 허용하려면 해당 컬렉션에 대해 100개의 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60193-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="60193-112">마찬가지로 800명의 사용자가 있는 기본 요금제의 RemoteApp 컬렉션의 경우에도 100개의 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60193-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="60193-113">최대값보다 적은 수의 사용자를 허용하려는 경우 컬렉션당 필요한 IP 주소 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60193-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="60193-114">최소 서브넷 크기 요구 사항은 30개 IP 주소입니다(/ 27).</span><span class="sxs-lookup"><span data-stu-id="60193-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="60193-115">다음 정보를 확인하여 VNET이 적절히 구성되고 작동하는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="60193-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="60193-116">개인 VNET에서 Azure VNET으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="60193-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="60193-117">Azure RemoteApp과 함께 사용하기 위해 Azure VNET의 유효성을 검사</span><span class="sxs-lookup"><span data-stu-id="60193-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

