---
title: "aaaBrowsing 서버 탐색기로 저장소 리소스 및 관리 | Microsoft Docs"
description: "서버 탐색기로 저장소 리소스 찾아보기 및 관리"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>서버 탐색기로 저장소 리소스 찾아보기 및 관리
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>개요
Hello Azure Tools for Microsoft Visual Studio를 설치한 경우 볼 수 있습니다 blob, 큐 및 테이블 데이터 저장소 계정에서 Azure에 대 한 합니다. 서버 탐색기에서 Azure 저장소 노드 hello 로컬 저장소 에뮬레이터 계정 및 다른 Azure 저장소 계정에 있는 데이터를 표시 합니다.

hello 메뉴 모음에서 Visual Studio 서버 탐색기 tooview 선택 **보기**, **서버 탐색기**합니다. hello 저장소 노드 모두에서 각 Azure 구독/인증서에 연결 되어 있는 hello 저장소 계정을 표시 됩니다. 저장소 계정이 표시 되지 않으면 hello 지침에 따라 추가할 수 있습니다 [이 항목의 뒷부분에 나오는](#add-storage-accounts-by-using-server-explorer)합니다.

Azure SDK 2.7부터 새로운 클라우드 탐색기 tooview hello를 사용 하 여 고 Azure 리소스를 관리할 수도 있습니다. 자세한 내용은 [클라우드 탐색기를 사용하여 Azure 리소스 관리](vs-azure-tools-resources-managing-with-cloud-explorer.md) 를 참조하세요.

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Visual Studio에서 저장소 리소스를 확인 및 관리합니다.
서버 탐색기는 저장소 에뮬레이터 계정에 있는 Blob, 큐, 테이블 목록을 자동으로 보여줍니다. hello 저장소 에뮬레이터 계정 hello hello 저장소 노드 아래에서 서버 탐색기에 나열 됩니다 **개발** 노드.

toosee hello 저장소 에뮬레이터 계정의 리소스 확장 hello **개발** 노드. Hello를 확장 하면 hello 저장소 에뮬레이터 시작 되지 않은 상태 경우 **개발** 노드를 자동으로 시작 됩니다. 이 작업은 몇 초 정도 걸릴 수 있습니다. Hello 저장소 에뮬레이터를 시작 하는 동안 Visual Studio의 다른 영역에서 toowork를 계속할 수 있습니다.

저장소 계정에 tooview 리소스 서버 탐색기에서 hello 저장소 계정의 노드를 확장 합니다. 하위 노드를 다음 hello 표시 됩니다.

* Blob
* 큐
* 테이블

## <a name="work-with-blob-resources"></a>Blob 리소스로 작업
hello Blob 노드에 hello 선택한 저장소 계정에 대 한 컨테이너 목록이 표시 됩니다. Blob 컨테이너는 Blob 파일을 포함하고 있으며 이러한 Blob을 폴더와 하위 폴더로 구성할 수 있습니다. 참조 [어떻게 toouse.NET에서 Blob 저장소](storage/blobs/storage-dotnet-how-to-use-blobs.md) 자세한 정보에 대 한 합니다.

### <a name="toocreate-a-blob-container"></a>toocreate blob 컨테이너
1. Hello에 대 한 바로 가기 메뉴를 열고 hello **Blob** 노드를 선택한 후 **Create Blob Container**합니다.
2. Hello에 **Create Blob Container** 대화 상자 hello 새 컨테이너의 hello 이름을 입력 합니다.  
3. 키를 눌러 **ENTER** 키보드 또는 있습니다 수 또는 클릭 하 여 hello 이름 필드 toosave hello blob 컨테이너의 외부 탭 합니다.
   
   > [!NOTE]
   > hello blob 컨테이너 이름은 숫자 (0-9) 또는 소문자 (a ~ z)로 시작 해야 합니다.
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete blob 컨테이너
* Tooremove을 눌러 hello blob 컨테이너에 대 한 바로 가기 메뉴를 열고 hello **삭제**합니다.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>blob 컨테이너에 toodisplay hello 항목 목록이 포함 된
* Hello 목록에서 blob 컨테이너 이름에 대 한 hello 바로 가기 메뉴를 열고 **열려**합니다.
  
    Blob 컨테이너의 hello 콘텐츠를 볼 때 hello blob 컨테이너 보기로 알려진 탭에 나타납니다.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    Hello blob 컨테이너 뷰의 hello 오른쪽 위 모서리에 hello 단추를 사용 하 여 blob에 대 한 작업을 수행 하는 hello를 수행할 수 있습니다.
  
  * 필터 값을 입력 및 적용하기
  * Hello hello 컨테이너의 blob 목록 새로 고침
  * 파일 업로드
  * Blob 삭제
    
    > [!NOTE]
    > Blob 컨테이너에서 파일을 삭제 하면 파일을 원본으로 사용 하는 hello; 삭제 되지 않습니다. 에서만 제거 hello blob 컨테이너에서 합니다.
    > 
    > 
  * Blob 열기
  * Blob toohello 로컬 컴퓨터를 저장 합니다.

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate 폴더 또는 blob 컨테이너에 대 한 하위 폴더
1. 클라우드 탐색기에서 hello blob 컨테이너를 선택 합니다. Hello 컨테이너 창의 hello 선택 **Blob 업로드** 단추입니다.
   
    ![Blob 폴더에 파일 업로드하기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. Hello에 **새 파일 업로드** 대화 상자에서 선택 하는 hello **찾아보기** 단추 toospecify hello 원하는 파일 tooupload를 선택한 다음 hello에 폴더 이름을 입력 **폴더 (옵션)** 상자 .
   
    하위 폴더에 따라 컨테이너 폴더에 동일한 hello를 추가할 수 있습니다 프로시저입니다. Hello 파일이 됩니다 폴더 이름을 지정 하지 않으면, hello blob 컨테이너의 최상위 수준 toohello 업로드 합니다. hello 파일이 hello 컨테이너에서 hello 지정한 폴더에 나타납니다.
   
    ![폴더는 tooa blob 컨테이너를 추가합니다.](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Hello 폴더를 두 번 클릭 하거나 hello 폴더 내용의 toosee hello ENTER 키를 누릅니다. Hello를 선택 하 여 hello 컨테이너의 뒤로 toohello 루트를 탐색할 수 hello 컨테이너 폴더에 있는 경우 **부모 디렉터리 열기** (위쪽 화살표) 단추입니다.

### <a name="toodelete-a-container-folder"></a>toodelete 컨테이너 폴더
* Hello 폴더에 hello 파일 모두 삭제
  
  > [!NOTE]
  > Blob 컨테이너의 폴더 가상 폴더 이므로, 빈 폴더를 만들 수 없습니다도 삭제할 수 폴더 toodelete 파일 내용을. Toodelete hello 폴더 toodelete hello 폴더의 전체 내용을 해야합니다.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>컨테이너의 blob toofilter
공통 접두사를 지정 하 여 표시 되는 hello blob를 필터링 할 수 있습니다.

예를 들어, hello 접두사를 입력 하면 `hello` 에 hello 필터 텍스트 상자를 선택한 후 hello **Execute** (**!**) 단추를 'hello'로 시작 하는 blob만 표시 됩니다.

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> hello 필터 필드는 대/소문자 구분 하 고 와일드 카드 문자를 사용 하 여 필터링을 지원 하지 않습니다. Blob은 접두사로만 필터링될 수 있습니다. hello 접두사는 가상 계층 구조에서 구분 기호 tooorganize blob을 사용 하는 경우 구분 기호를 포함할 수 있습니다. 예를 들어에서 필터링 접두사 HelloFabric hello/해당 문자열로 시작 하는 모든 blob를 반환 합니다.
> 
> 

### <a name="toodownload-blob-data"></a>toodownload blob 데이터
* **클라우드 탐색기**를 하나 이상의 blob에 대 한 hello 바로 가기 메뉴를 열고 다음을 선택 **열고**, 또는 hello blob 이름을 선택 하 고 hello 선택 **열** 단추를 두 번 클릭 하거나 hello blob 이름입니다.
  
    hello에 blob 다운로드 hello 진행률이 나타납니다 **Azure 활동 로그** 창.
  
    hello blob 해당 파일 형식에 대 한 hello 기본 편집기에서 열립니다. 로컬에 설치 된 응용 프로그램의 hello 파일이 열립니다 hello 운영 체제 hello 파일 형식을 인식 하는 경우 그렇지 않으면 묻는 toochoose hello hello blob 파일 형식에 적합 한 응용 프로그램입니다. blob을 다운로드할 때 만들어진 hello 로컬 파일 읽기 전용으로 표시 됩니다.
  
    Blob 데이터를 로컬로 캐시 되 고 hello hello Blob 서비스에서에서 blob의 마지막 수정된 시간이 검사 됩니다. 마지막으로 다운로드 이후 hello blob 업데이트 된 경우는 다시 다운로드 해; 그렇지 않으면 hello blob hello 로컬 디스크에서 로드 됩니다. 기본적으로 blob는 다운로드 한 tooa 임시 디렉터리입니다. toodownload blob tooa 특정 디렉터리를 선택 하는 hello에 대 한 바로 가기 메뉴를 열고 hello blob 이름을 선택한 **다른 이름으로 저장**합니다. 이런이 방식으로 blob을 저장할 때 hello blob 파일이 열려 있지 않으면 및 hello 로컬 파일 읽기 / 쓰기 특성을 사용 하 여 만들어집니다.

### <a name="tooupload-blobs"></a>tooupload blob
* Hello 선택 **Blob 업로드** hello 컨테이너 보기 hello blob 컨테이너 보기에 대해 열려 있을 때 단추입니다.
  
    하나를 선택할 수 또는 더 많은 파일 tooupload 및 모든 형식의 파일을 업로드할 수 있습니다. hello **Azure 활동 로그** 표시 hello hello 업로드의 진행률입니다. 방법에 대 한 자세한 내용은 blob 데이터로 toowork 참조 [어떻게 toouse hello.NET에서 Azure Blob 저장소 서비스로](http://go.microsoft.com/fwlink/p/?LinkId=267911)합니다.

### <a name="tooview-logs-transferred-tooblobs"></a>tooview 로그 전송 tooblobs
* Azure 응용 프로그램에서 Azure 진단을 toolog 데이터를 사용 하는 로그 tooyour 저장소 계정에 전송한 경우 이러한 로그에 대 한 Azure에서 만들어진 컨테이너가 표시 됩니다. 서버 탐색기에서 이러한 로그 보기 응용 프로그램에 쉽게 tooidentify 문제는 특히 경과 했는데도 문제가 있다면 배포 tooAzure 하는 경우. Azure 진단에 대한 자세한 내용은 [Azure 진단을 사용하여 로깅 데이터 수집](https://msdn.microsoft.com/library/azure/gg433048.aspx)을 참조하세요.

### <a name="tooget-hello-url-for-a-blob"></a>blob에 대 한 tooget hello URL
* Hello blob의 바로 가기 메뉴를 열고 **URL 복사**합니다.

### <a name="tooedit-a-blob"></a>tooedit blob
* Hello blob을 선택 하 고 hello를 눌러 **Blob 열기** 단추입니다.
  
    hello 파일은 임시 위치로 다운로드 한 tooa 고 hello 로컬 컴퓨터에서 열립니다. 변경한 후 다시 hello blob을 업로드 해야 합니다.

## <a name="work-with-queue-resources"></a>큐 리소스로 작업
저장소 서비스 큐는 Azure 저장소 계정에서 호스팅되며 tooallow 사용할 수 있습니다 프로그램 클라우드 서비스 역할 toocommunicate 서로 다른 서비스와 메시지 전달 메커니즘을 통해. 외부 클라이언트에 대 한 웹 서비스 및 클라우드 서비스를 통해 hello 큐를 프로그래밍 방식으로 액세스할 수 있습니다. 또한 Visual Studio에서 서버 탐색기를 사용 하 여 직접 hello 큐를 액세스할 수 있습니다.

큐를 사용 하는 클라우드 서비스를 개발 하는 경우 Visual Studio toocreate 큐 toouse 수도 있으며 작업할 대화식으로 개발 하 고 코드를 테스트 하는 동안 수 있습니다.

서버 탐색기에서 있습니다 수 hello 큐는 저장소 계정에 볼, 및 큐를 삭제, 큐 tooview 메시지를 만들고 열고 tooa 큐 메시지 추가 합니다. 보기에 대 한 큐를 열 때 hello 개별 메시지를 볼 수 있습니다 및 hello hello 왼쪽 위 모서리에 hello 단추를 사용 하 여 hello 큐에 작업을 다음을 수행할 수 있습니다.

* Hello hello 큐 보기 새로 고침
* 메시지 toohello 큐 추가
* Hello 최상위 메시지를 큐에서 제거
* 전체 큐 지우기 hello

다음 이미지는 hello에서는 두 개의 메시지를 포함 하는 큐를 보여 줍니다.

![큐 보기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

저장소에 대 한 자세한 내용은 서비스 큐에 대 한 참조 [하는 방법: 큐 저장소 서비스 사용 하 여 hello](http://go.microsoft.com/fwlink/?LinkID=264702)합니다. Hello 웹 서비스에 대 한 정보에 대 한 저장소 서비스 큐에 대 한 참조 [큐 서비스 개념](http://go.microsoft.com/fwlink/?LinkId=264788)합니다. Toosend 메시지 tooa 저장소 Visual Studio를 사용 하 여 큐를 서비스 하는 방법에 대 한 정보를 참조 하십시오. [저장소 서비스 큐의 메시지를 보내는 tooa](https://msdn.microsoft.com/library/azure/jj649344.aspx)합니다.

> [!NOTE]
> 저장소 서비스 큐는 서비스 버스 큐와 구별됩니다. 서비스 버스 큐에 대한 자세한 내용은 서비스 버스 큐, 항목 및 구독을 참조하세요.
> 
> 

## <a name="work-with-table-resources"></a>테이블 리소스로 작업
hello Azure 테이블 저장소 서비스는 다량의 구조화 된 데이터를 저장합니다. hello 서비스는 허용 하는 NoSQL 데이터 저장소 인증 내부와 Azure 클라우드 hello 외부에서 호출 됩니다. Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.

### <a name="toocreate-a-table"></a>toocreate 테이블
1. 클라우드 탐색기에서 선택 hello **테이블** 노드 hello 저장소 계정을 선택한 후 **Create Table**합니다.
2. Hello에 **Create Table** 대화 상자 hello 테이블에 대 한 이름을 입력 합니다.

### <a name="tooview-table-data"></a>tooview 테이블 데이터
1. 클라우드 탐색기에서 열어 hello **Azure** 노드를 차례로 연 다음 hello **저장소** 노드.
2. 관심 있는 하 고 hello를 열면 다음 열기 hello 저장소 계정 노드 **테이블** 노드 toosee hello 저장소 계정의 테이블 목록 합니다.
3. 테이블에 대 한 hello 바로 가기 메뉴를 열고 **뷰 테이블**합니다.
   
    ![솔루션 탐색기에 있는 Azure 테이블](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

hello 테이블은 엔터티 (행에 표시) 및 속성 (열에 표시)로 구성 됩니다. 다음 그림 hello hello에 나열 된 엔터티를 표시 하는 예를 들어 **테이블 디자이너**:

### <a name="tooedit-table-data"></a>tooedit 테이블 데이터
1. Hello에 **테이블 디자이너**를 엔터티 (단일 행) 또는 속성 (단일 셀)에 대 한 hello 바로 가기 메뉴를 열고 다음 선택 **편집**합니다.
   
    ![테이블 엔터티 추가 또는 편집](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    단일 테이블의 엔터티에 필요한 toohave hello 동일 속성 (열)의 설정 되지 않습니다. 제한 사항에 나오는 테이블 데이터 보기 및 편집에 유의 hello에 보관 합니다.
   
   * 이진 데이터(byte[] 형식)를 보거나 편집할 수 없지만 테이블에 저장할 수는 있습니다.
   * Hello를 편집할 수 없습니다 **PartitionKey** 또는 **RowKey** azure에서 테이블 저장소는 해당 작업을 지원 하지 않는 값입니다.
   * Timestamp는 Azure 저장소 서비스가 사용하는 이름이므로 해당 이름의 속성을 만들 수 없습니다.
   * 날짜/시간 값을 입력 하면 컴퓨터의 적절 한 toohello 국가 및 언어 설정 되는 형식을 따라야 (hh: MM/DD/YYYY mm: 예를 들어 [AM | PM] 미국 [AM|PM]).

### <a name="tooadd-entities"></a>tooadd 엔터티
1. Hello에 **테이블 디자이너**, hello 선택 **엔터티 추가** 단추입니다.
   
    ![엔터티 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. Hello에 **엔터티 추가** 대화 상자 hello의 hello 값을 입력 **PartitionKey** 및 **RowKey** 속성입니다.
   
    ![엔터티 대화 상자 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Hello 엔터티를 삭제 하 고 다시 추가 하지 않으면 hello 대화 상자를 닫은 후 변경할 수 없으므로 신중 하 게 hello 값을 입력 합니다.

### <a name="toofilter-entities"></a>toofilter 엔터티
Hello hello 쿼리 작성기를 사용 하는 경우 테이블에 표시 되는 엔터티 집합을 사용자 지정할 수 있습니다.

1. tooopen hello 쿼리 작성기 보기에 대 한 테이블을 엽니다.
2. Hello 테이블 보기의 도구 모음에서 hello 쿼리 작성기 단추를 선택 합니다.
   
    hello **쿼리 작성기** 대화 상자가 나타납니다. hello 다음 그림에서는 쿼리를 작성 중인 hello 쿼리 작성기.
   
    ![쿼리 작성기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. 완료 하면 hello 대화 상자를 닫고 hello 쿼리를 작성 합니다. hello hello 쿼리의 결과 텍스트 형식이 WCF Data Services 필터로 텍스트 상자에 나타납니다.
4. toorun hello 쿼리, hello 녹색 삼각형 아이콘을 선택 합니다.
   
    Hello에 표시 되는 엔터티 데이터를 필터링 할 수 있습니다 **테이블 디자이너** hello 필터 필드에 직접 WCF Data Services 필터 문자열을 입력 합니다. 이 종류의 문자열 비슷한 tooa SQL WHERE 절이 있지만 toohello 서버에 HTTP 요청으로 전송 됩니다. Tooconstruct 문자열을 필터링 하는 방법에 대 한 정보를 참조 하십시오. [hello 테이블 디자이너에 대 한 필터 문자열 생성](https://msdn.microsoft.com/library/azure/ff683669.aspx)합니다.
   
    hello 다음 그림과 유효한 필터 문자열의 예:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>저장소 데이터 새로 고침
서버 탐색기에 저장소 계정에서 데이터를 가져오면 tooor 연결 되 면 hello 작업 toocomplete tooa 분이 걸릴 수도 있습니다. 연결할 수 없는 경우 hello 작업이 시간 초과 될 수 있습니다. 데이터를 검색 하는 동안 Visual Studio의 다른 부분에서 toowork를 계속할 수 있습니다. 너무 오래 걸리는 경우 toocancel hello 작업이 선택 hello **새로 고침 중지** hello 서버 탐색기 도구 모음 단추입니다.

#### <a name="toorefresh-blob-container-data"></a>toorefresh blob 컨테이너 데이터
* 선택 hello **Blob** 아래에 있는 노드 **저장소** hello 선택 **새로 고침** hello 서버 탐색기 도구 모음 단추입니다.
* 표시 되는 blob의 toorefresh hello 목록 선택 hello **Execute** 단추입니다.

#### <a name="toorefresh-table-data"></a>toorefresh 테이블 데이터
* 선택 hello **테이블** 아래에 있는 노드 **저장소** hello 선택 **새로 고침** 단추입니다.
* hello에 표시 되는 엔터티의 toorefresh hello 목록을 **테이블 디자이너**, hello 선택 **Execute** hello 단추 **테이블 디자이너**합니다.

#### <a name="toorefresh-queue-data"></a>toorefresh 큐 데이터
* 선택 hello **큐** 노드를 선택한 후 hello **새로 고침** 단추입니다.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>저장소 계정에 있는 모든 항목 toorefresh
* Hello 계정 이름을 선택 하 고 hello 선택 **새로 고침** 서버 탐색기에 대 한 hello 도구 모음에서 단추입니다.

### <a name="add-storage-accounts-by-using-server-explorer"></a>서버 탐색기를 사용하여 저장소 계정 추가
두 가지가 tooadd 저장소 계정을 서버 탐색기를 사용 하 여 합니다. Azure 구독에서 새 저장소 계정을 만들거나 기존 저장소 계정을 연결할 수 있습니다.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>서버 탐색기를 사용 하 여 새 저장소 계정 toocreate
1. 서버 탐색기에서 hello 저장소 노드에 대 한 hello 바로 가기 메뉴를 열고 하 고 저장소 계정 만들기를 선택 합니다.
   
    ![새 Azure 저장소 계정 만들기](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. 선택 또는 입력 hello hello에 새 저장소 계정에 대 한 정보를 다음 hello **저장소 계정 만들기** 대화 상자.
   
   * hello Azure 구독 toowhich tooadd hello 저장소 계정입니다.
   * hello 이름 toouse hello 새 저장소 계정에 대 한입니다.
   * hello 지역 또는 선호도 그룹 (예: 미국 서 부 또는 아시아의 경우).
   * 형식 hello 복제 원하는 toouse 지리적 중복 같은 hello 저장소 계정에 대 한 합니다.
3. **만들기**를 선택합니다.
   
    hello에 hello 새 저장소 계정을 표시 **저장소** 솔루션 탐색기의 목록입니다.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>서버 탐색기를 사용 하 여 기존 저장소 계정 tooattach
1. 서버 탐색기에서 hello Azure 저장소 노드에 대 한 hello 바로 가기 메뉴를 열고 한 다음 **외부 저장소 연결**합니다.
   
    ![기존 저장소 계정 추가](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. 선택 또는 입력 hello hello에 새 저장소 계정에 대 한 정보를 다음 hello **저장소 계정 만들기** 대화 상자.
   
   * hello 이름 tooattach 원하는 hello 기존 저장소 계정입니다. 이름을 입력 하거나 hello 목록에서 선택할 수 있습니다.
   * hello에 대 한 hello 키 저장소 계정을 선택 합니다. 저장소 계정을 선택할 때 일반적으로 이 값이 제공됩니다. Visual Studio tooremember hello 저장소 계정 키 hello 사용자 이름 및 암호 계정 키 상자를 선택 합니다.
   * hello 프로토콜 toouse tooconnect toohello 저장소 계정, HTTP, HTTPS 또는 사용자 지정 끝점 등입니다. 참조 [연결 문자열의 tooConfigure 방법](https://msdn.microsoft.com/library/azure/ee758697.aspx) 사용자 지정 끝점에 대 한 자세한 내용은 합니다.

### <a name="tooview-hello-secondary-endpoints"></a>tooview hello 보조 끝점
* Hello를 사용 하 여 저장소 계정을 만든 경우 **읽기 액세스 지역 중복** 복제 옵션을 보조 끝점을 볼 수 있습니다. Hello 계정 이름에 대 한 hello 바로 가기 메뉴를 열고 **속성**합니다.
  
    ![저장소 보조 끝점](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>서버 탐색기에서 저장소 계정 tooremove
* 서버 탐색기에서 hello 계정 이름에 대 한 hello 바로 가기 메뉴를 열고 한 다음 **삭제**합니다. 저장소 계정을 삭제하면 해당 계정에 저장된 키 정보도 제거됩니다.
  
  > [!NOTE]
  > 서버 탐색기에서 저장소 계정을 삭제 하면 저장소 계정 또는; 포함 된 모든 데이터가 적용 되지 않습니다. 단순히 서버 탐색기에서 hello 참조를 제거합니다. toopermanently 저장소 계정을 삭제, hello를 사용 하 여 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
  > 
  > 

## <a name="next-steps"></a>다음 단계
toolearn 방법에 대 한 Azure 저장소 서비스를 사용 하 여, 참조 [hello Azure 저장소 서비스에 액세스](https://msdn.microsoft.com/library/azure/ee405490.aspx)합니다.

