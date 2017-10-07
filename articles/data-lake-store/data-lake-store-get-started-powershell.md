---
title: "Azure 데이터 레이크 저장소 aaaUse PowerShell tooget 시작 | Microsoft Docs"
description: "Azure PowerShell toocreate 데이터 레이크 저장소 계정을 사용 하 고 기본 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Azure PowerShell을 사용하여 Azure 데이터 레이크 저장소 시작
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

Azure 데이터 레이크는 저장 하는 Azure PowerShell toocreate toouse 방법에 대해 알아봅니다 계정 및 폴더를 만들어 업로드 및 다운로드 데이터 파일 등의 기본 작업 수행, 계정, 등을 삭제 합니다. Data Lake Store에 대한 자세한 내용은 [Data Lake Store 개요](data-lake-store-overview.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure PowerShell 1.0 이상**. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="authentication"></a>인증
이 문서에서는 간단한 인증 방법이 증명된 tooenter 있는 데이터 레이크 저장소와 Azure 계정 자격 증명 합니다. hello 액세스 수준 tooData Lake 저장소 계정 및 파일 시스템은 다음 hello 로그인 한 사용자의 hello 액세스 수준을 통해 제어 됩니다. 그러나 여러 가지 다른 접근 방법이 데이터 레이크 저장소와 잘 tooauthenticate로 요소인 **최종 사용자 인증** 또는 **서비스 간 인증**합니다. 지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.

## <a name="create-an-azure-data-lake-store-account"></a>Azure 데이터 레이크 저장소 계정 만들기
1. 바탕 화면에서 새 Windows PowerShell 창을 열고 입력 hello 조각 toolog tooyour Azure 계정에에서 따라, hello 구독을 설정 하 고 hello 데이터 레이크 저장소 공급자를 등록 합니다. , 입력 정보 요청된 toolog 있는지 확인 하는 경우 로그인 할 hello 구독 admininistrators/소유자 중 하나로:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Azure 데이터 레이크 저장소 계정은 Azure 리소스 그룹과 연결됩니다. Azure 리소스 그룹을 만드는 작업부터 시작합니다.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Azure 리소스 그룹 만들기](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Azure 리소스 그룹 만들기")
3. Azure 데이터 레이크 저장소 계정을 만듭니다. 지정한 hello 이름은 소문자와 숫자만 포함 해야 합니다.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Azure Data Lake Store 계정 만들기](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Azure Data Lake Store 계정 만들기")
4. Hello 계정을 성공적으로 만들어졌는지 확인 합니다.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    이 출력 하는 hello **True**합니다.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Azure 데이터 레이크 저장소에서 디렉터리 구조 만들기
Azure 데이터 레이크 저장소 계정 toomanage에서 디렉터리를 만들고 데이터를 저장할 수 있습니다.

1. 루트 디렉터리를 지정합니다.

        $myrootdir = "/"
2. 라는 새 디렉터리를 만듭니다 **mynewdirectory** hello 지정된 루트 아래 합니다.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. 해당 hello 새 디렉터리 성공적으로 만들어지면 확인 합니다.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Hello 다음과 같은 출력이 표시 됩니다.

    ![디렉터리 확인](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "디렉터리 확인")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>업로드 데이터 tooyour Azure 데이터 레이크 저장소
Hello 루트 수준 또는 tooa 만든 디렉터리를 hello 계정 내에서 직접 tooData 데이터 레이크 저장소에 업로드할 수 있습니다. 아래 hello 조각은 보여 방법을 tooupload 몇 가지 샘플 데이터 toohello 디렉터리 (**mynewdirectory**) hello 이전 섹션에서 만든 합니다.

몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다. Hello 파일을 다운로드 하 고 C:\sampledata\ 같은 컴퓨터에 로컬 디렉터리에 저장 합니다.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>데이터 레이크 저장소에서 데이터 이름 바꾸기, 다운로드 및 삭제
toorename 파일에 다음 명령을 사용 하 여 hello:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload 파일에 다음 명령을 사용 하 여 hello:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete 파일에 다음 명령을 사용 하 여 hello:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

메시지가 표시 되 면 입력 **Y** toodelete hello 항목입니다. 둘 이상의 파일 toodelete를 설정한 경우에 쉼표로 구분 하 여 모든 hello 경로 제공할 수 있습니다.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Azure 데이터 레이크 저장소 계정 삭제
데이터 레이크 저장소 계정 명령 toodelete 다음 hello를 사용 합니다.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

메시지가 표시 되 면 입력 **Y** toodelete hello 계정.

## <a name="performance-guidance-while-using-powershell"></a>PowerShell을 사용하는 동안 성능 지침

다음 hello 데이터 레이크 저장소와 PowerShell toowork를 사용 하는 동안 hello 최상의 성능이 튜닝된 tooget 일 수 있는 가장 중요 한 설정은 같습니다.

| 속성            | 기본값 | 설명 |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | 이 매개 변수를 업로드 하거나 다운로드 각 파일에 대 한 병렬 스레드의 toochoose hello 수가 있습니다. 이 숫자 hello 파일당 할당 될 수 있는 최대 스레드를 나타내지 않으며 해당 시나리오에 따라 덜 스레드를 발생할 수 있습니다 (예: 20 스레드에 게 요청 하는 경우에 하나의 스레드 1KB 파일을 업로드 하는 경우 얻을 수 있습니다).  |
| ConcurrentFileCount | 10      | 이 매개 변수는 특히 폴더 업로드 또는 다운로드를 위한 것입니다. 이 매개 변수는 hello 업로드 또는 다운로드 될 수 있는 동시 파일 수를 결정 합니다. 이 숫자는 hello 업로드 또는 다운로드 한 번에 수 있는 동시 파일의 최대 수를 나타내지 않으며 적은 동시성 시나리오에 따라 발생할 수 있습니다 (예: 두 개의 파일을 업로드 하는 경우에 게 요청 하는 경우에 두 개의 동시 파일 업로드 얻을 수 있습니다 15 개)입니다. |

**예제**

이 명령은 파일 및 100 개의 동시 파일 당 20 개의 스레드를 사용 하 여 Azure 데이터 레이크 저장소 toohello 사용자의 로컬 드라이브에서 파일을 다운로드 합니다.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>이러한 매개 변수에 대해 값 tooset hello를 확인 하려면 어떻게 해야 합니까?

다음은 사용할 수 있는 몇 가지 지침입니다.

* **1 단계: hello 총 스레드 수를 확인할** -계산 hello 총 스레드 수 toouse 먼저 시작 해야 합니다. 일반적으로 물리적 코어당 6개의 스레드를 사용해야 합니다.

        Total thread count = total physical cores * 6

    **예제**

    코어 16 개 있는 D14 VM에서 명령 hello PowerShell 실행

        Total thread count = 16 cores * 6 = 96 threads


* **2 단계: 계산 PerFileThreadCount** -우리의 PerFileThreadCount hello 파일의 hello 크기에 따라 계산 합니다. 파일의 2.5 g B 보다 작은 경우 없습니다 필요 toochange이 매개이 변수는 hello 기본값 10을 하기 때문에 있습니다. 2.5 g B 보다 큰 파일에 대 한 hello 자료에 대 한 첫 번째 2.5 g B hello와 파일 크기에서의 경우 256mb 이상 증가할 때마다 추가 대 한 1 개의 스레드를 추가 하는 대로 10 개 스레드를 사용 해야 합니다. 더 큰 크기의 파일 범위로 폴더를 복사하는 경우 보다 작은 파일 크기로 그룹화하는 것이 좋습니다. 다른 파일 크기를 사용하면 성능이 저하될 수 있습니다. 그렇지 않은 경우 가능한 toogroup 유사한 파일 크기, PerFileThreadCount hello 가장 큰 파일 크기에 따라 설정 해야 합니다.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **예제**

    1GB too10GB에서 이르는 100 개의 파일을 했 고, 가장 큰 hello로 10GB 파일 hello 다음과 같은 읽어오는 수식에 대 한 크기 hello를 사용 합니다.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **3 단계: 계산 ConcurrentFilecount** -수식 뒤 hello를 기반으로 사용 하 여 hello 총 스레드 수 및 PerFileThreadCount toocalculate ConcurrentFileCount 합니다.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **예제**

    사용 되 고 여기서 hello 예제 값을 기반으로

        96 = 40 * ConcurrentFileCount

    따라서 **ConcurrentFileCount** 은 **2.4**, 너무 반올림 수 우리는**2**합니다.

### <a name="further-tuning"></a>추가 조정

다양 한 파일 크기 toowork와 있기 때문에 사용자의 추가 조정 필요할 수 있습니다. 위의 계산 hello hello 파일의 전체 또는 대부분은 더 큰와 더 가깝기 때문 toohello 10GB 범위 하는 경우에 작동 합니다. 그렇지 않고 작은 파일이 많고 파일 크기가 매우 다양한 경우 PerFileThreadCount를 줄이면 됩니다. Hello PerFileThreadCount를 줄여 ConcurrentFileCount 향상 시킬 수 있습니다. 따라서이 파일의 대부분은 hello 5GB 범위에서 더 작은을 활용해 서 가정할 경우 우리는 계산 다시 수행 합니다.

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

따라서 **ConcurrentFileCount** 이제 4.8 형식인 96/20으로 반올림 됩니다 너무**4**합니다.

Hello를 변경 하 여 이러한 설정을 tootune를 계속할 수 **PerFileThreadCount** 파일 크기의 hello 분포에 따라 위와 아래로 합니다.

### <a name="limitation"></a>제한 사항

* **파일의 수를 사용 하면 ConcurrentFileCount 보다 작으면**: 업로드 하려는 파일 hello 수는 hello 보다 작은 경우 **ConcurrentFileCount** 를 계산한 다음 줄여야  **ConcurrentFileCount** toobe 같으면 toohello 파일 수입니다. 나머지 모든 스레드 tooincrease를 사용할 수 있습니다 **PerFileThreadCount**합니다.

* **너무 많은 스레드가**: 계산 클러스터 크기를 늘리지 않고도 너무 많은 스레드를 늘려야 하는 경우, 실행 하면 성능이 저하 되 hello 위험이 있습니다. CPU hello에 컨텍스트 전환 하는 경우 경합 문제 수 있습니다.

* **부족 하 여 동시성**: hello 동시성은 부족 한 경우 클러스터 너무 작을 수 있습니다. 더 많은 동시성 제공 하 여 클러스터의 노드 hello 수를 늘릴 수 있습니다.

* **제한 오류**: 동시성이 너무 높으면 제한 오류가 표시될 수 있습니다. 제한 오류를 표시 하는 경우 hello 동시성도 감소 하거나 문의 합니다.

## <a name="next-steps"></a>다음 단계
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight에 데이터 레이크 저장소 사용](data-lake-store-hdinsight-hadoop-use-portal.md)

