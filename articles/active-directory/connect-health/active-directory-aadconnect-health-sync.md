---
title: "동기화 하는 Azure AD Connect Health aaaUsing | Microsoft Docs"
description: "이 hello Azure AD Connect Health 페이지 toomonitor Azure AD Connect 동기화 하는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="bad94-103">Azure AD Connect Health를 사용하여 Azure AD Connect 동기화 모니터링</span><span class="sxs-lookup"><span data-stu-id="bad94-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="bad94-104">hello 설명서는 특정 toomonitoring Azure AD Connect Health를 사용 하 여 Azure AD 연결 (동기화)입니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-104">hello following documentation is specific toomonitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="bad94-105">Azure AD Connect Health와 함께 AD FS 모니터링에 대한 내용은 [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bad94-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="bad94-106">또한 Azure AD Connect Health와 함께 Active Directory 도메인 서비스를 모니터링하는 방법에 대한 정보는 [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bad94-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="bad94-108">동기화에 대한 Azure AD Connect Health에 대한 경고</span><span class="sxs-lookup"><span data-stu-id="bad94-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="bad94-109">hello Azure AD Connect Health 경고 동기화 섹션에 대 한 활성 경고 목록이 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-109">hello Azure AD Connect Health Alerts for sync section provides you hello list of active alerts.</span></span> <span data-ttu-id="bad94-110">각 경고 관련 정보, 해결 단계 및 toorelated 설명서 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-110">Each alert includes relevant information, resolution steps, and links toorelated documentation.</span></span> <span data-ttu-id="bad94-111">활성 또는 해결 된 경고를 선택 하 여 추가 정보 뿐만 아니라 tooresolve hello 경고 및 링크 tooadditional 설명서를 수행할 수 있는 단계는 새 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take tooresolve hello alert, and links tooadditional documentation.</span></span> <span data-ttu-id="bad94-112">또한 hello 과거에 해결 된 경고에 기록 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-112">You can also view historical data on alerts that were resolved in hello past.</span></span>

<span data-ttu-id="bad94-113">단계 뿐만 아니라 추가 정보 제공 되는 경고를 선택 하 여 수행할 수 tooresolve hello 경고 및 링크 tooadditional 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-113">By selecting an alert you will be provided with additional information as well as steps you can take tooresolve hello alert and links tooadditional documentation.</span></span>

