# 개요
## [Azure Active Directory란?](active-directory-whatis.md)
## [Azure ID 관리 정보](identity-fundamentals.md)
## [Azure ID 솔루션 이해](understand-azure-identity-solutions.md)
## [하이브리드 ID 솔루션 선택](choose-hybrid-identity-solution.md)
## [Azure 구독 연결](active-directory-how-subscriptions-associated-directory.md)
## [FAQ](active-directory-faq.md)

# 시작
## [Azure AD Premium에 등록](active-directory-get-started-premium.md)
## [사용자 지정 도메인 이름 추가](add-custom-domain.md)
## [회사 브랜딩 구성](customize-branding.md)
## [Azure AD에 사용자 추가](add-users-azure-active-directory.md)
## [사용자에게 라이선스 할당](license-users-groups.md)
## [셀프 서비스 암호 재설정 구성](active-directory-passwords-getting-started.md)


# 방법
## 계획 및 디자인
### [Azure AD 아키텍처 이해](active-directory-architecture.md)
### [하이브리드 ID 솔루션 배포](active-directory-hybrid-identity-design-considerations-overview.md)
### [Azure Active Directory의 클레임 매핑](active-directory-claims-mapping.md)
#### 요구 사항 결정
##### [ID](active-directory-hybrid-identity-design-considerations-business-needs.md)
##### [디렉터리 동기화](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
##### [Multi-Factor Auth](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)
##### [ID 수명 주기 전략](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)
#### [데이터 보안 계획](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)
##### [데이터 보호](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
##### [콘텐츠 관리](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
##### [액세스 제어](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
##### [사고 대응](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)
#### ID 수명 주기 계획
##### [작업](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)
##### [채택 전략](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)
#### [다음 단계](active-directory-hybrid-identity-design-considerations-nextsteps.md)
#### [도구 비교](active-directory-hybrid-identity-design-considerations-tools-comparison.md)

## 사용자 관리
### [그룹을 사용하여 라이선스 할당](active-directory-licensing-whatis-azure-portal.md)
#### [그룹에 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)
#### [그룹에서 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)
#### [개별 라이선스 사용자를 그룹 기반 라이선스로 마이그레이션](active-directory-licensing-group-migration-azure-portal.md)
#### [그룹 기반 라이선스에 대한 추가 시나리오](active-directory-licensing-group-advanced.md)
#### [그룹 기반 라이선스에 대한 PowerShell 예제](active-directory-licensing-ps-examples.md)
### [다른 디렉터리에서 사용자 추가(클래식 포털)](active-directory-create-users-external.md)
### [사용자 프로필 관리](active-directory-users-profile-azure-portal.md)
### [암호 재설정](active-directory-users-reset-password-azure-portal.md)
### [사용자 작업 정보 관리](active-directory-users-work-info-azure-portal.md)
### [공유 계정](active-directory-sharing-accounts.md)



## [그룹 및 구성원 관리](active-directory-manage-groups.md)
### 그룹 관리
#### [Azure Portal](active-directory-groups-create-azure-portal.md)
#### [클래식 포털](active-directory-accessmanagement-manage-groups.md)
#### [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
### [그룹 구성원 관리](active-directory-groups-members-azure-portal.md)
### [그룹 소유자 관리](active-directory-accessmanagement-managing-group-owners.md)
### [그룹 멤버 자격 관리](active-directory-groups-membership-azure-portal.md)
### [그룹을 사용하여 라이선스 할당](active-directory-licensing-whatis-azure-portal.md)
#### [그룹에 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)
#### [그룹에서 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)
#### [개별 라이선스 사용자를 그룹 기반 라이선스로 마이그레이션](active-directory-licensing-group-migration-azure-portal.md)
#### [그룹 기반 라이선스에 대한 추가 시나리오](active-directory-licensing-group-advanced.md)
#### [그룹 기반 라이선스에 대한 PowerShell 예제](active-directory-licensing-ps-examples.md)
### [Office 365 그룹 만료 설정](active-directory-groups-lifecycle-azure-portal.md)
### [모든 그룹 보기](active-directory-groups-view-azure-portal.md)
### [전용 그룹 사용](active-directory-accessmanagement-dedicated-groups.md)
### [SaaS 앱에 대한 그룹 액세스 추가](active-directory-accessmanagement-group-saasapps.md)
### [삭제된 Office 365 그룹 복원](active-directory-groups-restore-azure-portal.md)
### 그룹 설정 관리
#### [Azure 포털](active-directory-groups-settings-azure-portal.md)
#### [Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
### 고급 규칙 만들기
#### [Azure 포털](active-directory-groups-dynamic-membership-azure-portal.md)
#### [클래식 포털](active-directory-accessmanagement-groups-with-advanced-rules.md)
### [셀프 서비스 그룹 설정](active-directory-accessmanagement-self-service-group-management.md)
### [문제 해결](active-directory-accessmanagement-troubleshooting.md)

