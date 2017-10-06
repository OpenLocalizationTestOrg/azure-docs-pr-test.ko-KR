---
title: "가상 컴퓨터 크기 집합으로 aaaTroubleshoot 자동 크기 조정 | Microsoft Docs"
description: "가상 컴퓨터 규모 집합을 사용하여 자동 크기 조정 문제 해결 발생 하는 일반적인 문제 이해 및 방법을 tooresolve 해당 합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>가상 컴퓨터 규모 집합을 사용하여 자동 크기 조정 문제 해결
**문제** – 만든 자동 크기 조정 하는 인프라에서 Azure 리소스 관리자 VM 크기 집합을 사용 하 여-예를 들어 다음과 같은 서식 파일을 배포 하 여: https://github.com/Azure/azure-quickstart-templates/tree/master/201- vmss-bottle-자동 크기 조정-정의 된 크기 조정 규칙이 있으며 제외 하 고 자동 크기 조정 불가능 hello Vm에 두면 부하의 양을에 관계 없이, 잘 작동 합니다.

## <a name="troubleshooting-steps"></a>문제 해결 단계
일부 작업 tooconsider 다음과 같습니다.

* 코어 개수 각 VM에는, 하 고 각 코어를 로드 하 시겠습니까? hello 예제 Azure 빠른 시작 템플릿 위의 단일 코어를 로드 하는 do_work.php 스크립트를 있습니다. Standard_A1 또는 D1 하면 필요한 toorun이이 부하 여러 번 같은 단일 코어 VM 크기 보다 큰 VM을 사용 하는 합니다. [Azure에서 Windows 가상 컴퓨터 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Hello VM 크기 집합 Vm 수는 작업을 하는 각?
  
    이벤트에 확장만 때 수행 됩니다 hello 평균 CPU 간에 **모든** hello Vm 크기 집합의 임계값을 초과 hello, 내부 hello 시간별 hello 자동 크기 조정 규칙에 정의 되어 있습니다.
* 누락된 크기 조정 이벤트가 있나요?
  
    Hello 감사 hello 크기 조정 이벤트에 대 한 Azure 포털에서에서 로그를 확인 합니다. 누락된 규모 확장 및 축소가 있을 수 있습니다. "크기 조정"으로 필터링할 수 있습니다.
  
    ![감사 로그][audit]
* 규모 축소 및 확장 임계값 차이가 충분한가요?
  
    평균 CPU 50% 미만인 경우에 평균 CPU 보다 큰 경우 50 %5 분 동안 아웃 규칙 tooscale 및 tooscale를 설정 했다고 가정해 보겠습니다. 이렇게 하면 "날개"를 퍼 덕 문제가 CPU 사용량이 닫기 toothis 임계값 hello 지속적으로 확대 및 축소 하는 크기 조정 작업을 하는 경우 hello 집합의 크기입니다. 이 인해 hello 자동 크기 조정 서비스에서 tooprevent "플 래핑", 크기 조정이 아니라으로 나타날 수 있는 합니다. 따라서 확장 및 확장에서 임계값 통계가 다르면 tooallow 여유 공간 크기 조정을 사이 확인 합니다.
* 사용자 고유의 JSON 템플릿을 작성했나요?
  
    쉽게 toomake 실수는, 따라서 toowork, 입증 된 기준이 하나 hello와 같은 템플릿을 사용 하 여 시작 및 작은 변화를 확인 합니다. 
* 수동으로 규모를 축소 또는 확장할 수 있나요?
  
    수동으로 재배포 hello는 다른 "용량" toochange hello 번호를 설정 하는 vm을 사용 하 여 리소스 VM 크기 집합을 보십시오. 이 여기에 하는 예제 서식 파일 toodo: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – tooedit hello 템플릿 toomake hello 갖도록 할 수 크기에 크기 집합에서 사용 하는 컴퓨터 동일 합니다. 성공적으로 hello Vm 수를 수동으로 변경할 수 있습니다, 것을 알 수 hello 문제는 격리 된 tooautoscale 합니다.
* 프로그램 Microsoft.Compute/virtualMachineScaleSet 확인 Microsoft.Insights의 및 리소스 hello [Azure 리소스 탐색기](https://resources.azure.com/)
  
    이 필수적인는 Azure 리소스 관리자 리소스의 상태를 hello 보여 주는 도구 문제 해결 합니다. 구독에 대해 클릭 하 고 해결 하는 리소스 그룹 hello에 확인 합니다. Hello 계산 리소스 공급자에서 만든 VM 크기 집합 hello를 확인 하 고 hello 표시 되는 인스턴스 보기를 확인 hello 배포의 상태입니다. 또한 Vm의 VM 크기 집합 hello hello 인스턴스 보기를 확인 합니다. 그런 다음 hello Microsoft.Insights 리소스 공급자를 이동 하 고 hello 자동 크기 조정 규칙 제대로 표시를 확인 합니다.
* Hello 진단 확장 작업 및 성능 데이터를 표시 하 고 있습니까?
  
    **업데이트:** Azure 자동 크기 조정 된 향상 된 toouse 호스트 기반 메트릭 파이프라인 설치 진단 확장 toobe 더 이상 필요 합니다. 즉, hello 다음 몇 단락 hello 새 파이프라인을 사용 하 여 자동 크기 조정 응용 프로그램을 만들 경우 더 이상 적용 합니다. 변환 된 toouse hello 호스트 파이프라인 된 있는 Azure 서식 파일의 예는: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale 합니다. 
  
    자동 크기 조정에 대 한 호스트 기반 메트릭을 사용 하는 이유를 수행 하는 hello에 대 한는 것이 좋습니다.
  
  * 없는 진단 확장으로 작동 되는 적은 부분이 toobe 설치 해야 합니다.
  * 템플릿이 간단합니다. Insights 자동 크기 조정 규칙 tooan 기존 크기 집합 템플릿에 추가 됩니다.
  * 새 VM에 대한 더 신뢰할 수 있는 보고 및 빠른 시작이 가능합니다.
    
    hello만 이유 tookeep 진단 확장을 사용 하는 것 메모리 진단 보고/크기 조정 해야 하는 경우입니다. 호스트 기반 메트릭은 메모리를 보고하지 않습니다.
    
    이 점을 염두에서에 자동 크기 조정에 대 한 진단 확장을 여전히 사용 되는 경우이 문서의 나머지 부분 hello를 따라만 합니다.
    
    Azure 리소스 관리자의 자동 크기 조정 작업 수 (하지만 더 이상) hello 진단 확장을 호출 하는 VM 확장을 사용 하 여 합니다. 성능 데이터 tooa 저장소 계정을 hello 서식 파일에서 정의 내보냅니다. 이 데이터는 hello Azure 모니터 서비스에서 다음 집계 됩니다.
    
    Toosend 예상한 hello Insights 서비스는 hello Vm에서에서 데이터를 읽을 수 없습니다, 하는 경우 (hello Azure 계정을 만들 때 지정한 하나 hello) 사용자의 전자 메일 확인 수 있는 전자 메일-예를 들어 hello Vm 다운 된 경우.
    
    이동 하 고 hello 데이터를 직접 확인할 수도 있습니다. Hello 클라우드 탐색기를 사용 하 여 Azure 저장소 계정 확인 합니다. 예를 들어 hello를 사용 하 여 [Visual Studio 클라우드 탐색기](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), 로그인 및 hello를 사용 하는 Azure 구독을 선택 하 고 hello 진단 저장소 계정 이름을 참조할 hello 배포에 진단 확장 정의 서식 파일...
    
    ![Cloud Explorer][explorer]
    
    여기에 hello 각 VM에서 저장 되는 데이터 테이블의 여러를 표시 됩니다. Linux 및 예를 들어 CPU 메트릭 hello 걸립니다, hello 가장 최신 행 확인 합니다. hello Visual Studio 클라우드 탐색기와 같은 쿼리를 실행할 수 있도록 하는 쿼리 언어 지원 "타임 스탬프 gt datetime'2016-02-02T21:20:00Z'" toomake hello 가장 최근 이벤트 (utc에서 시간은 라고 가정)를 얻었는지 확인 합니다. 가 있는 toohello 해당에 표시 하는 hello 데이터를 설정 하는 규칙 확장? Hello 아래 예제에서는 hello CPU 20 컴퓨터에 대 한 최근 5 분 동안 hello에 따라 too100% 증가 시작...
    
    ![저장소 테이블][tables]
    
    Hello 데이터 없으면 hello 문제 hello 진단 확장 hello Vm에서에서 실행 되는 의미 합니다. Hello 데이터 중지 되지 않은 경우, 크기 조정 규칙을 사용 하거나 hello Insights 서비스와 어느 문제가 의미 합니다. [Azure 상태](https://azure.microsoft.com/status/)를 확인합니다.
    
    자동 크기 조정 문제가 발생 하는 경우 이러한 단계를 방문한 후 hello 포럼을 시도할 수 있습니다 [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), 또는 [스택 오버플로](http://stackoverflow.com/questions/tagged/azure), 또는 지원 통화를 로그 합니다. 준비 tooshare hello 템플릿과 hello 성능 데이터의 뷰 수입니다.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
