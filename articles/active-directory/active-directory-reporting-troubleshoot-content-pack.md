---
title: "Azure Active Directory 활동 로그 콘텐츠 팩 오류 문제 해결 | Microsoft Docs"
description: "Azure Active Directory 활동 콘텐츠 팩의 오류 메시지 목록 및 수정 단계를 제공합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="8648b-103">Azure Active Directory 활동 로그 콘텐츠 팩 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8648b-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="8648b-104">Azure Active Directory 미리 보기용 Power BI 콘텐츠 팩에서 작업할 경우 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="8648b-105">새로 고침 실패</span><span class="sxs-lookup"><span data-stu-id="8648b-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="8648b-106">데이터 원본 자격 증명을 업데이트하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="8648b-107">데이터를 가져오는 데 너무 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="8648b-108">이 항목에서는 발생할 수 있는 원인 및 이러한 오류 해결 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="8648b-109">새로 고침 실패</span><span class="sxs-lookup"><span data-stu-id="8648b-109">Refresh failed</span></span> 
 
<span data-ttu-id="8648b-110">**이 오류가 표시되는 방법**: Power BI 또는 새로 고침 기록 실패 상태로 인해 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="8648b-111">원인</span><span class="sxs-lookup"><span data-stu-id="8648b-111">Cause</span></span> | <span data-ttu-id="8648b-112">해결 방법</span><span class="sxs-lookup"><span data-stu-id="8648b-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="8648b-113">콘텐츠 팩에 연결되는 사용자의 자격 증명이 다시 설정되었지만 콘텐츠 팩의 연결 설정에서 업데이트되지 않은 경우 새로 고침 실패 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="8648b-114">Power BI에서 Azure Active Directory 활동 로그 대시보드(Azure Active Directory 활동 로그)에 해당하는 데이터 집합을 찾고 일정 새로 고침을 선택하고 Azure AD 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="8648b-115">기본 콘텐츠 팩에서 발생한 데이터 문제로 인해 새로 고침에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="8648b-116">지원 티켓을 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-116">File a support ticket.</span></span> <span data-ttu-id="8648b-117">자세한 내용은 [Azure Active Directory를 지원하는 방법](active-directory-troubleshooting-support-howto.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8648b-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="8648b-118">데이터 원본 자격 증명을 업데이트하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="8648b-119">**이 오류가 표시되는 경우**: Power BI에서 Azure Active Directory 활동 로그(미리 보기) 콘텐츠 팩에 연결하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="8648b-120">원인</span><span class="sxs-lookup"><span data-stu-id="8648b-120">Cause</span></span> | <span data-ttu-id="8648b-121">해결 방법</span><span class="sxs-lookup"><span data-stu-id="8648b-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="8648b-122">연결된 사용자는 전역 관리자 또는 보안 판독기나 보안 관리자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="8648b-123">전역 관리자 또는 보안 판독기 또는 보안 관리자인 계정을 사용하여 콘텐츠 팩에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="8648b-124">사용자의 테넌트가 프리미엄 테넌트가 아니거나 적어도 프리미엄 라이선스 파일이 있는 사용자가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="8648b-125">지원 티켓을 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-125">File a support ticket.</span></span> <span data-ttu-id="8648b-126">자세한 내용은 [Azure Active Directory를 지원하는 방법](active-directory-troubleshooting-support-howto.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8648b-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="8648b-127">데이터를 가져오는 데 너무 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="8648b-128">**이 오류가 표시되는 경우**: Power BI에서 콘텐츠 팩을 연결하면 데이터 가져오기 프로세스가 Azure Active Directory 활동 로그의 대시보드를 준비하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="8648b-129">"*데이터 가져오기...*"라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="8648b-130">원인</span><span class="sxs-lookup"><span data-stu-id="8648b-130">Cause</span></span> | <span data-ttu-id="8648b-131">해결 방법</span><span class="sxs-lookup"><span data-stu-id="8648b-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="8648b-132">테넌트의 크기에 따라 이 단계는 몇 분에서 최대 30분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="8648b-133">기다려 주세요.</span><span class="sxs-lookup"><span data-stu-id="8648b-133">Just be patient.</span></span> <span data-ttu-id="8648b-134">한 시간 내에 대시보드를 표시하도록 메시지가 변경되지 않는 경우 지원 티켓을 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="8648b-135">자세한 내용은 [Azure Active Directory를 지원하는 방법](active-directory-troubleshooting-support-howto.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8648b-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="8648b-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8648b-136">Next steps</span></span>

<span data-ttu-id="8648b-137">Azure Active Directory 미리 보기용 Power BI 콘텐츠 팩을 설치하려면 [여기](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8648b-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


