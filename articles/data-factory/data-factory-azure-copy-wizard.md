---
title: "팩터리 Azure 복사 마법사 aaaData | Microsoft Docs"
description: "Toouse 데이터 팩터리에 Azure 복사 마법사 toocopy 데이터로 지원 되는 데이터 원본 toosinks hello 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Azure Data Factory 복사 마법사
hello Azure 데이터 팩터리 복사 마법사는 종단 간 데이터 통합 시나리오에서 첫 번째 단계는 일반적으로 데이터 수집 하는 방법의 hello 프로세스 래핑할 수 있습니다. Hello Azure 데이터 팩터리 복사 마법사를 진행할 때 불필요 toounderstand JSON 정의 모두 연결 된 서비스, 데이터 집합 및 파이프라인에 대 한 합니다. hello 마법사 hello 선택한 데이터 원본 toohello 선택 된 대상에서 파이프라인 toocopy 데이터를 자동으로 만듭니다. 또한 hello 복사 마법사를 사용 하면 수집 되 고 된 제작 hello 시 toovalidate hello 데이터입니다. 이렇게 하면 시간이 절약 특히 때 사용자는 데이터 수집 hello에 대 한 처음으로 hello 데이터 원본의 합니다. toostart hello 복사 마법사를 클릭 하 여 hello **데이터 복사** 데이터 팩터리의 hello 홈 페이지에 바둑판식으로 배열 합니다.

