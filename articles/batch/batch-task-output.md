---
title: "로그 나 aaaPersist 결과 완료 작업 및 작업 tooa 데이터 저장소-Azure 일괄 처리 | Microsoft Docs"
description: "Batch 작업 및 태스크의 출력 데이터를 유지하기 위한 다양한 옵션을 알아봅니다. 데이터 저장소, tooAzure 또는 tooanother 데이터를 유지할 수를 저장 합니다."
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>작업 및 태스크 출력 유지

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

태스크 출력의 일반적인 예는 다음과 같습니다.

- 입력 데이터를 hello 작업 프로세스 때 만든 파일입니다.
- 태스크 실행과 관련된 로그 파일 

이 문서에서는 각 옵션은 가장 적합 한 지속 작업 출력과 hello 시나리오에 대 한 다양 한 옵션을 설명 합니다.   

## <a name="about-hello-batch-file-conventions-standard"></a>Hello 일괄 처리 파일 규칙 표준 정보

Batch는 Azure Storage에서 태스크 출력 파일의 이름을 지정하기 위한 선택적인 규칙 집합을 정의합니다. hello [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) 이러한 규칙을 설명 합니다. hello 파일 규칙 표준 hello 대상 컨테이너 및 blob 저장소의 경로 Azure hello hello 작업 및 작업 이름을 사용 하 여 지정 된 출력 파일에 대 한 hello 이름을 결정 합니다.

가 tooyou toouse hello 출력 데이터 파일 이름 지정에 대 한 표준 파일 규칙 있는지 여부를 결정 합니다. Hello 대상 컨테이너 및 blob 원하는 이름을 지정할 수도 있습니다. Hello 표준 파일 규칙을 사용 하 여 출력 파일 이름 지정에 대 한 않는 경우 출력 파일이 있는 hello에 표시할 수 있는 [Azure 포털][portal]합니다.

hello 파일 규칙 standard를 사용할 수 있는 몇 가지가 있습니다.

- Hello 일괄 처리 서비스 API toopersist 출력 파일을 사용 하는 경우 tooname 대상 컨테이너 및 blob toohello 표준 파일 규칙에 따라 선택할 수 있습니다. hello 일괄 처리 서비스 API를 사용 하면 클라이언트 코드에서 toopersist 출력 파일 작업 응용 프로그램을 수정 하지 않고 있습니다.
- .NET을 개발 하는 경우에 hello을 사용할 수 있습니다 [.NET 용 Azure 배치 파일 규칙 라이브러리][nuget_package]합니다. 이 라이브러리를 사용 하는 경우의 이점은 tootheir ID 나 목적에 따라 출력 파일이 쿼리 지원 한다는 점입니다. 클라이언트 응용 프로그램 또는 다른 작업에서 출력 파일을 쉽게 tooaccess hello 기본 제공 쿼리 기능이 있습니다. 그러나 작업 응용 프로그램 수정된 toocall 파일 규칙 라이브러리 여야 합니다. 자세한 내용은 참조 hello에 대 한 hello 참조 [.NET 용 라이브러리 파일 규칙](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx)합니다.
- .NET 이외의 다른 언어로 개발 하는 경우에 hello 응용 프로그램의 표준 파일 규칙을 구현할 수 있습니다.

## <a name="design-considerations-for-persisting-output"></a>출력 유지 설계 시 고려 사항 

일괄 처리 솔루션을 설계할 때는 hello 다음 관련된 toojob 요소 및 작업 출력이 것이 좋습니다.

* **계산 노드 수명**: 계산 노드는 특히 자동 크기 조정 가능한 풀에서 일시적인 경우가 많습니다. 노드에서 실행 되는 작업 출력은 hello 노드가 있으며 hello 작업에 대해 설정한 hello 파일 보존 기간 내 에서만 동안에 사용할 수입니다. Hello 작업이 완료 되 면 필요할 수 있는 출력을 생성 하는 작업을 하는 경우 해당 출력 파일 tooa 영 속 저장소 Azure 저장소와 같은 hello 작업에 업로드 해야 합니다.

* **출력 저장소**: Azure Storage는 태스크 출력을 위한 데이터 저장소로 권장되지만 모든 영구 저장소를 사용할 수 있습니다. 작업 출력 tooAzure 작성 저장소 hello 일괄 처리 서비스 API에 통합 됩니다. 지 속성 저장소의 또 다른 형태를 사용 하는 경우에 사용자가 직접 toowrite hello 응용 프로그램 논리 toopersist 작업 출력이 필요 합니다.   

* **검색 출력**: 작업 출력을 유지 하는 경우 풀의 hello 계산 노드 또는 Azure 저장소 서비스 또는 다른 데이터 저장소에서 직접 작업 출력 검색할 수 있습니다. tooretrieve 작업 계산 노드에에서 직접 출력 hello 파일 이름과 hello 노드에서 출력 위치 해야 합니다. 작업 출력 tooAzure 저장소를 유지 하는 경우 Azure 저장소 SDK hello로 Azure 저장소 toodownload hello 출력 파일의 hello 전체 경로 toohello 파일이 필요 하면 합니다.

