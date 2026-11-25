# Watery

Aplicação acadêmica da Global Solution CitizenTech 2026.2 para acompanhar a telemetria de um reservatório e administrar pontos monitorados. A interface reúne uma landing page explicativa e um painel conectado à API REST do projeto.

## Integrantes

- Artur de Novazzi Maia — RM 572624
- Bruno Araújo Castro — RM 572723
- Arthur Germano Pinheiro — RM 574042
- João Pedro de Souza — RM 571437
- Artur Nepomuceno Dias Gomes — RM 572626

## Funcionalidades

- Landing page com apresentação do desafio, proposta, integração, decisões de privacidade, impacto e etapas do projeto.
- Painel com leitura atual do reservatório, nível em litros, autonomia, estado e horário da última atualização.
- Tratamento visual para valores indisponíveis e leituras inválidas.
- Consulta e operações de criação, edição e exclusão de pontos monitorados.
- Formulário protegido por autenticação HTTP Basic; a senha é informada na tela e mantida apenas em memória durante a sessão.
- Componentes reutilizáveis, estados de carregamento e erro, navegação responsiva e suporte a movimento reduzido.

## Tecnologias

- React 19 com JSX
- Vite
- Tailwind CSS 4
- ESLint

## Requisitos

- Node.js compatível com a versão de Vite indicada em `package.json`.
- npm.

## Instalação e execução

```bash
npm install
npm run dev
```

Os comandos disponíveis são `npm run dev`, `npm run build`, `npm run lint` e `npm run preview`.

## Integração com a API

A aplicação usa caminhos relativos sob `/reserva/api`. Durante o desenvolvimento, o proxy do Vite encaminha as chamadas para o endereço configurado em `API_PROXY_TARGET`; no deploy, `vercel.json` define o rewrite equivalente.

| Operação | Caminho | Autenticação |
| --- | --- | --- |
| Consultar telemetria | `GET /reserva/api/telemetria/reserva-001` | Pública |
| Consultar histórico de telemetria | `GET /reserva/api/telemetria/reserva-001/historico?limite=50` | Pública |
| Listar pontos | `GET /reserva/api/pontos` | HTTP Basic |
| Criar ponto | `POST /reserva/api/pontos` | HTTP Basic |
| Atualizar ponto | `PATCH /reserva/api/pontos/{id}` | HTTP Basic |
| Excluir ponto | `DELETE /reserva/api/pontos/{id}` | HTTP Basic |

Configure o destino do proxy conforme o ambiente da equipe. Não armazene senha ou credenciais em variáveis `VITE_*`: elas são incorporadas ao código entregue ao navegador. O usuário e a senha da API são digitados no painel e não são persistidos. O contrato, os campos e os detalhes da autenticação estão em [`src/features/painel/services/API.md`](src/features/painel/services/API.md).

## Estrutura do projeto

```text
src/
├── app/                         # Composição e navegação da aplicação
├── features/
│   ├── landing/                  # Página institucional e suas seções
│   │   ├── components/           # Abertura da marca, telemetria e progresso
│   │   ├── sections/             # Blocos editáveis da landing page
│   │   └── styles/               # Estilos da landing page
│   └── painel/                   # Painel, componentes, hooks, API e estilos
└── shared/                      # Componentes e estilos compartilhados
```

### Onde editar a landing page

A ordem das seções e o cabeçalho estão em `src/features/landing/PaginaInicial.jsx`. Edite o texto de cada bloco no arquivo correspondente:

| Bloco | Arquivo |
| --- | --- |
| Abertura e chamada para o painel | `src/features/landing/sections/AberturaApresentacao.jsx` |
| Desafio | `src/features/landing/sections/SecaoDesafio.jsx` |
| Proposta | `src/features/landing/sections/SecaoProposta.jsx` |
| Integração com a API | `src/features/landing/sections/SecaoIntegracaoApi.jsx` |
| Decisões de privacidade | `src/features/landing/sections/SecaoDecisoes.jsx` |
| Impacto e ODS | `src/features/landing/sections/SecaoImpacto.jsx` |
| Etapas do projeto | `src/features/landing/sections/SecaoEtapas.jsx` |
| Chamada final e rodapé | `src/features/landing/sections/RodapeApresentacao.jsx` |

Os estilos desses blocos ficam em `src/features/landing/styles/landing.css`. A abertura animada da marca está em `src/features/landing/components/AberturaMarca.jsx`; a leitura apresentada na landing page está em `VisaoTelemetria.jsx`, e o indicador de progresso está em `ProgressoLeitura.jsx`.

### Organização do painel

- `src/features/painel/PainelComunidade.jsx`: composição da tela do painel.
- `src/features/painel/components/`: medidor, histórico, mensagens, tabela e formulário de pontos.
- `src/features/painel/hooks/`: carregamento e estado de telemetria e pontos monitorados.
- `src/features/painel/services/apiReserva.js`: chamadas HTTP para a API.
- `src/features/painel/styles/dashboard.css`: estilos do painel.

## Verificações

```bash
npm run lint
npm run build
```

As chamadas protegidas dependem de credenciais fornecidas pela equipe e de acesso ao serviço. Consulte a documentação da API antes de validar o CRUD em outro ambiente.

## Contexto acadêmico

O projeto demonstra composição de interface com React, hooks de estado e efeitos, hooks personalizados, separação entre visualização e acesso a dados, integração REST e componentes reutilizáveis. `AI.md` registra o uso de ferramentas de IA no desenvolvimento.
