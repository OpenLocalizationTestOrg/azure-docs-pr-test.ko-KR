
### <a name="installation-failures"></a>설치 오류
| **샘플 오류 메시지** | **권장 작업** |
|--------------------------|------------------------|
|오류 실패 tooload 계정입니다. 오류: System.IO.IOException: 수 없습니다 tooread 데이터 hello에서 설치 하 고 등록 CS 서버 hello 경우 연결을 전송 합니다.| TLS 1.0 hello 컴퓨터에서 활성화 되어 있는지 확인 합니다. |

### <a name="registration-failures"></a>등록 오류
등록 오류가 hello에 있는 hello 로그를 검토 하 여 디버깅할 수 **%ProgramData%\ASRLogs** 폴더입니다.

| **샘플 오류 메시지** | **권장 작업** |
|--------------------------|------------------------|
|**09:20:06**: InnerException.Type: SrsRestApiClientLib.AcsException,InnerException.<br>메시지: ACS50008: SAML 토큰이 잘못되었습니다.<br>추적 ID: 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>상관 관계 ID: 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>타임스탬프: **2016-12-12 14:50:08Z<br>** | 시스템 시계에 hello 시간 15 분 넘게 hello 현지 시간 off 인지 확인 합니다. Hello installer toocomplete hello 등록을 다시 실행 합니다.|
|**09시 35분: 27** : hello 선택한 인증서에 대 한 모든 재해 복구 볼트 tooget 동안 DRRegistrationException:: Exception.Message, Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException에서 발생 했습니다. ACS50008: SAML 토큰이 잘못 되었습니다.<br>추적 ID: e5ad1af1-2d39-4970-8eef-096e325c9950<br>상관 관계 ID: abe9deb8-3e64-464d-8375-36db9816427a<br>타임스탬프: **2016-05-19 01:35:39Z**<br> | 시스템 시계에 hello 시간 15 분 넘게 hello 현지 시간 off 인지 확인 합니다. Hello installer toocomplete hello 등록을 다시 실행 합니다.|
|06시 28분: 45: 실패 한 toocreate 인증서<br>06:28:45: 설치를 진행할 수 없습니다. 인증서 필요 tooauthenticate tooSite 복구를 만들 수 없습니다. 설치를 다시 실행합니다. | 로컬 관리자로 설치 프로그램을 실행하고 있는지 확인합니다. |
