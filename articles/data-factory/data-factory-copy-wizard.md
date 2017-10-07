---
title: "복사 마법사-Azure 사용 하 여 쉽게 aaaCopy 데이터 | Microsoft Docs"
description: "Toouse 데이터 팩터리 복사 마법사 toocopy 데이터로 지원 되는 데이터 원본 toosinks hello 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Azure Data Factory 복사 마법사를 사용하여 데이터를 쉽게 복사 또는 이동
hello Azure 데이터 팩터리 복사 마법사는 종단 간 데이터 통합 시나리오에서 첫 번째 단계는 일반적으로 데이터 수집 하는 방법의 tooease hello 프로세스입니다. Hello Azure 데이터 팩터리 복사 마법사를 진행할 때 불필요 toounderstand JSON 정의 모두 연결 된 서비스, 데이터 집합 및 파이프라인에 대 한 합니다. 그러나 hello 마법사의 모든 hello 단계를 완료 한 후 hello 마법사 파이프라인 toocopy 데이터 hello 선택한 데이터 원본 toohello 선택 된 대상에서 자동으로 만듭니다. 또한 복사 마법사를 사용 하면 toovalidate hello 데이터가 수집 되 고 된 제작 hello 시 상당한 시간을 저장 하는 hello 특히 때 하면는 수집 hello에 대 한 데이터 처음으로 hello 데이터 원본에서 합니다. toostart hello 복사 마법사를 클릭 하 여 hello **데이터 복사** 데이터 팩터리의 hello 홈 페이지에 바둑판식으로 배열 합니다.

