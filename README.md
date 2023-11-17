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

## Conclusão

O desenvolvimento da aplicação foi realizado com sucesso, atingindo os objetivos iniciais de desenvolvimento. A aplicação foi desenvolvida com foco em dispositivos móveis, porém também pode ser acessada através de computadores, sem perda de funcionalidades. Além das funcionalidades no lado do cliente, o back-end da aplicação também foi desenvolvido com foco em ambientes distribuídos, utilizando serviços de computação em nuvem e apresentando-se de maneira uniforme e coerente para o usuário final, mesmo executando em múltiplos computadores.

## Relatório com as linhas de código

```svelte
<!-- arquivo: src/routes/+page.svelte -->
<script lang="ts">
  import Input from '@/components/forms/Input.svelte'
  import type { ActionData } from './$types'
  import { enhance } from '$app/forms'
  import { fade } from 'svelte/transition'

  export let form: ActionData

  $: error = typeof form?.error === 'string' ? form.error : undefined
</script>

<svelte:head>
  <title>Collect-it | Login</title>
</svelte:head>

<div class="w-full h-screen grid place-items-center">
  <div class="flex flex-col items-center">
    <h1 class="mb-2 text-4xl font-bold tracking-tighter text-green-600">
      Collect-it
    </h1>
    <p class="mb-4 text-center leading-tight">
      Compartilhe pontos de coleta
      <br />
      de lixo recicláveis
    </p>
    <form method="POST" action="?/login" class="mb-4 grid gap-4" use:enhance>
      <Input
        name="username"
        label="Usuário"
        type="text"
        placeholder="Digite seu nome de usuário"
      />
      <Input
        type="password"
        name="password"
        label="Senha"
        placeholder="Digite sua senha"
      />
      <button class="py-2 px-4 bg-green-600 text-white rounded">
        Entrar
      </button>
      {#if error}
        <span in:fade class="text-sm text-red-600 text-center">{error}</span>
      {/if}
    </form>
    <p>
      Não tem uma conta?
      <a class="underline text-green-600" href="/cadastro">Cadastre-se</a>
    </p>
  </div>
</div>
```

```typescript
// arquivo: src/router/+page.server.ts
import { object, string } from 'zod'
import type { Actions } from './$types'
import { db } from '@/db/client'
import { fail, redirect } from '@sveltejs/kit'
import bcrypt from 'bcryptjs'
import crypto from 'node:crypto'
import type { User } from '@prisma/client'

const login = object({
  username: string().max(16),
  password: string().max(255),
})

function generateSessionToken(user: User) {
  return crypto
    .createHash('sha256')
    .update(
      JSON.stringify({
        id: user.id,
        username: user.username,
        email: user.email,
        date: new Date(),
      }),
    )
    .digest('hex')
}

export const actions: Actions = {
  async login({ request, cookies }) {
    const body = Object.fromEntries(await request.formData())

    const result = login.safeParse(body)

    if (!result.success) {
      return fail(400, {
        error: result.error.flatten().fieldErrors,
      })
    }

    const data = result.data

    const user = await db.user.findUnique({
      where: {
        username: data.username,
      },
    })

    if (!user) {
      return fail(400, {
        error: 'Usuário não encontrado',
      })
    }

    const isPasswordValid = await bcrypt.compare(data.password, user.password)

    if (!isPasswordValid) {
      return fail(400, {
        error: 'Senha incorreta',
      })
    }

    const token = generateSessionToken(user)

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
  },
}
```