* **출력 보기**: hello Azure 포털 및 선택에서 tooa 일괄 처리 작업을 이동할 때 **노드 상의 파일**, hello 작업과 관련 된 모든 파일 표시 됩니다, 뿐 아니라 출력 파일에 관심이 hello 합니다. 다시 계산 노드에서 파일을 hello 노드가 있으며 hello 작업에 대해 설정한 파일 보존 시간 hello 내 에서만 동안에 사용할 수 있습니다. tooview 작업 출력 tooAzure 저장소를 유지 한, Azure 포털 hello 또는 hello 같은 Azure 저장소 클라이언트 응용 프로그램을 사용할 수 있습니다 [Azure 저장소 탐색기][storage_explorer]합니다. tooview hello 포털 또는 다른 도구를 사용 하 여 Azure 저장소의 데이터 출력, hello 파일의 위치를 알아야 하 고 tooit 직접 이동 해야 합니다.

## <a name="options-for-persisting-output"></a>출력 유지 옵션

시나리오에 따라 가지 toopersist 작업 출력을 수행할 수 있는 몇 가지 다른 방법이 있습니다.

- Hello 일괄 처리 서비스 API를 사용 합니다.  
- .NET 용 hello 일괄 처리 파일 규칙 라이브러리를 사용 합니다.  
- Hello 표준 응용 프로그램에서 배치 파일 규칙을 구현 합니다.
- 사용자 지정 파일 이동 솔루션을 구현합니다.

hello 다음 섹션에서 자세히 각 방법에 설명 합니다.

### <a name="use-hello-batch-service-api"></a>Hello 일괄 처리 서비스 API를 사용 하 여

2017-05-01 버전 hello 일괄 처리 서비스는 작업 데이터에 대 한 Azure 저장소에 출력 파일을 지정 하는 것에 대 한 지원 추가 때 있습니다 [작업 tooa 작업에 추가할](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) 또는 [작업 tooa 작업의 컬렉션을 추가할](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job)합니다.

일괄 처리 서비스 API hello 지속 작업 데이터 tooan hello 가상 컴퓨터 구성을 사용 하 여 만든 풀에서 Azure 저장소 계정을 지원 합니다. 일괄 처리 서비스 API hello로 작업을 실행 하는 hello 응용 프로그램을 수정 하지 않고 작업 데이터를 유지할 수 있습니다. Toohello 준수 필요에 따라 수 [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) tooAzure 저장소를 유지 하는 hello 파일 명명 합니다. 

일괄 처리 서비스 API hello toopersist 작업 경우 출력을 사용 합니다.

- Toopersist 데이터 일괄 처리 작업 및 가상 컴퓨터 구성 hello 사용 하 여 만든 풀의 작업 관리자 태스크를 사용 하는 것이 좋습니다.
- Toopersist 데이터 tooan Azure 저장소 컨테이너는 임의의 이름으로 사용 하는 것이 좋습니다.
- 원하는 toopersist 데이터 tooan Azure 저장소 컨테이너에 따라 toohello 라는 [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)합니다. 

> [!NOTE]
> 일괄 처리 서비스 API hello hello 클라우드 서비스 구성을 사용 하 여 만든 풀에서 실행 되는 작업에서 데이터 유지를 지원 하지 않습니다. Hello 클라우드 서비스 구성을 실행 하는 풀에서 출력 지속 작업에 대 한 정보를 참조 하세요. [작업 및 작업 데이터 tooAzure 저장소.NET toopersist에 대 한 hello 일괄 처리 파일 규칙 라이브러리와 함께 유지](batch-task-output-file-conventions.md)
> 
> 

Hello 일괄 처리 서비스 API 사용 하 여 지속 작업 출력에 대 한 자세한 내용은 참조 하십시오. [hello 일괄 처리 서비스 API로 작업 데이터 tooAzure 저장소 유지](batch-task-output-files.md)합니다. 또한 hello를 참조 하십시오. [PersistOutputs] [github_persistoutputs] 샘플.NET toopersist 작업에 대 한 toouse hello 배치 클라이언트 라이브러리 toodurable 저장소를 출력 하는 방법을 보여 주는 GitHub에 대 한 프로젝트입니다.

### <a name="use-hello-batch-file-conventions-library-for-net"></a>.NET 용 hello 일괄 처리 파일 규칙 라이브러리를 사용 합니다.

C# 및.NET으로 일괄 처리 솔루션을 제작 하는 개발자 hello를 사용 하 여 [.NET 용 라이브러리 파일 규칙] [ nuget_package] toopersist 작업 데이터 tooan Azure 저장소 계정에 따라 toohello [배치 파일 표준 규칙](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)합니다. hello 파일 규칙 라이브러리 이동 출력 파일 tooAzure 저장소 명명 대상 컨테이너 및 blob는 잘 알려진 방법으로 처리합니다.