## [보고서 관리](active-directory-reporting-azure-portal.md)
### [로그인 활동](active-directory-reporting-activity-sign-ins.md)
### [감사 활동](active-directory-reporting-activity-audit-logs.md)
### [위험에 노출된 사용자](active-directory-reporting-security-user-at-risk.md)
### [위험한 로그인](active-directory-reporting-security-risky-sign-ins.md)
### [위험 이벤트](active-directory-reporting-risk-events.md)
### [FAQ](active-directory-reporting-faq.md)
### 작업
#### [명명된 위치 구성](active-directory-named-locations.md)
#### [활동 보고서 보기](active-directory-reporting-migration.md)
#### [Azure Active Directory Power BI 콘텐츠 팩 사용](active-directory-reporting-power-bi-content-pack-how-to.md)
### 참조
#### [보존](active-directory-reporting-retention.md)
#### [대기 시간](active-directory-reporting-latencies-azure-portal.md)
#### [Notifications](active-directory-reporting-notifications.md)
#### [로그인 작업 오류 코드](active-directory-reporting-activity-sign-ins-errors.md)
### 문제 해결
#### [누락된 감사 데이터](active-directory-reporting-troubleshoot-missing-audit-data.md)
#### [다운로드에서 누락된 데이터](active-directory-reporting-troubleshoot-missing-data-download.md)
#### [Azure Active Directory 활동 로그 콘텐츠 팩 오류](active-directory-reporting-troubleshoot-content-pack.md)
### [프로그래밍 방식 액세스](active-directory-reporting-api-getting-started-azure-portal.md)
#### [감사 참조](active-directory-reporting-api-audit-reference.md)
#### [로그인 참조](active-directory-reporting-api-sign-in-activity-reference.md)
#### [필수 구성 요소](active-directory-reporting-api-prerequisites-azure-portal.md)
#### [감사 샘플](active-directory-reporting-api-audit-samples.md)
#### [로그인 샘플](active-directory-reporting-api-sign-in-activity-samples.md)
#### [인증서 사용](active-directory-reporting-api-with-certificates.md)

## [암호 관리](active-directory-passwords-overview.md)
### 사용자 문서
#### [암호 재설정 또는 변경](active-directory-passwords-update-your-own-password.md)
#### [암호 모범 사례](active-directory-secure-passwords.md)
#### [셀프 서비스 암호 재설정 등록](active-directory-passwords-reset-register.md)
### [라이선스 SSPR](active-directory-passwords-licensing.md)
### [SSPR 배포](active-directory-passwords-best-practices.md)
### IT 관리자: 암호 재설정
#### [Azure 포털](active-directory-users-reset-password-azure-portal.md)
#### [Azure 클래식 포털](active-directory-create-users-reset-password.md)
### [SSPR 정책 이해](active-directory-passwords-policy.md)
### [암호 재설정 이해](active-directory-passwords-how-it-works.md)
### [SSPR 사용자 지정](active-directory-passwords-customize.md)
### [SSPR에 사용된 데이터](active-directory-passwords-data.md)
### [SSPR에 대한 보고](active-directory-passwords-reporting.md)
### [Azure AD Connect](./connect/active-directory-aadconnect.md)
### [비밀번호 쓰기 저장](active-directory-passwords-writeback.md)
### [암호 해시 동기화](./connect/active-directory-aadconnectsync-implement-password-synchronization.md#how-password-synchronization-works)
### [문제 해결](active-directory-passwords-troubleshoot.md)
### [FAQ](active-directory-passwords-faq.md)


