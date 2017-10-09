---
title: "Microsoft Azure에서 개인 데이터 aaaManage | Microsoft Docs"
description: "toocorrect를 업데이트, 삭제 및 Azure Active Directory 및 Azure SQL 데이터베이스의 개인 데이터를 내보내는 방법에 대 한 지침"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="d5f15-103">Microsoft Azure에서 개인 데이터 관리</span><span class="sxs-lookup"><span data-stu-id="d5f15-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="d5f15-104">이 문서는 toocorrect를 업데이트, 삭제 및 Azure Active Directory 및 Azure SQL 데이터베이스의 개인 데이터를 내보내는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="d5f15-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="d5f15-105">Scenario</span></span>

<span data-ttu-id="d5f15-106">더블린 기반 회사 하이엔드 대상 결혼 아일랜드에는 현지 및 국제적 고객층을 둘 다에 대 한 hello 전 세계에 대 한 통합 저장소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="d5f15-107">사무실, 고객, 직원 및 공급 업체 hello world toofully 서비스 hello 운송 수단을 제공 하는 주변에 있는 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="d5f15-108">다른 많은 항목 간의 hello 회사는 음식 질병 및 식사 기본 설정을 포함 하는 않으십니까의 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="d5f15-109">결혼 게스트 및 타기 등, 탈 싸우겠다는 보트 서핑와 같은 다양 한 활동에 대 한 등록도 상호 작용 하는 중앙 웹 페이지에서 toohello 이벤트 시키는 hello 개월 동안 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="d5f15-110">hello 회사는 직원, 공급 업체, 고객 및 결혼 게스트에서 개인 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="d5f15-111">Hello 인해 hello 비즈니스 hello 회사의 국제 특성 여러 수준 규정에 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="d5f15-112">문제 설명</span><span class="sxs-lookup"><span data-stu-id="d5f15-112">Problem statement</span></span>

- <span data-ttu-id="d5f15-113">데이터 관리자 수 toocorrect 부정확 한 개인 정보 불완전 하거나 변경 개인 정보 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="d5f15-114">데이터 관리자 요구는 데이터 주체의 hello 요청에 따라 수 toodelete 개인 정보 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="d5f15-115">데이터 관리자 tooexport 데이터가 필요 하 고 tooa 데이터 주제가 요청에 따라 일반적으로 구조적 형식에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="d5f15-116">회사 목표</span><span class="sxs-lookup"><span data-stu-id="d5f15-116">Company goals</span></span>

