---
title: "aaaRemove 서버 및 보호 사용 안 함 | Microsoft Docs"
description: "이 문서에서는 어떻게 toounregister 서버에서 사이트 복구 자격 증명 모음 및 toodisable 보호 가상 컴퓨터 및 물리적 서버에 대 한 설명입니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>서버 제거 및 보호 사용 안 함

Azure Site Recovery 서비스 hello tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략에 기여합니다. hello 서비스에는 복제, 장애 조치 및 복구 가상 컴퓨터와 물리적 서버와 조정합니다. 복제 된 tooAzure 또는 tooa 보조 온-프레미스 데이터 센터 컴퓨터 수 있습니다. 빠른 개요를 알아보려면 [Azure Site Recovery란?](site-recovery-overview.md)

이 문서에서는 복구 서비스에서 toounregister 서버 hello Azure 포털에서에서 자격 증명 모음에 어떻게 및 toodisable 보호 컴퓨터에 대 한 Site Recovery에서 보호 하는 방법을 설명 합니다.

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="unregister-a-connected-configuration-server"></a>연결된 구성 서버 등록 취소

VMware Vm 또는 실제 서버 tooAzure Windows/Linux를 복제 하는 경우 연결 된 구성 서버에서 자격 증명 모음을 다음과 같이 등록 취소할 수 있습니다.

1. 컴퓨터 보호 사용 안 함. **보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.
2. 모든 정책 연결 해제. **사이트 복구 인프라** > **물리적 컴퓨터 및 VMWare에 대 한** > **복제 정책**, hello를 두 번 클릭 연결 된 정책입니다. Hello 구성 서버를 마우스 오른쪽 단추로 클릭 > **연관 해제**합니다.
3. 추가 온-프레미스 프로세스 또는 마스터 대상 서버를 제거합니다. **사이트 복구 인프라** > **물리적 컴퓨터 및 VMWare에 대 한** > **구성 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 > **삭제**합니다.
4. Hello 구성 서버를 삭제 합니다.
5. Hello 마스터 대상 서버에서 실행 되는 hello 모바일 서비스를 수동으로 제거 (이 됩니다는 별도 서버 또는 hello 구성 서버에서 실행).
6. 추가 프로세스 서버를 제거합니다.
7. Hello 구성 서버를 제거 합니다.
8. Hello 구성 서버에서 hello Site Recovery에 의해 설치 된 MySQL 인스턴스를 제거 합니다.
9. Hello 구성 서버 hello 레지스트리에 hello 키 삭제 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``합니다.

## <a name="unregister-a-unconnected-configuration-server"></a>연결되지 않은 구성 서버 등록 취소

VMware Vm 또는 실제 서버 tooAzure Windows/Linux를 복제 하는 경우는 연결 되지 않은 구성 서버에서 자격 증명 모음을 다음과 같이 등록 취소할 수 있습니다.

1. 컴퓨터 보호 사용 안 함. **보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다. 선택 **hello 컴퓨터 관리 중지**합니다.
2. 추가 온-프레미스 프로세스 또는 마스터 대상 서버를 제거합니다. **사이트 복구 인프라** > **물리적 컴퓨터 및 VMWare에 대 한** > **구성 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 > **삭제**합니다.
3. Hello 구성 서버를 삭제 합니다.
4. Hello 마스터 대상 서버에서 실행 되는 hello 모바일 서비스를 수동으로 제거 (이 됩니다는 별도 서버 또는 hello 구성 서버에서 실행).
5. 추가 프로세스 서버를 제거합니다.
6. Hello 구성 서버를 제거 합니다.
7. Hello 구성 서버에서 hello Site Recovery에 의해 설치 된 MySQL 인스턴스를 제거 합니다.
8. Hello 구성 서버 hello 레지스트리에 hello 키 삭제 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``합니다.

## <a name="unregister-a-connected-vmm-server"></a>연결된 VMM 서버 등록 취소

