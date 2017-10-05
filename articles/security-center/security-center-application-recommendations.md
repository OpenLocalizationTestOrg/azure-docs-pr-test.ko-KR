---
title: "Azure Security Center에서 응용 프로그램 보호 | Microsoft Docs"
description: "이 문서에서는 Azure 응용 프로그램을 보호하고 보안 정책을 준수하는 데 도움이 되는 Azure 보안 센터의 권장 사항에 대해 설명합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: dfc7d14b95082842ba658bd94b15c8191ee5dca3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a><span data-ttu-id="e7c83-103">Azure 보안 센터에서 응용 프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="e7c83-103">Protecting your applications in Azure Security Center</span></span>
<span data-ttu-id="e7c83-104">Azure 보안 센터에서는 Azure 리소스의 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="e7c83-105">보안 센터가 잠재적인 보안 취약점을 식별하는 경우 필요한 컨트롤을 구성하는 과정을 안내하는 권장 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="e7c83-106">이러한 권장 사항은 가상 컴퓨터(VM), 네트워킹, SQL, 응용 프로그램 등의 Azure 리소스 유형에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="e7c83-107">이 문서에서는 응용 프로그램에 적용되는 권장 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-107">This article addresses recommendations that apply to applications.</span></span>  <span data-ttu-id="e7c83-108">응용 프로그램 권장 사항은 웹 응용 프로그램 방화벽의 배포에 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-108">Application recommendations center around deployment of a web application firewall.</span></span>  <span data-ttu-id="e7c83-109">아래 테이블을 참조로 사용하여 제공되는 응용 프로그램 권장 사항을 이해하고 각 권장 사항을 적용할 경우 어떻게 되는지 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-109">Use the table below as a reference to help you understand the available application recommendations and what each one does if you apply it.</span></span>

## <a name="available-application-recommendations"></a><span data-ttu-id="e7c83-110">제공되는 응용 프로그램 권장 사항</span><span class="sxs-lookup"><span data-stu-id="e7c83-110">Available application recommendations</span></span>
| <span data-ttu-id="e7c83-111">권장 사항</span><span class="sxs-lookup"><span data-stu-id="e7c83-111">Recommendation</span></span> | <span data-ttu-id="e7c83-112">설명</span><span class="sxs-lookup"><span data-stu-id="e7c83-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e7c83-113">웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="e7c83-113">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md) |<span data-ttu-id="e7c83-114">웹 끝점에 WAF(웹 응용 프로그램 방화벽)를 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-114">Recommends that you deploy a web application firewall (WAF) for web endpoints.</span></span> <span data-ttu-id="e7c83-115">공개 인바운드 웹 포트(80,443)으로 연결된 네트워크 보안 그룹에 있는 모든 공용 연결 IP(인스턴스 수준 IP 또는 부하 분산된 IP)에 대해 WAF 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-115">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span></br></br><span data-ttu-id="e7c83-116">Security Center에서는 가상 컴퓨터와 App Service 환경에 있는 웹 응용 프로그램을 대상으로 한 공격을 방어할 수 있도록 WAF를 프로비전할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-116">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="e7c83-117">ASE(App Service 환경)는 Azure App Service의 [프리미엄](https://azure.microsoft.com/pricing/details/app-service/) 서비스 계획 옵션으로, Azure App Service 앱의 안전한 실행을 위해 완전히 격리된 전용 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-117">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="e7c83-118">ASE에 대한 자세한 내용을 보려면 [App Service Environment 설명서](../app-service/app-service-app-service-environments-readme.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7c83-118">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span></br></br><span data-ttu-id="e7c83-119">기존 WAF 배포에 이러한 응용 프로그램을 추가하여 보안 센터에서 여러 웹 응용 프로그램을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-119">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span> |
| [<span data-ttu-id="e7c83-120">응용 프로그램 보호 완료</span><span class="sxs-lookup"><span data-stu-id="e7c83-120">Finalize application protection</span></span>](security-center-add-web-application-firewall.md#finalize-application-protection) |<span data-ttu-id="e7c83-121">WAF 구성을 완료하려면 트래픽 경로가 WAF 어플라이언스로 전환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-121">To complete the configuration of a WAF, traffic must be rerouted to the WAF appliance.</span></span> <span data-ttu-id="e7c83-122">이 권장 사항을 따르면 필요한 설정 변경이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-122">Following this recommendation completes the necessary setup changes.</span></span> |

## <a name="see-also"></a><span data-ttu-id="e7c83-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e7c83-123">See also</span></span>
<span data-ttu-id="e7c83-124">다른 Azure 리소스 유형에 적용되는 권장 사항에 대해 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7c83-124">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="e7c83-125">Azure 보안 센터에서 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="e7c83-125">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="e7c83-126">Azure 보안 센터에서 네트워크 보호</span><span class="sxs-lookup"><span data-stu-id="e7c83-126">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)
* [<span data-ttu-id="e7c83-127">Azure 보안 센터에서 Azure SQL 서비스 보호</span><span class="sxs-lookup"><span data-stu-id="e7c83-127">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="e7c83-128">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7c83-128">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e7c83-129">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-129">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e7c83-130">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-130">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e7c83-131">[Azure 보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e7c83-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
