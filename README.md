# Plano de desenvolvimento

O objetivo para a aplicação era a construção uma interface web, acessível de todos os dispositivos, porém com foco em dispositivos móveis, para que o usuário possa realizar o cadastro dos pontos de coleta de lixo reciclável, e também para que o usuário possa visualizar e criar reviews para os pontos de coleta de lixo cadastrados.

Para que isso fosse possível, iniciamos pela modelagem das tabelas de um banco de dados, mapeando as entidades e os relacionamentos. Sabendo da criação dos pontos de coletas e review, iniciamos com suas respectivas tabelas.

Para a tabela de usuários escolhemos armazenar os seguintes campos, id, nome, usuário, e-mail, senha, url do avatar e datas para controle do banco de dados. A descrição da tabela de usuários pode ser encontrada abaixo.

| Campo      | Tipo         | Descrição                      |
| ---------- | ------------ | ------------------------------ |
| id         | integer      | Identificador único do usuário |
| name       | text         | Nome do usuário                |
| username   | text (único) | Nome de usuário para login     |
| email      | text (único) | Email do usuário               |
| password   | text         | Senha do usuário               |
| avatar_url | text         | URL da imagem do usuário       |
| created_at | timestamp    | Data de criação do usuário     |
| updated_at | timestamp    | Data de atualização do usuário |

Com relação a tabela de pontos de coleta, armazenamos as informações de id, nome do ponto de coleta, endereço, cidade, estado, id do usuário, datas para controle e um valor booleano de "verificado" para exibir um selo para o usuário de que o ponto de coleta é válido. Os campos da tabela são apresentados abaixo.

| Campo      | Tipo      | Descrição                                                |
| ---------- | --------- | -------------------------------------------------------- |
| id         | integer   | Identificador único do ponto de coleta                   |
| name       | text      | Nome do ponto de coleta                                  |
| address    | text      | Endereço do ponto de coleta                              |
| city       | text      | Cidade do ponto de coleta                                |
| state      | text      | Estado do ponto de coleta                                |
| verified   | boolean   | Indica se o ponto de coleta foi verificado               |
| user_id    | integer   | Identificador do usuário que cadastrou o ponto de coleta |
| created_at | timestamp | Data de criação do ponto de coleta                       |
| updated_at | timestamp | Data de atualização do ponto de coleta                   |

Por último, a tabela de reviews, que armazena as informações de id, id do usuário, id do ponto de coleta, nota, comentário e datas para controle.

| Campo      | Tipo      | Descrição                                   |
| ---------- | --------- | ------------------------------------------- |
| id         | integer   | Identificador único da review               |
| user_id    | integer   | Identificador do usuário que criou a review |
| point_id   | integer   | Identificador do ponto de coleta da review  |
| rating     | integer   | Nota da review                              |
| comment    | text      | Comentário da review                        |
| created_at | timestamp | Data de criação da review                   |
| updated_at | timestamp | Data de atualização da review               |

No final da modelagem, adicionamos outras tabelas que seriam necessárias para uma aplicação web, como a tabela de sessões e tabelas que armazenam arquivos relacionados as entidades principais da aplicação. A modelagem final é representada na imagem abaixo.

![Modelagem do banco de dados](images/aps-8-sem.png)

Com a definição do banco de dados, iniciamos a prototipação das telas da aplicação. Inicialmente com a ideia de fazer formulários de login e cadastro, contendo os campos definidos nas tabelas. O objetivo de cada tela é reduzir o máximo de quantidade de informação, para que o usuário não se sinta sobrecarregado com muitas informações. As telas de login e cadastro podem ser vistas abaixo.

| Login                      | Cadastro                         |
| -------------------------- | -------------------------------- |
| ![Login](images/login.png) | ![Cadastro](images/cadastro.png) |

Definidos os conceitos iniciais da interface gráfica inicializamos o desenvolvimento de provas de conceito da aplicação. Inicialmente com o desenvolvimento de páginas estáticas, para realizar a conexão com um back-end posteriormente. As duas primeiras páginas desenvolvidas foram login e cadastro, seguindo o padrão definido nos wireframes iniciais. As páginas podem ser vistas abaixo.

| Login                             | Cadastro                                |
| --------------------------------- | --------------------------------------- |
| ![Login](images/login-final.jpeg) | ![Cadastro](images/cadastro-final.jpeg) |

Continuamos o desenvolvimento definindo a página inicial e a página de cadastro de pontos de coleta. A página inicial foi desenvolvida com o objetivo de apresentar os pontos de coleta cadastrados, com informações gerais a respeito do ponto. A página de cadastro de pontos de coleta foi desenvolvida com o objetivo de permitir que o usuário possa cadastrar um ponto de coleta, adicionando imagens e definindo os campos de endereço, cidade e estado. As páginas podem ser vistas abaixo.

