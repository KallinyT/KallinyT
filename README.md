# UniJornal 📚

## 📖 Descrição do aplicativo Unijornal

O **UniJornal** é voltado para amantes de informações do campus **Unifucamp**. Um aplicativo intuitivo, onde os usuários têm acesso às mais novas notícias de tudo que acontece na universidade.

O app oferece:

- Um **feed de notícias** com as atualizações mais recentes organizadas por blocos.
- Opção de **selecionar notícias específicas** para ver mais detalhes.
- **Busca personalizada** para encontrar notícias sobre temas de interesse.

### 🧭 Navegação

- **Tela Inicial:** Exibe todas as notícias por blocos, com títulos chamativos e um campo de busca.
- **Tela de Detalhes:** Ao selecionar uma notícia, o usuário é direcionado para uma nova página contendo a matéria completa, com **data, autor e imagem ilustrativa**.

---

## 🛠️ Funcionalidades Implementadas

- Consumo de dados via **API pública** utilizando **Retrofit**.
- Persistir dados da API da Fipe no banco local do Android usando **Room**, permitindo
**consultas e reutilização offline**
- Exibição de imagens com **Glide**.
- Interface construída com **ConstraintLayout**.
- Arquitetura baseada em **MVVM**, garantindo uma navegação fluida e uma experiência de usuário intuitiva.

---
## 📍 Diagrama UML

### Diagrama de caso de uso
Decidimos construir um diagrama de caso de uso para fornecer aos stakeholders uma visão de quais funcionalidades os usuários tem sobre o nosso aplicativo. Como visualizar notícias, buscar conteúdos específicos e acessar os detalhes das matérias.
<img width="785" height="904" alt="Image" src="https://github.com/user-attachments/assets/0b657c4f-76ee-4eb0-9f38-58ccd6e65732" />

---

## 📱 Capturas de Telas

