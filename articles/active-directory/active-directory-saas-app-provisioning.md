---
title: "Azure AD에서 SaaS 앱 사용자를 자동으로 프로비저닝 | Microsoft Docs"
description: "Azure AD를 사용하여 여러 타사 SaaS 응용 프로그램에서 사용자 계정을 자동으로 프로비저닝, 프로비저닝 해제, 지속적으로 업데이트하는 방법을 소개합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: 7cb780117d64d67449146b9757f8162e23e65d1e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-to-saas-applications-with-azure-active-directory"></a><span data-ttu-id="76214-103">Azure Active Directory를 사용하여 SaaS 응용 프로그램의 사용자를 자동으로 프로비저닝 및 프로비저닝 해제</span><span class="sxs-lookup"><span data-stu-id="76214-103">Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory</span></span>
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a><span data-ttu-id="76214-104">SaaS 앱을 위한 자동 사용자 프로비저닝이란?</span><span class="sxs-lookup"><span data-stu-id="76214-104">What is automated user provisioning for SaaS apps?</span></span>
<span data-ttu-id="76214-105">Azure AD(Azure Active Directory)를 사용하면 Dropbox, Salesforce, ServiceNow 등과 같은 클라우드([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) 응용 프로그램의 사용자 ID 생성, 관리 및 제거를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-105">Azure Active Directory (Azure AD) allows you to automate the creation, maintenance, and removal of user identities in cloud ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) applications such as Dropbox, Salesforce, ServiceNow, and more.</span></span>

<span data-ttu-id="76214-106">**다음은 이 기능을 어떻게 활용할 수 있는지에 대한 몇 가지 예입니다.**</span><span class="sxs-lookup"><span data-stu-id="76214-106">**Below are some examples of what this feature allows you to do:**</span></span>

* <span data-ttu-id="76214-107">새로운 사람이 팀에 참여했을 때 필요한 SaaS 앱에 자동으로 새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76214-107">Automatically create new accounts in the right SaaS apps for new people when they join your team.</span></span>
* <span data-ttu-id="76214-108">사람이 불가피하게 팀에서 떠날 때 SaaS 앱에서 계정을 자동으로 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-108">Automatically deactivate accounts from SaaS apps when people inevitably leave the team.</span></span>
* <span data-ttu-id="76214-109">디렉터리의 변경 내용을 기반으로 SaaS 앱의 ID가 최신 상태를 유지하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-109">Ensure that the identities in your SaaS apps are kept up to date based on changes in the directory.</span></span>
* <span data-ttu-id="76214-110">앱에서 지원할 경우, 그룹과 같이 사용자가 아닌 개체를 SaaS 앱에 프로비저닝합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-110">Provision non-user objects, such as groups, to SaaS apps that support them.</span></span>

<span data-ttu-id="76214-111">**자동 사용자 프로비저닝에는 다음과 같은 기능도 포함됩니다.**</span><span class="sxs-lookup"><span data-stu-id="76214-111">**Automated user provisioning also includes the following functionality:**</span></span>

* <span data-ttu-id="76214-112">기존 ID가 Azure AD와 SaaS 앱 사이에서 동일하도록 일치시킬 수 있는 기능.</span><span class="sxs-lookup"><span data-stu-id="76214-112">The ability to match existing identities between Azure AD and SaaS apps.</span></span>
* <span data-ttu-id="76214-113">조직에서 현재 사용하는 구성에 따라 Azure AD를 SaaS 앱의 현재 구성에 맞게 사용자 지정할 수 있는 옵션.</span><span class="sxs-lookup"><span data-stu-id="76214-113">Customization options to help Azure AD fit the current configurations of the SaaS apps that your organization is currently using.</span></span>
* <span data-ttu-id="76214-114">프로비전닝 오류를 전자 메일로 받을 수 있는 선택적 기능.</span><span class="sxs-lookup"><span data-stu-id="76214-114">Optional email alerts for provisioning errors.</span></span>
* <span data-ttu-id="76214-115">모니터링 및 문제 해결에 도움이 되는 보고 및 활동 로그.</span><span class="sxs-lookup"><span data-stu-id="76214-115">Reporting and activity logs to help with monitoring and troubleshooting.</span></span>

## <a name="why-use-automated-provisioning"></a><span data-ttu-id="76214-116">자동 프로비저닝을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="76214-116">Why Use Automated Provisioning?</span></span>
<span data-ttu-id="76214-117">이 기능을 사용하게 되는 일반적인 동기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-117">Some common motivations for using this feature include:</span></span>

* <span data-ttu-id="76214-118">수동 프로비저닝 절차에서 빚어지는 비용, 비효율성, 사람의 실수를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-118">To avoid the costs, inefficiencies, and human error associated with manual provisioning processes.</span></span>
* <span data-ttu-id="76214-119">사용자가 조직을 떠날 때 즉시 주요 SaaS 앱에서 사용자 ID를 제거하여 조직의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-119">To secure your organization by instantly removing users' identities from key SaaS apps when they leave the organization.</span></span>
* <span data-ttu-id="76214-120">특정 SaaS 응용 프로그램에 대량의 사용자를 손쉽게 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="76214-120">To easily import a bulk number of users into a particular SaaS application.</span></span>
* <span data-ttu-id="76214-121">Azure AD Single Sign-On에 정의한 앱 액세스 정책을 그대로 적용하는 프로비저닝 솔루션의 편리함을 즐길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-121">To enjoy the convenience of having your provisioning solution run off of the same app access policies that you defined for Azure AD Single Sign-On.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="76214-122">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="76214-122">Frequently Asked Questions</span></span>
<span data-ttu-id="76214-123">**Azure AD가 디렉터리의 변경 내용을 얼마나 자주 SaaS 앱에 씁니까?**</span><span class="sxs-lookup"><span data-stu-id="76214-123">**How frequently does Azure AD write directory changes to the SaaS app?**</span></span>

<span data-ttu-id="76214-124">Azure AD는 5 ~ 10분 마다 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-124">Azure AD checks for changes every five to ten minutes.</span></span> <span data-ttu-id="76214-125">SaaS 앱에서 여러 오류(예: 잘못된 관리자 자격 증명)를 반환하는 경우 Azure AD는 오류가 해결될 때까지 최대 하루에 한 번까지 천천히 빈도를 낮춥니다.</span><span class="sxs-lookup"><span data-stu-id="76214-125">If the SaaS app is returning several errors (such as in the case of invalid admin credentials), then Azure AD will gradually slow its frequency to up to once per day until the errors are fixed.</span></span>

<span data-ttu-id="76214-126">**사용자를 프로비저닝 하는 데 얼마나 걸립니까?**</span><span class="sxs-lookup"><span data-stu-id="76214-126">**How long will it take to provision my users?**</span></span>

<span data-ttu-id="76214-127">서서히 변경되는 내용은 거의 즉시 반영되지만 디렉터리 대부분을 프로비저닝하는 경우 사용자와 그룹의 수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="76214-127">Incremental changes happen nearly instantly but if you are trying to provision most of your directory, then it depends on the number of users and groups that you have.</span></span> <span data-ttu-id="76214-128">작은 디렉터리는 1 ~ 2분 정도, 중간 규모의 디렉터리는 몇 분 정도, 매우 큰 디렉터리의 경우는 몇 시간까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-128">Small directories take only a few minutes, medium-sized directories may take several minutes, and very large directories may take several hours.</span></span>

<span data-ttu-id="76214-129">**현재 프로비저닝 작업의 진행률을 어떻게 확인할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="76214-129">**How can I track the progress of the current provisioning job?**</span></span>

<span data-ttu-id="76214-130">디렉터리의 보고서 섹션에서 계정 프로비저닝 보고서를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-130">You can review the Account Provisioning Report under the Reports section of your directory.</span></span> <span data-ttu-id="76214-131">또 다른 방법은 프로비저닝하는 응용 프로그램의 대시보드 탭을 방문하여 페이지 아래쪽에 있는 "통합 상태" 섹션을 살펴보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76214-131">Another option is to visit the Dashboard tab for the SaaS application that you are provisioning to, and look under the "Integration Status" section near the bottom of the page.</span></span>

<span data-ttu-id="76214-132">**사용자가 제대로 프로비저닝되지 않았을 때 어떻게 알 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="76214-132">**How will I know if users fail to get provisioned properly?**</span></span>

<span data-ttu-id="76214-133">프로비저닝 구성 마법사를 끝낼 때 프로비저닝 실패에 대한 알림을 전자 메일로 받을 수 있는 구독 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-133">At the end of the provisioning configuration wizard there is an option to subscribe to email notifications for provisioning failures.</span></span> <span data-ttu-id="76214-134">프로비저닝 오류 보고서를 통해 어떤 사용자의 프로비저닝에 실패했으며 그 이유는 무엇인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-134">You can also check the Provisioning Errors Report to see which users failed to be provisioned and why.</span></span>

<span data-ttu-id="76214-135">**Azure AD가 SaaS 앱의 변경 내용을 디렉터리로 다시 쓸 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="76214-135">**Can Azure AD write changes from the SaaS app back to the directory?**</span></span>

<span data-ttu-id="76214-136">대부분의 SaaS 앱에서 프로비저닝은 아웃바운드 전용입니다. 이는 사용자가 디렉터리에서 응용 프로그램으로 쓰여지고, 응용 프로그램의 변경 내용은 디렉터리에 다시 쓸 수 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-136">For most SaaS apps, provisioning is outbound-only, which means that users are written from the directory to the application, and changes from the application cannot be written back to the directory.</span></span> <span data-ttu-id="76214-137">그러나 [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx)의 경우 프로비저닝이 인바운드 전용입니다. 즉 Workday에서 디렉터리로 사용자를 가져오며, 디렉터리의 변경 내용은 Workday에 쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-137">For [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), however, provisioning is inbound-only, which means that that users are imported into the directory from Workday, and likewise, changes in the directory do not get written back into Workday.</span></span>

<span data-ttu-id="76214-138">**엔지니어링 팀에 의견을 제출할 수 있는 방법은 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="76214-138">**How can I submit feedback to the engineering team?**</span></span>

<span data-ttu-id="76214-139">[Azure Active Directory 피드백 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)을 통해 연락해 주십시오.</span><span class="sxs-lookup"><span data-stu-id="76214-139">Please contact us through the [Azure Active Directory feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>

## <a name="how-does-automated-provisioning-work"></a><span data-ttu-id="76214-140">자동 프로비저닝은 어떻게 수행됩니까?</span><span class="sxs-lookup"><span data-stu-id="76214-140">How Does Automated Provisioning Work?</span></span>
<span data-ttu-id="76214-141">Azure AD는 각 응용 프로그램 공급 업체에서 제공하는 프로비저닝 끝점에 연결하여 SaaS 앱에 사용자를 프로비저닝합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-141">Azure AD provisions users to SaaS apps by connecting to provisioning endpoints provided by each application vendor.</span></span> <span data-ttu-id="76214-142">이러한 끝점을 사용하여 Azure AD에서 프로그래밍 방식으로 사용자를 만들고, 업데이트하고, 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-142">These endpoints allow Azure AD to programmatically create, update, and remove users.</span></span> <span data-ttu-id="76214-143">다음은 Azure AD에서 자동 프로비저닝을 수행하는 서로 다른 단계에 대한 간략한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="76214-143">Below is a brief overview of the different steps that Azure AD takes to automate provisioning.</span></span>

1. <span data-ttu-id="76214-144">응용 프로그램에 대한 프로비저닝을 처음 사용하는 경우 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="76214-144">When you enable provisioning for an application for the first time, the following actions are performed:</span></span>
   * <span data-ttu-id="76214-145">Azure AD에서 디렉터리의 ID와 SaaS 앱의 기존 사용자를 맞추는 작업을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-145">Azure AD will attempt to match any existing users in the SaaS app with their corresponding identities in the directory.</span></span> <span data-ttu-id="76214-146">사용자가 일치하는 경우 Single Sign-On에 대해 자동으로 사용하지 *않도록* 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="76214-146">When a user is matched, they are *not* automatically enabled for single sign-on.</span></span> <span data-ttu-id="76214-147">사용자가 응용 프로그램에 액세스하려면 직접 또는 그룹 구성원을 통해 사용자에게 Azure AD의 앱을 명시적으로 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-147">In order for a user to have access to the application, they must be explicitly assigned to the app in Azure AD, either directly or via group membership.</span></span>
   * <span data-ttu-id="76214-148">어떤 사용자를 응용 프로그램에 할당할지 이미 지정한 경우, 그리고 Azure AD가 이러한 사용자에 대한 기존 계정을 찾지 못한 경우, Azure AD는 이러한 사용자를 위해 응용 프로그램 내에 새 계정을 프로비저닝합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-148">If you have already specified which users should be assigned to the application, and if Azure AD fails to find existing accounts for those users, Azure AD will provision new accounts for them in the application.</span></span>
2. <span data-ttu-id="76214-149">위에 설명한 대로 초기 동기화가 완료되면 Azure AD는 다음 변경 내용을 10분마다 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-149">Once the initial synchronization has been completed as described above, Azure AD will check every 10 minutes for the following changes:</span></span>
   * <span data-ttu-id="76214-150">새 사용자가 응용 프로그램에 할당된 경우(직접 또는 그룹 멤버 자격을 통해) SaaS 앱에 새 계정이 프로비저닝됩니다.</span><span class="sxs-lookup"><span data-stu-id="76214-150">If new users have been assigned to the application (either directly or through group membership), then they will be provisioned a new account in the SaaS app.</span></span>
   * <span data-ttu-id="76214-151">사용자의 액세스 권한이 제거된 경우 이 계정은 SaaS 앱에서 사용할 수 없는 것으로 표시됩니다. 구성이 잘못되어 데이터가 손실되는 것을 방지하기 위해 사용자가 완전히 삭제되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-151">If a user's access has been removed, then their account in the SaaS app will be marked as disabled (users are never fully deleted, which protects you from data loss in the event of a misconfiguration).</span></span>
   * <span data-ttu-id="76214-152">사용자가 최근에 응용 프로그램에 할당되었고 SaaS 앱에 이미 계정이 있는 경우, 이 계정은 사용할 수 있는 것으로 표시되며, 사용자 속성이 디렉터리와 비교하여 오래된 정보일 경우 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="76214-152">If a user was recently assigned to the application and they already had an account in the SaaS app, that account will be marked as enabled, and certain user properties may be updated if they are out-of-date compared to the directory.</span></span>
   * <span data-ttu-id="76214-153">디렉터리에서 사용자의 정보(예: 전화 번호, 사무실 위치 등)가 변경된 경우, 이러한 정보 역시 SaaS 응용 프로그램에 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="76214-153">If a user's information (such as phone number, office location, etc) has been changed in the directory, then that information will also be updated in the SaaS application.</span></span>

<span data-ttu-id="76214-154">Azure AD와 SaaS 앱 사이에서 특성이 매핑되는 방법에 대한 자세한 내용은 [특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)의 문서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="76214-154">For more information on how attributes are mapped between Azure AD and your SaaS app, see the article on [Customizing Attribute Mappings](active-directory-saas-customizing-attribute-mappings.md).</span></span>

## <a name="list-of-apps-that-support-automated-user-provisioning"></a><span data-ttu-id="76214-155">자동 사용자 프로비저닝을 지원하는 앱 목록</span><span class="sxs-lookup"><span data-stu-id="76214-155">List of Apps that Support Automated User Provisioning</span></span>
<span data-ttu-id="76214-156">Azure AD 응용 프로그램 갤러리의 모든 "추천" 앱은 자동화된 사용자 프로비저닝을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-156">All of the "Featured" apps in the Azure AD application gallery support automated user provisioning.</span></span> [<span data-ttu-id="76214-157">추천 앱 목록은 여기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-157">The list of featured apps can be viewed here.</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

<span data-ttu-id="76214-158">응용 프로그램에서 자동 사용자 프로비저닝을 지원하려면, 먼저 외부 프로그램이 사용자를 만들고, 유지 관리하고, 제거하는 데 필요한 끝점을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76214-158">In order for an application to support automated user provisioning, it must first provide the necessary endpoints that allow for external programs to automate the creation, maintenance, and removal of users.</span></span> <span data-ttu-id="76214-159">따라서 모든 SaaS 앱이 이 기능과 호환되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76214-159">Therefore, not all SaaS apps are compatible with this feature.</span></span> <span data-ttu-id="76214-160">앱이 이를 지원하면 Azure AD 엔지니어링 팀이 이 앱에 대한 프로비저닝 커넥터를 만들 수 있게 되며, 이러한 작업은 현재와 잠재 고객의 필요에 따라 우선 순위가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="76214-160">For apps that do support this, the Azure AD engineering team will then be able to build a provisioning connector to those apps, and this work is prioritized by the needs of current and prospective customers.</span></span>

<span data-ttu-id="76214-161">추가 응용 프로그램을 위한 프로비저닝 지원을 요청하기 위해 Azure AD 엔지니어링 팀에 문의하려면 [Azure Active Directory 피드백 포럼](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning)을 통해 메시지를 제출하십시오.</span><span class="sxs-lookup"><span data-stu-id="76214-161">To contact the Azure AD engineering team to request provisioning support for additional applications, please submit a message through the [Azure Active Directory feedback forum](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).</span></span>

## <a name="related-articles"></a><span data-ttu-id="76214-162">관련 문서</span><span class="sxs-lookup"><span data-stu-id="76214-162">Related Articles</span></span>
* [<span data-ttu-id="76214-163">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="76214-163">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="76214-164">사용자 프로비저닝에 대한 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="76214-164">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="76214-165">특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="76214-165">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="76214-166">사용자 프로 비전에 대 한 필터 범위 지정</span><span class="sxs-lookup"><span data-stu-id="76214-166">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="76214-167">SCIM를 사용하여 Azure Active Directory으로부터 응용 프로그램에 사용자 및 그룹의 자동 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="76214-167">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="76214-168">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="76214-168">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="76214-169">SaaS App을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="76214-169">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

