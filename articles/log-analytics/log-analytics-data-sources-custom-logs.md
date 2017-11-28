---
title: "OMS Log Analytics에서 사용자 지정 로그 수집 | Microsoft Docs"
description: "Log Analytics는 Windows와 Linux 컴퓨터의 텍스트 파일에서 이벤트를 수집할 수 있습니다.  이 문서는 새 사용자 지정 로그를 정의하는 방법을 설명하고 OMS 리포지토리에 만드는 레코드에 대한 자세한 정보를 제공합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: b7f28868e3ffdf95dbe39872f382e7c97eae692c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="custom-logs-in-log-analytics"></a><span data-ttu-id="7a0ef-104">Log Analytics의 사용자 지정 로그</span><span class="sxs-lookup"><span data-stu-id="7a0ef-104">Custom logs in Log Analytics</span></span>
<span data-ttu-id="7a0ef-105">Log Analytics의 사용자 지정 로그 데이터 원본을 통해 Windows 및 Linux 컴퓨터의 텍스트 파일에서 이벤트를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-105">The Custom Logs data source in Log Analytics allows you to collect events from text files on both Windows and Linux computers.</span></span> <span data-ttu-id="7a0ef-106">많은 응용 프로그램이 Windows 이벤트 로그 또는 Syslog 같은 표준 로깅 서비스 대신 텍스트 파일에 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-106">Many applications log information to text files instead of standard logging services such as Windows Event log or Syslog.</span></span>  <span data-ttu-id="7a0ef-107">수집된 후에는, Log Analytics의 [사용자 지정 필드](log-analytics-custom-fields.md) 기능을 사용하여 로그의 각 레코드를 별도의 필드로 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-107">Once collected, you can parse each record in the log in to individual fields using the [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

![사용자 지정 로그 수집](media/log-analytics-data-sources-custom-logs/overview.png)

<span data-ttu-id="7a0ef-109">수집할 로그 파일은 다음 조건과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-109">The log files to be collected must match the following criteria.</span></span>

- <span data-ttu-id="7a0ef-110">로그는 줄 당 항목이 하나이거나 각 항목의 시작 지점에 다음 형식 중 하나와 일치하는 타임스탬프를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-110">The log must either have a single entry per line or use a timestamp matching one of the following formats at the start of each entry.</span></span>

    <span data-ttu-id="7a0ef-111">YYYY-MM-DD HH:MM:SS </span><span class="sxs-lookup"><span data-stu-id="7a0ef-111">YYYY-MM-DD HH:MM:SS</span></span><br><span data-ttu-id="7a0ef-112">M/D/YYYY HH:MM:SS AM/PM</span><span class="sxs-lookup"><span data-stu-id="7a0ef-112">M/D/YYYY HH:MM:SS AM/PM</span></span> <br><span data-ttu-id="7a0ef-113">Mon DD,YYYY HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="7a0ef-113">Mon DD,YYYY HH:MM:SS</span></span>

- <span data-ttu-id="7a0ef-114">로그 파일은 새 항목으로 파일을 덮어쓰는 순환 업데이트를 허용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-114">The log file must not allow circular updates where the file is overwritten with new entries.</span></span>
- <span data-ttu-id="7a0ef-115">로그 파일은 ASCII 또는 UTF-8 인코딩을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-115">The log file must use ASCII or UTF-8 encoding.</span></span>  <span data-ttu-id="7a0ef-116">UTF-16 등의 다른 형식은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-116">Other formats such as UTF-16 are not supported.</span></span>

>[!NOTE]
><span data-ttu-id="7a0ef-117">로그 파일에 중복된 항목이 있는 경우 Log Analytics에서 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-117">If there are duplicate entries in the log file, Log Analytics will collect them.</span></span>  <span data-ttu-id="7a0ef-118">그러나 검색 결과는 필터 결과가 결과 개수보다 더 많은 이벤트를 표시하는 위치에서 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-118">However, the search results will be inconsistent where the filter results show more events than the result count.</span></span>  <span data-ttu-id="7a0ef-119">이를 만드는 응용 프로그램에서 이 문제를 일으키는지 확인하도록 로그의 유효성을 검사하고 가능한 경우 사용자 지정 로그 컬렉션 정의를 만들기 전에 해결하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-119">It will be important that you validate the log to determine if the application that creates it is causing this behavior and address it if possible before creating the custom log collection definition.</span></span>  
>
  