```svelte
<!-- arquivo: src/routes/cadastro/+page.svelte -->
<script lang="ts">
  import { enhance } from '$app/forms'
  import ImageInput from '@/components/forms/ImageInput.svelte'
  import Input from '@/components/forms/Input.svelte'
  import type { ActionData } from './$types'

  export let form: ActionData

  $: fieldErrors = typeof form?.error === 'object' ? form.error : undefined
  $: actionError = typeof form?.error === 'string' ? form.error : undefined
</script>

<svelte:head>
  <title>Collect-it | Cadastro</title>
</svelte:head>

<div class="w-full h-screen grid place-items-center">
  <div class="flex flex-col items-center">
    <h1 class="mb-2 text-4xl font-bold tracking-tighter text-green-600">
      Cadastro
    </h1>
    <p class="leading-tight text-center mb-4">
      Preencha o formulário<br />para se cadastrar
    </p>
    <form
      method="POST"
      enctype="multipart/form-data"
      action="?/register"
      class="mb-4 grid gap-4"
      use:enhance
    >
      <Input
        name="name"
        label="Nome"
        type="text"
        placeholder="Digite seu nome completo"
        error={fieldErrors?.name?.join(' | ')}
      />
      <Input
        name="username"
        label="Usuário"
        type="text"
        placeholder="Digite seu nome de usuário"
        error={fieldErrors?.username?.join(' | ')}
      />
      <Input
        name="email"
        label="E-mail"
        type="email"
        placeholder="Digite seu e-mail"
        error={fieldErrors?.email?.join(' | ')}
      />
      <Input
        type="password"
        name="password"
        label="Senha"
        placeholder="Digite sua senha"
        error={fieldErrors?.password?.join(' | ')}
      />
      <ImageInput label="Foto de perfil" name="avatar" />
      <button class="py-2 px-4 rounded bg-green-600 text-white">
        Cadastrar
      </button>
      {#if actionError}
        <span class="text-sm text-red-600 text-center">{actionError}</span>
      {/if}
    </form>
    <p>
      Já tem uma conta?
      <a class="underline text-green-600" href="/">Faça login</a>
    </p>
  </div>
</div>
```

```typescript
// arquivo: src/routes/cadastro/+page.server.ts
import { redirect, fail } from '@sveltejs/kit'
import { object, string, instanceof as instanceOf } from 'zod'
import type { Actions } from './$types'
import bcrypt from 'bcryptjs'

import { db } from '@/db/client'
import { avatar } from '@/avatar/client'
import { storage } from '@/storage/client'

const register = object({
  name: string()
    .min(2, { message: 'Nome precisa ter pelo menos 2 caracteres ' })
    .max(255, {
      message: 'Nome pode ter no máximo 255 caracteres',
    }),
  username: string()
    .min(4, { message: 'Usuário precisa ter pelo menos 4 caracteres' })
    .max(16, { message: 'Usuário pode ter no máximo 16 caracteres' })
    .regex(/^[a-z0-9_]+$/i, {
      message: 'Usuário só pode conter letras, números e _',
    }),
  email: string().email({ message: 'E-mail precisa ser válido' }).max(255),
  password: string()
    .min(8, { message: 'Senha precisa ter pelo menos 8 caracteres ' })
    .max(255, {
      message: 'Senha pode ter no máximo 255 caracteres',
    }),
  avatar: instanceOf(File).optional(),
})

export const actions: Actions = {
  async register({ request }) {
    const body = Object.fromEntries(await request.formData())

    const result = register.safeParse(body)

    if (!result.success) {
      return fail(400, {
        error: result.error.flatten().fieldErrors,
      })
    }

    try {
      const data = result.data

      data.password = await bcrypt.hash(data.password, await bcrypt.genSalt())

      const user = await db.user.create({
        data: {
          email: data.email,
          name: data.name,
          username: data.username,
          password: data.password,
          avatarUrl: avatar.getAvatar(data.username),
        },
      })

      if (data.avatar) {
        const fileInfo = await storage.save(
          'avatars',
          `${crypto.randomUUID()}.jpg`,
          await data.avatar.arrayBuffer(),
        )

        await db.user.update({
          where: {
            id: user.id,
          },
          data: {
            avatarUrl: fileInfo.url,
          },
        })
      }
    } catch (err) {
      return fail(400, {
        error: 'Usuário já existe',
      })
    }

    throw redirect(302, '/')
  },
}
```

