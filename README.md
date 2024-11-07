# CI-CD-Automation-Pipeline
Developing an automated CI/CD pipeline for a containerized Flask application.

Tecnologie utilizzate:

    Sviluppo dell'app:         Python 3.11
    Containerizzazione:        Docker Engine
    Configurazione Pipeline:   GitHub Actions
    Registry:                  Docker Hub
    Vuln Scanning:             Trivy Action
    Monitoraggio:              Slack
    Server VPS:                Digital Ocean

    

  Sviluppo:
  
    L'applicazione è davvero semplice, scritta in Flask, 
    implementa un sistema di SignUp e Login tramite un database SQLite,
    una volta loggati si può accedere a una piccola slide che presenta alcune note 
    vulnerabilità software e interagire con i prompt simulando degli attacchi.

  Container:

    E' containerizzata (Ho usato Docker Engine sul mio sistema e docker.io sul server VPS)
    e include un Dockerfile per la costruzione dell'immagine.

  Pipeline CI-CD:

    La Pipeline copre tutte le fasi di integrazione continua (CI) e 
    distribuzione continua (CD), dopo un basico controllo del codice e
    l'installazione delle dipendenze necessarie esegue il login su Docker Hub,
    pushando l'applicazione sul registry.

  Security Scanning:

    Il passo successivo è il controllo di vulnerabilità per il quale ho usato Trivy Scan,
    riportando all'attenzione vulnerabilità di livello alto e critico,
    ma senza bloccare il deploy dell'app se tali vulnerabilità vengono scoperte.

  Deploy:

    Il deploy viene effettuato su un server VPS, la pipeline è configurata per:
    
    - Accedere alla CLI del server in modo automatico tramite SSH key 
    - Stoppare la corrente versione dell'app in esecuzione
    - Rimuovere l'immagine Docker esistente
    - Effettuare un pull dal registry della nuova versione
    - Eseguire la nuova versione (docker run -d etc.)

  Monitoring:

    Tutto il processo viene monitorato usando Slack e in caso di fallimento o successo
    di uno specifico step della pipeline viene inviata una mail al mio indirizzo. 
    Allo stesso modo nell'area di lavoro che ho configurato su Slack 
    viene notificato chiunque dovesse lavorare al progetto.

  

Il tutto avviene in modo automatizzato dall'inizio alla fine, 
ogni qualvolta un push viene effettuato sul repository.
L'applicazione funziona correttamente ed è accessibile da qualsiasi browser (non è attualmente ottimizzata per smartphone)
all'indirizzo IP specificato sopra.
