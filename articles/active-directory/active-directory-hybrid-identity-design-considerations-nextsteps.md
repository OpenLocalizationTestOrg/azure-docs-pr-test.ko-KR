---
title: "다음 단계 aaaAzure Active Directory 하이브리드 identity 디자인 고려 사항-| Microsoft Docs"
description: "개요 및 hello 하이브리드 Id 디자인 고려 사항 가이드를 읽은 후 다음 단계"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 02d48768-ea9e-4bfe-ae54-b54c4bd0a789
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7100eaaf61a7b3b7d38a381f6bb9d8b82677c352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations--next-steps"></a><span data-ttu-id="12e8f-103">Azure Active Directory 하이브리드 ID 디자인 고려 사항 - 다음 단계</span><span class="sxs-lookup"><span data-stu-id="12e8f-103">Azure Active Directory hybrid identity design considerations- next steps</span></span>
<span data-ttu-id="12e8f-104">이제 요구 사항을 정의 하 고 모바일 장치 관리 솔루션에 대 한 모든 hello 옵션을 검토를 완료 하면 준비 tootake hello 배포 다음 단계를 사용자에 대 한 오른쪽 및 조직 인프라를 지 원하는 hello 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-104">Now that you’ve completed defining your requirements and examining all hello options for your mobile device management solution, you’re ready tootake hello next steps for deploying hello supporting infrastructure that’s right for you and your organization.</span></span>

## <a name="hybrid-identity-solutions"></a><span data-ttu-id="12e8f-105">하이브리드 ID 솔루션</span><span class="sxs-lookup"><span data-stu-id="12e8f-105">Hybrid identity solutions</span></span>
<span data-ttu-id="12e8f-106">-사용자의 요구에 맞는 구체적인 솔루션 시나리오를 활용 하는 좋은 방법 tooreview 및 모바일 장치 관리 인프라 배포의 세부 정보 hello에 대 한 계획.</span><span class="sxs-lookup"><span data-stu-id="12e8f-106">-Leveraging specific solution scenarios that fit your needs is a great way tooreview and plan for hello details of deploying a mobile device management infrastructure.</span></span> <span data-ttu-id="12e8f-107">다음 솔루션 hello 일부의 hello 가장 일반적인 모바일 장치 관리 시나리오를 간략히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-107">hello following solutions outline several of hello most common mobile device management scenarios:</span></span>

