다음으로, 모든 서버 hello 클러스터에서 Windows Server 2008 R2 또는 Windows Server 2012를 실행 중인 경우 해당 hello 핫픽스가 확인 해야 [KB2854082](http://support.microsoft.com/kb/2854082) 각 hello 온-프레미스 서버 또는 hello 클러스터의 일부인 Azure 가상 컴퓨터에 설치 되어 있습니다. 모든 서버 또는 VM에 연결이 hello 클러스터만 hello 가용성 그룹에 없는 있어야이 핫픽스를 설치 합니다.

각 클러스터 노드에서 hello에 대 한 hello 원격 데스크톱 세션에서 다운로드 [KB2854082](http://support.microsoft.com/kb/2854082) tooa 로컬 디렉터리입니다. 순차적으로 각 클러스터 노드에서 hello 핫픽스를 설치 합니다. Hello 클러스터 노드에서 hello 클러스터 서비스가 현재 실행 중인 경우에 hello 서버 hello 끝 hello 핫픽스 설치 과정에서 다시 시작 됩니다.

> [!WARNING]
> Hello 클러스터 서비스를 중지 하거나 hello 서버를 다시 시작 하면 클러스터 및 hello 가용성 그룹의 hello 쿼럼 상태에 영향을 줍니다 하 고 오프 라인에 클러스터 toogo 발생할 수 있습니다. toomaintain hello 고가용성 클러스터를 설치 하는 동안 사항을 확인 합니다.
> 
> * hello 클러스터가 최적의 쿼럼 상태에 있습니다. 
> * 모든 노드에서 hello 핫픽스를 설치 하기 전에 모든 클러스터 노드가 온라인 상태가 됩니다.
> * Hello 클러스터의 노드에서 hello 핫픽스를 설치 하기 전에 hello 핫픽스 설치 toorun toocompletion 완전히 hello 서버 다시 시작을 포함 하 여 한 노드에서 허용 합니다.
> 
> 

