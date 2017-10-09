---
title: "aaaTutorial-사용 하 여 hello Python 용 Azure 일괄 처리 SDK | Microsoft Docs"
description: "Hello Azure 일괄 처리의 기본 개념을 알아봅니다 하 고 Python을 사용 하 여 간단한 솔루션을 빌드하십시오."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Python 용 hello 일괄 처리 SDK 시작

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.JS](batch-nodejs-get-started.md)
>
>

hello 기본 사항 알아보기 [Azure 배치] [ azure_batch] 및 hello [일괄 처리 Python] [ py_azure_sdk] 클라이언트 Python에서 작성 하는 작은 일괄 처리 응용 프로그램에 설명할 때. 어떻게 두 예제 스크립트 사용 하 여 hello 일괄 처리 서비스 tooprocess hello 클라우드에서 Linux 가상 컴퓨터에서 병렬 작업 및 상호 작용 하는 방법을 살펴보겠습니다 [Azure 저장소](../storage/common/storage-introduction.md) 파일 준비 및 검색 합니다. 일반적인 일괄 처리 응용 프로그램 워크플로 자세한 및 hello의 주요 구성 요소 일괄 처리 풀, 작업, 작업 등의 기본으로 이해 하 고 계산 노드 합니다.

![Batch 솔루션 워크플로(기본)][11]<br/>

## <a name="prerequisites"></a>필수 조건
이 문서에는 사용자가 Python에 대한 실용적인 지식을 가지고 Linux에 익숙하다고 가정합니다. 또한 Azure hello 일괄 처리 및 저장소 서비스에 대해 아래 지정 된 수 toosatisfy hello 계정 만들기 요구 하 가정 합니다.

### <a name="accounts"></a>계정
* **Azure 계정**: Azure 구독이 아직 없는 경우 [무료 Azure 계정][azure_free_account]을 만듭니다.
* **Batch 계정**: Azure 구독이 있으면 [Azure Batch 계정을 만듭니다](batch-account-create-portal.md).
* **저장소 계정**: [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)의 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 섹션을 참조하세요.

### <a name="code-sample"></a>코드 샘플
hello Python 자습서 [코드 샘플] [ github_article_samples] hello에서 찾을 수 많은 일괄 처리 코드 예제는 hello 중 하나인 [azure 일괄 처리-샘플] [ github_samples] 의 리포지토리 GitHub 합니다. 클릭 하 여 모든 hello 샘플을 다운로드할 수 있습니다 **클론 또는 다운로드 > zip 파일 다운로드** hello 리포지토리 홈 페이지에서 또는 hello를 클릭 하 여 [azure 일괄 처리-샘플 master.zip] [ github_samples_zip]직접 다운로드 링크입니다. 이 자습서에 대 한 hello 두 스크립트 hello에 부여 hello ZIP 파일의 내용을 hello를 추출 하면 `article_samples` 디렉터리:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Python 환경
toorun hello *python_tutorial_client.py* 해야 로컬 워크스테이션 샘플 스크립트는 **Python 인터프리터** 버전과 호환 **2.7** 또는 **3.3 +**합니다. hello 스크립트는 Linux 및 Windows에서 테스트 되었습니다.

