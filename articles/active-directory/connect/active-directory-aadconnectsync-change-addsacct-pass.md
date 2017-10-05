---
title: "Azure AD Connect 동기화: AD DS 계정 암호 변경 | Microsoft Docs"
description: "이 항목 문서에서는 AD DS 계정의 암호가 변경된 후 Azure AD Connect를 업데이트하는 방법을 설명합니다."
services: active-directory
keywords: "AD DS 계정, Active Directory 계정, 암호"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="4dbb5-104">AD DS 계정 암호 변경</span><span class="sxs-lookup"><span data-stu-id="4dbb5-104">Changing the AD DS account password</span></span>
<span data-ttu-id="4dbb5-105">AD DS 계정은 Azure AD Connect가 온-프레미스 Active Directory와 통신하는 데 사용하는 사용자 계정을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="4dbb5-106">AD DS 계정의 암호를 변경하는 경우 Azure AD Connect 동기화 서비스를 새 암호로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="4dbb5-107">그렇지 않으면 더 이상 온-프레미스 Active Directory와 올바르게 동기화될 수 없으며 다음 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="4dbb5-108">Synchronization Service Manager에서 온-프레미스 AD를 사용하여 가져오기 또는 내보내기 작업을 수행하면 **no-start-credentials** 오류를 나타내며 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="4dbb5-109">Windows 이벤트 뷰어에서 응용 프로그램 이벤트 로그에는 **이벤트 ID 6000** 오류 및 메시지 **'자격 증명이 잘못되었기 때문에 "contoso.com" 관리 에이전트를 실행하지 못했습니다.'**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="4dbb5-110">AD DS 계정에 대한 새 암호로 동기화 서비스를 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="4dbb5-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="4dbb5-111">새 암호로 동기화 서비스를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="4dbb5-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="4dbb5-112">Synchronization Service Manager를 시작합니다(시작 → 동기화 서비스).</span><span class="sxs-lookup"><span data-stu-id="4dbb5-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="4dbb5-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="4dbb5-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="4dbb5-114">**커넥터** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="4dbb5-115">암호가 변경된 AD DS 계정에 해당하는 **AD 커넥터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="4dbb5-116">**작업** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="4dbb5-117">팝업 대화 상자에서 **Active Directory 포리스트에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="4dbb5-118">**암호** 텍스트 상자에 AD DS 계정의 새 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="4dbb5-119">**확인**을 클릭하여 새 암호를 저장하고 팝업 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="4dbb5-120">Windows Service Control Manager에서 Azure AD Connect 동기화 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="4dbb5-121">이 경우 이전 암호에 대한 모든 참조는 메모리 캐시에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dbb5-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dbb5-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4dbb5-122">Next steps</span></span>
<span data-ttu-id="4dbb5-123">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="4dbb5-123">**Overview topics**</span></span>

* [<span data-ttu-id="4dbb5-124">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4dbb5-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="4dbb5-125">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="4dbb5-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
