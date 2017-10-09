## <a name="set-up-your-development-environment"></a>개발 환경 설정
이 가이드의 준비 tootry hello 코드 예제에서는 하므로 다음으로 Visual Studio에서 개발 환경을 설정.

### <a name="create-a-windows-console-application-project"></a>Windows 콘솔 응용 프로그램 프로젝트 만들기
Visual Studio에서 새로운 Windows 콘솔 응용 프로그램을 만듭니다. 그러나 단계를 수행 하는 hello 어떻게 toocreate 2017 년 hello 단계 Visual Studio에서 콘솔 응용 프로그램은 다른 버전의 Visual Studio와 비슷한 보여 줍니다.

1. **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
2. **설치됨** > **템플릿** > **Visual C#** > **Windows 기본 바탕 화면**을 선택합니다.
3. **콘솔 앱(.NET Framework)**를 선택합니다.
4. Hello에 응용 프로그램에 대 한 이름을 입력 **이름:** 필드
5. **확인**을 선택합니다.

![Visual Studio의 프로젝트 생성 대화 상자](./media/storage-development-environment-include/storage-development-environment-include-1.png)

이 자습서의 모든 코드 예제를 추가할 수 있습니다 toohello `Main()` 콘솔 응용 프로그램의 메서드에 `Program.cs` 파일입니다.

Azure 클라우드 서비스 또는 웹 앱을 포함 하 여.NET 응용 프로그램 및 데스크톱 및 모바일 응용 프로그램의 종류에 hello Azure 저장소 클라이언트 라이브러리를 사용할 수 있습니다. 이 가이드에서는 편의상 콘솔 응용 프로그램을 사용합니다.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>NuGet tooinstall hello 필요한 패키지를 사용 하 여
Tooreference에에서 필요한 프로젝트 toocomplete이 자습서이에서는 두 개의 패키지가 있습니다.

* [.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/):이 패키지 toodata 리소스 저장소 계정에 프로그래밍 방식의 액세스를 제공 합니다.
* [.NET용 Microsoft Azure 구성 관리자 라이브러리](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): 이 패키지는 응용 프로그램을 실행하는 위치에 관계없이 구성 파일에서 연결 문자열을 구문 분석하기 위한 클래스를 제공합니다.

Tooobtain NuGet 패키지를 모두 사용할 수 있습니다. 다음 단계를 수행하세요.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.
2. "WindowsAzure.Storage" 온라인 검색 하 고 클릭 **설치** tooinstall hello 저장소 클라이언트 라이브러리 및 해당 종속성.
3. "WindowsAzure.ConfigurationManager" 온라인 검색 하 고 클릭 **설치** tooinstall hello Azure 구성 관리자.

> [!NOTE]
> hello에 hello 저장소 클라이언트 라이브러리 패키지도 포함 되어 [Azure SDK for.NET](https://azure.microsoft.com/downloads/)합니다. 그러나 hello 클라이언트 라이브러리의 최신 버전 hello 항상 있는지 NuGet tooensure에서 hello 저장소 클라이언트 라이브러리도 설치 하는 것이 좋습니다.
> 
> hello.NET 용 저장소 클라이언트 라이브러리의에서 ODataLib 종속성 hello WCF 데이터 서비스에서가 아니라 NuGet에 사용할 수 있는 hello ODataLib 패키지에 의해 확인 됩니다. hello ODataLib 라이브러리 직접 다운로드 하거나 NuGet 통해 코드 프로젝트에서 참조 될 수 있습니다. hello 저장소 클라이언트 라이브러리에서 사용 하는 hello 해당 ODataLib 패키지는 [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), 및 [공간](http://nuget.org/packages/System.Spatial/)합니다. 이러한 라이브러리는 hello Azure 테이블 저장소 클래스에 의해 사용 되지만, 이들은 hello 저장소 클라이언트 라이브러리를 사용 하 여 프로그래밍에 대 한 필수 종속성입니다.
> 
> 

### <a name="determine-your-target-environment"></a>대상 환경 확인
이 가이드에서 hello 예제를 실행 하기 위한 두 개의 환경 옵션을 선택할:

* Hello 클라우드에서 Azure 저장소 계정에 대 한 코드를 실행할 수 있습니다. 
* Hello Azure 저장소 에뮬레이터에 대 한 코드를 실행할 수 있습니다. hello 저장소 에뮬레이터는 hello 클라우드에서 Azure 저장소 계정이 에뮬레이트하는 로컬 환경입니다. hello 에뮬레이터는 테스트 및 응용 프로그램을 개발 하는 동안 코드를 디버깅에 대 한 무료 옵션입니다. hello 에뮬레이터는 잘 알려진 계정 및 키를 사용합니다. 자세한 내용은 참조 [사용 하 여 hello 개발 및 테스트에 Azure 저장소 에뮬레이터](../articles/storage/common/storage-use-emulator.md)

Hello 클라우드에서 저장소 계정을 대상으로 하는 경우 hello Azure 포털에서에서 저장소 계정에 대 한 hello 기본 액세스 키를 복사 합니다. 자세한 내용은 [저장소 액세스 키 보기 및 복사](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)를 참조하세요.

> [!NOTE]
> Hello Azure 저장소와 관련 된 모든 비용을 발생 시 키 지는 저장소 에뮬레이터 tooavoid를 대상으로 지정할 수 있습니다. 그러나 hello 클라우드에서 tootarget를 Azure 저장소 계정을 선택 수행 하면,이 자습서를 수행 하기 위한 비용 무시할 수 있다는 됩니다.
> 
> 

### <a name="configure-your-storage-connection-string"></a>저장소 연결 문자열 구성
.NET 용 Azure 저장소 클라이언트 라이브러리 hello 저장소 연결 문자열 tooconfigure 끝점을 사용 하 여 지원 및 저장소 서비스에 액세스 하기 위한 자격 증명입니다. 구성 파일에 가장 좋은 방법은 toomaintain hello 저장소 연결 문자열은 

연결 문자열에 대 한 자세한 내용은 참조 [연결 문자열 tooAzure 저장소 구성](../articles/storage/common/storage-configure-connection-string.md)합니다.

> [!NOTE]
> 저장소 계정 키에는 저장소 계정에 대 한 유사한 toohello 루트 암호입니다. 항상 주의 tooprotect를 저장소 계정 키 여야합니다. 사용자 tooother tooothers 액세스할 수 있는 일반 텍스트 파일에 저장 하거나 하드 코딩을 배포 하지 마십시오. 노출 되었다고 판단 되 면 hello Azure 포털을 사용 하 여 키를 다시 생성 합니다.
> 
> 

tooconfigure 연결 문자열, 열기 hello `app.config` Visual Studio의 솔루션 탐색기에서 파일입니다. Hello의 hello 내용을 추가 `<appSettings>` 요소 아래에 표시 합니다. 대체 `account-name` hello 저장소 계정의 이름으로 및 `account-key` 계정 액세스 키로:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

예를 들어, 구성 설정은 다음과 유사하게 표시됩니다.

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

tootarget hello 저장소 에뮬레이터 toohello 잘 알려진 계정 이름과 키를 매핑하는 바로 가기를 사용할 수 있습니다. 이 경우에 연결 문자열 설정은 다음과 같습니다.

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

