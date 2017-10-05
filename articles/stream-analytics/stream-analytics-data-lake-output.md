---
title: "Stream Analytics Data Lake Store 출력 | Microsoft Docs"
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
ms.openlocfilehash: 3d867df3ef875d5cc41de418c3d1d269ff751fda
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="0f9ba-103">스트림 분석 Data Lake 저장소 출력</span><span class="sxs-lookup"><span data-stu-id="0f9ba-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="0f9ba-104">스트림 분석 작업은 여러 출력 메서드를 지원하며 그 중 하나는 [Azure Data Lake 저장소](https://azure.microsoft.com/services/data-lake-store/)입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="0f9ba-105">Azure 데이터 레이크 저장소는 빅 데이터 분석 작업을 위한 엔터프라이즈 수준 하이퍼 스케일 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="0f9ba-106">Data Lake 저장소를 사용하면 작동 및 예비 분석에 대해 모든 크기, 형식 및 수집 속도의 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="0f9ba-107">Data Lake 저장소 계정 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0f9ba-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="0f9ba-108">Data Lake Store를 Azure Portal에서 출력으로 선택하는 경우 기존 Data Lake Store의 사용 권한을 부여하거나 클래식 포털을 통해 Data Lake Store에 대한 액세스를 요청하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-108">When Data Lake Store is selected as an output in the Azure portal, you will be prompted to authorize use of your existing Data Lake Store or to request access to the Data Lake Store via the Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="0f9ba-109">Data Lake Store에 대한 액세스 권한이 이미 있는 경우 "지금 권한 부여"를 클릭하고 "권한 부여로 리디렉션..."을 나타내는 페이지가 잠깐 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization”.</span></span> <span data-ttu-id="0f9ba-110">페이지가 자동으로 닫히고 Data Lake 저장소 출력을 구성할 수 있도록 하는 페이지와 함께 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="0f9ba-111">Data Lake Store에 등록하지 않은 경우 "지금 등록" 링크를 클릭하여 등록 페이지로 이동해 요청을 시작하거나 [시작 지침](../data-lake-store/data-lake-store-get-started-portal.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="0f9ba-112">Data Lake 저장소 출력 속성 구성</span><span class="sxs-lookup"><span data-stu-id="0f9ba-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="0f9ba-113">Data Lake 저장소 계정을 인증하면 사용자가 Data Lake 저장소 출력에 대한 속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="0f9ba-114">다음 테이블은 속성 이름 및 해당 설명의 목록으로 Data Lake 저장소 출력을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="0f9ba-115"><B>속성 이름</B></span><span class="sxs-lookup"><span data-stu-id="0f9ba-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="0f9ba-116"><B>설명</B></span><span class="sxs-lookup"><span data-stu-id="0f9ba-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-117">출력 별칭</span><span class="sxs-lookup"><span data-stu-id="0f9ba-117">Output Alias</span></span></td>
<td><span data-ttu-id="0f9ba-118">쿼리 출력을 이 Data Lake 저장소로 직접 보내기 위해 쿼리에서 사용되는 식별 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-119">Data Lake 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="0f9ba-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="0f9ba-120">출력을 보내는 저장소 계정의 이름</span><span class="sxs-lookup"><span data-stu-id="0f9ba-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="0f9ba-121">로그인한 사용자가 액세스를 가진 Data Lake Store 계정의 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-121">You will be presented with a list of Data Lake Store accounts  the logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-122">경로 접두사 패턴[<I>선택 사항</I>]</span><span class="sxs-lookup"><span data-stu-id="0f9ba-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0f9ba-123">지정된 Data Lake 저장소 계정 내에서 파일을 작성하는 데 사용되는 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="0f9ba-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="0f9ba-124">{date}, {time}</span></span><BR><span data-ttu-id="0f9ba-125">예제 1: folder1/logs/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="0f9ba-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="0f9ba-126">예제 2: folder1/logs/{date}</span><span class="sxs-lookup"><span data-stu-id="0f9ba-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-127">날짜 형식[<I>선택 사항</I>]</span><span class="sxs-lookup"><span data-stu-id="0f9ba-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0f9ba-128">접두사 경로에 날짜 토큰을 사용하는 경우 파일을 구성하는 날짜 형식을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="0f9ba-129">예: YYYY/MM/DD</span><span class="sxs-lookup"><span data-stu-id="0f9ba-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-130">시간 형식[<I>선택 사항</I>]</span><span class="sxs-lookup"><span data-stu-id="0f9ba-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0f9ba-131">접두사 경로에 시간 토큰을 사용하는 경우 파일을 구성하는 시간 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="0f9ba-132">현재 지원되는 유일한 값은 HH입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-133">이벤트 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="0f9ba-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="0f9ba-134">출력 데이터에 대한 직렬화 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-134">Serialization format for output data.</span></span> <span data-ttu-id="0f9ba-135">JSON, CSV 및 Avro를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-136">인코딩</span><span class="sxs-lookup"><span data-stu-id="0f9ba-136">Encoding</span></span></td>
<td><span data-ttu-id="0f9ba-137">CSV 또는 JSON 형식인 경우 인코딩을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="0f9ba-138">지금은 지원되는 인코딩 형식이 UTF-8뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-139">구분 기호</span><span class="sxs-lookup"><span data-stu-id="0f9ba-139">Delimiter</span></span></td>
<td><span data-ttu-id="0f9ba-140">CSV 직렬화에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="0f9ba-141">스트림 분석은 CSV 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="0f9ba-142">지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0f9ba-143">형식</span><span class="sxs-lookup"><span data-stu-id="0f9ba-143">Format</span></span></td>
<td><span data-ttu-id="0f9ba-144">JSON 직렬화에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="0f9ba-145">구분된 줄은 출력이 각 JSON 개체를 새 줄로 구분된 형식이 되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="0f9ba-146">배열은 출력의 형식을 JSON 개체의 배열로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="0f9ba-147">Data Lake 저장소 권한 부여 갱신</span><span class="sxs-lookup"><span data-stu-id="0f9ba-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="0f9ba-148">현재 Data Lake 저장소 출력을 포함하는 모든 작업에 대해 90일 마다 인증 토큰을 수동으로 새로 고쳐야 하는 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="0f9ba-149">또한 작업을 만들거나 마지막으로 인증한 후에 암호를 변경한 경우 Data Lake 저장소 계정을 다시 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="0f9ba-150">이 문제의 증상은 다시 인증이 필요하다고 나타내는 작업 로그의 작업 출력 및 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="0f9ba-151">이 문제를 해결하려면 실행 중인 작업을 중지하고 Data Lake 저장소 출력으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="0f9ba-152">"권한 부여 갱신" 링크를 클릭하면 "권한 부여로 리디렉션..."을 나타내는 페이지가 잠깐 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="0f9ba-153">페이지가 자동으로 닫히고 성공하면 "권한 부여를 성공적으로 갱신했습니다"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="0f9ba-154">페이지의 맨 아래에서 "저장"을 클릭해야 하고 데이터 손실을 방지하도록 마지막 중지 시간에서 작업을 다시 시작하여 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f9ba-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

