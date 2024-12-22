# ProEduca
ProEduca é uma plataforma de vídeo aula voltada para a educação online, oferecendo uma experiência interativa e acessível para alunos e professores. A plataforma permite a criação, publicação e visualização de conteúdo educacional em vídeo, promovendo o aprendizado a qualquer hora e em qualquer lugar.

# ProEduca - Backend Tasks

## 1. Configuração Inicial

### 1.1. Configuração do ambiente de desenvolvimento
- **Descrição**: O desenvolvedor precisa configurar o ambiente de desenvolvimento backend utilizando Node.js com Express ou Nest.js. O ambiente deve incluir ESLint, Prettier, e ferramentas de teste como Jest. Além disso, o banco de dados relacional (PostgreSQL ou MySQL) será configurado com uma ORM como Prisma ou Sequelize.
- **História**: "A base do backend deve ser sólida, permitindo a fácil adição de novas funcionalidades, a integração com o banco de dados, e garantindo boas práticas de desenvolvimento com linting e formatação automáticos."

### 1.2. Configuração da estrutura do projeto
- **Descrição**: O desenvolvedor organizará a estrutura do projeto seguindo o padrão MVC (Model-View-Controller) ou outra arquitetura como Clean Architecture. Isso ajudará a manter o código modular e fácil de manter. Também será necessário criar rotas básicas e configurar o middleware para lidar com erros, autenticação e CORS.
- **História**: "Uma boa organização do código é essencial para escalar o projeto. Cada parte do sistema terá responsabilidades bem definidas, facilitando o desenvolvimento e a manutenção."

---

## 2. Autenticação e Autorização

### 2.1. Implementação do login
- **Descrição**: O desenvolvedor implementará a lógica de login para o backend. Será necessário criar uma rota POST `/login`, onde o usuário enviará email e senha. O sistema verificará as credenciais no banco de dados, e se estiverem corretas, gerará um token JWT que será retornado ao usuário. Esse token será usado para autenticar futuras requisições.
- **História**: "Quando o usuário envia suas credenciais (email e senha), o backend verifica se estão corretas. Se tudo estiver certo, o sistema gera um token JWT que será utilizado para garantir que o usuário tem permissão para acessar as demais funcionalidades da plataforma."

### 2.2. Implementação do registro
- **Descrição**: O desenvolvedor criará a rota POST `/register`, que permitirá novos usuários se cadastrarem na plataforma. O backend receberá as informações de email, senha e outros dados do usuário, validará e então armazenará no banco de dados. A senha será armazenada utilizando hashing seguro, como bcrypt.
- **História**: "Novos usuários poderão criar suas contas fornecendo email, senha e outras informações relevantes. A senha será armazenada de forma segura para garantir a privacidade e segurança do usuário."

### 2.3. Middleware de autenticação (JWT)
- **Descrição**: O desenvolvedor criará um middleware que verificará a validade do token JWT em cada requisição protegida. Caso o token seja inválido ou ausente, a requisição será negada com uma resposta de erro. O middleware será usado em todas as rotas que exigem autenticação.
- **História**: "Somente usuários autenticados podem acessar certas funcionalidades da plataforma. O middleware verificará se o token JWT presente na requisição é válido e, caso contrário, bloqueará o acesso, garantindo a segurança da plataforma."

---

## 3. Gestão de Cursos

### 3.1. Criação de curso
- **Descrição**: O desenvolvedor criará a rota POST `/courses`, que permitirá aos professores criar novos cursos. A requisição incluirá informações como título, descrição, categoria e outros detalhes. Essas informações serão armazenadas no banco de dados e vinculadas ao professor que criou o curso. Apenas professores autenticados poderão acessar essa rota.
- **História**: "Professores são a chave para a criação de conteúdo na plataforma. Eles poderão criar novos cursos fornecendo detalhes básicos como título, descrição e categoria. Esses cursos serão armazenados e poderão ser acessados pelos alunos."

### 3.2. Listagem de cursos para professores
- **Descrição**: O desenvolvedor implementará a rota GET `/courses/teacher`, que permitirá aos professores visualizar os cursos que eles criaram. A rota retornará uma lista com todos os cursos vinculados ao professor autenticado, incluindo detalhes como progresso de seus alunos e número de inscritos.
- **História**: "Os professores devem ter acesso fácil à lista de cursos que eles criaram. Isso inclui ver quantos alunos estão matriculados e acompanhar o progresso de cada um. Eles poderão gerenciar seus cursos a partir dessa lista."

