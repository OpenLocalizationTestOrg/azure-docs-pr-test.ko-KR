---
title: "Azure 저장소 탐색기 (미리 보기) 0.8.7 aaaMicrosoft | Microsoft Docs"
description: "Microsoft Azure 저장소 탐색기 0.8.7(미리 보기)에 대한 릴리스 정보"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Microsoft Azure Storage 탐색기 0.8.7(미리 보기)
## <a name="overview"></a>개요
이 문서는 Azure 저장소 탐색기 0.8.7 미리 보기 릴리스에 대 한 hello 릴리스 정보를 포함합니다.

[Microsoft Azure 저장소 탐색기 (미리 보기)](./vs-azure-tools-storage-manage-with-storage-explorer.md) 는 Windows, macOS 등 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있도록 하는 독립 실행형 앱입니다.

## <a name="azure-storage-explorer-087-preview"></a>Azure Storage 탐색기 0.8.7(미리 보기)
### <a name="download-azure-storage-explorer-087-preview"></a>Azure Storage 탐색기 0.8.7(미리 보기) 다운로드
- [Windows용 Azure Storage 탐색기 0.8.7 미리 보기](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Mac용 Azure Storage 탐색기 0.8.7 미리 보기](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Linux용 Azure Storage 탐색기 0.8.7 미리 보기](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>새 업데이트
* 업데이트를 시작 하는 hello에서 tooresolve 충돌 다운로드 또는 hello에 세션 복사 방법을 선택할 수 있습니다 **활동** 창.
* Hello 저장소 리소스의 탭 toosee hello 전체 경로 가리키면 됩니다.
* 탭을 클릭 하 여 hello 왼쪽 탐색 창에서 해당 위치와 동기화 합니다.

### <a name="fixes"></a>수정 프로그램
* 수정됨: 저장소 탐색기는 이제 macOS에서 신뢰할 수 있는 앱입니다.
* 수정됨: Ubuntu 14.04가 다시 지원됩니다.
* 고정: 때로는 hello 계정 UI 추가 깜박입니다 구독을 로드 하는 경우.
* 고정: 경우에 따라 모든 저장소 리소스 hello 왼쪽 탐색 창에 나열 된 합니다.
* 고정: hello 작업 창 경우가 표시 빈 동작.
* 고정: hello 창 크기 hello 마지막 닫힌 세션에서 이제 유지 됩니다.
* 고정: hello에 대 한 여러 탭을 열 수 hello 상황에 맞는 메뉴를 사용 하 여 동일한 리소스입니다.

### <a name="known-issues"></a>알려진 문제
* 빠른 액세스는 구독 기반 항목에만 작동합니다. 로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.
* 빠르게 액세스할 수는 몇 초 toonavigate toohello 대상 리소스에 있는 리소스의 수에 따라 걸릴 수 있습니다.
* Blob 또는 파일 같은 hello에 업로드 세 개 이상의 그룹화가 시간은 오류가 발생할 수 있습니다.
* 검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되거나 처리되지 않은 예외가 발생할 수 있습니다.
* MacOS 등에서 hello 저장소 탐색기를 사용 하 여 처음으로 hello에 대 한 사용자의 권한 tooaccess hello 키 집합을 요청 하는 여러 개의 프롬프트가 표시 될 수 있습니다. 선택 하는 것이 좋습니다 **항상 허용** hello 라는 메시지가 다시 표시 하지 않는 하므로

## <a name="previous-releases"></a>이전 릴리스
### <a name="features"></a>기능
#### <a name="main-features"></a>주요 기능
* macOS, Linux 및 Windows 버전
* 구독 별로 그룹화 하 여 저장소 계정의 tooview에 로그인 합니다.
    * 조직 계정, Microsoft 계정, 2FA, 등 사용
    * 프록시 설정 구성 및 관리
    * 로그아웃하여 계정 제거
* 사용 하 여 tooStorage 계정을 연결 합니다.
    * 계정 이름 및 키
    * 사용자 지정 끝점(Azure 중국 포함)
    * 저장소 계정에 대한 SAS URI
* Azure Resource Manager 및 클래식 저장소 지원
* blob, blob 컨테이너, 큐, 테이블 또는 파일 공유에 대한 SAS 키 생성
* 공유 액세스 서명 (SAS) 키를 가진 tooblob 컨테이너, 큐, 테이블 또는 파일 공유를 연결
* blob 컨테이너, 큐, 테이블 또는 파일 공유에 대한 저장된 액세스 정책 관리
* 저장소 에뮬레이터를 사용하는 로컬 개발 저장소(Windows만 해당)
* blob 컨테이너, 큐 또는 테이블 만들기 및 삭제
* $logs blob 컨테이너 및 $metrics 테이블 보기
* 특정 blob, 큐, 테이블 또는 파일 공유 검색
* 직접 링크 toostorage 계정 또는 컨테이너, 큐, 테이블 또는 파일 공유를 공유 하 고 쉽게 리소스에 액세스
* Blob 컨테이너, 테이블, 파일 공유 이름 바꾸기
* 기능 toomanage CORS 규칙을 구성 하 고
* 저장소 계정에 대한 기본 및 보조 키를 쉽게 복사
* 다운로드 및 업로드 시 데이터 무결성 및 일관성에 대해 MD5 검사 수행
* Blob 컨테이너, 테이블, 큐, 파일 공유 또는 hello 검색 상자에서 저장소 계정에 대 한 검색
* 이제 쉽게 탐색을 위한 pin 가장 자주 사용 되는 서비스 toohello 빠르게 액세스할 수 있습니다.
* 이제 다른 탭에 있는 여러 편집기를 열 수 있습니다. 단일 tooopen 임시 탭;를 클릭 합니다. tooopen 영구 탭을 두 번 클릭 합니다. Hello 임시 탭 toomake를 클릭할 수도 있습니다 것 영구 탭
* 빠른 컴퓨터에서 큰 파일에 대해 업로드 및 다운로드를 수행할 때 특히 성능 및 안정성이 개선되었습니다.
* म 재 hello 향상 된 범위 지정된 검색 및 범위 지정 추가 된 hello 개념에 도입 됩니다. 마우스 오른쪽 단추로 클릭-> 검색에서 "여기", 또는 수동으로 tooscope 해당 노드, hello 가리키기 아이콘을 통해 hello 경로 tooa 노드를 입력 합니다. 범위가 지정 되 면 해당 노드에서 시작 하는 hello 경로 toodeep 검색의 검색 용어 toohello 끝을 추가할 수 있습니다.
* 밝게(기본값), 어둡게, 고대비 검정 및 고대비 흰색 등의 다양한 테마를 추가했습니다.
* 이동 tooEdit-> 테마 toochange 테마 설정 기본 설정
* 이제 Linux에서는 64비트 OS가 필요합니다.
* 로고가 업데이트되었습니다.
#### <a name="blobs"></a>Blob
* Blob 보기 및 디렉터리 탐색
* Blob 및 폴더 업로드, 다운로드, 삭제 및 복사
* 열고 hello 내용을 텍스트와 그림 blob를 보려면
* blob 속성 및 메타데이터 보기 및 편집
* 접두사별로 blob 검색
* blob 및 blob 컨테이너에 대한 임대 만들기 및 중단
* 끌어 ' n tooupload 파일 삭제
* blob 및 폴더 이름 바꾸기
* 이제 blob 컨테이너에 빈 "가상" 폴더를 만들 수 있음
* Hello Blob 및 파일 속성을 수정할 수 있습니다.
#### <a name="tables"></a>테이블
* 보기 및 ODATA와 엔터티 쿼리 또는 쿼리 작성기 toocreate 복잡 한 쿼리를 사용 하 여
* 엔터티 추가, 편집, 삭제
* CSV 형식으로 테이블 내용 가져오기 및 내보내기(쿼리 결과 내보내기 포함)
* 열 순서 사용자 지정
* 기능 toosave 쿼리
#### <a name="queues"></a>큐
* 가장 최근의 32개 메시지 엿보기
* 메시지 추가, 큐에서 제거, 보기
* 큐 지우기
* म 있게 있습니다 toodecide 것인지 tooencode/디코딩에 큐 메시지
#### <a name="file-shares"></a>파일 공유
* 파일 보기 및 디렉터리 탐색
* 파일 및 디렉터리 업로드, 다운로드, 삭제 및 복사
* 파일 속성 보기
* 파일 및 디렉터리 이름 바꾸기

### <a name="bug-fixes"></a>버그 수정
* 수정됨: 화면 중단 문제
* 수정됨: 향상된 보안

### <a name="known-issues"></a>알려진 문제
* 검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되고, macOS 설치에 관리자 권한이 필요할 수 있습니다.
* Tooreenter 자격 증명 toofilter 구독 해야 하는 계정 설정 패널 표시 될 수 있습니다.
* blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다. blob, 파일 및 엔터티에 대한 다른 모든 속성 및 메타데이터는 이름을 바꾸는 동안 유지됩니다.
* Azure 스택 현재 지원 하지 않습니다 파일, tooexpand hello를 시도 하므로 **파일** 노드는 오류가 발생 함
* Linux 14.04 설치를 위해서는 gcc 버전을 업데이트하거나 업그레이드해야 합니다. hello 아래 단계에 설명 방법을 tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>이전 버전
#### <a name="october-2016-release-version-085"></a>2016년 10월 릴리스(버전 0.8.5)
* [Windows용 다운로드](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Mac용 다운로드](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Linux용 다운로드](https://go.microsoft.com/fwlink/?LinkId=809308)
