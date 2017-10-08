---
title: "Node.js에서 Azure 검색 시작 aaaGet | Microsoft Docs"
description: "Node.js를 프로그래밍 언어로 사용하여 사용자 지정 Azure에서 호스트된 클라우드 검색 서비스의 검색 응용 프로그램을 빌드하는 과정을 안내합니다."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Node.js에서 Azure Search 시작
> [!div class="op_single_selector"]
> * [포털](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

사용자 지정 Node.js toobuild 검색 경험에 대 한 Azure 검색을 사용 하는 응용 프로그램을 검색 하는 방법에 대해 알아봅니다. 이 자습서에서는 hello [Azure 검색 서비스 REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello 개체 및이 연습에서 사용 하는 작업입니다.

사용 [Node.js](https://Nodejs.org) 및 NPM [Sublime 텍스트 3](http://www.sublimetext.com/3), 및 Windows 8.1 toodevelop에서 Windows PowerShell이이 코드를 테스트 합니다.

toorun이이 샘플에서는 있어야 hello에에 등록할 수 있는 Azure 검색 서비스 [Azure 포털](https://portal.azure.com)합니다. 참조 [hello 포털에서 Azure 검색 서비스 만들기](search-create-service-portal.md) 단계별 지침.

## <a name="about-hello-data"></a>Hello 데이터에 대 한
이 샘플 응용 프로그램 데이터 hello에서 사용 하 여 [United States 지리 서비스 (USG)](http://geonames.usgs.gov/domestic/download_data.htm)hello 로드 아일랜드 상태 tooreduce hello 데이터 집합 크기에 필터링 되어 있습니다. 이 데이터 toobuild 호수, 스트림과 summits 같은 지리 기능 뿐만 아니라 병원 학교와 같은 이정표 건물을 반환 하는 검색 응용 프로그램을 사용 합니다.

이 응용 프로그램에서는 hello **DataIndexer** 프로그램을 빌드하고 로드 hello를 사용 하 여 인덱스는 [인덱서](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello 검색 구문 공용 Azure SQL 데이터베이스에서 USG 데이터 집합을 필터링 합니다. 자격 증명 및 연결 정보 toohello 온라인 데이터 원본을 hello 프로그램 코드에서 제공 됩니다. 추가 구성은 필요하지 않습니다.

> [!NOTE]
> Hello 10, 000 문서 제한의 hello 무료 가격 책정 계층에서이 데이터 집합 toostay에 필터를 적용 합니다. 표준 계층 hello를 사용 하는 경우이 제한이 적용 되지 않습니다. 각 가격 책정 계층의 용량에 대한 자세한 내용은 [검색 서비스 제한](search-limits-quotas-capacity.md)을 참조하세요.
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Hello 서비스 이름 및 Azure 검색 서비스의 api 키 찾기
Hello 서비스를 만든 후 반환 toohello 포털 tooget hello URL 또는 `api-key`합니다. 연결 tooyour 검색 서비스가 있어야 두 hello URL 및 `api-key` tooauthenticate hello 호출 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 점프 막대에서 클릭 **검색 서비스** toolist 구독에 대 한 모든 Azure 검색 서비스를 프로 비전 합니다.
3. Toouse hello 서비스를 선택 합니다.
4. Hello 서비스 대시보드에서 타일 hello 관리자 키에 액세스 하기 위한 키 아이콘 hello와 같은 중요 한 정보에 대 한 표시 되어야 합니다.
5. Hello 서비스 URL, 관리자 키 및 쿼리 키를 복사 합니다. 나중에 세 가지 모두 필요 하면 toohello config.js 파일을 추가 합니다.

## <a name="download-hello-sample-files"></a>Hello 샘플 파일 다운로드
Hello 접근 방식을 toodownload hello 샘플 다음 중 하나를 사용 합니다.

1. 너무 이동[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo)합니다.
2. 클릭 **zip 파일 다운로드**, hello.zip 파일을 저장 한 다음 포함 된 모든 hello 파일을 추출 합니다.

이후의 모든 파일 수정 및 실행 문은 이 폴더의 파일에 대해 수행됩니다.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Hello config.js를 업데이트 합니다. config.js를 업데이트합니다.
URL 및 api 키가 이전에 복사 하는 hello를 사용 하 여 구성 파일에 URL hello 관리자 키 및 쿼리 키를 지정 합니다.

관리 키는 인덱스 만들기 또는 삭제 및 문서 로드를 포함하여 서비스 작업에 대한 모든 권한을 부여합니다. 이와 달리 쿼리 키는 tooAzure 검색을 연결 하는 클라이언트 응용 프로그램에서 일반적으로 사용 하는 읽기 전용 작업에 대 한 합니다.

이 샘플에서는 키 toohelp hello hello 쿼리 키를 사용 하 여 클라이언트 응용 프로그램에서 모범 사례를 보완 하는 hello 쿼리를 포함 합니다.

다음 스크린 샷에 표시 hello **config.js** hello로 텍스트 편집기에 열려 있는 hello로 tooupdate hello 파일 값을 볼 수 있도록 demarcated 관련 항목은 검색 서비스에 대해 유효 합니다.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>호스트 hello 샘플에 대 한 런타임 환경
hello 샘플 필요 HTTP 서버는 전역적으로 npm을 사용 하 여 설치할 수 있습니다.

다음 명령을 hello에 대 한 PowerShell 창을 사용 합니다.

1. Hello 있는 toohello 폴더 탐색 **package.json** 파일입니다.
2. `npm install`을 입력합니다.
3. `npm install -g http-server`을 입력합니다.

## <a name="build-hello-index-and-run-hello-application"></a>Hello 응용 hello 인덱스를 빌드 및 실행
1. `npm run indexDocuments`을 입력합니다.
2. `npm run build`을 입력합니다.
3. `npm run start_server`을 입력합니다.
4. 브라우저에서 `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>USGS 데이터 검색
hello USG 데이터 집합에 로드 아일랜드의 관련 toohello 상태 레코드가 포함 됩니다. 클릭 하면 **검색** 빈 검색 상자에서 얻게 hello 상위 50 개의 항목 hello 기본값입니다.

검색어를 입력 제공 hello 검색 엔진 항목 합계에 toogo 합니다. 지역 이름을 입력해 봅니다. "Roger Williams" hello 로드 아일랜드의 첫 번째 관리자 했습니다. 유명한 공원, 빌딩 및 학교가 그의 이름을 따라 이름을 지었습니다.

![][9]

다음과 같은 용어를 입력해 볼 수도 있습니다.

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>다음 단계
Node.js 및 hello USG 데이터 집합에 따라 hello 첫 번째 Azure 검색 자습서입니다. 시간이 지남에 따라 추가 검색 기능을 사용자 지정 솔루션에서 toouse 할 수 있습니다이 자습서 toodemonstrate를 확장 합니다.

Azure 검색에 대한 약간의 배경 지식이 이미 있는 경우 이 샘플을 기반으로 suggesters(사전 입력 또는 자동 완성 쿼리), 필터 및 패싯 탐색을 시작할 수 있습니다. 또한 개수를 추가 하 고 hello 결과 통해 사용자가 페이지로 이동할 수 있도록 문서를 일괄 처리 하 여 hello 검색 결과 페이지를 개선할 수 있습니다.

새 tooAzure 검색? 다른 자습서 toodevelop 만들 수는 이해 하는 것이 좋습니다. 방문 우리의 [설명서 페이지](https://azure.microsoft.com/documentation/services/search/) toofind 리소스를 더 합니다. Hello에 대 한 링크를 볼 수도 있습니다 우리의 [비디오 및 자습서 목록](search-video-demo-tutorial-list.md) tooaccess 자세한 정보.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
