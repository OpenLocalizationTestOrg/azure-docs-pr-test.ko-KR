hello [.NET 용 Microsoft Azure 구성 관리자 라이브러리](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) 구성 파일에서 연결 문자열을 구문 분석 하기 위한 클래스를 제공 합니다. hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) 클래스에는 Azure 클라우드 서비스 또는 Azure 가상 컴퓨터에 모바일 장치에서 hello 바탕 화면에서 hello 클라이언트 응용 프로그램의 실행 여부에 관계 없이 구성 설정을 구문 분석 합니다.

tooreference CloudConfigurationManager 패키지 hello, hello 다음 추가 `using` 지시문:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

어떻게 tooretrieve는 연결 문자열을 구성 파일에서 보여 주는 예제는 다음과 같습니다.

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

Hello Azure 구성 관리자를 사용 하는 것은 선택 사항입니다. .NET Framework의 hello와 같은 API를 사용할 수도 있습니다 [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) 클래스입니다.