| Página inicial                  | Cadastro de ponto                                   |
| ------------------------------- | --------------------------------------------------- |
| ![Home](images/home-final.jpeg) | ![Cadastro de ponto](images/criar-ponto-final.jpeg) |

Prosseguimos o desenvolvimento com o desenvolvimento da página que detalha as informações dos pontos de coleta, nela apresentamos as imagens cadastradas no formulário anterior e as informações em mais detalhes, além das reviews criadas por usuários da aplicação. A imagem abaixo mostra o resultado final do desenvolvimento.

| Detalhes do ponto de coleta          |
| ------------------------------------ |
| ![Detalhes](images/ponto-final.jpeg) |

Por último, criamos uma página onde o usuário pudesse alterar as informações do seu perfil, como nome, e-mail e senha, além de um botão que permitisse que o usuário saísse da sua conta atual.

| Alterar perfil                              |
| ------------------------------------------- |
| ![Alterar perfil](images/perfil-final.jpeg) |

## Projeto

O projeto foi desenvolvido utilizando a linguagem de programação TypeScript com o framework SvelteKit para construção de interfaces gráficas. A utilização do SvelteKit possibilitou a criação de uma aplicação no lado do servidor sem utilização de estruturas intermediárias de comunicação, como APIs REST. O framework utiliza padrões de comunicações da web para facilitar a comunicação entre o cliente e o servidor, como envio de formulários ao invés de JSON e a utilização de cookies para armazenar informações de sessão. Com isso, muitas informações do estado da aplicação são armazenados em uma única fonte, facilitado a manutenção e a criação de funcionalidades.

Além do SvelteKit fornecer uma melhor experiência de desenvolvimento, ele também possibilita a implantação de aplicações desenvolvidas com ele em diferentes cenários, em especial, em ambientes de computação em nuvem. Para a implantação da aplicação, utilizamos o serviço de hospedagem de aplicações da Vercel, que permite a implantação de aplicações desenvolvidas com SvelteKit de forma gratuita, executando as diferentes rotas em ambiente serverless.

Após a definição do framework que seria utilizado, também definimos outros pontos que seriam cruciais para o funcionamento da aplicação em um ambiente distribuído, como o banco de dados e o sistema de armazenamento de arquivos.

Para o armazenamento dos dados da aplicação, utilizamos o MySQL como banco de dados relacional, que também foi hospedado em um ambiente de computação em nuvem. Utilizamos a plataforma Planet Scale, que possibilita a configuração de um banco de dados MySQL distribuído, com alta disponibilidade e escalabilidade, executando nós do banco de dados através do Vitess.

A aplicação conta com armazenamento de arquivos de imagem, como avatares de usuários e imagens de pontos de coleta, que são armazenados em um serviço de armazenamento de objetos da Vercel, que também é gratuito. O esse serviço é baseado no Amazon Simple Storage System, que armazena arquivos em buckets, que são agrupamentos de arquivos. Para cada arquivo armazenado, é gerado um link de acesso público, que pode ser utilizado para acessar o arquivo posteriormente, como na exibição de imagens.

Com os serviços de armazenamento de dados e arquivos definidos, iniciamos o desenvolvimento da aplicação final, sendo as primeiras páginas a serem integradas com o back-end as rotas de login e cadastro. Ambas possuindo ações no back-end suas respectivas ações. A rota de login realiza a autenticação do usuário, verificando se o usuário existe e se a senha informada é válida. A rota de cadastro realiza a criação de um novo usuário, verificando se o usuário já existe e se o e-mail informado já está sendo utilizado por outro usuário. Em ambas adicionamos o detalhe de segurança de gerar uma hash da senha original para ser salvo no banco de dados.

A rota de login conta com a criação de uma sessão de usuário, que é um token salvo pelo navegador através de cookies. A sessão é criada através de um hash gerado pelo back-end, que é salvo no banco de dados e enviado para o navegador. O navegador salva o token em um cookie, que é enviado em todas as requisições subsequentes para o back-end, permitindo que o back-end identifique o usuário que está realizando a requisição. A sessão permite a identificação do usuário para o back-end e é utilizada para atribuir pontos de coleta e reviews para o respectivo criador da entidade.

```typescript
// Consulta o usuário no banco de dados através do seu usuário
const user = await db.user.findUnique({
  where: {
    username: data.username,
  },
})

// Em caso de um usuário não encontrado, é retornado
// para o cliente a mensagem de erro.
if (!user) {
  return fail(400, {
    error: 'Usuário não encontrado',
  })
}

// Compara o hash da senha salva no banco
// com a senha do usuário encontrado
const isPasswordValid = await bcrypt.compare(data.password, user.password)

// Em caso de uma senha inválida, é retornado
// para o cliente a mensagem de erro.
if (!isPasswordValid) {
  return fail(400, {
    error: 'Senha incorreta',
  })
}

// Nos casos onde o usuário é encontrado e a senha é válida,
// é gerado um token de sessão para o usuário.
const token = generateSessionToken(user)

// O token é salvo no banco de dados e é enviado
// um cookie com um redirecionamento para a página
// inicial da aplicação.
await db.session.create({
  data: {
    token,
    userId: user.id,
  },
})

cookies.set('token', token, {
  path: '/',
  httpOnly: true,
})

throw redirect(302, '/app')
```