### 3.3. Listagem de cursos para alunos
- **Descrição**: O desenvolvedor implementará a rota GET `/courses`, que permitirá aos alunos ver todos os cursos disponíveis. A rota retornará uma lista paginada de cursos, permitindo que os alunos encontrem e se inscrevam em novos conteúdos de acordo com suas áreas de interesse.
- **História**: "Os alunos poderão navegar pela lista de cursos disponíveis na plataforma. Eles terão acesso a uma visão clara dos cursos, podendo filtrar por categoria e encontrar novas oportunidades de aprendizado."

---

## 4. Gestão de Aulas

### 4.1. Criação de aula
- **Descrição**: O desenvolvedor criará a rota POST `/courses/:courseId/lessons`, que permitirá aos professores adicionar novas aulas a um curso. Eles enviarão informações como título, descrição e o vídeo da aula (o vídeo será armazenado em um serviço como AWS S3). A aula será vinculada ao curso e ficará disponível para os alunos.
- **História**: "Cada curso é composto por várias aulas. Os professores poderão adicionar novas aulas enviando os vídeos e informações relacionadas. Isso garantirá que o curso esteja sempre atualizado e os alunos possam acompanhar novos conteúdos."

### 4.2. Listagem de aulas para alunos
- **Descrição**: O desenvolvedor criará a rota GET `/courses/:courseId/lessons`, que permitirá aos alunos ver todas as aulas de um curso específico. A resposta incluirá o título da aula, descrição e o progresso do aluno em cada uma delas. Ao clicar na aula, o aluno poderá assistir ao vídeo.
- **História**: "Os alunos terão acesso à lista completa de aulas em cada curso. Eles poderão acompanhar o progresso e escolher a próxima aula a ser assistida, garantindo que não percam nenhum conteúdo importante."

### 4.3. Sistema de acompanhamento de progresso
- **Descrição**: O desenvolvedor implementará uma funcionalidade para rastrear o progresso dos alunos em cada aula. A rota PATCH `/courses/:courseId/lessons/:lessonId/progress` será criada para atualizar o status de uma aula (iniciada, em andamento, concluída) no banco de dados.
- **História**: "Os alunos precisam acompanhar seu progresso ao longo do curso. Isso permitirá que eles vejam quais aulas já assistiram, quais estão em andamento e quanto falta para completar o curso."

---

## 5. Funcionalidades Adicionais

### 5.1. Sistema de avaliações interativas (quizzes)
- **Descrição**: O desenvolvedor criará uma rota POST `/lessons/:lessonId/quizzes`, que permitirá que os professores adicionem quizzes a uma aula. A rota POST `/lessons/:lessonId/answers` será criada para que os alunos enviem suas respostas. O backend verificará as respostas e retornará o resultado do quiz ao aluno.
- **História**: "Ao final de uma aula, os alunos podem reforçar o que aprenderam respondendo a quizzes. O professor poderá criar essas perguntas diretamente no backend, e o sistema validará as respostas, dando feedback ao aluno."

### 5.2. Sistema de comentários
- **Descrição**: O desenvolvedor implementará um sistema de comentários para as aulas. A rota POST `/lessons/:lessonId/comments` será criada para que os alunos possam enviar perguntas e comentários sobre a aula. Professores poderão moderar esses comentários.
- **História**: "A interação entre alunos e professores é fundamental para o aprendizado. O sistema de comentários permitirá que os alunos façam perguntas e compartilhem suas dúvidas, e os professores poderão moderar e responder esses comentários."

### 5.3. Emissão de certificados
- **Descrição**: O desenvolvedor criará a lógica para a emissão de certificados. Após a conclusão de um curso, uma rota POST `/courses/:courseId/certificate` será criada para gerar o certificado do aluno. O backend gerará o PDF com os dados do aluno e o curso concluído, permitindo que o aluno faça o download ou receba por email.
- **História**: "Ao final do curso, os alunos receberão um certificado que comprova a conclusão. O backend gerará um arquivo PDF personalizado com o nome do aluno e detalhes do curso, pronto para ser baixado ou enviado por email."


---
# ProEduca - Frontend Tasks

## 1. Configuração Inicial

