---
title: "Azure Security Center에서 파트너 통합 | Microsoft Docs"
description: "Azure Security Center를 파트너와 통합하여 Azure 리소스의 전반적인 보안을 강화하는 방법에 대해 알아봅니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 44beafeff5cbe58ac8ca37632879f6ffc2b67e53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="partner-integration-in-azure-security-center"></a><span data-ttu-id="36682-103">Azure Security Center에서 파트너 통합</span><span class="sxs-lookup"><span data-stu-id="36682-103">Partner integration in Azure Security Center</span></span>

<span data-ttu-id="36682-104">이 문서에서는 전반적인 보안을 향상시킬 수 있도록 하는 파트너와 Azure Security Center를 통합하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-104">In this article, we describe how Azure Security Center integrates with partners to help you enhance overall security.</span></span> <span data-ttu-id="36682-105">Security Center는 Azure에서 통합된 환경을 제공하고 파트너 인증 및 요금 청구를 위해 Azure Marketplace를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-105">Security Center offers an integrated experience in Azure, and takes advantage of the Azure Marketplace for partner certification and billing.</span></span>

> [!NOTE] 
> <span data-ttu-id="36682-106">2017년 6월을 기준으로 Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집 및 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-106">As of June 2017, Security Center uses the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="36682-107">자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36682-107">For more information, see [Azure Security Center platform migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="36682-108">이 문서의 정보는 Microsoft Monitoring Agent로 전환 후 Security Center 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36682-108">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>

## <a name="why-deploy-partner-solutions-from-security-center"></a><span data-ttu-id="36682-109">Security Center에서 파트너 솔루션을 배포하는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="36682-109">Why deploy partner solutions from Security Center</span></span>

<span data-ttu-id="36682-110">Security Center에서 파트너 통합을 활용하는 네 가지 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-110">Four main reasons to leverage partner integration in Security Center are:</span></span>

- <span data-ttu-id="36682-111">**배포의 용이성**</span><span class="sxs-lookup"><span data-stu-id="36682-111">**Ease of deployment**.</span></span> <span data-ttu-id="36682-112">Security Center 권장 사항에 따라 파트너 솔루션을 배포하는 것이 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-112">Deploying a partner solution by following the Security Center recommendation is much easier.</span></span> <span data-ttu-id="36682-113">기본 설정 및 네트워크 토폴로지를 사용하여 배포 프로세스를 완벽하게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-113">The deployment process can be fully automated by using a default setup and network topology.</span></span> <span data-ttu-id="36682-114">또는 고객은 유연성 및 사용자 지정을 위한 반자동화된 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-114">Alternatively, customers can choose a semi-automated option for more flexibility and customization.</span></span>
- <span data-ttu-id="36682-115">**통합된 감지**</span><span class="sxs-lookup"><span data-stu-id="36682-115">**Integrated detections**.</span></span> <span data-ttu-id="36682-116">파트너 솔루션의 보안 이벤트는 자동으로 수집, 집계되며 Security Center 알림 및 사고의 일부로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36682-116">Security events from partner solutions are automatically collected, aggregated, and displayed as part of Security Center alerts and incidents.</span></span> <span data-ttu-id="36682-117">또한 이러한 이벤트는 다른 원본의 감지를 결합하여 고급 위협 감지 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-117">These events also are fused with detections from other sources to provide advanced threat-detection capabilities.</span></span>
- <span data-ttu-id="36682-118">**통합 상태 모니터링 및 관리**</span><span class="sxs-lookup"><span data-stu-id="36682-118">**Unified health monitoring and management**.</span></span> <span data-ttu-id="36682-119">고객은 한 눈에 모든 파트너 솔루션을 모니터링하기 위해 통합 상태 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-119">Customers can use integrated health events to monitor all partner solutions at a glance.</span></span> <span data-ttu-id="36682-120">기본 관리는 파트너 솔루션을 사용하여 고급 설정에 쉽게 액세스하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-120">Basic management is available, with easy access to advanced setup by using the partner solution.</span></span>
- <span data-ttu-id="36682-121">**SIEM에 내보내기**</span><span class="sxs-lookup"><span data-stu-id="36682-121">**Export to SIEM**.</span></span> <span data-ttu-id="36682-122">고객은 Azure 로그 통합(미리 보기)를 사용하여 CEF(Common Event Format)에서 모든 Security Center 및 파트너 경고를 온-프레미스 SIEM(보안 정보 및 이벤트 관리) 시스템에 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-122">Customers can export all Security Center and partner alerts in Common Event Format (CEF) to on-premises Security Information and Event Management (SIEM) systems by using Azure log integration (preview).</span></span>


## <a name="partners-that-integrate-with-security-center"></a><span data-ttu-id="36682-123">Security Center와 통합되는 파트너</span><span class="sxs-lookup"><span data-stu-id="36682-123">Partners that integrate with Security Center</span></span>

<span data-ttu-id="36682-124">Security Center는 현재 다음과 같은 솔루션과 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-124">Currently, Security Center integrates with these solutions:</span></span>

- <span data-ttu-id="36682-125">끝점 보호([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec 및 [Azure Cloud Services와 Virtual Machines용 Microsoft 맬웨어 방지 프로그램](https://docs.microsoft.com/azure/security/azure-security-antimalware))</span><span class="sxs-lookup"><span data-stu-id="36682-125">Endpoint protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec, and [Microsoft Antimalware for Azure Cloud Services and Virtual Machines](https://docs.microsoft.com/azure/security/azure-security-antimalware))</span></span> 
- <span data-ttu-id="36682-126">웹 응용 프로그램 방화벽([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) 및 [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/))</span><span class="sxs-lookup"><span data-stu-id="36682-126">Web application firewall ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets), and [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/))</span></span> 
- <span data-ttu-id="36682-127">차세대 방화벽([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) 및 [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html))</span><span class="sxs-lookup"><span data-stu-id="36682-127">Next-generation firewall ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2), and [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html))</span></span> 
- <span data-ttu-id="36682-128">취약성 평가([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))</span><span class="sxs-lookup"><span data-stu-id="36682-128">Vulnerability assessment ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))</span></span>  

