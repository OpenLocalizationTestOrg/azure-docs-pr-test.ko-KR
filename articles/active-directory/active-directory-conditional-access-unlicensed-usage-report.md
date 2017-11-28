---
title: "사용 현황 보고서 aaaUnlicensed | Microsoft Docs"
description: "hello 허가 되지 않은 사용 현황 보고서 유료 Azure AD 기능을 사용 하는 라이선스가 없는 사용자가 식별 하는 유용 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="df6be-103">허가되지 않은 사용 현황 보고서</span><span class="sxs-lookup"><span data-stu-id="df6be-103">Unlicensed usage report</span></span>
<span data-ttu-id="df6be-104">hello 허가 되지 않은 사용 현황 보고서 유료 Azure AD 기능을 사용 하는 라이선스가 없는 사용자가 식별 하는 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df6be-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="df6be-105">이렇게 하면 toomake를 효과적으로 사용할은 구매한 라이선스 및 tooidentify 필요할 때 추가 라이선스를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df6be-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="df6be-106">hello 보고서 hello 유료 기능 hello에 지난 30 일의 활성 사용을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="df6be-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="df6be-107">보고서 구조</span><span class="sxs-lookup"><span data-stu-id="df6be-107">Report structure</span></span>
| <span data-ttu-id="df6be-108">열 이름</span><span class="sxs-lookup"><span data-stu-id="df6be-108">Column name</span></span> | <span data-ttu-id="df6be-109">설명</span><span class="sxs-lookup"><span data-stu-id="df6be-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="df6be-110">허가되지 않은 사용자</span><span class="sxs-lookup"><span data-stu-id="df6be-110">Unlicensed User</span></span> |<span data-ttu-id="df6be-111">Hello 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="df6be-111">Name of hello user</span></span> |
| <span data-ttu-id="df6be-112">기능</span><span class="sxs-lookup"><span data-stu-id="df6be-112">Feature</span></span> |<span data-ttu-id="df6be-113">hello 기능 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="df6be-113">hello feature name.</span></span> <span data-ttu-id="df6be-114">예: 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="df6be-114">For example: conditional access</span></span> |
| <span data-ttu-id="df6be-115">액세스한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="df6be-115">Application Accessed</span></span> |<span data-ttu-id="df6be-116">hello 기능에 액세스 하는 hello 응용 프로그램의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="df6be-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="df6be-117">예: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="df6be-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="df6be-118">사용자 계정이 삭제 되 면 hello ' 허가 되지 않은 사용자 ' 열을 채울 1003000090D8B285 같은 id가</span><span class="sxs-lookup"><span data-stu-id="df6be-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="df6be-119">조건부 액세스 기능</span><span class="sxs-lookup"><span data-stu-id="df6be-119">Conditional access feature</span></span>
<span data-ttu-id="df6be-120">Azure AD Premium 라이선스가 없는 경우에 적용되는 조건부 액세스 정책이 있는 서비스에 허가되지 않은 사용자가 액세스하면 플래그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="df6be-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="df6be-121">이 적용 됩니다 tooMFA/으로 위치 정책을 장치에 Intune을 사용 하는 정책을 합니다.</span><span class="sxs-lookup"><span data-stu-id="df6be-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="df6be-122">참고 항목</span><span class="sxs-lookup"><span data-stu-id="df6be-122">See also</span></span>
* [<span data-ttu-id="df6be-123">Office 365 및 기타 Azure Active Directory 연결 앱과 함께 조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="df6be-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="df6be-124">조건부 액세스 tooAzure AD 시작</span><span class="sxs-lookup"><span data-stu-id="df6be-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