## 장치 관리
### [소개](device-management-introduction.md)
### [Azure Portal 사용](device-management-azure-portal.md)
### [FAQ](device-management-faq.md)
### 작업
#### [하이브리드 Azure AD 가입 장치 구성](device-management-hybrid-azuread-joined-devices-setup.md) 
#### [온-프레미스 배포](active-directory-device-registration-on-premises-setup.md)
### 문제 해결
#### [하이브리드 Azure AD 가입 Windows 10 및 Windows Server 2016 장치](device-management-troubleshoot-hybrid-join-windows-current.md)
#### [하이브리드 Azure AD 가입 레거시 Windows 장치](device-management-troubleshoot-hybrid-join-windows-legacy.md)
### [Azure AD 조인](active-directory-azureadjoin-overview.md)
#### [계획](active-directory-azureadjoin-deployment-aadjoindirect.md)
#### [장치 등록 설정](active-directory-azureadjoin-setup.md)
#### [새 장치 등록](active-directory-azureadjoin-user-frx.md)
#### [배포](active-directory-azureadjoin-devices-group-policy.md)
#### [Windows 10 통합 이해](active-directory-azureadjoin-windows10-devices-overview.md)
#### [Windows 10 장치 사용](active-directory-azureadjoin-windows10-devices.md)
#### [장치 연결](active-directory-azureadjoin-personal-device.md)
#### [Windows 10 장치 연결](active-directory-azureadjoin-user-upgrade.md)

## 앱 관리
### [개요](active-directory-enable-sso-scenario.md)
### [시작](active-directory-integrating-applications-getting-started.md)
### [SaaS 앱 통합 자습서](active-directory-saas-tutorial-list.md)
### [클라우드 앱 검색](active-directory-cloudappdiscovery-whatis.md)
#### [레지스트리 설정 업데이트](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
#### [보안 및 개인 정보 이해](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)


### [앱 프록시를 사용하여 원격으로 앱에 액세스](active-directory-application-proxy-get-started.md)
#### 시작
##### [앱 프록시 사용](active-directory-application-proxy-enable.md)
##### [앱 게시](application-proxy-publish-azure-portal.md)
##### [사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)
#### [Single Sign-On](application-proxy-sso-overview.md)
##### [KCD와 SSO](active-directory-application-proxy-sso-using-kcd.md)
##### [헤더와 SSO](application-proxy-ping-access.md)
##### [암호 보관을 사용하는 SSO](application-proxy-sso-azure-portal.md)
#### 개념
##### [커넥터](application-proxy-understand-connectors.md)
##### [보안](application-proxy-security-considerations.md)
##### [네트워크](application-proxy-network-topology-considerations.md)


##### [TMG 또는 UAG에서 업그레이드](application-proxy-transition-from-uag-tmg.md)

#### 고급 구성
##### [별도 네트워크에 게시](active-directory-application-proxy-connectors-azure-portal.md)
##### [프록시 서버](application-proxy-working-with-proxy-servers.md)
##### [클레임 인식 앱](active-directory-application-proxy-claims-aware-apps.md)
##### [네이티브 클라이언트 앱](active-directory-application-proxy-native-client.md)
##### [자동 설치](active-directory-application-proxy-silent-installation.md)
##### [사용자 지정 홈 페이지](application-proxy-office365-app-launcher.md)
##### [인라인 링크 변환](application-proxy-link-translation.md)
#### 게시 연습
##### [원격 데스크톱](application-proxy-publish-remote-desktop.md)
##### [SharePoint](application-proxy-enable-remote-access-sharepoint.md)
##### [Microsoft 팀](application-proxy-teams.md)
#### [문제 해결](active-directory-application-proxy-troubleshoot.md)
#### 클래식 포털 사용
##### [커넥터 다운로드](application-proxy-enable-classic-portal.md)
##### [앱 게시](active-directory-application-proxy-publish.md)
##### [커넥터 사용](active-directory-application-proxy-connectors.md)
##### [조건부 액세스](active-directory-application-proxy-conditional-access.md)

