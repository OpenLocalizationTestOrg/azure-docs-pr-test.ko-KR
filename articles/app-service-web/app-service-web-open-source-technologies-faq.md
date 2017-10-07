---
title: "웹 앱 aaaOpen 소스 기술을 Azure에 대 한 Faq | Microsoft Docs"
description: "Azure 앱 서비스의 웹 응용 프로그램 기능 hello의에서 오픈 소스 기술에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Azure Web Apps에 대한 오픈 소스 기술 FAQ

이 문서는 오픈 소스 기술을 hello에 대 한 문제에 대 한 질문과 대답 (Faq) 답변 toofrequently 되어 [Azure 앱 서비스의 웹 응용 프로그램 기능](https://azure.microsoft.com/services/app-service/web/)합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>내 ClearDB 데이터베이스가 다운되었습니다. 이 문제를 해결하려면 어떻게 해야 하나요?

데이터베이스 관련 문제에 대해서는 [ClearDB 지원](https://www.cleardb.com/developers/help/support)에 문의하세요. 

ClearDB에 대 한 대답 toocommon 질문에 대 한 참조 [ClearDB Faq](https://docs.microsoft.com/azure/store-cleardb-faq/)합니다.

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>ClearDB 데이터베이스 hello 포털에 나열 되지 않은 이유는?

Hello에 ClearDB 데이터베이스를 만들 경우 [Azure 포털](http://portal.azure.com/), hello 데이터베이스 hello에 표시 되지 않으면 [Azure 클래식 포털](http://manage.windowsazure.com/)합니다. 이 문제를 해결할 toowork, 데이터베이스 toohello 웹 앱을 수동으로 연결할 수 있습니다.

마찬가지로, hello에 ClearDB 데이터베이스를 만들 경우 [Azure 클래식 포털](http://manage.windowsazure.com/), 데이터베이스 hello에 표시 되지 않습니다 [Azure 포털](http://portal.azure.com/)합니다. 이 경우 해결 방법이 없습니다. 

자세한 내용은 [Azure App Service를 사용하는 ClearDB MySQLl 데이터베이스에 대한 FAQ](https://docs.microsoft.com/azure/store-cleardb-faq/)를 참조하세요.

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>구독 마이그레이션 중에 내 ClearDB 데이터베이스가 마이그레이션되지 않은 이유는 무엇인가요?

구독 간에 리소스 마이그레이션을 수행할 때 일부 제한 사항 이 적용됩니다. ClearDB MySQL 데이터베이스는 타사 서비스이므로 Azure 구독 마이그레이션 중에 마이그레이션되지 않습니다.

Azure 리소스를 마이그레이션하기 전에 hello 마이그레이션의 MySQL 데이터베이스를 관리 하지 ClearDB MySQL 데이터베이스를 사용할 수 없습니다. tooavoid이이 먼저 수동으로 ClearDB 데이터베이스를 마이그레이션하고 다음 hello 웹 앱에 대 한 Azure 구독을 마이그레이션합니다.

자세한 내용은 [Azure App Service를 사용하는 ClearDB MySQLl 데이터베이스에 대한 FAQ](https://docs.microsoft.com/azure/store-cleardb-faq/)를 참조하세요.

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>PHP tootroubleshoot PHP 문제를 로깅에 하려면 어떻게 할까요?

PHP 로깅을 tooturn:

1. Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.
2. Hello 상단 메뉴에서 선택 **디버그 콘솔** > **CMD**합니다.
3. 선택 hello **사이트** 폴더입니다.
4. 선택 hello **wwwroot** 폴더입니다.
5. 선택 hello  **+**  아이콘을 선택한 후 **새 파일**합니다.
6. Hello 파일 이름을 너무 설정**. user.ini**합니다.
7. 다음 너무 hello 연필 아이콘을 선택한**. user.ini**합니다.
8. Hello 파일에서이 코드를 추가 합니다.`log_errors=on`
9. **저장**을 선택합니다.
10. 다음 너무 hello 연필 아이콘을 선택한**wp config.php**합니다.
11. Hello 텍스트 toohello 코드 다음 변경 합니다.
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Hello hello 웹 응용 프로그램 메뉴에 Azure 포털에서에서 웹 앱을 다시 시작 합니다.

자세한 내용은 [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/)(WordPress 오류 로그 사용)를 참조하세요.

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>App Service에 호스트된 앱에서 Python 응용 프로그램 오류를 기록하려면 어떻게 하나요?

toocapture Python 응용 프로그램 오류:

1. Hello 웹 앱에서 Azure 포털에서에서 선택 **설정을**합니다.
2. Hello에 **설정** 탭에서 **응용 프로그램 설정**합니다.
3. 아래 **앱 설정**를 키/값 쌍을 다음 hello 입력:
    * 키: WSGI_LOG
    * 값: D:\home\site\wwwroot\logs.txt(선택한 파일 이름 입력)

이제 hello wwwroot 폴더에 hello logs.txt 파일에 오류가 표시 됩니다.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Hello 버전의 hello 앱 서비스에서 호스팅되는 Node.js 응용 프로그램을 변경 하려면 어떻게 해야 합니까?

toochange hello 버전의 hello Node.js 응용 프로그램에서는 hello 다음 옵션 중 하나를 사용할 수 있습니다.

*   Hello Azure 포털에서에서 사용 하 여 **앱 설정**합니다.
    1. Azure 포털 hello tooyour 웹 응용 프로그램을 이동 합니다.
    2. Hello에 **설정** 블레이드를 **응용 프로그램 설정**합니다.
    3. **앱 설정**WEBSITE_NODE_DEFAULT_VERSION hello 키로 포함할 수 있으며 hello 버전의 Node.js 원하는 hello 값으로, 합니다.
    4. Tooyour 이동 [Kudu 콘솔](https://*yourwebsitename*.scm.azurewebsites.net)합니다.
    5. toocheck은 Node.js 버전 hello, hello 다음 명령을 입력 합니다.  
   ```
   node -v
   ```
*   Hello iisnode.yml 파일을 수정 합니다. Hello iisnode.yml 파일에 있는 hello Node.js 버전 변경만 hello 런타임 환경을 설정 해당 iisnode 사용 합니다. Kudu cmd 등과 여전히 hello Node.js 버전 사용에서 설정 된 **앱 설정** hello Azure 포털의에서.

    tooset hello iisnode.yml 응용 프로그램 루트 폴더에 있는 iisnode.yml 파일을 수동으로 만듭니다. Hello 파일에서 다음 줄 hello를 포함 합니다.
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   소스 제어 배포가 동안 package.json을 사용 하 여 hello iisnode.yml 파일을 설정 합니다.
    hello Azure 소스 제어 배포 과정 단계를 수행 하는 hello 포함 됩니다.
    1. 콘텐츠 toohello Azure 웹 앱으로 이동합니다.
    2. 절이 없는 경우 (deploy.cmd,.deployment 파일) hello 웹 응용 프로그램 루트 폴더에는 기본 배포 스크립트를 만듭니다.
    3. 해당 파일을 만듭니다 iisnode.yml hello package.json 파일에 있는 hello Node.js 버전을 언급 하는 경우 배포 스크립트를 실행 > 엔진`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. hello iisnode.yml 파일에 다음 코드 줄을 hello:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>앱 서비스에서 호스팅되는 내 WordPress 앱에서 "데이터베이스 연결 설정 오류" hello 메시지를 표시 합니다. 이 문제를 어떻게 해결해야 하나요?

에 대 한 전체 hello 단계가 자세히 Azure WordPress 응용 프로그램, tooenable php_errors.log 및 디버그 로그에이 오류가 표시 되 면 [WordPress 사용 오류 로그](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/)합니다.

Hello 로그 설정 되 면 hello 오류를 재현 한 다음 hello 로그 toosee 연결에서 실행 하는 경우:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

디버그 로그 또는 php_errors.log 파일에이 오류를 참조 하는 경우 앱이 hello 연결 수를 초과 합니다. ClearDB를 호스팅하는 경우 hello에서 사용할 수 있는 연결 수를 확인 하면 [서비스 계획](https://www.cleardb.com/pricing.view)합니다.

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>App Service에 호스트된 Node.js 앱을 디버그하려면 어떻게 하나요?

1.  Tooyour 이동 [Kudu 콘솔](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole)합니다.
2.  이동 tooyour 응용 프로그램 로그 폴더 (D:\home\LogFiles\Application)입니다.
3.  Hello logging_errors.txt 파일에서 콘텐츠를 확인 합니다.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>App Service 웹앱 또는 API 앱에서 기본 Python 모듈을 설치하려면 어떻게 하나요?

일부 패키지는 Azure에서 pip를 사용하여 설치할 수 없습니다. hello 패키지 hello Python 패키지 인덱스에 사용할 수 없습니다 또는 컴파일러 해야 할 수 있습니다 (컴파일러에서 사용할 수 없으면 앱 서비스의 hello 웹 응용 프로그램을 실행 중인 hello 컴퓨터). App Service Web Apps 및 API Apps에서 기본 모듈을 설치하는 방법에 대한 자세한 내용은 [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/)(App Service에서 Python 모듈 설치)를 참조하세요.

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Python의 Git 및 hello 새 버전을 사용 하 여 Django 앱 tooApp 서비스를 어떻게 배포 합니까?

Django 설치에 대 한 정보를 참조 하십시오. [Django 앱 tooApp 서비스 배포](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/)합니다.

## <a name="where-are-hello-tomcat-log-files-located"></a>에 있는 hello Tomcat 로그 파일은 어디에 있습니까?

Azure Marketplace 및 사용자 지정 배포의 경우:

* 폴더 위치: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* 관심 파일:
    * catalina.*yyyy-mm-dd*.log
    * host-manager.*yyyy-mm-dd*.log
    * localhost.*yyyy-mm-dd*.log
    * manager.*yyyy-mm-dd*.log
    * site_access_log.*yyyy-mm-dd*.log


포털 **앱 설정** 배포의 경우:

* 폴더 위치: D:\home\LogFiles
* 관심 파일:
    * catalina.*yyyy-mm-dd*.log
    * host-manager.*yyyy-mm-dd*.log
    * localhost.*yyyy-mm-dd*.log
    * manager.*yyyy-mm-dd*.log
    * site_access_log.*yyyy-mm-dd*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>JDBC 드라이버 연결 오류를 해결하려면 어떻게 하나요?

Hello Tomcat 로그에 메시지의 뒤에 나타날 수 있습니다.

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

tooresolve hello 오류:

1. 응용 프로그램/lib 폴더에서 hello sqljdbc*.jar 파일을 제거 합니다.
2. Hello 사용자 지정 Tomcat 또는 Azure 마켓플레이스 Tomcat 웹 서버를 사용 하는 경우이.jar 파일 toohello Tomcat lib 폴더를 복사 합니다.
3. Java를 사용 하는 경우 hello Azure 포털 (선택 **Java 1.8** > **Tomcat 서버**), 병렬 tooyour 앱 있는 hello 폴더에 hello sqljdbc.* jar 파일 복사 합니다. Hello 다음 클래스 경로 설정 toohello web.config 파일을 추가 합니다.

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Toocopy 실시간 로그 파일을 하려고 할 때 오류가 나타나는 이유는 무엇입니까?

Java 응용 프로그램 (예: Tomcat)에 대 한 toocopy 실시간 로그 파일을 시도 하면이 FTP 오류가 나타날 수 있습니다.

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

hello 오류 메시지가 hello FTP 클라이언트에 따라 달라질 수 있습니다.

모든 Java 앱에는 이 잠금 오류가 있습니다. Kudu만 지원 hello 응용 프로그램을 실행 하는 동안이 파일을 다운로드 합니다.

중지 hello 앱 toothese 파일이 FTP 액세스를 허용합니다.

다른 해결 방법은 toowrite 일정으로 실행 하 고 이러한 파일 tooa 다른 디렉터리를 복사 하는 웹 작업입니다. 샘플 프로젝트에 대 한 참조 hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) 프로젝트.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Jetty에 대 한 로그 파일 hello를 어디서 찾을 수 있습니까?

Marketplace와 사용자 지정 배포에 대 한 hello 로그 파일은 hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs 폴더에 있습니다. 참고 hello 폴더 위치를 사용 하는 jetty hello 버전에 따라 결정 됩니다. 예를 들어 hello 경로가 제공 Jetty 9.1.2에 대 한 다음과 같습니다. jetty_*YYYY_MM_DD*.stderrout.log를 찾습니다.

포털 응용 프로그램 설정 배포에 대 한 hello 로그 파일이 D:\home\LogFiles입니다. jetty_*YYYY_MM_DD*.stderrout.log 찾기

## <a name="can-i-send-email-from-my-azure-web-app"></a>내 Azure 웹앱에서 메일을 보낼 수 있나요?

App Service에는 기본 제공 메일 기능이 없습니다. 앱에서 메일을 보낼 수 있는 다른 좋은 방법은 이 [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure)(스택 오버플로 토론)을 참조하세요.

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>내 WordPress 사이트 tooanother URL를 리디렉션하도록 하는 이유

TooAzure 최근에 마이그레이션한 경우 WordPress toohello 이전 도메인 URL을 리디렉션할 수 있습니다. 이 설정 hello MySQL 데이터베이스에 의해 발생 합니다.

WordPress 버디 + hello 데이터베이스에서 직접 tooupdate hello 리디렉션 URL을 사용할 수 있는 Azure 사이트 확장입니다. WordPress Buddy+ 사용에 대한 자세한 내용은 [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)(WordPress Buddy+를 사용한 WordPress 도구 및 MySQL 마이그레이션)를 참조하세요.

SQL 쿼리 또는 PHPMyAdmin 사용 하 여 toomanually 업데이트 hello 리디렉션 URL을 선호 하는 경우 참조 또는 [WordPress: toowrong URL 리디렉션](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/)합니다.

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>내 WordPress 로그인 암호를 어떻게 변경할 수 있나요?

WordPress 로그인 암호를 잊어버린 경우에 WordPress 버디 + tooupdate을 사용할 수 있습니다 것입니다. 암호, WordPress Azure 버디 + 사이트 확장을 설치 hello 및 다음 전체 hello 단계에 설명 된 tooreset [WordPress 도구 및 MySQL 마이그레이션 WordPress 버디 + 준수](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)합니다.

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>TooWordPress 로그인 할 수 없습니다. 이 문제를 해결하려면 어떻게 해야 하나요?

최근에 플러그 인을 설치한 후 WordPress에서 잠긴 것을 알았다면 잘못된 플러그 인이 있을 수 있습니다. WordPress Buddy+는 WordPress에서 플러그 인을 사용하지 않도록 설정할 수 있는 Azure 사이트 확장입니다. 자세한 내용은 [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)(WordPress Buddy+를 사용한 WordPress 도구 및 MySQL 마이그레이션)를 참조하세요.

## <a name="how-do-i-migrate-my-wordpress-database"></a>내 WordPress 데이터베이스를 마이그레이션하려면 어떻게 하나요?

마이그레이션 hello MySQL 데이터베이스는 연결 된 tooyour WordPress 웹 사이트에 대 한 여러 옵션이 있습니다.

* 개발자: 사용 하 여 hello [명령 프롬프트 또는 PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* 비 개발자: [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) 사용

## <a name="how-do-i-help-make-wordpress-more-secure"></a>WordPress의 보안을 강화하려면 어떻게 해야 하나요?

WordPress에 대 한 보안 모범 사례에 대 한 toolearn 참조 [Azure에서 WordPress 보안에 대 한 유용한](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/)합니다.

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Toouse PHPMyAdmin, 려을 hello 메시지 "액세스가 거부 되었습니다." 표시 이 문제를 해결하려면 어떻게 해야 하나요?

이 앱 서비스 인스턴스에서 아직 실행 되지 않고 hello MySQL 앱에서 기능 하는 경우이 문제가 발생할 수 있습니다. tooresolve 문제, try tooaccess 웹 사이트를 hello 합니다. 이 앱에서 MySQL hello 프로세스를 비롯 한 hello 필요한 프로세스를 시작 합니다. 프로세스 탐색기에서 앱에서 실행 중인 MySQL 해당 mysqld.exe 확인는 tooverify hello 프로세스에 나열 됩니다.

앱에서 MySQL 실행 되 고 있는지 확인 한 후 toouse PHPMyAdmin 해 보십시오.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Tooimport 시도 하거나 PHPMyadmin를 사용 하 여 앱에서 MySQL 데이터베이스를 내보낼 때 HTTP 403 오류가 합니다. 이 문제를 해결하려면 어떻게 해야 하나요?

이전 버전의 Chrome을 사용하고 있으면 알려진 버그가 발생할 수 있습니다. 최신 버전의 Chrome 업그레이드 tooa tooresolve hello 문제가 있습니다. 또한 Internet Explorer 또는 hello 문제가 발생 하지 않으면 가장자리와 같은 다른 브라우저를 사용해 보십시오.
