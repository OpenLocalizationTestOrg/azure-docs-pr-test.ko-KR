---
title: "저장소 탐색기 (미리 보기)를 사용 하 여 Azure Blob 저장소 리소스 aaaManage | Microsoft Docs"
description: "저장소 탐색기(미리 보기)를 사용하여 Azure Blob 컨테이너 및 Blobs 관리"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>저장소 탐색기(미리 보기)를 사용하여 Blob 저장소 리소스 관리
## <a name="overview"></a>개요
[Azure Blob 저장소](storage/blobs/storage-dotnet-how-to-use-blobs.md) 는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 데이터를 저장 하는 서비스입니다.
Blob 저장소 tooexpose 데이터 사용 하 여 공개적으로 toohello 권역 또는 toostore 응용 프로그램 데이터 개인적으로 합니다. 이 문서에서는 알아봅니다 어떻게 toouse 저장소 탐색기 (미리 보기) toowork blob 컨테이너 및 blob와 함께 합니다.

## <a name="prerequisites"></a>필수 조건
이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.

* [저장소 탐색기(미리 보기) 다운로드 및 설치](http://www.storageexplorer.com)
* [Tooa Azure 저장소 계정 또는 서비스를 연결 합니다.](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Blob 컨테이너 만들기
모든 blob은 단지 blob의 논리적 그룹화인 blob 컨테이너에 있어야 합니다. 한 계정에 포함될 수 있는 컨테이너 수에 제한이 없으며, 각 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다.

hello 아래 단계에 설명 방법을 toocreate 저장소 탐색기 (미리 보기) 내에서 blob 컨테이너입니다.

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 원하는 toocreate hello blob 컨테이너는 hello 저장소 계정을 확장 합니다.
3. 마우스 오른쪽 단추로 클릭 **Blob 컨테이너**, 및-hello 상황에 맞는 메뉴-선택 **Create Blob Container**합니다.

   ![Blob 컨테이너 상황에 맞는 메뉴 만들기][0]
4. Hello 아래 텍스트 상자에 표시 될 **Blob 컨테이너** 폴더입니다. Blob 컨테이너에 대 한 hello 이름을 입력 합니다. Hello 참조 [컨테이너 명명 규칙](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) 명명 blob 컨테이너에 대 한 제한 규칙의 목록에 대 한 섹션에 있습니다.

   ![Blob 컨테이너 텍스트 상자 만들기][1]
5. 키를 눌러 **Enter** 끝나면 toocreate hello blob 컨테이너 또는 **Esc** toocancel 합니다. Hello blob 컨테이너 성공적으로 만든 후 그 아래에 표시 됩니다 hello **Blob 컨테이너** 폴더 hello에 대 한 저장소 계정을 선택 합니다.

   ![만든 Blob 컨테이너][2]

## <a name="view-a-blob-containers-contents"></a>Blob 컨테이너 내용 보기
Blob 컨테이너는 blob 및 폴더(blob도 포함할 수 있음)를 포함하고 있습니다.

hello 아래 단계에 설명 방법을 저장소 탐색기 (미리 보기) 내에서 blob 컨테이너의 tooview hello 내용:

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 원하는 tooview hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.
3. Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.
4. Hello blob 컨테이너를 마우스 오른쪽 단추로 클릭 tooview, 원하는-hello 상황에 맞는 메뉴-선택한 **Blob 컨테이너 편집기 열기**합니다.
   원하는 tooview hello blob 컨테이너를 두 번 클릭 합니다.

   ![blob 컨테이너 편집기 상황에 맞는 메뉴 열기][19]
5. hello 주 창에는 hello blob 컨테이너의 내용을 표시 됩니다.

   ![Blob 컨테이너 편집기][3]

## <a name="delete-a-blob-container"></a>Blob 컨테이너 삭제
필요에 따라 Blob 컨테이너를 쉽게 만들고 삭제할 수 있습니다. (toodelete 개별 blob toosee toohello 섹션을 참조 하십시오. [blob 컨테이너에 blob 관리](#managing-blobs-in-a-blob-container).)

hello 아래 단계에 설명 방법을 toodelete 저장소 탐색기 (미리 보기) 내에서 blob 컨테이너:

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 원하는 tooview hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.
3. Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.
4. Hello blob 컨테이너를 마우스 오른쪽 단추로 클릭 toodelete, 원하는-hello 상황에 맞는 메뉴-선택한 **삭제**합니다.
   또한 누르면 **삭제** toodelete hello 현재 선택 된 blob 컨테이너입니다.

   ![Blob 컨테이너 상황에 맞는 메뉴 삭제][4]
5. 선택 **예** toohello 확인 대화 상자.

   ![Blob 컨테이너 확인 삭제][5]

## <a name="copy-a-blob-container"></a>Blob 컨테이너 복사
저장소 탐색기 (미리 보기)을 사용 하면 blob 컨테이너 toohello 클립보드 toocopy 및 다른 저장소 계정에 컨테이너 blob 후 붙여넣습니다 있습니다. (toocopy 개별 blob toosee toohello 섹션을 참조 하십시오. [blob 컨테이너에 blob 관리](#managing-blobs-in-a-blob-container).)

단계를 수행 하는 hello toocopy 하나의 저장소에서 blob 컨테이너 tooanother를 고려 하는 방법을 보여 줍니다.

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 원하는 toocopy hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.
3. Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.
4. Hello blob 컨테이너를 마우스 오른쪽 단추로 클릭 toocopy, 원하는-hello 상황에 맞는 메뉴-선택한 **복사 Blob 컨테이너**합니다.

   ![Blob 컨테이너 상황에 맞는 메뉴 복사][6]
5. toopaste hello blob 컨테이너를 한-hello 상황에 맞는 메뉴-선택 hello 원하는 "대상" 저장소 계정을 마우스 오른쪽 단추로 **붙여넣기 Blob 컨테이너**합니다.

   ![Blob 컨테이너 상황에 맞는 메뉴 붙여넣기][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Blob 컨테이너에 대 한 SAS hello 가져오기
A [공유 액세스 서명 (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) 저장소 계정의 tooresources 위임 된 액세스를 제공 합니다.
이 계정 액세스 키를 공유 하지 않고 시간 및 지정한 사용 권한 집합이 지정된 된 기간에 대 한 제한 된 저장소 계정에 사용 권한을 tooobjects 클라이언트에 부여할 수 있는 것을 의미 합니다.

hello 아래 단계에 설명 방법을 toocreate blob 컨테이너에 대 한 SAS:

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 확장 hello 저장소 계정을 원하는 tooget SAS hello blob 컨테이너를 포함 합니다.
3. Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.
4. Hello 원하는 blob 컨테이너를 마우스 오른쪽 단추로 클릭 하 고-hello 상황에 맞는 메뉴-선택 **공유 액세스 서명을 가져올**합니다.

   ![SAS 상황에 맞는 메뉴 가져오기][8]
5. Hello에 **공유 액세스 서명을** 대화 상자에서 hello 정책, 시작 및 만료 날짜, 표준 시간대를 지정 하 고 수준을 hello 리소스에 대 한 액세스.

   ![SAS 옵션 가져오기][9]
6. Hello SAS 옵션을 지정 하 고 완료 되 면, 선택 **만들기**합니다.
7. 두 번째 **공유 액세스 서명을** 목록 hello hello URL 따라 blob 컨테이너 및 저장소 리소스를 hello QueryStrings tooaccess를 사용할 수 있습니다에 다음 대화 상자 표시 됩니다.
   선택 **복사** toocopy toohello 클립보드 원하는 다음 toohello URL입니다.

   ![SAS Url 복사][10]
8. 완료되면 **닫기**를 선택합니다.

## <a name="manage-access-policies-for-a-blob-container"></a>Blob 컨테이너에 대한 액세스 정책 관리
hello 아래 단계에 설명 방법을 toomanage (추가 및 제거) 액세스 한 blob 컨테이너에 대 한 정책:

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 hello 저장소 계정 blob 컨테이너 hello toomanage 원하는 액세스 정책이 포함 된를 확장 합니다.
3. Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.
4. Hello 원하는 blob 컨테이너를 선택 하 고-hello 상황에 맞는 메뉴-선택 **액세스 정책 관리**합니다.

   ![액세스 정책 상황에 맞는 메뉴 관리][11]
5. hello **액세스 정책을** 대화 이미 만든 hello 선택한 blob 컨테이너에 대 한 모든 액세스 정책 나열 됩니다.

   ![액세스 정책 옵션][12]        
6. Hello 액세스 정책 관리 작업에 따라 다음이 단계를 수행 합니다.

   * **새 액세스 정책 추가** - **추가**를 선택합니다. 생성 되 면 hello **액세스 정책을** hello 새로 추가 된 대화 상자가 표시 됩니다 (기본 설정)으로 정책에 액세스 합니다.
   * **액세스 정책 편집** -원하는 편집을 모두 마치고, **저장**을 선택합니다.
   * **액세스 정책을 제거** -선택 **제거** tooremove 원하는 다음 toohello 액세스 정책.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Blob 컨테이너에 대 한 공용 액세스 수준을 hello 설정
모든 blob 컨테이너가 너무 설정 기본적으로 "공용 액세스 권한이"입니다.

hello 아래 단계에 설명 공용 액세스 하는 toospecify 방법을 blob 컨테이너에 대 한 수준.

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 hello 저장소 계정 blob 컨테이너 hello toomanage 원하는 액세스 정책이 포함 된를 확장 합니다.
3. Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.
4. Hello 원하는 blob 컨테이너를 선택 하 고-hello 상황에 맞는 메뉴-선택 **공용 액세스 수준을 설정**합니다.

   ![공용 액세스 수준 상황에 맞는 메뉴 설정][13]
5. Hello에 **컨테이너 공용 액세스 수준을 설정** 대화 상자에서 원하는 hello 액세스 수준을 지정 합니다.

   ![공용 액세스 수준 옵션 설정][14]
6. **적용**을 선택합니다.

## <a name="managing-blobs-in-a-blob-container"></a>blob 컨테이너의 blob 관리
Blob 컨테이너를 만든 후 blob toothat blob 컨테이너에 업로드 blob tooyour 로컬 컴퓨터에 다운로드을 로컬 컴퓨터에 더 많은 blob을 열 수 있습니다.

단계를 수행 하는 hello를 toomanage blob 컨테이너 내의 blob (및 폴더)을 hello 방법을 보여 줍니다.

1. 저장소 탐색기(미리 보기)를 엽니다.
2. Hello 왼쪽된 창에서 원하는 toomanage hello blob 컨테이너를 포함 하는 hello 저장소 계정을 확장 합니다.
3. Hello 저장소 계정의 확장 **Blob 컨테이너**합니다.
4. 원하는 tooview hello blob 컨테이너를 두 번 클릭 합니다.
5. hello 주 창에는 hello blob 컨테이너의 내용을 표시 됩니다.

   ![Blob 컨테이너 보기][3]
6. hello 주 창에는 hello blob 컨테이너의 내용을 표시 됩니다.
7. Tooperform 원하는 hello 작업에 따라 다음이 단계를 수행:

   * **파일 tooa blob 컨테이너를 업로드 합니다.**

     1. Hello 주 창 도구 모음 선택 **업로드**, 차례로 **파일 업로드** hello 드롭 다운 메뉴에서 합니다.

        ![파일 메뉴 업로드][15]
     2. Hello에 **파일 업로드** 대화 상자에서 선택 hello 줄임표 (**... **)의 hello hello 오른쪽 단추를 **파일** 텍스트 상자에 원하는 tooupload tooselect hello 파일입니다.

        ![파일 옵션 업로드][16]
     3. Hello 유형의 지정 **유형 Blob**합니다. hello 문서 [.NET을 사용 하 여 Azure Blob 저장소 시작](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) 다양 한 blob 종류 hello hello 차이점에 설명 합니다.
     4. 필요에 따라 hello 선택한 파일은 업로드 대상 폴더를 지정 합니다. Hello 대상 폴더가 존재 하지 않는 경우 생성 됩니다.
     5. **업로드**를 선택합니다.
   * **폴더 tooa blob 컨테이너를 업로드 합니다.**

     1. Hello 주 창 도구 모음 선택 **업로드**, 차례로 **폴더 업로드** hello 드롭 다운 메뉴에서 합니다.

        ![폴더 메뉴 업로드][17]
     2. Hello에 **업로드 폴더** 대화 상자에서 선택 hello 줄임표 (**... **)의 hello hello 오른쪽 단추를 **폴더** 텍스트 상자 tooselect hello 내용을 폴더 tooupload 원하는 합니다.

        ![폴더 옵션 업로드][18]
     3. Hello 유형의 지정 **유형 Blob**합니다. hello 문서 [.NET을 사용 하 여 Azure Blob 저장소 시작](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) 다양 한 blob 종류 hello hello 차이점에 설명 합니다.
     4. 필요에 따라 어떤 hello에 선택한 폴더의 내용을 업로드할 수는 대상 폴더를 지정 합니다. Hello 대상 폴더가 존재 하지 않는 경우 생성 됩니다.
     5. **업로드**를 선택합니다.
   * **Blob tooyour 로컬 컴퓨터에 다운로드**

     1. 원하는 toodownload hello blob을 선택 합니다.
     2. Hello 주 창 도구 모음 선택 **다운로드**합니다.
     3. Hello에 **toosave hello blob를 다운로드 하는 위치 지정** 대화 상자에서 hello blob를 다운로드 한 저장할 hello 위치를 지정 하 고 toogive 이름 hello 것입니다.  
     4. **저장**을 선택합니다.
   * **로컬 컴퓨터에서 blob 열기**

     1. 원하는 tooopen hello blob을 선택 합니다.
     2. Hello 주 창 도구 모음 선택 **열려**합니다.
     3. hello blob 다운로드 되 고 hello blob의 기본 파일 형식과 연결 된 hello 응용 프로그램을 사용 하 여 열립니다.
   * **Blob toohello 클립보드에 복사**

     1. 원하는 toocopy hello blob을 선택 합니다.
     2. Hello 주 창 도구 모음 선택 **복사**합니다.
     3. Hello 왼쪽된 창에서 tooanother blob 컨테이너를 찾아 두 번 클릭 tooview hello 주 창에 해당 합니다.
     4. Hello 주 창 도구 모음 선택 **붙여넣기** toocreate hello blob의 복사본입니다.
   * **Blob 삭제**

     1. 원하는 toodelete hello blob을 선택 합니다.
     2. Hello 주 창 도구 모음 선택 **삭제**합니다.
     3. 선택 **예** toohello 확인 대화 상자.

## <a name="next-steps"></a>다음 단계
* 보기 hello [최신 저장소 탐색기 (미리 보기) 릴리스 정보 및 비디오](http://www.storageexplorer.com)합니다.
* 너무 방법에 대해 알아봅니다[Azure blob, 테이블, 큐 및 파일을 사용 하 여 응용 프로그램을 만들](https://azure.microsoft.com/documentation/services/storage/)합니다.

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
