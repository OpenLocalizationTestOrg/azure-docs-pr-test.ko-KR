---
title: "Net# 신경망 사양 언어에 대한 가이드 | Microsoft Docs"
description: "구문은 Net # 신경망 사양 언어 Net #을 사용 하 여 Microsoft Azure 기계 학습에서 사용자 지정 신경망 모델을 만드는 방법에 대 한 예제와 함께 네트워크"
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
ms.openlocfilehash: 965c60ffde55041cc3864d06d81f5590c7ea1c11
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-net-neural-network-specification-language-for-azure-machine-learning"></a><span data-ttu-id="0b966-103">Azure 기계 학습용 Net# 신경망 사양 언어에 대한 가이드</span><span class="sxs-lookup"><span data-stu-id="0b966-103">Guide to Net# neural network specification language for Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="0b966-104">개요</span><span class="sxs-lookup"><span data-stu-id="0b966-104">Overview</span></span>
<span data-ttu-id="0b966-105">Net#은 Microsft에서 개발된 언어로 신경망 아키텍처를 정의하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-105">Net# is a language developed by Microsoft that is used to define neural network architectures.</span></span> <span data-ttu-id="0b966-106">Microsoft Azure Machine Learning의 신경망 모듈에서 Net#을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-106">You can use Net# in neural network modules in Microsoft Azure Machine Learning.</span></span>

<!-- This function doesn't currentlyappear in the MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in the `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

<span data-ttu-id="0b966-107">이 문서에서는 사용자 지정 신경망을 개발하는 데 필요한 기본 개념에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-107">In this article, you will learn basic concepts needed to develop a custom neural network:</span></span> 

* <span data-ttu-id="0b966-108">신경망 요구 사항 및 기본 구성 요소를 정의하는 방법</span><span class="sxs-lookup"><span data-stu-id="0b966-108">Neural network requirements and how to define the primary components</span></span>
* <span data-ttu-id="0b966-109">Net# 사양 언어의 구문 및 키워드</span><span class="sxs-lookup"><span data-stu-id="0b966-109">The syntax and keywords of the Net# specification language</span></span>
* <span data-ttu-id="0b966-110">Net #을 사용 하 여 만든 사용자 지정 신경망의 예</span><span class="sxs-lookup"><span data-stu-id="0b966-110">Examples of custom neural networks created using Net#</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a><span data-ttu-id="0b966-111">신경망 기본 사항</span><span class="sxs-lookup"><span data-stu-id="0b966-111">Neural network basics</span></span>
<span data-ttu-id="0b966-112">신경망 구조는 ***계층***으로 이루어진 ***노드*** 및 노드 간의 가중 ***연결***(또는 ***에지***)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-112">A neural network structure consists of ***nodes*** that are organized in ***layers***, and weighted ***connections*** (or ***edges***) between the nodes.</span></span> <span data-ttu-id="0b966-113">연결은 방향성이 있고 각 연결에는 ***원본*** 노드와 ***대상*** 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-113">The connections are directional, and each connection has a ***source*** node and a ***destination*** node.</span></span>  

<span data-ttu-id="0b966-114">각 ***학습 가능한 계층***(숨겨진 계층 또는 출력 계층)에는 하나 이상의 ***연결 번들***이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-114">Each ***trainable layer*** (a hidden or an output layer) has one or more ***connection bundles***.</span></span> <span data-ttu-id="0b966-115">연결 번들은 원본 계층 및 해당 원본 계층의 연결 지정으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-115">A connection bundle consists of a source layer and a specification of the connections from that source layer.</span></span> <span data-ttu-id="0b966-116">특정 번들의 모든 연결은 같은 ***원본 계층*** 및 같은 ***대상 계층***을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-116">All the connections in a given bundle share the same ***source layer*** and the same ***destination layer***.</span></span> <span data-ttu-id="0b966-117">Net#에서 연결 번들은 번들의 대상 계층에 속하는 것으로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-117">In Net#, a connection bundle is considered as belonging to the bundle's destination layer.</span></span>  

<span data-ttu-id="0b966-118">Net#에서는 입력이 숨겨진 계층 및 출력에 매핑되는 방법을 사용자 지정할 수 있는 다양한 종류의 연결 번들을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-118">Net# supports various kinds of connection bundles, which lets you customize the way inputs are mapped to hidden layers and mapped to the outputs.</span></span>   

<span data-ttu-id="0b966-119">기본 또는 표준 번들은 원본 계층의 각 노드가 대상 계층의 모든 노드에 연결된 **전체 번들**입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-119">The default or standard bundle is a **full bundle**, in which each node in the source layer is connected to every node in the destination layer.</span></span>  

<span data-ttu-id="0b966-120">또한 Net#에서는 다음 네 가지 고급 연결 번들을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-120">Additionally, Net# supports the following four kinds of advanced connection bundles:</span></span>  

* <span data-ttu-id="0b966-121">**필터링된 번들**.</span><span class="sxs-lookup"><span data-stu-id="0b966-121">**Filtered bundles**.</span></span> <span data-ttu-id="0b966-122">사용자는 원본 계층 노드와 대상 계층 노드의 위치를 사용하여 조건자를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-122">The user can define a predicate by using the locations of the source layer node and the destination layer node.</span></span> <span data-ttu-id="0b966-123">노드는 조건자가 True일 때마다 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-123">Nodes are connected whenever the predicate is True.</span></span>
* <span data-ttu-id="0b966-124">**나선형 번들**.</span><span class="sxs-lookup"><span data-stu-id="0b966-124">**Convolutional bundles**.</span></span> <span data-ttu-id="0b966-125">사용자는 원본 계층에서 작은 노드 환경을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-125">The user can define small neighborhoods of nodes in the source layer.</span></span> <span data-ttu-id="0b966-126">대상 계층의 각 노드는 원본 계층의 노드 환경 하나에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-126">Each node in the destination layer is connected to one neighborhood of nodes in the source layer.</span></span>
* <span data-ttu-id="0b966-127">**풀링 번들** 및 **응답 정규화 번들**.</span><span class="sxs-lookup"><span data-stu-id="0b966-127">**Pooling bundles** and **Response normalization bundles**.</span></span> <span data-ttu-id="0b966-128">이러한 번들은 사용자가 원본 계층에서 작은 노드 환경을 정의하는 나선형 번들과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-128">These are similar to convolutional bundles in that the user defines small neighborhoods of nodes in the source layer.</span></span> <span data-ttu-id="0b966-129">차이점은 이러한 번들의 에지 가중치는 학습할 수 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-129">The difference is that the weights of the edges in these bundles are not trainable.</span></span> <span data-ttu-id="0b966-130">대신 미리 정의된 함수가 원본 노드 값에 적용되어 대상 노드 값을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-130">Instead, a predefined function is applied to the source node values to determine the destination node value.</span></span>  

<span data-ttu-id="0b966-131">Net#을 사용하여 신경망 구조를 정의하면 이미지, 오디오 또는 비디오 같은 데이터에서 학습을 향상하는 것으로 알려진 임의 차원의 나선 또는 DNN(Deep Neural Network) 같은 복잡한 구조를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-131">Using Net# to define the structure of a neural network makes it possible to define complex structures such as deep neural networks or convolutions of arbitrary dimensions, which are known to improve learning on data such as image, audio, or video.</span></span>  

## <a name="supported-customizations"></a><span data-ttu-id="0b966-132">지원되는 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0b966-132">Supported customizations</span></span>
<span data-ttu-id="0b966-133">Azure 기계 학습에서 만드는 신경망 모델의 아키텍처는 Net#을 사용하여 광범위하게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-133">The architecture of neural network models that you create in Azure Machine Learning can be extensively customized by using Net#.</span></span> <span data-ttu-id="0b966-134">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-134">You can:</span></span>  

* <span data-ttu-id="0b966-135">숨겨진 계층을 만들고 각 계층의 노드 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-135">Create hidden layers and control the number of nodes in each layer.</span></span>
* <span data-ttu-id="0b966-136">계층이 서로 연결되는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-136">Specify how layers are to be connected to each other.</span></span>
* <span data-ttu-id="0b966-137">나선 및 가중 공유 번들과 같은 특수 연결 구조를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-137">Define special connectivity structures, such as convolutions and weight sharing bundles.</span></span>
* <span data-ttu-id="0b966-138">여러 가지 활성화 함수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-138">Specify different activation functions.</span></span>  

