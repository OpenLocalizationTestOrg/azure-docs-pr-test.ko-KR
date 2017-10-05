---
title: "Azure AD Connect 동기화: 실수로 인한 삭제 방지 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect의 실수로 인한 삭제 방지 기능을 설명합니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a33fb729cff5007e40820af696cfec823a3ecfde
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a><span data-ttu-id="67d85-103">Azure AD Connect 동기화: 실수로 인한 삭제 방지</span><span class="sxs-lookup"><span data-stu-id="67d85-103">Azure AD Connect sync: Prevent accidental deletes</span></span>
<span data-ttu-id="67d85-104">이 항목에서는 Azure AD Connect의 실수로 인한 삭제 방지 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-104">This topic describes the prevent accidental deletes (preventing accidental deletions) feature in Azure AD Connect.</span></span>

<span data-ttu-id="67d85-105">Azure AD Connect를 설치하면 실수로 인한 삭제 방지가 기본적으로 사용되며 삭제 수가 500개를 초과하는 내보내기를 허용하지 않도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-105">When installing Azure AD Connect, prevent accidental deletes is enabled by default and configured to not allow an export with more than 500 deletes.</span></span> <span data-ttu-id="67d85-106">이 기능은 다수의 사용자 및 다른 개체에 영향을 주는 실수에 의한 구성 변경 및 온-프레미스 디렉터리 변경을 방지하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-106">This feature is designed to protect you from accidental configuration changes and changes to your on-premises directory that would affect many users and other objects.</span></span>

## <a name="what-is-prevent-accidental-deletes"></a><span data-ttu-id="67d85-107">실수로 인한 삭제를 방지하는 기능</span><span class="sxs-lookup"><span data-stu-id="67d85-107">What is prevent accidental deletes</span></span>
<span data-ttu-id="67d85-108">다수의 삭제가 다음을 포함하는 경우의 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-108">Common scenarios when you see many deletes include:</span></span>

* <span data-ttu-id="67d85-109">전체 [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) 또는 [도메인](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering)을 선택하지 않은 [필터링](active-directory-aadconnectsync-configure-filtering.md)으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-109">Changes to [filtering](active-directory-aadconnectsync-configure-filtering.md) where an entire [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) or [domain](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) is unselected.</span></span>
* <span data-ttu-id="67d85-110">OU의 모든 개체가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-110">All objects in an OU are deleted.</span></span>
* <span data-ttu-id="67d85-111">OU 이름이 변경되면 OU의 모든 개체가 동기화 범위를 벗어난 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-111">An OU is renamed so all objects in it are considered to be out of scope for synchronization.</span></span>

<span data-ttu-id="67d85-112">기본값인 500개 개체는 PowerShell에서 `Enable-ADSyncExportDeletionThreshold`를 사용하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-112">The default value of 500 objects can be changed with PowerShell using `Enable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="67d85-113">조직의 규모에 맞게 이 값을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-113">You should configure this value to fit the size of your organization.</span></span> <span data-ttu-id="67d85-114">동기화 스케줄러가 30분마다 실행되므로 이 값은 30분 내에 표시되는 삭제 수입니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-114">Since the sync scheduler runs every 30 minutes, the value is the number of deletes seen within 30 minutes.</span></span>

<span data-ttu-id="67d85-115">Azure AD로 내보내도록 스테이징된 삭제 수가 너무 많을 경우 내보내기가 중지되며 다음과 같은 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-115">If there are too many deletes staged to be exported to Azure AD, then the export stops and you receive an email like this:</span></span>

