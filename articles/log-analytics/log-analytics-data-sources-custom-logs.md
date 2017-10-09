---
title: "사용자 지정 aaaCollect OMS 로그 분석 로그인 | Microsoft Docs"
description: "Log Analytics는 Windows와 Linux 컴퓨터의 텍스트 파일에서 이벤트를 수집할 수 있습니다.  이 문서에서는 toodefine 새로운 사용자 지정 로그 및 hello 레코드의 세부 정보 작성 방법과 hello OMS 리포지토리에 설명 합니다."
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
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a><span data-ttu-id="7efaa-104">Log Analytics의 사용자 지정 로그</span><span class="sxs-lookup"><span data-stu-id="7efaa-104">Custom logs in Log Analytics</span></span>
<span data-ttu-id="7efaa-105">hello 사용자 지정 로그 데이터 원본 로그 분석에는 Windows 및 Linux 컴퓨터에 있는 텍스트 파일에서 toocollect 이벤트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-105">hello Custom Logs data source in Log Analytics allows you toocollect events from text files on both Windows and Linux computers.</span></span> <span data-ttu-id="7efaa-106">대부분의 응용 프로그램 Windows 이벤트 로그 또는 Syslog와 같은 표준 로깅 서비스 대신 tootext 파일 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-106">Many applications log information tootext files instead of standard logging services such as Windows Event log or Syslog.</span></span>  <span data-ttu-id="7efaa-107">Hello 로그인 hello를 사용 하 여 tooindividual 필드의 각 레코드를 구문 분석할 수 수집 면 [사용자 정의 필드](log-analytics-custom-fields.md) 로그 분석의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-107">Once collected, you can parse each record in hello log in tooindividual fields using hello [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

![사용자 지정 로그 수집](media/log-analytics-data-sources-custom-logs/overview.png)

<span data-ttu-id="7efaa-109">수집 된 hello 로그 파일 toobe hello 조건에 따라 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-109">hello log files toobe collected must match hello following criteria.</span></span>

- <span data-ttu-id="7efaa-110">hello 로그 항목이 줄에 하나씩 있을 하거나 타임 스탬프 짝이 되는 각 항목의 시작 부분 hello에 서식을 hello 다음 중 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-110">hello log must either have a single entry per line or use a timestamp matching one of hello following formats at hello start of each entry.</span></span>

    <span data-ttu-id="7efaa-111">YYYY-MM-DD HH:MM:SS </span><span class="sxs-lookup"><span data-stu-id="7efaa-111">YYYY-MM-DD HH:MM:SS</span></span><br><span data-ttu-id="7efaa-112">M/D/YYYY HH:MM:SS AM/PM</span><span class="sxs-lookup"><span data-stu-id="7efaa-112">M/D/YYYY HH:MM:SS AM/PM</span></span> <br><span data-ttu-id="7efaa-113">Mon DD,YYYY HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="7efaa-113">Mon DD,YYYY HH:MM:SS</span></span>

- <span data-ttu-id="7efaa-114">hello 로그 파일을 허용 하지 않아야 순환 업데이트 새 항목 hello 파일은 덮어쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-114">hello log file must not allow circular updates where hello file is overwritten with new entries.</span></span>
- <span data-ttu-id="7efaa-115">hello 로그 파일은 ASCII 또는 utf-8 인코딩을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-115">hello log file must use ASCII or UTF-8 encoding.</span></span>  <span data-ttu-id="7efaa-116">UTF-16 등의 다른 형식은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-116">Other formats such as UTF-16 are not supported.</span></span>

>[!NOTE]
><span data-ttu-id="7efaa-117">Hello 로그 파일에 중복 된 항목이 있는 경우 로그 분석 로그를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-117">If there are duplicate entries in hello log file, Log Analytics will collect them.</span></span>  <span data-ttu-id="7efaa-118">그러나 hello 검색 결과 일치 하지 않을 수 hello 필터 결과 hello 결과 개수 보다 더 많은 이벤트를 표시 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-118">However, hello search results will be inconsistent where hello filter results show more events than hello result count.</span></span>  <span data-ttu-id="7efaa-119">이 동작을 일으키는 hello 응용 프로그램을 만든 경우 hello 로그 toodetermine 유효성을 검사 하 고 hello 사용자 지정 로그 컬렉션 정의 만들기 전에 가능한 경우 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-119">It will be important that you validate hello log toodetermine if hello application that creates it is causing this behavior and address it if possible before creating hello custom log collection definition.</span></span>  
>
  
