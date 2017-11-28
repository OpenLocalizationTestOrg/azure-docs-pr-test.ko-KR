---
title: "분석 데이터 레이크 저장소 출력 aaaStream | Microsoft Docs"
description: "스트림 분석 작업에서 Azure Data Lake 저장소의 인증 및 권한 부여 구성"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="cebf9-103">스트림 분석 Data Lake 저장소 출력</span><span class="sxs-lookup"><span data-stu-id="cebf9-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="cebf9-104">스트림 분석 작업은 여러 출력 메서드를 지원하며 그 중 하나는 [Azure Data Lake 저장소](https://azure.microsoft.com/services/data-lake-store/)입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="cebf9-105">Azure 데이터 레이크 저장소는 빅 데이터 분석 작업을 위한 엔터프라이즈 수준 하이퍼 스케일 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="cebf9-106">데이터 레이크 저장소를 통해 운영 및 예비 분석에 대 한 원하는 크기, 유형 및 수집 속도의 toostore 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="cebf9-107">Data Lake 저장소 계정 권한 부여</span><span class="sxs-lookup"><span data-stu-id="cebf9-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="cebf9-108">데이터 레이크 저장소를 hello Azure 포털에서에서 출력으로 선택 하는 경우 메시지가 표시 됩니다 기존 데이터 레이크 저장소 또는 toorequest tooauthorize 사용 hello 클래식 포털을 통해 toohello 데이터 레이크 저장소에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="cebf9-109">이미 있는 경우 tooData 레이크 스토어에 액세스 "권한을 부여" 지금 "을 페이지 짧은 시간에 대 한 팝업 됩니다"리디렉션 tooauthorization "를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="cebf9-110">hello 페이지 자동으로 닫히고 tooconfigure hello Data Lake 저장소 출력은 허용 하는 hello 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="cebf9-111">데이터 레이크 저장소에 대 한 등록 하지 한 hello "등록 지금" 링크 tooinitiate hello 요청을 수행 하거나 수 hello에 따라 [시작된 지침 확인](../data-lake-store/data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="cebf9-112">Hello 데이터 레이크 저장소 출력 속성 구성</span><span class="sxs-lookup"><span data-stu-id="cebf9-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="cebf9-113">Hello 데이터 레이크 저장소 계정 인증을 사용 하는 후에 데이터 레이크 저장소 출력에 대 한 hello 속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="cebf9-114">hello 다음 표에서 hello 목록 속성 이름 및 해당 설명 tooconfigure 데이터 레이크 저장소 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="cebf9-115"><B>속성 이름</B></span><span class="sxs-lookup"><span data-stu-id="cebf9-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="cebf9-116"><B>설명</B></span><span class="sxs-lookup"><span data-stu-id="cebf9-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-117">출력 별칭</span><span class="sxs-lookup"><span data-stu-id="cebf9-117">Output Alias</span></span></td>
<td><span data-ttu-id="cebf9-118">쿼리 toodirect hello 쿼리 출력 toothis Data Lake 저장소에에서 사용 되는 친숙 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-119">Data Lake 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="cebf9-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="cebf9-120">출력을 보내는 hello 저장소 계정의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="cebf9-121">데이터 레이크 저장소 계정에 권한이 hello 로그인 한 사용자 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-122">경로 접두사 패턴[<I>선택 사항</I>]</span><span class="sxs-lookup"><span data-stu-id="cebf9-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="cebf9-123">파일에 사용 된 경로 toowrite hello hello 내에서 파일 데이터 레이크 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="cebf9-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="cebf9-124">{date}, {time}</span></span><BR><span data-ttu-id="cebf9-125">예제 1: folder1/logs/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="cebf9-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="cebf9-126">예제 2: folder1/logs/{date}</span><span class="sxs-lookup"><span data-stu-id="cebf9-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-127">날짜 형식[<I>선택 사항</I>]</span><span class="sxs-lookup"><span data-stu-id="cebf9-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="cebf9-128">Hello 날짜 토큰이 hello 접두사 경로에 사용 되며, hello 날짜 형식을 사용자 파일 구성할 지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="cebf9-129">예: YYYY/MM/DD</span><span class="sxs-lookup"><span data-stu-id="cebf9-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-130">시간 형식[<I>선택 사항</I>]</span><span class="sxs-lookup"><span data-stu-id="cebf9-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="cebf9-131">Hello 시간 토큰이 hello 접두사 경로에 사용 되며, 경우에 파일 구성 됩니다 hello 시간 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="cebf9-132">현재 hello만 지원 점은 HH입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-133">이벤트 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="cebf9-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="cebf9-134">출력 데이터에 대한 직렬화 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-134">Serialization format for output data.</span></span> <span data-ttu-id="cebf9-135">JSON, CSV 및 Avro를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-136">인코딩</span><span class="sxs-lookup"><span data-stu-id="cebf9-136">Encoding</span></span></td>
<td><span data-ttu-id="cebf9-137">CSV 또는 JSON 형식인 경우 인코딩을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="cebf9-138">U t F-8 hello만 현재 지원 인코딩 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-139">구분 기호</span><span class="sxs-lookup"><span data-stu-id="cebf9-139">Delimiter</span></span></td>
<td><span data-ttu-id="cebf9-140">CSV 직렬화에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="cebf9-141">스트림 분석은 CSV 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="cebf9-142">지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cebf9-143">형식</span><span class="sxs-lookup"><span data-stu-id="cebf9-143">Format</span></span></td>
<td><span data-ttu-id="cebf9-144">JSON 직렬화에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="cebf9-145">줄 바꿈을 하 여 지정 hello 출력 각 JSON 개체를 새 줄으로 구분 하 여 형식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="cebf9-146">배열 지정 hello 출력 JSON 개체의 배열으로 형식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="cebf9-147">Data Lake 저장소 권한 부여 갱신</span><span class="sxs-lookup"><span data-stu-id="cebf9-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="cebf9-148">현재는 제한 사항에서 인증 토큰 hello 필요한 toobe 수동으로 데이터 레이크 저장소 출력을 제공 하는 모든 작업에 대 한 일 마다 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="cebf9-149">Toore 만들어야-업무를 만든 이후 또는 마지막으로 인증 된 암호를 변경한 경우 사용자 데이터 레이크 저장소 계정을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="cebf9-150">이 문제의 증상은 작업 출력 없음 다시 권한 부여에 대 한 필요성을 나타내는 hello 작업 로그에 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="cebf9-151">tooresolve이이 문제를 실행 중인 작업을 중지 하 고 출력 tooyour 데이터 레이크 저장소로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="cebf9-152">Hello "갱신 인증" 링크를 클릭 하 고 페이지 짧은 시간에 대 한 팝업 됩니다 "리디렉션 tooauthorization..."를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="cebf9-153">hello 페이지 자동으로 닫히고 성공 하면 "권한 부여를 갱신 했습니다" 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="cebf9-154">그런 다음 "저장" tooclick hello hello 페이지 맨 아래에 필요 하 고 마지막으로 중지 된 시간 tooavoid 데이터 손실 hello에서 작업을 다시 시작 하 여 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cebf9-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

