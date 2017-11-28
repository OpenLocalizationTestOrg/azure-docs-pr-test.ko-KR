---
title: "Azure RemoteApp에서 Outlook 사용 | Microsoft Docs"
description: "Azure RemoteApp에서 Outlook을 구성 및 사용하는 방법 알아보기 | Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3feb21385a8b7fa219153c16181887e34d6ea41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a><span data-ttu-id="cf031-103">Azure RemoteApp에서 Microsoft Outlook 사용</span><span class="sxs-lookup"><span data-stu-id="cf031-103">Using Microsoft Outlook in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cf031-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cf031-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="cf031-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cf031-106">Azure RemoteApp은 Microsoft Outlook O365를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-106">Azure RemoteApp supports Microsoft Outlook O365.</span></span> <span data-ttu-id="cf031-107">[Azure RemoteApp에서 Office가 작동하는 방식](remoteapp-officesubscription.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cf031-107">Read more about how [Office works in Azure RemoteApp](remoteapp-officesubscription.md).</span></span> <span data-ttu-id="cf031-108">Azure RemoteApp에서 사용하는 경우 Outlook에 대한 몇 가지 권장되는 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-108">There are a few recommended settings for Outlook when used in Azure RemoteApp.</span></span>

## <a name="cached-mode"></a><span data-ttu-id="cf031-109">캐시 모드</span><span class="sxs-lookup"><span data-stu-id="cf031-109">Cached mode</span></span>
<span data-ttu-id="cf031-110">캐시 모드는 Azure RemoteApp에서 Outlook을 사용할 때 권장되는 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-110">Cached mode is a recommended configuration when using Outlook in Azure RemoteApp.</span></span> <span data-ttu-id="cf031-111">캐시된 Exchange 모드를 사용하도록 Outlook 2013 계정을 구성하는 경우 Outlook 2013은 OAB(오프라인 주소록)와 함께 사용자 컴퓨터의 오프라인 데이터 파일(OST 파일)에 저장된 사용자의 Microsoft Exchange 사서함 로컬 복사본에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-111">When you configure an Outlook 2013 account to use Cached Exchange Mode, Outlook 2013 works from a local copy of the user's Microsoft Exchange mailbox that is stored in an offline data file (OST file) on the user's computer, together with the Offline Address Book (OAB).</span></span> <span data-ttu-id="cf031-112">캐시된 사서함 및 OAB는 O365 서비스에서 주기적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-112">The cached mailbox and OAB are updated periodically from the O365 service.</span></span> <span data-ttu-id="cf031-113">[캐시 및 온라인 모드의 차이점](https://technet.microsoft.com/library/jj683103.aspx)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cf031-113">Read more about [the differences between cached and online mode](https://technet.microsoft.com/library/jj683103.aspx).</span></span>

<span data-ttu-id="cf031-114">사용자는 계정 설정 중 또는 계정 설정을 변경하여 **캐시된 Exchange 모드** 또는 **온라인 모드**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-114">The user can select **Cached Exchange Mode** or **Online Mode** during account setup or by changing the account settings.</span></span> <span data-ttu-id="cf031-115">또한 Office 사용자 지정 도구(OCT) 또는 그룹 정책을 사용하여 둘 중 하나의 모드를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-115">You can also deploy one mode or the other by using the Office Customization Tool (OCT) or Group Policy.</span></span>  

<span data-ttu-id="cf031-116">[캐시 모드를 활성화하는 단계별 지침](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="cf031-116">Read [step by step instructions on enabling cached mode](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).</span></span>

## <a name="search"></a><span data-ttu-id="cf031-117">검색</span><span class="sxs-lookup"><span data-stu-id="cf031-117">Search</span></span>
<span data-ttu-id="cf031-118">Azure RemoteApp에서 Outlook 내의 검색을 사용하는 데는 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-118">In Azure RemoteApp, using search within Outlook has limitations.</span></span> <span data-ttu-id="cf031-119">Azure RemoteApp은 사용자 세션을 수용하기 위해 풀링된 VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-119">Azure RemoteApp uses pooled VMs to accommodate user sessions.</span></span> <span data-ttu-id="cf031-120">검색 인덱싱은 VM마다 다른 컴퓨터 ID에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-120">Search indexing depends on the machine ID, which is different for different VMs.</span></span> <span data-ttu-id="cf031-121">사용자가 Azure RemoteApp에 로그인할 때마다 새 VM에 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-121">It is possible that every time a user logs into Azure RemoteApp, they are directed to a new VM.</span></span> <span data-ttu-id="cf031-122">따라서 로컬 검색을 사용하는 경우 컴퓨터 ID가 변경될 때마다 인덱서가 실행됩니다(사용자가 다른 VM에 있는 경우).</span><span class="sxs-lookup"><span data-stu-id="cf031-122">That would mean, if we enable local search, the indexer will run every time the machine ID changes (when the user is on a different VM).</span></span> <span data-ttu-id="cf031-123">.OST 파일의 크기에 따라 인덱서를 완료하는 데 시간이 오래 걸릴 수 있으며 다른 앱에 필요한 리소스까지도 소진할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-123">Depending on the size of the .OST file, the indexer could take a long time to complete and use up resources needed for other apps.</span></span> <span data-ttu-id="cf031-124">검색 속도도 느리고 결과가 생성되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-124">Search would not only be slow but might not produce results.</span></span> <span data-ttu-id="cf031-125">온라인 모드 계정 프로필을 사용하면 이 문제를 해결할 수 있지만 전반적인 성능이 로컬 캐시의 부족으로 인해 저하될 수 있습니다(캐시된 모드와 온라인 모드 간의 차이점에 대한 자세한 내용은 위의 링크 참조).</span><span class="sxs-lookup"><span data-stu-id="cf031-125">Using an Online Mode account profile would work around this, but overall performance would suffer due to the lack of a local cache (see the link above for more information about the difference between cached and online mode).</span></span> <span data-ttu-id="cf031-126">아쉽게도 Outlook 2013에서는 기본적으로 인덱싱된/로컬 검색을 비활성화할 수 없으며 온라인 검색을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf031-126">Unfortunately, indexed/local search cannot be disabled and online search cannot be enabled by default in Outlook 2013.</span></span>