## <a name="defining-a-custom-log"></a><span data-ttu-id="7efaa-120">사용자 지정 로그 정의</span><span class="sxs-lookup"><span data-stu-id="7efaa-120">Defining a custom log</span></span>
<span data-ttu-id="7efaa-121">프로시저 toodefine 사용자 지정 로그 파일을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-121">Use hello following procedure toodefine a custom log file.</span></span>  <span data-ttu-id="7efaa-122">사용자 지정 로그를 추가 하는 샘플의 연습은이 문서의 끝을 toohello 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="7efaa-122">Scroll toohello end of this article for a walkthrough of a sample of adding a custom log.</span></span>

### <a name="step-1-open-hello-custom-log-wizard"></a><span data-ttu-id="7efaa-123">1단계.</span><span class="sxs-lookup"><span data-stu-id="7efaa-123">Step 1.</span></span> <span data-ttu-id="7efaa-124">Hello 사용자 지정 로그 마법사를 열려면</span><span class="sxs-lookup"><span data-stu-id="7efaa-124">Open hello Custom Log Wizard</span></span>
<span data-ttu-id="7efaa-125">사용자 지정 로그 마법사 hello hello OMS 포털에서 실행 되며 새 사용자 지정 로그 toocollect toodefine 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-125">hello Custom Log Wizard runs in hello OMS portal and allows you toodefine a new custom log toocollect.</span></span>

1. <span data-ttu-id="7efaa-126">Hello OMS 포털에서 이동 너무**설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-126">In hello OMS portal, go too**Settings**.</span></span>
2. <span data-ttu-id="7efaa-127">**데이터**를 클릭한 다음 **사용자 지정 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-127">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="7efaa-128">기본적으로 모든 구성 변경 내용은 tooall 에이전트를 자동으로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-128">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="7efaa-129">Linux 에이전트에 대 한 구성 파일에는 toohello Fluentd 데이터 수집기를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-129">For Linux agents, a configuration file is sent toohello Fluentd data collector.</span></span>  <span data-ttu-id="7efaa-130">각 Linux 에이전트에서 수동으로이 파일 toomodify 원하는 hello 확인란의 선택을 취소 한 다음 *구성 toomy Linux 컴퓨터 아래 적용*합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-130">If you wish toomodify this file manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>
4. <span data-ttu-id="7efaa-131">클릭 **추가 +** tooopen hello 사용자 지정 로그 마법사.</span><span class="sxs-lookup"><span data-stu-id="7efaa-131">Click **Add+** tooopen hello Custom Log Wizard.</span></span>

### <a name="step-2-upload-and-parse-a-sample-log"></a><span data-ttu-id="7efaa-132">2단계.</span><span class="sxs-lookup"><span data-stu-id="7efaa-132">Step 2.</span></span> <span data-ttu-id="7efaa-133">샘플 로그 업로드 및 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7efaa-133">Upload and parse a sample log</span></span>
<span data-ttu-id="7efaa-134">Hello 사용자 지정 로그의 샘플을 업로드 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-134">You start by uploading a sample of hello custom log.</span></span>  <span data-ttu-id="7efaa-135">hello 마법사는 구문 분석 하 고 toovalidate 하기 위해이 파일에 hello 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-135">hello wizard will parse and display hello entries in this file for you toovalidate.</span></span>  <span data-ttu-id="7efaa-136">로그 분석 hello 구분 기호를 지정 하는 tooidentify 각 레코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-136">Log Analytics will use hello delimiter that you specify tooidentify each record.</span></span>

<span data-ttu-id="7efaa-137">**새 줄** hello 기본 구분 기호 이며 줄에 하나씩 단일 항목이 포함 된 로그 파일에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-137">**New Line** is hello default delimiter and is used for log files that have a single entry per line.</span></span>  <span data-ttu-id="7efaa-138">Hello 줄 날짜 및 시간 hello 사용 가능한 형식 중 하나로 시작 하 여 다음을 지정할 수 있습니다 하는 경우는 **타임 스탬프** 구분 기호는 둘 이상의 줄에 걸쳐 있는 항목을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-138">If hello line starts with a date and time in one of hello available formats, then you can specify a **Timestamp** delimiter which supports entries that span more than one line.</span></span>

