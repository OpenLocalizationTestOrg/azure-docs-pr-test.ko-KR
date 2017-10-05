---
title: "Azure AD Connect 동기화: 기본 구성 변경 | Microsoft Docs"
description: "Azure AD Connect 동기화의 기본 구성을 변경의 모범 사례를 제공합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b723ad800ccc0f3040eb480bb72960943b1fdb16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-the-default-configuration"></a><span data-ttu-id="28357-103">Azure AD Connect 동기화: 기본 구성 변경에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="28357-103">Azure AD Connect sync: Best practices for changing the default configuration</span></span>
<span data-ttu-id="28357-104">이 항목에서는 Azure AD Connect 동기화에 지원되거나 지원되지 않는 변경사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-104">The purpose of this topic is to describe supported and unsupported changes to Azure AD Connect sync.</span></span>

<span data-ttu-id="28357-105">Azure AD Connect에 의해 만들어진 구성은 온-프레미스 Active Directory와 Azure AD를 동기화하는 대부분의 환경에 대해 “있는 그대로” 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-105">The configuration created by Azure AD Connect works “as is” for most environments that synchronize on-premises Active Directory with Azure AD.</span></span> <span data-ttu-id="28357-106">그러나 일부 경우에는, 특정 필요 또는 요구 사항을 충족시키기 위해 구성에 일부 변경 내용을 적용할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-106">However, in some cases, it is necessary to apply some changes to a configuration to satisfy a particular need or requirement.</span></span>

## <a name="changes-to-the-service-account"></a><span data-ttu-id="28357-107">서비스 계정의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="28357-107">Changes to the service account</span></span>
<span data-ttu-id="28357-108">Azure AD Connect 동기화는 설치 마법사에서 만든 서비스 계정에서 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="28357-108">Azure AD Connect sync is running under a service account created by the installation wizard.</span></span> <span data-ttu-id="28357-109">이 서비스 계정은 동기화에 의해 사용되는 데이터베이스에 대한 암호화 키를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-109">This service account holds the encryption keys to the database used by sync.</span></span> <span data-ttu-id="28357-110">127자의 긴 암호로 만들어지며, 만료되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="28357-110">It is created with a 127 characters long password and the password is set to not expire.</span></span>

* <span data-ttu-id="28357-111">서비스 계정의 암호는 변경 또는 초기화가 **지원되지 않습니다** .</span><span class="sxs-lookup"><span data-stu-id="28357-111">It is **unsupported** to change or reset the password of the service account.</span></span> <span data-ttu-id="28357-112">이렇게 하면 암호화 키는 파기되고 서비스는 데이터베이스에 액세스할 수 없으며, 서비스를 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-112">Doing so destroys the encryption keys and the service is not able to access the database and is not able to start.</span></span>

## <a name="changes-to-the-scheduler"></a><span data-ttu-id="28357-113">스케줄러에 대한 변경 사항</span><span class="sxs-lookup"><span data-stu-id="28357-113">Changes to the scheduler</span></span>
<span data-ttu-id="28357-114">빌드 1.1(2016년 2월)의 릴리스부터 [스케줄러](active-directory-aadconnectsync-feature-scheduler.md) 가 기본값 30분이 아닌 다른 동기화 주기를 사용하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-114">Starting with the releases from build 1.1 (February 2016) you can configure the [scheduler](active-directory-aadconnectsync-feature-scheduler.md) to have a different sync cycle than the default 30 minutes.</span></span>

## <a name="changes-to-synchronization-rules"></a><span data-ttu-id="28357-115">동기화 규칙 변경</span><span class="sxs-lookup"><span data-stu-id="28357-115">Changes to Synchronization Rules</span></span>
<span data-ttu-id="28357-116">설치 마법사는 가장 일반적인 시나리오에 대한 작업으로 간주되는 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-116">The installation wizard provides a configuration that is supposed to work for the most common scenarios.</span></span> <span data-ttu-id="28357-117">구성을 변경해야 할 경우에도 여전히 지원되는 구성이 포함된 이 규칙을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-117">In case you need to make changes to the configuration, then you must follow these rules to still have a supported configuration.</span></span>

