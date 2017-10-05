---
title: "Azure 지원 요청을 만드는 방법 | Microsoft Docs"
description: "Azure 지원 요청을 만드는 방법을 알아봅니다."
services: Azure Supportability
documentationcenter: 
author: ganganarayanan
manager: scotthit
editor: 
ms.assetid: fd6841ea-c1d5-4bb7-86bd-0c708d193b89
ms.service: azure-supportability
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: gangan
ms.openlocfilehash: 70a4762383d64dc8d568c628cf260ebd8f2d179d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-an-azure-support-request"></a><span data-ttu-id="ff0c2-103">Azure 지원 요청을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ff0c2-103">How to create an Azure support request</span></span>
## <a name="summary"></a><span data-ttu-id="ff0c2-104">요약</span><span class="sxs-lookup"><span data-stu-id="ff0c2-104">Summary</span></span>
<span data-ttu-id="ff0c2-105">Azure 은 Azure 포털( [https://portal.azure.com](https://portal.azure.com))에서 지원 요청을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-105">Azure customers can create and manage support requests in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="ff0c2-106">독일에 대한 Azure Portal은 [https://portal.microsoftazure.de](https://portal.microsoftazure.de)이고 미국 정부에 대한 Azure Portal은 [https://portal.azure.us](https://portal.azure.us)입니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-106">Azure portal for Germany is [https://portal.microsoftazure.de](https://portal.microsoftazure.de) Azure portal for the United States government is [https://portal.azure.us](https://portal.azure.us).</span></span>
> 
> 

<span data-ttu-id="ff0c2-107">고객의 의견에 따라 다음 세 가지 기본 목표에 초점을 맞춰 지원 요청 환경을 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-107">Based on customer feedback, we’ve updated the support request experience to focus on three main goals:</span></span>

* <span data-ttu-id="ff0c2-108">**간소성**: 지원 요청 제출 프로세스를 간단히 하기 위해 클릭 및 블레이드 수를 줄였습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-108">**Streamlined**: Reduce clicks and blades to make the process of submitting a support request simple.</span></span>
* <span data-ttu-id="ff0c2-109">**통합**: Azure 리소스 문제를 해결할 때 컨텍스트를 전환하지 않고도 해당 리소스에 대한 지원 요청을 쉽게 개설할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-109">**Integrated**: When you’re troubleshooting an issue with an Azure resource, it should be easy to open a support request for that resource without switching context.</span></span>
* <span data-ttu-id="ff0c2-110">**효율성**: 지원 담당 엔지니어가 문제를 효율적으로 해결하는 데 필요한 주요 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-110">**Efficient**: Gather the key information your support engineer will need to efficiently resolve your issue.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ff0c2-111">시작</span><span class="sxs-lookup"><span data-stu-id="ff0c2-111">Getting started</span></span>
<span data-ttu-id="ff0c2-112">위쪽 탐색 메뉴에서 또는 리소스 블레이드에서 직접 지원 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-112">You can create a support request from the top navigation menu or directly from a resource blade.</span></span>

<span data-ttu-id="ff0c2-113">**위쪽 탐색 모음에서**</span><span class="sxs-lookup"><span data-stu-id="ff0c2-113">**From the top navigation bar**</span></span>

![새 지원 요청](./media/how-to-create-azure-support-request/NewSupportRequest.png)

<span data-ttu-id="ff0c2-115">**리소스 블레이드에서**</span><span class="sxs-lookup"><span data-stu-id="ff0c2-115">**From a resource blade**</span></span>

![컨텍스트 내](./media/how-to-create-azure-support-request/Incontext.png)

## <a name="basics"></a><span data-ttu-id="ff0c2-117">기본 사항</span><span class="sxs-lookup"><span data-stu-id="ff0c2-117">Basics</span></span>
<span data-ttu-id="ff0c2-118">지원 요청 프로세스의 첫 번째 단계에서는 문제 및 지원 계획에 대한 기본 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-118">The first step of the support request process gathers basic information about your issue and your support plan.</span></span>

<span data-ttu-id="ff0c2-119">예를 들어 보겠습니다. 가상 컴퓨터에 기술적인 문제가 발생했으며 네트워크 연결 문제가 의심됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-119">Let’s take an example: You’re facing technical difficulties with your virtual machine and suspect a network connectivity issue.</span></span>
<span data-ttu-id="ff0c2-120">마법사의 첫 번째 단계에서 서비스("Windows를 실행하는 가상 컴퓨터")와 리소스 (가상 컴퓨터의 이름)을 선택하면 이 문제에 대한 도움을 얻는 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-120">Selecting the service ("Virtual Machine running Windows") and the resource (the name of your virtual machine) in the first step of the wizard starts the process of getting help for this issue.</span></span>

![기본 사항 블레이드](./media/how-to-create-azure-support-request/Basics.png)

> [!NOTE]
> <span data-ttu-id="ff0c2-122">Azure에서는 구독 관리(예: 대금 청구, 할당량 조정 및 계정 전송 등)에 대한 무제한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-122">Azure provides unlimited support for subscription management (things like billing, quota adjustments, and account transfers).</span></span> <span data-ttu-id="ff0c2-123">기술 지원의 경우 지원 계획이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-123">For technical support, you need a support plan.</span></span> <span data-ttu-id="ff0c2-124">[지원 계획에 대해 자세히 알아보세요](https://azure.microsoft.com/support/plans).</span><span class="sxs-lookup"><span data-stu-id="ff0c2-124">[Learn more about support plans](https://azure.microsoft.com/support/plans).</span></span>
> 
> 

## <a name="problem"></a><span data-ttu-id="ff0c2-125">문제</span><span class="sxs-lookup"><span data-stu-id="ff0c2-125">Problem</span></span>
<span data-ttu-id="ff0c2-126">마법사의 두 번째 단계에서는 문제에 대한 추가 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-126">The second step of the wizard gathers additional details about the issue.</span></span> <span data-ttu-id="ff0c2-127">이 단계에서 정확한 정보가 제공되면 이 문제에 가장 적합한 지원 담당 엔지니어에게 사례를 라우팅하고 가능한 한 빨리 문제 진단을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-127">Providing accurate details in this step allows us to route your case to the best support engineer for the issue and to begin diagnosing the issue as soon as possible.</span></span>

![문제 블레이드](./media/how-to-create-azure-support-request/Problem.png)

<span data-ttu-id="ff0c2-129">계속해서 위의 가상 컴퓨터 연결 예에서 네트워크 연결 문제를 나타내도록 이 양식을 작성하고, 문제가 발생한 대략적인 시간 등 문제에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-129">Continuing with the virtual machine connectivity example from above, you would fill out this form to indicate a network connectivity issue, and you would provide further details about the issue, including the approximate time when you experienced the issue.</span></span>

## <a name="related-help"></a><span data-ttu-id="ff0c2-130">관련 도움말</span><span class="sxs-lookup"><span data-stu-id="ff0c2-130">Related Help</span></span>
<span data-ttu-id="ff0c2-131">일부 문제의 경우 문제를 해결하는 유용한 관련 도움말 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-131">For some problems, we provide related help links to troubleshoot the issue.</span></span> <span data-ttu-id="ff0c2-132">권장 문서가 도움이 되지 않는 경우 지원 요청을 만드는 프로세스를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-132">If the recommended documents do not help, you can continue through the process to create a support request.</span></span>
<span data-ttu-id="ff0c2-133">![관련 도움말](./media/how-to-create-azure-support-request/RelatedHelp.png)</span><span class="sxs-lookup"><span data-stu-id="ff0c2-133">![Related help](./media/how-to-create-azure-support-request/RelatedHelp.png)</span></span>

## <a name="contact-information"></a><span data-ttu-id="ff0c2-134">연락처 정보</span><span class="sxs-lookup"><span data-stu-id="ff0c2-134">Contact Information</span></span>
<span data-ttu-id="ff0c2-135">마법사의 마지막 단계에서는 연락 방법을 알 수 있도록 연락처 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-135">The last step of the wizard confirms your contact information so we know how to reach you.</span></span>
<span data-ttu-id="ff0c2-136">![연락처 정보](./media/how-to-create-azure-support-request/ContactInformation.png)</span><span class="sxs-lookup"><span data-stu-id="ff0c2-136">![Contact Information](./media/how-to-create-azure-support-request/ContactInformation.png)</span></span>

<span data-ttu-id="ff0c2-137">문제의 심각도에 따라 업무 시간 중에 연락하기를 원하는지 또는 연중무휴 24시간 응답(이 경우 사용자에게 언제든 연락할 수 있음)을 원하는지 지정하라는 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-137">Depending on the severity of your issue, you may be asked to indicate if you would like us to contact you during business hours or if you would prefer a 24x7 response, which means we may contact you at any time.</span></span>
<span data-ttu-id="ff0c2-138">![연락처 정보(연중 무휴)](./media/how-to-create-azure-support-request/ContactInformation-2.png)</span><span class="sxs-lookup"><span data-stu-id="ff0c2-138">![Contact Information 24x7](./media/how-to-create-azure-support-request/ContactInformation-2.png)</span></span>

## <a name="manage-support-requests"></a><span data-ttu-id="ff0c2-139">지원 요청 관리</span><span class="sxs-lookup"><span data-stu-id="ff0c2-139">Manage support requests</span></span>
<span data-ttu-id="ff0c2-140">지원 요청을 만든 후에는 **지원 요청 관리** 페이지에서 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-140">After you create the support request, you can view the details from the **Manage Support Requests** page.</span></span>

<span data-ttu-id="ff0c2-141">**위쪽 탐색 모음에서**</span><span class="sxs-lookup"><span data-stu-id="ff0c2-141">**From the top navigation bar**</span></span>

![지원 요청 관리 링크](./media/how-to-create-azure-support-request/ManageSupportRequest-link.png)

<span data-ttu-id="ff0c2-143">**지원 요청 관리** 페이지에서 모든 지원 요청과 해당 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-143">On the **Manage support requests** page, you can view all support requests and their status.</span></span>
<span data-ttu-id="ff0c2-144">![지원 요청 관리](./media/how-to-create-azure-support-request/ManageSupportRequest.png)</span><span class="sxs-lookup"><span data-stu-id="ff0c2-144">![Manage Support Request](./media/how-to-create-azure-support-request/ManageSupportRequest.png)</span></span>

<span data-ttu-id="ff0c2-145">심각도, 지원 담당 엔지니어가 응답하는 데 걸리는 예상 시간 등 세부 정보를 확인할 지원 요청을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-145">Select the support request to view details, including severity and the expected time it will take for a support engineer to respond.</span></span>
<span data-ttu-id="ff0c2-146">![VID](./media/how-to-create-azure-support-request/VID.png)</span><span class="sxs-lookup"><span data-stu-id="ff0c2-146">![VID](./media/how-to-create-azure-support-request/VID.png)</span></span>

<span data-ttu-id="ff0c2-147">요청의 심각도를 변경하려면 **비즈니스 영향** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-147">If you want to change the severity of the request, click the **Business impact** tile.</span></span> <span data-ttu-id="ff0c2-148">이전 예에서는 요청이 현재 심각도 3으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-148">In the preceeding example, the request is currently set to Severity C.</span></span>

<span data-ttu-id="ff0c2-149">타일을 클릭하면 진행 중인 지원 요청에 할당할 수 심각도 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-149">Clicking the tile shows you the list of severities you can assign to an open support request.</span></span>

> [!NOTE]
> <span data-ttu-id="ff0c2-150">최대 심각도 수준은 지원 계획에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-150">The maximum severity level depends on your support plan.</span></span> <span data-ttu-id="ff0c2-151">[지원 계획에 대해 자세히 알아보세요](https://azure.microsoft.com/support/plans).</span><span class="sxs-lookup"><span data-stu-id="ff0c2-151">[Learn more about support plans](https://azure.microsoft.com/support/plans).</span></span>
> 
> 

![VID-2](./media/how-to-create-azure-support-request/VID-2.png)

## <a name="feedback"></a><span data-ttu-id="ff0c2-153">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="ff0c2-153">Feedback</span></span>
<span data-ttu-id="ff0c2-154">Microsoft는 사용자 의견 및 제안을 항상 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="ff0c2-154">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="ff0c2-155">[제안 사항](https://feedback.azure.com/forums/266794-support-feedback)을 보내 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-155">Please send us your [suggestions](https://feedback.azure.com/forums/266794-support-feedback).</span></span> <span data-ttu-id="ff0c2-156">[Twitter](https://twitter.com/azuresupport)나 [MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure)을 통해 참여하실 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff0c2-156">Additionally, you can engage with us via [Twitter](https://twitter.com/azuresupport) or the [MSDN forums](https://social.msdn.microsoft.com/Forums/azure).</span></span>

## <a name="learn-more"></a><span data-ttu-id="ff0c2-157">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ff0c2-157">Learn more</span></span>
[<span data-ttu-id="ff0c2-158">Azure 지원 FAQ</span><span class="sxs-lookup"><span data-stu-id="ff0c2-158">Azure Support FAQ</span></span>](https://azure.microsoft.com/support/faq)

