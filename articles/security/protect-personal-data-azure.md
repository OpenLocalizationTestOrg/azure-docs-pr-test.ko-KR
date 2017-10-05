---
title: "Microsoft Azure에서 개인 데이터 보호 | Microsoft Docs"
description: "Azure를 사용하여 개인 데이터를 보호하는 데 도움이 되는 문서 시리즈의 첫 번째 문서입니다."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: dfb046374397c8a19672ce6b67741903fff6e178
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="113d9-103">Microsoft Azure에서 개인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="113d9-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="113d9-104">이 문서에서는 Azure 보안 기술 및 서비스를 사용하여 개인 데이터를 보호하는 데 도움이 되는 일련의 문서를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-104">This article introduces a series of articles that help you use Azure security technologies and services to protect personal data.</span></span> <span data-ttu-id="113d9-105">이는 많은 기업 및 업계의 규정 준수 및 거버넌스 이니셔티브의 핵심 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="113d9-106">여기에는 시나리오, 문제 설명 및 회사 목표가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-106">The scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="113d9-107">시나리오 및 문제 설명</span><span class="sxs-lookup"><span data-stu-id="113d9-107">Scenario and problem statement</span></span>

<span data-ttu-id="113d9-108">미국에 본사를 둔 대형 크루즈 회사는 영국 제도뿐만 아니라 지중해, 아드리아해 및 발트해 연안의 여정도 제공하도록 사업을 확장하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="113d9-109">이러한 노력을 지원하기 위해 이탈리아, 독일, 덴마크 및 영국에 기반을 둔 몇 개의 소형 크루즈 라인을 인수했습니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="113d9-110">회사에서 Microsoft Azure를 사용하여 클라우드에 회사 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="113d9-111">이 수 직원 또는 고객 정보가 다음과 같은 포함</span><span class="sxs-lookup"><span data-stu-id="113d9-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="113d9-112">주소</span><span class="sxs-lookup"><span data-stu-id="113d9-112">addresses</span></span>
- <span data-ttu-id="113d9-113">전화 번호</span><span class="sxs-lookup"><span data-stu-id="113d9-113">phone numbers</span></span>
- <span data-ttu-id="113d9-114">납세자 번호</span><span class="sxs-lookup"><span data-stu-id="113d9-114">tax identification numbers</span></span>
- <span data-ttu-id="113d9-115">의료 보험 정보</span><span class="sxs-lookup"><span data-stu-id="113d9-115">medical information</span></span>
- <span data-ttu-id="113d9-116">신용 카드 정보</span><span class="sxs-lookup"><span data-stu-id="113d9-116">credit card information</span></span>

<span data-ttu-id="113d9-117">회사는 데이터를 필요로 하는 해당 부서에 액세스할 수 있도록 하는 동안 직원 및 고객 데이터의 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="113d9-118">액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="113d9-119">회사 목표</span><span class="sxs-lookup"><span data-stu-id="113d9-119">Company goals</span></span> 

- <span data-ttu-id="113d9-120">개인 데이터가 포함된 데이터 원본은 클라우드 저장소에 있을 때 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="113d9-121">한 위치에서 다른 위치로 전송되는 개인 데이터는 전송 중에 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-121">Personal data that is transferred from one location to another is encrypted while in-transit.</span></span> <span data-ttu-id="113d9-122">데이터가 가상 네트워크에서 또는 기업 데이터 센터와 Azure 클라우드 사이의 인터넷에서 이동하는 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-122">This is true if the data is traveling across the virtual network or across the Internet between the corporate datacenter and the Azure cloud.</span></span>

- <span data-ttu-id="113d9-123">강력한 ID 관리 및 액세스 제어 기술을 통해 무단 액세스로부터 개인 데이터의 기밀성과 무결성을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="113d9-124">개인 데이터는 취약성 및 위협에 대해 모니터링하여 데이터 위반을 통한 노출로부터 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="113d9-125">개인 데이터를 저장하거나 전송하는 Azure 서비스의 보안 상태는 개인 데이터를 더 효율적으로 보호할 수 있는 기회를 식별하기 위해 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-125">The security state of Azure services that store or transmit personal data is assessed to identify opportunities to better protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="113d9-126">데이터 보호 지침</span><span class="sxs-lookup"><span data-stu-id="113d9-126">Data protection guidance</span></span>

<span data-ttu-id="113d9-127">다음 문서에는 위에서 나열된 개인 데이터 보호 목표를 달성하는 데 도움이 되는 기술적 사용 지침이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="113d9-127">The following articles contain technical how-to guidance that will help you attain the personal data protection goals listed above:</span></span>

- [<span data-ttu-id="113d9-128">Azure 암호화 기술</span><span class="sxs-lookup"><span data-stu-id="113d9-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="113d9-129">Azure 암호화 기술</span><span class="sxs-lookup"><span data-stu-id="113d9-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="113d9-130">Azure ID 및 액세스 기술</span><span class="sxs-lookup"><span data-stu-id="113d9-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="113d9-131">Azure 네트워크 보안 기술</span><span class="sxs-lookup"><span data-stu-id="113d9-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="113d9-132">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="113d9-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="113d9-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="113d9-133">Next steps</span></span>

- [<span data-ttu-id="113d9-134">Azure 보안 정보 사이트</span><span class="sxs-lookup"><span data-stu-id="113d9-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="113d9-135">Microsoft 보안 센터</span><span class="sxs-lookup"><span data-stu-id="113d9-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="113d9-136">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="113d9-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="113d9-137">Azure 보안 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="113d9-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="113d9-138">Azure.com 블로그 - 보안</span><span class="sxs-lookup"><span data-stu-id="113d9-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
