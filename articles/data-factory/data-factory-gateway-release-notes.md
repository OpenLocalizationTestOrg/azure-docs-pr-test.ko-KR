---
title: "데이터 관리 게이트웨이에 대 한 aaaRelease 노트 | Microsoft Docs"
description: "데이터 관리 게이트웨이 릴리스 정보"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>데이터 관리 게이트웨이에 대한 릴리스 정보
최신 데이터 통합에 대 한 hello 과제 중 하나에서 온-프레미스 toocloud toomove 데이터 tooand입니다. 데이터 팩터리 하면 데이터 관리 게이트웨이 온-프레미스 tooenable 하이브리드 데이터 이동의 설치할 수 있도록 하는 에이전트와의이 통합이 있습니다.

Hello 문서 데이터 관리 게이트웨이 대 한 자세한 내용은 다음 참조와 방법을 toouse 하기:

*  [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)
*  [Azure 데이터 팩터리를 사용하여 온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>현재 버전(2.10.6347.7)

### <a name="enhancements-"></a>향상된 기능
- 추가할 수 있습니다 허용 목록이 하지 않고 DNS 항목이 toowhitelist 서비스 버스 Azure IP 주소의 모든 방화벽에서 (필요한 경우). Azure Portal에서 각각의 DNS 항목을 찾을 수 있습니다(Data Factory -> '작성자 및 배포' -> '게이트웨이' -> JSON의 “serviceUrls”).
- 이제 HDFS 커넥터는 SSL 유효성 검사를 건너뛸 수 있도록 하여 자체 서명된 공용 인증서를 지원합니다.
- 업데이트 (기한 tooclock 오차) 하는 동안 오프 라인으로 게이트웨이 통해 문제를 수정된:



## <a name="earlier-versions"></a>이전 버전

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>향상된 기능
-   추가할 수 있습니다 허용 목록이 하지 않고 DNS 항목이 toowhitelist 서비스 버스 Azure IP 주소의 모든 방화벽에서 (필요한 경우). 자세한 내용은 다음을 참조하세요.
-   이제 too4.75 TB는 블록 blob의 hello 최대 지원 크기를 단일 블록 blob에서 데이터를 복사할 수 있습니다. 이전에는 195GB까지로 제한되었습니다.
-   복사 작업 중 작은 파일 여러 개의 압축을 푸는 동안 발생하는 메모리 부족 문제가 수정되었습니다.
-   고정된: 인덱스가 문서 DB tooan에서 복사 하는 동안 문제 범위를 벗어났습니다. 온-프레미스 SQL Server 멱 기능.
-   SQL 정리 스크립트가 복사 마법사에서 온-프레미스 SQL Server와 작동하지 않는 문제가 수정되었습니다.
-   고정: hello 끝에 공간이 있는 열 이름에서에서 작동 하지 않습니다 복사 작업입니다.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>향상된 기능
- 게이트웨이 컴퓨터를 다시 부팅할 때 자격 증명이 누락되는 문제가 수정되었습니다.
- 백업 파일을 사용하여 게이트웨이를 복원하는 중에 발생하는 등록 문제가 수정되었습니다.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>향상된 기능
- Oracle에서 10진수 null 값을 원본으로 잘못 읽는 문제가 수정되었습니다.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>새로운 기능
- 고객이 게이트웨이 등록 경험에 대한 피드백을 제공할 수 있습니다.
- 새 압축 형식 지원: ZIP (Deflate)

### <a name="enhancements-"></a>향상된 기능
- Oracle Sink, HDFS 원본에 대한 성능 개선
- 게이트웨이 자동 업데이트, 게이트웨이 병렬 처리 용량에 대한 버그 수정


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>향상된 기능
- 보다 강력 하 고 향상 된 게이트웨이 등록 경험-이제 응답성 hello 등록 경험을 낮추는 hello 게이트웨이 등록 프로세스 중 진행 상태를 추적할 수 있습니다.
- 이 업데이트 된 hello 게이트웨이 백업 파일이 없는 경우에 게이트웨이 복원 프로세스-있습니다 향상 게이트웨이 복구할 수 있습니다. 이 포털에서 tooreset 연결 된 서비스 자격 증명을 요구 합니다.
- 버그 수정

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>새로운 기능

- 이제 데이터 원본 자격 증명을 로컬로 저장할 수 있습니다. hello 자격 증명은 암호화 됩니다. hello 데이터 원본 자격 증명 복구할 수 있습니다 및 기존의 모든 온-프레미스 게이트웨이 hello에서 내보낼 수 있는 hello 백업 파일을 사용 하 여 복원 합니다.

### <a name="enhancements-"></a>향상된 기능

- 더 강력하게 향상된 게이트웨이 등록 환경을 제공합니다.
- 복사 마법사를 텍스트 형식에 대 한 QuoteChar 구성의 자동 검색을 지원 하 고 hello 개선 전체 검색 정확도 서식을 지정 합니다.

## <a name="2361002"></a>2.3.6100.2

- 온-프레미스 파일 시스템 및 HDFS의 텍스트 파일에 대해 복사 마법사의 firstRowAsHeader 및 SkipLineCount 자동 검색을 지원합니다.
- 서비스 버스와 게이트웨이 간의 네트워크 연결의 hello 안정성 향상
- 몇 가지 버그 수정


## <a name="2260721"></a>2.2.6072.1

*  Hello 게이트웨이 구성 관리자를 사용 하 여 hello 게이트웨이에 대 한 HTTP 프록시를 설정할 수 있도록 지원 합니다. Azure Blob, Azure 테이블, Azure Data Lake 및 DocumentDB가 구성되어 있는 경우 HTTP 프록시를 통해 액세스할 수 있습니다.
*  데이터를 복사 하는 경우 TextFormat에 대 한 처리는 지원 헤더 tooAzure Blob, Azure 데이터 레이크 저장소 온-프레미스 파일 시스템 및 온-프레미스 HDFS /입니다.
*  블록 Blob는 지원 데이터 복사 추가 Blob 및 페이지 Blob에서 hello와 함께 이미 하도록 지원 합니다.
*  새 게이트웨이 상태를 소개 **온라인 (제한 됨)**, 복사 마법사에 대 한 hello 대화형 작업 지원을 제외 하 고 작동 하는 hello 게이트웨이의 해당 hello 주요 기능을 나타냅니다.
*  등록 키를 사용 하 여 게이트웨이 등록의 hello 견고성을 향상 시킵니다.

## <a name="216040"></a>2.1.6040.

*  DB2 드라이버가 지금 hello 게이트웨이 설치 패키지에 포함 되어 있습니다. Tooinstall 필요가 없습니다 것 별도로 합니다.
*  Z/OS 용 DB2 및 DB2 driver에서는 이제 i (AS / 400) hello 이미 지원 되는 플랫폼 (Linux, Unix 및 Windows)와 함께 합니다.
*  온-프레미스 데이터 저장소에 대한 Azure Cosmos DB를 원본 또는 대상으로 사용하도록 지원합니다.
*  범용 저장소 계정을 지원 하는 hello와 함께 데이터에서 / toocold/핫 blob 저장소에 이미 복사 하도록 지원 합니다.
*  Tooconnect tooon 온-프레미스 사용 하면 원격 로그인 권한 사용 하 여 게이트웨이 통해 SQL Server.  

## <a name="2060131"></a>2.0.6013.1

*  수동 설치 하는 동안 한 게이트웨이에서 사용 되는 hello 언어/문화권 toobe를 선택할 수 있습니다.

*  게이트웨이가 예상 대로 작동 하지 않으면 마지막 7 일 tooMicrosoft toofacilitate 문제 해결의 hello 문제의 toosend 게이트웨이 로그 선택할 수 있습니다. 게이트웨이 사용할 경우 연결 된 toohello 클라우드 서비스 게이트웨이 로그를 보관 한 toosave 수도 있습니다.  

*  게이트웨이 구성 관리자에 대한 사용자 인터페이스 개선 사항:

    *  Hello 홈 탭에 더 많은 보이는 게이트웨이 상태를 확인 합니다.

    *  재구성되고 간소화된 컨트롤입니다.

    *  Hello를 사용 하 여 저장소에서 데이터를 복사할 수 [복사 코드 필요 없는 미리 보기 도구](data-factory-copy-data-wizard-tutorial.md)합니다. 이 기능에 대한 전반적인 세부 정보는 [준비된 복사](data-factory-copy-activity-performance.md#staged-copy) 를 참조하세요.
*  Azure 기계 학습에는 온-프레미스 SQL Server 데이터베이스에서 직접 데이터 관리 게이트웨이 tooingress 데이터를 사용할 수 있습니다.

*  성능 개선

    * 코드가 없는 미리 보기 도구의 SQL Server에 대해 스키마/미리 보기 보기의 성능이 향상됩니다.

## <a name="11259531"></a>1.12.5953.1

*  버그 수정

## <a name="11159181"></a>1.11.5918.1

*  Hello 게이트웨이 이벤트 로그의 최대 크기를 MB too40 1MB에서 증가 되었습니다.

*  게이트웨이를 자동 업데이트하는 동안 다시 시작이 필요하면 경고 대화 상자가 표시됩니다. 나중에 또는 다음 toorestart 오른쪽을 선택할 수 있습니다.

*  자동 업데이트가 실패하면 게이트웨이 설치 관리자는 자동 업데이트를 최대 3회까지 다시 시도합니다.

*  성능 개선

    * 코드가 없는 복사 시나리오를 통해 온-프레미스 서버의 큰 테이블을 로드하는 성능을 개선합니다.

*  버그 수정

## <a name="11058921"></a>1.10.5892.1

*  성능 개선

*  버그 수정

## <a name="1958652"></a>1.9.5865.2

*  0 터치 자동 업데이트 기능
*  게이트웨이 상태 표시기 포함 새 트레이 아이콘
*  기능 너무 "지금 업데이트" hello 클라이언트에서
*  기능 tooset 업데이트 일정 시간
*  자동 업데이트를 설정/해제하기 위한 PowerShell 스크립트
*  JSON 형식 파일 지원  
*  성능 개선
*  버그 수정

## <a name="1858221"></a>1.8.5822.1

*  문제 해결 환경 개선
*  성능 개선
*  버그 수정

### <a name="1757951"></a>1.7.5795.1

*  성능 개선
*  버그 수정

### <a name="1757641"></a>1.7.5764.1

*  성능 개선
*  버그 수정

### <a name="1657351"></a>1.6.5735.1

*  온-프레미스 HDFS 원본/싱크 지원
*  성능 개선
*  버그 수정

### <a name="1656961"></a>1.6.5696.1

*  성능 개선
*  버그 수정

### <a name="1656761"></a>1.6.5676.1

*  구성 관리자에서 진단 도구 지원
*  Azure 데이터 팩터리에 대 한 테이블 데이터 원본의 테이블 열 지원
*  Azure 데이터 팩터리에 대 한 SQL DW 지원
*  Azure 데이터 팩터리에 대한 BlobSource 및 FileSource의 단독 지원
*  CopyBehavior 지원 – Azure Data Factory의 이진 복사 기능을 통해 BlobSink 및 FileSink에서 MergeFiles, PreserveHierarchy, FlattenHierarchy 지원
*  Azure 데이터 팩터리의 진행률을 보고하는 복사 작업 지원
*  Azure 데이터 팩터리에 대한 데이터 원본 연결 유효성 검사 지원
*  버그 수정

### <a name="1656721"></a>1.6.5672.1

*  Azure 데이터 팩터리에 대 한 ODBC 데이터 원본의 테이블 이름 지원
*  성능 개선
*  버그 수정

### <a name="1656581"></a>1.6.5658.1

*  Azure 데이터 팩터리에 대 한 파일 싱크 지원
*  Azure 데이터 팩터리에 대 한 이진 복사본에서 계층 구조 유지 지원
*  Azure 데이터 팩터리에 대한 복사 작업 멱등성 지원
*  버그 수정

### <a name="1656401"></a>1.6.5640.1

*  Azure 데이터 팩터리(ODBC, OData, HDFS)에 대 한 3개 더 많은 데이터 원본 지원
*  Azure 데이터 팩터리에 대 한 csv 파서에서 따옴표 문자 지원
*  압축 지원(BZip2)
*  버그 수정

### <a name="1556121"></a>1.5.5612.1

*  Azure Data Factory에 대해 관계형 데이터베이스 5개(MySQL, PostgreSQL, DB2, Teradata, Sybase) 지원
*  압축 지원(Gzip 및 Deflate)
*  성능 개선
*  버그 수정

### <a name="1455491"></a>1.4.5549.1

*  Azure 데이터 팩터리에 대 한 Oracle 데이터 원본 지원 추가
*  성능 개선
*  버그 수정

### <a name="1454921"></a>1.4.5492.1

*  Microsoft Azure 데이터 팩터리 및 Office 365 Power BI 서비스를 지원하는 통합 된 이진 파일
*  Hello 구성 UI 및 등록 프로세스를 구체화합니다
*  Azure 데이터 팩터리 - SQL Server 데이터 원본에 대한 Azure 수신 및 송신 지원

### <a name="1253031"></a>1.2.5303.1

*  시간 초과 문제 toosupport 보다 시간이 많이 걸리는 데이터 원본 연결을 수정 합니다.

### <a name="1155268"></a>1.1.5526.8

*  설치하는 동안 필수 요소로 .NET Framework 4.5.1이 필요합니다.

### <a name="1051442"></a>1.0.5144.2

*  Azure 데이터 팩터리 시나리오에 영향을 주는 변경은 없습니다.
