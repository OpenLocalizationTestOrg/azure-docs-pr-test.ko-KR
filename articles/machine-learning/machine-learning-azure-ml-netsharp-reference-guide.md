---
title: "Net # 신경망 사양 언어 aaaGuide toohello | Microsoft Docs"
description: "구문은 hello Net # 신경망 사양 언어 Net #을 사용 하 여 Microsoft Azure 기계 학습에서 사용자 지정 신경망 toocreate 모델링 하는 방법의 예제와 함께 네트워크"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Azure 기계 학습에 대 한 tooNet # 신경망 사양 언어 가이드
## <a name="overview"></a>개요
Net # 신경망 아키텍처를 사용 하는 toodefine은 Microsoft에서 개발 된 언어입니다. Microsoft Azure Machine Learning의 신경망 모듈에서 Net#을 사용할 수 있습니다.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

이 문서에서는 기본 개념 필요한 사용자 지정 신경망 toodevelop 배웁니다. 

* 신경망 요구 사항과 어떻게 toodefine hello 기본 구성 요소
* hello 구문 및 hello Net # 사양 언어의 키워드
* Net#을 사용하여 만든 사용자 지정 신경망의 예 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>신경망 기본 사항
신경망 구조 이루어져 ***노드*** 에 구성 된 ***레이어***, 및가 중 ***연결*** (또는 ***가장자리***) 사이 hello 노드입니다. hello 연결은 방향이 고 각 연결에는 ***소스*** 노드 및 ***대상*** 노드.  

각 ***학습 가능한 계층***(숨겨진 계층 또는 출력 계층)에는 하나 이상의 ***연결 번들***이 있습니다. 연결 번들 소스 계층 및 해당 원본 계층에서 hello 연결에 대 한 사양으로 구성 됩니다. 지정 된 번들 공유에 있는 모든 hello 연결 hello 동일 ***소스 계층*** 동일 hello 및 ***대상 계층***합니다. Net # 연결 번들 속하는 toohello 번들 대상 계층으로 간주 됩니다.  

Net # 다양 한 종류의 지원 연결 번들 입력은 매핑된 toohidden 레이어 hello 방법을 사용자 지정할 수 있습니다 하 고 매핑된 toohello 출력 합니다.   

hello 기본 또는 표준 번들은 **전체 번들**, hello의 각 노드를 소스 계층은 hello 대상 계층의 연결 된 tooevery 노드입니다.  

또한, Net # 지원 다음 네 가지 유형의 고급 연결 번들 hello:  

* **필터링된 번들**. hello 사용자는 원본 계층 노드 hello 및 hello 대상 계층 노드의 hello 위치를 사용 하 여 조건자를 정의할 수 있습니다. 노드는 hello 조건자가 True 때마다 연결 됩니다.
* **나선형 번들**. hello 사용자 hello 원본 계층의 노드는 작은 공간을 정의할 수 있습니다. Hello 대상 계층의 각 노드는 hello 원본 계층에 있는 노드의 연결 된 tooone 환경입니다.
* **풀링 번들** 및 **응답 정규화 번들**. 이러한은 유사한 tooconvolutional 번들 해당 hello에 사용자는 작은 공간에서 hello 원본 계층의 노드를 정의 합니다. hello 차이점은 이러한 번들에 hello 지 hello 가중치 트레인 할 수 있는 하지 않는다는 것입니다. 미리 정의 된 함수를 적용 하는 대신, toohello 소스 노드에서 값 toodetermine hello 대상 노드 값입니다.  

Net #을 사용 하 여 toodefine hello 구조는 신경망의를 사용 가능한 toodefine 심층 신경망 또는 tooimprove 학습 이미지, 오디오 또는 비디오와 같은 데이터에 대해 알려진 임의의 차원의 나선 같은 복잡 한 구조입니다.  

## <a name="supported-customizations"></a>지원되는 사용자 지정
Azure 기계 학습에서 만드는 신경망 모델의 hello 아키텍처 Net #을 사용 하 여 광범위 하 게 사용자 지정할 수 있습니다. 다음을 수행할 수 있습니다.  

* 각 계층의 제어 hello 노드 수 및 숨겨진된 계층을 만듭니다.
* 계층의 다른 연결 toobe tooeach는 방법을 지정 합니다.
* 나선 및 가중 공유 번들과 같은 특수 연결 구조를 정의합니다.
* 여러 가지 활성화 함수를 지정합니다.  