<span data-ttu-id="7efaa-139">타임 스탬프 구분 기호를 사용 하는 경우 OMS에 저장 된 각 레코드의 hello TimeGenerated 속성 됩니다 hello 날짜/시간 hello 로그 파일에서 해당 항목에 대해 지정 된 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-139">If a timestamp delimiter is used, then hello TimeGenerated property of each record stored in OMS will be populated with hello date/time specified for that entry in hello log file.</span></span>  <span data-ttu-id="7efaa-140">새 줄 구분 기호를 사용 하는 경우 TimeGenerated은 날짜 및 시간은 로그 분석 수집 hello 항목으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-140">If a new line delimiter is used, then TimeGenerated is populated with date and time that Log Analytics collected hello entry.</span></span>

> [!NOTE]
> <span data-ttu-id="7efaa-141">현재 로그 분석 hello 날짜/시간에서 UTC로 타임 스탬프 구분 기호를 사용 하 여 로그 수집을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-141">Log Analytics currently treats hello date/time collected from a log using a timestamp delimiter as UTC.</span></span>  <span data-ttu-id="7efaa-142">곧 hello 에이전트에서 변경 된 toouse hello 표준 시간대 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-142">This will soon be changed toouse hello time zone on hello agent.</span></span>
>
>

1. <span data-ttu-id="7efaa-143">클릭 **찾아보기** tooa 샘플 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-143">Click **Browse** and browse tooa sample file.</span></span>  <span data-ttu-id="7efaa-144">일부 브라우저에서는 이 단추의 레이블이 **파일 선택** 인 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-144">Note that this may button may be labeled **Choose File** in some browsers.</span></span>
2. <span data-ttu-id="7efaa-145">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-145">Click **Next**.</span></span>
3. <span data-ttu-id="7efaa-146">사용자 지정 로그 마법사 hello를 식별 하는 hello 파일 및 목록 hello 레코드를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-146">hello Custom Log Wizard will upload hello file and list hello records that it identifies.</span></span>
4. <span data-ttu-id="7efaa-147">사용 되는 tooidentify 새 레코드를 구성 된 hello 구분 기호 및 로그 파일의 hello 레코드를 가장 잘 식별 하는 select hello 구분 기호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-147">Change hello delimiter that is used tooidentify a new record and select hello delimiter that best identifies hello records in your log file.</span></span>
5. <span data-ttu-id="7efaa-148">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-148">Click **Next**.</span></span>

### <a name="step-3-add-log-collection-paths"></a><span data-ttu-id="7efaa-149">3단계.</span><span class="sxs-lookup"><span data-stu-id="7efaa-149">Step 3.</span></span> <span data-ttu-id="7efaa-150">로그 수집 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7efaa-150">Add log collection paths</span></span>
<span data-ttu-id="7efaa-151">Hello 사용자 지정 로그를 찾을 수 있는 hello 에이전트에서 하나 이상의 경로 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-151">You must define one or more paths on hello agent where it can locate hello custom log.</span></span>  <span data-ttu-id="7efaa-152">특정 경로 및 hello 로그 파일에 대 한 이름을 입력 하거나 또는 와일드 카드 hello 이름에 대 한 경로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-152">You can either provide a specific path and name for hello log file, or you can specify a path with a wildcard for hello name.</span></span>  <span data-ttu-id="7efaa-153">이렇게 하면 매일 새 파일을 만드는 응용 프로그램을 지원하거나 하나의 파일이 일정한 크기에 도달하는 경우를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-153">This supports applications that create a new file each day or when one file reaches a certain size.</span></span>  <span data-ttu-id="7efaa-154">하나의 로그 파일에 여러 경로를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-154">You can also provide multiple paths for a single log file.</span></span>

<span data-ttu-id="7efaa-155">예를 들어 응용 프로그램 수 로그 파일을 매일 날짜로를 만들어 hello log20100316.txt에서와 같이 hello 이름에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-155">For example, an application might create a log file each day with hello date included in hello name as in log20100316.txt.</span></span> <span data-ttu-id="7efaa-156">이러한 로그에 대 한 패턴 수도 *로그\*.txt* hello 응용 프로그램을 다음 tooany 로그 파일을 적용할 수 있는 명명 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-156">A pattern for such a log might be *log\*.txt* which would apply tooany log file following hello application’s naming scheme.</span></span>

