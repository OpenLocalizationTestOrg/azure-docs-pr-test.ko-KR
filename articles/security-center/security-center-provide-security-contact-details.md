---
title: "aaaProvide 보안 연락처 세부 정보에서 Azure 보안 센터 | Microsoft Docs"
description: "이 문서에서는 tooprovide 보안 Azure 보안 센터에서 세부 정보를 문의 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="27ade-103">Azure 보안 센터의 보안 연락처 세부 정보 제공</span><span class="sxs-lookup"><span data-stu-id="27ade-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="27ade-104">Azure 보안 센터는 아직 없는 경우 Azure 구독에 대한 보안 연락처 세부 정보를 제공하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="27ade-105">이 정보는 Microsoft toocontact 하 여 사용 Microsoft 보안 대응 센터 (MSRC) hello 발견 불법 또는 무단 당사자가 고객 데이터에 액세스 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="27ade-106">MSRC 선택 보안 hello Azure 네트워크 및 인프라의 모니터링을 수행 하 고 제 3 자에서 위협 인텔리전스 및 남용 불만 받습니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="27ade-107">Hello 첫 번째 매일 발생 하 고 심각도 높은 경고에 대 한 경고의 전자 메일 알림이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="27ade-108">전자 메일 기본 설정은 구독 정책에 대해서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="27ade-109">구독 내의 리소스 그룹은 이러한 설정을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="27ade-110">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="27ade-111">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="27ade-112">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="27ade-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="27ade-113">Hello에 **권장 사항을** 블레이드를 **보안 연락처 세부 정보를 제공**합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="27ade-114">![보안 연락처 제공][1]</span><span class="sxs-lookup"><span data-stu-id="27ade-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="27ade-115">Hello 블레이드가 열립니다 **보안 연락처 세부 정보를 제공**합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="27ade-116">에 hello Azure 구독 tooprovide 연락처 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="27ade-117">![보안 연락처 세부 정보 제공][2]</span><span class="sxs-lookup"><span data-stu-id="27ade-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="27ade-118">두 번째 **보안 연락처 세부 정보 제공** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="27ade-119">Hello 보안 연락처 전자 메일 주소를 하나 이상 쉼표로 구분 하 여 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="27ade-120">입력할 수 있는 전자 메일 주소의 toohello 수는 제한 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="27ade-121">하나의 보안 연락처 국제 전화 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="27ade-122">심각도 높은 경고에 대 한 전자 메일 tooreceive hello 옵션을 설정 **경고에 대 한 전자 메일을 내게 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="27ade-123">Hello 이후, hello 옵션 toosend 전자 메일 알림을 toosubscription 소유자를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="27ade-124">이 옵션은 현재 회색으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="27ade-125">선택 **확인** tooapply hello 보안 tooyour 구독 정보를 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="27ade-126">참고 항목</span><span class="sxs-lookup"><span data-stu-id="27ade-126">See also</span></span>
<span data-ttu-id="27ade-127">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="27ade-128">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="27ade-129">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="27ade-130">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="27ade-131">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="27ade-132">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="27ade-133">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="27ade-134">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27ade-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
