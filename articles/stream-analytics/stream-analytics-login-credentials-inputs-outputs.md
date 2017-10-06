---
title: "Stream Analytics: 입력 및 출력에 대한 로그인 자격 증명 회전 | Microsoft Docs"
description: "Tooupdate hello 스트림 분석 입 / 출력에 대 한 자격 증명 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="69e3e-104">스트림 분석 작업에서 입력 및 출력을 위한 로그인 자격 증명 회전</span><span class="sxs-lookup"><span data-stu-id="69e3e-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="69e3e-105">요약</span><span class="sxs-lookup"><span data-stu-id="69e3e-105">Abstract</span></span>
<span data-ttu-id="69e3e-106">오늘날 azure 스트림 분석 hello 작업이 실행 되는 동안 입력/출력에서 hello 자격 증명을 교체 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="69e3e-107">Azure 스트림 분석에서 마지막으로 출력에서 작업을 다시 시작을 지원 하는 동안 싶었기 tooshare hello 전체 프로세스 중지 hello 및 hello 작업의 시작 및 로그인 자격 증명 hello 회전 사이의 hello 지연을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="69e3e-108">1 부-hello 새로운 자격 증명 집합을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="69e3e-109">이 부분은 입/출력 다음 적용 가능한 toohello:</span><span class="sxs-lookup"><span data-stu-id="69e3e-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="69e3e-110">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="69e3e-110">Blob Storage</span></span>
* <span data-ttu-id="69e3e-111">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="69e3e-111">Event Hubs</span></span>
* <span data-ttu-id="69e3e-112">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="69e3e-112">SQL Database</span></span>
* <span data-ttu-id="69e3e-113">테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="69e3e-113">Table Storage</span></span>