### 1.1. Configuração do ambiente de desenvolvimento
- **Descrição**: O desenvolvedor precisa configurar o ambiente de desenvolvimento frontend utilizando React.js (ou Next.js, se for uma SPA com SSR). Ele configurará o Vite ou Webpack para empacotar o código e o ESLint para garantir boas práticas. Também será necessário configurar o controle de versão e o ambiente de estilo com `styled-components` ou `CSS Modules`.
- **História**: "Todo projeto frontend precisa de uma base sólida. O ambiente precisa estar pronto para escalar conforme novas funcionalidades são adicionadas. Ele deve garantir uma boa performance no desenvolvimento e garantir a consistência do código com ferramentas de linting."

### 1.2. Integração com o backend (API)
- **Descrição**: O desenvolvedor configurará a comunicação com o backend utilizando Axios ou Fetch. Todas as chamadas à API serão abstraídas em um serviço para facilitar o reuso e centralizar as requisições. Isso incluirá configurações de timeout, interceptores de erro e tokens de autenticação.
- **História**: "A comunicação com o backend é o ponto central de uma aplicação frontend. Ela precisa ser eficiente e segura, lidando com erros de forma clara e usando tokens para garantir a autenticidade do usuário."

---

## 2. Autenticação e Autorização

### 2.1. Tela de Login
- **Descrição**: O desenvolvedor criará a tela de login. Nesta tela, o usuário irá inserir o seu email e senha. Após clicar no botão 'Login', uma requisição será enviada para a API de autenticação do backend. Se as credenciais estiverem corretas, o usuário será redirecionado para o dashboard. Se houver erros, uma mensagem amigável será exibida. A interface deve ser simples e intuitiva, com validação em tempo real dos campos (email válido, senha mínima de 8 caracteres).
- **História**: "O usuário abrirá a plataforma e verá os campos para email e senha. Ao preencher as informações e clicar em 'Login', ele será autenticado e redirecionado para sua área de trabalho, onde poderá acessar as funcionalidades de acordo com seu papel."

### 2.2. Tela de Registro
- **Descrição**: O desenvolvedor criará a tela de registro de novos usuários. Nessa página, o usuário irá preencher informações como nome, email, senha e confirmação de senha. A senha deve ser validada em relação à sua força (mínimo de 8 caracteres, combinação de números e letras). Ao submeter o formulário, uma requisição será enviada para o backend e, caso o registro seja bem-sucedido, o usuário será redirecionado para a página de login.
- **História**: "Novos usuários que queiram se cadastrar na plataforma precisam preencher um formulário simples. Assim que clicarem em 'Registrar', suas informações são validadas e, se estiver tudo correto, eles poderão fazer login."

### 2.3. Proteção de rotas
- **Descrição**: Nesta tarefa, o desenvolvedor implementará a lógica de proteção de rotas. Algumas páginas serão acessíveis apenas para usuários autenticados. Ao tentar acessar uma página protegida sem estar logado, o usuário será redirecionado para a tela de login. Para isso, será necessário verificar o token JWT em cada requisição.
- **História**: "Nem todas as páginas estão disponíveis para todos. Se o usuário não estiver logado e tentar acessar algo restrito, ele será redirecionado imediatamente para a página de login."

---

## 3. Dashboard

### 3.1. Tela de dashboard para Aluno
- **Descrição**: O desenvolvedor criará o dashboard que será exibido ao aluno após o login. Essa tela exibirá os cursos em andamento e cursos recomendados. Para cada curso, haverá uma barra de progresso indicando o quanto o aluno já completou. O aluno poderá clicar no curso para ver as aulas disponíveis e continuar de onde parou.
- **História**: "O aluno deve se sentir à vontade ao entrar na plataforma. Seu progresso será destacado, mostrando quanto ele já avançou em cada curso, e novas oportunidades de aprendizado serão sugeridas com base em seu histórico."

### 3.2. Tela de dashboard para Professor
- **Descrição**: O desenvolvedor criará o dashboard para os professores. Nesse dashboard, o professor poderá ver a lista de cursos que ele criou, visualizar as aulas dentro de cada curso, e acessar relatórios de progresso de seus alunos. Haverá um botão 'Criar Novo Curso', que redirecionará o professor para o formulário de criação de curso.
- **História**: "O professor deve ter uma visão clara de seus cursos e alunos. Ele precisa acompanhar como cada aluno está se saindo, além de poder facilmente criar novos cursos para continuar contribuindo para a plataforma."

---

## 4. Gestão de Conteúdo

