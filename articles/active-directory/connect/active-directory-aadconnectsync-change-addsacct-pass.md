---
title: "Azure AD Connect 동기화: hello AD DS 계정 암호를 변경할 | Microsoft Docs"
description: "이 항목 문서 tooupdate hello 계정의 암호를 AD DS hello 후 Azure AD Connect가 변경 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="bb82d-104">Hello AD DS 계정 암호 변경</span><span class="sxs-lookup"><span data-stu-id="bb82d-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="bb82d-105">hello AD DS 계정 toohello 사용자 계정을 온-프레미스 Active Directory와 Azure AD Connect toocommunicate에서 사용 하는 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="bb82d-106">AD DS 계정 hello hello 암호를 변경 하는 경우 Azure AD Connect 동기화 Service hello 새 암호로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="bb82d-107">그렇지 않으면 hello 동기화 더 이상 동기화 할 수 올바르게 hello로 온-프레미스 Active Directory 및 hello 다음 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="bb82d-108">Hello에 동기화 서비스 관리자, 가져오기 또는 내보내기 작업을 온-프레미스 AD 실패 하 고 **자격 증명 없음-시작** 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="bb82d-109">Hello 응용 프로그램 이벤트 로그에서 Windows 이벤트 뷰어 오류가 포함 되어 **이벤트 ID 6000** 및 메시지 **'hello 관리 에이전트 "contoso.com" 이므로 실패 toorun hello 자격 증명이 잘못 되었습니다.'** .</span><span class="sxs-lookup"><span data-stu-id="bb82d-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="bb82d-110">AD DS 계정에 대 한 새 암호로 tooupdate 동기화 서비스 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="bb82d-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="bb82d-111">hello 새 암호로 tooupdate hello 동기화 서비스:</span><span class="sxs-lookup"><span data-stu-id="bb82d-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="bb82d-112">Hello 동기화 서비스 관리자 (→ 시작 동기화 서비스)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="bb82d-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="bb82d-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="bb82d-114">Toohello 이동 **커넥터** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="bb82d-115">선택 hello **AD 커넥터** 해당 암호가 변경 된 것 toohello AD DS 계정에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="bb82d-116">**작업** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="bb82d-117">Hello 팝업 대화 상자에서 선택 **tooActive Directory 포리스트에 연결**:</span><span class="sxs-lookup"><span data-stu-id="bb82d-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="bb82d-118">Hello에 hello hello AD DS 계정의 새 암호를 입력 **암호** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="bb82d-119">클릭 **확인** toosave hello 새 암호와 닫기 hello 팝업 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="bb82d-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="bb82d-120">Azure AD Connect 동기화 Service Windows 서비스 제어 관리자에서 hello 하는 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="bb82d-121">이 tooensure 모든 참조 toohello 이전 암호 hello 메모리 내 캐시에서 제거 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb82d-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb82d-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb82d-122">Next steps</span></span>
<span data-ttu-id="bb82d-123">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="bb82d-123">**Overview topics**</span></span>

* [<span data-ttu-id="bb82d-124">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bb82d-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="bb82d-125">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="bb82d-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
