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
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Python을 사용하여 Azure Data Lake Store 시작

> [!div class="op_single_selector"]
> * [포털](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

어떻게 toouse hello Python SDK tooperform 기본 작업 Azure와 Azure 데이터 레이크 저장소와 같은 폴더를 만들기에 대 한 업로드 및 다운로드 등 데이터 파일에 알아봅니다. Data Lake에 대한 자세한 내용은 [Azure Data Lake Store](data-lake-store-overview.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

* **Python**. Python을 [여기](https://www.python.org/downloads/)에서 다운로드할 수 있습니다. 이 문서에서는 Python 3.5.2를 사용합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

* **Azure Active Directory 응용 프로그램을 만듭니다**. Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다. 없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다. 지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.

## <a name="install-hello-modules"></a>Hello 모듈 설치

Python을 사용 하 여 데이터 레이크 저장소와 toowork, tooinstall 단원과 필요 합니다.

* hello `azure-mgmt-resource` 모듈입니다. Active Directory 등 Azure 모듈을 포함합니다...
* hello `azure-mgmt-datalake-store` 모듈입니다. Hello Azure 데이터 레이크 저장소 계정 관리 작업도 포함 됩니다. 이 모듈에 대한 자세한 내용은 [Azure Data Lake Store 관리 모듈 참조](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html)를 참조하세요.
* hello `azure-datalake-store` 모듈입니다. 이 hello Azure 데이터 레이크 저장소 파일 시스템 작업이 포함 됩니다. 이 모듈에 대한 자세한 내용은 [Azure Data Lake Store 파일 시스템 모듈 참조](http://azure-datalake-store.readthedocs.io/en/latest/)를 참조하세요.

다음 명령을 tooinstall hello 모듈 hello를 사용 합니다.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>새 Python 응용 프로그램 만들기

1. 사용자가 선택한 IDE hello 새 Python 응용 프로그램을 예를 들어 만듭니다 **mysample.py**합니다.

2. 다음 줄 tooimport hello 필요한 모듈 hello를 추가 합니다.

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

3. 변경 내용을 toomysample.py를 저장 합니다.

## <a name="authentication"></a>인증

이 섹션에서는 Azure AD와 다양 한 방법 tooauthenticate hello에 설명 합니다. 사용 가능한 hello 옵션은 같습니다.

* 최종 사용자 인증
* 서비스 간 인증
* Multi-Factor Authentication

계정 관리와 파일 시스템 관리 모듈 모두에 대해 이러한 인증 옵션을 사용해야 합니다.

### <a name="end-user-authentication-for-account-management"></a>계정 관리를 위한 최종 사용자 인증

계정 관리 작업 (만들기/삭제 데이터 레이크 저장소 계정 등.)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다. Azure AD 사용자에 대한 사용자 이름과 암호를 제공해야 합니다. Note hello 사용자를 multi-factor authentication에 대해 구성 되지 않아야 합니다.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>파일 시스템 작업에 대한 최종 사용자 인증

파일 시스템 작업 (만들기 폴더, 파일 업로드 등)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다. 기존 Azure AD **네이티브 클라이언트**와 함께 사용합니다. 에 대 한 자격 증명을 제공 하는 hello Azure AD 사용자를 multi-factor authentication에 대해 구성 되어야 합니다.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>계정 관리를 위해 클라이언트 암호로 서비스 간 인증

계정 관리 작업 (만들기/삭제 데이터 레이크 저장소 계정 등.)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다. 다음 코드 조각 hello 수 tooauthenticate 사용 되는 응용 프로그램 비 대화형으로 hello 클라이언트 암호를 사용 하 여 응용 프로그램 / 서비스 주체에 대 한 합니다. 기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>파일 시스템 작업을 위해 클라이언트 암호로 서비스 간 인증

파일 시스템 작업 (만들기 폴더, 파일 업로드 등)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다. 다음 코드 조각 hello 수 tooauthenticate 사용 되는 응용 프로그램 비 대화형으로 hello 클라이언트 암호를 사용 하 여 응용 프로그램 / 서비스 주체에 대 한 합니다. 기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>계정 관리를 위한 Multi-Factor Authentication

계정 관리 작업 (만들기/삭제 데이터 레이크 저장소 계정 등.)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다. hello 다음 코드 조각 수 tooauthenticate 다단계 인증을 사용 하 여 응용 프로그램을 사용 합니다. 기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.

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

### <a name="multi-factor-authentication-for-filesystem-management"></a>파일 시스템 관리를 위한 Multi-Factor Authentication

파일 시스템 작업 (만들기 폴더, 파일 업로드 등)에 대 한 Azure AD와이 tooauthenticate를 사용 합니다. hello 다음 코드 조각 수 tooauthenticate 다단계 인증을 사용 하 여 응용 프로그램을 사용 합니다. 기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Azure 리소스 그룹 만들기

다음 코드 조각 toocreate Azure 리소스 그룹 hello를 사용 합니다.

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

## <a name="create-clients-and-data-lake-store-account"></a>클라이언트 및 Data Lake Store 계정 만들기

먼저 코드 조각 다음 hello hello 데이터 레이크 저장소 계정 클라이언트를 만듭니다. Hello 클라이언트 개체 toocreate 데이터 레이크 저장소 계정을 사용합니다. 마지막으로, hello 조각 파일 시스템 클라이언트 개체를 만듭니다.

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

## <a name="list-hello-data-lake-store-accounts"></a>Hello Data Lake 저장소 계정 나열

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>디렉터리 만들기

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>파일 업로드


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>파일 다운로드

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>디렉터리 삭제

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>참고 항목

- [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
- [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [데이터 레이크 저장소와 함께 Azure HDInsight 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Data Lake Store .NET SDK 참조](https://msdn.microsoft.com/library/mt581387.aspx)
- [Data Lake Store REST 참조](https://msdn.microsoft.com/library/mt693424.aspx)
