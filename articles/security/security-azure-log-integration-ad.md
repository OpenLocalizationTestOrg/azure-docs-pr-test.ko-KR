---
title: "Azure Active Directory 감사 로그와 로그 통합 aaaAzure | Microsoft Docs"
description: "Tooinstall hello Azure 로그 통합 서비스 하 고 Azure 감사 로그에서 로그를 통합 하는 방법에 대해 알아봅니다"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="b4315-103">Azure Active Directory 감사 로그 통합</span><span class="sxs-lookup"><span data-stu-id="b4315-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="b4315-104">Azure AD(Azure Active Directory) 감사 이벤트를 통해 Azure Active Directory에서 발생한 권한 있는 작업을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="b4315-105">이벤트를 검토 하 여 추적할 수 있는 hello 형식을 볼 수 있습니다 [Azure Active Directory 감사 보고서 이벤트](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b4315-106">이 문서의 hello 단계를 시도 하기 전에 hello 검토 해야 [시작](security-azure-log-integration-get-started.md) 문서 및 hello 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="b4315-107">단계 toointegrate Azure Active directory 감사 로그</span><span class="sxs-lookup"><span data-stu-id="b4315-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="b4315-108">Hello 명령 프롬프트를 열고이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="b4315-109">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="b4315-110">이 명령은 사용자에게 Azure 로그인을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="b4315-111">hello 명령 후 Azure Active Directory 서비스 사용자를 만듭니다 hello Azure AD 테 넌 트에서 해당 호스트 hello는 hello 로그인 한 사용자가 관리자, 공동 관리자 또는 소유자는 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="b4315-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="b4315-112">hello에 로그인 한 사용자가 게스트 사용자를 hello Azure AD 테 넌 트에만 hello 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="b4315-113">인증 tooAzure Azure AD를 통해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="b4315-114">Azure 로그 통합에 대 한 서비스 사용자를 만들면 hello 액세스 tooread Azure 구독에서 지정 된 Azure AD id 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="b4315-115">실행된 hello 다음 명령은 tooprovide 테 넌 트 ID</span><span class="sxs-lookup"><span data-stu-id="b4315-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="b4315-116">Hello 테 넌 트 관리자 역할 toorun hello 명령 toobe 소속이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="b4315-117">예제:</span><span class="sxs-lookup"><span data-stu-id="b4315-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="b4315-118">여기에 따라 Azure Active Directory 감사 로그 JSON 파일 hello 폴더 tooconfirm hello 만들어집니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="b4315-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="b4315-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="b4315-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="b4315-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="b4315-121">hello 다음 비디오에서는 보여줍니다이 문서에서 다루는 hello 단계:</span><span class="sxs-lookup"><span data-stu-id="b4315-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="b4315-122">보안 정보 및 이벤트 (SIEM) 관리 시스템으로 hello JSON 파일에서 hello 정보 보기에 대 한 자세한 내용은 SIEM 공급 업체에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="b4315-123">커뮤니티 지원 hello를 통해 사용할 수는 [Azure 로그 통합 MSDN 포럼](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="b4315-124">이 포럼으로 수 있도록 hello Azure 로그 통합 커뮤니티 toosupport에 서로 관련 된 질문, 대답, 팁 및 요령 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="b4315-125">또한 hello Azure 로그 통합 팀이이 포럼을 모니터링 하 고 가능 하기는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="b4315-126">[지원 요청](../azure-supportability/how-to-create-azure-support-request.md)을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="b4315-127">선택 **로그 통합** hello 서비스 지원을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4315-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4315-128">Next steps</span></span>
<span data-ttu-id="b4315-129">Azure 로그 통합에 대해 자세히 toolearn 참조:</span><span class="sxs-lookup"><span data-stu-id="b4315-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="b4315-130">[Azure 로그에 대한 Microsoft Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324): 이 다운로드 센터 페이지는 Azure 로그 통합에 대한 세부 정보, 시스템 요구 사항 및 설치 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="b4315-131">[로그 통합 소개 tooAzure](security-azure-log-integration-overview.md):이 문서에서는 소개 tooAzure 로그 통합의 주요 기능 및 작동 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="b4315-132">[구성 단계를 파트너](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/):이 블로그 게시물 표시 방법으로 Azure 로그 통합 toowork tooconfigure 파트너 솔루션 Splunk, HP ArcSight 및 IBM QRadar 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="b4315-133">[Azure 로그 통합 FAQ](security-azure-log-integration-faq.md): 이 문서는 Azure 로그 통합에 대한 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="b4315-134">[Azure 로그 통합 보안 센터 알림을 통합](../security-center/security-center-integrating-alerts-with-log-integration.md):이 문서에서는 Azure 진단 및 로그 분석을 사용 하 여 Azure 감사 로그에서 수집 하는 가상 컴퓨터 보안 이벤트와 함께 toosync 보안 센터 경고 방법 또는 SIEM 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="b4315-135">[Azure 진단 및 Azure에 대 한 새로운 기능 감사 로그](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/):이 블로그 게시물에서는 tooAzure 감사 로그 소개 하 고 Azure 리소스의 hello 작업을 파악할 수 있는 기타 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b4315-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
