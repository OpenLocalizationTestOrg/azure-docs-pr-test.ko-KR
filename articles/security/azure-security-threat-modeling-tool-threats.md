---
title: "-Microsoft 위협 모델링 도구-aaaThreats Azure | Microsoft Docs"
description: "Hello Microsoft 위협 모델링 도구에 대 한 위협 범주 페이지에서 노출 하는 모든 범주를 포함 하 위협 생성 됩니다."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a><span data-ttu-id="d669b-103">Microsoft 위협 모델링 도구 위협</span><span class="sxs-lookup"><span data-stu-id="d669b-103">Microsoft Threat Modeling Tool threats</span></span>

<span data-ttu-id="d669b-104">hello 위협 모델링 도구에는 hello Microsoft SDL Security Development Lifecycle ()의 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="d669b-105">소프트웨어를 통해 tooidentify 만드는 일 및 상대적으로 간편 하 고 비용 효율적인 tooresolve 있을 때 잠재적 보안 문제를 조기에 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="d669b-106">결과적으로, 개발의 hello 총 비용이 크게 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="d669b-107">또한 hello 도구를 보다 쉽게 위협 모델링에 대 한 모든 개발자가 작성 및 위협 모델 분석에 명확한 지침을 제공 하 여을 염두에 비보안 전문가 함께 설계 합니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span>

> <span data-ttu-id="d669b-108">Hello 방문  **[위협 모델링 도구](./azure-security-threat-modeling-tool.md)**  tooget 오늘 시작!</span><span class="sxs-lookup"><span data-stu-id="d669b-108">Visit hello **[Threat Modeling Tool](./azure-security-threat-modeling-tool.md)** tooget started today!</span></span>

<span data-ttu-id="d669b-109">위협 모델링 도구 hello hello 아래 셰이프와 같은 특정 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-109">hello Threat Modeling Tool helps you answer certain questions, such as hello ones below:</span></span>

* <span data-ttu-id="d669b-110">공격자가 수 hello 인증 데이터를 변경 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d669b-110">How can an attacker change hello authentication data?</span></span>
* <span data-ttu-id="d669b-111">공격자는 hello 사용자 프로필 데이터를 읽을 수 있으면 hello 영향 이란?</span><span class="sxs-lookup"><span data-stu-id="d669b-111">What is hello impact if an attacker can read hello user profile data?</span></span>
* <span data-ttu-id="d669b-112">Toohello 사용자 프로필 데이터베이스에 있어야 하는 경우 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="d669b-112">What happens if access is denied toohello user profile database?</span></span>

## <a name="stride-model"></a><span data-ttu-id="d669b-113">STRIDE 모델</span><span class="sxs-lookup"><span data-stu-id="d669b-113">STRIDE model</span></span>

<span data-ttu-id="d669b-114">이러한 종류의 뾰족한 질문, 다양 한 유형의 위협 분류 되 고 간소화 하 Microsoft 사용 하 여 hello STRIDE 모델을 작성 하는 toobetter 도움말 hello 전반적인 보안 대화입니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-114">toobetter help you formulate these kinds of pointed questions, Microsoft uses hello STRIDE model, which categorizes different types of threats and simplifies hello overall security conversations.</span></span>

