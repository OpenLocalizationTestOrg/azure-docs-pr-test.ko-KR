---
title: "Java에서 Azure 검색 시작 aaaGet | Microsoft Docs"
description: "호스트 된 클라우드 toobuild Java 프로그래밍 언어를 사용 하 여 Azure에서 응용 프로그램 검색 하는 방법입니다."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Java에서 Azure 검색 시작
> [!div class="op_single_selector"]
> * [포털](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

사용자 지정 Java toobuild 검색 경험에 대 한 Azure 검색을 사용 하는 응용 프로그램을 검색 하는 방법에 대해 알아봅니다. 이 자습서에서는 hello [Azure 검색 서비스 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 개체 및이 연습에서 사용 하는 작업입니다.

toorun이이 샘플에서는 있어야 hello에에 등록할 수 있는 Azure 검색 서비스 [Azure 포털](https://portal.azure.com)합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 단계별 지침.

다음 소프트웨어 toobuild hello를 사용 하 고이 샘플을 테스트 합니다.

* [Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). 있는지 toodownload hello EE 버전 이어야 합니다. Hello 확인 단계 중 하나에이 버전에만 있는 기능이 필요 합니다.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache는 Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Hello 데이터에 대 한
이 샘플 응용 프로그램 데이터 hello에서 사용 하 여 [United States 지리 서비스 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)hello 로드 아일랜드 상태 tooreduce hello 데이터 집합 크기에 필터링 되어 있습니다. 이 데이터 toobuild 호수, 스트림과 summits 같은 지리 기능 뿐만 아니라 병원 학교와 같은 이정표 건물을 반환 하는 검색 응용 프로그램을 사용 합니다.

이 응용 프로그램에서는 hello **SearchServlet.java** 프로그램을 빌드하고 로드 hello를 사용 하 여 인덱스는 [인덱서](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello 검색 구문 공용 Azure SQL 데이터베이스에서 USG 데이터 집합을 필터링 합니다. 미리 정의 된 자격 증명 및 연결 정보 toohello 온라인 데이터 원본 hello 프로그램 코드에서 제공 됩니다. 데이터 액세스 측면에서 추가 구성은 필요하지 않습니다.

> [!NOTE]
> Hello 10, 000 문서 제한의 hello 무료 가격 책정 계층에서이 데이터 집합 toostay에 필터를 적용 합니다. 표준 계층 hello를 사용 하는 경우이 제한이 적용 되지 않습니다 하 고이 코드 toouse 큰 데이터 집합을 수정할 수 있습니다. 각 가격 책정 계층의 용량에 대한 자세한 내용은 [제한 및 제약 조건](search-limits-quotas-capacity.md)을 참조하세요.
> 
> 

## <a name="about-hello-program-files"></a>Hello 프로그램 파일에 대 한
hello 다음 목록에서는 관련 toothis 샘플 있는 hello 파일.

* Search.jsp: hello 사용자 인터페이스를 제공합니다.
* SearchServlet.java: (MVC에서 유사한 tooa 컨트롤러) 메서드를 제공합니다.
* SearchServiceClient.java: HTTP 요청을 처리합니다.
* SearchServiceHelper.java: 정적 메서드를 제공하는 도우미 클래스입니다.
* Hello 데이터 모델을 제공 하는 Document.java:
* config.properties: hello 검색 서비스 URL 및 api 키를 설정 합니다.
* Pom.xml: Maven 종속성입니다.

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Hello 서비스 이름 및 Azure 검색 서비스의 api 키 찾기
Azure 검색에 대 한 모든 REST API 호출 hello 서비스 URL 및 api 키를 제공 해야 합니다. 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 점프 막대에서 클릭 **검색 서비스** toolist hello Azure 검색 서비스의 모든 구독에 대 한 프로 비전 합니다.
3. Toouse hello 서비스를 선택 합니다.
4. Hello 서비스 대시보드 타일에 대 한 중요 한 정보 뿐만 아니라 hello hello 관리자 키에 액세스 하기 위한 키 아이콘이 표시 됩니다.
   
      ![][3]
5. Hello 서비스 URL 및 관리자 키를 복사 합니다. 나중에 필요 합니다에, toohello를 추가할 때 **config.properties** 파일입니다.

## <a name="download-hello-sample-files"></a>Hello 샘플 파일 다운로드
1. 너무 이동[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) GitHub에서 합니다.
2. 클릭 **zip 파일 다운로드**hello.zip 파일 toodisk 저장 한 다음 포함 된 모든 hello 파일을 추출 합니다. 추출 하는 것이 좋습니다. hello로 파일 Java 작업 영역 toomake 것 보다 쉽게 toofind hello 프로젝트 나중입니다.
3. hello 예제 파일은 읽기 전용입니다. 폴더 속성 및 지우기 hello 읽기 전용 특성을 마우스 오른쪽 단추로 클릭 합니다.

이후의 모든 파일 수정 및 실행 문은 이 폴더의 파일에 대해 수행됩니다.  

## <a name="import-project"></a>프로젝트 가져오기
1. Eclipse에서 **File** > **Import** > **General** > **Existing Projects into Workspace**를 선택합니다.
   
    ![][4]
2. **Select의 루트 디렉터리**, 샘플 파일이 포함 된 toohello 폴더를 찾습니다. Hello 폴더가 포함 된 hello.project 폴더를 선택 합니다. hello 프로젝트 hello에 표시될지 **프로젝트** 선택한 항목으로 목록입니다.
   
    ![][12]
3. **마침**을 클릭합니다.
4. 사용 하 여 **프로젝트 탐색기** tooview 및 편집 hello 파일입니다. 열려 있지 않으면 클릭 **창** > **보기 표시** > **프로젝트 탐색기** 하거나 바로 가기 tooopen hello를 사용 하 여 것입니다.

## <a name="configure-hello-service-url-and-api-key"></a>Hello 서비스 URL 및 api 키 구성
1. **프로젝트 탐색기**를 두 번 클릭 **config.properties** tooedit hello 서버 이름 및 api 키를 포함 하는 hello 구성 설정입니다.
2. Hello에 hello 서비스 URL 및 api 키가 발견 되는 위치,이 문서의 앞부분에 toohello 단계 참조 [Azure 포털](https://portal.azure.com), 이제 입력할 예정 tooget hello 값 **config.properties**합니다.
3. **config.properties**, "Api 키" 서비스에 대 한 hello api 키로 바꿉니다. 다음으로, 서비스 이름 (hello 첫 번째 구성 요소 hello URL http://servicename.search.windows.net)을 대체 "서비스 이름인" hello 같은 파일입니다.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Hello 프로젝트, 빌드 및 런타임 환경 구성
1. Eclipse 프로젝트 탐색기에서에서 hello 프로젝트를 마우스 오른쪽 단추로 > **속성** > **프로젝트 패싯**합니다.
2. **Dynamic Web Module**, **Java** 및 **JavaScript**를 선택합니다.
   
    ![][6]
3. **Apply**를 클릭합니다.
4. <seg>
  **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**를 선택합니다.</seg>
5. Apache를 확장 하 고 이전에 설치한 hello Apache Tomcat 서버 hello 버전을 선택 합니다. 예제 시스템에는 버전 8이 설치되어 있습니다.
   
    ![][7]
6. Hello 다음 페이지에서 hello Tomcat 설치 디렉터리를 지정 합니다. Windows 컴퓨터의 경우 일반적으로 C:\Program Files\Apache Software Foundation\Tomcat *버전*입니다.
7. **마침**을 클릭합니다.
8. **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**를 선택합니다.
9. **Add JRE**에서 **Standard VM**을 선택합니다.
10. **다음**을 누릅니다.
11. JRE 정의의 JRE 홈에서 **Directory**를 클릭합니다.
12. 너무 이동**Program Files** > **Java** hello 이전에 설치한 JDK를 선택 합니다. 중요 한 tooselect hello JDK 프로토콜은 JRE hello로 합니다.
13. 설치 된 JREs 선택 hello **JDK**합니다. 비슷한 toohello 스크린 샷 다음 설정에 표시 됩니다.
    
    ![][9]
14. 필요에 따라 선택 **창** > **웹 브라우저** > **Internet Explorer** 외부 브라우저 창에서 tooopen hello 응용 프로그램입니다. 외부 브라우저를 사용하면 웹 응용 프로그램 환경이 향상됩니다.
    
    ![][8]

이제 hello 구성 작업을 완료 했습니다. 다음으로 작성 하 고 hello 프로젝트를 실행 합니다.

## <a name="build-hello-project"></a>Hello 프로젝트 빌드
1. 프로젝트 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **실행** > **Maven 빌드 중...**  tooconfigure hello 프로젝트.
   
    ![][10]
2. Edit Configuration에서 Goals에 "clean install"을 입력하고 **Run**을 클릭합니다.

상태 메시지는 출력 toohello 콘솔 창입니다. 빌드 성공 나타내는 hello 프로젝트 오류 없이 구축 표시 되어야 합니다.

## <a name="run-hello-app"></a>Hello 앱 실행
이 마지막 단계에서는 로컬 서버 런타임 환경에서 hello 응용 프로그램을 실행 합니다.

Eclipse에서 서버 런타임 환경을 아직 지정 하지 않은 경우 해야 toodo을 먼저 합니다.

1. Project Explorer에서 **WebContent**를 확장합니다.
2. **Search.jsp** > **Run As** > **Run on Server**를 마우스 오른쪽 단추로 클릭합니다. Hello Apache Tomcat 서버를 선택한 다음 클릭 **실행**합니다.

> [!TIP]
> 를 사용 하는 기본이 아닌 작업 영역의 toostore 프로젝트 toomodify 맞춰야 **실행 구성** toopoint toohello 프로젝트 위치 tooavoid 서버 시작 시 오류가 있습니다. Project Explorer에서 **Search.jsp** > **Run As** > **Run Configurations**를 마우스 오른쪽 단추로 클릭합니다. Hello Apache Tomcat 서버를 선택 합니다. **Arguments**를 클릭합니다. 클릭 **작업 영역** 또는 **파일 시스템** hello 프로젝트가 포함 된 tooset hello 폴더입니다.
> 
> 

Hello 응용 프로그램을 실행 하면 표시 됩니다는 브라우저 창 용어를 입력 하기 위한 검색 상자를 제공 합니다.

클릭 하기 전에 1 분 정도 기다렸다가 **검색** toogive hello 서비스 시간 toocreate 및 부하 hello 인덱스입니다. HTTP 404 오류가 발생 하는 경우 하기만 하면 toowait 약간 더 긴 다시 시도 하십시오.

## <a name="search-on-usgs-data"></a>USGS 데이터 검색
hello USG 데이터 집합에 로드 아일랜드의 관련 toohello 상태 레코드가 포함 됩니다. 클릭 하면 **검색** 빈 검색 상자에 항목을 가져오게 됩니다 hello 상위 50 개의 hello 기본값입니다.

검색어를 입력 합니다 hello 검색 엔진 어떤 toogo에 부여 합니다. 지역 이름을 입력해 봅니다. "Roger Williams" hello 로드 아일랜드의 첫 번째 관리자 했습니다. 유명한 공원, 빌딩 및 학교가 그의 이름을 따라 이름을 지었습니다.

![][11]

다음과 같은 용어를 입력해 볼 수도 있습니다.

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>다음 단계
Java 및 hello USG 데이터 집합에 따라 hello 첫 번째 Azure 검색 자습서입니다. 시간이 지남에 따라 추가 검색 기능을 사용자 지정 솔루션에서 toouse 할 수 있습니다이 자습서 toodemonstrate를 확장 합니다.

Azure 검색의 몇 가지 배경 이미 있는 경우으로 사용할 수 있습니다이 예제는 springboard 추가 실험에 대 한 hello 아마도 확대 [검색 페이지](search-pagination-page-layout.md), 구현 또는 [패싯 탐색](search-faceted-navigation.md)합니다. 또한 개수를 추가 하 고 hello 결과 통해 사용자가 페이지로 이동할 수 있도록 문서를 일괄 처리 하 여 hello 검색 결과 페이지를 개선할 수 있습니다.

새 tooAzure 검색? 다른 자습서 toodevelop 만들 수는 이해 하는 것이 좋습니다. 방문 우리의 [설명서 페이지](https://azure.microsoft.com/documentation/services/search/) toofind 리소스를 더 합니다. Hello에 대 한 링크를 볼 수도 있습니다 우리의 [비디오 및 자습서 목록](search-video-demo-tutorial-list.md) tooaccess 자세한 정보.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