As rotas da página inicial e do ponto de coleta foram desenvolvidas após isso, por se tratarem de rotas que apenas realizam consulta no banco de dados, não sendo necessário a criação de sessões ou ações de criação de entidades. A rota da página inicial realiza a consulta de todos os pontos de coleta cadastrados, retornando as informações necessárias para a exibição na página. A rota do ponto de coleta realiza a consulta de um ponto de coleta específico, retornando o ponto de coleta e as reviews cadastradas para ele.

```typescript
export const load: PageServerLoad = async ({ locals }) => {
  // O usuário é carregado através do token de sessão
  const user = locals.user

  // Os pontos de coleta são carregados através de uma consulta
  // ao banco de dados, incluindo as imagens e as informações
  // seguras do usuário que criou um respectivo ponto.
  const points = await db.point.findMany({
    orderBy: {
      createdAt: 'desc',
    },
    include: {
      user: {
        select: {
          id: true,
          username: true,
          avatarUrl: true,
        },
      },
      images: {
        select: {
          id: true,
          url: true,
        },
      },
    },
  })

  // É retornado para a montagem da página
  // o usuário autenticado e os pontos de
  // coleta.
  return {
    user: {
      id: user.id,
      name: user.name,
      username: user.username,
      email: user.email,
      avatarUrl: user.avatarUrl,
    },
    points,
  }
}
```

Com isso, adicionamos as páginas responsáveis por criação de pontos de coleta e alteração de perfil, ambas contando com ações para criação e alteração de entidades. A rota de criação de pontos de coleta realiza a criação de um novo ponto de coleta, salvando as imagens enviadas pelo usuário e criando um registro no banco de dados. A rota de alteração de perfil realiza a alteração das informações do usuário, como nome, e-mail e senha, além de permitir que o usuário altere a sua imagem de avatar. Abaixo é mostrado um trecho de código da função que executa a criação de um novo ponto de coleta.

```typescript
async function create({ request, locals }) {
  // O usuário é carregado através do token de sessão
  const user = locals.user

  // Caso o usuário não esteja autenticado, é retornado
  // para o cliente a mensagem de erro.
  if (!user) {
    return fail(400, {
      error: 'Você precisa estar logado para criar um ponto de coleta',
    })
  }

  // O formulário enviado pelo cliente é carregado
  // e é validado através de um schema.
  const form = await request.formData()
  const formResult = create.safeParse(Object.fromEntries(form))

  // Caso o formulário não seja válido, é retornado
  // para o cliente o erro com detalhes a respeito
  // dos campos inválidos.
  if (!formResult.success) {
    return fail(400, {
      error: formResult.error.flatten().fieldErrors,
    })
  }

  // O ponto de coleta é criado no banco de dados
  // com as informações do formulário e o usuário
  // autenticado.
  const point = await db.point.create({
    data: {
      ...formResult.data,
      userId: user.id,
    },
  })

  // As imagens enviadas pelo cliente validadas através de um schema.
  const filesResult = images.safeParse(Array.from(form.getAll('image')))

  // Caso as imagens não sejam válidas, é retornado
  // para o cliente o erro com detalhes a respeito
  // dos campos inválidos.
  if (!filesResult.success) {
    return fail(400, {
      error: filesResult.error.flatten().fieldErrors,
    })
  }

  const files = filesResult.data

  // As imagens são salvas no serviço de armazenamento
  // de arquivos e são criados registros no banco de
  // dados para cada imagem.
  const paths = await Promise.all(
    files.map(async (file) =>
      storage.save(
        'points',
        `${crypto.randomUUID()}-${file.name}.jpg`,
        await file.arrayBuffer(),
      ),
    ),
  )

  await Promise.all(
    paths.map((path) =>
      db.pointImage.create({
        data: {
          url: path.url,
          pointId: point.id,
        },
      }),
    ),
  )

  // É retornado para o cliente o redirecionamento
  // para a página inicial da aplicação, para que
  // ele possa visualizar o ponto de coleta criado.
  throw redirect(302, '/app')
}
```

Ao final do desenvolvimento, foram realizadas as implantações em ambiente de produção de cada peça do sistema, para validar o funcionamento do conjunto completo da aplicação. Como comentado anteriormente, o serviço foi implantado na Vercel, que atribuiu um domínio público para que qualquer usuário pudesse acessar a aplicação.

A url da aplicação é https://aps-8-sem.vercel.app, e a aplicação pode ser acessada através de qualquer navegador, em qualquer dispositivo, como computadores, tablets e smartphones, satisfazendo assim o objetivo inicial de desenvolvimento de uma aplicação acessível de clientes mobile.