모범 사례로, tooAzure에 연결한 경우 hello VMM 서버를 등록 취소 하는 것이 좋습니다. 이렇게 하면 설정 hello VMM 서버에 (및 클라우드와 쌍을 이루는 다른 VMM 서버에서) 제대로 정리 됩니다. 연결에 영구적인 문제가 있는 경우에만 연결되지 않은 서버를 제거해야 합니다. Hello VMM 서버에 연결 되지 않아 경우 해야 toomanually 설정을 스크립트 tooclean를 실행 합니다.

1. Vm 클라우드에 hello tooremove VMM 서버에서 복제를 중지 합니다.
2. Hello toodelete VMM 서버에 클라우드 사용 되는 모든 네트워크 매핑이 삭제 합니다. **사이트 복구 인프라** > **System Center VMM** > **네트워크 매핑을**, hello 네트워크 매핑을 마우스 오른쪽 단추로 클릭 >  **삭제**합니다.
3. Hello tooremove VMM 서버에 클라우드가 복제 정책 연결이 해제 됩니다.  **사이트 복구 인프라** > **System Center VMM** >  **복제 정책**, 연결 된 hello 정책을 두 번 클릭 합니다. Hello 클라우드를 마우스 오른쪽 단추로 클릭 > **연관 해제**합니다.
4. Hello VMM 서버 또는 현재 VMM 노드를 삭제 합니다. **사이트 복구 인프라** > **System Center VMM** > **VMM 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 >  **삭제**합니다.
5. Hello 공급자 hello VMM 서버에서 수동으로 제거 합니다. 클러스터가 있는 경우 모든 노드에서 제거합니다.
6. TooAzure를 복제 하는 경우 삭제 하는 hello 클라우드에서 Hyper-v 호스트에서 수동으로 hello Microsoft 복구 서비스 에이전트를 제거 합니다.



### <a name="unregister-an-unconnected-vmm-server"></a>연결되지 않은 VMM 서버 등록 취소

