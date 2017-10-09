저장소 에뮬레이터 hello 공유 키 인증에 대 한 단일 고정 계정과 잘 알려진 인증 키를 지원합니다. 이 계정과 키는 hello만 공유 된 키 자격 증명 hello 저장소 에뮬레이터와 함께 사용 하기 위해 허용. 아래에 이 계정과 키의 예제가 나와 있습니다.

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> 클라이언트 인증 코드의 테스트 hello 기능에 대해서만 hello 인증 키 hello 저장소 에뮬레이터에서 지원 됩니다. 보안 기능은 제공하지 않습니다. Hello 저장소 에뮬레이터와 함께 프로덕션 저장소 계정 및 키를 사용할 수 없습니다. 하지 프로덕션 데이터와 함께 hello 개발 계정을 사용 해야 합니다.
> 
> hello 저장소 에뮬레이터만 HTTP 통해 연결을 지원합니다. 그러나 HTTPS는 hello 프로토콜 프로덕션 Azure 저장소 계정 리소스에 액세스 하기 위한 것이 좋습니다.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>바로 가기를 사용 하 여 toohello 에뮬레이터 계정을 연결 하세요.
hello 가장 쉬운 방법은 tooconnect toohello 저장소 에뮬레이터에서 응용 프로그램은 tooconfigure hello 바로 가기 참조 하는 응용 프로그램 구성 파일에서 연결 문자열을 `UseDevelopmentStorage=true`합니다. 연결 문자열 toohello 저장소 에뮬레이터의 예로 *app.config* 파일: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Hello 잘 알려진 계정 이름과 키를 사용 하 여 toohello 에뮬레이터 계정을 연결 하세요.
toocreate 참조 hello 에뮬레이터 계정 이름 및 키를 지정 해야 hello 끝점 서비스를 각각 hello에 대 한 연결 문자열 hello 연결 문자열에 hello 에뮬레이터에서 toouse를 선택 합니다. 이 소프트웨어는 hello 연결 문자열은 프로덕션 저장소 계정에 대 한 것과 다른 hello 에뮬레이터 끝점 참조를 필요 합니다. 예를 들어 연결 문자열의 hello 값은 다음과 같이 표시 됩니다.

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

이 값은 위에 표시 된 동일 toohello 바로 가기 `UseDevelopmentStorage=true`합니다.

#### <a name="specify-an-http-proxy"></a>HTTP 프록시 지정
Hello 저장소 에뮬레이터에 대 한 서비스를 테스트할 때 HTTP 프록시 toouse를 지정할 수도 있습니다. 이 hello 저장소 서비스에 대 한 작업을 디버깅 하는 동안 HTTP 요청 및 응답을 관찰 하는 데 유용할 수 있습니다. 프록시, toospecify 추가 hello `DevelopmentStorageProxyUri` toohello 연결 문자열 옵션 및 해당 값 toohello 프록시 URI를 설정 합니다. 예를 들어 다음은 toohello 저장소 에뮬레이터를 가리키고 HTTP 프록시를 구성 하는 연결 문자열이입니다.

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

