---
title: "VMware-Azure 사이트 복구 배포 플래너 aaaAzure | Microsoft Docs"
description: "Hello Azure Site Recovery 배포 계획 사용 설명서입니다."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Azure Site Recovery Deployment Planner
이 문서는 Azure에 VMware 프로덕션 배포에 대 한 hello Azure 사이트 복구 배포 Planner 사용자 가이드입니다.

## <a name="overview"></a>개요

사이트 복구를 사용 하 여 VMware 가상 컴퓨터 (Vm) 보호를 시작 하기 전에 충분 한 대역폭을 할당 합니다. 원하는 복구 지점 목표 (RPO) 일별 데이터 변경 률 toomeet에 기반 합니다. 구성 서버 및 프로세스 서버 온-프레미스의 있는지 toodeploy hello 올바른 숫자 여야 합니다.

대상 Azure 저장소 계정 수와 toocreate hello 적합 한 형식이 필요 합니다. 시간이 지남에 따라 사용량이 증가하므로 원본 프로덕션 서버상의 증가를 고려하여 표준 또는 프리미엄 저장소 계정을 만듭니다. 작업 특성 (예를 들어: 읽기/쓰기 I/O 작업 / 초 [IOPS] 또는 데이터 변동을)에 따라 VM 당 hello 저장소 유형을 선택 하 고 사이트 복구 제한 합니다.

hello 사이트 복구 배포 계획 공개 미리 보기는 현재 hello VMware-Azure 시나리오에 대해서만 사용할 수 있는 명령줄 도구입니다. 원격으로 복제에 대 한이 도구 (영향을 주지 프로덕션 든) toounderstand hello 대역폭 및 Azure 저장소 요구 사항을 사용 하 여 VMware Vm을 프로 파일링 하 고 테스트 장애 조치 수 있습니다. 모든 사이트 복구 구성 요소가 온-프레미스를 설치 하지 않고 hello 도구를 실행할 수 있습니다. 그러나 tooget 정확한 처리량 결과 달성, hello 플래너 hello의 최소 요구 사항 hello Site Recovery 구성 서버는 결국 해야 toodeploy로 hello 첫 번째 단계 중 하나를 충족 하는 Windows 서버에서 실행 하는 것이 좋습니다. 프로덕션 환경에 배포 합니다.

hello 도구 hello를 다음 세부 정보를 제공 합니다.

**호환성 평가**

* 디스크 수, 디스크 크기, IOPS, 변동 및 부팅 형식(EFI/BIOS)에 따른 VM 적합성 평가
* 델타 복제 하는 데 필요한 예상 hello 네트워크 대역폭

**네트워크 대역폭 요구 사항 및 RPO 평가**

* 델타 복제 하는 데 필요한 예상 hello 네트워크 대역폭
* Site Recovery 온-프레미스 tooAzure에서 얻을 수 있는 hello 처리량
* hello 수가 Vm toobatch, hello에 따라 예상 대역폭 toocomplete 일정 시간 동안에서 초기 복제

**Azure 인프라 요구 사항**

* 각 VM에 대 한 hello 저장소 유형 (표준 또는 프리미엄 저장소 계정) 요구 사항
* 복제용으로 설정 하는 표준 및 프리미엄 저장소 계정 toobe hello 총 수
* Azure Storage 지침에 따른 저장소 계정 명명 제안
* 모든 Vm에 대 한 hello 저장소 계정이 배치
* hello Azure 코어 toobe 수가 hello 구독에 대 한 장애 조치 또는 테스트 장애 조치 하기 전에 설정합니다.
* hello Azure VM 권장 크기 각각에 대해 온-프레미스 VM

**온-프레미스 인프라 요구 사항**
* hello 필요한 수의 구성 서버 및 프로세스 서버 toobe 온-프레미스 배포

>[!IMPORTANT]
>
>작업 특성의 30% 증가 비율을 가정 하 고 모든 hello 메트릭 프로 파일링의 95 번째 백분위 수 값을 사용 하 여 계산을 수행 하는 이전 도구를 hello 사용 시간이 지남에 따라 가능성이 tooincrease 이기 때문에 모두 (읽기/쓰기 IOPS, 변동 하므로 세이프). 이러한 두 요소(증가율과 백분위수)는 모두 구성할 수 있습니다. 증가 비율에 대 한 toolearn hello "증가 비율 고려 사항" 섹션을 참조 합니다. 백분위 수 값에 대해 자세히 toolearn hello "hello 계산에 사용 된 백분위 수 값" 섹션을 참조 합니다.
>

## <a name="requirements"></a>요구 사항
hello 도구에는 두 가지 주요 단계: 프로 파일링 및 보고서 생성. 세 번째 옵션 toocalculate 처리량만 이기도합니다. 다음 표에 hello에 어떤 hello에서 프로 파일링 및 처리량 측정에서 시작 된 hello 서버에 대 한 hello 요구 사항 표시 됩니다.

