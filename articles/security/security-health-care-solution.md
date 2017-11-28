---
title: "aaaA 실무 가이드 toodesigning 보안 상태 Azure의 관리 솔루션 | Microsoft Docs"
description: " 이 문서는 tooimprove 보안 hello Azure 서비스와 기능을 사용 하 여 의료 솔루션에 대해 구성 하는 방법 이해 하도록 도와 줍니다. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 7e5b082d-dc9c-4d4f-b3f1-75edcdafbd8f
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/07/2017
ms.author: terrylan
ms.openlocfilehash: bf8812402c2181f033f5d71e1814fd1b4ee4fb2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="a-practical-guide-toodesigning-secure-health-care-solutions-in-azure"></a><span data-ttu-id="5900c-103">실제는 Azure에서 toodesigning 보안 의료 솔루션 가이드</span><span class="sxs-lookup"><span data-stu-id="5900c-103">A practical guide toodesigning secure health care solutions in Azure</span></span>
<span data-ttu-id="5900c-104">통합 보안 컨트롤 toomeet 준수 의무 사항이 도움이 되는 지침에 대 한 상태 업계 시작, 시스템 통합 업체가 (SIs), 독립 소프트웨어 공급 업체 (Isv) 및 이동 tooAzure를 고려 하는 조직이 의료 찾고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5900c-104">Health industry startups, system integrators (SIs), independent software vendors (ISVs), and healthcare organizations considering a move tooAzure are looking for guidance that helps them incorporate security controls toomeet their compliance obligations.</span></span>

<span data-ttu-id="5900c-105">[실무 가이드 tooDesigning Secure 의료 보험 솔루션 Microsoft Azure에서](https://aka.ms/azureindustrysecurity) 를 사용 하 여 솔루션 hello Azure 서비스 및 요구 사항에 따라 구성할 수 있는 기능에 대 한 보안을 개선 하는 방법을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5900c-105">[A Practical Guide tooDesigning Secure Health Care Solutions in Microsoft Azure](https://aka.ms/azureindustrysecurity) helps you understand how you can improve security for your solutions by using hello Azure services and features that you can configure based on your requirements.</span></span>
<span data-ttu-id="5900c-106">hello 콘텐츠는 세 가지 주요 부분으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5900c-106">hello content is divided into three major sections:</span></span>

1. <span data-ttu-id="5900c-107">위험 관리, 공동 책임, 정보 보안 관리 시스템 설정, 산업 및 지역 규정 이해 및 표준 운영 절차 설정을 포함하는 클라우드 기술을 사용하기 위한 고려 사항 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="5900c-107">Considerations guidance for using cloud technology, including risk management, shared responsibility, establishing an information security management system, understanding industry and local regulations, and establishing standard operating procedures.</span></span>
2. <span data-ttu-id="5900c-108">주요 보안 원칙을 둘 다 tooa 표준 정보 보안 관리 ISO 27001, 같은 표준 및 표준 개발 프로세스와 같은 Microsoft의 개발 수명 주기 SDL (Security)를 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="5900c-108">Key security principles that are both aligned tooa standard information security management standard, such as ISO 27001, and standard development processes, such as Microsoft’s Security Development Lifecycle (SDL).</span></span>
3. <span data-ttu-id="5900c-109">Hello 핵심 원칙 toouse 적용의 경우 솔루션에서 맞춤을 시연 함으로써 hello 솔루션에 대 한 요구 사항이 있는 정렬 된 toohello 정보 보안 관리 표준 관점을 설계 합니다.</span><span class="sxs-lookup"><span data-stu-id="5900c-109">Applying hello key principles toouse cases by demonstrating alignment from a solution architect perspective, where requirements for hello solutions are aligned toohello information security management standard.</span></span>

<span data-ttu-id="5900c-110">바라 [A 실무 가이드 tooDesigning Secure 의료 보험 솔루션](https://aka.ms/azureindustrysecurity) 유용한 질문이 나 제안 하는 경우 알려주세요 채로 아래 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5900c-110">We hope you find [A Practical Guide tooDesigning Secure Health Care Solutions](https://aka.ms/azureindustrysecurity) helpful and if you have any questions or suggestions, let us know by leaving a comment below.</span></span>