<span data-ttu-id="7efaa-157">hello 다음 표에서 유효한 패턴의 예 toospecify 서로 다른 파일.</span><span class="sxs-lookup"><span data-stu-id="7efaa-157">hello following table provides examples of valid patterns toospecify different log files.</span></span>

| <span data-ttu-id="7efaa-158">설명</span><span class="sxs-lookup"><span data-stu-id="7efaa-158">Description</span></span> | <span data-ttu-id="7efaa-159">Path</span><span class="sxs-lookup"><span data-stu-id="7efaa-159">Path</span></span> |
|:--- |:--- |
| <span data-ttu-id="7efaa-160">Windows 에이전트에서 확장명이 .txt인 *C:\Logs* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7efaa-160">All files in *C:\Logs* with .txt extension on Windows agent</span></span> |<span data-ttu-id="7efaa-161">C:\Logs\\\*.txt</span><span class="sxs-lookup"><span data-stu-id="7efaa-161">C:\Logs\\\*.txt</span></span> |
| <span data-ttu-id="7efaa-162">Windows 에이전트에서 이름이 log로 시작되고 확장명이 .txt인 *C:\Logs* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7efaa-162">All files in *C:\Logs* with a name starting with log and a .txt extension on Windows agent</span></span> |<span data-ttu-id="7efaa-163">C:\Logs\log\*.txt</span><span class="sxs-lookup"><span data-stu-id="7efaa-163">C:\Logs\log\*.txt</span></span> |
| <span data-ttu-id="7efaa-164">Linux 에이전트에서 확장명이 .txt인 */var/log/audit* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7efaa-164">All files in */var/log/audit* with .txt extension on Linux agent</span></span> |<span data-ttu-id="7efaa-165">/var/log/audit/*.txt</span><span class="sxs-lookup"><span data-stu-id="7efaa-165">/var/log/audit/*.txt</span></span> |
| <span data-ttu-id="7efaa-166">Linux 에이전트에서 이름이 log로 시작되고 확장명이 .txt인 */var/log/audit* 내 모든 파일</span><span class="sxs-lookup"><span data-stu-id="7efaa-166">All files in */var/log/audit* with a name starting with log and a .txt extension on Linux agent</span></span> |<span data-ttu-id="7efaa-167">/var/log/audit/log\*.txt</span><span class="sxs-lookup"><span data-stu-id="7efaa-167">/var/log/audit/log\*.txt</span></span> |

1. <span data-ttu-id="7efaa-168">어떤 경로 형식을 추가 하는 Windows 또는 Linux toospecify를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-168">Select Windows or Linux toospecify which path format you are adding.</span></span>
2. <span data-ttu-id="7efaa-169">Hello 경로 입력 하 고 hello 클릭  **+**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-169">Type in hello path and click hello **+** button.</span></span>
3. <span data-ttu-id="7efaa-170">모든 추가 경로 대 한 hello 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-170">Repeat hello process for any additional paths.</span></span>

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a><span data-ttu-id="7efaa-171">4단계.</span><span class="sxs-lookup"><span data-stu-id="7efaa-171">Step 4.</span></span> <span data-ttu-id="7efaa-172">이름 및 hello 로그에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-172">Provide a name and description for hello log</span></span>
<span data-ttu-id="7efaa-173">hello 지정한 이름이 사용 됩니다 hello 로그 형식에 대해 위에서 설명한 것 처럼.</span><span class="sxs-lookup"><span data-stu-id="7efaa-173">hello name that you specify will be used for hello log type as described above.</span></span>  <span data-ttu-id="7efaa-174">항상으로 끝납니다 _CL toodistinguish 것으로 사용자 지정 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-174">It will always end with _CL toodistinguish it as a custom log.</span></span>

