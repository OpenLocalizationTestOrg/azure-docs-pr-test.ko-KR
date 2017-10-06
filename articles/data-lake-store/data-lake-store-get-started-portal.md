---
title: "데이터 레이크 저장소와 Azure 포털 tooget aaaUse 시작 | Microsoft Docs"
description: "Hello Azure 포털 toocreate 데이터 레이크 저장소 계정 사용 하 고 hello 데이터 레이크 저장소의에서 기본 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작
> [!div class="op_single_selector"]
> * [포털](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Toouse Azure 포털 toocreate Azure 데이터 레이크 저장소 계정 hello 하 고 폴더를 만들어 업로드 한 데이터 파일을 다운로드할 같은 기본 작업을 수행 하는 방법에 대해 알아봅니다, 그리고 계정, 등을 삭제 합니다. 자세한 내용은 [Azure Data Lake Store의 개요](data-lake-store-overview.md)를 참조하세요.

다음 두 비디오 hello 포함이 문서에 설명 된 대로 동일한 정보를 hello:

* [Data Lake 저장소 계정 만들기](https://mix.office.com/watch/1k1cycy4l4gen)
* [Hello 데이터 탐색기를 사용 하 여 데이터 레이크 저장소에서 데이터 관리](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.

* **Azure 구독**. [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

## <a name="create-an-azure-data-lake-store-account"></a>Azure 데이터 레이크 저장소 계정 만들기

1. 새 toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기**를 클릭하고 **데이터 + 저장소**를 클릭한 다음 **Azure Data Lake Store**를 클릭합니다. Hello에 hello 정보 읽기 **Azure 데이터 레이크 저장소** 블레이드에서 하 고 클릭 한 다음 **만들기** hello 블레이드 hello 하단 왼쪽된 모서리에 있습니다.
3. Hello에 **새로 데이터 레이크 저장소** 블레이드에서 hello 스크린 샷 뒤에 표시 된 대로 hello 값을 제공:
   
    ![새 Azure Data Lake Store 계정 만들기](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "새 Azure Data Lake 계정 만들기")
   
   * **이름**. Hello Data Lake 저장소 계정에 대 한 고유 이름을 입력 합니다.
   * **구독**. 새 데이터 레이크 저장소 계정 toocreate 원하는 hello 구독을 선택 합니다.
   * **리소스 그룹**. 기존 리소스 그룹을 선택 하거나 선택 하는 hello **새로 만들기** 옵션 toocreate 하나입니다. 리소스 그룹은 응용 프로그램에 관련된 리소스를 보유하는 컨테이너입니다. 자세한 내용은 [Azure의 리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 참조하세요.
   * **위치**: toocreate hello Data Lake 저장소 계정이 저장할 위치를 선택 합니다.
   * **암호화 설정**. 세 개의 옵션이 있습니다.
     
     * **암호화를 활성화하지 않습니다**.
     * **Azure Data Lake에서 관리하는 키를 사용합니다**.  Azure 데이터 레이크 저장소 toomanage 암호화 키를 선택 합니다.
     * **Azure Key Vault에서 키를 선택합니다**. 기존 Azure Key Vault를 선택하거나 새 Key Vault를 선택할 수 있습니다. 키 자격 증명 모음에서 toouse hello 키 hello tooaccess hello Azure 키 자격 증명 모음 Azure 데이터 레이크 저장소 계정에 대 한 권한을 할당 해야 합니다. Hello 지침은 [주요 자격 증명 모음 사용 권한을 tooAzure 할당](#assign-permissions-to-azure-key-vault)합니다.
       
        ![Data Lake Store 암호화](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Data Lake Store 암호화")
       
        클릭 **확인** hello에 **암호화 설정** 블레이드입니다.

        자세한 내용은 [Azure Data Lake Store의 데이터 암호화](./data-lake-store-encryption.md)를 참조하세요.

4. **만들기**를 클릭합니다. Toopin hello 계정 toohello 대시보드를 선택 toohello 대시보드 다시 라인 되 고 Data Lake 저장소 계정 구축의 hello 진행률을 볼 수 있습니다. 한 번 hello Data Lake 저장소 계정이 프로 비전 되 면 hello 계정 블레이드를 표시 합니다.

Azure Resource Manager 템플릿을 사용하여 Data Lake Store 계정을 만들 수도 있습니다. 이러한 템플릿은에서 [Azure QuickStart 템플릿](https://azure.microsoft.com/resources/templates/?term=data+lake+store)에서 액세스할 수 있습니다.

- 데이터 암호화 미지원: [데이터 암호화 없이 Azure Data Lake Store를 배포합니다](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/).
- Data Lake Store를 사용하여 데이터 암호화 지원: [암호화로 Data Lake Store 계정을 배포합니다(Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
- Azure Key Vault를 사용하여 데이터 암호화 지원: [암호화로 Data Lake Store 계정을 배포합니다(Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).

### <a name="assign-permissions-to-azure-key-vault"></a>주요 자격 증명 모음 사용 권한을 tooAzure 할당
Hello Data Lake 저장소 계정에서 Azure 키 자격 증명 모음 tooconfigure 암호화에서 키를 사용한 경우에 hello 데이터 레이크 저장소 계정과 hello Azure 키 자격 증명 모음 계정 간의 액세스를 구성 해야 합니다. Hello 단계 toodo 하므로 다음을 수행 합니다.

1. Hello Azure 키 자격 증명 모음에서에서 키를 사용 하는 hello Data Lake 저장소 계정에 대 한 hello 블레이드 hello 위쪽에 경고를 표시 합니다. Hello 경고 tooopen hello 클릭 **키 자격 증명 모음 사용 권한 구성** 블레이드입니다.
   
    ![Data Lake Store 암호화](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Data Lake Store 암호화")
2. hello 블레이드 두 옵션 tooconfigure 액세스를 보여 줍니다.
   
   * Hello 첫 번째 옵션에서 클릭 **권한 부여** tooconfigure 액세스 합니다. hello 첫 번째 옵션은 hello 데이터 레이크 저장소 계정을 만든 hello 사용자 hello Azure 키 자격 증명 모음에 대 한 관리자 이기도 한 경우에 사용할 수 있습니다.
   * hello 방법도 toorun hello PowerShell cmdlet은 hello 블레이드를 표시 합니다. Azure 키 자격 증명 모음 hello의 toobe hello 소유자 또는 hello Azure 키 자격 증명 모음에 hello 기능 toogrant 권한이 있어야 합니다. Hello cmdlet을 실행 한 후 toohello 블레이드를 다시 시도 하 고 클릭 **사용** tooconfigure 액세스 합니다.

## <a name="createfolder"></a>Azure 데이터 레이크 저장소 계정에서 폴더 만들기
데이터 레이크 저장소 계정 toomanage에서 폴더를 만들고 데이터를 저장할 수 있습니다.

1. 사용자가 만든 hello 데이터 레이크 저장소 계정을 엽니다. Hello 왼쪽된 창에서 클릭 **찾아보기**, 클릭 **데이터 레이크 저장소**, hello 데이터 레이크 저장소 블레이드에서 toocreate 폴더 원하는 hello 계정 이름을 클릭 하 고 있습니다. Hello 계정 toohello 시작 보드를 고정 하는 경우 해당 계정 타일을 클릭 합니다.
2. 데이터 레이크 저장소 계정 블레이드에서 **데이터 탐색기**를 클릭합니다.
   
    ![Data Lake Store 계정에 폴더 만들기](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Data Lake Store 계정에 폴더 만들기")
3. 데이터 레이크 저장소 계정 블레이드를 사용 하 여 클릭 **새 폴더**hello 새 폴더에 대 한 이름을 입력 한 다음 클릭 **확인**합니다.
   
    ![Data Lake Store 계정에 폴더 만들기](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Data Lake Store 계정에 폴더 만들기")
   
    새로 만든 hello hello에 나열 됩니다 **데이터 탐색기** 블레이드입니다. 모든 수준까지 중첩된 폴더를 만들 수 있습니다.
   
    ![Data Lake 계정에 폴더 만들기](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Data Lake 계정에 폴더 만들기")

## <a name="uploaddata"></a>데이터 tooAzure Data Lake 저장소 계정에 업로드
사용자 데이터 tooan hello 루트 수준 또는 tooa 만든 폴더에 hello 계정 내에서 직접 Azure 데이터 레이크 저장소 계정에 업로드할 수 있습니다. Hello에 스크린 샷, 다음에 따라 hello 단계 tooupload 파일 tooa 하위 hello에서 **데이터 탐색기** 블레이드입니다. 이 화면 캡처 hello 파일이 업로드 된 tooa 하위 폴더 (빨간색 상자에서 표시) hello 이동 경로에 표시 된 경우

몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다.

![데이터 업로드](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "데이터 업로드")

## <a name="properties"></a>저장 된 데이터 속성 및 hello에 사용할 수 있는 작업
Hello 새로 추가 된 파일 tooopen hello 클릭 **속성** 블레이드입니다. hello 파일과 hello 파일에서 수행할 수 있는 하는 hello 동작은 연관 된 hello 속성은이 블레이드 됩니다. 또한 hello 스크린 샷 뒤의 hello 빨간색 상자에 강조 Azure 데이터 레이크 저장소 계정에 전체 경로 toofile hello를 복사할 수 있습니다.

![Hello 데이터에 속성](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "hello 데이터에 속성")

* 클릭 **미리 보기** toosee hello 브라우저에서 직접 hello 파일의 미리 보기. Hello 미리 보기의 경우에의 hello 형식을 지정할 수 있습니다. 클릭 **미리 보기**, 클릭 **형식** hello에 **파일 미리 보기** 블레이드 및 hello **파일 미리 보기 형식** 블레이드 등 hello 옵션 지정 행 toodisplay의 수치로 toouse, 구분 기호 toouse 등 인코딩입니다.
  
  ![파일 미리 보기 형식](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "파일 미리 보기 형식")
* 클릭 **다운로드** toodownload hello 파일 tooyour 컴퓨터입니다.
* 클릭 **파일 이름 바꾸기** toorename hello 파일입니다.
* 클릭 **파일 삭제** toodelete hello 파일입니다.

## <a name="secure-your-data"></a>데이터 보호
Azure Active Directory 및 액세스 제어 (Acl)를 사용 하 여 Azure 데이터 레이크 저장소 계정에 저장 된 hello 데이터를 보호할 수 있습니다. 방법에 대 한 참조는 toodo [Azure 데이터 레이크 저장소의 데이터를 보호 하려면](data-lake-store-secure-data.md)합니다.

## <a name="delete-azure-data-lake-store-account"></a>Azure 데이터 레이크 저장소 계정 삭제
데이터 레이크 저장소 블레이드에서 Azure 데이터 레이크 저장소 계정을 클릭 toodelete **삭제**합니다. tooconfirm hello 동작 toodelete 원하는 hello 계정의 증명된 tooenter hello 이름이 됩니다. Hello hello 계정 이름을 입력 한 다음 클릭 **삭제**합니다.

![Data Lake 계정 삭제](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Data Lake 계정 삭제")

## <a name="next-steps"></a>다음 단계
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight에 데이터 레이크 저장소 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Data Lake Store에 대한 진단 로그 액세스](data-lake-store-diagnostic-logs.md)

