---
title: "Azure Active Directory 활동 로그 콘텐츠 팩 오류 문제 해결 | Microsoft Docs"
description: "Hello Azure Active Directory 작업 콘텐츠 팩 및 단계 toofix의 오류 메시지 목록을 제공 하 합니다."
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
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="d1e65-103">Azure Active Directory 활동 로그 콘텐츠 팩 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d1e65-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="d1e65-104">Azure Active Directory 미리 보기에 대 한 Power BI 콘텐츠 팩 hello를 작업할 때 된 hello 다음 오류를 실행 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="d1e65-105">새로 고침 실패</span><span class="sxs-lookup"><span data-stu-id="d1e65-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="d1e65-106">실패 한 tooupdate 데이터 원본 자격 증명</span><span class="sxs-lookup"><span data-stu-id="d1e65-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="d1e65-107">데이터를 가져오는 데 너무 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="d1e65-108">이 항목에서는 hello 가능한 원인에 대 한 정보 및 방법 toofix 이러한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="d1e65-109">새로 고침 실패</span><span class="sxs-lookup"><span data-stu-id="d1e65-109">Refresh failed</span></span> 
 
<span data-ttu-id="d1e65-110">**이 오류가 표시 되는 어떻게**: Power BI 또는 hello 새로 고침 기록에 실패 한 상태에서 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="d1e65-111">원인</span><span class="sxs-lookup"><span data-stu-id="d1e65-111">Cause</span></span> | <span data-ttu-id="d1e65-112">어떻게 toofix</span><span class="sxs-lookup"><span data-stu-id="d1e65-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="d1e65-113">재생 오류 toohello 콘텐츠 팩을 연결 하는 hello 사용자의 hello 자격 증명 다시 설정 되었지만 hello 콘텐츠 팩의 hello의 hello 연결 설정에서 업데이트 되지 않은 경우 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="d1e65-114">Power BI에서 hello dataset 해당 toohello Azure Active Directory 작업 로그 대시보드 (Azure Active Directory 작업 로그의 경우)를 찾을, 새로 고침 일정을 선택 하 고 Azure AD 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="d1e65-115">새로 고침의 기본 콘텐츠 팩 hello toodata 문제 인해 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="d1e65-116">지원 티켓을 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-116">File a support ticket.</span></span> <span data-ttu-id="d1e65-117">자세한 내용은 참조 하십시오. [tooget Azure Active Directory에 대 한 지원 되는 방식을](active-directory-troubleshooting-support-howto.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="d1e65-118">실패 한 tooupdate 데이터 원본 자격 증명</span><span class="sxs-lookup"><span data-stu-id="d1e65-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="d1e65-119">**이 오류가 표시 되는 어떻게**:에서 Power BI에서는 toohello Azure Active Directory 작업 로그 (미리 보기) 콘텐츠 팩을 연결 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="d1e65-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="d1e65-120">원인</span><span class="sxs-lookup"><span data-stu-id="d1e65-120">Cause</span></span> | <span data-ttu-id="d1e65-121">어떻게 toofix</span><span class="sxs-lookup"><span data-stu-id="d1e65-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="d1e65-122">hello 연결 하는 사용자가 전역 관리자와 보안 판독기가 아니고 보안 관리자</span><span class="sxs-lookup"><span data-stu-id="d1e65-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="d1e65-123">보안 판독기 또는 전역 관리자 계정을 사용 하거나 보안 관리 tooaccess hello 콘텐츠 팩.</span><span class="sxs-lookup"><span data-stu-id="d1e65-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="d1e65-124">사용자의 테넌트가 프리미엄 테넌트가 아니거나 적어도 프리미엄 라이선스 파일이 있는 사용자가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="d1e65-125">지원 티켓을 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-125">File a support ticket.</span></span> <span data-ttu-id="d1e65-126">자세한 내용은 참조 하십시오. [tooget Azure Active Directory에 대 한 지원 되는 방식을](active-directory-troubleshooting-support-howto.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="d1e65-127">데이터를 가져오는 데 너무 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="d1e65-128">**이 오류가 표시 되는 어떻게**: Power BI 콘텐츠 팩을 연결 하 고 나면 hello 데이터 가져오기 프로세스 시작 tooprepare Azure Active Directory 작업 로그에 대 한 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="d1e65-129">Hello 메시지 표시: "*... 데이터 가져오기* "</span><span class="sxs-lookup"><span data-stu-id="d1e65-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="d1e65-130">원인</span><span class="sxs-lookup"><span data-stu-id="d1e65-130">Cause</span></span> | <span data-ttu-id="d1e65-131">어떻게 toofix</span><span class="sxs-lookup"><span data-stu-id="d1e65-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="d1e65-132">테 넌 트의 hello 크기에 따라이 단계는 몇 분 too30 분에서 아무 곳 이나 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="d1e65-133">기다려 주세요.</span><span class="sxs-lookup"><span data-stu-id="d1e65-133">Just be patient.</span></span> <span data-ttu-id="d1e65-134">Hello 메시지 변경 되지 않는 경우 tooshowing 대시보드 1 시간 내에, 지원 티켓을 보관 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d1e65-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="d1e65-135">자세한 내용은 참조 하십시오. [tooget Azure Active Directory에 대 한 지원 되는 방식을](active-directory-troubleshooting-support-howto.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="d1e65-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1e65-136">Next steps</span></span>

<span data-ttu-id="d1e65-137">Azure Active Directory 미리 보기의 경우 Power BI 콘텐츠 팩 tooinstall hello 클릭 [여기](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e65-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


