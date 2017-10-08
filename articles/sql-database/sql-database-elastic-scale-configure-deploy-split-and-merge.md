---
title: "분할 / 병합 서비스 aaaDeploy | Microsoft Docs"
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
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="31d54-103">분할/병합 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="31d54-103">Deploy a split-merge service</span></span>
<span data-ttu-id="31d54-104">hello 분할 / 병합 도구를 사용 하면 분할 된 데이터베이스 간에 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="31d54-105">[확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="31d54-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="31d54-106">Hello 분할 / 병합 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="31d54-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="31d54-107">Hello 최신 NuGet 버전에서 다운로드 [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="31d54-108">명령 프롬프트를 열고 nuget.exe 다운로드 toohello 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="31d54-109">hello 다운로드 PowerShell commmands 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="31d54-110">아래의 명령 hello로 hello 현재 디렉터리로 hello 최신 분할 / 병합 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="31d54-111">hello 파일이 디렉터리에 배치 됩니다 **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** 여기서 *x.x.xxx.x* hello 버전 번호를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="31d54-112">Hello hello 분할 / 병합 서비스 파일을 찾으려면 **content\splitmerge\service** 하위 디렉터리 및 hello 분할 / 병합 PowerShell 스크립트 (및 필요한 클라이언트.dll) hello **content\splitmerge\powershell** 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31d54-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31d54-113">Prerequisites</span></span>
1. <span data-ttu-id="31d54-114">Hello 분할 / 병합 상태를 데이터베이스로 사용 될 Azure SQL DB 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="31d54-115">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="31d54-116">새 **SQL 데이터베이스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="31d54-117">Hello 데이터베이스 이름을 지정 하 고 새 관리자 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="31d54-118">있는지 toorecord hello 이름 및 암호를 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="31d54-119">Azure SQL DB 서버에 Azure 서비스 tooconnect tooit을 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="31d54-120">Hello 포털 hello에 **방화벽 설정**, 해당 hello 확인 **tooAzure 서비스 액세스를 허용** 너무 설정은**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="31d54-121">Hello "저장" 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-121">Click hello "save" icon.</span></span>
   
   ![허용된 서비스][1]
3. <span data-ttu-id="31d54-123">진단 출력에 사용할 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="31d54-124">Azure 포털 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="31d54-125">Hello 왼쪽된 모음에서 **새로**, 클릭 **데이터 + 저장소**, 다음 **저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="31d54-126">분할/병합 서비스를 포함할 Azure 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="31d54-127">Azure 포털 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="31d54-128">Hello 왼쪽된 모음에서 **새로**, 다음 **계산**, **클라우드 서비스**, 및 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="31d54-129">분할/병합 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="31d54-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="31d54-130">분할/병합 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="31d54-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="31d54-131">분할 / 병합 hello 어셈블리 다운로드 hello 폴더에서 hello의 복사본을 만듭니다 **ServiceConfiguration.Template.cscfg** 와 함께 제공 된 파일 **SplitMergeService.cspkg** 하 고 이름을 **ServiceConfiguration.cscfg**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="31d54-132">열기 **ServiceConfiguration.cscfg** 인증서 지문 안녕하세요 형식 등의 입력의 유효성을 검사 하는 Visual Studio와 같은 텍스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="31d54-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="31d54-133">새 데이터베이스 만들기 또는 분할 / 병합 작업에 대 한 hello 상태 데이터베이스 이름으로 기존 데이터베이스 tooserve을 선택 하 고 해당 데이터베이스의 연결 문자열 hello를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="31d54-134">이때 hello 상태 데이터베이스 hello 라틴어 데이터 정렬을 사용 해야 합니다 (SQL\_Latin1\_일반\_CP1\_CI\_AS)입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="31d54-135">자세한 내용은 [Windows 데이터 정렬 이름(TRANSACT-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31d54-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="31d54-136">Azure SQL DB, 연결 문자열 hello hello 폼의 일반적으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="31d54-137">두 hello에 hello cscfg 파일에이 연결 문자열을 입력 **SplitMergeWeb** 및 **SplitMergeWorker** hello ElasticScaleMetadata 설정의 역할 섹션.</span><span class="sxs-lookup"><span data-stu-id="31d54-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="31d54-138">Hello에 대 한 **SplitMergeWorker** 역할 hello에 대 한 올바른 연결 문자열 tooAzure 저장소 입력 **WorkerRoleSynchronizationStorageAccountConnectionString** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="31d54-139">보안 구성</span><span class="sxs-lookup"><span data-stu-id="31d54-139">Configure security</span></span>
<span data-ttu-id="31d54-140">자세한 지침은 tooconfigure hello hello 서비스의 보안을 위해 toohello 참조 [분할 / 병합 보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="31d54-141">Hello이이 자습서에 대 한 간단한 테스트 배포를 위해 최소한의 구성 단계 tooget hello 서비스 시작 및 실행을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="31d54-142">다음이 단계 계정을 사용 하도록 설정만 hello 하나의 컴퓨터/toocommunicate hello 서비스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="31d54-143">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="31d54-143">Create a self-signed certificate</span></span>
<span data-ttu-id="31d54-144">새 디렉터리에서 다음 명령을 사용 하 여이 디렉터리 execute hello는 [Visual Studio 용 개발자 명령 프롬프트](http://msdn.microsoft.com/library/ms229859.aspx) 창:</span><span class="sxs-lookup"><span data-stu-id="31d54-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="31d54-145">암호 tooprotect hello 개인 키에 대 한 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="31d54-146">강력한 암호를 입력하고 이를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="31d54-147">그러면 hello 암호 toobe 그 후 한 번 더 사용에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="31d54-148">클릭 **예** hello 끝 tooimport에서 것 toohello 신뢰할 수 있는 인증 기관, 루트 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="31d54-149">PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="31d54-149">Create a PFX file</span></span>
<span data-ttu-id="31d54-150">Hello hello에서 다음 명령을 실행 makecert; 실행 위치 같은 창 사용 하 여 동일한 암호를 사용한 toocreate hello 인증서를 hello:</span><span class="sxs-lookup"><span data-stu-id="31d54-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="31d54-151">Hello hello 개인 저장소로 클라이언트 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="31d54-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="31d54-152">Windows 탐색기에서 **MyCert.pfx**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="31d54-153">Hello에 **인증서 가져오기 마법사** 선택 **현재 사용자** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="31d54-154">Hello 파일 경로 확인 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="31d54-155">Leave hello 암호 입력 **모든 확장된 속성을 포함** 채로 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="31d54-156">둡니다 **자동으로 선택 hello 인증서 저장소 [...]**  채로 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="31d54-157">**마침**, **확인**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="31d54-158">업로드 hello PFX 파일 toohello 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="31d54-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="31d54-159">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="31d54-160">**클라우드 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="31d54-161">Hello 분할/병합 서비스에 대 한 위에서 만든 hello 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="31d54-162">클릭 **인증서** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="31d54-163">클릭 **업로드** hello 아래쪽 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="31d54-164">Hello PFX 파일을 선택 하 고 hello 입력 위와 동일한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="31d54-165">완료 되 면 hello hello 목록에 새 항목에서 hello 인증서 지문을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="31d54-166">Hello 서비스 구성 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="31d54-166">Update hello service configuration file</span></span>
<span data-ttu-id="31d54-167">이러한 설정의 hello 지문/value 특성에 위의 복사 hello 인증서 지문을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="31d54-168">Hello 작업자 역할:</span><span class="sxs-lookup"><span data-stu-id="31d54-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="31d54-169">Hello 웹 역할:</span><span class="sxs-lookup"><span data-stu-id="31d54-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="31d54-170">암호화, CA, hello에 대 한 별도 인증서를 사용 해야 하는 프로덕션 배포에 대 한 hello 서버 인증서 및 클라이언트 인증서를 하십시오.</span><span class="sxs-lookup"><span data-stu-id="31d54-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="31d54-171">이와 관련된 자세한 지침은 [보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31d54-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="31d54-172">서비스 배포</span><span class="sxs-lookup"><span data-stu-id="31d54-172">Deploy your service</span></span>
1. <span data-ttu-id="31d54-173">Toohello 이동 [Azure 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="31d54-174">Hello 클릭 **클라우드 서비스** hello 왼쪽에 탭을 앞에서 만든 hello 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="31d54-175">**Dashboard**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="31d54-176">환경 준비 hello를 선택한 다음 클릭 **새 스테이징 배포를 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![스테이징][3]
5. <span data-ttu-id="31d54-178">Hello 대화 상자에서 배포 레이블을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="31d54-179">'패키지'와 '구성' 모두에 대 한 '에서 로컬 '를 클릭 하 고 hello 선택 **SplitMergeService.cspkg** 파일 및 이전에 구성 된.cscfg 파일.</span><span class="sxs-lookup"><span data-stu-id="31d54-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="31d54-180">해당 hello 확인란 확인 **하나 이상의 역할 단일 인스턴스가 포함 된 경우에 배포** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="31d54-181">Hello 맨 아래 오른쪽 toobegin hello 배포에서 hello 눈금 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="31d54-182">Tootake 예상 몇 분 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![업로드][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="31d54-184">Hello 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="31d54-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="31d54-185">웹 역할에 실패 하면 toocome 온라인가 hello 보안 구성에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="31d54-186">위에 설명 된 대로 SSL이 구성 되어 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="31d54-187">작업자 역할 toocome 온라인으로 실패 하는 경우 웹 역할에 성공 하면 것은 앞에서 만든 toohello 상태 데이터베이스 연결 문제가 있는 대부분입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="31d54-188">프로그램.cscfg의 hello 연결 문자열이 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="31d54-189">Hello 서버와 데이터베이스 존재 하는지, 그리고 hello 사용자 id와 암호가 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="31d54-190">Azure SQL DB에 대 한 연결 문자열 hello hello 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="31d54-191">해당 hello 서버 이름의로 시작 하지 않으면 확인 **https://**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="31d54-192">Azure SQL DB 서버에 Azure 서비스 tooconnect tooit을 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="31d54-193">toodo이를 열고 https://manage.windowsazure.com 왼쪽 hello에서 "SQL 데이터베이스"를 클릭, 클릭 "서버" hello 위쪽에, 한 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="31d54-194">클릭 **구성** hello에 가장 많이 사용 하 고 해당 hello 확인 **Azure 서비스** 설정 되어 너무 "Yes"입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="31d54-195">(Hello 필수 구성 요소를 참조 하십시오.이 문서의 hello 위쪽 섹션).</span><span class="sxs-lookup"><span data-stu-id="31d54-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="31d54-196">Hello 서비스 배포를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="31d54-197">웹 브라우저와 연결</span><span class="sxs-lookup"><span data-stu-id="31d54-197">Connect with a web browser</span></span>
<span data-ttu-id="31d54-198">분할 / 병합 서비스의 hello 웹 끝점을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="31d54-199">Toohello 이동 하 여 hello Azure 클래식 포털에서에서이 찾을 수 있습니다 **대시보드** 클라우드 서비스 및 아래 **사이트 URL** hello 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="31d54-200">대체 **http://** 와 **https://** 이후 hello 기본 보안 설정을 hello HTTP 끝점을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="31d54-201">이 URL에 대 한 hello 페이지를 브라우저에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="31d54-202">PowerShell 스크립트로 테스트</span><span class="sxs-lookup"><span data-stu-id="31d54-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="31d54-203">hello 배포 및 사용자 환경을 포함 하는 hello 샘플 PowerShell 스크립트를 실행 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="31d54-204">hello 스크립트 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-204">hello script files included are:</span></span>

1. <span data-ttu-id="31d54-205">**SetupSampleSplitMergeEnvironment.ps1** - 분할/병합에 대한 테스트 데이터 계층을 설정합니다. 자세한 설명은 아래 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31d54-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="31d54-206">**ExecuteSampleSplitMerge.ps1** -hello 테스트에서 테스트 작업을 실행 합니다 (자세한 설명은 아래 표 참조)는 데이터 계층</span><span class="sxs-lookup"><span data-stu-id="31d54-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="31d54-207">**GetMappings.ps1** 최상위-샘플 hello hello 분할 매핑의 현재 상태를 출력 하는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="31d54-208">**ShardManagement.psm1** -도우미 스크립트 래핑하는 hello ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="31d54-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="31d54-209">**SqlDatabaseHelpers.psm1** – SQL Database 생성 및 관리를 위한 도우미 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="31d54-210">PowerShell 파일</span><span class="sxs-lookup"><span data-stu-id="31d54-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="31d54-211">단계</span><span class="sxs-lookup"><span data-stu-id="31d54-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="31d54-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="31d54-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="31d54-213">분할된 데이터베이스 맵 관리자 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="31d54-214">분할된 데이터베이스를 2개 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="31d54-215">해당 데이터베이스에 대한 분할된 데이터베이스 맵을 만듭니다. 이때 해당 데이터베이스의 기존 분할된 데이터베이스 맵은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="31d54-216">두 hello 분할 영역에는 작은 예제 테이블을 만들고 hello 분할 된 데이터베이스 중 하나에 hello 테이블을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="31d54-217">Hello 분할 된 테이블에 대 한 hello SchemaInfo를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="31d54-218">PowerShell 파일</span><span class="sxs-lookup"><span data-stu-id="31d54-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="31d54-219">단계</span><span class="sxs-lookup"><span data-stu-id="31d54-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="31d54-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="31d54-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="31d54-221">분할 요청 toohello 분할 / 병합 서비스 웹 프런트 엔드를, hello 첫 번째 분할 toohello 두 번째 분할의 절반 hello 데이터를 분할 하 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="31d54-222">설문 hello hello 요청 완료 될 때까지 요청 상태 및 대기를 분할 하는 hello에 대 한 웹 프런트 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="31d54-223">병합 요청 toohello 분할 / 병합 서비스 웹 프런트 엔드를, hello 두 번째 분할 백 toohello 첫 번째 분할에서 hello 데이터를 이동 하 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="31d54-224">폴링 hello 웹 프런트 엔드 hello 병합 요청 상태와 hello 요청 완료 될 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="31d54-225">PowerShell tooverify 배포 사용</span><span class="sxs-lookup"><span data-stu-id="31d54-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="31d54-226">새 PowerShell 창을 열고 고 hello 분할 / 병합 패키지를 다운로드 한 toohello 디렉터리 이동한 hello "powershell" 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="31d54-227">Azure SQL 데이터베이스 서버 만들기 (또는 기존 서버 선택) 분할 하 고 hello shard map manager 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="31d54-228">hello SetupSampleSplitMergeEnvironment.ps1 스크립트 hello에 이러한 모든 데이터베이스를 만듭니다 기본 tookeep hello 스크립트 단순 하 여 동일한 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="31d54-229">이 한 제한은 아닙니다 hello 분할 / 병합 서비스의 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="31d54-230">SQL 인증 로그인 읽기/쓰기 액세스 toohello Db hello 분할 / 병합 서비스 toomove 데이터 및 업데이트 hello 분할 맵을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="31d54-231">Hello 클라우드에서 hello 분할 / 병합 서비스를 실행 하므로 지원 하지 않습니다 현재 통합 인증.</span><span class="sxs-lookup"><span data-stu-id="31d54-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="31d54-232">Hello Azure SQL server 구성 되어 있는지 확인 이러한 스크립트를 실행 하는 hello 컴퓨터의 IP 주소 hello에서에서 tooallow 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="31d54-233">이 설정은 hello Azure SQL server에서 찾을 수 / 구성 / IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="31d54-234">Hello SetupSampleSplitMergeEnvironment.ps1 스크립트 toocreate hello 예제 환경을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="31d54-235">이 스크립트를 실행 구조 hello shard map manager 데이터베이스 및 hello 분할 된 데이터베이스에 모든 기존 분할 맵 관리 데이터 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="31d54-236">초기화를 toore hello 분할 맵은 또는 분할 하려는 경우 유용한 toorerun hello 스크립트 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="31d54-237">샘플 명령줄:</span><span class="sxs-lookup"><span data-stu-id="31d54-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="31d54-238">Hello Getmappings.ps1 스크립트 tooview hello 매핑이 현재 존재 하는 hello 샘플 환경에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="31d54-239">(데이터를 이동 절반 hello hello 첫 번째 분할 toohello 두 번째 분할) 분할 작업 한 다음 병합 작업 (hello 데이터를 다시 hello 첫 번째 분할 영역으로 이동) hello ExecuteSampleSplitMerge.ps1 스크립트 tooexecute를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="31d54-240">SSL 및 사용 하지 않도록 설정 하는 왼쪽된 hello http 끝점을 구성한 경우 hello https:// 끝점을 대신 사용 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="31d54-241">샘플 명령줄:</span><span class="sxs-lookup"><span data-stu-id="31d54-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="31d54-242">Hello 아래의 오류를 받을 경우 대부분 웹 끝점의 인증서에 문제가입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="31d54-243">즐겨 찾는 웹 브라우저를 사용 하 여 toohello 웹 끝점 연결을 시도 하 고 인증서 오류가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="31d54-244">성공 하는 경우 아래 hello 같이 hello 출력 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="31d54-245">다른 데이터 형식으로도 연결해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-245">Experiment with other data types!</span></span> <span data-ttu-id="31d54-246">이러한 스크립트를 모두 수행 toospecify hello 키 유형 수 있는 선택적-ShardKeyType 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="31d54-247">hello 기본값은 Int32, 하지만 Int64, Guid 또는 이진 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="31d54-248">요청 만들기</span><span class="sxs-lookup"><span data-stu-id="31d54-248">Create requests</span></span>
<span data-ttu-id="31d54-249">hello 웹 UI를 사용 하 여 또는 가져오기 및 hello 웹 역할을 통해 사용자 요청을 제출 하는 hello SplitMerge.psm1 PowerShell 모듈을 사용 하 여 hello 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="31d54-250">hello 서비스에 분할 된 테이블과 참조 테이블에서 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="31d54-251">분할된 테이블에는 분할 키 열과 각 분할 키에 대한 여러 행의 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="31d54-252">참조 테이블이 분할 되지 않는 모든 분할 영역에 데이터를 행 동일 하므로 hello를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="31d54-253">참조 테이블은 데이터가 자주 변경 되지 않는 사용 하는 tooJOIN 된 쿼리에서 분할 된 테이블을 더 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="31d54-254">순서 tooperform 분할 / 병합 작업 hello 분할 된 테이블 및 참조 테이블을 이동 toohave를 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="31d54-255">Hello로 이렇게 **SchemaInfo** API입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="31d54-256">이 API는 hello에 **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="31d54-257">각 분할 된 테이블에 대해 만듭니다는 **ShardedTableInfo** hello 테이블의 부모 스키마 이름을 설명 하는 개체 (선택 사항 너무 기본값 "dbo"), 테이블 이름으로 hello 및 hello hello 분할 키가 포함 된 해당 테이블의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="31d54-258">각 참조 테이블에 대해 만듭니다는 **ReferenceTableInfo** hello 테이블의 부모 스키마 이름을 설명 하는 개체 (선택 사항 너무 기본값 "dbo")와 hello 테이블 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="31d54-259">새 TableInfo 개체 tooa 위에 hello 추가 **SchemaInfo** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="31d54-260">참조 tooa 가져오기 **ShardMapManager** 개체 및 호출 **GetSchemaInfoCollection**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="31d54-261">Hello 추가 **SchemaInfo** toohello **SchemaInfoCollection**, hello shard map 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="31d54-262">이러한 예는 hello SetupSampleSplitMergeEnvironment.ps1 스크립트에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="31d54-263">분할 / 병합 서비스 hello 만들지 않습니다 hello 대상 데이터베이스 (또는 hello 데이터베이스의 모든 테이블에 대 한 스키마)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="31d54-264">미리 생성 toohello 서비스 요청을 보내기 전에 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="31d54-265">문제 해결</span><span class="sxs-lookup"><span data-stu-id="31d54-265">Troubleshooting</span></span>
<span data-ttu-id="31d54-266">Hello 샘플 powershell 스크립트를 실행할 때는 hello 아래 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="31d54-267">이 오류는 SSL 인증서가 제대로 구성되지 않은 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="31d54-268">'웹 브라우저와 연결' 섹션의 지침에 hello 키를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="31d54-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="31d54-269">요청을 제출할 수 없는 경우에 다음이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="31d54-270">이 경우에 대해 특정 hello 설정에 구성 파일을 확인 **WorkerRoleSynchronizationStorageAccountConnectionString**합니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="31d54-271">이 오류는 일반적으로 해당 hello 작업자 역할 처음 사용 시 hello 메타 데이터 데이터베이스를 성공적으로 초기화할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="31d54-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

