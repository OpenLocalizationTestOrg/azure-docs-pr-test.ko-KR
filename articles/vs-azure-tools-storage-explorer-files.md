---
title: "aaaUsing Azure 파일 저장소와 저장소 탐색기 (미리 보기) | Microsoft Docs"
description: "자세한 내용은 toouse 저장소 탐색기 (미리 보기) toowork 파일과 함께 공유 하 고 파일 하는 방법을 알아보려면 어떻게 합니다."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Azure 파일 저장소와 함께 저장소 탐색기(미리 보기) 사용

Azure 파일 저장소 hello 클라우드 사용 하 여 공유 파일을 제공 하는 서비스는 hello 표준 서버 메시지 블록 (SMB) 프로토콜입니다. SMB 2.1과 SMB 3.0 모두를 지원합니다. Azure 파일 저장소를 신속 하 고 비용이 많이 드는 다시 작성 하지 않고도 파일 공유 tooAzure에 의존 하는 레거시 응용 프로그램을 마이그레이션할 수 있습니다. 파일 저장소 tooexpose 데이터 사용 하 여 공개적으로 toohello 권역 또는 toostore 응용 프로그램 데이터 개인적으로 합니다. 이 문서에서는 toouse 저장소 탐색기 (미리 보기) toowork 파일과 함께 공유 하 고 파일 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>필수 조건

이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.

