---
title: "SQL 커넥터 단계별 aaaGeneric 단계 | Microsoft Docs"
description: "이 문서는 단계별 hello 제네릭 SQL 커넥터를 사용 하 여 단계별 간단한 HR 시스템을 통해."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="a1824-103">일반 SQL 커넥터 단계별 가이드</span><span class="sxs-lookup"><span data-stu-id="a1824-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="a1824-104">이 항목은 단계별 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="a1824-105">이 항목에서는 간단한 샘플 HR 데이터베이스를 만들고 이를 사용하여 일부 사용자와 해당 그룹 멤버 자격을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="a1824-106">Hello 예제 데이터베이스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-106">Prepare hello sample database</span></span>
<span data-ttu-id="a1824-107">SQL Server를 실행 중인 서버의 hello SQL 스크립트를 실행 [부록 A](#appendix-a)합니다. 이 스크립트는 GSQLDEMO hello 이름의 예제 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="a1824-108">hello에 대 한 hello 개체 모델 생성이 그림의 데이터베이스 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="a1824-109">![개체 모델](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="a1824-110">또한 toouse tooconnect toohello 데이터베이스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="a1824-111">이 연습에서는 hello 사용자가 FABRIKAM\SQLUser 호출 되 고 hello 도메인에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="a1824-112">Hello ODBC 연결 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="a1824-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="a1824-113">일반 SQL 커넥터 hello ODBC tooconnect toohello 원격 서버를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="a1824-114">먼저 toocreate hello ODBC 연결 정보로 파일을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="a1824-115">서버에서 hello ODBC 관리 유틸리티를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="a1824-117">선택 hello 탭 **파일 DSN**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="a1824-118">**추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-118">Click **Add...**.</span></span>  
   <span data-ttu-id="a1824-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="a1824-120">hello 기본적으로 드라이버 works 미세, 따라서 선택 하 고 클릭 **다음 >**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="a1824-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="a1824-122">와 같은 hello 파일에 이름을 지정 **GenericSQL**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="a1824-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="a1824-124">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-124">Click **Finish**.</span></span>  
   <span data-ttu-id="a1824-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="a1824-126">시간 tooconfigure hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="a1824-127">Hello 데이터 소스를 적절 한 설명을 제공 하 고 SQL Server를 실행 하는 hello 서버 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="a1824-129">방법을 선택 sql tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="a1824-130">이 예제에서는 Windows 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="a1824-132">Hello 예제 데이터베이스의 hello 이름을 제공 **GSQLDEMO**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="a1824-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="a1824-134">이 화면에서는 모든 항목을 기본값으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-134">Keep everything default on this screen.</span></span> <span data-ttu-id="a1824-135">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-135">Click **Finish**.</span></span>  
   <span data-ttu-id="a1824-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="a1824-137">모든 것이 예상 대로 작동 tooverify 클릭 **테스트 데이터 소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="a1824-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="a1824-139">Hello 테스트 성공 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="a1824-141">이제 hello ODBC 구성 파일 파일 DSN에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="a1824-143">Hello 파일을 및 필요 hello 커넥터 만들기를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="a1824-144">Hello 제네릭 SQL 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="a1824-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="a1824-145">Hello 동기화 서비스 관리자 UI에서에서 선택 **커넥터** 및 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="a1824-146">**일반 SQL(Microsoft)** 을 선택하고 설명이 포함된 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="a1824-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="a1824-148">Hello 이전 섹션에서 만든 hello DSN 파일을 찾아 toohello 서버에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="a1824-149">Hello 자격 증명 tooconnect toohello 데이터베이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="a1824-151">이 연습에서는 작업을 쉽게 하기 위해 **User**와 **Group**이라는 두 개의 개체가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="a1824-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="a1824-153">toofind hello 특성 hello 테이블 자체를 보면 커넥터 toodetect 특성 hello 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="a1824-154">이후 **사용자** 예약어 tooprovide 사각형에서 대괄호 sql에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="a1824-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="a1824-156">시간 toodefine hello 앵커 특성 및 hello DN 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="a1824-157">에 대 한 **사용자**, hello 두 특성의 사용자 이름 및 EmployeeID의 hello 조합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="a1824-158">**Group**의 경우 GroupName(실제로는 현실적이지 않지만 이 연습에서는 작동함)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="a1824-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="a1824-160">일부 특성 유형은 SQL 데이터베이스에서 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="a1824-161">hello reference-type 특성 특히 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="a1824-162">Hello 그룹 개체 유형에 대해 toochange hello OwnerID 및 tooreference memberid를 지정 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="a1824-164">hello 이전 단계에서 참조 특성 hello 개체 유형 이러한 값에 대 한 참조는 필요에 따라 hello 특성 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="a1824-165">경우에 hello 사용자 개체 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-165">In our case, hello User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="a1824-167">Hello 글로벌 매개 변수 페이지에서 선택 **워터 마크** hello 델타 전략으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="a1824-168">또한 hello 날짜/시간 형식으로 입력 **yyyy-월-일 hh: mm:**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="a1824-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="a1824-170">Hello에 **파티션 구성 및 계층** 페이지에서 두 개체 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="a1824-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="a1824-172">Hello에 **개체 유형 선택** 및 **특성 선택**, 개체 유형 및 모든 특성을 모두 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="a1824-173">Hello에 **앵커 구성** 페이지 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="a1824-174">실행 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="a1824-174">Create Run Profiles</span></span>
1. <span data-ttu-id="a1824-175">Hello 동기화 서비스 관리자 UI에서에서 선택 **커넥터**, 및 **실행 프로필 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="a1824-176">**새 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-176">Click **New Profile**.</span></span> <span data-ttu-id="a1824-177">**전체 가져오기**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="a1824-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="a1824-179">Hello 유형 선택 **전체 가져오기 (스테이지 전용)**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="a1824-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="a1824-181">Hello 파티션을 선택 **개체 = 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="a1824-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="a1824-183">**테이블**을 선택하고 **[USERS]**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="a1824-184">Toohello 다중값된 개체 유형 섹션 아래로 스크롤하여 hello 다음 그림에서와 같이 hello 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="a1824-185">선택 **마침** toosave hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="a1824-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="a1824-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="a1824-188">**새 단계**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-188">Select **New Step**.</span></span> <span data-ttu-id="a1824-189">이번에는 **OBJECT=Group**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="a1824-190">Hello 마지막 페이지에 hello 다음 그림에서와 같이 hello 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="a1824-191">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-191">Click **Finish**.</span></span>  
   <span data-ttu-id="a1824-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="a1824-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="a1824-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="a1824-194">선택 사항: 원하는 경우 추가 실행 프로필을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="a1824-195">이 연습에 대 한 전체 가져오기 hello만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="a1824-196">클릭 **확인** toofinish 변경 실행 프로필.</span><span class="sxs-lookup"><span data-stu-id="a1824-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="a1824-197">일부 테스트 데이터 및 테스트 hello 가져오기 추가</span><span class="sxs-lookup"><span data-stu-id="a1824-197">Add some test data and test hello import</span></span>
<span data-ttu-id="a1824-198">샘플 데이터베이스에서 일부 테스트 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="a1824-199">준비되었으면 **실행** 및 **전체 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="a1824-200">다음은 두 개의 전화 번호가 있는 사용자와 몇 명의 구성원이 있는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a1824-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="a1824-203">부록 A</span><span class="sxs-lookup"><span data-stu-id="a1824-203">Appendix A</span></span>
<span data-ttu-id="a1824-204">**SQL 스크립트 toocreate hello 예제 데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="a1824-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
