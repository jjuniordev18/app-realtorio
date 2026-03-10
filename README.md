# Vale Command Center - Sistema Integrado

Este dashboard centraliza a gestão de múltiplos sistemas hospedados no Netlify e integrados via Firebase.

## Como Integrar Seus Projetos

Para incluir seus próprios projetos no dashboard, siga os passos abaixo:

### 1. Configuração de URL
No painel de **Configurações de Integração** (no final do dashboard), insira a URL do seu projeto hospedado no Netlify (ex: `https://meu-projeto.netlify.app`).

### 2. Comunicação via postMessage
Para que seu projeto envie dados em tempo real para o dashboard (como métricas de KPI e alertas), você deve usar a API `window.postMessage`.

#### Exemplo de envio de métricas (KPIs):
```javascript
window.parent.postMessage({
    type: 'METRICS_UPDATE',
    source: 'reports', // Use 'reports' para o novo módulo
    metrics: {
        count: 157,      // Total de relatórios
        syncProgress: 98 // Porcentagem de sincronização
    }
}, '*');
```

#### Exemplo de envio de alertas:
```javascript
window.parent.postMessage({
    type: 'ALERT',
    payload: {
        system: 'reports',
        level: 'warning', // 'critical', 'warning' ou 'info'
        title: 'Sincronização Pendente',
        message: 'Existem 5 fotos aguardando upload.'
    }
}, '*');
```

### 3. Configuração do Firebase
Você pode inserir suas credenciais do Firebase diretamente na interface de configurações. O dashboard se conectará ao seu banco de dados em tempo real para monitorar as atualizações.

## Estrutura do Projeto
- `index.html`: Dashboard principal com Tailwind CSS e integração Firebase.
- Módulos integrados via `<iframe>` para isolamento e segurança.
- Persistência de configurações via `localStorage`.
