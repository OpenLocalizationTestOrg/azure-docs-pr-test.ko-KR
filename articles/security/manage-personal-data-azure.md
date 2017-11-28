---
title: "Microsoft Azure에서 개인 데이터 관리 | Microsoft Docs"
description: "Azure Active Directory 및 Azure SQL Database에서 개인 데이터를 수정, 업데이트, 삭제 및 내보내는 방법에 관한 지침"
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
ms.openlocfilehash: b04c745feb710d3d1d8a1fce23807168d6e6fa3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="3c08b-103">Microsoft Azure에서 개인 데이터 관리</span><span class="sxs-lookup"><span data-stu-id="3c08b-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="3c08b-104">이 문서는 Azure Active Directory 및 Azure SQL Database에서 개인 데이터를 수정, 업데이트, 삭제 및 내보내는 방법에 관한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-104">This article provides guidance on how to correct, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="3c08b-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="3c08b-105">Scenario</span></span>

<span data-ttu-id="3c08b-106">더블린에 본사를 둔 회사는 아일랜드 및 전세계의 최상위 고객대상 웨딩에 관한 원스톱 쇼핑을 현지 및 국제적 고객 모두를 대상으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around the world for both a local and international customer base.</span></span> <span data-ttu-id="3c08b-107">회사가 제공하는 장소를 완벽히 제공하기 위해 전세계 각지에 사무실, 고객, 직원 및 공급 업체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-107">They have offices, customers, employees, and vendors located around the world to fully service the venues they offer.</span></span>

<span data-ttu-id="3c08b-108">다른 여러 항목 중에 회사는 음식 알레르기 및 음식 선호도를 포함한 RSVP(참석 여부 통지)를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-108">Among many other items, the company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="3c08b-109">웨딩 게스트들은 말타기, 서핑, 보트 타기 등과 같은 다양한 활동에 등록하고, 행사가 열리기 전 수개월 동안 중앙 웹 페이지에서 서로 교류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during the months leading up to the event.</span></span> <span data-ttu-id="3c08b-110">회사는 직원, 공급 업체, 고객 및 웨딩 게스트의 개인 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-110">The company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="3c08b-111">비즈니스의 국제적 특성으로 인해 회사는 다양한 수준의 규정을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-111">Because of the international nature of the business the company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="3c08b-112">문제 설명</span><span class="sxs-lookup"><span data-stu-id="3c08b-112">Problem statement</span></span>

- <span data-ttu-id="3c08b-113">데이터 관리자는 부정확한 개인 정보를 수정하고 불완전하거나 변경된 개인 정보를 업데이트할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-113">Data admins must be able to correct inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="3c08b-114">데이터 관리자 필요 데이터 주체의 요청에 따라 개인 정보를 삭제할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-114">Data admins need must be able to delete personal information upon the request of a data subject.</span></span>

- <span data-ttu-id="3c08b-115">데이터 관리자는 데이터를 내보내고 데이터 주체의 요구에 따라 그들에게 해당 데이터를 공용의 구조화된 형식으로 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-115">Data admins need to export data and provide it to a data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="3c08b-116">회사 목표</span><span class="sxs-lookup"><span data-stu-id="3c08b-116">Company goals</span></span>

- <span data-ttu-id="3c08b-117">정확하지 않거나 불완전한 고객, 웨딩 게스트, 직원 및 공급 업체 개인 정보를 수정하거나 Azure Active Directory 및 Azure SQL Database에 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="3c08b-118">개인 정보는 데이터 주체의 요청에 따라 Azure Active Directory 및 Azure SQL Database에서 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon the request of a data subject.</span></span>

