---
title: "Microsoft Azure에서 개인 데이터 aaaProtect | Microsoft Docs"
description: "먼저 문서는 일련의 문서 toohelp 사용 하 여 Azure tooprotect 개인 데이터"
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
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="002e9-103">Microsoft Azure에서 개인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="002e9-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="002e9-104">이 문서에서는 일련의 데 도움이 되는 문서를 소개 Azure 보안 기술 및 서비스 tooprotect 개인 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="002e9-105">이는 많은 기업 및 업계의 규정 준수 및 거버넌스 이니셔티브의 핵심 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="002e9-106">hello 시나리오 문제 문과 회사 목표 여기에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="002e9-107">시나리오 및 문제 설명</span><span class="sxs-lookup"><span data-stu-id="002e9-107">Scenario and problem statement</span></span>

<span data-ttu-id="002e9-108">Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="002e9-109">toosupport 이탈리아를 더 작은 여러 크루즈 줄 획득 이러한 노력 독일, 덴마크 및 hello 영국</span><span class="sxs-lookup"><span data-stu-id="002e9-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="002e9-110">hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="002e9-111">이 수 직원 또는 고객 정보가 다음과 같은 포함</span><span class="sxs-lookup"><span data-stu-id="002e9-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="002e9-112">주소</span><span class="sxs-lookup"><span data-stu-id="002e9-112">addresses</span></span>
- <span data-ttu-id="002e9-113">전화 번호</span><span class="sxs-lookup"><span data-stu-id="002e9-113">phone numbers</span></span>
- <span data-ttu-id="002e9-114">납세자 번호</span><span class="sxs-lookup"><span data-stu-id="002e9-114">tax identification numbers</span></span>
- <span data-ttu-id="002e9-115">의료 보험 정보</span><span class="sxs-lookup"><span data-stu-id="002e9-115">medical information</span></span>
- <span data-ttu-id="002e9-116">신용 카드 정보</span><span class="sxs-lookup"><span data-stu-id="002e9-116">credit card information</span></span>

<span data-ttu-id="002e9-117">hello 회사 필요로 하는 데이터 액세스 가능한 toothose 부서 이와 동시에 직원 및 고객 데이터의 hello 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="002e9-118">액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="002e9-119">회사 목표</span><span class="sxs-lookup"><span data-stu-id="002e9-119">Company goals</span></span> 

- <span data-ttu-id="002e9-120">개인 데이터가 포함된 데이터 원본은 클라우드 저장소에 있을 때 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="002e9-121">한 위치 tooanother에서 전송 되는 개인 데이터에 전송 하는 동안 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="002e9-122">Hello 데이터 hello 가상 네트워크 또는 인터넷 hello에서 hello 회사 데이터 센터와 hello Azure 클라우드 간의 여행는 경우에 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="002e9-123">강력한 ID 관리 및 액세스 제어 기술을 통해 무단 액세스로부터 개인 데이터의 기밀성과 무결성을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="002e9-124">개인 데이터는 취약성 및 위협에 대해 모니터링하여 데이터 위반을 통한 노출로부터 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="002e9-125">hello 저장 하거나 개인 데이터를 전송 하는 Azure 서비스의 보안 상태 평가 tooidentify 기회 toobetter 개인 데이터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="002e9-126">데이터 보호 지침</span><span class="sxs-lookup"><span data-stu-id="002e9-126">Data protection guidance</span></span>

<span data-ttu-id="002e9-127">다음 문서는 hello 위에 나열 된 hello 개인 데이터 보호 목표를 달성 하는 데 도움이 되는 기술 방법 tooguidance 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="002e9-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="002e9-128">Azure 암호화 기술</span><span class="sxs-lookup"><span data-stu-id="002e9-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="002e9-129">Azure 암호화 기술</span><span class="sxs-lookup"><span data-stu-id="002e9-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="002e9-130">Azure ID 및 액세스 기술</span><span class="sxs-lookup"><span data-stu-id="002e9-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="002e9-131">Azure 네트워크 보안 기술</span><span class="sxs-lookup"><span data-stu-id="002e9-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="002e9-132">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="002e9-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="002e9-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="002e9-133">Next steps</span></span>

- [<span data-ttu-id="002e9-134">Azure 보안 정보 사이트</span><span class="sxs-lookup"><span data-stu-id="002e9-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="002e9-135">Microsoft 보안 센터</span><span class="sxs-lookup"><span data-stu-id="002e9-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="002e9-136">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="002e9-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="002e9-137">Azure 보안 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="002e9-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="002e9-138">Azure.com 블로그 - 보안</span><span class="sxs-lookup"><span data-stu-id="002e9-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
