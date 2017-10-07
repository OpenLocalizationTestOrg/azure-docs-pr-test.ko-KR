---
title: "aaa \"Azure 배치 계산 노드 환경 변수 | \"Microsoft Docs"
description: "Azure Batch 분석에 대한 계산 노드 환경 변수 참조입니다."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Azure Batch 계산 노드 환경 변수
hello [Azure 배치 서비스](https://azure.microsoft.com/services/batch/) hello 계산 노드에서 환경 변수를 다음을 설정 합니다. Hello 명령줄에서 스크립트 실행 및 hello 프로그램 및 명령줄 작업에에서 이러한 환경 변수를 참조할 수 있습니다.

Batch에 환경 변수를 사용하는 방법에 대한 자세한 내용은 [태스크에 대한 환경 설정](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks)을 참조하세요.

## <a name="environment-variable-visibility"></a>환경 변수 이름 표시

이러한 환경 변수는 hello의 hello 컨텍스트에서만에서 표시 **작업 사용자**, hello hello 노드의 작업이 실행 되는 사용자 계정입니다. 수행 합니다 *하지* 경우 이러한 참조 하면 [원격으로 연결](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa 프로토콜 RDP (원격 데스크톱) 또는 SSH (보안 셸) 및 목록 hello 환경 변수를 통해 노드를 계산 합니다. 때문에 이것이 hello 사용자 계정이 원격 연결에 사용 되는 hello 하지는 hello 작업에서 사용 되는 hello 계정와 동일 합니다.

## <a name="command-line-expansion-of-environment-variables"></a>환경 변수의 명령줄 확장

hello 명령줄 작업에 의해 실행 계산 노드는는 shell에서 실행 되지 않습니다. 따라서 이러한 명령줄 활용할 수 없습니다 기본적으로 환경 변수 확장 등의 셸 기능 (여기에 hello `PATH`). tootake 이점은 이러한 기능을 수행 해야 **hello 셸 호출** hello 명령줄에서. 예를 들어 Windows 계산 노드에서 `cmd.exe`를 실행하거나 Linux 노드에서 `/bin/sh`를 실행합니다.

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>환경 변수

| 변수 이름                     | 설명                                                              | Availability | 예제 |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | hello 이름 작업 hello hello 일괄 처리 계정에 속해 있습니다.                  | 모든 태스크입니다.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Hello 내 디렉터리 [작업 작업 디렉터리] [ files_dirs] Linux에 대 한 저장 된 인증서에 노드를 계산 합니다. 참고가 환경 변수 tooWindows 계산 노드 적용 되지 않습니다.                                                  | 모든 태스크입니다.   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | 작업 hello hello 작업의 hello ID에 속해 있습니다. | 시작 태스크를 제외한 모든 태스크입니다. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | hello 작업 준비의 전체 경로 hello [작업 디렉터리] [ files_dirs] hello 노드에서 합니다. | 시작 태스크 및 작업 준비 태스크를 제외한 모든 태스크입니다. Hello 작업은 작업 준비 작업으로 구성 하는 경우에 사용할 수 있습니다. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | hello 작업 준비의 전체 경로 hello [작업 작업 디렉터리] [ files_dirs] hello 노드에서 합니다. | 시작 태스크 및 작업 준비 태스크를 제외한 모든 태스크입니다. Hello 작업은 작업 준비 작업으로 구성 하는 경우에 사용할 수 있습니다. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | 작업 hello hello 노드의 hello ID에 할당 됩니다. | 모든 태스크입니다. | tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | 모든 hello 루트의 전체 경로 hello [디렉터리 일괄] [ files_dirs] hello 노드에서 합니다. | 모든 태스크입니다. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | hello의 전체 경로 hello [공유 디렉터리] [ files_dirs] hello 노드에서 합니다. 노드에서 실행 되는 모든 작업에는 읽기/쓰기 액세스 toothis 디렉터리가 있어야 합니다. 다른 노드에서 실행 되는 작업에 원격 액세스 toothis 디렉터리 (이 "공유" 네트워크 디렉터리)를 사용할 필요가 없습니다. | 모든 태스크입니다. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | hello의 전체 경로 hello [작업 디렉터리를 시작] [ files_dirs] hello 노드에서 합니다. | 모든 태스크입니다. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | 작업 hello는 hello 풀의 hello ID에서 실행 됩니다. | 모든 태스크입니다. | batchpool001 |
| AZ_BATCH_TASK_DIR               | hello의 전체 경로 hello [작업 디렉터리] [ files_dirs] hello 노드에서 합니다. 이 디렉터리에 hello `stdout.txt` 및 `stderr.txt` hello 작업 및 AZ_BATCH_TASK_WORKING_DIR hello에 대 한 합니다. | 모든 태스크입니다. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | hello 현재 작업의 hello ID입니다. | 시작 태스크를 제외한 모든 태스크입니다. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | hello의 전체 경로 hello [작업 작업 디렉터리] [ files_dirs] hello 노드에서 합니다. 현재 작업을 실행 하는 hello에 읽기/쓰기 액세스 toothis 디렉터리가 있습니다. | 모든 태스크입니다. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | 노드 및 노드당 tooa 할당 된 코어 수의 hello 목록 [다중 인스턴스 작업][multi_instance]합니다. 노드 및 코어 hello 형식으로 나열 됩니다.`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`여기서 hello 노드 수가 뒤에 하나 이상의 노드 IP 주소와 hello 코어 수가 각각에 대 한 합니다. |  다중 인스턴스 기본 및 하위 태스크입니다. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | hello tooa 할당 되는 노드 목록을 [다중 인스턴스 작업] [ multi_instance] hello 형태로 표시 `nodeIP;nodeIP`합니다. | 다중 인스턴스 기본 및 하위 태스크입니다. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | hello tooa 할당 되는 노드 목록을 [다중 인스턴스 작업] [ multi_instance] hello 형태로 표시 `nodeIP,nodeIP`합니다. | 다중 인스턴스 기본 및 하위 태스크입니다. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | hello hello의 IP 주소와 포트 계산 노드는 hello 주 작업의 한 [다중 인스턴스 작업] [ multi_instance] 실행 합니다. | 다중 인스턴스 기본 및 하위 태스크입니다. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Hello 기본 작업 및의 모든 하위 작업에 대 한 동일한 디렉터리 경로 [다중 인스턴스 작업][multi_instance]합니다. hello 경로에 hello 다중 인스턴스 작업 실행 되는의 모든 노드에 있으며 읽기/쓰기 액세스할 수 있는 toohello 작업 명령을 해당 노드에서 실행 중 (두 hello [조정 명령] [ coord_cmd] 및 hello [응용 프로그램 명령][app_cmd]). 하위 또는 다른 노드에서 실행 되는 기본 작업 (이 "공유" 네트워크 디렉터리) toothis 디렉터리에 원격 액세스를 갖지 않습니다. | 다중 인스턴스 기본 및 하위 태스크입니다. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | 현재 노드가 hello에 대 한 hello 마스터 노드 인지를 지정 된 [다중 인스턴스 작업][multi_instance]합니다. 가능한 값은 `true` 및 `false`입니다.| 다중 인스턴스 기본 및 하위 태스크입니다. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | 경우 `true`, hello 현재 노드는 전용된 노드입니다. `false`의 경우 [우선 순위가 낮은 노드](batch-low-pri-vms.md)입니다. | 모든 태스크입니다. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
