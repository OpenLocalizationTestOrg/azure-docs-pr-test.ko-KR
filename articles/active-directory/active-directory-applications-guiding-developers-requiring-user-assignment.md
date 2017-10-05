---
title: "사용자 할당 필요 - Azure AD | Microsoft Docs"
description: "Azure 응용 프로그램에 대해 사용자 할당을 요구하는 방법."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="d7ec0-103">Azure AD 및 응용 프로그램: 사용자 할당 요구</span><span class="sxs-lookup"><span data-stu-id="d7ec0-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="d7ec0-104">사용자 할당 요구</span><span class="sxs-lookup"><span data-stu-id="d7ec0-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="d7ec0-105">관리자 계정으로 Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="d7ec0-106">주 메뉴에서 **모든 항목** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="d7ec0-107">응용 프로그램에 대해 사용하는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="d7ec0-108">**응용 프로그램** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="d7ec0-109">이 디렉터리와 연결된 응용 프로그램 목록에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="d7ec0-110">**구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="d7ec0-111">**앱 액세스에 필요한 사용자 할당** 토글을 예로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="d7ec0-112">화면 아래쪽에 있는 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="d7ec0-113">이제 응용 프로그램에 사용자 및/또는 그룹을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="d7ec0-114">[응용 프로그램에 사용자 지정](active-directory-applications-guiding-developers-assigning-users.md) 및 [응용 프로그램에 그룹 지정](active-directory-applications-guiding-developers-assigning-groups.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7ec0-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7ec0-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7ec0-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
