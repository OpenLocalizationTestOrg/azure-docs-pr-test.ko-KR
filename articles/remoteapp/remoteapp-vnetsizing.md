---
title: "Azure RemoteApp에서 VNET에 대 한 aaaSizing 정보 | Microsoft Docs"
description: "Azure RemoteApp VNET으로 실행에 대 한 IP 주소 요구 사항은 hello에 대 한 자세한 내용은"
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
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="cdf83-103">Azure RemoteApp의 VNET에 대한 크기 정보</span><span class="sxs-lookup"><span data-stu-id="cdf83-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cdf83-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cdf83-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cdf83-106">Azure RemoteApp 가상 네트워크 (VNET)와 함께 사용 하면 RemoteApp hello 서브넷 내의 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="cdf83-107">RemoteApp 서비스의 hello 배율에 따라, 사용자의 서브넷에 RemoteApp 가상 컴퓨터에 사용할 수 있는 IP 주소가 충분 한지 tooensure를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="cdf83-108">이 크기 조정 지침은 컬렉션 내에서 RemoteApp이 가상 컴퓨터를 위 또는 아래로 동적으로 회전하는 방법을 완벽하게 나타내지는 않지만, 서브넷 범위를 예측하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="cdf83-109">RemoteApp 제거 하지 않고 hello 서브넷 크기를 늘릴 수 없으면 RemoteApp 서비스를 VNET에 배치 되 면 때 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="cdf83-110">최대 용량에서 toorun 되도록 각 RemoteApp 컬렉션에 대해 사용할 수 있는 100 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="cdf83-111">예를 들어 hello 표준 계획의 RemoteApp 컬렉션을 하나 있고 toohave hello 최대 500 명의 사용자를 원하는 경우 해당 컬렉션에 대해 100 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="cdf83-112">마찬가지로, 사용자가 800 명 hello 기본 계획의 RemoteApp 컬렉션에 대 한 IP 주소를 100 필요.</span><span class="sxs-lookup"><span data-stu-id="cdf83-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="cdf83-113">(최대 hello 보다 작음) 사용자 수가 적은 toohave 하려는 경우 각 컬렉션 필요한 hello IP 주소를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf83-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="cdf83-114">hello 최소 서브넷 크기 요구 사항이 30 IP 주소 (/ 27).</span><span class="sxs-lookup"><span data-stu-id="cdf83-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="cdf83-115">VNET 구성 되어 있는지 정보 toomake 하 고 적절히 작동 하는 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="cdf83-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="cdf83-116">개인 VNET tooan Azure VNET에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cdf83-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="cdf83-117">Azure RemoteApp과 함께 hello Azure VNET toouse 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="cdf83-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

