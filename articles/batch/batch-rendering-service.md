---
title: "hello 클라우드에서 aaaUse hello Azure 일괄 처리 렌더링 서비스 toorender | Microsoft Docs"
description: "Maya에서 직접 사용량 기준 과금으로 Azure 가상 컴퓨터의 작업을 렌더링합니다."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Hello 렌더링 하는 일괄 처리 서비스 시작

hello Azure 일괄 처리 렌더링 서비스는 기본 사용 사용량 기준 과금 별로 클라우드 규모 렌더링 기능을 제공합니다. hello 렌더링 하는 일괄 처리 서비스는 작업 일정 및 큐 관리 실패 및 다시 시도 시간 및 렌더링 작업에 대 한 자동 크기 조정 처리합니다. hello 렌더링 하는 일괄 처리 서비스 지원 3ds Autodesk 마 야 Max 및 Arnold 곧 제공 하는 다른 응용 프로그램에 대 한 지원. 일괄 처리를 마 야 2017에 대 한 플러그 인 hello를 사용 하면 쉽게 toostart 렌더링 작업에 Azure 바탕 화면에서 오른쪽입니다. 

## <a name="supported-applications"></a>지원되는 응용 프로그램

hello 렌더링 하는 일괄 처리 서비스는 현재 응용 프로그램을 다음 hello를 지원 합니다.

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>필수 조건

toouse hello 렌더링 하는 일괄 처리 서비스를 해야합니다.

