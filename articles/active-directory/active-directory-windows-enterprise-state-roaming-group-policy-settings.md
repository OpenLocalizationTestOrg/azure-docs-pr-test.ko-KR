---
title: "<span data-ttu-id=\"a3938-101\">그룹 정책 및 MDM 설정 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"a3938-101\">Group Policy and MDM settings | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"a3938-102\">회사 소유의 장치에 사용해야 하는 그룹 정책 및 MDM(모바일 장치 관리) 설정에 대한 정보를 제공합니다.</span><span class=\"sxs-lookup\"><span data-stu-id=\"a3938-102\">Provides information about group policy and mobile device management (MDM) settings that should be used on corporate-owned devices.</span></span> <span data-ttu-id=\"a3938-103\">이러한 정책은 사용자의 장치 전체에 적용됩니다.</span><span class=\"sxs-lookup\"><span data-stu-id=\"a3938-103\">These policies are applied to the user’s entire device.</span></span>"
services: active-directory
keywords: "<span data-ttu-id=\"a3938-104\">엔터프라이즈 상태 로밍에 대한 그룹 정책 및 MDM 설정이란, 엔터프라이즈 상태 로밍, windows 클라우드</span><span class=\"sxs-lookup\"><span data-stu-id=\"a3938-104\">what are group Policy and MDM settings for Enterprise State Roaming, Enterprise State Roaming, windows cloud</span></span>"
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
ms.openlocfilehash: 71dd5281a618fe7367eab3e97daac069f77ab491
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="group-policy-and-mdm-settings"></a><span data-ttu-id="a3938-105">그룹 정책 및 MDM 설정</span><span class="sxs-lookup"><span data-stu-id="a3938-105">Group Policy and MDM settings</span></span>
<span data-ttu-id="a3938-106">이러한 정책은 사용자의 장치 전체에 적용되므로 회사 소유의 장치에만 그룹 정책 및 MDM(모바일 장치 관리) 설정을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a3938-106">Use these group policy and mobile device management (MDM) settings only on corporate-owned devices because these policies are applied to the user’s entire device.</span></span> <span data-ttu-id="a3938-107">개인의 설정 동기화를 비활성화하는 MDM 정책을 적용하면 사용자 소유의 장치가 해당 장치 사용에 부정적인 영향을 미치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-107">Applying an MDM policy to disable settings sync for a personal, user-owned device will negatively impact the use of that device.</span></span> <span data-ttu-id="a3938-108">뿐만 아니라 해당 장치의 다른 사용자도 정책의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-108">Additionally, other user accounts on the device will also be affected by the policy.</span></span>

<span data-ttu-id="a3938-109">개인(관리되지 않는) 장치에 대한 로밍을 관리하려는 기업은 그룹 정책이나 MDM 대신 Azure 포털을 사용하여 로밍을 활성화 또는 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-109">Enterprises that want to manage roaming for personal (unmanaged) devices can use the Azure portal to enable or disable roaming, rather than using Group Policy or MDM.</span></span>
<span data-ttu-id="a3938-110">다음은 사용 가능한 정책을 설명하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-110">The following tables describe the policy settings available.</span></span>

## <a name="mdm-settings"></a><span data-ttu-id="a3938-111">MDM 설정</span><span class="sxs-lookup"><span data-stu-id="a3938-111">MDM settings</span></span>
<span data-ttu-id="a3938-112">MDM 정책 설정은 Windows 10 및 Windows 10 Mobile에 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-112">The MDM policy settings apply to both Windows 10 and Windows 10 Mobile.</span></span>  <span data-ttu-id="a3938-113">Windows 10 Mobile 지원은 사용자의 OneDrive 계정을 통한 Microsoft 계정 기반의 로밍에 대해서만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-113">Windows 10 Mobile support exists only for Microsoft account based roaming via user’s OneDrive account.</span></span>  <span data-ttu-id="a3938-114">Azure AD 기반 동기화가 지원되는 장치에 대한 내용은 "장치 및 끝점" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3938-114">Please refer to “Devices and endpoints” section for details on what devices are supported for Azure AD based syncing.</span></span>

| <span data-ttu-id="a3938-115">이름</span><span class="sxs-lookup"><span data-stu-id="a3938-115">Name</span></span> | <span data-ttu-id="a3938-116">설명</span><span class="sxs-lookup"><span data-stu-id="a3938-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3938-117">Microsoft 계정 연결 허용</span><span class="sxs-lookup"><span data-stu-id="a3938-117">Allow Microsoft Account Connection</span></span> |<span data-ttu-id="a3938-118">사용자가 장치에서 Microsoft 계정을 사용하여 인증 가능</span><span class="sxs-lookup"><span data-stu-id="a3938-118">Allows users to authenticate using a Microsoft account on the device</span></span> |
| <span data-ttu-id="a3938-119">내 설정 동기화 허용</span><span class="sxs-lookup"><span data-stu-id="a3938-119">Allow Sync My Settings</span></span> |<span data-ttu-id="a3938-120">사용자가 Windows 설정 및 앱 데이터 로밍 가능: 이 정책을 사용하지 않도록 설정하면 모바일 장치의 동기화 및 백업이 모두 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-120">Allows users to roam Windows settings and app data; Disabling this policy will disable sync as well as backups on mobile devices</span></span> |