## <a name="defining-a-custom-log"></a><span data-ttu-id="7a0ef-120">사용자 지정 로그 정의</span><span class="sxs-lookup"><span data-stu-id="7a0ef-120">Defining a custom log</span></span>
<span data-ttu-id="7a0ef-121">다음 절차에 따라 사용자 지정 로그 파일을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-121">Use the following procedure to define a custom log file.</span></span>  <span data-ttu-id="7a0ef-122">사용자 지정 로그를 추가하는 샘플에 대한 연습을 보려면 이 문서의 끝으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-122">Scroll to the end of this article for a walkthrough of a sample of adding a custom log.</span></span>

### <a name="step-1-open-the-custom-log-wizard"></a><span data-ttu-id="7a0ef-123">1단계.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-123">Step 1.</span></span> <span data-ttu-id="7a0ef-124">Custom Log Wizard(사용자 지정 로그 마법사) 열기</span><span class="sxs-lookup"><span data-stu-id="7a0ef-124">Open the Custom Log Wizard</span></span>
<span data-ttu-id="7a0ef-125">Custom Log Wizard(사용자 지정 로그 마법사)는 OMS 포털에서 실행되며 수집할 새 사용자 지정 로그를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-125">The Custom Log Wizard runs in the OMS portal and allows you to define a new custom log to collect.</span></span>

1. <span data-ttu-id="7a0ef-126">OMS 포털에서 **설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-126">In the OMS portal, go to **Settings**.</span></span>
2. <span data-ttu-id="7a0ef-127">**데이터**를 클릭한 다음 **사용자 지정 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-127">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="7a0ef-128">기본적으로, 모든 구성 변경은 모든 에이전트로 자동 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-128">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="7a0ef-129">Linux 에이전트에서, 구성 파일은 Fluentd 데이터 수집기로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-129">For Linux agents, a configuration file is sent to the Fluentd data collector.</span></span>  <span data-ttu-id="7a0ef-130">각 Linux 에이전트에서 이 파일을 수동으로 수정하려면, *Apply below configuration to my Linux machines*(아래 구성을 내 Linux 컴퓨터에 적용) 확인란 선택을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-130">If you wish to modify this file manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>
4. <span data-ttu-id="7a0ef-131">**추가+** 를 클릭하여 Custom Log Wizard(사용자 지정 로그 마법사)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-131">Click **Add+** to open the Custom Log Wizard.</span></span>

### <a name="step-2-upload-and-parse-a-sample-log"></a><span data-ttu-id="7a0ef-132">2단계.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-132">Step 2.</span></span> <span data-ttu-id="7a0ef-133">샘플 로그 업로드 및 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7a0ef-133">Upload and parse a sample log</span></span>
<span data-ttu-id="7a0ef-134">사용자 지정 로그 샘플을 업로드하는 것부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-134">You start by uploading a sample of the custom log.</span></span>  <span data-ttu-id="7a0ef-135">마법사는 사용자가 유효성을 검사할 수 있도록 이 파일의 항목을 구문 분석하고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-135">The wizard will parse and display the entries in this file for you to validate.</span></span>  <span data-ttu-id="7a0ef-136">Log Analytics는 사용자가 지정하는 구분 기호를 사용하여 각 레코드를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-136">Log Analytics will use the delimiter that you specify to identify each record.</span></span>

<span data-ttu-id="7a0ef-137">**새 줄** 은 기본적인 구분 기호이며 줄당 하나의 항목을 포함하는 로그 파일에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-137">**New Line** is the default delimiter and is used for log files that have a single entry per line.</span></span>  <span data-ttu-id="7a0ef-138">줄이 사용 가능한 형식 중 한 가지의 날짜와 시간으로 시작되는 경우에는, 두 줄 이상에 걸쳐있는 항목을 지원하는 **타임스탬프** 구분 기호를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-138">If the line starts with a date and time in one of the available formats, then you can specify a **Timestamp** delimiter which supports entries that span more than one line.</span></span>