### <a name="cryptography-dependencies"></a>암호화 종속성
Hello에 대 한 hello 종속성을 설치 해야 [암호화] [ crypto] hello에 필요한 라이브러리 `azure-batch` 및 `azure-storage` Python 패키지 합니다. Hello 플랫폼에 대 한 적절 한 작업을 다음 중 하나를 수행 하거나 toohello 참조 [암호화 설치] [ crypto_install] 자세한 정보에 대 한 세부 정보:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Linux에서 Python 3.3 +를 설치 하는 경우 hello Python 종속성에 대 한 hello python3 해당 항목을 사용 합니다. 예를 들어 Ubuntu에서 `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Azure 패키지
다음으로, hello 설치 **Azure 배치** 및 **Azure 저장소** Python 패키지 합니다. 사용 하 여 두 패키지 모두를 설치할 수 있습니다 **pip** 및 hello *requirements.txt* ´ ֿ ´:

`/azure-batch-samples/Python/Batch/requirements.txt`

문제 다음 **pip** tooinstall hello 일괄 처리 및 저장소 패키지 명령:

`pip install -r requirements.txt`

Hello를 설치할 수 있습니다 또는 [azure 배치] [ pypi_batch] 및 [azure 저장소] [ pypi_storage] Python 수동으로 패키지:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> 권한 없는 계정을 사용 하는 할 수 있습니다 tooprefix 사용 하는 명령이 `sudo`합니다. 예: `sudo pip install -r requirements.txt`. Python 패키지를 설치하는 방법에 대한 자세한 내용은 python.org에서 [패키지 설치][pypi_install]를 참조하세요.
>
>

## <a name="batch-python-tutorial-code-sample"></a>배치 Python 자습서 코드 샘플
두 개의 Python 스크립트와 몇 개의 데이터 파일의 hello 일괄 처리 Python 자습서 코드 샘플 구성 됩니다.

* **python_tutorial_client.py**: 계산 노드 (가상 컴퓨터)에 병렬 작업 일괄 처리 및 저장소 서비스 tooexecute hello와 상호 작용 합니다. hello *python_tutorial_client.py* 스크립트는 로컬 워크스테이션에서 실행 합니다.
* **python_tutorial_task.py**:에서 실행 되는 hello 스크립트의에서 계산 노드 Azure tooperform hello 실제 작업 합니다. Hello 샘플에서 *python_tutorial_task.py* 구문 분석 하 여 hello Azure 저장소 (hello 입력된 파일)에서 다운로드 한 파일의 텍스트입니다. 텍스트 파일을 생성 한 다음 (hello 출력 파일) hello 상위 3 개의에 있는 단어 hello 입력된 파일의 목록이 들어 있습니다. Hello 출력 파일을 만든 후 *python_tutorial_task.py* 업로드 hello 파일 tooAzure 저장소입니다. 워크스테이션에서 실행 하는 다운로드 toohello 클라이언트 스크립트를 사용할 수 있도록 합니다. hello *python_tutorial_task.py* 여러에서 병렬 실행 스크립트의에서 계산 노드 hello 일괄 처리 서비스.
* **./data/taskdata\*.txt**: hello 작업 hello에서 실행 되는 계산 노드 수에 대 한 hello 입력이 세 개의 텍스트 파일에 제공 합니다.

다이어그램을 다음 hello hello 클라이언트와 작업 스크립트에 의해 수행 된 기본 작업이 hello를 보여 줍니다. 이러한 기본 워크플로는 Batch를 사용하여 만드는 많은 계산 솔루션의 일반적인 형태입니다. Hello 일괄 처리 서비스에서에서 사용할 수 있는 모든 기능을 보여 주지 동안 거의 모든 일괄 처리 시나리오가 워크플로의 일부를 포함 합니다.

![Batch 예제 워크플로][8]<br/>

[**1단계.**](#step-1-create-storage-containers) Azure Blob Storage에 **컨테이너**를 만듭니다.<br/>
[**2단계.**](#step-2-upload-task-script-and-data-files) 작업 스크립트와 입력 파일 toocontainers를 업로드 합니다.<br/>
[**3단계.**](#step-3-create-batch-pool) Batch **풀**을 만듭니다.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** 풀 hello **StartTask** 다운로드 hello 풀을 참가 작업 스크립트 (python_tutorial_task.py) toonodes hello 합니다.<br/>
[**4단계.**](#step-4-create-batch-job) Batch **작업**을 만듭니다.<br/>
[**5단계.**](#step-5-add-tasks-to-job) 추가 **작업** toohello 작업 합니다.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** hello 작업은 예약 된 tooexecute 노드에 있습니다.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** 각 태스크는 Azure Storage에서 입력 데이터를 다운로드한 다음 실행을 시작합니다.<br/>
[**6단계.**](#step-6-monitor-tasks) 태스크를 모니터링합니다.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** 작업을 완료 하는 대로 해당 출력 데이터 tooAzure 저장소 업로드 합니다.<br/>
[**7단계.**](#step-7-download-task-output) 저장소에서 태스크 출력을 다운로드합니다.

언급한 바와 같이, 모든 Batch 솔루션이 정확히 이러한 단계를 수행하는 것은 아니며, 훨씬 더 많은 단계를 포함할 수 있지만 이 샘플은 배치 솔루션에서 찾을 수 있는 일반적인 프로세스를 보여 줍니다.

## <a name="prepare-client-script"></a>클라이언트 스크립트 준비
Hello 예제를 실행 하기 전에 일괄 처리 및 저장소 계정 자격 증명을 너무 추가*python_tutorial_client.py*합니다. 아직 수행 하지 않은, 하는 경우 위의 삼각형 자격 증명을 사용 하면 즐겨 찾는 편집기 및 update hello에서 hello 파일을 엽니다.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

Hello에 일괄 처리 및 저장소 계정 자격 증명의 각 서비스 계정 블레이드 hello 내에서 찾을 수 있습니다 [Azure 포털][azure_portal]:

![Hello 포털에서 자격 증명을 일괄 처리][9]
![hello 포털에서 저장소 자격 증명][10]<br/>

다음 섹션 hello, hello 단계에서 사용 하는 분석 hello tooprocess hello 일괄 처리 서비스에서에서 작업을 스크립팅 합니다. 작업을 hello 문서의 나머지 부분 hello 수행 하는 동안 편집기에서 스크립트를 toohello 정기적으로 toorefer를 좋습니다.

다음 줄에서 toohello 이동 **python_tutorial_client.py** toostart 1 단계:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>1단계: Storage 컨테이너 만들기
![Azure Storage에 컨테이너 만들기][1]
<br/>

Batch에는 Azure Storage와의 상호 작용을 위해 기본 제공되는 지원이 포함됩니다. 저장소 계정의 컨테이너에는 일괄 처리 계정에서 실행 되는 hello 작업에서 필요한 hello 파일 제공 합니다. 또한 hello 컨테이너 hello 작업을 생성 하는 곳 toostore hello 출력 데이터를 제공 합니다. hello 먼저 hello *python_tutorial_client.py* 스크립트에 세 개의 컨테이너를 만들 [Azure Blob 저장소](../storage/common/storage-introduction.md#blob-storage):

* **응용 프로그램**:이 컨테이너는 hello 태스크가 실행 하는 hello Python 스크립트를 저장 하는 *python_tutorial_task.py*합니다.
* **입력**: 작업은 hello에서 데이터 파일 tooprocess hello를 다운로드 *입력* 컨테이너입니다.
* **출력**: hello 결과 toohello 업로드는 입력된 파일 처리를 완료 하는 작업 *출력* 컨테이너입니다.

저장소와 순서 toointeract에서 계정 및 컨테이너를 만들 hello 사용 하 여 [azure 저장소] [ pypi_storage] toocreate 패키지는 [BlockBlobService] [ py_blockblobservice] 개체-hello "blob 클라이언트입니다." 다음 세 개의 컨테이너가 hello 저장소 계정의 blob 클라이언트 hello를 사용 하 여 만듭니다.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

Hello 컨테이너를 만든 후에 이제 hello 응용 프로그램 hello 작업에 의해 사용 될 hello 파일을 업로드 수 있습니다.

> [!TIP]
> [어떻게 toouse Python에서 Azure Blob 저장소](../storage/blobs/storage-python-how-to-use-blob-storage.md) Azure 저장소 컨테이너 및 blob 작업의 개요를 제공 합니다. 일괄 처리 작업을 시작할 때 hello 위쪽 읽기 목록에 있는 이어야 합니다.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>2단계: 작업 스크립트 및 데이터 파일 업로드
![업로드 작업 응용 프로그램에 대 한 입력 (데이터) toocontainers 파일][2]
<br/>

Hello 파일에서 작업을 업로드 *python_tutorial_client.py* 먼저의 컬렉션을 정의 **응용 프로그램** 및 **입력** hello 로컬 컴퓨터에 있는 대로 파일 경로입니다. 그런 다음 이러한 파일 toohello 컨테이너 hello 이전 단계에서 만든를 업로드 합니다.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

Hello 목록 축약을 사용 하 여, `upload_file_to_container` hello 컬렉션의 각 파일 및 2에 대 한 함수가 호출 될 [ResourceFile] [ py_resource_file] 컬렉션을 채웁니다. hello `upload_file_to_container` 함수 아래에 나타납니다.

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ py_resource_file] 해당 태스크를 실행 하기 전에 hello URL tooa 파일 다운로드 한 tooa은 Azure 저장소에 있는 일괄 처리의 작업 계산 노드를 제공 합니다. hello [ResourceFile][py_resource_file]. **blob_source** Azure 저장소에 있는 속성 hello hello 파일의 전체 URL을 지정 합니다. hello URL toohello 파일 보안 액세스를 제공 하는 공유 액세스 서명 (SAS)을 포함할 수도 있습니다. 배치에서 대부분의 태스크 형식은 다음을 포함하는 *ResourceFiles* 속성을 포함합니다.

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

이 샘플에서는 JobPreparationTask hello 또는 JobReleaseTask 작업 종류를 사용 하지 않지만 자세히 알아볼 수 있습니다에 대 한 [Azure 일괄 처리에서 실행 작업 준비 및 완료 작업 하는 계산 노드](batch-job-prep-release.md)합니다.

### <a name="shared-access-signature-sas"></a>공유 액세스 서명(SAS)
공유 액세스 서명에 보안 액세스 toocontainers 및 Azure 저장소에서 blob를 제공 하는 문자열입니다. hello *python_tutorial_client.py* 스크립트과 사용 하 여 두 blob 컨테이너 공유 액세스 서명을 tooobtain 이러한 공유 서명 문자열 hello 저장소 서비스에서에서 액세스 하는 방법을 보여 줍니다.

* **공유 액세스 서명은 blob**: hello 작업 스크립트 및 입력 데이터 파일 저장소에서 다운로드할 때 hello 풀 StartTask 사용 하 여 blob 공유 액세스 서명 (참조 [단계 #3](#step-3-create-batch-pool) 아래). hello `upload_file_to_container` 함수 *python_tutorial_client.py* hello 코드가 포함 된 각 blob의 공유 액세스 서명을 가져옵니다. 호출 하 여 작업을 수행 [BlockBlobService.make_blob_url] [ py_make_blob_url] hello 저장소 모듈에 있습니다.
* **컨테이너 공유 액세스 서명을**: 각 작업 hello 계산 노드에서 작업을 마치면 대로 해당 출력 파일 toohello 업로드 *출력* Azure 저장소의 컨테이너입니다. toodo, *python_tutorial_task.py* 쓰기 액세스 toohello 컨테이너를 제공 하는 컨테이너 공유 액세스 서명을 사용 하 여 합니다. hello `get_container_sas_token` 함수 *python_tutorial_client.py* 명령줄 인수 toohello 작업으로 전달 되는 hello 컨테이너의 공유 액세스 서명을 가져옵니다. #5 단계 [추가 작업 tooa 작업](#step-5-add-tasks-to-job), hello 컨테이너 SAS의 hello 사용에 설명 합니다.

> [!TIP]
> 공유 액세스 서명에 대 hello 두 부분으로 구성 시리즈 체크아웃 [1 부: hello SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 및 [2 부: 만들기 및 SAS를 사용 하 여 Blob 서비스 hello로](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn 보안 액세스를 제공 하는 방법에 대 한 자세한 저장소 계정에 toodata 합니다.
>
>

## <a name="step-3-create-batch-pool"></a>3단계: Batch 풀 만들기
![Batch 풀 만들기][3]
<br/>

Batch **풀**은 Batch가 작업의 태스크를 실행하는 계산 노드(가상 컴퓨터)의 컬렉션입니다.

Hello 작업 스크립트 및 데이터 파일 toohello 저장소 계정에 업로드 한 후 *python_tutorial_client.py* hello 일괄 처리 Python 모듈을 사용 하 여 hello 일괄 처리 서비스 상호 작용을 시작 합니다. toodo 등에 [BatchServiceClient] [ py_batchserviceclient] 만들어집니다.

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

다음으로, 풀이 계산 노드의 만들어지면 hello 호출 하 여 일괄 처리 계정에에서 너무`create_pool`합니다.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

풀을 만들 때 정의 [PoolAddParameter] [ py_pooladdparam] hello 풀에 대 한 몇 가지 속성을 지정 하는:

* **ID** hello 풀의 (*id* -필요)<p/>배치에서 대부분의 엔터티처럼 새 풀은 배치 계정 내에서 고유 ID를 가지고 있어야 합니다. hello Azure의에서 hello 풀을 식별 하는 방법 및 코드 참조의 ID를 사용 하 여 toothis 풀 [포털][azure_portal]합니다.
* **계산 노드 수**(*target_dedicated* - 필수)<p/>이 속성 지정 hello 풀에 어떻게 많은 Vm을 배포 해야 합니다. 모든 일괄 처리 계정 기본 한지 중요 toonote는 **할당량** hello의 수를 제한 하 **코어** (및 따라서 계산 노드) 일괄 처리 계정에 있습니다. 찾을 수 있습니다 hello 기본 할당량 및 지침은 방법 너무[는 할당량을 늘릴 수](batch-quota-limit.md#increase-a-quota) (예: hello 최대 코어 수의 일괄 처리 계정)에 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md)합니다. "풀이 X 노드보다 더 멀리 도달할 수 없는 경우" 이 코어 할당량 hello 원인이 될 수 있습니다.
* 노드의 **운영 체제**(*virtual_machine_configuration* **또는** *cloud_service_configuration* - 필수)<p/>*python_tutorial_client.py*에서 [VirtualMachineConfiguration][py_vm_config]을 사용하여 Linux 노드 풀을 만듭니다. hello `select_latest_verified_vm_image_with_node_agent_sku` 함수 `common.helpers` 사용 작업을 간소화 [Azure 가상 컴퓨터 마켓플레이스] [ vm_marketplace] 이미지입니다. 마켓플레이스 이미지를 사용하는 방법에 대한 자세한 내용은 [Azure Batch 풀에서 Linux 계산 노드 프로비전](batch-linux-nodes.md) 을 참조하세요.
* **계산 노드 크기** (*vm_size* - 필수)<p/>[VirtualMachineConfiguration][py_vm_config]의 Linux 노드를 지정하는 것이기 때문에 [Azure의 가상 컴퓨터 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 VM 크기(이 샘플의 `STANDARD_A1`)를 지정합니다. 다시 자세한 내용은 [Azure 배치 풀에서 Linux 계산 노드 프로비전](batch-linux-nodes.md) 을 참조하세요.
* **시작 태스크**(*start_task* - 필수 아님)<p/>실제 노드 속성 위에 hello, 함께 지정할 수도 있습니다는 [StartTask] [ py_starttask] hello 풀 (필요 하지 않은)에 대 한 합니다. StartTask hello 해당 노드의 hello 풀에 참가 하 고 노드를 다시 시작 될 때마다 각 노드에서 실행 됩니다. StartTask hello hello 실행 작업을 실행 하는 hello 응용 프로그램을 설치 하는 등의 작업에 대 한 계산 노드를 준비 하기 위한 특히 유용 합니다.<p/>이 샘플 응용 프로그램에서는 hello StartTask 저장소에서 다운로드 하는 hello 파일에 복사 (hello StartTask를 사용 하 여 지정 되는 **resource_files** 속성) hello StartTask에서에서 *작업디렉터리* toohello *공유* hello 노드에서 실행 중인 모든 작업에 액세스할 수 있는 디렉터리입니다. 기본적으로,이 복사 `python_tutorial_task.py` toohello 공유 디렉터리 각 노드에서 hello 노드 hello 풀에 참가 하는 대로 hello 노드에서 실행 되는 모든 작업에 액세스할 수 있도록 합니다.

Hello 호출 toohello 없는데 `wrap_commands_in_shell` 도우미 함수입니다. 이 함수는 별도 명령의 컬렉션을 사용하고 작업의 명령줄 속성에 적절한 단일 명령줄을 만듭니다.

또한 위의 코드 조각 hello에에서 주목할 만한은 hello를 사용 하 여 hello에 두 환경 변수의 **command_line** hello StartTask의 속성: `AZ_BATCH_TASK_WORKING_DIR` 및 `AZ_BATCH_NODE_SHARED_DIR`합니다. 일괄 처리 풀 내에서 각 계산 노드가 특정 tooBatch 있는 여러 환경 변수가 자동으로 구성 됩니다. 작업에 의해 실행 되는 모든 프로세스는 액세스 toothese 환경 변수가 있습니다.

> [!TIP]
> toofind 작업 작업 디렉터리에 대 한 정보 뿐만 아니라는 일괄 처리 풀 계산 노드에서 사용할 수 있는 hello 환경 변수에 대 한 자세한 내용을 참조 **작업에 대 한 환경 설정을** 및 **파일 및 디렉터리**  hello에 [Azure 배치 기능 개요](batch-api-basics.md)합니다.
>
>

## <a name="step-4-create-batch-job"></a>4단계: Batch 작업 만들기
![Batch 작업 만들기][4]<br/>

Batch **작업**은 태스크의 컬렉션이며 계산 노드의 풀과 관련됩니다. 작업의 hello 작업 관련 hello 풀 계산 노드에서 실행 됩니다.

구성 하 고 관련된 작업에서 작업을 추적 뿐만 아니라-hello 최대 runtime hello 작업에 대 한 (및 확장 하면 해당 작업)와 같은 특정 제약 조건을 부과 하는 것에 대 한 작업을 사용할 수 있습니다 및 작업 우선 순위에 관계 tooother 작업에서 일괄 처리 계정 hello 합니다. 그러나이 예제에서는 hello 작업 3 단계에서 생성 된 hello 풀 연관 되어 있습니다. 추가적으로 구성되는 다른 속성은 없습니다.

모든 Batch 작업은 특정 풀에 연결됩니다. 이 연결은 hello 작업의 작업에서 실행 하는 노드를 표시 합니다. Hello를 사용 하 여 hello 풀을 지정 [PoolInformation] [ py_poolinfo] hello 아래 코드 조각에 나와 있는 것 처럼 속성입니다.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

작업을 만든 후, tooperform hello 작업 작업에 추가 됩니다.

## <a name="step-5-add-tasks-toojob"></a>5 단계: 추가 작업 toojob
![작업 toojob 추가][5]<br/>
*(1) 작업 toohello 작업 추가 되 고 (2) hello 작업은 노드에서 예약 된 toorun (3) hello 작업 hello 데이터 파일 tooprocess 다운로드*

일괄 처리 **작업** hello 개별 작업 단위 hello를 실행 하는 계산 노드는 합니다. 작업 명령줄 개이고 hello 스크립트 또는 명령줄에서 지정 하는 실행 파일을 실행 합니다.

작업을 수행 하는 tooactually, 작업 tooa 작업을 추가 해야 합니다. 각 [CloudTask] [ py_task] 명령줄 속성으로 구성 하 고 [ResourceFiles] [ py_resource_file] (hello 풀 StartTask와 마찬가지로) 해당 hello 해당 명령줄이 자동으로 실행 하기 전에 작업 toohello 노드를 다운로드 합니다. Hello 샘플 각 작업 하나의 파일을 처리합니다. 따라서 ResourceFiles 컬렉션은 단일 요소를 포함합니다.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> 와 같은 환경 변수에 액세스 하면 `$AZ_BATCH_NODE_SHARED_DIR` hello 노드에 없는 응용 프로그램을 실행 또는 `PATH`, 작업 명령줄 hello를 호출 해야와 같은 명시적으로 셸 `/bin/sh -c MyTaskApplication $MY_ENV_VAR`합니다. 이 요구 사항을 작업 hello 노드의 응용 프로그램을 실행 하는 경우에 필요 하지 않습니다. `PATH` 환경 변수를 참조 하지 않습니다.
>
>

Hello 내 `for` hello 위의 코드 조각에서 루프를 hello 작업에 대 한 hello 명령줄 너무 전달 되는 명령줄 인수를 5로 구성 되며을 볼 수 있습니다*python_tutorial_task.py*:

1. **filepath**: hello 노드에 있는 것 처럼 hello 로컬 경로 toohello 파일입니다. 때 ResourceFile 개체에 hello `upload_file_to_container` 만들어진 2 단계에서 위의 hello 파일 이름이이 속성 사용 (hello `file_path` hello ResourceFile 생성자에서 매개 변수). 해당 hello 파일이 hello에 동일한 나타냅니다으로 hello 노드에서 디렉터리 *python_tutorial_task.py*합니다.
2. **numwords**: hello top *N* 단어 toohello 출력 파일이 작성 해야 합니다.
3. **storageaccount**: hello hello hello 컨테이너 toowhich hello 작업 출력을 소유 하는 저장소 계정 이름을 업로드 되어야 합니다.
4. **storagecontainer**: hello 저장소 컨테이너 toowhich hello의 hello 이름을 출력 파일을 업로드 해야 합니다.
5. **sastoken**: toohello 쓰기 액세스를 제공 하는 hello 공유 액세스 서명 (SAS) **출력** Azure 저장소의 컨테이너입니다. hello *python_tutorial_task.py* 스크립트에이 공유 액세스 서명을 사용 하 여 때 해당 BlockBlobService 참조를 만듭니다. 이 hello 저장소 계정에 대 한 선택 키를 요구 하지 않고 쓰기 액세스 toohello 컨테이너를 제공 합니다.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>6단계: 작업 모니터링
![작업 모니터링][6]<br/>
*완료 상태에 대 한 스크립트 (1) 모니터 hello 작업 hello 및 (2) hello 작업 업로드 결과 데이터 tooAzure 저장소*

작업 tooa 작업 추가 되 면 자동으로 큐에 대기 되며 hello 작업과 연결 된 hello 풀 내에서 계산 노드에서 실행 되도록 예약 됩니다. 지정 된 hello 설정에 따라, 일괄 처리 모든 작업 큐, 예약, 다시 시도 및 기타 작업 관리 업무에 대 한 처리 있습니다.

가지 많은 작업 실행이 toomonitoring입니다. hello `wait_for_tasks_to_complete` 함수 *python_tutorial_client.py* 모니터링이 경우 특정 상태에 대 한 작업 hello의 간단한 예를 제공 [완료] [ py_taskstate] 상태입니다.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>7단계: 작업 출력 다운로드
![Storage에서 작업 출력 다운로드][7]<br/>

Hello 작업이 완료 되 면 했으므로 hello 작업의에서 출력을 hello Azure 저장소에서 다운로드할 수 있습니다. 이렇게 호출 하 여 너무`download_blobs_from_container` 에 *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> 호출을 너무 hello`download_blobs_from_container` 에 *python_tutorial_client.py* hello 파일을 다운로드 한 tooyour 홈 디렉터리 이어야 함을 지정 합니다. 무료 toomodify 느껴집니다이 위치를 출력 합니다.
>
>

## <a name="step-8-delete-containers"></a>8단계: 컨테이너 삭제
Azure 저장소에 있는 데이터에 대 한 요금이 청구 되므로 항상 것은 더 이상 존재 하지 않는 모든 blob 일괄 처리 작업에 필요한 것은 좋지 tooremove. *python_tutorial_client.py*, 이렇게 3 개의 호출이와 너무[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>9 단계: hello 작업과 hello 풀 삭제
증명된 toodelete hello 작업과 hello 풀 hello에서 만든 hello 마지막 단계에서는 *python_tutorial_client.py* 스크립트입니다. 작업 및 태스크 자체에 대한 요금이 부과되지 않지만 계산 노드에 대한 요금이 청구 *됩니다* . 따라서 노드를 필요할 때만 할당하는 것이 좋습니다. 사용하지 않는 풀을 삭제하는 것이 유지 관리 프로세스의 일부가 될 수 있습니다.

hello BatchServiceClient의 [JobOperations] [ py_job] 및 [PoolOperations] [ py_pool] 는 해당 삭제 메서드를 둘 다 삭제를 확인 하는 경우 호출.

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> 계산 리소스에 대해 요금이 부과되고 사용하지 않는 풀 삭제는 비용을 최소화한다는 점을 유의하세요. 또한,을 해당 풀에서 모든 계산 노드를 삭제할 풀을 삭제 하 고는 hello 노드에서 모든 데이터를 복구할 수 없습니까 hello 풀이 삭제 된 후 주의 합니다.
>
>

## <a name="run-hello-sample-script"></a>Hello 예제 스크립트 실행
Hello를 실행 하는 경우 *python_tutorial_client.py* hello 자습서에서 스크립트 [코드 샘플][github_article_samples], hello 콘솔 출력은 toohello 다음과 유사 합니다. 중지 `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` hello 풀의 계산 노드를 만듭니다 시작 하 고 hello 풀의 시작 작업의 hello 명령은 실행 됩니다. 사용 하 여 hello [Azure 포털] [ azure_portal] toomonitor 풀, 계산 노드, 작업 및 작업 동안과 그 후 실행 합니다. 사용 하 여 hello [Azure 포털] [ azure_portal] 또는 hello [Microsoft Azure 저장소 탐색기] [ storage_explorer] tooview hello 저장소 리소스 (컨테이너 및 blob) hello 응용 프로그램에 의해 생성 됩니다.

> [!TIP]
> Hello 실행 *python_tutorial_client.py* hello 내에서 스크립팅할 `azure-batch-samples/Python/Batch/article_samples` 디렉터리입니다. 상대 경로 사용 하 여 hello에 대 한 `common.helpers` 모듈 가져오기, 표시 될 수 있으므로 `ImportError: No module named 'common'` 이 디렉터리 내에서 hello 스크립트를 실행 하지 않는 경우.
>
>

일반적인 실행 시간은 **약 5-7 분** 기본 구성에서 hello 예제를 실행 합니다.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>다음 단계
무료 toomake 변경 너무 느껴집니다*python_tutorial_client.py* 및 *python_tutorial_task.py* tooexperiment 서로 다른 시나리오를 계산 합니다. 예를 들어 너무 실행 지연을 추가 해 보십시오*python_tutorial_task.py* toosimulate 장기 실행 작업 및 hello 포털에서이 모니터링 합니다. 시도 더 많은 작업을 추가 하거나 hello 계산 노드 수를 조정 합니다. 에 대 한 논리 toocheck를 추가 하 고 기존 풀 toospeed 실행 시간이 hello 사용을 허용 합니다.

이제 일괄 처리 솔루션의 기본 워크플로 hello에 익숙하다면 toohello hello 일괄 처리 서비스의 추가 기능에서 toodig 시간입니다.

* 검토 hello [Azure 배치 개요 기능](batch-api-basics.md) 아티클의 새 toohello 서비스 하는 경우는 것이 좋습니다.
* 시작 hello에서 다른 일괄 처리 개발 문서 **개발 심층 분석** hello에 [일괄 학습 경로][batch_learning_path]합니다.
* 체크 아웃의 hello에 일괄 처리를 사용 하 여 "상위 n 개 단어" hello 작업을 처리 한 다른 구현을 [TopNWords] [ github_topnwords] 샘플.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Azure Storage에 컨테이너 만들기"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "업로드 작업 응용 프로그램에 대 한 입력 (데이터) toocontainers 파일"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Batch 풀 만들기"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Batch 작업 만들기"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "작업 toojob 추가"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "작업 모니터링"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Storage에서 작업 출력 다운로드"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Batch 솔루션 워크플로(전체 다이어그램)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "포털의 Batch 자격 증명"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "포털의 Storage 자격 증명"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Batch 솔루션 워크플로(최소 다이어그램)"