- <span data-ttu-id="3c08b-119">개인 데이터를 데이터 주체의 요청에 따라 공용의 구조화된 형식으로 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-119">Personal data must be exported in a common, structured format upon the request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="3c08b-120">솔루션</span><span class="sxs-lookup"><span data-stu-id="3c08b-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="3c08b-121">Azure Active Directory: 부정확하거나 완료되지 않은 개인 데이터 수정 및 개인 데이터/사용자 프로필 지우기/삭제</span><span class="sxs-lookup"><span data-stu-id="3c08b-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="3c08b-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="3c08b-123">[Azure Portal](https://portal.azure.com/)을 사용하여 [AAD(Azure Active Directory)](https://azure.microsoft.com/services/active-directory/) 환경에서 사용자의 이름, 직함, 주소 또는 전화 번호 등 개인 데이터를 포함하는 고객 및 직원 사용자 프로필 및 사용자 작업 정보를 수정, 업데이트 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="3c08b-124">디렉터리에 대한 전역 관리자인 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-124">You must sign in with an account that’s a global admin for the directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="3c08b-125">Azure Active Directory에서 사용자 프로필 및 작업 정보를 수정하거나 업데이트하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="3c08b-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="3c08b-126">디렉터리에 대한 전역 관리자인 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-126">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="3c08b-127">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-127">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="3c08b-129">**사용자 및 그룹** 블레이드에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-129">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="3c08b-131">**사용자 및 그룹 - 사용자** 블레이드에서 목록에서 사용자를 선택한 다음 선택한 사용자에 대한 블레이드에서 **프로필**을 선택하여 수정하거나 업데이트해야 하는 사용자 프로필 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-131">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view the user profile information that needs to be corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="3c08b-133">정보를 수정하거나 업데이트한 다음, 명령 모음에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-133">Correct or update the information, and then, in the command bar, select **Save.**</span></span>

6.  <span data-ttu-id="3c08b-134">선택한 사용자에 대한 블레이드에서 **작업 정보**를 선택하여 수정하거나 업데이트해야 하는 사용자 작업 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-134">On the blade for the selected user, select **Work Info** to view user work information that needs to be corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="3c08b-136">사용자 작업 정보를 수정하거나 업데이트한 다음, 명령 모음에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-136">Correct or update the user work information, and then, in the command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="3c08b-137">Azure Active Directory에서 사용자 프로필을 삭제하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="3c08b-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="3c08b-138">디렉터리에 대한 전역 관리자인 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-138">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="3c08b-139">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-139">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="3c08b-140">**사용자 및 그룹** 블레이드에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-140">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="3c08b-142">**사용자 및 그룹 - 사용자** 블레이드의 목록에서 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-142">On the **Users and groups - Users** blade, select a user from the list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="3c08b-144">선택한 사용자에 대한 블레이드에서 **개요**를 선택한 다음 명령 모음에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-144">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="3c08b-145">SQL Database: 부정확하거나 완료되지 않은 개인 데이터 수정, 개인 데이터 지우기/삭제, 개인 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="3c08b-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="3c08b-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)는 개발자가 응용 프로그램을 빌드하고 유지하는 데 유용한 클라우드 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="3c08b-147">개인 데이터를 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)에서 표준 SQL 쿼리를 사용하여 업데이트할 수 있습니다. 또한 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="3c08b-148">또한 Azure SQL Server 가져오기 및 내보내기 마법사를 포함한 다양한 메서드를 사용하여 SQL Database에서 개인 데이터를 BACPAC 파일을 비롯한 다양한 형식으로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including the Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="3c08b-149">SQL Database에서 개인 데이터를 수정, 업데이트 또는 지우려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="3c08b-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="3c08b-150">SQL Database에서 개인 데이터를 수정 또는 업데이트하는 방법을 알아보려면 [업데이트(Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [텍스트 업데이트](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [공통 테이블 식을 사용한 업데이트](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql) 또는 [쓰기 텍스트 업데이트](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) 설명서를 방문해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3c08b-150">To learn how to correct or update personal data in SQL Database, visit the [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="3c08b-151">SQL Database에서 개인 데이터를 삭제하는 방법을 알아보려면 [삭제(Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) 설명서를 방문해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3c08b-151">To learn how to delete personal data in SQL Database, visit the [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-to-a-bacpac-file-in-sql-database"></a><span data-ttu-id="3c08b-152">SQL Database에서 BACPAC 파일로 개인 데이터를 내보내려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="3c08b-152">How do I export personal data to a BACPAC file in SQL Database?</span></span>

<span data-ttu-id="3c08b-153">BACPAC 파일에는 SQL Database 데이터 및 메타데이터가 포함되어 있으며 BACPAC 확장명은 zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-153">A BACPAC file includes the SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="3c08b-154">[Azure Portal](https://portal.azure.com/), SQLPackage 명령줄 유틸리티, SSMS(SQL Server Management Studio) 또는 PowerShell을 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-154">This can be done using the [Azure portal](https://portal.azure.com/), the SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="3c08b-155">데이터를 BACPAC 파일로 내보내는 방법을 알아보려면 위에 나열된 각 메서드에 대한 자세한 지침이 포함된 [Azure SQL Database를 BACPAC 파일로 내보내기](https://docs.microsoft.com/azure/sql-database/sql-database-export)를 방문해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3c08b-155">To learn how to export data to a BACPAC file, visit the [Export an Azure SQL database to a BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="3c08b-156">SQL Server 가져오기 및 내보내기 마법사를 사용하여 SQL Database에서 개인 데이터를 내보내려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="3c08b-156">How do I export personal data from SQL Database with the SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="3c08b-157">이 마법사는 데이터를 원본에서 대상으로 복사하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c08b-157">This wizard helps you copy data from a source to a destination.</span></span> <span data-ttu-id="3c08b-158">준비 방법, 사용 권한 정보 및 도구에 관한 도움말 얻기가 포함된 마법사에 대한 소개는 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) 웹 페이지를 방문해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3c08b-158">For an introduction to the wizard, including how to get it, permissions information, and how to get help with the tool, visit the [Import and Export Data with the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="3c08b-159">마법사에 대한 단계 개요는 [SQL Server 가져오기 및 내보내기 마법사의 단계](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) 웹 페이지를 방문해 보세요.</span><span class="sxs-lookup"><span data-stu-id="3c08b-159">For an overview of steps for the wizard, visit the [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c08b-160">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="3c08b-160">Next Steps:</span></span>

[<span data-ttu-id="3c08b-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3c08b-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="3c08b-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c08b-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

