---
title: "일반 SQL 커넥터 단계별 가이드 | Microsoft Docs"
description: "이 문서에서는 일반 SQL 커넥터를 사용하여 간단한 HR 시스템을 만드는 단계별 지침을 안내합니다."
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
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="00486-103">일반 SQL 커넥터 단계별 가이드</span><span class="sxs-lookup"><span data-stu-id="00486-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="00486-104">이 항목은 단계별 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="00486-105">이 항목에서는 간단한 샘플 HR 데이터베이스를 만들고 이를 사용하여 일부 사용자와 해당 그룹 멤버 자격을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00486-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="00486-106">샘플 데이터베이스 준비</span><span class="sxs-lookup"><span data-stu-id="00486-106">Prepare the sample database</span></span>
<span data-ttu-id="00486-107">SQL Server를 실행하는 서버에서 [부록 A](#appendix-a)에 있는 SQL 스크립트를 실행합니다. 이 스크립트는 GSQLDEMO라는 샘플 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00486-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="00486-108">만들어진 데이터베이스의 개체 모델은 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="00486-109">![개체 모델](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="00486-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="00486-110">또한 데이터베이스에 연결하는 데 사용할 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00486-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="00486-111">이 연습에서 사용자는 FABRIKAM\SQLUser이며 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="00486-112">ODBC 연결 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="00486-112">Create the ODBC connection file</span></span>
<span data-ttu-id="00486-113">일반 SQL 커넥터는 ODBC를 사용하여 원격 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="00486-114">먼저 ODBC 연결 정보를 사용하여 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="00486-115">서버에서 ODBC 관리 유틸리티를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="00486-117">**파일 DSN**탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="00486-118">**추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-118">Click **Add...**.</span></span>  
   <span data-ttu-id="00486-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="00486-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="00486-120">Windows에서 제공하지 않는 드라이버가 원활하게 작동하므로 이를 선택하고 **다음>**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="00486-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="00486-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="00486-122">**GenericSQL**과 같은 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="00486-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="00486-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="00486-124">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-124">Click **Finish**.</span></span>  
   <span data-ttu-id="00486-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="00486-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="00486-126">이제 연결을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-126">Time to configure the connection.</span></span> <span data-ttu-id="00486-127">데이터 원본에 대한 적절한 설명을 제공하고 SQL Server를 실행하는 서버의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="00486-129">SQL을 사용하여 인증할 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="00486-130">이 예제에서는 Windows 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="00486-132">샘플 데이터베이스의 이름 **GSQLDEMO**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="00486-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="00486-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="00486-134">이 화면에서는 모든 항목을 기본값으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-134">Keep everything default on this screen.</span></span> <span data-ttu-id="00486-135">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-135">Click **Finish**.</span></span>  
   <span data-ttu-id="00486-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="00486-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="00486-137">모든 항목이 예상대로 작동하는지 확인하기 위해 **데이터 원본 테스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="00486-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="00486-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="00486-139">테스트에 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="00486-141">이제 파일 DSN에 ODBC 구성 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00486-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="00486-143">필요한 파일이 있으므로 커넥터 만들기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="00486-144">일반 SQL 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="00486-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="00486-145">Synchronization Service Manager UI에서 **커넥터** 및 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="00486-146">**일반 SQL(Microsoft)** 을 선택하고 설명이 포함된 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="00486-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="00486-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="00486-148">이전 섹션에서 만든 DSN 파일을 찾아서 서버에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="00486-149">데이터베이스에 연결할 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="00486-151">이 연습에서는 작업을 쉽게 하기 위해 **User**와 **Group**이라는 두 개의 개체가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="00486-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="00486-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="00486-153">특성을 찾기 위해 커넥터에서 테이블 자체를 확인하여 해당 특성을 검색하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="00486-154">**Users** 는 SQL의 예약된 단어이므로 대괄호([ ]) 안에 이 단어를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="00486-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="00486-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="00486-156">이제 앵커 특성 및 DN 특성을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="00486-157">**User**의 경우 username과 EmployeeID라는 두 가지 특성의 조합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="00486-158">**Group**의 경우 GroupName(실제로는 현실적이지 않지만 이 연습에서는 작동함)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="00486-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="00486-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="00486-160">일부 특성 유형은 SQL 데이터베이스에서 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="00486-161">특히 참조 특성 유형은 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="00486-162">Group 개체 유형의 경우 OwnerID와 MemberID를 참조로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="00486-164">이전 단계에서 참조 특성으로 선택한 특성에는 이러한 값을 참조하는 개체 유형이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="00486-165">이 경우에 User 개체 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-165">In our case, the User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="00486-167">글로벌 매개 변수 페이지에서 **워터마크** 를 델타 전략으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="00486-168">또한 날짜/시간 형식 **yyyy-MM-dd HH:mm:ss**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="00486-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="00486-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="00486-170">**파티션 및 계층 구조 구성** 페이지에서 두 개체 유형을 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="00486-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="00486-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="00486-172">**개체 유형 선택** 및 **특성 선택**에서 두 개체 유형과 모든 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="00486-173">**앵커 구성** 페이지에서 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="00486-174">실행 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="00486-174">Create Run Profiles</span></span>
1. <span data-ttu-id="00486-175">Synchronization Service Manager UI에서 **커넥터** 및 **실행 프로필 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="00486-176">**새 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-176">Click **New Profile**.</span></span> <span data-ttu-id="00486-177">**전체 가져오기**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="00486-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="00486-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="00486-179">**전체 가져오기(스테이지 전용)**유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="00486-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="00486-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="00486-181">**OBJECT=User**파티션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="00486-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="00486-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="00486-183">**테이블**을 선택하고 **[USERS]**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="00486-184">다중값 개체 유형 섹션까지 아래로 스크롤하여 다음 그림과 같이 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="00486-185">**마침** 을 선택하여 단계를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="00486-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="00486-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="00486-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="00486-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="00486-188">**새 단계**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-188">Select **New Step**.</span></span> <span data-ttu-id="00486-189">이번에는 **OBJECT=Group**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="00486-190">마지막 페이지에서 다음 그림과 같이 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="00486-191">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-191">Click **Finish**.</span></span>  
   <span data-ttu-id="00486-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="00486-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="00486-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="00486-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="00486-194">선택 사항: 원하는 경우 추가 실행 프로필을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00486-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="00486-195">이 연습에서는 전체 가져오기만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="00486-196">**확인** 을 클릭하여 실행 프로필 변경을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="00486-197">일부 테스트 데이터를 추가하고 가져오기 테스트</span><span class="sxs-lookup"><span data-stu-id="00486-197">Add some test data and test the import</span></span>
<span data-ttu-id="00486-198">샘플 데이터베이스에서 일부 테스트 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="00486-199">준비되었으면 **실행** 및 **전체 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00486-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="00486-200">다음은 두 개의 전화 번호가 있는 사용자와 몇 명의 구성원이 있는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="00486-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="00486-203">부록 A</span><span class="sxs-lookup"><span data-stu-id="00486-203">Appendix A</span></span>
<span data-ttu-id="00486-204">**샘플 데이터베이스를 만드는 SQL 스크립트**</span><span class="sxs-lookup"><span data-stu-id="00486-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
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
