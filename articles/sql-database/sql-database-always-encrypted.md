---
title: "상시 암호화: Azure SQL Database - Windows 인증서 저장소 | Microsoft Docs"
description: "이 문서에서는 toosecure 중요 한 데이터를 사용 하 여 데이터베이스 암호화는 SQL 데이터베이스에서 상시 암호화 마법사 SQL Server Management Studio (SSMS) hello 하는 방법을 보여 줍니다. 또한 표시 방법을 toostore hello Windows 인증서에 암호화 키를 저장 합니다."
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
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="aa2b4-105">SQL 데이터베이스의 중요 한 데이터를 보호 하 고 hello Windows 인증서 저장소에 암호화 키 저장 항상 암호화:</span><span class="sxs-lookup"><span data-stu-id="aa2b4-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="aa2b4-106">이 문서에서는 hello를 사용 하 여 데이터베이스 암호화 된 데이터베이스 SQL의 중요 한 데이터 toosecure 방법 [상시 암호화 마법사](https://msdn.microsoft.com/library/mt459280.aspx) 에 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="aa2b4-107">또한 표시 방법을 toostore hello Windows 인증서에 암호화 키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="aa2b4-108">상시 암호화는 Azure SQL 데이터베이스에서 새 데이터 암호화 기술을 도움이 되는 SQL Server 클라이언트와 서버 간에 이동 하는 동안 중요 한 hello 서버에 저장 된 상태의 데이터를 보호 하 고 hello 데이터 사용 중으로 표시 하지 않고도 중요 한 데이터 확인 hello 데이터베이스 시스템 내부 일반 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="aa2b4-109">데이터를 암호화 한 후 클라이언트 응용 프로그램 또는 응용 프로그램 키가 서버를 액세스 toohello 일반 텍스트 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="aa2b4-110">자세한 내용은 [상시 암호화(데이터베이스 엔진)](https://msdn.microsoft.com/library/mt163865.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="aa2b4-111">Hello 데이터베이스 toouse 상시 암호화를 구성 했으면 C#으로 Visual Studio toowork hello 암호화 된 데이터와 클라이언트 응용 프로그램이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="aa2b4-112">에서 다음과 같이 hello이 문서 toolearn 어떻게 Azure SQL 데이터베이스에 대 한 상시 암호화를 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="aa2b4-113">이 문서에서는 tooperform hello 다음 작업 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="aa2b4-114">SSMS toocreate에서 사용 하 여 hello 상시 암호화 마법사 [상시 암호화 키](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="aa2b4-115">[CMK(열 마스터 키)](https://msdn.microsoft.com/library/mt146393.aspx)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="aa2b4-116">[CEK(열 암호화 키)](https://msdn.microsoft.com/library/mt146372.aspx)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="aa2b4-117">데이터베이스 테이블을 만들고 열을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="aa2b4-118">삽입 선택한 hello 암호화 된 열에서 데이터를 표시 하는 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa2b4-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="aa2b4-119">Prerequisites</span></span>
<span data-ttu-id="aa2b4-120">이 자습서에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="aa2b4-121">Azure 계정 및 구독</span><span class="sxs-lookup"><span data-stu-id="aa2b4-121">An Azure account and subscription.</span></span> <span data-ttu-id="aa2b4-122">없는 경우 지금 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="aa2b4-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 버전 13.0.700.242 이상.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="aa2b4-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) hello 클라이언트 컴퓨터에 이상.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="aa2b4-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa2b4-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="aa2b4-126">빈 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="aa2b4-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="aa2b4-127">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="aa2b4-128">**새로 만들기** > **데이터 + 저장소** > **SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="aa2b4-129">새 서버 또는 기존 서버에 **클리닉**이라는 **빈** 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="aa2b4-130">Hello Azure 포털에서에서 데이터베이스를 만드는 방법에 대 한 자세한 지침을 참조 하십시오. [첫 번째 Azure SQL 데이터베이스](sql-database-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![빈 데이터베이스 만들기](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="aa2b4-132">Hello 자습서의 뒷부분에 나오는 hello 연결 문자열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="aa2b4-133">Hello 데이터베이스를 만든 후 toohello 새 Clinic 데이터베이스와 복사본 hello 연결 문자열을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="aa2b4-134">언제 든 지 hello 연결 문자열을 가져올 수 있지만 간편한 toocopy hello Azure 포털에에서 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="aa2b4-135">**SQL Databases** > **Clinic** > **데이터베이스 연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="aa2b4-136">에 대 한 연결 문자열 hello 복사 **ADO.NET**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Hello 연결 문자열 복사](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="aa2b4-138">SSMS를 사용 하 여 toohello 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="aa2b4-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="aa2b4-139">SSMS를 열고 toohello 서버 hello Clinic 데이터베이스와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="aa2b4-140">SSMS를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-140">Open SSMS.</span></span> <span data-ttu-id="aa2b4-141">(클릭 **연결** > **데이터베이스 엔진** tooopen hello **tooServer 연결** 창이 열려 있지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="aa2b4-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="aa2b4-142">서버 이름 및 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-142">Enter your server name and credentials.</span></span> <span data-ttu-id="aa2b4-143">hello 연결 문자열에 앞에서 복사한을 hello 서버 이름을 hello SQL 데이터베이스 블레이드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="aa2b4-144">형식 hello 서버 전체 이름을 포함 하 여 *database.windows.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Hello 연결 문자열 복사](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="aa2b4-146">경우 hello **새 방화벽 규칙** 창이 열리고 tooAzure에 로그인 하 고 SSMS를 통해 사용자에 대 한 새 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="aa2b4-147">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="aa2b4-147">Create a table</span></span>
<span data-ttu-id="aa2b4-148">이 섹션에서는 테이블 toohold 환자 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="aa2b4-149">됩니다 일반 테이블 처음-hello 다음 섹션에서 암호화를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="aa2b4-150">**데이터베이스**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="aa2b4-151">마우스 오른쪽 단추로 클릭 hello **클리닉** 클릭 하 고 데이터베이스 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="aa2b4-152">TRANSACT-SQL (T-SQL) hello 새 쿼리 창에 다음 붙여넣기 hello 및 **Execute** 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="aa2b4-153">열 암호화(상시 암호화 구성)</span><span class="sxs-lookup"><span data-stu-id="aa2b4-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="aa2b4-154">마법사를 제공 하는 SSMS tooeasily 상시 암호화를 구성 하면 한 hello CMK, CEK를 암호화 된 열을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="aa2b4-155">**데이터베이스** > **빈** > **테이블**를 사용하여 데이터베이스 암호화로 SQL 데이터베이스의 중요한 데이터를 보호하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="aa2b4-156">마우스 오른쪽 단추로 클릭 hello **환자** 테이블을 선택한 **열 암호화** tooopen hello 상시 암호화 마법사:</span><span class="sxs-lookup"><span data-stu-id="aa2b4-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![열 암호화](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="aa2b4-158">hello 상시 암호화 마법사에는 다음 섹션 hello: **열 선택 영역**, **마스터 키 구성** (CMK) **유효성 검사**, 및  **요약**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="aa2b4-159">열 선택</span><span class="sxs-lookup"><span data-stu-id="aa2b4-159">Column Selection</span></span>
<span data-ttu-id="aa2b4-160">클릭 **다음** hello에 **소개** 페이지 tooopen hello **열 선택 영역** 페이지.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="aa2b4-161">이 페이지에서 열을 선택 합니다 tooencrypt, 원하는 [유형의 암호화를 hello 및 어떤 열 암호화 키 (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="aa2b4-162">각 환자에 대해 **SSN** 및 **BirthDate** 정보를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="aa2b4-163">hello **SSN** 열에서 같음 조회, 조인 및 그룹화를 지 원하는 결정적 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="aa2b4-164">hello **BirthDate** 열 작업을 지원 하지 않는 임의 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="aa2b4-165">집합 hello **암호화 유형** hello에 대 한 **SSN** 열 너무**결정적** 및 hello **BirthDate** 열 너무 **임의**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="aa2b4-166">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-166">Click **Next**.</span></span>

![열 암호화](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="aa2b4-168">마스터 키 구성</span><span class="sxs-lookup"><span data-stu-id="aa2b4-168">Master Key Configuration</span></span>
<span data-ttu-id="aa2b4-169">hello **마스터 키 구성** 설정한 CMK 및 선택 hello 키 저장소 공급자를 hello CMK를 저장할 페이지는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="aa2b4-170">현재 hello Windows 인증서 저장소, Azure 주요 자격 증명 모음 또는 하드웨어 보안 모듈 (HSM)는 CMK를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="aa2b4-171">이 자습서에서는 어떻게 toostore hello Windows 인증서에 키에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="aa2b4-172">**Windows 인증서 저장소**가 선택되었는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![마스터 키 구성](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="aa2b4-174">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="aa2b4-174">Validation</span></span>
<span data-ttu-id="aa2b4-175">이제 hello 열을 암호화 하거나 PowerShell 스크립트 toorun를 나중에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="aa2b4-176">이 자습서에 대 한 선택 **지금 toofinish 진행** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="aa2b4-177">요약</span><span class="sxs-lookup"><span data-stu-id="aa2b4-177">Summary</span></span>
<span data-ttu-id="aa2b4-178">Hello 설정이 모두 정확 하 고 클릭 확인 **마침** 상시 암호화를 위한 toocomplete hello 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![요약](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="aa2b4-180">Hello 마법사 작업 확인</span><span class="sxs-lookup"><span data-stu-id="aa2b4-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="aa2b4-181">Hello 마법사가 완료 되 면 데이터베이스에 상시 암호화에 대해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="aa2b4-182">hello 수행 하는 마법사 hello 동작을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="aa2b4-183">CMK를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-183">Created a CMK.</span></span>
* <span data-ttu-id="aa2b4-184">CEK를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-184">Created a CEK.</span></span>
* <span data-ttu-id="aa2b4-185">구성 된 hello 암호화에 대 한 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="aa2b4-186">프로그램 **환자** 테이블에 현재 데이터가 없는 하지만 모든 열의 기존 데이터를 선택 하는 hello 이제 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="aa2b4-187">SSMS의 hello 키의 hello 생성 너무 이동 하 여 확인할 수 있습니다**클리닉** > **보안** > **상시 암호화 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="aa2b4-188">이제 자동으로 생성 하는 마법사를 hello hello 새 키를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="aa2b4-189">Hello 암호화 된 데이터를 사용 하는 클라이언트 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="aa2b4-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="aa2b4-190">상시 암호화를 설정 했으므로 수행 하는 응용 프로그램을 빌드할 수 있습니다 *삽입* 및 *선택* hello에 암호화 된 열입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="aa2b4-191">toosuccessfully hello 샘플 응용 프로그램 실행을 실행 해야 hello에 같은 컴퓨터 hello 상시 암호화 마법사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="aa2b4-192">다른 컴퓨터에서 toorun hello 응용 프로그램을 항상 암호화 인증서 toohello 실행 하는 컴퓨터 hello 클라이언트 응용 프로그램을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="aa2b4-193">응용 프로그램 사용 해야 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 상시 암호화 열이 있는 일반 텍스트 데이터 toohello 서버를 전달 하는 경우 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="aa2b4-194">SqlParameter 개체를 사용하지 않고 리터럴 값을 전달하면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="aa2b4-195">Visual Studio를 열고 새 C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="aa2b4-196">프로젝트가 너무 설정 되어 있는지 확인**.NET Framework 4.6** 이상.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="aa2b4-197">이름 hello 프로젝트 **AlwaysEncryptedConsoleApp** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="aa2b4-199">항상 암호화 하 여 연결 문자열 tooenable 수정</span><span class="sxs-lookup"><span data-stu-id="aa2b4-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="aa2b4-200">이 섹션에서는 데이터베이스 연결 문자열에서 tooenable 항상 암호화 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="aa2b4-201">"항상 암호화 샘플 콘솔 응용 프로그램." hello 다음 섹션에서 방금 만든 hello 콘솔 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="aa2b4-202">항상 암호화 tooenable, 해야 tooadd hello **열 암호화 설정** 키워드 tooyour 연결 문자열을 너무 설정**Enabled**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="aa2b4-203">Hello 연결 문자열에서 직접 설정할 수 있습니다 또는 사용 하 여 설정할 수 있습니다는 [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="aa2b4-204">hello 예제 응용 프로그램 hello에 다음 섹션에서는 어떻게 toouse **SqlConnectionStringBuilder**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="aa2b4-205">이 hello 작업만 실행 하는 클라이언트 응용 프로그램 특정 tooAlways 암호화에에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="aa2b4-206">외부에서 연결 문자열을 저장 하는 기존 응용 프로그램의 경우 (즉, 구성 파일에), 모든 코드를 변경 하지 않고 항상 암호화 하는 수 tooenable 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="aa2b4-207">Hello 연결 문자열에서 상시 암호화를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="aa2b4-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="aa2b4-208">Hello tooyour 연결 문자열 키워드에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="aa2b4-209">SqlConnectionStringBuilder로 상시 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="aa2b4-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="aa2b4-210">hello 다음 코드를 보여 줍니다 방법을 설정 하 여 상시 암호화는 tooenable hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) 너무[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="aa2b4-211">상시 암호화 샘플 콘솔 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="aa2b4-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="aa2b4-212">이 샘플에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="aa2b4-213">항상 암호화 하 여 연결 문자열 tooenable를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="aa2b4-214">Hello 암호화 된 열에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="aa2b4-215">암호화된 열에서 특정 값에 필터링하여 레코드 선택.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="aa2b4-216">Hello 내용 바꾸기 **Program.cs** 코드 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="aa2b4-217">유효한 연결 문자열 hello Azure 포털에서에서 hello Main 메서드에 바로 위의 hello 줄에서 전역 connectionString 변수 hello에 대 한 연결 문자열을 hello를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="aa2b4-218">이 hello 작업만 toomake toothis 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="aa2b4-219">작업에서 항상 암호화 hello 앱 toosee를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-219">Run hello app toosee Always Encrypted in action.</span></span>

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
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

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
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
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

            Console.WriteLine("Press Enter tooexit...");
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
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
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


        // This method simply deletes all records in hello Patients table tooreset our demo.
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


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="aa2b4-220">Hello 데이터의 암호화를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="aa2b4-221">Hello를 쿼리하여 서버 hello에 hello 실제 데이터의 암호화를 신속 하 게 확인할 수 있습니다 **환자** SSMS 사용 하 여 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="aa2b4-222">(사용 하 여 현재 연결에 hello 열 암호화 설정 해제 되어 있는 아직.)</span><span class="sxs-lookup"><span data-stu-id="aa2b4-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="aa2b4-223">Hello hello Clinic 데이터베이스에서 다음 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="aa2b4-224">Hello 암호화 열 일반 텍스트 데이터가 포함 되지 않은 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="aa2b4-226">toouse SSMS tooaccess hello 일반 텍스트 데이터를 hello를 추가할 수 있습니다 **열 암호화 설정 = 사용** toohello 연결 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="aa2b4-227">SSMS에서 **개체 탐색기**에 있는 서버를 마우스 오른쪽 단추로 클릭하고 **연결 끊기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="aa2b4-228">클릭 **연결** > **데이터베이스 엔진** tooopen hello **tooServer 연결** 창과 클릭 **옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="aa2b4-229">**추가 연결 매개 변수**를 클릭하고 **열 암호화 설정=활성화**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="aa2b4-231">실행 hello hello에 대 한 쿼리 다음 **Clinic** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="aa2b4-232">이제 hello 암호화 된 열에 hello 일반 텍스트 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="aa2b4-234">SSMS (클라이언트)와 다른 컴퓨터에서 연결 하는 경우 액세스 toohello 암호화 키 체계가 없습니다 및 수 toodecrypt hello 데이터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="aa2b4-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa2b4-235">Next steps</span></span>
<span data-ttu-id="aa2b4-236">상시 암호화를 사용 하는 데이터베이스를 만든 후에 toodo hello 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="aa2b4-237">다른 컴퓨터에서 이 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-237">Run this sample from a different computer.</span></span> <span data-ttu-id="aa2b4-238">하므로 체계가 없습니다 toohello 일반 텍스트 데이터에 액세스 하 고 성공적으로 실행 되지 않습니다 액세스 toohello 암호화 키를 없을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa2b4-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="aa2b4-239">[키 회전 및 정리](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa2b4-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="aa2b4-240">[상시 암호화로 이미 암호화된 데이터 마이그레이션](https://msdn.microsoft.com/library/mt621539.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa2b4-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="aa2b4-241">[항상 암호화 인증서 tooother 클라이언트 컴퓨터를 배포](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (hello "사용 가능한 tooApplications 인증서 및 사용자 만들기" 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="aa2b4-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="aa2b4-242">관련 정보</span><span class="sxs-lookup"><span data-stu-id="aa2b4-242">Related information</span></span>
* [<span data-ttu-id="aa2b4-243">상시 암호화(클라이언트 개발)</span><span class="sxs-lookup"><span data-stu-id="aa2b4-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="aa2b4-244">투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="aa2b4-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="aa2b4-245">SQL Server 암호화</span><span class="sxs-lookup"><span data-stu-id="aa2b4-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="aa2b4-246">상시 암호화 마법사</span><span class="sxs-lookup"><span data-stu-id="aa2b4-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="aa2b4-247">상시 암호화 블로그</span><span class="sxs-lookup"><span data-stu-id="aa2b4-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

