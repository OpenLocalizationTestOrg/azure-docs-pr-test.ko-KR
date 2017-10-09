## <a name="configure-your-application-tooaccess-azure-storage"></a>사용자 응용 프로그램 tooaccess Azure 저장소를 구성 합니다.
사용자 응용 프로그램 tooaccess 저장소 서비스는 두 가지 방법으로 tooauthenticate:

* 공유 키: 테스트 목적으로만 공유 키 사용
* 공유 액세스 서명(SAS): 프로덕션 응용 프로그램에 대해 SAS 사용

### <a name="shared-key"></a>공유 키
공유 키 인증에는 응용 프로그램이 계정 이름을 사용 하 고 계정 키 tooaccess 저장소 서비스는 의미 합니다. 신속 하 게 보여 주는의 hello 목적을 위해 어떻게 toouse이이 라이브러리를 사용할 것임이 자습서에서 공유 키 인증 합니다.

> [!WARNING] 
> **테스트 목적으로만 공유 키 인증을 사용합니다.** 모든 읽기/쓰기 액세스 toohello을 제공 하는 사용자 계정 이름 및 계정 키에 연결 된 저장소 계정, 앱을 다운로드 하는 분산된 tooevery 사람 이어야 합니다. 이 방법은 신뢰할 수 없는 클라이언트가 키를 손상시킬 수 있는 위험이 있으므로 좋은 방법은 **아닙니다** .
> 
> 

공유 키 인증을 사용하면 [연결 문자열](../articles/storage/common/storage-configure-connection-string.md)이 만들어집니다. hello 연결 문자열 구성 됩니다.  

* hello **은 DefaultEndpointsProtocol** -HTTP 또는 HTTPS를 선택할 수 있습니다. 그러나 HTTPS를 사용하는 것이 좋습니다.
* hello **계정 이름을** -hello 사용자의 저장소 계정 이름
* hello **계정 키** -hello [Azure 포털](https://portal.azure.com)tooyour 저장소 계정 이동한 hello 클릭 **키** 아이콘 toofind이이 정보입니다.
* (선택 사항) **EndpointSuffix** - Azure 중국 또는 Azure 거버넌스와 같이 다른 끝점 접미사가 붙은 지역의 저장소 서비스에 사용됩니다.

공유 키 인증을 사용하는 연결 문자열의 예는 다음과 같습니다.

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>공유 액세스 서명(SAS)
모바일 응용 프로그램에 대 한 hello Azure 저장소 서비스에 대해 클라이언트에서 요청을 인증에 대 한 메서드를 권장 하는 hello는 공유 액세스 서명 (SAS)를 사용 하는 것입니다. SAS 지정한 사용 권한 집합으로는 시간을 지정 된 기간에 대 한 클라이언트 액세스 tooa 리소스 toogrant를 허용 합니다.
Hello 저장소 계정 소유자로 모바일 클라이언트 tooconsume에 대 한 SAS를 toogenerate가 필요 합니다. toogenerate SAS hello, toowrite hello SAS distributed toobe tooyour 클라이언트를 생성 하는 별도 서비스가 좋을 것입니다. 테스트를 위해 사용할 수 있습니다 hello [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) 또는 hello [Azure 포털](https://portal.azure.com) toogenerate SAS 합니다. Hello SAS를 만들 때 어떤 hello를 통해 SAS 올바른지, hello 시간 간격 및 SAS 권한 부여 toohello 클라이언트 hello hello 권한을 지정할 수 있습니다.

다음 예제는 hello 방법을 toouse hello Microsoft Azure 저장소 탐색기 toogenerate SAS를 보여 줍니다.

1. 아직 없는 경우, [설치 hello Microsoft Azure 저장소 탐색기](http://storageexplorer.com)
2. Tooyour 구독을 연결 합니다.
3. 저장소 계정을 클릭 하 고 왼쪽 아래에 hello에 동작"hello" 탭을 클릭 합니다. 프로그램 SAS에 대 한 "공유 액세스 서명을 가져오기" toogenerate "연결 문자열"를 클릭 합니다.
4. 부여 읽기 및 쓰기 권한이 hello 서비스, 컨테이너 및 개체 수준 hello 저장소 계정의 blob 서비스 hello에 대 한 수준에서 SAS 연결 문자열의 예를 들면 다음과 같습니다.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

위에 표시된 것처럼 SAS을 사용하는 경우, 응용 프로그램에서 계정 키가 노출되지 않습니다. SAS 및 체크 아웃 하 여 SAS를 사용 하기 위한 모범 사례에 대해 알아보십시오 [공유 액세스 서명: hello SAS 모델 이해](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)합니다.

