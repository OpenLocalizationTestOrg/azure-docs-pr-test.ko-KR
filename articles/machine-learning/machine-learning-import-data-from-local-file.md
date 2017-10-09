---
title: "aaaImport 파일 데이터를 Azure 기계 학습 스튜디오로 | Microsoft Docs"
description: "프로그램 하드 드라이브 tooAzure 기계 학습 스튜디오에서에서 tooupload 학습 데이터 파일 하는 방법에 대해 알아봅니다. 이렇게 하면 데이터 집합 모듈을 hello 작업 영역에서 만들어집니다."
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
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="d30ed-105">하드 드라이브의 파일에서 Machine Learning Studio로 학습 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="d30ed-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="d30ed-106">어떻게 tooupload 데이터 파일에서 하드 드라이브 toouse을으로 Azure 기계 학습 스튜디오에서 학습 데이터에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="d30ed-107">Hello 데이터 파일을 가져와서 작업 영역에서 사용할 수 있는 데이터 집합 모듈이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="d30ed-108">로컬 파일에서 단계 tooimport 데이터</span><span class="sxs-lookup"><span data-stu-id="d30ed-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="d30ed-109">로컬 하드 드라이브에서 tooimport 데이터 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="d30ed-110">클릭 **+ 새로 만들기** hello hello 기계 학습 스튜디오 창 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="d30ed-111">**데이터 집합** 및 **로컬 파일에서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="d30ed-112">Hello에 **새 데이터 집합을 업로드** 대화 상자에서 원하는 tooupload 찾아보기 toohello 파일</span><span class="sxs-lookup"><span data-stu-id="d30ed-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="d30ed-113">이름을 입력 하 고 hello 데이터 형식을 식별에 설명을 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="d30ed-114">설명은 것이 좋습니다.-toorecord 허용 한다고 tooremember hello 미래에 hello 데이터를 사용 하는 경우 hello 데이터에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="d30ed-115">확인란 hello **이 기존 데이터 집합의 새 버전 hello** tooupdate 새 데이터로 기존 데이터 집합을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="d30ed-116">이 확인란을 선택 하 고 기존 데이터 집합의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![새 데이터 집합 업로드](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="d30ed-118">업로드 중에 파일이 업로드 중임을 나타내는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="d30ed-119">업로드 시간은 연결 toohello 서비스의 데이터 및 hello 속도 hello 크기에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="d30ed-120">Hello 파일에는 시간이 오래 걸리는 알고 있는 경우 기다리는 동안 기계 학습 스튜디오 내 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="d30ed-121">그러나 hello 브라우저를 닫는 hello 데이터 업로드 toofail을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="d30ed-122">데이터 집합 모듈을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-122">Dataset module is ready for use</span></span>
<span data-ttu-id="d30ed-123">데이터를 업로드 한 후 데이터 집합 모듈에 저장 하 고 작업 영역에서 사용할 수 있는 tooany 실험은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="d30ed-124">실험을 편집 하는 경우에 hello에서 만든 hello 데이터 집합을 찾을 수 있습니다 **내 데이터 집합** hello 아래의 목록 **저장 된 데이터 집합** hello 모듈 색상표의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d30ed-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="d30ed-125">하면 끌어서 놓을 수 hello 실험 캔버스 hello 데이터 집합 추가 분석 및 기계 학습에 대 한 toouse hello 데이터 집합을 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="d30ed-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
