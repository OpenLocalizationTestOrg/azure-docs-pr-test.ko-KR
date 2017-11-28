---
title: "aaaHow는 사용자 데이터 및 설정 저장 Azure RemoteApp을 합니까? | Microsoft Docs"
description: "Azure RemoteApp hello 사용자 프로필 디스크를 사용 하 여 사용자 데이터를 저장 하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a><span data-ttu-id="cc7ec-104">Azure RemoteApp이 사용자 데이터와 설정을 저장하는 방법</span><span class="sxs-lookup"><span data-stu-id="cc7ec-104">How does Azure RemoteApp save user data and settings?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cc7ec-105">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cc7ec-106">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="cc7ec-107">Azure RemoteApp은 장치와 세션에서 사용자 ID 및 사용자 지정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-107">Azure RemoteApp saves user identity and customizations across devices and sessions.</span></span> <span data-ttu-id="cc7ec-108">이 사용자 데이터는 사용자 프로필 디스크(UPD)라고 하는 사용자별 컬렉션 디스크에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-108">This user data is stored in a per-user per-collection disk, known as a user profile disk (UPD).</span></span> <span data-ttu-id="cc7ec-109">hello 디스크 hello 사용자 따르며 hello 사용자에 게 로그인 할 위치에 관계 없이 일관 된 환경을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-109">hello disk follows hello user and ensures hello user has a consistent experience, regardless of where they sign in.</span></span>

<span data-ttu-id="cc7ec-110">사용자 프로필 디스크는 완전히 투명 하 게 toohello 사용자-사용자 (로컬 드라이브 toobe 나타나는 항목)에 문서 tootheir 문서 폴더를 저장 하 고 일반적인 방법 대로 해당 응용 프로그램 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-110">User profile disks are completely transparent toohello user — users save documents tootheir Documents folder (on what appears toobe a local drive) and change their app settings as usual.</span></span> <span data-ttu-id="cc7ec-111">At hello 동일 tooAzure RemoteApp 모든 장치에서 연결 하는 경우에 시간, 모든 개인 설정을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-111">At hello same time, all personal settings persist when connecting tooAzure RemoteApp from any device.</span></span> <span data-ttu-id="cc7ec-112">모든 hello 사용자에 게 hello에서 데이터는 같은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-112">All hello user sees is their data in hello same place.</span></span>

<span data-ttu-id="cc7ec-113">각 UPD에는 50GB의 영구 저장소가 있으며 사용자 데이터와 응용 프로그램 설정 모두를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-113">Each UPD has 50GB of persistent storage and contains both user data and application settings.</span></span> 

<span data-ttu-id="cc7ec-114">사용자 프로필 데이터에 대한 구체적인 내용을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-114">Read on for specifics on user profile data.</span></span>

> [!NOTE]
> <span data-ttu-id="cc7ec-115">UPD toodisable hello 필요?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-115">Need toodisable hello UPD?</span></span> <span data-ttu-id="cc7ec-116">이제는 가능합니다. 자세한 내용은 Pavithra의 블로그 게시물인 [Azure RemoteApp에서 UPD(사용자 프로필 디스크) 비활성화](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-116">You can do that now - check out Pavithra's blog post, [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), for details.</span></span>
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a><span data-ttu-id="cc7ec-117">관리자는 toohello 데이터를 어떻게 얻을 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-117">How can an admin get toohello data?</span></span>
<span data-ttu-id="cc7ec-118">(재해 복구 또는 hello 사용자 hello 퇴사 하는 경우)에 사용자가 tooaccess hello 데이터가 필요할 경우 Azure 지원에 문의 하 고 hello 컬렉션과 hello 사용자 id에 대 한 hello 구독 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-118">If you need tooaccess hello data for one of your users (for disaster recovery or if hello user leaves hello company), contact Azure Support and provide hello subscription information for hello collection and hello user identity.</span></span> <span data-ttu-id="cc7ec-119">hello Azure a p p 팀 URL toohello VHD를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-119">hello Azure RemoteApp team will provide you a URL toohello VHD.</span></span> <span data-ttu-id="cc7ec-120">해당 VHD를 다운로드하고 필요한 문서 또는 파일을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-120">Download that VHD and retrieve any documents or files you need.</span></span> <span data-ttu-id="cc7ec-121">비트 toodownload 걸립니다 하므로 해당 hello VHD는 50GB 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-121">Note that hello VHD is 50GB, so it will take a bit toodownload it.</span></span>

