---
title: "Azure 명령줄 2.0 aaaUse 인터페이스 tooget Azure 데이터 레이크 저장소 시작 | Microsoft Docs"
description: "Azure 크로스 플랫폼 명령줄 2.0 toocreate 데이터 레이크 저장소 계정을 사용 하 고 기본 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Azure CLI 2.0을 사용하여 Azure Data Lake Store 시작
> [!div class="op_single_selector"]
> * [포털](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Azure 데이터 레이크는 저장 하는 Azure CLI 2.0 toouse toocreate 방법에 대해 알아봅니다 계정 및 폴더를 만들어 업로드 및 다운로드 데이터 파일 등의 기본 작업 수행, 계정, 등을 삭제 합니다. Data Lake Store에 대한 자세한 내용은 [Data Lake Store 개요](data-lake-store-overview.md)를 참조하세요.

hello Azure CLI 2.0은 Azure 리소스 관리를 위해 Azure의 새로운 명령줄 환경입니다. macOS, Linux 및 Windows에서 사용할 수 있습니다. 자세한 내용은 [Azure CLI 2.0 개요](https://docs.microsoft.com/cli/azure/overview)를 참조하세요. Hello을 살펴볼 수도 있습니다 [Azure 데이터 레이크 저장소 CLI 2.0 참조](https://docs.microsoft.com/cli/azure/dls) 명령 및 구문을의 전체 목록은 합니다.


## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

* **Azure CLI 2.0** - 지침은 [Install Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.

## <a name="authentication"></a>인증

이 문서는 최종 사용자로 로그인하는 Data Lake Store에 보다 간단한 인증 방식을 사용합니다. hello 액세스 수준 tooData Lake 저장소 계정 및 파일 시스템은 다음 hello 로그인 한 사용자의 hello 액세스 수준을 통해 제어 됩니다. 그러나 여러 가지 다른 접근 방법이 데이터 레이크 저장소와 잘 tooauthenticate로 요소인 **최종 사용자 인증** 또는 **서비스 간 인증**합니다. 지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.


## <a name="log-in-tooyour-azure-subscription"></a>Azure 구독 tooyour에 로그인

1. Azure 구독에 로그인합니다.

    ```azurecli
    az login
    ```

    Hello 다음 단계에서 코드 toouse를 가져옵니다. 웹 브라우저 tooopen hello 페이지 https://aka.ms/devicelogin를 사용 하 고 hello 코드 tooauthenticate를 입력 합니다. 자격 증명을 사용 하 여 증명된 toolog 됩니다.

2. 모든 hello 창 목록에 로그인 hello 사용자 계정과 연결 된 Azure 구독. 다음 명령 toouse 특정 구독 hello를 사용 합니다.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Azure 데이터 레이크 저장소 계정 만들기

1. 새 리소스 그룹을 만듭니다. 다음 명령을 hello, hello toouse 원하는 매개 변수 값 제공 합니다. Hello 위치 이름에 공백이 포함 되어 있으면 따옴표로 묶습니다. 예를 들어 "East US 2"입니다. 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Hello 데이터 레이크 저장소 계정을 만듭니다.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Data Lake 저장소 계정에서 폴더 만들기

Azure 데이터 레이크 저장소 계정 toomanage에서 폴더를 만들고 데이터를 저장할 수 있습니다. 사용 하 여 hello 명령 toocreate는 폴더의 이름은 다음 **mynewfolder** hello hello 데이터 레이크 저장소 루트에 있습니다.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> hello `--folder` 매개 변수를 사용 하면 hello 명령 폴더를 만듭니다. 이 매개 변수가 없으면 hello 명령은 mynewfolder hello 루트 hello Data Lake 저장소 계정에 라는 빈 파일을 만듭니다.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>데이터 tooa Data Lake 저장소 계정에 업로드

Hello 루트 수준 또는 tooa 만든 폴더에 hello 계정 내에서 직접 데이터 tooData Lake 저장소에 업로드할 수 있습니다. 아래 hello 조각은 보여 방법을 tooupload 일부 예제 데이터 toohello 폴더 (**mynewfolder**) hello 이전 섹션에서 만든 합니다.

몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다. Hello 파일을 다운로드 하 고 C:\sampledata\ 같은 컴퓨터에 로컬 디렉터리에 저장 합니다.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Hello 대상에 대 한 hello hello 파일 이름을 포함 하는 전체 경로 지정 해야 합니다.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Data Lake Store 계정의 파일 나열

데이터 레이크 저장소 계정에서 명령 toolist hello 파일을 다음 hello를 사용 합니다.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

이 hello 출력 비슷한 toohello 다음과 같아야 합니다.

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Data Lake Store 계정에서 데이터 이름 바꾸기, 다운로드 및 삭제 

* **toorename 파일**, hello 다음 명령을 사용 하 여:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **toodownload 파일**, hello 다음 명령을 사용 합니다. 이미 지정 hello 대상 경로가 있는지 확인 합니다.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > 존재 하지 않는 경우 hello 명령은 hello 대상 폴더를 만듭니다.
    > 
    >

* **toodelete 파일**, hello 다음 명령을 사용 하 여:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Toodelete hello 폴더가 **mynewfolder** 및 hello 파일 **vehicle1_09142014_copy.csv** 함께 하나의 명령으로 사용 하 여 hello-매개 변수를 recurse

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Data Lake Store 계정에 대한 ACL 및 사용 권한 작업

이 섹션에서는 방법에 대 한 설명 toomanage Acl 및 Azure CLI 2.0을 사용 하 여 사용 권한. Azure Data Lake Store에서 ACL을 구현하는 방법에 대한 자세한 내용은 [Data Lake Store에서 액세스 제어 개요](data-lake-store-access-control.md)를 참조하세요.

* **파일/폴더의 tooupdate hello 소유자**, hello 다음 명령을 사용 하 여:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **파일/폴더에 대 한 tooupdate hello 권한을**, hello 다음 명령을 사용 하 여:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **지정된 된 경로 대 한 Acl tooget hello**, hello 다음 명령을 사용 하 여:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    hello 출력은 비슷한 toohello 다음 됩니다.

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **ACL에 대 한 항목이 tooset**, hello 다음 명령을 사용 하 여:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **ACL에 대 한 항목이 tooremove**, hello 다음 명령을 사용 하 여:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **전체 기본 ACL tooremove**, hello 다음 명령을 사용 하 여:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **전체 기본이 아닌 ACL tooremove**, hello 다음 명령을 사용 하 여:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Data Lake 저장소 계정 삭제
다음 명령 toodelete 데이터 레이크 저장소 계정 hello를 사용 합니다.

```azurecli
az dls account delete --account mydatalakestore
```

메시지가 표시 되 면 입력 **Y** toodelete hello 계정.

## <a name="next-steps"></a>다음 단계

* [Azure Data Lake Store CLI 2.0 참조](https://docs.microsoft.com/cli/azure/dls)
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight에 데이터 레이크 저장소 사용](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
