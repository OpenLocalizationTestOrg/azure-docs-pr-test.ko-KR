---
title: "Azure AD 및 응용 프로그램: 응용 프로그램에 그룹 지정 | Microsoft Docs"
description: "Azure 응용 프로그램에 대해 사용자 할당을 구현하는 방법."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 97ce69c1-4034-4e38-bd82-8caf984f6b98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 29d63bd5781dc7ef9e84840dd4b1b70222cf6892
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-assigning-users-to-an-application"></a><span data-ttu-id="03646-103">Azure AD 및 응용 프로그램: 응용 프로그램에 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="03646-103">Azure AD and Applications: Assigning Users to an Application</span></span>
<span data-ttu-id="03646-104">응용 프로그램에 사용자 및 그룹을 할당하기 전에 사용자 할당을 요구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-104">Before you can assign users and groups to an application, you must require user assignment.</span></span>  <span data-ttu-id="03646-105">사용자 할당을 요구하는 방법에 대한 내용은 [사용자 할당 요구](active-directory-applications-guiding-developers-requiring-user-assignment.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03646-105">To learn how to require user assignment please see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

## <a name="assigning-users-to-an-application"></a><span data-ttu-id="03646-106">응용 프로그램에 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="03646-106">Assigning Users to an Application</span></span>
1. <span data-ttu-id="03646-107">관리자 계정으로 Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-107">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="03646-108">주 메뉴에서 **모든 항목** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-108">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="03646-109">응용 프로그램에 대해 사용하는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-109">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="03646-110">**응용 프로그램** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-110">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="03646-111">이 디렉터리와 연결된 응용 프로그램 목록에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-111">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="03646-112">**사용자 및 그룹** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-112">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="03646-113">응용 프로그램에 할당하려는 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-113">Select the users you want to assign to the application.</span></span>
8. <span data-ttu-id="03646-114">**할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-114">Click **ASSIGN**.</span></span>
9. <span data-ttu-id="03646-115">메시지가 표시되면 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03646-115">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03646-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03646-116">Next Steps</span></span>
[!INCLUDE [guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]

