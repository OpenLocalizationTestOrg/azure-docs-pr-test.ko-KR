---
title: "aaaMicrosoft Azure 저장소 탐색기 (미리 보기) 릴리스 정보 | Microsoft Docs"
description: "Microsoft Azure Storage 탐색기(미리 보기) 릴리스 정보"
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
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Microsoft Azure Storage 탐색기(미리 보기) 릴리스 정보

이전 버전에 대 한 릴리스 정보 뿐만 아니라 Azure 저장소 탐색기 0.8.16에 대 한 정보 (Preview) 릴리스 hello 릴리스가 나와 있습니다.

[Microsoft Azure 저장소 탐색기 (미리 보기)](./vs-azure-tools-storage-manage-with-storage-explorer.md) 는 Windows, macOS 등 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있도록 하는 독립 실행형 앱입니다.

## <a name="version-0816-preview"></a>버전 0.8.16(미리 보기)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Azure Storage 탐색기 0.8.16(미리 보기) 다운로드
- [Windows용 Azure Storage 탐색기 0.8.16(미리 보기)](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Mac용 Azure Storage 탐색기 0.8.16(미리 보기)](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Linux용 Azure Storage 탐색기 0.8.16(미리 보기)](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>새로 만들기
* Blob을 열 때 저장소 탐색기 묻는 메시지가 나타납니다 tooupload hello 다운로드 한 파일 변경이 감지 된 경우
* 향상된 Azure Stack 로그인 환경
* Hello에 너무 작은 업로드/다운로드의 향상 된 hello 성능을 파일 같은 시간


### <a name="fixes"></a>수정 프로그램
* 일부 blob 유형에 대 한 선택 너무 "자동 대체" 업로드 충돌 하는 동안 하면 경우에 따라 발생 hello 업로드를 다시 시작 합니다. 
* 버전 0.8.15에서 업로드는 경우에 따라 99%에서 중단됩니다.
* 아직 존재 하지 않는 tooupload tooa 디렉터리를 선택 하는 경우 파일 tooa 파일 공유를 업로드, 하는 경우 업로드가 실패 합니다.
* 저장소 탐색기가 공유 액세스 서명 및 테이블 쿼리에 대한 타임스탬프를 잘못 생성합니다.


알려진 문제
* 현재 이름 및 키 연결 문자열을 사용할 수 없습니다. Hello 다음 릴리스에서 수정 될 예정입니다. 그때까지는 이름 및 키로 연결 기능을 사용할 수 있습니다.
* Tooopen 잘못 된 Windows 파일 이름으로 파일을 시도 하면 hello 다운로드 한 파일 없음 오류 발생 합니다.
* 작업에 "취소"를 클릭 한 후 해당 작업 toocancel 시간이 걸릴 수 있습니다. Hello Azure 저장소 노드 라이브러리의 제한 사항입니다.
* Blob 업로드를 완료 한 후 hello 업로드 중에서 어느 hello 탭 새로 고쳐집니다. 이전 동작에서 변경 된 내용 이므로 toobe toohello 루트에 있는 hello 컨테이너의 다시 이동 해도 됩니다.
* 잘못 된 PIN/스마트 카드 인증서 hello 다음 toorestart 순서 toohave 저장소 탐색기에에서 필요 합니다를 선택 하는 경우 기억해 해당 결정 합니다.
* hello 계정 설정 패널 tooreenter 자격 증명 toofilter 구독 해야 하는 표시할 수 있습니다.
* blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다. Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.
* Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다.
* Ubuntu 14.04에 사용자를 위해 GCC toodate 중일 tooensure 해야-hello를 실행 하 여이 작업을 수행할 수 있습니다 명령 하 고 다음 컴퓨터를 다시 시작 해야 합니다.

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Ubuntu 17.04에 사용자를 위해 tooinstall GConf 해야-이렇게 하 여 hello 명령, 다음 컴퓨터를 다시 시작 하 고 실행 합니다.

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>버전 0.8.14(미리 보기)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Azure Storage 탐색기 0.8.14(미리 보기) 다운로드
* [Windows용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Mac용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Linux용 Azure Storage 탐색기 0.8.14(미리 보기) 다운로드](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>새로 만들기

* 순서 tootake 활용 한 몇 가지 중요 한 보안 업데이트에서에서 업데이트 된 전자 버전 too1.7.2
* 이제 빠르게 액세스할 수 있습니다 hello 온라인 문제 해결 가이드 hello 도움말 메뉴에서
* Storage 탐색기 문제 해결 [가이드][2]
* [지침] [ 3] tooan 스택 Azure 구독 연결

### <a name="known-issues"></a>알려진 문제

* Hello 삭제 폴더 확인 대화 상자에서 단추 linux hello 마우스 클릭 하 여 등록 하지 않는 합니다. Toouse hello Enter 키를이 문제를 해결
* 잘못 된 PIN/스마트 카드 인증서 hello 다음 toorestart 순서 toohave 저장소 탐색기에에서 필요 합니다를 선택 하면 잊은 hello 의사 결정
* Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.
* hello 계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.
* blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다. Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.
* Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다. 
* Ubuntu 14.04 설치 요구 gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade 아래에

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>이전 릴리스

* [버전 0.8.13](#version-0813)
* [버전 0.8.12/0.8.11/0.8.10](#version-0812--0811--0810)
* [버전 0.8.9/0.8.8](#version-089--088)
* [버전 0.8.7](#version-087)
* [버전 0.8.6](#version-086)
* [버전 0.8.5](#version-085)
* [버전 0.8.4](#version-084)
* [버전 0.8.3](#version-083)
* [버전 0.8.2](#version-082)
* [버전 0.8.0](#version-080)
* [버전 0.7.20160509.0](#version-07201605090)
* [버전 0.7.20160325.0](#version-07201603250)
* [버전 0.7.20160129.1](#version-07201601291)
* [버전 0.7.20160105.0](#version-07201601050)
* [버전 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>버전 0.8.13
05/12/2017

#### <a name="new"></a>새로 만들기

* Storage 탐색기 문제 해결 [가이드][2]
* [지침] [ 3] tooan 스택 Azure 구독 연결

#### <a name="fixes"></a>수정 프로그램

* 수정됨: 파일 업로드 시의 높은 메모리 부족 오류 발생 가능성이 수정되었습니다.
* 수정됨: 이제 PIN/스마트 카드를 사용하여 로그인할 수 있습니다.
* 수정됨: 이제 포털에서 열기가 Azure 중국, Azure 독일, Azure 미국 정부 및 Azure Stack에서 작동합니다.
* 고정: 폴더 tooa blob 컨테이너를 업로드 하는 동안 "작업이 잘못 되었습니다." 오류가 경우가 발생 합니다.
* 수정됨: 스냅숏을 관리하는 동안 모두 선택 기능이 사용할 수 없도록 설정되었습니다.
* 고정: hello 기본 blob의 hello 메타 데이터 가져오기 덮어써질 스냅숏과 hello 속성을 검토 한 후

#### <a name="known-issues"></a>알려진 문제

* 잘못 된 PIN/스마트 카드 인증서 hello 다음 toorestart 순서 toohave 저장소 탐색기에에서 필요 합니다를 선택 하면 잊은 hello 의사 결정
* 확대 또는 축소, 동안 hello 확대/축소 수준을 일시적으로 다시 설정 toohello 기본 수준
* Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.
* hello 계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.
* blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다. Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.
* Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다. 
* Ubuntu 14.04 설치 요구 gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade 아래에

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>버전 0.8.12/0.8.11/0.8.10
04/07/2017

#### <a name="new"></a>새로 만들기

* 저장소 탐색기 자동으로 닫힙니다 hello 업데이트 알림에서 업데이트를 설치 하는 경우
* 현재 위치 빠른 액세스 기능이 자주 액세스하는 리소스 사용을 위한 향상된 환경을 제공합니다.
* Hello Blob 컨테이너 편집기에 표시 임대 된 blob에 속해 있는 가상 컴퓨터
* 이제 hello 왼쪽 패널 축소
* 검색 지금 실행 hello에서 동일한 시간 다운로드로
* 리소스 또는 선택의 Blob 컨테이너, 파일 공유 및 테이블 편집기 toosee hello 크기 hello에 통계를 사용 합니다.
* 이제 로그인 tooAzure Active Directory (AAD) Azure 스택 계정을 기반으로 할 수 있습니다. 
* 이제 업로드 보관 32 개 MB tooPremium 저장소 계정 파일 수 있습니다.
* 손쉬운 사용 옵션 지원이 개선되었습니다.
* 신뢰할 수 있는 base64 이제 추가할 수 있습니다 이동 tooEdit-X.509 SSL 인증서로 인코딩하지&gt; SSL 인증서-&gt; 인증서 가져오기

#### <a name="fixes"></a>수정 프로그램

* 고정: 계정의 자격 증명을 새로 고친 후 hello 트리 보기는 경우에 따라 자동으로 새로 고쳐지지 않습니다
* 수정됨: 에뮬레이터 큐 및 테이블에 대해 SAS를 생성하면 잘못된 URL이 생성되는 현상이 수정되었습니다.
* 수정됨: 이제 프록시가 사용하도록 설정된 상태에서 Premium Storage 계정을 확장할 수 있습니다.
* 고정: hello 적용 단추 hello 계정 관리 페이지에는 1 또는 0 계정을 선택한 경우 작동 하지 않습니다.
* 수정됨: 충돌을 해결해야 하는 Blob 업로드가 실패할 수 있는 현상이 버전 0.8.11에서 수정되었습니다. 
* 수정됨: 버전 0.8.11에서 피드백 전송이 중단되는 현상이 버전 0.8.12에서 수정되었습니다. 

#### <a name="known-issues"></a>알려진 문제

* Too0.8.10를 업그레이드 한 후 해야 toorefresh 모든 자격 증명입니다.
* 확대 또는 축소, 동안 hello 확대/축소 수준을 toohello 기본 수준 다시 설정 일시적으로 수 있습니다.
* Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간은 오류가 발생할 수 있습니다.
* hello 계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.
* blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다. Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.
* Azure Stack은 현재 파일 공유를 지원하지 않지만, 연결된 Azure Stack 저장소 계정에는 파일 공유 노드가 계속 표시됩니다. 
* Ubuntu 14.04 설치 요구 gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade 아래에

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>버전 0.8.9/0.8.8
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>새로 만들기

* 저장소 탐색기 0.8.9 hello 업데이트에 대 한 최신 버전을 자동으로 다운로드 됩니다.
* 핫픽스: 포털을 사용 하 여 SAS URI tooattach 저장소 계정을 결과 오류가 생성 됩니다.
* 이제 Blob 스냅숏을 만들고 관리하고 수준을 올릴 수 있습니다.
* 이제 tooAzure 중국, Azure 독일 및 Azure 미국 정부 계정을에 서명할 수 있습니다.
* 이제 hello 확대/축소 수준을 변경할 수 있습니다. 축소 및 확대/축소 다시 설정에서 보기 메뉴 tooZoom hello에에서 hello 옵션을 사용 합니다.
* 이제 Blob 및 파일의 사용자 메타데이터에서 유니코드 문자가 지원됩니다.
* 내게 필요한 옵션이 개선되었습니다.
* hello 업데이트 알림에서 hello 다음 버전의 릴리스 정보를 볼 수 있습니다. Hello hello 도움말 메뉴에서 현재 릴리스 정보를 볼 수 있습니다.

#### <a name="fixes"></a>수정 프로그램

* 고정: hello 버전 번호는 이제 올바르게 표시 Windows에서 제어판의
* 고정: 검색은 더 이상 제한 too50, 000 노드
* 고정: 업로드 tooa 파일 공유 된 영원히 hello 대상 디렉터리가 아직 없는 경우
* 수정됨: 오랫동안 실행되는 업로드와 다운로드의 안정성이 개선되었습니다.

#### <a name="known-issues"></a>알려진 문제

* 확대 또는 축소, 동안 hello 확대/축소 수준을 toohello 기본 수준 다시 설정 일시적으로 수 있습니다.
* 빠른 액세스는 구독 기반 항목에만 작동합니다. 로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.
* 빠르게 액세스할 수는 몇 초 toonavigate toohello 대상 리소스에 있는 리소스의 수에 따라 걸릴 수 있습니다.
* Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간은 오류가 발생할 수 있습니다.

12/16/2016
### <a name="version-087"></a>버전 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>새로 만들기

* 업데이트를 시작 하는 hello에서 tooresolve 충돌 다운로드 하거나 세션 hello 활동 창에서 복사 방법을 선택할 수 있습니다.
* Hello 저장소 리소스의 탭 toosee hello 전체 경로 위로 마우스를 가져가고합니다
* Hello 왼쪽 탐색 창에서 해당 위치와 동기화 하는 탭을 클릭할 때

#### <a name="fixes"></a>수정 프로그램

* 수정됨: 이제 Mac에서도 Storage 탐색기를 신뢰할 수 있는 앱으로 사용할 수 있습니다.
* 수정됨: Ubuntu 14.04가 다시 지원됩니다.
* 고정: 때로는 hello 계정을 추가 구독을 로드할 때 UI 깜박이
* 고정: 경우에 따라 모든 저장소 리소스 hello 왼쪽 탐색 창에 나열 된
* 고정: hello 작업 창 경우가 표시 빈 동작
* 고정: hello 창 크기 hello 마지막 닫힌 세션에서 이제 유지 됩니다.
* 고정: hello에 대 한 여러 탭을 열 수 hello 상황에 맞는 메뉴를 사용 하 여 동일한 리소스

#### <a name="known-issues"></a>알려진 문제

* 빠른 액세스는 구독 기반 항목에만 작동합니다. 로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.
* 빠르게 액세스할 수는 몇 초 toonavigate toohello 대상 리소스에 있는 리소스의 수에 따라 걸릴 수 있습니다.
* Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.
* 검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되거나 처리되지 않은 예외가 발생할 수 있습니다.
* MacOS 등에서 hello 저장소 탐색기를 사용 하 여 처음으로 hello에 대 한 사용자의 권한 tooaccess 키 집합을 요청 하는 여러 개의 프롬프트가 표시 될 수 있습니다. 항상 허용 되도록 선택 hello 프롬프트 다시 나타나지 않습니다 것이 좋습니다.

11/18/2016
### <a name="version-086"></a>버전 0.8.6

#### <a name="new"></a>새로 만들기

* 이제 쉽게 탐색을 위한 pin 가장 자주 사용 되는 서비스 toohello 빠르게 액세스할 수 있습니다.
* 이제 다른 탭에 있는 여러 편집기를 열 수 있습니다. 단일 tooopen 임시 탭;를 클릭 합니다. tooopen 영구 탭을 두 번 클릭 합니다. 클릭할 수도 있습니다 hello 임시 탭 toomake에 해당 영구 탭
* 특히 빠른 컴퓨터에서 큰 파일에 대해 업로드 및 다운로드를 수행할 때 성능 및 안정성이 크게 개선되었습니다.
* 이제 blob 컨테이너에 빈 "가상" 폴더를 만들 수 있음
* 새롭게 향상된 하위 문자열 검색에 범위 지정 검색 기능이 다시 도입되었으므로 이제 검색 시에 다음의 두 가지 옵션을 사용할 수 있습니다. 
    * 전역 검색-hello 검색 텍스트 상자에 검색 용어 입력
    * 범위 지정된 검색-hello 돋보기 아이콘 다음 tooa 노드를 클릭 한 다음 hello 경로 검색 용어 toohello 끝에 추가 또는 마우스 오른쪽 단추로 클릭 한 검색에서 "여기" 선택
* 밝게(기본값), 어둡게, 고대비 검정 및 고대비 흰색 등의 다양한 테마를 추가했습니다. TooEdit-이동&gt; 테마 toochange 테마 설정 기본 설정
* Blob 및 파일 속성을 수정할 수 있습니다.
* 이제 인코딩된 큐 메시지(Base64)와 인코딩되지 않은 큐 메시지가 모두 지원됩니다.
* 이제 Linux에서는 64비트 OS를 사용해야 합니다. 이번 릴리스에서는 64비트 Ubuntu 16.04.1 LTS만 지원됩니다.
* 로고가 업데이트되었습니다.

#### <a name="fixes"></a>수정 프로그램

* 수정됨: 화면 중단 문제
* 수정됨: 향상된 보안
* 수정됨: 가끔씩 연결된 계정이 중복으로 표시되는 현상이 수정되었습니다.
* 수정됨: Blob의 콘텐츠 형식이 정의되어 있지 않으면 예외가 발생할 수 있는 현상이 수정되었습니다.
* 고정: 빈 테이블에 대 한 쿼리 패널 열기 hello 수 없습니다.
* 수정됨: 검색의 버그가 확인 및 수정되었습니다.
* 고정: "부하 추가 정보"를 클릭 하면 50 too100에서 로드 하는 리소스의 hello 수 증가
* 수정됨: 이제는 첫 실행 시 계정에 로그인하면 기본적으로 해당 계정의 모든 구독이 선택됩니다. 

#### <a name="known-issues"></a>알려진 문제

* Ubuntu 14.04에서이 버전의 hello 저장소 탐색기를 실행할 수 없습니다.
* tooopen 동일한 리소스에 계속 하지 마십시오 클릭 hello에 대 한 여러 탭 hello 동일한 리소스입니다. 다른 리소스 클릭 하 고 이전 단계로 이동 하 고 원래 리소스 tooopen hello 다시 클릭 다른 탭에서 
* 빠른 액세스는 구독 기반 항목에만 작동합니다. 로컬 리소스 또는 키나 SAS 토큰을 통해 연결된 리소스는 이번 릴리스에서 지원되지 않습니다.
* 빠르게 액세스할 수는 몇 초 toonavigate toohello 대상 리소스에 있는 리소스의 수에 따라 걸릴 수 있습니다.
* Blob 또는 동일 hello에서 업로드 파일 3 개 이상의 그룹화가 시간 오류가 발생할 수 있습니다.
* 검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하되거나 처리되지 않은 예외가 발생할 수 있습니다.

10/03/2016
### <a name="version-085"></a>버전 0.8.5

#### <a name="new"></a>새로 만들기

* 사용 하 여 포털에서 생성 된 SAS 키 tooattach tooStorage 이제 계정 및 리소스

#### <a name="fixes"></a>수정 프로그램

* 경우에 따라 검색 하는 동안 경합 상태는 확장할 수 없는 노드 toobecome를 발생 수정 되었습니다.
* 고정: "HTTP 사용" 경우 작동 하지 않음 tooStorage 계정의 계정 이름과 키를 사용 하 여 연결
* 수정됨: SAS 키(구체적으로는 Portal에서 생성된 키)에서 "후행 슬래시" 오류가 반환되는 현상이 수정되었습니다.
* 수정됨: 테이블 가져오기 문제가 수정되었습니다.
    * 가끔씩 파티션 키와 행 키가 서로 바뀌는 문제
    * 파티션 키를 "null" 없습니다 tooread

#### <a name="known-issues"></a>알려진 문제

* 검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하될 수 있습니다.
* 시도 tooexpand 파일에서는 오류를 표시 하므로 azure 스택 파일을 현재 지원 하지 않습니다.

09/12/2016
### <a name="version-084"></a>버전 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>새로 만들기

* 직접 링크 toostorage 계정, 컨테이너, 큐, 테이블, 생성 또는 공유 하기 위한 쉽고 파일 공유 액세스 tooyour 리소스-Windows 및 Mac OS 지원
* Blob 컨테이너, 테이블, 큐, 파일 공유 또는 hello 검색 상자에서 저장소 계정에 대 한 검색
* 이제 절 hello 테이블 쿼리 작성기에서를 그룹 수 있습니다.
* SAS에 연결된 계정 및 컨테이너 내에서 Blob 컨테이너, 파일 공유, 테이블, Blob, Blob 폴더, 파일 및 디렉터리 복사/붙여넣기 및 이름 바꾸기를 수행할 수 있습니다.
* 이제 Blob 컨테이너와 파일 공유의 이름 바꾸기 및 복사 시에 속성과 메타데이터가 보존됩니다.

#### <a name="fixes"></a>수정 프로그램

* 수정됨: 부울 또는 이진 속성을 포함하는 테이블 엔터티를 편집할 수 없는 문제가 수정되었습니다.

#### <a name="known-issues"></a>알려진 문제

* 검색 기능이 약 50,000개 노드에서 검색을 처리하지만 이러한 검색 후에 성능이 저하될 수 있습니다.

08/03/2016
### <a name="version-083"></a>버전 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>새로 만들기

* 컨테이너, 테이블, 파일 공유의 이름을 바꿀 수 있습니다.
* 쿼리 작성기 환경이 개선되었습니다.
* 기능 toosave 및 부하 쿼리
* 직접 링크 toostorage 계정 또는 컨테이너, 큐, 테이블 또는 파일 공유를 공유 하 고 쉽게 리소스에 액세스 (Windows 전용-macOS 지원 출시 예정!)
* 기능 toomanage CORS 규칙을 구성 하 고

#### <a name="fixes"></a>수정 프로그램

* 수정됨: Microsoft 계정을 8-12시간마다 다시 인증해야 하는 문제가 수정되었습니다.

#### <a name="known-issues"></a>알려진 문제

* 경우에 따라 hello UI 수 중지 된 것 처럼-이 문제를 해결 하는 사용 하면 hello 창 최대화
* macOS 설치 시 관리자 권한이 필요할 수 있습니다.
* 계정 설정 패널 순서 toofilter 구독에 자격 증명 tooreenter 해야 표시 될 수 있습니다.
* 파일 공유 이름 바꾸기, blob 컨테이너 및 테이블 메타 데이터 또는 파일 공유 할당량, 공용 액세스 수준 액세스 정책 등 hello 컨테이너의 다른 속성을 유지 하지 않습니다.
* blob 이름을 바꿀 경우(개별적으로 또는 이름이 바뀐 blob 컨테이너 내에서) 스냅숏을 보존되지 않습니다. Blob, 파일 및 엔터티의 기타 모든 속성과 메타데이터는 이름을 바꾸어도 보존됩니다.
* SAS에 연결된 계정 내에서는 리소스 복사 또는 이름 바꾸기가 작동하지 않습니다.

07/07/2016
### <a name="version-082"></a>버전 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>새로 만들기

* Storage 계정이 구독별로 그룹화됩니다. 키 또는 SAS를 통해 연결된 개발 Storage 및 리소스는 (로컬 및 연결됨) 노드 아래에 표시됩니다.
* "Azure 계정 설정" 패널에서 계정을 로그오프할 수 있습니다.
* 프록시 설정을 tooenable 구성 및 로그인 관리
* Blob 임대를 작성/중단할 수 있습니다.
* 클릭 한 번으로 Blob 컨테이너, 큐, 테이블 및 파일을 열 수 있습니다.

#### <a name="fixes"></a>수정 프로그램

* 수정됨: .NET 또는 Java 라이브러리와 함께 삽입된 큐 메시지가 Base64에서 올바르게 디코드되지 않는 현상이 수정되었습니다.
* 수정됨: $metrics 테이블이 Blob Storage 계정에 대해 표시되지 않는 현상이 수정되었습니다.
* 수정됨: 로컬(개발) 저장소에 대해 테이블 노드가 작동하지 않는 현상이 수정되었습니다.

#### <a name="known-issues"></a>알려진 문제

* macOS 설치 시 관리자 권한이 필요할 수 있습니다.

06/15/2016
### <a name="version-080"></a>버전 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>새로 만들기

* 파일 공유 지원: 파일 및 디렉터리 보기/업로드/다운로드/복사, SAS URI 만들기 및 연결이 지원됩니다.
* TooStorage SAS Uri 또는 계정 키와 연결 하기 위한 사용자 환경 개선
* 테이블 쿼리 결과를 내보낼 수 있습니다.
* 테이블 열 다시 정렬 및 사용자 지정이 가능합니다.
* 메트릭이 사용하도록 설정된 Storage 계정의 $logs Blob 컨테이너와 $metrics 테이블을 확인할 수 있습니다.
* 내보내기 및 가져오기 동작이 개선되어 이제 속성 값 형식이 포함됩니다.

#### <a name="fixes"></a>수정 프로그램

* 수정됨: 큰 Blob를 업로드하거나 다운로드하면 업로드/다운로드가 완전히 진행되지 않는 현상이 수정되었습니다.
* 고정: 편집, 추가 또는 숫자 문자열 값 ("1")가 있는 엔터티를 가져오는 변환 toodouble
* Hello 로컬 개발 환경에서 문제가 해결된 됨 없습니다 tooexpand hello 테이블 노드

#### <a name="known-issues"></a>알려진 문제

* $metrics 테이블이 Blob Storage 계정에 대해 표시되지 않습니다.
* Base64 인코딩을 사용 하 여 hello 메시지를 인코딩하도록 경우 프로그래밍 방식으로 추가 하는 큐 메시지 제대로 표시 되지 않을 수 있습니다.

05/17/2016
### <a name="version-07201605090"></a>버전 0.7.20160509.0

#### <a name="new"></a>새로 만들기

* 앱 작동 중단 시의 오류가 보다 효율적으로 처리됩니다.

#### <a name="fixes"></a>수정 프로그램

* 로그인 자격 증명이 필요할 때 정보 표시줄 메시지가 가끔씩 표시되지 않는 버그가 수정되었습니다.

#### <a name="known-issues"></a>알려진 문제

* 테이블: 추가, 편집 또는 모호 하 게 숫자 값을 "1" 또는 "1.0"와 같은 속성을 가진 엔터티를 가져오는 및 사용자 시도 toosend hello로 `Edm.String`, hello 값 hello 클라이언트는 Edm.Double로 API 통해 다시 나올지

03/31/2016

### <a name="version-07201603250"></a>버전 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>새로 만들기

* 테이블 지원: 엔터티 보기/쿼리/내보내기/가져오기 및 CRUD 작업이 지원됩니다.
* 큐 지원: 메시지 보기, 추가, 큐에서 제거가 지원됩니다.
* Storage 계정에 대해 SAS URI를 생성할 수 있습니다.
* SAS Uri를 사용 하 여 tooStorage 계정 연결
* 향후 업데이트 tooStorage 탐색기에 대 한 업데이트 알림
* 디자인이 업데이트되었습니다.

#### <a name="fixes"></a>수정 프로그램

* 성능과 안정성이 개선되었습니다.

### <a name="known-issues-amp-mitigations"></a>알려진 문제 &amp; 완화 방법

* 큰 Blob 파일 다운로드가 제대로 작동하지 않습니다. 이 문제를 해결하는 방법이 제공될 때까지는 AzCopy를 사용하는 것이 좋습니다. 
* 계정 자격 증명을 검색할 않았거나 hello 홈 폴더를 찾을 수 없거나에 쓸 수 없는 경우 캐시 되지 않습니다.
* Hello 사용자가 toosend 및 우리는 추가, 편집 또는 모호 하 게 숫자 값을 "1" 또는 "1.0"와 같은 속성을 가진 엔터티를 가져오는 경우로 `Edm.String`, hello 값 hello 클라이언트는 Edm.Double로 API 통해 다시 나올지
* 여러 줄로 된 레코드를 사용 하 여 CSV 파일을 가져올 때 hello 데이터 수 되었다고 해 가져오거나 스크램블

02/03/2016

### <a name="version-07201601291"></a>버전 0.7.20160129.1

#### <a name="fixes"></a>수정 프로그램

* Blob 업로드, 다운로드 및 복사 시의 전반적인 성능이 개선되었습니다.

01/14/2016

### <a name="version-07201601050"></a>버전 0.7.20160105.0

#### <a name="new"></a>새로 만들기

* Linux 지원 (패리티 기능 tooOSX)
* SAS(공유 액세스 서명) 키를 사용하여 Blob 컨테이너를 추가할 수 있습니다.
* Azure 중국의 Storage 계정을 추가할 수 있습니다.
* 사용자 지정 끝점이 있는 Storage 계정을 추가할 수 있습니다.
* 열고 hello 내용을 텍스트와 그림 blob를 보려면
* blob 속성 및 메타데이터 보기 및 편집

#### <a name="fixes"></a>수정 프로그램

* 고정: 업로드 또는 다운로드 많은 수의 blob (500 이상) 될 수 있습니다 하는 경우가 발생할 hello 앱 toohave 흰색 화면 
* 고정된: blob 컨테이너 공용 액세스 수준의 설정할 때 hello 새 값 업데이트 되지 않습니다 hello 컨테이너에서 hello 포커스를 다시 설정 될 때까지 합니다. 또한 hello 대화 상자에서 항상 기본값 너무 "public"에 액세스 하 고 hello 실제 현재 값이 아닌 합니다.
* 전반적인 키보드/손쉬운 사용 및 UI 지원이 향상되었습니다.
* 이동 경로 기록 텍스트가 길면 공백이 추가되어 줄이 바뀝니다.
* SAS 대화 상자에서 입력 유효성 검사가 지원됩니다.
* 사용자의 자격 증명이 만료 하는 경우에 toobe 사용 가능한 로컬 저장소에 계속
* Hello 오른쪽에 hello blob 탐색기 닫혀 열린된 blob 컨테이너를 삭제 하면

#### <a name="known-issues"></a>알려진 문제

* Gcc 버전 업데이트 또는 업그레이드 – 단계 tooupgrade Linux 설치 요구 사항 아래에 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>버전 0.7.20151116.0

#### <a name="new"></a>새로 만들기

* macOS 및 Windows 버전이 지원됩니다.
* 저장소 계정에서 tooview sign-조직 계정, Microsoft 계정, 2FA, 등을 사용 합니다.
* 로컬 개발 저장소가 제공됩니다(Storage 에뮬레이터 사용, Windows 전용).
* Azure Resource Manager 및 클래식 리소스가 지원됩니다.
* Blob, 큐 또는 테이블을 만들고 삭제할 수 있습니다.
* 특정 Blob, 큐 또는 테이블을 검색할 수 있습니다.
* Blob 컨테이너의 내용을 hello 탐색
* 디렉터리를 보고 디렉터리 간을 이동할 수 있습니다.
* Blob와 폴더를 업로드, 다운로드 및 삭제할 수 있습니다.
* blob 속성 및 메타데이터 보기 및 편집
* SAS 키를 생성할 수 있습니다.
* SAP(저장된 액세스 정책)를 관리하고 만들 수 있습니다.
* 접두사별로 blob 검색
* ' N 파일 tooupload drop 끌거나 다운로드

#### <a name="known-issues"></a>알려진 문제

* Blob 컨테이너 공용 액세스 수준의 설정할 때 hello 컨테이너에서 hello 포커스를 다시 설정 하기 전에 hello 새 값 업데이트 되지 않습니다.
* Hello 실제 현재 값이 아닌 hello 기본적으로 "공용 액세스 권한이" hello 대화 tooset hello 공용 액세스 수준의 열 때 항상 표시
* 다운로드한 Blob 이름을 바꿀 수 없습니다.
* 이 경우에 따라 "중단"에서 진행 중인 활동 로그 항목 상태 때 오류가 발생 하 고 hello 오류가 표시 되지 않습니다.
* 경우에 따라 중단을 일으키거나 turns 완전히 흰색 tooupload 하려고 할 때 또는 다 수의 blob 다운로드
* 가끔씩 복사 작업을 취소할 수 없습니다.
* (테이블/blob/큐) 컨테이너를 만드는 동안 잘못 된 이름을 입력 하 고 toocreate 진행 하는 경우 서로 다른 컨테이너 형식에서 다른 설정할 수 없습니다 포커스 hello 새 형식
* 새 폴더를 만들거나 폴더 이름을 바꿀 수 없습니다.




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md