<span data-ttu-id="7a0ef-139">타임스탬프 구분 기호가 사용되면, OMS에 저장된 각 레코드의 TimeGenerated 속성이 로그 파일의 해당 항목에 대해 지정된 날짜/시간으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-139">If a timestamp delimiter is used, then the TimeGenerated property of each record stored in OMS will be populated with the date/time specified for that entry in the log file.</span></span>  <span data-ttu-id="7a0ef-140">새 줄 구분 기호가 사용되는 경우에는, TimeGenerated가 Log Analytics 항목을 수집한 날짜와 시간으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-140">If a new line delimiter is used, then TimeGenerated is populated with date and time that Log Analytics collected the entry.</span></span>

> [!NOTE]
> <span data-ttu-id="7a0ef-141">Log Analytics는 현재 타임스탬프 구분 기호를 사용하여 로그로부터 수집된 날짜/시간을 UTC로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-141">Log Analytics currently treats the date/time collected from a log using a timestamp delimiter as UTC.</span></span>  <span data-ttu-id="7a0ef-142">이것은 곧 에이전트의 표준 시간대를 사용하도록 변경될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-142">This will soon be changed to use the time zone on the agent.</span></span>
>
>

1. <span data-ttu-id="7a0ef-143">**찾아보기** 를 클릭하고 샘플 파일로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-143">Click **Browse** and browse to a sample file.</span></span>  <span data-ttu-id="7a0ef-144">일부 브라우저에서는 이 단추의 레이블이 **파일 선택** 인 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-144">Note that this may button may be labeled **Choose File** in some browsers.</span></span>
2. <span data-ttu-id="7a0ef-145">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-145">Click **Next**.</span></span>
3. <span data-ttu-id="7a0ef-146">Custom Log Wizard(사용자 지정 로그 마법사)가 파일을 업로드하고 식별된 레코드를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-146">The Custom Log Wizard will upload the file and list the records that it identifies.</span></span>
4. <span data-ttu-id="7a0ef-147">새 레코드 식별에 사용된 구분 기호를 변경하고 로그 파일의 레코드를 가장 잘 식별하는 구분 기호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-147">Change the delimiter that is used to identify a new record and select the delimiter that best identifies the records in your log file.</span></span>
5. <span data-ttu-id="7a0ef-148">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-148">Click **Next**.</span></span>

### <a name="step-3-add-log-collection-paths"></a><span data-ttu-id="7a0ef-149">3단계.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-149">Step 3.</span></span> <span data-ttu-id="7a0ef-150">로그 수집 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7a0ef-150">Add log collection paths</span></span>
<span data-ttu-id="7a0ef-151">사용자 지정 로그를 찾을 수 있는 에이전트의 경로를 하나 이상의 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-151">You must define one or more paths on the agent where it can locate the custom log.</span></span>  <span data-ttu-id="7a0ef-152">로그 파일의 특정 경로 및 이름을 제공하거나 이름의 와일드카드를 포함하는 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-152">You can either provide a specific path and name for the log file, or you can specify a path with a wildcard for the name.</span></span>  <span data-ttu-id="7a0ef-153">이렇게 하면 매일 새 파일을 만드는 응용 프로그램을 지원하거나 하나의 파일이 일정한 크기에 도달하는 경우를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-153">This supports applications that create a new file each day or when one file reaches a certain size.</span></span>  <span data-ttu-id="7a0ef-154">하나의 로그 파일에 여러 경로를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-154">You can also provide multiple paths for a single log file.</span></span>