### 4.1. Tela de criação de curso
- **Descrição**: Nesta tela, o professor poderá criar um novo curso. Ele precisará preencher um formulário com o título do curso, a descrição e a categoria. Haverá um botão de 'Adicionar Aula', onde o professor poderá vincular aulas ao curso. Ao finalizar a criação, o curso será salvo no banco de dados e aparecerá no dashboard do professor.
- **História**: "Professores são os principais criadores de conteúdo na plataforma. Para criar um curso, eles simplesmente preenchem o título, a descrição e escolhem a categoria. Ao final, podem começar a adicionar as aulas e o curso ficará disponível para os alunos."

### 4.2. Tela de criação de aulas
- **Descrição**: O desenvolvedor implementará a tela onde o professor pode adicionar novas aulas ao curso. Ele fará o upload de um vídeo e preencherá campos com o título da aula e sua descrição. Ao clicar em 'Salvar', a aula será vinculada ao curso e os alunos poderão assisti-la. O vídeo será hospedado em um serviço de armazenamento externo (como AWS S3).
- **História**: "Cada aula é uma peça chave do aprendizado. O professor carrega o vídeo diretamente para a plataforma e adiciona informações como título e descrição, facilitando para os alunos entenderem o que será abordado."

### 4.3. Tela de visualização de curso (Aluno)
- **Descrição**: Esta tela permitirá que os alunos vejam todos os detalhes de um curso. O aluno verá a lista de aulas disponíveis e poderá clicar em qualquer uma para assisti-la. A interface exibirá o progresso do aluno e destacará as aulas que ele já completou.
- **História**: "Ao abrir um curso, o aluno verá toda a estrutura de aulas disponíveis e poderá assistir a qualquer uma, continuando de onde parou. Isso ajuda na organização e motiva o aluno a completar o curso."

---

## 5. Funcionalidades Interativas

### 5.1. Sistema de avaliações interativas (quizzes)
- **Descrição**: O desenvolvedor criará a interface para quizzes. Após assistir a uma aula, o aluno poderá responder a perguntas relacionadas ao conteúdo. A interface do quiz deve ser simples, exibindo uma pergunta por vez, com opções de múltipla escolha. Ao final do quiz, o aluno receberá o feedback de seu desempenho.
- **História**: "Ao final de cada aula, o aluno será desafiado com um quiz. Isso reforça o conteúdo aprendido e ajuda o professor a medir o nível de compreensão do aluno."

### 5.2. Comentários em aulas
- **Descrição**: O desenvolvedor criará uma seção de comentários na página da aula, onde os alunos poderão fazer perguntas ou deixar observações sobre o conteúdo. Os comentários serão moderados, e o professor poderá responder ou excluir comentários. A interface deve ser clara e intuitiva, com suporte para respostas em threads.
- **História**: "Alunos poderão interagir com professores e colegas deixando comentários em cada aula. Essa troca de ideias e perguntas enriquece a experiência de aprendizado e promove um ambiente colaborativo."

### 5.3. Certificados
- **Descrição**: O desenvolvedor criará a interface para a emissão de certificados. Após completar um curso, o aluno poderá acessar um botão 'Emitir Certificado'. Ao clicar, o certificado será gerado e exibido na tela, com a opção de download ou envio por email. A interface deve ser simples e funcional, com o layout do certificado predefinido.
- **História**: "Ao final de um curso, o aluno receberá um certificado de conclusão. Ele poderá fazer o download diretamente da plataforma, garantindo uma prova concreta de seu aprendizado."

---

## Ordem de Desenvolvimento

### Backend:
1. Configuração Inicial (1.1 - 1.2)
2. Autenticação e Autorização (2.1 - 2.2)
3. Gestão de Usuários (3.1 - 3.2)
4. Gestão de Conteúdo (4.1 - 4.3)
5. Funcionalidades Interativas (5.1 - 5.4)
6. Pagamentos (6.1 - 6.2)
7. Segurança e Monitoramento (7.1 - 7.2)
8. Testes e Deploy (8.1 - 8.2)

### Frontend:
1. Configuração Inicial (1.1 - 1.2)
2. Autenticação e Autorização (2.1 - 2.2)
3. Interface de Usuário (3.1 - 3.4)
4. Gestão de Cursos e Aulas (4.1 - 4.3)
5. Funcionalidades Interativas (5.1 - 5.3)
6. Sistema de Pagamento (6.1 - 6.2)
7. Design Responsivo (7.1)
8. Testes e Deploy (8.1 - 8.2)

