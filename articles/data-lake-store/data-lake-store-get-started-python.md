---
title: "Azure 데이터 레이크 저장소 aaaUse hello Python SDK tooget 시작 | Microsoft Docs"
description: "데이터 레이크 저장소 계정 및 hello toouse Python SDK toowork 파일 시스템 방법에 대해 알아봅니다."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="d6a89-103">Python을 사용하여 Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="d6a89-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6a89-104">포털</span><span class="sxs-lookup"><span data-stu-id="d6a89-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="d6a89-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6a89-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="d6a89-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="d6a89-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="d6a89-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="d6a89-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="d6a89-108">REST API</span><span class="sxs-lookup"><span data-stu-id="d6a89-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="d6a89-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d6a89-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="d6a89-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d6a89-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="d6a89-111">Python</span><span class="sxs-lookup"><span data-stu-id="d6a89-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="d6a89-112">어떻게 toouse hello Python SDK tooperform 기본 작업 Azure와 Azure 데이터 레이크 저장소와 같은 폴더를 만들기에 대 한 업로드 및 다운로드 등 데이터 파일에 알아봅니다. Data Lake에 대한 자세한 내용은 [Azure Data Lake Store](data-lake-store-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6a89-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6a89-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d6a89-113">Prerequisites</span></span>

* <span data-ttu-id="d6a89-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="d6a89-114">**Python**.</span></span> <span data-ttu-id="d6a89-115">Python을 [여기](https://www.python.org/downloads/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="d6a89-116">이 문서에서는 Python 3.5.2를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="d6a89-117">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="d6a89-117">**An Azure subscription**.</span></span> <span data-ttu-id="d6a89-118">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6a89-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d6a89-119">**Azure Active Directory 응용 프로그램을 만듭니다**.</span><span class="sxs-lookup"><span data-stu-id="d6a89-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="d6a89-120">Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="d6a89-121">없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="d6a89-122">지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="d6a89-123">Hello 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="d6a89-123">Install hello modules</span></span>

<span data-ttu-id="d6a89-124">Python을 사용 하 여 데이터 레이크 저장소와 toowork, tooinstall 단원과 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="d6a89-125">hello `azure-mgmt-resource` 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="d6a89-126">Active Directory 등 Azure 모듈을 포함합니다...</span><span class="sxs-lookup"><span data-stu-id="d6a89-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="d6a89-127">hello `azure-mgmt-datalake-store` 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="d6a89-128">Hello Azure 데이터 레이크 저장소 계정 관리 작업도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="d6a89-129">이 모듈에 대한 자세한 내용은 [Azure Data Lake Store 관리 모듈 참조](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6a89-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="d6a89-130">hello `azure-datalake-store` 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="d6a89-131">이 hello Azure 데이터 레이크 저장소 파일 시스템 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="d6a89-132">이 모듈에 대한 자세한 내용은 [Azure Data Lake Store 파일 시스템 모듈 참조](http://azure-datalake-store.readthedocs.io/en/latest/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6a89-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="d6a89-133">다음 명령을 tooinstall hello 모듈 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="d6a89-134">새 Python 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d6a89-134">Create a new Python application</span></span>

1. <span data-ttu-id="d6a89-135">사용자가 선택한 IDE hello 새 Python 응용 프로그램을 예를 들어 만듭니다 **mysample.py**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="d6a89-136">다음 줄 tooimport hello 필요한 모듈 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-136">Add hello following lines tooimport hello required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="d6a89-137">변경 내용을 toomysample.py를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="d6a89-138">인증</span><span class="sxs-lookup"><span data-stu-id="d6a89-138">Authentication</span></span>

<span data-ttu-id="d6a89-139">이 섹션에서는 Azure AD와 다양 한 방법 tooauthenticate hello에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="d6a89-140">사용 가능한 hello 옵션은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-140">hello options available are:</span></span>

* <span data-ttu-id="d6a89-141">최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d6a89-141">End-user authentication</span></span>
* <span data-ttu-id="d6a89-142">서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="d6a89-142">Service-to-service authentication</span></span>
* <span data-ttu-id="d6a89-143">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d6a89-143">Multi-factor authentication</span></span>

<span data-ttu-id="d6a89-144">계정 관리와 파일 시스템 관리 모듈 모두에 대해 이러한 인증 옵션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="d6a89-145">계정 관리를 위한 최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d6a89-145">End-user authentication for account management</span></span>

<span data-ttu-id="d6a89-146">계정 관리 작업 (만들기/삭제 데이터 레이크 저장소 계정 등.)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="d6a89-147">Azure AD 사용자에 대한 사용자 이름과 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="d6a89-148">Note hello 사용자를 multi-factor authentication에 대해 구성 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="d6a89-149">파일 시스템 작업에 대한 최종 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d6a89-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="d6a89-150">파일 시스템 작업 (만들기 폴더, 파일 업로드 등)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="d6a89-151">기존 Azure AD **네이티브 클라이언트**와 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="d6a89-152">에 대 한 자격 증명을 제공 하는 hello Azure AD 사용자를 multi-factor authentication에 대해 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="d6a89-153">계정 관리를 위해 클라이언트 암호로 서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="d6a89-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="d6a89-154">계정 관리 작업 (만들기/삭제 데이터 레이크 저장소 계정 등.)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="d6a89-155">다음 코드 조각 hello 수 tooauthenticate 사용 되는 응용 프로그램 비 대화형으로 hello 클라이언트 암호를 사용 하 여 응용 프로그램 / 서비스 주체에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="d6a89-156">기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="d6a89-157">파일 시스템 작업을 위해 클라이언트 암호로 서비스 간 인증</span><span class="sxs-lookup"><span data-stu-id="d6a89-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="d6a89-158">파일 시스템 작업 (만들기 폴더, 파일 업로드 등)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="d6a89-159">다음 코드 조각 hello 수 tooauthenticate 사용 되는 응용 프로그램 비 대화형으로 hello 클라이언트 암호를 사용 하 여 응용 프로그램 / 서비스 주체에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="d6a89-160">기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="d6a89-161">계정 관리를 위한 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d6a89-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="d6a89-162">계정 관리 작업 (만들기/삭제 데이터 레이크 저장소 계정 등.)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="d6a89-163">hello 다음 코드 조각 수 tooauthenticate 다단계 인증을 사용 하 여 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="d6a89-164">기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="d6a89-165">파일 시스템 관리를 위한 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d6a89-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="d6a89-166">파일 시스템 작업 (만들기 폴더, 파일 업로드 등)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="d6a89-167">hello 다음 코드 조각 수 tooauthenticate 다단계 인증을 사용 하 여 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="d6a89-168">기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="d6a89-169">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d6a89-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="d6a89-170">다음 코드 조각 toocreate Azure 리소스 그룹 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="d6a89-171">클라이언트 및 Data Lake Store 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d6a89-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="d6a89-172">먼저 코드 조각 다음 hello hello 데이터 레이크 저장소 계정 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="d6a89-173">Hello 클라이언트 개체 toocreate 데이터 레이크 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="d6a89-174">마지막으로, hello 조각 파일 시스템 클라이언트 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6a89-174">Finally, hello snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="d6a89-175">Hello Data Lake 저장소 계정 나열</span><span class="sxs-lookup"><span data-stu-id="d6a89-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="d6a89-176">디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="d6a89-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="d6a89-177">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="d6a89-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="d6a89-178">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="d6a89-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="d6a89-179">디렉터리 삭제</span><span class="sxs-lookup"><span data-stu-id="d6a89-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="d6a89-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d6a89-180">See also</span></span>

- [<span data-ttu-id="d6a89-181">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="d6a89-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="d6a89-182">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="d6a89-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="d6a89-183">데이터 레이크 저장소와 함께 Azure HDInsight 사용</span><span class="sxs-lookup"><span data-stu-id="d6a89-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="d6a89-184">Data Lake Store .NET SDK 참조</span><span class="sxs-lookup"><span data-stu-id="d6a89-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="d6a89-185">Data Lake Store REST 참조</span><span class="sxs-lookup"><span data-stu-id="d6a89-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
