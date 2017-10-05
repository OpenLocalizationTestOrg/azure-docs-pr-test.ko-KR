---
title: "Azure AD Connect: 설치 유형 선택 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect에 사용할 설치 유형을 선택하는 방법을 안내합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="45004-103">Azure AD Connect에 사용할 설치 유형 선택</span><span class="sxs-lookup"><span data-stu-id="45004-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="45004-104">Azure AD Connect에서는 새 설치에 대해 기본 및 사용자 지정의 두 가지 설치 유형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="45004-105">이 항목은 설치 중에 사용할 옵션을 결정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45004-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="45004-106">Express</span><span class="sxs-lookup"><span data-stu-id="45004-106">Express</span></span>
<span data-ttu-id="45004-107">기본은 가장 일반적인 옵션으로, 약 90%의 새 설치에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="45004-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="45004-108">이 옵션은 가장 일반적인 고객 시나리오에 적합한 구성을 제공하기 위해 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="45004-109">이 옵션에서는 다음과 같이 전제합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-109">It assumes:</span></span>

- <span data-ttu-id="45004-110">단일 Active Directory 포리스트 온-프레미스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="45004-111">설치에 사용할 수는 엔터프라이즈 관리자 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="45004-112">온-프레미스 Active Directory에 100,000개 미만의 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="45004-113">다음 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-113">You get:</span></span>

- <span data-ttu-id="45004-114">Single Sign-On을 위해 온-프레미스에서 Azure AD로 [비밀번호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)</span><span class="sxs-lookup"><span data-stu-id="45004-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="45004-115">[사용자, 그룹, 연락처 및 Windows 10 컴퓨터](active-directory-aadconnectsync-understanding-default-configuration.md)를 동기화하는 구성</span><span class="sxs-lookup"><span data-stu-id="45004-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="45004-116">모든 도메인 및 모든 OU에 포함된 적합한 모든 개체의 동기화</span><span class="sxs-lookup"><span data-stu-id="45004-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="45004-117">항상 사용 가능한 최신 버전을 사용할 수 있도록 [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md)가 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="45004-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="45004-118">기본을 계속 사용할 수 있는 경우의 옵션:</span><span class="sxs-lookup"><span data-stu-id="45004-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="45004-119">모든 OU를 동기화하지는 않으려면 기본을 계속 사용하고 마지막 페이지에서 **동기화 프로세스 시작...***을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="45004-120">그런 후 설치 마법사를 다시 실행하고 [구성 옵션](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)에서 OU를 변경한 후 예약된 동기화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="45004-121">Azure AD Premium에서 비밀번호 쓰기 저장 등의 기능 중 하나를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="45004-122">먼저 기본 방법을 진행하여 초기 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="45004-123">그런 후 설치 마법사를 다시 실행하고 [구성 옵션](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="45004-124">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="45004-124">Custom</span></span>
<span data-ttu-id="45004-125">사용자 지정된 경로는 기본보다 더 많은 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="45004-126">기본 설치에 대해 이전 섹션에 설명된 구성이 조직에 맞지 않는 모든 경우에 이 옵션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="45004-127">사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="45004-127">Use when:</span></span>

- <span data-ttu-id="45004-128">Active Directory에서 엔터프라이즈 관리자 계정에 대한 액세스 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="45004-129">둘 이상의 포리스트가 있거나 앞으로 둘 이상의 포리스트를 동기화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="45004-130">Connect 서버에서 연결할 수 있는 도메인이 포리스트에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="45004-131">사용자 로그인을 위해 페더레이션 또는 통과 인증을 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="45004-132">100,000개가 넘는 개체가 있고 전체 SQL Server를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="45004-133">그룹 기반 필터링과 도메인 또는 OU 기반 필터링을 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="45004-134">DirSync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="45004-134">Upgrade from DirSync</span></span>
<span data-ttu-id="45004-135">현재 DirSync를 사용하는 경우 [DirSync에서 업그레이드](active-directory-aadconnect-dirsync-upgrade-get-started.md)의 단계에 따라 기존 구성을 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="45004-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="45004-136">업그레이드 옵션에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="45004-137">동일한 서버에 Connect를 설치하기 위한 전체 업그레이드</span><span class="sxs-lookup"><span data-stu-id="45004-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="45004-138">기존 DirSync 서버가 여전히 작동 중인 상태에서 Connect를 새 서버에 설치하는 병렬 배포</span><span class="sxs-lookup"><span data-stu-id="45004-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="45004-139">Azure AD Sync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="45004-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="45004-140">현재 Azure AD Sync를 사용하는 경우 한 Connect 버전에서 최신 버전으로 업그레이드할 때와 [동일한 단계](active-directory-aadconnect-upgrade-previous-version.md)를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="45004-141">업그레이드 옵션에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45004-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="45004-142">동일한 서버에 Connect를 설치하기 위한 전체 업그레이드</span><span class="sxs-lookup"><span data-stu-id="45004-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="45004-143">기존 Azure AD Sync 서버가 여전히 작동 중인 상태에서 Connect를 새 서버에 설치하는 스윙 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="45004-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="45004-144">FIM2010 또는 MIM2016에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="45004-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="45004-145">현재 Azure AD Connect에서 Forefront Identity Manager 2010 또는 Microsoft Identity Manager 2016을 사용하는 경우 마이그레이션만 가능한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="45004-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="45004-146">[스윙 마이그레이션](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="45004-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="45004-147">이러한 단계에서는 Azure AD Sync를 모두 FIM2010/MIM2016으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45004-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45004-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45004-148">Next steps</span></span>
<span data-ttu-id="45004-149">사용하도록 선택한 옵션에 따라 왼쪽의 목차에서 자세한 단계를 제공하는 문서를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="45004-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