Hello 사양 언어 구문의 자세한 참조 [구조 사양](#Structure-specifications)합니다.  

신경망 학습 단면 toocomplex에서 작업을 몇 가지 일반적인 컴퓨터에 대 한 정의의 예제 참조 [예제](#Examples-of-Net#-usage)합니다.  

## <a name="general-requirements"></a>일반 요구 사항
* 정확히 출력 계층 1개, 입력 계층 1개 이상, 숨겨진 계층 0개 이상이 있어야 합니다. 
* 각 계층에는 개념적으로 임의 차원의 사각형 배열로 정렬된 고정된 수의 노드가 있습니다. 
* 입력된 레이어 관련 학습 된 매개 변수 및 인스턴스 데이터는 hello 네트워크를 저장 하는 hello 요소를 나타냅니다. 
* 트레인 할 수 있는 계층 (숨겨진 계층과 출력 계층 hello) 가중치 및 편향 라는 학습 된 매개 변수를 연결 합니다. 
* hello 소스 노드와 대상 노드는 별도 계층에 있어야 합니다. 
* 연결 된 비순환; 수 있어야 합니다. 즉, 체인 연결 백 toohello 초기 소스 노드 앞에 있을 수 없습니다.
* hello 출력 계층 연결 번들의 소스 계층 일 수 없습니다.  

## <a name="structure-specifications"></a>구조 사양
세 가지 섹션으로 구성 된 신경망 구조 사양: hello **상수 선언**, hello **선언 레이어**, hello **연결 선언**합니다. 또한 선택적 **공유 선언** 섹션도 있습니다. hello 섹션은 순서에 관계 없이 지정할 수 있습니다.  

## <a name="constant-declaration"></a>상수 선언
상수 선언은 선택 사항입니다. Hello 신경망 정의에서 다른 위치에서 사용 되는 값은 toodefine 제공 합니다. 선언문 hello 식별자 뒤에 등호와 값 식으로 구성 됩니다.   

문 다음 hello 상수를 정의 하는 예를 들어 **x**:  

    Const X = 28;  

toodefine 동시에 둘 이상의 상수 hello 식별자 이름 및 값을 중괄호로 묶습니다 및 세미콜론을 사용 하 여 구분 합니다. 예:  

    Const { X = 28; Y = 4; }  

각 대입 식의 오른쪽 hello 정수, 실수, 부울 값 (True 또는 False) 또는 수학 식 수 있습니다. 예:  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>계층 선언
hello 레이어 선언이 필요 합니다. Hello 크기 및 해당 연결 번들와 특성을 포함 하 여 hello 계층의 소스를 정의 합니다. 선언 문 hello 계층 (입력, 숨겨진 경우 또는 출력)의 hello 이름 시작 하 고 hello, hello 계층 (양의 정수 튜플)의 hello 차원 차례로 나옵니다. 예:  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* hello 차원의 hello 제품 hello 계층의 노드 hello입니다. 이 예제는 hello 계층에는 100 노드가 즉 두 개의 차원 [5,20]입니다.
* 그러나 예외적으로 임의의 순서로 hello 레이어를 선언할 수 있습니다: 선언 된 hello 순서에 hello 입력된 데이터의 기능 hello 순서와 일치 해야 하나 이상의 입력된 레이어 정의 된 경우.  

hello는 계층의 노드 수는 toospecify 자동으로 사용 하 여 hello 결정 **자동** 키워드입니다. hello **자동** 키워드 hello 계층에 따라 다양 한 효과 가집니다.  

* 입력된 계층 선언에서 hello 노드 수는 hello 입력된 데이터에서 기능 hello 수가입니다.
* 숨겨진된 계층 선언에서 hello 노드 수입니다. hello에 대 한 hello 매개 변수 값으로 지정 된 **숨겨진 노드의 수**합니다. 
* 출력 계층 선언에 hello 노드 수는 2 클래스 분류와 회귀를과 같은 toohello 다중 클래스 분류에 대 한 출력 노드 수가 1 2입니다.   

예를 들어 hello 다음 네트워크 정의 사용 하면 자동으로 결정 하는 모든 계층 toobe의 hello 크기:  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


트레인 할 수 있는 계층에 대 한 레이어 선언 (숨겨진 또는 출력 계층 hello) hello 출력 함수 (활성화 함수 라고도 함) 너무 기본값으로 사용 하는 선택적으로 포함할 수**시그모이드** 분류 모델 및 **선형** 회귀 모델에 대 한 합니다. (Hello 기본값을 사용 하는 경우에 명시적으로 명시할 수 hello 활성화 함수 쉽게 구별할 수 있도록 원하는 경우.)

hello 다음과 같은 출력 함수 지원 됩니다.  

* sigmoid
* linear
* softmax
* rlinear
* square
* sqrt
* srlinear
* abs
* tanh 
* brlinear  

선언 뒤 hello hello를 사용 하는 예를 들어 **softmax** 함수:  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>연결 선언
Hello 트레인 할 수 있는 계층을 정의한 후 즉시 정의한 hello 계층 간 연결을 선언 해야 합니다. hello 연결 번들 선언 hello 키워드로 시작 **에서**고 hello 번들의 원본 계층 및 hello 종류의 연결 번들 toocreate hello 이름이 옵니다.   

현재 다음 5가지 연결 번들이 지원됩니다.  

* **전체** hello 키워드로 표시 된 번들 **모든**
* **필터링** hello 키워드로 표시 된 번들 **여기서**, 조건자 식
* **Convolutional** hello 키워드로 표시 된 번들 **convolve**, hello 회선 특성
* **풀링** hello 키워드로 표시 된 번들 **풀 max** 또는 **풀을 의미 합니다.**
* **응답 정규화** hello 키워드로 표시 된 번들 **응답 norm**      

## <a name="full-bundles"></a>전체 번들
전체 연결 번들에서 각 노드의 연결 hello 소스 레이어 tooeach hello 대상 계층의 노드를 포함합니다. 이것이 hello 기본 네트워크 연결 유형입니다.  

## <a name="filtered-bundles"></a>필터링된 번들
필터링된 연결 번들 사양은 구문상 C# 람다 식과 훨씬 비슷하게 표현된 조건자를 포함합니다. hello 다음 예제에서는 두 가지 필터링 된 번들:  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* 에 대 한 hello 조건자에서 *ByRow*, **s** hello 입력된 계층의 노드 hello 사각형 배열로 인덱스를 나타내는 매개 변수는 *픽셀*, 및 **d**  hello 숨겨진된 계층의 노드 hello 배열로 인덱스를 나타내는 매개 변수는 *ByRow*합니다. 두 유형의 hello **s** 및 **d** 길이의 두 정수의 튜플입니다. 개념적으로 **s**는 *0 <= s[0] < 10* 및 *0 <= s[1] < 20* 조건의 모든 정수 쌍을 포함하고 **d**는 *0 <= d[0] < 10* 및 *0 <= d[1] < 12* 조건의 모든 정수 쌍을 포함합니다. 
* Hello 조건자 식의 오른쪽을 hello에 상태. 모든 값에 대 한이 예에서 **s** 및 **d** hello 조건이 True 이면 되도록 hello 소스 노드에서 계층 노드 toohello 대상 계층 형성 됩니다. 따라서이 필터 식은 해당 hello 번들 포함 하 여 정의 된 hello 노드에서 연결을 나타냅니다 **s** 정의한 toohello 노드 **d** 여기서 s [0]는 [0] 같으면 tood 모든 경우에 합니다.  

선택적으로 필터링된 번들의 가중치 집합을 지정할 수 있습니다. hello에 대 한 값을 hello **가중치** 특성에는 부동 소수점 값 길이가 hello 번들에서 정의 된 연결의 hello 번호와 일치 하는 tuple 이어야 합니다. 기본적으로 가중치는 임의로 생성됩니다.  

가중치 값 hello 대상 노드 인덱스 별로 그룹화 됩니다. Hello 첫 번째 대상 노드가 연결 된 경우 걸린 소스 노드, 즉 먼저 hello *K* hello 요소의 **가중치** 튜플은 hello 첫 번째 대상 노드를 소스 인덱스 순서에서에 대 한 hello 가중치입니다. hello에 대 한 나머지 대상 노드에서 hello에도 마찬가지입니다.  

가능한 toospecify 가중치 프로토콜은 상수 값으로 직접 합니다. 예를 들어 hello 가중치를 이전에 배운 경우이 구문을 사용 하 여 상수로 지정할 수 있습니다.

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>나선형 번들
Hello 학습 데이터의 구조는 유형이 같은, 자주 사용 되는 toolearn hello 데이터의 상위 수준 기능 convolutional 연결 됩니다. 예를 들어 이미지, 오디오 또는 비디오 데이터에서 공간 또는 임시 차원은 상당히 균일할 수 있습니다.  

Convolutional 번들 채택 사각형 **커널** hello 차원을 통해 밀어는입니다. 각 커널 공간에서 로컬, 참조 tooas에 적용 된 가중치의 집합을 정의 하는 기본적으로, **커널 응용 프로그램**합니다. 참조 된 tooas hello hello 원본 계층에서 tooa 노드에 해당 하는 각 커널 응용 프로그램 **중앙 노드**합니다. hello 가중치에 대 한 커널의 많은 연결에서 공유 됩니다. Convolutional 번들에서 각 커널 사각형 이며 모든 커널 응용 프로그램은 동일한 hello 크기입니다.  

Convolutional 번들 hello 다음 특성을 지원 합니다.

**InputShape** 이 convolutional 번들의 hello 목적을 위해 hello 원본 계층의 hello 차원을 정의 합니다. hello 값은 양의 정수 튜플 이어야 합니다. hello 정수 hello 제품 hello hello 원본 계층의 노드 수와 같아야 하지만 그렇지 않은 경우 toomatch hello 차원 hello 원본 계층에 대 한 선언 필요 하지 않습니다. 이 튜플의 hello 길이 hello **인자** hello convolutional 번들에 대 한 값입니다. (일반적으로 인자 참조 toohello 수의 인수 또는 함수를 사용할 수 있는 피연산자입니다.)  

toodefine hello 모양과 hello 커널의 위치 hello 특성을 사용 하 여 **KernelShape**, **Stride**, **패딩**, **LowerPad**, 및 **UpperPad**:   

* **KernelShape**: hello convolutional 번들에 대 한 각 커널의 정의 hello 차원을 (필수). hello 값의 길이가 hello 번들의 hello 인자 수가 해당 하는 양의 정수 여야 합니다. 이 튜플의 각 구성 요소는 hello의 해당 구성 요소 보다 크지 않아야 합니다. **InputShape**합니다. 
* **Stride**: (선택 사항) 정의 hello 슬라이딩 hello 중앙 노드 사이의 hello 거리에 있는 hello 회선 (각 차원에 대 한 단계 크기)의 단계 크기입니다. hello 값의 hello 번들의 hello 인자가 길이가 양의 정수 여야 합니다. 이 튜플의 각 구성 요소는 hello의 해당 구성 요소 보다 크지 않아야 합니다. **KernelShape**합니다. hello 기본값은 모든 구성 요소 같은 tooone 된 튜플의입니다. 
* **공유**: (선택 사항) 정의 hello 가중치 hello 회선의 각 차원에 대 한 공유 합니다. hello 값은 단일 부울 값 또는 부울 값 hello 번들의 hello 인자가 길이가 튜플 수 있습니다. 단일 부울 값이 모든 구성 요소와 hello 올바른 길이의 튜플이 확장된 toobe 같은 toohello 값을 지정 합니다. hello 기본값은 모든 True 값의 구성 된 튜플을입니다. 
* **MapCount**: hello convolutional 번들에 대 한 기능의 정의 hello 번호 (선택 사항)에 매핑합니다. hello 번들의 hello 인자가 길이가 정수 튜플 또는 단일 양의 정수 hello 값일 수 있습니다. 단일 정수 값 toobe 확장은 값과 모든 나머지 구성 요소 같은 tooone hello hello 첫 번째 구성 요소 같은 toohello와 hello 올바른 길이의 튜플을 지정 합니다. hello 기본 값은 1입니다. 기능 맵 hello 총 수는 hello 제품 hello 튜플의 hello 구성 요소입니다. hello 구성 요소에서이 총 개수 팩터링 hello hello 대상 노드 hello 기능 맵 값 그룹화 되는 방법을 결정 합니다. 
* **가중치**: hello 번들에 대 한 (선택 사항) 정의 hello 초기 가중치입니다. hello 값의 부동 소수점 값이이 문서의 뒷부분에 정의 된 대로 hello 수 커널 당 가중치 커널 시간 hello 수 있는 길이가 같아야 합니다. hello 기본 가중치는 임의로 생성 됩니다.  

안쪽 여백 상호 배타적인 되 고 hello 속성을 제어 하는 속성의 두 집합이 있습니다.

* **패딩**: (선택 사항) Determines hello 입력 여부 채워져야를 사용 하 여 한 **기본 패딩 구성표**합니다. hello 값일 수는 단일 부울 값 또는 hello 번들의 hello 인자가 있는 길이 사용 하 여 부울 값의 수입니다. 단일 부울 값이 모든 구성 요소와 hello 올바른 길이의 튜플이 확장된 toobe 같은 toohello 값을 지정 합니다. 해당 차원에서 첫 번째 및 마지막 커널 hello hello 중앙 노드는 hello 첫 번째 및 마지막 노드 되도록 hello 소스 값이 0 인 셀 toosupport 추가 커널 응용 프로그램과 해당 차원에 패딩 논리적으로 차원에 대 한 hello 값이 True 이면 hello 원본 계층에서 해당 차원의 합니다. 따라서 각 차원에 있는 "dummy" 노드 hello 수는 자동으로 결정 toofit 정확 하 게 *(InputShape [d]-1) [d] Stride / + 1* 패딩 hello 원본 계층으로 커널을 합니다. 차원에 대 한 hello 값이 False 인 경우 hello의 각 면으로 남아 있는 노드 hello 수 있도록 커널 정의 됩니다 (위쪽 1 tooa 차이) 동일 hello 합니다. 모든 구성 요소 같은 tooFalse와 튜플이 hello이이 특성의 기본값입니다.
* **UpperPad** 및 **LowerPad**: (선택 사항) 제공 대 한 제어 강화 패딩 toouse hello 양입니다. **중요:** 경우에 hello 이러한 특성을 정의할 수 있습니다 **패딩** 위의 속성은 ***하지*** 정의 합니다. hello 값 튜플 길이 hello 번들의 hello 인자 수는 정수 값 이어야 합니다. 이러한 특성을 지정 하는 경우 "dummy" 노드를 더 낮은 toohello 추가 하 고 위쪽 끝 hello의 각 차원 계층을 입력 합니다. hello 노드 수가 추가 toohello 아래쪽 및 위쪽 끝 각 차원에 따라 사용자가 **LowerPad**[i] 및 **UpperPad**[i] 각각. tooensure 커널 모니터는 너무만 "실제" 노드, 하지 너무 "dummy" 노드 hello 다음 조건이 충족 되어야 합니다.
  * **LowerPad**의 각 구성 요소는 KernelShape[d]/2보다 작아야 합니다. 
  * **UpperPad**의 각 구성 요소는 KernelShape[d]/2보다 크지 않아야 합니다. 
  * 이러한 특성의 기본값 hello와 모든 구성 요소 같은 too0 튜플이 합니다. 

hello 설정을 **패딩** = true 그대로 안쪽 여백 tookeep hello "센터" hello 커널의 "real"를 입력 하는 hello 내 필요할 수 있습니다. 이렇게 hello 수학 hello 출력 크기를 계산 하는 데 약간 변경 됩니다. Hello 크기를 출력 하는 일반적으로 *D* 로 계산 *D (I-K) = / S + 1*여기서 *I* 크기를 입력 하는 hello, *K* hello 커널 크기가 *S* hello stride는 및  */*  는 정수 나누기 (소수점 둥근). = UpperPad를 설정한 경우 [1, 1] hello 크기를 입력 *I* 29은 사실상 이므로 *D = (29-5) / 2 + 1 = 13*합니다. 그러나 **Padding** = true인 경우 기본적으로 *I*는 *K - 1*만큼 증가합니다. 따라서 *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*입니다. 에 대 한 값을 지정 하 여 **UpperPad** 및 **LowerPad** 훨씬 더 많이 제어할 패딩 경우 보다 있습니다 ड ि hello 얻게 **패딩** = true입니다.

나선형 네트워크 및 해당 응용 프로그램에 대한 자세한 내용은 다음 문서를 참조하세요.  

* [http://deeplearning.net/tutorial/lenet.html ](http://deeplearning.net/tutorial/lenet.html)
* [http://research.microsoft.com/pubs/68920/icdar03.pdf](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>풀링 번들
A **번들 풀링** geometry 비슷한 tooconvolutional 연결을 적용 하지만 미리 정의 된 함수 toosource 노드 값 tooderive hello 대상 노드 값을 사용 합니다. 또한 풀링 번들에는 학습 가능 상태가 없습니다(가중치 또는 편차). 풀링 convolutional 특성을 제외한 모든 hello 번들 지원 **공유**, **MapCount**, 및 **가중치**합니다.  

일반적으로 인접 한 장치를 풀링 하 여 요약 된 hello 커널 중첩 되지 않습니다. 각 차원에 동일한 tooKernelShape [d] [d] Stride을 사용 하는 경우 가져온 hello 레이어는 hello 기존의 로컬 풀링 계층, convolutional 신경망에 일반적으로 사용 되는. 각 대상 노드는 최대 hello 또는 hello 원본 계층에서 해당 커널의 hello 활동의 hello 평균을 계산합니다.  

다음 예제는 hello 풀링 번들을 보여 줍니다. 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* hello 번들의 hello 인자 수는 3 (길이 만큼의 튜플 hello hello **InputShape**, **KernelShape**, 및 **Stride**). 
* hello hello 원본 계층의 노드 수는 *5 * 24 * 24 = 2880*합니다. 
* **KernelShape** 및 **Stride**가 같으므로 이는 기존 로컬 풀링 계층입니다. 
* hello hello 대상 계층의 노드 수는 *5 * 12 * 12 = 1440*합니다.  

풀링 계층에 대한 자세한 내용은 다음 문서를 참조하세요.  

* [http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf)(섹션 3.4)
* [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>응답 정규화 번들
**응답 정규화** Geoffrey Hinton에서 처음 도입 된 로컬 정규화 체계 hello 백서에서 et al [Convolutional 심층 신경망와 ImageNet Classiﬁcation](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf)합니다. 응답 정규화는 신경망 네트워크에서 사용 되는 tooaid 일반화 합니다. 뉴런 하나를 정품 인증 매우 높은 수준에서 발생 하는 경우 로컬 응답 정규화 계층의 뉴런을 둘러싼 hello hello 활성화 수준을 표시 하지 않습니다. 이 작업에는 매개 변수 3개(***α***, ***β***, ***k***)와 나선형 구조(또는 환경 셰이프)를 사용합니다. Hello 대상 계층의 모든 뉴런 ***y*** tooa 뉴런 하 나와 해당 ***x*** hello 원본 계층에 있습니다. 정품 인증 수준의 hello ***y*** 를 지정 하 여 다음 수식을, hello 여기서 ***f*** hello 활성화 수준의 뉴런에 및 ***Nx*** hello 커널 (또는 hello를 포함 하는 hello 집합 hello 환경에 대 한 뉴런 ***x***) hello convolutional 구조를 다음에 정의 된 대로,:  

![][1]  

응답 정규화 번들 제외 하 고 hello convolutional 특성을 모두 지원 **공유**, **MapCount**, 및 **가중치**합니다.  

* 로 매핑 hello 커널 hello 뉴런을 포함 하는 경우 동일한 ***x***, hello 정규화 구성표는 참조 된 tooas **정규화를 매핑할 동일**합니다. 정규화, hello 첫 번째 좌표에 동일한 매핑할 toodefine **InputShape** hello 값 1이 있어야 합니다.
* Hello 커널 hello 뉴런을 포함 하는 경우와 같은 공간 위치 ***x***, hello 정규화 구성표 라고, hello 뉴런 다른 지도에 있지만 **across 정규화 매핑합니다**합니다. 이 유형의 응답 정규화 측면 inhibition hello에에서 형식이 실제 뉴런 지도에 계산 뉴런 출력 간에 큰 정품 인증 수준에 대 한 경합은 만들기에서 영감을 얻은의 형태를 구현 합니다. toodefine 정규화, hello 첫 번째 좌표 1 보다 크고 맵 hello 수보다 더 큰 정수 여야 합니다. 매핑하고 hello 좌표 hello 나머지 hello 값 1이 있어야 합니다.  

미리 정의 된 함수 toosource 노드 값 toodetermine hello 대상 노드 값을 적용 하는 응답 정규화 번들 (가중치 또는 편향) 트레인 할 수 있는 상태가 없는 있습니다.   

**경고**: hello 대상 계층의 노드에서 hello 해당 tooneurons hello 커널의 hello 중앙 노드입니다. 예를 들어, 다음 KernelShape [d]는 홀수 이면 *KernelShape [d] / 2* toohello 중앙 커널 노드에 해당 합니다. 경우 *KernelShape [d]* hello 중앙 노드가,은 *KernelShape [d] / 2-1*합니다. 따라서 경우 **패딩**[d]가 False 이면 먼저 hello 및 마지막 hello *KernelShape [d] / 2* 노드에 hello 대상 계층에서 해당 노드는 없습니다. tooavoid이이 경우 정의 **패딩** 으로 [true 이면 true,..., true].  

또한 toohello 네 가지 특성이 앞에서 설명한 정규화 번들 응답도 특성 뒤 지원 hello:  

* **알파**: 너무 해당 하는 부동 소수점 값 (필수) 지정***α*** hello 이전 수식에서 합니다. 
* **베타**: 너무 해당 하는 부동 소수점 값 (필수) 지정***β*** hello 이전 수식에서 합니다. 
* **오프셋**: 너무 해당는 부동 소수점 값을 지정 합니다 (옵션)***k*** hello 이전 수식에서 합니다. Too1을 기본값으로 사용 합니다.  

hello 다음 예제에서는 이러한 특성을 사용 하 여 응답 정규화 번들:  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* hello 소스 계층 각각 aof 차원 1440 노드에, 총 12 x 12의 5 개 지도 포함 합니다. 
* 값을 hello **KernelShape** hello 환경은 3 x 3 사각형 같은 지도 정규화 계층 임을 나타냅니다. 
* 기본값인 hello **패딩** 가 False 이면 따라서 hello 대상 계층에 10 개의 노드가 각 차원에 있습니다. 안쪽 여백을 추가 hello 원본 계층의 tooevery 노드에 해당 하는 hello 대상 계층의 한 노드에 tooinclude = [true, true, true]; 너무 RN1의 hello 크기를 변경 하 고 [5, 12, 12].  

## <a name="share-declaration"></a>공유 선언
Net#에서는 선택적으로 공유 가중치를 사용하여 여러 번들을 정의하도록 지원합니다. 해당 구조는 동일 hello는 경우 모든 두 번들의 hello 가중치를 공유할 수 있습니다. hello 구문 다음에 가중치 공유 번들 정의 합니다.  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

예를 들어 hello 다음 공유 선언 hello 레이어 이름을 지정를 나타내는 가중치와 편향 공유 되지 않아야 합니다.  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* hello 입력된 기능에 두 개의 동일한 크기의 입력된 계층으로 분할 됩니다. 
* 숨겨진 hello 레이어 hello 두 입력된 계층에 더 높은 수준 기능 계산 해야 합니다. 
* hello 공유 선언 지정 *H1* 및 *H2* hello에 계산 되어야 해당 입력에서 동일한 방식으로 합니다.  

또는 다음과 같이 개별 공유 선언 두 개를 사용하여 이를 지정할 수 있습니다.  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

Hello 약식 hello 레이어에 단일 번들을 포함 하는 경우에 사용할 수 있습니다. 일반적으로 공유를 가능한 hello 관련 구조 hello 동일 동일한 convolutional geometry, 크기 등을 수 있는 의미와 동일한 경우에 합니다.  

## <a name="examples-of-net-usage"></a>Net# 사용의 예
이 섹션에서는 몇 가지 사용 하는 방법을 Net # tooadd 숨겨진 계층 hello 방식이 숨겨진된 계층이 다른 계층 상호 작용 하 고 convolutional 네트워크 빌드를 정의 합니다.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>단순 사용자 지정 신경망 정의: "Hello World" 예제
이 간단한 예제 toocreate 신경망 a에 하나의 숨겨진된 계층이 모델 네트워크 하는 방법을 보여 줍니다.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

hello 예제는 다음과 같은 몇 가지 기본 명령의 보여 줍니다.  

* hello 첫 번째 줄을 정의 hello 입력된 계층 (라는 *데이터*). Hello를 사용 하는 경우 **자동** 키워드를 hello 신경망 hello 입력된 예제에서 모든 기능 열이 자동으로 포함 합니다. 
* 두 번째 줄 hello hello 숨겨진된 계층을 만듭니다. hello 이름 *H* 200 노드가 있는 toohello 숨겨진된 계층에 할당 됩니다. 이 계층은 완전히 연결 된 toohello 입력된 계층입니다.
* 세 번째 줄에서는 hello 정의 hello 출력 계층 (라는 *O*), 10 출력 노드를 포함 하 합니다. Hello 신경망 분류를 위해 사용 하는 경우 클래스 마다 출력 노드가 하나씩 있습니다. 키워드 hello **시그모이드** hello 출력 함수 적용된 toohello 출력 계층 임을 나타냅니다.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>여러 숨겨진 계층 정의: 컴퓨터 비전 예제
hello 다음 예제에서는 어떻게 toodefine 약간 더 복잡 한 신경망을 여러 개의 사용자 지정 숨겨진된 계층 사용 합니다.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

이 예제에서는 hello 신경망 사양 언어의 여러 기능을 보여 줍니다.  

* hello 구조에 두 개의 입력된 계층으로 *픽셀* 및 *메타 데이터*합니다.
* hello *픽셀* 계층은 대상 계층으로 두 개의 연결 번들에 대 한 원본 계층 *ByRow* 및 *ByCol*합니다.
* 레이어 hello *수집* 및 *결과* 은 여러 연결 번들에서 대상 계층입니다.
* hello 출력 계층 *결과*은 대상 계층으로 두 개의 연결 번들, 하나는 hello로 대상 계층으로 숨겨진된 (수집)를 두 번째 수준 및 대상 계층으로 hello와 hello 입력된 계층 (메타 데이터)를 사용 합니다.
* 숨겨진된 계층을 hello *ByRow* 및 *ByCol*, 조건자 식을 사용 하 여 필터링 된 연결을 지정 합니다. 보다 정확 하 게 hello 노드 *ByRow* 에서 [x, y]에서 연결 된 toohello 노드의 *픽셀* hello 첫 번째 인덱스 좌표 같은 toohello 노드의 첫 번째 좌표, x 있는 합니다. 마찬가지로, hello 노드에서 *[x, y]에서 ByCol _Pixels에 연결 된 toohello 노드의* hello hello 노드의 두 번째 좌표 중 하나에서 두 번째 인덱스 좌표에 있는 y 합니다.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>다중 클래스 분류에 대한 나선형 네트워크 정의: 숫자 인식 예제
다음 네트워크 hello의 hello 정의 설계 된 toorecognize 번호 이며 신경망 사용자 지정에 대 한 고급 기술을 보여 줍니다.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* hello 구조에는 단일 입력된 계층 *이미지*합니다.
* 키워드 hello **convolve** hello 레이어 라는 나타냅니다 *Conv1* 및 *Conv2* convolutional 계층이 있습니다. 이러한 각 계층 선언은 hello 회선 특성 목록이 옵니다.
* net hello 세 번째 숨겨진 계층을 *Hid3*는 완벽 하 게 연결 된 두 번째 숨겨진된 계층 toohello *Conv2*합니다.
* hello 출력 계층 *자리*, 연결 된 유일한 toohello 세 번째 숨겨진된 계층은 *Hid3*합니다. 키워드 hello **모든** 해당 hello 출력 계층은 완전히 너무 연결 나타냅니다*Hid3*합니다.
* hello hello 회선의 인자 수는 3 개입니다 (길이 만큼의 튜플 hello hello **InputShape**, **KernelShape**, **Stride**, 및 **공유**). 
* 커널 당 가중치 hello 수는 *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26입니다. 또는 26 * 50 = 1300*입니다.
* 각 숨겨진된 계층의 hello 노드는 다음과 같이 계산할 수 있습니다.
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[1] = (13 - 5) / 2 + 1 = 5. 
  * **NodeCount**\[2] = (13 - 5) / 2 + 1 = 5. 
* hello 총 노드 수 계산 hello의 차원을 선언 하는 hello를 사용 하 여 계층이 [50, 5, 5], 다음과 같이:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*
* 때문에 **공유**[d]가 False에 대해서만 *d = = 0*, 커널 hello 수는  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*합니다. 

## <a name="acknowledgements"></a>감사의 말
Net # 신경망의 hello 아키텍처를 사용자 지정 하기 위한 언어 hello Shon Katzenberger (설계자, 기계 학습) 및 Alexey Kamenev (소프트웨어 엔지니어, Microsoft Research)에서 Microsoft에서 개발 되었습니다. 기계 학습 프로젝트와 이미지 검색 tootext 분석에서 사이의 응용 프로그램에 대 한 내부적으로 사용 됩니다. 자세한 내용은 참조 [신경망 네트 Azure ML-소개 tooNet #에서](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

