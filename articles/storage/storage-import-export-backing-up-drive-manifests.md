---
title: "Azure 가져오기/내보내기 드라이브 매니페스트를 aaaBacking | Microsoft Docs"
description: "어떻게 toohave 드라이브 매니페스트를 자동으로 백업 하는 hello Microsoft Azure 가져오기/내보내기 서비스에 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Azure Import/Export 작업에 대한 드라이브 배니페스트 백업

드라이브 매니페스트 자동으로 백업할 수 tooblobs hello 설정 하 여 `BackupDriveManifest` 속성 너무`true` hello에 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 또는 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API 작업 합니다. 기본적으로 hello 드라이브 매니페스트 백업 되지 않습니다. 드라이브 매니페스트 백업은 hello hello 작업과 연결 된 hello 저장소 계정 내의 컨테이너에 블록 blob으로 저장 됩니다. Hello 컨테이너 이름이 기본적으로 `waimportexport`, hello에 다른 이름을 지정할 수 있지만 `DiagnosticsPath` 속성 hello를 호출할 때 `Put Job` 또는 `Update Job Properties` 작업 합니다. hello 백업 매니페스트 blob에에서 이름이 지정 형식에 따라 hello: `waies/jobname_driveid_timestamp_manifest.xml`합니다.

 Hello hello를 호출 하 여 작업에 대 한 URI hello 백업 드라이브의 매니페스트를 검색할 수 있습니다 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 작업 합니다. hello에 URI가 반환 되는 hello blob `ManifestUri` 각 드라이브에 대 한 속성입니다.

## <a name="next-steps"></a>다음 단계

* [Hello 가져오기/내보내기 서비스 REST API를 사용 하 여](storage-import-export-using-the-rest-api.md)
