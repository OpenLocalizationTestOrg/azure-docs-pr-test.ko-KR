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
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a><span data-ttu-id="a86f5-103">Azure 기계 학습에 대 한 tooNet # 신경망 사양 언어 가이드</span><span class="sxs-lookup"><span data-stu-id="a86f5-103">Guide tooNet# neural network specification language for Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="a86f5-104">개요</span><span class="sxs-lookup"><span data-stu-id="a86f5-104">Overview</span></span>
<span data-ttu-id="a86f5-105">Net # 신경망 아키텍처를 사용 하는 toodefine은 Microsoft에서 개발 된 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-105">Net# is a language developed by Microsoft that is used toodefine neural network architectures.</span></span> <span data-ttu-id="a86f5-106">Microsoft Azure Machine Learning의 신경망 모듈에서 Net#을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-106">You can use Net# in neural network modules in Microsoft Azure Machine Learning.</span></span>

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

<span data-ttu-id="a86f5-107">이 문서에서는 기본 개념 필요한 사용자 지정 신경망 toodevelop 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-107">In this article, you will learn basic concepts needed toodevelop a custom neural network:</span></span> 

* <span data-ttu-id="a86f5-108">신경망 요구 사항과 어떻게 toodefine hello 기본 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a86f5-108">Neural network requirements and how toodefine hello primary components</span></span>
* <span data-ttu-id="a86f5-109">hello 구문 및 hello Net # 사양 언어의 키워드</span><span class="sxs-lookup"><span data-stu-id="a86f5-109">hello syntax and keywords of hello Net# specification language</span></span>
* <span data-ttu-id="a86f5-110">Net#을 사용하여 만든 사용자 지정 신경망의 예</span><span class="sxs-lookup"><span data-stu-id="a86f5-110">Examples of custom neural networks created using Net#</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a><span data-ttu-id="a86f5-111">신경망 기본 사항</span><span class="sxs-lookup"><span data-stu-id="a86f5-111">Neural network basics</span></span>
<span data-ttu-id="a86f5-112">신경망 구조 이루어져 ***노드*** 에 구성 된 ***레이어***, 및가 중 ***연결*** (또는 ***가장자리***) 사이 hello 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-112">A neural network structure consists of ***nodes*** that are organized in ***layers***, and weighted ***connections*** (or ***edges***) between hello nodes.</span></span> <span data-ttu-id="a86f5-113">hello 연결은 방향이 고 각 연결에는 ***소스*** 노드 및 ***대상*** 노드.</span><span class="sxs-lookup"><span data-stu-id="a86f5-113">hello connections are directional, and each connection has a ***source*** node and a ***destination*** node.</span></span>  

<span data-ttu-id="a86f5-114">각 ***학습 가능한 계층***(숨겨진 계층 또는 출력 계층)에는 하나 이상의 ***연결 번들***이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-114">Each ***trainable layer*** (a hidden or an output layer) has one or more ***connection bundles***.</span></span> <span data-ttu-id="a86f5-115">연결 번들 소스 계층 및 해당 원본 계층에서 hello 연결에 대 한 사양으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-115">A connection bundle consists of a source layer and a specification of hello connections from that source layer.</span></span> <span data-ttu-id="a86f5-116">지정 된 번들 공유에 있는 모든 hello 연결 hello 동일 ***소스 계층*** 동일 hello 및 ***대상 계층***합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-116">All hello connections in a given bundle share hello same ***source layer*** and hello same ***destination layer***.</span></span> <span data-ttu-id="a86f5-117">Net # 연결 번들 속하는 toohello 번들 대상 계층으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-117">In Net#, a connection bundle is considered as belonging toohello bundle's destination layer.</span></span>  

<span data-ttu-id="a86f5-118">Net # 다양 한 종류의 지원 연결 번들 입력은 매핑된 toohidden 레이어 hello 방법을 사용자 지정할 수 있습니다 하 고 매핑된 toohello 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-118">Net# supports various kinds of connection bundles, which lets you customize hello way inputs are mapped toohidden layers and mapped toohello outputs.</span></span>   

<span data-ttu-id="a86f5-119">hello 기본 또는 표준 번들은 **전체 번들**, hello의 각 노드를 소스 계층은 hello 대상 계층의 연결 된 tooevery 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-119">hello default or standard bundle is a **full bundle**, in which each node in hello source layer is connected tooevery node in hello destination layer.</span></span>  

<span data-ttu-id="a86f5-120">또한, Net # 지원 다음 네 가지 유형의 고급 연결 번들 hello:</span><span class="sxs-lookup"><span data-stu-id="a86f5-120">Additionally, Net# supports hello following four kinds of advanced connection bundles:</span></span>  

* <span data-ttu-id="a86f5-121">**필터링된 번들**.</span><span class="sxs-lookup"><span data-stu-id="a86f5-121">**Filtered bundles**.</span></span> <span data-ttu-id="a86f5-122">hello 사용자는 원본 계층 노드 hello 및 hello 대상 계층 노드의 hello 위치를 사용 하 여 조건자를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-122">hello user can define a predicate by using hello locations of hello source layer node and hello destination layer node.</span></span> <span data-ttu-id="a86f5-123">노드는 hello 조건자가 True 때마다 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-123">Nodes are connected whenever hello predicate is True.</span></span>
* <span data-ttu-id="a86f5-124">**나선형 번들**.</span><span class="sxs-lookup"><span data-stu-id="a86f5-124">**Convolutional bundles**.</span></span> <span data-ttu-id="a86f5-125">hello 사용자 hello 원본 계층의 노드는 작은 공간을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-125">hello user can define small neighborhoods of nodes in hello source layer.</span></span> <span data-ttu-id="a86f5-126">Hello 대상 계층의 각 노드는 hello 원본 계층에 있는 노드의 연결 된 tooone 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-126">Each node in hello destination layer is connected tooone neighborhood of nodes in hello source layer.</span></span>
* <span data-ttu-id="a86f5-127">**풀링 번들** 및 **응답 정규화 번들**.</span><span class="sxs-lookup"><span data-stu-id="a86f5-127">**Pooling bundles** and **Response normalization bundles**.</span></span> <span data-ttu-id="a86f5-128">이러한은 유사한 tooconvolutional 번들 해당 hello에 사용자는 작은 공간에서 hello 원본 계층의 노드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-128">These are similar tooconvolutional bundles in that hello user defines small neighborhoods of nodes in hello source layer.</span></span> <span data-ttu-id="a86f5-129">hello 차이점은 이러한 번들에 hello 지 hello 가중치 트레인 할 수 있는 하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-129">hello difference is that hello weights of hello edges in these bundles are not trainable.</span></span> <span data-ttu-id="a86f5-130">미리 정의 된 함수를 적용 하는 대신, toohello 소스 노드에서 값 toodetermine hello 대상 노드 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-130">Instead, a predefined function is applied toohello source node values toodetermine hello destination node value.</span></span>  

<span data-ttu-id="a86f5-131">Net #을 사용 하 여 toodefine hello 구조는 신경망의를 사용 가능한 toodefine 심층 신경망 또는 tooimprove 학습 이미지, 오디오 또는 비디오와 같은 데이터에 대해 알려진 임의의 차원의 나선 같은 복잡 한 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-131">Using Net# toodefine hello structure of a neural network makes it possible toodefine complex structures such as deep neural networks or convolutions of arbitrary dimensions, which are known tooimprove learning on data such as image, audio, or video.</span></span>  

## <a name="supported-customizations"></a><span data-ttu-id="a86f5-132">지원되는 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a86f5-132">Supported customizations</span></span>
<span data-ttu-id="a86f5-133">Azure 기계 학습에서 만드는 신경망 모델의 hello 아키텍처 Net #을 사용 하 여 광범위 하 게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-133">hello architecture of neural network models that you create in Azure Machine Learning can be extensively customized by using Net#.</span></span> <span data-ttu-id="a86f5-134">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-134">You can:</span></span>  

* <span data-ttu-id="a86f5-135">각 계층의 제어 hello 노드 수 및 숨겨진된 계층을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-135">Create hidden layers and control hello number of nodes in each layer.</span></span>
* <span data-ttu-id="a86f5-136">계층의 다른 연결 toobe tooeach는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-136">Specify how layers are toobe connected tooeach other.</span></span>
* <span data-ttu-id="a86f5-137">나선 및 가중 공유 번들과 같은 특수 연결 구조를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-137">Define special connectivity structures, such as convolutions and weight sharing bundles.</span></span>
* <span data-ttu-id="a86f5-138">여러 가지 활성화 함수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-138">Specify different activation functions.</span></span>  

