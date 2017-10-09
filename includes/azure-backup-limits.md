hello 제한을 따르는 tooAzure 백업을 적용 합니다.

| 제한 식별자 | 기본 제한 |
| --- | --- |
| 각 자격 증명 모음에 대해 등록할 수 있는 서버/컴퓨터 수 |Windows Server/Client/SCDPM의 경우 50개  <br/> IaaS VM의 경우 200개 |
| Azure 자격 증명 모음 저장소에 저장 된 데이터에 대한 데이터 원본의 크기 |최대 54400GB<sup>1</sup> |
| 각 Azure 구독에 만들 수 있는 백업 자격 증명 모음의 개수 |25개(백업 자격 증명 모음) <br/> 지역당 Recovery Services 자격 증명 모음 25개 |
| 하루에 백업을 예약할 수 있는 횟수 |Windows 서버/클라이언트의 경우 하루에 3번  <br/> SCDPM에 대해 하루에 2번 <br/> IaaS VM의 경우 하루에 한 번 |
| 데이터 디스크가 연결 tooan 백업에 대 한 Azure 가상 컴퓨터 |16 |

* <sup>1</sup>hello 54400 GB 제한은 tooIaaS VM 백업을 적용 되지 않습니다.