![실수로 인한 삭제 방지 메일](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> <span data-ttu-id="67d85-117">*안녕하세요. (기술 담당자). (시간)에 ID 동기화 서비스에서 삭제 수가 (조직 이름)에 대해 구성된 삭제 임계값을 초과했음을 검색했습니다. 총 (개수)개 개체가 이 ID 동기화 실행에서 삭제를 위해 전송되었습니다. 이는 구성된 삭제 임계값인 (개수)개 개체에 도달했거나 초과했습니다. 진행하기 전에 사용자가 이러한 삭제가 처리되어야 한다는 확인을 제공해야 합니다. 이 메일 메시지에 나열된 오류에 대한 자세한 내용은 실수로 인한 삭제 방지를 참조하세요.*</span><span class="sxs-lookup"><span data-stu-id="67d85-117">*Hello (technical contact). At (time) the Identity synchronization service detected that the number of deletions exceeded the configured deletion threshold for (organization name). A total of (number) objects were sent for deletion in this Identity synchronization run. This met or exceeded the configured deletion threshold value of (number) objects. We need you to provide confirmation that these deletions should be processed before we will proceed. Please see the preventing accidental deletions for more information about the error listed in this email message.*</span></span>
>
> 

<span data-ttu-id="67d85-118">또한 프로파일 내보내기에 대한 **Synchronization Service Manager** UI를 찾아보면 `stopped-deletion-threshold-exceeded` 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-118">You can also see the status `stopped-deletion-threshold-exceeded` when you look in the **Synchronization Service Manager** UI for the Export profile.</span></span>
<span data-ttu-id="67d85-119">![실수로 인한 삭제 방지 동기화 서비스 관리자 UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span><span class="sxs-lookup"><span data-stu-id="67d85-119">![Prevent Accidental deletes Sync Service Manager UI](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)</span></span>

<span data-ttu-id="67d85-120">예상된 경우가 아니라면 조사하여 수정 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-120">If this was unexpected, then investigate and take corrective actions.</span></span> <span data-ttu-id="67d85-121">삭제되는 개체를 확인하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-121">To see which objects are about to be deleted, do the following:</span></span>

1. <span data-ttu-id="67d85-122">시작 메뉴에서 **동기화 서비스** 를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-122">Start **Synchronization Service** from the Start Menu.</span></span>
2. <span data-ttu-id="67d85-123">**커넥터**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-123">Go to **Connectors**.</span></span>
3. <span data-ttu-id="67d85-124">**Azure Active Directory**유형의 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-124">Select the Connector with type **Azure Active Directory**.</span></span>
4. <span data-ttu-id="67d85-125">오른쪽에 있는 **작업**에서 **커넥터 공간 검색**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-125">Under **Actions** to the right, select **Search Connector Space**.</span></span>
5. <span data-ttu-id="67d85-126">**범위** 아래의 팝업에서 **다음 이후 연결이 끊어짐**을 선택하고 과거 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-126">In the pop-up under **Scope**, select **Disconnected Since** and pick a time in the past.</span></span> <span data-ttu-id="67d85-127">**검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-127">Click **Search**.</span></span> <span data-ttu-id="67d85-128">이 페이지는 삭제되는 모든 개체의 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-128">This page provides a view of all objects about to be deleted.</span></span> <span data-ttu-id="67d85-129">각 항목을 클릭하면 개체에 대한 추가 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-129">By clicking each item, you can get additional information about the object.</span></span> <span data-ttu-id="67d85-130">**열 설정**을 클릭하여 그리드에 표시되는 특성을 더 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-130">You can also click **Column Setting** to add additional attributes to be visible in the grid.</span></span>

![커넥터 공간 검색](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

<span data-ttu-id="67d85-132">모든 삭제를 진행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-132">If all the deletes are desired, then do the following:</span></span>

1. <span data-ttu-id="67d85-133">현재 삭제 임계값을 검색하려면 PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-133">To retrieve the current deletion threshold, run the PowerShell cmdlet `Get-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="67d85-134">Azure AD 전역 관리자 계정 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-134">Provide an Azure AD Global Administrator account and password.</span></span> <span data-ttu-id="67d85-135">기본값은 500입니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-135">The default value is 500.</span></span>
2. <span data-ttu-id="67d85-136">일시적으로 이 보호를 해제하고 삭제를 진행할 수 있도록 하려면 PowerShell cmdlet `Disable-ADSyncExportDeletionThreshold`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-136">To temporarily disable this protection and let those deletes go through, run the PowerShell cmdlet: `Disable-ADSyncExportDeletionThreshold`.</span></span> <span data-ttu-id="67d85-137">Azure AD 전역 관리자 계정 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-137">Provide an Azure AD Global Administrator account and password.</span></span>
   <span data-ttu-id="67d85-138">![자격 증명](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span><span class="sxs-lookup"><span data-stu-id="67d85-138">![Credentials](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)</span></span>
3. <span data-ttu-id="67d85-139">Azure Active Directory Connector를 선택한 상태로 **실행** 작업, **내보내기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-139">With the Azure Active Directory Connector still selected, select the action **Run** and select **Export**.</span></span>
4. <span data-ttu-id="67d85-140">보호를 다시 사용하도록 설정하려면 PowerShell cmdlet `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-140">To re-enable the protection, run the PowerShell cmdlet: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`.</span></span> <span data-ttu-id="67d85-141">현재 삭제 임계값을 검색할 때 500을 알게 된 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-141">Replace 500 with the value you noticed when retrieving the current deletion threshold.</span></span> <span data-ttu-id="67d85-142">Azure AD 전역 관리자 계정 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67d85-142">Provide an Azure AD Global Administrator account and password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67d85-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67d85-143">Next steps</span></span>
<span data-ttu-id="67d85-144">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="67d85-144">**Overview topics**</span></span>

* [<span data-ttu-id="67d85-145">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="67d85-145">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="67d85-146">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="67d85-146">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
