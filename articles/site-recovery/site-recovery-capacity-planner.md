---
title: "Azure에서 복제 용량 aaaEstimate | Microsoft Docs"
description: "Azure Site Recovery와 복제할 경우이 문서 tooestimate 용량을 사용 하 여"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Azure Site Recovery에서 가상 컴퓨터 및 물리적 서버를 보호하기 위한 용량 계획

hello Azure 사이트 복구 Capacity Planner 도구를 사용 하면 용량 요구 사항을 초과 toofigure Hyper-v Vm, VMware Vm 및 Azure 사이트 복구와 Windows/Linux 물리적 서버의 복제 하는 경우.

사이트 복구 Capacity Planner tooanalyze hello를 사용 하 여 원본 환경 및 워크 로드, 대역폭 요구 사항 및 hello 원본 위치에 필요한 서버 리소스 및 hello 리소스 (가상 컴퓨터 및 저장소 등)는 hello 대상에 필요한 예상 위치입니다.

몇 가지 모드에서에서 hello 도구를 실행할 수 있습니다.

* **계획 빠른**: Vm, 디스크, 저장소 및 변경률이 평균 수에 따라 tooget 네트워크 및 서버 프로젝션이이 모드에서는 hello 도구를 실행 합니다.
* **계획 세부**:이 모드에서는 hello 도구를 실행 하 고 VM 수준에서 각 작업의 세부 정보를 제공 합니다. VM 호환성을 분석하고 네트워크 및 서버를 예상합니다.

## <a name="before-you-start"></a>시작하기 전에