<span data-ttu-id="7a0ef-155">예를 들어, 응용 프로그램이 이름에 날짜가 포함된 로그 파일(예: log20100316.txt)을 매일 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-155">For example, an application might create a log file each day with the date included in the name as in log20100316.txt.</span></span> <span data-ttu-id="7a0ef-156">이런 로그의 패턴으로 *log\*.txt*를 사용할 수 있으며, 이것은 응용 프로그램의 명명 체계에 따르는 모든 로그 파일에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-156">A pattern for such a log might be *log\*.txt* which would apply to any log file following the application’s naming scheme.</span></span>

<span data-ttu-id="7a0ef-157">다음 테이블은 다른 로그 파일을 지정하는 데 유효한 패턴의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-157">The following table provides examples of valid patterns to specify different log files.</span></span>

| <span data-ttu-id="7a0ef-158">설명</span><span class="sxs-lookup"><span data-stu-id="7a0ef-158">Description</span></span> | <span data-ttu-id="7a0ef-159">Path</span><span class="sxs-lookup"><span data-stu-id="7a0ef-159">Path</span></span> |
|:--- |:--- |
| <span data-ttu-id="7a0ef-160">Windows 에이전트에서 확장명이 .txt인 *C:\Logs* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7a0ef-160">All files in *C:\Logs* with .txt extension on Windows agent</span></span> |<span data-ttu-id="7a0ef-161">C:\Logs\\\*.txt</span><span class="sxs-lookup"><span data-stu-id="7a0ef-161">C:\Logs\\\*.txt</span></span> |
| <span data-ttu-id="7a0ef-162">Windows 에이전트에서 이름이 log로 시작되고 확장명이 .txt인 *C:\Logs* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7a0ef-162">All files in *C:\Logs* with a name starting with log and a .txt extension on Windows agent</span></span> |<span data-ttu-id="7a0ef-163">C:\Logs\log\*.txt</span><span class="sxs-lookup"><span data-stu-id="7a0ef-163">C:\Logs\log\*.txt</span></span> |
| <span data-ttu-id="7a0ef-164">Linux 에이전트에서 확장명이 .txt인 */var/log/audit* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7a0ef-164">All files in */var/log/audit* with .txt extension on Linux agent</span></span> |<span data-ttu-id="7a0ef-165">/var/log/audit/*.txt</span><span class="sxs-lookup"><span data-stu-id="7a0ef-165">/var/log/audit/*.txt</span></span> |
| <span data-ttu-id="7a0ef-166">Linux 에이전트에서 이름이 log로 시작되고 확장명이 .txt인 */var/log/audit* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7a0ef-166">All files in */var/log/audit* with a name starting with log and a .txt extension on Linux agent</span></span> |<span data-ttu-id="7a0ef-167">/var/log/audit/log\*.txt</span><span class="sxs-lookup"><span data-stu-id="7a0ef-167">/var/log/audit/log\*.txt</span></span> |

1. <span data-ttu-id="7a0ef-168">Windows 또는 Linux를 선택하여 추가하는 경로 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-168">Select Windows or Linux to specify which path format you are adding.</span></span>
2. <span data-ttu-id="7a0ef-169">경로를 입력하고 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-169">Type in the path and click the **+** button.</span></span>
3. <span data-ttu-id="7a0ef-170">경로가 더 있으면 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-170">Repeat the process for any additional paths.</span></span>

### <a name="step-4-provide-a-name-and-description-for-the-log"></a><span data-ttu-id="7a0ef-171">4단계.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-171">Step 4.</span></span> <span data-ttu-id="7a0ef-172">로그의 이름과 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-172">Provide a name and description for the log</span></span>
<span data-ttu-id="7a0ef-173">지정한 이름은 위의 설명처럼 로그 유형에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-173">The name that you specify will be used for the log type as described above.</span></span>  <span data-ttu-id="7a0ef-174">파일을 사용자 지정 로그로 구분하기 위해 항상_CL로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-174">It will always end with _CL to distinguish it as a custom log.</span></span>

1. <span data-ttu-id="7a0ef-175">로그의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-175">Type in a name for the log.</span></span>  <span data-ttu-id="7a0ef-176">**\_CL** 접미사가 자동으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-176">The **\_CL** suffix is automatically provided.</span></span>
2. <span data-ttu-id="7a0ef-177">선택적인 **설명**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-177">Add an optional **Description**.</span></span>
3. <span data-ttu-id="7a0ef-178">**다음**을 클릭하여 사용자 지정 로그 정의를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-178">Click **Next** to save the custom log definition.</span></span>

