---
title: "Azure RemoteApp에서 Outlook aaaUsing | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure Outlook을 사용 하 여 Azure RemoteApp에서 | Microsoft Azure"
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
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a><span data-ttu-id="9a2ee-103">Azure RemoteApp에서 Microsoft Outlook 사용</span><span class="sxs-lookup"><span data-stu-id="9a2ee-103">Using Microsoft Outlook in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9a2ee-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9a2ee-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9a2ee-106">Azure RemoteApp은 Microsoft Outlook O365를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-106">Azure RemoteApp supports Microsoft Outlook O365.</span></span> <span data-ttu-id="9a2ee-107">[Azure RemoteApp에서 Office가 작동하는 방식](remoteapp-officesubscription.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-107">Read more about how [Office works in Azure RemoteApp](remoteapp-officesubscription.md).</span></span> <span data-ttu-id="9a2ee-108">Azure RemoteApp에서 사용하는 경우 Outlook에 대한 몇 가지 권장되는 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-108">There are a few recommended settings for Outlook when used in Azure RemoteApp.</span></span>

## <a name="cached-mode"></a><span data-ttu-id="9a2ee-109">캐시 모드</span><span class="sxs-lookup"><span data-stu-id="9a2ee-109">Cached mode</span></span>
<span data-ttu-id="9a2ee-110">캐시 모드는 Azure RemoteApp에서 Outlook을 사용할 때 권장되는 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-110">Cached mode is a recommended configuration when using Outlook in Azure RemoteApp.</span></span> <span data-ttu-id="9a2ee-111">캐시 된 Exchange 모드를 Outlook 2013 hello 오프 라인 주소록 함께 hello 사용자의 컴퓨터에서 오프 라인 데이터 파일 (OST 파일)에 저장 된 hello 사용자의 Microsoft Exchange 사서함의 로컬 복사본에서 작동 하는 Outlook 2013 계정 toouse를 구성 하는 경우 OAB ()입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-111">When you configure an Outlook 2013 account toouse Cached Exchange Mode, Outlook 2013 works from a local copy of hello user's Microsoft Exchange mailbox that is stored in an offline data file (OST file) on hello user's computer, together with hello Offline Address Book (OAB).</span></span> <span data-ttu-id="9a2ee-112">캐시 된 사서함 hello 및 OAB hello O365 서비스에서에서 정기적으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-112">hello cached mailbox and OAB are updated periodically from hello O365 service.</span></span> <span data-ttu-id="9a2ee-113">에 대해 자세히 알아보세요 [캐시 및 온라인 모드 간 차이점 hello](https://technet.microsoft.com/library/jj683103.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-113">Read more about [hello differences between cached and online mode](https://technet.microsoft.com/library/jj683103.aspx).</span></span>

<span data-ttu-id="9a2ee-114">hello 선택할 수 있는 **Exchange 캐시 된 모드** 또는 **온라인 모드** 계정 설정 되어 있거나 hello 계정 설정을 변경 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-114">hello user can select **Cached Exchange Mode** or **Online Mode** during account setup or by changing hello account settings.</span></span> <span data-ttu-id="9a2ee-115">또한 하나의 모드 또는 다른 hello hello Office 사용자 지정 도구 (OCT) 이나 그룹 정책을 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-115">You can also deploy one mode or hello other by using hello Office Customization Tool (OCT) or Group Policy.</span></span>  

<span data-ttu-id="9a2ee-116">[캐시 모드를 활성화하는 단계별 지침](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-116">Read [step by step instructions on enabling cached mode](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).</span></span>

## <a name="search"></a><span data-ttu-id="9a2ee-117">검색</span><span class="sxs-lookup"><span data-stu-id="9a2ee-117">Search</span></span>
<span data-ttu-id="9a2ee-118">Azure RemoteApp에서 Outlook 내의 검색을 사용하는 데는 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-118">In Azure RemoteApp, using search within Outlook has limitations.</span></span> <span data-ttu-id="9a2ee-119">Azure RemoteApp 풀링된 Vm tooaccommodate 사용자 세션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-119">Azure RemoteApp uses pooled VMs tooaccommodate user sessions.</span></span> <span data-ttu-id="9a2ee-120">검색 인덱싱 다른 Vm에 대 한 다른 hello 컴퓨터 ID에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-120">Search indexing depends on hello machine ID, which is different for different VMs.</span></span> <span data-ttu-id="9a2ee-121">사용자가 Azure RemoteApp에는 로그인, 때마다는 방향이 지정 된 tooa 수 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-121">It is possible that every time a user logs into Azure RemoteApp, they are directed tooa new VM.</span></span> <span data-ttu-id="9a2ee-122">메시지의 의미는 로컬 검색을 사용 하도록 설정 하는 경우 hello 인덱서 hello 컴퓨터 ID (hello 사용자가 다른 VM에도) 하는 경우이 변경 될 때마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-122">That would mean, if we enable local search, hello indexer will run every time hello machine ID changes (when hello user is on a different VM).</span></span> <span data-ttu-id="9a2ee-123">Hello의 hello 크기에 따라. OST hello 인덱서 수 오랜 시간이 toocomplete 걸릴 파일과 다른 앱에 필요한 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-123">Depending on hello size of hello .OST file, hello indexer could take a long time toocomplete and use up resources needed for other apps.</span></span> <span data-ttu-id="9a2ee-124">검색 속도도 느리고 결과가 생성되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-124">Search would not only be slow but might not produce results.</span></span> <span data-ttu-id="9a2ee-125">로컬 캐시의 toohello 부족 때문이 전반적인 성능이 저하 될 수 있지만 온라인 모드 계정 프로필을 사용 하 여이 문제를 해결 작동할 것 (캐시 된 및 온라인 모드의 hello 차이점에 대 한 자세한 내용은 위에 링크 hello 참조).</span><span class="sxs-lookup"><span data-stu-id="9a2ee-125">Using an Online Mode account profile would work around this, but overall performance would suffer due toohello lack of a local cache (see hello link above for more information about hello difference between cached and online mode).</span></span> <span data-ttu-id="9a2ee-126">아쉽게도 Outlook 2013에서는 기본적으로 인덱싱된/로컬 검색을 비활성화할 수 없으며 온라인 검색을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2ee-126">Unfortunately, indexed/local search cannot be disabled and online search cannot be enabled by default in Outlook 2013.</span></span>

