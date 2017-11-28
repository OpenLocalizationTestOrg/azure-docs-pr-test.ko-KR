---
title: "aaaGroup 정책 및 MDM 설정 | Microsoft Docs"
description: "회사 소유의 장치에 사용해야 하는 그룹 정책 및 MDM(모바일 장치 관리) 설정에 대한 정보를 제공합니다. 이러한 정책은 적용된 toohello 사용자의 전체 장치 사용 됩니다."
services: active-directory
keywords: "엔터프라이즈 상태 로밍에 대한 그룹 정책 및 MDM 설정이란, 엔터프라이즈 상태 로밍, windows 클라우드"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a><span data-ttu-id="72144-105">그룹 정책 및 MDM 설정</span><span class="sxs-lookup"><span data-stu-id="72144-105">Group Policy and MDM settings</span></span>
<span data-ttu-id="72144-106">이러한 정책 적용된 toohello 사용자의 전체 장치 때문에 이러한 그룹 정책 및 모바일 장치 관리 (MDM) 설정 회사 소유 장치에만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-106">Use these group policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied toohello user’s entire device.</span></span> <span data-ttu-id="72144-107">개인은 MDM 정책 toodisable 설정 동기화를 적용 하는 경우, 사용자 소유 장치 부정적인 영향을 줍니다 해당 장치의 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-107">Applying an MDM policy toodisable settings sync for a personal, user-owned device will negatively impact hello use of that device.</span></span> <span data-ttu-id="72144-108">또한 다른 사용자 계정에 hello 장치 영향도 hello 정책에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-108">Additionally, other user accounts on hello device will also be affected by hello policy.</span></span>

<span data-ttu-id="72144-109">개인 (비관리) 장치에 대 한 로밍 toomanage צ ְ ײ를 원하는 엔터프라이즈에 Azure 포털 tooenable hello 또는 그룹 정책 또는 mdm.를 사용 하 여 보다는 로밍, 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="72144-109">Enterprises that want toomanage roaming for personal (unmanaged) devices can use hello Azure portal tooenable or disable roaming, rather than using Group Policy or MDM.</span></span>
<span data-ttu-id="72144-110">다음 표에서 hello hello 정책 설정을 사용할 수 있는 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-110">hello following tables describe hello policy settings available.</span></span>

## <a name="mdm-settings"></a><span data-ttu-id="72144-111">MDM 설정</span><span class="sxs-lookup"><span data-stu-id="72144-111">MDM settings</span></span>
<span data-ttu-id="72144-112">hello MDM 정책 설정은 tooboth Windows 10 및 Windows 10 Mobile에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72144-112">hello MDM policy settings apply tooboth Windows 10 and Windows 10 Mobile.</span></span>  <span data-ttu-id="72144-113">Windows 10 Mobile 지원은 사용자의 OneDrive 계정을 통한 Microsoft 계정 기반의 로밍에 대해서만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="72144-113">Windows 10 Mobile support exists only for Microsoft account based roaming via user’s OneDrive account.</span></span>  <span data-ttu-id="72144-114">참조 하십시오 너무 Azure AD에 대 한 지원 되는 장치에 대 한 자세한 내용은 "장치 및 끝점" 섹션에 따라 동기화 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="72144-114">Please refer too“Devices and endpoints” section for details on what devices are supported for Azure AD based syncing.</span></span>

| <span data-ttu-id="72144-115">이름</span><span class="sxs-lookup"><span data-stu-id="72144-115">Name</span></span> | <span data-ttu-id="72144-116">설명</span><span class="sxs-lookup"><span data-stu-id="72144-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="72144-117">Microsoft 계정 연결 허용</span><span class="sxs-lookup"><span data-stu-id="72144-117">Allow Microsoft Account Connection</span></span> |<span data-ttu-id="72144-118">사용자가 tooauthenticate를 hello 장치에서 Microsoft 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72144-118">Allows users tooauthenticate using a Microsoft account on hello device</span></span> |
| <span data-ttu-id="72144-119">내 설정 동기화 허용</span><span class="sxs-lookup"><span data-stu-id="72144-119">Allow Sync My Settings</span></span> |<span data-ttu-id="72144-120">사용자가 tooroam Windows 설정 및 앱 데이터가; 허용 비활성화 하면이 정책이 비활성화 됩니다 동기화 뿐만 아니라 모바일 장치에 백업</span><span class="sxs-lookup"><span data-stu-id="72144-120">Allows users tooroam Windows settings and app data; Disabling this policy will disable sync as well as backups on mobile devices</span></span> |