### <a name="step-5-validate-that-the-custom-logs-are-being-collected"></a><span data-ttu-id="7a0ef-179">5단계.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-179">Step 5.</span></span> <span data-ttu-id="7a0ef-180">사용자 지정 로그를 수집 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="7a0ef-180">Validate that the custom logs are being collected</span></span>
<span data-ttu-id="7a0ef-181">Log Analytics에 새 사용자 지정 로그의 초기 데이터가 나타나기 까지 최대 한 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-181">It may take up to an hour for the initial data from a new custom log to appear in Log Analytics.</span></span>  <span data-ttu-id="7a0ef-182">사용자 지정 로그를 정의한 시점부터, 사용자가 지정한 경로에서 찾은 로그로부터 항목을 수집하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-182">It will start collecting entries from the logs found in the path you specified from the point that you defined the custom log.</span></span>  <span data-ttu-id="7a0ef-183">사용자 지정 로그를 만드는 동안 업로드한 항목은 유지하지 않고, 찾는 로그 파일에 이미 존재하는 항목을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-183">It will not retain the entries that you uploaded during the custom log creation, but it will collect already existing entries in the log files that it locates.</span></span>

<span data-ttu-id="7a0ef-184">Log Analytics가 사용자 지정 로그에서 수집을 시작하면, 해당 레코드를 로그 검색을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-184">Once Log Analytics starts collecting from the custom log, its records will be available with a Log Search.</span></span>  <span data-ttu-id="7a0ef-185">사용자 지정 로그에 지정한 이름을 쿼리의 **유형**으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-185">Use the name that you gave the custom log as the **Type** in your query.</span></span>

> [!NOTE]
> <span data-ttu-id="7a0ef-186">RawData 속성이 검색에 없으면, 브라우저를 닫았다가 다시 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-186">If the RawData property is missing from the search, you may need to close and reopen your browser.</span></span>
>
>

### <a name="step-6-parse-the-custom-log-entries"></a><span data-ttu-id="7a0ef-187">6단계.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-187">Step 6.</span></span> <span data-ttu-id="7a0ef-188">사용자 지정 로그 항목 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7a0ef-188">Parse the custom log entries</span></span>
<span data-ttu-id="7a0ef-189">전체 로그 항목은 **RawData**라는 하나의 속성에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-189">The entire log entry will be stored in a single property called **RawData**.</span></span>  <span data-ttu-id="7a0ef-190">각 항목에 포함된 다양한 종류의 정보를 레코드에 저장된 개별 속성으로 분리하려는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-190">You will most likely want to separate the different pieces of information in each entry into individual properties stored in the record.</span></span>  <span data-ttu-id="7a0ef-191">이런 작업은 Log Analytics의 [사용자 지정 필드](log-analytics-custom-fields.md) 기능을 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-191">You do this using the [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

<span data-ttu-id="7a0ef-192">사용자 지정 로그 항목을 구문 분석하는 자세한 단계는 여기에 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-192">Detailed steps for parsing the custom log entry are not provided here.</span></span>  <span data-ttu-id="7a0ef-193">이 정보는 [사용자 지정 필드](log-analytics-custom-fields.md) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-193">Please refer to the [Custom Fields](log-analytics-custom-fields.md) documentation for this information.</span></span>

## <a name="disabling-a-custom-log"></a><span data-ttu-id="7a0ef-194">사용자 지정 로그 비활성화</span><span class="sxs-lookup"><span data-stu-id="7a0ef-194">Disabling a custom log</span></span>
<span data-ttu-id="7a0ef-195">생성된 사용자 지정 로그 정의는 제거할 수 없지만 모든 수집 경로를 제거하여 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-195">You cannot remove a custom log definition once it's been created, but you can disable it by removing all of its collection paths.</span></span>

