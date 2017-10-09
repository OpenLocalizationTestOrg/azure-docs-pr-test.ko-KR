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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>하드 드라이브의 파일에서 Machine Learning Studio로 학습 데이터 가져오기
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

어떻게 tooupload 데이터 파일에서 하드 드라이브 toouse을으로 Azure 기계 학습 스튜디오에서 학습 데이터에 알아봅니다. Hello 데이터 파일을 가져와서 작업 영역에서 사용할 수 있는 데이터 집합 모듈이 있는 합니다.

## <a name="steps-tooimport-data-from-a-local-file"></a>로컬 파일에서 단계 tooimport 데이터
로컬 하드 드라이브에서 tooimport 데이터 다음 hello지 않습니다.

1. 클릭 **+ 새로 만들기** hello hello 기계 학습 스튜디오 창 맨 아래에 있습니다.
2. **데이터 집합** 및 **로컬 파일에서**를 선택합니다.
3. Hello에 **새 데이터 집합을 업로드** 대화 상자에서 원하는 tooupload 찾아보기 toohello 파일
4. 이름을 입력 하 고 hello 데이터 형식을 식별에 설명을 입력할 수도 있습니다. 설명은 것이 좋습니다.-toorecord 허용 한다고 tooremember hello 미래에 hello 데이터를 사용 하는 경우 hello 데이터에 대 한 특성입니다.
5. 확인란 hello **이 기존 데이터 집합의 새 버전 hello** tooupdate 새 데이터로 기존 데이터 집합을 허용 합니다. 이 확인란을 선택 하 고 기존 데이터 집합의 hello 이름을 입력 합니다.

![새 데이터 집합 업로드](media/machine-learning-import-data-from-local-file/upload-dataset.png)

업로드 중에 파일이 업로드 중임을 나타내는 메시지가 표시됩니다. 업로드 시간은 연결 toohello 서비스의 데이터 및 hello 속도 hello 크기에 따라 다릅니다. Hello 파일에는 시간이 오래 걸리는 알고 있는 경우 기다리는 동안 기계 학습 스튜디오 내 다른 작업을 수행할 수 있습니다. 그러나 hello 브라우저를 닫는 hello 데이터 업로드 toofail을 발생 합니다.

## <a name="dataset-module-is-ready-for-use"></a>데이터 집합 모듈을 사용할 준비가 되었습니다.
데이터를 업로드 한 후 데이터 집합 모듈에 저장 하 고 작업 영역에서 사용할 수 있는 tooany 실험은 합니다.

실험을 편집 하는 경우에 hello에서 만든 hello 데이터 집합을 찾을 수 있습니다 **내 데이터 집합** hello 아래의 목록 **저장 된 데이터 집합** hello 모듈 색상표의 목록입니다. 하면 끌어서 놓을 수 hello 실험 캔버스 hello 데이터 집합 추가 분석 및 기계 학습에 대 한 toouse hello 데이터 집합을 하려는 경우.
