---
title: "Stream Analytics: 입력 및 출력에 대한 로그인 자격 증명 회전 | Microsoft Docs"
description: "스트림 분석 입력 및 출력에 대한 자격 증명을 업데이트 하는 방법에 대해 알아봅니다."
keywords: "로그인 자격 증명"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 2cb995a3969a8cb025f371ed0ab160cd04b0454d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="59d57-104">스트림 분석 작업에서 입력 및 출력을 위한 로그인 자격 증명 회전</span><span class="sxs-lookup"><span data-stu-id="59d57-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="59d57-105">요약</span><span class="sxs-lookup"><span data-stu-id="59d57-105">Abstract</span></span>
<span data-ttu-id="59d57-106">오늘날 Azure 스트림 분석은 작업이 실행되는 동안에 입/출력 시 자격 증명을 대체할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="59d57-107">Azure 스트림 분석은 마지막 출력에서 작업 재시작을 지원하지만, 작업의 중지 및 시작과 로그인 자격 증명 회전 사이의 간격을 최소화하기 위해 전체 프로세스를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="59d57-108">1부-새로운 자격 증명 집합을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="59d57-109">이 부분은 다음 입력/출력에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="59d57-110">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="59d57-110">Blob Storage</span></span>
* <span data-ttu-id="59d57-111">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="59d57-111">Event Hubs</span></span>
* <span data-ttu-id="59d57-112">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="59d57-112">SQL Database</span></span>
* <span data-ttu-id="59d57-113">테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="59d57-113">Table Storage</span></span>

