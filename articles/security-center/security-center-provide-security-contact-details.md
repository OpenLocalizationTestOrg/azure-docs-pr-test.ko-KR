---
title: "Azure Security Center의 보안 연락처 세부 정보 제공 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터에서 보안 연락처 세부 정보를 제공하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="4c1d5-103">Azure 보안 센터의 보안 연락처 세부 정보 제공</span><span class="sxs-lookup"><span data-stu-id="4c1d5-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="4c1d5-104">Azure 보안 센터는 아직 없는 경우 Azure 구독에 대한 보안 연락처 세부 정보를 제공하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="4c1d5-105">이 정보는 MSRC(Microsoft 보안 대응 센터)에서 불법적인 또는 권한 없는 당사자가 고객 데이터에 액세스한 것을 발견하는 경우 사용자에게 연락하기 위해 Microsoft에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="4c1d5-106">MSRC는 Azure 네트워크 및 인프라의 선택 보안 모니터링을 수행하고 타사에서 위협 인텔리전스 및 남용 불만 사항을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="4c1d5-107">최초로 일별 경고가 발생할 때와 높은 심각도 경고가 발생하는 경우에만 전자 메일 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="4c1d5-108">전자 메일 기본 설정은 구독 정책에 대해서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="4c1d5-109">구독 내의 리소스 그룹은 이러한 설정을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="4c1d5-110">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="4c1d5-111">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="4c1d5-112">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="4c1d5-112">Implement the recommendation</span></span>
1. <span data-ttu-id="4c1d5-113">**권장 사항** 블레이드에서 **보안 연락처 세부 정보 제공**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="4c1d5-114">![보안 연락처 제공][1]</span><span class="sxs-lookup"><span data-stu-id="4c1d5-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="4c1d5-115">**보안 연락처 세부 정보 제공**블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="4c1d5-116">연락처 정보를 제공할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="4c1d5-117">![보안 연락처 세부 정보 제공][2]</span><span class="sxs-lookup"><span data-stu-id="4c1d5-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="4c1d5-118">두 번째 **보안 연락처 세부 정보 제공** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="4c1d5-119">쉼표로 구분하여 보안 연락처 전자 메일 주소 또는 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="4c1d5-120">입력할 수 있는 전자 메일 주소 수에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="4c1d5-121">하나의 보안 연락처 국제 전화 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="4c1d5-122">심각도 높은 경고에 대해 전자 메일을 받으려면 **경고에 대한 전자 메일 받기**옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="4c1d5-123">향후에는 구독 소유자에게 전자 메일 알림을 보내는 옵션도 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="4c1d5-124">이 옵션은 현재 회색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="4c1d5-125">**확인** 을 선택하여 보안 연락처 정보를 구독에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="4c1d5-126">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4c1d5-126">See also</span></span>
<span data-ttu-id="4c1d5-127">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="4c1d5-128">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4c1d5-129">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4c1d5-130">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="4c1d5-131">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="4c1d5-132">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="4c1d5-133">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="4c1d5-134">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4c1d5-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
