---
title: "aaaProtecting Azure 보안 센터에서 응용 프로그램 | Microsoft Docs"
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
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a><span data-ttu-id="ad108-103">Azure 보안 센터에서 응용 프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="ad108-103">Protecting your applications in Azure Security Center</span></span>
<span data-ttu-id="ad108-104">Azure 보안 센터 리소스를 Azure의 hello 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="ad108-105">보안 센터 잠재적인 보안 문제를 식별 하는 경우 필요한 hello 컨트롤 구성 hello 과정을 안내 하는 권장 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="ad108-106">권장 사항이 적용 tooAzure 리소스 종류: 가상 컴퓨터 (Vm), 네트워킹, SQL, 및 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="ad108-107">이 문서에서는 tooapplications 적용 되는 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-107">This article addresses recommendations that apply tooapplications.</span></span>  <span data-ttu-id="ad108-108">응용 프로그램 권장 사항은 웹 응용 프로그램 방화벽의 배포에 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-108">Application recommendations center around deployment of a web application firewall.</span></span>  <span data-ttu-id="ad108-109">Hello 사용할 수 있는 응용 프로그램 권장 사항 및 각 용도 적용 하는 경우 참조 toohelp으로 아래 hello 테이블 사용 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-109">Use hello table below as a reference toohelp you understand hello available application recommendations and what each one does if you apply it.</span></span>

## <a name="available-application-recommendations"></a><span data-ttu-id="ad108-110">제공되는 응용 프로그램 권장 사항</span><span class="sxs-lookup"><span data-stu-id="ad108-110">Available application recommendations</span></span>
| <span data-ttu-id="ad108-111">권장 사항</span><span class="sxs-lookup"><span data-stu-id="ad108-111">Recommendation</span></span> | <span data-ttu-id="ad108-112">설명</span><span class="sxs-lookup"><span data-stu-id="ad108-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ad108-113">웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="ad108-113">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md) |<span data-ttu-id="ad108-114">웹 끝점에 WAF(웹 응용 프로그램 방화벽)를 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-114">Recommends that you deploy a web application firewall (WAF) for web endpoints.</span></span> <span data-ttu-id="ad108-115">공개 인바운드 웹 포트(80,443)으로 연결된 네트워크 보안 그룹에 있는 모든 공용 연결 IP(인스턴스 수준 IP 또는 부하 분산된 IP)에 대해 WAF 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-115">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span></br></br><span data-ttu-id="ad108-116">보안 센터 앱 서비스 환경 및 가상 컴퓨터에서 웹 응용 프로그램을 대상으로 하는 공격 방어 WAF toohelp 구축 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-116">Security Center recommends that you provision a WAF toohelp defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="ad108-117">ASE(App Service 환경)는 Azure App Service의 [프리미엄](https://azure.microsoft.com/pricing/details/app-service/) 서비스 계획 옵션으로, Azure App Service 앱의 안전한 실행을 위해 완전히 격리된 전용 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-117">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="ad108-118">toolearn ASE에 대 한 자세한 참조 hello [앱 서비스 환경 설명서](../app-service/app-service-app-service-environments-readme.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-118">toolearn more about ASE, see hello [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span></br></br><span data-ttu-id="ad108-119">이러한 응용 프로그램 tooyour 기존 WAF 배포를 추가 하 여 보안 센터에서 여러 웹 응용 프로그램을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-119">You can protect multiple web applications in Security Center by adding these applications tooyour existing WAF deployments.</span></span> |
| [<span data-ttu-id="ad108-120">응용 프로그램 보호 완료</span><span class="sxs-lookup"><span data-stu-id="ad108-120">Finalize application protection</span></span>](security-center-add-web-application-firewall.md#finalize-application-protection) |<span data-ttu-id="ad108-121">toocomplete hello 구성을 WAF, 트래픽 다시 라우팅된 toohello WAF 기기 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-121">toocomplete hello configuration of a WAF, traffic must be rerouted toohello WAF appliance.</span></span> <span data-ttu-id="ad108-122">이렇게 hello 필요한 설정 변경을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-122">Following this recommendation completes hello necessary setup changes.</span></span> |

## <a name="see-also"></a><span data-ttu-id="ad108-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ad108-123">See also</span></span>
<span data-ttu-id="ad108-124">tooother Azure 리소스 유형에 적용 되는 권장 사항에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-124">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="ad108-125">Azure 보안 센터에서 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="ad108-125">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="ad108-126">Azure 보안 센터에서 네트워크 보호</span><span class="sxs-lookup"><span data-stu-id="ad108-126">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)
* [<span data-ttu-id="ad108-127">Azure 보안 센터에서 Azure SQL 서비스 보호</span><span class="sxs-lookup"><span data-stu-id="ad108-127">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="ad108-128">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-128">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ad108-129">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-129">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ad108-130">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-130">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ad108-131">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="ad108-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
