---
title: "Azure HDInsight에서 aaaUnderstand 및 해결 WebHCat 오류 | Microsoft Docs"
description: "HDInsight에 WebHCat에 의해 tooabout 일반적인 오류를 반환 하는 방법 및 방법에 대해 알아봅니다 tooresolve 해당 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>HDInsight WebHCat에서 받은 오류 이해 및 해결

Tooresolve WebHCat HDInsight를 사용 하는 시기와 방법을 받은 오류에 대 한 자세한 내용은 해당 합니다. WebHCat는 Visual Studio 용 Azure PowerShell 및 hello 데이터 레이크 도구와 같은 클라이언트 도구에서 내부적으로 사용 됩니다.

## <a name="what-is-webhcat"></a>WebHCat이란?

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat)은 [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog)용 REST API, Hadoop용 테이블 및 저장소 관리 계층입니다. WebHCat HDInsight 클러스터를 기본적으로 사용 하며 다양 한 도구 toosubmit 작업에서 사용 됩니다, 그리고 toohello 클러스터 로그인 하지 않고 등 작업 상태를 가져옵니다.

## <a name="modifying-configuration"></a>구성 수정

> [!IMPORTANT]
> 이 문서에 나열 된 hello 오류 구성된 최대값을 초과 했기 때문에 발생 합니다. Hello 해결 단계에 언급 한 값을 변경할 수 있습니다 때 hello tooperform hello 변경 중 하나를 사용 해야 합니다.

* 에 대 한 **Windows** 클러스터: 클러스터를 만드는 동안 스크립트 동작 tooconfigure hello 값을 사용 합니다. 자세한 내용은 [스크립트 동작 개발](hdinsight-hadoop-script-actions.md)을 참조하세요.

* 에 대 한 **Linux** 클러스터: (웹 또는 REST API) 사용 하 여 Ambari toomodify hello 값입니다. 자세한 내용은 [Ambari를 사용하여 HDInsight 관리](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

### <a name="default-configuration"></a>기본 구성

다음 기본 값에는 hello 초과 된 경우 WebHCat 성능이 저하 될 하거나 오류가 발생할 수 있습니다.

| 설정 | 기능 | 기본값 |
| --- | --- | --- |
| [yarn.scheduler.capacity.maximum-applications][maximum-applications] |최대 동시에 활성화 될 수 있는 작업 수를 hello (보류 중 또는 실행) |10000 |
| [templeton.exec.max-procs][max-procs] |hello 최대 동시에 제공 될 수 있습니다. 있는 요청 수 |20 |
| [mapreduce.jobhistory.max-age-ms][max-age-ms] |작업 기록 하는 일 수 hello 유지 됩니다. |7 일 |

## <a name="too-many-requests"></a>너무 많은 요청

**HTTP 상태 코드**: 429

| 원인 | 해결 방법 |
| --- | --- |
| 기본값인 20 분 당 WebHCat 통해 저장 된 hello 최대 동시 요청을 지났습니다. |사용자 작업 tooensure 하지 제출 보다 최대 동시 요청 수가 hello 또는 않는 수정 하 여 hello 동시 요청 한도 늘릴 줄일 `templeton.exec.max-procs`합니다. 자세한 내용은 [구성 수정](#modifying-configuration)을 참조하세요. |

## <a name="server-unavailable"></a>서버 사용할 수 없음

**HTTP 상태 코드**: 503

| 원인 | 해결 방법 |
| --- | --- |
| 이 상태 코드는 일반적으로 hello 기본 및 보조 간 장애 조치 하는 동안 발생 hello 클러스터 헤드 노드에 |2 분 동안 기다린 후 hello 작업을 다시 시도 |

## <a name="bad-request-content-could-not-find-job"></a>잘못된 요청 콘텐츠: 작업을 찾을 수 없습니다.

**HTTP 상태 코드**: 400

| 원인 | 해결 방법 |
| --- | --- |
| 작업 세부 정보를 정리 된 hello 작업 기록에서 수행 되는 클리너 |작업 기록에 대 한 hello 기본 보존 기간 7 일입니다. hello 기본 보존 기간을 수정 하 여 변경할 수 있습니다 `mapreduce.jobhistory.max-age-ms`합니다. 자세한 내용은 [구성 수정](#modifying-configuration)을 참조하세요. |
| 장애 조치 tooa 인해 작업이 중단 되었고 |Tootwo 분을에 대 한 작업 제출을 다시 시도 하십시오. |
| 잘못된 작업 ID가 사용되었습니다. |작업 id hello 올바른지 확인 하십시오 |

## <a name="bad-gateway"></a>나쁜 게이트웨이

**HTTP 상태 코드**: 502

| 원인 | 해결 방법 |
| --- | --- |
| 내부 가비지 수집이 hello WebHCat 프로세스 내에서 발생 |가비지 컬렉션 toofinish 기다리거나 hello WebHCat 서비스를 다시 시작 |
| Hello ResourceManager 서비스의에서 응답을 기다리는 제한 시간입니다. 활성 응용 프로그램 수가 hello hello 구성 된 최대 (10, 000 기본값)이 되 면이 오류가 발생할 수 있습니다. |현재 작업 toocomplete 실행 또는 수정 하 여 hello 동시 작업 한도 늘릴 `yarn.scheduler.capacity.maximum-applications`합니다. 자세한 내용은 참조 hello [수정 구성](#modifying-configuration) 섹션. |
| Tooretrieve hello 통해 모든 작업을 시도 [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) 호출 하는 동안 `Fields` 너무 설정`*` |*모든* 작업 세부 정보를 검색하지는 마세요. 대신 사용 하 여 `jobid` 만 특정 작업 id 보다 큰 작업에 대 한 tooretrieve 세부 정보입니다. 또는 `Fields`를 사용하지 마십시오. |
| 헤드 노드에 장애 조치 중 다운 hello WebHCat 서비스는 |2 분 동안 기다렸다가 hello 작업을 다시 시도 |
| WebHCat을 통해 전송되는 500개 이상의 보류 중인 작업이 있습니다. |더 많은 작업을 제출하기 전에 현재 보류 중인 작업이 완료될 때까지 대기합니다. |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
