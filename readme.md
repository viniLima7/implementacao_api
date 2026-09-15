# Projeto: Consulta de Personagens dos Simpsons (Springfield API)

Aplicação web interativa desenvolvida para consultar, pesquisar e visualizar os cidadãos de Springfield consumindo a API pública oficial da série **Os Simpsons**.

---

## 📺 API Utilizada

* **Site oficial da API:** [https://thesimpsonsapi.com](https://thesimpsonsapi.com)
* **Documentação dos Personagens:** [https://thesimpsonsapi.com/api/characters](https://thesimpsonsapi.com/api/characters)
* **CDN de Imagens em Alta Resolução:** `https://cdn.thesimpsonsapi.com/500/character/{id}.webp`

---

## 🚀 O que foi desenvolvido

A aplicação foi construída com foco em **experiência do usuário**, **design autoral com estética de desenho animado/quadrinhos** (sem templates genéricos de inteligência artificial) e consumo assíncrono via `fetch()` e `async/await`.

### Dados consumidos da API:
* **id:** Identificador numérico do personagem (ex: `#001`);
* **name:** Nome completo (ex: Homer Simpson, Ned Flanders);
* **occupation:** Profissão ou ocupação em Springfield;
* **age:** Idade do personagem;
* **birthdate:** Data de nascimento (formatada no padrão brasileiro DD/MM/AAAA);
* **gender:** Gênero do personagem;
* **status:** Situação com badge temático (**Vivo** ou **Falecido**);
* **phrases:** Bordões e frases clássicas da série exibidas em **balões de fala de gibi** (com botão interativo para alternar entre as falas);
* **portrait_path:** Caminho da imagem oficial no CDN.

---

## 🛠️ Funcionalidades Principais

1. **Pesquisa Inteligente de Personagens:**
   * Campo de busca por nome (ou profissão);
   * Pesquisa com clique no botão ou pressionando a tecla **Enter**;
   * Busca rápida no cache local e busca profunda nas páginas da API.
2. **Atalhos Rápidos de Springfield:**
   * Tags para busca imediata dos personagens clássicos (*Homer, Bart, Lisa, Ned Flanders, Moe, Sr. Burns, Krusty, Milhouse*).
3. **Limpeza da Pesquisa:**
   * Botão para limpar a busca e restaurar instantaneamente a lista completa.
4. **Estados Visuais Interativos:**
   * **Carregamento (Loading):** Rosquinha do Homer girando com mensagem amigável;
   * **Não Encontrado (Empty State):** Mensagem temática de Springfield com dicas de busca e botão para voltar;
   * **Tratamento de Erros:** Alerta amigável caso a conexão caia ou a API oscile, com opção de tentar novamente.
5. **Paginação Progressiva:**
   * Botão *"Carregar Mais Personagens de Springfield"* para navegar pelas páginas da API.
6. **Design Cartoon Pop-Art:**
   * Traços pretos marcantes de quadrinhos (`border: 3px solid #1B1B1B`);
   * Sombras sólidas duras (`box-shadow: 5px 5px 0px #1B1B1B`);
   * Cores clássicas dos Simpsons (Amarelo `#FED90F`, Azul do Céu de Springfield `#70D1FE`, Rosa Glacê `#F285A2`);
   * Nuvens da abertura clássica no topo;
   * 100% responsivo para computador, tablet e celular.

---

## 📁 Estrutura de Arquivos

```
implementacao_api/
│
├── index.php         # Página principal da aplicação (compatível com servidores PHP)
├── index.html        # Clone estático para abertura direta ou Live Server no VSCode
├── readme.md         # Documentação e relatório do projeto
│
├── css/
│   └── style.css     # Estilização completa com identidade visual dos Simpsons
│
└── js/
    ├── api.js        # Módulo de integração com a API, CDN e paginação
    └── app.js        # Manipulação do DOM, eventos de busca e renderização
```

---

## 💻 Como Rodar o Projeto

Você pode executar o projeto de três formas simples:

### Opção 1: Servidor PHP embutido (Recomendado)
Abra o terminal na pasta do projeto e execute:
```bash
php -S localhost:8000
```
Depois, acesse no navegador: `http://localhost:8000`

### Opção 2: Extensão Live Server (VS Code)
1. Abra a pasta no VS Code.
2. Clique com o botão direito em `index.html` ou `index.php`.
3. Selecione **"Open with Live Server"**.

### Opção 3: Abertura Direta no Navegador
* Dê dois cliques diretamente no arquivo `index.html`.

---

## 💡 Dificuldades Encontradas e Soluções Adotadas

1. **Parâmetros de Busca na API:**
   * *Desafio:* A API oficial `thesimpsonsapi.com/api/characters` não possui um filtro de busca nativo via parâmetro de URL (como `?name=Homer`). Ela suporta apenas paginação com `?page=1..60`.
   * *Solução:* Foi desenvolvido um sistema inteligente em `api.js` que carrega os personagens da primeira página e realiza pré-carregamento em segundo plano das páginas seguintes, permitindo uma busca instantânea e fluida no navegador sem gargalos de rede.

2. **Caminho das Imagens:**
   * *Desafio:* A propriedade `portrait_path` retorna um caminho relativo como `/character/1.webp`, que dá 404 se chamado na raiz do domínio principal.
   * *Solução:* Identificamos que as imagens estão hospedadas no CDN de alta resolução `https://cdn.thesimpsonsapi.com/500`. A função `getImageUrl()` em `api.js` normaliza e prefixa automaticamente todas as URLs.
