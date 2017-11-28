---
title: "Hello Azure AD Connect 설치 마법사를 다시 실행 | Microsoft Docs"
description: "Hello 설치 마법사의 작동 원리 hello 실행 하면 두 번째 시간에 설명 합니다."
keywords: "hello Azure AD Connect 설치 마법사를 사용 하면 두 번째로 실행 하면 유지 관리 설정을 hello를 구성할 수"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="07d6d-104">Azure AD Connect 동기화: hello 설치 마법사를 두 번째로 실행</span><span class="sxs-lookup"><span data-stu-id="07d6d-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="07d6d-105">hello 처음 hello Azure AD Connect 설치 마법사를 실행 하면 그 방법을 안내 합니다 tooconfigure 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="07d6d-106">Hello 설치 마법사를 다시 실행 하면 유지 관리에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="07d6d-107">명명 된 hello 시작 메뉴에서 hello 설치 마법사를 찾을 수 있습니다 **Azure AD Connect**합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![시작 메뉴](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="07d6d-109">Hello 설치 마법사를 시작 하면이 옵션으로 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-109">When you start hello installation wizard, you see a page with these options:</span></span>

![추가 작업의 목록이 있는 페이지](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="07d6d-111">Azure AD Connect와 함께 ADFS를 설치한 경우 더 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="07d6d-112">추가 옵션에 문서화 된 ad FS에 대해 싶은 의견이 hello [ADFS 관리](active-directory-aadconnect-federation-management.md#manage-ad-fs)합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="07d6d-113">Hello 작업 중 하나를 선택 하 고 클릭 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07d6d-114">Hello 설치 마법사를 열고 있는 동안 hello 동기화 엔진의 모든 작업이 일시 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="07d6d-115">구성 변경을 완료 한으로 hello 설치 마법사를 닫으면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="07d6d-116">현재 구성 보기</span><span class="sxs-lookup"><span data-stu-id="07d6d-116">View current configuration</span></span>
<span data-ttu-id="07d6d-117">이 옵션은 현재 구성된 옵션의 빠른 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-117">This option gives you a quick view of your currently configured options.</span></span>

![모든 옵션 및 해당 상태의 목록이 있는 페이지](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="07d6d-119">클릭 **이전** toogo 백 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="07d6d-120">선택 하는 경우 **종료**, hello 설치 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="07d6d-121">동기화 옵션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="07d6d-121">Customize synchronization options</span></span>
<span data-ttu-id="07d6d-122">이 옵션을 사용 하는 toomake 변경 toohello 동기화 구성.</span><span class="sxs-lookup"><span data-stu-id="07d6d-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="07d6d-123">Hello 사용자 지정 구성 설치 경로에서 옵션 중 일부는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="07d6d-124">Express 설치를 처음 사용하더라도 이 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="07d6d-125">[더 많은 디렉터리 추가](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="07d6d-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="07d6d-126">디렉터리를 제거하려면 [커넥터 삭제](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07d6d-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="07d6d-127">[도메인 및 OU 필터링 변경](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)</span><span class="sxs-lookup"><span data-stu-id="07d6d-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="07d6d-128">그룹 필터링을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-128">Remove Group filtering.</span></span>
* <span data-ttu-id="07d6d-129">[선택적 기능 변경](active-directory-aadconnect-get-started-custom.md#optional-features)</span><span class="sxs-lookup"><span data-stu-id="07d6d-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="07d6d-130">hello hello 초기 설치에서 다른 옵션을 변경할 수 없습니다 및 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="07d6d-131">이러한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-131">These options are:</span></span>

* <span data-ttu-id="07d6d-132">UserPrincipalName 및 sourceAnchor에 대 한 특성 toouse hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="07d6d-133">다른 포리스트의 개체에 대 한 메서드를 조인 하는 hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="07d6d-134">그룹 기반 필터링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="07d6d-135">디렉터리 스키마 새로 고침</span><span class="sxs-lookup"><span data-stu-id="07d6d-135">Refresh directory schema</span></span>
<span data-ttu-id="07d6d-136">온-프레미스 중 하나에 hello 스키마를 변경 했을 경우이 옵션을 사용 합니다. AD DS 포리스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="07d6d-137">예를 들어 Exchange 설치 했을 수 있습니다 또는 장치 개체와 함께 Windows Server 2012 tooa 스키마를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="07d6d-138">이 경우 AD DS에서 다시 tooinstruct tooread hello 스키마를 Azure AD Connect가 필요 하 고 캐시를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="07d6d-139">이 작업에는 hello 동기화 규칙 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="07d6d-140">예를 들어 hello Exchange 스키마를 추가 하는 경우 교환에 대 한 동기화 규칙 hello toohello 구성을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="07d6d-141">이 옵션을 선택 하면 모든 hello 디렉터리 구성에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="07d6d-142">Hello 기본 설정을 유지할 하 고 모든 포리스트에 새로 고침 하거나 선택 취소 합니다. 그 중 일부를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Hello 환경에서 모든 디렉터리의 목록이 있는 페이지](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="07d6d-144">준비 모드 구성</span><span class="sxs-lookup"><span data-stu-id="07d6d-144">Configure staging mode</span></span>
<span data-ttu-id="07d6d-145">이 옵션 tooenable 있으며 hello 서버에서 준비 모드를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="07d6d-146">준비 모드 및 사용 방법에 대한 자세한 내용은 [작업](active-directory-aadconnectsync-operations.md#staging-mode)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="07d6d-147">hello 옵션 스테이징 현재 사용 또는 사용 하지 않도록 설정 하는 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![또한 hello 준비 모드의 현재 상태를 표시 하는 옵션](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="07d6d-149">toochange 상태 hello,이 옵션 선택 하거나 선택을 취소 hello 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![또한 hello 준비 모드의 현재 상태를 표시 하는 옵션](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="07d6d-151">사용자 로그인 변경</span><span class="sxs-lookup"><span data-stu-id="07d6d-151">Change user sign-in</span></span>
<span data-ttu-id="07d6d-152">이 옵션에서는 암호 동기화 toofederation 또는 그 반대의 hello toochange가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="07d6d-153">너무 변경할 수 없습니다**구성 하지 않으면**합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="07d6d-154">이 옵션에 대한 자세한 내용은 [사용자 로그인](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07d6d-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d6d-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07d6d-155">Next steps</span></span>
* <span data-ttu-id="07d6d-156">Azure AD Connect 동기화에서 사용 하는 hello 구성 모델에 대 한 자세한 [이해 선언적 프로비저닝이](active-directory-aadconnectsync-understanding-declarative-provisioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07d6d-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="07d6d-157">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="07d6d-157">**Overview topics**</span></span>

* [<span data-ttu-id="07d6d-158">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="07d6d-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="07d6d-159">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="07d6d-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
