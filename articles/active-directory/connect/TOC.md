# Overzicht
## [Wat is Azure AD Connect?](active-directory-aadconnect.md)
## [Wat is Azure AD Connect Sync?](active-directory-aadconnectsync-whatis.md)
### [Gebruikers en contactpersonen](active-directory-aadconnectsync-understanding-users-and-contacts.md)
### [Architectuur](active-directory-aadconnectsync-understanding-architecture.md)
### [Declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md)
#### [Declaratieve inrichtingsexpressies](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
### [Standaardconfiguratie](active-directory-aadconnectsync-understanding-default-configuration.md)
## [Wat is Azure AD Connect en federatie?](active-directory-aadconnectfed-whatis.md)


# Aan de slag
## [Vereisten](active-directory-aadconnect-prerequisites.md)
## [Azure AD Connect installeren](active-directory-aadconnect-select-installation.md)
### [Snelle instellingen](active-directory-aadconnect-get-started-express.md)
### [Aangepaste instellingen](active-directory-aadconnect-get-started-custom.md)
### [Upgraden van DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
### [Upgrade uitvoeren van een vorige versie](active-directory-aadconnect-upgrade-previous-version.md)


# Procedures
## Plannen en ontwerpen
### [Ontwerpconcepten](active-directory-aadconnect-design-concepts.md)
### [Topologieën voor Azure AD Connect](active-directory-aadconnect-topologies.md)
### [Eenmalige aanmelding](active-directory-aadconnect-sso.md)
### [Active Directory Federation Services in Azure](active-directory-aadconnect-azure-adfs.md)
### [Speciale overwegingen voor exemplaren](active-directory-aadconnect-instances.md)
### [Als u Azure AD al hebt](active-directory-aadconnect-existing-tenant.md)
## [Azure AD Connect beheren](active-directory-aadconnect-whats-next.md)
### [Certificaten vernieuwen voor O365 en Azure AD](active-directory-aadconnect-o365-certs.md)
### [Write-back van apparaat inschakelen](active-directory-aadconnect-feature-device-writeback.md)
### [Aanmeldingsopties voor gebruiker](active-directory-aadconnect-user-signin.md)
### [Ondersteuning van meerdere domeinen voor federeren](active-directory-aadconnect-multiple-domains.md)
### [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md)



## Azure AD Connect Sync beheren
### [Onopzettelijke verwijderingen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
### [Wachtwoordsynchronisatie](active-directory-aadconnectsync-implement-password-synchronization.md)
### [Pass-through-verificatie](active-directory-aadconnect-pass-through-authentication.md)
### [Azure AD-serviceaccount](active-directory-aadconnectsync-howto-azureadaccount.md)
### [Installatiewizard](active-directory-aadconnectsync-installation-wizard.md)
### [De standaardconfiguratie wijzigen](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)
### [Filteren configureren](active-directory-aadconnectsync-configure-filtering.md)
### [Scheduler](active-directory-aadconnectsync-feature-scheduler.md)
### [Uitbreidingen van de directory](active-directory-aadconnectsync-feature-directory-extensions.md)

### [Het wachtwoord van het Azure AD Sync-serviceaccount wijzigen](active-directory-aadconnectsync-change-serviceacct-pass.md)
### [Het wachtwoord voor het AD DS-account wijzigen](active-directory-aadconnectsync-change-addsacct-pass.md)
### [AD-prullenbak inschakelen](active-directory-aadconnectsync-recycle-bin.md)

### [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md)
#### [Bewerkingen](active-directory-aadconnectsync-service-manager-ui-operations.md)
#### [Connectors](active-directory-aadconnectsync-service-manager-ui-connectors.md)
#### [Metaverse-ontwerper](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md)
#### [Metaverse zoeken](active-directory-aadconnectsync-service-manager-ui-mvsearch.md)


## Federation Services beheren
### [Beheren en aanpassen](active-directory-aadconnect-federation-management.md)
### [Meerdere exemplaren van Azure AD federeren met één exemplaar van AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)


## Problemen oplossen
### [Connectiviteit](active-directory-aadconnect-troubleshoot-connectivity.md)
### [Fouten tijdens synchronisatie](active-directory-aadconnect-troubleshoot-sync-errors.md)
### [Object is niet gesynchroniseerd](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)
### [Wachtwoordsynchronisatie](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)
### [LargeObject-fout veroorzaakt door userCertificate](active-directory-aadconnectsync-largeobjecterror-usercertificate.md)
### [Probleem met LocalDB met limiet van 10 GB oplossen](active-directory-aadconnect-recover-from-localdb-10gb-limit.md)

# Naslaginformatie
## [Tolerantie voor synchronisatie- en duplicatiekenmerken identificeren](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
## [Voor hybride identiteit benodigde poorten en protocollen](active-directory-aadconnect-ports.md)
## [Functies in preview](active-directory-aadconnect-feature-preview.md)
## [Versiegeschiedenis](active-directory-aadconnect-version-history.md)
## [Accounts en machtigingen](active-directory-aadconnect-accounts-permissions.md)

## Azure AD Connect Sync
### [Kenmerken gesynchroniseerd naar Azure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md)
### [Releasegeschiedenis van connectorversie](active-directory-aadconnectsync-connector-version-history.md)
### [Functieverwijzing](active-directory-aadconnectsync-functions-reference.md)
### [Operationele taken en overwegingen](active-directory-aadconnectsync-operations.md)
### [Compatibiliteitslijst voor Azure AD-federatie](active-directory-aadconnect-federation-compatibility.md)
### [Technische concepten](active-directory-aadconnectsync-technical-concepts.md)
### [Servicekenmerken](active-directory-aadconnectsyncservice-features.md)




# Verwant
## [Uw on-premises infrastructuur voor identiteiten en synchronisatieservices in de cloud controleren](../connect-health/active-directory-aadconnect-health.md)
## [Ontwerphandleiding voor hybride identiteit](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/)


# Bronnen
##[Veelgestelde vragen over Azure AD Connect](active-directory-aadconnect-faq.md)
##[Afschaffing van DirSync](active-directory-aadconnect-dirsync-deprecated.md)
