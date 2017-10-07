---
title: "학습 스크립트 aaaExecute Python 컴퓨터 | Microsoft Docs"
description: "Azure 기계 학습에서 Python 스크립트를 지원하는 데 기본이 되는 디자인 원칙 및 기본 사용 시나리오, 기능 및 제한 사항을 간략히 설명합니다."
keywords: "python 기계 학습, pandas, python pandas, python 스크립트, python 스크립트 실행"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Azure 기계 학습 스튜디오에서 Python 기계 학습 스크립트 실행

이 항목에서는 hello 현재 Azure 기계 학습에서 Python 스크립트 지원 기본 hello 디자인 원칙을 설명 합니다. 제공 하는 hello 주 기능도 요약 되어 포함 하 여:

- 기본 사용 시나리오 실행
- 웹 서비스에서 실험 점수 매기기
- 기존 코드 가져오기 지원
- 시각화 내보내기
- 감독 모드 기능 선택 수행
- 일부 제한 사항 파악

[Python](https://www.python.org/) 는 대부분 데이터 과학자의 hello 도구 상자에 필수적인 도구입니다. 여기에는:

* 세련되고 간결한 구문, 
* 플랫폼 간 지원, 
* 방대한 양의 강력한 라이브러리 컬렉션 및 
* 완성도 있는 개발 도구가 포함되어 있습니다. 

Python은 기계 학습 모델링에서 일반적으로 사용되는 워크플로의 다음과 같은 모든 단계에서 사용되고 있습니다.

- 데이터 수집 및 처리 
- 기능 생성
- 모델 학습 
- 모델 유효성 검사
- hello 모델 배포

Azure Machine Learning Studio에서는 기계 학습 실험의 다양한 부분에 Python 스크립트를 포함할 수 있으며, 해당 스크립트를 Microsoft Azure의 웹 서비스로 원활하게 게시할 수도 있습니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>기계 학습에서 Python 스크립트의 디자인 원칙

Azure 기계 학습 스튜디오의 기본 인터페이스 tooPython hello는 hello를 통해 [Python 스크립트 실행] [ execute-python-script] 그림 1에 표시 된 모듈입니다.

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

그림 1. hello **Python 스크립트 실행** 모듈입니다.

hello [Python 스크립트 실행] [ execute-python-script] Azure 기계 학습 스튜디오의 모듈 toothree 입력을 허용 하 고 생성 tootwo 출력 (hello 다음 섹션에서에서 설명)를 해당 R 아날로그 같은 hello [ R 스크립트 실행] [ execute-r-script] 모듈입니다. hello 실행할 Python 코드 toobe에 입력 된 특수 이라고 명명 된 매개 변수 상자 hello 진입점 함수를 호출 `azureml_main`합니다. 다음은 원칙 tooimplement이이 모듈을 사용 하는 hello 주요 디자인이입니다.

1. *Python 사용자에게 자연스러워야 합니다.* 대부분의 Python 사용자는 코드를 모듈 내의 함수로 고려합니다. 따라서 최상위 모듈에 실행 가능 문을 많이 포함하는 경우는 거의 없습니다. 결과적으로, hello 스크립트 상자도 특별 하 게 명명 된 Python 함수 변수로 사용 것과 반대로 toojust 문의 시퀀스를 합니다. hello hello 함수에서 제공 하는 개체 유형이 표준 Python 라이브러리와 같은 [팬더](http://pandas.pydata.org/) 데이터 프레임 및 [NumPy](http://www.numpy.org/) 배열입니다.
2. *로컬 및 클라우드 실행 간의 충실도가 높아야 합니다.* hello 사용 되는 백 엔드 tooexecute hello Python 코드 기반 [Anaconda](https://store.continuum.io/cshop/anaconda/), 광범위 하 게 플랫폼 간 과학 Python 배포를 사용 합니다. 가장 일반적인 Python 패키지 hello 닫기 too200 함께 제공 합니다. 따라서 데이터 과학자는 자신의 로컬 Azure Machine Learning 호환 Anaconda 환경에서 코드를 디버그하고 한정할 수 있습니다. 그런 다음 기존 개발 환경와 같은 사용 [IPython](http://ipython.org/) 노트북 또는 [Python Tools for Visual Studio](http://aka.ms/ptvs), toorun Azure ML 실험의 일환으로 합니다. hello `azureml_main` 바닐라 Python 함수 등 진입점은 * * * SDK가 설치 되어 hello 또는 Azure ML 관련 코드 없이 작성 될 수 있습니다.
3. *다른 Azure 기계 학습 모듈로 원활하게 구성할 수 있어야 합니다.* hello [Python 스크립트 실행] [ execute-python-script] 모듈에서는 입력 및 출력,으로 표준 Azure 기계 학습 데이터 집합입니다. 투명 하 고 효율적으로 hello 기본 프레임 워크는 hello Azure ML 및 Python 런타임은 연결 합니다. 따라서 Python을 기존 Azure ML 워크플로(R 및 SQLite를 호출하는 워크플로 포함)와 함께 사용할 수 있습니다. 이를 통해 데이터 과학자는 다음과 같은 워크플로를 작성할 수 있습니다.
   * 데이터 전처리 및 정리에 Python 및 Pandas를 사용하는 워크플로
   * 피드 hello 데이터 tooa SQL 변환, 여러 데이터 집합 tooform 기능 조인
   * hello 알고리즘을 사용 하 여 Azure 기계 학습에서 모델을 학습 합니다. 
   * 평가 하 고 오른쪽을 사용 하 여 hello 결과 한 후 처리


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>ML의 Python 스크립트 기본 사용 시나리오

이 섹션에서는 설문 조사 hello의 기본 용도 hello에 [Python 스크립트 실행] [ execute-python-script] 모듈입니다. 입력 toohello Python 모듈 팬더 데이터 프레임으로 노출 됩니다. hello 함수 반환 해야 합니다는 Python 안에 패키징된 단일 팬더 데이터 프레임 [시퀀스](https://docs.python.org/2/c-api/sequence.html) 튜플, 목록 또는 배열 NumPy 등입니다. 이 시퀀스의 첫 번째 요소 hello는 hello hello 모듈의 첫 번째 출력 포트에 반환 됩니다. 이 스키마는 그림 2에 표시됩니다.

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

그림 2. 매핑 포트 tooparameters 입력과 toooutput 포트 값을 반환 합니다.

더 자세한 hello 입력된 포트의 hello 매핑된 tooparameters를 얻는 방법의 의미 체계 `azureml_main` 함수 표 1에 표시 됩니다.

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

표 1. 입력된 포트 toofunction 매개 변수 매핑이 있습니다.

hello 매핑 입력된 포트 사이의 함수 매개 변수는 위치:

- hello 첫 번째 연결 된 입력된 포트는 매핑된 toohello hello 함수의 첫 번째 매개 변수입니다. 
- hello (연결) 하는 경우 두 번째 입력은 매핑된 toohello hello 함수의 두 번째 매개 변수입니다.

참조 *데이터 분석에 대 한 Python* (2012 O'Reilly) 여 서 McKinney 효과적이 고 효율적으로 사용 되는 toomanipulate 데이터 수 있습니다 어떻게 및 Python 팬더에 자세한 내용은 합니다. 


## <a name="translation-of-input-and-output-types"></a>입력 및 출력 유형 변환 
Azure 기계 학습에서 입력된 데이터 집합은 팬더에서 변환 된 toodata 프레임입니다. 출력 데이터 프레임 백 tooAzure 기계 학습 데이터 집합을 변환 됩니다. 변환을 수행 하는 hello 수행 됩니다.

1. 문자열 및 숫자 열으로 변환 됩니다-이 데이터 집합에서 누락 된 값은 변환 된 too'NA' 팬더의 값입니다. hello 동일한 변환이 발생 하는 방식으로 다시 hello에 (팬더에 NA 값은 Azure ML에서 변환 된 toomissing 값).
2. Pandas의 인덱스 벡터는 Azure ML에서 지원되지 않습니다. 모든 입력된 데이터 프레임 hello Python 함수에는 항상 0 toohello 행 수-1에서에서 64 비트 숫자 인덱스를 가집니다. 
3. Azure ML 데이터 집합에는 중복된 열 이름과 문자열이 아닌 열 이름이 있을 수 없습니다. 출력 데이터 프레임에 숫자가 아닌 열이 포함 된 경우 프레임 워크 호출 hello `str` hello 열 이름에서. 마찬가지로, 자동으로 바뀐된 tooinsure는 모든 중복 열 이름을 hello 이름이 고유한 지 합니다. hello 접미사 (2) toohello 첫 번째 중복, (3) toohello 두 번째 중복 및에 추가 됩니다.


## <a name="operationalizing-python-scripts"></a>Python 스크립트 운영 가능화

점수 매기기 실험에서 모든 [Python 스크립트 실행][execute-python-script] 모듈은 웹 서비스로 게시될 때 호출됩니다. 예를 들어 그림 3은 hello 코드 tooevaluate 단일 Python 식을 포함 하는 점수 매기기 실험을 나타냅니다. 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

그림 3. Python 식을 평가하기 위한 웹 서비스입니다.

이 실험에서 작성된 웹 서비스는 다음을 수행합니다.

- Python 식(문자열)을 입력으로 사용
- toohello Python 인터프리터를 보냅니다. 
- hello 식과 hello 평가 결과 모두 포함 하는 테이블을 반환 합니다.


## <a name="importing-existing-python-script-modules"></a>기존 Python 스크립트 모듈 가져오기

대부분 데이터 과학자에 대 한 일반적인 사용 사례 tooincorporate Azure 기계 학습 실험에 기존 Python 스크립트입니다. 모든 코드를 연결 하 고 단일 스크립트 상자에 붙여넣을 수 않아도 hello [Python 스크립트 실행] [ execute-python-script] 모듈 hello 세 번째 입력 포트 Python 모듈을 포함 하는 zip 파일을 수락 합니다. 런타임 시 hello 실행 프레임 워크에 의해 hello 파일 압축을 푼 및 hello 내용이 hello Python 인터프리터의 toohello 라이브러리 경로 추가 됩니다. hello `azureml_main` 진입점 함수 이러한 모듈을 직접 가져올 다음 수 있습니다.

예를 들어 hello 파일을 Hello.py 간단한 "Hello, World" 함수를 포함 하는 것이 좋습니다.

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

그림 4. Hello.py 파일의 사용자 정의 함수

다음으로 Hello.py을 포함하는 Hello.zip이라는 파일을 만듭니다.

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

그림 5. 사용자 정의 Python 코드가 포함된 Zip 파일.

Azure 기계 학습 스튜디오에 데이터 집합으로 hello zip 파일을 업로드 합니다. 그런 다음 만들고 toohello hello의 세 번째 입력된 포트를 연결 하 여 hello Hello.zip 파일에 hello Python 코드를 사용 하는 실험을 실행할 **Python 스크립트 실행** 이 그림에 표시 된 것과 같이 모듈입니다.

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

그림 6. zip 파일로 업로드된 사용자 정의 Python 코드를 사용하는 샘플 실험.

해당 hello zip 파일을 패키지에 포함 된 되었습니다 hello 모듈 출력에 표시 하 고 해당 hello 함수 `print_hello` 를 실행 합니다.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

그림 7. 사용자 정의 함수가 사용 hello 내 [Python 스크립트 실행] [ execute-python-script] 모듈입니다.


## <a name="working-with-visualizations"></a>시각화 작업

Hello에서 시각화할 수 MatplotLib를 사용 하 여 hello 브라우저에 생성 된 플롯을 반환할 수 [Python 스크립트 실행][execute-python-script]합니다. 하지만 hello 점도 없는 자동으로 리디렉션된 tooimages 오른쪽을 사용 하는 것 처럼 Hello 사용자 명시적으로 파일 저장 해야 모든 점도 tooPNG 있더라도 하므로 toobe 백 tooAzure 기계 학습을 반환 합니다. 

MatplotLib에서 toogenerate 이미지 hello 절차를 완료 해야 합니다.

* hello 백 엔드 전환 너무 "AGG" hello에서 기본 하 기반 렌더러 
* 새 그림 개체 만들기 
* hello 축 및 것에 모든 표와 예측치를 생성 합니다. 
* hello 그림 tooa PNG 파일 저장 

그림 8 hello scatter_matrix 함수를 사용 하 여 팬더에는 산 점도 행렬을 만드는 다음 hello이이 과정을 보여 줍니다.

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

그림 8. MatplotLib 그림 tooimages toosave 코드.

그림 9 tooreturn 점도 hello 두 번째 출력 포트를 통해 이전에 표시 된 hello 스크립트를 사용 하는 실험을 보여줍니다.

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

그림 9. Python 코드에서 생성된 그림 시각화.

가능한 tooreturn 여러 그림 서로 다른 이미지를 저장 하 여, 모든 이미지를 Azure 기계 학습 런타임 선택 hello 사용 되며 시각화에 대 한이 연결 합니다.


## <a name="advanced-examples"></a>고급 예제

Azure 기계 학습에 설치 된 hello Anaconda 환경을 NumPy, SciPy, 및 Scikits-설명 등의 일반적인 패키지를 포함 합니다. 이러한 패키지는 기계 학습 파이프라인의 여러 데이터 처리 작업에 효율적으로 사용할 수 있습니다. 예를 들어 hello 다음 실험 및 스크립트 설명 Scikits 배우기 toocompute 기능 중요도 점수에 앙상블 학습자의 데이터 집합에 대 한 hello를 사용 합니다. hello 점수는 다른 ML 모델 공급 하기 전에 사용 되는 tooperform 감독 기능 선택 될 수 있습니다.

Hello Python 사용 되는 함수 toocompute hello 중요도 점수와 hello 점수를 기준으로 순서 hello 기능 다음과 같습니다.

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

그림 10. 기능 점수 여 toorank 기능입니다.
 hello 다음 실험 다음을 계산 하 고 Azure 기계 학습에서 hello "Pima 인도양 식이 조절" 데이터 집합의 기능 hello 중요도 점수를 반환 합니다.

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

그림 11. Hello Pima 인도양 식이 조절 데이터 집합의 실험 toorank 기능입니다.

## <a name="limitations"></a>제한 사항
hello [Python 스크립트 실행] [ execute-python-script] 현재 다음과 같은 제한을 hello에:

1. *샌드박스 실행.* hello Python 런타임의 현재 보안으로 보호 하 고 결과적으로,을 영구적으로 액세스 toohello 네트워크나 toohello 로컬 파일 시스템을 허용 하지 않습니다. 로컬에 저장 하는 모든 파일 격리 되며 hello 모듈 완료 되 면 삭제 됩니다. hello Python 코드에서 실행 하는 hello 컴퓨터에서 대부분의 디렉터리에 액세스할 수 없습니다, 그리고 현재 디렉터리와 하위 디렉터리 hello hello 예외 되 고 있습니다.
2. *정교한 개발 및 디버깅 지원이 부족합니다.* 현재 hello Python 모듈은 intellisense 및 디버깅 같은 IDE 기능을 지원 하지 않습니다. 또한 런타임 시 hello 모듈이 실패할 경우 hello 전체 Python 스택 추적 ´ ù. 하지만 hello 모듈에 대 한 hello 출력 로그에서 볼 수 있어야 합니다. 개발 및 IPython 등의 환경에서 Python 스크립트를 디버그할 하 hello 모듈에 hello 코드를 가져온 다음 현재 권장 합니다.
3. *단일 데이터 프레임 출력.* hello Python 되는 허용 된 tooreturn 단일 데이터 프레임을 출력으로. 현재는 가능 tooreturn 임의의 Python 학습 된 모델에는 직접 toohello Azure 기계 학습 런타임 다시와 같은 개체는 없습니다. 와 같은 [R 스크립트 실행][execute-r-script], hello가 같은 제한 사항이 것은 바이트에 toopickle 개체 배열 및 다음 데이터 프레임 내에서 반환 하는 대부분의 경우에 가능 합니다.
4. *Python 설치 불가능 toocustomize*합니다. 현재 hello 방법은 tooadd 사용자 지정 Python 모듈에만 앞에서 설명한 hello zip 파일 메커니즘을 통해. 이 방법은 작은 모듈의 경우 가능하지만, 모듈이 크거나(특히 네이티브 DLL이 있는 모듈) 모듈 수가 많은 경우 번거로울 수 있습니다. 

## <a name="conclusions"></a>결론
hello [Python 스크립트 실행] [ execute-python-script] 모듈을 사용 하면 데이터 과학자 tooincorporate 기존 Python 코드를 Azure 기계 학습 및 tooseamlessly 학습 워크플로에 클라우드에서 호스팅하는 컴퓨터 웹 서비스의 일부분으로 운영 화 합니다. Azure 기계 학습의 다른 모듈와 hello Python 스크립트 모듈 자연스럽 게 상호 운용 합니다. 데이터 탐색 toopre 처리 및 기능 추출 / tooevaluation 작업의 범위 및 hello 결과의 사후 처리에 대 한 hello 모듈을 사용할 수 있습니다. 실행을 위해 사용 되는 hello 백 엔드 런타임 Anaconda, 충분 한 테스트를 널리 사용 되는 Python 배포를 기반으로 합니다. 이 백 엔드 쉽게 있습니다 tooon 보드 기존 코드 자산에 대 한 hello 클라우드로 있습니다.

추가 기능 toohello tooprovide 것으로 예상 [Python 스크립트 실행] [ execute-python-script] 기능 tootrain hello 및 Python에서 모델을 운용와 같은 모듈 및 tooadd hello에 대 한 지원 향상 개발 및 Azure 기계 학습 스튜디오에서 코드를 디버깅 합니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [Python 개발자 센터](https://azure.microsoft.com/develop/python/)합니다.

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
