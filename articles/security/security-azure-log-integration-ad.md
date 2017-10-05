---
title: "Azure 로그 통합 및 Azure Active Directory 감사 로그 | Microsoft Docs"
description: "Azure 로그 통합 서비스를 설치하고 Azure 감사 로그의 로그를 통합하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3757d-103">Azure Active Directory 감사 로그 통합</span><span class="sxs-lookup"><span data-stu-id="3757d-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="3757d-104">Azure AD(Azure Active Directory) 감사 이벤트를 통해 Azure Active Directory에서 발생한 권한 있는 작업을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="3757d-105">[Azure Active Directory 감사 보고서 이벤트](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)를 검토하여 추적할 수 있는 이벤트 유형을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3757d-106">이 문서의 단계를 시도하기 전에 먼저 [시작하기](security-azure-log-integration-get-started.md) 문서를 검토하고 해당 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-106">Before you attempt the steps in this article, you must review the [Get started](security-azure-log-integration-get-started.md) article and complete the steps there.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="3757d-107">Azure Active Directory 감사 로그 통합 단계</span><span class="sxs-lookup"><span data-stu-id="3757d-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="3757d-108">명령 프롬프트를 열고 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-108">Open the command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="3757d-109">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="3757d-110">이 명령은 사용자에게 Azure 로그인을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="3757d-111">그런 다음 로그인한 사용자가 관리자, 공동 관리자 또는 소유자인 Azure 구독을 호스트하는 Azure AD 테넌트에 Azure Active Directory 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-111">The command then creates an Azure Active Directory service principal in the Azure AD tenants that host the Azure subscriptions in which the logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="3757d-112">로그인한 사용자가 Azure AD 테넌트의 게스트 사용자이면 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-112">The command will fail if the logged-in user is only a guest user in the Azure AD tenant.</span></span> <span data-ttu-id="3757d-113">Azure에 대한 인증은 Azure AD를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-113">Authentication to Azure is done through Azure AD.</span></span> <span data-ttu-id="3757d-114">Azure 로그 통합에 대한 서비스 주체를 만들면 Azure 구독을 읽을 수 있는 Azure AD ID가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-114">Creating a service principal for Azure Log Integration creates the Azure AD identity that is given access to read from Azure subscriptions.</span></span>

3. <span data-ttu-id="3757d-115">다음 명령을 실행하여 테넌트 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-115">Run the following command to provide your tenant ID.</span></span> <span data-ttu-id="3757d-116">이 명령을 실행하려면 테넌트 관리자 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-116">You need to be member of the tenant admin role to run the command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="3757d-117">예제:</span><span class="sxs-lookup"><span data-stu-id="3757d-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="3757d-118">다음 폴더에서 Azure Active Directory 감사 로그 JSON 파일을 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-118">Check the following folders to confirm that the Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="3757d-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="3757d-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="3757d-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="3757d-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="3757d-121">다음 비디오는 이 문서에서 설명하는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-121">The following video demonstrates the steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="3757d-122">SIEM(보안 정보 및 이벤트 관리) 시스템으로 JSON 파일에서 정보를 가져오는 것과 관련한 특정 지침은 해당 SIEM 공급업체에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3757d-122">For specific instructions on bringing the information in the JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="3757d-123">[Azure 로그 통합 MSDN 포럼](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)을 통해 커뮤니티의 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="3757d-124">이 포럼을 통해 Azure 로그 통합 커뮤니티의 사람들은 질문, 답변, 팁, 요령 등을 통해 서로 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-124">This forum enables people in the Azure Log Integration community to support each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="3757d-125">또한 Azure 로그 통합 팀이 이 포럼을 모니터링하며 가능한 한 언제든지 도움을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-125">In addition, the Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="3757d-126">[지원 요청](../azure-supportability/how-to-create-azure-support-request.md)을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="3757d-127">지원을 요청하려면 서비스로 **로그 통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-127">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3757d-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3757d-128">Next steps</span></span>
<span data-ttu-id="3757d-129">Azure 로그 통합에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3757d-129">To learn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="3757d-130">[Azure 로그에 대한 Microsoft Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324): 이 다운로드 센터 페이지는 Azure 로그 통합에 대한 세부 정보, 시스템 요구 사항 및 설치 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="3757d-131">[Azure 로그 통합 소개](security-azure-log-integration-overview.md): 이 문서에서는 Azure 로그 통합, 주요 기능 및 작동 원리를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-131">[Introduction to Azure Log Integration](security-azure-log-integration-overview.md): This article introduces you to Azure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="3757d-132">[파트너 구성 단계](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): 이 블로그 게시물에서는 Splunk, HP ArcSight, IBM QRadar 등의 파트너 솔루션과 함께 작동하도록 Azure 로그 통합을 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how to configure Azure Log Integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="3757d-133">[Azure 로그 통합 FAQ](security-azure-log-integration-faq.md): 이 문서는 Azure 로그 통합에 대한 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="3757d-134">[Security Center 경고를 Azure 로그 통합과 통합](../security-center/security-center-integrating-alerts-with-log-integration.md): 이 문서에서는 Azure 진단 및 Azure 감사 로그에 수집된 가상 컴퓨터 보안 이벤트와 함께 Security Center 경고를 로그 분석 또는 SIEM 솔루션과 동기화하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="3757d-135">[Azure 진단 및 Azure 감사 로그를 위한 새 기능](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): 이 블로그 게시물에서는 Azure 리소스 운영에 대한 정보 수집에 도움이 되는 Azure 감사 로그 및 기타 기능에 대해 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3757d-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you to Azure audit logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