1. <span data-ttu-id="7efaa-175">Hello 로그에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-175">Type in a name for hello log.</span></span>  <span data-ttu-id="7efaa-176">hello  **\_CL** 접미사가 자동으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-176">hello **\_CL** suffix is automatically provided.</span></span>
2. <span data-ttu-id="7efaa-177">선택적인 **설명**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-177">Add an optional **Description**.</span></span>
3. <span data-ttu-id="7efaa-178">클릭 **다음** toosave hello 사용자 지정 로그 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-178">Click **Next** toosave hello custom log definition.</span></span>

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a><span data-ttu-id="7efaa-179">5단계.</span><span class="sxs-lookup"><span data-stu-id="7efaa-179">Step 5.</span></span> <span data-ttu-id="7efaa-180">Hello 사용자 지정 로그를 수집 하는 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7efaa-180">Validate that hello custom logs are being collected</span></span>
<span data-ttu-id="7efaa-181">로그 분석에서 새 사용자 지정 로그 tooappear에서 초기 데이터 hello에 대 한 tooan 시간을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-181">It may take up tooan hour for hello initial data from a new custom log tooappear in Log Analytics.</span></span>  <span data-ttu-id="7efaa-182">Hello에서 항목을 수집을 시작 하면 정의 된 hello 사용자 지정 로그에 hello 지 점으로부터 지정한 로그 hello 경로에서 발견 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-182">It will start collecting entries from hello logs found in hello path you specified from hello point that you defined hello custom log.</span></span>  <span data-ttu-id="7efaa-183">Hello 사용자 지정 로그를 만드는 중에 업로드 하는 hello 항목 유지 되지 않습니다 되지만 찾을 hello 로그 파일에 이미 기존 항목을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-183">It will not retain hello entries that you uploaded during hello custom log creation, but it will collect already existing entries in hello log files that it locates.</span></span>

<span data-ttu-id="7efaa-184">로그 분석 시작 hello 사용자 지정 로그에서에서 수집 되 면 해당 레코드는 로그 검색을 통해 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-184">Once Log Analytics starts collecting from hello custom log, its records will be available with a Log Search.</span></span>  <span data-ttu-id="7efaa-185">Hello 사용자 지정 로그 hello로 지정한 사용 하 여 hello 이름을 **형식** 쿼리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-185">Use hello name that you gave hello custom log as hello **Type** in your query.</span></span>

> [!NOTE]
> <span data-ttu-id="7efaa-186">Hello RawData 속성 hello 검색에서 없는 경우에 tooclose 필요 하 고 브라우저를 다시 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-186">If hello RawData property is missing from hello search, you may need tooclose and reopen your browser.</span></span>
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a><span data-ttu-id="7efaa-187">6단계.</span><span class="sxs-lookup"><span data-stu-id="7efaa-187">Step 6.</span></span> <span data-ttu-id="7efaa-188">Hello 사용자 지정 로그 항목을 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7efaa-188">Parse hello custom log entries</span></span>
<span data-ttu-id="7efaa-189">hello 전체 로그 항목 라는 단일 속성에 저장 될 **RawData**합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-189">hello entire log entry will be stored in a single property called **RawData**.</span></span>  <span data-ttu-id="7efaa-190">대개 tooseparate hello 다른 여러 hello 레코드에 저장 된 개별 속성에 각 항목에 대 한 정보 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-190">You will most likely want tooseparate hello different pieces of information in each entry into individual properties stored in hello record.</span></span>  <span data-ttu-id="7efaa-191">이렇게 하면 hello를 사용 하 여 [사용자 정의 필드](log-analytics-custom-fields.md) 로그 분석의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-191">You do this using hello [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

<span data-ttu-id="7efaa-192">Hello 사용자 지정 로그 항목을 구문 분석 하는 자세한 단계는 여기 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-192">Detailed steps for parsing hello custom log entry are not provided here.</span></span>  <span data-ttu-id="7efaa-193">Toohello를 참조 하십시오 [사용자 정의 필드](log-analytics-custom-fields.md) 이 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-193">Please refer toohello [Custom Fields](log-analytics-custom-fields.md) documentation for this information.</span></span>

## <a name="disabling-a-custom-log"></a><span data-ttu-id="7efaa-194">사용자 지정 로그 비활성화</span><span class="sxs-lookup"><span data-stu-id="7efaa-194">Disabling a custom log</span></span>
<span data-ttu-id="7efaa-195">생성된 사용자 지정 로그 정의는 제거할 수 없지만 모든 수집 경로를 제거하여 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-195">You cannot remove a custom log definition once it's been created, but you can disable it by removing all of its collection paths.</span></span>