- [Azure 계정](https://azure.microsoft.com/free/) 
- **Azure Batch 계정.** Hello Azure 포털에서에서 일괄 처리 계정 만들기에 대 한 지침을 참조 하십시오. [hello Azure 포털 일괄 처리 계정을 만들고](batch-account-create-portal.md)합니다.
- **Azure Storage 계정.** hello 자산 렌더링 작업에 사용 되는 Azure 저장소에 저장 됩니다. Batch 계정을 설정할 때 자동으로 저장소 계정을 만들 수 있습니다. 기존 저장소 계정을 사용할 수도 있습니다. 저장소 계정에 대해 자세히 toolearn 참조 [toocreate, 관리 또는 hello Azure 포털에서에서 저장소 계정을 삭제 방법을](https://docs.microsoft.com/azure/storage/storage-create-storage-account)합니다.

toouse hello 일괄 처리 해야 마 야에 대 한 플러그 인:

- **Maya 2017**
- **Arnold for Maya**

Hello를 사용할 수도 있습니다 [Azure 포털](https://portal.azure.com) 마 야, 3ds로 미리 구성 되어 있는 가상 컴퓨터의 toocreate 풀 Max 및 Arnold 합니다. Hello 포털 toomonitor 작업 사용 수 있으며 응용 프로그램 로그를 다운로드 하 고 RDP 또는 SSH를 사용 하 여 tooindividual Vm에 원격으로 연결 하 여 실패 한 작업을 진단할 수 있습니다.

## <a name="basic-batch-concepts"></a>기본 Batch 개념

Hello 렌더링 하는 일괄 처리 서비스 사용을 시작 하기 전에 계산 노드, 풀 및 작업을 비롯 한 몇 가지 일괄 처리 개념을 이해 하는 것이 도움이 toobe 됩니다. 일반적으로 Azure 일괄 처리에 대 한 자세한 참조 toolearn [일괄 처리를 사용 하 여 기본적으로 병렬 작업 실행](batch-technical-overview.md)합니다.

### <a name="pools"></a>풀

Batch는 렌더링처럼 계산 집약적인 작업을 **계산 노드** **풀**에서 실행하기 위한 플랫폼 서비스입니다. 풀의 각 계산 노드는 Linux 또는 Windows에서 실행 중인 Azure VM(가상 컴퓨터)입니다. 

계산 노드 및 일괄 처리 풀에 대 한 자세한 내용은 참조 hello [풀](batch-api-basics.md#pool) 및 [계산 노드](batch-api-basics.md#compute-node) 섹션 [개발 대규모 병렬 일괄 처리를 사용 하 여 솔루션을 계산](batch-api-basics.md)합니다.

### <a name="jobs"></a>작업

일괄 처리 **작업** hello에서 실행 되는 작업 컬렉션의에서 계산 노드는 풀은 합니다. 렌더링 작업을 제출 하면 일괄 처리 작업으로 hello 작업을 나누고 hello 풀 toorun hello 작업 toohello 계산 노드를 배포 합니다.

일괄 처리 작업에 대 한 자세한 내용은 참조 hello [작업](batch-api-basics.md#job) 섹션 [개발 대규모 병렬 일괄 처리를 사용 하 여 솔루션을 계산](batch-api-basics.md)합니다.

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>사용 하 여 hello 일괄 처리를 마 야 toosubmit 렌더링 작업에 대 한 플러그 인

일괄 처리를 마 야에 대 한 플러그 인 hello로 작업 toohello 마 야에서 직접 렌더링 하는 일괄 처리 서비스를 제출할 수 있습니다. 다음 섹션 hello tooconfigure이 hello hello 플러그 인에서 작업 하 고 전송 하는 것 하는 방법을 설명 합니다. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Hello 일괄 처리를 마 야에 플러그 인을 로드 합니다.

hello 플러그 인 일괄 처리에서 사용할 수는 [GitHub](https://github.com/Azure/azure-batch-maya/releases)합니다. 사용자가 선택한 hello 보관 tooa 디렉터리로 압축을 풉니다. Hello에서 직접 hello 플러그 인을 로드할 수 있습니다 *azure_batch_maya* 디렉터리입니다.

tooload hello 마 야에 플러그 인:

1. Maya를 실행합니다.
2. **Window** > **설정/기본 설정** > **플러그 인 관리자**를 엽니다.
3. **찾아보기**를 클릭합니다.
4. Tooand 선택 이동 *azure_batch_maya/plug-in/AzureBatch.py*합니다.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>액세스 tooyour 일괄 처리 및 저장소 계정 인증

toouse hello 플러그 인, Azure 일괄 처리 및 Azure 저장소 계정 키를 사용 하 여 tooauthenticate가 필요 합니다. tooretrieve 계정 키:

1. 디스플레이 hello 마 야에서 플러그 인 및 선택 hello **Config** 탭 합니다.
2. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.
3. 선택 **일괄 처리 계정** hello 왼쪽 메뉴에서 합니다. 필요한 경우 **추가 서비스**를 클릭하고 _Batch_로 필터링합니다.
4. Hello 목록에서 원하는 hello 일괄 처리 계정을 찾습니다.
5. 선택 hello **키** 메뉴 항목 toodisplay 계정 이름, 계정 URL 및 액세스 키:
    - Hello hello 일괄 처리 계정 URL을 붙여 **서비스** 필드 hello 플러그 인 일괄 처리에에서 있습니다.
    - Hello에 붙여넣기 hello 계정 이름을 **일괄 처리 계정** 필드입니다.
    - Hello에 hello 기본 계정 키 붙여넣기 **일괄 처리 키** 필드입니다.
7. Hello 왼쪽 메뉴에서 저장소 계정을 선택 합니다. 필요한 경우 **추가 서비스**를 클릭하고 _Storage_로 필터링합니다.
8. Hello 목록에서 원하는 hello 저장소 계정을 찾습니다.
9. 선택 hello **선택 키** 메뉴 항목 toodisplay hello 저장소 계정 이름 및 키입니다.
    - Hello에 붙여넣기 hello 저장소 계정 이름을 **저장소 계정** 필드 hello 플러그 인 일괄 처리에에서 있습니다.
    - Hello에 hello 기본 계정 키 붙여넣기 **저장소 키** 필드입니다.
10. 클릭 **Authenticate** 플러그 인 hello tooensure 두 계정 모두에 액세스할 수 있습니다.

Hello 플러그 인 집합 상태 필드를 너무 hello 성공적으로 인증 되 면**인증 된**: 

![Batch 및 Storage 계정 인증](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>렌더링 작업에 대한 풀 구성

Batch 및 Storage 계정을 인증한 후에는 렌더링 작업에 사용할 풀을 설정합니다. 플러그 인 hello 세션 간에 선택 항목을 저장합니다. 기본 구성을 설정한 후 toomodify 필요 하지는 않습니다 것 변경 하지 않는 한 합니다.

hello 다음 섹션에서는 과정을 단계별로 hello에서 사용할 수 있는 hello 사용 가능한 옵션 **전송** 탭:

#### <a name="specify-a-new-or-existing-pool"></a>새 풀 또는 기존 풀 지정

toorun hello 렌더링 작업 (job)을 선택 하는 hello에 풀 toospecify **전송** 탭 합니다. 이 탭은 풀을 만들거나 기존 풀을 선택하는 옵션을 제공합니다.

- 할 수 있습니다 **자동이이 작업에 대 한 풀 프로 비전** (hello 기본 옵션). 이 옵션을 선택 하면 일괄 처리 hello 풀 hello 현재 작업에 대 한 단독으로 만들고 자동으로 삭제 hello 풀 hello 렌더링 작업은 완료 합니다. 단일 렌더링 작업 toocomplete 있는 경우이 옵션을 사용 하는이 가장 좋습니다.
- **기존의 영구 풀을 다시 사용할 수 있습니다**. 기존 풀이 유휴 상태를 설정한 경우 hello 드롭다운에서 선택 하 여 실행 중인 hello 렌더링 작업에 대 한 해당 풀을 지정할 수 있습니다. Hello 필요한 시간 tooprovision hello 풀을 저장 영구 기존 풀을 다시 사용 합니다.  
- **새 영구 풀을 만들 수 있습니다**. 이 옵션을 선택 하면 hello 작업을 실행 하기 위한 새 풀을 만듭니다. 이후의 작업을 쉽게 사용할 수 있도록 hello 작업이 완료 되 면 hello 풀을 삭제 되지 않습니다. 렌더링 작업 연속 필요 toorun 있는 경우이 옵션을 선택 합니다. 후속 작업에서 선택할 수 있습니다 **영구 기존 풀을 다시 사용할** toouse hello hello 첫 번째 작업에 대해 만든 영구 풀입니다.

![풀, OS 이미지, VM 크기 및 라이선스 지정](./media/batch-rendering-service/submit.png)

Azure Vm에 대 한 비용 발생 하는 방법에 대 한 자세한 내용은 참조 hello [Linux 가격 정보 FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) 및 [Windows 가격 정보 FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq)합니다.

#### <a name="specify-hello-os-image-tooprovision"></a>Hello OS 이미지 tooprovision 지정

Hello hello 풀에 hello 유형의 OS 이미지 toouse tooprovision 계산 노드를 지정할 수 있습니다 **Env** (환경)를 탭 합니다. 현재 일괄 처리 hello 다음 작업을 렌더링 하기 위한 이미지 옵션을 지원 합니다.

|운영 체제  |이미지  |
|---------|---------|
|Linux     |Batch CentOS Preview |
|Windows     |Batch Windows Preview |

#### <a name="choose-a-vm-size"></a>VM 크기 선택

Hello에 hello v M 크기를 지정할 수 있습니다 **Env** 탭 합니다. 사용 가능한 VM 크기에 대한 자세한 내용은 [Azure에서 Linux VM 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) 및 [Azure에서 Windows VM 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)를 참조하세요. 

![Hello Env 탭 hello VM OS 이미지와 크기를 지정 합니다.](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>라이선스 옵션 지정

Hello toouse를 원하는 hello 라이선스를 지정할 수 있습니다 **Env** 탭 합니다. 옵션은 다음과 같습니다.

- **Maya**, 기본적으로 활성화됩니다.
- **Arnold**, Arnold 마 야에 hello 활성 렌더링 엔진으로 검색 되 면 활성화 되어 있습니다.

 사용자 고유 라이선스를 사용 하 여 toorender 원한다 면 hello 적절 한 환경 변수 toohello 테이블을 추가 하 여 라이선스 시작점과 끝점을 구성할 수 있습니다. 이렇게 하면 있는지 toodeselect hello 기본 라이선스 옵션을 수 있습니다.

> [!IMPORTANT]
> 요금 지불 hello 라이선스 사용 Vm hello 풀에서 실행 되는 동안 Vm hello 렌더링을 위해 현재 사용 되지 않는 경우에 합니다. tooavoid 추가 요금이 이동 toohello **풀** 탭 및 크기 조정 hello 풀 too0 노드 준비 toorun가 아닌 경우 다른 렌더링 작업입니다. 
>
>

#### <a name="manage-persistent-pools"></a>영구 풀 관리

Hello에 영구 기존 풀을 관리할 수 있습니다 **풀** 탭 합니다. Hello 목록에서 풀을 선택 하면 hello hello 풀의 현재 상태가 표시 됩니다.

Hello에서 **풀** 탭 hello 풀을 삭제 하 고 hello 번호 hello 풀에 있는 Vm의 크기를 조정할 수도 있습니다. 작업 사이는 비용이 발생 하는 풀 too0 노드 tooavoid 크기를 조정할 수 있습니다.

![풀 보기, 크기 조정 및 삭제](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>제출할 수 있도록 렌더링 작업 구성

Hello 렌더링 작업을 실행 하는 hello 풀에 대 한 hello 매개 변수를 지정 하면 hello 작업 자체를 구성 합니다. 

#### <a name="specify-scene-parameters"></a>장면 매개 변수 지정

hello 플러그 인 일괄 처리를 마 야에서 현재 사용 중인 어떤 렌더링 엔진을 검색 한 적절 한 표시 hello 렌더링 hello에 대 한 설정 **전송** 탭 합니다. 이러한 설정에는 hello 시작 프레임, 끝 프레임, 출력 접두사 및 프레임 단계가 포함 됩니다. Hello 플러그 인에서 서로 다른 설정을 지정 하 여 hello 장면 파일 렌더링 설정을 재정의할 수 있습니다. 변경 내용은 toohello 플러그 인 설정 되지 않으므로 지속형된 백 toohello 장면 파일 렌더링 설정을 tooreupload hello 장면 파일 필요 없이 작업에서 작업 별로 변경을 수행할 수 있습니다.

hello 플러그 인 경고 hello 마 야에서 선택한 엔진을 렌더링 하는 경우 사용자가 지원 되지 않습니다.

플러그 인 hello 열려 있는 동안 새 장면을 로드 하면 클릭 hello **새로 고침** 단추 toomake 있는지 hello 설정이 업데이트 됩니다.

#### <a name="resolve-asset-paths"></a>자산 경로 확인

Hello 플러그 인을 로드 하는 경우 hello 장면 파일에 대 한 외부 파일 참조를 검색 합니다. 이러한 참조는 hello에 표시 되는 **자산** 탭 합니다. 참조 경로 확인할 수 없는 경우 hello 플러그 인 포함 한 몇 가지 기본 위치에서 toolocate hello 파일을 시도 합니다.

- hello 장면 파일의 hello 위치 
- hello 현재 프로젝트의 _sourceimages_ 디렉터리
- hello 현재 작업 디렉터리입니다. 

Hello 자산 여전히을 찾을 수 없는 경우에 경고 아이콘이 표시 됩니다.

![누락된 자산이 경고 아이콘과 함께 표시됨](./media/batch-rendering-service/missing_assets.png)

해결 되지 않은 파일 참조의 hello 위치를 알고 있는 경우 경고 메시지가 표시 tooadd 검색 경로 아이콘 toobe hello 클릭 수 있습니다. hello 다음 플러그 인이 검색 경로 tooattempt tooresolve 누락 된 모든 자산을 사용합니다. 추가 검색 경로를 원하는 만큼 추가할 수 있습니다.

참조가 확인되면 녹색 등 아이콘이 표시됩니다.

![확인된 자산에 녹색 등 아이콘이 표시됨](./media/batch-rendering-service/found_assets.png)

장면이 다른 파일이 필요한 경우 플러그 인에 해당 hello가 검색 되지 않은 추가 파일 또는 디렉터리를 추가할 수 있습니다. 사용 하 여 hello **파일 추가** 및 **디렉터리 추가** 단추입니다. 플러그 인 hello 열려 있는 동안 새 장면을 로드 하면 수 있는지 tooclick **새로 고침** tooupdate hello 장면 참조 합니다.

#### <a name="upload-assets-tooan-asset-project"></a>자산 tooan 자산 프로젝트 업로드

참조 된 hello에 표시 되는 파일을 제출할 때 렌더링 작업 hello **자산** 탭 자동으로 업로드 된 tooAzure 자산 프로젝트로 저장 됩니다. 또한 hello를 사용 하 여 hello 자산 파일 렌더링 작업을 독립적으로 업로드할 수 있습니다 **업로드** hello 단추 **자산** hello에 탭 hello 자산 프로젝트 이름이 지정 된 **프로젝트**필드를 현재 마 야 프로젝트 hello 기본적으로 지정 합니다. 자산 파일 업로드 되 면 hello 로컬 파일 구조가 보존 됩니다. 

자산이 업로드되면 임의의 수의 렌더링 작업에서 자산을 참조할 수 있습니다. 모든 업로드 된 자산은 hello 자산 프로젝트를 참조 하는 사용 가능한 tooany 작업 hello 장면에 포함 된 여부입니다. hello에 hello 이름 변경, 다음 작업에서 참조 하는 toochange hello 자산 프로젝트용 **프로젝트** 필드 hello에 **자산** 탭 합니다. 참조 된 파일을 업로드 tooexclude 있으면 선택을 취소 hello 목록 옆의 녹색 hello 단추를 사용 하 여 합니다.

#### <a name="submit-and-monitor-hello-render-job"></a>모니터 hello 렌더링 작업 및 제출

Hello 플러그 인에 hello 렌더링 작업을 구성 하 고 나면 클릭 hello **작업 제출** hello 단추 **전송** toosubmit hello 작업 tooBatch 탭:

![Hello 렌더링 작업을 제출](./media/batch-rendering-service/submit_job.png)

Hello에서 진행 중인 작업을 모니터링할 수 있습니다 **작업** hello 플러그 인에 탭 합니다. Hello 목록 toodisplay hello 작업의 현재 상태 hello에서에서 작업을 선택 합니다. 이 탭 toocancel를 사용 하 고 삭제 작업으로 toodownload hello 출력 및 로그를 렌더링 수도 있습니다. 

toodownload 출력 수정 hello **출력** 필드 tooset hello 원하는 대상 디렉터리입니다. Hello 기어 아이콘 toostart hello 작업을 감시 하 고 닫힘으로 출력을 다운로드 하는 백그라운드 프로세스를 클릭 합니다. 

![작업 상태 확인 및 출력 다운로드](./media/batch-rendering-service/jobs.png)

Hello 다운로드 프로세스를 방해 하지 않고 마 야를 닫을 수 있습니다.

## <a name="next-steps"></a>다음 단계

일괄 처리에 대해 자세히 toolearn 참조 [일괄 처리를 사용 하 여 기본적으로 병렬 작업 실행](batch-technical-overview.md)합니다.