<span data-ttu-id="69e3e-114">다른 입력/출력의 경우 2부를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="69e3e-115">Blob 저장소/테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="69e3e-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="69e3e-116">Hello Azure 관리 포털에서 toohello 저장소 확장명을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="69e3e-118">작업에서 사용 하는 hello 저장소 찾아서 것으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="69e3e-120">Hello 액세스 키 관리 명령을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="69e3e-122">Hello 기본 액세스 키 및 보조 액세스 키를 hello 사이의 **선택 하지 작업에서 사용 하는 hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="69e3e-123">히트 다시 생성: </span><span class="sxs-lookup"><span data-stu-id="69e3e-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="69e3e-125">Hello 새로 생성 된 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="69e3e-127">TooPart 2를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="69e3e-128">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="69e3e-128">Event hubs</span></span>
1. <span data-ttu-id="69e3e-129">서비스 버스 확장 toohello hello Azure 관리 포털에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="69e3e-131">작업에서 사용 하는 서비스 버스 Namespace hello 찾아서 것으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="69e3e-133">작업에서 서비스 버스 Namespace hello에 대해 공유 액세스 정책, 점프 toostep 6</span><span class="sxs-lookup"><span data-stu-id="69e3e-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="69e3e-134">Toohello 이벤트 허브 탭으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="69e3e-136">작업에서 사용 하는 이벤트 허브 hello 찾아서 것으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="69e3e-138">Toohello 구성 탭 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="69e3e-140">Hello 정책 이름 드롭다운 목록, 작업에서 사용 하는 hello 공유 액세스 정책을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="69e3e-142">Hello 기본 키와 보조 키 hello 사이의 **선택 하지 작업에서 사용 하는 hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="69e3e-143">히트 다시 생성: </span><span class="sxs-lookup"><span data-stu-id="69e3e-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="69e3e-145">Hello 새로 생성 된 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="69e3e-147">TooPart 2를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="69e3e-148">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="69e3e-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="69e3e-149">참고: tooconnect toohello SQL 데이터베이스 서비스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="69e3e-150">하겠습니다 tooshow toodo 사용 하 여이에 관리 경험을 hello 방법 hello Azure 관리 포털 하지만 일부 클라이언트 쪽 도구 등 SQL Server Management Studio와 함께 toouse를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="69e3e-151">SQL 데이터베이스 확장 toohello hello Azure 관리 포털에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="69e3e-153">찾기 작업에서 사용 하는 SQL 데이터베이스 hello 및 **hello 서버를 클릭** hello에 동일한 연결 줄:</span><span class="sxs-lookup"><span data-stu-id="69e3e-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="69e3e-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="69e3e-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="69e3e-155">Hello 관리 명령을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="69e3e-157">데이터베이스 마스터 유형: </span><span class="sxs-lookup"><span data-stu-id="69e3e-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="69e3e-159">사용자 이름, 암호를 입력하고 로그를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="69e3e-161">새 쿼리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="69e3e-163">Hello 바꾸고 사용자 이름으로 쿼리 교체 < login_name > 뒤에 형식 <enterStrongPasswordHere> 새 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="69e3e-164">실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="69e3e-166">Toostep 2 돌아가서이 이번 hello 데이터베이스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="69e3e-168">Hello 관리 명령을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="69e3e-170">사용자 이름, 암호를 입력하고 로그를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="69e3e-172">새 쿼리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="69e3e-174">이 로그인이이 데이터베이스의 hello 컨텍스트에서 hello tooidentify 기준이 될 이름으로 쿼리 교체 사용자 < _ > 뒤에 입력 (제공할 수 있습니다 < login_name >에 대 한 예를 들어 지정한 동일한 값을 hello)와 < login_name >로 대체 새 사용자 이름:</span><span class="sxs-lookup"><span data-stu-id="69e3e-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="69e3e-175">실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="69e3e-177">Hello로 이제 새 사용자를 제공 해야 역할과 같은 역할 및 사용 하면 원래 사용자에 게 권한.</span><span class="sxs-lookup"><span data-stu-id="69e3e-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="69e3e-178">TooPart 2를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="69e3e-179">2 부: Stopping hello 스트림 분석 작업</span><span class="sxs-lookup"><span data-stu-id="69e3e-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="69e3e-180">Hello Azure 관리 포털에서 toohello 스트림 분석 확장 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="69e3e-182">작업을 찾아 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="69e3e-184">Toohello 입력 탭 이나 hello 자격 증명에 대 한 입력 또는 출력에서 회전 하는지 여부에 따라 hello 출력 탭 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="69e3e-186">Hello 중지 명령을 클릭 하 고 hello 작업이 중지 되었습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="69e3e-187">![graphic29][graphic29] hello 작업 toostop 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="69e3e-188">찾을 hello 입/출력 원하는 toorotate 자격 증명 on 및 이동 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="69e3e-190">TooPart 3을 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="69e3e-191">3 부: hello 스트림 분석 작업 시 hello 자격 편집</span><span class="sxs-lookup"><span data-stu-id="69e3e-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="69e3e-192">Blob 저장소/테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="69e3e-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="69e3e-193">Hello 저장소 계정 키 필드를 찾아 새로 생성 된 키를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="69e3e-195">Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="69e3e-197">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="69e3e-198">TooPart 4를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="69e3e-199">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="69e3e-199">Event hubs</span></span>
1. <span data-ttu-id="69e3e-200">Hello 이벤트 허브 정책 키 필드를 찾아 새로 생성 된 키를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="69e3e-202">Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="69e3e-204">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="69e3e-205">TooPart 4를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="69e3e-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="69e3e-206">Power BI</span></span>
1. <span data-ttu-id="69e3e-207">Hello 갱신 권한 부여를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="69e3e-209">확인을 수행 하는 hello를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="69e3e-211">Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="69e3e-213">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="69e3e-214">TooPart 4를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="69e3e-215">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="69e3e-215">SQL Database</span></span>
1. <span data-ttu-id="69e3e-216">Hello 사용자 이름 및 암호 필드를 찾아 새로 만든된 자격 증명 집합을 수용 여부에.</span><span class="sxs-lookup"><span data-stu-id="69e3e-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="69e3e-218">Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="69e3e-220">변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="69e3e-221">TooPart 4를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="69e3e-222">4부: 마지막 중지된 시간에서 해당 작업 시작</span><span class="sxs-lookup"><span data-stu-id="69e3e-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="69e3e-223">입/출력 hello를 나 가려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="69e3e-225">Hello 시작 명령을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="69e3e-227">Hello 마지막으로 중지 된 시간을 선택 하 고 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="69e3e-229">TooPart 5를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="69e3e-230">5 단계: 제거 hello 이전 자격 증명 집합</span><span class="sxs-lookup"><span data-stu-id="69e3e-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="69e3e-231">이 부분은 입/출력 다음 적용 가능한 toohello:</span><span class="sxs-lookup"><span data-stu-id="69e3e-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="69e3e-232">Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="69e3e-232">Blob Storage</span></span>
* <span data-ttu-id="69e3e-233">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="69e3e-233">Event Hubs</span></span>
* <span data-ttu-id="69e3e-234">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="69e3e-234">SQL Database</span></span>
* <span data-ttu-id="69e3e-235">테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="69e3e-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="69e3e-236">Blob 저장소/테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="69e3e-236">Blob storage/Table storage</span></span>
<span data-ttu-id="69e3e-237">1 부 hello 작업에서 이전에 사용한 선택 키에 대 한 반복 toorenew hello 이제 사용 되지 않은 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="69e3e-238">이벤트 허브(영문)</span><span class="sxs-lookup"><span data-stu-id="69e3e-238">Event hubs</span></span>
<span data-ttu-id="69e3e-239">1 부 hello 작업에서 이전에 사용한 키에 대 한 반복 toorenew hello 이제 사용 되지 않는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="69e3e-240">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="69e3e-240">SQL Database</span></span>
1. <span data-ttu-id="69e3e-241">Toohello 쿼리 창에 다음 쿼리, 작업에서 이전에 사용한 사용자 이름 hello로 < previous_login_name > 대체 hello 유형과 파트 1에서 7 단계에서 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="69e3e-242">실행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="69e3e-244">Hello를 다음 확인을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="69e3e-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="69e3e-245">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="69e3e-245">Get help</span></span>
<span data-ttu-id="69e3e-246">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="69e3e-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="69e3e-247">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69e3e-247">Next steps</span></span>
* [<span data-ttu-id="69e3e-248">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="69e3e-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="69e3e-249">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="69e3e-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="69e3e-250">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="69e3e-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="69e3e-251">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="69e3e-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="69e3e-252">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="69e3e-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

