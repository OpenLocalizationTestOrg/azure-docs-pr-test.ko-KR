---
title: "aaaGet 시작 저장소 탐색기 (미리 보기) | Microsoft Docs"
description: "저장소 탐색기(미리 보기)를 사용하여 Azure 저장소 리소스 관리"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>저장소 탐색기(미리 보기) 시작
## <a name="overview"></a>개요
Azure 저장소 탐색기 (미리 보기)는 Windows, macOS 등 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있도록 하는 독립 실행형 앱입니다. 이 문서에서는 hello tooand Azure 저장소 계정 관리를 연결 하는 다양 한 방법을 배웁니다.

![Microsoft Azure Storage 탐색기(미리 보기)][15]

## <a name="prerequisites"></a>필수 조건
* [저장소 탐색기(미리 보기) 다운로드 및 설치](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Tooa 저장소 계정 또는 서비스를 연결 합니다.
저장소 탐색기 (미리 보기)에서는 여러 가지 방법으로 tooconnect toostorage 계정을 제공 합니다. 예를 들어 다음을 수행할 수 있습니다.
* Azure 구독과 연결 된 toostorage 계정을 연결 합니다.
* 다른 Azure 구독에서 toostorage 계정과 공유 되는 서비스를 연결 합니다.
* 연결 tooand hello Azure 저장소 에뮬레이터를 사용 하 여 로컬 저장소를 관리 합니다. 

또한 글로벌 및 국가별 Azure에서 저장소 계정으로 작업할 수 있습니다.

* [Tooan Azure 구독 연결](#connect-to-an-azure-subscription): tooyour Azure 구독에 속하는 저장소 리소스를 관리 합니다.
* [로컬 개발 저장소에서 작동](#work-with-local-development-storage): hello Azure 저장소 에뮬레이터를 사용 하 여 로컬 저장소를 관리 합니다.
* [Tooexternal 저장소 연결](#attach-or-detach-an-external-storage-account): tooanother Azure 구독에 속하는 저장소 리소스를 관리 또는 hello 저장소 계정의 이름, 키 및 끝점을 사용 하 여 Azure 클라우드에서 national 됩니다.
* [SAS를 사용 하 여 저장소 계정을 연결](#attach-storage-account-using-sas): 저장소 리소스는 공유 액세스 서명 (SAS)를 사용 하 여 Azure 구독 tooanother 속하는 관리 합니다.
* [서비스는 SAS를 사용 하 여 연결](#attach-service-using-sas):는 SAS를 사용 하 여 Azure 구독 tooanother 속하는 특정 저장소 서비스 (blob 컨테이너, 큐 또는 테이블)을 관리 합니다.

## <a name="connect-tooan-azure-subscription"></a>Tooan Azure 구독 연결
> [!NOTE]
> Azure 계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.
>
>

1. 저장소 탐색기(미리 보기)에서 **Azure 계정 설정**을 선택합니다.

    ![Azure 계정 설정][0]

2. hello 왼쪽된 창에는 모든 hello Microsoft 계정에 로그인 한 사용자 표시 됩니다. 선택 tooconnect tooanother 계정 **계정 추가**, 한 다음 활성 Azure 구독을 하나 이상와 연결 된 Microsoft 계정 사용 하 여 hello 지침 toosign를 따릅니다.

    >[!NOTE]
    >Toonational Azure (예: Azure 독일, Azure Government 및 로그인을 통해 Azure 중국) 연결 하는 현재 지원 되지 않습니다. Hello 참조 "연결 또는 분리 된 외부 저장소 계정"는 방법에 대 한 섹션 tooconnect toonational Azure 저장소 계정입니다.

3. 후 성공적으로 Microsoft 계정으로 로그인, hello 왼쪽 창의 hello 채워집니다 해당 계정과 연결 된 Azure 구독. 선택 hello toowork, 한 다음 선택 하는 Azure 구독이 **적용**합니다. (선택 **모든 구독** 토글 모두 지정 하거나 hello를 선택 하면 Azure 구독을 나열 합니다.)

    ![Azure 구독 선택][3]  
    hello 왼쪽된 창에 선택한 hello Azure 구독과 연결 된 hello 저장소 계정을 표시 됩니다.

    ![선택한 Azure 구독][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Tooan 스택 Azure 구독 연결

연결 tooan 스택 Azure 구독에 대 한 정보를 참조 하십시오. [저장소 탐색기 연결 tooan Azure 스택 구독](azure-stack/azure-stack-storage-connect-se.md)합니다.

## <a name="work-with-local-development-storage"></a>로컬 개발 저장소로 작업
저장소 탐색기 (미리 보기)를 hello Azure 저장소 에뮬레이터를 사용 하 여 로컬 저장소에 대해 작업할 수 있습니다. 이 방법에 대 한 코드 및 테스트 저장소 hello Azure 저장소 에뮬레이터에서 에뮬레이트 되 hello 저장소 계정 때문에 Azure에 배포 된 저장소 계정이 필요 없이 작성할 수 있습니다.

> [!NOTE]
> hello Azure 저장소 에뮬레이터는 현재 Windows에 대해서만 지원 됩니다.
>
>

1. 저장소 탐색기 (미리 보기)의 hello 왼쪽된 창에서 확장 hello **(로컬 및 연결 된)** > **저장소 계정은** > **(개발)** 노드.

    ![로컬 개발 노드][21]

2. 입력 정보 요청된 toodo 모르는 hello Azure 저장소 에뮬레이터를 아직 설치 하지 않은 경우 정보 표시줄을 통해 너무 합니다. Hello 정보 표시줄 표시 되 면 선택 **hello 최신 버전 다운로드**, 다음 hello 에뮬레이터를 설치 합니다.

    ![Azure Storage 에뮬레이터 프롬프트 다운로드][22]

3. Hello 에뮬레이터를 설치한 후 만들 하 고 로컬 blob, 큐 및 테이블을 작업할 수 있습니다. toolearn toowork 각 저장소 계정으로 입력 하는 방법을 hello 다음 중 하나를 참조 합니다.

    * [Azure Blob 저장소 리소스 관리](vs-azure-tools-storage-explorer-blobs.md)
    * Azure 파일 공유 저장소 리소스 관리: *서비스 예정*
    * Azure 큐 저장소 리소스 관리: *서비스 예정*
    * Azure 테이블 저장소 리소스 관리: *서비스 예정*

## <a name="attach-or-detach-an-external-storage-account"></a>외부 저장소 계정 연결 또는 분리
저장소 탐색기 (미리 보기)로 저장소 계정을 쉽게 공유할 수 있도록 tooexternal 저장소 계정에 연결할 수 있습니다. 이 섹션에서는 어떻게 tooattach too(and detach from) 외부 저장소 계정입니다.

### <a name="get-hello-storage-account-credentials"></a>Hello 저장소 계정 자격 증명 가져오기
외부 저장소 계정 tooshare 해당 계정의 hello 소유자 값이 먼저 hello 계정 (계정 이름 및 키) hello 자격 증명을 가져오지 및 hello 사람이 tooattach toothat (외부) 계정과 해당 정보를 공유할 합니다. Hello 다음을 수행 하 여 hello Azure 포털을 통해 hello 저장소 계정 자격 증명을 가져올 수 있습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. **찾아보기**를 선택합니다.

3. **저장소 계정**을 선택합니다.

4. Hello에 **저장소 계정은** 블레이드, 원하는 선택 hello 저장소 계정입니다.

5. Hello에 **설정** 블레이드 hello에 대 한 저장소 계정을 선택, 선택 **액세스 키**합니다.

    ![액세스 키 옵션][5]

6. Hello에 **액세스 키** 블레이드, 복사 hello **저장소 계정 이름** 및 **key1** toohello 저장소 계정을 연결할 때 사용할 값입니다.

    ![액세스 키][6]

### <a name="attach-tooan-external-storage-account"></a>Tooan 외부 저장소 계정을 연결합니다
hello 계정 이름과 키 tooattach tooan 외부 저장소 계정에 필요 합니다. hello "Get hello 저장소 계정 자격 증명" 섹션에서 이들 값이 tooobtain Azure 포털 hello 하는 방법을 설명 합니다. 그러나 hello 포털에서 계정 키 hello 라고 **key1**합니다. 따라서 저장소 탐색기 (미리 보기)를 묻는 메시지가 나타나면 계정 키를 입력 하면 hello **key1** 값입니다.

1. 저장소 탐색기 (미리 보기)에서 선택 **tooAzure 저장소 연결**합니다.

    ![연결 tooAzure 저장소 옵션][23]

2. Hello에 **tooAzure 저장소 연결** 대화 상자 hello 계정 키를 지정 합니다 (hello **key1** hello Azure 포털의에서 값)을 선택한 후 **다음**합니다.

    > [!NOTE]
    > National Azure에서 저장소 계정에서 hello 저장소 연결 문자열을 입력할 수 있습니다. 예를 들어 tooconnect tooAzure 독일 저장소 계정 연결 문자열 비슷한 toohello 다음을 입력 합니다. 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >Hello Azure에서에서 hello 연결 문자열을 가져올 수 있습니다 hello에 포털 동일에 설명 된 방식으로 hello "hello 저장소 계정 자격 증명 가져오기" 섹션.

    ![연결 tooAzure 저장소 대화 상자][24]

3. Hello에 **외부 저장소 연결** 대화 상자의 hello **계정 이름** 상자, hello 저장소 계정 이름을 입력 하 고, 다른 원하는 설정을 지정 하 고 다음 선택 **다음**합니다.

    ![외부 저장소 연결 대화 상자][8]

4. Hello에 **연결 요약** 대화 상자, hello 정보를 확인 합니다. 어느 것에 toochange를 하려는 경우 선택 **다시** 원하는 hello 설정을 다시 입력 하 고 있습니다. 

5. **연결**을 선택합니다.

6. Hello 외부 저장소 계정을 붙습니다 성공적으로 연결 **(외부)** toohello 저장소 계정 이름을 추가 합니다.

    ![Tooan 외부 저장소 계정을 연결할 때의 결과][9]

### <a name="detach-from-an-external-storage-account"></a>외부 저장소 계정에서 분리
1. 원하는 toodetach, 다음을 선택 하는 hello 외부 저장소 계정을 마우스 오른쪽 단추로 클릭 **분리**합니다.

    ![저장소 옵션에서 분리][10]

2. Hello 확인 메시지에서 선택 **예** hello 외부 저장소 계정에서 tooconfirm hello 분리 합니다.

## <a name="attach-a-storage-account-by-using-an-sas"></a>SAS를 사용하여 저장소 계정 연결
[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) admin 님 안녕하세요 Azure 구독의 tooprovide Azure 구독 자격 증명 필요 없이 임시 액세스 tooa 저장소 계정 권한을 부여할 수 있습니다.

tooillustrate이이 시나리오에서는 해당 UserA Azure 구독의 관리자는 한다고 가정 하겠습니다 및 UserA가 tooallow UserB tooaccess 특정 사용 권한이 있는 제한 된 시간에 대 한 저장소 계정:

1. UserA는 기간 및 hello 필요한 사용 권한이 있는 특정 시간에 대 한 (hello 저장소 계정에 대 한 hello 연결 문자열의 구성)는 SAS를 생성 합니다.

2. UserA 공유 액세스 toohello 저장소 계정 게 hello 사용자 (이 예제에서 사용자 b)와 SAS hello 합니다.  

3. 사용자 b를 사용 하 여 tooUserA 속하는 저장소 탐색기 (미리 보기) tooattach toohello 계정을 사용 하 여 hello SAS를 제공 합니다.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>SAS는 원하는 tooshare hello 계정에 대 한 가져오기
1. 저장소 탐색기 (미리 보기)를 공유 하 고 다음을 선택 하려는 hello 저장소 계정을 마우스 오른쪽 단추로 클릭 **공유 액세스 서명을 가져올**합니다.

    ![SAS 상황에 맞는 메뉴 옵션 가져오기][13]

2. Hello에 **공유 액세스 서명을** 대화 상자를 hello 계정에 대 한 한 다음 선택 하는 사용 권한과 hello 기간 지정 **만들기**합니다.

    ![SAS 가져오기 대화 상자][14]  
    hello **공유 액세스 서명을** 대화 상자가 열리고 hello SAS 표시 됩니다.

3. 다음 toohello **연결 문자열**선택, **복사** toocopy 것 toohello 클립보드에 선택한 후 **닫기**합니다.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Hello SAS를 사용 하 여 공유 toohello 계정 연결
1. 저장소 탐색기 (미리 보기)에서 선택 **tooAzure 저장소 연결**합니다.

    ![연결 tooAzure 저장소 옵션][23]

2. Hello에 **tooAzure 저장소 연결** 대화 상자, hello 연결 문자열을 지정 하 고 다음 선택 **다음**합니다.

    ![연결 tooAzure 저장소 대화 상자][24]

3. Hello에 **연결 요약** 대화 상자, hello 정보를 확인 합니다. toomake 변경 선택 **다시**, 한 후 원하는 hello 설정을 입력 합니다. 

4. **연결**을 선택합니다.

5. Hello 저장소 계정이 표시 됩니다, 연결 후 **(SAS)** 사용자가 제공한 toohello 계정 이름을 추가 합니다.

    ![SAS를 사용 하 여 연결 된 tooan 계정의 결과][17]

## <a name="attach-a-service-by-using-an-sas"></a>SAS를 사용하여 서비스 연결
hello "는 SAS를 사용 하 여 저장소 계정을 연결" 섹션으로 인해 Azure 구독 관리자를 생성 하 고 hello 저장소 계정에 대 한 SAS를 공유 하 여 임시 액세스 tooa 저장소 계정을 부여 하는 방법에 대해 설명 합니다. 마찬가지로, 저장소 계정 내에서 특정 서비스(Blob 컨테이너, 큐 또는 테이블)에 대한 SAS를 생성할 수 있습니다.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Tooshare hello 서비스에 대 한 SAS를 생성 합니다.
이 컨텍스트에서 서비스는 Blob 컨테이너, 큐 또는 테이블일 수 있습니다. 나열 된 서비스에 대 한 SAS toogenerate hello 참조:

* [Blob 컨테이너에 대 한 SAS hello 가져오기](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* 파일 공유에 대 한 SAS hello 가져오기: *출시 예정*
* 큐에 대 한 SAS hello 가져오기: *출시 예정*
* 테이블에 대 한 SAS hello 가져오기: *출시 예정*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Toohello 공유 계정을 사용 하 여 서비스 hello SAS 연결
1. 저장소 탐색기 (미리 보기)에서 선택 **tooAzure 저장소 연결**합니다.

    ![연결 tooAzure 저장소 옵션][23]

2. Hello에 **tooAzure 저장소 연결** 대화 상자는 hello SAS URI를 지정 하 고 다음 선택 **다음**합니다.

    ![연결 tooAzure 저장소 대화 상자][24]

3. Hello에 **연결 요약** 대화 상자, hello 정보를 확인 합니다. toomake 변경 선택 **다시**, 한 후 원하는 hello 설정을 입력 합니다. 

4. **연결**을 선택합니다.

5. 연결 된 후 hello 새로 연결 된 서비스 아래에 표시 됩니다 hello **서비스 SAS ()** 노드.

    ![Tooa 공유 서비스는 SAS를 사용 하 여 연결의 결과][20]

## <a name="search-for-storage-accounts"></a>저장소 계정 검색
신속 하 게 toolocate 특정 저장소 계정의 저장소 계정 목록이 긴 있을 경우 toouse hello 검색 상자 hello 왼쪽 창의 hello 상단에 있습니다.

Hello 검색 상자에 입력할 때 hello 왼쪽 창 toothat 포인트 입력 한 hello 검색 값과 일치 하는 표시 hello 저장소 계정 예를 들어 한 모든 저장소 계정 이름에 대해 포함 검색 **tarcher** hello 스크린 샷 뒤에 표시 됩니다.

![저장소 계정 검색][11]

## <a name="next-steps"></a>다음 단계
* [저장소 탐색기(미리 보기)를 사용하여 Azure Blob Storage 리소스 관리](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