### 엔터프라이즈 앱 관리
#### [사용자 할당](active-directory-coreapps-assign-user-azure-portal.md)
#### [브랜딩 사용자 지정](active-directory-coreapps-change-app-logo-user-azure-portal.md)
#### [사용자 로그인 비활성화](active-directory-coreapps-disable-app-azure-portal.md)
#### [사용자 제거](active-directory-coreapps-remove-assignment-azure-portal.md)
#### [내 앱 모두 보기](active-directory-coreapps-view-azure-portal.md)
#### [사용자 계정 프로비전 관리](active-directory-enterprise-apps-manage-provisioning.md)

### [앱에 대한 액세스 관리](active-directory-managing-access-to-apps.md)
#### [셀프 서비스 액세스](active-directory-self-service-application-access.md)
#### [SSO 액세스](active-directory-appssoaccess-whatis.md)
#### [SSO 인증서](active-directory-sso-certs.md)
#### [테넌트 제한 사항](active-directory-tenant-restrictions.md)
#### [SCIM 프로비전 사용자 사용](active-directory-scim-provisioning.md)

### [문제 해결](active-directory-application-troubleshoot-content-map.md)
#### [응용 프로그램 개발](active-directory-application-dev-troubleshoot-content-map.md)
##### [구성 및 등록](active-directory-application-dev-config-content-map.md)
##### [개발](active-directory-application-dev-development-content-map.md)
#### [응용 프로그램 관리](active-directory-application-management-troubleshoot-content-map.md)
##### [구성](active-directory-application-config-content-map.md)
##### [로그인](active-directory-application-sign-in-content-map.md)
##### [프로비전](active-directory-application-provisioning-content-map.md)
##### [액세스 관리](active-directory-application-access-content-map.md)
##### [액세스 패널](active-directory-application-access-panel-content-map.md)
##### [응용 프로그램 프록시](active-directory-application-proxy-content-map.md)
##### [조건부 액세스](active-directory-application-conditional-access-content-map.md)
### [앱 개발](active-directory-applications-guiding-developers-for-lob-applications.md)
### [문서 라이브러리](active-directory-apps-index.md)

## 디렉터리 관리
### [Azure AD Connect](./connect/active-directory-aadconnect.md)
### 사용자 지정 도메인 이름
#### [개요](active-directory-add-domain-concepts.md)
#### 도메인 이름 관리
##### [Azure Portal](active-directory-domains-manage-azure-portal.md)
##### [클래식 포털](active-directory-add-manage-domain-names.md)
### [디렉터리 관리](active-directory-administer.md)
### [여러 디렉터리](active-directory-licensing-directory-independence.md)
### [O365 디렉터리](active-directory-manage-o365-subscription.md)
### [셀프 서비스 등록](active-directory-self-service-signup.md)
### [엔터프라이즈 상태 로밍](active-directory-windows-enterprise-state-roaming-overview.md)
#### [사용](active-directory-windows-enterprise-state-roaming-enable.md)
#### [그룹 정책 설정](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
#### [Windows 10 설정](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
#### [FAQ](active-directory-windows-enterprise-state-roaming-faqs.md)
#### [문제 해결](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

