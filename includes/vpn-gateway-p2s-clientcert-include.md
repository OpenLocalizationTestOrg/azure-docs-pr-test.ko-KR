Tooa 연결 하는 각 클라이언트 컴퓨터 VNet 지점-사이트를 사용 하 여 클라이언트 인증서가 설치 되어 있어야 합니다. hello 클라이언트 인증서 hello 루트 인증서에서 생성 되며 각 클라이언트 컴퓨터에 설치 합니다. 유효한 클라이언트 인증서가 설치 되지 hello 클라이언트 tooconnect toohello VNet을 시도 하는 경우 인증이 실패 합니다.

각 클라이언트에 대 한 고유한 인증서를 생성할 수도 있고 또는 hello 같은 여러 클라이언트에 대 한 인증서를 사용할 수 있습니다. hello 장점은 toogenerating 고유 클라이언트 인증서 hello 기능 toorevoke 단일 인증서입니다. 그렇지 않으면 여러 클라이언트가 있는 경우 동일한 클라이언트 인증서를 hello를 사용 하 고 toorevoke 필요, toogenerate 있고 해당 인증서 tooauthenticate를 사용 하는 클라이언트 hello 모두에 대 한 새 인증서를 설치 합니다.

메서드를 다음 hello를 사용 하 여 클라이언트 인증서를 생성할 수 있습니다.

- **엔터프라이즈 인증서:**

  - 엔터프라이즈 인증서 솔루션을 사용 하는 경우 일반 이름 값 형식은 hello로 클라이언트 인증서 생성 'name@yourdomain.com'를 대신 hello '도메인 name\username' 형식입니다.
  - 카드 로그온 등 Smart 하지 않고 hello 클라이언트 인증서 템플릿을 기반으로 hello 'User' 인증서 hello hello 사용 하 여 목록에서 첫 번째 항목으로 ' 클라이언트 인증 '가 있는지 확인 합니다. Hello 클라이언트 인증서를 두 번 클릭 하 고 보기 hello 인증서를 확인할 수 있습니다 **세부 정보 > 확장 된 키 사용**합니다.

- **자체 서명 된 루트 인증서:** hello 단계 아래 P2S hello 인증서 문서 중 하나에 따라 고려해 야 합니다. 그렇지 않으면 hello 클라이언트 인증서를 만들면 P2S 연결과 호환 되지 않습니다 및 클라이언트 tooconnect 하려고 할 때 오류가 발생 합니다. hello 단계 hello 문서 다음 중 하나에 호환 되는 클라이언트 인증서를 생성 합니다. 

  * [Windows 10 PowerShell 지침](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): 이러한 지침은 Windows 10 및 PowerShell toogenerate 인증서가 필요 합니다. 지원 되는 모든 P2S 클라이언트에 생성 되는 hello 인증서를 설치할 수 있습니다.
  * [MakeCert 지침](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): 액세스 tooa Windows 10 컴퓨터 toouse toogenerate 인증서가 없는 경우 MakeCert를 사용 합니다. MakeCert 더 이상 사용 되지 않지만 MakeCert toogenerate 인증서를 계속 사용할 수 있습니다. 지원 되는 모든 P2S 클라이언트에 생성 되는 hello 인증서를 설치할 수 있습니다.

  Hello 앞에 지침을 사용 하 여 자체 서명 된 루트 인증서에서 클라이언트 인증서를 생성할 때 것에 자동으로 컴퓨터에 설치 hello toogenerate를 사용 하는 것입니다. Tooexport tooinstall 다른 클라이언트 컴퓨터에서 클라이언트 인증서를 사용 하도록 하려는 경우 필요한 전체 인증서 체인 hello와 함께.pfx로 합니다. 이 hello 클라이언트 toosuccessfully 인증에 필요 hello 루트 인증서 정보를 포함 하는.pfx 파일을 만듭니다. 단계 tooexport 인증서 참조 [인증서-클라이언트 인증서 내보내기](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport)합니다.