1. Vm 클라우드에 hello tooremove VMM 서버에서 복제를 중지 합니다.
2. 원하는 toodelete hello VMM 서버의 클라우드에 사용 되는 모든 네트워크 매핑이 삭제 합니다. **사이트 복구 인프라** > **System Center VMM** > **네트워크 매핑을**, hello 네트워크 매핑을 마우스 오른쪽 단추로 클릭 >  **삭제**합니다.
3. Note hello ID hello VMM 서버입니다.
4. Hello tooremove VMM 서버에 클라우드가 복제 정책 연결이 해제 됩니다.  **사이트 복구 인프라** > **System Center VMM** >  **복제 정책**, 연결 된 hello 정책을 두 번 클릭 합니다. Hello 클라우드를 마우스 오른쪽 단추로 클릭 > **연관 해제**합니다.
5. VMM 서버 hello 또는 액티브 노드를 삭제 합니다. **사이트 복구 인프라** > **System Center VMM** > **VMM 서버**를 마우스 오른쪽 단추로 클릭 hello 서버 >  **삭제**합니다.
6. 다운로드 및 실행 hello [정리 스크립트](http://aka.ms/asr-cleanup-script-vmm) hello VMM 서버에 있습니다. Hello로 PowerShell을 열고 **관리자 권한으로 실행** toochange hello 실행 정책을 hello 기본 (LocalMachine) 범위에 대 한 옵션입니다. Hello 스크립트에 hello hello tooremove VMM 서버 ID를 지정 합니다. hello 스크립트 등록 및 클라우드 페어링 hello 서버에서 정보를 제거 합니다.
5. Hello tooremove VMM 서버에 클라우드가 함께 사용 되는 클라우드를 포함 하는 다른 VMM 서버 hello 정리 스크립트를 실행 합니다.
6. 모든 다른 패시브 노드에서 VMM 클러스터 hello 공급자가 설치 되어 있는 hello 정리 스크립트를 실행 합니다.
7. Hello 공급자 hello VMM 서버에서 수동으로 제거 합니다. 클러스터가 있는 경우 모든 노드에서 제거합니다.
8. TooAzure 복제 하면을 제거할 수 있으면 hello Microsoft 복구 서비스 에이전트 hello 삭제 클라우드에서 Hyper-v 호스트에서 합니다.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Hyper-V 사이트에서 Hyper-V 호스트 등록 취소

VMM에 의해 관리되지 않는 Hyper-V 호스트가 Hyper-V 사이트로 수집됩니다. 다음과 같이 Hyper-V 사이트에서 호스트를 제거합니다.

1. Hello 호스트에 있는 Hyper-v Vm에 대 한 복제를 사용 하지 않도록 설정 합니다.
2. Hello 하이퍼-V 사이트에 대 한 정책 연결이 해제 됩니다. **사이트 복구 인프라** > **하이퍼-V 사이트에 대 한** >  **복제 정책**, 연결 된 hello 정책을 두 번 클릭 합니다. 마우스 오른쪽 단추로 클릭 hello 사이트 > **연관 해제**합니다.
3. Hyper-V 호스트를 삭제합니다. **사이트 복구 인프라** > **System Center VMM** > **Hyper-v 호스트**를 마우스 오른쪽 단추로 클릭 hello 서버 >  **삭제**합니다.
4. 모든 호스트에서 제거 된 후 hello 하이퍼-V 사이트를 삭제 합니다. **사이트 복구 인프라** > **System Center VMM** > **Hyper-v 사이트**를 마우스 오른쪽 단추로 클릭 hello 사이트 >  **삭제**합니다.
5. 제거 된 각 Hyper-v 호스트에서 스크립트를 다음 hello를 실행 합니다. hello 스크립트 hello 서버의 설정을 정리 하 고 hello 자격 증명 모음에서 등록을 취소 합니다.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>VMware VM 또는 물리적 서버에 대한 보호를 사용 안 함

1. **보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.
2. **컴퓨터 제거**에서 다음 중 하나를 선택합니다.
    - **(권장) hello 컴퓨터에 대 한 보호 사용 안 함**합니다. 이 옵션 toostop hello 컴퓨터에 복제를 사용 합니다. Site Recovery 설정은 자동으로 정리됩니다. 이 옵션의 경우 다음 hello에만 나타납니다.
        - **Hello VM 볼륨 크기를 조정할**-컴퓨터 위험 상태 전환 되는 볼륨 hello 가상 크기를 조정 합니다. Azure에서 복구 지점을 유지 하는 동안이 옵션 toodisables 보호를 선택 합니다. Hello 컴퓨터에 대 한 보호를 다시 사용 하도록 설정 하면 크기가 조정 hello 볼륨에 대 한 hello 데이터 전송된 tooAzure 됩니다.
        - **장애 조치를 최근에 실행 한**-장애 조치 tootest 환경을 실행 한 후이 옵션 toostart 온-프레미스 컴퓨터를 다시 보호를 선택 합니다. 각 가상 컴퓨터를 비활성화 한 다음 있습니다 tooenable 보호를 다시 합니다. 이 설정을 사용 하지 않도록 설정 hello 컴퓨터 Azure의 hello 복제 가상 컴퓨터에 영향을 주지 않습니다. Hello 컴퓨터에서 hello 모바일 서비스를 제거 하지 마세요.
    - **Hello 컴퓨터 관리 중지**합니다. 이 옵션을 선택 하는 경우 hello 컴퓨터만 hello 자격 증명 모음에서 제거 됩니다. Hello 컴퓨터에 대 한 온-프레미스 보호 설정의 영향을 받지 않습니다. hello 컴퓨터와 hello Azure 구독에서에서 tooremove hello 컴퓨터, tooremove 설정이 hello 모바일 서비스를 제거 하 여 tooclean hello 설정이 필요 하면 합니다.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>VMM 클라우드에서 Hyper-V VM에 대한 보호 사용 안 함

1. **보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.
2. **컴퓨터 제거**에서 다음 중 하나를 선택합니다.

    - **(권장) hello 컴퓨터에 대 한 보호 사용 안 함**합니다. 이 옵션 toostop hello 컴퓨터에 복제를 사용 합니다. Site Recovery 설정은 자동으로 정리됩니다.
    - **Hello 컴퓨터 관리 중지**합니다. 이 옵션을 선택 하는 경우 hello 컴퓨터만 hello 자격 증명 모음에서 제거 됩니다. Hello 컴퓨터에 대 한 온-프레미스 보호 설정의 영향을 받지 않습니다. hello 컴퓨터와 hello Azure 구독에서에서 tooremove hello 컴퓨터, tooremove 설정이 필요한 tooclean hello 설정을 수동으로 아래 hello 지침을 사용 하 여 합니다. 참고 toodelete hello 가상 컴퓨터와 해당 하드 디스크를 선택한 경우 이러한 것에서 꺼내야 합니다 hello 대상 위치입니다.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>복제 tooa 보조 VMM 사이트-보호 설정 정리

선택한 경우 **hello 컴퓨터 관리 중지** hello 주 가상 컴퓨터에 대 한 hello 설정을 hello 주 서버 tooclean에서이 스크립트 실행 tooa 보조 사이트를 복제 해야 하 고 있습니다. Hello VMM 콘솔에서 hello PowerShell 단추 tooopen hello VMM PowerShell 콘솔을 클릭 합니다. SQLVM1 가상 컴퓨터의 hello 이름으로 대체 합니다.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Hello 보조 VMM 서버에서이 스크립트 tooclean hello 보조 가상 컴퓨터에 대 한 hello 설정을 실행합니다.

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. 보조 VMM 서버 hello hello Hyper-v 호스트 서버의 가상 컴퓨터 hello hello 보조 VM 가져옵니다 검색 되도록 다시 hello VMM 콘솔에서 새로 고칩니다.
4. 단계는 hello hello 복제 설정을 hello VMM 서버에서 문제를 해결 합니다. Hello 가상 컴퓨터를 다음 hello 실행에 대 한 toostop 복제 하려는 경우 스크립트 안녕하세요 기본 및 보조 Vm입니다. SQLVM1 가상 컴퓨터의 hello 이름으로 대체 합니다.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>보호 설정-복제 tooAzure 정리

1. 선택한 경우 **hello 컴퓨터 관리 중지** tooAzure 복제, hello VMM 콘솔에서 PowerShell을 사용 하 여 hello 원본 VMM 서버에서이 스크립트를 실행 하 고 있습니다.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. 단계는 hello hello VMM 서버의 복제 설정을 hello 선택을 취소 합니다. 이 스크립트를 실행 하는 hello Hyper-v 호스트 서버에서 실행 하는 hello 가상 컴퓨터에 대 한 toostop 복제 합니다. SQLVM1 hello Hyper-v 호스트 서버 hello 이름 가진 가상 컴퓨터 및 host01.contoso.com hello 이름을 대체 합니다.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Hyper-V 사이트에서 Hyper-V VM에 대한 보호 사용 안 함

VMM 서버 없이 tooAzure Hyper-v Vm을 복제 하는 경우이 절차를 사용 합니다.

1. **보호 된 항목** > **복제 항목**를 마우스 오른쪽 단추로 클릭 hello 컴퓨터 > **삭제**합니다.
2. **컴퓨터 제거**, hello 다음 옵션을 선택할 수 있습니다.

   - **(권장) hello 컴퓨터에 대 한 보호 사용 안 함**합니다. 이 옵션 toostop hello 컴퓨터에 복제를 사용 합니다. Site Recovery 설정은 자동으로 정리됩니다.
   - **Hello 컴퓨터 관리 중지**합니다. 이 옵션을 선택 하는 경우 hello 컴퓨터만 hello 자격 증명 모음에서 제거 됩니다. Hello 컴퓨터에 대 한 온-프레미스 보호 설정의 영향을 받지 않습니다. hello 컴퓨터와 hello Azure 구독에서에서 tooremove hello 가상 컴퓨터, tooremove 설정이 필요한 tooclean hello 설정을 수동으로 합니다. Toodelete hello 가상 컴퓨터와 해당 하드 디스크를 선택 하는 경우 hello 대상 위치에서 제거 됩니다.
3. 선택한 경우 **hello 컴퓨터 관리 중지**,이 hello 원본 Hyper-v 호스트 서버에서 스크립트, tooremove hello 가상 컴퓨터 복제를 실행 합니다. SQLVM1 가상 컴퓨터의 hello 이름으로 대체 합니다.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