### [Azure AD B2B와 파트너 통합](active-directory-b2b-what-is-azure-ad-b2b.md)
#### [B2B 사용자를 추가하는 관리자](active-directory-b2b-admin-add-users.md)
#### [B2B 사용자를 추가하는 지식 근로자](active-directory-b2b-iw-add-users.md)
#### [API 및 사용자 지정](active-directory-b2b-api.md)
#### [코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
#### [셀프 서비스 등록 포털 샘플](active-directory-b2b-self-service-portal.md)
#### [초대 전자 메일](active-directory-b2b-invitation-email.md)
#### [초대 상환](active-directory-b2b-redemption-experience.md)
#### [초대 없이 B2B 사용자 추가](active-directory-b2b-add-user-without-invite.md)
#### [B2B에 대한 조건부 액세스](active-directory-b2b-mfa-instructions.md)
#### [B2B 공유 정책](active-directory-b2b-delegate-invitations.md)
#### [역할에 B2B 사용자 추가](active-directory-b2b-add-guest-to-role.md)
#### [동적 그룹 및 B2B 사용자](active-directory-b2b-dynamic-groups.md)
#### [감사 및 보고서](active-directory-b2b-auditing-and-reporting.md)
#### [B2B 및 Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
#### [라이선스](active-directory-b2b-licensing.md)
#### [현재 제한 사항](active-directory-b2b-current-limitations.md)
#### [FAQ](active-directory-b2b-faq.md)
#### [B2B 문제 해결](active-directory-b2b-troubleshooting.md)
#### [B2B 사용자 이해](active-directory-b2b-user-properties.md)
#### [B2B 사용자 토큰](active-directory-b2b-user-token.md)
#### [Azure AD용 B2B 통합 앱](active-directory-b2b-configure-saas-apps.md)
#### [B2B 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
#### [B2B 공동 작업 및 B2C 비교](active-directory-b2b-compare-b2c.md)
#### [B2B에 대한 지원 받기](active-directory-b2b-support.md)

### [Azure AD Connect를 사용하여 온-프레미스 ID 통합](./connect/active-directory-aadconnect.md)

## 리소스에 대한 액세스 위임
### [관리자 역할](active-directory-assign-admin-roles.md)
#### [관리자 역할 할당](active-directory-users-assign-role-azure-portal.md)
### [관리 단위](active-directory-administrative-units-management.md)
### [Azure의 리소스 액세스](active-directory-understanding-resource-access.md)
### [역할 기반 액세스 제어](role-based-access-control-what-is.md)
#### 액세스 할당 관리
##### [사용자별](role-based-access-control-manage-assignments.md)
##### [리소스별](role-based-access-control-configure.md)
#### [기본 제공 역할](role-based-access-built-in-roles.md)
#### [사용자 지정 역할](role-based-access-control-custom-roles.md)
#### [내부 및 외부 사용자에 대한 사용자 지정 역할 할당](role-based-access-control-create-custom-roles-for-internal-external-users.md)
#### [보고](role-based-access-control-access-change-history-report.md)
#### 역할을 관리하는 다양한 방법
##### [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
##### [PowerShell](role-based-access-control-manage-access-powershell.md)
##### [REST (영문)](role-based-access-control-manage-access-rest.md)
#### [테넌트 관리자 액세스 권한 상승](role-based-access-control-tenant-admin-access.md)
#### [문제 해결](role-based-access-control-troubleshooting.md)
#### [리소스 공급자 작업](role-based-access-control-resource-provider-operations.md)
### [토큰 수명](active-directory-configurable-token-lifetimes.md)

## ID 보안
### [조건부 액세스](active-directory-conditional-access-azure-portal.md)
#### [시작](active-directory-conditional-access-azure-portal-get-started.md)
#### [모범 사례](active-directory-conditional-access-best-practices.md)
#### [기술 참조](active-directory-conditional-access-technical-reference.md)
#### [지원되는 앱](active-directory-conditional-access-supported-apps.md)
#### [장치 정책 이해](active-directory-conditional-access-device-policies.md)
#### [연결된 앱에 대한 액세스 설정](active-directory-conditional-access-policy-connected-applications.md)
#### [재구성](active-directory-conditional-access-device-remediation.md)
#### [FAQ](active-directory-conditional-faqs.md)
#### [클래식 포털](active-directory-conditional-access.md)
##### [시작](active-directory-conditional-access-azuread-connected-apps.md)


