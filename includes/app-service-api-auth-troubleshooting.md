Hello 시간 인증 오류는 대부분 올바르지 않거나 일치 하지 않는 구성 설정에서 발생 합니다. 다음은 작업 toocheck에 대 한 몇 가지 특정 제안 사항입니다.

* Hello를 누락 하지 않은 확인 **저장** 원격 단추입니다. 이 문제는 주로 쉽게 toodo 및 hello 결과 포털 페이지에 올바른 값이 hello 기대 하지만 hello Azure 환경 또는 Azure AD 응용 프로그램에 저장 되지 않은 실제로 합니다.
* Hello에 구성 된 설정에 대 한 **응용 프로그램 설정** hello Azure 포털의 블레이드에서 있는지 확인 hello 설정을 입력 된 때 API 앱 또는 웹 앱 선택 된 올바른 hello에 해당 합니다.  또한 hello 설정으로 입력 된 있는지를 확인 **앱 설정** 아닌 **연결 문자열**처럼 hello 두 섹션의 hello 형식은 유사 합니다.
* 인증 tooa JavaScript 프런트 엔드에 대 한 다운로드 hello 매니페스트 다시 tooverify는 `oauth2AllowImplicitFlow` 너무 변경 되었습니다`true`합니다.
* 다음에서 URL을 구성하는 데 HTTPS를 사용했는지 확인합니다.
  
  * 프로젝트 코드
  * CORS
  * 각 API 앱 및 웹앱에 대한 Azure 환경 앱 설정
  * Azure AD 응용 프로그램 설정
    
    Hello 포털에서 API 앱의 URL을 복사 하는 경우 종종은 `http://` toomanually 속성을 변경할 수 있으며`https://`합니다.
* 모든 코드 변경이 성공적으로 배포되었는지 확인합니다. 예를 들어, 다중 프로젝트 솔루션에서 프로젝트 코드 및 실수로 중 하나를 선택 hello 다른 toodeploy hello 변경 하려는 경우 가능한 toochange입니다.
* HTTP Url 하지 브라우저에서 Url tooHTTPS 것 있는지 확인 합니다. 기본적으로 Visual Studio는 다음과 같이 생성 됩니다. HTTP Url을 사용 하 여 프로필 게시 되며 여기에 프로젝트를 배포한 후 hello 브라우저에서 열립니다.
* 인증 tooa JavaScript 프런트 엔드에 대 한 CORS hello JavaScript 코드를 호출 하는 hello API 앱에 올바르게 구성 되어 있는지 확인 합니다. 시도 hello 문제는 CORS 관련 의문이 있는 경우 "*"으로 hello 원본 URL을 허용 합니다. 
* JavaScript 프런트 엔드에 대 한 브라우저의 개발자 도구 콘솔 탭 tooget 자세한 오류 정보를 열고 네트워크 hello에 HTTP 요청을 검사 합니다. 그러나 콘솔 오류 메시지가 잘못될 수 있습니다. CORS 오류를 나타내는 메시지가, 인증 hello 실제 문제가 될 수 있습니다. 인증을 일시적으로 일시적으로 사용할 hello 응용 프로그램을 실행 하 여 hello 경우가는 확인할 수 있습니다.
* .NET API 앱에 대 한 확인을 설정 하 여 가능한 한 많은 정보 오류 메시지에 수신 된 [customErrors 모드 tooOff](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview)합니다.
* .NET API 앱에 대 한 시작는 [원격 디버깅 세션](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), 전달자 토큰 또는 예상 hello 서비스 보안 주체 ID에 대 한 클레임을 확인 하는 코드 hello tooacquire ADAL을 사용 하 여 toocode 전달 되는 hello 변수 값을 검토 하 고 이러한 방식으로 가능한 toofind 예기치 않은 문제는 코드 많은 다양 한 원본에서 구성 값을 선택할 수는 참고 사항 예를 들어를 잘못 입력 했거나 `ida:ClientId` 으로 `ida:ClientID` Azure 앱 서비스 환경 설정의 구성할 때 hello 코드 hello 표시 될 수 `ida:ClientId` hello Azure 앱 서비스 설정을 무시 하 고 hello Web.config 파일에서 찾을 값입니다. 
* 일반 Internet Explorer 창에서 작동하지 않으면 기존 로그인이 방해가 될 수 있으니 InPrivate을 시도하고 Chrome 또는 Firefox를 시도해 보세요.