<span data-ttu-id="a86f5-139">Hello 사양 언어 구문의 자세한 참조 [구조 사양](#Structure-specifications)합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-139">For details of hello specification language syntax, see [Structure Specification](#Structure-specifications).</span></span>  

<span data-ttu-id="a86f5-140">신경망 학습 단면 toocomplex에서 작업을 몇 가지 일반적인 컴퓨터에 대 한 정의의 예제 참조 [예제](#Examples-of-Net#-usage)합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-140">For examples of defining neural networks for some common machine learning tasks, from simplex toocomplex, see [Examples](#Examples-of-Net#-usage).</span></span>  

## <a name="general-requirements"></a><span data-ttu-id="a86f5-141">일반 요구 사항</span><span class="sxs-lookup"><span data-stu-id="a86f5-141">General requirements</span></span>
* <span data-ttu-id="a86f5-142">정확히 출력 계층 1개, 입력 계층 1개 이상, 숨겨진 계층 0개 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-142">There must be exactly one output layer, at least one input layer, and zero or more hidden layers.</span></span> 
* <span data-ttu-id="a86f5-143">각 계층에는 개념적으로 임의 차원의 사각형 배열로 정렬된 고정된 수의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-143">Each layer has a fixed number of nodes, conceptually arranged in a rectangular array of arbitrary dimensions.</span></span> 
* <span data-ttu-id="a86f5-144">입력된 레이어 관련 학습 된 매개 변수 및 인스턴스 데이터는 hello 네트워크를 저장 하는 hello 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-144">Input layers have no associated trained parameters and represent hello point where instance data enters hello network.</span></span> 
* <span data-ttu-id="a86f5-145">트레인 할 수 있는 계층 (숨겨진 계층과 출력 계층 hello) 가중치 및 편향 라는 학습 된 매개 변수를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-145">Trainable layers (hello hidden and output layers) have associated trained parameters, known as weights and biases.</span></span> 
* <span data-ttu-id="a86f5-146">hello 소스 노드와 대상 노드는 별도 계층에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-146">hello source and destination nodes must be in separate layers.</span></span> 
* <span data-ttu-id="a86f5-147">연결 된 비순환; 수 있어야 합니다. 즉, 체인 연결 백 toohello 초기 소스 노드 앞에 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-147">Connections must be acyclic; in other words, there cannot be a chain of connections leading back toohello initial source node.</span></span>
* <span data-ttu-id="a86f5-148">hello 출력 계층 연결 번들의 소스 계층 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-148">hello output layer cannot be a source layer of a connection bundle.</span></span>  

## <a name="structure-specifications"></a><span data-ttu-id="a86f5-149">구조 사양</span><span class="sxs-lookup"><span data-stu-id="a86f5-149">Structure specifications</span></span>
<span data-ttu-id="a86f5-150">세 가지 섹션으로 구성 된 신경망 구조 사양: hello **상수 선언**, hello **선언 레이어**, hello **연결 선언**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-150">A neural network structure specification is composed of three sections: hello **constant declaration**, hello **layer declaration**, hello **connection declaration**.</span></span> <span data-ttu-id="a86f5-151">또한 선택적 **공유 선언** 섹션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-151">There is also an optional **share declaration** section.</span></span> <span data-ttu-id="a86f5-152">hello 섹션은 순서에 관계 없이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-152">hello sections can be specified in any order.</span></span>  

## <a name="constant-declaration"></a><span data-ttu-id="a86f5-153">상수 선언</span><span class="sxs-lookup"><span data-stu-id="a86f5-153">Constant declaration</span></span>
<span data-ttu-id="a86f5-154">상수 선언은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-154">A constant declaration is optional.</span></span> <span data-ttu-id="a86f5-155">Hello 신경망 정의에서 다른 위치에서 사용 되는 값은 toodefine 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-155">It provides a means toodefine values used elsewhere in hello neural network definition.</span></span> <span data-ttu-id="a86f5-156">선언문 hello 식별자 뒤에 등호와 값 식으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-156">hello declaration statement consists of an identifier followed by an equal sign and a value expression.</span></span>   

<span data-ttu-id="a86f5-157">문 다음 hello 상수를 정의 하는 예를 들어 **x**:</span><span class="sxs-lookup"><span data-stu-id="a86f5-157">For example, hello following statement defines a constant **x**:</span></span>  

    Const X = 28;  

<span data-ttu-id="a86f5-158">toodefine 동시에 둘 이상의 상수 hello 식별자 이름 및 값을 중괄호로 묶습니다 및 세미콜론을 사용 하 여 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-158">toodefine two or more constants simultaneously, enclose hello identifier names and values in braces, and separate them by using semicolons.</span></span> <span data-ttu-id="a86f5-159">예:</span><span class="sxs-lookup"><span data-stu-id="a86f5-159">For example:</span></span>  

    Const { X = 28; Y = 4; }  

<span data-ttu-id="a86f5-160">각 대입 식의 오른쪽 hello 정수, 실수, 부울 값 (True 또는 False) 또는 수학 식 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-160">hello right-hand side of each assignment expression can be an integer, a real number, a Boolean value (True or False), or a mathematical expression.</span></span> <span data-ttu-id="a86f5-161">예:</span><span class="sxs-lookup"><span data-stu-id="a86f5-161">For example:</span></span>  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a><span data-ttu-id="a86f5-162">계층 선언</span><span class="sxs-lookup"><span data-stu-id="a86f5-162">Layer declaration</span></span>
<span data-ttu-id="a86f5-163">hello 레이어 선언이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-163">hello layer declaration is required.</span></span> <span data-ttu-id="a86f5-164">Hello 크기 및 해당 연결 번들와 특성을 포함 하 여 hello 계층의 소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-164">It defines hello size and source of hello layer, including its connection bundles and attributes.</span></span> <span data-ttu-id="a86f5-165">선언 문 hello 계층 (입력, 숨겨진 경우 또는 출력)의 hello 이름 시작 하 고 hello, hello 계층 (양의 정수 튜플)의 hello 차원 차례로 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-165">hello declaration statement starts with hello name of hello layer (input, hidden, or output), followed by hello dimensions of hello layer (a tuple of positive integers).</span></span> <span data-ttu-id="a86f5-166">예:</span><span class="sxs-lookup"><span data-stu-id="a86f5-166">For example:</span></span>  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* <span data-ttu-id="a86f5-167">hello 차원의 hello 제품 hello 계층의 노드 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-167">hello product of hello dimensions is hello number of nodes in hello layer.</span></span> <span data-ttu-id="a86f5-168">이 예제는 hello 계층에는 100 노드가 즉 두 개의 차원 [5,20]입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-168">In this example, there are two dimensions [5,20], which means there are  100 nodes in hello layer.</span></span>
* <span data-ttu-id="a86f5-169">그러나 예외적으로 임의의 순서로 hello 레이어를 선언할 수 있습니다: 선언 된 hello 순서에 hello 입력된 데이터의 기능 hello 순서와 일치 해야 하나 이상의 입력된 레이어 정의 된 경우.</span><span class="sxs-lookup"><span data-stu-id="a86f5-169">hello layers can be declared in any order, with one exception: If more than one input layer is defined, hello order in which they are declared must match hello order of features in hello input data.</span></span>  

<span data-ttu-id="a86f5-170">hello는 계층의 노드 수는 toospecify 자동으로 사용 하 여 hello 결정 **자동** 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-170">toospecify that hello number of nodes in a layer be determined automatically, use hello **auto** keyword.</span></span> <span data-ttu-id="a86f5-171">hello **자동** 키워드 hello 계층에 따라 다양 한 효과 가집니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-171">hello **auto** keyword has different effects, depending on hello layer:</span></span>  

* <span data-ttu-id="a86f5-172">입력된 계층 선언에서 hello 노드 수는 hello 입력된 데이터에서 기능 hello 수가입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-172">In an input layer declaration, hello number of nodes is hello number of features in hello input data.</span></span>
* <span data-ttu-id="a86f5-173">숨겨진된 계층 선언에서 hello 노드 수입니다. hello에 대 한 hello 매개 변수 값으로 지정 된 **숨겨진 노드의 수**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-173">In a hidden layer declaration, hello number of nodes is hello number that is specified by hello parameter value for **Number of hidden nodes**.</span></span> 
* <span data-ttu-id="a86f5-174">출력 계층 선언에 hello 노드 수는 2 클래스 분류와 회귀를과 같은 toohello 다중 클래스 분류에 대 한 출력 노드 수가 1 2입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-174">In an output layer declaration, hello number of nodes is 2 for two-class classification, 1 for regression, and equal toohello number of output nodes for multiclass classification.</span></span>   

<span data-ttu-id="a86f5-175">예를 들어 hello 다음 네트워크 정의 사용 하면 자동으로 결정 하는 모든 계층 toobe의 hello 크기:</span><span class="sxs-lookup"><span data-stu-id="a86f5-175">For example, hello following network definition allows hello size of all layers toobe automatically determined:</span></span>  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


<span data-ttu-id="a86f5-176">트레인 할 수 있는 계층에 대 한 레이어 선언 (숨겨진 또는 출력 계층 hello) hello 출력 함수 (활성화 함수 라고도 함) 너무 기본값으로 사용 하는 선택적으로 포함할 수**시그모이드** 분류 모델 및 **선형** 회귀 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-176">A layer declaration for a trainable layer (hello hidden or output layers) can optionally include hello output function (also called an activation function), which defaults too**sigmoid** for classification models, and **linear** for regression models.</span></span> <span data-ttu-id="a86f5-177">(Hello 기본값을 사용 하는 경우에 명시적으로 명시할 수 hello 활성화 함수 쉽게 구별할 수 있도록 원하는 경우.)</span><span class="sxs-lookup"><span data-stu-id="a86f5-177">(Even if you use hello default, you can explicitly state hello activation function, if desired for clarity.)</span></span>

<span data-ttu-id="a86f5-178">hello 다음과 같은 출력 함수 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-178">hello following output functions are supported:</span></span>  

* <span data-ttu-id="a86f5-179">sigmoid</span><span class="sxs-lookup"><span data-stu-id="a86f5-179">sigmoid</span></span>
* <span data-ttu-id="a86f5-180">linear</span><span class="sxs-lookup"><span data-stu-id="a86f5-180">linear</span></span>
* <span data-ttu-id="a86f5-181">softmax</span><span class="sxs-lookup"><span data-stu-id="a86f5-181">softmax</span></span>
* <span data-ttu-id="a86f5-182">rlinear</span><span class="sxs-lookup"><span data-stu-id="a86f5-182">rlinear</span></span>
* <span data-ttu-id="a86f5-183">square</span><span class="sxs-lookup"><span data-stu-id="a86f5-183">square</span></span>
* <span data-ttu-id="a86f5-184">sqrt</span><span class="sxs-lookup"><span data-stu-id="a86f5-184">sqrt</span></span>
* <span data-ttu-id="a86f5-185">srlinear</span><span class="sxs-lookup"><span data-stu-id="a86f5-185">srlinear</span></span>
* <span data-ttu-id="a86f5-186">abs</span><span class="sxs-lookup"><span data-stu-id="a86f5-186">abs</span></span>
* <span data-ttu-id="a86f5-187">tanh</span><span class="sxs-lookup"><span data-stu-id="a86f5-187">tanh</span></span> 
* <span data-ttu-id="a86f5-188">brlinear</span><span class="sxs-lookup"><span data-stu-id="a86f5-188">brlinear</span></span>  

<span data-ttu-id="a86f5-189">선언 뒤 hello hello를 사용 하는 예를 들어 **softmax** 함수:</span><span class="sxs-lookup"><span data-stu-id="a86f5-189">For example, hello following declaration uses hello **softmax** function:</span></span>  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a><span data-ttu-id="a86f5-190">연결 선언</span><span class="sxs-lookup"><span data-stu-id="a86f5-190">Connection declaration</span></span>
<span data-ttu-id="a86f5-191">Hello 트레인 할 수 있는 계층을 정의한 후 즉시 정의한 hello 계층 간 연결을 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-191">Immediately after defining hello trainable layer, you must declare connections among hello layers you have defined.</span></span> <span data-ttu-id="a86f5-192">hello 연결 번들 선언 hello 키워드로 시작 **에서**고 hello 번들의 원본 계층 및 hello 종류의 연결 번들 toocreate hello 이름이 옵니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-192">hello connection bundle declaration starts with hello keyword **from**, followed by hello name of hello bundle's source layer and hello kind of connection bundle toocreate.</span></span>   

<span data-ttu-id="a86f5-193">현재 다음 5가지 연결 번들이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-193">Currently, five kinds of connection bundles are supported:</span></span>  

* <span data-ttu-id="a86f5-194">**전체** hello 키워드로 표시 된 번들 **모든**</span><span class="sxs-lookup"><span data-stu-id="a86f5-194">**Full** bundles, indicated by hello keyword **all**</span></span>
* <span data-ttu-id="a86f5-195">**필터링** hello 키워드로 표시 된 번들 **여기서**, 조건자 식</span><span class="sxs-lookup"><span data-stu-id="a86f5-195">**Filtered** bundles, indicated by hello keyword **where**, followed by a predicate expression</span></span>
* <span data-ttu-id="a86f5-196">**Convolutional** hello 키워드로 표시 된 번들 **convolve**, hello 회선 특성</span><span class="sxs-lookup"><span data-stu-id="a86f5-196">**Convolutional** bundles, indicated by hello keyword **convolve**, followed by hello convolution attributes</span></span>
* <span data-ttu-id="a86f5-197">**풀링** hello 키워드로 표시 된 번들 **풀 max** 또는 **풀을 의미 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a86f5-197">**Pooling** bundles, indicated by hello keywords **max pool** or **mean pool**</span></span>
* <span data-ttu-id="a86f5-198">**응답 정규화** hello 키워드로 표시 된 번들 **응답 norm**</span><span class="sxs-lookup"><span data-stu-id="a86f5-198">**Response normalization** bundles, indicated by hello keyword **response norm**</span></span>      

## <a name="full-bundles"></a><span data-ttu-id="a86f5-199">전체 번들</span><span class="sxs-lookup"><span data-stu-id="a86f5-199">Full bundles</span></span>
<span data-ttu-id="a86f5-200">전체 연결 번들에서 각 노드의 연결 hello 소스 레이어 tooeach hello 대상 계층의 노드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-200">A full connection bundle includes a connection from each node in hello source layer tooeach node in hello destination layer.</span></span> <span data-ttu-id="a86f5-201">이것이 hello 기본 네트워크 연결 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-201">This is hello default network connection type.</span></span>  

## <a name="filtered-bundles"></a><span data-ttu-id="a86f5-202">필터링된 번들</span><span class="sxs-lookup"><span data-stu-id="a86f5-202">Filtered bundles</span></span>
<span data-ttu-id="a86f5-203">필터링된 연결 번들 사양은 구문상 C# 람다 식과 훨씬 비슷하게 표현된 조건자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-203">A filtered connection bundle specification includes a predicate, expressed syntactically, much like a C# lambda expression.</span></span> <span data-ttu-id="a86f5-204">hello 다음 예제에서는 두 가지 필터링 된 번들:</span><span class="sxs-lookup"><span data-stu-id="a86f5-204">hello following example defines two filtered bundles:</span></span>  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* <span data-ttu-id="a86f5-205">에 대 한 hello 조건자에서 *ByRow*, **s** hello 입력된 계층의 노드 hello 사각형 배열로 인덱스를 나타내는 매개 변수는 *픽셀*, 및 **d**  hello 숨겨진된 계층의 노드 hello 배열로 인덱스를 나타내는 매개 변수는 *ByRow*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-205">In hello predicate for *ByRow*, **s** is a parameter representing an index into hello rectangular array of nodes of hello input layer, *Pixels*, and **d** is a parameter representing an index into hello array of nodes of hello hidden layer, *ByRow*.</span></span> <span data-ttu-id="a86f5-206">두 유형의 hello **s** 및 **d** 길이의 두 정수의 튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-206">hello type of both **s** and **d** is a tuple of integers of length two.</span></span> <span data-ttu-id="a86f5-207">개념적으로 **s**는 *0 <= s[0] < 10* 및 *0 <= s[1] < 20* 조건의 모든 정수 쌍을 포함하고 **d**는 *0 <= d[0] < 10* 및 *0 <= d[1] < 12* 조건의 모든 정수 쌍을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-207">Conceptually, **s** ranges over all pairs of integers with *0 <= s[0] < 10* and *0 <= s[1] < 20*, and **d** ranges over all pairs of integers, with *0 <= d[0] < 10* and *0 <= d[1] < 12*.</span></span> 
* <span data-ttu-id="a86f5-208">Hello 조건자 식의 오른쪽을 hello에 상태.</span><span class="sxs-lookup"><span data-stu-id="a86f5-208">On hello right-hand side of hello predicate expression, there is a condition.</span></span> <span data-ttu-id="a86f5-209">모든 값에 대 한이 예에서 **s** 및 **d** hello 조건이 True 이면 되도록 hello 소스 노드에서 계층 노드 toohello 대상 계층 형성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-209">In this example, for every value of **s** and **d** such that hello condition is True, there is an edge from hello source layer node toohello destination layer node.</span></span> <span data-ttu-id="a86f5-210">따라서이 필터 식은 해당 hello 번들 포함 하 여 정의 된 hello 노드에서 연결을 나타냅니다 **s** 정의한 toohello 노드 **d** 여기서 s [0]는 [0] 같으면 tood 모든 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-210">Thus, this filter expression indicates that hello bundle includes a connection from hello node defined by **s** toohello node defined by **d** in all cases where s[0] is equal tood[0].</span></span>  

<span data-ttu-id="a86f5-211">선택적으로 필터링된 번들의 가중치 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-211">Optionally, you can specify a set of weights for a filtered bundle.</span></span> <span data-ttu-id="a86f5-212">hello에 대 한 값을 hello **가중치** 특성에는 부동 소수점 값 길이가 hello 번들에서 정의 된 연결의 hello 번호와 일치 하는 tuple 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-212">hello value for hello **Weights** attribute must be a tuple of floating point values with a length that matches hello number of connections defined by hello bundle.</span></span> <span data-ttu-id="a86f5-213">기본적으로 가중치는 임의로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-213">By default, weights are randomly generated.</span></span>  

<span data-ttu-id="a86f5-214">가중치 값 hello 대상 노드 인덱스 별로 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-214">Weight values are grouped by hello destination node index.</span></span> <span data-ttu-id="a86f5-215">Hello 첫 번째 대상 노드가 연결 된 경우 걸린 소스 노드, 즉 먼저 hello *K* hello 요소의 **가중치** 튜플은 hello 첫 번째 대상 노드를 소스 인덱스 순서에서에 대 한 hello 가중치입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-215">That is, if hello first destination node is connected tooK source nodes, hello first *K* elements of hello **Weights** tuple are hello weights for hello first destination node, in source index order.</span></span> <span data-ttu-id="a86f5-216">hello에 대 한 나머지 대상 노드에서 hello에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-216">hello same applies for hello remaining destination nodes.</span></span>  

<span data-ttu-id="a86f5-217">가능한 toospecify 가중치 프로토콜은 상수 값으로 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-217">It's possible toospecify weights directly as constant values.</span></span> <span data-ttu-id="a86f5-218">예를 들어 hello 가중치를 이전에 배운 경우이 구문을 사용 하 여 상수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-218">For example, if you learned hello weights previously, you can specify them as constants using this syntax:</span></span>

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a><span data-ttu-id="a86f5-219">나선형 번들</span><span class="sxs-lookup"><span data-stu-id="a86f5-219">Convolutional bundles</span></span>
<span data-ttu-id="a86f5-220">Hello 학습 데이터의 구조는 유형이 같은, 자주 사용 되는 toolearn hello 데이터의 상위 수준 기능 convolutional 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-220">When hello training data has a homogeneous structure, convolutional connections are commonly used toolearn high-level features of hello data.</span></span> <span data-ttu-id="a86f5-221">예를 들어 이미지, 오디오 또는 비디오 데이터에서 공간 또는 임시 차원은 상당히 균일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-221">For example, in image, audio, or video data, spatial or temporal dimensionality can be fairly uniform.</span></span>  

<span data-ttu-id="a86f5-222">Convolutional 번들 채택 사각형 **커널** hello 차원을 통해 밀어는입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-222">Convolutional bundles employ rectangular **kernels** that are slid through hello dimensions.</span></span> <span data-ttu-id="a86f5-223">각 커널 공간에서 로컬, 참조 tooas에 적용 된 가중치의 집합을 정의 하는 기본적으로, **커널 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-223">Essentially, each kernel defines a set of weights applied in local neighborhoods, referred tooas **kernel applications**.</span></span> <span data-ttu-id="a86f5-224">참조 된 tooas hello hello 원본 계층에서 tooa 노드에 해당 하는 각 커널 응용 프로그램 **중앙 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-224">Each kernel application corresponds tooa node in hello source layer, which is referred tooas hello **central node**.</span></span> <span data-ttu-id="a86f5-225">hello 가중치에 대 한 커널의 많은 연결에서 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-225">hello weights of a kernel are shared among many connections.</span></span> <span data-ttu-id="a86f5-226">Convolutional 번들에서 각 커널 사각형 이며 모든 커널 응용 프로그램은 동일한 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-226">In a convolutional bundle, each kernel is rectangular and all kernel applications are hello same size.</span></span>  

<span data-ttu-id="a86f5-227">Convolutional 번들 hello 다음 특성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-227">Convolutional bundles support hello following attributes:</span></span>

<span data-ttu-id="a86f5-228">**InputShape** 이 convolutional 번들의 hello 목적을 위해 hello 원본 계층의 hello 차원을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-228">**InputShape** defines hello dimensionality of hello source layer for hello purposes of this convolutional bundle.</span></span> <span data-ttu-id="a86f5-229">hello 값은 양의 정수 튜플 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-229">hello value must be a tuple of positive integers.</span></span> <span data-ttu-id="a86f5-230">hello 정수 hello 제품 hello hello 원본 계층의 노드 수와 같아야 하지만 그렇지 않은 경우 toomatch hello 차원 hello 원본 계층에 대 한 선언 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-230">hello product of hello integers must equal hello number of nodes in hello source layer, but otherwise, it does not need toomatch hello dimensionality declared for hello source layer.</span></span> <span data-ttu-id="a86f5-231">이 튜플의 hello 길이 hello **인자** hello convolutional 번들에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-231">hello length of this tuple becomes hello **arity** value for hello convolutional bundle.</span></span> <span data-ttu-id="a86f5-232">(일반적으로 인자 참조 toohello 수의 인수 또는 함수를 사용할 수 있는 피연산자입니다.)</span><span class="sxs-lookup"><span data-stu-id="a86f5-232">(Typically arity refers toohello number of arguments or operands that a function can take.)</span></span>  

<span data-ttu-id="a86f5-233">toodefine hello 모양과 hello 커널의 위치 hello 특성을 사용 하 여 **KernelShape**, **Stride**, **패딩**, **LowerPad**, 및 **UpperPad**:</span><span class="sxs-lookup"><span data-stu-id="a86f5-233">toodefine hello shape and locations of hello kernels, use hello attributes **KernelShape**, **Stride**, **Padding**, **LowerPad**, and **UpperPad**:</span></span>   

* <span data-ttu-id="a86f5-234">**KernelShape**: hello convolutional 번들에 대 한 각 커널의 정의 hello 차원을 (필수).</span><span class="sxs-lookup"><span data-stu-id="a86f5-234">**KernelShape**: (required) Defines hello dimensionality of each kernel for hello convolutional bundle.</span></span> <span data-ttu-id="a86f5-235">hello 값의 길이가 hello 번들의 hello 인자 수가 해당 하는 양의 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-235">hello value must be a tuple of positive integers with a length that equals hello arity of hello bundle.</span></span> <span data-ttu-id="a86f5-236">이 튜플의 각 구성 요소는 hello의 해당 구성 요소 보다 크지 않아야 합니다. **InputShape**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-236">Each component of this tuple must be no greater than hello corresponding component of **InputShape**.</span></span> 
* <span data-ttu-id="a86f5-237">**Stride**: (선택 사항) 정의 hello 슬라이딩 hello 중앙 노드 사이의 hello 거리에 있는 hello 회선 (각 차원에 대 한 단계 크기)의 단계 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-237">**Stride**: (optional) Defines hello sliding step sizes of hello convolution (one step size for each dimension), that is hello distance between hello central nodes.</span></span> <span data-ttu-id="a86f5-238">hello 값의 hello 번들의 hello 인자가 길이가 양의 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-238">hello value must be a tuple of positive integers with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="a86f5-239">이 튜플의 각 구성 요소는 hello의 해당 구성 요소 보다 크지 않아야 합니다. **KernelShape**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-239">Each component of this tuple must be no greater than hello corresponding component of **KernelShape**.</span></span> <span data-ttu-id="a86f5-240">hello 기본값은 모든 구성 요소 같은 tooone 된 튜플의입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-240">hello default value is a tuple with all components equal tooone.</span></span> 
* <span data-ttu-id="a86f5-241">**공유**: (선택 사항) 정의 hello 가중치 hello 회선의 각 차원에 대 한 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-241">**Sharing**: (optional) Defines hello weight sharing for each dimension of hello convolution.</span></span> <span data-ttu-id="a86f5-242">hello 값은 단일 부울 값 또는 부울 값 hello 번들의 hello 인자가 길이가 튜플 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-242">hello value can be a single Boolean value or a tuple of Boolean values with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="a86f5-243">단일 부울 값이 모든 구성 요소와 hello 올바른 길이의 튜플이 확장된 toobe 같은 toohello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-243">A single Boolean value is extended toobe a tuple of hello correct length with all components equal toohello specified value.</span></span> <span data-ttu-id="a86f5-244">hello 기본값은 모든 True 값의 구성 된 튜플을입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-244">hello default value is a tuple that consists of all True values.</span></span> 
* <span data-ttu-id="a86f5-245">**MapCount**: hello convolutional 번들에 대 한 기능의 정의 hello 번호 (선택 사항)에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-245">**MapCount**: (optional) Defines hello number of feature maps for hello convolutional bundle.</span></span> <span data-ttu-id="a86f5-246">hello 번들의 hello 인자가 길이가 정수 튜플 또는 단일 양의 정수 hello 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-246">hello value can be a single positive integer or a tuple of positive integers with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="a86f5-247">단일 정수 값 toobe 확장은 값과 모든 나머지 구성 요소 같은 tooone hello hello 첫 번째 구성 요소 같은 toohello와 hello 올바른 길이의 튜플을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-247">A single integer value is extended toobe a tuple of hello correct length with hello first components equal toohello specified value and all hello remaining components equal tooone.</span></span> <span data-ttu-id="a86f5-248">hello 기본 값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-248">hello default value is one.</span></span> <span data-ttu-id="a86f5-249">기능 맵 hello 총 수는 hello 제품 hello 튜플의 hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-249">hello total number of feature maps is hello product of hello components of hello tuple.</span></span> <span data-ttu-id="a86f5-250">hello 구성 요소에서이 총 개수 팩터링 hello hello 대상 노드 hello 기능 맵 값 그룹화 되는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-250">hello factoring of this total number across hello components determines how hello feature map values are grouped in hello destination nodes.</span></span> 
* <span data-ttu-id="a86f5-251">**가중치**: hello 번들에 대 한 (선택 사항) 정의 hello 초기 가중치입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-251">**Weights**: (optional) Defines hello initial weights for hello bundle.</span></span> <span data-ttu-id="a86f5-252">hello 값의 부동 소수점 값이이 문서의 뒷부분에 정의 된 대로 hello 수 커널 당 가중치 커널 시간 hello 수 있는 길이가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-252">hello value must be a tuple of floating point values with a length that is hello number of kernels times hello number of weights per kernel, as defined later in this article.</span></span> <span data-ttu-id="a86f5-253">hello 기본 가중치는 임의로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-253">hello default weights are randomly generated.</span></span>  

<span data-ttu-id="a86f5-254">안쪽 여백 상호 배타적인 되 고 hello 속성을 제어 하는 속성의 두 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-254">There are two sets of properties that control padding, hello properties being mutually exclusive:</span></span>

* <span data-ttu-id="a86f5-255">**패딩**: (선택 사항) Determines hello 입력 여부 채워져야를 사용 하 여 한 **기본 패딩 구성표**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-255">**Padding**: (optional) Determines whether hello input should be padded by using a **default padding scheme**.</span></span> <span data-ttu-id="a86f5-256">hello 값일 수는 단일 부울 값 또는 hello 번들의 hello 인자가 있는 길이 사용 하 여 부울 값의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-256">hello value can be a single Boolean value, or it can be a tuple of Boolean values with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="a86f5-257">단일 부울 값이 모든 구성 요소와 hello 올바른 길이의 튜플이 확장된 toobe 같은 toohello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-257">A single Boolean value is extended toobe a tuple of hello correct length with all components equal toohello specified value.</span></span> <span data-ttu-id="a86f5-258">해당 차원에서 첫 번째 및 마지막 커널 hello hello 중앙 노드는 hello 첫 번째 및 마지막 노드 되도록 hello 소스 값이 0 인 셀 toosupport 추가 커널 응용 프로그램과 해당 차원에 패딩 논리적으로 차원에 대 한 hello 값이 True 이면 hello 원본 계층에서 해당 차원의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-258">If hello value for a dimension is True, hello source is logically padded in that dimension with zero-valued cells toosupport additional kernel applications, such that hello central nodes of hello first and last kernels in that dimension are hello first and last nodes in that dimension in hello source layer.</span></span> <span data-ttu-id="a86f5-259">따라서 각 차원에 있는 "dummy" 노드 hello 수는 자동으로 결정 toofit 정확 하 게 *(InputShape [d]-1) [d] Stride / + 1* 패딩 hello 원본 계층으로 커널을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-259">Thus, hello number of "dummy" nodes in each dimension is determined automatically, toofit exactly *(InputShape[d] - 1) / Stride[d] + 1* kernels into hello padded source layer.</span></span> <span data-ttu-id="a86f5-260">차원에 대 한 hello 값이 False 인 경우 hello의 각 면으로 남아 있는 노드 hello 수 있도록 커널 정의 됩니다 (위쪽 1 tooa 차이) 동일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-260">If hello value for a dimension is False, hello kernels are defined so that hello number of nodes on each side that are left out is hello same (up tooa difference of 1).</span></span> <span data-ttu-id="a86f5-261">모든 구성 요소 같은 tooFalse와 튜플이 hello이이 특성의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-261">hello default value of this attribute is a tuple with all components equal tooFalse.</span></span>
* <span data-ttu-id="a86f5-262">**UpperPad** 및 **LowerPad**: (선택 사항) 제공 대 한 제어 강화 패딩 toouse hello 양입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-262">**UpperPad** and **LowerPad**: (optional) Provide greater control over hello amount of padding toouse.</span></span> <span data-ttu-id="a86f5-263">**중요:** 경우에 hello 이러한 특성을 정의할 수 있습니다 **패딩** 위의 속성은 ***하지*** 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-263">**Important:** These attributes can be defined if and only if hello **Padding** property above is ***not*** defined.</span></span> <span data-ttu-id="a86f5-264">hello 값 튜플 길이 hello 번들의 hello 인자 수는 정수 값 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-264">hello values should be integer-valued tuples with lengths that are hello arity of hello bundle.</span></span> <span data-ttu-id="a86f5-265">이러한 특성을 지정 하는 경우 "dummy" 노드를 더 낮은 toohello 추가 하 고 위쪽 끝 hello의 각 차원 계층을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-265">When these attributes are specified, "dummy" nodes are added toohello lower and upper ends of each dimension of hello input layer.</span></span> <span data-ttu-id="a86f5-266">hello 노드 수가 추가 toohello 아래쪽 및 위쪽 끝 각 차원에 따라 사용자가 **LowerPad**[i] 및 **UpperPad**[i] 각각.</span><span class="sxs-lookup"><span data-stu-id="a86f5-266">hello number of nodes added toohello lower and upper ends in each dimension is determined by **LowerPad**[i] and **UpperPad**[i] respectively.</span></span> <span data-ttu-id="a86f5-267">tooensure 커널 모니터는 너무만 "실제" 노드, 하지 너무 "dummy" 노드 hello 다음 조건이 충족 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-267">tooensure that kernels correspond only too"real" nodes and not too"dummy" nodes, hello following conditions must be met:</span></span>
  * <span data-ttu-id="a86f5-268">**LowerPad**의 각 구성 요소는 KernelShape[d]/2보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-268">Each component of **LowerPad** must be strictly less than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="a86f5-269">**UpperPad**의 각 구성 요소는 KernelShape[d]/2보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-269">Each component of **UpperPad** must be no greater than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="a86f5-270">이러한 특성의 기본값 hello와 모든 구성 요소 같은 too0 튜플이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-270">hello default value of these attributes is a tuple with all components equal too0.</span></span> 

<span data-ttu-id="a86f5-271">hello 설정을 **패딩** = true 그대로 안쪽 여백 tookeep hello "센터" hello 커널의 "real"를 입력 하는 hello 내 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-271">hello setting **Padding** = true allows as much padding as is needed tookeep hello "center" of hello kernel inside hello "real" input.</span></span> <span data-ttu-id="a86f5-272">이렇게 hello 수학 hello 출력 크기를 계산 하는 데 약간 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-272">This changes hello math a bit for computing hello output size.</span></span> <span data-ttu-id="a86f5-273">Hello 크기를 출력 하는 일반적으로 *D* 로 계산 *D (I-K) = / S + 1*여기서 *I* 크기를 입력 하는 hello, *K* hello 커널 크기가 *S* hello stride는 및  */*  는 정수 나누기 (소수점 둥근).</span><span class="sxs-lookup"><span data-stu-id="a86f5-273">Generally, hello output size *D* is computed as *D = (I - K) / S + 1*, where *I* is hello input size, *K* is hello kernel size, *S* is hello stride, and */* is integer division (round toward zero).</span></span> <span data-ttu-id="a86f5-274">= UpperPad를 설정한 경우 [1, 1] hello 크기를 입력 *I* 29은 사실상 이므로 *D = (29-5) / 2 + 1 = 13*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-274">If you set UpperPad = [1, 1], hello input size *I* is effectively 29, and thus *D = (29 - 5) / 2 + 1 = 13*.</span></span> <span data-ttu-id="a86f5-275">그러나 **Padding** = true인 경우 기본적으로 *I*는 *K - 1*만큼 증가합니다. 따라서 *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-275">However, when **Padding** = true, essentially *I* gets bumped up by *K - 1*; hence *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*.</span></span> <span data-ttu-id="a86f5-276">에 대 한 값을 지정 하 여 **UpperPad** 및 **LowerPad** 훨씬 더 많이 제어할 패딩 경우 보다 있습니다 ड ि hello 얻게 **패딩** = true입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-276">By specifying values for **UpperPad** and **LowerPad** you get much more control over hello padding than if you just set **Padding** = true.</span></span>

<span data-ttu-id="a86f5-277">나선형 네트워크 및 해당 응용 프로그램에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a86f5-277">For more information about convolutional networks and their applications, see these articles:</span></span>  

* [<span data-ttu-id="a86f5-278">http://deeplearning.net/tutorial/lenet.html </span><span class="sxs-lookup"><span data-stu-id="a86f5-278">http://deeplearning.net/tutorial/lenet.html </span></span>](http://deeplearning.net/tutorial/lenet.html)
* [<span data-ttu-id="a86f5-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span><span class="sxs-lookup"><span data-stu-id="a86f5-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span></span>](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [<span data-ttu-id="a86f5-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span><span class="sxs-lookup"><span data-stu-id="a86f5-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span></span>](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a><span data-ttu-id="a86f5-281">풀링 번들</span><span class="sxs-lookup"><span data-stu-id="a86f5-281">Pooling bundles</span></span>
<span data-ttu-id="a86f5-282">A **번들 풀링** geometry 비슷한 tooconvolutional 연결을 적용 하지만 미리 정의 된 함수 toosource 노드 값 tooderive hello 대상 노드 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-282">A **pooling bundle** applies geometry similar tooconvolutional connectivity, but it uses predefined functions toosource node values tooderive hello destination node value.</span></span> <span data-ttu-id="a86f5-283">또한 풀링 번들에는 학습 가능 상태가 없습니다(가중치 또는 편차).</span><span class="sxs-lookup"><span data-stu-id="a86f5-283">Hence, pooling bundles have no trainable state (weights or biases).</span></span> <span data-ttu-id="a86f5-284">풀링 convolutional 특성을 제외한 모든 hello 번들 지원 **공유**, **MapCount**, 및 **가중치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-284">Pooling bundles support all hello convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

<span data-ttu-id="a86f5-285">일반적으로 인접 한 장치를 풀링 하 여 요약 된 hello 커널 중첩 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-285">Typically, hello kernels summarized by adjacent pooling units do not overlap.</span></span> <span data-ttu-id="a86f5-286">각 차원에 동일한 tooKernelShape [d] [d] Stride을 사용 하는 경우 가져온 hello 레이어는 hello 기존의 로컬 풀링 계층, convolutional 신경망에 일반적으로 사용 되는.</span><span class="sxs-lookup"><span data-stu-id="a86f5-286">If Stride[d] is equal tooKernelShape[d] in each dimension, hello layer obtained is hello traditional local pooling layer, which is commonly employed in convolutional neural networks.</span></span> <span data-ttu-id="a86f5-287">각 대상 노드는 최대 hello 또는 hello 원본 계층에서 해당 커널의 hello 활동의 hello 평균을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-287">Each destination node computes hello maximum or hello mean of hello activities of its kernel in hello source layer.</span></span>  

<span data-ttu-id="a86f5-288">다음 예제는 hello 풀링 번들을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-288">hello following example illustrates a pooling bundle:</span></span> 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* <span data-ttu-id="a86f5-289">hello 번들의 hello 인자 수는 3 (길이 만큼의 튜플 hello hello **InputShape**, **KernelShape**, 및 **Stride**).</span><span class="sxs-lookup"><span data-stu-id="a86f5-289">hello arity of hello bundle is 3 (hello length of hello tuples **InputShape**, **KernelShape**, and **Stride**).</span></span> 
* <span data-ttu-id="a86f5-290">hello hello 원본 계층의 노드 수는 *5 * 24 * 24 = 2880*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-290">hello number of nodes in hello source layer is *5 * 24 * 24 = 2880*.</span></span> 
* <span data-ttu-id="a86f5-291">**KernelShape** 및 **Stride**가 같으므로 이는 기존 로컬 풀링 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-291">This is a traditional local pooling layer because **KernelShape** and **Stride** are equal.</span></span> 
* <span data-ttu-id="a86f5-292">hello hello 대상 계층의 노드 수는 *5 * 12 * 12 = 1440*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-292">hello number of nodes in hello destination layer is *5 * 12 * 12 = 1440*.</span></span>  

<span data-ttu-id="a86f5-293">풀링 계층에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a86f5-293">For more information about pooling layers, see these articles:</span></span>  

* <span data-ttu-id="a86f5-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf)(섹션 3.4)</span><span class="sxs-lookup"><span data-stu-id="a86f5-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Section 3.4)</span></span>
* [<span data-ttu-id="a86f5-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span><span class="sxs-lookup"><span data-stu-id="a86f5-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span></span>](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [<span data-ttu-id="a86f5-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span><span class="sxs-lookup"><span data-stu-id="a86f5-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span></span>](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a><span data-ttu-id="a86f5-297">응답 정규화 번들</span><span class="sxs-lookup"><span data-stu-id="a86f5-297">Response normalization bundles</span></span>
<span data-ttu-id="a86f5-298">**응답 정규화** Geoffrey Hinton에서 처음 도입 된 로컬 정규화 체계 hello 백서에서 et al [Convolutional 심층 신경망와 ImageNet Classiﬁcation](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-298">**Response normalization** is a local normalization scheme that was first introduced by Geoffrey Hinton, et al, in hello paper [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf).</span></span> <span data-ttu-id="a86f5-299">응답 정규화는 신경망 네트워크에서 사용 되는 tooaid 일반화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-299">Response normalization is used tooaid generalization in neural nets.</span></span> <span data-ttu-id="a86f5-300">뉴런 하나를 정품 인증 매우 높은 수준에서 발생 하는 경우 로컬 응답 정규화 계층의 뉴런을 둘러싼 hello hello 활성화 수준을 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-300">When one neuron is firing at a very high activation level, a local response normalization layer suppresses hello activation level of hello surrounding neurons.</span></span> <span data-ttu-id="a86f5-301">이 작업에는 매개 변수 3개(***α***, ***β***, ***k***)와 나선형 구조(또는 환경 셰이프)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-301">This is done by using three parameters (***α***, ***β***, and ***k***) and a convolutional structure (or neighborhood shape).</span></span> <span data-ttu-id="a86f5-302">Hello 대상 계층의 모든 뉴런 ***y*** tooa 뉴런 하 나와 해당 ***x*** hello 원본 계층에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-302">Every neuron in hello destination layer ***y*** corresponds tooa neuron ***x*** in hello source layer.</span></span> <span data-ttu-id="a86f5-303">정품 인증 수준의 hello ***y*** 를 지정 하 여 다음 수식을, hello 여기서 ***f*** hello 활성화 수준의 뉴런에 및 ***Nx*** hello 커널 (또는 hello를 포함 하는 hello 집합 hello 환경에 대 한 뉴런 ***x***) hello convolutional 구조를 다음에 정의 된 대로,:</span><span class="sxs-lookup"><span data-stu-id="a86f5-303">hello activation level of ***y*** is given by hello following formula, where ***f*** is hello activation level of a neuron, and ***Nx*** is hello kernel (or hello set that contains hello neurons in hello neighborhood of ***x***), as defined by hello following convolutional structure:</span></span>  

![][1]  

<span data-ttu-id="a86f5-304">응답 정규화 번들 제외 하 고 hello convolutional 특성을 모두 지원 **공유**, **MapCount**, 및 **가중치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-304">Response normalization bundles support all hello convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

* <span data-ttu-id="a86f5-305">로 매핑 hello 커널 hello 뉴런을 포함 하는 경우 동일한 ***x***, hello 정규화 구성표는 참조 된 tooas **정규화를 매핑할 동일**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-305">If hello kernel contains neurons in hello same map as ***x***, hello normalization scheme is referred tooas **same map normalization**.</span></span> <span data-ttu-id="a86f5-306">정규화, hello 첫 번째 좌표에 동일한 매핑할 toodefine **InputShape** hello 값 1이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-306">toodefine same map normalization, hello first coordinate in **InputShape** must have hello value 1.</span></span>
* <span data-ttu-id="a86f5-307">Hello 커널 hello 뉴런을 포함 하는 경우와 같은 공간 위치 ***x***, hello 정규화 구성표 라고, hello 뉴런 다른 지도에 있지만 **across 정규화 매핑합니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-307">If hello kernel contains neurons in hello same spatial position as ***x***, but hello neurons are in other maps, hello normalization scheme is called **across maps normalization**.</span></span> <span data-ttu-id="a86f5-308">이 유형의 응답 정규화 측면 inhibition hello에에서 형식이 실제 뉴런 지도에 계산 뉴런 출력 간에 큰 정품 인증 수준에 대 한 경합은 만들기에서 영감을 얻은의 형태를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-308">This type of response normalization implements a form of lateral inhibition inspired by hello type found in real neurons, creating competition for big activation levels amongst neuron outputs computed on different maps.</span></span> <span data-ttu-id="a86f5-309">toodefine 정규화, hello 첫 번째 좌표 1 보다 크고 맵 hello 수보다 더 큰 정수 여야 합니다. 매핑하고 hello 좌표 hello 나머지 hello 값 1이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-309">toodefine across maps normalization, hello first coordinate must be an integer greater than one and no greater than hello number of maps, and hello rest of hello coordinates must have hello value 1.</span></span>  

<span data-ttu-id="a86f5-310">미리 정의 된 함수 toosource 노드 값 toodetermine hello 대상 노드 값을 적용 하는 응답 정규화 번들 (가중치 또는 편향) 트레인 할 수 있는 상태가 없는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-310">Because response normalization bundles apply a predefined function toosource node values toodetermine hello destination node value, they have no trainable state (weights or biases).</span></span>   

<span data-ttu-id="a86f5-311">**경고**: hello 대상 계층의 노드에서 hello 해당 tooneurons hello 커널의 hello 중앙 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-311">**Alert**: hello nodes in hello destination layer correspond tooneurons that are hello central nodes of hello kernels.</span></span> <span data-ttu-id="a86f5-312">예를 들어, 다음 KernelShape [d]는 홀수 이면 *KernelShape [d] / 2* toohello 중앙 커널 노드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-312">For example, if KernelShape[d] is odd, then *KernelShape[d]/2* corresponds toohello central kernel node.</span></span> <span data-ttu-id="a86f5-313">경우 *KernelShape [d]* hello 중앙 노드가,은 *KernelShape [d] / 2-1*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-313">If *KernelShape[d]* is even, hello central node is at *KernelShape[d]/2 - 1*.</span></span> <span data-ttu-id="a86f5-314">따라서 경우 **패딩**[d]가 False 이면 먼저 hello 및 마지막 hello *KernelShape [d] / 2* 노드에 hello 대상 계층에서 해당 노드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-314">Therefore, if **Padding**[d] is False, hello first and hello last *KernelShape[d]/2* nodes do not have corresponding nodes in hello destination layer.</span></span> <span data-ttu-id="a86f5-315">tooavoid이이 경우 정의 **패딩** 으로 [true 이면 true,..., true].</span><span class="sxs-lookup"><span data-stu-id="a86f5-315">tooavoid this situation, define **Padding** as [true, true, …, true].</span></span>  

<span data-ttu-id="a86f5-316">또한 toohello 네 가지 특성이 앞에서 설명한 정규화 번들 응답도 특성 뒤 지원 hello:</span><span class="sxs-lookup"><span data-stu-id="a86f5-316">In addition toohello four attributes described earlier, response normalization bundles also support hello following attributes:</span></span>  

* <span data-ttu-id="a86f5-317">**알파**: 너무 해당 하는 부동 소수점 값 (필수) 지정***α*** hello 이전 수식에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-317">**Alpha**: (required) Specifies a floating-point value that corresponds too***α*** in hello previous formula.</span></span> 
* <span data-ttu-id="a86f5-318">**베타**: 너무 해당 하는 부동 소수점 값 (필수) 지정***β*** hello 이전 수식에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-318">**Beta**: (required) Specifies a floating-point value that corresponds too***β*** in hello previous formula.</span></span> 
* <span data-ttu-id="a86f5-319">**오프셋**: 너무 해당는 부동 소수점 값을 지정 합니다 (옵션)***k*** hello 이전 수식에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-319">**Offset**: (optional) Specifies a floating-point value that corresponds too***k*** in hello previous formula.</span></span> <span data-ttu-id="a86f5-320">Too1을 기본값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-320">It defaults too1.</span></span>  

<span data-ttu-id="a86f5-321">hello 다음 예제에서는 이러한 특성을 사용 하 여 응답 정규화 번들:</span><span class="sxs-lookup"><span data-stu-id="a86f5-321">hello following example defines a response normalization bundle using these attributes:</span></span>  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* <span data-ttu-id="a86f5-322">hello 소스 계층 각각 aof 차원 1440 노드에, 총 12 x 12의 5 개 지도 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-322">hello source layer includes five maps, each with aof dimension of 12x12, totaling in 1440 nodes.</span></span> 
* <span data-ttu-id="a86f5-323">값을 hello **KernelShape** hello 환경은 3 x 3 사각형 같은 지도 정규화 계층 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-323">hello value of **KernelShape** indicates that this is a same map normalization layer, where hello neighborhood is a 3x3 rectangle.</span></span> 
* <span data-ttu-id="a86f5-324">기본값인 hello **패딩** 가 False 이면 따라서 hello 대상 계층에 10 개의 노드가 각 차원에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-324">hello default value of **Padding** is False, thus hello destination layer has only 10 nodes in each dimension.</span></span> <span data-ttu-id="a86f5-325">안쪽 여백을 추가 hello 원본 계층의 tooevery 노드에 해당 하는 hello 대상 계층의 한 노드에 tooinclude = [true, true, true]; 너무 RN1의 hello 크기를 변경 하 고 [5, 12, 12].</span><span class="sxs-lookup"><span data-stu-id="a86f5-325">tooinclude one node in hello destination layer that corresponds tooevery node in hello source layer, add Padding = [true, true, true]; and change hello size of RN1 too[5, 12, 12].</span></span>  

## <a name="share-declaration"></a><span data-ttu-id="a86f5-326">공유 선언</span><span class="sxs-lookup"><span data-stu-id="a86f5-326">Share declaration</span></span>
<span data-ttu-id="a86f5-327">Net#에서는 선택적으로 공유 가중치를 사용하여 여러 번들을 정의하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-327">Net# optionally supports defining multiple bundles with shared weights.</span></span> <span data-ttu-id="a86f5-328">해당 구조는 동일 hello는 경우 모든 두 번들의 hello 가중치를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-328">hello weights of any two bundles can be shared if their structures are hello same.</span></span> <span data-ttu-id="a86f5-329">hello 구문 다음에 가중치 공유 번들 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-329">hello following syntax defines bundles with shared weights:</span></span>  

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

<span data-ttu-id="a86f5-330">예를 들어 hello 다음 공유 선언 hello 레이어 이름을 지정를 나타내는 가중치와 편향 공유 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-330">For example, hello following share-declaration specifies hello layer names, indicating that both weights and biases should be shared:</span></span>  

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

* <span data-ttu-id="a86f5-331">hello 입력된 기능에 두 개의 동일한 크기의 입력된 계층으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-331">hello input features are partitioned into two equal sized input layers.</span></span> 
* <span data-ttu-id="a86f5-332">숨겨진 hello 레이어 hello 두 입력된 계층에 더 높은 수준 기능 계산 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-332">hello hidden layers then compute higher level features on hello two input layers.</span></span> 
* <span data-ttu-id="a86f5-333">hello 공유 선언 지정 *H1* 및 *H2* hello에 계산 되어야 해당 입력에서 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-333">hello share-declaration specifies that *H1* and *H2* must be computed in hello same way from their respective inputs.</span></span>  

<span data-ttu-id="a86f5-334">또는 다음과 같이 개별 공유 선언 두 개를 사용하여 이를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-334">Alternatively, this could be specified with two separate share-declarations as follows:</span></span>  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

<span data-ttu-id="a86f5-335">Hello 약식 hello 레이어에 단일 번들을 포함 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-335">You can use hello short form only when hello layers contain a single bundle.</span></span> <span data-ttu-id="a86f5-336">일반적으로 공유를 가능한 hello 관련 구조 hello 동일 동일한 convolutional geometry, 크기 등을 수 있는 의미와 동일한 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-336">In general, sharing is possible only when hello relevant structure is identical, meaning that they have hello same size, same convolutional geometry, and so forth.</span></span>  

## <a name="examples-of-net-usage"></a><span data-ttu-id="a86f5-337">Net# 사용의 예</span><span class="sxs-lookup"><span data-stu-id="a86f5-337">Examples of Net# usage</span></span>
<span data-ttu-id="a86f5-338">이 섹션에서는 몇 가지 사용 하는 방법을 Net # tooadd 숨겨진 계층 hello 방식이 숨겨진된 계층이 다른 계층 상호 작용 하 고 convolutional 네트워크 빌드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-338">This section provides some examples of how you can use Net# tooadd hidden layers, define hello way that hidden layers interact with other layers, and build convolutional networks.</span></span>   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a><span data-ttu-id="a86f5-339">단순 사용자 지정 신경망 정의: "Hello World" 예제</span><span class="sxs-lookup"><span data-stu-id="a86f5-339">Define a simple custom neural network: "Hello World" example</span></span>
<span data-ttu-id="a86f5-340">이 간단한 예제 toocreate 신경망 a에 하나의 숨겨진된 계층이 모델 네트워크 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-340">This simple example demonstrates how toocreate a neural network model that has a single hidden layer.</span></span>  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

<span data-ttu-id="a86f5-341">hello 예제는 다음과 같은 몇 가지 기본 명령의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-341">hello example illustrates some basic commands as follows:</span></span>  

* <span data-ttu-id="a86f5-342">hello 첫 번째 줄을 정의 hello 입력된 계층 (라는 *데이터*).</span><span class="sxs-lookup"><span data-stu-id="a86f5-342">hello first line defines hello input layer (named *Data*).</span></span> <span data-ttu-id="a86f5-343">Hello를 사용 하는 경우 **자동** 키워드를 hello 신경망 hello 입력된 예제에서 모든 기능 열이 자동으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-343">When you use hello  **auto** keyword, hello neural network automatically includes all feature columns in hello input examples.</span></span> 
* <span data-ttu-id="a86f5-344">두 번째 줄 hello hello 숨겨진된 계층을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-344">hello second line creates hello hidden layer.</span></span> <span data-ttu-id="a86f5-345">hello 이름 *H* 200 노드가 있는 toohello 숨겨진된 계층에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-345">hello name *H* is assigned toohello hidden layer, which has 200 nodes.</span></span> <span data-ttu-id="a86f5-346">이 계층은 완전히 연결 된 toohello 입력된 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-346">This layer is fully connected toohello input layer.</span></span>
* <span data-ttu-id="a86f5-347">세 번째 줄에서는 hello 정의 hello 출력 계층 (라는 *O*), 10 출력 노드를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-347">hello third line defines hello output layer (named *O*), which contains 10 output nodes.</span></span> <span data-ttu-id="a86f5-348">Hello 신경망 분류를 위해 사용 하는 경우 클래스 마다 출력 노드가 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-348">If hello neural network is used for classification, there is one output node per class.</span></span> <span data-ttu-id="a86f5-349">키워드 hello **시그모이드** hello 출력 함수 적용된 toohello 출력 계층 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-349">hello keyword **sigmoid** indicates that hello output function is applied toohello output layer.</span></span>   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a><span data-ttu-id="a86f5-350">여러 숨겨진 계층 정의: 컴퓨터 비전 예제</span><span class="sxs-lookup"><span data-stu-id="a86f5-350">Define multiple hidden layers: computer vision example</span></span>
<span data-ttu-id="a86f5-351">hello 다음 예제에서는 어떻게 toodefine 약간 더 복잡 한 신경망을 여러 개의 사용자 지정 숨겨진된 계층 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-351">hello following example demonstrates how toodefine a slightly more complex neural network, with multiple custom hidden layers.</span></span>  

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

<span data-ttu-id="a86f5-352">이 예제에서는 hello 신경망 사양 언어의 여러 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-352">This example illustrates several features of hello neural networks specification language:</span></span>  

* <span data-ttu-id="a86f5-353">hello 구조에 두 개의 입력된 계층으로 *픽셀* 및 *메타 데이터*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-353">hello structure has two input layers, *Pixels* and *MetaData*.</span></span>
* <span data-ttu-id="a86f5-354">hello *픽셀* 계층은 대상 계층으로 두 개의 연결 번들에 대 한 원본 계층 *ByRow* 및 *ByCol*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-354">hello *Pixels* layer is a source layer for two connection bundles, with destination layers, *ByRow* and *ByCol*.</span></span>
* <span data-ttu-id="a86f5-355">레이어 hello *수집* 및 *결과* 은 여러 연결 번들에서 대상 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-355">hello layers *Gather* and *Result* are destination layers in multiple connection bundles.</span></span>
* <span data-ttu-id="a86f5-356">hello 출력 계층 *결과*은 대상 계층으로 두 개의 연결 번들, 하나는 hello로 대상 계층으로 숨겨진된 (수집)를 두 번째 수준 및 대상 계층으로 hello와 hello 입력된 계층 (메타 데이터)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-356">hello output layer, *Result*, is a destination layer in two connection bundles; one with hello second level hidden (Gather) as a destination layer, and hello other with hello input layer (MetaData) as a destination layer.</span></span>
* <span data-ttu-id="a86f5-357">숨겨진된 계층을 hello *ByRow* 및 *ByCol*, 조건자 식을 사용 하 여 필터링 된 연결을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-357">hello hidden layers, *ByRow* and *ByCol*, specify filtered connectivity by using predicate expressions.</span></span> <span data-ttu-id="a86f5-358">보다 정확 하 게 hello 노드 *ByRow* 에서 [x, y]에서 연결 된 toohello 노드의 *픽셀* hello 첫 번째 인덱스 좌표 같은 toohello 노드의 첫 번째 좌표, x 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-358">More precisely, hello node in *ByRow* at [x, y] is connected toohello nodes in *Pixels* that have hello first index coordinate equal toohello node's first coordinate, x.</span></span> <span data-ttu-id="a86f5-359">마찬가지로, hello 노드에서 *[x, y]에서 ByCol _Pixels에 연결 된 toohello 노드의* hello hello 노드의 두 번째 좌표 중 하나에서 두 번째 인덱스 좌표에 있는 y 합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-359">Similarly, hello node in *ByCol at [x, y] is connected toohello nodes in _Pixels* that have hello second index coordinate within one of hello node's second coordinate, y.</span></span>  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a><span data-ttu-id="a86f5-360">다중 클래스 분류에 대한 나선형 네트워크 정의: 숫자 인식 예제</span><span class="sxs-lookup"><span data-stu-id="a86f5-360">Define a convolutional network for multiclass classification: digit recognition example</span></span>
<span data-ttu-id="a86f5-361">다음 네트워크 hello의 hello 정의 설계 된 toorecognize 번호 이며 신경망 사용자 지정에 대 한 고급 기술을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-361">hello definition of hello following network is designed toorecognize numbers, and it illustrates some advanced techniques for customizing a neural network.</span></span>  

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


* <span data-ttu-id="a86f5-362">hello 구조에는 단일 입력된 계층 *이미지*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-362">hello structure has a single input layer, *Image*.</span></span>
* <span data-ttu-id="a86f5-363">키워드 hello **convolve** hello 레이어 라는 나타냅니다 *Conv1* 및 *Conv2* convolutional 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-363">hello keyword **convolve** indicates that hello layers named *Conv1* and *Conv2* are convolutional layers.</span></span> <span data-ttu-id="a86f5-364">이러한 각 계층 선언은 hello 회선 특성 목록이 옵니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-364">Each of these layer declarations is followed by a list of hello convolution attributes.</span></span>
* <span data-ttu-id="a86f5-365">net hello 세 번째 숨겨진 계층을 *Hid3*는 완벽 하 게 연결 된 두 번째 숨겨진된 계층 toohello *Conv2*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-365">hello net has a third hidden layer, *Hid3*, which is fully connected toohello second hidden layer, *Conv2*.</span></span>
* <span data-ttu-id="a86f5-366">hello 출력 계층 *자리*, 연결 된 유일한 toohello 세 번째 숨겨진된 계층은 *Hid3*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-366">hello output layer, *Digit*, is connected only toohello third hidden layer, *Hid3*.</span></span> <span data-ttu-id="a86f5-367">키워드 hello **모든** 해당 hello 출력 계층은 완전히 너무 연결 나타냅니다*Hid3*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-367">hello keyword **all** indicates that hello output layer is fully connected too*Hid3*.</span></span>
* <span data-ttu-id="a86f5-368">hello hello 회선의 인자 수는 3 개입니다 (길이 만큼의 튜플 hello hello **InputShape**, **KernelShape**, **Stride**, 및 **공유**).</span><span class="sxs-lookup"><span data-stu-id="a86f5-368">hello arity of hello convolution is three (hello length of hello tuples **InputShape**, **KernelShape**, **Stride**, and **Sharing**).</span></span> 
* <span data-ttu-id="a86f5-369">커널 당 가중치 hello 수는 *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26입니다. 또는 26 * 50 = 1300*입니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-369">hello number of weights per kernel is *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape**\[2] = 1 + 1 * 5 * 5 = 26. Or 26 * 50 = 1300*.</span></span>
* <span data-ttu-id="a86f5-370">각 숨겨진된 계층의 hello 노드는 다음과 같이 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-370">You can calculate hello nodes in each hidden layer as follows:</span></span>
  * <span data-ttu-id="a86f5-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="a86f5-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span></span>
  * <span data-ttu-id="a86f5-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="a86f5-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5.</span></span> 
  * <span data-ttu-id="a86f5-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="a86f5-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5.</span></span> 
* <span data-ttu-id="a86f5-374">hello 총 노드 수 계산 hello의 차원을 선언 하는 hello를 사용 하 여 계층이 [50, 5, 5], 다음과 같이:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*</span><span class="sxs-lookup"><span data-stu-id="a86f5-374">hello total number of nodes can be calculated by using hello declared dimensionality of hello layer, [50, 5, 5], as follows: ***MapCount** * **NodeCount**\[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*</span></span>
* <span data-ttu-id="a86f5-375">때문에 **공유**[d]가 False에 대해서만 *d = = 0*, 커널 hello 수는  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*합니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-375">Because **Sharing**[d] is False only for *d == 0*, hello number of kernels is ***MapCount** * **NodeCount**\[0] = 10 * 5 = 50*.</span></span> 

## <a name="acknowledgements"></a><span data-ttu-id="a86f5-376">감사의 말</span><span class="sxs-lookup"><span data-stu-id="a86f5-376">Acknowledgements</span></span>
<span data-ttu-id="a86f5-377">Net # 신경망의 hello 아키텍처를 사용자 지정 하기 위한 언어 hello Shon Katzenberger (설계자, 기계 학습) 및 Alexey Kamenev (소프트웨어 엔지니어, Microsoft Research)에서 Microsoft에서 개발 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-377">hello Net# language for customizing hello architecture of neural networks was developed at Microsoft by Shon Katzenberger (Architect, Machine Learning) and Alexey Kamenev (Software Engineer, Microsoft Research).</span></span> <span data-ttu-id="a86f5-378">기계 학습 프로젝트와 이미지 검색 tootext 분석에서 사이의 응용 프로그램에 대 한 내부적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a86f5-378">It is used internally for machine learning projects and applications ranging from image detection tootext analytics.</span></span> <span data-ttu-id="a86f5-379">자세한 내용은 참조 [신경망 네트 Azure ML-소개 tooNet #에서](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span><span class="sxs-lookup"><span data-stu-id="a86f5-379">For more information, see [Neural Nets in Azure ML - Introduction tooNet#](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span></span>

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

