---
title: "R로 실험 확장 | Microsoft Docs"
description: "R 스크립트 실행 모듈을 사용하여 R 언어를 통해 Azure 기계 학습 스튜디오의 기능을 확장하는 방법."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fe207ef917980be8b554ad9c08176d108b19fb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="df3da-103">R을 사용하여 실험 확장</span><span class="sxs-lookup"><span data-stu-id="df3da-103">Extend your experiment with R</span></span>
<span data-ttu-id="df3da-104">[R 스크립트 실행][execute-r-script] 모듈을 사용하여 R 언어를 통해 Azure Machine Learning Studio의 기능을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="df3da-105">이 모듈에서는 여러 입력 데이터 집합을 허용하고 출력으로 단일 데이터 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="df3da-106">[R 스크립트 실행][execute-r-script] 모듈의 **R 스크립트** 매개 변수에 R 스크립트를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="df3da-107">다음과 비슷한 코드를 사용하여 모듈의 각 입력 포트에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="df3da-108">현재 설치된 모든 패키지 나열</span><span class="sxs-lookup"><span data-stu-id="df3da-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="df3da-109">설치된 패키지 목록을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-109">The list of installed packages can change.</span></span> <span data-ttu-id="df3da-110">[Azure Machine Learning에서 지원하는 R 패키지](https://msdn.microsoft.com/library/azure/mt741980.aspx)에 현재 설치된 패키지의 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="df3da-111">[R 스크립트 실행][execute-r-script] 모듈에 다음 코드를 입력하여 설치된 패키지의 완전한 현재 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="df3da-112">[R 스크립트 실행][execute-r-script] 모듈의 출력 포트에 패키지의 목록을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="df3da-113">패키지 목록을 보려면 [CSV로 변환][convert-to-csv]과 같은 변환 모듈을 [R 스크립트 실행][execute-r-script] 모듈의 왼쪽 출력에 연결하고, 실험을 실행한 다음, 변환 모듈의 출력을 클릭하고 **다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

!["CSV로 변환" 모듈의 출력 다운로드](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="df3da-115">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="df3da-115">Importing packages</span></span>
<span data-ttu-id="df3da-116">[R 스크립트 실행][execute-r-script] 모듈에서 다음 명령을 사용하여 아직 설치되지 않은 패키지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="df3da-117">여기에서 `my_favorite_package.zip` 파일은 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df3da-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
