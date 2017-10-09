---
title: "사용자 지정 Java 웹 응용 프로그램 tooAzure aaaUpload"
description: "이 자습서에서는 어떻게 tooupload 사용자 지정 Java 웹 응용 프로그램 tooAzure 앱 서비스 웹 앱입니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a>사용자 지정 Java 웹 응용 프로그램 tooAzure 업로드
이 항목에서는 방법을 tooupload 사용자 지정 Java 웹 앱 너무 설명[Azure 앱 서비스] 웹 앱입니다. Tooany Java 웹 사이트 또는 웹 응용 프로그램 및 특정 응용 프로그램에 대 한 몇 가지 예제에도 적용 되는 정보는 포함 되어 있습니다.

Azure에서는 hello Azure 포털의 구성 UI를 사용 하 여 Java 웹 앱을 만들기 위한 수단을 제공 하 고 설명에 따라 Azure 마켓플레이스 hello [Azure 앱 서비스에서 Java 웹 앱을 만들](web-sites-java-get-started.md)합니다. 시나리오를 또는 하지 않는 toouse hello Azure 포털 구성 UI를 원하는 Azure 마켓플레이스 hello에 대 한이 자습서가입니다.  

## <a name="configuration-guidelines"></a>구성 지침
hello 다음에는 Azure에서 사용자 지정 Java 웹 앱에 대 한 예상 하는 hello 설정을 설명 합니다.

* hello Java 프로세스에서 사용 하는 hello HTTP 포트를 동적으로 할당 됩니다.  hello 프로세스 hello 환경 변수에서 hello 포트를 사용 해야 `HTTP_PLATFORM_PORT`합니다.
* 모든 단일 HTTP 수신기 hello 않도록 것과 다른 포트를 수신 합니다.  Tomcat에서 포함 된 hello 종료, HTTPS 및 AJP 포트입니다.
* hello 컨테이너 toobe IPv4 트래픽에 대해서만 구성 해야 합니다.
* hello **시작** hello 응용 프로그램 요구 toobe에 명령 hello 구성에서 설정 합니다.
* 사용 하 여 디렉터리 쓰기 권한이 필요한 응용 프로그램에 필요한 toobe는 hello Azure 웹 앱의 콘텐츠 디렉터리에 **D:\home**합니다.  환경 변수 hello `HOME` tooD:\home 참조 합니다.  

필요에 따라 hello web.config 파일에서 환경 변수를 설정할 수 있습니다.

## <a name="webconfig-httpplatform-configuration"></a>web.config httpPlatform 구성
hello 다음 설명 hello **httpPlatform** web.config 내의 형식입니다.

**arguments** (기본값 = ""). Hello에 지정 된 스크립트 또는 실행 가능한 인수 toohello **processPath** 설정 합니다.

예제( **processPath** 도 함께 표시):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -실행 파일 경로 toohello 또는 HTTP 요청을 수신 하는 프로세스를 시작 하는 스크립트입니다.

예제:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute**(기본값 = 10). 시간에 지정 된 hello 프로세스 **processPath** 분당 toocrash ï ´ ù. 이 제한을 초과 하는 경우 **HttpPlatformHandler** 는 hello 분의 나머지 부분에서는 hello에 대 한 hello 프로세스 시작을 중지 합니다.

**requestTimeout**(기본값 = "00:02:00"). 기간 **HttpPlatformHandler** 수신 hello 프로세스에서 응답을 받기 위해 대기 `%HTTP_PLATFORM_PORT%`합니다.

**startupRetryCount**(기본값 = 10). 횟수 **HttpPlatformHandler** toolaunch hello 프로세스에 지정 된 시도 **processPath**합니다. 자세한 내용은 **startupTimeLimit** 를 참조하세요.

**startupTimeLimit**(기본값 = 10초). 기간 **HttpPlatformHandler** hello 포트에서 수신 하는 프로세스가 실행/스크립팅 toostart hello에 대 한 대기 합니다.  이 시간 제한을 초과 하는 경우 **HttpPlatformHandler** hello 프로세스 종료 되며 toolaunch 시도 다시 **startupRetryCount** 시간입니다.

