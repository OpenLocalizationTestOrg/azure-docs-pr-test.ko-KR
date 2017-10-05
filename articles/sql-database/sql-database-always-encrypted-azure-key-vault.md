---
title: "상시 암호화: SQL Database - Azure Key Vault | Microsoft Docs"
description: "이 문서에서는 SQL Server Management Studio의 상시 암호화 마법사를 사용하여 데이터 암호화로 SQL Database의 중요한 데이터를 보호하는 방법을 보여 줍니다. 또한 Azure 주요 자격 증명 모음에 각 암호화 키를 저장하는 방법을 보여 주는 지침도 포함되어 있습니다."
keywords: "데이터 암호화, 암호화 키, 클라우드 암호화"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 61bfd420425b4740f6d4ebc01a403a88ff351382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="1e088-105">상시 암호화: SQL 데이터베이스의 중요한 데이터 보호 및 Azure 주요 자격 증명 모음에 암호화 키 저장</span><span class="sxs-lookup"><span data-stu-id="1e088-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="1e088-106">이 문서에서는 [SSMS(SQL Server Management Studio)](https://msdn.microsoft.com/library/hh213248.aspx)의 [상시 암호화 마법사](https://msdn.microsoft.com/library/mt459280.aspx)를 사용하여 데이터 암호화로 SQL Database의 중요한 데이터를 보호하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-106">This article shows you how to secure sensitive data in a SQL database with data encryption using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="1e088-107">또한 Azure 주요 자격 증명 모음에 각 암호화 키를 저장하는 방법을 보여 주는 지침도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-107">It also includes instructions that will show you how to store each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="1e088-108">상시 암호화는 클라이언트와 서버 사이의 이동 중에, 그리고 데이터를 사용 중일 때 서버에서 중요한 미사용 데이터를 보호하는 Azure SQL 데이터베이스 및 SQL Server 내의 새로운 데이터 암호 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use.</span></span> <span data-ttu-id="1e088-109">상시 암호화는 중요한 데이터가 데이터베이스 시스템에서 일반 텍스트로 나타나지 않도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-109">Always Encrypted ensures that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="1e088-110">데이터 암호화를 구성한 후 키에 액세스할 수 있는 클라이언트 응용 프로그램 또는 앱 서버만 일반 텍스트 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-110">After you configure data encryption, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="1e088-111">자세한 내용은 [상시 암호화(데이터베이스 엔진)](https://msdn.microsoft.com/library/mt163865.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e088-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="1e088-112">상시 암호화를 사용하는 데이터베이스를 구성한 후에 Visual Studio로 C#에서 클라이언트 응용 프로그램을 만들어 암호화된 데이터로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-112">After you configure the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="1e088-113">이 문서의 단계를 수행하고 Azure SQL 데이터베이스에 대해 상시 암호화를 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-113">Follow the steps in this article and learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="1e088-114">이 문서에서는 다음 작업을 수행하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-114">In this article you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="1e088-115">SSMS에서 상시 암호화 마법사를 사용하여 [상시 암호화 키](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-115">Use the Always Encrypted wizard in SSMS to create [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="1e088-116">[CMK(열 마스터 키)](https://msdn.microsoft.com/library/mt146393.aspx)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="1e088-117">[CEK(열 암호화 키)](https://msdn.microsoft.com/library/mt146372.aspx)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="1e088-118">데이터베이스 테이블을 만들고 열을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="1e088-119">암호화된 열에서 데이터를 삽입하고 선택하며 표시한 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-119">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e088-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1e088-120">Prerequisites</span></span>
<span data-ttu-id="1e088-121">이 자습서에는 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="1e088-122">Azure 계정 및 구독</span><span class="sxs-lookup"><span data-stu-id="1e088-122">An Azure account and subscription.</span></span> <span data-ttu-id="1e088-123">없는 경우 지금 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="1e088-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1e088-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 버전 13.0.700.242 이상.</span><span class="sxs-lookup"><span data-stu-id="1e088-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="1e088-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) 이상(클라이언트 컴퓨터에서).</span><span class="sxs-lookup"><span data-stu-id="1e088-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="1e088-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e088-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="1e088-127">[Azure PowerShell](/powershell/azure/overview) 버전 1.0 이상.</span><span class="sxs-lookup"><span data-stu-id="1e088-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="1e088-128">실행 중인 PowerShell 버전을 보려면 **(Get-Module azure -ListAvailable).Version** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-128">Type **(Get-Module azure -ListAvailable).Version** to see what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-to-access-the-sql-database-service"></a><span data-ttu-id="1e088-129">클라이언트 응용 프로그램에서 SQL 데이터베이스 서비스에 액세스하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1e088-129">Enable your client application to access the SQL Database service</span></span>
<span data-ttu-id="1e088-130">필요한 인증을 설정하고 다음 코드에서 응용 프로그램을 인증하는 데 필요한 *ClientId* 및 *Secret*를 가져와 클라이언트 응용 프로그램에서 SQL Database 서비스에 액세스하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-130">You must enable your client application to access the SQL Database service by setting up the required authentication and acquiring the *ClientId* and *Secret* that you will need to authenticate your application in the following code.</span></span>

1. <span data-ttu-id="1e088-131">[Azure 클래식 포털](http://manage.windowsazure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-131">Open the [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1e088-132">**Active Directory** 를 선택하고 응용 프로그램에서 사용할 Active Directory 인스턴스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-132">Select **Active Directory** and click the Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="1e088-133">**응용 프로그램**을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="1e088-134">응용 프로그램 이름(예: *myClientApp*)을 입력하고 **웹 응용 프로그램**을 선택한 후 화살표를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click the arrow to continue.</span></span>
5. <span data-ttu-id="1e088-135">**로그온 URL** 및 **앱 ID URI**의 경우 유효한 URL(예: *http://myClientApp*)을 입력하고 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-135">For the **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="1e088-136">**구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="1e088-137">**클라이언트 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="1e088-138">(코드에서 나중에 이 값이 필요합니다.)</span><span class="sxs-lookup"><span data-stu-id="1e088-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="1e088-139">**키** 섹션에서 **기간 선택** 드롭다운 목록에서 **1년**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-139">In the **keys** section, select **1 year** from the  **Select duration** drop-down list.</span></span> <span data-ttu-id="1e088-140">(13단계에서 저장한 후 키를 복사합니다.)</span><span class="sxs-lookup"><span data-stu-id="1e088-140">(You will copy the key after you save in step 13.)</span></span>
9. <span data-ttu-id="1e088-141">아래로 스크롤하여 **응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="1e088-142">**표시**를 **Microsoft 앱**으로 설정하고 **Microsoft Azure Service Management API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-142">Leave **SHOW** set to **Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="1e088-143">계속하려면 확인 표시를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-143">Click the checkmark to continue.</span></span>
11. <span data-ttu-id="1e088-144">**위임된 권한** 드롭다운 목록에서 **Azure 서비스 관리 액세스...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-144">Select **Access Azure Service Management...** from the **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="1e088-145">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="1e088-146">저장이 끝나면 **키** 섹션에서 키 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-146">After the save finishes, copy the key value in the **keys** section.</span></span> <span data-ttu-id="1e088-147">(코드에서 나중에 이 값이 필요합니다.)</span><span class="sxs-lookup"><span data-stu-id="1e088-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-to-store-your-keys"></a><span data-ttu-id="1e088-148">키를 저장할 주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="1e088-148">Create a key vault to store your keys</span></span>
<span data-ttu-id="1e088-149">클라이언트 앱이 구성되고 클라이언트 ID가 있으므로 이제 주요 자격 증명 모음을 만들고 사용자와 사용자 응용 프로그램에서 이 자격 증명 모음의 암호에 액세스하도록 허용하는 액세스 정책을 구성해야 합니다(항상 암호화된 키).</span><span class="sxs-lookup"><span data-stu-id="1e088-149">Now that your client app is configured and you have your client ID, it's time to create a key vault and configure its access policy so you and your application can access the vault's secrets (the Always Encrypted keys).</span></span> <span data-ttu-id="1e088-150">새 열 마스터 키를 만들고 SQL Server Management Studio에서 암호화를 설정하기 위해서는 *create*, *get*, *list*, *sign*, *verify*, *wrapKey* 및 *unwrapKey* 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-150">The *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="1e088-151">다음 스크립트를 실행하여 주요 자격 증명 모음을 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-151">You can quickly create a key vault by running the following script.</span></span> <span data-ttu-id="1e088-152">이러한 cmdlet에 대한 자세한 설명 및 주요 자격 증명 모음을 만들고 구성하는 방법은 [Azure 주요 자격 증명 모음 시작](../key-vault/key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e088-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="1e088-153">빈 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="1e088-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="1e088-154">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-154">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1e088-155">**새로 만들기** > **데이터 + 저장소** > **SQL Database**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-155">Go to **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="1e088-156">새 서버 또는 기존 서버에 **클리닉**이라는 **빈** 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="1e088-157">Azure Portal에서 데이터베이스를 만드는 방법에 대한 자세한 지침은 [첫 Azure SQL Database](sql-database-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e088-157">For detailed directions about how to create a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![빈 데이터베이스 만들기](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="1e088-159">자습서의 뒷부분에서 연결 문자열이 필요하므로 데이터베이스를 만든 다음 새 Clinic 데이터베이스로 이동한 후 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-159">You will need the connection string later in the tutorial, so after you create the database, browse to the new  Clinic database and copy the connection string.</span></span> <span data-ttu-id="1e088-160">언제든지 연결 문자열을 가져올 수 있지만 Azure 포털에서 복사하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-160">You can get the connection string at any time, but it's easy to copy it in the Azure portal.</span></span>

1. <span data-ttu-id="1e088-161">**SQL Database** > **Clinic** > **데이터베이스 연결 문자열 표시**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-161">Go to **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="1e088-162">**ADO.NET**에 대한 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-162">Copy the connection string for **ADO.NET**.</span></span>
   
    ![연결 문자열 복사](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="1e088-164">SSMS로 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="1e088-164">Connect to the database with SSMS</span></span>
<span data-ttu-id="1e088-165">SSMS를 열고 클리닉 데이터베이스가 있는 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-165">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="1e088-166">SSMS를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-166">Open SSMS.</span></span> <span data-ttu-id="1e088-167">(열리지 않은 경우 **연결** > **데이터베이스 엔진**으로 이동하여 **서버에 연결** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-167">(Go to **Connect** > **Database Engine** to open the **Connect to Server** window if it isn't open.)</span></span>
2. <span data-ttu-id="1e088-168">서버 이름 및 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-168">Enter your server name and credentials.</span></span> <span data-ttu-id="1e088-169">앞에서 복사한 SQL 데이터베이스 블레이드 및 연결 문자열에 서버 이름을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-169">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="1e088-170">*database.windows.net*을 포함하는 전체 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-170">Type the complete server name, including *database.windows.net*.</span></span>
   
    ![연결 문자열 복사](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="1e088-172">**새 방화벽 규칙** 창이 열리면 Azure에 로그인하고 SSMS가 새 방화벽 규칙을 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-172">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="1e088-173">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="1e088-173">Create a table</span></span>
<span data-ttu-id="1e088-174">이 섹션에서는 환자 데이터를 저장할 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-174">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="1e088-175">처음에는 암호화되어 있지 않지만, 다음 섹션에서 암호화를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-175">It's not initially encrypted--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="1e088-176">**데이터베이스**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="1e088-177">**Clinic** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-177">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="1e088-178">새 쿼리 창에 다음 Transact-SQL(T-SQL)을 붙여넣고 **실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-178">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="1e088-179">열 암호화(상시 암호화 구성)</span><span class="sxs-lookup"><span data-stu-id="1e088-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="1e088-180">SSMS는 쉽게 열 마스터 키, 열 암호화 키 및 암호화된 열을 설정하여 상시 암호화를 쉽게 구성하는 마법사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up the column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="1e088-181">**데이터베이스** > **빈** > **테이블**를 사용하여 데이터베이스 암호화로 SQL 데이터베이스의 중요한 데이터를 보호하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="1e088-182">**Patients** 테이블을 마우스 오른쪽 단추로 클릭하고 **열 암호화**를 선택하여 상시 암호화 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-182">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![열 암호화](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="1e088-184">상시 암호화 마법사에는 **열 선택**, **마스터 키 구성**, **유효성 검사** 및 **요약** 섹션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-184">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="1e088-185">열 선택</span><span class="sxs-lookup"><span data-stu-id="1e088-185">Column Selection</span></span>
<span data-ttu-id="1e088-186">**소개** 페이지에서 **다음**을 클릭하여 **열 선택** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-186">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="1e088-187">이 페이지에서 암호화하려는 열, [암호화 형식 및 사용할 CEK(열 암호화 키)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-187">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="1e088-188">각 환자에 대해 **SSN** 및 **BirthDate** 정보를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="1e088-189">SSN 열은 같음 조회, 조인 및 그룹화를 지원하는 결정적 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-189">The SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="1e088-190">BirthDate 열은 작업을 지원하지 않는 임의의 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-190">The BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="1e088-191">SSN 열에 대한 **암호화 형식**을 **결정적**으로 설정하고 BirthDate 열을 **무작위**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-191">Set the **Encryption Type** for the SSN column to **Deterministic** and the BirthDate column to **Randomized**.</span></span> <span data-ttu-id="1e088-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-192">Click **Next**.</span></span>

![열 암호화](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="1e088-194">마스터 키 구성</span><span class="sxs-lookup"><span data-stu-id="1e088-194">Master Key Configuration</span></span>
<span data-ttu-id="1e088-195">**마스터 키 구성** 페이지는 CMK를 설치하고 CMK가 저장될 키 저장소 공급자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-195">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="1e088-196">현재 Windows 인증서 저장소, Azure 주요 자격 증명 모음 또는 하드웨어 보안 모듈(HSM)에 CMK를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-196">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="1e088-197">이 자습서에서는 Azure 주요 자격 증명 모음에 키를 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-197">This tutorial shows how to store your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="1e088-198">**Azure 주요 자격 증명 모음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="1e088-199">드롭다운 목록에서 원하는 주요 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-199">Select the desired key vault from the drop-down list.</span></span>
3. <span data-ttu-id="1e088-200">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-200">Click **Next**.</span></span>

![마스터 키 구성](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="1e088-202">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1e088-202">Validation</span></span>
<span data-ttu-id="1e088-203">이제 열을 암호화하거나 나중에 실행할 PowerShell 스크립트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-203">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="1e088-204">이 자습서의 경우 **지금 전체 과정 진행**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-204">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="1e088-205">요약</span><span class="sxs-lookup"><span data-stu-id="1e088-205">Summary</span></span>
<span data-ttu-id="1e088-206">설정이 모두 정확한 것을 확인하고 **마침** 을 클릭하여 상시 암호화에 대한 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-206">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![요약](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="1e088-208">마법사의 작업 확인</span><span class="sxs-lookup"><span data-stu-id="1e088-208">Verify the wizard's actions</span></span>
<span data-ttu-id="1e088-209">마법사가 완료된 후에 데이터베이스는 상시 암호화에 대해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-209">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="1e088-210">마법사는 다음 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-210">The wizard performed the following actions:</span></span>

* <span data-ttu-id="1e088-211">열 마스터 키가 만들어지고 Azure 주요 자격 증명 모음에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="1e088-212">열 암호화 키가 만들어지고 Azure 주요 자격 증명 모음에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="1e088-213">암호화에 선택한 열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-213">Configured the selected columns for encryption.</span></span> <span data-ttu-id="1e088-214">Patients 테이블에는 현재 데이터가 없지만 이제 선택된 열의 기존 데이터가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-214">The Patients table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="1e088-215">**Clinic** > **보안** > **상시 암호화 키**를 확장하여 SSMS에서 키 만들기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-215">You can verify the creation of the keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="1e088-216">암호화된 데이터로 작동하는 클라이언트 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1e088-216">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="1e088-217">상시 암호화가 설정되었으므로 암호화된 열에서 *삽입* 및 *선택*을 수행하는 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1e088-218">상시 암호화 열이 있는 서버에 일반 텍스트 데이터를 전달하는 경우 응용 프로그램은 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 개체를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="1e088-219">SqlParameter 개체를 사용하지 않고 리터럴 값을 전달하면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="1e088-220">Visual Studio를 열고 새 C# **콘솔 응용 프로그램**(Visual Studio 2015 이전) 또는 **콘솔 앱(.NET Framework)**(Visual Studio 2017 이상)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="1e088-221">프로젝트가 **.NET Framework 4.6** 이상으로 설정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-221">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="1e088-222">프로젝트 이름을 **AlwaysEncryptedConsoleAKVApp**으로 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-222">Name the project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="1e088-223">**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**로 이동하여 다음 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-223">Install the following NuGet packages by going to **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="1e088-224">패키지 관리자 콘솔에서 코드의 다음 두 줄을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-224">Run these two lines of code in the Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="1e088-225">연결 문자열을 수정하여 상시 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="1e088-225">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="1e088-226">이 섹션에는 데이터베이스 연결 문자열에서 상시 암호화를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-226">This section  explains how to enable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="1e088-227">상시 암호화를 사용하려면 **열 암호화 설정** 키워드를 연결 문자열에 추가하고 **사용함**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-227">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="1e088-228">이 연결 문자열에서 직접 설정하거나 [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx)를 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-228">You can set this directly in the connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="1e088-229">다음 섹션에서 응용 프로그램 예제는 **SqlConnectionStringBuilder**를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-229">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="1e088-230">연결 문자열에서 상시 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="1e088-230">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="1e088-231">연결 문자열에 다음 키워드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-231">Add the following keyword to your connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="1e088-232">SqlConnectionStringBuilder로 상시 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="1e088-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="1e088-233">다음 코드는 [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx)을 [사용함](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)으로 설정하여 상시 암호화를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-233">The following code shows how to enable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-the-azure-key-vault-provider"></a><span data-ttu-id="1e088-234">Azure 주요 자격 증명 모음 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="1e088-234">Register the Azure Key Vault provider</span></span>
<span data-ttu-id="1e088-235">다음 코드는 ADO.NET 드라이버로 Azure 주요 자격 증명 모음 공급자를 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-235">The following code shows how to register the Azure Key Vault provider with the ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="1e088-236">상시 암호화 샘플 콘솔 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1e088-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="1e088-237">이 샘플에서는 다음 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="1e088-238">연결 문자열을 수정하여 상시 암호화 사용.</span><span class="sxs-lookup"><span data-stu-id="1e088-238">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="1e088-239">Azure 주요 자격 증명 모음을 응용 프로그램의 키 저장소 공급자로 등록</span><span class="sxs-lookup"><span data-stu-id="1e088-239">Register Azure Key Vault as the application's key store provider.</span></span>  
* <span data-ttu-id="1e088-240">암호화된 열에 데이터 삽입.</span><span class="sxs-lookup"><span data-stu-id="1e088-240">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="1e088-241">암호화된 열에서 특정 값에 필터링하여 레코드 선택.</span><span class="sxs-lookup"><span data-stu-id="1e088-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="1e088-242">**Program.cs** 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-242">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="1e088-243">Main 메서드 바로 위의 줄에서 전역 connectionString 변수에 대한 연결 문자열을 Azure 포털에서 유효한 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-243">Replace the connection string for the global connectionString variable in the line that directly precedes the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="1e088-244">이 코드에 대한 유일한 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-244">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="1e088-245">작업에서 상시 암호화를 확인하려면 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-245">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"<connection string from the portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed to obtain the access token");
            return result.AccessToken;
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



## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="1e088-246">데이터가 암호화되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-246">Verify that the data is encrypted</span></span>
<span data-ttu-id="1e088-247">SSMS로 Patients 데이터를 쿼리하여 서버의 실제 데이터가 암호화되었는지 빠르게 확인할 수 있습니다( **열 암호화 설정** 이 아직 사용되지 않는 현재 연결을 사용).</span><span class="sxs-lookup"><span data-stu-id="1e088-247">You can quickly check that the actual data on the server is encrypted by querying the Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="1e088-248">Clinic 데이터베이스에 대해 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-248">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="1e088-249">암호화된 열에 일반 텍스트 데이터가 포함되지 않은 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-249">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="1e088-251">SSMS를 사용하여 일반 텍스트 데이터에 액세스하려면 *열 암호화 설정=활성화* 매개 변수를 연결에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-251">To use SSMS to access the plaintext data, you can add the *Column Encryption Setting=enabled* parameter to the connection.</span></span>

1. <span data-ttu-id="1e088-252">SSMS에서 **개체 탐색기**에 있는 서버를 마우스 오른쪽 단추로 클릭하고 **연결 끊기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="1e088-253">**연결** > **데이터베이스 엔진**을 클릭하여 **서버에 연결** 창을 열고 **옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-253">Click **Connect** > **Database Engine** to open the **Connect to Server** window and click **Options**.</span></span>
3. <span data-ttu-id="1e088-254">**추가 연결 매개 변수**를 클릭하고 **열 암호화 설정=활성화**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="1e088-256">Clinic 데이터베이스에 대해 다음 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-256">Run the following query on the Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="1e088-257">이제 암호화된 열에서 일반 텍스트 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-257">You can now see the plaintext data in the encrypted columns.</span></span>

    ![새 콘솔 응용 프로그램](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="1e088-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e088-259">Next steps</span></span>
<span data-ttu-id="1e088-260">상시 암호화를 사용하는 데이터베이스를 만든 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e088-260">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="1e088-261">[키 회전 및 정리](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e088-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="1e088-262">[상시 암호화로 이미 암호화된 데이터 마이그레이션](https://msdn.microsoft.com/library/mt621539.aspx)</span><span class="sxs-lookup"><span data-stu-id="1e088-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="1e088-263">관련 정보</span><span class="sxs-lookup"><span data-stu-id="1e088-263">Related information</span></span>
* [<span data-ttu-id="1e088-264">상시 암호화(클라이언트 개발)</span><span class="sxs-lookup"><span data-stu-id="1e088-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="1e088-265">투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="1e088-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="1e088-266">SQL Server 암호화</span><span class="sxs-lookup"><span data-stu-id="1e088-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="1e088-267">상시 암호화 마법사</span><span class="sxs-lookup"><span data-stu-id="1e088-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="1e088-268">상시 암호화 블로그</span><span class="sxs-lookup"><span data-stu-id="1e088-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

