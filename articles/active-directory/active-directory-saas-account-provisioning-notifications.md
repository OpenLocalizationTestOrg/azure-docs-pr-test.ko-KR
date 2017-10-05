---
title: "계정 프로비전 알림 | Microsoft Docs"
description: "계정 프로비전 알림 활성화를 통해 주의가 필요한 사용자 프로비전 관련 문제에 대한 알림을 받는 방법을 알아보세요."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="bd0d4-103">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="bd0d4-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="bd0d4-104">사용자 프로비전으로 타사 SaaS 응용 프로그램에서 사용자 관리 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="bd0d4-105">자동화 프로세스이지만 때때로 조작이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="bd0d4-106">예를 들어 이 경우는 타사 SaaS 응용 프로그램과 데이터를 교환하기 위해 구성된 계정의 암호가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="bd0d4-107">계정 프로비전 알림을 활성화하면 주의가 필요한 사용자 프로비전 관련 문제에 대해 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="bd0d4-108">타사 SaaS 응용 프로그램에 대한 사용자 프로비전 구성으로 계정 프로비전 알림을 활성화 또는 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![사용자 프로비저닝][1] 

<span data-ttu-id="bd0d4-110">계정 프로비전 알림을 활성화하려면 **확인** 대화 상자 페이지에서 해당 확인란을 선택하고 받는 사람의 메일 별칭을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![계정 프로비전 알림][2]

<span data-ttu-id="bd0d4-112">배포 목록을 받는 사람으로 입력할 수 있습니다. 하지만 알림 메일에는 Azure AD 관리자에 의해서만 액세스할 수 있는 보고서 링크가 포함되어 있다는 사실을 참고해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="bd0d4-113">계정 프로비전 알림을 활성화하면 사용자 프로비전과 관련된 중요한 문제에 대한 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="bd0d4-114">그러나 메일 오버로드를 방지하기 위해, 알림 메일이 활성화된 각 SaaS 응용 프로그램에 대하여 하루에 한 개의 알림 메일만 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bd0d4-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="bd0d4-115">관련 문서</span><span class="sxs-lookup"><span data-stu-id="bd0d4-115">Related Articles</span></span>
* [<span data-ttu-id="bd0d4-116">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="bd0d4-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="bd0d4-117">SaaS 앱에 자동화된 사용자 프로비전/프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="bd0d4-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="bd0d4-118">사용자 프로비저닝에 대한 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bd0d4-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="bd0d4-119">특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="bd0d4-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="bd0d4-120">사용자 프로 비전에 대 한 필터 범위 지정</span><span class="sxs-lookup"><span data-stu-id="bd0d4-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="bd0d4-121">SCIM를 사용하여 Azure Active Directory으로부터 응용 프로그램에 사용자 및 그룹의 자동 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="bd0d4-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="bd0d4-122">SaaS App을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="bd0d4-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
