---
title: "Azure 배치 aaaRun (미리 보기) 코드를 작성 하지 않고도 종단 간 작업 | Microsoft Docs"
description: "Hello Azure CLI toocreate 일괄 처리 풀, 작업 및 작업에 대 한 템플릿 파일을 생성 합니다."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Azure Batch CLI 템플릿 및 파일 전송 사용(미리 보기)

Hello Azure CLI를 사용 하는 코드를 작성 하지 않고 가능한 toorun 일괄 처리 작업

템플릿 파일을 만들고 일괄 처리 풀, 작업 및 작업 toobe 생성을 허용 하는 Azure CLI hello로 사용 되는 사용할 수 있는 합니다. 작업 입력된 파일 hello 배치 계정과 작업이 출력 파일 다운로드와 관련 된 hello 저장소 계정에 쉽게 업로드할 수 있습니다.

## <a name="overview"></a>개요

확장 toohello Azure CLI 일괄 처리 사용 toobe에 종단 간 개발자가 아닌 사용자가을 수 있습니다. 풀을 만들 수 있으며, 입력된 데이터 업로드 작업 및 기타 관련된 작업을 만든 및 hello 결과 출력 데이터-다운로드 한 필수, 코드가 없는 hello CLI 직접 사용 되는 또는 스크립트에 통합 되 고 있습니다.

일괄 처리 템플릿 hello를 토대로 [hello Azure CLI의에서 기존 배치 지원을](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) JSON 파일 hello 생성 풀, 작업, 작업 및 기타 항목에 대 한 toospecify 속성 값을 허용 하는 합니다. 일괄 처리 템플릿으로 hello 다음과 같은 기능이 추가 되었습니다 hello JSON 파일으로 가능한를 통해.

-   매개 변수를 정의할 수 있습니다. Hello 서식 파일 사용 되는 경우 hello 매개 변수 값만 hello 템플릿 본문에 지정 된 다른 항목 속성 값으로 지정 된 toocreate hello 항목을 합니다. 사용자 일괄 처리에 의해 실행 된 일괄 처리 및 응용 프로그램 toobe 이해 하는 풀, 작업 및 작업 속성 값을 지정 템플릿을 만들 수 있습니다. 작은 일괄 처리 및/또는 응용 프로그램에 익숙한 사용자는 정의 된 hello 매개 변수에 대 한 toospecify hello 값만 필요합니다.

-   작업 작업 팩터리 하나 만들거나 더 많은 작업 hello를 방지 하는 작업과 연결 된 많은 만든 작업 정의 toobe 및 크게 간소화 하기 위해 작업 제출에 필요 합니다.


입력된 데이터 파일에는 작업에 대 한 제공 된 toobe 필요 하 고 출력 데이터 파일은 종종 발생 했습니다. 기본적으로 저장소 계정을 연결 된, 각 일괄 처리 계정 및 파일 수 코딩이와 CLI를 사용 하 여이 저장소 계정에서 쉽게 전송된 tooand 있으며 저장소 자격 증명 없이 필요 합니다.

