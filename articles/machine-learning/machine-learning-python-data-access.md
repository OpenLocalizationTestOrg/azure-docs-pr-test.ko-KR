---
title: "기계 학습 Python 클라이언트 라이브러리와 함께 데이터 집합 aaaAccess | Microsoft Docs"
description: "설치 및 Python 클라이언트 라이브러리 tooaccess hello 사용 하 여 로컬 Python 환경에서 Azure 기계 학습 데이터를 안전 하 게 관리 합니다."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Hello Azure 기계 학습 Python 클라이언트 라이브러리를 사용 하 여 Python으로 데이터 집합 액세스
Microsoft Azure 기계 학습 Python 클라이언트 라이브러리의 hello 미리 보기는 보안 액세스 tooyour 로컬 Python 환경에서 Azure 기계 학습 데이터 집합을 사용 하도록 설정할 수 하 고 작업 영역에서 데이터 집합의 hello 생성 및 관리를 활성화 합니다.

이 항목에서는 다음 수행 방법에 대한 지침을 제공합니다.

* hello 기계 학습 Python 클라이언트 라이브러리를 설치 합니다. 
* 액세스 방법에 대 한 지침을 포함 하 여 데이터 집합을 업로드 하 고 tooget 권한 부여 tooaccess 로컬 Python 환경에서 Azure 기계 학습 데이터 집합
* 실험에서 중간 데이터 집합에 액세스
* hello Python 클라이언트 라이브러리 tooenumerate 데이터 집합을 사용 하 여, 메타 데이터에 액세스, 데이터 집합의 hello 내용의 읽을, 새 데이터 집합을 만들 및 기존 데이터 집합 업데이트

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>필수 조건
hello Python 클라이언트 라이브러리 hello 다음 환경에서 테스트 되었습니다.

* Windows, Mac 및 Linux
* Python 2.7, 3.3 및 3.4

Hello 다음 패키지에 종속 되어:

* requests
* python-dateutil
* pandas