### Windows Hello
#### [암호 없이 인증](active-directory-azureadjoin-passport.md)
#### [비즈니스용 Windows Hello 사용](active-directory-azureadjoin-passport-deployment.md)
### 인증서 기반 인증
#### [Android](active-directory-certificate-based-authentication-android.md)
#### [iOS](active-directory-certificate-based-authentication-ios.md)
#### [시작](active-directory-certificate-based-authentication-get-started.md)

### [Azure AD ID 보호](active-directory-identityprotection.md)
#### [사용](active-directory-identityprotection-enable.md)
#### [취약점 감지](active-directory-identityprotection-vulnerabilities.md)
#### [위험 이벤트](active-directory-identity-protection-risk-events.md)
#### [Notifications](active-directory-identityprotection-notifications.md)
#### [로그인 환경](active-directory-identityprotection-flows.md)
#### [위험 이벤트 시뮬레이션](active-directory-identityprotection-playbook.md)
#### [사용자 차단 해제](active-directory-identityprotection-unblock-howto.md)
#### [FAQ](active-directory-identity-protection-faqs.md)
#### [용어](active-directory-identityprotection-glossary.md)
#### [Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
### [Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

## [Azure VM에 AD DS 배포](virtual-networks-windows-server-active-directory-virtual-machines.md)
### [Azure VM의 Windows Server Active Directory](active-directory-deploying-ws-ad-guidelines.md)
### [Azure 가상 네트워크의 복제본 도메인 컨트롤러](active-directory-install-replica-active-directory-domain-controller.md)
### [Azure 가상 네트워크의 새 포리스트](active-directory-new-forest-virtual-machine.md)



## [Azure에서 AD FS 배포](active-directory-aadconnect-azure-adfs.md)
### [고가용성](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
### [서명 해시 알고리즘 변경](active-directory-federation-sha256-guidance.md)

## [문제 해결](active-directory-troubleshooting-support-howto.md)
### [문제 해결: Active Directory 항목이 없거나 사용할 수 없음](active-directory-troubleshooting.md)

## Azure AD 개념 증명(PoC) 배포
### [PoC 플레이 북: 소개](active-directory-playbook-intro.md)
### [PoC 플레이 북: 재료](active-directory-playbook-ingredients.md)
### [PoC 플레이 북: 구현](active-directory-playbook-implementation.md)
### [PoC 플레이 북: 구성 요소](active-directory-playbook-building-blocks.md)


# 참조
## [코드 샘플](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory)
## [PowerShell cmdlet](/powershell/azure/overview)
## [Java API 참조](/java/api)
## [.NET API](/active-directory/adal/microsoft.identitymodel.clients.activedirectory)
## [서비스 제한 및 제한 사항](active-directory-service-limits-restrictions.md)

# 관련 항목
## [Multi-Factor Authentication](/azure/multi-factor-authentication/)
## [Azure AD Connect](./connect/active-directory-aadconnect.md)
## [Azure AD Connect Health](./connect-health/active-directory-aadconnect-health.md)
## [개발자용 Azure AD](./develop/active-directory-how-to-integrate.md)
## [Azure AD Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

# 리소스
## [Azure 피드백 포럼](https://feedback.azure.com/forums/169401-azure-active-directory)
## [Azure 로드맵](https://azure.microsoft.com/roadmap/?category=security-identity)
## [MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)
## [가격](https://azure.microsoft.com/pricing/details/active-directory/)
## [요금 계산기](https://azure.microsoft.com/pricing/calculator/)
## [서비스 업데이트](https://azure.microsoft.com/updates/?product=active-directory)
## [스택 오버플로](http://stackoverflow.com/questions/tagged/azure-active-directory)
## [비디오](https://azure.microsoft.com/documentation/videos/index/?services=active-directory)