```svelte
<!-- arquivo: src/routes/app/+page.svelte -->
<script lang="ts">
  import type { PageData } from './$types'

  export let data: PageData
</script>

<svelte:head>
  <title>Collect-it | App</title>
</svelte:head>

<h1 class="text-4xl font-bold tracking-tighter text-green-600">
  Pontos de coleta
</h1>

<p class="mb-4">Veja os pontos de coleta próximos de você.</p>

<div class="mb-4 flex gap-2 items-center">
  <img
    src={data.user.avatarUrl}
    alt={data.user.username}
    class="w-12 h-12 rounded-full object-cover"
  />
  <div>
    <h2 class="leading-none text-lg font-bold tracking-tighter">
      @{data.user.username}
    </h2>
    <p>{data.user.name}</p>
  </div>
</div>

{#if data.points.length > 0}
  <ul class="grid gap-4">
    {#each data.points as point (point.id)}
      <li class="p-4 border rounded">
        <img
          src={point.images[0].url}
          alt={point.name}
          class="mb-4 h-48 w-full object-cover rounded"
        />
        <div class="mb-2 flex gap-1 items-center">
          <a
            href={`/app/pontos/${point.id}`}
            class="text-2xl font-bold tracking-tighter">{point.name}</a
          >
          {#if !point.verified}
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              fill="currentColor"
              class="w-6 h-6 text-blue-600"
            >
              <path
                fill-rule="evenodd"
                d="M8.603 3.799A4.49 4.49 0 0112 2.25c1.357 0 2.573.6 3.397 1.549a4.49 4.49 0 013.498 1.307 4.491 4.491 0 011.307 3.497A4.49 4.49 0 0121.75 12a4.49 4.49 0 01-1.549 3.397 4.491 4.491 0 01-1.307 3.497 4.491 4.491 0 01-3.497 1.307A4.49 4.49 0 0112 21.75a4.49 4.49 0 01-3.397-1.549 4.49 4.49 0 01-3.498-1.306 4.491 4.491 0 01-1.307-3.498A4.49 4.49 0 012.25 12c0-1.357.6-2.573 1.549-3.397a4.49 4.49 0 011.307-3.497 4.49 4.49 0 013.497-1.307zm7.007 6.387a.75.75 0 10-1.22-.872l-3.236 4.53L9.53 12.22a.75.75 0 00-1.06 1.06l2.25 2.25a.75.75 0 001.14-.094l3.75-5.25z"
                clip-rule="evenodd"
              />
            </svg>
          {/if}
        </div>
        <p>{point.address}.</p>
        <p>{point.city} - {point.state}.</p>
        <p>Criado por @{point.user.username}</p>
      </li>
    {/each}
  </ul>
{:else}
  <div class="p-8 text-center border-2 border-dashed rounded text-gray-400">
    <p>Nenhum ponto a ser exibido</p>
  </div>
{/if}
```

```typescript
// arquivo: src/routes/app/+page.server.ts
import { db } from '@/db/client'
import type { PageServerLoad } from './$types'

export const load: PageServerLoad = async ({ locals }) => {
  const user = locals.user!
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

```svelte
<!-- arquivo: src/routes/app/criar/+page.svelte -->
<script lang="ts">
  import ImageInput from '@/components/forms/ImageInput.svelte'
  import Input from '@/components/forms/Input.svelte'

  let images = 1

  function addImages() {
    if (images > 3) {
      return
    }

    images += 1
  }

  function removeImages() {
    if (images <= 1) {
      return
    }

    images -= 1
  }
</script>

<svelte:head>
  <title>Collect-it | Criar ponto</title>
</svelte:head>

<h1 class="mb-2 text-4xl font-bold tracking-tighter text-green-600">
  Criar ponto
</h1>
<p class="mb-4 leading-tight">
  Preencha o formulário para criar um novo ponto de coleta
</p>

<form
  method="POST"
  enctype="multipart/form-data"
  action="?/create"
  class="grid gap-4"
