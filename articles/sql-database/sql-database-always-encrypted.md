---
title: "상시 암호화: Azure SQL Database - Windows 인증서 저장소 | Microsoft Docs"
description: "이 문서에서는 SSMS(SQL Server Management Studio)의 상시 암호화 마법사를 사용하여 데이터베이스 암호화로 SQL Database의 중요한 데이터를 보호하는 방법을 보여 줍니다. 그뿐 아니라 Windows 인증서 저장소에 암호화 키를 저장하는 방법을 보여 줍니다."
keywords: "데이터 암호화, sql 암호화, 데이터베이스 암호화, 중요한 데이터 암호화, 상시 암호화"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: d1fdfc4f739e65ff532b159eefaffe1622ad0963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-the-windows-certificate-store"></a><span data-ttu-id="b49ff-105">상시 암호화 - SQL 데이터베이스의 중요한 데이터 보호 및 Windows 인증서 저장소에 암호화 키 저장</span><span class="sxs-lookup"><span data-stu-id="b49ff-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in the Windows certificate store</span></span>

<span data-ttu-id="b49ff-106">이 문서에서는 [SSMS(SQL Server Management Studio)](https://msdn.microsoft.com/library/hh213248.aspx)의 [상시 암호화 마법사](https://msdn.microsoft.com/library/mt459280.aspx)를 사용하여 데이터베이스 암호화로 SQL Database의 중요한 데이터를 보호하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-106">This article shows you how to secure sensitive data in a SQL database with database encryption by using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="b49ff-107">그뿐 아니라 Windows 인증서 저장소에 암호화 키를 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-107">It also shows you how to store your encryption keys in the Windows certificate store.</span></span>

<span data-ttu-id="b49ff-108">상시 암호화는 클라이언트와 서버 사이의 이동 중에, 그리고 데이터를 사용 중일 때 서버에서 중요한 미사용 데이터를 보호하는 Azure SQL 데이터베이스 및 SQL Server 내의 새로운 데이터 암호 기술로서, 중요한 데이터가 데이터베이스 시스템에서 일반 텍스트로 나타나지 않도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use, ensuring that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="b49ff-109">키에 액세스할 수 있는 클라이언트 응용 프로그램 또는 앱 서버는 일반 텍스트 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-109">After you encrypt data, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="b49ff-110">자세한 내용은 [상시 암호화(데이터베이스 엔진)](https://msdn.microsoft.com/library/mt163865.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b49ff-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="b49ff-111">상시 암호화를 사용하는 데이터베이스를 구성한 후에 Visual Studio로 C#에서 클라이언트 응용 프로그램을 만들어 암호화된 데이터로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-111">After configuring the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="b49ff-112">이 문서의 단계를 수행하고 Azure SQL 데이터베이스에 대해 상시 암호화를 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-112">Follow the steps in this article to learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="b49ff-113">이 문서에서는 다음 작업을 수행하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-113">In this article, you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="b49ff-114">SSMS에서 상시 암호화 마법사를 사용하여 [상시 암호화 키](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-114">Use the Always Encrypted wizard in SSMS to create [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="b49ff-115">[CMK(열 마스터 키)](https://msdn.microsoft.com/library/mt146393.aspx)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="b49ff-116">[CEK(열 암호화 키)](https://msdn.microsoft.com/library/mt146372.aspx)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="b49ff-117">데이터베이스 테이블을 만들고 열을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="b49ff-118">암호화된 열에서 데이터를 삽입하고 선택하며 표시한 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-118">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b49ff-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b49ff-119">Prerequisites</span></span>
<span data-ttu-id="b49ff-120">이 자습서에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="b49ff-121">Azure 계정 및 구독</span><span class="sxs-lookup"><span data-stu-id="b49ff-121">An Azure account and subscription.</span></span> <span data-ttu-id="b49ff-122">없는 경우 지금 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="b49ff-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b49ff-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 버전 13.0.700.242 이상.</span><span class="sxs-lookup"><span data-stu-id="b49ff-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="b49ff-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) 이상(클라이언트 컴퓨터에서).</span><span class="sxs-lookup"><span data-stu-id="b49ff-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="b49ff-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="b49ff-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="b49ff-126">빈 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b49ff-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="b49ff-127">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-127">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b49ff-128">**새로 만들기** > **데이터 + 저장소** > **SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="b49ff-129">새 서버 또는 기존 서버에 **클리닉**이라는 **빈** 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="b49ff-130">Azure Portal에서 데이터베이스를 만드는 자세한 지침은 [첫 Azure SQL Database](sql-database-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b49ff-130">For detailed instructions about creating a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![빈 데이터베이스 만들기](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="b49ff-132">자습서의 뒷부분에서 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-132">You will need the connection string later in the tutorial.</span></span> <span data-ttu-id="b49ff-133">데이터베이스를 만든 후에 새 Clinic 데이터베이스로 이동하고 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-133">After the database is created, go to the new Clinic database and copy the connection string.</span></span> <span data-ttu-id="b49ff-134">언제든지 연결 문자열을 가져올 수 있지만 Azure 포털에 있을 때 복사하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-134">You can get the connection string at any time, but it's easy to copy it when you're in the Azure portal.</span></span>

1. <span data-ttu-id="b49ff-135">**SQL Databases** > **Clinic** > **데이터베이스 연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="b49ff-136">**ADO.NET**에 대한 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-136">Copy the connection string for **ADO.NET**.</span></span>
   
    ![연결 문자열 복사](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="b49ff-138">SSMS로 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="b49ff-138">Connect to the database with SSMS</span></span>
<span data-ttu-id="b49ff-139">SSMS를 열고 클리닉 데이터베이스가 있는 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-139">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="b49ff-140">SSMS를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-140">Open SSMS.</span></span> <span data-ttu-id="b49ff-141">(열리지 않은 경우 **연결** > **데이터베이스 엔진**을 클릭하여 **서버에 연결** 창을 엽니다.)</span><span class="sxs-lookup"><span data-stu-id="b49ff-141">(Click **Connect** > **Database Engine** to open the **Connect to Server** window if it is not open).</span></span>
2. <span data-ttu-id="b49ff-142">서버 이름 및 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-142">Enter your server name and credentials.</span></span> <span data-ttu-id="b49ff-143">앞에서 복사한 SQL 데이터베이스 블레이드 및 연결 문자열에 서버 이름을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-143">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="b49ff-144">*database.windows.net*을 포함하여 전체 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-144">Type the complete server name including *database.windows.net*.</span></span>
   
    ![연결 문자열 복사](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="b49ff-146">**새 방화벽 규칙** 창이 열리면 Azure에 로그인하고 SSMS가 새 방화벽 규칙을 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-146">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="b49ff-147">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="b49ff-147">Create a table</span></span>
<span data-ttu-id="b49ff-148">이 섹션에서는 환자 데이터를 저장할 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-148">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="b49ff-149">처음에는 일반 테이블이지만 다음 섹션에서 암호화를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-149">This will be a normal table initially--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="b49ff-150">**데이터베이스**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="b49ff-151">**Clinic** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-151">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="b49ff-152">새 쿼리 창에 다음 Transact-SQL(T-SQL)을 붙여넣고 **실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-152">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="b49ff-153">열 암호화(상시 암호화 구성)</span><span class="sxs-lookup"><span data-stu-id="b49ff-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="b49ff-154">SSMS는 CMK, CEK 및 암호화된 열을 설정하여 상시 암호화를 쉽게 구성하는 마법사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-154">SSMS provides a wizard to easily configure Always Encrypted by setting up the CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="b49ff-155">**데이터베이스** > **빈** > **테이블**를 사용하여 데이터베이스 암호화로 SQL 데이터베이스의 중요한 데이터를 보호하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="b49ff-156">**Patients** 테이블을 마우스 오른쪽 단추로 클릭하고 **열 암호화**를 선택하여 상시 암호화 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-156">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![열 암호화](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="b49ff-158">상시 암호화 마법사에는 **열 선택**, **마스터 키 구성**(CMK), **유효성 검사** 및 **요약** 섹션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-158">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="b49ff-159">열 선택</span><span class="sxs-lookup"><span data-stu-id="b49ff-159">Column Selection</span></span>
<span data-ttu-id="b49ff-160">**소개** 페이지에서 **다음**을 클릭하여 **열 선택** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-160">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="b49ff-161">이 페이지에서 암호화하려는 열, [암호화 형식 및 사용할 CEK(열 암호화 키)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-161">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="b49ff-162">각 환자에 대해 **SSN** 및 **BirthDate** 정보를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="b49ff-163">**SSN** 열은 같음 조회, 조인 및 그룹화를 지원하는 결정적 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-163">The **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="b49ff-164">**BirthDate** 열은 작업을 지원하지 않는 임의의 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-164">The **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="b49ff-165">**SSN** 열에 대한 **암호화 형식**을 **결정적**으로 설정하고 **BirthDate** 열을 **무작위**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-165">Set the **Encryption Type** for the **SSN** column to **Deterministic** and the **BirthDate** column to **Randomized**.</span></span> <span data-ttu-id="b49ff-166">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-166">Click **Next**.</span></span>

![열 암호화](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="b49ff-168">마스터 키 구성</span><span class="sxs-lookup"><span data-stu-id="b49ff-168">Master Key Configuration</span></span>
<span data-ttu-id="b49ff-169">**마스터 키 구성** 페이지는 CMK를 설치하고 CMK가 저장될 키 저장소 공급자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-169">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="b49ff-170">현재 Windows 인증서 저장소, Azure 주요 자격 증명 모음 또는 하드웨어 보안 모듈(HSM)에 CMK를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-170">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="b49ff-171">이 자습서에는 Windows 인증서 저장소에 키를 저장하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-171">This tutorial shows how to store your keys in the Windows certificate store.</span></span>

<span data-ttu-id="b49ff-172">**Windows 인증서 저장소**가 선택되었는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![마스터 키 구성](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="b49ff-174">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="b49ff-174">Validation</span></span>
<span data-ttu-id="b49ff-175">이제 열을 암호화하거나 나중에 실행할 PowerShell 스크립트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-175">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="b49ff-176">이 자습서의 경우 **지금 전체 과정 진행**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-176">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="b49ff-177">요약</span><span class="sxs-lookup"><span data-stu-id="b49ff-177">Summary</span></span>
<span data-ttu-id="b49ff-178">설정이 모두 정확한 것을 확인하고 **마침** 을 클릭하여 상시 암호화에 대한 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-178">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![요약](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="b49ff-180">마법사의 작업 확인</span><span class="sxs-lookup"><span data-stu-id="b49ff-180">Verify the wizard's actions</span></span>
<span data-ttu-id="b49ff-181">마법사가 완료된 후에 데이터베이스는 상시 암호화에 대해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-181">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="b49ff-182">마법사는 다음 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-182">The wizard performed the following actions:</span></span>

* <span data-ttu-id="b49ff-183">CMK를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-183">Created a CMK.</span></span>
* <span data-ttu-id="b49ff-184">CEK를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-184">Created a CEK.</span></span>
* <span data-ttu-id="b49ff-185">암호화에 선택한 열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-185">Configured the selected columns for encryption.</span></span> <span data-ttu-id="b49ff-186">**Patients** 테이블에는 현재 데이터가 없지만 이제 선택된 열의 기존 데이터가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-186">Your **Patients** table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="b49ff-187">**Clinic** > **보안** > **상시 암호화 키**로 이동하여 SSMS에서 키 만들기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-187">You can verify the creation of the keys in SSMS by going to **Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="b49ff-188">이제 마법사에서 생성한 새 키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-188">You can now see the new keys that the wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="b49ff-189">암호화된 데이터로 작동하는 클라이언트 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b49ff-189">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="b49ff-190">상시 암호화가 설정되었으므로 암호화된 열에서 *삽입* 및 *선택*을 수행하는 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span> <span data-ttu-id="b49ff-191">샘플 응용 프로그램을 성공적으로 실행하려면 상시 암호화 마법사를 실행한 동일한 컴퓨터에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-191">To successfully run the sample application, you must run it on the same computer where you ran the Always Encrypted wizard.</span></span> <span data-ttu-id="b49ff-192">다른 컴퓨터에서 이 응용 프로그램을 실행하려면 클라이언트 앱을 실행하는 컴퓨터에 상시 암호화 인증서를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-192">To run the application on another computer, you must deploy your Always Encrypted certificates to the computer running the client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="b49ff-193">상시 암호화 열이 있는 서버에 일반 텍스트 데이터를 전달하는 경우 응용 프로그램은 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 개체를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="b49ff-194">SqlParameter 개체를 사용하지 않고 리터럴 값을 전달하면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="b49ff-195">Visual Studio를 열고 새 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="b49ff-196">프로젝트가 **.NET Framework 4.6** 이상으로 설정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-196">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="b49ff-197">프로젝트 이름을 **AlwaysEncryptedConsoleApp**으로 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-197">Name the project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="b49ff-199">연결 문자열을 수정하여 상시 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="b49ff-199">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="b49ff-200">이 섹션에는 데이터베이스 연결 문자열에서 상시 암호화를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-200">This section explains how to enable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="b49ff-201">다음 섹션 "상시 암호화 샘플 콘솔 응용 프로그램"에서 실제로 방금 만든 콘솔 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-201">You will modify the console app you just created in the next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="b49ff-202">상시 암호화를 사용하려면 **열 암호화 설정** 키워드를 연결 문자열에 추가하고 **사용함**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-202">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="b49ff-203">이 연결 문자열에서 직접 설정하거나 [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)를 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-203">You can set this directly in the connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="b49ff-204">다음 섹션에서 응용 프로그램 예제는 **SqlConnectionStringBuilder**를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-204">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="b49ff-205">상시 암호화에 특정된 클라이언트 응용 프로그램에서 필요한 유일한 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-205">This is the only change required in a client application specific to Always Encrypted.</span></span> <span data-ttu-id="b49ff-206">외부(즉, 구성 파일)에서 연결 문자열을 저장하는 기존 응용 프로그램이 있는 경우 코드를 변경하지 않고 상시 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able to enable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="b49ff-207">연결 문자열에서 상시 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="b49ff-207">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="b49ff-208">연결 문자열에 다음 키워드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-208">Add the following keyword to your connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="b49ff-209">SqlConnectionStringBuilder로 상시 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="b49ff-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="b49ff-210">다음 코드는 [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx)을 [사용함](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)으로 설정하여 상시 암호화를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-210">The following code shows how to enable Always Encrypted by setting the [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="b49ff-211">상시 암호화 샘플 콘솔 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b49ff-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="b49ff-212">이 샘플에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="b49ff-213">연결 문자열을 수정하여 상시 암호화 사용.</span><span class="sxs-lookup"><span data-stu-id="b49ff-213">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="b49ff-214">암호화된 열에 데이터 삽입.</span><span class="sxs-lookup"><span data-stu-id="b49ff-214">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="b49ff-215">암호화된 열에서 특정 값에 필터링하여 레코드 선택.</span><span class="sxs-lookup"><span data-stu-id="b49ff-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="b49ff-216">**Program.cs** 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-216">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="b49ff-217">Main 메서드 바로 위의 줄에서 전역 connectionString 변수에 대한 연결 문자열을 Azure 포털에서 유효한 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-217">Replace the connection string for the global connectionString variable in the line directly above the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="b49ff-218">이 코드에 대한 유일한 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-218">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="b49ff-219">작업에서 상시 암호화를 확인하려면 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-219">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from the Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for the connection.
            // This is the only change specific to Always Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update the connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign the updated connection string to our global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records to restart this demo app.
            ResetPatientsTable();

            // Add sample data to the Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data to the database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // The example allows duplicate SSN entries so we will return all records
            // that match the provided value and store the results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("The following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key to exit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in the Patients table to reset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="b49ff-220">데이터가 암호화되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-220">Verify that the data is encrypted</span></span>
<span data-ttu-id="b49ff-221">SSMS로 **Patients** 데이터를 쿼리하여 서버의 실제 데이터가 암호화되었는지 신속하게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-221">You can quickly check that the actual data on the server is encrypted by querying the **Patients** data with SSMS.</span></span> <span data-ttu-id="b49ff-222">(열 암호화 설정이 아직 사용되도록 설정되지 않은 경우 현재 연결을 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="b49ff-222">(Use your current connection where the column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="b49ff-223">Clinic 데이터베이스에 대해 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-223">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="b49ff-224">암호화된 열에 일반 텍스트 데이터가 포함되지 않은 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-224">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="b49ff-226">SSMS를 사용하여 일반 텍스트 데이터에 액세스하려면 **열 암호화 설정=활성화** 매개 변수를 연결에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-226">To use SSMS to access the plaintext data, you can add the **Column Encryption Setting=enabled** parameter to the connection.</span></span>

1. <span data-ttu-id="b49ff-227">SSMS에서 **개체 탐색기**에 있는 서버를 마우스 오른쪽 단추로 클릭하고 **연결 끊기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="b49ff-228">**연결** > **데이터베이스 엔진**을 클릭하여 **서버에 연결** 창을 열고 **옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-228">Click **Connect** > **Database Engine** to open the **Connect to Server** window, and then click **Options**.</span></span>
3. <span data-ttu-id="b49ff-229">**추가 연결 매개 변수**를 클릭하고 **열 암호화 설정=활성화**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="b49ff-231">**Clinic** 데이터베이스에 대해 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-231">Run the following query on the **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="b49ff-232">이제 암호화된 열에서 일반 텍스트 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-232">You can now see the plaintext data in the encrypted columns.</span></span>

    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="b49ff-234">다른 컴퓨터에서 SSMS(또는 클라이언트)와 연결한 경우 암호화 키에 대한 액세스 권한이 없으므로 데이터를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-234">If you connect with SSMS (or any client) from a different computer, it will not have access to the encryption keys and will not be able to decrypt the data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b49ff-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b49ff-235">Next steps</span></span>
<span data-ttu-id="b49ff-236">상시 암호화를 사용하는 데이터베이스를 만든 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-236">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="b49ff-237">다른 컴퓨터에서 이 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-237">Run this sample from a different computer.</span></span> <span data-ttu-id="b49ff-238">암호화 키에 대한 액세스 권한이 없으므로 일반 텍스트 데이터에 액세스할 수 없고 성공적으로 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b49ff-238">It won't have access to the encryption keys, so it will not have access to the plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="b49ff-239">[키 회전 및 정리](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="b49ff-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="b49ff-240">[상시 암호화로 이미 암호화된 데이터 마이그레이션](https://msdn.microsoft.com/library/mt621539.aspx)</span><span class="sxs-lookup"><span data-stu-id="b49ff-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="b49ff-241">[다른 클라이언트 컴퓨터에 상시 암호화 인증서 배포](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) ("응용 프로그램 및 사용자가 인증서를 사용할 수 있도록 지정" 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="b49ff-241">[Deploy Always Encrypted certificates to other client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see the "Making Certificates Available to Applications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="b49ff-242">관련 정보</span><span class="sxs-lookup"><span data-stu-id="b49ff-242">Related information</span></span>
* [<span data-ttu-id="b49ff-243">상시 암호화(클라이언트 개발)</span><span class="sxs-lookup"><span data-stu-id="b49ff-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="b49ff-244">투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="b49ff-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="b49ff-245">SQL Server 암호화</span><span class="sxs-lookup"><span data-stu-id="b49ff-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="b49ff-246">상시 암호화 마법사</span><span class="sxs-lookup"><span data-stu-id="b49ff-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="b49ff-247">상시 암호화 블로그</span><span class="sxs-lookup"><span data-stu-id="b49ff-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

