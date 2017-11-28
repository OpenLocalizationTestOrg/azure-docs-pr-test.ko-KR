---
title: "Azure Machine Learning Studio로 파일 데이터 가져오기 | Microsoft Docs"
description: "하드 드라이브에서 Azure Machine Learning Studio로 학습 데이터 파일을 업로드 하는 방법에 대해 알아봅니다. 이렇게 하면 작업 영역에 데이터 집합 모듈이 만들어집니다."
keywords: "데이터 가져오기, 데이터 형식, 데이터 유형, 데이터 원본, 학습 데이터"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="d2246-105">하드 드라이브의 파일에서 Machine Learning Studio로 학습 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2246-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="d2246-106">Azure Machine Learning Studio에서 학습 데이터로 사용할 하드 드라이브의 데이터 파일을 업로드하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="d2246-107">데이터 파일을 가져오면 작업 영역에서 사용할 수 있도록 데이터 집합 모듈을 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="d2246-108">로컬 파일에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2246-108">Steps to import data from a local file</span></span>
<span data-ttu-id="d2246-109">로컬 하드 드라이브에서 데이터를 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="d2246-110">기계 학습 스튜디오 창 하단에 있는 **+새로 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="d2246-111">**데이터 집합** 및 **로컬 파일에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="d2246-112">**새 데이터 집합 업로드** 대화 상자에서 업로드할 파일을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="d2246-113">이름을 입력하고, 데이터 형식을 식별하며, 선택적으로 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="d2246-114">설명을 사용하면 나중에 데이터를 사용할 때 기억하려는 데이터에 대한 특성을 기록할 수 있으므로 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="d2246-115">**기존 데이터 집합의 새로운 버전** 확인란을 사용하면 새 데이터로 기존 데이터 집합을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="d2246-116">이 확인란을 클릭한 다음 기존 데이터 집합의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![새 데이터 집합 업로드](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="d2246-118">업로드 중에 파일이 업로드 중임을 나타내는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="d2246-119">업로드 시간은 데이터의 크기와 서비스에 대한 연결 속도에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="d2246-120">파일이 오래 걸릴 것을 알고 있으면 기다리는 동안 기계 학습 스튜디오에서 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="d2246-121">그러나 브라우저를 닫으면 데이터 업로드에 실패하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="d2246-122">데이터 집합 모듈을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-122">Dataset module is ready for use</span></span>
<span data-ttu-id="d2246-123">데이터가 업로드되면 데이터 집합 모듈에 저장되고 작업 영역의 모든 실험에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="d2246-124">실험을 편집할 때 모듈 팔레트에 있는 **저장된 데이터 집합** 목록의 **내 데이터 집합** 목록에서 만든 데이터 집합을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="d2246-125">추가 분석 및 기계 학습을 위해 데이터 집합을 사용하려고 할 때 데이터 집합을 실험 캔버스에 끌어서 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2246-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