## <a name="group-policy-settings"></a><span data-ttu-id="72144-121">그룹 정책 설정</span><span class="sxs-lookup"><span data-stu-id="72144-121">Group Policy settings</span></span>
<span data-ttu-id="72144-122">hello 그룹 정책 설정은 10 tooWindows 장치 tooan 조인 된 Active Directory 도메인에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72144-122">hello Group Policy settings apply tooWindows 10 devices that are joined tooan Active Directory domain.</span></span> <span data-ttu-id="72144-123">hello 테이블에는 레거시 설정이 toomanage 동기화 설정에 표시 하는 엔터프라이즈 상태 로밍에 대 한 Windows 10에서는 작동 하지 않는 '사용 하지 않는' hello 설명에서와 설명 하는 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72144-123">hello table also includes legacy settings that would appear toomanage sync settings, but that do not work for Enterprise State Roaming for Windows 10, which are noted with ‘Do not use’ in hello description.</span></span>

| <span data-ttu-id="72144-124">이름</span><span class="sxs-lookup"><span data-stu-id="72144-124">Name</span></span> | <span data-ttu-id="72144-125">설명</span><span class="sxs-lookup"><span data-stu-id="72144-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="72144-126">계정: Microsoft 계정 차단</span><span class="sxs-lookup"><span data-stu-id="72144-126">Accounts: Block Microsoft Accounts</span></span> |<span data-ttu-id="72144-127">이 정책 설정은 사용자가 이 컴퓨터에서 새 Microsoft 계정을 추가하지 못하게 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-127">This policy setting prevents users from adding new Microsoft accounts on this computer</span></span> |
| <span data-ttu-id="72144-128">동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-128">Do not sync</span></span> |<span data-ttu-id="72144-129">사용자가 tooroam Windows 설정 및 응용 프로그램 데이터를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-129">Prevents users tooroam Windows settings and app data</span></span> |
| <span data-ttu-id="72144-130">개인 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-130">Do not sync personalize</span></span> |<span data-ttu-id="72144-131">Hello 테마 그룹의 동기화를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-131">Disables syncing of hello Themes group</span></span> |
| <span data-ttu-id="72144-132">브라우저 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-132">Do not sync browser settings</span></span> |<span data-ttu-id="72144-133">Hello Internet Explorer 그룹의 동기화를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72144-133">Disables syncing of hello Internet Explorer group</span></span> |
| <span data-ttu-id="72144-134">암호 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-134">Do not sync passwords</span></span> |<span data-ttu-id="72144-135">암호 그룹 동기화 비활성화</span><span class="sxs-lookup"><span data-stu-id="72144-135">Disables syncing of Passwords group</span></span> |
| <span data-ttu-id="72144-136">기타 Windows 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-136">Do not sync other Windows settings</span></span> |<span data-ttu-id="72144-137">기타 Windows 설정 그룹 동기화 비활성화</span><span class="sxs-lookup"><span data-stu-id="72144-137">Disables syncing of Other Windows settings group</span></span> |
| <span data-ttu-id="72144-138">바탕 화면 개인 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-138">Do not sync desktop personalization</span></span> |<span data-ttu-id="72144-139">사용 안 함. 효과 없음</span><span class="sxs-lookup"><span data-stu-id="72144-139">Do not use; has no effect</span></span> |
| <span data-ttu-id="72144-140">데이터 통신 연결에서 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-140">Do not sync on metered connections</span></span> |<span data-ttu-id="72144-141">셀룰러 3G 같은 데이터 통신 연결에서 로밍 비활성화</span><span class="sxs-lookup"><span data-stu-id="72144-141">Disables roaming on metered connections, such as cellular 3G</span></span> |
| <span data-ttu-id="72144-142">앱 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-142">Do not sync apps</span></span> |<span data-ttu-id="72144-143">사용 안 함. 효과 없음</span><span class="sxs-lookup"><span data-stu-id="72144-143">Do not use; has no effect</span></span> |
| <span data-ttu-id="72144-144">앱 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-144">Do not sync app settings</span></span> |<span data-ttu-id="72144-145">앱 데이터 로밍 비활성화</span><span class="sxs-lookup"><span data-stu-id="72144-145">Disables roaming of app data</span></span> |
| <span data-ttu-id="72144-146">시작 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="72144-146">Do not sync start settings</span></span> |<span data-ttu-id="72144-147">사용 안 함. 효과 없음</span><span class="sxs-lookup"><span data-stu-id="72144-147">Do not use; has no effect</span></span> |

## <a name="related-topics"></a><span data-ttu-id="72144-148">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="72144-148">Related topics</span></span>
* [<span data-ttu-id="72144-149">엔터프라이즈 상태 로밍 개요</span><span class="sxs-lookup"><span data-stu-id="72144-149">Enterprise State Roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="72144-150">Azure Active Directory에서 엔터프라이즈 상태 로밍 활성화</span><span class="sxs-lookup"><span data-stu-id="72144-150">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="72144-151">설정 및 데이터 로밍 FAQ</span><span class="sxs-lookup"><span data-stu-id="72144-151">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="72144-152">Windows 10 로밍 설정 참조</span><span class="sxs-lookup"><span data-stu-id="72144-152">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [<span data-ttu-id="72144-153">문제 해결</span><span class="sxs-lookup"><span data-stu-id="72144-153">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

