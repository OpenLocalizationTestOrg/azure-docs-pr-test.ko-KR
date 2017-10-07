---
title: "aaaComparing 사용자 지정 이미지 및 수식에서 DevTest Labs | Microsoft Docs"
description: "VM 기반 환경에 가장 적합 한 어떤 것을 결정할 수 있도록 사용자 지정 이미지와 수식 hello 차이점에 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>DevTest Lab에서 사용자 지정 이미지와 수식 비교
[사용자 지정 이미지](devtest-lab-create-template.md) 및 [수식](devtest-lab-manage-formulas.md)은 모두 [새로 생성된 VM](devtest-lab-add-vm-with-artifacts.md)의 기반으로 사용될 수 있습니다. 그러나 hello 중요 한 차이점 수식와 사용자 지정 이미지 간의 사용자 지정 이미지 수식은 VHD를 기반으로 이미지는 VHD를 기반으로 이미지 단순히 된다는 점입니다 *외에* 설정-VM 크기, 가상 네트워크와 같은 미리 구성 서브넷 및 아티팩트를 제공 합니다. 미리 구성 된 이러한 설정은 hello VM 생성 시 재정의할 수 있는 기본 값으로 설정 되어 있습니다. 이 문서 (전문가) hello 장점 중 일부에 대해 설명 하 고 (cons) 및 수식을 사용 하 여 사용자 지정 이미지 toousing 단점입니다.

## <a name="custom-image-pros-and-cons"></a>사용자 지정 이미지의 장점 및 단점
사용자 지정 이미지 정적, 변경할 수 없는 방식으로 toocreate Vm 원하는 환경에서 제공합니다. 

**장점**

* VM 사용자 지정 이미지에서 프로 비전 hello 이미지에서 VM을 된 hello 후 변경 사항이 없는 빠릅니다. 즉, 없음 설정을 tooapply hello 사용자 지정 이미지는이 설정이 없는 이미지로 합니다. 
* 하나의 사용자 지정 이미지를 통해 만들어진 VM은 동일합니다.

**단점**

* Hello 사용자 지정 이미지의 일부 측면 tooupdate 해야 할 경우 hello 이미지를 다시 만들어야 합니다.  

## <a name="formula-pros-and-cons"></a>수식의 장점 및 단점
수식은 동적 방법으로 toocreate Vm에서 필요한 hello 구성/설정을 제공합니다.

**장점**

* 아티팩트를 통해 신속 하 게 hello hello 환경에서 변경 내용은 캡처할 수 있습니다. 예를 들어, 릴리스 파이프라인에서 최신 파일 hello와 함께 설치 된 VM 이나 hello 최신 코드 리포지토리에서 참여를 지정할 수 있습니다 단순히 hello와 함께 hello 수식에 최신 코드를 인 리스트 먼 트 또는 hello 최신 파일을 배포 하는 아티팩트는 대상 기본 이미지입니다. 이 수식을 사용 하는 toocreate Vm 때마다 hello 최신 비트/코드 배포/참여 toohello VM는 있습니다. 
* 수식은 사용자 지정 이미지가 제공할 수 없는 기본 설정(예: VM 크기 및 가상 네트워크 설정)을 정의할 수 있습니다. 
* 수식에 저장 된 hello 설정은 기본 값으로 표시 되지만 VM hello를 만들 때에 수정할 수 있습니다. 

**단점**

* 수식을 통해 VM을 만들면 사용자 지정 이미지를 통해 VM을 만드는 것보다 시간이 더 소요됩니다.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>관련 블로그 게시물
* [사용자 지정 이미지 또는 수식?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>다음 단계
- [DevTest Labs FAQ](devtest-lab-faq.md)