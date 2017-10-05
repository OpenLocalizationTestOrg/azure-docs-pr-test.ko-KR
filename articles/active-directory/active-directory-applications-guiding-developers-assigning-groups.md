---
title: "Azure AD 앱에 그룹 할당 | Microsoft Docs'"
description: "Azure 응용 프로그램에 대해 그룹 할당을 구현하는 방법."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="44ceb-103">응용 프로그램에 Azure Active Directory 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="44ceb-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="44ceb-104">응용 프로그램에 사용자 및 그룹을 할당하기 전에 사용자 할당을 요구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="44ceb-105">사용자 할당을 요구하는 방법에 대한 내용은 [사용자 할당 요구](active-directory-applications-guiding-developers-requiring-user-assignment.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44ceb-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="44ceb-106">이 문서에서는 이 응용 프로그램에 대해 사용하는 Active Directory에서 그룹을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="44ceb-107">응용 프로그램에 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="44ceb-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="44ceb-108">관리자 계정으로 Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="44ceb-109">주 메뉴에서 **모든 항목** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="44ceb-110">응용 프로그램에 대해 사용하는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="44ceb-111">**응용 프로그램** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="44ceb-112">이 디렉터리와 연결된 응용 프로그램 목록에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="44ceb-113">**사용자 및 그룹** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="44ceb-114">**그룹** 드롭다운 목록을 사용하여 Active Directory에서 그룹 목록을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="44ceb-115">그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-115">Select the group.</span></span>
9. <span data-ttu-id="44ceb-116">**할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="44ceb-117">메시지가 표시되면 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44ceb-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44ceb-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44ceb-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