1. <span data-ttu-id="7efaa-196">Hello OMS 포털에서 이동 너무**설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-196">In hello OMS portal, go too**Settings**.</span></span>
2. <span data-ttu-id="7efaa-197">**데이터**를 클릭한 다음 **사용자 지정 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-197">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="7efaa-198">클릭 **세부 정보** 다음 toohello 사용자 지정 로그 정의 toodisable 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-198">Click **Details** next toohello custom log definition toodisable.</span></span>
4. <span data-ttu-id="7efaa-199">각 사용자 지정 로그 정의 hello에 대 한 hello 컬렉션 경로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-199">Remove each of hello collection paths for hello custom log definition.</span></span>

## <a name="data-collection"></a><span data-ttu-id="7efaa-200">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="7efaa-200">Data collection</span></span>
<span data-ttu-id="7efaa-201">Log Analytics는 각 사용자 지정 로그로부터 새로운 항목을 약 5분마다 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-201">Log Analytics will collect new entries from each custom log approximately every 5 minutes.</span></span>  <span data-ttu-id="7efaa-202">hello 에이전트는 해당 위치를 수집 하는 각 로그 파일에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-202">hello agent will record its place in each log file that it collects from.</span></span>  <span data-ttu-id="7efaa-203">Hello 에이전트 일정 시간 동안 오프 라인이 되 면 다음 로그 분석에서 수집 합니다 항목 마지막 중단, hello 에이전트 오프 라인 상태일 때 해당 항목을 만든 경우에.</span><span class="sxs-lookup"><span data-stu-id="7efaa-203">If hello agent goes offline for a period of time, then Log Analytics will collect entries from where it last left off, even if those entries were created while hello agent was offline.</span></span>

<span data-ttu-id="7efaa-204">hello 로그 항목의 전체 내용이 hello 라는 tooa 단일 속성이 기록 **RawData**합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-204">hello entire contents of hello log entry are written tooa single property called **RawData**.</span></span>  <span data-ttu-id="7efaa-205">분석 및 정의 하 여 개별적으로 검색할 수 있는 여러 속성에이 구문을 분석할 수 있습니다 [사용자 지정 필드](log-analytics-custom-fields.md) hello 사용자 지정 로그를 만든 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-205">You can parse this into multiple properties that can be analyzed and searched separately by defining [Custom Fields](log-analytics-custom-fields.md) after you have created hello custom log.</span></span>

## <a name="custom-log-record-properties"></a><span data-ttu-id="7efaa-206">사용자 지정 로그 레코드 속성</span><span class="sxs-lookup"><span data-stu-id="7efaa-206">Custom log record properties</span></span>
<span data-ttu-id="7efaa-207">사용자 지정 로그 레코드를 제공 하 고 다음 표에 hello에 대 한 속성을 hello 하는 hello 로그 이름 가진 유형을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-207">Custom log records have a type with hello log name that you provide and hello properties in hello following table.</span></span>

| <span data-ttu-id="7efaa-208">속성</span><span class="sxs-lookup"><span data-stu-id="7efaa-208">Property</span></span> | <span data-ttu-id="7efaa-209">설명</span><span class="sxs-lookup"><span data-stu-id="7efaa-209">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7efaa-210">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="7efaa-210">TimeGenerated</span></span> |<span data-ttu-id="7efaa-211">날짜 및 시간을 레코드 hello 로그 분석에 의해 수집 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-211">Date and time that hello record was collected by Log Analytics.</span></span>  <span data-ttu-id="7efaa-212">Hello 로그 시간 기반 구분 기호를 사용 하는 경우 이것이 hello 항목에서 수집 하는 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-212">If hello log uses a time-based delimiter then this is hello time collected from hello entry.</span></span> |
| <span data-ttu-id="7efaa-213">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="7efaa-213">SourceSystem</span></span> |<span data-ttu-id="7efaa-214">에이전트 hello 레코드 종류에서 수집 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-214">Type of agent hello record was collected from.</span></span> <br> <span data-ttu-id="7efaa-215">OpsManager – Windows 에이전트, 직접 연결 또는 System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="7efaa-215">OpsManager – Windows agent, either direct connect or System Center Operations Manager</span></span> <br> <span data-ttu-id="7efaa-216">Linux – 모든 Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="7efaa-216">Linux – All Linux agents</span></span> |
| <span data-ttu-id="7efaa-217">RawData</span><span class="sxs-lookup"><span data-stu-id="7efaa-217">RawData</span></span> |<span data-ttu-id="7efaa-218">Hello의 전체 텍스트 항목을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-218">Full text of hello collected entry.</span></span> |
| <span data-ttu-id="7efaa-219">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="7efaa-219">ManagementGroupName</span></span> |<span data-ttu-id="7efaa-220">에이전트 시스템 센터 작업 관리에 대 한 hello 관리 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-220">Name of hello management group for System Center Operations Manage agents.</span></span>  <span data-ttu-id="7efaa-221">다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-221">For other agents, this is AOI-\<workspace ID\></span></span> |

