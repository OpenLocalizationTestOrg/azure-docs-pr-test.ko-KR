---
title: "Azure RemoteApp이 사용자 데이터와 설정을 저장하는 방법 | Microsoft Docs"
description: "Azure RemoteApp에서 사용자 프로필 디스크를 사용하여 사용자 데이터를 저장하는 방법을 알아봅니다."
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
ms.openlocfilehash: 4993bf507536659d7951e1552559cf0a6061d345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a><span data-ttu-id="8902b-104">Azure RemoteApp이 사용자 데이터와 설정을 저장하는 방법</span><span class="sxs-lookup"><span data-stu-id="8902b-104">How does Azure RemoteApp save user data and settings?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8902b-105">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8902b-106">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="8902b-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8902b-107">Azure RemoteApp은 장치와 세션에서 사용자 ID 및 사용자 지정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-107">Azure RemoteApp saves user identity and customizations across devices and sessions.</span></span> <span data-ttu-id="8902b-108">이 사용자 데이터는 사용자 프로필 디스크(UPD)라고 하는 사용자별 컬렉션 디스크에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-108">This user data is stored in a per-user per-collection disk, known as a user profile disk (UPD).</span></span> <span data-ttu-id="8902b-109">디스크는 사용자를 따르며 사용자가 로그인한 위치와 관계 없이 일관된 환경을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-109">The disk follows the user and ensures the user has a consistent experience, regardless of where they sign in.</span></span>

<span data-ttu-id="8902b-110">사용자 프로필 디스크는 사용자에게 완전히 투명합니다. 사용자는 자신의 문서 폴더에 문서를 저장하고(로컬 드라이브처럼 표시된) 일반적인 방법으로 해당 앱 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-110">User profile disks are completely transparent to the user — users save documents to their Documents folder (on what appears to be a local drive) and change their app settings as usual.</span></span> <span data-ttu-id="8902b-111">동시에 모든 장치에서 Azure RemoteApp에 연결할 때 모든 개인 설정이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-111">At the same time, all personal settings persist when connecting to Azure RemoteApp from any device.</span></span> <span data-ttu-id="8902b-112">사용자가 볼 수 있는 것은 같은 위치의 해당 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-112">All the user sees is their data in the same place.</span></span>

<span data-ttu-id="8902b-113">각 UPD에는 50GB의 영구 저장소가 있으며 사용자 데이터와 응용 프로그램 설정 모두를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-113">Each UPD has 50GB of persistent storage and contains both user data and application settings.</span></span> 

<span data-ttu-id="8902b-114">사용자 프로필 데이터에 대한 구체적인 내용을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-114">Read on for specifics on user profile data.</span></span>