## <a name="is-hello-data-backed-up"></a><span data-ttu-id="cc7ec-122">Hello 데이터를 백업?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-122">Is hello data backed up?</span></span>
<span data-ttu-id="cc7ec-123">예, 지리적 위치 당 hello 사용자 데이터의 백업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-123">Yes, we save a backup of hello user data per geographic location.</span></span> <span data-ttu-id="cc7ec-124">hello 데이터는 읽기 전용 이며 수 있습니다 액세스할 hello에 동일한 방식으로 일반 데이터 hello 가능성이 (Azure RemoteApp tooget 문의 것) hello 기본 데이터 센터가 다운 된 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-124">hello data is read-only and can be accessed in hello same way as hello regular data would be (contact Azure RemoteApp tooget it), if hello primary data center is down.</span></span> <span data-ttu-id="cc7ec-125">hello 데이터는 복사 된 실시간 toohello 백업 위치 하 고 서로 다른 버전의 복사본을 유지 하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-125">hello data is copied real-time toohello backup location and we do not keep copies of different versions.</span></span> <span data-ttu-id="cc7ec-126">따라서 데이터 손상 시 म 됩니다 수 toorestore 것 hello 기본 데이터 센터 다운 된 경우 수 tooget 사용자 데이터를 사용할 수 있지만 좋은 버전 이전의 tooa hello 다른 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-126">So, on data corruption, we will not be able toorestore it tooa previously known good version but if hello primary data center is down, you will be able tooget user data from hello other location.</span></span>

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a><span data-ttu-id="cc7ec-127">사용자가 보려면 어떻게 hello UPD hello 서버 쪽에서?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-127">How do users see hello UPD on hello server side?</span></span>
<span data-ttu-id="cc7ec-128">각 사용자는 자신의 디렉터리 tootheir UPD 매핑되는 hello 서버의 해야: c:\Users\username 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-128">Each user will have their own directory on hello server that maps tootheir UPD: c:\Users\username.</span></span>

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a><span data-ttu-id="cc7ec-129">Hello 가장 좋은 방법은 toouse Outlook 및 UPD 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-129">What's hello best way toouse Outlook and UPD?</span></span>
<span data-ttu-id="cc7ec-130">Azure RemoteApp 세션 간에 hello Outlook 상태 (사서함 Pst)을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-130">Azure RemoteApp saves hello Outlook state (mailboxes, PSTs) between sessions.</span></span> <span data-ttu-id="cc7ec-131">tooenable이 PST toobe hello 사용자 프로필 데이터에 저장 된 hello 필요 했습니다 (c:\users\<사용자 이름 >).</span><span class="sxs-lookup"><span data-stu-id="cc7ec-131">tooenable this, we need hello PST toobe stored in hello user profile data (c:\users\<username>).</span></span> <span data-ttu-id="cc7ec-132">따라서 만큼 hello 위치를 변경 하지 않으면 hello 데이터에 대 한 hello 기본 위치를 hello 데이터는 세션 간에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-132">This is hello default location for hello data, so as long as you do not change hello location, hello data will persist between sessions.</span></span>

<span data-ttu-id="cc7ec-133">Outlook에서 "캐시" 모드를 사용하고 검색을 위해 "서버/온라인" 모드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-133">We also recommend that you use "cached" mode in Outlook and use "server/online" mode for searching.</span></span>