| <span data-ttu-id="d669b-115">Category</span><span class="sxs-lookup"><span data-stu-id="d669b-115">Category</span></span> | <span data-ttu-id="d669b-116">설명</span><span class="sxs-lookup"><span data-stu-id="d669b-116">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="d669b-117">**스푸핑**</span><span class="sxs-lookup"><span data-stu-id="d669b-117">**Spoofing**</span></span> | <span data-ttu-id="d669b-118">사용자 이름 및 암호와 같은 다른 사용자의 인증 정보를 불법적으로 액세스하고 사용하는 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-118">Involves illegally accessing and then using another user's authentication information, such as username and password</span></span> |
| <span data-ttu-id="d669b-119">**변조**</span><span class="sxs-lookup"><span data-stu-id="d669b-119">**Tampering**</span></span> | <span data-ttu-id="d669b-120">Hello 악성 데이터 수정을 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-120">Involves hello malicious modification of data.</span></span> <span data-ttu-id="d669b-121">예로 무단된 변경한 hello 인터넷 등의 개방형 네트워크를 통한 두 컴퓨터 사이 전달 되는 데이터베이스 및 데이터를 변경할 때 hello에 보관 된 같은 toopersistent 데이터</span><span class="sxs-lookup"><span data-stu-id="d669b-121">Examples include unauthorized changes made toopersistent data, such as that held in a database, and hello alteration of data as it flows between two computers over an open network, such as hello Internet</span></span> |
| <span data-ttu-id="d669b-122">**거부**</span><span class="sxs-lookup"><span data-stu-id="d669b-122">**Repudiation**</span></span> | <span data-ttu-id="d669b-123">상대방은 모든 방식으로 tooprove 그렇지 않으면 없이 작업 수행을 거부 된 사용자와 연결 된-사용자가 없는 hello 기능 tootrace 금지 hello 작업 시스템에서 잘못 된 작업을 수행 하는 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-123">Associated with users who deny performing an action without other parties having any way tooprove otherwise—for example, a user performs an illegal operation in a system that lacks hello ability tootrace hello prohibited operations.</span></span> <span data-ttu-id="d669b-124">Non-repudiation 시스템 toocounter 거부 위협의 toohello 능력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-124">Non-Repudiation refers toohello ability of a system toocounter repudiation threats.</span></span> <span data-ttu-id="d669b-125">예를 들어 항목을 구입 하는 사용자를 받 때 hello 항목에 대 한 toosign이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-125">For example, a user who purchases an item might have toosign for hello item upon receipt.</span></span> <span data-ttu-id="d669b-126">사용 하 여 hello hello 사용자가 hello 패키지를 수신 하는 증명 정보로 수신을 서명 그런 다음 공급 업체 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-126">hello vendor can then use hello signed receipt as evidence that hello user did receive hello package</span></span> |
| <span data-ttu-id="d669b-127">**정보 공개**</span><span class="sxs-lookup"><span data-stu-id="d669b-127">**Information Disclosure**</span></span> | <span data-ttu-id="d669b-128">Toohave 액세스 tooit 해서는 안 되는 정보 tooindividuals hello 노출 포함-예를 들어 사용자가 tooread 없었기 하는 파일의 hello 기능 액세스 권한이 부여 to, 또는 hello 두 컴퓨터 간에 전송 되는 침입자가 tooread 데이터의 기능</span><span class="sxs-lookup"><span data-stu-id="d669b-128">Involves hello exposure of information tooindividuals who are not supposed toohave access tooit—for example, hello ability of users tooread a file that they were not granted access to, or hello ability of an intruder tooread data in transit between two computers</span></span> |
| <span data-ttu-id="d669b-129">**서비스 거부**</span><span class="sxs-lookup"><span data-stu-id="d669b-129">**Denial of Service**</span></span> | <span data-ttu-id="d669b-130">서비스 거부 (dos) 공격 서비스 toovalid 사용자의 거부-예를 들어 함으로써 웹 서버 일시적으로 사용할 수 없거나 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-130">Denial of service (DoS) attacks deny service toovalid users—for example, by making a Web server temporarily unavailable or unusable.</span></span> <span data-ttu-id="d669b-131">특정 유형의 DoS 공격 으로부터 보호 해야 tooimprove 시스템 가용성 및 안정성을 간단히 위협</span><span class="sxs-lookup"><span data-stu-id="d669b-131">You must protect against certain types of DoS threats simply tooimprove system availability and reliability</span></span> |
| <span data-ttu-id="d669b-132">**권한 상승**</span><span class="sxs-lookup"><span data-stu-id="d669b-132">**Elevation of Privilege**</span></span> | <span data-ttu-id="d669b-133">권한 없는 사용자 권한 있는 액세스 권한을 얻는 함으로써에 충분 한 액세스 toocompromise 여부나 한 hello 전체 시스템을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-133">An unprivileged user gains privileged access and thereby has sufficient access toocompromise or destroy hello entire system.</span></span> <span data-ttu-id="d669b-134">권한 상승 위협 경우 공격자가 효과적으로 모든 시스템 방어에 침투 하 고 있는 자체를 위험한 상황을 실제로 hello 신뢰할 수 있는 시스템의 일부가 포함</span><span class="sxs-lookup"><span data-stu-id="d669b-134">Elevation of privilege threats include those situations in which an attacker has effectively penetrated all system defenses and become part of hello trusted system itself, a dangerous situation indeed</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d669b-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d669b-135">Next steps</span></span>

<span data-ttu-id="d669b-136">너무 계속**[위협 모델링 도구 완화](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn hello 다양 한 방법으로 Azure는 이러한 위협을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d669b-136">Proceed too**[Threat Modeling Tool Mitigations](./azure-security-threat-modeling-tool-mitigations.md)** toolearn hello different ways you can mitigate these threats with Azure.</span></span>
