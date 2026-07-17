# Changelog — Simple Monday

## Versão 0.21.0

### Novidades

- Leitura de QR preferindo o **Google Lens** (`com.google.ar.lens`) quando o app estiver instalado no Android.

### Melhorias

- Sem Lens instalado (ex.: tablet), o app abre a **câmera interna** — sem redirecionar para a Play Store.
- Manifesto Android declara `<queries>` para `com.google.ar.lens`, necessário no Android 11+ para detectar e abrir o pacote.

### Correções

- Detecção do Lens deixa de depender do `MainActivity` em Android antigo (falha por `BackEvent`), usando Context via `ActivityThread`.
- Removido fallback `google://lens` que no tablet reportava sucesso sem abrir nada e bloqueava a câmera.

## Versão 0.20.0

### Novidades

- Apontamentos e relógio locais: destino **Local** ou **Monday**, com catálogo próprio (tarefa/subitem) sem misturar com a sync do Monday.
- Dashboard com cards **Corretos** e **Incorretos** no ciclo selecionado (dias úteis de apontamento).
- Menu de atualização no AppBar: escolher sincronizar tudo ou só uma integração ativa (Monday, Clock In, Meu RH, agenda, ICS).

### Melhorias

- Botão **Justificar** deixa de usar URL fixa: a URL do formulário vem do QR/config da organização; se ainda não existir, o app pede no primeiro clique.
- Site [configure](https://simplemonday.gfsolutions.app.br/configure.html) e QR da Solinftec atualizados com a URL de justificativa.

### Correções

- Recuperação automática do SQLite em camadas (reparar índices → restaurar backup → quarentena e recriar), sem tela vermelha e sem deadlock ao recriar tabelas.
- Backup consistente do banco local após escritas (no máximo a cada 5 minutos) para reduzir perda de dados em corrupção.
- Kotlin alinhado ao modo WAL do SQLite Python, reduzindo risco de corrupção por acesso misto.

## Versão 0.19.0

### Correções

- Meu RH passa a resolver UTC em cascata a partir do Clock In (`pair` → `recent_gmt` → `punch_timezone`), com suporte a `America/Cuiaba` e fallback quando o Android não tem base IANA.
- Corrigido o deep link `simplemonday://` no Android (intent-filter no manifesto) e o botão "Abrir no app" no site (Intent URL no Chrome).
- Corrigidas permissões e fluxo de notificações/alarme/bateria no Android (incl. keep JNI no ProGuard).

### Melhorias

- Atualizado o stack do app: **Flet 0.86**, Flutter e Python do bundle Android (**3.14**), com `tzdata` empacotado.
- Nova task de compilação **v2 (single-pass)** para APK e AAB, além de **Fast push** adaptado ao layout 0.86.
- Configuração da organização deixa de depender de URL hardcoded: escolha e liberação dos endpoints passam pelo site ([configure](https://simplemonday.gfsolutions.app.br/configure.html)), com atalho no app, QR, deep link e opção de copiar código.

## Versão 0.18.3

### Melhorias

- Otimizada a verificação de sons de alarme e notificação, removendo o processo de consulta contínua (poll) para melhor desempenho.

### Correções

- Corrigido um problema na integração com a agenda do celular.

## Versão 0.18.2

### Novidades

- Adicionado sistema de atualização automática (Auto Update) para a versão Windows.

### Correções

- Corrigido um problema na atualização da API interna, garantindo maior estabilidade e confiabilidade nas sincronizações.

## Versão 0.18.0

### Novidades

- Adicionado sistema de atualização automática (auto-update) na versão para Windows.

## Versão 0.17.1

### Novidades

- Adicionada a opção de criar abonos manualmente.

### Melhorias

- Sistema de notificações aprimorado para maior confiabilidade.
- Agora é possível escolher se as notificações serão reproduzidas como notificação padrão ou como alarme.

## Versão 0.15.0

### Novidades

- Sincronização de compromissos do Microsoft Teams e Outlook também na versão para PC, utilizando links ICS de calendários compartilhados.
- Abonos do Meu RH agora são exibidos no Calendário e no Dashboard.
- Novos filtros na tela de apontamentos manuais do Monday.
- Sugestão automática do último apontamento para agilizar novos registros.
- Nova notificação para lembrar de bater o ponto ao conectar em uma rede Wi-Fi específica.

### Melhorias

- Notificações de horários fixos e de turnos agora também funcionam na versão para PC (com o aplicativo em primeiro plano).

### Correções

- Corrigido o corte da interface na parte inferior do aplicativo em celulares com barra de navegação.

## Versão 0.14.7

- **Android:** Adicionado suporte a assinaturas de release.
- **Banco de Dados:** Implementação de travas de acesso ao banco de dados para evitar conflitos de leitura/escrita.
- **Interface do Calendário:** Adicionadas novas colunas de status no calendário.
- **Configurações:** Melhorias na interface visual de configurações.
- **Ferramentas:** Criação de novas tarefas no VSCode para compilação automática do pacote AAB.

## Versão 0.14.2

- **Apontamentos:** Adicionada a opção de editar apontamentos já registrados.
- **Sincronização:** Remoção da sincronização completa obrigatória logo após operações de CRUD (otimizando a performance).

## Versão 0.12.1

- **Recuperação:** Criada rotina para recuperação do Banco de Dados (DB).

## Versão 0.12.0 / 0.11.3 / 0.10.0

- **Autenticação:** Criada a opção de obter automaticamente o token de acesso.
- **Builds:** Atualização do número de build para 70.
- **Rede:** Melhoria e refinamento no tratamento de erros de rede na função `is_network_error`.

## Versão 0.7.3

### Correções de Horário

- Correção no bug da data/hora que era exibida de forma divergente (Lester).

### Home Office e Serviços Externos

- Adicionadas sugestões automáticas para marcação de home office e serviços externos.

### Apontamentos Manuais

- Criada a opção de realizar apontamentos de forma manual.
- Implementação de retry automático para apontamentos manuais falhos no Monday.
- Possibilidade de apontar múltiplos intervalos e registrar múltiplos pontos de uma única vez.

### Turnos

- Mudança na lógica e fluxo de criação de turnos.

### Notificações

- Adicionada a funcionalidade de notificações em horário fixo.

## Versão 0.6.2 / 0.6.0

### Integrações

- Integração com as ações de Play/Pause diretamente do Monday.
- Integração com a plataforma Meu RH.
- Integração com a plataforma Clockin.

### UX/UI

- Construção completa do Dashboard e melhorias visuais gerais na interface.

### Sistema

- Melhorias na verificação do estado da internet, acerto nos timers e mudanças nas regras de TTL.