## <a name="log-searches-with-custom-log-records"></a><span data-ttu-id="7efaa-222">사용자 지정 로그 레코드를 사용한 로그 검색</span><span class="sxs-lookup"><span data-stu-id="7efaa-222">Log searches with custom log records</span></span>
<span data-ttu-id="7efaa-223">사용자 지정 로그의 레코드를 다른 데이터 원본의 레코드와 마찬가지로 hello OMS 리포지토리에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-223">Records from custom logs are stored in hello OMS repository just like records from any other data source.</span></span>  <span data-ttu-id="7efaa-224">특정 로그에서 수집 된 검색 tooretrieve 레코드의 hello Type 속성을 사용할 수 있도록 hello 로그를 정의 하는 경우 제공 하는 hello 이름과 일치 하는 형식을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-224">They will have a type matching hello name that you provide when you define hello log, so you can use hello Type property in your search tooretrieve records collected from a specific log.</span></span>

<span data-ttu-id="7efaa-225">hello 다음 표에서 사용자 지정 로그에서 레코드를 검색 하는 로그 검색의 다른 예.</span><span class="sxs-lookup"><span data-stu-id="7efaa-225">hello following table provides different examples of log searches that retrieve records from custom logs.</span></span>

| <span data-ttu-id="7efaa-226">쿼리</span><span class="sxs-lookup"><span data-stu-id="7efaa-226">Query</span></span> | <span data-ttu-id="7efaa-227">설명</span><span class="sxs-lookup"><span data-stu-id="7efaa-227">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7efaa-228">Type=MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="7efaa-228">Type=MyApp_CL</span></span> |<span data-ttu-id="7efaa-229">이름 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7efaa-229">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="7efaa-230">Type=MyApp_CL Severity_CF=error</span><span class="sxs-lookup"><span data-stu-id="7efaa-230">Type=MyApp_CL Severity_CF=error</span></span> |<span data-ttu-id="7efaa-231">이름이 *Severity_CF*인 사용자 지정 필드의 값이 *error*이고 이름이 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7efaa-231">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |

