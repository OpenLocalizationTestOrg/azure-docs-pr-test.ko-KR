---
title: "Azure 가져오기/내보내기 서비스 REST API aaaUsing hello | Microsoft Docs"
description: "Azure 가져오기/내보내기 hello를 사용 하기 위한 toofind 리소스 REST API를 모두 방법 tooand 참조 자료를 포함 하 여 서비스 위치에 대해 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>Hello Azure 가져오기/내보내기 서비스 REST API를 사용 하 여

hello Microsoft Azure 가져오기/내보내기 서비스는 가져오기/내보내기 작업의 REST API tooenable 프로그래밍 방식 제어를 제공합니다. Hello REST API tooperform hello의 모든 가져오기/내보내기 hello로 수행할 수 있는 작업을 사용할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다. 또한 REST API tooperform hello hello hello Azure 클래식 포털에서에서 현재 사용할 수 없는 작업의 완료 백분율 쿼리와 같은 특정 세부 작업을 사용할 수 있습니다.

참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md) hello 가져오기/내보내기 서비스 및 toouse 클래식 포털 toocreate hello 하 및 가져오기를 관리 하는 방법을 보여 주는 자습서에 대 한 개요 작업 및 내보내기 작업 합니다.

## <a name="service-endpoints"></a>서비스 끝점

hello Azure 가져오기/내보내기 서비스는 Azure 리소스 관리자 리소스 공급자 고 hello 가져오기/내보내기 작업을 관리 하기 위한 HTTPS 끝점 뒤에 일련의 REST Api를 제공 합니다.

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>버전 관리

Toohello 가져오기/내보내기 서비스는 hello를 지정 해야 하는 요청 `api-version` 매개 변수 값을 너무 설정`2016-11-01`합니다.

## <a name="importexport-service-operations"></a>Import/Export 서비스 작업

[가져오기 작업 만들기](../storage-import-export-creating-an-import-job.md)

[내보내기 작업 만들기](../storage-import-export-creating-an-export-job.md)

[작업에 대한 상태 정보 검색](storage-import-export-retrieving-state-info-for-a-job.md)

[작업 열거](../storage-import-export-enumerating-jobs.md)

[작업 취소 및 삭제](storage-import-export-cancelling-and-deleting-jobs.md)

[드라이브 매니페스트 백업](../storage-import-export-backing-up-drive-manifests.md)

[가져오기/내보내기 작업에 대한 진단 및 오류 복구](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>다음 단계

* [저장소 Import/Export REST](/rest/api/storageimportexport)
