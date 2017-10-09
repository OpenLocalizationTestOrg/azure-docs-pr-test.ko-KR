---
title: "aaaCreate HDInsight 클러스터 데이터 레이크 저장소와 기본 저장소로 PowerShell을 사용 하 여 | Microsoft Docs"
description: "Azure PowerShell toocreate를 사용 하 고 HDInsight 클러스터를 사용 하 여 Azure 데이터 레이크 저장소"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="41b29-103">PowerShell을 사용하여 Data Lake Store를 기본 저장소로 사용한 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="41b29-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41b29-104">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="41b29-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="41b29-105">PowerShell 사용(기본 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="41b29-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="41b29-106">PowerShell 사용(추가 저장소의 경우)</span><span class="sxs-lookup"><span data-stu-id="41b29-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="41b29-107">Resource Manager 사용</span><span class="sxs-lookup"><span data-stu-id="41b29-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="41b29-108">기본 저장소로 Azure 데이터 레이크 저장소와 toouse Azure PowerShell tooconfigure Azure HDInsight 클러스터 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="41b29-109">Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터를 만드는 방법에 대한 지침은 [Data Lake Store를 추가 저장소로 사용하여 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41b29-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="41b29-110">Data Lake Store에서 HDInsight를 사용하는 몇 가지 중요한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="41b29-111">hello 옵션 toocreate HDInsight 클러스터에 액세스할 수 있는 기본 저장소로 tooData Lake 저장소는 HDInsight 버전 3.5 및 3.6 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="41b29-112">기본 저장소는 HDInsight 클러스터를 hello 옵션 toocreate 액세스할 tooData Lake 저장소 *사용할 수 없는* 프리미엄 HDInsight 클러스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="41b29-113">PowerShell을 사용 하 여 데이터 레이크 저장소와 tooconfigure HDInsight toowork hello 다음 5 개의 섹션에 hello 지침을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="41b29-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41b29-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41b29-114">Prerequisites</span></span>
<span data-ttu-id="41b29-115">이 자습서를 시작 하기 전에 hello 요구 사항을 준수를 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="41b29-116">**Azure 구독**: 너무 이동[가져오기 Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="41b29-117">**Azure PowerShell 1.0 이상**: 참조 [어떻게 tooinstall PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="41b29-118">**Windows 소프트웨어 개발 키트 (SDK)**: Windows SDK tooinstall 너무 이동[다운로드 및 Windows 10 용 도구](https://dev.windows.com/en-us/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="41b29-119">hello SDK에 사용 되는 toocreate 보안 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="41b29-120">**Azure Active Directory 서비스 사용자**:이 자습서에서는 설명 방법을 toocreate Azure Active Directory (Azure AD)에 서비스 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="41b29-121">그러나 toocreate 서비스 사용자 여야 Azure AD 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="41b29-122">관리자 인 경우이 필수 구성이 요소를 건너뛰고 hello 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="41b29-123">Azure AD 관리자인 경우에만 서비스 주체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="41b29-124">Azure AD 관리자가 서비스 주체를 만들어야 Data Lake Store와 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="41b29-125">hello 서비스 사용자에서 만들어야 합니다는 인증서에 설명 된 대로 [인증서로 서비스 사용자를 만들](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="41b29-126">Data Lake 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="41b29-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="41b29-127">데이터 레이크 저장소 계정 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="41b29-128">바탕 화면에서 PowerShell 창을 열고 하 고 아래 hello 조각은 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="41b29-129">사용자가 hello 구독 관리자 또는 소유자 중 하나로 로그인에서 증명된 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="41b29-130">Hello 데이터 레이크 저장소 리소스 공급자를 등록 하 고 다음과 같은 오류가 발생 너무`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, 사용자 구독 데이터 레이크 저장소에 대 한 허용 목록에 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="41b29-131">tooenable hello 데이터 레이크 저장소 공개 미리 보기에서는 Azure 구독에 hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="41b29-132">Data Lake Store 계정은 Azure 리소스 그룹과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="41b29-133">리소스 그룹을 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="41b29-134">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="41b29-135">Data Lake Store 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="41b29-136">hello 계정 이름을 지정 하는 유일한 소문자와 숫자만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="41b29-137">Hello 다음과 같은 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-137">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. <span data-ttu-id="41b29-138">기본 저장소로 데이터 레이크 저장소를 사용 하려면 toospecify 루트 경로 toowhich hello 클러스터 관련 파일은 클러스터를 만드는 동안 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="41b29-139">루트 경로 toocreate **/클러스터/hdiadlcluster** hello 코드 조각에서 cmdlet 뒤 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41b29-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="41b29-140">역할 기반 인증에 대 한 설정 tooData 레이크 스토어에 액세스</span><span class="sxs-lookup"><span data-stu-id="41b29-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="41b29-141">모든 Azure 구독은 Azure AD 엔터티와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="41b29-142">사용자 및 서비스를 사용 하 여 구독 리소스에 액세스 hello Azure 포털 또는 Azure 리소스 관리자 API hello 먼저 Azure AD에 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="41b29-143">액세스가는 hello Azure 리소스에 적절 한 역할을 지정 하 여 tooAzure 구독 및 서비스 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="41b29-144">서비스에 대 한 서비스 사용자는 Azure AD에서 hello 서비스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="41b29-145">이 섹션에서는 HDInsight에 대 한 액세스 tooan Azure 리소스 (hello 앞에서 만든 데이터 레이크 저장소 계정)와 같은 응용 프로그램 toogrant 서비스 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="41b29-146">이렇게 하면 서비스 hello 응용 프로그램에 대 한 주 만들고 역할 tooit PowerShell 통해 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="41b29-147">Azure 데이터 레이크에 대 한 Active Directory 인증을 tooset hello 다음 두 섹션에서에서 hello 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="41b29-148">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="41b29-148">Create a self-signed certificate</span></span>
<span data-ttu-id="41b29-149">있는지 [Windows SDK](https://dev.windows.com/en-us/downloads) 이 섹션의 단계를 hello 계속 하기 전에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="41b29-150">또한 만들었어야 디렉터리와 같은 *C:\mycertdir*hello 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="41b29-151">Hello PowerShell 창에서 Windows SDK를 설치한 toohello 위치로 이동 합니다 (일반적으로 *C:\Program Files (x86) \Windows Kits\10\bin\x86*) hello를 사용 하 여 [MakeCert] [ makecert] 유틸리티 toocreate 자체 서명 된 인증서와 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="41b29-152">다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="41b29-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="41b29-153">입력 정보 요청된 tooenter hello 개인 키 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="41b29-154">Hello 명령을 성공적으로 실행 된 후 표시 되어야 **CertFile.cer** 및 **mykey.pvk** 지정한 hello 인증서 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="41b29-155">사용 하 여 hello [Pvk2Pfx] [ pvk2pfx] 유틸리티 tooconvert hello.pvk와.cer 파일 MakeCert 만든된 tooa.pfx 파일에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="41b29-156">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="41b29-157">메시지가 표시 되 면 hello 개인 키 암호를 이전에 지정한 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="41b29-158">hello에 대 한 사용자가 지정한 값 hello **po** 매개 변수는 hello.pfx 파일을 연관 된 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="41b29-159">Hello 명령을 성공적으로 완료 된 후 또한 표시는 **CertFile.pfx** 지정한 hello 인증서 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="41b29-160">Azure AD 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="41b29-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="41b29-161">이 섹션에서는 Azure AD 응용 프로그램에 대 한 서비스 사용자 역할 toohello 서비스 사용자를 할당 만들고 인증서를 제공 하 여 hello 서비스 사용자로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="41b29-162">toocreate hello 다음 명령을 실행 합니다. Azure AD에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="41b29-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="41b29-163">Hello를 hello PowerShell 콘솔 창에서 cmdlet 뒤에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="41b29-164">Hello에 대 한 사용자가 지정한 해당 hello 값 확인 **-DisplayName** 속성은 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="41b29-165">에 대 한 값을 hello **-홈 페이지** 및 **-IdentiferUris** 자리 표시자 값 이며 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="41b29-166">Hello 응용 프로그램 ID를 사용 하 여 서비스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="41b29-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="41b29-167">Hello 서비스 보안 주체 액세스 toohello 데이터 레이크 저장소 루트 및 이전에 지정한 hello 루트 경로에 모든 hello 폴더에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="41b29-168">Hello 다음 cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="41b29-169">Hello 기본 저장소로 데이터 레이크 저장소 HDInsight Linux 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="41b29-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="41b29-170">이 섹션에서는 hello 기본 저장소로 데이터 레이크 저장소와 HDInsight Hadoop Linux 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="41b29-171">이 릴리스의 경우 HDInsight 클러스터를 hello 및 데이터 레이크 저장소 hello에 있어야 합니다. 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="41b29-172">Hello 구독 테 넌 트 ID를 검색 하 고 저장 toouse 나중에 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="41b29-173">Hello 다음 cmdlet을 사용 하 여 hello HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="41b29-174">Hello cmdlet 성공적으로 완료 된 후에 hello 클러스터 세부 정보를 나열 하는 출력을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="41b29-175">Hello HDInsight 클러스터 toouse 데이터 레이크 저장소에서 테스트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="41b29-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="41b29-176">HDInsight 클러스터를 구성 하 고 나면 tooensure 데이터 레이크 저장소에 액세스할 수 있는지를 테스트 작업이 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="41b29-177">toodo 따라서 실행 샘플 하이브 작업 toocreate에 데이터 레이크 저장소에서 이미 사용할 수 있는 hello 예제 데이터를 사용 하는 테이블  *<cluster root>/example/data/sample.log*합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="41b29-178">이 섹션에서는 hello 만든 HDInsight Linux 클러스터에 SSH (보안 셸) 연결을 만들고 샘플 하이브 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="41b29-179">Windows 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="41b29-180">Linux 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="41b29-181">Hello 연결을 만든 후 다음 명령을 hello를 사용 하 여 hello 하이브 CLI (명령줄 인터페이스)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="41b29-182">다음 문을 toocreate 라는 새 테이블이 사용 하 여 hello CLI tooenter hello **차량** 데이터 레이크 저장소의 hello 예제 데이터를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="41b29-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="41b29-183">Hello 쿼리 출력 hello SSH 콘솔에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="41b29-184">hello hello CREATE TABLE 명령 앞에 경로 toohello 예제 데이터는 `adl:///example/data/`여기서 `adl:///` hello 클러스터 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="41b29-185">이 자습서에 지정 된 hello 클러스터 루트의 hello 예제에서는 다음 hello 명령은 `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="41b29-186">Hello 더 짧은 대체를 사용 하거나 hello 전체 경로 toohello 클러스터 루트를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="41b29-187">HDFS 명령을 사용하여 Data Lake Store에 액세스</span><span class="sxs-lookup"><span data-stu-id="41b29-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="41b29-188">Hello HDInsight 클러스터 toouse Data Lake 저장소를 구성 하 고 나면 Hadoop 분산 파일 시스템 (HDFS) 셸 명령을 tooaccess hello 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="41b29-189">이 섹션에서는 hello 만든 HDInsight Linux 클러스터에 대 한 SSH 연결을 확인 하 고 hello HDFS 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="41b29-190">Windows 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH를 Windows에서 HDInsight의 Linux 기반 Hadoop 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="41b29-191">Linux 클라이언트 toomake hello 클러스터에 대 한 SSH 연결을 사용 하는 경우 참조 [SSH Linux에서 HDInsight의 Hadoop Linux 기반를 사용](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="41b29-192">Hello 연결을 완료 한 후 다음 HDFS 파일 시스템 명령을 hello를 사용 하 여 데이터 레이크 저장소의 hello 파일을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="41b29-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="41b29-193">Hello를 사용할 수도 있습니다 `hdfs dfs -put` 일부 파일 tooData Lake 저장소 tooupload 명령을 클릭 한 다음 사용 하 여 `hdfs dfs -ls` tooverify hello 파일이 성공적으로 업로드 된 여부.</span><span class="sxs-lookup"><span data-stu-id="41b29-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="41b29-194">참고 항목</span><span class="sxs-lookup"><span data-stu-id="41b29-194">See also</span></span>
* [<span data-ttu-id="41b29-195">Azure 포털: HDInsight 클러스터 toouse 데이터 레이크 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="41b29-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
