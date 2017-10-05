---
title: "분할/병합 서비스 배포 | Microsoft Docs"
description: "탄력적 데이터베이스 도구를 사용하는 분할 및 병합"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6e2fea882c248fa095a9d450ed54a7b4e64b45e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="ad4ca-103">분할/병합 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="ad4ca-103">Deploy a split-merge service</span></span>
<span data-ttu-id="ad4ca-104">분할-병합 도구를 사용하면 분할된 데이터베이스 간에 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="ad4ca-105">[확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="ad4ca-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="ad4ca-106">분할-병합 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="ad4ca-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="ad4ca-107">[NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)에서 최신 NuGet 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="ad4ca-108">명령 프롬프트를 열고 nuget.exe를 다운로드한 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="ad4ca-109">다운로드에는 PowerShell 명령이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-109">The download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="ad4ca-110">아래 명령을 사용하여 최신 분할/병합 패키지를 현재 디렉터리에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="ad4ca-111">파일은 **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x**라는 디렉터리에 저장됩니다. 여기서 *x.x.xxx.x*는 버전 번호를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="ad4ca-112">**content\splitmerge\service** 하위 디렉터리에서 분할/병합 서비스 파일을 찾고 **content\splitmerge\powershell** 하위 디렉터리에서 분할/병합 PowerShell 스크립트 및 필요한 클라이언트 .dll을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client .dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad4ca-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ad4ca-113">Prerequisites</span></span>
1. <span data-ttu-id="ad4ca-114">분할/병합 상태 데이터베이스로 사용할 Azure SQL DB 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="ad4ca-115">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad4ca-116">새 **SQL 데이터베이스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="ad4ca-117">데이터베이스에 이름을 지정하고 새 관리자 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="ad4ca-118">나중에 사용할 수 있도록 이름과 암호를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="ad4ca-119">Azure SQL DB 서버에서 Azure 서비스의 연결을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="ad4ca-120">포털의 **방화벽 설정**에서 **Azure 서비스에 대한 액세스 허용** 설정이 **On**으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-120">In the portal, in the **Firewall Settings**, ensure that the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="ad4ca-121">"저장" 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-121">Click the "save" icon.</span></span>
   
   ![허용된 서비스][1]
3. <span data-ttu-id="ad4ca-123">진단 출력에 사용할 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="ad4ca-124">Azure 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-124">Go to the Azure Portal.</span></span> <span data-ttu-id="ad4ca-125">왼쪽 막대에서 **새로 만들기**, **데이터 + 저장소**, **저장소**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-125">In the left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="ad4ca-126">분할/병합 서비스를 포함할 Azure 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="ad4ca-127">Azure 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-127">Go to the Azure Portal.</span></span> <span data-ttu-id="ad4ca-128">왼쪽 막대에서 **새로 만들기**, **계산**, **클라우드 서비스**, **만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-128">In the left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="ad4ca-129">분할/병합 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="ad4ca-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="ad4ca-130">분할/병합 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="ad4ca-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="ad4ca-131">분할/병합 어셈블리를 다운로드한 폴더에서 **SplitMergeService.cspkg**와 함께 제공된 **ServiceConfiguration.Template.cscfg** 파일의 복사본을 만들고 이름을 **ServiceConfiguration.cscfg**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-131">In the folder where you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="ad4ca-132">Visual Studio와 같은 텍스트 편집기에서 인증서 지문 형식과 같은 입력의 유효성을 검사하는 **ServiceConfiguration.cscfg** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="ad4ca-133">새 데이터베이스를 만들거나 분할/병합 작업에 대한 상태 데이터베이스로 사용할 기존 데이터베이스를 선택하고 해당 데이터베이스의 연결 문자열을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-133">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="ad4ca-134">지금은 상태 데이터베이스에서 라틴어 데이터 정렬(SQL\_Latin1\_General\_CP1\_CI\_AS)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-134">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="ad4ca-135">자세한 내용은 [Windows 데이터 정렬 이름(TRANSACT-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="ad4ca-136">Azure SQL DB를 사용할 경우 연결 문자열의 형식은 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-136">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="ad4ca-137">ElasticScaleMetadata 설정의 **SplitMergeWeb** 및 **SplitMergeWorker** 역할 섹션에서 cscfg 파일에 이 연결 문자열을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-137">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="ad4ca-138">**SplitMergeWorker** 역할의 경우, **WorkerRoleSynchronizationStorageAccountConnectionString** 설정에 대해 Azure 저장소에 유효한 연결 문자열을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-138">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="ad4ca-139">보안 구성</span><span class="sxs-lookup"><span data-stu-id="ad4ca-139">Configure security</span></span>
<span data-ttu-id="ad4ca-140">서비스의 보안을 구성하는 자세한 지침은 [분할-병합 보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-140">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="ad4ca-141">이 자습서에 대한 간단한 테스트를 배포하기 위해 서비스를 작동하고 실행하는 데 필요한 최소 구성 단계가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-141">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="ad4ca-142">이러한 단계에서는 단계를 실행하는 데 사용하는 컴퓨터/계정 하나만 서비스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-142">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ad4ca-143">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="ad4ca-143">Create a self-signed certificate</span></span>
<span data-ttu-id="ad4ca-144">새 디렉터리를 만들고 이 디렉터리에서 [Visual Studio용 개발자 명령 프롬프트](http://msdn.microsoft.com/library/ms229859.aspx) 창을 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-144">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="ad4ca-145">개인 키를 보호 하기 위해 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-145">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="ad4ca-146">강력한 암호를 입력하고 이를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="ad4ca-147">이후에 사용할 암호를 한 번 더 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-147">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="ad4ca-148">마지막에 **예** 를 클릭하여 신뢰할 수 있는 인증 기관 루트 저장소로 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-148">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="ad4ca-149">PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="ad4ca-149">Create a PFX file</span></span>
<span data-ttu-id="ad4ca-150">makecert가 실행된 동일한 창에서 다음 명령을 실행하고, 인증서를 만드는 데 사용한 동일한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-150">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="ad4ca-151">개인 저장소로 클라이언트 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="ad4ca-151">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="ad4ca-152">Windows 탐색기에서 **MyCert.pfx**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="ad4ca-153">**인증서 가져오기 마법사**에서 **현재 사용자**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-153">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="ad4ca-154">파일 경로를 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-154">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="ad4ca-155">암호를 입력하고 **확장 속성 모두 포함**을 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-155">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="ad4ca-156">**인증서 저장소를 자동으로 선택[…]**을 선택된 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-156">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="ad4ca-157">**마침**, **확인**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="ad4ca-158">클라우드 서비스에 PFX 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ad4ca-158">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="ad4ca-159">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-159">Go to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ad4ca-160">**클라우드 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="ad4ca-161">분할/병합 서비스에 대해 위에서 만든 클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-161">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="ad4ca-162">최상위 메뉴에서 **인증서** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-162">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="ad4ca-163">아래쪽 메뉴 모음에서 **업로드** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-163">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="ad4ca-164">PFX 파일을 선택하고 위와 동일한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-164">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="ad4ca-165">완료되면 목록의 새 항목에서 인증서 지문을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-165">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="ad4ca-166">서비스 구성 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="ad4ca-166">Update the service configuration file</span></span>
<span data-ttu-id="ad4ca-167">이러한 설정의 지문/값 특성에 위의 복사한 인증서 지문을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-167">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="ad4ca-168">작업자 역할의 경우:</span><span class="sxs-lookup"><span data-stu-id="ad4ca-168">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="ad4ca-169">웹 역할의 경우:</span><span class="sxs-lookup"><span data-stu-id="ad4ca-169">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="ad4ca-170">프로덕션 배포의 경우 CA, 암호화, 서버 인증서 및 클라이언트 인증서에 개별 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-170">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="ad4ca-171">이와 관련된 자세한 지침은 [보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="ad4ca-172">서비스 배포</span><span class="sxs-lookup"><span data-stu-id="ad4ca-172">Deploy your service</span></span>
1. <span data-ttu-id="ad4ca-173">[Azure 포털](https://manage.windowsazure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-173">Go to the [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ad4ca-174">왼쪽에서 **클라우드 서비스** 탭을 클릭하고 앞에서 만든 클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-174">Click the **Cloud Services** tab on the left, and select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="ad4ca-175">**대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="ad4ca-176">스테이징 환경을 선택한 다음 **새 스테이징 배포 업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-176">Choose the staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![스테이징][3]
5. <span data-ttu-id="ad4ca-178">대화 상자에서 배포 레이블을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-178">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="ad4ca-179">'패키지'와 '구성' 모두에 대해, '로컬에서'를 클릭하고 **SplitMergeService.cspkg** 파일 및 이전에 구성한 .cscfg 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-179">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="ad4ca-180">**단일 인스턴스가 포함된 역할이 하나 이상 있는 경우에도 배포** 확인란이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-180">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="ad4ca-181">오른쪽 아래의 눈금 단추를 눌러 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-181">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="ad4ca-182">배포를 완료하려면 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-182">Expect it to take a few minutes to complete.</span></span>

   ![업로드][4]

## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="ad4ca-184">배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ad4ca-184">Troubleshoot the deployment</span></span>
<span data-ttu-id="ad4ca-185">웹 역할을 온라인 상태로 전환하지 못하면 보안 구성에 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-185">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="ad4ca-186">위에서 설명한 대로 SSL이 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-186">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="ad4ca-187">작업자 역할을 온라인 상태로 전환하지 못했지만 웹 역할은 성공하면 대개 이전에 만든 상태 데이터베이스에 대한 연결 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-187">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="ad4ca-188">.cscfg의 연결 문자열이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-188">Make sure that the connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="ad4ca-189">서버 및 데이터베이스가 존재하며, 사용자 ID 및 암호가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-189">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="ad4ca-190">Azure SQL DB의 경우 연결 문자열은 다음 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-190">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="ad4ca-191">서버 이름이 **https://**로 시작하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-191">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="ad4ca-192">Azure SQL DB 서버에서 Azure 서비스의 연결을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-192">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="ad4ca-193">이렇게 하려면 https://manage.windowsazure.com을 열고 왼쪽에서 “SQL 데이터베이스”를 클릭하고 위쪽에서 “서버”를 클릭하고 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-193">To do this, open https://manage.windowsazure.com, click “SQL Databases” on the left, click “Servers” at the top, and select your server.</span></span> <span data-ttu-id="ad4ca-194">위쪽에서 **구성**을 클릭하고 **Azure 서비스** 설정이 “예”로 지정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-194">Click **Configure** at the top and ensure that the **Azure Services** setting is set to “Yes”.</span></span> <span data-ttu-id="ad4ca-195">관련 정보는 이 문서 앞부분의 필수 조건 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-195">(See the Prerequisites section at the top of this article).</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="ad4ca-196">서비스 배포 테스트</span><span class="sxs-lookup"><span data-stu-id="ad4ca-196">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="ad4ca-197">웹 브라우저와 연결</span><span class="sxs-lookup"><span data-stu-id="ad4ca-197">Connect with a web browser</span></span>
<span data-ttu-id="ad4ca-198">분할/병합 서비스의 웹 끝점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-198">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="ad4ca-199">Azure 클래식 포털에서 클라우드 서비스의 **대시보드**로 이동한 다음 오른쪽의 **사이트 URL**에서 이 끝점을 찾아 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-199">You can find this in the Azure Classic Portal by going to the **Dashboard** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="ad4ca-200">기본 보안 설정을 통해 HTTP 끝점을 사용하지 않도록 설정되므로 **http://**를 **https://**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-200">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="ad4ca-201">이 URL에 해당하는 페이지를 브라우저에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-201">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="ad4ca-202">PowerShell 스크립트로 테스트</span><span class="sxs-lookup"><span data-stu-id="ad4ca-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="ad4ca-203">포함된 샘플 PowerShell 스크립트를 실행하여 사용자 환경 및 배포를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-203">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="ad4ca-204">포함된 스크립트 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-204">The script files included are:</span></span>

1. <span data-ttu-id="ad4ca-205">**SetupSampleSplitMergeEnvironment.ps1** - 분할/병합에 대한 테스트 데이터 계층을 설정합니다. 자세한 설명은 아래 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="ad4ca-206">**ExecuteSampleSplitMerge.ps1** - 데이터 계층에 대한 테스트 작업을 실행합니다. 자세한 설명은 아래 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="ad4ca-207">**GetMappings.ps1** – 분할된 데이터베이스 매핑의 현재 상태를 출력하는 최상위 샘플 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-207">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="ad4ca-208">**ShardManagement.psm1** – ShardManagement API를 래핑하는 도우미 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-208">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="ad4ca-209">**SqlDatabaseHelpers.psm1** – SQL Database 생성 및 관리를 위한 도우미 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="ad4ca-210">PowerShell 파일</span><span class="sxs-lookup"><span data-stu-id="ad4ca-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="ad4ca-211">단계</span><span class="sxs-lookup"><span data-stu-id="ad4ca-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="ad4ca-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="ad4ca-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="ad4ca-213">분할된 데이터베이스 맵 관리자 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="ad4ca-214">분할된 데이터베이스를 2개 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="ad4ca-215">해당 데이터베이스에 대한 분할된 데이터베이스 맵을 만듭니다. 이때 해당 데이터베이스의 기존 분할된 데이터베이스 맵은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="ad4ca-216">두 분할된 데이터베이스에서 작은 샘플 테이블을 만들고 둘 중 하나의 테이블을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-216">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="ad4ca-217">분할된 테이블에 대한 SchemaInfo를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-217">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="ad4ca-218">PowerShell 파일</span><span class="sxs-lookup"><span data-stu-id="ad4ca-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="ad4ca-219">단계</span><span class="sxs-lookup"><span data-stu-id="ad4ca-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="ad4ca-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="ad4ca-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="ad4ca-221">첫 번째 분할된 데이터베이스에서 두 번째 분할된 데이터베이스로 데이터의 절반을 분할하는 분할 요청을 분할/병합 서비스 웹 프런트 엔드로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-221">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="ad4ca-222">분할 요청 상태를 확인하기 위해 웹 프런트 엔드를 폴링한 다음 요청이 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-222">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="ad4ca-223">두 번째 분할된 데이터베이스에서 첫 번째 분할된 데이터베이스로 데이터를 다시 이동하는 병합 요청을 분할/병합 서비스 웹 프런트 엔드로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-223">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="ad4ca-224">병합 요청 상태를 확인하기 위해 웹 프런트 엔드를 폴링한 다음 요청이 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-224">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="ad4ca-225">PowerShell을 사용하여 배포 확인</span><span class="sxs-lookup"><span data-stu-id="ad4ca-225">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="ad4ca-226">새 PowerShell 창을 열고 분할/병합 패키지를 다운로드한 디렉터리로 이동한 다음 "powershell" 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-226">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="ad4ca-227">Azure SQL 데이터베이스 서버를 만들거나 기존 서버를 선택합니다. 이 서버에 분할된 데이터베이스 맵 관리자 및 분할된 데이터베이스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-227">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ad4ca-228">SetupSampleSplitMergeEnvironment.ps1 스크립트가 기본적으로 동일한 서버에 이러한 모든 데이터베이스를 만들어 스크립트를 단순하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-228">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="ad4ca-229">이 제한은 분할/병합 서비스 자체의 제한은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-229">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="ad4ca-230">분할/병합 서비스에서 데이터를 이동하고 분할된 데이터베이스 맵을 업데이트하려면 읽기/쓰기 액세스 권한이 있는 SQL 인증 로그인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-230">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="ad4ca-231">분할/병합 서비스는 클라우드에서 실행되므로 현재 통합 인증을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-231">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="ad4ca-232">Azure SQL Server가 이러한 스크립트를 실행하는 컴퓨터의 IP 주소에서 액세스할 수 있도록 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-232">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="ad4ca-233">이 설정은 Azure SQL Server/구성/허용된 IP 주소에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-233">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="ad4ca-234">SetupSampleSplitMergeEnvironment.ps1 스크립트를 실행하여 샘플 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-234">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="ad4ca-235">이 스크립트를 실행하면 분할된 데이터베이스 맵 관리자 데이터베이스 및 분할된 데이터베이스에서 기존의 분할된 데이터베이스 맵 관리 데이터 구조가 모두 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-235">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="ad4ca-236">분할된 데이터베이스 맵 또는 분할된 데이터베이스를 다시 초기화하려는 경우에 이 스크립트를 다시 실행하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-236">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="ad4ca-237">샘플 명령줄:</span><span class="sxs-lookup"><span data-stu-id="ad4ca-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="ad4ca-238">현재 샘플 환경에 있는 매핑을 보려면 Getmappings.ps1 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-238">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="ad4ca-239">ExecuteSampleSplitMerge.ps1 스크립트를 실행하여 첫 번째 분할된 데이터베이스에서 두 번째 분할된 데이터베이스로 데이터의 절반을 이동하는 분할 작업을 실행한 다음 데이터를 첫 번째 분할된 데이터베이스로 다시 이동하는 병합 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-239">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="ad4ca-240">SSL을 구성하고 http 끝점을 사용할 수 없도록 설정해 둔 경우에는 https:// 끝점을 대신 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-240">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="ad4ca-241">샘플 명령줄:</span><span class="sxs-lookup"><span data-stu-id="ad4ca-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="ad4ca-242">아래 오류가 표시되면 대개 웹 끝점의 인증서에 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-242">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="ad4ca-243">원하는 웹 브라우저로 웹 끝점에 연결하여 인증서 오류가 발생하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-243">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="ad4ca-244">정상적으로 연결되는 경우의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-244">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="ad4ca-245">다른 데이터 형식으로도 연결해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-245">Experiment with other data types!</span></span> <span data-ttu-id="ad4ca-246">이러한 모든 스크립트는 키 유형을 지정할 수 있도록 하는 선택적인 -ShardKeyType 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-246">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="ad4ca-247">기본값은 Int32지만 Int64, GUID 또는 이진 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-247">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="ad4ca-248">요청 만들기</span><span class="sxs-lookup"><span data-stu-id="ad4ca-248">Create requests</span></span>
<span data-ttu-id="ad4ca-249">웹 UI를 사용하거나 웹 역할을 통해 요청을 제출하는 SplitMerge.psm1 PowerShell 모듈을 가져와서 사용하여 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-249">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="ad4ca-250">이 서비스는 분할된 테이블과 참조 테이블 모두에서 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-250">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="ad4ca-251">분할된 테이블에는 분할 키 열과 각 분할 키에 대한 여러 행의 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="ad4ca-252">참조 테이블은 분할되지 않으므로 모든 분할된 데이터베이스에 동일한 행 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-252">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="ad4ca-253">참조 테이블은 자주 변경되지 않으며 쿼리에서 분할된 테이블과 조인하는 데 사용되는 데이터에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-253">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="ad4ca-254">분할/병합 작업을 수행하려면 이동할 분할된 테이블 및 참조 테이블을 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-254">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="ad4ca-255">**SchemaInfo** API를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-255">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="ad4ca-256">이 API는 **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** 네임스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-256">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="ad4ca-257">각 분할된 테이블에 대해 테이블의 부모 스키마 이름(선택 사항, 기본값은 “dbo”), 테이블 이름 및 분할 키가 포함된 해당 테이블의 열 이름을 설명하는 **ShardedTableInfo** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-257">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="ad4ca-258">각 참조 테이블에 대해 테이블의 부모 스키마 이름(선택 사항, 기본값은 “dbo”) 및 테이블 이름을 설명하는 **ReferenceTableInfo** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-258">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="ad4ca-259">새 **SchemaInfo** 개체에 위의 TableInfo 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-259">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="ad4ca-260">**ShardMapManager** 개체에 대한 참조를 가져와 **GetSchemaInfoCollection**을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-260">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="ad4ca-261">**SchemaInfo**를 **SchemaInfoCollection**에 추가하고 분할된 데이터베이스 맵 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-261">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="ad4ca-262">이러한 예는 SetupSampleSplitMergeEnvironment.ps1 스크립트에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-262">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="ad4ca-263">분할/병합 서비스에서 대상 데이터베이스(또는 데이터베이스의 모든 테이블에 대한 스키마)를 자동으로 생성하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-263">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="ad4ca-264">대상 데이터베이스가 미리 생성되어 있어야 서비스에 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-264">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ad4ca-265">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ad4ca-265">Troubleshooting</span></span>
<span data-ttu-id="ad4ca-266">샘플 PowerShell 스크립트를 실행할 때 아래 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-266">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="ad4ca-267">이 오류는 SSL 인증서가 제대로 구성되지 않은 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="ad4ca-268">'웹 브라우저로 연결' 섹션의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-268">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="ad4ca-269">요청을 제출할 수 없는 경우에 다음이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="ad4ca-270">이 경우 구성 파일, 특히 **WorkerRoleSynchronizationStorageAccountConnectionString**에 대한 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-270">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="ad4ca-271">이 오류는 일반적으로 작업자 역할이 처음 사용할 때 메타데이터 데이터베이스를 성공적으로 초기화하지 못했을 때 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ad4ca-271">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

