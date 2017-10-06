---
title: "Azure의 이벤트에 대 한 Windows Vm aaaScheduled | Microsoft Docs"
description: "예약 된 이벤트에 대 한 hello Azure 메타 데이터 서비스를 사용 하 여 Windows 가상 컴퓨터에 있습니다."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a>Azure 메타데이터 서비스: Windows VM에 예정된 이벤트(미리 보기)

> [!NOTE] 
> 미리 보기 toohello 사용 약관을 동의 하는 hello 조건에 사용 가능한 tooyou를 만들어집니다. 자세한 내용은 [Microsoft Azure Preview에 대한 Microsoft Azure 추가 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.
>

예약 된 이벤트 hello Azure 메타 데이터 서비스에서 hello 하위 서비스 중 하나입니다. 응용 프로그램에서 이벤트를 준비하고 중단을 제한할 수 있도록 예정된 이벤트(예: 다시 부팅)에 대한 정보를 나타냅니다. 이 기능은 PaaS 및 IaaS를 포함한 모든 Azure Virtual Machine 유형에 사용할 수 있습니다. 예약 된 이벤트는 이벤트의 toominimize hello 효과 가상 컴퓨터 시간 tooperform 예방 작업을 제공 합니다. 

예약된 이벤트를 Linux 및 Windows VM 모두에서 사용할 수 있습니다. Linux에서 예약된 이벤트에 대한 자세한 내용은 [Linux VM에 예약된 이벤트](../windows/scheduled-events.md)를 참조하세요.

## <a name="why-scheduled-events"></a>예정된 이벤트 의의

예약 된 이벤트로 인해 서비스에서 단계에 플랫폼 intiated 유지 관리 또는 사용자가 시작한 작업의 toolimit hello 영향을 걸릴 수 있습니다. 

복제 기술을 toomaintain 상태를 사용 하는 다중 인스턴스 작업 인스턴스를 여러 개에서 일어나 고 취약 한 toooutages 수도 있습니다. 이러한 중단으로 인해 비용이 많이 드는 작업(예: 인덱스 다시 빌드) 또는 복제본 손실이 발생할 수 있습니다. 

대부분의 경우에서 hello 전반적인 서비스 가용성을 향상 시킬 수 있습니다와 같은 정상적인 종료 시퀀스를 수행 하 여 완료 (또는 취소) 진행 중인 트랜잭션은, hello (수동 장애 조치) 클러스터에서 작업 tooother Vm을 다시 할당 하거나 hello를 제거 합니다. 네트워크 부하 분산 장치 풀에서 가상 컴퓨터가 있습니다. 

여기서 예정 된 이벤트에 대 한 관리자에 게 알리는 나 이러한 이벤트를 로깅하는 데 도움이 hello 클라우드에서 호스트 되는 응용 프로그램의 hello 서비스 효율성을 개선 하는 경우가 있습니다.

Azure 서비스 메타 데이터 표면 예약 된 이벤트 hello 다음에서 사용 사례:
-   플랫폼 시작 유지 관리(예: 호스트 OS 롤아웃)
-   사용자 시작 호출(예: 사용자에 의한 VM 다시 시작 또는 다시 배포)


## <a name="hello-basics"></a>hello 기본 사항  

Azure 메타 데이터 서비스는 hello VM 내에서 액세스할 수 있는 REST 끝점을 사용 하는 가상 컴퓨터를 실행 하는 방법에 대 한 정보를 노출 합니다. hello 정보는 불가능 IP를 통해 사용할 수 있으므로 hello VM 외부에 노출 되지 않습니다.

### <a name="scope"></a>범위
예약 된 이벤트는 표시 tooall 클라우드 서비스의 가상 컴퓨터 또는 가상 컴퓨터 가용성 집합에 tooall입니다. Hello를 확인 해야 하는 결과적으로, `Resources` 필드에 hello 이벤트 tooidentify Vm toobe 영향을 받는 것입니다. 

### <a name="discovering-hello-endpoint"></a>Hello 끝점 검색
Hello 경우 가상 네트워크 (VNet) 내에서 가상 컴퓨터를 만들 위치 hello 메타 데이터 서비스에서 라우팅 불가능 고정 IP를 사용할 수는 `169.254.169.254`합니다.
추가 논리 hello 가상 컴퓨터 가상 네트워크를 클라우드 서비스 및 클래식 Vm에 대 한 hello 기본 사례 내에서 만들지 않은 경우 필요한 toodiscover hello 끝점 toouse. 어떻게 너무 toothis 샘플 toolearn 참조[hello 호스트 끝점을 검색](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)합니다.

### <a name="versioning"></a>버전 관리 
hello 인스턴스 메타 데이터 서비스 버전 관리입니다. 버전은 필수 이며 hello 현재 버전은 `2017-03-01`합니다.

> [!NOTE] 
> 이전 버전으로 hello api 버전 {최신 버전을 (를) 지원 되는 예약 된 이벤트의 미리 보기. 이 형식은 더 이상 지원 하며 hello 나중에 지원 되지 않습니다.

### <a name="using-headers"></a>헤더 사용
Hello 헤더를 제공 해야 hello 메타 데이터 서비스를 쿼리할 때 `Metadata: true` tooensure hello 요청이 실수로 리디렉션된 되지 않습니다.

### <a name="enabling-scheduled-events"></a>예약된 이벤트 사용
hello 예약 된 이벤트에 대 한 요청을 수행 하는 처음으로 Azure 암시적으로 hello 기능을 활성화 가상 컴퓨터에 합니다. 따라서 지연 된 응답을 tootwo 분의 첫 번째 호출에서 하시면 됩니다.

### <a name="user-initiated-maintenance"></a>사용자 시작 유지 관리
사용자 시작한 hello Azure 포털, API, CLI를 통해 가상 컴퓨터 유지 관리 또는 PowerShell 예약 된 이벤트를 발생 합니다. 응용 프로그램에서 tootest hello 유지 관리 준비 논리를 허용 하 고 사용자가 시작한 유지 관리에 대 한 응용 프로그램 tooprepare 프로그램을 허용 합니다.

가상 컴퓨터를 다시 시작하면 `Reboot` 유형의 이벤트가 예약됩니다. 가상 컴퓨터를 다시 배포하면 `Redeploy` 유형의 이벤트가 예약됩니다.

> [!NOTE] 
> 현재는 사용자 시작 유지 관리 작업을 최대 10개까지 동시 예약할 수 있습니다. 이 제한은 예정된 이벤트 일반 공급 이전에 완화될 예정입니다.

> [!NOTE] 
> 현재는 예약된 이벤트를 실행하는 사용자 시작 유지 관리를 구성할 수 없습니다. 구성 기능은 이후 버전에 추가될 계획입니다.

## <a name="using-hello-api"></a>Hello API를 사용 하 여

### <a name="query-for-events"></a>이벤트 쿼리
호출 하는 hello 다음을 수행 하 여 예약 된 이벤트를 쿼리할 수 있습니다.

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

응답에는 예약된 이벤트의 배열이 포함됩니다. 빈 배열은 현재 예약된 이벤트가 없음을 의미합니다.
Hello 경우에서 예약 된 이벤트 인 hello 응답 이벤트의 배열을 포함 합니다. 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>이벤트 속성
|속성  |  설명 |
| - | - |
| EventId | 이 이벤트의 GUID(Globally Unique Identifier)입니다. <br><br> 예제: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | 이 이벤트로 인해 발생하는 결과입니다. <br><br> 값 <br><ul><li> `Freeze`: hello 가상 컴퓨터를 몇 초 동안 예약 된 toopause는 합니다. hello CPU 일시 중단 되어 있지만 메모리, 열려 있는 파일 또는 네트워크 연결에 영향을 주지 않습니다. <li>`Reboot`: 가상 컴퓨터를 다시 부팅에 대 한 예약 된 hello (비 영구적인 메모리가 손실). <li>`Redeploy`: hello 가상 컴퓨터는 예약 된 toomove tooanother 노드 (임시 디스크는 손실 됨). |
| ResourceType | 이 이벤트가 영향을 주는 리소스 형식입니다. <br><br> 값 <ul><li>`VirtualMachine`|
| 리소스| 이 이벤트가 영향을 주는 리소스 목록입니다. 이 최대 하나의에서 toocontain 컴퓨터 보장 [업데이트 도메인](manage-availability.md), 하지만 hello UD의에서 모든 컴퓨터를 포함할 수 있습니다. <br><br> 예제: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| 이벤트 상태 | 이 이벤트의 상태입니다. <br><br> 값 <ul><li>`Scheduled`:이 이벤트는 hello에 지정 된 hello 시간 후 예약 된 toostart `NotBefore` 속성입니다.<li>`Started`: 이 이벤트가 시작되었습니다.</ul> 더 `Completed` 또는 유사한 상태는 제공 된 적이; hello 이벤트 hello 이벤트가 완료 될 때 더 이상 반환 됩니다.
| NotBefore| 이 시간이 지난 후 이 이벤트가 시작될 수 있습니다. <br><br> 예제: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>이벤트 예약
각 이벤트 예약 된 이벤트 형식에 따라 이후 hello 시간의 최소 양입니다. 이 시간은 이벤트의 `NotBefore` 속성에 반영됩니다. 

|EventType  | 최소 공지 |
| - | - |
| 중지| 15분 |
| Reboot | 15분 |
| 재배포 | 10분 |

### <a name="starting-an-event"></a>이벤트 시작 

예정 된 이벤트의 학습 하 고 정상 종료 논리를 완료 하 여 hello 처리 중인 이벤트를 승인할 수 있습니다는 `POST` hello로 toohello 메타 데이터 서비스를 호출할 `EventId`합니다. 이 tooAzure hello 최소 알림을 줄일 수를 나타냅니다 (가능한 경우) 시간입니다. 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> 모든 이벤트 tooproceed hello를 사용 하면 이벤트를 승인 `Resources` hello hello 이벤트도 인해 가상 컴퓨터 뿐 아니라 hello 이벤트에서입니다. 따라서 수도 있습니다 tooelect hello hello에 첫 번째 컴퓨터 처럼 간단할 수도 있음 리더 toocoordinate hello 승인을 `Resources` 필드입니다.


## <a name="powershell-sample"></a>PowerShell 샘플 

hello 다음 샘플 쿼리 hello 예약 된 이벤트에 대 한 메타 데이터를 서비스 하 고 승인 각 처리 중인 이벤트.

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a>C\# 샘플 

hello 다음 예제는 hello 메타 데이터 서비스와 통신 하는 간단한 클라이언트입니다.

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

데이터 구조를 따르면 hello를 사용 하 여 예약 된 이벤트를 나타낼 수 있습니다.

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

hello 다음 샘플 쿼리 hello 예약 된 이벤트에 대 한 메타 데이터를 서비스 하 고 승인 각 처리 중인 이벤트.

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a>Python 샘플 

hello 다음 샘플 쿼리 hello 예약 된 이벤트에 대 한 메타 데이터를 서비스 하 고 승인 각 처리 중인 이벤트.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>다음 단계 

- Hello hello에서 사용할 수 있는 Api에 대해 자세히 읽어보세요 [인스턴스 메타 데이터 서비스](instance-metadata-service.md)합니다.
- [Azure에서 Windows 가상 컴퓨터에 대한 계획된 유지 관리](planned-maintenance.md)에 대해 알아봅니다.