<span data-ttu-id="36682-129">시간이 지남에 따라 Security Center는 이러한 범주 내에서 파트너의 수를 확장하고 새 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-129">Over time, Security Center will expand the number of partners within these categories, and add new categories.</span></span> 

## <a name="deploy-a-partner-solution"></a><span data-ttu-id="36682-130">파트너 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="36682-130">Deploy a partner solution</span></span>

<span data-ttu-id="36682-131">정의한 Azure 환경 및 보안 정책의 설정에 따라 Security Center에서는 파트너 솔루션을 배포하도록 권장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-131">Based on the setup of your Azure environment and the security policy you defined, Security Center might recommend that you deploy a partner solution.</span></span> <span data-ttu-id="36682-132">Security Center 권장 사항은 파트너 솔루션을 선택하고 설치하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-132">The Security Center recommendation guides you through the process of selecting and installing a partner solution.</span></span> <span data-ttu-id="36682-133">전반적인 배포 환경은 사용한 솔루션 및 파트너의 유형에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-133">The overall deployment experience might vary, depending on the type of solution and partner you use.</span></span> <span data-ttu-id="36682-134">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36682-134">For more information, see the following articles:</span></span>

- [<span data-ttu-id="36682-135">Endpoint Protection 설치</span><span class="sxs-lookup"><span data-stu-id="36682-135">Install endpoint protection</span></span>](security-center-install-endpoint-protection.md)
- [<span data-ttu-id="36682-136">웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="36682-136">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md)
- [<span data-ttu-id="36682-137">차세대 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="36682-137">Add a next-generation firewall</span></span>](security-center-add-next-generation-firewall.md)
- [<span data-ttu-id="36682-138">취약점 평가 설치되지 않음</span><span class="sxs-lookup"><span data-stu-id="36682-138">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a><span data-ttu-id="36682-139">파트너 솔루션 관리</span><span class="sxs-lookup"><span data-stu-id="36682-139">Manage partner solutions</span></span>

<span data-ttu-id="36682-140">배포 후에 솔루션의 상태에 대한 정보를 보고 기본 관리 작업을 수행하려면 **Security Center** 블레이드에서 **파트너 솔루션** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36682-140">After deployment, to view information about the health of the solution and perform basic management tasks, on the **Security Center** blade, select the **Partner solutions** option.</span></span> <span data-ttu-id="36682-141">Security Center에서 파트너 솔루션을 관리하는 방법에 대한 자세한 내용은 [Azure Security Center로 파트너 솔루션 모니터링](security-center-partner-solutions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36682-141">For more information about managing partner solutions in Security Center, see [Monitor partner solutions with Azure Security Center](security-center-partner-solutions.md).</span></span>

![파트너 통합](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> <span data-ttu-id="36682-143">Symantec Endpoint Protection 지원은 검색으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="36682-143">Symantec endpoint protection support is limited to discovery.</span></span> <span data-ttu-id="36682-144">상태 경고는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-144">No health alerts are available.</span></span>
>

## <a name="see-also"></a><span data-ttu-id="36682-145">참고 항목</span><span class="sxs-lookup"><span data-stu-id="36682-145">See also</span></span>

<span data-ttu-id="36682-146">이 문서에서는 Azure Security Center에서 파트너 솔루션을 통합하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-146">In this article, you learned how to integrate partner solutions in Azure Security Center.</span></span> <span data-ttu-id="36682-147">Security Center에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36682-147">To learn more about Security Center, see the following articles:</span></span>

* [<span data-ttu-id="36682-148">Security Center 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="36682-148">Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="36682-149">Security Center에서 보안 경고 관리 및 응답</span><span class="sxs-lookup"><span data-stu-id="36682-149">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="36682-150">Azure Security Center에서 유형별 보안 경고</span><span class="sxs-lookup"><span data-stu-id="36682-150">Security alerts by type in Security Center</span></span>](security-center-alerts-type.md)
* <span data-ttu-id="36682-151">[Security Center에서 보안 상태 모니터링](security-center-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="36682-151">[Security health monitoring in Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="36682-152">Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="36682-152">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="36682-153">[Security Center를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="36682-153">[Monitoring partner solutions with Security Center](security-center-partner-solutions.md).</span></span> <span data-ttu-id="36682-154">파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="36682-154">Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="36682-155">[Azure Security Center FAQ](security-center-faq.md)</span><span class="sxs-lookup"><span data-stu-id="36682-155">[Azure Security Center FAQs](security-center-faq.md).</span></span> <span data-ttu-id="36682-156">서비스 사용에 관한 질문과 대답에 대한 답을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="36682-156">Get answers to frequently asked questions about using the service.</span></span>
* <span data-ttu-id="36682-157">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)</span><span class="sxs-lookup"><span data-stu-id="36682-157">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="36682-158">Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="36682-158">Find blog posts about Azure security and compliance.</span></span>