![복사 마법사](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>데이터를 복사할 수 있는 직관적인 마법사
이 분 후에 다양 한 원본 toodestinations tooeasily 이동 데이터를 사용 합니다. Hello 마법사를 거친 후 복사 작업으로 파이프라인은 자동으로 있습니다에 대 한 종속 데이터 팩터리 엔터티 (연결 된 서비스 및 데이터 집합)와 함께 생성 됩니다. 추가 단계는 필요한 toocreate hello 파이프라인.   

![데이터 원본 선택](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> 참조 [복사 마법사 자습서](data-factory-copy-data-wizard-tutorial.md) , Azure blob tooan Azure SQL 데이터베이스 테이블에서 샘플 파이프라인 toocopy 데이터에 대 한 단계별 지침 toocreate 문서입니다. 
> 
> 

hello 마법사는 hello 시작부터 빅 데이터 관련 설계 되었습니다. 간단 하 고 효율적인 tooauthor 데이터 팩터리 파이프라인 수백 폴더, 파일 또는 hello 데이터 복사 마법사를 사용 하 여 테이블을 이동 하는 경우 hello 마법사는 다음 세 가지 기능 hello: 자동 데이터 미리 보기, 스키마 캡처 및 매핑 및 데이터를 필터링 합니다. 

## <a name="automatic-data-preview"></a>자동 데이터 미리 보기
hello 복사 마법사 있습니다 tooreview hello 데이터 hello에서 선택한 데이터 원본 수에 대 한 toovalidate hello 데이터는 hello 마우스 오른쪽 단추로 원하는 toocopy 데이터가 있는지 여부를 수 있습니다. 또한 hello 원본 데이터를 텍스트 파일에 있으면, hello 복사 마법사 구문 분석 hello 텍스트 파일 toolearn 행 및 열 구분 기호 및 스키마 자동으로 합니다. 

![파일 형식 설정](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>스키마 캡처 및 매핑
hello 스키마 입력된 데이터의 경우에 따라 출력 데이터의 hello 스키마와 일치 하지 않을 수 있습니다. 이 시나리오에서는 hello 대상 스키마에서 원본 스키마 toocolumns hello에서에서 toomap 열 필요 합니다. 

hello 복사 마법사는 자동으로 hello 소스 스키마 toocolumns hello 대상 스키마에서의 열을 매핑합니다. 사용자 수 hello 드롭 다운 목록을 사용 하 여 hello 매핑을 재정의 (또는) toobe hello 데이터를 복사 하는 동안 해당 열에 필요한 지 여부를 지정 합니다.   

![스키마 매핑](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>데이터 필터링
hello 마법사 toofilter 데이터 tooselect 유일한 hello는 원본 데이터 복사 toobe toohello 대상/싱크 데이터 저장소를 사용 합니다. 필터링을 사용 하면 hello 양의 hello 데이터 toobe 복사한 toohello 싱크 데이터를 저장 하 고 따라서 hello 복사 작업의 hello 처리량을 향상 시킵니다. Azure blob 폴더에 있는 SQL 쿼리 언어 (또는) 파일을 사용 하 여 사용 하 여 관계형 데이터베이스의 유연한 방식으로 toofilter 데이터를 제공 [데이터 팩터리 함수 및 변수](data-factory-functions-variables.md)합니다.   

### <a name="filtering-of-data-in-a-database"></a>데이터베이스 데이터 필터링
Hello 예에서 hello SQL 쿼리에서 사용 하 여 hello `Text.Format` 함수 및 `WindowStart` 변수입니다. 

![식 유효성 검사](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Azure Blob 폴더의 데이터 필터링
변수를 사용 하 여 hello 폴더 경로 toocopy 데이터에 따라 런타임에 결정 되는 폴더에 있는 [시스템 변수](data-factory-functions-variables.md#data-factory-system-variables)합니다. 지원 되는 hello 변수는: **{year}**, **{month}**, **{day}**, **{시간}**, **{분}**, 및 **{사용자 지정}**합니다. 예: inputfolder/{year}/{month}/{day}.

형식에 따라 hello에 폴더를 입력 한다고 가정 합니다.

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Hello 클릭 **찾아보기** 단추에 대 한 **파일 또는 폴더**, 이러한 폴더의 tooone 찾아보기 (2016-03을 > 예를 들어-> 01-02 >)를 클릭 하 고 **선택**합니다. 표시 되어야 `2016/03/01/02` hello 텍스트 상자에 있습니다. 이제 **2016**을 **{year}**로, **03**을 **{month}**로, **01**을 **{day}**로, **02**를 **{hour}**로 바꾸고 탭을 누릅니다. 이러한 네 개의 변수 드롭 다운 목록을 tooselect hello 형식을 표시 되어야 합니다.

![시스템 변수 사용](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

다음 스크린 샷에서 hello와 같이 사용할 수도 있습니다는 **사용자 지정** 변수 프로그램과 [형식 문자열을 지원](https://msdn.microsoft.com/library/8kb3ddd4.aspx)합니다. 해당 구조를 사용 하 여 hello와 폴더 tooselect **찾아보기** 먼저 단추입니다. 그런 다음 사용 하 여 값을 대체 **{사용자 지정}**, 탭 toosee hello 텍스트 상자 hello 형식 문자열을 입력할 수 있는 키를 누릅니다.     

![사용자 지정 변수 사용](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>다양한 데이터 및 개체 유형 지원
Hello 복사 마법사를 사용 하 여 수백 대의 폴더, 파일 또는 테이블을 효율적으로 이동할 수 있습니다.

![Toocopy 데이터에서 테이블을 선택 합니다.](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>일정 옵션
실행할 수 있습니다 hello 복사 작업이 한 번 또는 일정에 따라 (시간별, 일별, 등). 두이 옵션 모두 온-프레미스, 클라우드 및 로컬 데스크톱 복사본 간에 hello 범위의 hello 커넥터에 대해 사용할 수 있습니다.

일회성 복사 작업은 한 번만 원본 tooa 대상에서 데이터를 이동할을 수 있습니다. 모든 크기 및 모든 지원 되는 형식 toodata 적용 됩니다. 예약 된 hello 복사 하면 지정 된 되풀이에 toocopy 데이터 있습니다. 풍부한 설정 (예: 재시도, 제한 시간 및 경고)를 사용할 수 있습니다 tooconfigure hello 복사를 예약 합니다.

![일정 속성](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>다음 단계
Hello 데이터 팩터리 복사 마법사 toocreate 파이프라인을 사용 하 여 복사 작업으로의 간략 한 설명이 참조 하십시오. [자습서: hello 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다.