1. VM, VM당 디스크, 디스크당 저장소를 포함하여 사용자 환경에 대한 정보를 수집합니다.
2. 복제된 데이터에 대한 일일 변경(이탈)률을 식별합니다. toodo이:

   * Hyper-v Vm을 복제 하는 경우 다음 hello 다운로드 [Hyper-v 용량 계획 도구](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello 변경 비율입니다. [자세히 알아보세요](site-recovery-capacity-planning-for-hyper-v-replication.md) . 평균 주 toocapture를 통해이 도구를 실행 하는 것이 좋습니다.
   * VMware 가상 컴퓨터를 복제 하는 경우 사용 하 여 hello [Azure 사이트 복구 배포 계획](./site-recovery-deployment-planner.md) hello 아웃 toofigure 변동 속도입니다.
   * 물리적 서버를 복제 하는, tooestimate 수동으로 필요 합니다.

## <a name="run-hello-quick-planner"></a>Hello 빠른 계획을 실행 합니다.
1. 다운로드 하 고 hello 엽니다 [Azure 사이트 복구 Capacity Planner](http://aka.ms/asr-capacity-planner-excel) 도구입니다. Toorun 매크로, 선택 tooenable 편집 및 필요한 사용 가능 대화 상자가 나타나면 콘텐츠.
2. **계획 유형을 선택** 선택 **빠른 플래너** hello 목록 상자에서 합니다.

   ![시작](./media/site-recovery-capacity-planner/getting-started.png)
3. Hello에 **Capacity Planner** 워크시트 hello 필요한 정보를 입력 합니다. Hello 화면 아래에 빨간색 원이 표시 된 모든 hello 필드를 입력 해야 합니다.

   * **시나리오 선택**, 선택 **Hyper-v tooAzure** 또는 **/물리적 tooAzure**합니다.
   * **평균 일별 데이터 변경 률 (%)**, hello를 사용 하 여 수집 된 hello 정보에 [Hyper-v 용량 계획 도구](site-recovery-capacity-planning-for-hyper-v-replication.md) 또는 hello [Azure 사이트 복구 배포 계획](./site-recovery-deployment-planner.md).  
   * **압축** toocompression 제공 VMware Vm 또는 실제 서버 tooAzure를 복제 하는 경우에 적용 됩니다. 30% 이상 예상 하지만 필요에 따라 hello 설정을 수정할 수 있습니다. Hyper-v Vm tooAzure 압축을 복제에 대 한 Riverbed 등 제 3 자 어플라이언스를 사용할 수 있습니다.
   * **보존 입력**은 복제본을 보존해야 하는 기간을 지정합니다. VMware 또는 물리적 서버를 복제 하는 경우 일 이내에 hello 값을 입력 합니다. Hyper-v를 복제 하는 경우 hello 시간 단위로 지정 합니다.
   * **가상 컴퓨터의 hello 일괄 처리에 대 한 초기 복제의 시간을 완료 해야** 및 **초기 복제 일괄 처리당 가상 컴퓨터 수가**, 사용 되는 설정 입력 toocompute 초기 복제 요구 사항입니다.  Site Recovery를 배포할 때 hello 전체 초기 데이터 집합을 업로드 해야 합니다.

   ![입력](./media/site-recovery-capacity-planner/inputs.png)
4. Hello 원본 환경에 대 한 hello 값 넣으면 후 표시 된 출력에 포함 됩니다.

   * **델타 복제에 필요한 대역폭** (MB/sec). Hello 평균 일별 데이터 변경 률 델타 복제에 대 한 네트워크 대역폭을 계산 합니다.
   * **초기 복제에 필요한 대역폭** (MB/sec). 초기 복제에 대 한 네트워크 대역폭에 넣으면 hello 초기 복제 값 계산 됩니다.
   * **저장소 (Gb))에 필요한** 필요한 Azure 저장소 총 hello 됩니다.
   * **표준 저장소 계정에서 IOP는 총** hello 총 표준 저장소 계정에 8k IOPS 단위 크기에 따라 계산 됩니다.  빠른 플래너 hello에 대 한 모든 hello 소스 Vm 디스크 및 일일 데이터 변경 률에 hello 수 기준 계산 됩니다. 에 대 한 자세한 플래너 hello, hello 수는 Vm 매핑된 toostandard Azure Vm의 계산된에 따라 총 수 및 데이터 변경 률 해당 Vm에 합니다.
   * **표준 저장소 계정의 수** hello Vm 표준 저장소 계정이 필요 tooprotect hello 총 수를 제공 합니다. 표준 저장소 계정이 표준 저장소에 있는 모든 hello Vm 간에 too20000 IOPS를 보유할 수 및 디스크 당 500 IOPS의 최대 지원 됩니다.
   * **필요한 blob 디스크 수** 제공 hello Azure 저장소에 만들 수 있는 디스크 수.
   * **필요한 프리미엄 저장소 계정 수** hello Vm 프리미엄 저장소 계정 필요한 tooprotect hello 총 수를 제공 합니다. 높은 IOPS(20000 이상)를 포함한 원본 VM에는 Premium Storage 계정이 필요합니다. 프리미엄 저장소 계정을 too80000 IOPS를 보유할 수 있습니다.
   * **프리미엄 저장소에서 IOP는 총** hello 총 프리미엄 저장소 계정에 대 한 256k IOPS 단위 크기에 따라 계산 됩니다.  빠른 플래너 hello에 대 한 모든 hello 소스 Vm 디스크 및 일일 데이터 변경 률에 hello 수 기준 계산 됩니다. 에 대 한 자세한 플래너 hello, hello 수는 Vm 매핑된 toopremium Azure VM (DS 및 GS 시리즈)의 총 수 계산된에 따라 hello 및 hello 데이터 변경 률 해당 Vm에 합니다.
   * **필요한 구성 서버 수** 구성 서버의 수는 hello 배포에 필요한 표시 됩니다.
   * **필요한 추가 프로세스 서버 수** 추가 프로세스 서버가 기본적으로 hello 구성 서버에서 실행 되는 추가 toohello 프로세스 서버에 필요한 지를 보여 줍니다.
   * **100 %hello 소스에서 추가 저장소** hello 원본 위치에 추가 저장소가 필요한 지를 보여 줍니다.

   ![출력](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>실행 hello 자세한 계획

1. 다운로드 하 고 hello 엽니다 [Azure 사이트 복구 Capacity Planner](http://aka.ms/asr-capacity-planner-excel) 도구입니다. Toorun 매크로, 선택 tooenable 편집 및 필요한 사용 가능 대화 상자가 나타나면 콘텐츠.
2. **계획 유형을 선택**선택, **자세한 플래너** hello 목록 상자에서 합니다.

   ![시작하기](./media/site-recovery-capacity-planner/getting-started-2.png)
3. Hello에 **작업 한정** 워크시트 hello 필요한 정보를 입력 합니다. 필드를 표시 하는 모든 hello를 입력 해야 합니다.

   * **프로세서 코어**, 원본 서버에서 hello 코어의 총 수를 지정 합니다.
   * **mb에서 메모리 할당**, 원본 서버 hello RAM 크기를 지정 합니다.
   * hello **Nic 수**, 원본 서버에서 네트워크 어댑터의 hello 수를 지정 합니다.
   * **총 저장소 공간 (GB)**, hello hello VM 저장소의 총 크기를 지정 합니다. 예를 들어 hello 원본 서버에 3 개의 각 500gb 디스크, 하는 경우 총 저장소 크기는 1500GB입니다.
   * **연결 된 디스크 수**, hello 원본 서버의 디스크의 총 수를 지정 합니다.
   * **디스크 용량 사용률**, hello 평균 사용률을 지정 합니다.
   * **매일 변경 률 (%)**, hello 일일 데이터 변경 률 원본 서버를 지정 합니다.
   * **매핑 Azure 크기**, 원하는 toomap hello Azure VM 크기를 입력 합니다. Toodo을 수동으로 수행 해야 않으려면 클릭 **계산 IaaS Vm**합니다. 입력 수동 설정 하 고 계산 IaaS Vm을 클릭 한 다음 hello 계산 프로세스에 자동으로 Azure VM 크기에 가장 일치 hello 식별 하기 때문에 수동 hello 설정을 덮어쓸 수 있습니다.

   ![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification.png)
4. **IaaS VM 계산** 을 클릭하면 수행되는 작업은 다음과 같습니다.

   * Hello 필수 입력의 유효성을 검사 합니다.
   * IOPS를 계산 하 고 hello 제안 최상의 Azure VM aize 복제 tooAzure에 해당 되는 각 Vm에 대 한 일치 합니다. Azure VM에 적합한 크기를 감지할 수 없는 경우 오류가 발생합니다. 예를 들어 디스크 수가 hello 65을 연결한 경우 hello 가장 높은 Azure VM 크기가 64 때문에 오류가 생성 됩니다.
   * Azure VM에 대해 사용할 수 있는 저장소 계정을 제안합니다.
   * Hello hello 작업 부하에 필요한 프리미엄 저장소 계정 및 표준 저장소 계정의 총 수를 계산 합니다. Tooview hello Azure 저장소 유형 및 원본 서버에 대해 사용할 수 있는 hello 저장소 계정 아래로 스크롤하십시오.
   * 완료 하 고 hello 나머지 VM 및 연결 된 디스크 수 hello에 대 한 할당 필요한 저장소 유형 (표준 또는 프리미엄)에 따라 hello 테이블을 정렬 합니다. Azure 용 hello 요구 사항을 충족 하는 모든 Vm에 대 한 열 hello **정규화는 VM?** 표시 **예**합니다. VM tooAzure 백업할 수 없으며, 오류가 표시 됩니다.

열 AA tooAE 출력 있으며 각 VM에 대 한 정보를 제공 합니다.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>예제
예를 들어 hello 값 hello 표에 나와 있는 vm에 6 개의 hello 도구 계산한 hello 가장 하는 Azure VM 일치과 hello Azure 저장소 요구 사항을 지정 합니다.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* Hello 예제 출력에서 note hello 다음:

  * hello 첫 번째 열은 hello Vm, 디스크 및 변동에 대 한 유효성 검사 열입니다.
  * VM 5대에 표준 저장소 계정 두 개와 프리미엄 저장소 계정 하나가 필요합니다.
  * VM3은 하나 이상의 디스크가 1TB를 초과하므로 보호하기에 적합하지 않습니다.
  * VM1 및 v m 2는 hello 첫 번째 표준 저장소 계정을 사용할 수 있습니다.
  * VM4는 hello 두 번째 표준 저장소 계정을 사용할 수 있습니다.
  * VM5 및 VM6에는 Premium Storage 계정이 필요하고 둘 다 단일 계정을 사용할 수 있습니다.

    > [!NOTE]
    > 표준 및 프리미엄 저장소의 IOPS 디스크 수준이 아닌 hello VM 수준에서 계산 됩니다. 표준 가상 컴퓨터 디스크 드라이브당 IOPS가 too500 처리할 수 있습니다. 디스크의 IOPS가 500개보다 많은 경우 Premium Storage가 필요합니다. 그러나 디스크에 대 한 IOPS는 500 개 이상의 이지만 IOPS hello 내 hello 총 VM 디스크에 대 한 지원 표준 Azure VM 제한 (VM 크기, 디스크 수, 어댑터, CPU, 메모리) hello 플래너 선택는 standard VM 및 하지 hello DS 또는 GS 시리즈 합니다. 적절 한 DS 또는 GS 시리즈 VM 사용 하 여 toomanually 업데이트 hello 매핑 Azure 크기 셀이 필요합니다.


Hello에 대 한 세부 정보를 모두을 저장 한 후 클릭 **전송 데이터 toohello planner 도구** tooopen hello **Capacity Planner** 작업은 강조 표시 되며 tooshow 여부 보호에 적합 하 고 있는지 여부를 합니다.

### <a name="submit-data-in-hello-capacity-planner"></a>Capacity Planner hello에 대 한 데이터 전송
1. Hello를 열 때 **Capacity Planner** 지정한 hello 설정의 기반으로 하는 워크시트를 채웁니다. '워크 로드' hello에 표시 되는 단어 hello **인프라 입력 소스** 셀 입력 hello tooshow는 hello **작업 한정** 워크시트입니다.
2. Toomodify hello toomake 변경 하려는 경우 필요한 **작업 한정** 워크시트 및 클릭 **전송 데이터 toohello planner 도구** 다시 합니다.  

   ![Capacity Planner](./media/site-recovery-capacity-planner/capacity-planner.png)
