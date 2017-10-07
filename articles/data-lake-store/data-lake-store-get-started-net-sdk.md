---
title: "aaaUse hello.NET SDK toodevelop 응용 프로그램에서 Azure 데이터 레이크 저장소 | Microsoft Docs"
description: "Azure 데이터 레이크 저장소.NET SDK toocreate 데이터 레이크 저장소 계정을 사용 하 고 hello 데이터 레이크 저장소의에서 기본 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>.NET SDK를 사용하여 Azure 데이터 레이크 저장소 시작
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

자세한 내용은 방법 toouse hello [Azure 데이터 레이크 저장소.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform와 같은 기본 작업 폴더를 만들어 업로드 한 데이터 파일 등을 다운로드 합니다. Data Lake에 대한 자세한 내용은 [Azure Data Lake Store](data-lake-store-overview.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
* **Visual Studio 2013, 2015 또는 2017**. Visual Studio 2015 업데이트 2를 사용 하는 hello 지침은 다음과 같습니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

* **Azure Data Lake Store 계정**. 방법에 대 한 계정에는 toocreate 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)

* **Azure Active Directory 응용 프로그램을 만듭니다**. Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다. 없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다. 지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.

## <a name="create-a-net-application"></a>.NET 응용 프로그램 만들기
1. Visual Studio를 열고 콘솔 응용 프로그램을 만듭니다.
2. Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.
3. **새 프로젝트**입력 하거나 다음 값에는 hello를 선택 합니다.

   | 속성 | 값 |
   | --- | --- |
   | Category |Templates/Visual C#/Windows |
   | Template |콘솔 응용 프로그램 |
   | 이름 |CreateADLApplication |
4. 클릭 **확인** toocreate hello 프로젝트.
5. Hello Nuget 패키지 tooyour 프로젝트를 추가 합니다.

   1. Hello 솔루션 탐색기에서에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.
   2. Hello에 **Nuget 패키지 관리자** 탭에서 다음 사항을 확인 **패키지 소스** 너무 설정**nuget.org** 있는지 **시험판 포함** 확인란 선택 되어 있습니다.
   3. 검색 하 고 hello 다음 NuGet 패키지를 설치 합니다.

      * `Microsoft.Azure.Management.DataLake.Store` - 이 자습서에서는 v2.1.3-미리 보기를 사용합니다.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - 이 자습서는 v2.2.12를 사용합니다.

        ![Nuget 원본 추가](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "새 Azure Data Lake 계정 만들기")
   4. 닫기 hello **Nuget 패키지 관리자**합니다.
6. 열기 **Program.cs**, hello 기존 코드를 삭제 하 고 hello 문을 tooadd 참조 toonamespaces 다음이 포함 됩니다.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. 아래와 같이 hello 변수를 선언 하 고 데이터 레이크 저장소 이름 및 이미 존재 하는 hello 리소스 그룹 이름에 대 한 hello 값을 제공 합니다. 여기에서 제공한 로컬 경로 파일 이름을 hello hello 컴퓨터에 있어야 하 고 있는지 확인 합니다. Hello 코드 조각 hello 네임 스페이스 선언 후 다음을 추가 합니다.

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

Hello 문서의 섹션 남은 hello, 어떻게 toouse hello 인증, 파일 업로드 등의 사용 가능한.NET 메서드 tooperform 작업을 볼 수 있습니다.

## <a name="authentication"></a>인증

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>최종 사용자 인증을 사용하는 경우(이 자습서에 권장됨)

이 사용 하 여 기존 Azure AD 네이티브 응용 프로그램 tooauthenticate 응용 프로그램 **대화형으로**, 어떤 의미 됩니다 메시지가 tooenter Azure 자격 증명입니다.

경우 사용 편의성에 대 한 아래 hello 조각 클라이언트 ID와 리디렉션 Azure 구독과 작동 하는 URI에 대 한 기본값을 사용 합니다. 이 자습서를 더 빨리 완료할 toohelp,이 방법을 사용 하면 두는 것이 좋습니다. 아래 hello 조각 제공 hello 값 테 넌 트 id 제공 하는 hello 지침을 사용 하 여 검색할 수 있습니다 [Active Directory 응용 프로그램을 만들](data-lake-store-end-user-authenticate-using-active-directory.md)합니다.

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

위의이 조각에 대 한 작업 tooknow 몇:

* hello 자습서를 더 빨리 완료 toohelp,이 코드 조각을 사용 하 여 Azure AD는 기본적으로 모든 Azure 구독에 대해 사용할 수 있는 도메인 및 클라이언트 ID입니다. 따라서 **이 코드 조각을 응용 프로그램에서 있는 그대로 사용**할 수 있습니다.
* 그러나 toouse 자신의 Azure AD 도메인을 선택 하 여 응용 프로그램 클라이언트 ID는 Azure AD 네이티브 응용 프로그램을 만들어야 하 고 사용 하 여 hello Azure AD 테 넌 트 ID, 클라이언트 ID 및 리디렉션 URI hello 응용 프로그램에 대 한 다음 만들었습니다. 지침은 [Data Lake Store를 사용하여 최종 사용자 인증을 위한 Active Directory 응용 프로그램 만들기](data-lake-store-end-user-authenticate-using-active-directory.md)를 참조하세요.

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>클라이언트 암호로 서비스 간 인증을 사용하는 경우
다음 코드 조각 hello tooauthenticate 사용 되는 응용 프로그램 수 **비 대화형**/ hello 클라이언트 암호를 사용 하 여 응용 프로그램 / 서비스 주체에 대 한 키입니다. 기존 Azure AD "Web App" 응용 프로그램과 함께 사용합니다. Toocreate hello Azure AD 웹 응용 프로그램 및 클라이언트 ID와 클라이언트 암호가 hello 조각 아래에 필요한 tooretrieve hello 하는 방법을 참조 하는 방법에 대 한 지침은 [데이터로 서비스 간 인증에 대 한 Active Directory 응용 프로그램 만들기 레이크 저장소](data-lake-store-authenticate-using-active-directory.md)합니다.

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>인증서로 서비스 간 인증을 사용하는 경우

세 번째 옵션을 hello 처럼 다음 코드 조각 수 tooauthenticate 사용 되는 응용 프로그램 **비 대화형**hello 인증서를 사용 하 여 Azure Active Directory 응용 프로그램 / 서비스 보안 주체, 합니다. 이것은 [인증서에서 기존 Azure AD 응용 프로그램](../azure-resource-manager/resource-group-authenticate-service-principal.md)과 함께 사용합니다.

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>클라이언트 개체 만들기
hello 다음 조각에서는 hello 데이터 레이크 저장소 계정 및 파일 시스템 사용 되는 클라이언트 개체 tooissue toohello 서비스를 요청 합니다.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>구독 내 모든 Data Lake Store 계정 나열
hello 다음 코드 조각에서는 특정된 Azure 구독 내에서 모든 데이터 레이크 저장소 계정

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a>디렉터리 만들기
다음 조각과 hello는 `CreateDirectory` 메서드 toocreate 데이터 레이크 저장소 계정 내에서 디렉터리를 사용할 수 있습니다.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>파일 업로드
다음 조각과 hello는 `UploadFile` tooupload를 사용할 수 있는 메서드 tooa 데이터 레이크 저장소 계정 파일입니다.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

hello SDK 재귀 업로드 및 다운로드는 로컬 파일 경로와 데이터 레이크 저장소 파일 경로 지원합니다.    

## <a name="get-file-or-directory-info"></a>파일 또는 디렉터리 정보 가져오기
다음 조각과 hello는 `GetItemInfo` 메서드 데이터 레이크 저장소의 파일 또는 디렉터리를 사용할 수 있는 방법에 대 한 tooretrieve 정보를 사용할 수 있습니다.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>파일 또는 디렉터리 나열
다음 조각과 hello는 `ListItem` toolist hello 파일 및 디렉터리 데이터 레이크 저장소 계정에서 사용할 수 있는 메서드.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>파일 연결
다음 조각과 hello는 `ConcatenateFiles` 메서드 tooconcatenate 파일을 사용 합니다.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Tooa 파일 추가
다음 조각과 hello는 `AppendToFile` 를 사용 하면 데이터 레이크 저장소 계정에 이미 저장 된 데이터 tooa 파일을 추가 합니다.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>파일 다운로드
다음 조각과 hello는 `DownloadFile` toodownload 데이터 레이크 저장소 계정에서 파일을 사용 하는 메서드.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>다음 단계
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [데이터 레이크 저장소와 함께 Azure HDInsight 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Data Lake Store .NET SDK 참조](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Data Lake Store REST 참조](https://msdn.microsoft.com/library/mt693424.aspx)