1. <span data-ttu-id="7a0ef-196">OMS 포털에서 **설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-196">In the OMS portal, go to **Settings**.</span></span>
2. <span data-ttu-id="7a0ef-197">**데이터**를 클릭한 다음 **사용자 지정 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-197">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="7a0ef-198">비활성화할 사용자 지정 로그 정의 옆에 있는 **세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-198">Click **Details** next to the custom log definition to disable.</span></span>
4. <span data-ttu-id="7a0ef-199">사용자 지정 로그 정의에 대한 각 수집 경로를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-199">Remove each of the collection paths for the custom log definition.</span></span>

## <a name="data-collection"></a><span data-ttu-id="7a0ef-200">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="7a0ef-200">Data collection</span></span>
<span data-ttu-id="7a0ef-201">Log Analytics는 각 사용자 지정 로그로부터 새로운 항목을 약 5분마다 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-201">Log Analytics will collect new entries from each custom log approximately every 5 minutes.</span></span>  <span data-ttu-id="7a0ef-202">에이전트는 데이터를 수집하는 각 로그 파일에서 해당 위치를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-202">The agent will record its place in each log file that it collects from.</span></span>  <span data-ttu-id="7a0ef-203">에이전트가 일정 기간 동안 오프라인 상태로 전환된 경우 Log Analytics는 마지막으로 오프라인 상태가 유지된 위치에서 항목을 수집하며, 이는 에이전트가 오프라인 상태에 있는 동안 해당 항목이 생성된 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-203">If the agent goes offline for a period of time, then Log Analytics will collect entries from where it last left off, even if those entries were created while the agent was offline.</span></span>

<span data-ttu-id="7a0ef-204">로그 항목의 전체 내용은 **RawData**라는 단일 속성에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-204">The entire contents of the log entry are written to a single property called **RawData**.</span></span>  <span data-ttu-id="7a0ef-205">이것을 사용자 지정 로그를 만든 후에 [사용자 지정 필드](log-analytics-custom-fields.md)를 정의하여 개별적으로 검색하고 분석할 수 있는 여러 개의 속성으로 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-205">You can parse this into multiple properties that can be analyzed and searched separately by defining [Custom Fields](log-analytics-custom-fields.md) after you have created the custom log.</span></span>

## <a name="custom-log-record-properties"></a><span data-ttu-id="7a0ef-206">사용자 지정 로그 레코드 속성</span><span class="sxs-lookup"><span data-stu-id="7a0ef-206">Custom log record properties</span></span>
<span data-ttu-id="7a0ef-207">사용자 지정 로그 레코드에는 사용자가 제공하는 로그 이름의 유형과 다음 테이블의 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-207">Custom log records have a type with the log name that you provide and the properties in the following table.</span></span>

| <span data-ttu-id="7a0ef-208">속성</span><span class="sxs-lookup"><span data-stu-id="7a0ef-208">Property</span></span> | <span data-ttu-id="7a0ef-209">설명</span><span class="sxs-lookup"><span data-stu-id="7a0ef-209">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7a0ef-210">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="7a0ef-210">TimeGenerated</span></span> |<span data-ttu-id="7a0ef-211">Log Analytics에 의해 레코드가 수집된 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-211">Date and time that the record was collected by Log Analytics.</span></span>  <span data-ttu-id="7a0ef-212">로그에 시간 기반 구분 기호가 사용되는 경우, 항목에서 수집한 시간이 여기에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-212">If the log uses a time-based delimiter then this is the time collected from the entry.</span></span> |
| <span data-ttu-id="7a0ef-213">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="7a0ef-213">SourceSystem</span></span> |<span data-ttu-id="7a0ef-214">레코드가 수집된 에이전트의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-214">Type of agent the record was collected from.</span></span> <br> <span data-ttu-id="7a0ef-215">OpsManager – Windows 에이전트, 직접 연결 또는 System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="7a0ef-215">OpsManager – Windows agent, either direct connect or System Center Operations Manager</span></span> <br> <span data-ttu-id="7a0ef-216">Linux – 모든 Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="7a0ef-216">Linux – All Linux agents</span></span> |
| <span data-ttu-id="7a0ef-217">RawData</span><span class="sxs-lookup"><span data-stu-id="7a0ef-217">RawData</span></span> |<span data-ttu-id="7a0ef-218">수집된 항목의 전체 텍스트.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-218">Full text of the collected entry.</span></span> |
| <span data-ttu-id="7a0ef-219">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="7a0ef-219">ManagementGroupName</span></span> |<span data-ttu-id="7a0ef-220">System Center Operations Manage 에이전트의 관리 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-220">Name of the management group for System Center Operations Manage agents.</span></span>  <span data-ttu-id="7a0ef-221">다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-221">For other agents, this is AOI-\<workspace ID\></span></span> |