hello 파일 규칙 라이브러리 출력 파일 ID 또는 목적으로 쿼리를 지원 hello 필요 없이 해당 파일 Uri 완료 쉽게 toolocate 수행 합니다. 

.NET toopersist 작업 경우 출력에 대 한 hello 일괄 처리 파일 규칙 라이브러리를 사용 합니다.

- 원하는 toostream 데이터 tooAzure 저장소 hello 작업 실행 중입니다.
- Toopersist 데이터 hello 클라우드 서비스 구성 또는 hello 가상 컴퓨터 구성 중 하나를 사용 하 여 만든 풀에서 사용 하는 것이 좋습니다.
- 클라이언트 응용 프로그램 또는 hello의 다른 작업이 요구 toolocate 작업 하 고 ID 또는 용도 따라 작업 출력 파일을 다운로드 합니다. 
- 원하는 초기 결과의 tooperform-검사점 하거나 초기 업로드 합니다.
- Tooview 작업 출력을 hello Azure 포털에서에서 사용 하는 것이 좋습니다.

.NET 용 hello 파일 규칙 라이브러리와 함께 지속 작업 출력에 자세한 내용은 참조 [작업 및 작업 데이터 tooAzure 저장소.NET toopersist에 대 한 hello 일괄 처리 파일 규칙 라이브러리와 유지 ](batch-task-output-file-conventions.md)합니다. 또한 hello를 참조 하십시오. [PersistOutputs] [github_persistoutputs] 샘플.NET toopersist 작업에 대 한 toouse hello 파일 규칙 라이브러리 toodurable 저장소를 출력 하는 방법을 보여 주는 GitHub에서 프로젝트.

hello GitHub에서 [PersistOutputs] [github_persistoutputs] 샘플 프로젝트에서는.NET toopersist 작업에 대 한 toouse hello 배치 클라이언트 라이브러리 toodurable 저장소를 출력 하는 방법

### <a name="implement-hello-batch-file-conventions-standard"></a>Hello 표준 일괄 처리 파일 규칙을 구현 합니다.

다른.NET 언어를 사용 하는 경우에 hello을 구현할 수 있습니다 [일괄 처리 파일 규칙 표준](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) 사용자 응용 프로그램에서 합니다. 

좋습니다 tooimplement hello 파일 규칙 이름 지정 표준을 직접 검증 된 이름 지정 체계를 이동 하거나 hello Azure 포털에서에서 tooview 작업 출력 하려는 경우.

### <a name="implement-a-custom-file-movement-solution"></a>사용자 지정 파일 이동 솔루션 구현

사용자 고유의 완벽한 파일 이동 솔루션도 구현할 수 있습니다. 다음과 같은 경우에는 이 방법을 사용합니다.

- Azure 저장소 이외의 toopersist 작업 데이터 tooa 데이터 저장소를 사용 하는 것이 좋습니다. 파일 tooa 데이터 저장소와 같은 SQL Azure 또는 Azure DataLake tooupload 하 고, 사용자 지정 스크립트 또는 실행 tooupload toothat 위치를 만들 수 있습니다. 또한 주 실행 파일을 실행 한 후 hello 명령줄에서 호출 후 합니다. 예를 들어 Windows 노드에서 두 명령(`doMyWork.exe && uploadMyFilesToSql.exe`)을 호출할 수 있습니다.
- 원하는 초기 결과의 tooperform-검사점 하거나 초기 업로드 합니다.
- 원하는 toomaintain 오류 처리 세부적으로 제어 합니다. 예를 들어 사용자 고유의 솔루션을 원하는 toouse 작업 종속성 동작 tootake 특정 경우 특정 작업 종료 코드에 따라 작업 업로드 tooimplement을 좋습니다. 작업 종속성 작업에 대 한 자세한 내용은 참조 하십시오. [다른 작업에 종속 된 toorun 작업 작업 종속성을 만들고](batch-task-dependencies.md)합니다. 

## <a name="next-steps"></a>다음 단계

- 일괄 처리 서비스 API hello toopersist 작업 데이터의 hello 새로운 기능을 사용 하 여 탐색 [hello 일괄 처리 서비스 API로 작업 데이터 tooAzure 저장소 유지](batch-task-output-files.md)합니다.
- Hello 일괄 처리 파일 규칙 라이브러리를 사용 하 여.NET에 대 한 알아봅니다 [작업 및 작업 데이터 tooAzure 저장소.NET toopersist에 대 한 hello 일괄 처리 파일 규칙 라이브러리와 유지 ](batch-task-output-file-conventions.md)합니다.
- Hello [PersistOutputs] [github_persistoutputs] 참조 github 방법을 toouse 둘 다 hello 일괄 처리.NET 클라이언트 라이브러리 및.NET toopersist 작업에 대 한 hello 파일 규칙 라이브러리 보여 주는 샘플 프로젝트 toodurable 저장소를 출력 합니다.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