| 서버 요구 사항 | 설명|
|---|---|
|프로파일링 및 처리량 측정| <ul><li>운영 체제: Microsoft Windows Server 2012 R2<br>(이상 hello 일치 하는 것이 가장 좋습니다 [크기 hello 구성 서버에 대 한 권장 사항](https://aka.ms/asr-v2a-on-prem-components))</li><li>컴퓨터 구성: 8개 vCPus, 16GB RAM, 300GB HDD</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Visual Studio 2012용 Microsoft Visual C++ 재배포 가능 패키지](https://aka.ms/vcplusplus-redistributable)</li><li>이 서버에서 인터넷 액세스 tooAzure</li><li>Azure Storage 계정</li><li>서버 hello에 대 한 관리자 액세스</li><li>최소 100GB의 사용 가능한 디스크 공간(각각 디스크 3개의 평균을 포함한 VM 1000개를 가정, 30일 동안 프로파일링)</li><li>VMware vCenter 통계 수준 설정은 too2 또는 높은 수준 설정 해야</li><li>443 포트를 허용 합니다:이 포트 tooconnect toovCenter 서버/ESXi 호스트를 사용 하는 ASR 배포 계획</ul></ul>|
| 보고서 생성 | Microsoft Excel 2013 이상을 포함한 모든 Windows PC 또는 Windows Server |
| 사용자 권한 | 프로 파일링 하는 동안 tooaccess hello VMware vCenter 서버/VMware vSphere ESXi 호스트를 사용 하는 hello 사용자 계정에 대 한 읽기 전용 권한 |

> [!NOTE]
>
>hello 도구에는 VMDK 및 RDM 디스크와 Vm만 프로 파일링 수 있습니다. iSCSI 또는 NFS 디스크를 갖춘 VM은 프로파일링할 수 없습니다. 사이트 복구에 iSCSI 및 NFS 디스크 VMware 서버에 대 한 지원지 않습니다 했지만 이러한 디스크 형식에 대 한 가시성 hello 배포 계획 하지 않고 서 hello 게스트 vCenter 성능 카운터를 사용 하 여 프로필을 hello 도구가 없습니다.
>

## <a name="download-and-extract-hello-public-preview"></a>다운로드 하 고 압축 hello 공개 미리 보기
1. 최신 버전의 hello hello 다운로드 [사이트 복구 배포 계획 공개 미리 보기](https://aka.ms/asr-deployment-planner)합니다.  
hello 도구.zip 폴더에 패키지 됩니다. 현재 버전의 hello 도구 hello hello VMware-Azure 시나리오만 지원합니다.

2. Toorun hello 도구 원하는 hello.zip 폴더 toohello Windows 서버에 복사 합니다.  
Hello 서버에 네트워크 액세스 tooconnect toohello vCenter 서버/vSphere ESXi 호스트 hello Vm toobe 프로 파일링을 보유 하는 경우 Windows Server 2012 r 2에서 hello 도구를 실행할 수 있습니다. 하지만 하드웨어 구성이 hello를 충족 하는 서버에서 hello 도구를 실행 하는 권장 [구성 서버의 크기 조정 지침](https://aka.ms/asr-v2a-on-prem-components)합니다. Site Recovery 구성 요소 온-프레미스 이미 배포한 경우 hello 구성 서버에서 hello 도구를 실행 합니다.

 Hello를 해야 하는 것이 좋습니다 hello 구성 서버 (에 기본 제공 프로세스 서버) hello 도구를 실행 하는 hello 서버에 동일한 하드웨어 구성을 합니다. 이러한 구성은 hello 도구 보고서 일치 hello 실제 처리량 Site Recovery는 복제 하는 동안 얻을 수 있는 달성 하는 hello 처리량을 확인 합니다. hello 처리량 계산 hello 서버와 hello 서버의 하드웨어 구성 (CPU, 저장소, 등)에서 사용 가능한 네트워크 대역폭에 따라 달라 집니다. 다른 서버에서 hello 도구를 실행 하는 경우 처리량이 hello 해당 서버 tooMicrosoft Azure에서에서 계산 됩니다. 또한 hello hello 서버의 하드웨어 구성 될 수 있습니다는 hello 구성 서버에서 다르므로 도구 보고서 hello 하는 처리량을 달성 하는 hello 올바르지 않을 합니다.

3. Hello.zip 폴더를 추출 합니다.  
hello 폴더에는 여러 개의 파일 및 하위 폴더 포함 됩니다. hello 실행 파일은 ASRDeploymentPlanner.exe hello 상위 폴더에 있습니다.

    예제:  
    Hello.zip 파일 tooE 복사: \ 드라이브 하 고 압축을 풉니다.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>기능
Hello 명령줄 도구 (ASRDeploymentPlanner.exe) hello 다음 세 가지 모드 중 하나에서 실행할 수 있습니다.

1. 프로파일링  
2. 보고서 생성
3. 처리량 가져오기

첫째, 프로 파일링 모드 toogather VM 데이터 변동 및 IOPS에 hello 도구를 실행 합니다. 다음으로 toofind hello 네트워크 대역폭 및 저장소 요구 사항 hello 도구 toogenerate hello 보고서를 실행 합니다.

## <a name="profiling"></a>프로파일링
프로 파일링 모드 hello 배포 계획 도구 toohello vCenter 서버/vSphere hello VM에 대 한 ESXi 호스트 toocollect 성능 데이터를 연결합니다.

* 프로 파일링는 직접 연결 되지 toothem 되기 때문에 hello 성능 hello 프로덕션 Vm에 적용 되지 않습니다. Hello vCenter 서버/vSphere ESXi 호스트에서 모든 성능 데이터가 수집 됩니다.
* 프로 파일링, hello 도구 쿼리 hello vCenter 서버/vSphere ESXi 호스트 15 분 마다 한 번으로 인해 hello 서버에 미치는 영향은 있다고 tooensure 합니다. 이 쿼리 간격 hello 도구 매 분의 성능 카운터 데이터를 저장 하기 때문에 프로 파일링의 정확도 손상 시 키 지 않습니다.

### <a name="create-a-list-of-vms-tooprofile"></a>Vm tooprofile 목록 만들기
첫째, 프로 파일링 hello Vm toobe 목록이 필요 합니다. 절차를 수행 하는 hello hello VMware vSphere PowerCLI 명령을 사용 하 여 vCenter 서버/vSphere ESXi 호스트에 Vm의 모든 hello 이름을 얻을 수 있습니다. 또는 파일 hello 친숙 한 이름에 나열할 수 있습니다 또는의 IP 주소 hello Vm tooprofile 수동으로 되도록 합니다.

1. Toohello PowerCLI에 설치 된 VMware vSphere 해당 VM에에서 로그인 합니다.
2. Hello VMware vSphere PowerCLI 콘솔을 엽니다.
3. Hello 스크립트에 대 한 hello 실행 정책이 설정 되어 있는지 확인 합니다. 해제 된 경우 hello 관리자 모드에서 VMware vSphere PowerCLI 콘솔을 시작 하 고 hello 다음 명령을 실행 하 여 사용 하도록 설정 합니다.

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. 옵션은 필요 toorun hello 연결 VIServer cmdlet의 hello 이름으로 인식 되지 않으면 다음 명령을 수 있습니다.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget 모든 hello vCenter 서버/vSphere ESXi에 Vm의 호스트 이름과 hello 목록이 실행된 hello 두 명령은 여기에 나열 된.txt 파일에 저장 합니다.
&lsaquo;서버 이름&rsaquo;, &lsaquo;사용자 이름&rsaquo;, &lsaquo;암호&rsaquo;, &lsaquo;outputfile.txt&rsaquo;을 입력 내용으로 바꿉니다.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. 메모장에서 hello 출력 파일을 열고 tooprofile tooanother 파일 (예를 들어 ProfileVMList.txt) 줄당 하나의 VM 이름을 하려는 모든 Vm의 hello 이름을 복사 합니다. 이 파일은 입력된 toohello로 사용 *-VMListFile* hello 명령줄 도구의 매개 변수입니다.

    ![Hello 배포 계획에 VM 이름 목록](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>프로파일링 시작
프로 파일링 하는 Vm toobe hello 목록을 확보 한 후 프로 파일링 모드에서 hello 도구를 실행할 수 있습니다. 프로 파일링 모드에서 hello hello 도구 toorun의 필수 및 선택적 매개 변수 목록은 다음과 같습니다.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| 매개 변수 이름 | 설명 |
|---|---|
| -Operation | StartProfiling |
| -Server | hello 정규화 된 도메인 이름 또는 해당 Vm이 프로 파일링 toobe hello vCenter 서버/vSphere ESXi 호스트의 IP 주소입니다.|
| -User | hello 사용자 이름 tooconnect toohello vCenter 서버/vSphere ESXi 호스트입니다. hello 사용자는 최소한 toohave 읽기 전용 액세스가 필요 합니다.|
| -VMListFile | 프로 파일링 하는 Vm toobe hello 목록을 포함 하는 hello 파일입니다. 절대 또는 상대 hello 파일 경로일 수 있습니다. hello 파일 줄당 하나의 VM 이름/i P 주소를 포함 해야 합니다. Hello 파일에 지정 된 가상 컴퓨터 이름을 hello vCenter 서버/vSphere ESXi 호스트에 hello VM 이름과 달라 서 hello 해야 합니다.<br>예를 들어 hello 파일 VMList.txt Vm 다음 hello를 포함 되어 있습니다.<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
| -NoOfDaysToProfile | hello 기간 (일)를 프로 파일링은 toobe 실행 합니다. 15 일 이상 hello를 통해 사용자 환경에서 작업 부하 패턴 hello tooensure 확인 되는 기간과 tooprovide는 정확 하 게 권장 구성에 사용 되는 지정 된 프로 파일링을 실행 하는 것이 좋습니다. |
| -Directory | (선택 사항) hello 범용 명명 규칙 (UNC) 또는 로컬 디렉터리 경로 toostore 프로 파일링 하는 동안 생성 된 데이터를 프로 파일링 합니다. 디렉터리 이름이 제공 되지 않으면 'ProfiledData' hello 현재 경로 아래 라는 hello 디렉터리는 hello 기본 디렉터리로 사용 됩니다. |
| -Password | (선택 사항) hello 암호 toouse tooconnect toohello vCenter 서버/vSphere ESXi 호스트입니다. 지정 하지 않으면 하나 이제, 하는 경우 메시지가 표시 됩니다에 대 한 hello 명령이 실행 되 면입니다.|
| -StorageAccountName | (선택 사항) hello 저장소 계정 이름 사용 되는 toofind hello 처리량 데이터를 복제 하기 위해 수행할 수 있는 온-프레미스 tooAzure 합니다. hello 도구 업로드 테스트 데이터 toothis 저장소 계정 toocalculate 처리량입니다.|
| -StorageAccountKey | Tooaccess hello 저장소 계정 사용 (선택 사항) hello 저장소 계정 키 Azure 포털 toohello 이동 > 저장소 계정은 ><*저장소 계정 이름*>> 설정 > 선택 키 > Key1 (또는 클래식 저장소 계정에 대 한 기본 액세스 키)입니다. |
| -Environment | (선택 사항) 대상 Azure Storage 계정 환경입니다. AzureCloud, AzureUSGovernment, AzureChinaCloud의 3가지 값 중 하나일 수 있습니다. 기본값은 AzureCloud입니다. 대상 Azure 지역은 Azure 미국 정부 또는 Azure China 클라우드의 경우 hello 매개 변수를 사용 합니다. |


최소 15 too30 일에 대 한 프로 파일링 할 Vm에 유지 하는 것이 좋습니다. Hello 기간을 프로 파일링, 하는 동안 ASRDeploymentPlanner.exe 계속 실행 됩니다. hello 도구 일 이내에 프로 파일링 시간 입력을 가져옵니다. Hello 공개 미리 보기에서 몇 시간 또는 분 hello 도구의 빠른 테스트에 대 한 tooprofile를 원하는 tooconvert hello 시간 일 hello 해당 측정값으로 할 수 있습니다. 예를 들어, 30 분 동안 tooprofile hello 입력 해야 30/(60*24) = 0.021 일 합니다. 허용 시간을 프로 파일링 hello 최소 30 분입니다.

프로 파일링 하는 동안 저장소 계정 이름 및 사이트 복구 프로세스 서버 tooAzure 또는 hello 구성 서버에서 복제 시 hello 얻을 수 있는 키 toofind hello 처리량을 선택적으로 전달할 수 있습니다. 프로 파일링 동안 hello 저장소 계정 이름과 키 전달 되지 않은 경우 hello 도구 달성 가능한 처리량을 계산 되지 않습니다.

다양 한 가지 Vm에 대 한 hello 도구의 여러 인스턴스를 실행할 수 있습니다. 모든 집합을 프로 파일링 하는 hello hello VM 이름이 반복 되지 않는 것을 확인 합니다. 예를 들어 10 개의 Vm을 프로 파일링 했습니다 (VM10 통해 VM1) 몇 일 후 원하는 tooprofile 다른 5 개의 Vm 및 (VM11 VM15 통해)를 Vm의 hello 두 번째 집합에 대 한 다른 명령줄 콘솔 hello 도구를 실행할 수 있습니다 (VM11 VM15 통해). Vm의 두 번째 집합 hello hello 첫 번째 프로 파일링 인스턴스에서 모든 VM 이름이 있는 경우 두 번째 실행 hello에 대 한 다른 출력 디렉터리를 사용 했는지 확인 합니다. 두 인스턴스가 hello 도구의 프로 파일링 하기 위해 사용 되는 경우 hello 동일한 Vm 및 사용 하 여 hello 동일한 출력 디렉터리, hello 생성 된 보고서를 잘못 됩니다.

VM 구성은 작업 프로 파일링 하는 hello hello 맨 앞에 한 번 캡처된 되며 VMDetailList.xml 라는 파일에 저장 합니다. 이 정보는 hello 보고서가 생성 될 때 사용 됩니다. VM 구성 (예를 들어의 횟수가 증가 코어, 디스크 또는 Nic) 프로 파일링의 hello 시작 toohello 끝에서의 변경 내용이 캡처되지 않습니다. 프로 파일링 된 VM 구성을 hello 공개 미리 보기에서 프로 파일링 hello 과정 동안 변경 된 경우 다음은 hello 해결 방법 tooget 최신 VM 세부 hello 보고서를 생성할 때:

* VMdetailList.xml를 백업 하 고 현재 위치에서 hello 파일을 삭제 합니다.
* -사용자 및-Password 인수 전달 hello 시 보고서를 생성 합니다.

명령 프로 파일링 하는 hello hello 디렉터리를 프로 파일링에 여러 개의 파일을 생성 합니다. 삭제 하지 마십시오 hello 파일 이렇게 하면 보고서를 생성 하므로 영향을 주므로.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>예제 1: 프로필 Vm에서 온-프레미스 tooAzure 찾기 hello 처리량 및 30 일에 대 한
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>예제 2: 15일 동안 프로파일링

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Hello 도구의 빠른 테스트에 대 한 1 시간에 대 한 예 3: 프로필 Vm
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Hello 서버 해당 hello 도구는 다시 부팅 되었거나 중지 된에서 실행 하거나 닫을 경우 도구 Ctrl을 사용 하 여 hello + C, hello 프로 파일링 데이터는 유지 합니다. 그러나 확률이 있습니다의 누락 된 hello 프로 파일링된 데이터의 최근 15 분입니다. 이러한 상황에서 프로 파일링 모드의 hello 도구 hello 서버를 다시 시작한 후 다시 실행 합니다.
>* Hello 저장소 계정 이름과 키 전달 때, 프로 파일링의 hello 마지막 단계에서 hello 도구 측정값 hello 처리량입니다. 프로 파일링을 완료 하기 전에 hello 도구 닫혀 있는 경우에 hello 처리량 계산 되지 않습니다. toofind hello 처리량을 생성 하기 전에 hello 보고서, hello 명령줄 콘솔에서 hello GetThroughput 작업을 실행할 수 있습니다. 그렇지 않은 경우 생성 된 hello 보고서 hello 처리량 정보가 포함 되지 않습니다.


## <a name="generate-a-report"></a>보고서 생성
hello 도구는 Microsoft Excel 매크로 사용 파일 (XLSM 파일)을 모든 hello 배포 권장 사항 요약 hello 보고서 출력으로 생성 합니다. hello 보고서 DeploymentPlannerReport_ 라는 <*고유 숫자 식별자*>.xlsm 및 hello에 디렉터리를 지정 합니다.

완료 되 면 프로 파일링 보고서 생성 모드에서 hello 도구를 실행할 수 있습니다. 다음 표에 hello 보고서 생성 모드에서 매개 변수 toorun 필수 및 선택적 도구 목록이 포함 되어 있습니다.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|매개 변수 이름 | 설명 |
|-|-|
| -Operation | GenerateReport |
| -Server |  hello vCenter/vSphere 서버 정규화 된 도메인 이름 또는 IP 주소 (사용 하 여 hello 동일한 이름 또는 IP 주소 프로 파일링의 hello 시 사용 하는) 있는 hello 해당 보고서가 생성 된 toobe Vm을 프로 파일링 할 위치. 프로 파일링의 hello 시 vCenter 서버를 사용 하는 경우 사용할 수 없다는 vSphere 서버 보고서 생성 및 반대의 note 합니다.|
| -VMListFile | 프로 파일링 하는 Vm의 보고서 hello hello 목록을 포함 하는 hello 파일에 대해 생성 된 toobe입니다. 절대 또는 상대 hello 파일 경로일 수 있습니다. 하나의 VM 이름 또는 IP 주소가 한 줄당 hello 파일 포함 됩니다. hello 파일에 지정 된 hello VM 이름을 hello vCenter 서버/vSphere ESXi 호스트 및 프로 파일링 하는 동안 사용 된 일치 항목에 있는 hello VM 이름은 동일 hello 해야 합니다.|
| -Directory | (선택 사항) hello UNC 또는 로컬 디렉터리 경로 여기서 hello를 프로 파일링 데이터 (프로 파일링 하는 동안 생성 된 파일)에 저장 됩니다. 이 데이터는 hello 보고서 생성에 필요 합니다. 이름을 지정하지 않으면 'ProfiledData' 디렉터리가 사용됩니다. |
| -GoalToCompleteIR | (선택 사항) hello hello의 초기 복제는 hello에 Vm을 프로 파일링 하는 시간 수가 toobe 완료 해야 합니다. 생성 된 hello כ ַ ׁ Vm 초기 복제를 완료할 수에 지정 된 hello hello 수 시간입니다. hello 기본값은 72 시간입니다. |
| -User | (선택 사항) hello 사용자 이름 toouse tooconnect toohello vCenter/vSphere 서버입니다. hello 이름은 hello Vm 디스크 hello 수, 코어 수, toouse hello 보고서에 Nic의 번호 등의 사용 되는 toofetch hello 최신 구성 정보입니다. Hello 이름이 제공 되지 않는 경우 hello 개시 프로 파일링의 hello 시작 부분에서 수집 된 hello 구성 정보 사용 됩니다. |
| -Password | (선택 사항) hello 암호 toouse tooconnect toohello vCenter 서버/vSphere ESXi 호스트입니다. Hello 암호를 매개 변수로 지정 하지 않으면 메시지가 표시 됩니다에 대 한 나중 hello 명령이 실행 되 면입니다. |
| -DesiredRPO | (선택 사항) hello 원하는 복구 지점 목표를 분에서입니다. hello 기본값은 15 분입니다.|
| -Bandwidth | 대역폭(Mbps)입니다. hello 매개 변수 toouse toocalculate hello RPO hello에 대 한 얻을 수 있는 대역폭을 지정 합니다. |
| -StartDate | (선택 사항) hello mm에서 시작 날짜 및 시간-DD-YYYY:HH:MM (24 시간 형식). *StartDate*는 *EndDate*와 함께 지정해야 합니다. 시작 날짜를 지정 하면 StartDate와 EndDate 사이의 수집 되는 hello 프로 파일링 데이터에 대 한 hello 보고서가 생성 됩니다. |
| -EndDate | (선택 사항) hello 종료 날짜 및 시간 mm에서-DD-YYYY:HH:MM (24 시간 형식). *EndDate*는 *StartDate*와 함께 지정해야 합니다. 종료 날짜를 지정 하면 StartDate와 EndDate 사이의 수집 되는 hello 프로 파일링 데이터에 대 한 hello 보고서가 생성 됩니다. |
| -GrowthFactor | (선택 사항) hello 증가 비율을 백분율로 표시 합니다. hello 기본값은 30%입니다. |
| -UseManagedDisks | (선택 사항)UseManagedDisks - 예/아니요. 기본값은 [예]입니다. 관리 되지 않는 디스크 대신 관리 되는 디스크에서 가상 컴퓨터의 장애 조치/테스트 장애 조치는 수행 하는 여부 고려 하면 단일 저장소 계정에 배치할 수 있는 가상 컴퓨터의 hello 수가 계산 됩니다. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>예제 1: hello를 프로 파일링 데이터 hello 로컬 드라이브에 있으면 기본 값으로 보고서를 생성
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>예제 2: hello를 프로 파일링 데이터는 원격 서버에 있으면 보고서 생성
Hello 원격 디렉터리에 읽기/쓰기 권한이 있어야 합니다.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>예제 3: 지정 된 시간 안에 특정 대역폭 및 목표 toocomplete IR 사용 하 여 보고서 생성
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>예 4: 대신 hello 기본 30% 5% 증가 비율을 사용 하 여 보고서를 생성 합니다.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>예제 5: 프로파일링된 데이터의 하위 집합으로 보고서 생성
예를 들어 프로 파일링된 데이터의 30 일 이내와 때 toogenerate 보고서만 20 일에 대 한 합니다.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>예제 6: 5분 동안의 RPO 보고서 생성
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Hello 계산에 사용 된 백분위 수 값
**Hello 성능 메트릭 중 어떤 기본 백분위 수 값은 보고서를 생성 하는 경우에 hello 도구 사용을 프로 파일링 하는 동안 수집 하나요?**

hello 도구 기본값 toohello 95 백분위 수 값을 읽기/쓰기 IOPS, IOPS, 및 모든 hello Vm의 프로 파일링 하는 중에 수집 된 데이터 변동을 작성 합니다. 이 메트릭은 Vm에 임시 이벤트 때문에 표시 될 수는 hello 100th 백분위 수 스파이크 보장은 사용된 되지 않습니다 toodetermine 대상 저장소 계정 및 소스 대역폭 요구 사항입니다. 예를 들어 일시적 이벤트는 하루에 한 번 실행하는 백업 작업, 주기적 데이터베이스 인덱싱 또는 분석 보고서 생성 작업 또는 기타 유사한 단기적 시점 이벤트일 수 있습니다.

95 백분위 수 값을 사용 하 여 hello 작업은 Azure에서 실행 하는 경우 제공 하면 전체 실제 작업 부하 특성 그리고 최상의 성능을 hello 합니다. 해야 toochange이이 숫자 예측 하지 못한 합니다. Hello 값 (toohello 90 번째 백분위 수, 예:)를 변경한 경우에 hello 구성 파일을 업데이트할 수 있습니다 *ASRDeploymentPlanner.exe.config* hello 기본 폴더와 새 보고서 toogenerate hello 프로 파일링 할 기존에 저장 데이터입니다.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>증가율 고려 사항
**배포를 계획할 때 증가율을 왜 고려해야 하나요?**

것이 중요 한 tooaccount 시간이 지남에 따라 사용에서 잠재적 증가 가정 하 여 작업 특성에서 확장 합니다. 작업 특성을 변경 하는 경우 현재 위치에서 보호 되 면 hello 보호를 다시 활성화 및 비활성화 하지 않고 tooa 다른 저장소 계정에 대 한 보호를 전환할 수 없습니다.

예를 들어 현재 VM이 표준 저장소 복제 계정에 적합하다고 가정해 보겠습니다. 다음 3 개월 hello를 통해 몇 가지 변경 내용이 가능성이 toooccur:

* hello hello VM에서 실행 되는 hello 응용 프로그램의 사용자 수 증가 합니다.
* hello 결과 증가 변동을 hello VM에는 사이트 복구 복제 속도 맞출 수 있도록 hello VM toogo toopremium 저장소가 있어야 합니다.
* 따라서 toodisable가 쿼리하고 다시 보호 tooa 프리미엄 저장소 계정을 사용 하도록 설정 합니다.

배포를 계획 하는 동안 및 hello 기본값은 30% 동안 증가 대 한 계획 하는 것이 좋습니다. 프로그램 응용 프로그램 사용 패턴 및 증가 예측 hello 전문가이 숫자를 적절 하 게 변경할 수 있습니다 및 보고서를 생성 하는 중입니다. 여러 보고서를 생성할 수는 또한 hello로 다양 한 성장 요소와 동일 데이터 프로 파일링 하 고 어떤 대상 저장소와 소스 대역폭 권장 사항을 잘 결정 합니다.

생성 된 hello Microsoft Excel 보고서는 다음 정보는 hello를 포함 되어 있습니다.

* [입력](site-recovery-deployment-planner.md#input)
* [권장 사항](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [권장 사항-대역폭 입력](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [VM<->저장소 배치](site-recovery-deployment-planner.md#vm-storage-placement)
* [호환되는 VM](site-recovery-deployment-planner.md#compatible-vms)
* [호환되지 않는 VM](site-recovery-deployment-planner.md#incompatible-vms)

![Deployment Planner](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>처리량 가져오기

Site Recovery는 복제, GetThroughput 모드로 hello 도구를 실행 하는 동안 온-프레미스 tooAzure에서 얻을 수 있는 tooestimate hello 처리량입니다. hello 도구에서 hello 처리량 도구 hello hello 서버에서 실행 되 고 계산 합니다. 이상적으로이 서버 hello 구성 서버에 대 한 크기 조정 가이드를 기반으로 합니다. 사이트 복구 인프라 구성 요소 온-프레미스를 이미 배포한 경우 hello 구성 서버에서 hello 도구를 실행 합니다.

명령줄 콘솔을 열고 toohello 사이트 복구 배포 계획 도구 폴더를 이동 합니다. 다음 매개 변수를 사용하여 ASRDeploymentPlanner.exe를 실행합니다.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|매개 변수 이름 | 설명 |
|-|-|
| -Operation | GetThroughput |
| -Directory | (선택 사항) hello UNC 또는 로컬 디렉터리 경로 여기서 hello를 프로 파일링 데이터 (프로 파일링 하는 동안 생성 된 파일)에 저장 됩니다. 이 데이터는 hello 보고서 생성에 필요 합니다. 디렉터리 이름을 지정하지 않으면 'ProfiledData' 디렉터리가 사용됩니다. |
| -StorageAccountName | 사용 하는 hello 대역폭 toofind tooAzure 온-프레미스에서에서 데이터 복제에 대 한 사용 hello 저장소 계정 이름입니다. hello 도구 업로드 테스트 데이터 toothis 저장소 계정 toofind hello 사용 하는 대역폭입니다. |
| -StorageAccountKey | tooaccess hello 저장소 계정 사용 hello 저장소 계정 키 Azure 포털 toohello 이동 > 저장소 계정은 ><*저장소 계정 이름*>> 설정 > 선택 키 > Key1 (또는 클래식 저장소 계정에 대 한 기본 액세스 키)입니다. |
| -VMListFile | 사용 하는 계산 hello 대역폭에 대 한 프로 파일링 하는 Vm toobe hello 목록을 포함 하는 hello 파일입니다. 절대 또는 상대 hello 파일 경로일 수 있습니다. hello 파일 줄당 하나의 VM 이름/i P 주소를 포함 해야 합니다. hello 파일에 지정 된 hello VM 이름은 hello vCenter 서버/vSphere ESXi 호스트에 있는 hello VM 이름은 동일 hello 해야 합니다.<br>예를 들어 hello 파일 VMList.txt Vm 다음 hello를 포함 되어 있습니다.<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (선택 사항) 대상 Azure Storage 계정 환경입니다. AzureCloud, AzureUSGovernment, AzureChinaCloud의 3가지 값 중 하나일 수 있습니다. 기본값은 AzureCloud입니다. 대상 Azure 지역은 Azure 미국 정부 또는 Azure China 클라우드의 경우 hello 매개 변수를 사용 합니다. |

hello 도구 여러 개 만들어 64MB asrvhdfile <> #.vhd 파일 (여기서 "#"는 파일 수가 hello) hello 지정 된 디렉터리에 있습니다. hello 도구 hello 파일 toohello 저장소 계정 toofind hello 처리량을 업로드합니다. Hello 처리량을 측정 하는 hello 도구 및 로컬 서버 hello hello 저장소 계정에서 모든 hello 파일을 삭제 합니다. Hello 도구 처리량을 계산 하는 동안 어떤 이유로 종료 되 면 hello 저장소 또는 로컬 서버 hello hello 파일 삭제 되지 않습니다. Toodelete 가지게을 수동으로 합니다.

hello 처리량은 지정 된 기간의 시간 단위로 측정 되며 hello 최대 처리량 Site Recovery는 복제 시 얻을 수 있는 기타 모든 요소가 남아 있는 hello 동일 합니다. 예를 들어, 모든 응용 프로그램 시작 복제 하는 동안 동일한 네트워크에서 실제 처리량 hello 다릅니다 hello에 더 많은 대역폭을 사용 하는 경우. 구성 서버에서 hello GetThroughput 명령을 실행 하는 경우에 hello 도구 진행 중인 복제 및 보호 되는 Vm의 인식 하지 않습니다. hello hello 측정 된 처리량의 결과 차이가 있는 경우 Vm을 보호 하는 hello 경우 작업이 실행 되는 GetThroughput hello 변동 높은 데이터 있습니다. 실행 하는 hello 도구 다양 한 포인트에서 toounderstand 프로 파일링 하는 중에 다양 한 시간에 수준을 달성 어떤 출력 하는 것이 좋습니다. Hello 보고서 hello 도구 hello 마지막 측정 된 처리량을 보여 줍니다.

### <a name="example"></a>예제
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Hello 수 있는 서버에서 hello 도구를 실행 hello 구성 서버로 CPU 특징과 같은 저장소입니다.
>
> 복제에 대 한 hello 권장 되는 대역폭 toomeet hello RPO 100%의 hello 시간을 설정 합니다. Hello 도구에서 보고 하는 hello 달성 처리량을 증가 표시 되지 않으면 hello 오른쪽 대역폭을 설정한 후 다음 hello지 않습니다.
>
>  1. 서비스 품질 (QoS) 사이트 복구 처리량을 제한 하는 모든 네트워크 인지 toodetermine를 확인 합니다.
>
>  2. 사이트 복구 자격 증명 모음에 물리적으로 지원 되는 Microsoft Azure 지역 toominimize 네트워크 대기 시간이 가장 가까운 hello 인지 toodetermine를 확인 합니다.
>
>  3. 로컬 저장소 특성 toodetermine를 hello 하드웨어 (예를 들어 HDD tooSSD)를 향상 시킬 수 있는지 여부를 확인 합니다.
>
>  4. Hello 프로세스 서버에서 사이트 복구 설정이 hello도 변경[hello 복제에 사용 되는 네트워크 대역폭 양을 증가](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth)합니다.

## <a name="recommendations-with-desired-rpo-as-input"></a>입력으로 원하는 RPO를 사용하는 권장 사항

### <a name="profiled-data"></a>프로파일링된 데이터

![hello 배포 계획의 hello 프로 파일링 데이터 뷰](./media/site-recovery-deployment-planner/profiled-data-period.png)

**데이터 프로 파일링 된 기간**: hello 기간 동안는 hello 프로 파일링 된를 실행 합니다. 기본적으로 hello 도구 보고서를 생성 하는 동안 StartDate와 EndDate 옵션을 사용 하 여 특정 기간에 대 한 hello 보고서를 생성 하지 않는 한 hello 계산에서는 모든 프로 파일링된 데이터를 포함 합니다.

**서버 이름**: hello 이름 또는 IP 주소 hello VMware vCenter 또는 ESXi 호스트 인 Vm의 보고서가 생성 됩니다.

**RPO를 원하는**: 배포에 대 한 hello 복구 지점 목표입니다. 기본적으로 hello 15, 30 ~ 60 분의 RPO 값에 대 한 네트워크 대역폭을 계산 하는 데 필요 합니다. Hello 선택에 따라, 영향을 받는 hello 값 hello 시트에서 업데이트 됩니다. Hello를 사용한 경우 *DesiredRPOinMin* 매개 변수 값은 hello RPO 원하는 결과에 표시 하는 hello 보고서를 생성 하는 중입니다.

### <a name="profiling-overview"></a>프로파일링 개요

![Hello 배포 계획에 대 한 프로 파일링 결과](./media/site-recovery-deployment-planner/profiling-overview.png)

**가상 컴퓨터를 프로 파일링 총**: hello를 프로 파일링된 데이터를 사용할 수는 Vm의 총 수입니다. Hello VMListFile의 프로 파일링 되지 된 있는 모든 Vm의 이름이 해당 Vm hello 보고서 생성에서 고려 되지 않는 하 고 프로 파일링 된 총 Vm 수 hello에서에서 제외 됩니다.

**호환 가상 컴퓨터**: hello Site Recovery를 사용 하 여 보호 된 tooAzure 일 수 있는 Vm의 수입니다. 그는 hello에 대 한 필요한 네트워크 대역폭, 저장소 계정 수, Azure의 코어 수 및 구성 서버 및 추가 프로세스 서버 수가 계산 됩니다 호환 Vm의 hello 총 수입니다. 호환 가능한 모든 VM의 hello 세부 사항은 hello "호환 Vm" 섹션에서에서 사용할 수 있습니다.

**호환 되지 않는 가상 컴퓨터**: hello Site recovery 보호를 위해 호환 되지 않는 프로 파일링 된 Vm의 수입니다. 비 호환성에 대 한 hello 이유 hello "호환 되지 않는 Vm" 섹션에에서 기록 됩니다. Hello VMListFile의 프로 파일링 되지 된 모든 Vm의 이름이 해당 Vm hello 호환 되지 않는 Vm 개수에서 제외 됩니다. 이러한 Vm은 "데이터 찾을 수 없습니다" hello "호환 되지 않는 Vm" 섹션의 hello 끝에 나열 됩니다.

**원하는 RPO**: 원하는 복구 지점 목표(분)입니다. 세 개의 RPO 값에 대 한 hello 보고서가 생성 됩니다: (기본값), 15, 30 ~ 60 분입니다. hello 보고서의 hello 대역폭 권장 조치는 hello 시트의 오른쪽 위 hello에 hello 원하는 RPO 드롭 다운 목록에서 선택한 항목에 따라 변경 됩니다. Hello를 사용 하 여 hello 보고서를 생성 한 경우 *-DesiredRPO* 매개 변수의 사용자 지정 값을 사용자 지정 값이 hello hello 원하는 RPO 드롭 다운 목록에는 기본적으로 표시 됩니다.

### <a name="required-network-bandwidth-mbps"></a>필요한 네트워크 대역폭(Mbps)

![Hello 배포 계획에 필요한 네트워크 대역폭](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**100%의 hello 시간 RPO toomeet:** hello Mbps toobe에 할당할 대역폭 toomeet 원하는 RPO에 100%의 hello 시간 하는 것이 좋습니다. 이 대역폭 양을 해야 RPO 위반에 호환 되는 모든 Vm tooavoid 델타 안정 상태 복제 하기 위해 전용입니다.

**toomeet RPO hello 시간의 90%**: 광대역 가격으로 인해 또는 다른 이유로 경우 설정할 수 없습니다. 필요한 대역폭 toomeet hello 원하는 RPO에 100%의 hello 시간을 선택할 수 있습니다 설정 낮은 대역폭 toogo 충족할 수 있는 사용자 원하는 RPO hello 시간의 90%입니다. toounderstand hello에 영향을 줄이 더 낮은 대역폭 설정, hello 보고서 hello 개수와 RPO 위반 tooexpect 기간에는 가상 분석을 제공 합니다.

**처리량 달성된:** 기반이 hello 저장소 계정 위치한 hello GetThroughput 명령 toohello Microsoft Azure 영역을 실행 한 hello 서버에서 hello 처리량입니다. 이 처리량 번호에 구성 서버 또는 프로세스 서버 특성 저장소 및 네트워크 남아 있는 경우 사이트 복구를 사용 하 여 호환 가능한 Vm의 것과 동일한 hello hello를 보호 하는 경우 얻을 수 있는 예상 hello 수준을 나타냅니다. hello 서버 hello 도구를 실행 합니다.

복제에 대 한 hello 권장 되는 대역폭 toomeet hello RPO 100%의 hello 시간을 설정 해야 합니다. Hello 도구에서 보고 하는 대로 달성 hello 처리량을 증가 시 키 지 보이지 않으면 hello 대역폭을 설정한 후 hello 다음을 수행 합니다.

1. 서비스 품질 (QoS) 사이트 복구 처리량을 제한 하는 모든 네트워크 인지 toosee를 확인 합니다.

2. 사이트 복구 자격 증명 모음에 물리적으로 지원 되는 Microsoft Azure 지역 toominimize 네트워크 대기 시간이 가장 가까운 hello 인지 toosee를 확인 합니다.

3. 로컬 저장소 특성 toodetermine를 hello 하드웨어 (예를 들어 HDD tooSSD)를 향상 시킬 수 있는지 여부를 확인 합니다.

4. Hello 프로세스 서버에서 사이트 복구 설정이 hello도 변경[hello 복제에 사용 되는 금액 네트워크 대역폭을 높일](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth)합니다.

구성 서버 또는 이미 Vm 보호는 프로세스 서버 hello 도구를 실행 하는 경우 hello 도구를 여러 번 실행 합니다. hello 달성 hello 양의 시간 해당 시점에 처리 중인 변동에 따라 처리량 번호 변경 됩니다.

모든 엔터프라이즈 Site Recovery 배포의 경우 [ExpressRoute](https://aka.ms/expressroute)를 사용하는 것이 좋습니다.

### <a name="required-storage-accounts"></a>필요한 저장소 계정
모든 필수 tooprotect 됩니다 (표준 및 프리미엄) hello 총 수의 스토리지 계정 차트 표시 다음 hello hello 호환 Vm입니다. 저장소는 각 VM에 대 한 toouse 계정 toolearn hello "VM 저장소 배치" 섹션을 참조 합니다.

![Hello 배포 계획에 필요한 저장소 계정](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>필요한 Azure 코어 수
이 결과 hello 전에 모든 장애 조치 또는 테스트 장애 조치 hello 호환 Vm을 설정 하는 코어 toobe 총 수입니다. Hello 시점에 사이트 복구가 실패 한 toocreate Vm 너무 적은 코어를 hello 구독에서 사용할 수 있는 경우 테스트 장애 조치 또는 장애 조치 합니다.

![필요한 Azure hello 배포 계획 코어 수](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>필요한 온-프레미스 인프라
이 그림은 hello 총 호환 Vm hello 모든 구성 서버 및 추가 프로세스 서버 toobe 구성 tooprotect 충분 합니다. 지원 되는 hello에 따라 [크기 hello 구성 서버에 대 한 권장 사항](https://aka.ms/asr-v2a-on-prem-components), hello 도구 추가 서버를 권장할 수도 있습니다. hello hello 매일 변동 또는 hello (VM 당 3 개의 디스크의 평균 가정) 보호 된 Vm의 최대 수의 더 큰 hello 권장 사항은, 구성 서버 hello 또는 hello 추가 프로세스 서버에 처음 적중 중 더 합니다. Hello "Input" 섹션에에서는 보호 된 디스크의 총 수 및 일 당 총 변동 hello 세부 정보를 찾을 수 있습니다.

![Hello 배포 계획에서 필요한 온-프레미스 인프라](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>가상 분석
이 분석 RPO toobe 원하는 hello에 대 한 낮은 대역폭 충족 hello 시간의 90%에만 개수 위반 hello 기간을 설정 하는 경우 프로 파일링 하는 동안 발생할 수에 대해 간략하게 설명 합니다. 지정한 날짜에 하나 이상의 RPO 위반이 발생할 수 있습니다. hello 그래프 hello 피크 hello 일의 RPO를 보여 줍니다.
이 분석에 따라, 낮은 대역폭 hello에 지정 된 모든 일 수와 최대 하루 적중 RPO RPO 위반 hello 수와 허용 되는 경우를 결정할 수 있습니다. 허용 되는 경우 복제에 대 한 hello 낮은 대역폭 할당을 다른 hello 더 높은 대역폭이 제안된 toomeet hello 원하는 RPO hello 시간의 100%를 할당할 수 있습니다.

![Hello 배포 계획의 가상 분석](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>초기 복제에 권장되는 VM 일괄 처리 크기
이 섹션에서는 병렬 toocomplete hello 초기 복제 hello로 72 시간 이내에 보호할 수 있는 Vm 수 hello 대역폭 toomeet 원하는 RPO hello 시간 설정의 100%를 제안 하는 것이 좋습니다. 이 값은 구성 가능한 값입니다. toochange 보고서 생성 시간을 사용 하 여 hello에서 *GoalToCompleteIR* 매개 변수입니다.

hello 여기 그래프 대역폭 값의 범위 및 한 계산된 VM 일괄 처리 크기 count toocomplete 초기 복제 72 시간 동안에서 hello 평균에 따라 검색 VM 크기에 모든 hello 호환 Vm입니다.

Hello 공개 미리 보기에서 hello 보고서 지정 하지 않습니다는 Vm 일괄 처리에 포함 되어야 합니다. 각 VM의 크기를 hello "호환 Vm" 섹션 toofind 에서처럼 hello 디스크 크기를 사용할 수 있으며 일괄 처리에서는를 선택 하거나 알려진된 작업 특성에 따라 hello Vm을 선택할 수 있습니다. 초기 복제 변경 내용 hello hello 완료 시간, hello 실제 VM 디스크 크기에 따라, 디스크 공간 및 사용 가능한 네트워크 처리량을 사용 합니다.

![권장 VM 일괄 처리 크기](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>사용된 증가율 및 백분위 수 값
Hello hello 맨 아래에이 섹션에서는 hello 백분위 수 값 (기본값은 95 번째 백분위 수 임)의 프로 파일링 하는 hello Vm의 모든 hello 성능 카운터에 사용 되는 고 hello 증가 비율 (기본값은 30%) 모든 hello 계산에 사용 되는 합니다.

![사용된 증가율 및 백분위 수 값](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>입력으로 사용 가능한 대역폭을 사용하는 권장 사항

![입력으로 사용 가능한 대역폭을 사용하는 권장 사항](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Site Recovery 복제를 위해 x Mbps 이상의 대역폭을 설정할 수 없다는 것을 알고 있는 상황이 있을 수 있습니다. hello 도구 tooinput 사용 가능한 대역폭을 사용 하면 (사용 하 여 hello-보고서를 생성 하는 동안 대역폭 매개 변수) 및 get 분 후에 달성 가능한 RPO hello 합니다. 이 달성 가능한 RPO 값을 가진 추가 대역폭 tooset 필요 여부는 사용자가 확인이 rpo 재해 복구 솔루션을 갖추는 것을 결정할 수 있습니다.

![500 Mbps 대역폭에 사용 가능한 RPO](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>입력
hello 입력 워크시트 hello에 대 한 개요를 프로 파일링 VMware 환경을 제공 합니다.

![Hello 간략하게 VMware 환경을 프로 파일링](./media/site-recovery-deployment-planner/Input.png)

**시작 날짜** 및 **종료 날짜**: hello hello 프로 파일링 보고서 생성에 대 한 것으로 간주 되는 데이터의 시작 및 종료 날짜입니다. 기본적으로 hello 시작 날짜는 프로 파일링이 시작 되 면 hello 날짜 hello 종료 날짜는 hello 날짜 프로 파일링 하 고 있습니다. 이러한 매개 변수와 함께 hello 보고서가 생성 하는 경우 hello 'StartDate' 및 'EndDate' 값 수 있습니다.

**일을 프로 파일링의 총**: hello 총 기간 (일) hello 사이의 프로 파일링 시작 및 종료 날짜는 hello에 대 한 보고서가 생성 됩니다.

**호환 가상 컴퓨터 수가**: hello 사용할 hello 필요한 네트워크 대역폭에 대 한 호환 Vm의 총 수, 필요한 수의 스토리지 계정, Microsoft Azure 개 코어, 구성 서버 및 추가 프로세스 서버는 계산 됩니다.

**호환 되는 모든 가상 컴퓨터에서 디스크의 총 수**: hello 중 하나로 사용 되는 hello 번호 구성 서버와 hello 배포에 사용 되는 추가 프로세스 서버 toobe toodecide hello 수를 입력 합니다.

**가상 컴퓨터당 호환 되는 디스크의 평균 수**: 호환 되는 모든 Vm에 대해 계산 된 hello 디스크의 평균 수입니다.

**평균 디스크 크기 (GB)**: 호환 되는 모든 Vm에 대해 계산 된 hello 평균 디스크 크기입니다.

**RPO (분)을 원하는**: 어느 hello 기본 복구 지점 목표 또는 hello 값 hello 'DesiredRPO' 매개 변수에 대 한 시간에 전달 된 hello 필요한 보고서 생성 tooestimate의 대역폭입니다.

**대역폭 (Mbps) 원하는**: 보고서 생성 tooestimate hello 시 hello 'Bandwidth' 매개 변수에 대해 전달 된 값을 hello 달성 가능한 RPO 합니다.

**관찰 된 일반적인 데이터 변동을 (GB) 하루**: 모든 프로 파일링 일 동안 관찰 된 평균 데이터 변동을 hello 합니다. 이 번호는 hello 입력 toodecide hello 수의 구성 서버와 hello 배포에 사용 되는 추가 프로세스 서버 toobe 중 하나로 사용 됩니다.


## <a name="vm-storage-placement"></a>VM-저장소 배치

![VM-저장소 배치](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**디스크 저장소 유형**: 중 하나는 표준 또는 프리미엄 저장소 계정에 사용 되는 tooreplicate hello에 언급 된 해당 Vm을 hello 모든 **Vm tooPlace** 열입니다.

**접두사를 제안**: hello 저장소 계정 이름 지정에 사용할 수 있는 hello 제안 된 세 글자 접두사입니다. 고유한 접두사를 사용할 수 있지만 hello 도구 제안 뒤 hello [파티션 저장소 계정에 대 한 명명 규칙](https://aka.ms/storage-performance-checklist)합니다.

**계정 이름을 제안**: hello 제안 된 접두사를 포함 한 후 hello 저장소 계정 이름입니다. Hello 꺾쇠 괄호 안에 (< 및 >) 사용자 지정 사용자 입력이 포함 된 hello 이름을 바꿉니다.

**저장소 계정 로그**: 모든 hello 복제 로그 표준 저장소 계정에 저장 됩니다. 프리미엄 저장소 계정 tooa를 복제 하는 Vm에 대 한 로그 저장소에 대 한 추가 표준 저장소 계정이 설정 합니다. 여러 프리미엄 복제 저장소 계정에서 단일 표준 로그 저장소 계정을 사용할 수 있습니다. Vm을 복제 된 toostandard 저장소 계정을 사용 하 여 hello 로그에 대 한 동일한 저장소 계정입니다.

**제안 된 로그 계정 이름**: hello 제안 된 접두사를 포함 한 후 저장소 로그 계정 이름을 합니다. Hello 꺾쇠 괄호 안에 (< 및 >) 사용자 지정 사용자 입력이 포함 된 hello 이름을 바꿉니다.

**배치 요약**: hello에 대 한 요약 복제 시 hello hello 저장소 계정에 Vm의 부하를 총 및 테스트 장애 조치 또는 장애 조치 합니다. Hello 총 수가 Vm 매핑된 toohello 저장소 계정, 총 읽기/쓰기 IOPS 총이 저장소 계정에 배치 하는 모든 Vm에서 쓰기 (복제) IOPS, 총 설치 크기에 모든 디스크 및 디스크의 총 수를 포함 합니다.

**가상 컴퓨터 tooPlace**: 모든 목록이 hello 최적의 성능 및 사용에 대 한 저장소 계정을 지정 하는 hello에 배치 해야 하는 Vm입니다.

## <a name="compatible-vms"></a>호환되는 VM
![호환되는 VM에 대한 Excel 스프레드시트](./media/site-recovery-deployment-planner/compatible-vms.png)

**VM 이름**: hello VM 이름 또는 보고서가 생성 될 때 VMListFile hello에 사용 되는 IP 주소입니다. 또한이 열 hello (Vmdk)가 디스크를 연결 된 toohello Vm을 나열 합니다. 중복 이름 또는 IP 주소와 toodistinguish vCenter Vm에서 hello 이름 hello ESXi 호스트 이름이 포함 합니다. hello 나열된 ESXi 호스트는 hello 하나 hello VM 놓여진 위치 hello 도구 hello 기간을 프로 파일링 중에 발견 된 경우입니다.

**VM 호환성**: 값은 **예** 및 **예**\*입니다. **예** \* 용인지 경우 어떤 hello VM에 대 한 맞춤 [Azure 프리미엄 저장소](https://aka.ms/premium-storage-workload)합니다. 여기서 hello 높은 변동을 프로 파일링 또는 IOPS 디스크 P20 hello 또는 P30 범주에 적합 하지만 hello 디스크의 크기 hello 인해 P10 또는 P20 tooa 아래로 매핑된 toobe 합니다. hello 저장소 계정이 프리미엄 저장소 디스크 입력 toomap 디스크 크기에 맞게를 결정 합니다. 예:
* 128GB 미만은 P10입니다.
* GB too512 128GB는 P20입니다.
* GB too1024 512GB는 P30입니다.
* 1025 GB too2048 GB는 P40입니다.
* 2049 GB too4095 GB는 P50입니다.

Hello 도구 표시로 해당 VM 디스크의 작업 부하 특성 hello P20 hello 또는 P30 범주에 배치 하는 경우 hello 크기 아래로 tooa 낮은 프리미엄 저장소 디스크 형식을 매핑합니다 **예**\*합니다. 또한 hello 도구 hello 원본 디스크 크기 toofit hello 권장 프리미엄 저장소 디스크 형식을 변경 하거나 hello 대상 디스크 유형 장애 조치 후 변경 하는 것이 좋습니다.

**저장소 유형**: 표준 또는 프리미엄입니다.

**접두사를 제안**: hello 3 자의 저장소 계정 접두사입니다.

**저장소 계정**: hello 제안 된 저장소 계정 접두사를 사용 하는 hello 이름입니다.

**증가 비율) (된 읽기/쓰기 IOPS**: 최대 작업 읽기/쓰기 IOPS hello 디스크에 hello (기본값은 95 번째 백분위 수) hello 미래 증가 비율을 포함 하 여 (기본값은 30%). 총 읽기/쓰기 IOPS VM의 hello 참고가 아닙니다. 항상 hello VM의 개별 디스크의 읽기/쓰기 IOPS의 hello 합계 hello 최대 읽기/쓰기 IOPS의 hello VM은 해당 개별 디스크 hello 합계의 hello 최고 때문에 읽기/쓰기 IOPS의 hello 매분 중 프로 파일링 하는 기간.

**데이터 증가 비율) (있음 Mbps 단위로 변동**: hello 디스크에 hello 피크 변동률 (기본값은 95 번째 백분위 수) hello 미래 증가 비율을 포함 하 여 (기본값은 30%). 해당 hello 참고 hello VM의 총 데이터 변동을 항상 hello VM의 개별 디스크의 데이터 변동이의 hello 합계 hello VM의 최대 데이터 변동을 hello은 해당 개별 디스크의 변동 hello 합계의 hello 최대 기간을 프로 파일링 하는 hello에 매 분 동안 합니다.

**Azure VM 크기**: hello 이상적인이 온-프레미스 VM 클라우드 서비스를 Azure 가상 컴퓨터 크기 매핑됩니다. hello 매핑 hello 온-프레미스 VM의 메모리, 디스크/코어/Nic 및 읽기/쓰기 IOPS 수를 기반으로 합니다. hello 권장 항상 hello 온-프레미스 VM 특성 모두 일치 하는 hello 가장 낮은 하는 Azure VM 크기입니다.

**디스크 수**: hello hello VM에 가상 컴퓨터 디스크 (Vmdk)의 총 수입니다.

**디스크 크기 (GB)**: hello hello VM의 모든 디스크의 총 설치 크기입니다. hello 도구는 또한 hello VM에서에서 hello 개별 디스크에 대 한 hello 디스크 크기를 표시합니다.

**코어**: hello CPU 코어의 수에 hello VM입니다.

**메모리 (MB)**: hello VM에 RAM hello 합니다.

**Nic**: hello hello VM에서 Nic 개수입니다.

**형식 부팅**: hello VM 유형의 부팅 합니다. BIOS 또는 EFI일 수 있습니다. 현재 Azure Site Recovery는 BIOS 부팅 유형만 지원합니다. EFI 부팅 형식의 모든 hello 가상 컴퓨터는 호환 되지 않는 Vm 워크시트에 나열 됩니다.

**OS 유형**: hello는 hello VM의 OS 유형이 있습니다. Windows, Linux 또는 기타일 수 있습니다.

## <a name="incompatible-vms"></a>호환되지 않는 VM

![호환되지 않는 VM에 대한 Excel 스프레드시트](./media/site-recovery-deployment-planner/incompatible-vms.png)

**VM 이름**: hello VM 이름 또는 보고서가 생성 될 때 VMListFile hello에 사용 되는 IP 주소입니다. 이 열 또한 연결 된 toohello vm hello Vmdk를 나열 합니다. 중복 이름 또는 IP 주소와 toodistinguish vCenter Vm에서 hello 이름 hello ESXi 호스트 이름이 포함 합니다. hello 나열된 ESXi 호스트는 hello 하나 hello VM 놓여진 위치 hello 도구 hello 기간을 프로 파일링 중에 발견 된 경우입니다.

**VM 호환성**: VM을 제공 하는 hello 이유 사이트 복구와 사용 하기 위해 호환 되지 않습니다 나타냅니다. hello 이유는 hello VM의 호환 되지 않는 각 디스크에 대 한 설명, 기반에 게시 된 [저장소 제한](https://aka.ms/azure-storage-scalbility-performance), hello 다음 중 하나일 수 있습니다.

* 디스크 크기가 4,095GB보다 큽니다. Azure Storage는 현재 4,095GB보다 큰 디스크 크기를 지원하지 않습니다.
* OS 디스크는 2,048GB보다 큽니다. Azure Storage는 현재 2,048GB보다 큰 OS 디스크 크기를 지원하지 않습니다.
* 부팅 유형은 EFI입니다. 현재 Azure Site Recovery는 BIOS 부팅 유형 가상 컴퓨터만 지원합니다.

* 총 VM 크기 (복제 + TFO) hello 지원 저장소 계정 크기 제한 (35 테라바이트)를 초과합니다. 이러한 비 호환성은 일반적으로 hello VM 내의 단일 디스크 hello 최대 지원 되는 Azure Site Recovery에 대해 또는 제한을 표준 저장소를 초과 하는 성능 특징에 있을 때 발생 합니다. 이러한 인스턴스는 hello 프리미엄 저장소 영역으로 hello VM을 푸시합니다. 그러나 여러 저장소 계정에서 최대 프리미엄 저장소 계정의 지원 되는 크기는 35 TB 하 고는 단일 VM을 보호 하는 hello는 보호할 수 없습니다. 또한 테스트 장애 조치는 보호 된 VM에서 실행 되 면 실행 hello에 참고 복제가 진행 되 고 동일한 저장소 계정입니다. 이 인스턴스에서 복제 tooprogress에 대 한 hello 디스크의 hello 크기 x 2를 설정 하 고 동시에 장애 조치 toosucceed를 테스트 합니다.
* 원본 IOPS가 디스크당 지원되는 저장소 IOPS 한도(5000)를 초과합니다.
* 원본 IOPS가 VM당 지원되는 저장소 IOPS 한도(80,000)를 초과합니다.
* 평균 데이터 변동을 hello 디스크에 대 한 평균 I/O 크기에 대 한 10mbps의 지원 되는 사이트 복구 데이터 변동을 제한을 초과 했습니다.
* 총 데이터 변동을 hello VM에서 모든 디스크에 VM 당 54 MBps의 hello 최대 지원 사이트 복구 데이터 변동을 제한을 초과합니다.
* 효과적인 평균 쓰기 IOPS 840 디스크에 대 한 지원 hello 사이트 복구 IOPS 제한을 초과 했습니다.
* 계산 된 스냅숏 저장소 10TB의 지원 되는 hello 스냅숏 저장소 용량 한도 초과합니다.

**증가 비율) (된 읽기/쓰기 IOPS**: hello hello 디스크에서 최대 작업 IOPS (기본값은 95 번째 백분위 수) hello 미래 증가 비율을 포함 하 여 (기본값은 30%). 총 읽기/쓰기 IOPS의 hello VM hello 참고가 아닙니다. 항상 hello VM의 개별 디스크의 읽기/쓰기 IOPS의 hello 합계 hello 최대 읽기/쓰기 IOPS의 hello VM은 해당 개별 디스크 hello 합계의 hello 최고 때문에 읽기/쓰기 IOPS의 hello 매분 중 프로 파일링 하는 기간.

**데이터 증가 비율) (있음 Mbps 단위로 변동**: hello 피크 변동률 hello 미래 증가 비율 (기본값 30%)을 포함 하 여 hello 디스크 (기본 95 번째 백분위 수)입니다. 해당 hello 참고 hello VM의 총 데이터 변동을 항상 hello VM의 개별 디스크의 데이터 변동이의 hello 합계 hello VM의 최대 데이터 변동을 hello은 해당 개별 디스크의 변동 hello 합계의 hello 최대 기간을 프로 파일링 하는 hello에 매 분 동안 합니다.

**디스크 수**: hello hello VM에 Vmdk의 총 수입니다.

**디스크 크기 (GB)**: hello hello VM의 모든 디스크의 총 설치 크기입니다. hello 도구는 또한 hello VM에서에서 hello 개별 디스크에 대 한 hello 디스크 크기를 표시합니다.

**코어**: hello CPU 코어의 수에 hello VM입니다.

**메모리 (MB)**: hello VM에서 hello 양의 RAM.

**Nic**: hello hello VM에서 Nic 개수입니다.

**형식 부팅**: hello VM 유형의 부팅 합니다. BIOS 또는 EFI일 수 있습니다. 현재 Azure Site Recovery는 BIOS 부팅 유형만 지원합니다. EFI 부팅 형식의 모든 hello 가상 컴퓨터는 호환 되지 않는 Vm 워크시트에 나열 됩니다.

**OS 유형**: hello는 hello VM의 OS 유형이 있습니다. Windows, Linux 또는 기타일 수 있습니다.


## <a name="site-recovery-limits"></a>사이트 복구 제한

**복제 저장소 대상** | **평균 원본 디스크 I/O 크기** |**평균 원본 디스크 데이터 변동** | **일일 총 원본 디스크 데이터 변동**
---|---|---|---
Standard Storage | 8KB | 2MBps | 디스크당 168GB
프리미엄 P10 디스크 | 8KB | 2MBps | 디스크당 168GB
프리미엄 P10 디스크 | 16KB | 4MBps | 디스크당 336GB
프리미엄 P10 디스크 | 32KB 이상 | 8MBps | 디스크당 672GB
프리미엄 P20 또는 P30 디스크 | 8KB  | 5MBps | 디스크당 421GB
프리미엄 P20 또는 P30 디스크 | 16KB 이상 |10MBps | 디스크당 842GB

여기서는 I/O가 30% 겹치고 있다고 가정하는 평균 숫자입니다. Site Recovery는 중첩 비율, 더 큰 쓰기 크기 및 실제 워크로드 I/O 동작에 따라 더 높은 처리량을 다룰 수 있습니다. hello 숫자 앞 가정 약 5 분의 일반적인 백로그 합니다. 즉, 데이터를 업로드한 후에 처리되며 5분 내에 복구 지점이 생성됩니다.

이러한 한도는 테스트를 기반으로 하지만 모든 가능한 응용 프로그램 I/O 조합을 다룰 수는 없습니다. 실제 결과는 응용 프로그램 I/O 조합에 따라 달라질 수 있습니다. 최상의 결과 배포 계획 한 후에 항상 권장 광범위 한 응용 프로그램 테스트 장애 조치 tooget hello true 성능 그림을 사용 하 여 테스트를 수행 합니다.

## <a name="updating-hello-deployment-planner"></a>Hello 배포 계획을 업데이트합니다.
tooupdate hello 배포 planner 다음 hello지 않습니다.

1. 최신 버전의 hello hello 다운로드 [Azure Site Recovery 배포 계획](https://aka.ms/asr-deployment-planner)합니다.

2. 원하는 toorun 복사 hello.zip 폴더 tooa 서버에 있습니다.

3. Hello.zip 폴더를 추출 합니다.

4. Hello 다음 중 하나를 수행 합니다.
 * Hello 최신 버전에는 프로 파일링 수정 프로그램이 포함 되어 있지 않습니다 hello 플래너의 현재 버전에서 진행에서 되어 프로 파일링 hello 프로 파일링 계속 합니다.
 * Hello에 대 한 최신 정보는 프로 파일링 수정이 없는 경우에 현재 사용 중인 버전에서 프로 파일링을 중지 하 고 hello hello 새 버전으로 프로 파일링 다시 시작 하는 것이 좋습니다.

  >[!NOTE]
  >
  >Hello 새 버전으로 패스 hello hello 도구가 추가 프로 파일 데이터에 있도록 동일한 출력 디렉터리 경로 프로 파일링을 시작할 때 hello 기존 파일입니다. 전체 프로 파일링된 데이터 집합이 됩니다 toogenerate hello 보고서를 사용 합니다. 사용 되지 않는 다른 출력 디렉터리를 전달 하 고 새 파일을 만드는 이전에 데이터 프로 파일링 하는 경우 toogenerate hello 보고서입니다.
  >
  >각 새 배포 계획은 hello.zip 파일의 누적 업데이트입니다. Toocopy hello 최신 파일 toohello 이전 폴더가 필요 하지 않습니다. 새 폴더를 만들어 사용할 수 있습니다.


## <a name="version-history"></a>버전 기록

### <a name="131"></a>1.3.1
업데이트: 2017년 7월 19일

다음과 같은 새로운 기능이 추가됩니다.

* 보고서 생성에서 1TB보다 큰 대용량 디스크에 대한 지원이 추가되었습니다. 이제 디스크 크기가 1TB (최대 4095 GB) 보다 큰 가상 컴퓨터에 대 한 배포 계획 tooplan 복제를 사용할 수 있습니다.
[Azure Site Recovery에서 대용량 디스크 지원(영문)](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)에 대해 자세히 알아보세요.


### <a name="13"></a>1.3
업데이트: 2017년 5월 9일

다음과 같은 새로운 기능이 추가됩니다.

* 보고서 생성에서 Managed Disk 지원이 추가되었습니다. hello 가상 컴퓨터 수가 배치할 tooa 단일 저장소 계정은 디스크 관리 하는 경우에 따라 계산 된 장애 조치/테스트 장애 조치에 대해 선택 된입니다.        


### <a name="12"></a>1.2
업데이트: 2017년 4월 7일

다음 수정 사항이 추가되었습니다.

* 추가 부팅 hello 가상 컴퓨터는 호환 또는 hello 보호에 대 한 호환 되지 않는 경우 각 가상 컴퓨터 toodetermine에 대 한 확인 (BIOS 또는 EFI)을 입력 합니다.
* 추가 된 OS hello 호환 Vm의에서 각 가상 컴퓨터에 대 한 정보 및 호환 되지 않는 Vm 워크시트를 입력합니다.
* hello GetThroughput 작업 hello 미국 정부 및 중국 Microsoft Azure 지역에서 이제 지원 됩니다.
* vCenter 및 ESXi 서버에 대한 몇 가지 추가 필수 요건이 추가되었습니다.
* 잘못 된 보고서가 생성 된 가져오기 로캘 설정을 영어 toonon에 설정 된 경우.


### <a name="11"></a>1.1
업데이트: 2017년 3월 9일

문제를 따르는 고정된 hello:

* hello 도구 hello vCenter에는 두 개 또는 다양 한 ESXi 호스트 간에 동일한 이름이 나 IP 주소를 환영 하는 많은 수의 Vm으로 하는 경우 Vm을 프로 파일링 수 없습니다.
* 복사 및 검색 hello 호환 Vm과 호환 되지 않는 Vm 워크시트에 대 한 비활성화 됩니다.

### <a name="10"></a>1.0
업데이트: 2017년 2월 23일

Azure 사이트 복구 배포 계획 공개 미리 보기 1.0 hello 다음과 같은 알려진 문제 (toobe 향후 업데이트에서 해결)에 있습니다.

* hello 도구는 Azure에 하이퍼 V 배포에 대해 Azure에 VMware 시나리오에 대해서만 작동합니다. Azure에 하이퍼 V 시나리오에 대 한 hello를 사용 하 여 [Hyper-v 용량 계획 도구](./site-recovery-capacity-planning-for-hyper-v-replication.md)합니다.
* hello GetThroughput 작업 hello 미국 정부 및 중국 Microsoft Azure 지역에서 지원 되지 않습니다.
* hello 도구 hello vCenter 서버에는 두 개 또는 다양 한 ESXi 호스트 간에 동일한 이름이 나 IP 주소를 환영 하는 많은 수의 Vm으로 하는 경우 Vm을 프로 파일링 수 없습니다. 이 버전에서는 hello 도구 중복 VM 이름 또는 IP 주소 VMListFile hello에 대 한 프로 파일링을 건너뜁니다. vCenter 서버 hello 대신 ESXi 호스트를 사용 하 여 한 tooprofile hello Vm hello 방법은 참조 하십시오입니다. 각 ESXi 호스트에 대해 인스턴스 하나만 실행해야 합니다.