- <span data-ttu-id="d5f15-117">정확하지 않거나 불완전한 고객, 웨딩 게스트, 직원 및 공급 업체 개인 정보를 수정하거나 Azure Active Directory 및 Azure SQL Database에 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="d5f15-118">개인 정보는 데이터 주체의 hello 요청에 따라 Azure Active Directory 및 Azure SQL 데이터베이스에서 삭제 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="d5f15-119">개인 데이터는 데이터 주체의 hello 요청에 따라 일반적으로 구조적 형식으로 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="d5f15-120">솔루션</span><span class="sxs-lookup"><span data-stu-id="d5f15-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="d5f15-121">Azure Active Directory: 부정확하거나 완료되지 않은 개인 데이터 수정 및 개인 데이터/사용자 프로필 지우기/삭제</span><span class="sxs-lookup"><span data-stu-id="d5f15-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="d5f15-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="d5f15-123">수정, 업데이트 또는 삭제 고객 및 직원에 해당 하는 사용자의 프로필 및 사용자 작업 정보에 사용자의 이름, 직함, 주소 또는 전화 번호 등의 개인 데이터를 포함 하 여 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) hello를 사용 하 여 환경 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="d5f15-124">Hello 디렉터리에 대 한 전역 관리자 인 계정으로 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="d5f15-125">Azure Active Directory에서 사용자 프로필 및 작업 정보를 수정하거나 업데이트하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d5f15-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="d5f15-126">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="d5f15-127">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="d5f15-129">Hello에 **사용자 및 그룹** 블레이드를 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="d5f15-131">Hello에 **사용자 및 그룹-사용자가** 블레이드를 hello 목록에서 사용자를 선택한 다음 선택 hello 선택한 사용자에 대 한 hello 블레이드에서 **프로필** 수정 toobe 필요한 tooview hello 사용자 프로필 정보 또는 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="d5f15-133">수정 하거나 hello 정보를 업데이트 한 다음 hello 명령 모음에서 선택 **저장 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5f15-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="d5f15-134">Hello 선택한 사용자에 대 한 hello 블레이드에서 선택 **작업 정보** toobe 필요한 tooview 사용자 작업 정보를 수정 또는 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="d5f15-136">수정 하거나 hello 사용자 작업 정보를 업데이트 한 다음 hello 명령 모음에서 선택 **저장 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d5f15-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="d5f15-137">Azure Active Directory에서 사용자 프로필을 삭제하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d5f15-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="d5f15-138">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="d5f15-139">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="d5f15-140">Hello에 **사용자 및 그룹** 블레이드를 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="d5f15-142">Hello에 **사용자 및 그룹-사용자가** 블레이드에서 hello 목록에서 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="d5f15-144">Hello 선택한 사용자에 대 한 hello 블레이드에서 선택 **개요**를 선택한 다음 hello 명령 모음에서 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="d5f15-145">SQL Database: 부정확하거나 완료되지 않은 개인 데이터 수정, 개인 데이터 지우기/삭제, 개인 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="d5f15-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="d5f15-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)는 개발자가 응용 프로그램을 빌드하고 유지하는 데 유용한 클라우드 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="d5f15-147">개인 데이터를 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)에서 표준 SQL 쿼리를 사용하여 업데이트할 수 있습니다. 또한 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="d5f15-148">또한 다양 한 다양 한 형식으로 BACPAC 파일을 포함 하 고 hello Azure SQL Server 가져오기 및 내보내기 마법사를 포함 한 메서드를 사용 하 여 SQL 데이터베이스에서 개인 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="d5f15-149">SQL Database에서 개인 데이터를 수정, 업데이트 또는 지우려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d5f15-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="d5f15-150">toolearn SQL 데이터베이스의 개인 데이터 toocorrect 또는 업데이트 hello를 방문 하는 방법을 [업데이트 (Transact SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [텍스트 업데이트](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [with 공통 테이블 식 업데이트](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), 또는 [ 쓸 텍스트 업데이트](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="d5f15-151">toolearn SQL 데이터베이스의 개인 데이터 toodelete hello를 방문 하는 방법을 [삭제 (Transact SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="d5f15-152">SQL 데이터베이스에서 tooa BACPAC 파일을 개인 데이터를 내보내려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="d5f15-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="d5f15-153">BACPAC 파일 hello SQL 데이터베이스 데이터 및 메타 데이터를 포함 하 고 BACPAC 확장명이 zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="d5f15-154">이렇게 hello를 사용 하 여 [Azure 포털](https://portal.azure.com/), hello SQLPackage 명령줄 유틸리티, SQL Server Management Studio (SSMS), 또는 PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="d5f15-155">toolearn 어떻게 tooexport 데이터 tooa BACPAC 파일을 방문 hello [는 Azure SQL 데이터베이스 tooa BACPAC 파일 내보내기](https://docs.microsoft.com/azure/sql-database/sql-database-export) 위에 나열 된 각 방법에 대 한 자세한 지침이 포함 된 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="d5f15-156">SQL 데이터베이스 hello SQL Server 가져오기 및 내보내기 마법사에서 개인 데이터를 내보내려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="d5f15-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="d5f15-157">이 마법사를 사용 하면 소스 tooa 대상에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="d5f15-158">프로그램 소개 toohello 마법사에 대 한 hello에 어떻게 tooget, 사용 권한 정보 및 hello 도구로 tooget 방법을 방문 비롯 하 여 [가져오기 및 내보내기 데이터로 hello SQL Server 가져오기 및 내보내기 마법사](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="d5f15-159">단계 hello 마법사에 대 한 개요를 방문 hello [hello SQL Server 가져오기 및 내보내기 마법사의 단계를](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d5f15-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5f15-160">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="d5f15-160">Next Steps:</span></span>

[<span data-ttu-id="d5f15-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d5f15-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="d5f15-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5f15-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

