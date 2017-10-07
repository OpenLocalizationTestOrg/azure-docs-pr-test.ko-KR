---
title: "aaaConnect tooSQL C 및 c + +를 사용 하 여 데이터베이스 | Microsoft Docs"
description: "사용 하 여 hello 샘플의 코드에서이 빠른 시작 toobuild c + +와 최신 응용 프로그램 및 hello 클라우드에서 Azure SQL 데이터베이스와 함께 강력한 관계형 데이터베이스에서 지원 합니다."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>TooSQL 연결 C 및 c + +를 사용 하 여 데이터베이스
이 게시물은 tooconnect tooAzure SQL DB를 시도 하는 C 및 c + + 개발자를 대상으로 합니다. 나뉘어집니다 구간으로 분할 toohello 섹션 가장 관심을 캡처하는 이동할 수 있도록 합니다. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>C/c + + 자습서 hello에 대 한 필수 구성 요소
다음 항목 hello 지정 했는지 확인 합니다.

* 활성 Azure 계정. 아직 구독하지 않은 경우 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* [Visual Studio](https://www.visualstudio.com/downloads/). C + + 언어 구성 요소 toobuild hello를 설치 하 고이 샘플을 실행 해야 합니다.
* [Visual Studio Linux 개발](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Linux에서 개발 하는 경우에 hello Visual Studio Linux 확장도 설치 해야 합니다. 

## <a id="AzureSQL"></a>가상 컴퓨터에서 Azure SQL Database 및 SQL Server
Azure SQL Microsoft SQL Server에서 작성 되 고 높은 가용성, 성능, 좋 및 확장 가능한 서비스 디자인 된 tooprovide 됩니다. 독점적인 온-프레미스에서 실행 중인 데이터베이스를 통해 많은 이점을 toousing SQL Azure 있습니다. SQL Azure와 함께 하지 않는 tooinstall, 설정, 유지 관리 했거나 데이터베이스 있지만 hello 콘텐츠 및 데이터베이스의 hello 구조를 관리 합니다. 내결함성과 중복성처럼 데이터 베이스에 대해 일반적으로 걱정하는 것이 모두 기본 제공됩니다. 

Azure에는 현재 Azure SQL server 작업 부하를 호스팅하기 위한 두 가지 옵션, 즉 서비스로서 데이터베이스인 Azure SQL Database와 가상 컴퓨터(VM)의 SQL server가 있습니다. 우리는 가져올 수 없습니다 이러한 두 hello 차이점에 대 한 정보를 확인할 Azure SQL 데이터베이스는 새로운 클라우드 기반 응용 프로그램 tootake 이점이 hello 비용 절감 효과 위한 최선의 방법은 클라우드 서비스 성능 최적화를 제공 된다는 점이 다릅니다. 마이그레이션 또는 온-프레미스 응용 프로그램 toohello 클라우드 확장 하려는 경우 Azure 가상 컴퓨터에 SQL server 더 적합 작동 될 수 있습니다. tookeep 가지 간단한이이 문서에서는 Azure SQL 데이터베이스를 만들어 보겠습니다. 

## <a id="ODBC"></a>데이터 액세스 기술: ODBC 및 OLE DB
SQL DB 연결 tooAzure 마찬가지 이며 현재 두 가지 tooconnect toodatabases: ODBC (Open Database connectivity) 및 OLE DB (개체 연결과 데이터베이스). 최근 몇 년간 Microsoft는 [기본 관계형 데이터 액세스에 대해 ODBC](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)에 맞추어 왔습니다. ODBC은 비교적 간단하고 OLE DB보다 훨씬 빠릅니다. 유일한 주의할 여기 hello ODBC는 이전 C 스타일 API를 사용 하는입니다. 

## <a id="Create"></a>1단계: Azure SQL Database 만들기
Hello 참조 [시작 하기 페이지](sql-database-get-started-portal.md) toolearn 어떻게 toocreate 예제 데이터베이스.  또는 설치 하려면이 방법을 [짧은 2 분 비디오](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) 사용 하 여 Azure SQL 데이터베이스 toocreate hello Azure 포털입니다.

## <a id="ConnectionString"></a>2단계: 연결 문자열 가져오기
Azure SQL 데이터베이스 프로 비전 한 후 다음 단계 toodetermine 연결 정보는 hello 아웃 toocarry 필요 하 고 방화벽 액세스에 대 한 클라이언트 IP 추가 합니다. 

[Azure 포털](https://portal.azure.com/), tooyour Azure SQL 데이터베이스 ODBC 연결 문자열 hello를 사용 하 여 이동 **데이터베이스 연결 문자열 표시** 데이터베이스에 대 한 hello 개요 섹션의 일부분으로 나열: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Hello의 hello 내용을 복사 **ODBC (포함 Node.js) [SQL 인증]** 문자열입니다. 이 문자열을 사용 하 여 우리는 c + + ODBC 명령줄 인터프리터에서 이후 tooconnect 합니다. 이 문자열 hello 드라이버, 서버 및 다른 데이터베이스 연결 매개 변수 등의 세부 정보를 제공합니다. 

## <a id="Firewall"></a>3 단계: 추가 IP toohello 방화벽
Toohello 방화벽 섹션 데이터베이스 서버에 이동 하 고 추가 프로그램 [다음이 단계를 사용 하 여 클라이언트 IP toohello 방화벽](sql-database-configure-firewall-settings.md) toomake 있는지 성공적으로 연결을 설정할 수 있습니다. 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

이 시점에서 Azure SQL DB 구성 및 준비 tooconnect c + + 코드는 합니다. 

## <a id="Windows"></a>4단계: Windows C/C++ 응용 프로그램에서 연결
Tooyour를 쉽게 연결할 수 있습니다 [이 샘플을 사용 하 여 Windows에서 ODBC를 사용 하 여 Azure SQL DB](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) 을 Visual Studio와 함께 빌드하 합니다. hello 샘플 사용된 tooconnect tooour Azure SQL DB 수 있는 ODBC 명령줄 인터프리터를 구현 합니다. 이 샘플에서는 명령줄 인수로 데이터베이스 원본 이름 (DSN) 파일 파일 또는 hello Azure 포털에서에서 앞에서 복사한 우리는 hello verbose 연결 문자열을 사용 합니다. 이 프로젝트에 대 한 hello 속성 페이지를 열고이 하 다음과 같이 명령 인수로 hello 연결 문자열을 붙여 넣습니다. 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

해당 데이터베이스 연결 문자열의 일부로 데이터베이스에 대 한 hello 올바른 인증 세부 정보를 제공 해야 합니다. 

Hello 응용 프로그램 toobuild 시작 것입니다. 창 성공적인 연결 유효성 검사를 수행 하는 hello를 표시 되어야 합니다. 와 같은 몇 가지 기본 SQL 명령의 실행할 수 **테이블을 만들** toovalidate 데이터베이스 연결:

![SQL 명령](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

또는 명령 인수에 제공 되는 경우 시작 된 hello 마법사를 사용 하는 DSN 파일을 만들 수 있습니다. 이 옵션을 함께 시도하는 것이 좋습니다. 자동화 및 인증 설정 보호를 위해 DSN 파일을 사용할 수 있습니다. 

![파일 DSN 만들기](./media/sql-database-develop-cplusplus-simple/datasource.png)

축하합니다. SQL tooAzure를 성공적으로 연결 되어 이제 c + + 및 ODBC를 사용 하 여 Windows에서 합니다. 계속 읽어보세요 수 toodo hello Linux 플랫폼에 동일 합니다. 

## <a id="Linux"></a>5 단계: Linux C/C++ 응용 프로그램에서 연결
경우에 대비 hello 뉴스 듣지 아직 Visual Studio를 사용 하면 있습니다 toodevelop c + + Linux 응용 프로그램의 경우에 합니다. 이 새 시나리오 hello에서 참고할 수 [Linux 개발용 Visual c + +](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) 블로그. Linux 용 toobuild, Linux 배포판 실행 되 고 있는 원격 컴퓨터가 필요 합니다. 원격 컴퓨터가 없다면 [Linux Azure 가상 컴퓨터](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용하여 신속하게 하나를 설정할 수 있습니다. 

이 자습서에서는 Ubuntu 16.04 Linux 배포판이 설치되어 있다고 가정합니다. 여기에 나오는 hello 단계 tooUbuntu 15.10, Red Hat 6 및 Red Hat 7에도 적용 해야 합니다. 

hello 다음 설치 단계를 수행 하면 배포판에 대 한 SQL 및 ODBC에 대 한 필요한 hello 라이브러리:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Visual Studio를 시작합니다. 도구-> 옵션에는 플랫폼 간-> 연결 관리자-> 연결 tooyour Linux 상자를 추가 합니다. 

![도구 옵션](./media/sql-database-develop-cplusplus-simple/tools.png)

SSH 통해 연결이 설정된 후에 빈 프로젝트(Linux) 템플릿을 만듭니다. 

![새 프로젝트 템플릿](./media/sql-database-develop-cplusplus-simple/template.png)

그런 다음 [새 C 소스 파일을 추가하고 다음 내용으로 교체](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c)할 수 있습니다. ODBC Api SQLAllocHandle hello, SQLSetConnectAttr, 및 SQLDriverConnect를 사용 하 여 있습니다 수 tooinitialize와 tooyour 데이터베이스 연결을 설정 합니다. 마찬가지로 hello Windows ODBC 샘플 해야 hello Azure 포털에서에서 이전에 복사한 데이터베이스 연결 문자열 매개 변수에서 tooreplace hello SQLDriverConnect 호출 hello 세부 정보. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

컴파일 전에 tooadd 마지막 일 toodo hello **odbc** 라이브러리 종속성으로: 

![입력된 라이브러리로 ODBC 추가](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch 응용 프로그램에서 hello hello Linux 콘솔 (를) 실행 **디버그** 메뉴: 

![Linux 콘솔](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

연결에 성공 하면 이제 표시 되어야 hello hello Linux 콘솔에에서 인쇄는 현재 데이터베이스 이름: 

![Linux 콘솔 창 출력](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

축하합니다. Hello 자습서를 성공적으로 마쳤습니다 및 Azure SQL DB tooyour c + +에서 Windows 및 Linux 플랫폼에 연결할 이제 수 있습니다.

## <a id="GetSolution"></a>Hello 완료 C/c + + 자습서 솔루션 가져오기
Github에서이 문서에서 모든 hello 샘플을 포함 하는 hello GetStarted 솔루션을 찾을 수 있습니다.

* [Windows c + + ODBC 샘플](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), hello Windows c + + ODBC 샘플 tooconnect tooAzure SQL 다운로드
* [C + + Linux ODBC 샘플](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), hello Linux c + + ODBC 샘플 tooconnect tooAzure SQL 다운로드

## <a name="next-steps"></a>다음 단계
* 검토 hello [SQL 데이터베이스 개발 개요](sql-database-develop-overview.md)
* Hello에 대 한 자세한 내용은 [ODBC API 참조](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>추가 리소스
* [Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램 디자인 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* 모든 hello 탐색 [SQL 데이터베이스의 기능](https://azure.microsoft.com/services/sql-database/)