> [!NOTE]
> <span data-ttu-id="8902b-115">UPD를 비활성화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="8902b-115">Need to disable the UPD?</span></span> <span data-ttu-id="8902b-116">이제는 가능합니다. 자세한 내용은 Pavithra의 블로그 게시물인 [Azure RemoteApp에서 UPD(사용자 프로필 디스크) 비활성화](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8902b-116">You can do that now - check out Pavithra's blog post, [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), for details.</span></span>
> 
> 

## <a name="how-can-an-admin-get-to-the-data"></a><span data-ttu-id="8902b-117">관리자는 데이터를 어떻게 얻을 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-117">How can an admin get to the data?</span></span>
<span data-ttu-id="8902b-118">사용자 중 하나에 대한 데이터에 액세스해야 하는 경우(재해 복구 또는 사용자가 회사를 떠날 경우), Azure 지원에 컬렉션 및 사용자 ID에 대한 구독 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-118">If you need to access the data for one of your users (for disaster recovery or if the user leaves the company), contact Azure Support and provide the subscription information for the collection and the user identity.</span></span> <span data-ttu-id="8902b-119">Azure RemoteApp 팀에서 VHD의 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-119">The Azure RemoteApp team will provide you a URL to the VHD.</span></span> <span data-ttu-id="8902b-120">해당 VHD를 다운로드하고 필요한 문서 또는 파일을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-120">Download that VHD and retrieve any documents or files you need.</span></span> <span data-ttu-id="8902b-121">VHD는 50GB이므로 다운로드하는 데 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-121">Note that the VHD is 50GB, so it will take a bit to download it.</span></span>

## <a name="is-the-data-backed-up"></a><span data-ttu-id="8902b-122">데이터를 백업했습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-122">Is the data backed up?</span></span>
<span data-ttu-id="8902b-123">예, 지리적 위치별로 사용자 데이터의 백업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-123">Yes, we save a backup of the user data per geographic location.</span></span> <span data-ttu-id="8902b-124">주 데이터 센터가 다운된 경우, 데이터는 읽기 전용 및 일반 데이터처럼 동일한 방식으로 액세스할 수 있습니다(Azure RemoteApp에 문의하여 가져옵니다).</span><span class="sxs-lookup"><span data-stu-id="8902b-124">The data is read-only and can be accessed in the same way as the regular data would be (contact Azure RemoteApp to get it), if the primary data center is down.</span></span> <span data-ttu-id="8902b-125">데이터는 실시간으로 백업 위치에 복사되며 다른 버전의 사본을 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-125">The data is copied real-time to the backup location and we do not keep copies of different versions.</span></span> <span data-ttu-id="8902b-126">따라서 데이터가 손상된 경우 이전에 알려진 버전으로 복원할 수 없지만 주 데이터 센터의 작동이 중단되면 다른 위치에서 사용자 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-126">So, on data corruption, we will not be able to restore it to a previously known good version but if the primary data center is down, you will be able to get user data from the other location.</span></span>

## <a name="how-do-users-see-the-upd-on-the-server-side"></a><span data-ttu-id="8902b-127">사용자가 서버측에서 어떻게 UPD를 볼 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-127">How do users see the UPD on the server side?</span></span>
<span data-ttu-id="8902b-128">각 사용자는 자신의 UPD: c:\Users\username에 매핑되는 서버에 자신의 디렉터리를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-128">Each user will have their own directory on the server that maps to their UPD: c:\Users\username.</span></span>

## <a name="whats-the-best-way-to-use-outlook-and-upd"></a><span data-ttu-id="8902b-129">UPD 및 Outlook을 사용하는 가장 좋은 방법은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-129">What's the best way to use Outlook and UPD?</span></span>
<span data-ttu-id="8902b-130">Azure RemoteApp은 세션 간에 Outlook 상태(사서함, PST)를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-130">Azure RemoteApp saves the Outlook state (mailboxes, PSTs) between sessions.</span></span> <span data-ttu-id="8902b-131">이 기능을 사용하려면 PST를 사용자 프로필 데이터(c:\users\<사용자 이름>)에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-131">To enable this, we need the PST to be stored in the user profile data (c:\users\<username>).</span></span> <span data-ttu-id="8902b-132">데이터에 대한 기본 위치이며, 위치를 변경하지 않으면 데이터는 세션 간에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-132">This is the default location for the data, so as long as you do not change the location, the data will persist between sessions.</span></span>

<span data-ttu-id="8902b-133">Outlook에서 "캐시" 모드를 사용하고 검색을 위해 "서버/온라인" 모드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-133">We also recommend that you use "cached" mode in Outlook and use "server/online" mode for searching.</span></span>

<span data-ttu-id="8902b-134">Outlook 및 Azure RemoteApp 사용에 대한 자세한 내용은 [이 문서](remoteapp-outlook.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8902b-134">Check out [this article](remoteapp-outlook.md) for more information on using Outlook and Azure RemoteApp.</span></span>

## <a name="what-about-redirection"></a><span data-ttu-id="8902b-135">리디렉션은 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-135">What about redirection?</span></span>
<span data-ttu-id="8902b-136">[리디렉션](remoteapp-redirection.md)을 설정하여 사용자가 로컬 장치에 액세스할 수 있도록 Azure RemoteApp을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-136">You can configure Azure RemoteApp to let users access local devices by setting up [redirection](remoteapp-redirection.md).</span></span> <span data-ttu-id="8902b-137">로컬 장치는 UPD의 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-137">Local devices will then be able to access the data on the UPD.</span></span>

## <a name="can-i-use-my-upd-as-a-network-share"></a><span data-ttu-id="8902b-138">내 UPD를 네트워크 공유로 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-138">Can I use my UPD as a network share?</span></span>
<span data-ttu-id="8902b-139">아니요.</span><span class="sxs-lookup"><span data-stu-id="8902b-139">No.</span></span> <span data-ttu-id="8902b-140">UPD를 네트워크 공유로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-140">UPDs cannot be used as a network share.</span></span> <span data-ttu-id="8902b-141">사용자가 Azure RemoteApp에 연결된 경우에만 UPD를 사용자가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-141">A UPD is only available to the user when the user is actively connected to Azure RemoteApp.</span></span>

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a><span data-ttu-id="8902b-142">컬렉션에서 사용자를 삭제하면 해당 UPD가 삭제됩니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-142">If I delete a user from a collection, is their UPD deleted?</span></span>
<span data-ttu-id="8902b-143">아니요, 사용자를 삭제하는 경우 UPD를 자동으로 삭제하지 않으며, 대신 컬렉션을 삭제할 때까지 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-143">No, when you delete a user, we do not automatically delete the UPD - instead, we store the data until you delete the collection.</span></span> <span data-ttu-id="8902b-144">컬렉션을 삭제 한 후 90일 동안 모든 UPD를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-144">90 days after you delete the collection, we delete all UPDs.</span></span> 

<span data-ttu-id="8902b-145">컬렉션에서 UPD를 삭제해야 할 경우 Azure RemoteApp에 문의하여 우리쪽에서 UPD를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-145">If you need to delete a UPD from a collection, contact Azure RemoteApp - we can delete UPD from our side.</span></span>

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a><span data-ttu-id="8902b-146">내 사용자의 UPD(현재 또는 삭제된 사용자)에 액세스할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-146">Can I access my users' UPDs (either current or deleted users)?</span></span>
<span data-ttu-id="8902b-147">예, [Azure RemoteApp](mailto:remoteappforum@microsoft.com)에 문의하면 데이터에 액세스하기 위한 URL을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-147">Yes, if you contact [Azure RemoteApp](mailto:remoteappforum@microsoft.com), we can set you up with a URL to access the data.</span></span> <span data-ttu-id="8902b-148">액세스가 만료되기 전에 UPD에서 모든 데이터나 파일을 다운로드하려면 약 10시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-148">You'll have about 10 hours to download any data or files from the UPD before the access expires.</span></span>

## <a name="are-upds-available-offline"></a><span data-ttu-id="8902b-149">UPD를 오프라인으로 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-149">Are UPDs available offline?</span></span>
<span data-ttu-id="8902b-150">지금 당장은 UPD에 대한 오프라인 액세스를 제공하지 않습니다. 위에서 설명한 10시간이 넘어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-150">Right now we do not provide offline access to UPDs, beyond the 10 hour access window described above.</span></span> <span data-ttu-id="8902b-151">감사를 위해 데이터에 액세스하거나 UPD에서 백신 소프트웨어를 실행하는 것과 같이 좀 더 복잡한 작업을 완료하는 데 충분한 액세스 시간을 제공하는 방법이 현재 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-151">This means that we do not currently have a way to provide you with access for long enough to complete more complicated tasks, like running anti-virus software on the UPDs or accessing data for an audit.</span></span>

## <a name="do-registry-key-settings-persist"></a><span data-ttu-id="8902b-152">레지스트리 키 설정이 유지됩니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-152">Do registry key settings persist?</span></span>
<span data-ttu-id="8902b-153">예, HKEY_Current_User로 기록된 내용은 UPD의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-153">Yes, anything written to HKEY_Current_User is part of the UPD.</span></span>

## <a name="can-i-disable-upds-for-a-collection"></a><span data-ttu-id="8902b-154">컬렉션에 대한 UPD를 비활성화할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-154">Can I disable UPDs for a collection?</span></span>
<span data-ttu-id="8902b-155">예, 구독에 UPD를 사용하지 않도록 Azure RemoteApp을 요청할 수 있지만 직접 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-155">Yes, you can ask Azure RemoteApp to disable UPDs for a subscription, but you cannot do that yourself.</span></span> <span data-ttu-id="8902b-156">즉, UPD는 구독의 모든 컬렉션에 대해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-156">This means that UPDs will be disabled for all collections in the subscription.</span></span>

<span data-ttu-id="8902b-157">다음 상황 중 하나에서 UPD를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-157">You might want to disable UPDs in any of the following situations:</span></span> 

* <span data-ttu-id="8902b-158">사용자 데이터에 대한 완전한 액세스 및 제어가 필요합니다(금융 기관처럼 감사 및 검토 목적으로).</span><span class="sxs-lookup"><span data-stu-id="8902b-158">You need complete access and control of user data (for audit and review purposes such as financial institutions).</span></span>
* <span data-ttu-id="8902b-159">타사 사용자 프로필 관리 솔루션이 온-프레미스에 있고 도메인에 가입된 Azure RemoteApp 배포에서 계속 사용하고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-159">You have 3rd-party user profile management solutions on-premises and want to continue using them in your domain-joined Azure RemoteApp deployment.</span></span> <span data-ttu-id="8902b-160">골드 이미지에 프로필 에이전트가 로드되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-160">This would require the profile agent to be loaded into the gold image.</span></span> 
* <span data-ttu-id="8902b-161">로컬 데이터 저장소가 필요하지 않으며 모든 데이터를 클라우드 또는 파일 공유로 유지하고 Azure RemoteApp을 사용하여 데이터를 로컬로 저장하는 것을 제어하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-161">You don’t need any local data storage or you have all data in the cloud or file share and would like to control saving of data locally using Azure RemoteApp.</span></span>

<span data-ttu-id="8902b-162">자세한 내용은 [Azure RemoteApp에서 UPD(사용자 프로필 디스크) 비활성화](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8902b-162">See  [Disable User Profile Disks (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) for more information.</span></span>

## <a name="can-i-restrict-users-from-saving-data-to-the-system-drive"></a><span data-ttu-id="8902b-163">시스템 드라이브에 데이터를 저장하지 않도록 사용자를 제한할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-163">Can I restrict users from saving data to the system drive?</span></span>
<span data-ttu-id="8902b-164">예, 하지만 컬렉션을 만들기 전에 템플릿 이미지에 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-164">Yes, but you'll need to set that up in the template image before you create the collection.</span></span> <span data-ttu-id="8902b-165">시스템 드라이브에 대한 액세스를 차단하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-165">Use the following steps to block access to the system drive:</span></span>

1. <span data-ttu-id="8902b-166">템플릿 이미지에서 **gpedit.msc** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-166">Run **gpedit.msc** on the template image.</span></span>
2. <span data-ttu-id="8902b-167">**사용자 구성 > 관리 템플릿 > Windows 구성 요소 > 탐색기**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-167">Navigate to **User Configuration > Administrative Templates > Windows Components > Explorer**.</span></span>
3. <span data-ttu-id="8902b-168">다음 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-168">Select the following options:</span></span>
   * <span data-ttu-id="8902b-169">**내 컴퓨터에 지정된 드라이브 숨기기**</span><span class="sxs-lookup"><span data-stu-id="8902b-169">**Hide these specified drives in My Computer**</span></span>
   * <span data-ttu-id="8902b-170">**내 컴퓨터에서 드라이브에 대한 액세스 방지**</span><span class="sxs-lookup"><span data-stu-id="8902b-170">**Prevent access to drives from My Computer**</span></span>

## <a name="can-i-seed-upds-i-want-to-put-some-data-in-the-upd-thats-available-the-first-time-the-user-signs-in"></a><span data-ttu-id="8902b-171">UPD를 시드할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-171">Can I seed UPDs?</span></span> <span data-ttu-id="8902b-172">사용자가 처음 로그인할 때 사용할 수 있는 UPD에 일부 데이터를 배치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-172">I want to put some data in the UPD that's available the first time the user signs in.</span></span>
<span data-ttu-id="8902b-173">예, 템플릿 이미지를 만들 때 기본 프로필에 정보를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-173">Yes, when you create the template image, you can add information to the default profile.</span></span> <span data-ttu-id="8902b-174">해당 정보는 UPD에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-174">That information is then added to the UPD.</span></span>

## <a name="can-i-change-the-size-of-the-upd-depending-on-how-much-data-i-want-to-store"></a><span data-ttu-id="8902b-175">저장할 데이터 크기에 따라 UPD의 크기를 변경할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-175">Can I change the size of the UPD depending on how much data I want to store?</span></span>
<span data-ttu-id="8902b-176">아니요. 모든 UPD에는 50GB의 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-176">No, all UPDs have 50 GB of storage.</span></span> <span data-ttu-id="8902b-177">다양한 양의 데이터를 저장하려는 경우 다음을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-177">If you want to store different amounts of data, try the following:</span></span>

1. <span data-ttu-id="8902b-178">컬렉션에 대한 UPD를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-178">Disable UPDs for the collection.</span></span>
2. <span data-ttu-id="8902b-179">사용자가 액세스할 파일 공유를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-179">Set up a file share for users to access.</span></span>
3. <span data-ttu-id="8902b-180">시작 스크립트를 사용하여 파일 공유를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-180">Load the file share by using a startup script.</span></span> <span data-ttu-id="8902b-181">Azure RemoteApp의 시작 스크립트에 대한 자세한 내용은 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8902b-181">See below for details on startup scripts in Azure RemoteApp.</span></span>
4. <span data-ttu-id="8902b-182">사용자에 모든 데이터를 파일 공유에 저장하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-182">Direct users to save all data to the file share.</span></span>

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a><span data-ttu-id="8902b-183">Azure RemoteApp의 시작 스크립트를 어떻게 실행합니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-183">How do I run a startup script in Azure RemoteApp?</span></span>
<span data-ttu-id="8902b-184">시작 스크립트를 실행하려는 경우, 컬렉션에 대해 사용하려는 템플릿 이미지에 예약된 작업을 만들어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-184">If you want to run a startup script, start by creating a scheduled task in the template image you are going to use for the collection.</span></span> <span data-ttu-id="8902b-185">(sysprep를 실행하기 *전에* 이를 수행합니다.)</span><span class="sxs-lookup"><span data-stu-id="8902b-185">(Do this *before* you run sysprep.)</span></span> 

![시스템 작업 만들기](./media/remoteapp-upd/upd1.png)

![사용자가 로그온할 때 실행되는 시스템 작업 만들기](./media/remoteapp-upd/upd2.png)

<span data-ttu-id="8902b-188">**일반** 탭에서 [보안] 아래의 **사용자 계정**을 "BUILTIN\Users"로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-188">On the **General** tab, be sure to change the **User Account** under Security to "BUILTIN\Users."</span></span>

![사용자 계정을 그룹으로 변경](./media/remoteapp-upd/upd4.png)

<span data-ttu-id="8902b-190">예약된 작업은 사용자의 자격 증명을 사용하여 시작 스크립트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-190">The scheduled task will launch your startup script, using the user's credentials.</span></span> <span data-ttu-id="8902b-191">사용자가 로그온할 때마다 작업을 실행하도록 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-191">Schedule the task to run every a time a user logs on.</span></span>

!["로그온 시" 작업에 대한 트리거 설정](./media/remoteapp-upd/upd3.png)

<span data-ttu-id="8902b-193">[그룹 정책 기반 시작 스크립트](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-193">You can also use [Group Policy-based startup scripts](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx).</span></span> 

## <a name="what-about-placing-a-startup-script-in-the-start-menu-would-that-work"></a><span data-ttu-id="8902b-194">시작 메뉴에서 시작 스크립트를 어떻게 배치합니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-194">What about placing a startup script in the Start menu?</span></span> <span data-ttu-id="8902b-195">작동되나요?</span><span class="sxs-lookup"><span data-stu-id="8902b-195">Would that work?</span></span>
<span data-ttu-id="8902b-196">즉, config window 스크립트를 실행하는 .bat 파일을 만들고 c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp 폴더에 저장한 다음, 사용자가 RemoteApp 세션을 시작할 때마다 해당 스크립트를 실행할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-196">In other words, can I create a .bat file that runs a config window script and save it to the c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp folder, and then have that script run whenever a user starts a RemoteApp session?</span></span>

<span data-ttu-id="8902b-197">아니요, Azure RemoteApp에서 지원되지 않으며, 시작 메뉴에서 시작 스크립트를 지원하지 않는 RDSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-197">No, that's not supported with Azure RemoteApp, which uses RDSH, which also does not support startup scripts in the Start menu.</span></span>

## <a name="can-i-use-mstscexe-the-remote-desktop-program-to-configure-logon-scripts"></a><span data-ttu-id="8902b-198">mstsc.exe(원격 데스크톱 프로그램)를 사용하여 로그온 스크립트를 구성할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8902b-198">Can I use mstsc.exe (the Remote Desktop program) to configure logon scripts?</span></span>
<span data-ttu-id="8902b-199">아니요, Azure RemoteApp에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-199">Nope, not supported by Azure RemoteApp.</span></span>

## <a name="can-i-store-data-on-the-vm-locally"></a><span data-ttu-id="8902b-200">VM에 데이터를 로컬로 저장할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8902b-200">Can I store data on the VM locally?</span></span>
<span data-ttu-id="8902b-201">아니요, UPD 이외의 VM에서 임의 위치에 저장된 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-201">NO, data stored anywhere on the VM other than in the UPD will be lost.</span></span> <span data-ttu-id="8902b-202">사용자가 다음에 Azure RemoteApp에 로그인할 때 동일한 VM을 얻지 못할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-202">There is a high chance the user will not get the same VM the next time that they sign into Azure RemoteApp.</span></span> <span data-ttu-id="8902b-203">사용자-VM의 지속성을 유지하지 않으므로 사용자가 동일한 VM에 로그인하지 않고 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-203">We do not maintain user-VM persistence, so the user will not sign into the same VM, and the data will be lost.</span></span> <span data-ttu-id="8902b-204">또한 컬렉션을 업데이트할 때 기존 VM이 새 VM 집합으로 바뀝니다. 따라서 VM 자체에 저장된 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-204">Additionally, when we update the collection, the existing VMs are replaced with a new set of VMs - that means any data stored on the VM itself is lost.</span></span> <span data-ttu-id="8902b-205">권장되는 방법은 UPD, Azure Files과 같은 공유 저장소, VNET 내부의 파일 서버, DropBox와 같은 클라우드 저장소 시스템을 사용하는 클라우드에 데이터를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-205">The recommendation is to store data in the UPD, shared storage like Azure Files, a file server inside a VNET, or on the cloud using a cloud storage system like DropBox.</span></span>

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a><span data-ttu-id="8902b-206">PowerShell을 사용하여 VM에 Azure File 공유를 탑재하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="8902b-206">How do I mount an Azure File share on a VM, using PowerShell?</span></span>
<span data-ttu-id="8902b-207">Net-PSDrive cmdlet을 사용하여 다음과 같이 드라이브를 탑재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-207">You can use the Net-PSDrive cmdlet to mount the drive, as follows:</span></span>

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


<span data-ttu-id="8902b-208">또한 다음을 실행하여 자격 증명을 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-208">You can also save your credentials by running the following:</span></span>

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


<span data-ttu-id="8902b-209">이렇게 하면 New-PSDrive cmdlet에서  -Credential 매개 변수를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8902b-209">That lets you skip the -Credential parameter in the New-PSDrive cmdlet.</span></span>

