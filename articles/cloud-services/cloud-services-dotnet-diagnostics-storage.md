---
title: "aaaStore 및 Azure 저장소에 진단 데이터 보기 | Microsoft Docs"
description: "Azure 저장소로 Azure 진단 데이터를 가져오고 보기"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Azure 저장소에서 진단 데이터 저장 및 보기
Toohello Microsoft Azure 저장소 에뮬레이터 또는 tooAzure 저장소 전송 하지 않는 한 진단 데이터는 영구적으로 저장 되지 않습니다. 저장소에서 사용할 수 있는 여러 도구 중 하나로 한 번 볼 수 있습니다.

## <a name="specify-a-storage-account"></a>저장소 계정 지정
Toouse hello ServiceConfiguration.cscfg 파일에 지정 하는 hello 저장소 계정을 지정 합니다. hello 계정 정보는 구성 설정에 대 한 연결 문자열로 정의 됩니다. hello 다음 예제는 Visual Studio에서 새 클라우드 서비스 프로젝트에 대해 만든 hello 기본 연결 문자열.

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

Azure 저장소 계정에 대 한이 연결 문자열 tooprovide 계정 정보를 변경할 수 있습니다.

수집 되 고 진단 데이터의 hello 형식에 따라 Azure 진단 hello Blob 서비스 또는 hello 테이블 서비스를 사용 합니다. hello 다음 표에서 지속 hello 데이터 원본 및 해당 형식입니다.

| 데이터 원본 | 저장소 형식 |
| --- | --- |
| Azure 로그 |테이블 |
| IIS 7.0 로그 |Blob |
| Azure 진단 인프라 로그 |테이블 |
| 실패한 요청 추적 로그 |Blob |
| Windows 이벤트 로그 |테이블 |
| 성능 카운터 |테이블 |
| 크래시 덤프 |Blob |
| 사용자 지정 오류 로그 |Blob |

## <a name="transfer-diagnostic-data"></a>진단 데이터 전송
SDK 2.5 이상 버전에서는 hello 요청 tootransfer 진단 데이터는 hello 구성 파일을 통해 발생할 수 있습니다. Hello 구성에 지정 된 예약 된 간격으로 진단 데이터를 전송할 수 있습니다.

SDK 2.4 및 이전 프로그래밍 방식 tootransfer hello에 대 한 진단 데이터도 hello 구성 파일을 통해 요청할 수 있습니다. hello 프로그래밍 방식을 toodo 주문형 전송을 허용 합니다.

> [!IMPORTANT]
> 진단 데이터 tooan Azure 저장소 계정으로 전송할 경우 진단 데이터가 사용 하는 hello 저장소 리소스에 대 한 비용이 발생 합니다.
> 
> 

## <a name="store-diagnostic-data"></a>진단 데이터 저장
로그 데이터는 이름 다음 hello로 Blob 또는 테이블 저장소에 저장 됩니다.

**테이블**

* **WadLogsTable** -hello 추적 수신기를 사용 하 여 코드를 작성 한 로그입니다.
* **WADDiagnosticInfrastructureLogsTable** - 진단 모니터 및 구성 변경 내용입니다.
* **WADDirectoriesTable** – 디렉터리 해당 hello 진단 모니터는 모니터링 합니다.  IIS 로그, IIS 실패한 요청 로그 및 사용자 지정 디렉터리를 포함합니다.  hello blob 로그 파일의 위치 hello hello Container 필드에 지정 된 및 hello hello blob 이름이 hello RelativePath 필드에 있습니다.  hello AbsolutePath 필드 hello Azure 가상 컴퓨터에 hello 파일의 이름과 hello 위치를 나타냅니다.
* **WADPerformanceCountersTable** – 성능 카운터입니다.
* **WADWindowsEventLogsTable** – Windows 이벤트 로그입니다.

**Blob**

* **wad 컨트롤 컨테이너** – (SDK 2.4 및 이전) hello Azure 진단을 제어 하는 hello XML 구성 파일이 포함 되어 있습니다.
* **wad-iis-failedreqlogfiles** – IIS 실패한 요청 로그에서 정보를 포함합니다.
* **wad-iis-logfiles** – IIS 로그에 관한 정보를 포함합니다.
* **"custom"** – hello 진단 모니터에 의해 모니터링 되는 디렉터리를 구성 하는 방법에 따라 사용자 지정 컨테이너입니다.  이 blob 컨테이너의 hello 이름은 WADDirectoriesTable에 지정 됩니다.

## <a name="tools-tooview-diagnostic-data"></a>도구 tooview 진단 데이터
여러 가지 도구는 전송된 toostorage 올바르게 설치 후 사용 가능한 tooview hello 데이터입니다. 예:

* Visual Studio-서버 탐색기 hello Azure 도구 for Microsoft Visual Studio를 설치 하는 경우 사용할 수 있습니다 hello Azure 저장소 노드 서버 탐색기 tooview 읽기 전용 blob 및 테이블 데이터의 Azure 저장소 계정에서. 로컬 저장소 에뮬레이터 계정 및 Azure용으로 만든 저장소 계정에서 데이터를 표시할 수 있습니다. 자세한 내용은 [서버 탐색기로 저장소 리소스 탐색 및 관리](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md)를 참조하세요.
* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) 는 Windows, OSX 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있도록 하는 독립 실행형 앱입니다.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) tooview, 수 있는 Azure 진단 관리자를 포함 합니다. 다운로드 하 고 Azure에서 실행 되는 hello 응용 프로그램에서 수집한 hello 진단 데이터를 관리 합니다.

## <a name="next-steps"></a>다음 단계
[Azure 진단으로 클라우드 서비스 응용 프로그램에서 추적 hello 흐름](cloud-services-dotnet-diagnostics-trace-flow.md)

