---
title: "다른 실험에서 얻은 데이터를 Machine Learning 스튜디오로 가져오기 | Microsoft Docs"
description: "Azure 기계 학습 스튜디오에서 학습 데이터를 저장하고 다른 실험에 사용하는 방법."
keywords: "데이터 가져오기, 데이터, 데이터 원본, 학습 데이터"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: cac35aa26fcdb7f2fb0db3b895d3c99d77f3b4ba
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a>다른 실험에서 얻은 사용자의 데이터를 Azure 기계 학습 스튜디오로 가져오기
[!INCLUDE [import-data-into-aml-studio-selector](../../../includes/machine-learning-import-data-into-aml-studio.md)]

한 실험의 중간 결과를 다른 실험의 일부로 사용하려는 경우가 있습니다. 이렇게 하려면 모듈을 데이터 집합으로 저장합니다.

1. 데이터 집합으로 저장할 모듈의 출력을 클릭합니다.
2. **데이터 집합으로 저장**을 클릭합니다.
3. 메시지가 표시되면 데이터 집합을 쉽게 식별할 수 있는 이름과 설명을 입력합니다.
4. **확인** 확인 표시를 클릭합니다.

저장이 완료되면 작업 영역의 모든 실험에서 데이터 집합을 사용할 수 있습니다. 모듈 팔레트의 **저장된 데이터 집합** 목록에서 찾을 수 있습니다.

