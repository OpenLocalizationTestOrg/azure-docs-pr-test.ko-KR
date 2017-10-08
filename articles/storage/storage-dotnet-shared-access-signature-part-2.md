---
title: "aaaCreate 공유 액세스 서명 (SAS)를 사용 하 여 Azure Blob 저장소와 | Microsoft Docs"
description: "이 자습서에서는 Blob 저장소를 통해 toocreate 공유 액세스 서명을 사용 하기 위해 방법 등에 tooconsume 클라이언트 응용 프로그램에서 해당 합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>공유 액세스 서명, 2부: Blob 저장소를 사용하여 SAS 만들기 및 사용

[1부](storage-dotnet-shared-access-signature-part-1.md) 에서는 SAS(공유 액세스 서명)에 대해 설명하고 SAS 사용을 위한 모범 사례를 살펴보았습니다. 2 부를 보면 어떻게 toogenerate 하 고 다음 사용 하 여 공유 액세스 서명은 Blob 저장소입니다. hello 예제 C#으로 작성 하 고.NET 용 hello Azure 저장소 클라이언트 라이브러리를 사용 합니다. 이 자습서에서는 예제 hello:

* 컨테이너에서 공유 액세스 서명 생성
* Blob에서 공유 액세스 서명 생성
* 컨테이너의 리소스에 저장 된 액세스 정책 toomanage 서명 만들기
* Hello 공유 액세스 서명을 클라이언트 응용 프로그램 테스트

## <a name="about-this-tutorial"></a>이 자습서 정보
이 자습서에서는 두 개의 콘솔 응용 프로그램을 만들어 컨테이너 및 Blob에 대한 공유 액세스 서명을 만들고 사용하는 방법을 설명합니다.

**응용 프로그램 1**: hello 관리 응용 프로그램입니다. 컨테이너 및 Blob에 대한 공유 액세스 서명을 생성합니다. 소스 코드에 hello 저장소 계정 액세스 키를 포함합니다.

