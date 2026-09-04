# Changelog — Simple Monday

## Versão 0.30.3

### Novidades

- **Linux:** “Manter-me conectado” com autenticação do sistema (PolicyKit ou fallback zenity/PAM).
- Builds **Windows / Android / Linux** passam a rodar a suite de testes unitários antes de compilar.

### Melhorias

- Helper do **Windows Hello** empacotado no build PyInstaller (e resolvido corretamente no app compilado).
- Credenciais Supabase embutidas no build Windows a partir do `.env` (igual APK/Linux).
- Site: removido aviso de teste fechado / grupo Google; secção de recursos com agenda do celular e apontamento/ponto locais.

### Correções

- Subitens sem duração no Monday passam a aparecer no apontamento (API interna omite colunas vazias — o app completa a partir dos metadados do board).

## Versão 0.30.2

### Melhorias

- Fluxo de compra Play (cartão e Pix): confirmação/`acknowledge` no servidor para o Premium não cair após o prazo do Google.
- Banner de plano gratuito no calendário atualiza ao ativar o Premium (sem precisar reiniciar o app).
- Mensagens mais claras enquanto a compra está a ser verificada / Pix pendente.

### Correções

- Tratamento de erro ao atualizar entitlements na conta.
- Reconhecimento de assinaturas Play mais robusto no backend (RTDN / verify-play-purchase).

## Versão 0.30.0

### Novidades

- Conta **Simple Monday** (e-mail/senha e Google): login, registo e sessão persistente.
- Planos **Free / Premium** com Google Play Billing, restauro de compras e sincronização de entitlements (Supabase).
- **Windows Hello** e biometria/PIN no Android para “Manter-me conectado”.
- Anúncios (AdMob) no plano free, com gate antes de sync forçado.

### Melhorias

- Configurações → Conta: estado do plano, assinar/restaurar e gestão da sessão.
- Organização e onboarding alinhados ao fluxo de autenticação.

## Versão 0.29.0

### Novidades

- Monday **sem obrigatoriedade do token** da API pública: basta e-mail e senha da conta Monday (API interna) para sincronizar, apontar e usar o relógio.
- Fluxo de ligação ao Monday simplificado — o token público passa a ser opcional.

### Melhorias

- App passa a funcionar de forma estável só com a API interna do Monday (sem depender da GraphQL pública).

## Versão 0.27.1

### Correções

- Ajuste fino na shell após a divisão do módulo de calendário.

## Versão 0.27.0

### Melhorias

- Calendário e settings **divididos em módulos** (UI e serviços), com manutenção e builds mais estáveis.
- Serviço de calendário e de settings reorganizados (`services/calendar/*`, `services/settings/*`).

## Versão 0.26.0

### Novidades

- Diagnóstico e testes de performance na troca de dia no calendário.
- Loading em ecrã completo mais consistente na arranque e autenticação de fluxos.

### Melhorias

- Calendário mais responsivo (menos trabalho na thread da UI ao mudar de dia).
- Rede: detecção de erros de rede refinada.
- QR / organização: melhorias no serviço de leitura e configuração.

### Correções

- Estabilidade geral na shell e no calendário após as otimizações de 0.25.x.

## Versão 0.24.0

### Novidades

- Configurações → Ponto: feriados, pontos salvos, sugestões de justificativa, turnos, horário do ponto e ciclo/meta de horas passam a abrir em **subpáginas** a partir de cards clicáveis (lista principal mais limpa).
- Alerta de batida ímpar no calendário vira **badge** no canto superior direito do dia (ícone sem fundo, sobre a quina da borda).

### Melhorias

- Banner de sync: padding à esquerda no loading para o anel não ficar cortado.
- Relógio de horas trabalhadas mais estável (menos engasgos / pulos de segundos).
- Perfil: card da conta em linha expansível com nome, ID e slug em linhas internas.
- Alertas visuais reposicionados acima de ciclo/meta de horas.

### Correções

- Android: “Justificar local” no menu do dia abre o modal de forma confiável (não engole o diálogo ao fechar o PopupMenu).
- Justificativa local: inserir/remover só atualiza a UI — sem disparar sync de endpoints.
- ICS/Teams: respeita o TTL como as outras integrações; ao abrir, só sincroniza (e mostra o banner) se o cache estiver vencido.
- Logo do modal Sobre passa a aparecer também no APK (resolução de assets no layout Flet `path=src`).

## Versão 0.23.6

### Correções

- Calendário ICS e agenda do celular deixam de depender de flags no SQLite: a conexão passa a seguir o secure storage (como as outras credenciais), evitando aparecer “desconectado” após recriação/atualização do banco.
- ICS: conectado = URL presente no secure storage; agenda Android: flag `android_calendar_enabled` também no secure storage, com migração automática do valor legado.

## Versão 0.23.5

### Correções

- Calendário Teams/Outlook (ICS): reuniões recorrentes com o mesmo `UID` deixam de falhar na sincronização (`UNIQUE constraint failed`).
- Ocorrências da série passam a aparecer corretamente no mês — tanto quando o Outlook já expande as instâncias quanto quando envia só o evento mestre com `RRULE` (com suporte a `EXDATE` e `RECURRENCE-ID`).

## Versão 0.21.1

### Novidades

- Configurações usam a **pilha de Views** do Flet: o botão/gesto voltar do Android retorna à tela anterior (subpágina → menu → abas) em vez de fechar o app.
- **Catálogo local** em Configurações → Apontamentos: criar e renomear workspace, board, status, tarefas e subelementos (aparecem ao apontar sem precisar de apontamento prévio).
- Filtro workspace/board/status no **apontamento** também para destino Local.
- Filtro workspace/board/status no **iniciar relógio** para Monday e Local.


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