<span data-ttu-id="cc7ec-134">Outlook 및 Azure RemoteApp 사용에 대한 자세한 내용은 [이 문서](remoteapp-outlook.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-134">Check out [this article](remoteapp-outlook.md) for more information on using Outlook and Azure RemoteApp.</span></span>

## <a name="what-about-redirection"></a><span data-ttu-id="cc7ec-135">리디렉션은 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-135">What about redirection?</span></span>
<span data-ttu-id="cc7ec-136">Azure RemoteApp toolet 사용자가을 설정 하 여 로컬 장치 액세스를 구성할 수 있습니다 [리디렉션](remoteapp-redirection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-136">You can configure Azure RemoteApp toolet users access local devices by setting up [redirection](remoteapp-redirection.md).</span></span> <span data-ttu-id="cc7ec-137">로컬 장치 수 tooaccess hello 데이터 UPD hello에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-137">Local devices will then be able tooaccess hello data on hello UPD.</span></span>

## <a name="can-i-use-my-upd-as-a-network-share"></a><span data-ttu-id="cc7ec-138">내 UPD를 네트워크 공유로 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-138">Can I use my UPD as a network share?</span></span>
<span data-ttu-id="cc7ec-139">아니요.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-139">No.</span></span> <span data-ttu-id="cc7ec-140">UPD를 네트워크 공유로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-140">UPDs cannot be used as a network share.</span></span> <span data-ttu-id="cc7ec-141">UPD만 사용할 수 있는 toohello 사용자 때 hello 사용자가 적극적으로 tooAzure RemoteApp 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-141">A UPD is only available toohello user when hello user is actively connected tooAzure RemoteApp.</span></span>

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a><span data-ttu-id="cc7ec-142">컬렉션에서 사용자를 삭제하면 해당 UPD가 삭제됩니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-142">If I delete a user from a collection, is their UPD deleted?</span></span>
<span data-ttu-id="cc7ec-143">아니요, 사용자를 삭제 하면 hello UPD 자동으로 삭제 하지 않는 것-hello 컬렉션을 삭제할 때까지 hello 데이터 저장 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-143">No, when you delete a user, we do not automatically delete hello UPD - instead, we store hello data until you delete hello collection.</span></span> <span data-ttu-id="cc7ec-144">hello 컬렉션을 삭제 한 후 90 일 동안 모든 Upd 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-144">90 days after you delete hello collection, we delete all UPDs.</span></span> 

<span data-ttu-id="cc7ec-145">컬렉션에서 UPD toodelete 해야 할 경우 Azure RemoteApp에 문의-UPD 저희 쪽에서 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-145">If you need toodelete a UPD from a collection, contact Azure RemoteApp - we can delete UPD from our side.</span></span>

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a><span data-ttu-id="cc7ec-146">내 사용자의 UPD(현재 또는 삭제된 사용자)에 액세스할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-146">Can I access my users' UPDs (either current or deleted users)?</span></span>
<span data-ttu-id="cc7ec-147">예, 문의할 [Azure RemoteApp](mailto:remoteappforum@microsoft.com), 우리에 설정할 수 있습니다 URL tooaccess hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-147">Yes, if you contact [Azure RemoteApp](mailto:remoteappforum@microsoft.com), we can set you up with a URL tooaccess hello data.</span></span> <span data-ttu-id="cc7ec-148">해야 합니다.이 10 시간은 toodownload에 대 한 데이터 나 hello UPD에서에서 파일 hello 액세스 만료 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-148">You'll have about 10 hours toodownload any data or files from hello UPD before hello access expires.</span></span>

## <a name="are-upds-available-offline"></a><span data-ttu-id="cc7ec-149">UPD를 오프라인으로 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-149">Are UPDs available offline?</span></span>
<span data-ttu-id="cc7ec-150">지금은 hello 10 시간 액세스 창 위에서 설명한 이상 오프 라인 액세스 tooUPDs를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-150">Right now we do not provide offline access tooUPDs, beyond hello 10 hour access window described above.</span></span> <span data-ttu-id="cc7ec-151">이 현재 없으므로 hello Upd에서 바이러스 백신 소프트웨어를 실행 하거나 감사에 대 한 데이터에 액세스 등의 길이가 짧습니다 toocomplete 보다 복잡 한 작업에 대 한 액세스는 방식으로 tooprovide 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-151">This means that we do not currently have a way tooprovide you with access for long enough toocomplete more complicated tasks, like running anti-virus software on hello UPDs or accessing data for an audit.</span></span>

## <a name="do-registry-key-settings-persist"></a><span data-ttu-id="cc7ec-152">레지스트리 키 설정이 유지됩니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-152">Do registry key settings persist?</span></span>
<span data-ttu-id="cc7ec-153">예, tooHKEY_Current_User 기록 된 hello UPD의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-153">Yes, anything written tooHKEY_Current_User is part of hello UPD.</span></span>

## <a name="can-i-disable-upds-for-a-collection"></a><span data-ttu-id="cc7ec-154">컬렉션에 대한 UPD를 비활성화할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-154">Can I disable UPDs for a collection?</span></span>
<span data-ttu-id="cc7ec-155">예, 구독에 대 한 Azure RemoteApp toodisable Upd를 요청할 수 있지만 해당 사용자가 직접 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-155">Yes, you can ask Azure RemoteApp toodisable UPDs for a subscription, but you cannot do that yourself.</span></span> <span data-ttu-id="cc7ec-156">즉, Upd hello 구독의 모든 컬렉션에 사용 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-156">This means that UPDs will be disabled for all collections in hello subscription.</span></span>

<span data-ttu-id="cc7ec-157">Toodisable Upd hello 다음 상황 중 하나를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-157">You might want toodisable UPDs in any of hello following situations:</span></span> 

* <span data-ttu-id="cc7ec-158">사용자 데이터에 대한 완전한 액세스 및 제어가 필요합니다(금융 기관처럼 감사 및 검토 목적으로).</span><span class="sxs-lookup"><span data-stu-id="cc7ec-158">You need complete access and control of user data (for audit and review purposes such as financial institutions).</span></span>
* <span data-ttu-id="cc7ec-159">타사 사용자 솔루션 온-프레미스 관리 프로 파일링 하 고 도메인에 가입 된 Azure RemoteApp 배포에 사용 하 여 toocontinue 원하는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-159">You have 3rd-party user profile management solutions on-premises and want toocontinue using them in your domain-joined Azure RemoteApp deployment.</span></span> <span data-ttu-id="cc7ec-160">Hello 프로필 에이전트 toobe hello 골드 이미지에 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-160">This would require hello profile agent toobe loaded into hello gold image.</span></span> 
* <span data-ttu-id="cc7ec-161">어떤 로컬 데이터 저장소를 필요 하지 않습니다 또는 모든 데이터 hello 클라우드 또는 파일 공유에 있고 Azure RemoteApp을 사용 하 여 로컬로 데이터 toocontrol 저장할 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-161">You don’t need any local data storage or you have all data in hello cloud or file share and would like toocontrol saving of data locally using Azure RemoteApp.</span></span>

<span data-ttu-id="cc7ec-162">자세한 내용은 [Azure RemoteApp에서 UPD(사용자 프로필 디스크) 비활성화](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-162">See  [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) for more information.</span></span>

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a><span data-ttu-id="cc7ec-163">데이터 toohello 시스템 드라이브를 저장 합니다. 사용자가 제한할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-163">Can I restrict users from saving data toohello system drive?</span></span>
<span data-ttu-id="cc7ec-164">예, 하지만 tooset 있는를 hello 템플릿에서 hello 컬렉션을 만들기 전에 이미지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-164">Yes, but you'll need tooset that up in hello template image before you create hello collection.</span></span> <span data-ttu-id="cc7ec-165">다음 단계 tooblock 액세스 toohello 시스템 드라이브 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-165">Use hello following steps tooblock access toohello system drive:</span></span>

1. <span data-ttu-id="cc7ec-166">실행 **gpedit.msc** hello 템플릿 이미지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-166">Run **gpedit.msc** on hello template image.</span></span>
2. <span data-ttu-id="cc7ec-167">너무 이동**사용자 구성 > 관리 템플릿 > Windows 구성 요소 > 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-167">Navigate too**User Configuration > Administrative Templates > Windows Components > Explorer**.</span></span>
3. <span data-ttu-id="cc7ec-168">Hello 다음 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-168">Select hello following options:</span></span>
   * <span data-ttu-id="cc7ec-169">**내 컴퓨터에 지정된 드라이브 숨기기**</span><span class="sxs-lookup"><span data-stu-id="cc7ec-169">**Hide these specified drives in My Computer**</span></span>
   * <span data-ttu-id="cc7ec-170">**내 컴퓨터에서 액세스 toodrives 방지**</span><span class="sxs-lookup"><span data-stu-id="cc7ec-170">**Prevent access toodrives from My Computer**</span></span>

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a><span data-ttu-id="cc7ec-171">UPD를 시드할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-171">Can I seed UPDs?</span></span> <span data-ttu-id="cc7ec-172">Tooput hello 시간 hello 사용자 인 첫 번째 사용 가능한 hello UPD의에서 일부 데이터에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-172">I want tooput some data in hello UPD that's available hello first time hello user signs in.</span></span>
<span data-ttu-id="cc7ec-173">예, hello 템플릿 이미지를 만들 때 toohello 기본 프로필 정보를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-173">Yes, when you create hello template image, you can add information toohello default profile.</span></span> <span data-ttu-id="cc7ec-174">해당 정보 toohello UPD 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-174">That information is then added toohello UPD.</span></span>

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a><span data-ttu-id="cc7ec-175">Hello UPD의 hello 크기 변경할 수 있나요 toostore 데이터 크기에 따라 원하는?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-175">Can I change hello size of hello UPD depending on how much data I want toostore?</span></span>
<span data-ttu-id="cc7ec-176">아니요. 모든 UPD에는 50GB의 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-176">No, all UPDs have 50 GB of storage.</span></span> <span data-ttu-id="cc7ec-177">Toostore 서로 다른 양의 데이터를 원하는 경우에 hello 다음을 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-177">If you want toostore different amounts of data, try hello following:</span></span>

1. <span data-ttu-id="cc7ec-178">Hello 컬렉션에 대 한 Upd를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-178">Disable UPDs for hello collection.</span></span>
2. <span data-ttu-id="cc7ec-179">사용자가 tooaccess에 대 한 파일 공유를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-179">Set up a file share for users tooaccess.</span></span>
3. <span data-ttu-id="cc7ec-180">시작 스크립트를 사용 하 여 부하 hello 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-180">Load hello file share by using a startup script.</span></span> <span data-ttu-id="cc7ec-181">Azure RemoteApp의 시작 스크립트에 대한 자세한 내용은 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-181">See below for details on startup scripts in Azure RemoteApp.</span></span>
4. <span data-ttu-id="cc7ec-182">사용자가 toosave 모든 데이터 toohello 파일 공유를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-182">Direct users toosave all data toohello file share.</span></span>

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a><span data-ttu-id="cc7ec-183">Azure RemoteApp의 시작 스크립트를 어떻게 실행합니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-183">How do I run a startup script in Azure RemoteApp?</span></span>
<span data-ttu-id="cc7ec-184">시작 스크립트 toorun 시작 hello 템플릿 이미지에 예약된 된 작업을 만들어서 hello 컬렉션에 대 한 toouse는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-184">If you want toorun a startup script, start by creating a scheduled task in hello template image you are going toouse for hello collection.</span></span> <span data-ttu-id="cc7ec-185">(sysprep를 실행하기 *전에* 이를 수행합니다.)</span><span class="sxs-lookup"><span data-stu-id="cc7ec-185">(Do this *before* you run sysprep.)</span></span> 

![시스템 작업 만들기](./media/remoteapp-upd/upd1.png)

![사용자가 로그온할 때 실행되는 시스템 작업 만들기](./media/remoteapp-upd/upd2.png)

<span data-ttu-id="cc7ec-188">Hello에 **일반** 탭, 있는지 toochange hello 수 **사용자 계정** 보안에서 너무 "BUILTIN\Users."</span><span class="sxs-lookup"><span data-stu-id="cc7ec-188">On hello **General** tab, be sure toochange hello **User Account** under Security too"BUILTIN\Users."</span></span>

![Hello 그룹 tooa 사용자 계정 변경](./media/remoteapp-upd/upd4.png)

<span data-ttu-id="cc7ec-190">hello 예약 된 작업에는 hello 사용자의 자격 증명을 사용 하 여 시작 스크립트로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-190">hello scheduled task will launch your startup script, using hello user's credentials.</span></span> <span data-ttu-id="cc7ec-191">Hello 작업 toorun 예약 모든 사용자는 한 번에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-191">Schedule hello task toorun every a time a user logs on.</span></span>

!["에서 로그 에" hello 작업에 대 한 hello 트리거 설정](./media/remoteapp-upd/upd3.png)

<span data-ttu-id="cc7ec-193">[그룹 정책 기반 시작 스크립트](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-193">You can also use [Group Policy-based startup scripts](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx).</span></span> 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a><span data-ttu-id="cc7ec-194">시작 메뉴를 hello에 시작 스크립트를 배치 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-194">What about placing a startup script in hello Start menu?</span></span> <span data-ttu-id="cc7ec-195">작동되나요?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-195">Would that work?</span></span>
<span data-ttu-id="cc7ec-196">즉, 수 있습니까 구성 창 스크립트를 실행 하는.bat 파일을 만들 및 toohello c:\ProgramData\Microsoft\Windows\Start 누릅니다 폴더를 저장 한 후 해당 스크립트는 사용자가 RemoteApp 세션을 시작할 때마다 실행?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-196">In other words, can I create a .bat file that runs a config window script and save it toohello c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp folder, and then have that script run whenever a user starts a RemoteApp session?</span></span>

<span data-ttu-id="cc7ec-197">아니요, 또한 hello 시작 메뉴에서 시작 스크립트를 지원 하지 않는 RDSH를 사용 하 여 Azure RemoteApp과 함께 지원 되지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-197">No, that's not supported with Azure RemoteApp, which uses RDSH, which also does not support startup scripts in hello Start menu.</span></span>

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a><span data-ttu-id="cc7ec-198">Mstsc.exe (원격 데스크톱 프로그램 hello) tooconfigure 로그온 스크립트를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-198">Can I use mstsc.exe (hello Remote Desktop program) tooconfigure logon scripts?</span></span>
<span data-ttu-id="cc7ec-199">아니요, Azure RemoteApp에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-199">Nope, not supported by Azure RemoteApp.</span></span>

## <a name="can-i-store-data-on-hello-vm-locally"></a><span data-ttu-id="cc7ec-200">로컬로 hello VM에 데이터를 저장할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-200">Can I store data on hello VM locally?</span></span>
<span data-ttu-id="cc7ec-201">아니요, UPD hello에 hello 외의 다른 VM에 저장 된 데이터는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-201">NO, data stored anywhere on hello VM other than in hello UPD will be lost.</span></span> <span data-ttu-id="cc7ec-202">가능성이 높은 hello 사용자는 hello를 가져올 수 없습니다는 동일한 VM hello 다음 번에 Azure RemoteApp에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-202">There is a high chance hello user will not get hello same VM hello next time that they sign into Azure RemoteApp.</span></span> <span data-ttu-id="cc7ec-203">Hello 사용자가에 로그인 하지 하므로 사용자 VM 지 속성은 유지 되지 않습니다 동일한 VM hello 및 hello 데이터는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-203">We do not maintain user-VM persistence, so hello user will not sign into hello same VM, and hello data will be lost.</span></span> <span data-ttu-id="cc7ec-204">또한 hello 컬렉션 업데이트를 기존 Vm의 Vm-hello VM 자체에 저장 된 데이터를 의미 하는 새 집합으로 대체 됩니다 hello 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-204">Additionally, when we update hello collection, hello existing VMs are replaced with a new set of VMs - that means any data stored on hello VM itself is lost.</span></span> <span data-ttu-id="cc7ec-205">hello 권장 사항은 hello UPD 파일 Azure VNET을 내부 또는 DropBox 등 클라우드 저장소 시스템을 사용 하 여 hello 클라우드에서 파일 서버와 같은 공유 저장소의에서 toostore 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-205">hello recommendation is toostore data in hello UPD, shared storage like Azure Files, a file server inside a VNET, or on hello cloud using a cloud storage system like DropBox.</span></span>

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a><span data-ttu-id="cc7ec-206">PowerShell을 사용하여 VM에 Azure File 공유를 탑재하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cc7ec-206">How do I mount an Azure File share on a VM, using PowerShell?</span></span>
<span data-ttu-id="cc7ec-207">다음과 같이 hello Net PSDrive cmdlet toomount hello 드라이브를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-207">You can use hello Net-PSDrive cmdlet toomount hello drive, as follows:</span></span>

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


<span data-ttu-id="cc7ec-208">Hello 다음을 실행 하 여 자격 증명을 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-208">You can also save your credentials by running hello following:</span></span>

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


<span data-ttu-id="cc7ec-209">건너뛸 수 있는 hello-hello New-psdrive cmdlet에서 자격 증명 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7ec-209">That lets you skip hello -Credential parameter in hello New-PSDrive cmdlet.</span></span>