![복사 마법사](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>빅 데이터를 위한 설계
이 분 후에 다양 한 원본 toodestinations tooeasily 이동 데이터를 사용 합니다. Hello 마법사를 통해 이동 후 파이프라인 복사 작업을 자동으로 만들어집니다를 종속 데이터 팩터리 엔터티 (연결 된 서비스 및 데이터 집합)와 함께 합니다. 추가 단계는 필요한 toocreate hello 파이프라인.   

![데이터 원본 선택](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> 단계별 지침은 toocreate, Azure blob tooan Azure SQL 데이터베이스 테이블에서 샘플 파이프라인 toocopy 데이터에 대 한 참조 hello [복사 마법사 자습서](data-factory-copy-data-wizard-tutorial.md)합니다.
>
>

hello 마법사는 다양 한 데이터 및 개체 유형을 지 원하는 hello 시작부터 빅 데이터 관련 설계 되었습니다. 수백 개의 폴더, 파일 또는 테이블을 이동하는 Data Factory 파이프라인을 만들 수 있습니다. hello 마법사는 자동 데이터 미리 보기, 스키마 캡처 및 매핑 및 데이터 필터링을 지원합니다.

## <a name="automatic-data-preview"></a>자동 데이터 미리 보기
원하는 작업 인지 hello 데이터 순서 toovalidate에 hello 선택한 데이터 원본의 hello 데이터의 일부를 미리 볼 수 있습니다 toocopy 합니다. 또한 hello 원본 데이터를 텍스트 파일에 있으면, hello 복사 마법사 구문 분석 hello 텍스트 파일 toolearn hello 행 및 열 구분 기호 및 스키마 자동으로 합니다.

![파일 형식 설정](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>스키마 캡처 및 매핑
hello 스키마 입력된 데이터의 경우에 따라 출력 데이터의 hello 스키마와 일치 하지 않을 수 있습니다. 이 시나리오에서는 hello 대상 스키마에서 원본 스키마 toocolumns hello에서에서 toomap 열 필요 합니다.

> [!TIP]
> 때 SQL Server 또는 Azure SQL 데이터 웨어하우스에 hello 대상 저장소, Data Factory에에서 hello 테이블이 존재 하지 않는 경우 Azure SQL 데이터베이스의 데이터 복사는 소스 스키마를 사용 하 여 자동 테이블 생성을 지원 합니다. 자세한 정보 [Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스 로부터 데이터 tooand 이동](./data-factory-azure-sql-data-warehouse-connector.md)합니다.
>

Hello 대상 스키마의 드롭다운 목록에서 tooselect hello 원본 스키마 toomap tooa 열에서 열을 사용 합니다. hello 복사 마법사는 toounderstand 열 매핑에 대 한 패턴을 시도합니다. 각 tooselect hello 열은 개별적으로 필요 하지 않도록 동일한 패턴 toohello hello 열의 놓으면 hello 적용 toocomplete hello 스키마 매핑. 원하는 경우 hello 드롭 다운 목록을 toomap hello 열 하나씩 사용 하 여 이러한 매핑을 재정의할 수 있습니다. hello 패턴 더 많은 열을 매핑해야 보다 정확 하 게 됩니다. hello 복사 마법사는 지속적으로 hello 패턴을 업데이트 하 고 궁극적으로 량에 도달 하면 매핑 hello 열에 대 한 hello 오른쪽 패턴 tooachieve 합니다.     

![스키마 매핑](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>데이터 필터링
데이터 tooselect 유일한 hello는 원본 데이터 복사 toobe toohello 싱크 데이터 저장소를 필터링 할 수 있습니다. 필터링을 사용 하면 hello 양의 hello 데이터 toobe 복사한 toohello 싱크 데이터를 저장 하 고 따라서 hello 복사 작업의 hello 처리량을 향상 시킵니다. Hello SQL 쿼리 언어를 사용 하 여 관계형 데이터베이스의 유연한 방식으로 toofilter 데이터를 제공 하거나 사용 하 여 Azure blob 폴더에 파일 [데이터 팩터리 함수 및 변수](data-factory-functions-variables.md)합니다.   

### <a name="filtering-of-data-in-a-database"></a>데이터베이스 데이터 필터링
hello 다음 스크린샷은 hello를 사용 하 여 SQL 쿼리 `Text.Format` 함수 및 `WindowStart` 변수입니다.

![식 유효성 검사](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Azure Blob 폴더의 데이터 필터링
변수를 사용 하 여 hello 폴더 경로 toocopy 데이터에 따라 런타임에 결정 되는 폴더에 있는 [시스템 변수](data-factory-functions-variables.md#data-factory-system-variables)합니다. 지원 되는 hello 변수는: **{year}**, **{month}**, **{day}**, **{시간}**, **{분}**, 및 **{사용자 지정}**합니다. 예를 들어 inputfolder/{year}/{month}/{day}와 같습니다.

형식에 따라 hello에 폴더를 입력 한다고 가정 합니다.

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Hello 클릭 **찾아보기** 단추에 대 한 **파일 또는 폴더**, 이러한 폴더의 tooone 찾아보기 (2016-03을 > 예를 들어-> 01-02 >)를 클릭 하 고 **선택**합니다. 표시 되어야 `2016/03/01/02` hello 텍스트 상자에 있습니다. 이제 대체 **2016** 와 **{year}**, **03** 와 **{month}**, **01** 와 **{day}** , 및 **02** 와 **{시간}**, 및 키를 눌러 hello **탭** 키입니다. 이러한 네 개의 변수 드롭 다운 목록을 tooselect hello 형식을 표시 되어야 합니다.

![시스템 변수 사용](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

다음 스크린 샷에서 hello와 같이 사용할 수도 있습니다는 **사용자 지정** 변수 프로그램과 [형식 문자열을 지원](https://msdn.microsoft.com/library/8kb3ddd4.aspx)합니다. 해당 구조를 사용 하 여 hello와 폴더 tooselect **찾아보기** 먼저 단추입니다. 다음 사용 하 여 값을 바꿉니다 **{사용자 지정}**, 및 키를 눌러 hello **탭** 키 toosee hello 텍스트 상자 hello 형식 문자열을 입력할 수 있습니다.     

![사용자 지정 변수 사용](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>일정 옵션
실행할 수 있습니다 hello 복사 작업이 한 번 또는 일정에 따라 (시간별, 일별, 등). 온-프레미스, 클라우드 및 로컬 데스크톱 복사본을 포함 하 여 환경에 걸쳐 hello 커넥터의 hello 너비에 대 한 이러한 두 옵션을 사용할 수 있습니다.

일회성 복사 작업은 한 번만 원본 tooa 대상에서 데이터를 이동할을 수 있습니다. 모든 크기 및 모든 지원 되는 형식 toodata 적용 됩니다. 예약 된 hello 복사 하면 지정 된 되풀이에 toocopy 데이터 있습니다. 풍부한 설정 (예: 재시도, 제한 시간 및 경고)를 사용할 수 있습니다 tooconfigure hello 복사를 예약 합니다.

![일정 속성](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>다음 단계
Hello 데이터 팩터리 복사 마법사 toocreate 파이프라인을 사용 하 여 복사 작업으로의 간략 한 설명이 참조 하십시오. [자습서: hello 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다.
