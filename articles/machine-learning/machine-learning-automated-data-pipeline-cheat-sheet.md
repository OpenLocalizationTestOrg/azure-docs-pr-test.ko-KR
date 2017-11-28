---
title: "기계 학습 aaaAzure 자동 데이터 파이프라인 치트 시트 | Microsoft Docs"
description: "데이터가 온-프레미스에서 Azure 또는 타사 클라우드 서비스에서 스트리밍 인지 자동화 된 데이터를 tooset tooyour Azure 기계 학습 웹 서비스를 파이프라인 하는 방법을 보여 주는 인쇄 가능한 치트 시트를 반환 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 22674d6b-4491-4805-a3ac-d423611177bb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: mithal;garye
ms.openlocfilehash: 045f5c0a40fe301fcdc8df61a156f93246286174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cheat-sheet-for-an-automated-data-pipeline-for-azure-machine-learning-predictions"></a><span data-ttu-id="e5eb9-103">Azure 기계 학습 예측에 대한 자동화된 데이터 파이프라인용 참고 자료</span><span class="sxs-lookup"><span data-stu-id="e5eb9-103">Cheat sheet for an automated data pipeline for Azure Machine Learning predictions</span></span>
<span data-ttu-id="e5eb9-104">hello **데이터 파이프라인 치트 시트를 자동으로 Microsoft Azure 기계 학습** 사용 하는 기술 수 tooget 사용자 데이터 tooyour 기계 학습 웹 서비스를 예측에 의해 매길 수를 탐색 하는 데 도움이 됩니다. 분석 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-104">hello **Microsoft Azure Machine Learning automated data pipeline cheat sheet** helps you navigate through the technology you can use tooget your data tooyour Machine Learning web service where it can be scored by your predictive analytics model.</span></span>

<span data-ttu-id="e5eb9-105">데이터 인지 온-프레미스에 따라 hello 클라우드 또는 스트리밍 실시간으로 다양 한 메커니즘 사용 가능한 toomove hello 데이터 tooyour 웹 서비스 끝점 점수를 매기기 위해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-105">Depending on whether your data is on-premises, in hello cloud, or streaming real-time, there are different mechanisms available toomove hello data tooyour web service endpoint for scoring.</span></span>
<span data-ttu-id="e5eb9-106">Hello 결정 하며 toomake를 통해 제공 수 있는 링크 tooarticles 치트 시트 워크가 솔루션을 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-106">This cheat sheet walks you through hello decisions you need toomake, and it offers links tooarticles that can help you develop your solution.</span></span>

## <a name="download-hello-machine-learning-automated-data-pipeline-cheat-sheet"></a><span data-ttu-id="e5eb9-107">Hello 기계 학습 자동화 된 데이터 파이프라인 치트 시트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-107">Download hello Machine Learning automated data pipeline cheat sheet</span></span>
<span data-ttu-id="e5eb9-108">Hello 치트 시트를 다운로드 한 후 tabloid 크기 (11 x 17 인치)에 인쇄할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-108">Once you download hello cheat sheet, you can print it in tabloid size (11 x 17 in.).</span></span>

<span data-ttu-id="e5eb9-109">여기에 hello 치트 시트를 다운로드:  **[데이터 파이프라인 치트 시트를 자동으로 Microsoft Azure 기계 학습](http://download.microsoft.com/download/C/C/7/CC726F8B-2E6F-4C20-9B6F-AFBEE8253023/microsoft-machine-learning-operationalization-cheat-sheet_v1.pdf)**</span><span class="sxs-lookup"><span data-stu-id="e5eb9-109">Download hello cheat sheet here: **[Microsoft Azure Machine Learning automated data pipeline cheat sheet](http://download.microsoft.com/download/C/C/7/CC726F8B-2E6F-4C20-9B6F-AFBEE8253023/microsoft-machine-learning-operationalization-cheat-sheet_v1.pdf)**</span></span>

![Microsoft Azure 기계 학습 스튜디오 기능 개요][op-cheat-sheet]

[op-cheat-sheet]: ./media/machine-learning-automated-data-pipeline-cheat-sheet/machine-learning-automated-data-pipeline-cheat-sheet_v1.1.png


## <a name="more-help-with-machine-learning-studio"></a><span data-ttu-id="e5eb9-111">기계 학습 스튜디오에 대한 추가 도움말</span><span class="sxs-lookup"><span data-stu-id="e5eb9-111">More help with Machine Learning Studio</span></span>
* <span data-ttu-id="e5eb9-112">Microsoft Azure 기계 학습의 개요를 참조 하십시오. [Microsoft Azure에서 학습 소개 toomachine](machine-learning-what-is-machine-learning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-112">For an overview of Microsoft Azure Machine Learning, see [Introduction toomachine learning on Microsoft Azure](machine-learning-what-is-machine-learning.md).</span></span>
* <span data-ttu-id="e5eb9-113">방법에 대 한 toodeploy 점수 매기기 웹 서비스 참조 [Azure 기계 학습 웹 서비스를 배포](machine-learning-publish-a-machine-learning-web-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-113">For an explanation of how toodeploy a scoring web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="e5eb9-114">방법에 대 한 tooconsume 점수 매기기 웹 서비스 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5eb9-114">For a discussion of how tooconsume a scoring web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

