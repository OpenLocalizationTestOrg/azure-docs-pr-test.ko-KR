---
title: "Azure AD Connect 설치 마법사 다시 실행 | Microsoft Docs"
description: "두 번째로 실행하는 설치 마법사 작동 방법을 설명합니다."
keywords: "Azure AD Connect 설치 마법사를 사용하면 두 번째로 실행하는 유지 관리 설정을 구성합니다."
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
ms.openlocfilehash: 42855b785c0ab334e33a622c8db912ce2438c627
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="db965-104">Azure AD Connect 동기화: 두 번째로 설치 마법사 실행</span><span class="sxs-lookup"><span data-stu-id="db965-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="db965-105">처음으로 Azure AD Connect 설치 마법사를 실행하는 경우 설치를 구성하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="db965-106">설치 마법사를 다시 실행하는 경우 유지 관리에 대한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="db965-107">**Azure AD Connect**라는 시작 메뉴에서 설치 마법사를 찾을 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="db965-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![시작 메뉴](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="db965-109">설치 마법사를 시작하는 경우 이러한 옵션이 있는 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db965-109">When you start the installation wizard, you see a page with these options:</span></span>

![추가 작업의 목록이 있는 페이지](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="db965-111">Azure AD Connect와 함께 ADFS를 설치한 경우 더 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="db965-112">ADFS에 있는 추가 옵션은 [ADFS 관리](active-directory-aadconnect-federation-management.md#manage-ad-fs)에 문서화됩니다.</span><span class="sxs-lookup"><span data-stu-id="db965-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="db965-113">작업 중 하나를 선택하고 **다음**을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db965-114">설치 마법사가 열린 동안 동기화 엔진의 모든 작업이 일시 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="db965-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="db965-115">구성 변경을 완료하는 즉시 설치 마법사를 닫았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="db965-116">현재 구성 보기</span><span class="sxs-lookup"><span data-stu-id="db965-116">View current configuration</span></span>
<span data-ttu-id="db965-117">이 옵션은 현재 구성된 옵션의 빠른 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-117">This option gives you a quick view of your currently configured options.</span></span>

![모든 옵션 및 해당 상태의 목록이 있는 페이지](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="db965-119">**이전**을 클릭하여 다시 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="db965-119">Click **Previous** to go back.</span></span> <span data-ttu-id="db965-120">**종료**를 선택하는 경우 설치 마법사를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="db965-121">동기화 옵션 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="db965-121">Customize synchronization options</span></span>
<span data-ttu-id="db965-122">이 옵션을 사용하여 동기화 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="db965-123">사용자 지정 구성 설치 경로에서 옵션의 하위 집합을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="db965-124">Express 설치를 처음 사용하더라도 이 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db965-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="db965-125">[더 많은 디렉터리 추가](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="db965-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="db965-126">디렉터리를 제거하려면 [커넥터 삭제](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db965-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="db965-127">[도메인 및 OU 필터링 변경](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)</span><span class="sxs-lookup"><span data-stu-id="db965-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="db965-128">그룹 필터링을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-128">Remove Group filtering.</span></span>
* <span data-ttu-id="db965-129">[선택적 기능 변경](active-directory-aadconnect-get-started-custom.md#optional-features)</span><span class="sxs-lookup"><span data-stu-id="db965-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="db965-130">초기 설치에서 다른 옵션을 변경할 수 없고 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="db965-131">이러한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-131">These options are:</span></span>

* <span data-ttu-id="db965-132">userPrincipalName 및 sourceAnchor에 사용할 특성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="db965-133">다른 포리스트의 개체에 대한 조인 방법을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="db965-134">그룹 기반 필터링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="db965-135">디렉터리 스키마 새로 고침</span><span class="sxs-lookup"><span data-stu-id="db965-135">Refresh directory schema</span></span>
<span data-ttu-id="db965-136">온-프레미스 AD DS 포리스트 중 하나에서 스키마를 변경하는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="db965-137">예를 들어 Exchange를 설치했거나 장치 개체를 사용하여 Windows Server 2012 스키마로 업그레이드했습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="db965-138">이 경우에 Azure AD Connect가 AD DS에서 스키마를 다시 읽고 캐시를 업데이트하도록 지시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="db965-139">이 작업은 또한 동기화 규칙을 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="db965-140">예를 들어 Exchange 스키마를 추가하는 경우 Exchange에 대한 동기화 규칙을 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="db965-141">이 옵션을 선택하면 구성에 있는 모든 디렉터리가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="db965-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="db965-142">기본 설정을 유지하고 모든 포리스트를 새로 고치거나 선택을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![환경에서 모든 디렉터리의 목록이 있는 페이지](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="db965-144">준비 모드 구성</span><span class="sxs-lookup"><span data-stu-id="db965-144">Configure staging mode</span></span>
<span data-ttu-id="db965-145">이 옵션을 사용하면 서버에서 준비 모드를 설정하거나 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="db965-146">준비 모드 및 사용 방법에 대한 자세한 내용은 [작업](active-directory-aadconnectsync-operations.md#staging-mode)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="db965-147">옵션은 현재 준비를 설정하는지 또는 해제하는지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-147">The option shows if staging is currently enabled or disabled:</span></span>  
![준비 모드의 현재 상태도 표시하는 옵션](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="db965-149">상태를 변경하려면 이 옵션을 선택하고 확인란을 선택하거나 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="db965-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![준비 모드의 현재 상태도 표시하는 옵션](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="db965-151">사용자 로그인 변경</span><span class="sxs-lookup"><span data-stu-id="db965-151">Change user sign-in</span></span>
<span data-ttu-id="db965-152">이 옵션을 사용하면 암호 동기화에서 페더레이션에 또는 그 반대로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="db965-153">**구성하지 않음**으로 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db965-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="db965-154">이 옵션에 대한 자세한 내용은 [사용자 로그인](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db965-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db965-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db965-155">Next steps</span></span>
* <span data-ttu-id="db965-156">[선언적 프로비전 이해](active-directory-aadconnectsync-understanding-declarative-provisioning.md)에서 Azure AD Connect 동기화에서 사용되는 구성 모델에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db965-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="db965-157">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="db965-157">**Overview topics**</span></span>

* [<span data-ttu-id="db965-158">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="db965-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="db965-159">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="db965-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
