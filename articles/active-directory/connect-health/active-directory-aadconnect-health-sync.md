---
title: "동기화된 Azure AD Connect Health 사용 | Microsoft Docs"
description: "Azure AD Connect 동기화를 모니터링하는 방법을 설명하는 Azure AD Connect Health 페이지입니다."
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
ms.openlocfilehash: 4b06338cb62cc458e7b097db36023f0746d4e969
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="095a9-103">Azure AD Connect Health를 사용하여 Azure AD Connect 동기화 모니터링</span><span class="sxs-lookup"><span data-stu-id="095a9-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="095a9-104">다음 문서는 Azure AD Connect Health와 함께 Azure AD Connect (동기화) 모니터링에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-104">The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="095a9-105">Azure AD Connect Health와 함께 AD FS 모니터링에 대한 내용은 [AD FS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adfs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="095a9-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="095a9-106">또한 Azure AD Connect Health와 함께 Active Directory 도메인 서비스를 모니터링하는 방법에 대한 정보는 [AD DS와 함께 Azure AD Connect Health 사용](active-directory-aadconnect-health-adds.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="095a9-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="095a9-108">동기화에 대한 Azure AD Connect Health에 대한 경고</span><span class="sxs-lookup"><span data-stu-id="095a9-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="095a9-109">동기화에 대한 Azure AD Connect Health 경고 섹션은 활성 경고 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-109">The Azure AD Connect Health Alerts for sync section provides you the list of active alerts.</span></span> <span data-ttu-id="095a9-110">각 경고에는 관련 정보, 해결 단계 및 관련된 설명서 링크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-110">Each alert includes relevant information, resolution steps, and links to related documentation.</span></span> <span data-ttu-id="095a9-111">활성 또는 해결된 경고를 선택하면 추가 정보는 물론, 경고를 해결하기 위해 수행할 수 있는 단계와 추가 설명서 링크가 포함된 새 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation.</span></span> <span data-ttu-id="095a9-112">과거에 해결된 경고에 대한 기록 데이터도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-112">You can also view historical data on alerts that were resolved in the past.</span></span>

<span data-ttu-id="095a9-113">경고를 선택하면 추가 정보는 물론 경고를 해결하기 위해 수행할 수 있는 단계와 추가 설명서 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-113">By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.</span></span>

![Azure AD Connect 동기화 오류](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="095a9-115">제한된 경고 평가</span><span class="sxs-lookup"><span data-stu-id="095a9-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="095a9-116">Azure AD Connect가 기본 구성을 사용하지 않으면(예: 특성 필터링이 기본 구성에서 사용자 지정 구성으로 변경된 경우) Azure AD Connect Health 에이전트가 Azure AD Connect와 관련된 오류 이벤트를 업로드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-116">If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.</span></span>

<span data-ttu-id="095a9-117">이로 인해 서비스의 경고 평가가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-117">This limits the evaluation of alerts by the service.</span></span> <span data-ttu-id="095a9-118">Azure 포털에서 해당 서비스 아래에 이 조건을 나타내는 배너가 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-118">You'd will see a banner that indicates this condition in the Azure Portal under your service.</span></span>

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="095a9-120">"설정"을 클릭하고 Azure AD Connect Health 에이전트가 모든 오류 로그를 업로드할 수 있도록 허용하여 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.</span></span>

![동기화에 대한 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="095a9-122">동기화 정보</span><span class="sxs-lookup"><span data-stu-id="095a9-122">Sync Insight</span></span>
<span data-ttu-id="095a9-123">관리자는 Azure AD에 대한 동기화 변경에 걸리는 시간과 변화의 양에 대해 자주 알아보려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-123">Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place.</span></span> <span data-ttu-id="095a9-124">이 기능은 아래 그래프를 사용하여 시각화하는 간편한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-124">This feature provides an easy way to visualize this using the below graphs:</span></span>   

* <span data-ttu-id="095a9-125">동기화 작업의 대기 시간</span><span class="sxs-lookup"><span data-stu-id="095a9-125">Latency of sync operations</span></span>
* <span data-ttu-id="095a9-126">개체 변경 추세</span><span class="sxs-lookup"><span data-stu-id="095a9-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="095a9-127">동기화 대기 시간</span><span class="sxs-lookup"><span data-stu-id="095a9-127">Sync Latency</span></span>
<span data-ttu-id="095a9-128">이 기능은 커넥터에 대한 동기화 작업(가져오기, 내보내기, 등)의 대기 시간을 그래픽 추세로 표시니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-128">This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="095a9-129">작업의 대기 시간(변경 사항이 대규모인 경우 적합)뿐만 아니라 대기 시간에 좀 더 조사가 필요한 이상을 감지하는 방법을 빠르고 쉽게 이해하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-129">This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.</span></span>

![동기화 대기 시간](./media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="095a9-131">기본적으로 Azure AD 커넥터에 대한 '내보내기' 작업의 대기 시간만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-131">By default, only the latency of the 'Export' operation for the Azure AD connector is shown.</span></span>  <span data-ttu-id="095a9-132">커넥터에 대한 더 많은 작업 또는 다른 커넥터에서 작업을 보려면 차트를 마우스 오른쪽 단추로 클릭하고, 차트 편집을 선택하거나 "대기 시간 차트 편집" 버튼을 클릭하고 특정 작업 및 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-132">To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="095a9-133">동기화 개체 변경 사항</span><span class="sxs-lookup"><span data-stu-id="095a9-133">Sync Object Changes</span></span>
<span data-ttu-id="095a9-134">이 기능은 평가되어 Azure AD로 내보내진 변경 횟수를 그래픽 추세로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-134">This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.</span></span>  <span data-ttu-id="095a9-135">오늘날, 동기화 로그에서 이러한 정보를 수집하는 것은 어려운 일입니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-135">Today, trying to gather this information from the sync logs is difficult.</span></span>  <span data-ttu-id="095a9-136">차트를 통해 사용자의 환경에서 발생하는 변경 횟수를 보다 간단하게 모니터링하는 방법뿐만 아니라 발생하는 오류를 시각적으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-136">The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.</span></span>

![동기화 대기 시간](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="095a9-138">개체 수준 동기화 오류 보고서(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="095a9-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="095a9-139">이 기능은 Azure AD Connect를 사용하여 Windows Server AD와 Azure AD 간의 ID 데이터를 동기화할 때 발생할 수 있는 동기화 오류에 대한 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="095a9-140">보고서에서는 동기화 클라이언트를 통해 기록된 오류를 포함합니다(Azure AD Connect 1.1.281.0 버전 이상)</span><span class="sxs-lookup"><span data-stu-id="095a9-140">The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="095a9-141">동기화 엔진의 마지막 동기화 작업에서 발생한 오류를 포함합니다</span><span class="sxs-lookup"><span data-stu-id="095a9-141">It includes the errors that occurred in the last synchronization operation on the sync engine.</span></span> <span data-ttu-id="095a9-142">(Azure AD 커넥터에 “내보내기”).</span><span class="sxs-lookup"><span data-stu-id="095a9-142">("Export" on the Azure AD Connector.)</span></span>
* <span data-ttu-id="095a9-143">동기화에 대한 Azure AD Connect Health agent에는 최신 데이터를 포함하는 보고서에 필요한 끝점의 아웃바운드 연결이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-143">Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.</span></span>
* <span data-ttu-id="095a9-144">보고서는 동기화를 위한 Azure AD Connect Health 에이전트에서 업로드한 데이터를 사용하여 **30분 마다 업데이트**됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-144">The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync.</span></span>
  <span data-ttu-id="095a9-145">다음과 같은 주요 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-145">It provides the following key capabilities</span></span>

  * <span data-ttu-id="095a9-146">오류 분류</span><span class="sxs-lookup"><span data-stu-id="095a9-146">Categorization of errors</span></span>
  * <span data-ttu-id="095a9-147">범주별 오류에 따른 개체의 목록</span><span class="sxs-lookup"><span data-stu-id="095a9-147">List of objects with error per category</span></span>
  * <span data-ttu-id="095a9-148">한 곳에서 발생한 오류에 대한 모든 데이터</span><span class="sxs-lookup"><span data-stu-id="095a9-148">All the data about the errors at one place</span></span>
  * <span data-ttu-id="095a9-149">충돌로 인해 오류와 함께 개체의 특징을 비교 정렬</span><span class="sxs-lookup"><span data-stu-id="095a9-149">Side by side comparison of Objects with error due to a conflict</span></span>
  * <span data-ttu-id="095a9-150">CVS로 오류 보고서를 다운로드(출시 예정)</span><span class="sxs-lookup"><span data-stu-id="095a9-150">Download the error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="095a9-151">오류 분류</span><span class="sxs-lookup"><span data-stu-id="095a9-151">Categorization of Errors</span></span>
<span data-ttu-id="095a9-152">보고서에서는 기존 동기화 오류를 다음과 같은 범주로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-152">The report categorizes the existing synchronization errors in the following categories:</span></span>

| <span data-ttu-id="095a9-153">Category</span><span class="sxs-lookup"><span data-stu-id="095a9-153">Category</span></span> | <span data-ttu-id="095a9-154">설명</span><span class="sxs-lookup"><span data-stu-id="095a9-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="095a9-155">중복 특성</span><span class="sxs-lookup"><span data-stu-id="095a9-155">Duplicate Attribute</span></span> |<span data-ttu-id="095a9-156">proxyAddresses, UserPrincipalName 같은 테넌트 내에서 고유해야 하는 Azure AD에서 하나 이상의 특성의 값이 중복된 개체를 만들거나 업데이트하려고 시도할 때의 오류</span><span class="sxs-lookup"><span data-stu-id="095a9-156">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="095a9-157">데이터 불일치</span><span class="sxs-lookup"><span data-stu-id="095a9-157">Data Mismatch</span></span> |<span data-ttu-id="095a9-158">소프트 일치가 동기화 오류가 발생하는 개체와 일치하도록 하는 데 실패할 경우발생하는 오류</span><span class="sxs-lookup"><span data-stu-id="095a9-158">Errors when the soft-match fails to match objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="095a9-159">데이터 유효성 검사 실패</span><span class="sxs-lookup"><span data-stu-id="095a9-159">Data Validation Failure</span></span> |<span data-ttu-id="095a9-160">UserPrincipalName와 같은 중요한 특성에서 지원되지 않는 문자 등 잘못된 데이터로 인한 오류, Azure AD에 기록되기 전에 유효성 검사에 실패하는 서식 오류.</span><span class="sxs-lookup"><span data-stu-id="095a9-160">Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="095a9-161">큰 특성</span><span class="sxs-lookup"><span data-stu-id="095a9-161">Large Attribute</span></span> |<span data-ttu-id="095a9-162">하나 이상의 특성의 허용 되는 크기, 길이 또는 개수보다 클 때 발생하는 오류</span><span class="sxs-lookup"><span data-stu-id="095a9-162">Errors when one or more attributes are larger than the allowed size, length or count.</span></span> |
| <span data-ttu-id="095a9-163">기타</span><span class="sxs-lookup"><span data-stu-id="095a9-163">Other</span></span> |<span data-ttu-id="095a9-164">위 범주에 맞지 않는 다른 모든 오류</span><span class="sxs-lookup"><span data-stu-id="095a9-164">All other errors that don't fit in the above categories.</span></span> <span data-ttu-id="095a9-165">의견에 따라 이 범주는 하위 범주로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-165">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="095a9-166">![동기화 오류 보고서 요약](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![동기화 오류 보고서 범주](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span><span class="sxs-lookup"><span data-stu-id="095a9-166">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="095a9-167">범주별 오류에 따른 개체의 목록</span><span class="sxs-lookup"><span data-stu-id="095a9-167">List of objects with error per category</span></span>
<span data-ttu-id="095a9-168">각 범주에 대해 자세히 알아보면 해당 범주의 오류가 포함된 개체의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-168">Drilling into each category will provide the list of objects having the error in that category.</span></span>
<span data-ttu-id="095a9-169">![동기화 오류 보고서 목록](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="095a9-169">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="095a9-170">오류 세부 정보</span><span class="sxs-lookup"><span data-stu-id="095a9-170">Error Details</span></span>
<span data-ttu-id="095a9-171">다음 데이터를 각 오류에 대한 자세한 보기에 사용할 수 있음</span><span class="sxs-lookup"><span data-stu-id="095a9-171">Following data is available in the detailed view for each error</span></span>

* <span data-ttu-id="095a9-172">관련된 *AD 개체*에 대한 식별자</span><span class="sxs-lookup"><span data-stu-id="095a9-172">Identifiers for the *AD Object* involved</span></span>
* <span data-ttu-id="095a9-173">관련된 *Azure AD 개체*에 대한 식별자</span><span class="sxs-lookup"><span data-stu-id="095a9-173">Identifiers for the *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="095a9-174">오류 설명 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="095a9-174">Error description and how to fix</span></span>
* <span data-ttu-id="095a9-175">관련 문서</span><span class="sxs-lookup"><span data-stu-id="095a9-175">Related articles</span></span>

![동기화 오류 보고서 세부 정보](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-the-error-report-as-csv"></a><span data-ttu-id="095a9-177">CVS로 오류 보고서를 다운로드</span><span class="sxs-lookup"><span data-stu-id="095a9-177">Download the error report as CSV</span></span>
<span data-ttu-id="095a9-178">“내보내기” 단추를 선택하면 모든 오류에 대한 세부 정보를 모두 포함하는 CSV 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095a9-178">By selecting the "Export" button you can download a CSV file with all the details about all the errors.</span></span>

## <a name="related-links"></a><span data-ttu-id="095a9-179">관련 링크</span><span class="sxs-lookup"><span data-stu-id="095a9-179">Related links</span></span>
* [<span data-ttu-id="095a9-180">동기화 중 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="095a9-180">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="095a9-181">중복 특성 복원력</span><span class="sxs-lookup"><span data-stu-id="095a9-181">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="095a9-182">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="095a9-182">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="095a9-183">Azure AD Connect Health Agent 설치</span><span class="sxs-lookup"><span data-stu-id="095a9-183">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="095a9-184">Azure AD Connect Health 작업</span><span class="sxs-lookup"><span data-stu-id="095a9-184">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="095a9-185">AD FS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="095a9-185">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="095a9-186">AD DS와 함께 Azure AD Connect Health 사용</span><span class="sxs-lookup"><span data-stu-id="095a9-186">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="095a9-187">Azure AD Connect Health FAQ</span><span class="sxs-lookup"><span data-stu-id="095a9-187">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="095a9-188">Azure AD Connect Health 버전 내역</span><span class="sxs-lookup"><span data-stu-id="095a9-188">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)