## <a name="log-searches-with-custom-log-records"></a><span data-ttu-id="7a0ef-222">사용자 지정 로그 레코드를 사용한 로그 검색</span><span class="sxs-lookup"><span data-stu-id="7a0ef-222">Log searches with custom log records</span></span>
<span data-ttu-id="7a0ef-223">사용자 지정 로그의 레코드는 다른 데이터 소스의 레코드처럼 OMS 리포지토리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-223">Records from custom logs are stored in the OMS repository just like records from any other data source.</span></span>  <span data-ttu-id="7a0ef-224">Type이 로그를 정의할 때 제공한 이름과 일치하기 때문에 검색에 Type 속성을 이용하여 특정 로그에서 수집한 레코드를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-224">They will have a type matching the name that you provide when you define the log, so you can use the Type property in your search to retrieve records collected from a specific log.</span></span>

<span data-ttu-id="7a0ef-225">다음 테이블은 사용자 지정 로그로부터 레코드를 검색하는 로그 검색의 다양한 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-225">The following table provides different examples of log searches that retrieve records from custom logs.</span></span>

| <span data-ttu-id="7a0ef-226">쿼리</span><span class="sxs-lookup"><span data-stu-id="7a0ef-226">Query</span></span> | <span data-ttu-id="7a0ef-227">설명</span><span class="sxs-lookup"><span data-stu-id="7a0ef-227">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7a0ef-228">Type=MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="7a0ef-228">Type=MyApp_CL</span></span> |<span data-ttu-id="7a0ef-229">이름 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-229">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="7a0ef-230">Type=MyApp_CL Severity_CF=error</span><span class="sxs-lookup"><span data-stu-id="7a0ef-230">Type=MyApp_CL Severity_CF=error</span></span> |<span data-ttu-id="7a0ef-231">이름이 *Severity_CF*인 사용자 지정 필드의 값이 *error*이고 이름이 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-231">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |

>[!NOTE]
> <span data-ttu-id="7a0ef-232">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위의 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-232">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="7a0ef-233">쿼리</span><span class="sxs-lookup"><span data-stu-id="7a0ef-233">Query</span></span> | <span data-ttu-id="7a0ef-234">설명</span><span class="sxs-lookup"><span data-stu-id="7a0ef-234">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7a0ef-235">MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="7a0ef-235">MyApp_CL</span></span> |<span data-ttu-id="7a0ef-236">이름 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-236">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="7a0ef-237">MyApp_CL &#124; where Severity_CF=="error"</span><span class="sxs-lookup"><span data-stu-id="7a0ef-237">MyApp_CL &#124; where Severity_CF=="error"</span></span> |<span data-ttu-id="7a0ef-238">이름이 *Severity_CF*인 사용자 지정 필드의 값이 *error*이고 이름이 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-238">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a><span data-ttu-id="7a0ef-239">사용자 지정 로그 추가 샘플 연습</span><span class="sxs-lookup"><span data-stu-id="7a0ef-239">Sample walkthrough of adding a custom log</span></span>
<span data-ttu-id="7a0ef-240">다음 섹션은 사용자 지정 로그를 만드는 예제를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-240">The following section walks through an example of creating a custom log.</span></span>  <span data-ttu-id="7a0ef-241">수집되는 샘플 로그에는 각 줄에 하나의 항목이 포함되며, 각 줄은 날짜와 시간으로 시작되고 코드, 상태 및 메시지에 대해 쉼표로 구분된 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-241">The sample log being collected has a single entry on each line starting with a date and time and then comma-delimited fields for code, status, and message.</span></span>  <span data-ttu-id="7a0ef-242">몇 가지 샘플 항목이 아래에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-242">Several sample entries are shown below.</span></span>

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect to database
    2016-03-10 01:31:34 303,Error,Application lost connection to database