### Tela principal (Feed de Notícias):
![Image](https://github.com/user-attachments/assets/1068d077-7815-4047-8f64-5fc5f5932be7)

### Tela com Filtro de Busca:
![Image](https://github.com/user-attachments/assets/4f9acb6d-c3d5-4bf2-a712-0a6a27f4f89f)

### Tela de Detalhe da Notícia:
![Image](https://github.com/user-attachments/assets/2e9ce6ee-01eb-464b-9254-9d63fb41aeaf)

---

## ⚙️ Decisões Técnicas

O **UniJornal** foi desenvolvido com foco em **praticidade, fluidez** e **boa experiência do usuário**, especialmente para os estudantes da **Unifucamp**. A seguir, destacamos as principais decisões técnicas e tecnologias utilizadas no projeto:

### 🧪 Tecnologias Utilizadas

-   **Kotlin**: Linguagem moderna e concisa, utilizada para todo o desenvolvimento nativo Android do aplicativo.
    
-   **Android Studio**: Ambiente de desenvolvimento oficial para Android, utilizado para codificação, testes e emulação do app.
    
-   **Glide**: Biblioteca utilizada para carregamento e cache eficiente de imagens, garantindo uma boa performance no feed de notícias.
    
-   **Room (DAO)**: Implementação de banco de dados local com persistência usando **DAO (Data Access Object)**, permitindo acesso offline às notícias consultadas anteriormente.
    
-   **Retrofit**: Biblioteca de cliente HTTP usada para realizar o consumo da API pública de notícias, com suporte à conversão automática de dados JSON.
    
-   **MVVM (Model-View-ViewModel)**: Arquitetura adotada para garantir separação de responsabilidades, facilitando a manutenção do código e promovendo escalabilidade do projeto.
    

### 📐 Boas Práticas Adotadas

-   Organização em **camadas (Model, View e ViewModel)** para facilitar testes, manutenções e expansões futuras.
    
-   Uso de **LiveData** para comunicação reativa entre ViewModel e a interface do usuário.
    
-   Utilização de **ConstraintLayout** para garantir uma interface adaptável a diferentes tamanhos de tela.
    
-   Implementação de **tratamento de erros** e **validação de estados de rede** para garantir estabilidade e boa experiência mesmo em condições adversas.
    
## 🗂️ Estrutura de Arquivos do Projeto

O projeto está estruturado de forma modular, seguindo os princípios da arquitetura **MVVM (Model-View-ViewModel)** e promovendo a separação clara de responsabilidades. Abaixo, apresentamos uma descrição detalhada de cada diretório e seus arquivos:

```
uninoticia/
├── local/
│   ├── dao/
│   │   └── PostDao.kt               ← Interface com métodos de acesso ao banco de dados local (Room)
│   └── database/
│       └── AppDatabase.kt          ← Classe que configura e instancia o banco de dados local
│
├── model/
│   └── Post.kt                     ← Data class que representa o modelo de uma notícia (Post)
│
├── network/
│   ├── ApiService.kt              ← Interface com os endpoints da API REST
│   └── RetrofitClient.kt          ← Objeto singleton que configura e fornece o Retrofit
│
├── repository/
│   └── PostRepository.kt          ← Camada que une dados da API e banco local, usada pelos ViewModels
│
├── viewmodel/
│   ├── PostViewModel.kt           ← ViewModel principal para gerenciar a lista de notícias (feed)
│   ├── PostViewModelFactory.kt    ← Factory para instanciar o PostViewModel com dependências
│   ├── PostDetailViewModel.kt     ← ViewModel para gerenciar os dados da tela de detalhe
│   └── PostDetailViewModelFactory.kt ← Factory para PostDetailViewModel
│
├── MainActivity.kt                ← Tela principal que exibe o feed de notícias
├── PostAdapter.kt                 ← Adaptador do RecyclerView que exibe os itens de notícia no feed
└── PostDetailActivity.kt         ← Tela de detalhes da notícia selecionada

```

----------

### 🔍 Explicação por Pacote

#### 📁 `local/`

-   **PostDao.kt**: Define operações como `insert`, `getAllPosts` e `getPostById` usando a biblioteca **Room**.
    
-   **AppDatabase.kt**: Responsável por criar e acessar a instância do banco de dados local do app.
    

#### 📁 `model/`

-   **Post.kt**: Classe de modelo que representa as informações de uma notícia. Utilizada em toda a aplicação, inclusive na API, banco de dados e UI.
    

#### 📁 `network/`

-   **ApiService.kt**: Define os endpoints da API, como `getPosts()`.
    
-   **RetrofitClient.kt**: Configura e fornece a instância de **Retrofit** usada para fazer chamadas HTTP à API.
    

#### 📁 `repository/`

-   **PostRepository.kt**: Camada intermediária entre as fontes de dados (API e banco) e a ViewModel. Implementa lógica como atualização de cache e fallback offline.
    

#### 📁 `viewmodel/`

-   **PostViewModel.kt**: Gerencia os dados exibidos no feed principal, buscando do repositório e expondo via `LiveData`.
    
-   **PostViewModelFactory.kt**: Permite a injeção do repositório na ViewModel de forma segura e modular.
    
-   **PostDetailViewModel.kt**: Responsável por carregar os detalhes de uma notícia específica.
    
-   **PostDetailViewModelFactory.kt**: Equivalente ao anterior, mas para a tela de detalhe.
    

#### 📄 `MainActivity.kt`

Tela inicial do app. Observa o `PostViewModel`, carrega o feed de notícias e aplica a lógica de navegação e busca.

#### 📄 `PostAdapter.kt`

Adaptador usado pelo `RecyclerView` para exibir os posts dinamicamente no feed, com imagens (carregadas via **Glide**).

#### 📄 `PostDetailActivity.kt`

Apresenta os dados completos de uma notícia (título, conteúdo, imagem, data e autor), com base na seleção feita na tela principal.
 

> rProjeto desenvolvido com foco em praticidade, fluidez e boa experiência para os estudantes da Unifucamp.