**stdoutLogEnabled**(기본값 = "true"). True 이면 **stdout** 및 **stderr** hello에 지정 된 hello 프로세스에 대 한 **processPath** 설정에 지정 된 리디렉션된 toohello 파일 됩니다  **가 stdoutLogFile** (참조 **가 stdoutLogFile** 섹션).

**stdoutLogFile**(기본값 = "d:\home\LogFiles\httpPlatformStdout.log"). 절대 파일 경로 **stdout** 및 **stderr** 에 지정 된 hello 프로세스에서 **processPath** 기록 됩니다.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`일부로 toospecified는 특수 한 자리 표시자 **인수** 또는 hello의 일부로 **httpPlatform** **environmentVariables** 목록입니다. 여는 내부적으로 생성 된 포트에 의해 대체 됩니다 **HttpPlatformHandler** hello 프로세스에서 지정 하는 **processPath** 이 포트에서 수신할 수 있습니다.
> 
> 

## <a name="deployment"></a>배포
Hello 인터넷 정보 서비스 (IIS) 기반 웹 응용 프로그램에 사용 되는 대부분의 동일한 것을 의미 하는 hello 통해 Java 기반 웹 응용 프로그램을 쉽게 배포할 수 있습니다.  FTP, Git 및 Kudu는 모든 지원 배포 메커니즘으로 웹 앱에 대 한 통합 된 SCM 기능 hello 됩니다. WebDeploy는 프로토콜로 작동하지만 Visual Studio에서 Java를 개발하지 않으므로 WebDeploy는 Java 웹 앱 배포 사용 사례로 적합하지 않습니다.

## <a name="application-configuration-examples"></a>응용 프로그램 구성 예제
다음 응용 프로그램, web.config 파일 및 hello hello에 대 한 응용 프로그램 구성으로 제공 되 예제 tooshow 어떻게 tooenable 앱 서비스 웹 앱에서 Java 응용 프로그램입니다.

### <a name="tomcat"></a>Tomcat
앱 서비스 웹 앱에 제공 되는 Tomcat에 두 가지 변형이 인 것은 여전히 가능성이 높으며 tooupload 고객 특정 인스턴스 합니다. 다음은 다른 JVM(Java Virtual Machine)으로 Tomcat을 설치한 예제입니다.

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

Tomcat 쪽 hello에 몇 가지 구성 변경 내용을 toobe 내용이 나와 있습니다. hello server.xml 편집할 toobe tooset 항목이 필요합니다.

* 종료 포트 = -1
* HTTP 커넥터 포트 = ${port.http}
* HTTP 커넥터 주소 = "127.0.0.1"
* HTTPS 및 AJP 커넥터를 주석으로 처리
* hello IPv4 설정은 추가할 수 있는 hello catalina.properties 파일에서 설정할 수도 있습니다.`java.net.preferIPv4Stack=true`

Direct3d 호출은 앱 서비스 웹 앱에서 지원되지 않습니다. 다음 Java 옵션 응용 프로그램이 이러한 호출을 수행 해야 하는 hello를 추가, toodisable 합니다.`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Tomcat 용 hello 경우, 마찬가지로 고객 Jetty에 대 한 자신의 인스턴스를 업로드할 수 있습니다. 실행 중인 hello는 Jetty의 전체 설치의 경우 hello hello 구성은 다음과 같습니다.

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

hello Jetty 구성이 필요한 hello start.ini tooset에서 변경 toobe `java.net.preferIPv4Stack=true`합니다.

### <a name="springboot"></a>Springboot
순서 tooget 실행 중인 Springboot 응용 프로그램에서에서 JAR 또는 WAR 파일 tooupload 필요 하 고 hello 다음 web.config 파일을 추가 합니다. hello web.config 파일의 hello wwwroot 폴더로 이동 합니다. Hello에도 hello wwwroot 폴더에 있는 다음 예제에서는 hello JAR 파일을 hello web.config에서 hello 인수 toopoint tooyour JAR 파일을 조정 합니다.  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a>Hudson
테스트를 사용 하 여 Hudson 3.1.2 전쟁 hello 및 기본 Tomcat 7.0.50 인스턴스 hello hello UI tooset 작업 사용 하지 않은 상태입니다.  이 권장된 tooinstall 변수가 Hudson 소프트웨어 빌드 도구 이므로 여기서 hello 인스턴스 전용에 **AlwaysOn** hello 웹 앱에 플래그를 설정할 수 있습니다.