와 같은 Python 배포를 사용 하는 것이 좋습니다 [Anaconda](http://continuum.io/downloads#all) 또는 [Canopy](https://store.enthought.com/downloads/), python, IPython 나오는 및 위에 나열 된 3 hello 패키지 설치 합니다. IPython은 반드시 필요하지는 않지만 데이터를 대화식으로 조작하고 시각화는 데 훌륭한 환경입니다.

### <a name="installation"></a>어떻게 tooinstall hello Azure 기계 학습 Python 클라이언트 라이브러리
hello Azure 기계 학습 Python 클라이언트 라이브러리는이 항목에 설명 된 설치 된 toocomplete hello 작업 이어야 합니다. Hello에서 다운로드할 수 [Python 패키지 인덱스](https://pypi.python.org/pypi/azureml)합니다. Python 환경에서 실행 tooinstall 다음 로컬 Python 환경에서 명령을 hello:

    pip install azureml

다운로드 하 고 hello 원본에서의 설치 수 또는 [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python)합니다.

    python setup.py install

Git 컴퓨터에 설치 되어 있는 경우 pip tooinstall hello git 리포지토리에서 직접 사용할 수 있습니다.

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Studio 코드 조각 tooaccess 데이터 집합 사용
hello Python 클라이언트 라이브러리 실행 된 실험에서 프로그래밍 방식 액세스 tooyour 기존 데이터 집합을 제공 합니다.

Hello Studio 웹 인터페이스에서 모든 hello 필요한 정보 toodownload가 포함 된 데이터 집합 위치 컴퓨터에 팬더 데이터 프레임 개체로 deserialize 하는 코드 조각을 생성할 수 있습니다.

### <a name="security"></a>데이터 액세스를 위한 보안
hello Python 클라이언트 라이브러리와 함께 사용 하 여 작업 영역 id 및 권한 부여 포함 Studio에서 제공 하는 코드 조각 hello 토큰입니다. 이러한 모든 권한 tooyour 작업 영역을 제공 하 고는 암호와 같은 보호 되어야 합니다.

보안상의 이유로 hello 코드 조각 기능은만 해당 역할이으로 설정 되어 사용할 수 있는 toousers **소유자** hello 작업 영역에 대 한 합니다. Hello에 Azure 기계 학습 스튜디오에 사용자 역할이 표시 **사용자** 페이지 **설정을**합니다.

![보안][security]

역할으로 설정 되어 있지 않으면 **소유자**는 소유자로 reinvited toobe 요청 하거나 작업 영역 tooprovide hello의 hello 소유자에 게 hello 코드 조각으로 있습니다.

tooobtain hello 권한 부여 토큰 hello 다음 중 하나를 수행할 수 있습니다.

* 소유자에서 토큰을 요청합니다. 소유자가 작업 영역 Studio에서의 hello 설정 페이지에서 해당 권한 부여 토큰을 액세스할 수 있습니다. 선택 **설정** hello 왼쪽 창에서 데이터 및 클릭에서에서 **권한 부여 토큰** toosee hello 기본 및 보조 토큰입니다.  기본 hello 또는 hello 보조 권한 부여 토큰 사용할 수 있지만 hello 코드 조각에, 소유자만 hello 보조 권한 부여 토큰을 공유 하는 것이 좋습니다.

![권한 부여 토큰](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* 승격 toobe toorole 소유자에 게 요청 합니다.  toodo이 hello 작업 영역 요구 toofirst의 현재 소유자 hello 작업 영역에서 제거 하면 다음 다시 초대 하거나 소유자로 tooit 합니다.

개발자가 얻은 hello 작업 영역 id 및 권한 부여 되 면 토큰을 서로 수 tooaccess hello 역할에 관계 없이 hello 코드 조각을 사용 하 여 작업 영역입니다.

Hello에 관리 되는 권한 부여 토큰 **권한 부여 토큰** 페이지 **설정을**합니다. 다시 생성할 수 있지만이 절차 액세스 toohello 이전 토큰을 취소 합니다.

### <a name="accessingDatasets"></a>로컬 Python 응용 프로그램에서 데이터 집합에 액세스
1. 기계 학습 스튜디오에서 클릭 **데이터 집합** hello hello 왼쪽 탐색 모음에서.
2. Tooaccess 원하는 hello 데이터 집합을 선택 합니다. Hello에서 hello 데이터 집합 중 하나를 선택할 수 있습니다 **내 데이터 집합** 목록 또는 hello **샘플** 목록입니다.
3. Hello 아래쪽 도구 모음에서 클릭 **데이터 액세스 코드 생성**합니다. Hello 데이터가 hello Python 클라이언트 라이브러리와 호환 되지 않는 형식 이면이 단추가 비활성화 됩니다.
   
    ![데이터 집합][datasets]
4. Hello 코드 조각 표시 되는 hello 창에서 선택한 tooyour 클립보드로 복사 합니다.
   
    ![액세스 코드][dataset-access-code]
5. 로컬 Python 응용 프로그램의 hello 노트북에 hello 코드를 붙여 넣습니다.
   
    ![노트북][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>기계 학습 실험에서 중간 데이터 집합에 액세스
실험을 hello 기계 학습 스튜디오에서에서 실행 가능한 tooaccess hello 중간에서 데이터 집합 hello 출력 노드 모듈의 파일은입니다. 중간 데이터 집합은 모델 도구가 실행될 때 중간 단계를 위해 생성되고 사용된 데이터입니다.

중간 데이터 집합이 hello 데이터 형식은 hello Python 클라이언트 라이브러리와 호환으로 액세스할 수 있습니다.

hello 다음과 같은 형식이 지원 됩니다 (hello에 이러한 상수는 `azureml.DataTypeIds` 클래스).

* 일반 텍스트
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

모듈 출력 노드 위로 이동 하 여 hello 형식을 확인할 수 있습니다. 도구 설명에 hello 노드 이름과 함께 표시 됩니다.

Hello 같은 hello 모듈의 일부 [분할] [ split] 모듈, 명명 된 출력 tooa 형식 `Dataset`, hello Python 클라이언트 라이브러리에서 지원 되지 않습니다.

![데이터 집합 형식][dataset-format]

같은 toouse 변환 모듈이 필요 [tooCSV 변환][convert-to-csv], tooget 지원 되는 형식으로 출력 합니다.

![GenericCSV 형식][csv-format]

hello 다음 단계는 보여 주는 예제는 실험을 만들고 실행를 hello 중간 데이터 집합에 액세스 하는 합니다.

1. 새로운 실험 만들기
2. **성인 인구 조사 소득 이진 분류 데이터 집합** 모듈을 삽입합니다.
3. 삽입 한 [분할] [ split] 모듈 toohello 입력된 데이터 집합 모듈 출력을 연결 합니다.
4. 삽입 한 [tooCSV 변환] [ convert-to-csv] 모듈의 hello 해당 입력된 tooone 연결 [분할] [ split] 모듈의 출력입니다.
5. Hello 실험을 저장 하 고 실행 될 때까지 기다렸다가 toofinish 실행 합니다.
6. Hello에 hello 출력 노드를 클릭 [tooCSV 변환] [ convert-to-csv] 모듈입니다.
7. Hello 상황에 맞는 메뉴에 표시 되 면 선택 **데이터 액세스 코드 생성**합니다.
   
    ![상황에 맞는 메뉴][experiment]
8. Hello 코드 조각 선택에서 나타나는 hello 창 tooyour 클립보드를 복사 합니다.
   
    ![액세스 코드][intermediate-dataset-access-code]
9. 전자 필기장의 hello 코드를 붙여 넣습니다.
   
    ![노트북][ipython-intermediate-dataset]
10. Matplotlib를 사용 하 여 hello 데이터를 시각화할 수 있습니다. 그러면 hello 나가 열에 대 한 히스토그램에 표시 됩니다.
    
    ![히스토그램][ipython-histogram]

## <a name="clientApis"></a>기계 학습 Python 클라이언트 라이브러리 tooaccess hello를 사용 하 여, 읽기, 작성 및 데이터 집합 관리
### <a name="workspace"></a>작업 영역
hello 작업 영역은 hello hello Python 클라이언트 라이브러리에 대 한 진입점입니다. Hello 제공 `Workspace` 클래스에 작업 영역 id 및 권한 부여 토큰 toocreate와 인스턴스:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>데이터 집합 열거
tooenumerate 지정된 된 작업 영역에서 모든 데이터 집합.

    for ds in ws.datasets:
        print(ds.name)

tooenumerate 정당한 hello 사용자가 만든 데이터 집합:

    for ds in ws.user_datasets:
        print(ds.name)

tooenumerate 정당한 hello 예제 데이터 집합:

    for ds in ws.example_datasets:
        print(ds.name)

데이터 집합 이름(대/소문자 구분)으로 액세스할 수 있습니다.

    ds = ws.datasets['my dataset name']

또는 인덱스별로 액세스할 수 있습니다.

    ds = ws.datasets[0]


### <a name="metadata"></a>Metadata
메타 데이터를 추가 toocontent에 있어야 하는 데이터 집합. (중간 데이터 집합 예외 toothis 규칙은 및 메타 데이터에는 필요가 없습니다.)

일부 메타 데이터 값은 생성 시 hello 사용자가 할당 됩니다.

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

다른 메타 데이터 값은 Azure 기계 학습에서 할당:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Hello 참조 `SourceDataset` 자세한 on hello 사용 가능한 메타 데이터에 대 한 클래스입니다.

### <a name="read-contents"></a>콘텐츠 읽기
자동으로 기계 학습 스튜디오에서 제공 하는 hello 코드 조각 다운로드 하 여 hello dataset tooa 팬더 데이터 프레임 개체를 역직렬화 합니다. Hello로 이렇게 `to_dataframe` 메서드:

    frame = ds.to_dataframe()

Toodownload hello 원시 데이터를 선호 하 고 직접 hello deserialization을 수행 하는 옵션입니다. Hello 순간에 상위 hello Python 클라이언트 라이브러리를 역직렬화 할 수 없습니다 'ARFF' 등의 형식에 대 한 hello 유일한 옵션입니다.

텍스트로 tooread hello 내용:

    text_data = ds.read_as_text()

이진으로 tooread hello 내용:

    binary_data = ds.read_as_binary()

클릭할 수도 스트림 toohello 내용을 열 수 있습니다.

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>새 데이터 집합 만들기
hello Python 클라이언트 라이브러리에서는 Python 프로그램에서 tooupload 데이터 집합이 있습니다. 이러한 데이터 집합은 작업 영역에서 사용할 수 있습니다.

데이터 팬더 데이터 프레임에 있으면 코드 다음 hello를 사용 합니다.

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

데이터가 이미 직렬화된 경우 다음을 사용할 수 있습니다.

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

hello Python 클라이언트 라이브러리는 팬더 데이터 프레임 toohello 다음 서식을 지정 하는 수 tooserialize (hello에 이러한 상수는 `azureml.DataTypeIds` 클래스).

* 일반 텍스트
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>기존 데이터 집합 업데이트
기존 데이터 집합을 일치 하는 이름 가진 새 데이터 집합을 tooupload 하려고 하면 충돌 오류를 가져와야 합니다.

기존 데이터 집합 tooupdate 먼저 tooget 참조 toohello 기존 데이터 집합.

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

다음 사용 하 여 `update_from_dataframe` Azure의 hello 데이터 집합의 tooserialize 및 바꾸기 hello 내용을:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Tooserialize hello 데이터 tooa 서로 다른 서식을 지정 하려는 경우 선택적 hello에 대 한 값을 지정 합니다. `data_type_id` 매개 변수입니다.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Hello에 대 한 값을 지정 하 여 새 설명을 선택적으로 설정할 수 있습니다 `description` 매개 변수입니다.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

Hello에 대 한 값을 지정 하 여 새 이름을 지정할 수도 있습니다 `name` 매개 변수입니다. 이제 새 이름만 hello를 사용 하 여 hello 데이터 집합을 얻을 수 있습니다. hello 코드 다음에 hello 데이터, 이름 및 설명을 업데이트 합니다.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

hello `data_type_id`, `name` 및 `description` 매개 변수는 선택 사항이 며 기본 tootheir 이전 값입니다. hello `dataframe` 매개 변수는 항상 있어야 합니다.

데이터가 이미 직렬화된 경우 `update_from_dataframe` 대신 `update_from_raw_data`를 사용합니다. `dataframe` 대신 `raw_data`만 전달하면, 비슷하게 작동합니다.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