### <a name="upload-and-parse-a-sample-log"></a><span data-ttu-id="7a0ef-243">샘플 로그 업로드 및 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7a0ef-243">Upload and parse a sample log</span></span>
<span data-ttu-id="7a0ef-244">로그 파일 중 하나를 제공하며 수집할 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-244">We provide one of the log files and can see the events that it will be collecting.</span></span>  <span data-ttu-id="7a0ef-245">이 경우 New Line(새 줄)은 충분한 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-245">In this case New Line is a sufficient delimiter.</span></span>  <span data-ttu-id="7a0ef-246">하지만 로그의 단일 항목이 여러 줄에 걸치는 경우 타임스탬프 구분 기호가 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-246">If a single entry in the log could span multiple lines though, then a timestamp delimiter would need to be used.</span></span>

![샘플 로그 업로드 및 구문 분석](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a><span data-ttu-id="7a0ef-248">로그 수집 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7a0ef-248">Add log collection paths</span></span>
<span data-ttu-id="7a0ef-249">로그 파일은 *C:\MyApp\Logs*에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-249">The log files will be located in *C:\MyApp\Logs*.</span></span>  <span data-ttu-id="7a0ef-250">*appYYYYMMDD.log*패턴의 날짜를 포함하는 이름으로 매일 새 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-250">A new file will be created each day with a name that includes the date in the pattern *appYYYYMMDD.log*.</span></span>  <span data-ttu-id="7a0ef-251">이 로그에 충분한 패턴은 *C:\MyApp\Logs\\\*.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-251">A sufficient pattern for this log would be *C:\MyApp\Logs\\\*.log*.</span></span>

![로그 수집 경로](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-the-log"></a><span data-ttu-id="7a0ef-253">로그의 이름과 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-253">Provide a name and description for the log</span></span>
<span data-ttu-id="7a0ef-254">*MyApp_CL*이라는 이름을 사용하여 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-254">We use a name of *MyApp_CL* and type in a **Description**.</span></span>

![로그 이름](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-the-custom-logs-are-being-collected"></a><span data-ttu-id="7a0ef-256">사용자 지정 로그를 수집 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="7a0ef-256">Validate that the custom logs are being collected</span></span>
<span data-ttu-id="7a0ef-257">수집된 로그의 모든 레코드를 반환하는 *Type=MyApp_CL* 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-257">We use a query of *Type=MyApp_CL* to return all records from the collected log.</span></span>

![사용자 지정 필드가 없는 로그 쿼리](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-the-custom-log-entries"></a><span data-ttu-id="7a0ef-259">사용자 지정 로그 항목 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7a0ef-259">Parse the custom log entries</span></span>
<span data-ttu-id="7a0ef-260">사용자 지정 필드를 사용하여 *EventTime*, *Code*, *Status*, *Message* 필드를 정의하며, 쿼리에 의해 반환되는 레코드의 차이를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-260">We use Custom Fields to define the *EventTime*, *Code*, *Status*, and *Message* fields and we can see the difference in the records that are returned by the query.</span></span>

![사용자 지정 필드가 있는 로그 쿼리](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a><span data-ttu-id="7a0ef-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a0ef-262">Next steps</span></span>
* <span data-ttu-id="7a0ef-263">[사용자 지정 필드](log-analytics-custom-fields.md)를 사용하여 사용자 지정 로그의 항목을 개별적인 필드로 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-263">Use [Custom Fields](log-analytics-custom-fields.md) to parse the entries in the custom log in to individual fields.</span></span>
* <span data-ttu-id="7a0ef-264">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a0ef-264">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