예를 들어 [ffmpeg](http://ffmpeg.org/)는 오디오 및 비디오 파일을 처리하는 인기 있는 응용 프로그램입니다. Azure 일괄 처리 CLI hello 사용된 tooinvoke ffmpeg tootranscode 원본 비디오 파일 toodifferent 해결 될 수 있습니다.

-   풀 템플릿을 만들었습니다. hello 서식 파일을 만드는 hello 사용자 ffmpeg 응용 프로그램 및 요구 사항; toocall hello 하는 방법을 알고 있는 hello 지정 적절 한 운영 체제, VM 크기 (응용 프로그램 패키지 또는 패키지 관리자를 사용 하 여 예를 들어)에서 설치 및 기타 ffmpeg 어떤가요 풀 속성 값입니다. 매개 변수가 있으므로 hello 풀 id와 Vm의 수만 지정 toobe 필요 hello 서식 파일 사용 될 때 만들어집니다.

-   작업 템플릿을 만들었습니다. hello 사용자 만드는 hello 템플릿 ffmpeg 요구 toobe tootranscode 원본 비디오 tooa 다른 해상도 호출 하 고 hello 작업 명령줄;을 지정 하는 방법을 알고 있는 알고는 hello 원본 비디오 파일, 입력된 파일 당 필요한 작업에 포함 된 폴더입니다.

-   비디오 파일 tootranscode 집합이 있는 최종 사용자는 먼저 hello 풀 템플릿을 사용 하 여만 hello 풀 id와 필요한 Vm 수를 지정 하는 풀을 만듭니다. Hello 소스 파일 tootranscode를 업로드할 수 있습니다. Hello 풀 id 및 업로드 하는 hello 소스 파일의 위치 지정 hello 작업 서식 파일을 사용 하 여 작업을 제출할 수 있습니다. hello 일괄 처리 작업이 생성 되 고 입력된 파일 당 하나의 작업으로 생성 되었습니다. 마지막으로, hello 코드 변환 된 출력 파일 다운로드 수 있습니다.

## <a name="installation"></a>설치

hello 템플릿 및 파일 전송 기능을 설치 하는 확장 toobe 사용 하려면.

Tooinstall hello Azure CLI 확인 하는 방법에 대 한 지침은 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.

한 번 hello Azure CLI 설치가 완료 된 후 hello 일괄 처리 된 다음 CLI 명령을 사용 하 여 확장을 설치할 수 있습니다.

```azurecli
az component update --add batch-extensions --allow-third-party
```

Hello 일괄 처리 확장 프로그램에 대 한 자세한 내용은 참조 [Microsoft Azure 일괄 처리 CLI 확장에 대 한 Windows, Mac 및 Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux)합니다.

## <a name="templates"></a>템플릿

Azure 일괄 처리 CLI hello 풀, 작업 및 속성 이름 및 값을 포함 하는 JSON 파일을 지정 하 여 만든 작업 toobe 등의 항목 수 있습니다. 예:

```azurecli
az batch pool create –-json-file AppPool.json
```

Azure 일괄 처리 템플릿은 기능과 구문에 비슷한 tooAzure 리소스 관리자 템플릿이 있습니다. 항목 속성 이름 및 값을 포함 하지만 다음 주요 개념과 hello를 추가 하는 JSON 파일 됩니다.

-   **매개 변수**

    -   매개 변수 값만 필요한 toobe hello 서식 파일을 사용 하는 경우 제공 된 본문 섹션에 지정 된 속성 값 toobe를 허용 합니다. 예를 들어 hello 본문 및 풀 id;에 대해 정의 된 매개 변수가 하나만 hello 풀에 대 한 완료 정의 배치할 수 있습니다. 풀 id 문자열을만 따라서 toobe 제공 toocreate 풀이 필요합니다.
        
    -   hello 템플릿 본문 일괄 처리에 대 한 지식이 있는 사용자가 작성 될 수 있습니다 및 hello 응용 프로그램 toobe; 일괄 처리에 의해 실행 hello 서식 파일을 사용 하는 경우에 매개 변수 작성자 정의 hello에 대 한 값만 제공 되어야 합니다. 사용 하지 않는 사용자 hello 깊이 있는 일괄 처리 및/또는 응용 프로그램 기술 따라서 서식 파일을 사용할 수 있습니다.

-   **변수**

    -   간단 하거나 복잡 한 매개 변수 값 toobe 한 곳에서 지정 하 고 hello 템플릿 본문의 하나 이상의 위치에서 사용을 허용 합니다. 변수 수 단순화 및 hello 서식 파일의 hello 크기를 줄이려면으로 더 쉽게 유지 관리할 위치 toochange 속성 값이 변경 될 수 있습니다 하나 있는 것으로 확인 합니다.

-   **더 높은 수준의 구문**

    -   일부 높은 수준의 구문 아직 hello 배치 Api에서에서 제공 되지 않는 hello 서식 파일에 표시 됩니다. 예를 들어 작업 서식 파일을 만드는 일반적인 작업 정의 사용 하 여 hello 작업에 대 한 여러 작업에서 작업 팩터리를 정의할 수 있습니다. 이러한 구문으로 동적으로 같은 작업을 마다 한 파일씩 여러 JSON 파일을 만드는 예를 들어 스크립트 패키지 관리자를 통해 파일 tooinstall 응용 프로그램을 만들 필요성 toocode를 hello 하지 마십시오.

    -   일부 지점에서는 해당 되는 경우 이러한 구문 수도 있습니다. 추가할 toothe 일괄 처리 서비스 및에서 사용할 수 있는 일괄 처리 Api, Ui 등 hello 됩니다.

### <a name="pool-templates"></a>풀 템플릿

또한 hello 풀 템플릿 매개 변수 및 변수 보다 높은 수준의 구문을 따르는 hello toohello 표준 템플릿 기능을 지원 합니다.

-   **패키지 참조**

    -   필요에 따라 소프트웨어 복사 toobe toopool 노드 사용 하 여 허용 패키지 관리자. hello 패키지 관리자 및 패키지 id가 지정 됩니다. 수 toodeclare 되 고 하나 이상의 패키지 방지 hello 필요 toocreate hello 필요한 패키지를 가져오는 스크립트를 hello 스크립트를 설치 하 고 각 풀 노드에서 hello 스크립트를 실행 합니다.

hello 다음은 Vm 제공 toobe toouse의 풀 id 문자열과 hello 번호를 요구 하는 설치 하 고 유일한 ffmpeg와 Linux Vm의 풀을 만드는 템플릿의 예입니다.

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Hello 템플릿 파일의 이름이 면 _풀 ffmpeg.json_, 다음 hello 템플릿이 다음과 같이 호출 됩니다.

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>작업 템플릿

또한 hello 작업 서식 파일의 매개 변수 및 변수를 보다 높은 수준의 구문을 따르는 hello toohello 표준 템플릿 기능이 지원 됩니다.

-   **태스크 팩터리**

    -   하나의 태스크 정의에서 작업에 여러 태스크를 만듭니다. 파라메트릭 스윕, 파일당 태스크 및 태스크 컬렉션이라는 세 가지 형식의 태스크 팩터리가 지원됩니다.

hello 다음은 ffmpeg 두 낮은 해상도의 MP4 비디오 파일 tooone 코드 변환에 원본 비디오 파일 당 만들 하나 이상의 태스크를 사용 하는 작업을 생성 하는 서식 파일의 예입니다.

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Hello 템플릿 파일의 이름이 있는 경우 _작업 ffmpeg.json_, 다음 hello 템플릿이 다음과 같이 호출 됩니다.

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>파일 그룹 및 파일 전송

대부분의 작업 및 태스크에는 입력 파일이 필요하고 결과로 출력 파일을 생성합니다. 둘 다 입력 파일 및 출력 파일에는 일반적으로 toobe hello 클라이언트 toohello 노드 또는 hello 노드 toohello 클라이언트에서 전송 해야 합니다. Azure 일괄 처리 CLI 확장 hello 추상화 트래버스하여 파일 전송 및 각 일괄 처리 계정에 대해 기본적으로 생성 되어 hello 저장소 계정을 사용 합니다.

파일 그룹 tooa 컨테이너를 hello Azure 저장소 계정에서에서 생성 된 것과 같습니다. hello 파일 그룹에는 폴더가 가질 수 있습니다.

일괄 처리 CLI 확장 hello 클라이언트 tooa 지정 된 파일 그룹에서 업로드 파일 및 지정 된 파일 그룹 tooa 클라이언트 hello에서에서 파일 다운로드에 대 한 명령을 제공합니다.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

풀 및 작업 템플릿을 풀 노드 복사에 대 한 지정 된 파일 그룹 toobe에 저장 된 파일을 사용 하거나 노드 풀 해제 tooa 파일 그룹을 백업 합니다. 예를 들어 이전에 지정한 작업 서식 파일에서 hello 파일 그룹 "ffmpeg-입력"이 지정 hello 작업 팩터리에 대 한 hello 노드에; 트랜스 코딩을 위해 복사한 hello 원본 비디오 파일의 hello 위치로 hello 파일 그룹 "ffmpeg-output" hello hello 코드 변환 된 출력 파일이 있는 위치로 복사 toofrom hello 노드 각 작업 실행에 사용 됩니다.

## <a name="summary"></a>요약

서식 파일 및 파일 전송 지원이 현재 toohello Azure CLI 추가 되었습니다. hello 목표는 일괄 처리 toousers 연구원, IT 사용자 등 hello 일괄 처리 Api를 사용 하 여 toodevelop 코드 필요 없는 사용자를 사용할 수 있는 tooexpand hello 대상 그룹입니다. 코딩 하지 않고 Azure, 일괄 처리 및 일괄 처리에 의해 실행 hello 응용 프로그램 toobe 아는 사용자 풀 및 작업 만들기에 대 한 템플릿을 만들 수 있습니다. 템플릿 매개 변수를 사용자가 일괄 처리 및 hello 응용 프로그램의 세부 정보를 제공 하지 않고 hello 템플릿을 사용할 수 있습니다.

모든 피드백이 나 제안 사항을 제공 중 하나에 hello hello 또는이 문서에 대 한 설명을 hello Azure CLI hello에 대 한 일괄 처리 확장 프로그램을 사용해 [Azure 배치 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)합니다.

## <a name="next-steps"></a>다음 단계

- Hello 일괄 처리 템플릿 블로그 게시물을 참조: [Azure 일괄 처리 실행 작업을 사용 하 여 hello Azure CLI – 코드가 필요 하지 않습니다](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/)합니다.
- 설치 및 사용에 대 한 자세한 설명서, 샘플 및 소스 코드 hello에서 사용할 수 있는 [Azure GitHub 리포지토리](https://github.com/Azure/azure-batch-cli-extensions)합니다.
