---
title: "aaaExtend R 사용 하 여 실험 | Microsoft Docs"
description: "어떻게 tooextend hello R 스크립트 실행 모듈을 사용 하 여 hello R 언어를 통해 Azure 기계 학습 스튜디오의 기능을 hello 합니다."
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
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a>R을 사용하여 실험 확장
Hello를 사용 하 여 hello R 언어를 통해 Azure 기계 학습 스튜디오의 hello 기능을 확장할 수 [R 스크립트 실행] [ execute-r-script] 모듈입니다.

이 모듈에서는 여러 입력 데이터 집합을 허용하고 출력으로 단일 데이터 집합을 생성합니다. Hello에 R 스크립트를 입력할 수 있습니다 **R 스크립트** hello의 매개 변수 [R 스크립트 실행] [ execute-r-script] 모듈입니다.

유사한 toohello 다음 코드를 사용 하 여 hello 모듈의 각 입력된 포트에 액세스할 수 있습니다.

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>현재 설치된 모든 패키지 나열
설치 된 패키지 hello 목록을 변경할 수 있습니다. [Azure Machine Learning에서 지원하는 R 패키지](https://msdn.microsoft.com/library/azure/mt741980.aspx)에 현재 설치된 패키지의 목록이 있습니다.

또한 hello hello에 코드를 다음을 입력 하 여 설치 된 패키지의 hello 완전 하 고 현재 목록을 가져올 수 [R 스크립트 실행] [ execute-r-script] 모듈:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Hello 목록 hello의 패키지 toohello 출력 포트의 전송 [R 스크립트 실행] [ execute-r-script] 모듈입니다.
tooview hello 패키지 목록에서 변환 모듈을와 같은 연결 [tooCSV 변환] [ convert-to-csv] hello의 출력을 왼쪽 toohello [R 스크립트 실행] [ execute-r-script]hello 실험을 실행 하는 모듈을 클릭 한 다음 선택한 hello 변환 모듈의 hello 출력 **다운로드**합니다. 

!["TooCSV" 변환"모듈의 출력을 다운로드 합니다.](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>패키지 가져오기
Hello에 대 한 명령을 수행 하는 hello를 사용 하 여 이미 설치 되지 않은 패키지를 가져올 수 [R 스크립트 실행] [ execute-r-script] 모듈:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

여기서 hello `my_favorite_package.zip` 파일 패키지에 포함 되어 있습니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