## <a name="group-policy-settings"></a><span data-ttu-id="a3938-121">그룹 정책 설정</span><span class="sxs-lookup"><span data-stu-id="a3938-121">Group Policy settings</span></span>
<span data-ttu-id="a3938-122">그룹 정책 설정은 Active Directory 도메인에 조인된 Windows 10 장치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-122">The Group Policy settings apply to Windows 10 devices that are joined to an Active Directory domain.</span></span> <span data-ttu-id="a3938-123">이 테이블에는 동기화 설정을 관리하지만 Windows 10의 엔터프라이즈 상태 로밍을 지원하지 않는(설명에 ‘사용 안 함'으로 표시) 기존 설정도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-123">The table also includes legacy settings that would appear to manage sync settings, but that do not work for Enterprise State Roaming for Windows 10, which are noted with ‘Do not use’ in the description.</span></span>

| <span data-ttu-id="a3938-124">이름</span><span class="sxs-lookup"><span data-stu-id="a3938-124">Name</span></span> | <span data-ttu-id="a3938-125">설명</span><span class="sxs-lookup"><span data-stu-id="a3938-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3938-126">계정: Microsoft 계정 차단</span><span class="sxs-lookup"><span data-stu-id="a3938-126">Accounts: Block Microsoft Accounts</span></span> |<span data-ttu-id="a3938-127">이 정책 설정은 사용자가 이 컴퓨터에서 새 Microsoft 계정을 추가하지 못하게 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="a3938-127">This policy setting prevents users from adding new Microsoft accounts on this computer</span></span> |
| <span data-ttu-id="a3938-128">동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-128">Do not sync</span></span> |<span data-ttu-id="a3938-129">사용자의 Windows 설정 및 앱 데이터 로밍 금지</span><span class="sxs-lookup"><span data-stu-id="a3938-129">Prevents users to roam Windows settings and app data</span></span> |
| <span data-ttu-id="a3938-130">개인 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-130">Do not sync personalize</span></span> |<span data-ttu-id="a3938-131">테마 그룹 동기화 비활성화</span><span class="sxs-lookup"><span data-stu-id="a3938-131">Disables syncing of the Themes group</span></span> |
| <span data-ttu-id="a3938-132">브라우저 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-132">Do not sync browser settings</span></span> |<span data-ttu-id="a3938-133">Internet Explorer 그룹 동기화 비활성화</span><span class="sxs-lookup"><span data-stu-id="a3938-133">Disables syncing of the Internet Explorer group</span></span> |
| <span data-ttu-id="a3938-134">암호 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-134">Do not sync passwords</span></span> |<span data-ttu-id="a3938-135">암호 그룹 동기화 비활성화</span><span class="sxs-lookup"><span data-stu-id="a3938-135">Disables syncing of Passwords group</span></span> |
| <span data-ttu-id="a3938-136">기타 Windows 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-136">Do not sync other Windows settings</span></span> |<span data-ttu-id="a3938-137">기타 Windows 설정 그룹 동기화 비활성화</span><span class="sxs-lookup"><span data-stu-id="a3938-137">Disables syncing of Other Windows settings group</span></span> |
| <span data-ttu-id="a3938-138">바탕 화면 개인 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-138">Do not sync desktop personalization</span></span> |<span data-ttu-id="a3938-139">사용 안 함. 효과 없음</span><span class="sxs-lookup"><span data-stu-id="a3938-139">Do not use; has no effect</span></span> |
| <span data-ttu-id="a3938-140">데이터 통신 연결에서 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-140">Do not sync on metered connections</span></span> |<span data-ttu-id="a3938-141">셀룰러 3G 같은 데이터 통신 연결에서 로밍 비활성화</span><span class="sxs-lookup"><span data-stu-id="a3938-141">Disables roaming on metered connections, such as cellular 3G</span></span> |
| <span data-ttu-id="a3938-142">앱 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-142">Do not sync apps</span></span> |<span data-ttu-id="a3938-143">사용 안 함. 효과 없음</span><span class="sxs-lookup"><span data-stu-id="a3938-143">Do not use; has no effect</span></span> |
| <span data-ttu-id="a3938-144">앱 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-144">Do not sync app settings</span></span> |<span data-ttu-id="a3938-145">앱 데이터 로밍 비활성화</span><span class="sxs-lookup"><span data-stu-id="a3938-145">Disables roaming of app data</span></span> |
| <span data-ttu-id="a3938-146">시작 설정 동기화 안 함</span><span class="sxs-lookup"><span data-stu-id="a3938-146">Do not sync start settings</span></span> |<span data-ttu-id="a3938-147">사용 안 함. 효과 없음</span><span class="sxs-lookup"><span data-stu-id="a3938-147">Do not use; has no effect</span></span> |

## <a name="related-topics"></a><span data-ttu-id="a3938-148">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="a3938-148">Related topics</span></span>
* [<span data-ttu-id="a3938-149">엔터프라이즈 상태 로밍 개요</span><span class="sxs-lookup"><span data-stu-id="a3938-149">Enterprise State Roaming overview</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)
* [<span data-ttu-id="a3938-150">Azure Active Directory에서 엔터프라이즈 상태 로밍 활성화</span><span class="sxs-lookup"><span data-stu-id="a3938-150">Enable enterprise state roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md)
* [<span data-ttu-id="a3938-151">설정 및 데이터 로밍 FAQ</span><span class="sxs-lookup"><span data-stu-id="a3938-151">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md)
* [<span data-ttu-id="a3938-152">Windows 10 로밍 설정 참조</span><span class="sxs-lookup"><span data-stu-id="a3938-152">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [<span data-ttu-id="a3938-153">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a3938-153">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