**응용 프로그램 2**: hello 클라이언트 응용 프로그램입니다. 액세스 컨테이너 및 blob 리소스 hello 첫 번째 응용 프로그램을 사용 하 여 만든 hello 공유 액세스 서명을 사용 하 여입니다. 가 사용 하 여만 hello 공유 액세스 서명 tooaccess 컨테이너 및 blob 리소스- *하지* hello 저장소 계정 액세스 키를 포함 합니다.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>1 단계: 콘솔 응용 프로그램 toogenerate 공유 액세스 서명 만들기
먼저,.NET 설치에 대 한 Azure 저장소 클라이언트 라이브러리 hello 있는지 확인 합니다. Hello를 설치할 수 있습니다 [NuGet 패키지](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet 패키지") hello 클라이언트 라이브러리에 대 한 hello 가장 최신 어셈블리를 포함 하 합니다. 이 hello 권장 hello 가장 최근 픽스를 확보 하는 방법입니다. Hello hello 가장 최신 버전의 일부로 hello 클라이언트 라이브러리를 다운로드할 수도 있습니다 [Azure SDK for.NET](https://azure.microsoft.com/downloads/)합니다.

Visual Studio에서 새 Windows 콘솔 응용 프로그램을 만들고 이름을 **GenerateSharedAccessSignatures**로 지정합니다. 참조를 너무 추가[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) 및 [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) hello 다음 방법 중 하나를 사용 하 여:

* 사용 하 여 hello [NuGet 패키지 관리자](https://docs.nuget.org/consume/installing-nuget) Visual Studio에서. **프로젝트** > **NuGet 패키지 관리**를 선택하여 각 패키지(Microsoft.WindowsAzure.ConfigurationManager 및 WindowsAzure.Storage)를 온라인으로 검색하고 설치합니다.
* Hello Azure SDK 설치에서 이러한 어셈블리를 찾아서 toothem 참조 추가 또는:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

Hello Program.cs 파일의 hello 위쪽 hello 다음 추가 **를 사용 하 여** 지시문:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Tooyour 저장소 계정을 가리키는 연결 문자열을 사용 하는 구성 설정 포함 되도록 hello app.config 파일을 편집 합니다. App.config 파일은 유사한 toothis 하나 표시 됩니다.

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>컨테이너에 대한 공유 액세스 서명 URI 생성
와 toobegin, 새 컨테이너에 메서드 toogenerate 공유 액세스 서명을 추가합니다. 이 경우 hello 서명을 저장 된 액세스 정책과 연결 되어 있지 않습니다., 부여 hello 만료 시간 및 hello 사용 권한을 나타내는 URI hello 정보에 전달 하도록 합니다.

먼저 추가 하는 코드 toohello **main ()** 메서드 tooauthenticate tooyour 저장소 계정에 액세스 하 고 새 컨테이너 만들기:

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

다음으로 hello 컨테이너에 대 한 hello 공유 액세스 서명을 생성 하 고 hello 서명 URI를 반환 하는 메서드를 추가 합니다.

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

위의 hello hello 맨 아래에 있는 삼각형 hello 추가 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**, toocall **GetContainerSasUri()** hello 및 서명 URI toohello 콘솔 창:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

컴파일하고 hello 새 컨테이너에 대 한 toooutput hello 공유 액세스 서명 URI를 실행 합니다. hello URI 비슷한 toohello 다음 됩니다.

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Hello 코드를 실행 하면 hello 컨테이너에 대해 만든 hello 공유 액세스 서명을 수 hello에 대 한 유효한 다음 24 시간. hello 서명은 클라이언트 hello 컨테이너와 toowrite 새 blob toohello 컨테이너의 권한 toolist blob을 부여합니다.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Blob에 대한 공유 액세스 서명 URI 생성
다음으로, 비슷한 코드 toocreate hello 컨테이너 내에서 새 blob을 쓰는 하 고 그에 대 한 공유 액세스 서명을 생성 합니다. Hello 시작 시간, 만료 시간 및 사용 권한 정보 hello URI에에서 포함 하도록이 공유 액세스 서명을 저장 된 액세스 정책과 연결 되지 않습니다.

새 메서드를 추가 새 blob을 만듭니다 및 일부 텍스트 tooit 작성 한 다음 공유 액세스 서명을 생성 hello 서명 URI를 반환 합니다.

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Hello hello 맨 아래에 **main ()** 메서드를 다음 줄 toocall hello 추가 **GetBlobSasUri()**hello 너무 호출 전에,**console.readline ()**를 공유 하는 hello 및 액세스 서명 URI toohello 콘솔 창:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

컴파일하고 hello 새 blob에 대 한 toooutput hello 공유 액세스 서명 URI를 실행 합니다. hello URI 비슷한 toohello 다음 됩니다.

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Hello 컨테이너에 저장 된 액세스 정책 만들기
이제 연결 된 모든 공유 액세스 서명에 대 한 hello 제약 조건을 정의 하는 hello 컨테이너에 저장된 된 액세스 정책을 만들어 보겠습니다.

Hello 이전 예제의 (암시적 또는 명시적) hello 시작 시간 지정, hello 만료 시간 및 hello에 대 한 hello 권한을 공유 액세스 서명 URI 자체입니다. 다음 예제는 hello, 이러한 hello 공유 액세스 서명을 아니라 hello 저장 된 액세스 정책에 지정 합니다. 이렇게 하면 우리 toochange hello를 다시 발급 하지 않고도 이러한 제약 조건을 공유 서명에 액세스 합니다.

Hello 공유 액세스 서명에 대 한 hello 제약 조건 및 hello 나머지 hello 저장 된 액세스 정책에서 하나 이상의 가능한 toohave 것합니다. 그러나 hello 시작 시간, 만료 시간 및 권한을 한 위치 또는 다른 hello에만 지정할 수 있습니다. 예를 들어 hello 공유 액세스 서명에서 사용 권한을 지정 하 고 hello 저장 된 액세스 정책에서 지정할 수도 없습니다.

저장 된 액세스 정책 tooa 컨테이너를 추가 하면 기존 사용 권한을 가지 hello 컨테이너, hello 새 액세스 정책 추가 하며 다음 hello 컨테이너의 사용 권한을 설정 합니다.

컨테이너에 새 저장 된 액세스 정책을 만들고 hello 정책 hello 이름을 반환 하는 새 메서드를 추가 합니다.

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

Hello hello 맨 아래에 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**다음 hello toofirst 지우기 모든 기존 액세스 정책을 줄을 추가 하 고, 다음 호출 hello  **CreateSharedAccessPolicy()** 메서드:

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

컨테이너에서 hello 액세스 정책을 선택을 취소 하면 먼저 hello 컨테이너의 기존 사용 권한을 다음 지우기 hello 사용 권한을 가져올 하십시오 hello 권한을 다시 설정 합니다.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>공유 액세스 서명 URI에 대 한 액세스 정책을 사용 하는 hello 컨테이너 생성
다음으로, 앞에서 만든 hello 컨테이너에 대 한 다른 공유 액세스 서명을 만듭니다 하지만이 이번 म hello 서명을와 연결 hello 이전 예제에서 만든 hello 저장 된 액세스 정책.

새 메서드 toogenerate hello 컨테이너에 대 한 다른 공유 액세스 서명을 추가 합니다.

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Hello hello 맨 아래에 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**, 다음 줄 toocall hello hello 추가 **GetContainerSasUriWithPolicy** 메서드 :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>액세스 정책에 Blob을 사용 하는 hello는 공유 액세스 서명 URI 생성
마지막으로, 비슷한 메서드 toocreate 다른 blob을 추가 하 고 저장 된 액세스 정책은 연관 된 공유 액세스 서명을 생성 합니다.

새 메서드 toocreate blob을 추가 하 고 공유 액세스 서명을 생성 합니다.

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Hello hello 맨 아래에 **main ()** 메서드를 hello 너무 호출 전에**console.readline ()**, 다음 줄 toocall hello hello 추가 **GetBlobSasUriWithPolicy** 메서드:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

hello **main ()** 메서드는 이제 한 번에 다음과 같이 표시 됩니다. Toowrite hello 공유 액세스 서명 Uri toohello 콘솔 창 실행 복사 및 hello이이 자습서의 두 번째 부분에서 사용 하기 위해 텍스트 파일에 붙여 넣습니다.

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

Hello GenerateSharedAccessSignatures 콘솔 응용 프로그램을 실행 하면 유사한 toohello 다음 출력이 표시 됩니다. 이들은 hello 자습서의 2 부에에서는 사용 하 여 hello 공유 액세스 서명입니다.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>2 단계: 콘솔 응용 프로그램 tootest hello 공유 액세스 서명 만들기
tootest hello 공유 액세스 서명을 hello 이전 예제에서 만든, blob 및 hello 컨테이너에서 hello 서명 tooperform 작업을 사용 하는 두 번째 콘솔 응용 프로그램을 만듭니다.

> [!NOTE]
> Hello hello 자습서의 첫 번째 단계를 완료 후 24 시간 이상 경과할 hello 서명을 생성 하는 더 이상 유효 하지 합니다. 이 경우 hello hello 자습서의 두 번째 부분에서 사용 하기 위해 새 공유 액세스 서명을 hello 첫 번째 콘솔 응용 프로그램 toogenerate에 hello 코드를 실행 해야 있습니다.
>

Visual Studio에서 새 Windows 콘솔 응용 프로그램을 만들고 이름을 **ConsumeSharedAccessSignatures**로 지정합니다. 참조를 너무 추가[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) 및 [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/)위에서 설명한 것 처럼, 합니다.

Hello Program.cs 파일의 hello 위쪽 hello 다음 추가 **를 사용 하 여** 지시문:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Hello의 hello 본문에서 **main ()** 메서드를 추가 hello 문자열 상수 뒤, hello 자습서의 1 단계에서 생성 한 해당 값 toohello 공유 액세스 서명을 변경 합니다.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>공유 액세스 서명을 사용 하 여 지정 하 여 메서드 tootry 컨테이너 작업 추가
다음으로 hello 컨테이너에 대 한 공유 액세스 서명을 사용 하 여 일부 컨테이너 작업을 테스트 하는 메서드를 추가 합니다. hello 공유 액세스 서명을 사용 하는 tooreturn 단독 hello 서명 기반의 액세스 toohello 컨테이너를 인증 하는 참조 toohello 컨테이너입니다.

다음 메서드 tooProgram.cs hello를 추가 합니다.

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

업데이트 hello **main ()** 메서드 toocall **UseContainerSAS()** hello를 모두 사용 하 여 공유 액세스 서명 hello 컨테이너에서 만든:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>공유 액세스 서명을 사용 하는 메서드 tootry blob 작업 추가
마지막으로, 공유 액세스 서명을 사용 하 여 hello blob에서 일부 blob 작업을 테스트 하는 메서드를 추가 합니다. 이 경우 hello 생성자 사용 **CloudBlockBlob(String)**tooreturn 참조 toohello blob, 공유 액세스 서명을 hello에 전달 합니다. 다른 인증이 필요 하지 않습니다. hello 시그니처 만으로는 기반으로 합니다.

다음 메서드 tooProgram.cs hello를 추가 합니다.

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

업데이트 hello **main ()** 메서드 toocall **UseBlobSAS()** hello를 모두 사용 하 여 공유 hello blob에 만든 액세스 서명:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

Hello 콘솔 응용 프로그램을 실행 하 고 hello 출력 toosee 어떤 서명에 대 한 허용 되는 작업을 관찰 합니다. hello 콘솔 창의 hello 출력에는 비슷한 toohello 다음 표시 됩니다.

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>다음 단계

* [이해 hello 공유 액세스 서명, 1 부: SAS 모델](storage-dotnet-shared-access-signature-part-1.md)
* [익명 읽기 권한을 toocontainers 및 blob 관리](storage-manage-access-to-resources.md)
* [공유 액세스 서명을 사용하여 액세스 위임(REST API)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [테이블 및 큐 SAS 소개](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
