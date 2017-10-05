---
title: "허가되지 않은 사용 현황 보고서 | Microsoft Docs"
description: "허가되지 않은 사용 현황 보고서를 사용하면 유료 Azure AD 기능을 사용하는 허가되지 않은 사용자를 식별할 수 있습니다."
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
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="93716-103">허가되지 않은 사용 현황 보고서</span><span class="sxs-lookup"><span data-stu-id="93716-103">Unlicensed usage report</span></span>
<span data-ttu-id="93716-104">허가되지 않은 사용 현황 보고서를 사용하면 유료 Azure AD 기능을 사용하는 허가되지 않은 사용자를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93716-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="93716-105">이를 통해 구매한 라이선스를 더 잘 활용할 수 있도록 해주고 추가 라이선스가 필요할 때를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="93716-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="93716-106">보고서는 지난 30 일 동안 유료 기능의 실제 사용 현황을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="93716-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="93716-107">보고서 구조</span><span class="sxs-lookup"><span data-stu-id="93716-107">Report structure</span></span>
| <span data-ttu-id="93716-108">열 이름</span><span class="sxs-lookup"><span data-stu-id="93716-108">Column name</span></span> | <span data-ttu-id="93716-109">설명</span><span class="sxs-lookup"><span data-stu-id="93716-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="93716-110">허가되지 않은 사용자</span><span class="sxs-lookup"><span data-stu-id="93716-110">Unlicensed User</span></span> |<span data-ttu-id="93716-111">사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="93716-111">Name of the user</span></span> |
| <span data-ttu-id="93716-112">기능</span><span class="sxs-lookup"><span data-stu-id="93716-112">Feature</span></span> |<span data-ttu-id="93716-113">기능 이름</span><span class="sxs-lookup"><span data-stu-id="93716-113">The feature name.</span></span> <span data-ttu-id="93716-114">예: 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="93716-114">For example: conditional access</span></span> |
| <span data-ttu-id="93716-115">액세스한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="93716-115">Application Accessed</span></span> |<span data-ttu-id="93716-116">기능에 액세스하는 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93716-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="93716-117">예: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="93716-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="93716-118">사용자 계정이 삭제된 경우 ‘허가되지 않은 사용자’ 열은 1003000090D8B285와 같은 ID로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="93716-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="93716-119">조건부 액세스 기능</span><span class="sxs-lookup"><span data-stu-id="93716-119">Conditional access feature</span></span>
<span data-ttu-id="93716-120">Azure AD Premium 라이선스가 없는 경우에 적용되는 조건부 액세스 정책이 있는 서비스에 허가되지 않은 사용자가 액세스하면 플래그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="93716-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="93716-121">이는 MFA/위치 정책뿐만 아니라 Intune을 사용하는 장치 정책에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93716-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="93716-122">참고 항목</span><span class="sxs-lookup"><span data-stu-id="93716-122">See also</span></span>
* [<span data-ttu-id="93716-123">Office 365 및 기타 Azure Active Directory 연결 앱과 함께 조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="93716-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="93716-124">Azure AD 조건부 액세스 시작하기</span><span class="sxs-lookup"><span data-stu-id="93716-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

