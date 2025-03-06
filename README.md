# README - Aplikace Vrátnice

Tento dokument popisuje nastavení, konfiguraci a spuštění aplikace Vrátnice spolu s přidruženým Keycloak autentizačním serverem. Níže najdete informace o uživatelských účtech, konfiguraci Docker souborů a postup spuštění aplikací.

## Obsah
- [Účty Keycloak](#účty-keycloak)
- [Spuštění aplikací](#spuštění-aplikací)
- [Docker soubory](#docker-soubory)
- [Technické požadavky](#technické-požadavky)
- [Kontakt](#kontakt)

## Účty Keycloak

Aplikace Vrátnice využívá Keycloak pro správu autentizace a autorizace. Níže jsou uvedeny přihlašovací údaje pro různé typy účtů.

### Keycloak (admin) účet
- **Username/Password**: `admin/admin123`
- **Popis**: Tento účet slouží pouze ke správě Keycloaku (např. konfigurace rolí, klientů atd.) a nemá přístup k aplikaci Vrátnice.

### Uživatelské účty pro aplikaci Vrátnice
Níže jsou uvedeny účty pro aplikaci Vrátnice, každý s specifickými oprávněními podle role:
- **Hlavní administrátor**
  - **Username/Password**: `hlavni_administrator/DipPra123*`
  - **Oprávnění**: Všechny vjezdy vozidla, Správa vjezdů vozidla, Správa návštěvnických listků, Správa docházky, Správa vpuštěk klíčů, Evidence vjezdů a vjezdů vozidel, vpuštěk klíčů, náhledů a docházek zaměstnanců.
  - **Přístup ke všem funkcím vrátnice**.

- **Vrátný**
  - **Username/Password**: `vratny/DipPra123*`
  - **Oprávnění**: Správa návštěvnických listků, Správa vjezdů vozidla, Správa výjezdů vozidla, Evidence vjezdů a vjezdů vozidla, vpuštěk klíčů.
  - **Přístup**: Správa a schvalování základních požadavků na povolení vjezdů.

- **Bezpečnostní manažer**
  - **Username/Password**: `bezpecnostni_manager/DipPra123*`
  - **Oprávnění**: Správa povolení vjezdů vozidla, Správa služebních vozidel, Správa SPZ kamer vrátků.
  - **Přístup**: Detekce SPZ, klíče a jejich vpuštěk (přístupy).

- **Správce budovy**
  - **Username/Password**: `spravce_budovy/DipPra123*`
  - **Oprávnění**: Správa budov, Správa klíčů, Správa žádostí o klíče.
  - **Přístup**: Správa budov, klíčů a jejich vpuštěk (přístupy).

**Poznámka**: Hesla (`DipPra123*`) jsou pro vývojové prostředí. Doporučuje se po nasazení do produkce změnit hesla a zajistit jejich bezpečnost.

## Spuštění aplikací

Aplikace Vrátnice se skládá z backendové části (Java) a frontendové části (Angular). Tyto části se nespouštějí přímo z Dockeru, ale pomocí vývojového prostředí nebo příkazové řádky.

### Backend (Java)
- **Nástroje**: IntelliJ IDEA, Eclipse nebo jiné vývojové prostředí pro Java.
- **Spuštění**:
  1. Otevřete projekt v IDE.
  2. Ověřte konfiguraci databáze (viz Docker soubory níže).
  3. Spusťte hlavní třídu aplikace (např. `VratniceApplication`) nebo použijte příkaz:
     ```bash
     mvn spring-boot:run
    ```
    
### Frontend (Angular)
- **Nástroje**: e: Node.js, npm, Visual Studio Code nebo jiné vývojové prostředí.
- **Spuštění**:
  1. Přejděte do adresáře s frontendovým projektem.
  2. Nainstalujte závislosti:
    ```bash
     npm install
    ```
  3. Spusťte hlavní třídu aplikace (např. `VratniceApplication`) nebo použijte příkaz:
     ```bash
     npm start
     ```

### Docker soubory
Projekt využívá dva Docker soubory pro lokální nastavení databází a Keycloaku. Tyto soubory nejsou použity pro spuštění aplikací, ale pro přípravu prostředí.

**1. Repozitář** `vratnice-keycloak`
- **Obsah**: Docker soubor pro spuštění Keycloaku včetně databázových dat.
- **Spuštění**:
  1. Přejděte do adresáře `vratnice-keycloak`.
  2. Spusťte Docker:
    ```bash
     docker-compose up
    ```
- **Databáze**: Obsahuje předkonfigurovaná data pro Keycloak (např. uživatelské účty)


**2. Repozitář** `vratnice`
- **Obsah**: Docker soubor pro lokální databázi aplikace Vrátnice.
- **Spuštění**:
  1. Přejděte do adresáře `vratnice`.
  2. Spusťte Docker:
    ```bash
     docker-compose up
    ```
- **Databáze**: Obsahuje předkonfigurovaná data pro Keycloak (např. uživatelské účty 