>[!NOTE]
> <span data-ttu-id="7efaa-232">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-232">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="7efaa-233">쿼리</span><span class="sxs-lookup"><span data-stu-id="7efaa-233">Query</span></span> | <span data-ttu-id="7efaa-234">설명</span><span class="sxs-lookup"><span data-stu-id="7efaa-234">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7efaa-235">MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="7efaa-235">MyApp_CL</span></span> |<span data-ttu-id="7efaa-236">이름 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7efaa-236">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="7efaa-237">MyApp_CL &#124; where Severity_CF=="error"</span><span class="sxs-lookup"><span data-stu-id="7efaa-237">MyApp_CL &#124; where Severity_CF=="error"</span></span> |<span data-ttu-id="7efaa-238">이름이 *Severity_CF*인 사용자 지정 필드의 값이 *error*이고 이름이 MyApp_CL인 사용자 지정 로그의 모든 이벤트.</span><span class="sxs-lookup"><span data-stu-id="7efaa-238">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a><span data-ttu-id="7efaa-239">사용자 지정 로그 추가 샘플 연습</span><span class="sxs-lookup"><span data-stu-id="7efaa-239">Sample walkthrough of adding a custom log</span></span>
<span data-ttu-id="7efaa-240">hello 다음 섹션 안내 사용자 지정 로그를 만드는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-240">hello following section walks through an example of creating a custom log.</span></span>  <span data-ttu-id="7efaa-241">수집 되 고 hello 샘플 로그 시작 날짜 및 코드, 상태 및 메시지에 대 한 시간 및 다음 쉼표로 구분 된 필드의 각 줄에 단일 항목에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-241">hello sample log being collected has a single entry on each line starting with a date and time and then comma-delimited fields for code, status, and message.</span></span>  <span data-ttu-id="7efaa-242">몇 가지 샘플 항목이 아래에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-242">Several sample entries are shown below.</span></span>

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a><span data-ttu-id="7efaa-243">샘플 로그 업로드 및 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7efaa-243">Upload and parse a sample log</span></span>
<span data-ttu-id="7efaa-244">Hello 로그 파일 중 하나를 제공 하 고 수집 됩니다 hello 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-244">We provide one of hello log files and can see hello events that it will be collecting.</span></span>  <span data-ttu-id="7efaa-245">이 경우 New Line(새 줄)은 충분한 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-245">In this case New Line is a sufficient delimiter.</span></span>  <span data-ttu-id="7efaa-246">그러나 hello 로그의 단일 항목을 여러 줄에 걸쳐 수, 하는 경우 타임 스탬프 구분 기호는 toobe 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-246">If a single entry in hello log could span multiple lines though, then a timestamp delimiter would need toobe used.</span></span>

![샘플 로그 업로드 및 구문 분석](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a><span data-ttu-id="7efaa-248">로그 수집 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7efaa-248">Add log collection paths</span></span>
<span data-ttu-id="7efaa-249">hello 로그 파일에 배치 됩니다 *C:\MyApp\Logs*합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-249">hello log files will be located in *C:\MyApp\Logs*.</span></span>  <span data-ttu-id="7efaa-250">매일 hello 패턴에서 hello 날짜를 포함 하는 이름의 새 파일이 생성 됩니다 *appYYYYMMDD.log*합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-250">A new file will be created each day with a name that includes hello date in hello pattern *appYYYYMMDD.log*.</span></span>  <span data-ttu-id="7efaa-251">이 로그에 충분한 패턴은 *C:\MyApp\Logs\\\*.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-251">A sufficient pattern for this log would be *C:\MyApp\Logs\\\*.log*.</span></span>

![로그 수집 경로](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a><span data-ttu-id="7efaa-253">이름 및 hello 로그에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-253">Provide a name and description for hello log</span></span>
<span data-ttu-id="7efaa-254">*MyApp_CL*이라는 이름을 사용하여 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-254">We use a name of *MyApp_CL* and type in a **Description**.</span></span>

![로그 이름](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a><span data-ttu-id="7efaa-256">Hello 사용자 지정 로그를 수집 하는 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7efaa-256">Validate that hello custom logs are being collected</span></span>
<span data-ttu-id="7efaa-257">쿼리 사용 *형식 MyApp_CL =* tooreturn 모든 hello 수집 된 로그에서를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-257">We use a query of *Type=MyApp_CL* tooreturn all records from hello collected log.</span></span>

![사용자 지정 필드가 없는 로그 쿼리](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a><span data-ttu-id="7efaa-259">Hello 사용자 지정 로그 항목을 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7efaa-259">Parse hello custom log entries</span></span>
<span data-ttu-id="7efaa-260">사용자 정의 필드 toodefine hello 사용 하 여 *EventTime*, *코드*, *상태*, 및 *메시지* 필드 및 우리는 hello hello 차이 볼 수 있습니다 hello 쿼리에서 반환 되는 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-260">We use Custom Fields toodefine hello *EventTime*, *Code*, *Status*, and *Message* fields and we can see hello difference in hello records that are returned by hello query.</span></span>

![사용자 지정 필드가 있는 로그 쿼리](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a><span data-ttu-id="7efaa-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7efaa-262">Next steps</span></span>
* <span data-ttu-id="7efaa-263">사용 하 여 [사용자 지정 필드](log-analytics-custom-fields.md) tooparse hello hello tooindividual 필드에 사용자 지정 로그 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-263">Use [Custom Fields](log-analytics-custom-fields.md) tooparse hello entries in hello custom log in tooindividual fields.</span></span>
* <span data-ttu-id="7efaa-264">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7efaa-264">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