* <span data-ttu-id="28357-118">기본 직접 특성 흐름이 조직에 적합하지 않은 경우 [특성 흐름을 변경](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-118">You can [change attribute flows](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) if the default direct attribute flows are not suitable for your organization.</span></span>
* <span data-ttu-id="28357-119">[특성을 전달되지 않도록](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) 하고 Azure AD에서 기존 특성 값을 제거하려면 이 시나리오에 대한 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-119">If you want to [not flow an attribute](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) and remove any existing attribute values in Azure AD, then you need to create a rule for this scenario.</span></span>
* <span data-ttu-id="28357-120">[원치 않는 동기화 규칙을 사용하지 않습니다](#disable-an-unwanted-sync-rule) .</span><span class="sxs-lookup"><span data-stu-id="28357-120">[Disable an unwanted Sync Rule](#disable-an-unwanted-sync-rule) rather than deleting it.</span></span> <span data-ttu-id="28357-121">삭제된 규칙을 업그레이드 중 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28357-121">A deleted rule is recreated during an upgrade.</span></span>
* <span data-ttu-id="28357-122">[기본 규칙을 변경하려면](#change-an-out-of-box-rule)원래 규칙의 복사본을 만든 다음 기본 규칙을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-122">To [change an out-of-box rule](#change-an-out-of-box-rule), you should make a copy of the original rule and disable the out-of-box rule.</span></span> <span data-ttu-id="28357-123">동기화 규칙 편집기에서 도움이 되는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="28357-123">The Sync Rule Editor prompts and helps you.</span></span>
* <span data-ttu-id="28357-124">동기화 규칙 편집기를 사용하여 사용자 지정 동기화 규칙을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="28357-124">Export your custom synchronization rules using the Synchronization Rules Editor.</span></span> <span data-ttu-id="28357-125">이 편집기는 재해 복구 시나리오에서 쉽게 다시 만드는 데 사용할 수 있는 PowerShell 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-125">The editor provides you with a PowerShell script you can use to easily recreate them in a disaster recovery scenario.</span></span>

> [!WARNING]
> <span data-ttu-id="28357-126">기본 동기화 규칙에는 지문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-126">The out-of-box sync rules have a thumbprint.</span></span> <span data-ttu-id="28357-127">이들 규칙을 변경하면 지문이 더 이상 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-127">If you make a change to these rules, the thumbprint is no longer matching.</span></span> <span data-ttu-id="28357-128">나중에 Azure AD Connect의 새 릴리스를 적용할 때 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-128">You might have problems in the future when you try to apply a new release of Azure AD Connect.</span></span> <span data-ttu-id="28357-129">이 문서에 유일하게 변경하는 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-129">Only make changes the way it is described in this article.</span></span>

### <a name="disable-an-unwanted-sync-rule"></a><span data-ttu-id="28357-130">원치 않는 동기화 규칙을 사용하지 않습니다</span><span class="sxs-lookup"><span data-stu-id="28357-130">Disable an unwanted Sync Rule</span></span>
<span data-ttu-id="28357-131">기본 동기화 규칙을 삭제하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="28357-131">Do not delete an out-of-box sync rule.</span></span> <span data-ttu-id="28357-132">다음 업그레이드 도중에 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="28357-132">It is recreated during next upgrade.</span></span>

<span data-ttu-id="28357-133">경우에 따라 설치 마법사가 사용 중인 토폴로지에 대해 작동하지 않는 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-133">In some cases, the installation wizard has produced a configuration that is not working for your topology.</span></span> <span data-ttu-id="28357-134">예를 들어, 계정 리소스 포리스트 토폴로지를 가지고 있지만 계정 포리스트의 스키마를 Exchange 스키마로 확장한 경우 Exchange에 대한 규칙은 계정 포리스트와 리소스 포리스트에 대해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="28357-134">For example, if you have an account-resource forest topology but you have extended the schema in the account forest with the Exchange schema, then rules for Exchange are created for the account forest and the resource forest.</span></span> <span data-ttu-id="28357-135">이 경우 Exchange에 대한 동기화 규칙을 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-135">In this case, you need to disable the Sync Rule for Exchange.</span></span>

![비활성화된 동기화 규칙](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

<span data-ttu-id="28357-137">위의 그림에서 설치 마법사가 계정 포리스트의 이전 버전 Exchange 2003 스키마를 발견했습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-137">In the picture above, the installation wizard has found an old Exchange 2003 schema in the account forest.</span></span> <span data-ttu-id="28357-138">이 스키마 확장은 리소스 포리스트가 Fabrikam의 환경에 도입되기 전에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-138">This schema extension was added before the resource forest was introduced in Fabrikam's environment.</span></span> <span data-ttu-id="28357-139">동기화된 이전 버전의 Exchange 구현에 대한 특성이 없는지 확인하려면 동기화 규칙을 보여지는 것처럼 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-139">To ensure no attributes from the old Exchange implementation are synchronized, the sync rule should be disabled as shown.</span></span>

### <a name="change-an-out-of-box-rule"></a><span data-ttu-id="28357-140">기본 규칙을 변경하려면</span><span class="sxs-lookup"><span data-stu-id="28357-140">Change an out-of-box rule</span></span>
<span data-ttu-id="28357-141">조인 규칙을 변경해야 할 때만 기본 규칙을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-141">The only time you should change an out-of-box rule is when you need to change the join rule.</span></span> <span data-ttu-id="28357-142">특성 흐름을 변경해야 할 경우 기본 규칙보다 우선 순위가 높은 동기화 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-142">If you need to change an attribute flow, then you should create a sync rule with higher precedence than the out-of-box rules.</span></span> <span data-ttu-id="28357-143">실질적으로 복제해야 하는 유일한 규칙은 **In from AD - User Join** 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="28357-143">The only rule you practically need to clone is the rule **In from AD - User Join**.</span></span> <span data-ttu-id="28357-144">다른 모든 규칙을 더 높은 우선 순위 규칙으로 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28357-144">You can override all other rules with a higher precedence rule.</span></span>

<span data-ttu-id="28357-145">기본 규칙을 변경해야 할 경우 기본 규칙의 복사본을 만든 다음 원래 규칙을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-145">If you need to make changes to an out-of-box rule, then you should make a copy of the out-of-box rule and disable the original rule.</span></span> <span data-ttu-id="28357-146">그런 다음 복제된 규칙을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-146">Then make the changes to the cloned rule.</span></span> <span data-ttu-id="28357-147">동기화 규칙 편집기가 이들 단계를 수행하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="28357-147">The Sync Rule Editor is helping you with those steps.</span></span> <span data-ttu-id="28357-148">기본 규칙을 열면 이 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="28357-148">When you open an out-of-box rule, you are presented with this dialog box:</span></span>  
![경고 받은 기본 규칙](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

<span data-ttu-id="28357-150">**예**를 선택하여 규칙의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28357-150">Select **Yes** to create a copy of the rule.</span></span> <span data-ttu-id="28357-151">그런 다음 복제된 규칙이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="28357-151">The cloned rule is then opened.</span></span>  
<span data-ttu-id="28357-152">![복제된 규칙](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)</span><span class="sxs-lookup"><span data-stu-id="28357-152">![Cloned rule](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)</span></span>

<span data-ttu-id="28357-153">이 복제된 규칙에서 범위, 조인 및 변환에 필요한 사항을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="28357-153">On this cloned rule, make any necessary changes to scope, join, and transformations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28357-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28357-154">Next steps</span></span>
<span data-ttu-id="28357-155">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="28357-155">**Overview topics**</span></span>

* [<span data-ttu-id="28357-156">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="28357-156">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="28357-157">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="28357-157">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
