---
title: "Cloud App discovery는 클라우드 응용 프로그램을 관리 되지 않는 aaaFinding | Microsoft Docs"
description: "찾기 및 Cloud App Discovery, hello 장점은 무엇입니까 및 작동 방식으로 응용 프로그램을 관리 하는 방법에 대 한 정보를 제공 합니다."
services: active-directory
keywords: "Cloud App Discovery, 응용 프로그램 관리"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="fa540-104">클라우드 앱 검색을 사용하여 관리되지 않은 클라우드 응용 프로그램 찾기</span><span class="sxs-lookup"><span data-stu-id="fa540-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="fa540-105">개요</span><span class="sxs-lookup"><span data-stu-id="fa540-105">Overview</span></span>
<span data-ttu-id="fa540-106">오늘날의 기업에서 IT 부서가 조직의 구성원이 사용 작업 toodo 한다고 된 모든 hello 클라우드 응용 프로그램의 인식 종종 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="fa540-107">쉽게 toosee 이유 관리자 toocorporate 데이터를 무단된 액세스, 가능한 데이터 누수 및 기타 보안 위험에 대 한 질문이 있을 경우합니다</span><span class="sxs-lookup"><span data-stu-id="fa540-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="fa540-108">인식이 부족하여 이러한 보안 위험을 다루는 계획 수립이 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="fa540-109">Cloud App Discovery는 조직의 hello 사용자에서 사용 하 고 toodiscover 클라우드 응용 프로그램 수 있는 Azure AD (Active Directory) Premium의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="fa540-110">**클라우드 앱 검색으로 다음을 할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="fa540-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="fa540-111">Hello 클라우드 응용 프로그램을 사용 하 고 찾아 해당 사용 사용자 수, 트래픽 양 또는 웹 요청 toohello 응용 프로그램의 수를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="fa540-112">응용 프로그램을 사용 하는 hello 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="fa540-113">오프라인 분석을 위해 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="fa540-114">IT 제어에서 이러한 응용 프로그램을 가져오고 사용자 관리에 대해 Single Sign On을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="fa540-115">작동 방법</span><span class="sxs-lookup"><span data-stu-id="fa540-115">How it works</span></span>
1. <span data-ttu-id="fa540-116">응용 프로그램 사용 에이전트는 사용자의 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="fa540-117">hello 에이전트에 의해 캡처된 hello 응용 프로그램 사용 정보는 암호화 된 보안 채널 toohello cloud app discovery 서비스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="fa540-118">hello Cloud App Discovery 서비스는 hello 데이터를 평가 하 고 보고서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa540-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![클라우드 앱 검색 다이어그램](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="fa540-120">Cloud App discovery 시작 tooget 참조 [가져오는 Cloud App Discovery 시작](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="fa540-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="fa540-121">관련 문서</span><span class="sxs-lookup"><span data-stu-id="fa540-121">Related articles</span></span>
* [<span data-ttu-id="fa540-122">클라우드 앱 보안 및 개인정보 취급 방침 고려 사항</span><span class="sxs-lookup"><span data-stu-id="fa540-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="fa540-123">클라우드 앱 검색 그룹 정책 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="fa540-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="fa540-124">클라우드 앱 검색 시스템 센터 배포 가이드</span><span class="sxs-lookup"><span data-stu-id="fa540-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="fa540-125">사용자 지정 포트를 사용하는 프록시 서버용 클라우드 앱 검색 레지스트리 설정</span><span class="sxs-lookup"><span data-stu-id="fa540-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="fa540-126">클라우드 앱 검색 에이전트 Changelog </span><span class="sxs-lookup"><span data-stu-id="fa540-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="fa540-127">클라우드 앱 검색 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="fa540-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="fa540-128">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="fa540-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