![Azure AD Connect 동기화 오류](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="bad94-115">제한된 경고 평가</span><span class="sxs-lookup"><span data-stu-id="bad94-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="bad94-116">Azure AD Connect (예: 특성 필터링 hello 기본 구성 tooa 사용자 지정 구성에서 변경 된 경우) hello 기본 구성을 사용 하지 않으면, 다음 hello Azure AD Connect Health agent는 업로드 하지 hello 오류 이벤트에 대 한 관련된 tooAzure AD 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-116">If Azure AD Connect is NOT using hello default configuration (for example, if Attribute Filtering is changed from hello default configuration tooa custom configuration), then hello Azure AD Connect Health agent will not upload hello error events related tooAzure AD Connect.</span></span>

<span data-ttu-id="bad94-117">이 경고의 hello 평가 hello 서비스에 의해 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-117">This limits hello evaluation of alerts by hello service.</span></span> <span data-ttu-id="bad94-118">서비스에서 hello Azure 포털에서에서이 문제를 나타내는 배너를 나타납니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-118">You'd will see a banner that indicates this condition in hello Azure Portal under your service.</span></span>

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="bad94-120">"설정"을 클릭 하 고 Azure AD Connect Health agent tooupload 모든 오류 로그를 허용 하 여이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent tooupload all error logs.</span></span>

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="bad94-122">동기화 정보</span><span class="sxs-lookup"><span data-stu-id="bad94-122">Sync Insight</span></span>
<span data-ttu-id="bad94-123">Admins 자주 tooknow hello 시간이 toosync 변경 tooAzure AD 및 hello 양의 변화에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-123">Admins Frequently want tooknow about hello time it takes toosync changes tooAzure AD and hello amount of changes taking place.</span></span> <span data-ttu-id="bad94-124">이 기능을 통해 쉽게 toovisualize이 그래프 아래의 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="bad94-124">This feature provides an easy way toovisualize this using hello below graphs:</span></span>   

* <span data-ttu-id="bad94-125">동기화 작업의 대기 시간</span><span class="sxs-lookup"><span data-stu-id="bad94-125">Latency of sync operations</span></span>
* <span data-ttu-id="bad94-126">개체 변경 추세</span><span class="sxs-lookup"><span data-stu-id="bad94-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="bad94-127">동기화 대기 시간</span><span class="sxs-lookup"><span data-stu-id="bad94-127">Sync Latency</span></span>
<span data-ttu-id="bad94-128">이 기능은 hello 동기화 (가져오기, 내보내기 등)에 대 한 작업 커넥터의 대기 시간의 그래픽 추세를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-128">This feature provides a graphical trend of latency of hello sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="bad94-129">빠른 하며 쉽게 toounderstand 조사 해야 하는 hello 대기 시간 (큰 발생 한 변경 집합이 있는 경우 더 큰) 작업 뿐만 아니라 방식으로 toodetect 비정상의 대기 시간을 뿐만 아니라 hello.</span><span class="sxs-lookup"><span data-stu-id="bad94-129">This provides a quick and easy way toounderstand not only hello latency of your operations (larger if you have a large set of changes occurring) but also a way toodetect anomalies in hello latency that may require further investigation.</span></span>

![동기화 대기 시간](./media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="bad94-131">기본적으로 hello hello Azure AD 커넥터에 대 한 작업 'Export' hello 대기 시간만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-131">By default, only hello latency of hello 'Export' operation for hello Azure AD connector is shown.</span></span>  <span data-ttu-id="bad94-132">toosee hello 커넥터에는 다양 한 작업 또는 tooview 작업에서 다른 커넥터를 마우스 오른쪽 단추로 클릭 hello 차트에서 차트 편집를 선택 하거나 hello "대기 시간 차트 편집" 단추를 클릭 하 고 hello 특정 작업 및 커넥터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-132">toosee more operations on hello connector or tooview operations from other connectors, right-click on hello chart,  select Edit Chart or click on hello "Edit Latency Chart" button and choose hello specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="bad94-133">동기화 개체 변경 사항</span><span class="sxs-lookup"><span data-stu-id="bad94-133">Sync Object Changes</span></span>
<span data-ttu-id="bad94-134">이 기능은 hello 계산 하 고 AD tooAzure 내보내집니다 변경 내용 수의 그래픽 추세를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-134">This feature provides a graphical trend of hello number of changes that are being evaluated and exported tooAzure AD.</span></span>  <span data-ttu-id="bad94-135">오늘날, 동안 toogather hello 동기화 로그에서이 정보는 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-135">Today, trying toogather this information from hello sync logs is difficult.</span></span>  <span data-ttu-id="bad94-136">hello 차트 제공, 보다 간단한 방법을 뿐만 아니라 사용자 환경에서 발생 하는 변경 내용 hello 수 뿐만 아니라 발생 하는 hello 오류의 시각적 보기를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-136">hello chart gives you, not only a simpler way of monitoring hello number of changes that are occurring in your environment, but also a visual view of hello failures that are occurring.</span></span>

![동기화 대기 시간](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="bad94-138">개체 수준 동기화 오류 보고서(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="bad94-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="bad94-139">이 기능은 Azure AD Connect를 사용하여 Windows Server AD와 Azure AD 간의 ID 데이터를 동기화할 때 발생할 수 있는 동기화 오류에 대한 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="bad94-140">hello 보고서에서는 오류 hello 동기화 클라이언트 (Azure AD Connect 버전 1.1.281.0 또는 이상)</span><span class="sxs-lookup"><span data-stu-id="bad94-140">hello report covers errors recorded by hello sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="bad94-141">Hello hello 동기화 엔진에서 마지막 동기화 작업의 hello 발생 한 오류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-141">It includes hello errors that occurred in hello last synchronization operation on hello sync engine.</span></span> <span data-ttu-id="bad94-142">("Export" hello Azure AD 커넥터에서.)</span><span class="sxs-lookup"><span data-stu-id="bad94-142">("Export" on hello Azure AD Connector.)</span></span>
* <span data-ttu-id="bad94-143">동기화 용 azure AD Connect Health agent hello 보고서 tooinclude hello 최신 데이터에 대 한 아웃 바운드 연결 필요한 toohello 시작점과 끝점이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-143">Azure AD Connect Health agent for sync must have outbound connectivity toohello required end points for hello report tooinclude hello latest data.</span></span>
* <span data-ttu-id="bad94-144">hello 보고서가 **매 30 분 후 업데이트 된** 동기화 용 Azure AD Connect Health agent가 업로드 hello 데이터를 사용 하 여 합니다. 주요 기능을 수행 하는 hello 제공</span><span class="sxs-lookup"><span data-stu-id="bad94-144">hello report is **updated after every 30 minutes** using hello data uploaded by Azure AD Connect Health agent for sync. It provides hello following key capabilities</span></span>

  * <span data-ttu-id="bad94-145">오류 분류</span><span class="sxs-lookup"><span data-stu-id="bad94-145">Categorization of errors</span></span>
  * <span data-ttu-id="bad94-146">범주별 오류에 따른 개체의 목록</span><span class="sxs-lookup"><span data-stu-id="bad94-146">List of objects with error per category</span></span>
  * <span data-ttu-id="bad94-147">한 곳에서 발생 한 hello 오류에 대 한 모든 hello 데이터</span><span class="sxs-lookup"><span data-stu-id="bad94-147">All hello data about hello errors at one place</span></span>
  * <span data-ttu-id="bad94-148">오류로 인해 tooa 충돌 개체의 특징이 비교 정렬</span><span class="sxs-lookup"><span data-stu-id="bad94-148">Side by side comparison of Objects with error due tooa conflict</span></span>
  * <span data-ttu-id="bad94-149">(출시 예정) CVS로 hello 오류 보고서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-149">Download hello error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="bad94-150">오류 분류</span><span class="sxs-lookup"><span data-stu-id="bad94-150">Categorization of Errors</span></span>
<span data-ttu-id="bad94-151">hello 보고서 hello 기존 동기화 오류 범주를 수행 하는 hello에서 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-151">hello report categorizes hello existing synchronization errors in hello following categories:</span></span>

| <span data-ttu-id="bad94-152">Category</span><span class="sxs-lookup"><span data-stu-id="bad94-152">Category</span></span> | <span data-ttu-id="bad94-153">설명</span><span class="sxs-lookup"><span data-stu-id="bad94-153">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bad94-154">중복 특성</span><span class="sxs-lookup"><span data-stu-id="bad94-154">Duplicate Attribute</span></span> |<span data-ttu-id="bad94-155">proxyAddresses, UserPrincipalName 같은 테넌트 내에서 고유해야 하는 Azure AD에서 하나 이상의 특성의 값이 중복된 개체를 만들거나 업데이트하려고 시도할 때의 오류</span><span class="sxs-lookup"><span data-stu-id="bad94-155">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="bad94-156">데이터 불일치</span><span class="sxs-lookup"><span data-stu-id="bad94-156">Data Mismatch</span></span> |<span data-ttu-id="bad94-157">Hello 소프트 일치 toomatch 개체 동기화 오류를 일으키는 실패 한 경우 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-157">Errors when hello soft-match fails toomatch objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="bad94-158">데이터 유효성 검사 실패</span><span class="sxs-lookup"><span data-stu-id="bad94-158">Data Validation Failure</span></span> |<span data-ttu-id="bad94-159">UserPrincipalName, 등의 중요 한 특성에서 지원 되지 않는 문자가 같은 tooinvalid 데이터 않아서 발생 한 오류에는 Azure AD에 기록 되기 전에 유효성 검사가 실패 하는 오류 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-159">Errors due tooinvalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="bad94-160">큰 특성</span><span class="sxs-lookup"><span data-stu-id="bad94-160">Large Attribute</span></span> |<span data-ttu-id="bad94-161">하나 이상의 특성 hello 보다 큰 경우 오류 크기, 길이 또는 수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-161">Errors when one or more attributes are larger than hello allowed size, length or count.</span></span> |
| <span data-ttu-id="bad94-162">기타</span><span class="sxs-lookup"><span data-stu-id="bad94-162">Other</span></span> |<span data-ttu-id="bad94-163">모든 다른 오류 범주 위에 hello에 맞지 않는입니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-163">All other errors that don't fit in hello above categories.</span></span> <span data-ttu-id="bad94-164">의견에 따라 이 범주는 하위 범주로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-164">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="bad94-165">![동기화 오류 보고서 요약](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![동기화 오류 보고서 범주](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span><span class="sxs-lookup"><span data-stu-id="bad94-165">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="bad94-166">범주별 오류에 따른 개체의 목록</span><span class="sxs-lookup"><span data-stu-id="bad94-166">List of objects with error per category</span></span>
<span data-ttu-id="bad94-167">각 범주를 드릴링 하는 hello 오류 해당 범주에 포함 된 개체의 hello 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-167">Drilling into each category will provide hello list of objects having hello error in that category.</span></span>
<span data-ttu-id="bad94-168">![동기화 오류 보고서 목록](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="bad94-168">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="bad94-169">오류 세부 정보</span><span class="sxs-lookup"><span data-stu-id="bad94-169">Error Details</span></span>
<span data-ttu-id="bad94-170">다음 데이터는 hello에서 사용할 수 있는 각 오류에 대 한 보기를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-170">Following data is available in hello detailed view for each error</span></span>

* <span data-ttu-id="bad94-171">Hello에 대 한 식별자 *AD 개체* 참여</span><span class="sxs-lookup"><span data-stu-id="bad94-171">Identifiers for hello *AD Object* involved</span></span>
* <span data-ttu-id="bad94-172">Hello에 대 한 식별자 *Azure AD 개체* (로) 참여</span><span class="sxs-lookup"><span data-stu-id="bad94-172">Identifiers for hello *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="bad94-173">오류 설명 및 방법을 toofix</span><span class="sxs-lookup"><span data-stu-id="bad94-173">Error description and how toofix</span></span>
* <span data-ttu-id="bad94-174">관련 문서</span><span class="sxs-lookup"><span data-stu-id="bad94-174">Related articles</span></span>

![동기화 오류 보고서 세부 정보](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a><span data-ttu-id="bad94-176">Hello 오류 보고서를 CSV로 다운로드</span><span class="sxs-lookup"><span data-stu-id="bad94-176">Download hello error report as CSV</span></span>
<span data-ttu-id="bad94-177">Hello를 선택 하 여 "내보내기" 단추 모든 hello 오류에 대 한 모든 hello 세부 정보가 된 CSV 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad94-177">By selecting hello "Export" button you can download a CSV file with all hello details about all hello errors.</span></span>

## <a name="related-links"></a><span data-ttu-id="bad94-178">관련 링크</span><span class="sxs-lookup"><span data-stu-id="bad94-178">Related links</span></span>
* [<span data-ttu-id="bad94-179">동기화 중 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="bad94-179">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="bad94-180">중복 특성 복원력</span><span class="sxs-lookup"><span data-stu-id="bad94-180">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="bad94-181">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="bad94-181">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="bad94-182">Azure AD Connect Health Agent 설치</span><span class="sxs-lookup"><span data-stu-id="bad94-182">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="bad94-183">Azure AD Connect Health 작업</span><span class="sxs-lookup"><span data-stu-id="bad94-183">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="bad94-184">AD FS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="bad94-184">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="bad94-185">AD DS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="bad94-185">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="bad94-186">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="bad94-186">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="bad94-187">Azure AD Connect Health 버전 내역</span><span class="sxs-lookup"><span data-stu-id="bad94-187">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)