>
  <Input
    name="name"
    type="text"
    label="Nome"
    placeholder="Nome do ponto de coleta"
  />
  <Input
    name="address"
    type="text"
    label="Endereço"
    placeholder="Endereço do ponto de coleta"
  />
  <Input name="city" type="text" label="Cidade" placeholder="Cidade" />
  <Input name="state" type="text" label="Estado" placeholder="Estado" />
  {#each Array.from({ length: images }) as _, index (index)}
    <ImageInput label="Imagem" name="image" />
  {/each}
  <div class="grid grid-cols-2 gap-4 text-gray-800">
    <button
      type="button"
      class="py-2 px-4 border rounded grid place-items-center disabled:bg-gray-100"
      on:click={removeImages}
      disabled={images <= 1}
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="h-4 w-4"
      >
        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 12h-15" />
      </svg>
    </button>
    <button
      type="button"
      class="py-2 px-4 border rounded grid place-items-center disabled:bg-gray-100"
      on:click={addImages}
      disabled={images >= 3}
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="h-4 w-4"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M12 4.5v15m7.5-7.5h-15"
        />
      </svg>
    </button>
  </div>
  <button class="py-2 px-4 bg-green-600 rounded text-white">Criar</button>
</form>
```

```typescript
// arquivo: src/routes/app/criar/+page.server.ts
import {
  object,
  string,
  instanceof as instanceOf,
  array,
  union,
  literal,
} from 'zod'
import type { Actions } from './$types'
import { fail, redirect } from '@sveltejs/kit'
import { db } from '@/db/client'
import { storage } from '@/storage/client'

const STATES = [
  { name: 'Acre', value: 'AC' },
  { name: 'Alagoas', value: 'AL' },
  { name: 'Amapá', value: 'AP' },
  { name: 'Amazonas', value: 'AM' },
  { name: 'Bahia', value: 'BA' },
  { name: 'Ceará', value: 'CE' },
  { name: 'Distrito Federal', value: 'DF' },
  { name: 'Espírito Santo', value: 'ES' },
  { name: 'Goiás', value: 'GO' },
  { name: 'Maranhão', value: 'MA' },
  { name: 'Mato Grosso', value: 'MT' },
  { name: 'Mato Grosso do Sul', value: 'MS' },
  { name: 'Minas Gerais', value: 'MG' },
  { name: 'Pará', value: 'PA' },
  { name: 'Paraíba', value: 'PB' },
  { name: 'Paraná', value: 'PR' },
  { name: 'Pernambuco', value: 'PE' },
  { name: 'Piauí', value: 'PI' },
  { name: 'Rio de Janeiro', value: 'RJ' },
  { name: 'Rio Grande do Norte', value: 'RN' },
  { name: 'Rio Grande do Sul', value: 'RS' },
  { name: 'Rondônia', value: 'RO' },
  { name: 'Roraima', value: 'RR' },
  { name: 'Santa Catarina', value: 'SC' },
  { name: 'São Paulo', value: 'SP' },
  { name: 'Sergipe', value: 'SE' },
  { name: 'Tocantins', value: 'TO' },
] as const

const create = object({
  name: string()
    .min(2, { message: 'Nome deve ter pelo menos 2 caracteres' })
    .max(255, {
      message: 'Nome deve ter no máximo 255 caracteres',
    }),
  address: string()
    .min(2, {
      message: 'Endereço deve ter pelo menos 2 caracteres',
    })
    .max(255, {
      message: 'Endereço deve ter no máximo 255 caracteres',
    }),
  city: string()
    .min(2, {
      message: 'Cidade deve ter pelo menos 2 caracteres',
    })
    .max(255, {
      message: 'Cidade deve ter no máximo 255 caracteres',
    }),
  state: string().max(32),
})

const images = array(instanceOf(File)).min(1)

export const actions: Actions = {
  async create({ request, locals }) {
    const user = locals.user

    if (!user) {
      return fail(400, {
        error: 'Você precisa estar logado para criar um ponto de coleta',
      })
    }

    const form = await request.formData()
    const formResult = create.safeParse(Object.fromEntries(form))

    if (!formResult.success) {
      return fail(400, {
        error: formResult.error.flatten().fieldErrors,
      })
    }

    const point = await db.point.create({
      data: {
        ...formResult.data,
        userId: user.id,
      },
    })

    const filesResult = images.safeParse(Array.from(form.getAll('image')))

    if (!filesResult.success) {
      return fail(400, {
        error: filesResult.error.flatten().fieldErrors,
      })
    }

    const files = filesResult.data

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

    throw redirect(302, '/app')
  },
}
```