<span data-ttu-id="0b966-139">사양 언어 구문에 대한 자세한 내용은 [구조 사양](#Structure-specifications)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b966-139">For details of the specification language syntax, see [Structure Specification](#Structure-specifications).</span></span>  

<span data-ttu-id="0b966-140">일부 일반적인 Machine Learning 태스크에 대한 신경망 정의의 예는 [예제](#Examples-of-Net#-usage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b966-140">For examples of defining neural networks for some common machine learning tasks, from simplex to complex, see [Examples](#Examples-of-Net#-usage).</span></span>  

## <a name="general-requirements"></a><span data-ttu-id="0b966-141">일반 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0b966-141">General requirements</span></span>
* <span data-ttu-id="0b966-142">정확히 출력 계층 1개, 입력 계층 1개 이상, 숨겨진 계층 0개 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-142">There must be exactly one output layer, at least one input layer, and zero or more hidden layers.</span></span> 
* <span data-ttu-id="0b966-143">각 계층에는 개념적으로 임의 차원의 사각형 배열로 정렬된 고정된 수의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-143">Each layer has a fixed number of nodes, conceptually arranged in a rectangular array of arbitrary dimensions.</span></span> 
* <span data-ttu-id="0b966-144">입력 계층은 연결된 학습된 매개 변수를 포함하지 않고 인스턴스 데이터가 네트워크에 들어가는 지점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-144">Input layers have no associated trained parameters and represent the point where instance data enters the network.</span></span> 
* <span data-ttu-id="0b966-145">학습 가능 계층(숨겨진 계층 및 출력 계층)에는 가중치 및 편차라는 연결된 학습된 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-145">Trainable layers (the hidden and output layers) have associated trained parameters, known as weights and biases.</span></span> 
* <span data-ttu-id="0b966-146">원본 및 대상 노드는 서로 다른 계층에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-146">The source and destination nodes must be in separate layers.</span></span> 
* <span data-ttu-id="0b966-147">연결은 비순환 방식이어야 합니다. 즉, 초기 원본 노드로 돌아가는 연결 체인은 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-147">Connections must be acyclic; in other words, there cannot be a chain of connections leading back to the initial source node.</span></span>
* <span data-ttu-id="0b966-148">출력 계층은 연결 번들의 원본 계층일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-148">The output layer cannot be a source layer of a connection bundle.</span></span>  

## <a name="structure-specifications"></a><span data-ttu-id="0b966-149">구조 사양</span><span class="sxs-lookup"><span data-stu-id="0b966-149">Structure specifications</span></span>
<span data-ttu-id="0b966-150">신경망 구조 사양은 세 가지 섹션인 **상수 선언**, **계층 선언**, **연결 선언**으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-150">A neural network structure specification is composed of three sections: the **constant declaration**, the **layer declaration**, the **connection declaration**.</span></span> <span data-ttu-id="0b966-151">또한 선택적 **공유 선언** 섹션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-151">There is also an optional **share declaration** section.</span></span> <span data-ttu-id="0b966-152">섹션은 순서와 관계없이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-152">The sections can be specified in any order.</span></span>  

## <a name="constant-declaration"></a><span data-ttu-id="0b966-153">상수 선언</span><span class="sxs-lookup"><span data-stu-id="0b966-153">Constant declaration</span></span>
<span data-ttu-id="0b966-154">상수 선언은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-154">A constant declaration is optional.</span></span> <span data-ttu-id="0b966-155">신경망 정의에서 사용되는 값을 정의하는 수단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-155">It provides a means to define values used elsewhere in the neural network definition.</span></span> <span data-ttu-id="0b966-156">선언문은 식별자, 등호, 값 식 순으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-156">The declaration statement consists of an identifier followed by an equal sign and a value expression.</span></span>   

<span data-ttu-id="0b966-157">예를 들어 다음 문은 상수 **x**를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-157">For example, the following statement defines a constant **x**:</span></span>  

    Const X = 28;  

<span data-ttu-id="0b966-158">상수를 동시에 두 개 이상 정의하려면 식별자 이름과 값을 중괄호로 묶고 세미콜론으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-158">To define two or more constants simultaneously, enclose the identifier names and values in braces, and separate them by using semicolons.</span></span> <span data-ttu-id="0b966-159">예:</span><span class="sxs-lookup"><span data-stu-id="0b966-159">For example:</span></span>  

    Const { X = 28; Y = 4; }  

<span data-ttu-id="0b966-160">각 대입 식의 오른쪽은 정수, 실수, 부울 값(True/False) 또는 수치 연산 식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-160">The right-hand side of each assignment expression can be an integer, a real number, a Boolean value (True or False), or a mathematical expression.</span></span> <span data-ttu-id="0b966-161">예:</span><span class="sxs-lookup"><span data-stu-id="0b966-161">For example:</span></span>  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a><span data-ttu-id="0b966-162">계층 선언</span><span class="sxs-lookup"><span data-stu-id="0b966-162">Layer declaration</span></span>
<span data-ttu-id="0b966-163">계층 선언은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-163">The layer declaration is required.</span></span> <span data-ttu-id="0b966-164">연결 번들 및 특성을 포함하여 계층의 크기와 원본을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-164">It defines the size and source of the layer, including its connection bundles and attributes.</span></span> <span data-ttu-id="0b966-165">선언문은 계층 이름(input, hidden 또는 output)으로 시작하고 계층 차원(양의 정수 튜플)이 뒤따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-165">The declaration statement starts with the name of the layer (input, hidden, or output), followed by the dimensions of the layer (a tuple of positive integers).</span></span> <span data-ttu-id="0b966-166">예:</span><span class="sxs-lookup"><span data-stu-id="0b966-166">For example:</span></span>  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* <span data-ttu-id="0b966-167">차원의 곱은 계층의 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-167">The product of the dimensions is the number of nodes in the layer.</span></span> <span data-ttu-id="0b966-168">이 예제에 있는 차원 두 개 [5,20]은 계층에 노드 100개가 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-168">In this example, there are two dimensions [5,20], which means there are  100 nodes in the layer.</span></span>
* <span data-ttu-id="0b966-169">계층은 순서와 관계없이 선언할 수 있지만 한 가지 예외가 있습니다. 입력 계층을 두 개 이상 정의하면 계층 선언 순서가 입력 데이터의 기능 순서와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-169">The layers can be declared in any order, with one exception: If more than one input layer is defined, the order in which they are declared must match the order of features in the input data.</span></span>  

<span data-ttu-id="0b966-170">계층의 노드 수가 자동으로 결정되도록 지정하려면 **자동** 키워드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-170">To specify that the number of nodes in a layer be determined automatically, use the **auto** keyword.</span></span> <span data-ttu-id="0b966-171">**auto** 키워드는 계층에 따라 다른 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-171">The **auto** keyword has different effects, depending on the layer:</span></span>  

* <span data-ttu-id="0b966-172">입력 계층 선언에서 노드 수는 입력 데이터의 기능 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-172">In an input layer declaration, the number of nodes is the number of features in the input data.</span></span>
* <span data-ttu-id="0b966-173">숨겨진 계층 선언에서 노드 수는 **숨겨진 노드 수**의 매개 변수 값으로 지정된 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-173">In a hidden layer declaration, the number of nodes is the number that is specified by the parameter value for **Number of hidden nodes**.</span></span> 
* <span data-ttu-id="0b966-174">출력 계층 선언에서 노드 수는 2클래스 분류에 대해 2, 회귀에 대해 1이고 다중 클래스 분류에 대한 출력 노드 수와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-174">In an output layer declaration, the number of nodes is 2 for two-class classification, 1 for regression, and equal to the number of output nodes for multiclass classification.</span></span>   

<span data-ttu-id="0b966-175">예를 들어 다음 네트워크 정의에서는 모든 계층 크기가 자동으로 결정되도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-175">For example, the following network definition allows the size of all layers to be automatically determined:</span></span>  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


<span data-ttu-id="0b966-176">학습 가능 계층(숨겨진 계층 또는 출력 계층)에 대한 계층 선언은 선택적으로 활성화 함수라는 출력 함수를 포함할 수 있습니다(기본값: 분류 모델의 경우 **sigmoid**, 회귀 모델의 경우 **linear**).</span><span class="sxs-lookup"><span data-stu-id="0b966-176">A layer declaration for a trainable layer (the hidden or output layers) can optionally include the output function (also called an activation function), which defaults to **sigmoid** for classification models, and **linear** for regression models.</span></span> <span data-ttu-id="0b966-177">기본값을 사용하는 경우에도 명확한 설명을 위해 필요한 경우 활성화 함수를 명시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-177">(Even if you use the default, you can explicitly state the activation function, if desired for clarity.)</span></span>

<span data-ttu-id="0b966-178">다음 출력 함수가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-178">The following output functions are supported:</span></span>  

* <span data-ttu-id="0b966-179">sigmoid</span><span class="sxs-lookup"><span data-stu-id="0b966-179">sigmoid</span></span>
* <span data-ttu-id="0b966-180">linear</span><span class="sxs-lookup"><span data-stu-id="0b966-180">linear</span></span>
* <span data-ttu-id="0b966-181">softmax</span><span class="sxs-lookup"><span data-stu-id="0b966-181">softmax</span></span>
* <span data-ttu-id="0b966-182">rlinear</span><span class="sxs-lookup"><span data-stu-id="0b966-182">rlinear</span></span>
* <span data-ttu-id="0b966-183">square</span><span class="sxs-lookup"><span data-stu-id="0b966-183">square</span></span>
* <span data-ttu-id="0b966-184">sqrt</span><span class="sxs-lookup"><span data-stu-id="0b966-184">sqrt</span></span>
* <span data-ttu-id="0b966-185">srlinear</span><span class="sxs-lookup"><span data-stu-id="0b966-185">srlinear</span></span>
* <span data-ttu-id="0b966-186">abs</span><span class="sxs-lookup"><span data-stu-id="0b966-186">abs</span></span>
* <span data-ttu-id="0b966-187">tanh</span><span class="sxs-lookup"><span data-stu-id="0b966-187">tanh</span></span> 
* <span data-ttu-id="0b966-188">brlinear</span><span class="sxs-lookup"><span data-stu-id="0b966-188">brlinear</span></span>  

<span data-ttu-id="0b966-189">예를 들어 다음 선언은 **softmax** 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-189">For example, the following declaration uses the **softmax** function:</span></span>  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a><span data-ttu-id="0b966-190">연결 선언</span><span class="sxs-lookup"><span data-stu-id="0b966-190">Connection declaration</span></span>
<span data-ttu-id="0b966-191">학습 가능 계층을 정의한 후에 바로 정의한 계층 간의 연결을 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-191">Immediately after defining the trainable layer, you must declare connections among the layers you have defined.</span></span> <span data-ttu-id="0b966-192">연결 번들 선언은 키워드 **from**으로 시작하고 번들의 원본 계층 이름 및 만들 연결 번들 종류가 뒤따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-192">The connection bundle declaration starts with the keyword **from**, followed by the name of the bundle's source layer and the kind of connection bundle to create.</span></span>   

<span data-ttu-id="0b966-193">현재 다음 5가지 연결 번들이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-193">Currently, five kinds of connection bundles are supported:</span></span>  

* <span data-ttu-id="0b966-194">**전체** 번들 - 키워드 **all**로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-194">**Full** bundles, indicated by the keyword **all**</span></span>
* <span data-ttu-id="0b966-195">**필터링된** 번들 - 키워드 **where**로 나타내고 조건자 식이 뒤따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-195">**Filtered** bundles, indicated by the keyword **where**, followed by a predicate expression</span></span>
* <span data-ttu-id="0b966-196">**나선형** 번들 - 키워드 **convolve**로 나타내고 나선 특성이 뒤따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-196">**Convolutional** bundles, indicated by the keyword **convolve**, followed by the convolution attributes</span></span>
* <span data-ttu-id="0b966-197">**풀링** 번들 - 키워드 **max pool** 또는 **mean pool**로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-197">**Pooling** bundles, indicated by the keywords **max pool** or **mean pool**</span></span>
* <span data-ttu-id="0b966-198">**응답 정규화** 번들 - 키워드 **response norm**으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-198">**Response normalization** bundles, indicated by the keyword **response norm**</span></span>      

## <a name="full-bundles"></a><span data-ttu-id="0b966-199">전체 번들</span><span class="sxs-lookup"><span data-stu-id="0b966-199">Full bundles</span></span>
<span data-ttu-id="0b966-200">전체 연결 번들은 원본 계층의 각 노드에서 대상 계층의 각 노드로의 연결을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-200">A full connection bundle includes a connection from each node in the source layer to each node in the destination layer.</span></span> <span data-ttu-id="0b966-201">이 번들이 기본 네트워크 연결 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-201">This is the default network connection type.</span></span>  

## <a name="filtered-bundles"></a><span data-ttu-id="0b966-202">필터링된 번들</span><span class="sxs-lookup"><span data-stu-id="0b966-202">Filtered bundles</span></span>
<span data-ttu-id="0b966-203">필터링된 연결 번들 사양은 구문상 C# 람다 식과 훨씬 비슷하게 표현된 조건자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-203">A filtered connection bundle specification includes a predicate, expressed syntactically, much like a C# lambda expression.</span></span> <span data-ttu-id="0b966-204">다음 예제에서는 필터링된 번들 두 개를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-204">The following example defines two filtered bundles:</span></span>  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* <span data-ttu-id="0b966-205">*ByRow*에 대한 조건자에서 **s**는 입력 계층 *Pixels*의 사각형 노드 배열로 인덱스를 표시하는 매개 변수이고 **d**는 숨겨진 계층 *ByRow*의 노드 배열로 인덱스를 표시하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-205">In the predicate for *ByRow*, **s** is a parameter representing an index into the rectangular array of nodes of the input layer, *Pixels*, and **d** is a parameter representing an index into the array of nodes of the hidden layer, *ByRow*.</span></span> <span data-ttu-id="0b966-206">**s** 및 **d** 유형은 둘 다 길이가 2인 정수의 튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-206">The type of both **s** and **d** is a tuple of integers of length two.</span></span> <span data-ttu-id="0b966-207">개념적으로 **s**는 *0 <= s[0] < 10* 및 *0 <= s[1] < 20* 조건의 모든 정수 쌍을 포함하고 **d**는 *0 <= d[0] < 10* 및 *0 <= d[1] < 12* 조건의 모든 정수 쌍을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-207">Conceptually, **s** ranges over all pairs of integers with *0 <= s[0] < 10* and *0 <= s[1] < 20*, and **d** ranges over all pairs of integers, with *0 <= d[0] < 10* and *0 <= d[1] < 12*.</span></span> 
* <span data-ttu-id="0b966-208">조건자 식의 오른쪽에는 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-208">On the right-hand side of the predicate expression, there is a condition.</span></span> <span data-ttu-id="0b966-209">이 예제에서는 조건이 True가 되도록 **s** 및 **d**의 모든 값에 해당하는 원본 계층 노드에서 대상 계층 노드로의 에지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-209">In this example, for every value of **s** and **d** such that the condition is True, there is an edge from the source layer node to the destination layer node.</span></span> <span data-ttu-id="0b966-210">따라서 이 필터 식은 s[0]이 d[0]과 같은 모든 경우에 번들이 **s**로 정의된 노드에서 **d**로 정의된 노드로의 연결을 포함함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-210">Thus, this filter expression indicates that the bundle includes a connection from the node defined by **s** to the node defined by **d** in all cases where s[0] is equal to d[0].</span></span>  

<span data-ttu-id="0b966-211">선택적으로 필터링된 번들의 가중치 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-211">Optionally, you can specify a set of weights for a filtered bundle.</span></span> <span data-ttu-id="0b966-212">**Weights** 특성 값은 길이가 번들로 정의된 연결 수와 일치하는 부동 소수점 값의 튜플이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-212">The value for the **Weights** attribute must be a tuple of floating point values with a length that matches the number of connections defined by the bundle.</span></span> <span data-ttu-id="0b966-213">기본적으로 가중치는 임의로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-213">By default, weights are randomly generated.</span></span>  

<span data-ttu-id="0b966-214">가중치 값은 대상 노드 인덱스별로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-214">Weight values are grouped by the destination node index.</span></span> <span data-ttu-id="0b966-215">즉, 첫 번째 대상 노드가 K 원본 노드에 연결되면 **Weights** 튜플의 첫 번째 *K* 요소는 원본 인덱스 순서에서 첫 번째 대상 노드의 가중치입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-215">That is, if the first destination node is connected to K source nodes, the first *K* elements of the **Weights** tuple are the weights for the first destination node, in source index order.</span></span> <span data-ttu-id="0b966-216">나머지 대상 노드에서 같은 원리가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-216">The same applies for the remaining destination nodes.</span></span>  

<span data-ttu-id="0b966-217">가중치를 상수 값으로 직접 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-217">It's possible to specify weights directly as constant values.</span></span> <span data-ttu-id="0b966-218">예를 들어 이전에 가중치를 알고 있었다면 이 구문을 사용하여 해당 가중치를 상수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-218">For example, if you learned the weights previously, you can specify them as constants using this syntax:</span></span>

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a><span data-ttu-id="0b966-219">나선형 번들</span><span class="sxs-lookup"><span data-stu-id="0b966-219">Convolutional bundles</span></span>
<span data-ttu-id="0b966-220">학습 데이터에 같은 유형 구조가 있으면 일반적으로 데이터의 높은 수준 기능을 학습하는 데 나선형 연결이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-220">When the training data has a homogeneous structure, convolutional connections are commonly used to learn high-level features of the data.</span></span> <span data-ttu-id="0b966-221">예를 들어 이미지, 오디오 또는 비디오 데이터에서 공간 또는 임시 차원은 상당히 균일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-221">For example, in image, audio, or video data, spatial or temporal dimensionality can be fairly uniform.</span></span>  

<span data-ttu-id="0b966-222">나선형 번들에는 차원을 통해 움직이는 사각형 **커널**이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-222">Convolutional bundles employ rectangular **kernels** that are slid through the dimensions.</span></span> <span data-ttu-id="0b966-223">기본적으로 각 커널은 로컬 환경에 적용되는 **커널 응용 프로그램**이라는 가중치 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-223">Essentially, each kernel defines a set of weights applied in local neighborhoods, referred to as **kernel applications**.</span></span> <span data-ttu-id="0b966-224">각 커널 응용 프로그램은 **중앙 노드**라는 원본 계층의 노드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-224">Each kernel application corresponds to a node in the source layer, which is referred to as the **central node**.</span></span> <span data-ttu-id="0b966-225">커널의 가중치는 많은 연결에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-225">The weights of a kernel are shared among many connections.</span></span> <span data-ttu-id="0b966-226">나선형 번들에서 각 커널은 사각형이고 모든 커널 응용 프로그램은 같은 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-226">In a convolutional bundle, each kernel is rectangular and all kernel applications are the same size.</span></span>  

<span data-ttu-id="0b966-227">나선형 번들은 다음 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-227">Convolutional bundles support the following attributes:</span></span>

<span data-ttu-id="0b966-228">**InputShape**는 이 나선형 번들을 위한 원본 계층의 차원을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-228">**InputShape** defines the dimensionality of the source layer for the purposes of this convolutional bundle.</span></span> <span data-ttu-id="0b966-229">값은 양의 정수 튜플이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-229">The value must be a tuple of positive integers.</span></span> <span data-ttu-id="0b966-230">정수의 곱은 원본 계층의 노드 수와 같아야 하지만 원본 계층에 대해 선언된 차원과 일치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-230">The product of the integers must equal the number of nodes in the source layer, but otherwise, it does not need to match the dimensionality declared for the source layer.</span></span> <span data-ttu-id="0b966-231">이 튜플의 길이는 나선형 번들에 대한 **인자 수** 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-231">The length of this tuple becomes the **arity** value for the convolutional bundle.</span></span> <span data-ttu-id="0b966-232">일반적으로 인자 수는 함수가 사용할 수 있는 인수 또는 피연산자 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-232">(Typically arity refers to the number of arguments or operands that a function can take.)</span></span>  

<span data-ttu-id="0b966-233">커널의 셰이프와 위치를 정의하려면 **KernelShape**, **Stride**, **Padding**, **LowerPad**, **UpperPad** 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-233">To define the shape and locations of the kernels, use the attributes **KernelShape**, **Stride**, **Padding**, **LowerPad**, and **UpperPad**:</span></span>   

* <span data-ttu-id="0b966-234">**KernelShape**: (필수) 나선형 번들에 대한 각 커널의 차원을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-234">**KernelShape**: (required) Defines the dimensionality of each kernel for the convolutional bundle.</span></span> <span data-ttu-id="0b966-235">값은 길이가 번들 인자 수와 같은 양의 정수 튜플이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-235">The value must be a tuple of positive integers with a length that equals the arity of the bundle.</span></span> <span data-ttu-id="0b966-236">이 튜플의 각 구성 요소는 **InputShape**의 해당하는 구성 요소보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-236">Each component of this tuple must be no greater than the corresponding component of **InputShape**.</span></span> 
* <span data-ttu-id="0b966-237">**Stride**: (선택 사항) 중앙 노드 간의 거리인 나선의 이동식 단계 크기를 정의합니다(각 차원에 대해 단계 크기 하나).</span><span class="sxs-lookup"><span data-stu-id="0b966-237">**Stride**: (optional) Defines the sliding step sizes of the convolution (one step size for each dimension), that is the distance between the central nodes.</span></span> <span data-ttu-id="0b966-238">값은 길이가 번들 인자 수인 양의 정수 튜플이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-238">The value must be a tuple of positive integers with a length that is the arity of the bundle.</span></span> <span data-ttu-id="0b966-239">이 튜플의 각 구성 요소는 **KernelShape**의 해당하는 구성 요소보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-239">Each component of this tuple must be no greater than the corresponding component of **KernelShape**.</span></span> <span data-ttu-id="0b966-240">기본값은 모든 구성 요소가 1과 같은 튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-240">The default value is a tuple with all components equal to one.</span></span> 
* <span data-ttu-id="0b966-241">**Sharing**: (선택 사항) 나선의 각 차원에 대한 가중치 공유를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-241">**Sharing**: (optional) Defines the weight sharing for each dimension of the convolution.</span></span> <span data-ttu-id="0b966-242">값은 단일 부울 값 또는 길이가 번들 인자 수인 부울 값 튜플일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-242">The value can be a single Boolean value or a tuple of Boolean values with a length that is the arity of the bundle.</span></span> <span data-ttu-id="0b966-243">단일 부울 값은 모든 구성 요소가 지정된 값과 같은 올바른 길이의 튜플로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-243">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span></span> <span data-ttu-id="0b966-244">기본값은 모든 True 값으로 구성된 튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-244">The default value is a tuple that consists of all True values.</span></span> 
* <span data-ttu-id="0b966-245">**MapCount**: (선택 사항) 나선형 번들에 대한 기능 맵 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-245">**MapCount**: (optional) Defines the number of feature maps for the convolutional bundle.</span></span> <span data-ttu-id="0b966-246">값은 단일 양의 정수이거나 길이가 번들 인자 수인 양의 정수 튜플일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-246">The value can be a single positive integer or a tuple of positive integers with a length that is the arity of the bundle.</span></span> <span data-ttu-id="0b966-247">단일 정수 값은 첫 번째 구성 요소가 지정된 값과 같고 나머지 모든 구성 요소가 1과 같은 올바른 길이의 튜플로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-247">A single integer value is extended to be a tuple of the correct length with the first components equal to the specified value and all the remaining components equal to one.</span></span> <span data-ttu-id="0b966-248">기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-248">The default value is one.</span></span> <span data-ttu-id="0b966-249">총 기능 맵 수는 튜플 구성 요소의 곱입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-249">The total number of feature maps is the product of the components of the tuple.</span></span> <span data-ttu-id="0b966-250">전체 구성 요소에서 이 총 맵 수를 인수 분해하여 대상 노드에서 기능 맵 값을 그룹화하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-250">The factoring of this total number across the components determines how the feature map values are grouped in the destination nodes.</span></span> 
* <span data-ttu-id="0b966-251">**Weights**: (선택 사항) 번들에 대한 초기 가중치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-251">**Weights**: (optional) Defines the initial weights for the bundle.</span></span> <span data-ttu-id="0b966-252">값은 이 문서의 뒷부분에 정의된 대로 길이가 커널 수에 커널당 가중치 수를 곱한 값인 부동 소수점 값의 튜플이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-252">The value must be a tuple of floating point values with a length that is the number of kernels times the number of weights per kernel, as defined later in this article.</span></span> <span data-ttu-id="0b966-253">기본 가중치는 임의로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-253">The default weights are randomly generated.</span></span>  

<span data-ttu-id="0b966-254">안쪽 여백을 제어하는 상호 배타적인 두 가지 속성 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-254">There are two sets of properties that control padding, the properties being mutually exclusive:</span></span>

* <span data-ttu-id="0b966-255">**Padding**: (선택 사항) **기본 패딩 체계**를 사용하여 입력의 안쪽 여백을 지정해야 할지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-255">**Padding**: (optional) Determines whether the input should be padded by using a **default padding scheme**.</span></span> <span data-ttu-id="0b966-256">값은 단일 부울 값 또는 길이가 번들 인자 수인 부울 값 튜플일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-256">The value can be a single Boolean value, or it can be a tuple of Boolean values with a length that is the arity of the bundle.</span></span> <span data-ttu-id="0b966-257">단일 부울 값은 모든 구성 요소가 지정된 값과 같은 올바른 길이의 튜플로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-257">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span></span> <span data-ttu-id="0b966-258">차원 값이 True이면 추가 커널 응용 프로그램을 지원하도록 해당 차원에서 값이 0인 셀을 사용하여 원본의 안쪽 여백이 논리적으로 지정되므로 해당 차원에 있는 첫 번째 및 마지막 커널의 중앙 노드는 원본 계층에서 해당 차원에 있는 첫 번째 및 마지막 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-258">If the value for a dimension is True, the source is logically padded in that dimension with zero-valued cells to support additional kernel applications, such that the central nodes of the first and last kernels in that dimension are the first and last nodes in that dimension in the source layer.</span></span> <span data-ttu-id="0b966-259">따라서 각 차원의 "더미" 노드 수는 *(InputShape[d] - 1) / Stride[d] + 1* 커널을 안쪽 여백이 지정된 원본 계층에 정확히 맞추도록 자동으로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-259">Thus, the number of "dummy" nodes in each dimension is determined automatically, to fit exactly *(InputShape[d] - 1) / Stride[d] + 1* kernels into the padded source layer.</span></span> <span data-ttu-id="0b966-260">차원 값이 False이면 커널은 각 측면에 남아 있는 노드 수가 같도록 정의됩니다(최대 차이 1).</span><span class="sxs-lookup"><span data-stu-id="0b966-260">If the value for a dimension is False, the kernels are defined so that the number of nodes on each side that are left out is the same (up to a difference of 1).</span></span> <span data-ttu-id="0b966-261">이 특성의 기본값은 모든 구성 요소가 False와 같은 튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-261">The default value of this attribute is a tuple with all components equal to False.</span></span>
* <span data-ttu-id="0b966-262">**UpperPad** 및 **LowerPad**: (선택 사항) 사용할 안쪽 여백 크기를 더 구체적으로 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-262">**UpperPad** and **LowerPad**: (optional) Provide greater control over the amount of padding to use.</span></span> <span data-ttu-id="0b966-263">**Important:** 위의 **Padding** 속성이 정의되지 ***않은*** 경우에만 이러한 특성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-263">**Important:** These attributes can be defined if and only if the **Padding** property above is ***not*** defined.</span></span> <span data-ttu-id="0b966-264">값은 길이가 번들 인자 수인 정수 값 튜플이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-264">The values should be integer-valued tuples with lengths that are the arity of the bundle.</span></span> <span data-ttu-id="0b966-265">이러한 특성을 지정하면 "더미" 노드가 입력 계층에 있는 각 차원의 아래쪽 및 위쪽 끝에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-265">When these attributes are specified, "dummy" nodes are added to the lower and upper ends of each dimension of the input layer.</span></span> <span data-ttu-id="0b966-266">각 차원의 아래쪽 및 위쪽 끝에 추가되는 노드 수는 각각 **LowerPad**[i] 및 **UpperPad**[i]를 통해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-266">The number of nodes added to the lower and upper ends in each dimension is determined by **LowerPad**[i] and **UpperPad**[i] respectively.</span></span> <span data-ttu-id="0b966-267">커널이 "실제" 노드에만 해당하고 "더미" 노드에 해당하지 않도록 하려면 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-267">To ensure that kernels correspond only to "real" nodes and not to "dummy" nodes, the following conditions must be met:</span></span>
  * <span data-ttu-id="0b966-268">**LowerPad**의 각 구성 요소는 KernelShape[d]/2보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-268">Each component of **LowerPad** must be strictly less than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="0b966-269">**UpperPad**의 각 구성 요소는 KernelShape[d]/2보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-269">Each component of **UpperPad** must be no greater than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="0b966-270">이러한 특성의 기본값은 모든 구성 요소가 0과 같은 튜플입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-270">The default value of these attributes is a tuple with all components equal to 0.</span></span> 

<span data-ttu-id="0b966-271">**Padding** = true로 설정하면 최대한 많은 안쪽 여백을 사용하여 "실제" 입력 내 커널의 "중심"을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-271">The setting **Padding** = true allows as much padding as is needed to keep the "center" of the kernel inside the "real" input.</span></span> <span data-ttu-id="0b966-272">이 경우 출력 크기를 계산하는 수식이 약간 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-272">This changes the math a bit for computing the output size.</span></span> <span data-ttu-id="0b966-273">일반적으로 출력 크기 *D*는 *D = (I - K) / S + 1*로 계산됩니다. 여기서 *I*는 입력 크기, *K*는 커널 크기, *S*는 진행 속도, */*는 정수 나누기(0으로 반올림)입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-273">Generally, the output size *D* is computed as *D = (I - K) / S + 1*, where *I* is the input size, *K* is the kernel size, *S* is the stride, and */* is integer division (round toward zero).</span></span> <span data-ttu-id="0b966-274">UpperPad = [1, 1]로 설정한 경우 입력 크기 *I*는 사실상 29이므로 *D = (29 - 5) / 2 + 1 = 13*입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-274">If you set UpperPad = [1, 1], the input size *I* is effectively 29, and thus *D = (29 - 5) / 2 + 1 = 13*.</span></span> <span data-ttu-id="0b966-275">그러나 **Padding** = true인 경우 기본적으로 *I*는 *K - 1*만큼 증가합니다. 따라서 *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-275">However, when **Padding** = true, essentially *I* gets bumped up by *K - 1*; hence *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*.</span></span> <span data-ttu-id="0b966-276">**UpperPad** 및 **LowerPad** 값을 지정하면 **Padding** = true로 설정한 경우보다 안쪽 여백을 훨씬 구체적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-276">By specifying values for **UpperPad** and **LowerPad** you get much more control over the padding than if you just set **Padding** = true.</span></span>

<span data-ttu-id="0b966-277">나선형 네트워크 및 해당 응용 프로그램에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b966-277">For more information about convolutional networks and their applications, see these articles:</span></span>  

* [<span data-ttu-id="0b966-278">http://deeplearning.net/tutorial/lenet.html </span><span class="sxs-lookup"><span data-stu-id="0b966-278">http://deeplearning.net/tutorial/lenet.html </span></span>](http://deeplearning.net/tutorial/lenet.html)
* [<span data-ttu-id="0b966-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span><span class="sxs-lookup"><span data-stu-id="0b966-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span></span>](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [<span data-ttu-id="0b966-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span><span class="sxs-lookup"><span data-stu-id="0b966-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span></span>](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a><span data-ttu-id="0b966-281">풀링 번들</span><span class="sxs-lookup"><span data-stu-id="0b966-281">Pooling bundles</span></span>
<span data-ttu-id="0b966-282">**풀링 번들**은 나선형 연결과 비슷한 기하 도형에 적용되지만 원본 노드 값에 대한 미리 정의된 함수를 사용하여 대상 노드 값을 도출합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-282">A **pooling bundle** applies geometry similar to convolutional connectivity, but it uses predefined functions to source node values to derive the destination node value.</span></span> <span data-ttu-id="0b966-283">또한 풀링 번들에는 학습 가능 상태가 없습니다(가중치 또는 편차).</span><span class="sxs-lookup"><span data-stu-id="0b966-283">Hence, pooling bundles have no trainable state (weights or biases).</span></span> <span data-ttu-id="0b966-284">풀링 번들은 **Sharing**, **MapCount**, **Weights**를 제외하고 모든 나선형 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-284">Pooling bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

<span data-ttu-id="0b966-285">일반적으로 인접 풀링 단위로 요약된 커널은 겹치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-285">Typically, the kernels summarized by adjacent pooling units do not overlap.</span></span> <span data-ttu-id="0b966-286">각 차원에서 Stride[d]가 KernelShape[d]와 같으면 얻은 계층은 일반적으로 나선형 신경망에서 적용되는 기존 로컬 풀링 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-286">If Stride[d] is equal to KernelShape[d] in each dimension, the layer obtained is the traditional local pooling layer, which is commonly employed in convolutional neural networks.</span></span> <span data-ttu-id="0b966-287">각 대상 노드에서는 원본 계층에 있는 커널 활동의 최대값이나 평균을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-287">Each destination node computes the maximum or the mean of the activities of its kernel in the source layer.</span></span>  

<span data-ttu-id="0b966-288">다음 예제에서는 풀링 번들을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-288">The following example illustrates a pooling bundle:</span></span> 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* <span data-ttu-id="0b966-289">번들 인자 수는 3입니다(**InputShape**, **KernelShape** 및 **Stride** 튜플의 길이).</span><span class="sxs-lookup"><span data-stu-id="0b966-289">The arity of the bundle is 3 (the length of the tuples **InputShape**, **KernelShape**, and **Stride**).</span></span> 
* <span data-ttu-id="0b966-290">원본 계층의 노드 수는 *5 * 24 * 24 = 2880*입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-290">The number of nodes in the source layer is *5 * 24 * 24 = 2880*.</span></span> 
* <span data-ttu-id="0b966-291">**KernelShape** 및 **Stride**가 같으므로 이는 기존 로컬 풀링 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-291">This is a traditional local pooling layer because **KernelShape** and **Stride** are equal.</span></span> 
* <span data-ttu-id="0b966-292">대상 계층의 노드 수는 *5 * 12 * 12 = 1440*입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-292">The number of nodes in the destination layer is *5 * 12 * 12 = 1440*.</span></span>  

<span data-ttu-id="0b966-293">풀링 계층에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b966-293">For more information about pooling layers, see these articles:</span></span>  

* <span data-ttu-id="0b966-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf)(섹션 3.4)</span><span class="sxs-lookup"><span data-stu-id="0b966-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Section 3.4)</span></span>
* [<span data-ttu-id="0b966-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span><span class="sxs-lookup"><span data-stu-id="0b966-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span></span>](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [<span data-ttu-id="0b966-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span><span class="sxs-lookup"><span data-stu-id="0b966-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span></span>](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a><span data-ttu-id="0b966-297">응답 정규화 번들</span><span class="sxs-lookup"><span data-stu-id="0b966-297">Response normalization bundles</span></span>
<span data-ttu-id="0b966-298">**응답 정규화**는 Geoffrey Hinton 외 연구자가 [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) 논문에서 처음 도입한 로컬 정규화 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-298">**Response normalization** is a local normalization scheme that was first introduced by Geoffrey Hinton, et al, in the paper [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf).</span></span> <span data-ttu-id="0b966-299">응답 정규화는 신경망에서 일반화를 지원하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-299">Response normalization is used to aid generalization in neural nets.</span></span> <span data-ttu-id="0b966-300">신경 하나가 매우 높은 활성화 수준에서 실행되면 로컬 응답 정규화 계층에서는 주위 신경의 활성화 수준을 억제합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-300">When one neuron is firing at a very high activation level, a local response normalization layer suppresses the activation level of the surrounding neurons.</span></span> <span data-ttu-id="0b966-301">이 작업에는 매개 변수 3개(***α***, ***β***, ***k***)와 나선형 구조(또는 환경 셰이프)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-301">This is done by using three parameters (***α***, ***β***, and ***k***) and a convolutional structure (or neighborhood shape).</span></span> <span data-ttu-id="0b966-302">대상 계층 ***y***의 모든 신경은 원본 계층의 신경 ***x***에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-302">Every neuron in the destination layer ***y*** corresponds to a neuron ***x*** in the source layer.</span></span> <span data-ttu-id="0b966-303">***y***의 활성화 수준은 다음 공식으로 제공됩니다. 여기서 ***f***는 신경의 활성화 수준이고 ***Nx***는 나선형 구조를 통해 정의된 대로 ***x***의 환경에 신경이 포함된 집합 또는 커널입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-303">The activation level of ***y*** is given by the following formula, where ***f*** is the activation level of a neuron, and ***Nx*** is the kernel (or the set that contains the neurons in the neighborhood of ***x***), as defined by the following convolutional structure:</span></span>  

![][1]  

<span data-ttu-id="0b966-304">응답 정규화 번들은 **Sharing**, **MapCount**, **Weights**를 제외하고 모든 나선형 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-304">Response normalization bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

* <span data-ttu-id="0b966-305">커널에서 ***x***와 같은 맵에 신경이 포함되면 정규화 체계를 **동일 맵 정규화**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-305">If the kernel contains neurons in the same map as ***x***, the normalization scheme is referred to as **same map normalization**.</span></span> <span data-ttu-id="0b966-306">동일 맵 정규화를 정의하려면 **InputShape**의 첫 번째 좌표에 값 1이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-306">To define same map normalization, the first coordinate in **InputShape** must have the value 1.</span></span>
* <span data-ttu-id="0b966-307">커널에서 ***x***와 같은 공간 위치에 신경이 포함되지만 신경이 다른 맵에 있으면 이 정규화 체계를 **맵 간 정규화**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-307">If the kernel contains neurons in the same spatial position as ***x***, but the neurons are in other maps, the normalization scheme is called **across maps normalization**.</span></span> <span data-ttu-id="0b966-308">이 응답 정규화 유형은 실제 신경에 있는 유형에서 영향을 받은 측면 억제 형태를 구현하여 여러 맵에서 계산된 신경 출력 가운데 큰 활성화 수준에 대한 경쟁을 조성합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-308">This type of response normalization implements a form of lateral inhibition inspired by the type found in real neurons, creating competition for big activation levels amongst neuron outputs computed on different maps.</span></span> <span data-ttu-id="0b966-309">맵 간 정규화를 정의하려면 첫 번째 좌표가 1보다 크고 맵 수보다 큰 정수여야 하고 나머지 좌표는 값이 1이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-309">To define across maps normalization, the first coordinate must be an integer greater than one and no greater than the number of maps, and the rest of the coordinates must have the value 1.</span></span>  

<span data-ttu-id="0b966-310">응답 정규화 번들은 미리 정의된 함수를 원본 노드 값에 적용하여 대상 노드 값을 결정하므로 학습 가능 상태(가중치 또는 편차)가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-310">Because response normalization bundles apply a predefined function to source node values to determine the destination node value, they have no trainable state (weights or biases).</span></span>   

<span data-ttu-id="0b966-311">**Alert**: 대상 계층의 노드는 커널의 중앙 노드인 신경에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-311">**Alert**: The nodes in the destination layer correspond to neurons that are the central nodes of the kernels.</span></span> <span data-ttu-id="0b966-312">예를 들어 KernelShape[d]가 홀수이면 *KernelShape[d]/2*는 중앙 커널 노드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-312">For example, if KernelShape[d] is odd, then *KernelShape[d]/2* corresponds to the central kernel node.</span></span> <span data-ttu-id="0b966-313">*KernelShape[d]*가 짝수인 경우에는 중앙 노드가 *KernelShape[d]/2 - 1*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-313">If *KernelShape[d]* is even, the central node is at *KernelShape[d]/2 - 1*.</span></span> <span data-ttu-id="0b966-314">따라서 **Padding**[d]가 False이면 첫 번째 및 마지막 *KernelShape[d]/2* 노드에 해당하는 노드가 대상 계층에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-314">Therefore, if **Padding**[d] is False, the first and the last *KernelShape[d]/2* nodes do not have corresponding nodes in the destination layer.</span></span> <span data-ttu-id="0b966-315">이 상황을 피하려면 **Padding**을 [true, true, …, true]로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-315">To avoid this situation, define **Padding** as [true, true, …, true].</span></span>  

<span data-ttu-id="0b966-316">위에 설명된 네 가지 특성 이외에 응답 정규화 번들은 다음 특성도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-316">In addition to the four attributes described earlier, response normalization bundles also support the following attributes:</span></span>  

* <span data-ttu-id="0b966-317">**Alpha**: (필수) 위의 공식에서 ***α***에 해당하는 부동 소수점 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-317">**Alpha**: (required) Specifies a floating-point value that corresponds to ***α*** in the previous formula.</span></span> 
* <span data-ttu-id="0b966-318">**Beta**: (필수) 위의 공식에서 ***β***에 해당하는 부동 소수점 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-318">**Beta**: (required) Specifies a floating-point value that corresponds to ***β*** in the previous formula.</span></span> 
* <span data-ttu-id="0b966-319">**Offset**: (선택 사항) 위의 공식에서 ***k***에 해당하는 부동 소수점 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-319">**Offset**: (optional) Specifies a floating-point value that corresponds to ***k*** in the previous formula.</span></span> <span data-ttu-id="0b966-320">기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-320">It defaults to 1.</span></span>  

<span data-ttu-id="0b966-321">다음 예제에서는 이들 특성을 사용하여 응답 정규화 번들을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-321">The following example defines a response normalization bundle using these attributes:</span></span>  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* <span data-ttu-id="0b966-322">원본 계층에는 맵 5개가 포함되고 각 맵은 총 노드 수가 1440개인 12x12 차원입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-322">The source layer includes five maps, each with aof dimension of 12x12, totaling in 1440 nodes.</span></span> 
* <span data-ttu-id="0b966-323">**KernelShape** 값은 이 계층이 3x3 사각형 환경이 있는 같은 맵 정규화 계층임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-323">The value of **KernelShape** indicates that this is a same map normalization layer, where the neighborhood is a 3x3 rectangle.</span></span> 
* <span data-ttu-id="0b966-324">**Padding**의 기본값은 False이므로 대상 계층의 각 차원에는 노드가 10개만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-324">The default value of **Padding** is False, thus the destination layer has only 10 nodes in each dimension.</span></span> <span data-ttu-id="0b966-325">원본 계층의 각 노드에 해당하는 단일 노드를 대상 계층에 포함하려면 Padding = [true, true, true]를 추가하고 RN1 크기를 [5, 12, 12]로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-325">To include one node in the destination layer that corresponds to every node in the source layer, add Padding = [true, true, true]; and change the size of RN1 to [5, 12, 12].</span></span>  

## <a name="share-declaration"></a><span data-ttu-id="0b966-326">공유 선언</span><span class="sxs-lookup"><span data-stu-id="0b966-326">Share declaration</span></span>
<span data-ttu-id="0b966-327">Net#에서는 선택적으로 공유 가중치를 사용하여 여러 번들을 정의하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-327">Net# optionally supports defining multiple bundles with shared weights.</span></span> <span data-ttu-id="0b966-328">구조가 같으면 번들 두 개의 가중치를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-328">The weights of any two bundles can be shared if their structures are the same.</span></span> <span data-ttu-id="0b966-329">다음 구문에서는 공유 가중치를 사용하여 번들을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-329">The following syntax defines bundles with shared weights:</span></span>  

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

<span data-ttu-id="0b966-330">예를 들어 다음 공유 선언은 계층 이름을 지정하여 가중치 및 편차를 둘 다 공유하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-330">For example, the following share-declaration specifies the layer names, indicating that both weights and biases should be shared:</span></span>  

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

* <span data-ttu-id="0b966-331">입력 기능은 크기가 같은 입력 계층 두 개로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-331">The input features are partitioned into two equal sized input layers.</span></span> 
* <span data-ttu-id="0b966-332">숨겨진 계층에서는 입력 계층 두 개에서 더 높은 수준의 기능을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-332">The hidden layers then compute higher level features on the two input layers.</span></span> 
* <span data-ttu-id="0b966-333">공유 선언은 개별 입력에서 같은 방법으로 *H1* 및 *H2*를 계산하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-333">The share-declaration specifies that *H1* and *H2* must be computed in the same way from their respective inputs.</span></span>  

<span data-ttu-id="0b966-334">또는 다음과 같이 개별 공유 선언 두 개를 사용하여 이를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-334">Alternatively, this could be specified with two separate share-declarations as follows:</span></span>  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

<span data-ttu-id="0b966-335">계층에 단일 번들이 포함되어 있을 때만 약식 양식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-335">You can use the short form only when the layers contain a single bundle.</span></span> <span data-ttu-id="0b966-336">일반적으로 관련 구조가 동일하여 크기, 나선형 기하 도형 등이 같을 때만 공유가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-336">In general, sharing is possible only when the relevant structure is identical, meaning that they have the same size, same convolutional geometry, and so forth.</span></span>  

## <a name="examples-of-net-usage"></a><span data-ttu-id="0b966-337">Net# 사용의 예</span><span class="sxs-lookup"><span data-stu-id="0b966-337">Examples of Net# usage</span></span>
<span data-ttu-id="0b966-338">이 섹션에서는 Net#을 사용하여 숨겨진 계층을 추가하고 숨겨진 계층이 다른 계층을 조작하는 방법을 정의하고 나선형 네트워크를 빌드하는 방법의 몇 가지 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-338">This section provides some examples of how you can use Net# to add hidden layers, define the way that hidden layers interact with other layers, and build convolutional networks.</span></span>   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a><span data-ttu-id="0b966-339">단순 사용자 지정 신경망 정의: "Hello World" 예제</span><span class="sxs-lookup"><span data-stu-id="0b966-339">Define a simple custom neural network: "Hello World" example</span></span>
<span data-ttu-id="0b966-340">이 단순 예제에서는 단일 숨겨진 계층이 있는 신경망 모델을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-340">This simple example demonstrates how to create a neural network model that has a single hidden layer.</span></span>  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

<span data-ttu-id="0b966-341">이 예제에서는 다음과 같은 몇 가지 기본 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-341">The example illustrates some basic commands as follows:</span></span>  

* <span data-ttu-id="0b966-342">첫 번째 줄에서는 이름이 *Data*인 입력 계층을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-342">The first line defines the input layer (named *Data*).</span></span> <span data-ttu-id="0b966-343">**자동** 키워드를 사용하는 경우 신경망에 입력 예제의 모든 기능 열이 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-343">When you use the  **auto** keyword, the neural network automatically includes all feature columns in the input examples.</span></span> 
* <span data-ttu-id="0b966-344">두 번째 줄에서는 숨겨진 계층을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-344">The second line creates the hidden layer.</span></span> <span data-ttu-id="0b966-345">노드 200개가 포함된 숨겨진 계층에 이름 *H*가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-345">The name *H* is assigned to the hidden layer, which has 200 nodes.</span></span> <span data-ttu-id="0b966-346">이 계층은 입력 계층에 완전히 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-346">This layer is fully connected to the input layer.</span></span>
* <span data-ttu-id="0b966-347">세 번째 줄에서는 이름이 *O*이고 출력 노드 10개가 포함된 출력 계층을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-347">The third line defines the output layer (named *O*), which contains 10 output nodes.</span></span> <span data-ttu-id="0b966-348">신경망을 분류에 사용하는 경우 클래스당 하나의 출력 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-348">If the neural network is used for classification, there is one output node per class.</span></span> <span data-ttu-id="0b966-349">키워드 **sigmoid**는 출력 계층에 적용된 출력 함수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-349">The keyword **sigmoid** indicates that the output function is applied to the output layer.</span></span>   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a><span data-ttu-id="0b966-350">여러 숨겨진 계층 정의: 컴퓨터 비전 예제</span><span class="sxs-lookup"><span data-stu-id="0b966-350">Define multiple hidden layers: computer vision example</span></span>
<span data-ttu-id="0b966-351">다음 예제에서는 여러 사용자 지정 숨겨진 계층을 사용하여 약간 더 복잡한 신경망을 정의하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-351">The following example demonstrates how to define a slightly more complex neural network, with multiple custom hidden layers.</span></span>  

    // Define the input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define the first two hidden layers, using data only from the Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define the third hidden layer, which uses as source the hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define the output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

<span data-ttu-id="0b966-352">이 예제에서는 신경망 사양 언어의 여러 가지 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-352">This example illustrates several features of the neural networks specification language:</span></span>  

* <span data-ttu-id="0b966-353">구조에는 2개의 입력 계층인 *Pixels* 및 *MetaData*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-353">The structure has two input layers, *Pixels* and *MetaData*.</span></span>
* <span data-ttu-id="0b966-354">*Pixels* 계층은 대상 계층이 *ByRow* 및 *ByCol*인 두 연결 번들에 대한 원본 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-354">The *Pixels* layer is a source layer for two connection bundles, with destination layers, *ByRow* and *ByCol*.</span></span>
* <span data-ttu-id="0b966-355">*Gather* 및 *Result* 계층은 여러 연결 번들의 대상 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-355">The layers *Gather* and *Result* are destination layers in multiple connection bundles.</span></span>
* <span data-ttu-id="0b966-356">출력 계층인 *Result*는 각각 두 번째 수준 숨겨진 계층(Gather) 및 입력 계층(MetaData)이 대상 계층인 두 연결 번들의 대상 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-356">The output layer, *Result*, is a destination layer in two connection bundles; one with the second level hidden (Gather) as a destination layer, and the other with the input layer (MetaData) as a destination layer.</span></span>
* <span data-ttu-id="0b966-357">숨겨진 계층인 *ByRow* 및 *ByCol*은 조건자 식을 사용하여 필터링된 연결을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-357">The hidden layers, *ByRow* and *ByCol*, specify filtered connectivity by using predicate expressions.</span></span> <span data-ttu-id="0b966-358">보다 정확하게, [x, y]에 있는 *ByRow*의 노드는 첫 번째 인덱스 좌표가 노드의 첫 번째 좌표인 x와 동일한 *Pixels*의 노드에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-358">More precisely, the node in *ByRow* at [x, y] is connected to the nodes in *Pixels* that have the first index coordinate equal to the node's first coordinate, x.</span></span> <span data-ttu-id="0b966-359">이와 마찬가지로 [x, y]에 있는 *ByCol의 노드는 두 번째 인덱스 좌표가 노드의 두 번째 좌표인 y 중 하나 내에 있는 _Pixels*의 노드에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-359">Similarly, the node in *ByCol at [x, y] is connected to the nodes in _Pixels* that have the second index coordinate within one of the node's second coordinate, y.</span></span>  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a><span data-ttu-id="0b966-360">다중 클래스 분류에 대한 나선형 네트워크 정의: 숫자 인식 예제</span><span class="sxs-lookup"><span data-stu-id="0b966-360">Define a convolutional network for multiclass classification: digit recognition example</span></span>
<span data-ttu-id="0b966-361">숫자를 인식하도록 고안된 다음 네트워크 정의에서는 신경망 사용자 지정을 위한 몇 가지 고급 기법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-361">The definition of the following network is designed to recognize numbers, and it illustrates some advanced techniques for customizing a neural network.</span></span>  

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


* <span data-ttu-id="0b966-362">구조에는 단일 입력 계층인 *Image*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-362">The structure has a single input layer, *Image*.</span></span>
* <span data-ttu-id="0b966-363">키워드 **convolve**는 *Conv1* 및 *Conv2*라는 계층이 나선형 계층임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-363">The keyword **convolve** indicates that the layers named *Conv1* and *Conv2* are convolutional layers.</span></span> <span data-ttu-id="0b966-364">이러한 각 계층 선언 뒤에는 나선 특성 목록이 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-364">Each of these layer declarations is followed by a list of the convolution attributes.</span></span>
* <span data-ttu-id="0b966-365">네트워크에는 두 번째 숨겨진 계층인 *Conv2*에 완전히 연결된 세 번째 숨겨진 계층인 *Hid3*이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-365">The net has a third hidden layer, *Hid3*, which is fully connected to the second hidden layer, *Conv2*.</span></span>
* <span data-ttu-id="0b966-366">*Digit* 출력 계층은 세 번째 계층인 *Hid3*에만 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-366">The output layer, *Digit*, is connected only to the third hidden layer, *Hid3*.</span></span> <span data-ttu-id="0b966-367">키워드 **all**은 출력 계층이 *Hid3*에 완전히 연결되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-367">The keyword **all** indicates that the output layer is fully connected to *Hid3*.</span></span>
* <span data-ttu-id="0b966-368">나선 인자 수는 3입니다(**InputShape**, **KernelShape**, **Stride** 및 **Sharing** 튜플의 길이).</span><span class="sxs-lookup"><span data-stu-id="0b966-368">The arity of the convolution is three (the length of the tuples **InputShape**, **KernelShape**, **Stride**, and **Sharing**).</span></span> 
* <span data-ttu-id="0b966-369">커널당 가중치 수는 *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape**\[2] = 1 + 1 * 5 * 5 = 26입니다. 또는 26 * 50 = 1300*입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-369">The number of weights per kernel is *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape**\[2] = 1 + 1 * 5 * 5 = 26. Or 26 * 50 = 1300*.</span></span>
* <span data-ttu-id="0b966-370">다음과 같이 각 숨겨진 계층에서 노드를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-370">You can calculate the nodes in each hidden layer as follows:</span></span>
  * <span data-ttu-id="0b966-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="0b966-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span></span>
  * <span data-ttu-id="0b966-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="0b966-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5.</span></span> 
  * <span data-ttu-id="0b966-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="0b966-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5.</span></span> 
* <span data-ttu-id="0b966-374">총 노드 수는 계층의 선언된 차원인 [50, 5, 5]를 사용하여 ***MapCount** * **NodeCount**\[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*와 같이 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-374">The total number of nodes can be calculated by using the declared dimensionality of the layer, [50, 5, 5], as follows: ***MapCount** * **NodeCount**\[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*</span></span>
* <span data-ttu-id="0b966-375">**Sharing**[d]가 *d == 0*에 대해서만 False이므로 커널 수는 ***MapCount** * **NodeCount**\[0] = 10 * 5 = 50*입니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-375">Because **Sharing**[d] is False only for *d == 0*, the number of kernels is ***MapCount** * **NodeCount**\[0] = 10 * 5 = 50*.</span></span> 

## <a name="acknowledgements"></a><span data-ttu-id="0b966-376">감사의 말</span><span class="sxs-lookup"><span data-stu-id="0b966-376">Acknowledgements</span></span>
<span data-ttu-id="0b966-377">신경망 아키텍처를 사용자 지정하기 위한 Net# 언어는 Microsoft에서 Shon Katzenberger(설계자, 기계 학습) 및 Alexey Kamenev(소프트웨어 엔지니어, Microsoft Research)에 의해 개발되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-377">The Net# language for customizing the architecture of neural networks was developed at Microsoft by Shon Katzenberger (Architect, Machine Learning) and Alexey Kamenev (Software Engineer, Microsoft Research).</span></span> <span data-ttu-id="0b966-378">내부적으로 이미지 검색에서 텍스트 분석에 이르기까지 다양한 기계 학습 프로젝트 및 응용 프로그램에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b966-378">It is used internally for machine learning projects and applications ranging from image detection to text analytics.</span></span> <span data-ttu-id="0b966-379">자세한 내용은 [Azure ML의 신경망 - Net# 소개](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b966-379">For more information, see [Neural Nets in Azure ML - Introduction to Net#](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span></span>

<span data-ttu-id="0b966-380">[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif</span><span class="sxs-lookup"><span data-stu-id="0b966-380">[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif</span></span>