- [저장소 탐색기(미리 보기) 다운로드 및 설치](http://www.storageexplorer.com/)

- [Tooa Azure 저장소 계정 또는 서비스를 연결 합니다.](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>파일 공유 만들기

모든 파일은 단지 파일의 논리적 그룹화인 파일 공유에 있어야 합니다. 한 계정에 포함될 수 있는 파일 공유 수에 제한이 없으며, 각 공유에 저장될 수 있는 파일 수에도 제한이 없습니다.

단계를 수행 하는 hello 어떻게 toocreate 파일은 내 저장소 탐색기 (미리 보기)을 공유 하는 방법을 보여 줍니다.

1. 저장소 탐색기(미리 보기)를 엽니다.

2. Hello 왼쪽된 창에서 원하는 toocreate hello 파일 공유는 hello 저장소 계정의 확장

3. 마우스 오른쪽 단추로 클릭 **파일 공유**, 및-hello 상황에 맞는 메뉴-선택 **파일 공유 만들기**합니다.

    ![파일 공유 만들기](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Hello 아래 텍스트 상자에 표시 될 **파일 공유** 폴더입니다. 파일 공유에 대 한 hello 이름을 입력 합니다. Hello 참조 [명명 규칙 공유](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) 섹션 목록에 대 한 규칙 및 파일 공유 이름 지정에 대 한 제한입니다.

    ![Hello 공유 이름 지정](media/vs-azure-tools-storage-explorer-files/image2.png)

5. 키를 눌러 **Enter** 완료 toocreate hello 파일 공유 하는 경우 또는 **Esc** toocancel 합니다. 파일 공유 hello 성공적으로 만든 후 그 아래에 표시 됩니다 hello **파일 공유** 폴더 hello에 대 한 저장소 계정을 선택 합니다.

    ![hello 새 공유](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>파일 공유의 내용 보기

파일 공유는 파일 및 폴더(파일을 포함할 수도 있음)를 포함합니다.

hello 아래 단계에 설명 된 파일의 tooview hello 내용을 저장소 탐색기 (미리 보기) 내에서 공유 하는 방법: +

1. 저장소 탐색기(미리 보기)를 엽니다.

2. Hello 왼쪽된 창에서 원하는 tooview hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.

3. Hello 저장소 계정의 확장 **파일 공유**합니다.

4. Hello 파일 공유를 마우스 오른쪽 단추로 클릭 tooview, 원하는-hello 상황에 맞는 메뉴-선택한 **열려**합니다. 원하는 tooview hello 파일 공유를 두 번 클릭 합니다.

    ![공유 열기](media/vs-azure-tools-storage-explorer-files/image4.png)

5. hello 주 창에는 hello 파일 공유의 내용이 표시 됩니다.
    
    ![hello 공유의 내용](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>파일 공유 삭제

필요에 따라 파일 공유를 쉽게 만들고 삭제할 수 있습니다. (toosee toodelete 개별 파일 toohello 섹션을 참조 하는 방법 [파일 공유에서 파일 관리](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

단계를 수행 하는 hello를 어떻게 toodelete 파일 공유 저장소 탐색기 (미리 보기)를 보여 줍니다.

1. 저장소 탐색기(미리 보기)를 엽니다.

2. Hello 왼쪽된 창에서 원하는 tooview hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.

3. Hello 저장소 계정의 확장 **파일 공유**합니다.

4. Hello 파일 공유를 마우스 오른쪽 단추로 클릭 toodelete, 원하는-hello 상황에 맞는 메뉴-선택한 **삭제**합니다. 또한 누르면 **삭제** toodelete hello 현재 선택 된 파일 공유 합니다.

    ![삭제](media/vs-azure-tools-storage-explorer-files/image6.png)

5. 선택 **예** toohello 확인 대화 상자.
    
    ![확인 대화 상자](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>파일 공유 복사

저장소 탐색기 (미리 보기) toocopy 파일 공유 toohello 클립보드를 사용 하면 한 다음 다른 저장소 계정에 해당 파일 공유를 붙여 넣습니다. (toosee toocopy 개별 파일 toohello 섹션을 참조 하는 방법 [파일 공유에서 파일 관리](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

단계를 수행 하는 hello toocopy 파일 한 저장소 계정 tooanother에서 공유 하는 방법을 보여 줍니다.

1. 저장소 탐색기(미리 보기)를 엽니다.

2. Hello 왼쪽된 창에서 원하는 toocopy hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.

3. Hello 저장소 계정의 확장 **파일 공유**합니다.

4. Hello 파일 공유를 마우스 오른쪽 단추로 클릭 toocopy, 원하는-hello 상황에 맞는 메뉴-선택한 **복사본 파일 공유**합니다.

    ![파일 공유 복사](media/vs-azure-tools-storage-explorer-files/image8.png)

5. toopaste hello 파일 공유를 한-hello 상황에 맞는 메뉴-선택 hello 원하는 "대상" 저장소 계정을 마우스 오른쪽 단추로 **붙여넣기 파일 공유**합니다.

    ![파일 공유 붙여넣기](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>파일 공유에 대 한 SAS hello 가져오기

A [공유 액세스 서명 (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) 저장소 계정의 tooresources 위임 된 액세스를 제공 합니다. 이 클라이언트가 시간 및 지정한 사용 권한 집합이 지정된 된 기간에 대 한 저장소 계정에 사용 권한을 tooobjects tooshare 계정 액세스 키 필요 없이 제한에 부여할 수 있는 것을 의미 합니다.

hello 아래 단계에 설명 파일에 대 한 SAS를 공유 하는 toocreate 어떻게: +

1. 저장소 탐색기(미리 보기)를 엽니다.

2. Hello 왼쪽된 창에서 확장 hello 저장소 계정 hello 파일 공유를 원하는 tooget SAS를 포함 합니다.

3. Hello 저장소 계정의 확장 **파일 공유**합니다.

4. Hello 원하는 파일 공유를 마우스 오른쪽 단추로 클릭 하 고-hello 상황에 맞는 메뉴-선택 **공유 액세스 서명을 가져올**합니다.

    ![공유 액세스 서명 가져오기](media/vs-azure-tools-storage-explorer-files/image10.png)

5. Hello에 **공유 액세스 서명을** 대화 상자에서 hello 정책, 시작 및 만료 날짜, 표준 시간대를 지정 하 고 수준을 hello 리소스에 대 한 액세스.

    ![SAS 대화 상자](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Hello SAS 옵션을 지정 하 고 완료 되 면, 선택 **만들기**합니다.

7. 두 번째 **공유 액세스 서명을** 목록 hello hello URL 따라 파일 공유 및 저장소 리소스를 hello QueryStrings tooaccess를 사용할 수 있습니다에 다음 대화 상자 표시 됩니다. 선택 **복사** toocopy toohello 클립보드 원하는 다음 toohello URL입니다.
    
    ![두 번째 SAS 대화 상자](media/vs-azure-tools-storage-explorer-files/image12.png)

8. 완료되면 **닫기**를 선택합니다.

## <a name="manage-access-policies-for-a-file-share"></a>파일 공유에 대한 액세스 정책 관리

hello 아래 단계에 설명 방법을 toomanage (추가 및 제거) 액세스 파일 공유에 대 한 정책: + 합니다. 사용자 צ ְ ײ tooaccess hello 저장소 파일 리소스 정의 된 기간 동안 SAS Url 생성을 위한 hello 액세스 정책 사용 됩니다.

1. 저장소 탐색기(미리 보기)를 엽니다.

2. Hello 왼쪽된 창에서 확장 hello 저장소 계정 액세스 정책이 toomanage 원하는 hello 파일 공유를 포함 합니다.

3. Hello 저장소 계정의 확장 **파일 공유**합니다.

4. Hello 원하는 파일 공유를 선택 하 고-hello 상황에 맞는 메뉴-선택 **액세스 정책 관리**합니다.

    ![액세스 정책 상황에 맞는 메뉴 관리](media/vs-azure-tools-storage-explorer-files/image13.png)

5. hello **액세스 정책을** 대화 이미 만든 hello 선택한 파일 공유에 대 한 모든 액세스 정책 나열 됩니다.
    
    ![액세스 정책](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Hello 액세스 정책 관리 작업에 따라 다음이 단계를 수행 합니다.
    
    - **새 액세스 정책 추가** - **추가**를 선택합니다. 생성 되 면 hello **액세스 정책을** hello 새로 추가 된 대화 상자가 표시 됩니다 (기본 설정)으로 정책에 액세스 합니다.

    - **액세스 정책 편집** - 원하는 편집을 모두 마치고, **저장**을 선택합니다.

    - **액세스 정책을 제거** -선택 **제거** tooremove 원하는 다음 toohello 액세스 정책.

7. 앞에서 만든 액세스 정책 hello를 사용 하 여 새 SAS URL을 만듭니다.
    
    ![SAS 가져오기](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS 이름 및 속성](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>파일 공유에서 파일 관리

파일 공유를 만든 후 업로드 파일 toothat 파일 공유 파일 tooyour 로컬 컴퓨터에 다운로드을 등과 로컬 컴퓨터에 파일을 열 수 있습니다.

hello 아래 단계에 설명 toomanage hello 파일 및 폴더 파일 내에서 공유 하는 방법입니다.

1.  저장소 탐색기(미리 보기)를 엽니다.

2.  Hello 왼쪽된 창에서 원하는 toomanage hello 파일 공유를 포함 하는 hello 저장소 계정을 확장 합니다.

3.  Hello 저장소 계정의 확장 **파일 공유**합니다.

4.  원하는 tooview hello 파일 공유를 두 번 클릭 합니다.

5.  hello 주 창에는 hello 파일 공유의 내용이 표시 됩니다.

    ![hello 공유의 내용](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  hello 주 창에는 hello 파일 공유의 내용이 표시 됩니다.

7.  Tooperform 원하는 hello 작업에 따라 다음이 단계를 수행:

    - **업로드 파일 tooa 파일 공유**

        a.  Hello 주 창 도구 모음 선택 **업로드**, 차례로 **파일 업로드** hello 드롭 다운 메뉴에서 합니다.

        ![파일 업로드](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. Hello에 **파일 업로드** 대화 상자에서 선택 hello 줄임표 (**...** )의 hello hello 오른쪽 단추를 **파일** 텍스트 상자에 원하는 tooupload tooselect hello 파일입니다.

        ![파일 추가](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. **업로드**를 선택합니다.

    - **폴더 tooa 파일 공유를 업로드 합니다.**
        
        a. Hello 주 창 도구 모음 선택 **업로드**, 차례로 **폴더 업로드** hello 드롭 다운 메뉴에서 합니다.

        ![폴더 메뉴 업로드](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. Hello에 **업로드 폴더** 대화 상자에서 선택 hello 줄임표 (**...** )의 hello hello 오른쪽 단추를 **폴더** 텍스트 상자 tooselect hello 내용을 폴더 tooupload 원하는 합니다.

        c. 필요에 따라 어떤 hello에 선택한 폴더의 내용을 업로드할 수는 대상 폴더를 지정 합니다. Hello 대상 폴더가 존재 하지 않는 경우 생성 됩니다.

        d. **업로드**를 선택합니다.

    - **다운로드 파일 tooyour 로컬 컴퓨터**
        
        a. Toodownload hello 파일을 선택 합니다.
        
        b. Hello 주 창 도구 모음 선택 **다운로드**합니다.
        
        c. Hello에 **지정 toosave hello 파일을 다운로드 한** 대화 상자에서 hello 파일 다운로드를 저장할 hello 위치를 지정 하 고 toogive 이름 hello 것입니다.

        d. **저장**을 선택합니다.

    - **로컬 컴퓨터에서 파일 열기**
        
        a.  Tooopen hello 파일을 선택 합니다.
        
        b.  Hello 주 창 도구 모음 선택 **열려**합니다.
        
        c.  hello 파일 다운로드 되 고 hello 파일의 원본으로 사용 하는 파일 형식과 연결 된 hello 응용 프로그램을 사용 하 여 열립니다.

    - **파일 toohello 클립보드로 복사**

        a. Toocopy hello 파일을 선택 합니다.

        b. Hello 주 창 도구 모음 선택 **복사**합니다.

        c. Hello 왼쪽된 창에서 tooanother 파일 공유를 찾아 두 번 클릭 tooview hello 주 창에 해당 합니다.

        d. Hello 주 창 도구 모음 선택 **붙여넣기** toocreate hello 파일의 복사본입니다.

    - **파일 삭제**

        a. Toodelete hello 파일을 선택 합니다.

        b. Hello 주 창 도구 모음 선택 **삭제**합니다.

        c. 선택 **예** toohello 확인 대화 상자.

## <a name="next-steps"></a>다음 단계

- 보기 hello [최신 저장소 탐색기 (미리 보기) 릴리스 정보 및 비디오](http://www.storageexplorer.com/)합니다.

- 너무 방법에 대해 알아봅니다[Azure blob, 테이블, 큐 및 파일을 사용 하 여 응용 프로그램을 만들](https://azure.microsoft.com/documentation/services/storage/)합니다.