* <span data-ttu-id="12e8f-108">hello [엔터프라이즈 환경 솔루션에서 모바일 장치 및 Pc 관리](https://technet.microsoft.com/library/dn582037.aspx) microsoft hello 클라우드로 온-프레미스 System Center 2012 Configuration Manager 인프라를 확장 하 여 모바일 장치를 관리할 수 있습니다 Intune 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-108">hello [manage mobile devices and PCs in enterprise environments solution](https://technet.microsoft.com/library/dn582037.aspx) helps you manage mobile devices by extending your on-premises System Center 2012 Configuration Manager infrastructure into hello cloud with Microsoft Intune.</span></span> <span data-ttu-id="12e8f-109">이 하이브리드 인프라를 사용하면 중간 규모 및 대규모 환경에서 IT 전문가가 BYOD 및 원격 액세스를 사용하면서 관리의 복잡성을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-109">This hybrid infrastructure helps IT Pros in medium and large environments enable BYOD and remote access while reducing administrative complexity.</span></span>
* <span data-ttu-id="12e8f-110">hello [Configuration Manager 2007 솔루션에 대 한 모바일 장치 관리](https://technet.microsoft.com/library/dn508400.aspx) 인프라가 System Center Configuration Manager 2007 때 모바일 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-110">hello [managing mobile devices for Configuration Manager 2007 solution](https://technet.microsoft.com/library/dn508400.aspx) helps you manage mobile devices when your infrastructure rests on a System Center Configuration Manager 2007.</span></span> <span data-ttu-id="12e8f-111">이 솔루션에서는 다음 Microsoft Intune을 실행 하 고 MDM 기능을 활용할 수 있도록 System Center 2012 Configuration Manager를 실행 하 여 단일 서버 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-111">This solution shows you how tooset up a single server running System Center 2012 Configuration Manager so you can then run Microsoft Intune and take advantage of its MDM ability.</span></span>
* <span data-ttu-id="12e8f-112">hello [소규모 환경 솔루션에서 모바일 장치 관리](https://technet.microsoft.com/library/dn715906.aspx) toosupport mdm. 해야 하는 소규모 기업을 위한 것은</span><span class="sxs-lookup"><span data-stu-id="12e8f-112">hello [managing mobile devices in small environments solution](https://technet.microsoft.com/library/dn715906.aspx) is intended for small businesses that need toosupport MDM.</span></span> <span data-ttu-id="12e8f-113">설명 방법을 toouse Microsoft Intune tooextend 현재 인프라 toosupport 모바일 장치 관리 및 BYOD 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-113">It explains how toouse Microsoft Intune tooextend your current infrastructure toosupport mobile device management and BYOD.</span></span> <span data-ttu-id="12e8f-114">이 솔루션에서는 hello 독립 실행형 로컬 서버가 없는 클라우드 전용 구성에서에서 Microsoft Intune을 사용 하 여 지원 되는 가장 간단한 시나리오를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-114">This solution describes hello simplest scenario supported for using Microsoft Intune in a standalone, cloud-only configuration with no local servers.</span></span>

## <a name="hybrid-identity-documentation"></a><span data-ttu-id="12e8f-115">하이브리드 ID 설명서</span><span class="sxs-lookup"><span data-stu-id="12e8f-115">Hybrid identity documentation</span></span>
<span data-ttu-id="12e8f-116">개념 및 절차 계획, 배포 및 관리 콘텐츠는 모바일 장치 관리 솔루션을 구현할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-116">Conceptual and procedural planning, deployment, and administration content are useful when implementing your mobile device management solution:</span></span>

* <span data-ttu-id="12e8f-117">[Microsoft System Center](https://technet.microsoft.com/library/cc507089.aspx) 솔루션은 IT 직원이 관리하기 쉬운 시스템을 구축하고 작업을 자동화할 수 있도록 인프라, 정책, 프로세스 및 모범 사례에 대한 지식을 파악하고 집계하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-117">[Microsoft System Center](https://technet.microsoft.com/library/cc507089.aspx) solutions can help you capture and aggregate knowledge about your infrastructure, policies, processes, and best practices so that your IT staff can build manageable systems and automate operations.</span></span>
* <span data-ttu-id="12e8f-118">[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) 컴퓨터 및 모바일 장치 및 toosecure toomanage 하는 데 도움이 되는 클라우드 기반 장치 관리 서비스는 회사의 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-118">[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) is a cloud-based device management service that helps you toomanage your computers and mobile devices and toosecure your company’s information.</span></span>
* <span data-ttu-id="12e8f-119">[Office 365 용 MDM](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) 연결된 tooyour Office 365 조직에 있을 때 toomanage 및 안전한 모바일 장치 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-119">[MDM for Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) allows you toomanage and secure mobile devices when they're connected tooyour Office 365 organization.</span></span> <span data-ttu-id="12e8f-120">분실 하거나 도난 당한 경우 Office 365 tooset 장치 보안 정책 및 액세스 규칙 toowipe 모바일 장치에 대 한 MDM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e8f-120">You can use MDM for Office 365 tooset device security policies and access rules, and toowipe mobile devices if they’re lost or stolen.</span></span>

## <a name="hybrid-identity-resources"></a><span data-ttu-id="12e8f-121">하이브리드 ID 리소스</span><span class="sxs-lookup"><span data-stu-id="12e8f-121">Hybrid identity resources</span></span>
<span data-ttu-id="12e8f-122">모니터링 hello 다음 리소스 종종 한 hello 최신 뉴스 및 모바일 장치 관리 솔루션에 업데이트:</span><span class="sxs-lookup"><span data-stu-id="12e8f-122">Monitoring hello following resources often provides hello latest news and updates on mobile device management solutions:</span></span>

* [<span data-ttu-id="12e8f-123">Microsoft Enterprise Mobility 블로그</span><span class="sxs-lookup"><span data-stu-id="12e8f-123">Microsoft Enterprise Mobility blog</span></span>](http://blogs.technet.com/b/enterprisemobility/)
* [<span data-ttu-id="12e8f-124">Microsoft의 hello 클라우드 블로그</span><span class="sxs-lookup"><span data-stu-id="12e8f-124">Microsoft In hello Cloud blog</span></span>](http://blogs.technet.com/b/in_the_cloud/)
* [<span data-ttu-id="12e8f-125">Microsoft Intune 블로그</span><span class="sxs-lookup"><span data-stu-id="12e8f-125">Microsoft Intune blog</span></span>](http://blogs.technet.com/b/microsoftintune/)
* [<span data-ttu-id="12e8f-126">Microsoft System Center Configuration Manager 블로그</span><span class="sxs-lookup"><span data-stu-id="12e8f-126">Microsoft System Center Configuration Manager blog</span></span>](http://blogs.technet.com/b/configurationmgr/)
* [<span data-ttu-id="12e8f-127">Microsoft System Center Configuration Manager 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="12e8f-127">Microsoft System Center Configuration Manager Team blog</span></span>](http://blogs.technet.com/b/configmgrteam/)

## <a name="see-also"></a><span data-ttu-id="12e8f-128">참고 항목</span><span class="sxs-lookup"><span data-stu-id="12e8f-128">See also</span></span>
[<span data-ttu-id="12e8f-129">디자인 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="12e8f-129">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