1. **d:\home\site\wwwroot**와 같이 웹앱의 루트 디렉토리에서 **webapps** 디렉토리를 만들고(디렉토리가 없는 경우), Hudson.war을 **d:\home\site\wwwroot\webapps**에 저장합니다.
2. Apache Maven 3.0.5(Hudson과 호환됨)를 다운로드하여 **d:\home\site\wwwroot**에 저장합니다.
3. Web.config에서 만들 **d:\home\site\wwwroot** 붙여넣기 hello 내용을 따라:
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    이 시점에서 hello 웹 응용 프로그램 다시 시작된 tootake hello 변경 될 수 있습니다.  Toohttp://yourwebapp/hudson toostart Hudson을 연결 합니다.
4. Hudson 자체 구성 후 다음 화면 hello를 표시 되어야 합니다.
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. 액세스 hello Hudson 구성 페이지: 클릭 **관리 Hudson**, 클릭 하 고 **시스템 구성**합니다.
6. Hello JDK 아래와 같이 구성 합니다.
   
    ![Hudson 구성](./media/web-sites-java-custom-upload/hudson2.png)
7. 아래와 같이 Maven을 구성합니다.
   
    ![Maven 구성](./media/web-sites-java-custom-upload/maven.png)
8. Hello 설정을 저장 합니다. Hudson을 구성하였으므로 이제 사용할 준비가 되었습니다.

Hudson에 대한 자세한 내용은 [http://hudson-ci.org](http://hudson-ci.org)를 참조하십시오.

### <a name="liferay"></a>Liferay
Liferay는 앱 서비스 웹 앱에서 지원됩니다. Liferay 중요 한 메모리를 요구할 수, 중형 또는 대형 전용된 작업자에 충분 한 메모리를 제공할 수 있는에 toorun hello 웹 앱 필요 합니다. 또한 Liferay 몇 분 toostart를 사용합니다. 따라서 것이 좋습니다 너무 hello 웹 앱 설정**Always On**합니다.  

Tomcat으로 Liferay Community Edition GA3 bundled 6.1.2를 사용 하 여, hello 다음 파일 편집 되었습니다 Liferay 다운로드 한 후:

**Server.xml**

* 종료 포트 너무-1을 변경 합니다.
* HTTP 커넥터에도 변경`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* 주석 hello AJP 커넥터 처리 합니다.

Hello에 **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** 폴더 라는 파일을 만들어 **포털 ext.properties**합니다. 다음과 같이이 파일 toocontain 한 줄을 해야 합니다.

    liferay.home=%HOME%/site/wwwroot/liferay

Hello tomcat 7.0.40 폴더와 같은 디렉터리 수준에서 hello 라는 파일을 만들어 **web.config** 콘텐츠를 다음 hello로:

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

Hello에서 **httpPlatform** 차단 hello **requestTimeout** 너무 설정 된 "00: 10:00"입니다.  줄일 수 있습니다 하지만 다음 가능성이 toosee 하는 동안 시간 초과 오류 일부 Liferay 부트스트래핑 됩니다.  이 값을 변경 하는 경우 다음 hello **connectionTimeout** hello tomcat에서 server.xml 스페이스도 수정 해야 합니다.  

해당 hello JRE_HOME 환경 varariable web.config toopoint toohello 위에 hello에 지정 된 주목할 64 비트 JDK. hello 기본값은 32 비트 이지만 toouse 좋습니다 Liferay 높은 수준의 메모리 필요할 수 있습니다, 때문 hello 64 비트 JDK.

이러한 내용을 변경하면 Liferay를 실행하는 웹앱을 다시 시작한 후 http://yourwebapp을 엽니다. hello Liferay 포털을 hello 웹 응용 프로그램 루트에서 사용할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
Liferay에 대한 자세한 내용은 [http://www.liferay.com](http://www.liferay.com)을 참조하세요.

Java에 대한 자세한 내용은 [Java 개발자용 Azure](/java/azure)를 참조하세요.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure 앱 서비스]: http://go.microsoft.com/fwlink/?LinkId=529714