<span data-ttu-id="59d57-114">다른 입력/출력의 경우 2부를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="59d57-115">Blob 저장소/테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="59d57-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="59d57-116">Azure 관리 포털에서 Storage 확장명으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="59d57-118">사용자 작업에서 사용되는 Storage를 찾아 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-118">Locate the storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="59d57-120">액세스 키 관리 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-120">Click the Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="59d57-122">기본 액세스 키 및 보조 액세스 키 사이에서 **작업에서 사용되지 않는 키를 선택합니다**.</span><span class="sxs-lookup"><span data-stu-id="59d57-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="59d57-123">히트 다시 생성: </span><span class="sxs-lookup"><span data-stu-id="59d57-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="59d57-125">새로 생성된 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-125">Copy the newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="59d57-127">2부를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="59d57-128">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="59d57-128">Event hubs</span></span>
1. <span data-ttu-id="59d57-129">Azure 관리 포털에서 Service Bus 확장명으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="59d57-131">작업에서 사용하는 Service Bus 네임스페이스를 찾아 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="59d57-133">작업이 서비스 버스 네임스페이스에서 공유 액세스 정책을 사용하는 경우 6단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="59d57-134">Event Hubs 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-134">Go to the Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="59d57-136">사용자 작업에서 사용되는 Event Hubs를 찾아 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="59d57-138">구성 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-138">Go to the Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="59d57-140">정책 이름 드롭다운 목록에서 작업에서 사용되는 공유 액세스 정책을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="59d57-142">기본 키와 보조 키 사이에서 **작업에서 사용되지 않는 키를 선택합니다**.</span><span class="sxs-lookup"><span data-stu-id="59d57-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="59d57-143">히트 다시 생성: </span><span class="sxs-lookup"><span data-stu-id="59d57-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="59d57-145">새로 생성된 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-145">Copy the newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="59d57-147">2부를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="59d57-148">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="59d57-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="59d57-149">참고: SQL 데이터베이스 서비스에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="59d57-150">Azure 관리 포털에서 관리 환경을 사용하여 이를 수행하는 방법을 보여줄 수 있지만 SQL Server Management Studio와 같은 일부 클라이언트측 도구를 함께 사용하 여 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="59d57-151">Azure 관리 포털에서 SQL Database 확장명으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="59d57-153">작업에서 사용되는 SQL Database를 찾아 동일한 줄에 있는 **서버 링크를 클릭합니다.**</span><span class="sxs-lookup"><span data-stu-id="59d57-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="59d57-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="59d57-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="59d57-155">관리 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-155">Click the Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="59d57-157">데이터베이스 마스터 유형: </span><span class="sxs-lookup"><span data-stu-id="59d57-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="59d57-159">사용자 이름, 암호를 입력하고 로그를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="59d57-161">새 쿼리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="59d57-163"><login_name>을 사용자 이름으로 교체하고 <enterStrongPasswordHere>를 새 암호로 교체하여 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="59d57-164">실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="59d57-166">2단계로 돌아가서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-166">Go back to step 2 and this time click the database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="59d57-168">관리 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-168">Click the Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="59d57-170">사용자 이름, 암호를 입력하고 로그를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="59d57-172">새 쿼리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="59d57-174">이 데이터베이스의 컨텍스트에서 이 로그인을 식별할 이름으로 <user_name>을 대체하고(예를 들어, <login_name>에 대해 동일한 값을 제공할 수 있음) 및 새 사용자 이름으로 <login_name>을 대체하는 다음 쿼리에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="59d57-175">실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="59d57-177">이제 원래 사용자가 가졌던 동일한 역할과 권한을 새로운 사용자에게 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="59d57-178">2부를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="59d57-179">2부: 스트림 분석 작업 중지</span><span class="sxs-lookup"><span data-stu-id="59d57-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="59d57-180">Azure 관리 포털에서 Stream Analytics 확장으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="59d57-182">작업을 찾아 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="59d57-184">입력 또는 출력의 자격 증명을 회전하는 지 여부에 따라 입력 탭이나 출력 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="59d57-186">중지 명령을 클릭하고</span><span class="sxs-lookup"><span data-stu-id="59d57-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="59d57-187">![graphic29][graphic29] 작업이 중지되었는지 확인합니다. 작업이 중지될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="59d57-188">자격 증명을 회전할 입/출력을 찾아 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="59d57-190">3부로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="59d57-191">3 부: 스트림 분석 작업에서 자격 증명 편집</span><span class="sxs-lookup"><span data-stu-id="59d57-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="59d57-192">Blob 저장소/테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="59d57-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="59d57-193">Storage 계정 키 필드를 찾아 새로 생성된 키를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="59d57-195">저장 명령을 클릭하고 변경 내용 저장을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-195">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="59d57-197">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="59d57-198">4부로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="59d57-199">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="59d57-199">Event hubs</span></span>
1. <span data-ttu-id="59d57-200">Event Hubs 정책 키 필드를 찾아 새로 생성된 키를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="59d57-202">저장 명령을 클릭하고 변경 내용 저장을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-202">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="59d57-204">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="59d57-205">4부로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="59d57-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="59d57-206">Power BI</span></span>
1. <span data-ttu-id="59d57-207">권한 부여 갱신을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-207">Click the Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="59d57-209">다음 확인 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-209">You will get the following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="59d57-211">저장 명령을 클릭하고 변경 내용 저장을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-211">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="59d57-213">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="59d57-214">4부로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="59d57-215">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="59d57-215">SQL Database</span></span>
1. <span data-ttu-id="59d57-216">사용자 이름 및 암호 필드를 찾아 새로 만든 자격 증명 집합을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="59d57-218">저장 명령을 클릭하고 변경 내용 저장을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-218">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="59d57-220">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="59d57-221">4부로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="59d57-222">4부: 마지막 중지된 시간에서 해당 작업 시작</span><span class="sxs-lookup"><span data-stu-id="59d57-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="59d57-223">입/출력에서 다른 부분으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-223">Navigate away from the Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="59d57-225">시작 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-225">Click the Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="59d57-227">마지막 중지 시간을 선택하고 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="59d57-229">5부로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="59d57-230">5부: 이전 자격 증명 집합 제거</span><span class="sxs-lookup"><span data-stu-id="59d57-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="59d57-231">이 부분은 다음 입력/출력에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="59d57-232">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="59d57-232">Blob Storage</span></span>
* <span data-ttu-id="59d57-233">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="59d57-233">Event Hubs</span></span>
* <span data-ttu-id="59d57-234">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="59d57-234">SQL Database</span></span>
* <span data-ttu-id="59d57-235">테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="59d57-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="59d57-236">Blob 저장소/테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="59d57-236">Blob storage/Table storage</span></span>
<span data-ttu-id="59d57-237">이제 사용되지 않은 액세스 키를 갱신하 도록 이전에 작업에서 사용한 액세스 키에 대해 1부를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="59d57-238">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="59d57-238">Event hubs</span></span>
<span data-ttu-id="59d57-239">이제 사용되지 않은 키를 갱신하도록 이전에 작업에서 사용한 키에 대해 1부를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="59d57-240">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="59d57-240">SQL Database</span></span>
1. <span data-ttu-id="59d57-241">1부 7단계의 쿼리 창으로 돌아가서 <previous_login_name>을 이전에 사용자가 작업에 사용한 사용자 이름으로 바꾸고 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="59d57-242">실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="59d57-244">다음 확인 메시지가 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d57-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="59d57-245">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="59d57-245">Get help</span></span>
<span data-ttu-id="59d57-246">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="59d57-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="59d57-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59d57-247">Next steps</span></span>
* [<span data-ttu-id="59d57-248">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="59d57-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="59d57-249">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="59d57-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="59d57-250">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="59d57-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="59d57-251">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="59d57-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="59d57-252">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="59d57-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

